# Detection Attributes

Detection Attributes explores how structured information about individual detections can support documentation, assessment, and analysis.

The proposed model organizes detection characteristics, environmental context, telemetry requirements, dependencies, validation evidence, operational observations, and maintenance needs.

Its intended purpose is to preserve information that may support detection engineering assessments and downstream security analytics.

**Status:** Proposed attribute model under development. The current template and catalog remain subject to refinement through practitioner review and practical examples.

## Files

| File | Purpose |
|---|---|
| [Attribute Catalog](attribute_catalog.md) | Defines proposed attributes, their purpose, classification, and maintenance approach. |
| [Detection Attributes YAML](detection-attributes.yaml) | Provides a structured template for recording detection information. |

The attribute catalog is a working design reference, not a formal schema. The YAML template reflects the current proposed structure.

## Practitioner Reading Flow

The attribute model is organized around questions practitioners may encounter when reviewing or maintaining a detection.

| Area | Practitioner question |
|---|---|
| Definition | What is the detection intended to identify? |
| Context | Where does the detection apply? |
| Telemetry | What data does the detection require? |
| Dependencies | What supporting components does it rely on? |
| Logic | How does the detection identify the intended behavior? |
| Validation | What evidence shows that the detection works as intended? |
| Actionability | Can an analyst understand and act on the output? |
| Observability | Can the team monitor execution and operational behavior? |
| Maintenance | What needs to be reviewed or updated over time? |

## Model Boundaries

The proposed structure is intended to organize source information, practitioner observations, and supporting evidence about an individual detection.

The model should not duplicate information already maintained in authoritative systems when references can preserve traceability.

Derived measurements, condition assessments, and analytical conclusions should remain separate from source attributes.

Related models, including [Detection Capability](../security-models/detection-capability/README.md) and [Analytic Story](../security-models/analytic-story/README.md), may use these attributes to support broader assessments.

## Current Development

The proposed fields and classifications remain under review.

Further development will examine:

- Which attributes are essential across detection types
- Which fields should be optional or context-dependent
- Which values should be maintained manually, referenced, or derived
- How the structure performs when applied to completed detection examples
- Whether the model supports useful assessments without excessive documentation overhead

The attribute model is intended to evolve as practical use reveals missing information, redundancy, or maintenance concerns.
