# Analytic Story Record

The Analytic Story Record proposes a structure for documenting information about an individual Analytic Story.

The proposed fields organize story-level context, detection relationships, coverage observations, dependencies, findings, and supporting evidence without duplicating detection-level information.

**Status:** Draft record specification under development. Field selection, relationships, and maintenance requirements remain subject to practical testing and refinement.

## Record Structure

### Identity

| Field | Purpose | Maintenance |
|---|---|---|
| `story_id` | Stable identifier for the story | Maintained |
| `title` | Human-readable story name | Maintained |
| `lifecycle_status` | Current lifecycle state | Maintained |
| `description` | Short description of the story | Maintained |

Suggested lifecycle values:

- `planned`
- `active`
- `under_review`
- `retired`

### Objective

| Field | Purpose | Maintenance |
|---|---|---|
| `security_question` | Shared security question that organizes the story | Maintained |
| `objective` | Defensive purpose of the story | Maintained |
| `scope_notes` | Boundaries, assumptions, or relevant context | Maintained |
| `domains` | Security domains related to the story | Maintained |

The security question should remain stable unless the meaning of the story materially changes.

### Composition

| Field | Purpose | Maintenance |
|---|---|---|
| `detections` | References to detections that contribute to the story | Reference |
| `role` | Relationship of a detection to the story | Maintained |
| `relationship_status` | Current state of the detection-to-story relationship | Maintained |

Possible roles may include:

- `primary`
- `supporting`
- `correlation`
- `contextual`

Detection counts should be derived from these relationships rather than manually maintained.

### Coverage

| Field | Purpose | Maintenance |
|---|---|---|
| `covered_behaviors` | Behaviors assessed as covered within a stated scope and supported by evidence | Maintained |
| `partial_behaviors` | Behaviors assessed as addressed only under certain conditions or within a limited scope | Maintained |
| `uncovered_behaviors` | In-scope behaviors for which no applicable detection capability has been identified | Maintained |
| `coverage_notes` | Scope, evidence limitations, and uncertainty affecting coverage assessments | Maintained |

Coverage classifications are proposed analytical findings, not proof of detection effectiveness. Assessments should consider detection scope, supporting evidence, and unresolved limitations.

### Dependencies

| Field | Purpose | Maintenance |
|---|---|---|
| `dependencies` | Shared telemetry, enrichment, lookups, controls, or supporting services | Reference |
| `related_detections` | Detections affected by the dependency | Reference |
| `dependency_notes` | Story-level context about the dependency | Maintained |

Dependency health or concentration should be derived in the security analytics layer when possible.

### Evidence

| Field | Purpose | Maintenance |
|---|---|---|
| `evidence_refs` | References supporting story-level conclusions | Reference |
| `validation_refs` | References to relevant validation evidence | Reference |
| `operational_refs` | References to runtime or operational observations | Reference |
| `evidence_notes` | Context needed to interpret the evidence | Maintained |

The record should reference evidence rather than become a raw evidence store.

### Findings

| Field | Purpose | Maintenance |
|---|---|---|
| `findings` | Story-level weaknesses, gaps, or unknowns | Maintained |
| `related_detections` | Detections connected to the finding | Reference |
| `related_dependencies` | Dependencies connected to the finding | Reference |
| `evidence_refs` | Evidence supporting the finding | Reference |

Story-level findings may describe gaps, limitations, relationships, or unknowns relevant to the shared security objective. Findings should reference supporting evidence and distinguish confirmed conditions from unresolved concerns.

### Maintenance

| Field | Purpose | Maintenance |
|---|---|---|
| `owner_team` | Team responsible for maintaining the story | Maintained |
| `review_cadence` | Expected review interval | Maintained |
| `last_reviewed` | Most recent review date | Maintained |
| `reassessment_triggers` | Changes that should trigger review | Maintained |
| `work_item_refs` | References to related engineering work | Reference |

Dates such as the next review should be derived when they can be calculated from maintained fields.

### Relationships

| Field | Purpose | Maintenance |
|---|---|---|
| `related_stories` | Other Analytic Stories with a meaningful relationship | Reference |
| `shared_dependencies` | Dependencies shared with other stories | Reference |
| `overlapping_detections` | Detections that contribute across stories | Reference |

Relationships may later support graph, overlap, and change-impact analysis.

## Information Handling

**Maintained** — information entered or updated as part of the story record.

**Reference** — a pointer to information maintained in another record or system.

**Derived** — information calculated from maintained fields, relationships, or operational data.

Derived values should live in the security analytics layer unless there is a clear reason to persist them.

## Record Rules

1. Keep detection-level facts in Detection Attributes.
2. Store only information that has meaning at the Analytic Story level.
3. Reference evidence instead of duplicating it.
4. Prefer deriving counts, ratios, condition summaries, and review indicators from maintained information when supporting data and methods are available.
5. Keep lifecycle state separate from analytical condition.
6. Preserve the factors behind conclusions rather than relying on a single composite score.
7. Keep unresolved questions visible instead of replacing them with assumed values.

## Open Questions

- Should story condition be stored in the record or derived by a separate model?
- Should coverage use structured behavior records or remain a simpler maintained list?
- Should dependencies become reusable records shared across models?
- Should findings remain embedded in the story or become standalone referenced records?
- Which reassessment triggers should be standardized across security models?
