# Starter reference sources

These public sources were checked while drafting the workspace specification on 2026-10-12. They are starting points, not a fixed tool mandate. Recheck the current versions and technology-specific documentation at evaluation time, and preserve version/date with each cited practice.

## Standards and official tool documentation

| Topic | Source | How it informs the workflow |
|---|---|---|
| Web application security controls | [OWASP Application Security Verification Standard (ASVS)](https://owasp.org/www-project-application-security-verification-standard/) | Use versioned requirements as a security assessment checklist; the project page identifies ASVS 5.0.0 as the latest stable version at the time checked. |
| Web accessibility | [W3C Web Accessibility Initiative — WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/) | WCAG success criteria are testable requirements; the WAI page recommends the latest WCAG 2 version, currently 2.2. State the target and manual/automated coverage. |
| Browser test assertions | [Playwright — Assertions](https://playwright.dev/docs/test-assertions) | Prefer web-specific auto-retrying assertions for asynchronous UI rather than fragile immediate checks; cite applicable guidance when evaluating candidate tests. |
| Web quality and performance audits | [Chrome for Developers — Lighthouse overview](https://developer.chrome.com/docs/lighthouse/overview/) | Lighthouse provides automated page audits across performance, accessibility, SEO, and other quality areas; use consistent environment and retain raw results. |
| Static analysis/security checks | [Semgrep documentation](https://semgrep.dev/docs/) | A language-aware analyzer can find bugs and security patterns; findings need triage and verification rather than blind acceptance. |

## Production repository research

The candidate stacks are not known until submissions are added, so a single set of exemplar repositories would be premature and could bias the comparison. During each run, select a small number of maintained, production-grade repositories that use the candidate's actual framework/toolchain and demonstrate the particular practice being assessed.

For every repository cited, record its URL, license, last meaningful maintenance/release signal, relevant file or documented pattern, and date accessed. Confirm the source is a relevant example; do not present it as an official standard, use stars/popularity as a quality score, or copy code. If no credible matching repository is found, state that and rely on official documentation.

## Citation and verification rules

- Cite the exact documentation page/section and version or release when available.
- Distinguish normative official guidance from illustrative open-source practice.
- Record the date accessed and check that the source still exists and applies to the candidate's installed version.
- Do not claim that a tool proves correctness, security, WCAG conformance, or performance beyond its documented scope.
- If web access is unavailable, disclose the limitation and leave current-practice claims unverified.
