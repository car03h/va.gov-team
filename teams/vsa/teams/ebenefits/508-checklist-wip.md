# 508 Checklist

This checklist is a work-in-progress. Currently, this is a rather high-level overview of general practices and considerations. Line items were pulled from various team sources and a few personal additions.

### Resources
* https://accessibility.18f.gov/	Good Overview/Reference
* [VSP 508 Best Practices](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/platform/accessibility/508-accessibility-best-practices.md)
* [Request a 508 Complaince Review](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/platform/accessibility/508-request-prelaunch-review.md)

### Section 508 Compliance
* Use headings appropriately & consistently
* Apply autofocus to initial functional element on screen (This may change to focusing on this initial H1)
* Keep layout as simple and concise as possible to reduce tab-travel
* Keep functional groups together; avoid tabbing in and out of group (e.g. forms, navigation)
* Dynamic elements that reveal content (tooltips/alerts) must be keyboard accessible; allow screen readers to read dynamic content

### Vision
- [ ] Adhere to appropriate color combinations (maintain acceptable contrast)
- [ ] Accommodate browser zoom function to 400% with no scroll or reflow
- [ ] Ensure all elements are ‘colorblind visible’
- [ ] When displaying charts and diagrams, include visible or hidden tabular data
- [ ] Avoid CSS background images if image is meaningful (vs. decorative) or presented as content
- [ ] Avoid using color as the sole conveyance of information (e.g. red for error)
- [ ] Generally, text should be presented no smaller than 13px on-screen (guideline)

### Screen Readers
- [ ] Use HTML 5 semantic markup
- [ ] Use native HTML elements where possible (e.g. buttons and form elements)
- [ ] Use appropriate ALT tags for images
- [ ] Ensure FOR attributes exist for form inputs
- [ ] Accommodate UI state changes (e.g. sorted table)
- [ ] Use properly formed HTML tables for tabular data
- [ ] Ensure dynamic elements have proper ARIA tagging
- [ ] Ensure elements read on focus

### Motor/Keyboard
- [ ] Ensure all functional elements are keyboard accessible (minimum: tab/enter)
- [ ] Implement tab-trapping for modals and other imperative elements
- [ ] Include content skips for areas with large lightly-accessed elements (e.g. navigation)
- [ ] Ensure consistent, logical tab flow across screen; avoid trapped tabbing (ex. modals and other imperative content)
- [ ] Consider ‘target size’ of mouse-clickable elements

### 508 Review/Testing Procedures
* [Initial 508 Audit when code is stable](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/platform/accessibility/508-request-prelaunch-review.md)
* Final audit approx. four weeks out from release
* Post-release VA 508 Office review

### Tools
* Axe Chrome/Firefox Plugin (Mandatory)
* Colorblinding Chrome Plugin
* ChromeLens Chrome Plugin
* Color Contrast Analyzer for Sketch
* JAWS Screen Reader (Mandatory for IE 11; Requires License)
* NVDA Screen Reader
* Apple VoiceOver Screen Reader
* ES Lint VS Code Plugin
* Axe VS Code Plugin

18F lists quite a few more…
