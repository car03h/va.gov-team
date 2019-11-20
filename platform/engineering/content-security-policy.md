# Content Security Policy 

This document is an overview of how Va.gov implements, uses, and manages a content security policy. This document assumes you have an understanding of CSP, CSP directives and a high level understanding of Va.gov's infrastructure (specifically where the reverse proxy sits in the content delivery flow).

## Generation of CSP

There are two components of the CSP generated by Va.gov's reverse proxy. 

- **CSP HTTP headers**: `Content-Security-Policy-Report-Only` and `Content-Security-Policy` (currently not active) 
- **`nonce` header value and HTML attribute**: A unique value (nonce) is generated for each page visit. The nonce is added to the CSP header and to each occurence of the nonce attribute in the HTML document. The nonce is added to the HTML document with a simple string replacement of `CSP_NONCE`. 

## CSP logger 

Va.gov uses Sentry as its CSP logger. **Sentry CSP logs** for each environment: 
- [Production](http://sentry.vfs.va.gov/vets-gov/website-production/?query=is%3Aunresolved+logger%3Acsp)
- [Staging](http://sentry.vfs.va.gov/vets-gov/website-staging/?query=is%3Aunresolved+logger%3Acsp)

_Reports are throttled by the reverse proxy by setting the `report-url` in the CSP header for **only on a percentage** of visits._

## Configuration and maintenance 

The following applies when editing the CSP: 

- Updates to the CSP **must be approved** by the [front end review group](https://github.com/orgs/department-of-veterans-affairs/teams/frontend-review-group)
- Updates to the CSP must be tested on staging before releasing into production 
  - The only way to test the CSP is to add it to an environment and monitor the logger for violations 
- Updates to the CSP must be in pull requests without other changes to enable easy rollback 
- The updater is responsible for monitoring the CSP logger after changes are pushed into production
- The CSP should be backwards compatible to version 1.0 to ensure maximum coverage

CSP configurations:

- [report-url set percentage](https://github.com/department-of-veterans-affairs/devops/blob/626321758f9e6065db9aee2ebd7e10862f2612cd/ansible/roles/revproxy-configure/templates/nginx_revproxy.conf#L125)
- [nonce generation](https://github.com/department-of-veterans-affairs/devops/blob/0eb82373423c7f96ce131982196aa266c73089bc/ansible/deployment/config/revproxy-vagov/templates/nginx_revproxy.conf.j2#L322-L325)
- [Production CSP directives](https://github.com/department-of-veterans-affairs/devops/blob/626321758f9e6065db9aee2ebd7e10862f2612cd/ansible/deployment/config/revproxy-vagov/vars/content_security_policy_vagov-prod.yml)
- [Staging CSP directives](https://github.com/department-of-veterans-affairs/devops/blob/626321758f9e6065db9aee2ebd7e10862f2612cd/ansible/deployment/config/revproxy-vagov/vars/content_security_policy_vagov-staging.yml)

## Exempted third party scripts 

This is an overview of the third party managed scripts allowed to run on Va.gov.

|Name|Description| 
|---------------------|---|
|[Digital Analytics Program](https://github.com/digital-analytics-program/gov-wide-code)|Provides a JavaScript file for US federal agencies to link or embed in their websites to participate in the Digital Analytics Program.|
|[Forsee](https://github.com/department-of-veterans-affairs/va.gov-team/blob/d754c8638a21c442cdb56bd0147c4ed25884dddb/platform/analytics/foresee/foresee)|Survey tool that displays surveys via an <iframe>.|
|[Github User Content](https://github.com/department-of-veterans-affairs/vets-website/blob/master/src/applications/static-pages/renderHomepageBanner.js)|Hosts configuration file for the homepage banner.|
|[Google Analytics](https://github.com/department-of-veterans-affairs/va.gov-team/blob/3d5b5b5f2307eb10af1f2e04d2c1a00707a1cf25/platform/analytics/google-analytics/readme.md)|Web analytics platform.|
|[Google Maps (via Leafletjs)](https://leafletjs.com/)|Facility locator uses leaflet to annotate its map. This dependency leverages the Google maps js framework.|
|[Google Optimize](https://github.com/department-of-veterans-affairs/vets.gov-team/blob/9fd4d5da296a4570fd10e7a6643c8418020c97c0/Practice%20Areas/Insights/Analytics/optimize360/readme.md#optimize-360o)|An a/b testing + personalization tool.|
|Govdelivery|used to deliver messages to veterans.|
|[Mapbox](https://github.com/department-of-veterans-affairs/va.gov-team/blob/7a662d972fa9e571a222a4b8b13b929ca1795c7a/products/facilities/facility-locator/README.md#what-to-know-about-the-product)|A location / address tool used in the Facility Locator.|
|[Medallia](https://github.com/department-of-veterans-affairs/vets.gov-team/blob/1c9fbe5f9291dbc9d425bca5fb8dbe5274a486aa/Products/Education/GIBCT/readme.md)|Survey tool|
|[Uservoice](https://github.com/department-of-veterans-affairs/va.gov-team/search?q=user+voice&unscoped_q=user+voice)|Survey tool|
|[YouTube](https://github.com/department-of-veterans-affairs/vets.gov-team/blob/1c9fbe5f9291dbc9d425bca5fb8dbe5274a486aa/Products/Education/GIBCT/readme.md)|Embedded video used on "Know Before You Go" video on GI Bill Comparison Tool.|

## Related info 
- [Strict csp](https://csp.withgoogle.com/docs/strict-csp.html)
- [CSP directives](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)
- [Locking down your website scripts with csp hashes, nonces, and report-uri](https://www.troyhunt.com/locking-down-your-website-scripts-with-csp-hashes-nonces-and-report-uri/)