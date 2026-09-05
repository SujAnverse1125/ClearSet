# ClearSet Scaling Plan

## Scaling principles

1. Start as a modular monolith.
2. Keep processing workers stateless.
3. Store metadata separately from dataset files.
4. Never overwrite immutable dataset versions.
5. Represent transformations as structured plans.
6. Keep connectors behind a common interface.
7. Scale only after measuring the actual bottleneck.

## Stage 1: local single user

```text
Web UI or Streamlit
        |
FastAPI or local service
        |
Polars + DuckDB
        |
SQLite + local file storage
```

This supports personal CSV, Excel, JSON, and Parquet workflows.

## Stage 2: background jobs

Large operations move to workers through a queue:

```text
UI -> API -> Redis queue -> Worker pool -> Object or file storage
                  |
              PostgreSQL
```

Jobs need progress, cancellation, retries, idempotency, timeouts, and temporary-file cleanup.

## Stage 3: storage separation

PostgreSQL stores users, datasets, versions, jobs, issues, recipes, and audits. S3-compatible storage stores original files, generated versions, reports, previews, and exports.

Large datasets should not be stored inside PostgreSQL.

## Stage 4: processing scale

- Small files: Polars in memory
- Medium files: Polars streaming
- Large local files: DuckDB and partitioned Parquet
- Warehouses: SQL pushdown
- Distributed data: Spark or Ray only when required

The profiler and transformation interfaces should remain stable when the execution engine changes.

## Stage 5: collaboration

Add organizations, workspaces, projects, permissions, API keys, encrypted storage, usage limits, and dataset deletion policies.

## Scaling dimensions

### File size

Use sampling, streaming, partitioned files, and out-of-core processing.

### Concurrent users

Use multiple stateless API instances and worker autoscaling.

### Processing speed

Profile only changed versions, cache results, use columnar formats, and push work to DuckDB or a source database where possible.

### Reliability

Use durable job records, retries, checksums, health checks, structured logs, metrics, and backups.

## Future integrations

Scheduled checks, CI/CD validation, Airflow or Dagster, webhooks, database connectors, cloud warehouses, and machine-learning pipeline integrations should be added through adapters rather than hardcoded into the core.