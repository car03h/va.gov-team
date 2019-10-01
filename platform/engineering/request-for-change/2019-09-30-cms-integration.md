# RFC: CMS Integration

- Date: _2019-09-30_
- Related Issue:

## Background
_Explain the current state of the feature._

### Metalsmith
Currently, `vets-website`'s build is managed by Metalsmith, a
plugin-based static site generator. We have a number of custom plugins
used to manipulate the static content in various ways. One such plugin
fetches the content from Drupal if we pass the `--pull-drupal` flag to
the build script or if the local cache isn't found. Another checks for
broken links.

This build script is run in a number of ways:
- The Jenkins pipeline for a normal build
- The Jenkins pipeline for a content-only build
- Locally, with `yarn build` or `yarn watch`

Separate, but related, we have a modified version of the Metalsmith
build for the preview server (`yarn preview`).

Having a Metalsmith build pipeline came from a time when
`vets-website` had a `content/` directory from which the static pages
were built. These days, however, all of the content comes from outside
`vets-website`.

### Content validation
As a part of the Metalsmith pipeline, we do some basic content
validation, such as broken link checking. In a separate step in the
Jenkins pipeline for the normal `vets-website` build, we do an
accessibility test, which runs the aXe checker on all pages listed in
the sitemap.

Whenever the accessibility check fails, the Jenkins build fails.

When broken links are discovered during a normal Jenkins build, we
send a Slack notification with a link to the build. If Jenkins was
building the production branch, the build will also fail, to prevent
broken links in production.

## Motivation
_Why do we want to change the current implementation? What problem(s)
does the change solve?_

During the Jenkins builds for branches, the build script fetches the
latest content from `vagov-content` and the CMS. This means that **two
subsequent builds on a branch with no changes to the code can have two
different results.** In fact, this happens _very_ frequently, because
the changed content in Drupal often introduces broken links.

The goal of this RFC is to separate the content build from the
`vets-website` Webpack build, so when `vets-website` pulls the content
to serve up, it's already been built and validated. If this RFC is
successful, **all the sources of build failures due to content issues
will be isolated to the content build and will not affect
`vets-website` builds or deploys.**

## Design
_Explain the proposed changes in enough detail so that a team member
with working knowledge of the project could implement the change
themselves. Bonus points if this is easily mappable to user stories or
specs._

I propose rearchitecting the `vets-website` build to separate the
content building into a process distinct from the website.

[Insert diagram here]

**Note:** Pulling the already-built content _can still_ have two
different results, much like the current state, but since the content
it's pulling will have already been validated, the likelihood of a
failure is drastically reduced.

### Changes
- `vets-website` will no longer build the content
  - **Possible exception:** We may need to update some things in the
    pre-built content such as references to the new cache-busted
    filenames for JS and CSS assets
  - **Possible exception:** It should still be responsible for building
    the React pages, which would need to have the surrounding markup
    come from the templates
- There will be a new repo for the content build process
  - This will include scripts and templates
- There will be a new Jenkins pipeline for building the content
  - And everything that goes with this
- There will be a (new?) S3 bucket which holds all the built content
  - We currently do this with the cache, so this isn't much of a
    deviation
- The preview server will live in the new content-building repo
- Sitemap accessibility tests will be done during the content build,
  not the `vets-website` build
- The `vets-website` Jenkins build will have the following changes
  - There will be no cache fallback
  - There will be no content caching
  - There will be no sitemap accessibility testing
  
### Serving React apps
`vets-website` should be responsible for making the pages where the
React apps live, but not responsible for building the header, footer,
and other surrounding markup. To make this possible, **I propose we
have the content build produce an empty React page which the
`vets-website` can copy into each place a React app lives.** The new
page would then be updated with references to the correct JavaScript
bundle and CSS files.

The empty React page would then be deleted or otherwise prevented from
being served to production.

### Beneficial side effects
- The `vets-website` build will be faster both locally and in Jenkins
  - Currently, performing transformations to the content accounts for
    about half of the time in `yarn build` / `yarn watch` when the
    cache is used
  - Pulling the content from Drupal currently takes upwards of a full
    minute
	- This is because Drupal has to parse the _massive_ GraphQL query,
      put together the result, and send back the ~3.7MB response
  - The sitemap accessibility tests will be performed in the content
    build
	- This may not actually speed up the Jenkins build since it's done
      in parallel with the normal e2e tests
- `vets-website` will be isolated from any changes to the way content
  is built
  - Example 1: Rather than querying for all the content at once, the
    build could query for only the _new_ content
  - Example 2: Whoever manages the content build in the future can
    decide to skip any pages with broken links, and `vets-website`
    won't be burdened with the complexity of that decision
	  
### How this would affect the CMS team
I _think_ the impact would be minimal. Rather than using the full
`vets-website` in their integration environment, they'd use the new
content building repo.

The CMS team can also trigger a content-only deploy from inside
Drupal. If this is done before the latest content build is finished,
the deploy may not have all the latest changes.

## Risks
_What are the risks of the proposed changes?_

- The current integration is _so_ complex; it would be easy to
  overlook something while implementing the changes

## Questions
- Who owns the content build repo?
  - The CMS team?
  - VSP?
- Who owns managing the content build Jenkins pipeline?
  - The same team that owns the repo?
- What triggers a content build?
  - Could be a daily job
  - Could be triggered manually from inside Jenkins or even Drupal

## Alternatives
_What other alternatives solutions were considered, why weren't they
chosen?_

### Keep on keeping on
We could change nothing.

The problem here is that `vets-website` deploys will be blocked for
non-`vets-website` issues. As we scale both the platform and usage of
the CMS, we'll have to coordinate with the CMS team and content
editors a _lot_ to resolve issues since it will affect VFS teams.

### Allow bad content
Where "bad content" is defined here as broken links and accessibility
issues in the content from CMS or the `vagov-content` repo.

The problem with this is the degraded experience for Veterans.

### Output HTML files directly from Drupal
I don't know what the level of complexity for this would be.

I'm not proposing this for now simply because there's nothing I can do
about it. From the `vets-website` perspective, pivoting from this
proposal of a separate content building repo to having Drupal output
HTMl files directly would be nominal.