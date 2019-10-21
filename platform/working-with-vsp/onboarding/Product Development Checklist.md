# Product development checklist

This list is here to help you more easily ensure your feature meets VA's required standards for design, UX, reliability, availability, and measurability in order to launch.

### Ask yourself these questions weekly, starting from Day 1.

You won't have answers right away, but starting early and checking in weekly helps you develop answers incrementally and iteratively over the lifetime of your product. In orderr to launch, each item in this list must be completed and ok'd by Platform, so check in with us early and often to avoid encountering roadblocks which could delay launch.

_Note: processes for some items in this list may be under construction, so as always, use the **#vfs-platform-support** Slack channel whenever you have a question about how to proceed! Hearing your questions also helps us know where the Platform processes and resources may be falling short, so over time so we can keep improving your experience._

---

Make a copy of this and store it in the appropriate [product folder](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products) so you can keep track of your progress from discovery through post-launch.


## Is my feature/product...

## User-friendly (for ALL users)?

- [ ] Talk to and test with (multiple times!) users, and VA employees providing the service
- [ ] Write a [Product Outline](https://github.com/department-of-veterans-affairs/va.gov-team/blob/34add7c7b3d558158ccf3f599e79c2380076481c/platform/product-management/product-outline-template.md) 
- [ ] Make everything [508 Accessibile](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/platform/accessibility/508-request-prelaunch-review.md) and check in with us for reviews
- [ ] Reach out for a [feature content check in](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/platform/content/content-review-process.md#how-to-request-content-review)
- [ ] Follow [Design best practices(), and [check in with us for reviews](https://github.com/department-of-veterans-affairs/va.gov-vfs-teams/blob/master/Request-Reviews/request-design-qa.md)
- [ ] Reach out for a [QA check in](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/platform/quality-assurance/README.md)
- [ ] Perform User Acceptance Testing
- [ ] Reach out for a Research check in

## Findable?

- [ ] Reach out for an [IA check in](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/platform/information-architecture/working-with-ia.md)
- [ ] Reach out for a static content check in
- [ ] Reach out for an SEO and cross-linking check-in

## Compliant?

- [ ] [ATO check in](https://github.com/department-of-veterans-affairs/va.gov-vfs-teams/blob/master/Request-Reviews/request-ato-reviews.md)

## Measurable?
- [ ] Analytics / Product Health Report review: this process is under construction, Slack us in **#vfs-platform-support** to organically coordinate working through this requirement!
- [ ] [Release plan check in](https://github.com/department-of-veterans-affairs/va.gov-team/blob/97759a81a47c73da8bf03e35f3a13bb3c689d18b/platform/product-management/release-plan-template.md)

## Safe and reliable?
- [ ] Security review: this process is under construction, Slack us in **#vfs-platform-support** to organically coordinate working through this requirement!
- [ ] Privacy review: this process is under construction, Slack us in **#vfs-platform-support** to organically coordinate working through this requirement!
- [ ] Production readiness / infrastructure review
- [ ] Documentation for quickly addressing when things go wrong: this process is under construction, Slack us in **#vfs-platform-support** to organically coordinate working through this requirement!
- [ ]   Contacts for oncall support: who do we contact if the application is failing? What kinds of failure modes are likely?
    - [ ]   Documentation and points of contact for any new backend dependencies
    - [ ]   Links to important dashboards for investigating relevant issues
- [ ] No high-severity bugs present
- [ ] Testing requirements
    - [ ]   E2e tests, running in CI/CD, passing on all browsers
    - [ ]   Code coverage requirements
    - [ ]   Load testing
- [ ] Monitoring requirements
    - [ ]   Contact (mailing list? Slack channel?) for errors to be reported to
    - [ ]   Errors getting sent directly to team

~- [ ] Contact center(s) are prepared for this launch, with updated scripts/documentation as needed~
~- [ ] VA web comms team is aware of this launch and has accurate messaging~

- [ ] Tested in prod with VA back-of-house people and systems
- [ ] Entrance pages (i.e. supporting static content) in place
- [ ] Downtime UX and error messaging documentation complete
- [ ] "Learn and Improve" plan written: KPI measurements, analytics reporting, next phase of features to build


Usable?
508 audit complete, and issues documented
e2e manual testing complete, and bugs fixed
e2e automated testing complete and successful

Discoverable?
URL and nav are ready
SEO is set up
Any necessary redirects / crosslinks from other webpages are in place
Supporting static content is ready

Secure?
Internal VA.gov security audit completed
VA (WASA) security experts have reviewed

Reliable?
Load testing complete
Alerts configured (saturation, error rate, latency, availability)
Rate limits set
Downtime notification rules and messaging set

Trackable?
Analytics set up
Monitoring set up
Logging configured

Supportable?
Call centers are ready (Product Outline and Demo Video)
VA.gov Feedback Form support team is ready
Platform is prepared to disable via feature flag

Marketable?
Web comms team knows value propositions AND limitations for accurate messaging
Vets.gov and wider VA are aware of impending launch and main talking points (Product Launch Email)

Live?
Go/No-go complete and successful
Product launched!
