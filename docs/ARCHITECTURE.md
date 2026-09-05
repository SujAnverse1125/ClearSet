# ClearSet Architecture

## Architectural style

ClearSet starts as a modular monolith with clear internal boundaries. This is simpler to develop and deploy than microservices while preserving the interfaces needed to separate services later.

## Detailed component flow

### Visible architecture flow

```text
User
  -> React web interface
  -> FastAPI application API
	  -> Authentication and file security
	  -> Dataset catalog
	  -> Job manager
	  -> Audit and lineage service
		  -> Direct execution or Redis queue
			  -> Stateless processing worker
				  -> Connector manager
				  -> Schema registry
				  -> Profiling engine
				  -> Issue detection
				  -> Recommendation engine
				  -> Transformation planner
				  -> Safe preview
				  -> Transformation engine
				  -> Validation engine
					  -> Immutable dataset version
						  -> Versioned data and reports
```

The Mermaid version below provides the rendered visual form of the same architecture.

```mermaid
flowchart TB
	User[User] --> UI[React Web Interface]
	UI --> API[FastAPI Application API]

	API --> Security[Authentication and File Security]
	API --> Catalog[Dataset Catalog]
	API --> Jobs[Job Manager]
	API --> Audit[Audit and Lineage Service]

	Jobs --> Queue[Direct Execution or Redis Queue]
	Queue --> Worker[Processing Worker]

	Worker --> Connector[Connector Manager]
	Connector --> CSV[CSV]
	Connector --> Excel[Excel]
	Connector --> JSON[JSON]
	Connector --> Parquet[Parquet]
	Connector --> Database[Database]

	Worker --> Schema[Schema Registry]
	Worker --> Profiler[Profiling Engine]
	Worker --> Detector[Issue Detection]
	Worker --> Recommender[Recommendation Engine]
	Worker --> Planner[Transformation Planner]
	Worker --> Preview[Preview Runner]
	Worker --> Transformer[Transformation Engine]
	Worker --> Validator[Validation Engine]

	Validator --> Version[Immutable Dataset Version]
	Catalog --> Metadata[(SQLite or PostgreSQL)]
	Audit --> AuditDB[(Audit Database)]
	Connector --> Raw[(Original Data)]
	Version --> Outputs[(Versioned Data and Reports)]
```

The system has two logical planes:

### Control plane

Responsible for coordination and metadata:

- API requests
- Dataset catalog
- Users and permissions
- Job records
- Transformation plans
- Dataset versions
- Audit events
- Reports and status

### Data plane

Responsible for reading and processing data:

- Format connectors
- Sampling
- Profiling
- Issue detection
- Recommendations
- Transformations
- Output validation
- Report generation

## Component responsibilities

### Web interface

Provides dataset upload, profiling views, recommendations, previews, version history, reports, and exports. It should never implement cleaning logic itself.

### API

Validates requests, authorizes access, creates jobs, returns status, and exposes metadata. Large processing must run in workers rather than blocking API requests.

### Connector manager

Presents a common interface for CSV, Excel, JSON, Parquet, databases, and object storage. Profilers and transformers should consume a standard dataset abstraction rather than format-specific code.

### Profiling engine

Calculates row and column counts, inferred types, missingness, uniqueness, distributions, date ranges, constants, duplicates, and possible identifiers.

### Issue detection engine

Finds problems but does not change data. Issues have a type, severity, affected columns, affected rows, evidence, and confidence.

### Recommendation engine

Converts issues into possible actions with explanations, risk levels, expected effects, and reversibility information.

### Transformation engine

Executes approved structured operations. It should produce deterministic output and record the affected rows and columns.

### Validation engine

Runs schema, integrity, and quality checks before and after transformations. A failed output is discarded rather than published as a new valid version.

### Versioning and storage

Original data and every generated version are immutable files. Metadata stores the parent version, operations, hashes, statistics, and validation results.

## Processing contract

Workers should receive a dataset location, parent version, transformation plan, and configuration. They should return an output location, result metadata, validation results, and audit events. This keeps workers stateless and makes horizontal scaling possible.

The API should never depend on a particular dataframe library. The processing boundary should expose operations such as `inspect`, `sample`, `profile`, `validate`, `transform`, and `export`. Polars, DuckDB, SQL pushdown, or a distributed engine can implement these operations later.

## Reliability boundaries

- Uploads are checked for size, type, encoding, and safe paths before parsing.
- Original files and published versions are immutable.
- Jobs have queued, running, completed, failed, and cancelled states.
- Retries are idempotent and cannot silently create duplicate versions.
- Temporary outputs are cleaned up after success or failure.
- Failed validation prevents a result from becoming a published version.
- Structured logs, metrics, health checks, backups, and migrations are required before hosted deployment.

## Technology direction

Initial local stack:

- FastAPI
- Polars
- DuckDB
- Pandera
- SQLite
- Local file storage

Growth path:

- SQLite to PostgreSQL
- Local files to S3 or MinIO
- In-process jobs to Redis-backed workers
- One worker to multiple workers
- Polars-only processing to Polars, DuckDB, and SQL pushdown