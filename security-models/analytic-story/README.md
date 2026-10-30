# Analytic Story

Analytic Story explores how related detections may be examined together around a shared security question or defensive objective.

> How do related detections collectively address a shared security problem?

The proposed model considers detection relationships, behavioral coverage, potential gaps, and shared dependencies.

An Analytic Story is a conceptual analytical model, not an executable detection rule. Its intended purpose is to support examination of collective detection capability and findings that may not be apparent when reviewing individual detections.

**Status:** Conceptual model under development. The proposed analytical methods require further examples, practitioner review, testing, and validation.

## Model Relationships

An Analytic Story sits above individual detections and references information maintained in Detection Attributes rather than duplicating detection-level facts.

```text
Domain
  ↓
Analytic Story
  ↓
Detection
  ↓
Detection Attributes
```

A detection may contribute to one or more Analytic Stories.

Examining related detections through an Analytic Story may reveal relationships, limitations, or areas requiring further investigation.

## Story Components

### Security Question

Defines the security problem or defensive objective that the Analytic Story intends to address.

The question should be broad enough for multiple detections to contribute, but narrow enough to support meaningful coverage analysis.

### Composition

Identifies the detections contributing to the story and describes their relationship to the shared objective.

Possible relationships include:

- **Primary:** Directly identifies behavior central to the objective.
- **Supporting:** Identifies related behavior that contributes additional detection coverage.
- **Correlation:** Connects related observations or detection signals.
- **Contextual:** Provides information that supports interpretation of other detection outputs.

These relationships describe each detection's contribution. They do not imply that the Analytic Story executes or combines the underlying rules.

### Coverage

Examines how contributing detections address the behaviors within the story's intended scope.

Coverage analysis should distinguish:

- **Expected behaviors:** Relevant behaviors identified as part of the defensive objective.
- **Covered behaviors:** Behaviors addressed by contributing detections within an established scope and supported by sufficient evidence.
- **Partially covered behaviors:** Behaviors addressed only under certain conditions, environments, or variants.
- **Uncovered behaviors:** In-scope behaviors for which no applicable detection capability has been identified.
- **Unknown coverage:** Behaviors for which available information is insufficient to determine coverage.

Coverage should reflect more than a detection's existence or MITRE ATT&CK mapping.

A mapped detection does not establish that the intended behavior can be detected reliably in production.

### Dependencies

Identifies shared or related components that detections require to operate as intended.

Dependencies may include:

- Telemetry sources and required fields
- Parsers and normalization processes
- Lookups and enrichment services
- Supporting platforms, services, or controls

Dependency analysis can help practitioners understand which detections may be affected by changes or failures in supporting components.

Shared dependencies should not automatically be classified as weaknesses. Their significance depends on how each detection uses the component, whether alternatives exist, and the consequences of degradation or failure.

### Evidence

Identifies evidence supporting claims about detection coverage, dependencies, and collective capability.

Evidence may include:

- Detection validation results
- Telemetry assessments
- Operational observations
- Dependency documentation
- Relevant investigation findings

Evidence should remain traceable to the underlying detection or supporting record.

Where evidence is insufficient, the resulting uncertainty should remain visible.

### Findings

Captures weaknesses, limitations, unknowns, and other observations identified at the Analytic Story level.

Examples include:

- Incomplete behavioral coverage
- Shared dependency weaknesses
- Redundant or complementary coverage
- Missing investigation context
- Validation gaps affecting multiple detections
- Potential change impact across related detections

Findings should identify their supporting evidence and affected detections or dependencies.

## Cross-Detection Analysis

Cross-detection analysis examines relationships between contributing detections that may influence the collective defensive objective.

The following analytical concepts are proposed for further development.

### Behavioral Coverage Analysis

**Question:** Which relevant behaviors can the contributing detections address, and where does coverage remain incomplete or unknown?

The practitioner identifies the behaviors relevant to the story's security question and examines the detections associated with each behavior.

This supports analysis of:

- Behaviors addressed by existing detections
- Behavioral variants or environments not fully addressed
- Behaviors without an identified detection
- Coverage claims requiring further validation

Expected behavioral scope provides a reference point for coverage assessment.

Without that reference point, analysis may describe only existing detections rather than identify missing capabilities.

### Coverage Overlap Analysis

**Question:** Where do contributing detections address similar behaviors, and does that overlap provide additional defensive value?

Overlap may occur when detections identify similar activity through different logic, telemetry sources, or operating conditions.

Potential interpretations include:

- **Complementary coverage:** Detections address different aspects or variants of a behavior.
- **Independent coverage:** Detections use sufficiently independent mechanisms to provide an alternative means of detecting a behavior.
- **Redundant coverage:** Detections produce substantially similar signals without a clear additional benefit.
- **Unresolved overlap:** Available evidence does not establish whether the overlap is useful.

Overlap is not inherently undesirable. It may improve resilience or provide additional context.

Analysis should consider the contribution of each detection rather than use detection counts as a measure of coverage quality.

### Dependency Concentration Analysis

**Question:** Which supporting components are shared across detections, and what could be affected if those components change or fail?

The practitioner examines relationships between detections and their required dependencies.

Potential findings include:

- Multiple detections relying on the same telemetry source
- Shared normalization or parsing requirements
- Common enrichment dependencies
- Components whose failure may affect several detections

Dependency concentration analysis may reveal potential exposure to shared changes or failures.

It does not establish a failure or weakness without examining dependency requirements, available alternatives, and operational evidence.

### Change-Impact Analysis

**Question:** Which contributing detections may require review or revalidation when a supporting component changes?

Changes may include:

- Telemetry source modifications
- Field or schema changes
- Lookup or enrichment changes
- Detection logic updates
- Platform configuration changes

The intended output is a set of potentially affected detections, their relevant dependencies, and the evidence or validation needed to understand the impact.

Change-impact analysis identifies reassessment candidates rather than automatically classifying detections as degraded.

## Practitioner Example

### Analytic Story: Potential Account Compromise

**Security question:** How do existing detections collectively identify suspicious identity activity that may indicate account compromise?

Example contributing detections:

| Detection | Intended contribution |
| --- | --- |
| D-001 — Suspicious Sign-In Location | Identifies authentication activity from unexpected geographic locations |
| D-002 — Unusual Authentication Failures | Identifies abnormal authentication failure patterns |
| D-003 — Suspicious Privilege Changes | Identifies potentially unauthorized privilege changes |

### Example Coverage Findings

| Behavior | Example assessment |
| --- | --- |
| Suspicious geographic authentication | Addressed by D-001 within its tested scope |
| Repeated authentication failures | Addressed by D-002 |
| Suspicious privilege changes | Addressed by D-003 |
| Session-token misuse | No contributing detection identified |
| Suspicious post-authentication activity | Not yet assessed |

These assessments are hypothetical. Actual coverage conclusions require review of detection scope and supporting evidence.

### Example Dependency Finding

D-001 and D-002 rely on a shared identity normalization process.

A change to that process may affect both detections.

In this hypothetical example, examining the relationship could help practitioners investigate:

- Which detections depend on the affected normalization process
- Which required fields or values may change
- Whether detection logic remains functional
- Whether additional validation is necessary

The shared dependency is a potential change-impact concern, not proof that either detection has failed.

### Example Collective Finding

The contributing detections address several identity-related behaviors, but the story does not yet establish coverage for session-token misuse.

This finding can support further research into the relevant behavior, available telemetry, existing controls, and whether additional detection engineering is warranted.

## Levels and Boundaries

### Detection vs. Analytic Story

A detection represents an individual analytic implementation.

An Analytic Story examines how related detections collectively contribute to a defensive objective.

Detection-level facts should remain in Detection Attributes. The story should reference and interpret those facts.

### Domain vs. Analytic Story

A domain represents a broad security area, such as Identity, Endpoint, Network, Cloud, or Email.

An Analytic Story represents a narrower defensive objective within or across those domains.

### Analytic Story vs. Security Analytics

The proposed Analytic Story model organizes relationships, scope, and findings around a shared security question.

Security Analytics may later use that information to derive measurements, identify patterns, and support portfolio-level decisions.

The Analytic Story should not duplicate calculations or derived states that belong in the analytics layer.

## Model Principles

### Use the security question as the organizing principle

Maintain a clear defensive objective and defined behavioral scope.

### Reference Detection Attributes

Keep detection-level facts in their authoritative records rather than maintaining duplicate information.

### Preserve differences between coverage and effectiveness

The existence of a detection does not establish that it reliably detects the intended behavior.

### Treat overlap as a relationship requiring interpretation

Overlapping coverage may be complementary, independent, redundant, or unresolved.

### Treat dependencies as part of collective capability

Shared components can influence multiple detections and may create change-impact or resilience considerations.

### Preserve uncertainty

Distinguish unsupported claims and unknown coverage from confirmed weaknesses.

### Keep findings traceable

Analytical conclusions should reference the detections, dependencies, and evidence that support them.

### Avoid simple roll-up scoring

Story condition should not be reduced to a simple average or single composite score. Preserve the underlying conditions and their significance.

## Record

The proposed [Analytic Story Record](analytic_story_record.md) outlines information that may be maintained for an individual Analytic Story.

The record should preserve story-level facts, relationships, findings, and references without duplicating detection-level information.

## Research Questions

The following questions remain open for practitioner review:

1. How should expected behaviors be represented without creating an overly complex coverage taxonomy?
2. What evidence is sufficient to classify behavior as covered, partially covered, or uncovered?
3. How should meaningful overlap be distinguished from unnecessary redundancy?
4. What information is needed to establish whether shared dependencies create a common failure point?
5. Which relationship and dependency fields should be maintained, referenced, or derived?
6. How should changes to a dependency trigger review of affected detections?
7. Which cross-detection findings warrant engineering work, and which should remain informational?
8. How should story-level findings later connect to Security Analytics without duplicating conclusions?
