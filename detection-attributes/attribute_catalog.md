# Detection Attribute Catalog

This catalog documents the fields currently proposed in `detection-attributes.yaml`.

The catalog is a working design reference, not a formal schema. It is used to decide which attributes belong in the detection record, how they should be maintained, and what later analytics they may support.

## Classification

| Class | Meaning |
| --- | --- |
| **Core** | Strong candidate for the common detection record. |
| **Optional** | Useful when applicable, but not expected for every detection. |
| **Candidate** | Still under review for placement, meaning, or long-term value. |
| **Derived** | Better calculated from other data than manually maintained. |

**Maintenance** describes how a value is expected to enter the record:

- **Manual** — maintained by a practitioner.
- **Reference** — points to another artifact or system.
- **Manual / derived** — may begin as a practitioner-maintained summary but could later be calculated from runtime data.

## Record

| Attribute | Type | Class | Maintenance | Purpose | Potential analytical use |
| --- | --- | --- | --- | --- | --- |
| `schema_version` | string | Core | Manual | Identifies the attribute model version used by the record. | Schema/version distribution |
| `record.detection_id` | string | Core | Manual | Stable identifier for the detection. | Joins, inventory, history |
| `record.title` | string | Core | Manual | Human-readable detection name. | Reporting and views |
| `record.lifecycle_status` | enum | Core | Manual | Describes where the detection is in its lifecycle. | Inventory and lifecycle reporting |
| `record.created_on` | date | Optional | Manual | Records when the detection record was created. | Age and inventory history |
| `record.last_updated` | date | Optional | Manual / derived | Records the most recent meaningful record update. | Staleness and review reporting |
| `record.change_notes` | text | Optional | Manual | Captures context for a meaningful record update. | Change history and review context |

## Definition

**Question:** What is this detection intended to identify, and why does it exist?

| Attribute | Type | Class | Maintenance | Purpose | Potential analytical use |
| --- | --- | --- | --- | --- | --- |
| `definition.description` | text | Core | Manual | Short description of the detection. | Search and reporting |
| `definition.detection_type` | enum | Optional | Manual | Describes the general analytic form. | Detection-type distribution |
| `definition.behavior` | text | Core | Manual | States the behavior the detection is intended to identify. | Behavior grouping and coverage analysis |
| `definition.security_objective` | text | Core | Manual | States the defensive purpose of the detection. | Objective and capability grouping |
| `definition.expected_signal` | text | Core | Manual | Describes what signal should be produced when the intended behavior occurs. | Validation and actionability review |
| `definition.threat_relevance` | text | Optional | Manual | Records why the behavior matters from a threat perspective. | Threat-informed prioritization |
| `definition.detection_platform` | string | Optional | Manual | Identifies the analytics or SIEM platform hosting the detection. | Platform distribution and dependency analysis |
| `definition.rule_language` | string | Optional | Manual | Identifies the query or rule language. | Engineering inventory |
| `definition.rule_reference` | reference | Optional | Reference | Points to the implementation of the detection. | Traceability |
| `definition.analytic_story_refs` | list[reference] | Optional | Reference | Links the detection to related analytic stories. | Story composition and relationship analysis |
| `definition.attack_mapping[].technique_id` | string | Optional | Manual | Maps the detection to an ATT&CK technique. | ATT&CK classification |
| `definition.attack_mapping[].subtechnique_id` | string | Optional | Manual | Maps the detection to an ATT&CK sub-technique. | ATT&CK classification |
| `definition.attack_mapping[].rationale` | text | Optional | Manual | Explains why the ATT&CK mapping applies. | Mapping review and evidence quality |
| `definition.tags` | list[string] | Optional | Manual | Supports local classification and search. | Filtering and grouping |

## Context

**Question:** Where should this detection apply, and what assumptions or boundaries shape its intended use?

| Attribute | Type | Class | Maintenance | Purpose | Potential analytical use |
| --- | --- | --- | --- | --- | --- |
| `context.environments` | list[string] | Core | Manual | Defines the intended environments for the detection. | Environment coverage |
| `context.platforms` | list[string] | Optional | Manual | Defines endpoint, operating-system, cloud, or service platforms in scope. | Platform coverage |
| `context.asset_scope` | list[string] | Optional | Manual | Defines relevant asset populations or classes. | Scope and coverage analysis |
| `context.identity_scope` | list[string] | Optional | Manual | Defines relevant identity populations or classes. | Identity coverage |
| `context.assumptions` | list[text] | Core | Manual | Records environmental assumptions required for expected behavior. | Limitation and risk review |
| `context.exclusions` | list[text] | Optional | Manual | Records intentional scope exclusions. | Coverage-gap interpretation |
| `context.security_context` | text | Optional | Manual | Captures defensive or environmental context needed to interpret the detection. | Prioritization and reporting |
| `context.scope_notes` | text | Optional | Manual | Preserves additional scope detail that does not fit structured fields. | Practitioner context |

## Telemetry

**Question:** What data does this detection depend on, and is that data sufficient and reliable for the intended analytic?

| Attribute | Type | Class | Maintenance | Purpose | Potential analytical use |
| --- | --- | --- | --- | --- | --- |
| `telemetry.sources[].source_id` | string | Core | Manual | Stable identifier for a required or supporting telemetry source. | Dependency and source concentration |
| `telemetry.sources[].source_name` | string | Core | Manual | Human-readable telemetry source name. | Reporting |
| `telemetry.sources[].required` | boolean | Core | Manual | Distinguishes required sources from supporting sources. | Critical dependency analysis |
| `telemetry.sources[].notes` | text | Optional | Manual | Preserves source-specific context. | Review context |
| `telemetry.required_fields` | list[string] | Core | Manual | Identifies fields the analytic requires. | Field dependency and data-quality review |
| `telemetry.optional_fields` | list[string] | Optional | Manual | Identifies fields that improve the analytic but are not required. | Enrichment opportunities |
| `telemetry.normalization.required` | boolean | Optional | Manual | Indicates whether normalized data is required. | Normalization dependency analysis |
| `telemetry.normalization.method` | string | Optional | Manual | Identifies the normalization method or model. | Change-impact analysis |
| `telemetry.normalization.notes` | text | Optional | Manual | Records normalization caveats. | Data-quality interpretation |
| `telemetry.data_quality_notes` | list[text] | Core | Manual | Records known quality observations affecting use of the telemetry. | Telemetry condition analysis |
| `telemetry.known_gaps` | list[text] | Core | Manual | Records known missing or unreliable telemetry. | Gap and risk analysis |
| `telemetry.evidence_refs` | list[reference] | Optional | Reference | Links telemetry claims to supporting evidence. | Evidence completeness |
| `telemetry.practitioner_notes` | text | Optional | Manual | Preserves practitioner interpretation. | Qualitative review |

## Dependencies

**Question:** What supporting components or services must remain available or reliable for this detection to work as intended?

| Attribute | Type | Class | Maintenance | Purpose | Potential analytical use |
| --- | --- | --- | --- | --- | --- |
| `dependencies[].dependency_id` | string | Core | Manual | Stable identifier for a nontrivial dependency. | Dependency graphing |
| `dependencies[].dependency_type` | enum | Core | Manual | Classifies the dependency. | Dependency concentration |
| `dependencies[].name` | string | Core | Manual | Human-readable dependency name. | Reporting |
| `dependencies[].required` | boolean | Core | Manual | Indicates whether the detection requires the dependency to function as intended. | Critical dependency analysis |
| `dependencies[].owner_or_source` | string | Optional | Manual | Records ownership or origin of the dependency. | Change coordination |
| `dependencies[].notes` | text | Optional | Manual | Preserves dependency-specific context. | Change-impact interpretation |

## Logic

**Question:** How does the detection identify the behavior, and what assumptions, filters, or limitations affect the analytic?

| Attribute | Type | Class | Maintenance | Purpose | Potential analytical use |
| --- | --- | --- | --- | --- | --- |
| `logic.analytic_method` | string | Core | Manual | Describes the analytic approach used by the detection. | Analytic-method grouping |
| `logic.summary` | text | Core | Manual | Explains the logic at a readable level without reproducing the full rule. | Review and reporting |
| `logic.conditions` | list[text] | Core | Manual | Records the principal conditions used to produce a signal. | Logic review |
| `logic.thresholds` | list[text] | Optional | Manual | Records thresholds that materially affect behavior. | Tuning and change review |
| `logic.time_window` | string | Optional | Manual | Records time-based evaluation or correlation windows. | Correlation and tuning analysis |
| `logic.joins` | list[text] | Optional | Manual | Records required joins between datasets or entities. | Complexity and dependency analysis |
| `logic.lookups` | list[text] | Optional | Manual | Records lookups used by the analytic. | Dependency and change-impact analysis |
| `logic.enrichments` | list[text] | Optional | Manual | Records enrichment used to improve detection context or logic. | Enrichment dependency analysis |
| `logic.filters` | list[text] | Optional | Manual | Records meaningful filters. | Tuning and exclusion review |
| `logic.suppressions` | list[text] | Optional | Manual | Records suppression behavior. | Noise-management review |
| `logic.analytic_assumptions` | list[text] | Optional | Manual | Records assumptions specific to how the analytic logic behaves. | Logic risk review |
| `logic.known_limitations` | list[text] | Core | Manual | Records known limitations of the analytic. | Detection-quality analysis |
| `logic.edge_cases` | list[text] | Optional | Manual | Records known cases that may behave differently from the common path. | Validation planning |
| `logic.evidence_refs` | list[reference] | Optional | Reference | Links logic claims to supporting artifacts. | Evidence completeness |
| `logic.practitioner_notes` | text | Optional | Manual | Preserves implementation or tuning context. | Qualitative review |

## Validation

**Question:** What evidence shows that this detection works as intended against representative behavior?

| Attribute | Type | Class | Maintenance | Purpose | Potential analytical use |
| --- | --- | --- | --- | --- | --- |
| `validation.state` | enum | Core | Manual | Summarizes the current validation state. | Validation-condition reporting |
| `validation.last_validated` | date | Core | Manual | Records the most recent meaningful validation date. | Validation age and staleness |
| `validation.methods` | list[enum] | Core | Manual | Records how the detection was validated. | Validation-method coverage |
| `validation.test_case_refs` | list[reference] | Optional | Reference | Links to reusable validation cases. | Test coverage |
| `validation.positive_test_refs` | list[reference] | Optional | Reference | Links to tests expected to generate a signal. | Positive-path evidence |
| `validation.negative_test_refs` | list[reference] | Optional | Reference | Links to tests expected not to generate a signal. | False-positive resistance |
| `validation.representative_data` | boolean/null | Candidate | Manual | Indicates whether validation used data representative of intended operation. | Validation-confidence analysis |
| `validation.regression_tested` | boolean/null | Optional | Manual | Indicates whether prior expected behavior has been retested after change. | Change and maintenance analytics |
| `validation.evidence_refs` | list[reference] | Core | Reference | Links validation claims to evidence. | Evidence completeness |
| `validation.practitioner_notes` | text | Optional | Manual | Preserves validation interpretation and caveats. | Qualitative review |

## Actionability

**Question:** When this detection fires, does the alert provide enough context for an analyst to understand, investigate, and act?

| Attribute | Type | Class | Maintenance | Purpose | Potential analytical use |
| --- | --- | --- | --- | --- | --- |
| `actionability.expected_context` | list[string] | Core | Manual | Defines context expected to support triage or investigation. | Context completeness |
| `actionability.available_context` | list[string] | Core | Manual | Records context currently delivered with the signal. | Actionability comparison |
| `actionability.analyst_guidance_ref` | reference | Optional | Reference | Links to analyst-facing guidance. | Guidance coverage |
| `actionability.triage_notes` | text | Optional | Manual | Records important triage considerations. | Operational context |
| `actionability.known_noise` | list[text] | Optional | Manual | Records known recurring low-value or repetitive signal patterns. | Noise analysis |
| `actionability.known_false_positive_patterns` | list[text] | Core | Manual | Records understood benign patterns that may trigger the detection. | Tuning and false-positive analysis |
| `actionability.escalation_context` | text | Optional | Manual | Describes conditions or evidence that may warrant escalation. | Investigation guidance |
| `actionability.evidence_refs` | list[reference] | Optional | Reference | Supports actionability claims with evidence. | Evidence completeness |
| `actionability.practitioner_notes` | text | Optional | Manual | Preserves practitioner context. | Qualitative review |

Derived example: missing context can be calculated by comparing `expected_context` with `available_context` rather than maintained as a separate source field.

## Observability

**Question:** Can the team tell whether this detection is running and producing expected operational signals over time?

| Attribute | Type | Class | Maintenance | Purpose | Potential analytical use |
| --- | --- | --- | --- | --- | --- |
| `observability.deployment_state` | enum | Core | Manual / derived | Describes whether the detection is deployed and active. | Deployment inventory |
| `observability.alert_destination` | string | Optional | Manual | Records where generated alerts or findings are delivered. | Workflow mapping |
| `observability.last_observed_alert` | date/time | Candidate | Derived | Records the most recent observed signal. | Inactivity analysis |
| `observability.operational_observations` | list[text] | Core | Manual | Preserves useful runtime observations when formal metrics are unavailable. | Qualitative runtime analysis |
| `observability.dashboard_refs` | list[reference] | Optional | Reference | Links to supporting operational views. | Traceability |
| `observability.evidence_refs` | list[reference] | Optional | Reference | Supports runtime observations. | Evidence completeness |
| `observability.practitioner_notes` | text | Optional | Manual | Preserves runtime interpretation. | Qualitative review |

Runtime health, inactivity state, execution health, and noise state are intentionally left out of the source record for now. They are stronger candidates for derived analytics once supporting runtime data is defined.

## Maintenance

**Question:** What needs to be reviewed, monitored, or updated to keep this detection useful as the environment changes?

| Attribute | Type | Class | Maintenance | Purpose | Potential analytical use |
| --- | --- | --- | --- | --- | --- |
| `maintenance.owner_team` | string | Core | Manual | Identifies the team accountable for the detection. | Ownership and workload reporting |
| `maintenance.maintainer` | string | Optional | Manual | Identifies an individual or role responsible for maintenance. | Work routing |
| `maintenance.review_cadence` | string | Optional | Manual | Records an expected review interval. | Review planning |
| `maintenance.last_reviewed` | date | Core | Manual | Records the most recent substantive review. | Review age |
| `maintenance.reassessment_triggers[].trigger_type` | enum | Core | Manual | Classifies a condition that should cause reassessment. | Change-impact analytics |
| `maintenance.reassessment_triggers[].condition` | text | Core | Manual | Describes the condition that should trigger review. | Reassessment planning |
| `maintenance.reassessment_triggers[].related_dependency_refs` | list[reference] | Optional | Reference | Connects triggers to known dependencies. | Dependency-driven reassessment |
| `maintenance.finding_refs` | list[reference] | Optional | Reference | Links known findings affecting the detection. | Finding concentration and backlog |
| `maintenance.work_item_refs` | list[reference] | Optional | Reference | Links active engineering work. | Maintenance workload |
| `maintenance.maintenance_notes` | text | Optional | Manual | Preserves maintenance context not captured elsewhere. | Qualitative review |

Derived example: the next expected review date can be calculated from `last_reviewed` and `review_cadence` when cadence is structured consistently.

## References

| Attribute | Type | Class | Maintenance | Purpose | Potential analytical use |
| --- | --- | --- | --- | --- | --- |
| `references[].ref_id` | string | Core | Manual | Stable local identifier for a referenced artifact. | Reference joins |
| `references[].type` | enum | Core | Manual | Classifies the referenced artifact. | Evidence-source analysis |
| `references[].location` | string | Core | Reference | Points to the source artifact. | Traceability |
| `references[].notes` | text | Optional | Manual | Describes why the reference matters. | Evidence interpretation |

## Current review questions

Version 0.3 incorporates revisions to attribute placement and duplication. The remaining design questions require testing against completed example records:

1. **Controlled vocabularies** — enum values remain provisional until examples show that the categories are practical.
2. **Noise versus false positives** — keep both only if examples show practitioners can distinguish recurring low-value signal from benign activity that incorrectly matches analytic intent.
3. **Representative validation data** — determine whether `representative_data` is useful as a boolean or needs a richer evidence-oriented structure.
4. **Dependency modeling** — the new top-level Dependencies section may later become a reusable object model if cross-detection dependency analysis requires it.
5. **Runtime-derived attributes** — determine which Observability values should be sourced automatically from SIEM or monitoring data instead of maintained in the record.
6. **Review cadence** — determine whether cadence should become a controlled value so review dates can be calculated consistently.
