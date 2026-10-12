# Scoring rubric

## Score interpretation

Every dimension score is 0–100, where higher is better. Scores are not percentages of truth and should be accompanied by evidence, status, and confidence. Use the rubric anchors below consistently:

- **0**: confirmed complete failure against the dimension's defined scope.
- **1–39**: major deficiencies; core evidence fails or severe gaps are verified.
- **40–59**: partial; significant issues or important missing evidence.
- **60–79**: generally adequate; some notable gaps or defects remain.
- **80–94**: strong, with minor issues and good supporting evidence.
- **95–100**: exceptional against the defined scope, with unusually complete evidence. Do not award this merely because no issue was found.

When there is not enough evidence, use `not_evaluated`/`partially_evaluated` rather than assigning a zero. A confirmed critical defect may score zero in its dimension, but still provide the evidence and impact.

## Initial dimension weights

These proposed weights total 100. Confirm or adjust them before the first scored run; never tune them to favor a candidate.

| Dimension | Weight | What it measures |
|---|---:|---|
| Functionality against the brief | 24 | Weighted acceptance-criterion completion and core user journey success |
| Security and privacy | 15 | Verified security controls/findings, dependency/configuration risk, privacy exposure |
| Code correctness | 14 | Reproducible defects, static/type/build errors, runtime failures outside requirement checks |
| Test suite quality | 12 | Whether candidate tests are meaningful, reliable, maintainable, and effective at detecting defects |
| Accessibility | 8 | Automated checks plus manual keyboard/semantic review against the declared target |
| Performance | 7 | Repeated, controlled page and interaction measurements |
| Best practices | 7 | Fit with current official technology guidance and justified industry patterns |
| Robustness and portability | 6 | Reproducible install/build/start, failure handling, and verified OS/browser compatibility |
| Maintainability and modularity | 4 | Cohesion, separation of concerns, understandable structure, changeability |
| User experience and visual fidelity | 3 | Clarity, consistency, responsive behavior, and alignment with brief/reference |

If a dimension does not apply, explain why before scoring and redistribute its weight proportionally among remaining applicable dimensions before evaluation. Document the adjusted weights and preserve their sum as 100. Prefer a new rubric version over silently omitting a dimension.

## Dimension measurement and evidence

### 1. Functionality against the brief — 24

Create a traceability table for every stable requirement ID in `benchmark/PRODUCT_SPEC.md`. Assign requirement weights before running candidates: Critical 5, High 3, Normal 2, Low 1 (or explicit numeric values agreed before the run).

For each requirement classify shared black-box acceptance evidence as `pass` (1), `partial` (0.5), `fail` (0), or `not_testable` (exclude from denominator with explanation). Then compute:

`functionality_score = 100 * sum(requirement_weight * result_value) / sum(testable_requirement_weights)`

Additionally report critical-requirement pass rate and each primary-journey pass/fail. This arithmetic is a baseline; do not let a high average hide failed critical flows. Manual review can clarify acceptance evidence but cannot quietly change a requirement's meaning.

### 2. Security and privacy — 15

Use layered evidence: source/configuration review, dependency and secret scanning, and scoped dynamic tests against synthetic data in isolation. Compare applicable controls to a pinned OWASP ASVS version and product-specific threat assumptions. Consider injection, authentication/authorization where applicable, unsafe rendering, sensitive data exposure, secret handling, transport/storage, dependency risk, and unsafe defaults.

- Report verified vulnerabilities by severity and confidence, with reproduction/evidence and affected path/lines where safe.
- Separate exploitable findings from scanner alerts, false positives, and unverified concerns.
- A clean scan is not proof of security. AI opinion alone is not a finding or a clean bill of health.
- Any confirmed Critical or High security issue triggers the security eligibility gate (below).
- Use only synthetic inputs; do not probe external systems or access real user data.

Provide the 0–100 score with a concise method-specific scale: start at 100, subtract 40 per confirmed Critical, 25 per High, 12 per Medium, and 4 per Low finding, capped at 100 total deductions. Weight findings by exploitability and scope when evidence justifies it; document any adjusted deduction. Do not deduct for unverified scanner noise as if it were confirmed.

### 3. Code correctness — 14

Report clean install/build/typecheck/lint outcomes where supported; runtime errors; reproducible bugs; and defects not already fully captured by requirement-level functionality tests. Classify defect severity and reproducibility. Use representative static analysis appropriate to each candidate's stack.

Do not count the same symptom repeatedly across functionality and correctness without explaining the distinction. Candidate-specific clean build/typecheck is useful but does not prove runtime correctness.

### 4. Test suite quality — 12

Inspect tests and run them in isolation. Score these subcriteria (0–100 each, equally weighted unless reweighted before the run):

- **Behavior and risk coverage (30%)**: coverage of critical user flows, boundary/error cases, and security-sensitive behavior; map test names to requirement IDs.
- **Assertion quality (25%)**: verifies observable outcomes and state, not merely rendering/execution or implementation details.
- **Reliability and diagnostic value (20%)**: deterministic, independent, useful failure output, no unnecessary timing dependence or skipped/disabled tests.
- **Effectiveness (25%)**: mutation testing or carefully seeded representative fault tests where appropriate; report test count, mutations attempted/killed/survived, and limitations.

`test_quality_score = 0.30*behavior + 0.25*assertions + 0.20*reliability + 0.25*effectiveness`.

Use line/branch coverage only as supporting context, not as a stand-alone quality score. A test that passes while the behavior is broken is not effective. Do not create mutations that escape the isolation controls.

### 5. Accessibility — 8

Run the same automated accessibility checker against equivalent states/viewports, preferably axe-core or an equivalent tool, and manually verify key keyboard-only flows, focus order/visibility, labels/names, semantics, and contrast issues. Map findings to the declared WCAG target and success criteria. Automated scans cannot prove conformance; report manual coverage and limitations. Avoid counting one underlying defect multiple times.

### 6. Performance — 7

Run the same browser/tool build, viewport, network profile, synthetic data, and warm/cold-start policy. Use Lighthouse or equivalent and focused interaction timings. Record at least three independent runs when feasible; report median and range/raw values. Treat Lighthouse category values and Core Web Vitals as observed indicators, not universal guarantees. If candidates use materially different hosting/deployment setups, disclose the difference and avoid false precision.

### 7. Best practices — 7

Assess the practices relevant to each candidate's actual stack, not a single preferred language or framework. For each consequential recommendation cite:

1. current official documentation, standard, or vendor guidance (normative reference);
2. where useful, a maintained production-grade repository demonstrating a comparable pattern (illustrative reference);
3. the candidate evidence showing adherence, justified deviation, or violation.

Check dated/versioned source URLs and date accessed. Treat an official recommendation as stronger evidence than an arbitrary repository convention. Evaluate only meaningful practices such as supported APIs, framework conventions, type safety, configuration, accessibility/security patterns, dependency management, and maintainable error handling.

### 8. Robustness and portability — 6

Measure clean, documented install/build/start and test commands from a clean state; repeatability; graceful handling of expected error/empty/loading states; configuration via documented environment variables; and dependency on undeclared local state.

Test OS/browser portability only on a declared matrix. Give credit only for actual verified runs. A source inspection suggesting portability is not a successful OS test. Report setup steps, time-to-first-success, failures, and reproducibility.

### 9. Maintainability and modularity — 4

Assess responsibility boundaries, cohesion, coupling, naming, duplication, data flow, ease of locating behavior, and whether changes can be made without broad unrelated edits. Support claims with examples and paths/lines. Do not reward folder count or abstractions by themselves; judge whether structure is appropriate for the actual app size.

### 10. User experience and visual fidelity — 3

Use the same defined workflows, viewport sizes, synthetic content, and reference assets. Assess clarity, consistency, responsive layout, feedback, error recovery, and fidelity to explicit requirements/reference. Include screenshots or recordings with the environment in evidence. Do not let aesthetic taste override functional or accessibility evidence.

## Recommendation gates

Keep eligibility separate from score. A candidate is eligible for the top recommendation only if:

- all Critical requirements in the shared brief pass;
- overall functionality score is at least 70;
- security score is at least 70; and
- there are no confirmed Critical or High security findings.

If no candidate meets all gates, explicitly say **no recommended production-ready solution**. The highest-scoring candidate may be named as the best starting point, but must not be called a safe winner. A High finding may be shown alongside the score; do not bury it in an average.

If evaluated-weight coverage differs by more than 10 percentage points between candidates, or the leading score difference is less than 3 points, label the ordering **provisional / effectively tied**, explain why, and recommend further tests or human review. Do not pretend the formula resolves uncertainty.

## Overall score and interpretation

Calculate the weighted overall score using the formula in `COMPARISON_SPEC.md`, using only dimensions with comparable evidence. Also show evaluated-weight coverage, gate outcomes, and confidence caveats. Do not silently adjust weights, scores, or missing results to produce a winner.
