# Competency Questions - SPARQL Queries

This directory contains SPARQL query implementations for the 13 canonical competency questions (CQs) defined in the MQTO paper (Section 3).

## Structure

Each query file follows the naming convention: `CQ-{number}-{short-description}.rq`

## Competency Questions

1. **CQ-01**: Which causes are responsible for a given failure, and with what probability?
2. **CQ-02**: Which metrics and failures are related to each other?
3. **CQ-03**: Which signals, data, etc., are associated with a given metric?
4. **CQ-04**: Which failures occurred how often in a defined context?
5. **CQ-05**: Which countermeasures and execution steps are associated with a failure or were carried out?
6. **CQ-06**: What is the temporal progression of a given metric? Which data was it based on?
7. **CQ-07**: Which measurement data are available for a given item?
8. **CQ-08**: Which processes and items were active in a given context?
9. **CQ-09**: Which metrics have already been evaluated in a given context?
10. **CQ-10**: Which metrics triggered which failures?
11. **CQ-11**: How is a metric calculated?
12. **CQ-12a**: Which countermeasures can resolve a given failure directly or indirectly? **CQ-12b**: Which countermeasures are most likely to directly resolve a given failure?
13. **CQ-13**: Which failure occurrences were dismissed, and which countermeasure or step executions were aborted?

## Compatibility

`CQ-12-countermeasure-ranking.rq` remains available for existing scripts, with
its original result columns and behavior. New integrations should use
`CQ-12a-countermeasures.rq` for direct and indirect discovery, or
`CQ-12b-countermeasure-ranking.rq` for ranking direct countermeasures by weight.
The legacy query's `causalStrength` column is not a general causal ranking;
use CQ-01 to rank failure causes.

`mqto:weight` accepts both `xsd:decimal` (including integer datatypes) and
`xsd:double`. Existing integer weights do not need conversion.

The window properties `mqto:itemWindowSize` and `mqto:timeWindowSize` now apply
to either `mqto:Metric` or `mqto:FailureMode`. A window alone no longer entails
that its subject is a `mqto:Metric`. Explicitly declare the intended type;
existing explicitly typed metrics remain supported. This is an inference
change for data that relied solely on the old property domains.

`mqto:lowerBound`, `mqto:upperBound`, `mqto:calculatedValue`, and `mqto:score`
also accept both `xsd:decimal` (including integer datatypes) and `xsd:double`.
This preserves existing double-typed data while accepting the example data's
original decimal literals without conversion. A Turtle literal such as `680.0`
is an `xsd:decimal`, not an `xsd:double`.

## Usage

These queries demonstrate the queryability of the MQTO ontology. They are referenced in the paper's evaluation section (Section 6) as evidence that the ontology successfully answers the requirements-driven competency questions.

### Example with Jena ARQ:

```bash
# Execute a query against the example dataset
sparql --data=example-data.ttl --query=CQ-02-metrics-failures.rq
```

### Example with SPARQL endpoint:

```bash
# Query remote endpoint
curl -X POST -H "Content-Type: application/sparql-query" \
  --data-binary @CQ-02-metrics-failures.rq \
  http://your-endpoint/sparql
```

## Query Modifiers

The paper defines several modifiers that can be combined with canonical CQs:

- **plantScope**: Filter by Machine, Material, or Method
- **timeFilter**: Temporal filtering (time interval, latest, relative window)
- **itemHistoryFilter**: Filter by item identifier, sequence, or batch
- **statusFilter**: Filter by threshold values (normal, warning, out-of-tolerance)
- **failureFilter**: Filter by failure mode or actual failure IDs
- **outputMode**: Answer format (list, table, count, exists)

These modifiers can be applied by extending the queries with additional FILTER clauses or by using SPARQL query patterns.
