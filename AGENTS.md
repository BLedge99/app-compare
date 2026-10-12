# Comparison workspace instructions

This workspace compares web-app implementations of the same product brief. Follow this file and the linked documents whenever asked to run, evaluate, compare, or report on the candidates.

## Start here

1. Read `README.md`, `COMPARISON_SPEC.md`, `SCORING_RUBRIC.md`, `WORKFLOW.md`, `REPORT_CONTRACT.md`, and `REFERENCE_SOURCES.md`.
2. Read `benchmark/PRODUCT_SPEC.md` and the candidate directories under `solutions/`.
3. If the product spec is missing, still a template, or ambiguous on a behavior needed for scoring, stop before grading that behavior and ask the user to clarify it. Do not invent requirements.
4. Discover every eligible candidate folder; do not assume there are five. See `WORKFLOW.md` for discovery and exclusions.

## Non-negotiable evaluation rules

- Treat candidate folders as untrusted, read-only inputs. Do not edit, reformat, install into, or commit changes to them. Place generated data in a new run folder under `results/`.
- Do not run candidate code directly on the host. Use an available isolated container/runtime with least privilege, resource limits, no unnecessary secrets, and restricted network access. If safe isolation is unavailable, stop execution-based checks and clearly report the limitation; do not silently fall back to host execution.
- Do not expose secrets or personal data to a model, a candidate, a report, or an external service. Never put credentials in tracked files. External AI providers are optional and must be chosen/configured by the user at run time.
- Keep the benchmark spec, test inputs, environment, tool versions, scoring weights, AI reviewer/model identity (when known), and evidence provenance consistent across candidates. Record deviations.
- Prefer reproducible, shared acceptance tests and tool outputs over candidate claims or AI impressions. Never treat a passing test suite as proof that a candidate is correct or secure.
- Ground every finding and qualitative score in evidence. Cite candidate-relative paths and line numbers, test names, command/tool and version, output/artifact, and confidence where applicable. Separate verified facts, inferences, and unknowns.
- Do not fabricate tool results, web research, citations, successful runs, or line numbers. If a tool or source cannot be accessed, report that gap.
- Do not use candidate identity, author, or AI agent branding as a scoring factor. Mask identities where practical during qualitative review.
- Preserve the raw per-candidate evidence and machine-readable scores. Never hide a failed run or omit a candidate from the report; mark unavailable dimensions as `not_evaluated` with a reason.

## Workflow

Execute `WORKFLOW.md` end to end. Keep the following in mind:

- Assess each candidate independently against the common brief before comparing them.
- Apply the predeclared weights and gates in `SCORING_RUBRIC.md`. Do not adjust weights after seeing results. If the user changes them, start a new run and record the change.
- Do not let the overall average conceal a critical security finding or a failed core workflow. Report eligibility separately from numeric score.
- The merge recommendations page is a reasoned proposal, not an instruction to modify candidate folders. Describe compatible components, conflicts, dependencies, risks, and a staged integration/test plan. Do not claim the parts can be combined without validating that claim.
- If an AI reviewer is used, ask it to cite evidence and identify uncertainty; verify consequential claims against the source or tool artifacts. Do not let an AI reviewer generate a score from vibes or unsupported repository comparisons.

## Deliverables

For each run, write a self-contained report to `results/<run-id>/` following `REPORT_CONTRACT.md`. At minimum include:

- `index.html`: polished report with overview, comparative charts, individual candidate scorecards, detailed findings, recommended solution, and recommended merge plan.
- `report.json`: machine-readable results conforming to the documented contract.
- `report.md`: accessible, printable written report with the same substantive findings.
- `evidence/`: relevant raw tool output, test results, screenshots, source notes, and run metadata; do not copy secrets or unnecessary personal information.

Keep generated results out of candidate folders. The HTML report must work locally without sending report data to a remote service or depending on remote chart/font assets.

## Useful user request

The user should be able to start the process by asking an AI coding assistant: “Run the comparison workflow in `AGENTS.md`.” Ask focused questions only when a required benchmark detail, safety prerequisite, or user choice is missing.
