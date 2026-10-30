# Detection Capability

Detection Capability explores how the condition of an individual detection may be assessed using structured information and supporting evidence.

> What is the current condition of this detection, and what factors support that conclusion?

The proposed model draws on Detection Attributes to examine detection condition without creating a separate detection record.

**Status:** Proposed assessment model under development. The eight capability dimensions provide an initial structure for examination. Assessment criteria, evidence requirements, and consistency across practitioners require further research, testing, and validation.

## Capability Dimensions

### Behavior Definition

Examines whether the target behavior is clearly defined, relevant, bounded, and distinguishable from expected benign activity.

Key considerations may include:

- behavior definition
- environmental relevance
- meaningful behavioral variants
- expected benign activity
- behavioral boundaries and distinguishing conditions

### Telemetry Readiness

Examines whether the required telemetry is available, representative, understandable, timely, and dependable.

Key considerations may include:

- required telemetry availability
- required field availability
- semantic reliability
- scope representation
- timeliness and retention
- telemetry dependencies

### Detection Logic

Examines how well the detection logic represents the intended behavior and scope.

Key considerations may include:

- behavioral alignment
- scope alignment
- logic dependencies and conditions
- resilience to meaningful behavioral variation
- handling of expected benign activity

### Validation Evidence

Examines whether available evidence supports claims about detection performance under representative conditions.

Key considerations may include:

- positive behavior validation
- variant validation
- benign and negative validation
- representative validation conditions
- regression and post-change validation
- validation limitations

### Operational Context

Examines whether the context needed to interpret detection output is available and reliable.

Key considerations may include:

- context requirements
- context availability at decision time
- context reliability
- distinguishing context sufficiency
- context dependencies and limitations

### Analyst Actionability

Examines whether the detection provides a clear, repeatable, and sustainable investigation and decision path.

Key considerations may include:

- investigation path
- decision and escalation guidance
- ownership and routing
- operational burden
- response feasibility

### Detection Observability

Examines whether practitioners have sufficient visibility into detection execution, dependencies, and operational behavior.

Key considerations may include:

- current execution state
- telemetry continuity
- dependency health
- unexpected silence or activity change
- failure and degradation visibility

### Lifecycle Maintainability

Examines the considerations affecting ongoing understanding, modification, validation, and maintenance of a detection.

Key considerations may include:

- maintainability
- environmental change resilience
- behavioral adaptability
- engineering and technical cost
- maintenance and decision history
- ongoing maintenance burden

## Why Detection Condition Needs More Than a Healthy/Unhealthy Label

A detection may function as configured without providing dependable defensive value. Execution, effectiveness, and operational usefulness answer different questions:

- **Execution:** Does the rule run as configured, with required inputs and dependencies available?
- **Effectiveness:** Does the logic identify the intended behavior under relevant conditions while handling meaningful benign and adversarial variations?
- **Operational usefulness:** Does the output provide enough reliable context and a workable investigation path for the security team?

These distinctions explain different aspects of detection condition; they are not additional assessment dimensions. The eight capability dimensions presented earlier form the proposed assessment structure.

### Example Conditions

| Observed situation | What it establishes | What it does not establish | Dimensions to examine |
| --- | --- | --- | --- |
| A scheduled rule executes without errors. | The execution path completed. | The rule received adequate telemetry or would detect the intended activity. | Detection Observability, Telemetry Readiness |
| A positive test generates the expected alert. | The rule matched the tested behavior under those test conditions. | It covers meaningful variants or avoids benign matches in production. | Detection Logic, Validation Evidence |
| The rule matches known malicious behavior but also alerts on routine administration. | The target behavior is detectable, but the distinction from authorized activity is weak. | The alert is consistently useful to analysts. | Behavior Definition, Detection Logic, Analyst Actionability |
| Enrichment is missing or stale, while the rule still fires. | An output may be produced despite degraded context. | The finding can be interpreted or routed reliably. | Operational Context, Analyst Actionability, Detection Observability |
| Alert volume drops to zero after a parser change. | An operational change warrants investigation. | The detection is broken: silence alone does not prove failure. | Telemetry Readiness, Detection Observability, Validation Evidence |
| The rule triggers correctly but gives analysts no clear next step. | The rule can produce a technically valid signal. | The signal supports a useful or sustainable response. | Analyst Actionability, Operational Context |
| A detection passed validation months ago but its data source has changed. | Historical validation evidence exists. | That evidence still represents the current environment. | Validation Evidence, Telemetry Readiness, Lifecycle Maintainability |
| The rule works but requires a costly query and repeated manual tuning. | Functional detection is possible. | The capability is economical to operate over time. | Lifecycle Maintainability, Detection Observability |

### Interpreting These Examples

- Do not call a detection healthy solely because it is enabled, executes successfully, or has recently alerted.
- Do not equate a quiet detection with a failed one. Compare observed behavior with expected activity, telemetry availability, execution results, and test evidence.
- Do not treat a successful positive test as proof of broad detection effectiveness. Record the tested scope and limitations.
- Distinguish **observations** (what was measured), **condition findings** (what the evidence supports), and **unknowns** (what has not been established).
- Preserve dimension-level differences so a functioning rule can still be flagged for limited effectiveness, inadequate context, or maintenance burden.

These cases are intended to guide practitioner discussion and future assessment design. They are examples, not a validated grading rubric or a claim that any specific detection has these conditions.

## Model Principles

### Condition is not confidence

The condition of a detection and confidence in that judgment are separate concepts.

A weak condition may be supported by strong evidence. A seemingly strong condition may still have limited supporting evidence.

### Unknown is not failure

Insufficient evidence should remain visible as an unknown rather than being treated as a weak or failed condition.

Unknowns help identify where additional evidence or investigation is needed.

### Preserve dimension-level differences

Detection Capability should not be reduced to a simple average or single composite score.

A detection may be strong in one dimension and weak in another. Those differences are important for understanding where engineering attention is needed.

### Keep source information in Detection Attributes

The model should interpret the information maintained in Detection Attributes rather than duplicate detection-level facts.

### Keep derived conclusions traceable

Any condition, finding, or analytical conclusion should remain traceable to the attributes and evidence that support it.
