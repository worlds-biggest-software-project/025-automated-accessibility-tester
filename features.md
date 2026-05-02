# Automated Accessibility Tester — Feature & Functionality Survey

> Candidate #25 · Researched: 2026-05-02

## Solutions Analysed

| Tool | Type | Licence / Model | URL |
|------|------|-----------------|-----|
| axe-core | Open-source engine/library | MPL-2.0 (open source) | https://github.com/dequelabs/axe-core |
| axe DevTools | Commercial suite (built on axe-core) | Commercial / quote-based | https://www.deque.com/axe/devtools/ |
| Siteimprove Accessibility | SaaS platform | Commercial / quote-based | https://www.siteimprove.com |
| AudioEye | Hybrid SaaS (overlay + human review) | Commercial / from $199/month | https://www.audioeye.com |
| accessiBe | Overlay SaaS | Commercial / $49–$199/month | https://accessibe.com |
| UserWay | Overlay SaaS (now under LevelAccess) | Commercial / $49–$199/month | https://userway.org |
| Pa11y | CLI / Node.js library | MIT (open source) | https://pa11y.org |
| Google Lighthouse | CLI / DevTools | Apache 2.0 (open source) | https://developer.chrome.com/docs/lighthouse/ |
| WAVE (WebAIM) | Browser extension + commercial API | Free extension; commercial API | https://wave.webaim.org |

---

## Feature Analysis by Solution

### axe-core

**Core features**
- Tests HTML-based interfaces against WCAG 2.0, 2.1, and 2.2 at A, AA, and AAA levels
- Detects approximately 57% of WCAG violations automatically with a published zero-false-positive guarantee
- Returns "incomplete" results for items requiring human review rather than suppressing them
- Integrates natively with Playwright, Cypress, Selenium, Puppeteer, and Jest
- Conforms to W3C Accessibility Conformance Testing (ACT) rules
- Available as a JavaScript library (browser and Node.js), CLI, and VS Code linter (axe Linter)
- New minor release every 3–5 months; WCAG 2.2 rules added in v4.5+

**Differentiating features**
- De-facto standard engine: over 9 million weekly npm downloads as of 2026; embedded in Lighthouse, Playwright's accessibility utilities, and dozens of third-party tools
- Only major open-source engine with an explicit, enforced zero-false-positive design goal
- ACT rule conformance allows results to be independently validated and compared across tools

**UX patterns**
- Used primarily as a programmatic API within existing test suites; no standalone UI
- Results returned as structured JSON with rule ID, impact level (critical/serious/moderate/minor), and failing element selectors
- axe Linter surfaces violations in the IDE editor as inline diagnostics before runtime

**Integration points**
- npm package for Node.js and browser environments
- Official integrations with Playwright (`@axe-core/playwright`), Cypress (`cypress-axe`), Selenium WebDriver (`axe-core/webdriverjs`)
- Embeds in GitHub Actions, Jenkins, CircleCI via CLI wrappers
- Rules library is the engine behind Google Lighthouse accessibility audits

**Known gaps**
- Cannot evaluate cognitive accessibility, reading-level clarity, or meaningful use of ARIA in context (those require human testers)
- No built-in monitoring or dashboard — pure detection library
- Dynamic SPA content rendered after hydration may not be fully captured without explicit test-time waits
- No remediation suggestions — reports violations but not fixes

**Licence / IP notes**
- MPL-2.0: file-level copyleft; modifications to axe-core files must be made available, but proprietary code calling the library is not affected. A Snyk-flagged MPL-2.0 licence notice appeared on v4.7.0; no patent encumbrance has been confirmed in public issue discussion. No patent claims are known to exist on the axe-core ruleset itself.

---

### axe DevTools (Deque commercial suite)

**Core features**
- Browser extension providing in-page visual highlighting of accessibility violations during development
- axe DevTools Linter: 44 accessibility rules checked in CI/CD, with results posted directly to GitHub pull requests
- Intelligent Guided Tests (IGTs): step-by-step workflows guiding manual testers through issues not detectable by automation
- axe Monitor: continuous crawler-based monitoring and trend dashboards for production websites
- axe Auditor: WCAG audit workflow for comprehensive manual audits with evidence collection
- Native Android and iOS mobile accessibility testing modules
- CLI for no-code automated scanning within CI/CD pipelines

**Differentiating features**
- Only commercial product combining automated scanning, guided manual testing, mobile testing, and continuous monitoring in one integrated platform under a single vendor
- Blocks inaccessible code in GitHub pull requests before merge via linter integration
- Enterprise SLA, SSO, audit trail, and compliance reporting capabilities

**UX patterns**
- Developer-focused: embedded in Chrome DevTools panel; issues shown with in-page overlays and element highlights
- IGT workflows provide structured checklists for testers regardless of a11y experience level
- Dashboard provides remediation tracking with issue status over time

**Integration points**
- Playwright, Cypress, Selenium integration; GitHub/GitLab pull request checks
- JIRA and project management ticket creation from scan results
- REST API for programmatic access to scan results and issue management
- CI/CD platforms: GitHub Actions, Jenkins, CircleCI, Azure DevOps

**Known gaps**
- Quote-based pricing ($10K–$50K/yr) excludes small teams and freelancers
- Mobile testing requires separate module license
- No AI-generated code fix suggestions; still surfaces issues for developer remediation
- WCAG 3.0 support not yet available (as of April 2026)

**Licence / IP notes**
- Proprietary commercial licence; no source code available. Built on axe-core (MPL-2.0); commercial wrapper is fully proprietary.

---

### Siteimprove Accessibility

**Core features**
- Continuous crawler-based scanning of entire websites for WCAG 2.0, 2.1, and 2.2 A/AA issues
- Accessibility AI Assistant (launched August 2025): conversational AI within the page report allowing teams to ask questions about specific issues and receive contextual remediation guidance
- PDF accessibility checks including list structure detection (added October 2025)
- Compliance tab providing conformance summaries mapped to regulatory standards (ADA, EAA, Section 508)
- CMS plugin integrations (including Adobe Experience Manager as of October 2025)
- Platform-wide WCAG 2.2 AA improvements applied to Siteimprove's own UI (December 2025)
- Code Checker for development-time scanning within dev environments

**Differentiating features**
- Only platform in this space combining accessibility, SEO, content quality, and analytics in one SaaS product
- Recognised as a Forrester Wave Leader in Digital Accessibility Platforms, Q4 2025
- AI Assistant provides contextual explanation of issues and suggested fixes in natural language — the only tool in this segment with a conversational remediation interface at GA as of 2025

**UX patterns**
- Dashboard-first: manages accessibility health across a portfolio of pages with trend reporting
- Page Report drills down to individual violations with in-page visual reference
- Role-based views for developers, editors, and compliance officers

**Integration points**
- CMS plugins (WordPress, Drupal, Sitecore, AEM)
- Accessibility Code Checker integrates into developer IDE and CI
- API for pulling issue data into external reporting systems
- SSO/SAML for enterprise identity management

**Known gaps**
- Crawler cannot test pages behind authentication without configuration
- Limited JavaScript / SPA scanning depth compared to browser-extension-based tools
- AI Assistant is a Q&A explainer, not an automated code-fix generator
- No open-source components; vendor lock-in is high
- Pricing (~$10K–$30K/yr) makes it inaccessible to small agencies

**Licence / IP notes**
- Fully proprietary SaaS; no open-source components. No patent concerns identified in public sources.

---

### AudioEye

**Core features**
- JavaScript overlay automatically applied to the live site to attempt runtime WCAG fixes
- Claims approximately 50% of WCAG issues addressed automatically via the overlay
- Human accessibility expert review and remediation for issues the overlay cannot address
- AudioEye Ally toolbar: user-adjustable display preferences (text size, contrast, etc.)
- Legal support and certification documentation for ADA compliance defence
- Continuous automated monitoring with issue alerting

**Differentiating features**
- Hybrid model: automated overlay + certified human expert review combined in one subscription
- Provides legal compliance documentation and a published Certificate of Conformance

**UX patterns**
- No-code deployment: a single JavaScript snippet injected into the page
- Customer-facing accessibility toolbar visible to site visitors

**Integration points**
- JavaScript CDN snippet; no deep code integration
- CMS-specific plugins for WordPress, Shopify, Squarespace, Wix
- Reporting dashboard for issue tracking

**Known gaps**
- Overlay approach cannot modify source HTML; structural errors (missing semantic elements, incorrect ARIA roles, broken focus management) persist at the DOM level
- Research (Hounder, 2025) shows AudioEye customer sites still fail meaningful alt-text checks in 54% of cases despite the overlay
- Human remediation does not fix underlying source code — changes apply only at runtime via JavaScript
- Customers have faced ADA lawsuits despite using the service; the overlay does not guarantee legal compliance
- Disability advocates and 600+ accessibility professionals have published opposition statements to overlay approaches

**Licence / IP notes**
- Proprietary SaaS. FTC action finalised April 2025 against accessiBe (same overlay category) for deceptive WCAG compliance claims; AudioEye has not been subject to a comparable FTC order but faces the same category of criticism.

---

### accessiBe

**Core features**
- AI-powered JavaScript overlay claiming automated WCAG 2.1 compliance
- Two-component architecture: a foreground accessibility interface (toolbar) and a background AI process that scans and modifies the DOM at runtime
- Auto-applies ARIA labels, alt text descriptions via AI image recognition, keyboard navigation adjustments
- Accessibility Statement and Certification report generation

**Differentiating features**
- Entry-level pricing ($49–$199/month) making it the most accessible overlay for small businesses
- Claims 48-hour initial setup time

**UX patterns**
- Single snippet installation; no developer involvement after deployment
- User-facing widget toolbar for visitor customisation

**Integration points**
- JavaScript snippet; WordPress, Shopify, Wix plugins

**Known gaps**
- FTC finalised a $1 million order against accessiBe in April 2025 barring the company from claiming its automated products can make any website WCAG compliant
- Over 600 accessibility professionals signed a public statement that overlay solutions do not meet legal requirements and in many cases worsen accessibility for assistive technology users
- Cannot fix underlying source code; structural and semantic errors persist
- Real-world testing shows high failure rates for meaningful alt text and keyboard navigation on customer sites
- Widely recommended against by the W3C WAI and disability advocacy community

**Licence / IP notes**
- Proprietary SaaS. Subject to FTC enforcement order (April 2025). Reputational and legal risk to any project that incorporates or emulates this approach.

---

### UserWay

**Core features**
- JavaScript overlay with AI-assisted runtime WCAG adjustments
- User toolbar for display preference customisation
- Acquired by LevelAccess (2023), providing access to LevelAccess's professional manual audit services
- Accessibility monitoring and compliance documentation

**Differentiating features**
- Post-acquisition access to LevelAccess's expert manual audit network differentiates it from pure-overlay competitors

**UX patterns**
- Single snippet deployment; user-facing widget
- Enterprise dashboard for multi-site management

**Integration points**
- JavaScript snippet; CMS plugins (WordPress, Shopify, Wix, Drupal, Squarespace)

**Known gaps**
- Shares all fundamental technical limitations of JavaScript overlays (cannot fix source HTML)
- Research cited above shows user sites still fail alt-text and keyboard navigation checks at high rates
- Disability advocate opposition mirrors that directed at accessiBe
- Post-acquisition integration between UserWay overlay and LevelAccess expert services is still maturing

**Licence / IP notes**
- Proprietary SaaS. No patent encumbrance identified in public sources.

---

### Pa11y

**Core features**
- Node.js CLI and programmable API for automated accessibility scanning
- Tests against WCAG 2.0 and 2.1 (via HTML_CodeSniffer under the hood; can also be configured to use axe-core rules)
- pa11y-ci: CI-centric runner that accepts a list of URLs, processes sitemaps, and handles authenticated sessions
- Outputs results in JSON, CSV, and HTML formats
- Integrates with GitLab CI accessibility testing pipeline natively (GitLab Docs, 2025)
- 2025 improvements focused on better SPA and JavaScript-heavy page support

**Differentiating features**
- Entirely open source (MIT) with no commercial components; well-suited for budget-constrained teams and open-source projects
- Simpler configuration footprint than axe-core for basic bulk URL scanning

**UX patterns**
- Command-line first; steep learning curve for non-technical users
- No GUI or dashboard; outputs to terminal or files
- Limited documentation and community support compared to axe-core

**Integration points**
- npm package; GitHub Actions, GitLab CI, Jenkins via shell commands
- Can be pointed at any publicly accessible URL including authenticated pages (with cookie config)

**Known gaps**
- Detects only approximately 30–40% of WCAG criteria — less comprehensive than axe-core
- No remediation guidance: reports errors without explaining how to fix them
- Cannot assess meaningful alt text, cognitive clarity, or screen-reader UX
- No monitoring, trend tracking, or dashboard capabilities
- Community maintenance pace is slower than axe-core; some rules lag WCAG 2.2 coverage

**Licence / IP notes**
- MIT licence: maximally permissive; no patent concerns identified.

---

### Google Lighthouse

**Core features**
- Accessibility audit module is one of six audit categories (performance, accessibility, best practices, SEO, PWA)
- Accessibility rules powered by axe-core; surfaces a subset of axe findings in a UI-friendly report
- Integrated into Chrome DevTools (Lighthouse panel), Chrome DevTools command palette, and the `lighthouse` npm CLI
- Generates scored reports with per-issue documentation links
- Can be run in CI via `@lhci/cli` (Lighthouse CI)
- Covers WCAG 2.0/2.1 checks; limited WCAG 2.2 rule coverage compared to running axe-core directly

**Differentiating features**
- Zero friction for developers already using Chrome DevTools: no installation required for basic use
- Single audit runs performance, accessibility, SEO, and best-practices simultaneously — useful for general site health checks

**UX patterns**
- GUI report in browser DevTools with colour-coded pass/fail indicators and per-issue documentation
- CLI output as JSON or HTML report

**Integration points**
- Chrome DevTools (built-in); `lighthouse` npm CLI
- Lighthouse CI (`@lhci/cli`) for GitHub Actions, CircleCI, Jenkins integration
- PageSpeed Insights API (Google cloud-hosted version)

**Known gaps**
- Accessibility audit is a subset of axe-core; running axe-core directly provides more comprehensive results
- Not designed as a dedicated accessibility tool; coverage is surface-level for compliance purposes
- No monitoring, historical tracking, or remediation workflow
- Does not support authenticated pages or complex SPA interactions without additional scripting

**Licence / IP notes**
- Apache 2.0 licence: permissive; no patent concerns identified.

---

### WAVE (WebAIM)

**Core features**
- Injects visual icons and indicators directly onto the rendered page, showing errors, alerts, structural elements, and ARIA features in their visual context
- Browser extensions for Chrome, Firefox, and Edge (version 3.3.0.4, December 2025; aligned to WCAG 2.2)
- Navigation Order panel shows the keyboard/screen-reader traversal sequence through page elements
- Commercial Subscription API: GET request with API key returns results as JSON or XML; 100 free credits for new accounts, then per-credit pricing ($4–$40/month by volume)
- Stand-alone WAVE API: locally installed headless-Chrome engine for scanning intranet, authenticated, and private pages; integrates with Selenium and Puppeteer
- Sitewide scanning tools for multi-page or whole-site analysis

**Differentiating features**
- In-context visual overlay is uniquely intuitive for non-developer reviewers: issues are shown exactly where they appear on the rendered page
- Navigation Order panel is considered one of the most useful — and underused — keyboard accessibility diagnostic tools available in any free tool

**UX patterns**
- Browser extension: click toolbar button to activate overlay on current page; toggle categories (errors, alerts, structure, etc.)
- No project management, tracking, or CI integration in the free extension
- API is developer-facing; raw JSON/XML output requires post-processing

**Integration points**
- Subscription API: REST GET requests; JSON/XML output
- Stand-alone API: integrates with Selenium, Puppeteer, CI pipelines
- No native integrations with project management tools or IDEs

**Known gaps**
- No AI features or remediation suggestions
- API is rate-limited and credit-based; cost scales with volume
- Extension requires manual page-by-page review; not suitable for automated regression testing of large sites without the API
- Stand-alone API requires local installation; no cloud-hosted automated scanning service

**Licence / IP notes**
- Browser extension: free, no source licence published for public modification. Commercial API: proprietary SaaS. No patent concerns identified.

---

## Cross-Cutting Feature Themes

### Table-Stakes Features
- WCAG 2.1 AA scanning with documented rule coverage percentage
- Zero-false-positive or low-false-positive mode — actionable results without noise
- Integration with at least one major test framework (Playwright, Cypress, Selenium) and one CI/CD platform
- JSON/structured output for downstream processing and dashboards
- Per-violation severity classification (critical / serious / moderate / minor)
- Coverage of the top 5 most prevalent issue types: low contrast, missing alt text, missing form labels, empty links, missing page language

### Differentiating Features
- AI-generated code-level fix suggestions (currently absent from all tools reviewed)
- Conversational natural-language explanation of violations and remediation guidance (Siteimprove AI Assistant is the only current example, but it is a Q&A bot, not a fix generator)
- SPA/dynamic-content-aware scanning that tests post-hydration DOM states
- Intelligent prioritisation: grouping related violations, ranking by user-impact and persona (low-vision, motor-impaired, etc.), rather than flat occurrence lists
- Monitoring and trend dashboards for production accessibility regression detection

### Underserved Areas / Opportunities
- Automated code-patch generation — no tool currently generates deployable HTML/ARIA/CSS fixes
- Detection beyond the 57% ceiling: criteria involving cognitive load, reading level, meaningful ARIA usage, and screen-reader flow quality are universally manual
- Open-source AI-native tooling: the axe-core + Pa11y ecosystem provides strong detection infrastructure but zero AI layer
- Accessible SPA testing: most tools still struggle with React/Vue/Angular component trees and interaction patterns that require runtime-aware testing
- Overlay-free remediation for non-technical site owners: the overlay market exists because there is no accessible middle ground between "DIY developer tool" and "$30K enterprise platform"

### AI-Augmentation Candidates
- Alt text generation for images (already done by accessiBe/AudioEye via AI, but inaccurately; an LLM with vision capabilities could do this at source-code level)
- Reading-level and plain-language assessment of page content (WCAG 3.1.5)
- Meaningful ARIA label validation (distinguishing semantically correct vs. technically present labels)
- Prioritisation and remediation roadmap generation from a raw violation list
- Automated fix generation for structural issues: adding `<label>` associations, correcting heading hierarchy, inserting `lang` attributes

---

## Legal & IP Summary

All open-source tools reviewed (axe-core MPL-2.0, Pa11y MIT, Google Lighthouse Apache 2.0) are free of known patent encumbrances. The MPL-2.0 licence on axe-core is file-level copyleft: modifications to axe-core files must be disclosed, but proprietary applications that import and call the library are unaffected. No patent claims on the axe-core rule implementation have been identified in public sources. Commercial tools (Deque suite, Siteimprove, AudioEye, accessiBe, UserWay) are fully proprietary; incorporating their techniques or interfaces without a licence would constitute infringement. The most significant IP risk in this space is reputational: the FTC finalised a $1 million enforcement order against accessiBe in April 2025 for deceptive WCAG compliance claims, and 600+ accessibility professionals have publicly opposed overlay technology. Any product in this category must avoid claims of automated full WCAG compliance and must not adopt an overlay architecture.

---

## Recommended Feature Scope

**Must-have (MVP)**
- Automated scanning engine built on or compatible with axe-core (MPL-2.0), covering WCAG 2.1 AA and 2.2 A/AA rules
- Playwright and Cypress integration for CI/CD pipeline use; JSON output
- Severity-ranked violation report with human-readable descriptions and WCAG success criterion references
- SPA/dynamic-content support via controlled browser automation (post-hydration DOM testing)
- AI-generated, context-aware code fix suggestions for at least the top 10 most common violation types (missing alt text, form labels, heading hierarchy, language attribute, button names, link text, colour contrast flags)

**Should-have (v1.1)**
- Natural-language explanation layer: for each violation, generate a plain-English description of the problem and its user impact, addressable to a developer with no accessibility expertise
- Violation prioritisation and grouping: cluster related issues, rank by impact across user disability personas, generate a suggested remediation sequence
- Monitoring mode: scheduled scans with trend reporting and regression alerting
- WCAG criteria coverage reporting: tell users what percentage and which categories of WCAG 2.2 the tool covers vs. what requires human review

**Nice-to-have (backlog)**
- LLM-powered assessment of previously manual criteria: reading level (3.1.5), focus-order logic (2.4.3), ARIA semantics in context
- IDE extension (VS Code) for shift-left detection during authoring
- Remediation dashboard with issue lifecycle tracking (open, in-progress, resolved, verified)
- Export formats for legal/audit use: VPAT-compatible output, accessibility conformance report generation
