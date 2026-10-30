# Detection Engineering Security Analytics

Detection Engineering Security Analytics is an ongoing research project exploring how structured detection information can support visibility metrics, security analytics, and detection engineering decisions.

The project proposes approaches for organizing and maintaining detection attributes and supporting evidence, with the aim of developing metrics and analytics that may inform engineering priorities, maintenance, coverage planning, and detection strategy.

The proposed models and methods remain under development and require practical testing and validation. Questions, feedback, and contributions are welcome.

## Purpose

The project is intended to be read from the detection outward.

### 1. Detection Attributes

Detection Attributes proposes a structured approach for recording information about individual detections, including their behavior, dependencies, validation, and operational context.

**Definition → Context → Telemetry → Dependencies → Logic → Validation → Actionability → Observability → Maintenance**

[Detection Attributes YAML](detection-attributes/detection-attributes.yaml)

### 2. Analytical Models

Analytical Models explore how structured detection information may be used to examine detection capability, relationships, coverage, and supporting telemetry.

**Detection Capability**

> What is the current condition of this detection?

[Detection Capability](security-models/detection-capability/README.md)

**Analytic Story**

> How do related detections collectively address a shared security problem?

[Analytic Story](security-models/analytic-story/README.md)

**Security Telemetry**

> What telemetry can support security detection and analysis?

[Security Telemetry](security-models/security-telemetry/README.md)

### 3. Analytics and Metrics

The project explores how metrics and analytics may be developed from detection attributes, model findings, and supporting evidence to examine patterns, conditions, changes, and areas requiring attention.

Potential areas include:

- validation age
- telemetry condition
- detection condition
- dependency concentration
- coverage
- maintenance needs
- reassessment
- change impact
- portfolio trends

A metric measures something available from the underlying information. An analytic interprets what that measurement means in context.

[Security Analytics](security-analytics/README.md)

## Levels of Analysis

The project explores how structured detection information can provide visibility into detection capability, telemetry, coverage, and maintenance needs.

The goal is to develop metrics and analytics that help practitioners understand their detection environment, identify areas requiring attention, and inform detection engineering priorities and strategy.

**Detection**

- What behavior is this detection intended to identify?
- Is it functioning and producing useful results?
- What requires tuning, validation, or maintenance?

**Analytic Story**

- How do related detections address a shared security problem?
- Where are the behavioral gaps, overlaps, and shared dependencies?

**Domain**

- What telemetry is available, reliable, and relevant?
- Which behaviors can we observe, and where are visibility gaps?
- What detection capabilities are missing or need improvement?

**Portfolio**

- What is the current condition of the detection environment?
- What patterns exist across detection health, coverage, validation, and maintenance?

**Decision Support**

- What requires engineering attention, and why?
- What evidence supports the priorities?
- How can these findings inform detection planning and strategy?

## License

Research documentation is licensed under CC BY 4.0. Reusable templates and software are licensed under MIT.

See [Licensing](LICENSE.md) for details.
