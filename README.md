# Automated Accessibility Tester

**Status:** Candidate Project  
**Market Size:** $848M (2026) → ~$1B+ (2034) at 12% CAGR  
**Last Updated:** 2026-05-02

## Overview

An AI-native web accessibility testing and remediation platform that moves beyond detection to **automatic code-level fixes**. Today's tools (axe-core, Pa11y, WAVE) excel at flagging violations but leave remediation to developers. This project generates actual, deployable code patches:

- **Automated fix generation:** Generate HTML/ARIA/CSS patches for violations, not just detection
- **Crossing the 57% ceiling:** LLMs can evaluate cognitive accessibility, reading clarity, and ARIA semantics in context—areas where rule engines fail
- **Intelligent prioritization:** Rank violations by user-impact severity; group related issues; suggest remediation roadmap by business priority
- **Dynamic SPA-aware scanning:** Test React, Vue, Angular single-page apps with runtime-aware component analysis

## The Market Gap

The accessibility testing market is growing at 12% CAGR. Market drivers include:

- **ADA Title II ruling (April 2024):** Public entities must comply with WCAG 2.1 AA by April 2026 (large) or April 2027 (small)
- **EU Accessibility Act (June 2025):** Mandates accessibility for private-sector digital products across EU
- **Section 508 / WCAG updates:** Compliance requirements increasingly codified as law

**But all existing tools share a critical limitation:**
- **Automated detection ceiling:** Rule-based engines (axe-core, Pa11y) detect only 25–57% of WCAG violations
- **No fix generation:** Tools flag issues but leave remediation to developers (manual, slow, error-prone)
- **Overlay stigma:** JavaScript overlays (accessiBe, UserWay) are actively opposed by disability advocates and facing FTC enforcement
- **Unserved segment:** No open-source tool offers AI-driven automatic remediation

## Core Features

### MVP (Must-Have)
- Automated scanning engine built on or compatible with axe-core (MPL-2.0), covering WCAG 2.1 AA and 2.2 A/AA rules
- Playwright and Cypress integration for CI/CD pipeline use; JSON output
- Severity-ranked violation report with human-readable descriptions and WCAG success criterion references
- SPA/dynamic-content support via controlled browser automation (post-hydration DOM testing)
- **AI-generated, context-aware code fix suggestions** for at least the top 10 most common violation types (missing alt text, form labels, heading hierarchy, language attribute, button names, link text, colour contrast flags)

### Should-Have (v1.1)
- **Natural-language explanation layer:** For each violation, generate plain-English description of the problem and its user impact
- **Violation prioritisation and grouping:** Cluster related issues; rank by impact across user disability personas; generate suggested remediation sequence
- Monitoring mode: scheduled scans with trend reporting and regression alerting
- WCAG criteria coverage reporting: tell users what percentage of WCAG 2.2 the tool covers vs. what requires human review

### Nice-to-Have (Backlog)
- LLM-powered assessment of previously manual criteria: reading level (3.1.5), focus-order logic (2.4.3), ARIA semantics in context
- IDE extension (VS Code) for shift-left detection during authoring
- Remediation dashboard with issue lifecycle tracking (open, in-progress, resolved, verified)
- Export formats for legal/audit use: VPAT-compatible output, accessibility conformance report generation

## AI-Native Opportunities

1. **Fix generation, not just detection**
   - Current tools flag issues but leave remediation to developers
   - An LLM could generate specific, context-aware code patches: corrected HTML/ARIA attributes, alt text from image context, focus management scripts
   - 2026 arXiv preprint (López et al.) demonstrates this is feasible with LLMs on real Angular SPAs

2. **Crossing the 57% automated detection ceiling**
   - Rule-based engines cannot assess cognitive load, reading-level clarity, or screen-reader UX flow
   - LLMs that understand natural language and page semantics can evaluate criteria previously requiring human testers
   - Examples: WCAG 3.1 (language/labels/instructions), 2.4.3 (focus order logic), meaningful ARIA usage in context

3. **Intelligent prioritization and triage**
   - Existing scanners produce large, undifferentiated lists of violations
   - An AI layer could rank issues by user-impact severity, group related violations, map them to personas (low-vision, motor-impaired, cognitive), and generate remediation roadmap ordered by business priority

4. **Dynamic / SPA-aware scanning**
   - Most scanners still struggle with React, Vue, Angular where content is rendered dynamically post-hydration
   - An AI agent understanding component trees and interaction patterns could test accessibility in a runtime-aware manner

5. **Open-source differentiation vs. overlays**
   - Existing open-source tools (axe-core, Pa11y) provide detection infrastructure but no AI layer
   - A free, open-source AI-native tester that generates real remediation code aligns with how developers actually want to work—unlike the opaque JavaScript overlays sold by commercial vendors (which disability advocates actively oppose)

## Competitive Landscape

| Tool | Type | Detects % WCAG | Fix Generation | Cost | Approach |
|------|------|---------------|----------------|------|----------|
| **axe-core** | OSS engine | 57% | ❌ | Free | Rule-based |
| **Pa11y** | OSS CLI | 30–40% | ❌ | Free | Rule-based |
| **WAVE** | Free extension | ~40% | ❌ | Free | Rule-based |
| **axe DevTools** | Commercial | 57% | ❌ | $10K–$50K/yr | Rule-based |
| **Siteimprove** | Commercial SaaS | ~60% | ✓ (AI Q&A) | $10K–$30K/yr | AI-assisted |
| **accessiBe** | Overlay (FTC banned) | ~50% | ✗ (overlay, not fixes) | $49–$199/mo | JavaScript overlay |
| **This Project** | OSS + SaaS | 57%+ → 80%+ | ✓ (AI-generated) | Free self-hosted | AI-native fix generation |

## Technical Design Considerations

- **Detection:** Build on axe-core (MPL-2.0); add LLM-based assessment for manual criteria
- **Fix generation:** Claude API for generating context-aware HTML/ARIA/CSS patches; integrate into code review workflows
- **SPA testing:** Playwright or Cypress for post-hydration DOM analysis; wait-for-stable-DOM heuristics
- **Prioritization:** Severity scoring based on WCAG success criterion weight + estimated user impact
- **CI/CD:** GitHub Actions / GitLab CI native integration; PR comments with fix suggestions
- **Explanation:** Plain-English descriptions of each violation; reference to WCAG success criteria; suggested user impact

## Market Validation

- **Market drivers:**
  - ADA compliance deadline (April 2026–2027) creates immediate demand
  - EU Accessibility Act enforcement (June 2025+) expanding compliance scope globally
  - 4,000+/year US web accessibility lawsuits (2024 data) — companies actively seeking proactive solutions
  - Disability advocates' FTC victory against accessiBe (April 2025) discrediting overlay approach

- **Customer personas:**
  - Enterprise development teams at regulated orgs (finance, government, healthcare)
  - Digital accessibility officers / compliance counsel facing April 2026/2027 deadlines
  - Web agencies and freelancers building accessible sites for clients
  - E-commerce and SaaS companies facing ADA litigation risk

## Why Build This

1. **Market timing:** ADA Title II deadline (April 2026–2027) creates immediate compliance pressure; EU EAA enforcement starting 2025
2. **Technology maturity:** LLM-based accessibility remediation papers (2025–2026) demonstrate feasibility; not speculative
3. **Open-source gap:** axe-core provides detection; no open-source AI layer for fix generation or prioritization
4. **Regulatory advantage:** FTC's accessiBe enforcement (April 2025) discredits overlay approach, creating demand for legitimate remediation tools
5. **Accessibility ethics:** Aligns with W3C WAI advocacy for source-code fixes over JavaScript overlays

## Success Metrics

- **Adoption:** 500+ GitHub stars within 12 months; featured as alternative to Siteimprove/axe DevTools
- **Compliance:** Help 50+ organisations meet April 2026/2027 ADA/EAA deadlines
- **Fix quality:** Generate deployable patches for 80%+ of top 10 violation types; user-tested patch accuracy >90%
- **Community:** Active issue triage; 2+ contributors beyond core team

---

**Resources:**
- [WCAG 2.2 Specification](https://www.w3.org/WAI/WCAG22/quickref/)
- [axe DevTools Documentation](https://www.deque.com/axe/devtools/)
- [WebAIM Million Report 2024](https://webaim.org/projects/million/2024/)
- [ADA Title II April 2026 Ruling](https://www.ada.gov/)
- [W3C WAI Evaluation Tools](https://www.w3.org/WAI/test-evaluate/tools/list/)
