# Shared product brief

> Replace this template before running a comparison. Keep requirements independent of any one candidate's implementation. Every candidate must be assessed against the same frozen version of this document.

## Brief metadata

- Product name:
- Brief version:
- Date frozen:
- Owner/approver:
- Target users:
- Supported browsers/devices:
- Explicitly out of scope:

## Product overview

Describe the product, its purpose, and the user problem it solves.

## User journeys and acceptance criteria

Write requirements as observable outcomes. Assign stable IDs; mark importance and make success testable. Example:

| ID | User journey / requirement | Acceptance condition | Importance |
|---|---|---|---|
| F-001 | A user can create an item | Given valid input, when the user submits, the item appears once in the list and survives a reload | Critical |

Importance values:

- **Critical**: required for the product's primary purpose; failure may fail the functionality gate.
- **High**: important common behavior.
- **Normal**: expected but non-core behavior.
- **Low**: polish or edge behavior.

### Requirements

<!-- Add stable-ID requirements here. Avoid untestable wording such as "works well." -->

## Data and state

- Required fields and validation:
- Persistence expectations:
- Empty/loading/error states:
- Seed/test data:
- Data deletion/retention expectations:
- Any sensitive data that must never be used in the evaluation:

## Interface and visual expectations

- Required screens and navigation:
- Responsive viewports:
- Interaction expectations:
- Reference mockups/assets (if any):
- Visual aspects that are essential versus discretionary:

## Accessibility expectations

- Target standard/level (suggested default: WCAG 2.2 AA):
- Required keyboard and assistive-technology flows:
- Any exceptions:

## Non-functional requirements

- Performance targets (if applicable):
- Availability/recovery expectations:
- Supported deployment environments:
- Security/privacy constraints:
- Localization requirements:

## Evaluation fixtures and constraints

- Approved test accounts/fixtures (synthetic only):
- External services candidates may or may not use:
- Network access required by the product:
- Environment or tool constraints:
- Product-specific security threat assumptions:

## Clarifications and decisions

Record material interpretations agreed before grading. Do not silently resolve ambiguities after seeing candidate results.

| Date | Requirement ID | Decision / clarification | Approved by |
|---|---|---|---|
