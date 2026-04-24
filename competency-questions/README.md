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
12. **CQ-12**: Which countermeasures are most likely to resolve a given failure?
13. **CQ-13**: Was a detected failure or a suggested countermeasure rejected by the user?

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
