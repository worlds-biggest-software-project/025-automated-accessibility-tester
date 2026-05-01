# Automated Accessibility Tester

> Candidate #25 · Researched: 2026-05-01

## Existing Products and Software Packages

| Tool | Type | Description | Open Source / Commercial | Pricing |
|---|---|---|---|---|
| **axe-core** | Engine/library | The de-facto standard accessibility testing engine by Deque Systems, covering WCAG 2.0/2.1/2.2 A/AA/AAA rules. Zero false-positive guarantee. Detects ~57% of WCAG issues automatically. | Open source (MPL-2.0) | Free |
| **axe DevTools** | Commercial suite | Full-featured browser extension, CI/CD integrations, guided manual tests, and monitoring built on top of axe-core. Targets enterprise dev teams. | Commercial | Quote-based; typically $10K–$50K/yr |
| **Deque WorldSpace Attest** | Enterprise platform | Server-side scanning, accessibility management dashboards, remediation tracking, integrates into SDLC pipelines. | Commercial | Enterprise quote |
| **Siteimprove Accessibility** | SaaS platform | All-in-one platform combining accessibility monitoring with SEO, content quality, and analytics. Continuous crawler-based scanning. | Commercial | Quote-based; mid-market ~$10K–$30K/yr |
| **AudioEye** | Hybrid SaaS | Combines automated JavaScript overlay with human expert remediation. Claims to cover ~50% of WCAG issues automatically, rest via expert review. | Commercial | Starts ~$199/month |
| **accessiBe** | Overlay SaaS | AI-powered JavaScript overlay claiming automated WCAG compliance. Widely criticized by disability advocates for not fixing underlying code and failing real assistive technology users. | Commercial | $49–$199/month per site |
| **UserWay** | Overlay SaaS | Similar overlay approach to accessiBe; acquired by LevelAccess in 2023, giving it access to professional services. | Commercial | $49–$199/month per site |
| **Pa11y** | CLI/library | Open source Node.js command-line tool and API built on HTML_CodeSniffer. Good for CI integration; less comprehensive than axe-core. | Open source (MIT) | Free |
| **Lighthouse (Google)** | CLI/DevTools | Built into Chrome DevTools and CI pipelines; includes an accessibility audit powered by axe-core. Widely used but surface-level. | Open source | Free |
| **WAVE (WebAIM)** | Browser extension / API | Visual in-page overlay showing accessibility errors and warnings. Good for manual review; paid API for automated scanning. | Free extension; Commercial API | API: $4–$40/month depending on volume |

**Strengths of leading open source tools:** axe-core's rule library is continuously updated, free to use, and integrates with Cypress, Playwright, Selenium, and all major CI/CD platforms.

**Key weakness across the board:** Automated tools — including the most advanced AI-assisted ones — detect only 25–57% of WCAG violations. Low-contrast text is the single most pervasive issue (found on 81% of the top million home pages per WebAIM 2024 study), yet contextual, cognitive, and interaction-pattern failures still require human review with real assistive technologies.

## Relevant Industry Standards or Protocols

- **WCAG 2.1 (W3C, 2018)** — The current compliance baseline for ADA, Section 508, and EU EAA; defines A, AA, and AAA success criteria across Perceivable, Operable, Understandable, Robust principles.
- **WCAG 2.2 (W3C, 2023)** — Adds 9 new success criteria; increasingly adopted as the design target for new products; axe-core 4.5+ includes WCAG 2.2 rules.
- **WCAG 3.0 (W3C Working Draft, March 2026)** — Introduces scoring-based conformance (replacing binary pass/fail), broader technology coverage, and new outcome categories. Not yet a formal recommendation; not a compliance target.
- **Section 508 (U.S. Rehabilitation Act)** — Requires federal agencies and their contractors to make ICT accessible to WCAG 2.0 AA; DHS Trusted Tester 5.1.3 updated in 2025–2026.
- **ADA Title II (DOJ ruling, April 2024)** — Requires public entities (state and local government) to comply with WCAG 2.1 AA by April 2026 (large) or April 2027 (small).
- **EU Accessibility Act (EAA, effective June 2025)** — Mandates accessibility for private-sector digital products and services across EU member states; references EN 301 549 which incorporates WCAG 2.1 AA.
- **ARIA (WAI-ARIA 1.2, W3C)** — Specifies roles, states, and properties for assistive technology interoperability; correct ARIA usage is testable and often flagged by scanners.
- **ISO 9241-171:2008** — Ergonomics of human-system interaction: guidance on software accessibility; used in procurement contexts.

## Available Research Materials

1. WebAIM (2024). *The WebAIM Million: The 2024 report on the accessibility of the top 1,000,000 home pages.* WebAIM. https://webaim.org/projects/million/2024 [Annual industry benchmark; not peer-reviewed]

2. WebAIM (2026). *The WebAIM Million: 2026 report.* WebAIM. https://webaim.org/projects/million/ [Updated annual benchmark]

3. Alonso, F. et al. (2025). *Coverage of web accessibility guidelines provided by automated checking tools.* Universal Access in the Information Society, Springer. https://link.springer.com/article/10.1007/s10209-025-01263-x [Peer-reviewed; documents the ~1/6 WCAG criteria coverage gap]

4. Sánchez-Gordón, M. et al. (2025). *Turning manual web accessibility success criteria into automatic: an LLM-based approach.* Universal Access in the Information Society, Springer. https://link.springer.com/article/10.1007/s10209-024-01108-z [Peer-reviewed; LLM-based automation of previously manual criteria]

5. López, G. et al. (2026). *Automated LLM-Based Accessibility Remediation: From Conventional Websites to Angular Single-Page Applications.* arXiv:2602.17887. https://arxiv.org/html/2602.17887 [Preprint; demonstrates modular LLM tool generating corrected HTML for WCAG 2.2 Level A violations]

6. Abou-Zahra, S. et al. (2024). *Policy in Practice: A Systematic Review of WCAG 2.2 and ADA 2024 Effects on Web and Mobile Accessibility.* ResearchGate. https://www.researchgate.net/publication/396366120 [Peer-reviewed systematic review]

7. Level Access (2026). *Automated Accessibility Testing: A Practical Guide to WCAG Coverage.* Level Access Blog. https://www.levelaccess.com/blog/automated-accessibility-testing-a-practical-guide-to-wcag-coverage/ [Industry white paper]

8. W3C WAI (2026). *Web Accessibility Evaluation Tools List.* W3C. https://www.w3.org/WAI/test-evaluate/tools/list/ [Official registry of 100+ evaluation tools]

## Market Research

**Market size:** The accessibility testing tools market was estimated at USD 848 million in 2026, growing at a CAGR of ~12% through 2033 (360 Research Reports). The broader digital accessibility software market is valued at USD 1.75 billion in 2026, growing at 8.6% CAGR to 2034 (Fortune Business Insights). Website accessibility software specifically is estimated at USD 613 million in 2026 growing at 6.9% CAGR to 2032 (360iResearch). Variation in figures reflects differing definitions of scope.

**Pricing landscape:**

| Tier | Example | Price |
|---|---|---|
| Free open source | axe-core, Pa11y, Lighthouse | Free |
| Overlay widgets | accessiBe, UserWay | $49–$199/month/site |
| Hybrid automated+human | AudioEye | $199+/month |
| Mid-market SaaS scanner | Siteimprove | ~$10K–$30K/yr |
| Enterprise platform | axe DevTools, LevelAccess | $30K–$100K+/yr |

**Key buyer personas:**
- **Enterprise development teams** at large regulated organizations (finance, government, healthcare) seeking CI/CD-integrated automated testing to catch issues before production.
- **Digital accessibility officers / compliance counsel** at Title II entities facing the April 2026/2027 DOJ deadline, needing audit trails and remediation tracking.
- **Web agencies and freelancers** building accessible sites for clients, needing per-site tools at low monthly cost.
- **E-commerce and SaaS companies** facing ADA litigation risk (U.S. web accessibility lawsuits exceeded 4,000/year in 2024) seeking proactive compliance tooling.

**Notable acquisitions/funding:**
- **UserWay acquired by LevelAccess (2023)** — consolidation of overlay and enterprise-grade testing.
- **Deque Systems** remains privately held, positioned as the technical authority; axe-core has 9M+ weekly npm downloads as of 2026.
- EU EAA enforcement beginning June 2025 is driving significant new demand from European enterprises previously underinvested in accessibility.

## AI-Native Opportunity

- **Fix generation, not just detection:** Current tools flag issues but leave remediation to developers. An AI-native tool could generate specific, context-aware code patches (corrected HTML/ARIA attributes, alt text, focus management) directly in the developer's codebase — moving from a scanner to an auto-remediation agent. The 2026 arXiv preprint (López et al.) demonstrates this is feasible with LLMs on real Angular SPAs.

- **Crossing the 57% automated detection ceiling:** Rule-based engines cannot assess cognitive load, reading level clarity, screen-reader UX flow, or whether ARIA usage is semantically meaningful in context. LLMs that understand natural language and page semantics can evaluate criteria previously requiring human testers — specifically WCAG success criteria related to language, labels, and instructions.

- **Intelligent prioritization and triage:** Existing scanners produce large, undifferentiated lists of violations. An AI layer could rank issues by user-impact severity, group related violations, map them to user personas (low-vision users, motor-impaired users, etc.), and generate a remediation roadmap ordered by business priority rather than technical occurrence.

- **Dynamic / SPA-aware scanning:** Most scanners still struggle with React, Vue, and Angular single-page applications where content is rendered dynamically post-hydration. An AI agent that understands component trees and interaction patterns could test accessibility in a more realistic, runtime-aware manner.

- **Open-source differentiation:** Existing open-source tools (axe-core, Pa11y) provide detection infrastructure but no AI layer. A free, open-source AI-native tester that generates real remediation code — rather than the opaque JavaScript overlays sold by commercial vendors (which disability advocates actively oppose) — fills a significant gap and aligns with how developers actually want to work.
