# Report contract

Every comparison run produces the files below under `results/<run-id>/`. They are generated artifacts; do not place them in candidate folders.

## `index.html`

Create a polished, responsive report that opens locally. Do not load scripts, fonts, images, analytics, or chart libraries from remote services. Inline small static assets or use native HTML/CSS/SVG. Provide semantic headings, keyboard access, readable contrast, and text/table equivalents for every chart.

Required sections/pages:

1. **Overview**: run identity, brief/rubric versions, date/environment, candidate count, data coverage, overall conclusion and caveats.
2. **Comparison**: side-by-side dimension scores, weighted scores, gate/eligibility state, requirement pass rates, and meaningful tool measurements.
3. **Candidate detail**: one full scorecard and written report per candidate, including criteria, evidence, defects, test results, security findings, limitations, and recommendation status.
4. **Recommended solution**: top eligible option and rationale, or a clear no-eligible-solution decision; include trade-offs and remediation.
5. **Recommended merge**: best contributions from other candidates, proposed destinations/integration sequence, risks, compatibility and license notes, and validation plan.
6. **Method and evidence**: rubric/weights, environment, tools and versions, commands, repeat measurements, research sources, exclusions, and not-evaluated dimensions.

Use clear severity markers and labels, but never rely on color alone. Avoid misleading axes/scales and unsupported numerical precision.

## `report.md`

Provide an accessible, printable written equivalent of the HTML report. It must include the same substantive scores, gate decisions, findings, recommendation, merge proposal, and limitations.

## `report.json`

Use UTF-8 JSON. Keep score and provenance fields explicit; do not encode `not_evaluated` as 0 or null without a status and reason. Suggested minimum shape:

```json
{
  "schema_version": "1.0",
  "run": {
    "id": "2026-10-12T123900Z-example",
    "started_at": "ISO-8601 timestamp",
    "completed_at": "ISO-8601 timestamp",
    "product_spec": { "version": "string", "sha256": "string" },
    "rubric": { "version": "string", "sha256": "string" },
    "environment": {},
    "tools": [],
    "ai_review": { "used": false, "provider": null, "model": null }
  },
  "weights": {
    "functionality": 24,
    "security_privacy": 15,
    "correctness": 14,
    "test_quality": 12,
    "accessibility": 8,
    "performance": 7,
    "best_practices": 7,
    "robustness_portability": 6,
    "maintainability_modularity": 4,
    "ux_visual_fidelity": 3
  },
  "candidates": [
    {
      "id": "candidate-a",
      "folder": "solutions/candidate-a",
      "source_fingerprint": "string",
      "dimensions": {
        "functionality": {
          "status": "evaluated",
          "score": 0,
          "confidence": 0.0,
          "weight": 24,
          "evidence": [],
          "limitations": []
        }
      },
      "raw_overall_score": 0,
      "evaluated_weight_coverage": 0,
      "gates": {
        "critical_requirements_pass": false,
        "functionality_minimum_pass": false,
        "security_minimum_pass": false,
        "no_critical_or_high_security_findings": false,
        "eligible": false
      },
      "findings": [],
      "requirement_results": [],
      "recommendation": {
        "rank": null,
        "status": "not_recommended",
        "summary": "string"
      }
    }
  ],
  "ranking": [],
  "recommended_solution": {},
  "merge_proposal": { "status": "proposed_not_validated", "items": [] },
  "limitations": [],
  "artifacts": []
}
```

This is a minimum shape, not a strict schema file. Preserve detail in `evidence`, `findings`, and artifact references. Use consistent dimension identifiers from the weights object. When a dimension is not evaluated, use for example:

```json
{
  "status": "not_evaluated",
  "score": null,
  "confidence": 0.0,
  "weight": 7,
  "evidence": [],
  "limitations": ["Application did not start in the isolated environment."]
}
```

Allowed dimension statuses: `evaluated`, `partially_evaluated`, `not_evaluated`. Allowed recommendation statuses should distinguish at least `recommended`, `best_starting_point_not_eligible`, `eligible_alternative`, `not_recommended`, and `provisional`.

Evidence should use stable artifact paths relative to the run folder where possible, plus candidate-relative source path/line, tool and version, command/test name, requirement ID, and concise interpretation. Sanitize secrets and personal information.

## `evidence/`

Store useful raw results: environment/run manifest, shared acceptance test output, candidate test output, scanner output (redacted as needed), screenshots, traces, measurement values, and research citations. Include only evidence needed to substantiate and reproduce the report. Do not persist credentials, real personal data, bulky dependency caches, or irrelevant full candidate copies.
