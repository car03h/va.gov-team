# Product development checklist

### Ask yourself the questions below weekly, starting from Day 1.

You won't have answers right away, but should develope your answers iteratively over the lifetime of your product. This checklist is here to help you meet VA's required standards. Each item must be completed and ok'd by Platform, so check in with us early and often to avoid encountering roadblocks which could delay launch.

_Note: step-by-step processes for some items in this list may be under construction, so as always, use the **#vfs-platform-support** Slack channel whenever you have a question on how to proceed!_

---

# Step 1 

Make a copy of the checklist below and store it in the appropriate [product folder](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products) and get ready to check in with Platform regularly to make sure you're on track across all areas and have the support you need to succeed.

---

# Step 2

Ask yourself the following questions weekly and update the checklist with your progress.

## Is my product...

### ...usable (for ALL users)?

- [ ] Talk to and test with users and back-of-house VA employees at multiple intervals
- [ ] Keep a [Product Outline](https://github.com/department-of-veterans-affairs/va.gov-team/blob/34add7c7b3d558158ccf3f599e79c2380076481c/platform/product-management/product-outline-template.md) updated as you learn more and further define your solution
- [ ] Make everything [508 Accessible](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/platform/accessibility/508-request-prelaunch-review.md) and resolve any Sev1 accessibility issues
- [ ] Use plain language to [write your product content](https://design.va.gov/content-style-guide/)
- [ ] Use our [Design System](https://design.va.gov/) to mock up, build, and iterate on ideas
- [ ] Create and document [downtime notification rules and appropriate error messaging](https://design.va.gov/patterns/messaging-error-messages)
- [ ] [Do end-to-end QA](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/platform/quality-assurance/README.md) (including back-of-house people and systems) and resolve Sev1 bugs
- [ ] Do end-to-end UAT in production (including back-of-house people and systems) and fix Sev1 bugs
- [ ] Creat end-to-end tests, running in CI/CD, that pass on all browsers

### ...findable?

- [ ] Create URL and navigation per the user mental model
- [ ] Bake SEO into everything
- [ ] Create static entrance content
- [ ] Cross link as necessary from other locations per the user mental model

### ...compliant?

- [ ] [ATO check in](https://github.com/department-of-veterans-affairs/va.gov-vfs-teams/blob/master/Request-Reviews/request-ato-reviews.md)

### ...measurable?

- [ ] Define and track KPIs
- [ ] Update code with appropriate Google Analytics tagging
- [ ] [Release plan check in](https://github.com/department-of-veterans-affairs/va.gov-team/blob/97759a81a47c73da8bf03e35f3a13bb3c689d18b/platform/product-management/release-plan-template.md)
- [ ] Configure logging?
- [ ] Set up monitoring

### ...safe, reliable, and supportable?

- [ ] Make sure your product is secure
- [ ] Make sure users' private data is safe
- [ ] Document how to quickly respond when things go wrong (@gunsch) and what kinds of failure modes are likely
    - [ ]   Documentation and points of contact for any new backend dependencies
    - [ ]   Links to important dashboards for investigating relevant issues
- [ ] Determine contacts for on call support: who do we contact if the application is failing?
- [ ] Hit 90% code coverage requirement
- [ ] Load test your product
- [ ] Configure alerts (saturation, error rate, latency, availability)? and document POC for errors
- [ ] Set rate limits?

### ...marketable?
- [ ] Create Product brief with visuals, outlining the value and functionality of your product
- [ ] Update Product Outline with proposed next phase of features to build

## Here's what each practice area will be looking for during your check ins:
  - [Accessibility](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/platform/accessibility/508-request-prelaunch-review.md)
  - [Analytics]
  - [ATO](https://github.com/department-of-veterans-affairs/va.gov-vfs-teams/blob/master/Request-Reviews/request-ato-reviews.md)
  - [Content](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/platform/content/content-review-process.md#how-to-request-content-review)
  - [Design](https://github.com/department-of-veterans-affairs/va.gov-vfs-teams/blob/master/Request-Reviews/request-design-qa.md)
  - [Information Architecture](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/platform/information-architecture/working-with-ia.md)
  - [Infrastructure / Production Readiness]
  - [Load testing]
  - [Privacy]
  - [Product]
  - [QA]
  - [Security]

# Step 3

Schedule a Go / No Go meeting With Platform, your PO, and other stakeholders whose sign-off you need in order to kick off your release plan. [Here's a template for a great go / no go meeting agenda](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/platform/product-management/go-no-go-meeting-template.md)

# Step 4

Report on your KPIs in Team of Teams:
- The KPIs you set
- Which #s you're hitting and missing
- What you're doing as a result
