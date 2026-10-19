# Manufacturing Quality Troubleshooting Ontology (MQTO)

<img src="logo.png" alt="MQTO Logo" width="400"/>

**Namespace:** `https://w3id.org/mqto#`  
**Prefix:** `mqto`  
**Version:** 1.1.0 (in preparation)<br>
**Version URI:** `https://w3id.org/mqto/1.1` (publication pending)<br>
**Previous release (1.0.0) DOI:** [10.5281/zenodo.19571023](https://doi.org/10.5281/zenodo.19571023)

## Overview

The Manufacturing Quality Troubleshooting Ontology (MQTO) is a domain-independent **connector ontology** for manufacturing quality troubleshooting. It semantically links three disconnected information silos — quality management, quantitative data infrastructure, and production context — to enable traceable, queryable, and reusable cross-domain reasoning for root cause analysis, failure diagnosis, and countermeasure recommendation.

MQTO was developed following the Linked Open Terms (LOT) methodology and driven by 13 competency questions and 10 additional requirements derived from an industrial die-casting use case at TCG Unitech GmbH. It generalises working domain-specific implementations into domain-independent connector patterns applicable across discrete manufacturing processes.

## Architecture

MQTO occupies the middle layer in a three-layer architecture:

- **Upper layer:** LIS/IDO (production context), SOSA/SSN (observations), PKO (procedural knowledge)
- **Middle layer:** MQTO — domain-independent troubleshooting connector patterns
- **Lower layer:** Domain-specific application ontologies (e.g., die-casting, injection molding, CNC machining)

The central bridging role is played by the **Metric/MetricAssessment** concept, which connects quality management (failure modes, countermeasures) to the data infrastructure (signals, observations, actuations) under explicit production context (machines, materials, methods).

## Documentation

- **HTML Documentation & WebVOWL:** <https://w3id.org/mqto> (content-negotiated)
- **Source Repository:** <https://w3id.org/mqto/git>
- **Turtle File:** [mqto-1.1.ttl](./mqto-1.1.ttl)

The 1.1.0 release is in preparation. Published HTML documentation and diagrams
may still describe 1.0 until regenerated. Publication requires configuring
the `/1.1` persistent URI, finalizing the release date and DOI, and marking
the ontology as published. The stable namespace remains `https://w3id.org/mqto#`.
The 1.0.0 source remains available at the
[`v1.0.0` tag](https://github.com/dg-assist/mqto/tree/v1.0.0).

- **Class diagram:** [class-diagram.drawio.svg](./class-diagram.drawio.svg)
- **Module diagram:** [modules.drawio.svg](./modules.drawio.svg)

Both diagrams are SVG images that can also be edited in draw.io.

## Competency Questions

MQTO is validated against 13 canonical competency questions. SPARQL query implementations and an example dataset are available in [`competency-questions/`](./competency-questions/).

To run a query (requires [Apache Jena](https://jena.apache.org/)):

```bash
sparql --data=competency-questions/example-data.ttl --query=competency-questions/CQ-10-metric-failures.rq
```

## Extending MQTO

Adaptation to other manufacturing domains (e.g., injection molding, CNC machining, additive manufacturing) requires:

- Specialising `Machine`, `Material`, `Method` with domain-specific equipment types, material classes, and process operations
- Defining domain-relevant `FailureMode` types, `Metric` specifications, and `Signal` channels
- Creating `Countermeasure` libraries appropriate to the domain's remediation practices

The core connector structure remains unchanged.

## Acknowledgements

This work was conducted within the Austrian research project DG Assist (FFG project number: FO999899053), funded by the Federal Ministry for Climate Protection, Environment, Energy, Mobility, Innovation and Technology (BMK), carried out as part of the Production of the Future programme.

## Citation

See [CITATION.cff](./CITATION.cff) for machine-readable citation metadata.

## License

[Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0)

## Contributing

Community contributions are managed through GitHub Issues and Pull Requests. We welcome competency-question proposals, vocabulary alignment suggestions, and bug reports. The ontology follows semantic versioning: backwards-compatible additions are released as minor versions, while breaking changes require a new major version.

---

**Generated with:** [WIDOCO](https://github.com/dgarijo/Widoco) | [OnToology](https://ontoology.linkeddata.es/)
