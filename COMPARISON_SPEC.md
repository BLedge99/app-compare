# Comparison specification

## Purpose

Compare an open-ended number of independent web-app implementations against one shared, frozen product brief. The outcome is a reproducible, evidence-backed comparison—not a claim that one solution is objectively best in every context.

The primary deliverables are a detailed report for every solution, an overall recommendation (or an explicit “none qualifies”), and a separate proposal for combining the strongest parts of different implementations.

## Principles

1. **Same target, same conditions.** Requirements, acceptance tests, fixtures, environment, tools, and scoring rules are fixed before results are examined.
2. **Observe behavior.** Functionality is graded against requirement-level evidence and shared tests, not the amount of code or the candidate's own description.
3. **Keep evidence and judgment distinct.** Tests, scanners, and measurements produce evidence; qualitative interpretations are reasoned judgments with citations and confidence.
4. **Report uncertainty.** A missing or incompatible tool result is `not_evaluated`, not a zero and not a pass. Low-confidence scores must not be presented as precise facts.
5. **Safety by default.** Candidate code is untrusted; keep it read-only and use a restricted isolated environment.
6. **No winner by arithmetic alone.** Show the weighted score, gates, and per-dimension trade-offs. A critical failure can disqualify a high-scoring candidate.
7. **Provider-neutral AI.** The workflow does not mandate a provider, model, API, or SDK. The user configures any external AI service at runtime. If no reviewer is configured, report which qualitative checks remain incomplete.
8. **Useful and reproducible research.** Cite current official documentation and maintained, relevant production repositories when judging technology-specific practices. Record URLs, version/date accessed, and the specific practice compared; do not treat repository popularity as proof of quality.

## Candidate and run identity

- Discover all eligible, immediate, non-hidden subdirectories in `solutions/`, or use an explicit user-provided manifest.
- Give each a neutral ID. Preserve a mapping to folder name in run metadata; mask author or agent identity during qualitative comparison where practical.
- Before evaluation, record candidate file inventories and a content hash/commit ID when available. Do not modify the input folders.
- Freeze and record the product brief version/hash, scoring rubric version, weights, gates, tool versions, host/container details, commands, timeouts, fixtures, and AI reviewer identity/model if known.
- A changed candidate, brief, environment, tool set, or weight set is a distinct run.

## Evidence model

For each criterion, report:

- score (0–100), status (`evaluated`, `partially_evaluated`, or `not_evaluated`), confidence (0–1), and weight;
- evidence references (requirement IDs, file paths/line numbers, command and tool versions, test names, raw artifact paths, or source URLs);
- what passed, failed, and was not tested;
- limitations, environment variance, and any reviewer disagreement.

Do not fabricate precision. Measurements with repeat runs should include the raw values and summary statistic. Use confidence to qualify interpretation, not as a hidden multiplier on the total.

## Comparability controls

- Use the same operating environment, browser, viewport, fixture data, network policy, test steps, timeouts, and resource limits for all candidates.
- Start each candidate from a clean state and perform repeat runs for flaky workflows and noisy measures. Three independent runs is the suggested minimum for non-deterministic functional or performance observations; report median and range for numeric timings.
- Do not compare incomparable measurements. For example, if a candidate cannot start, label browser performance as not evaluated and explain the failed prerequisite.
- Run common black-box acceptance flows independently of each candidate's own tests. A candidate's test suite is graded as a separate artifact, never used as the sole proof of application correctness.
- Do not change rubric thresholds or weights after seeing results. If the user requests a different priority, generate a new run with the revised rubric.

## Scoring

Use the dimensions and initial weights in `SCORING_RUBRIC.md`. Each evaluated score is 0–100. The raw overall score is the weighted sum of evaluated scores normalized by their total evaluated weight:

`raw_overall = sum(dimension_score * dimension_weight) / sum(evaluated_dimension_weights)`

Also show **evaluated weight coverage**: sum of weights for evaluated dimensions / 100. Partial or missing evidence must be clearly visible. Do not rank candidates with materially different evidence coverage as though they were directly comparable; label the ranking provisional or defer a recommendation.

Eligibility is separate from the numeric score. Apply the gates in the rubric. If no candidate passes, recommend none rather than selecting an unsafe/nonfunctional winner. Always show raw score and gate status.

## AI-assisted qualitative review

When an AI reviewer is available:

- Give it the frozen brief/rubric, only necessary source/evidence, and anonymized candidate IDs where practical.
- Request requirement IDs, exact source paths and lines, evidence citations, counterexamples, uncertainty, and alternative explanations for each claim.
- Require independent candidate assessments before any cross-candidate ranking. Have a second independent review or targeted human verification for high-impact disputed claims when feasible.
- Verify consequential findings against source or raw tool output. AI output alone cannot establish a vulnerability, confirm absence of vulnerabilities, or justify a security gate.
- Keep credentials and sensitive data out of prompts and artifacts. Record whether provider data retention/training settings were checked when external review is used.
- For technology best practices, check official vendor/specification documentation and at least one relevant maintained, production-grade reference implementation. Note that reference repositories are examples, not normative standards.

## Recommended report contents

Follow `REPORT_CONTRACT.md`. At minimum, the report has:

1. Executive summary with candidate count, benchmark version, run conditions, evidence coverage, winner/no-winner decision, and major caveats.
2. Side-by-side charts for weighted total, each dimension, gate outcomes, test outcomes, and relevant measurements.
3. A complete individual scorecard and detailed, evidence-linked written assessment for every candidate.
4. A recommended solution page explaining why the top eligible implementation is recommended and for which use case.
5. A recommended merge page mapping best candidate components to target, compatibility/conflict risks, license/dependency considerations, and an ordered integration/validation plan.
6. Appendix with reproducibility metadata, raw measurements, tool output references, research citations, exclusions, and not-evaluated items.

Charts must include accessible text/table equivalents. Report output should be self-contained and open locally without remote assets or uploading report content.
