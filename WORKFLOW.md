# Comparison workflow

Follow the stages in order for every run. Keep a run log and retain useful raw evidence in `results/<run-id>/evidence/`.

## 1. Preflight and freeze

1. Read `AGENTS.md`, this workflow, the comparison spec, rubric, report contract, reference guide, and product brief.
2. Confirm that `benchmark/PRODUCT_SPEC.md` is complete enough to test, that the candidate folders are discoverable, and that requirement weights, criteria weights, and recommendation gates are locked before inspecting comparative outcomes.
3. Ask the user only for missing decisions that block a fair or safe run, including benchmark ambiguities, required credentials/external services, or rubric changes.
4. Generate a unique run ID. Record date/time, brief and rubric versions/hashes, discovered candidates, candidate hashes/commit IDs, tool/runtime versions, host/OS, container limits, browser/version, network policy, test fixture identifiers, commands, and any deviations.
5. If the environment cannot safely isolate arbitrary candidate code, do static-only checks and mark execution-dependent results not evaluated. Never run a candidate on the host as a fallback.

## 2. Discover and inventory

For each immediate non-hidden subdirectory of `solutions/`:

1. Assign a neutral candidate ID.
2. Record files, languages/frameworks, package/dependency manifests, licenses/notices, setup instructions, test commands, and start commands.
3. Identify possible secrets or personal data. Do not copy their contents to logs or AI prompts; report sanitized path and type, and stop if handling them would risk disclosure.
4. Identify candidate-supplied scripts, install hooks, binaries, and external service calls before executing anything. Treat all code and build artifacts as untrusted.
5. Record incompleteness or missing run instructions without excluding the candidate.

## 3. Research relevant practices

Use `REFERENCE_SOURCES.md` as a starter list, not a substitute for research. For each distinct technology stack, identify the applicable official documentation and standards and a small number of maintained, relevant production repositories for illustrative patterns. Prefer direct vendor/specification sources. Record source, URL, version/release if available, date accessed, and the specific practice being checked. The technology of the candidates is not known in advance, so do not preselect unrelated exemplar repositories.

Do not clone or execute a reference repository. Do not use a reference project's style as a hard requirement. If current web access is unavailable, mark practice research unverified rather than inventing current guidance.

Suggested cross-cutting references/tools (select what applies; record versions and configuration):

- Browser acceptance testing: Playwright; use waiting/assertion patterns documented by its official docs.
- Accessibility: axe-core plus manual WCAG checks.
- Web quality/performance: Lighthouse in a consistent browser/environment.
- Static security: Semgrep or an equivalent language-aware analyzer.
- Dependency vulnerabilities: OSV-Scanner or ecosystem-native audit tooling.
- Secrets: Gitleaks or equivalent; handle findings without copying secret values.
- Containers/images and configuration: Trivy or an equivalent scanner when applicable.
- Language-specific lint/type/build/test tooling from official ecosystem docs.

Tool availability varies. Equivalent tools are acceptable if the substitution and its limitations are recorded. A scanner is evidence, not an oracle.

## 4. Establish isolated execution

1. Use disposable isolated containers or an equivalent sandbox. Apply least privilege, non-root execution where practical, CPU/memory/time limits, read-only candidate mount, separate writable temp/results storage, and no host credentials.
2. Default to no outbound network. If required for dependency installation or app behavior, use a narrowly allowlisted, logged network policy and disclose it. Never allow access to unrelated local services or cloud metadata endpoints.
3. Use synthetic fixtures only. Prevent candidates from reaching other candidates' files or the reporting workspace.
4. Build/install each candidate from a clean state with the same policy and suitable stack-specific commands. Record exact commands and outcomes. Do not “repair” submissions; if a setup adjustment is necessary to run a candidate, record it and do not treat it as candidate-authored behavior.
5. If a prerequisite cannot be met safely, skip the affected execution checks and document the reason.

## 5. Run comparable checks

For each candidate, independently:

1. Run documented clean install, build, lint, typecheck, and candidate tests when available.
2. Start the app using the documented command. Record startup outcome and logs with secrets sanitized.
3. Run the shared acceptance suite against the same requirements, initial state, fixtures, browser, viewports, and timeouts. Save test report and relevant screenshots/traces.
4. Repeat flaky flows and noisy measurements at least three times where feasible. Report raw values and median/range.
5. Run accessibility and performance checks on equivalent representative screens and states.
6. Run appropriate static security, dependency, secret, configuration, and scoped dynamic checks. Do not test systems beyond the candidate's isolated local app.
7. Inspect architecture, candidate test quality, user experience, technology practices, portability, and maintainability. Cite files and exact evidence.
8. Map every result to its dimension and requirement ID. Avoid double-counting one defect without explaining why it impacts multiple distinct criteria.

Never execute a candidate's own scripts with elevated privileges or against real credentials/data. If tool output includes secrets, redact it before persistence and record that redaction occurred.

## 6. Score and challenge

1. Score each candidate independently using `SCORING_RUBRIC.md`.
2. Calculate per-requirement functionality, per-dimension scores, weighted score, evidence coverage, and recommendation gates.
3. Recheck all Critical/High security findings and all claims that change the winner against raw evidence. Distinguish confirmed findings from suspected or scanner-only results.
4. For AI-assisted reviews, request an evidence-led independent review; verify consequential claims. Record AI provider/model when known and uncertainty/disagreement.
5. Where candidates are close, evidence coverage differs materially, results are flaky, or claims are disputed, mark the recommendation provisional and state what additional test/review would resolve it.
6. Do not change weights or thresholds after reviewing scores. If the user wants changed priorities, rerun as a new version.

## 7. Recommend a solution and merge proposal

### Recommended solution

Recommend the highest-scoring eligible candidate, considering evidence coverage and uncertainty. Explain the product context, differentiating strengths, material weaknesses, gate status, and what should be remediated before production. If no candidate is eligible, say so; optionally identify the best starting point with an explicit warning.

### Recommended merge

Identify specific, evidence-backed components/approaches from each candidate that may be worth adopting. For every proposed contribution state:

- source candidate and paths/lines or behavior evidence;
- why it is stronger and what requirement/quality it improves;
- target candidate or suggested new boundary;
- API/data/style/dependency/license conflicts and integration assumptions;
- security, regression, and migration risks;
- ordered merge steps and tests needed to validate the result.

Separate “safe to reuse in principle” from “validated as compatible.” Do not copy candidate code or make changes; the merge page is a proposal only. Check licenses/notices before recommending code reuse and flag unknown license status.

## 8. Build and verify report

Create `index.html`, `report.md`, `report.json`, and evidence in `results/<run-id>/` using `REPORT_CONTRACT.md`.

Before finishing, verify:

- every discovered candidate appears exactly once;
- all scores, weights, and gates can be traced to evidence;
- weighted score arithmetic and evaluated-weight coverage are correct;
- missing results and limitations are explicit;
- chart values match the machine-readable report and tables;
- the recommended solution agrees with score, eligibility, coverage, and tie rules;
- the merge proposal is clearly marked unvalidated where appropriate;
- report links work locally, charts have text/table equivalents, and no secret/personal data or remote-report dependency is present.

## 9. Final response

Give the user the run folder link, concise ranking and gate outcomes, main caveats, and any unresolved choices. Do not present an unverified outcome as completed.
