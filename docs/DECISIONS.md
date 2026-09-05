# ClearSet Decisions

This file records the current answers to the product and architecture questions discussed so far.

## Product decisions

| Question | Current answer |
| --- | --- |
| First user | The project owner and personal-project users |
| Product style | Local-first, privacy-friendly dataset assistant |
| First formats | CSV and Parquet |
| First-release file limit | Configurable 2 GB per file, with sampling and streaming where supported |
| Later formats | Excel, JSON, databases, and object storage |
| First deployment | Local application |
| Main workflow | Profile, detect, recommend, preview, approve, validate, version, export |
| Automatic changes | Not allowed without user approval |
| Original dataset | Never overwritten |
| Versioning | Immutable versions with parent references |
| ML checks | Later module; warnings and recommendations first |
| Essential version-one cleaning | Standardize names, normalize text casing, convert approved types, handle missing values, remove or flag exact duplicates, and validate ranges and formats |

## Technical decisions

| Area | Initial choice | Growth path |
| --- | --- | --- |
| API | FastAPI | Multiple stateless API instances |
| Processing | Polars | DuckDB, SQL pushdown, distributed engines if needed |
| Validation | Pandera | Custom rule registry and project schemas |
| Metadata | SQLite | PostgreSQL |
| File storage | Local directories | S3 or MinIO |
| Jobs | Direct or synchronous for small files | Redis-backed worker queue |
| Transformation format | Structured JSON plan | Multiple execution backends |
| UI | Simple web interface | React and TypeScript application |

## Safety decisions

- Validate uploads before parsing.
- Preserve the original input.
- Show affected rows and columns before applying a change.
- Validate previews and final outputs.
- Record hashes, parent versions, operations, and results.
- Discard failed outputs rather than publishing them.
- Treat ML findings as warnings unless the user explicitly approves an action.
- Do not modify a source database directly in the first release; create a version or export instead.

## Quality-score decision

The score must expose its components. It should not be a black-box number. Initial components are completeness, validity, uniqueness, consistency, and integrity. Weights can become configurable later.

## Naming decision

The working product name is ClearSet. The planned repository is `SujAnverse1125/ClearSet`. Repository, package, domain, and trademark availability should be checked before public release.

## Planning answers

| Question | Answer for the current project |
| --- | --- |
| First representative dataset | A real CSV or Parquet dataset from a personal project, selected before implementation begins |
| First useful workflow | Profile, detect missing values and duplicates, preview a selected fix, validate it, create a version, and export it |
| Expected first-year size | Small and medium files that fit local processing; large-file limits will be measured rather than guessed |
| Deployment direction | Local-only for the first release, with a future hosted mode |
| Automatic recommendations | Allowed; automatic application is not allowed |
| High-risk operations | Dropping rows, changing identifiers, imputing labels, and changing target or feature columns |
| Conflicting recommendations | Show alternatives with evidence, risk, affected-row counts, and require an explicit choice |
| Lineage identifiers | Use a stable row identifier when present; otherwise store reproducible row-selection rules and dataset hashes |
| Built-in rules | Missingness, types, ranges, formats, categories, duplicates, uniqueness, consistency, and integrity |
| Custom rules | Start with Pandera or structured JSON rules; add UI rule editing later |
| Rule configuration | Project-level configuration, with explainable default quality-score weights |
| ML target and split | User selects the target and supplies or configures the train/test split |
| ML dependencies | Keep Cleanlab optional until the core data workflow is stable |
| PII handling | Detect and warn before hosted deployment; masking and encryption are required for hosted sensitive data |
| Background processing | Direct execution for small files; background workers when size or concurrency makes it necessary |
| Retention | Keep originals and versions until the user deletes them; hosted deployments need configurable retention and backups |
| Transformation testing | Use representative fixtures, edge cases, deterministic-output tests, and connector contract tests |

## User-experience answers

| Question | Answer for the current project |
| --- | --- |
| Main journey | Upload or select dataset, review profile, inspect issues, select recommendations, preview changes, approve, validate, version, and export |
| First screen | Dataset name, row and column counts, quality-score components, highest-severity issues, missingness summary, duplicate count, and primary actions |
| Individual row inspection | Show a before-and-after table with changed cells highlighted, filters for affected rows, and the operation responsible for each change |
| Version comparison | Compare schemas, row and column counts, quality components, changed columns, affected rows, and representative before-and-after samples |
| Recipe reuse | Save recipes per project, apply them to compatible future datasets, and stop with a schema mismatch report when they are incompatible |

## Risk and uncertainty answers

| Question | Answer for the current project |
| --- | --- |
| Risk levels | Low: formatting or labels; medium: type conversion or imputation; high: dropping rows, changing identifiers, labels, target, or features |
| Low-confidence detection | Report the issue as a warning with evidence and confidence; do not recommend automatic application below the configured threshold |
| Always-reversible changes | Every local transformation is reversible through immutable parent versions; direct external database writes are not supported initially |
| Incorrect types and invalid values | Infer candidate types, test parse success and constraints, report failed values with examples, and require approval for coercion or replacement |

## Security and integration answers

| Question | Answer for the current project |
| --- | --- |
| PII | Local datasets may contain PII; local processing stays on the user machine by default |
| PII detection and masking | Required before hosted sensitive-data support; masking is optional and user-approved locally |
| Accounts and permissions | Not required for the personal MVP; required for hosted workspaces and collaboration |
| Encryption | Local mode relies on OS file permissions; hosted mode requires TLS in transit and encrypted storage at rest |
| Permanent deletion | Delete original files, versions, previews, reports, recipes, metadata, and queued jobs, then apply the hosted backup-retention policy |
| Metadata and audit store | SQLite locally; PostgreSQL for hosted deployment, with audit events in the same transactional metadata system initially |
| Dataset files | Local versioned directories initially; S3 or MinIO for hosted deployment |
| External API | Not required for the MVP; expose a versioned API before integrations and hosted automation |
| Scheduled checks | Later capability for local schedules and hosted workers |
| Orchestration integrations | Later adapters for Airflow, Dagster, Prefect, CI/CD, and webhooks |

## Reliability and scaling answers

| Question | Answer for the current project |
| --- | --- |
| First scaling limit | File size and local memory are expected before concurrent users; measure profiling and transformation memory first |
| Large-file processing | Sample for profiling, stream where supported, use DuckDB and Parquet for out-of-core work, and move to workers when responsiveness drops |
| Job retry and cancellation | Retry only idempotent jobs with bounded attempts; cancellation marks the job and cleans temporary outputs |
| Common transformation plan | Store operations as versioned JSON with engine-neutral types; Polars, DuckDB, SQL, or future engines interpret the same plan |