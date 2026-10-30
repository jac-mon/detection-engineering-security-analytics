# Security Models

Security Models explores proposed approaches for interpreting structured detection information to support practitioner assessments and broader security analysis.

Each model examines a different detection engineering question, including individual detection conditions, relationships, dependencies, and coverage. The models may draw on [Detection Attributes](../detection-attributes/README.md) and other authoritative sources.

**Status:** Research and model development. Assessment methods, evidence requirements, and practical usefulness require further testing and validation.

## Proposed Models

| Model | Security Question | Focus |
|---|---|---|
| [Detection Capability](detection-capability/README.md) | What is the current condition of this detection? | Examines individual detection conditions across technical and operational dimensions. |
| [Analytic Story](analytic-story/README.md) | How do related detections collectively address a shared security problem? | Examines behavioral coverage, detection relationships, shared dependencies, and collective findings. |
| [Security Telemetry](security-telemetry/README.md) | What telemetry can support security detection and analysis? | Explores telemetry characteristics, requirements, availability, and relationships to detection capability. |

## Model Relationships

The models examine detection information at different levels.

**Detection Capability** focuses on an individual detection and the evidence supporting its condition.

**Analytic Story** examines how related detections contribute to a shared defensive objective and where collective weaknesses or dependencies may exist.

**Security Telemetry** explores the supporting data sources and telemetry characteristics needed for detection and analysis. Its scope and relationship to existing detection attributes remain under development.

Models may reference common information without maintaining duplicate detection records.

## Model Principles

- **Reference source information.** Detection-level facts and evidence should remain in Detection Attributes or their authoritative systems.
- **Preserve analytical boundaries.** Each model should address a defined question without duplicating the responsibilities of another model.
- **Keep conclusions traceable.** Assessments and findings should identify the supporting information and evidence.
- **Preserve uncertainty.** Insufficient evidence should remain visible rather than being treated as a confirmed weakness.
- **Support further analysis.** Model information may contribute to derived measurements and analytical views in [Security Analytics](../security-analytics/README.md).

## Current Development

The models are at different stages of research and development. Some have proposed structures and assessment methods, while others remain exploratory.

Further research and practical testing will examine whether these approaches support consistent practitioner assessments, meaningful relationships, and useful analytical findings.

Model-specific limitations and open questions are documented in their respective sections.
