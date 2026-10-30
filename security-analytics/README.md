# Security Analytics

Security Analytics explores how structured detection information, security models, and supporting evidence can be used to produce measurements, identify patterns, and inform detection engineering decisions.

The intended purpose is to help practitioners examine individual detections, relationships, and broader detection environments through analytical questions that may not be answered by reviewing individual records alone.

**Status:** Research area under development. The proposed analytical areas, measurement methods, and outputs require further definition, practical examples, and validation.

## Analytical Approach

Security Analytics distinguishes between measurements and their interpretation.

- **Metrics:** Quantitative measurements derived from defined source information, such as validation age or the number of detections sharing a dependency.
- **Analytics:** Methods that examine measurements, relationships, observations, and supporting evidence to answer a security engineering question.

An analytic may produce findings, identify conditions requiring review, or highlight areas where additional evidence is needed.

A metric alone does not establish the significance of an observed condition.

## Research Scope

Potential analytical areas include:

### Detection Condition and Validation

- Validation age and evidence sufficiency
- Detection execution and operational health
- Detection condition findings across capability dimensions
- Changes requiring reassessment or revalidation

### Telemetry and Dependencies

- Telemetry availability and quality findings
- Shared telemetry and enrichment dependencies
- Dependency concentration
- Potential change impact across dependent detections

### Coverage and Relationships

- Behavioral coverage and identified gaps
- Complementary, independent, or redundant detection coverage
- Cross-detection relationships and shared limitations
- Coverage findings requiring further investigation

### Maintenance and Portfolio Analysis

- Recurring maintenance needs
- Operational burden and investigation limitations
- Findings and unresolved conditions
- Trends across detections, Analytic Stories, and security domains

These areas are proposed research directions. They do not represent implemented analytics or validated measurement methods.

## Relationship to Detection Attributes and Security Models

### Detection Attributes

[Detection Attributes](../detection-attributes/README.md) maintains structured information about an individual detection.

Security Analytics may use those attributes and supporting evidence as inputs for measurements and analysis.

Derived results should reference their underlying records rather than duplicate source information.

### Security Models

[Security Models](../security-models/README.md) provides analytical structures for examining particular security questions.

Security Analytics may use model findings, relationships, and evidence to examine patterns across individual detections, Analytic Stories, and broader security areas.

The analytics layer should not reproduce assessments already maintained by the underlying models.

## Analytical Principles

- **Start with a defined question.** An analytic should explain what it is intended to examine and why the result may be useful.
- **Preserve traceability.** Measurements and findings should identify their supporting records, relationships, and evidence.
- **Distinguish observations from conclusions.** A measured change or unusual pattern does not automatically establish a detection failure or capability gap.
- **Preserve uncertainty.** Missing or insufficient evidence should remain visible in analytical outputs.
- **Avoid misleading aggregation.** Counts, averages, and composite scores should not conceal important differences between detections or their operating conditions.
- **Limit duplication.** Derived results should reference existing assessment information rather than create competing records.

## Research Considerations

Further development should examine:

1. Which analytical questions provide practical value to detection engineers and security teams?
2. What source attributes, relationships, and evidence are required to support each analytic?
3. How should analytical findings distinguish confirmed conditions, potential concerns, and insufficient evidence?
4. Which measurements can be calculated consistently across different detection types and environments?
5. How should analysis account for differences in detection scope, dependencies, and operational importance?
6. How can analytical outputs support engineering decisions without relying on a single composite score?

The initial focus should be on practical examples that demonstrate how structured detection information can produce useful, evidence-supported findings.
