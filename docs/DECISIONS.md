# ClearSet Decisions

This file records the current answers to the product and architecture questions discussed so far.

## Product decisions

| Question | Current answer |
| --- | --- |
| First user | The project owner and personal-project users |
| Product style | Local-first, privacy-friendly dataset assistant |
| First formats | CSV and Parquet |
| Later formats | Excel, JSON, databases, and object storage |
| First deployment | Local application |
| Main workflow | Profile, detect, recommend, preview, approve, validate, version, export |
| Automatic changes | Not allowed without user approval |
| Original dataset | Never overwritten |
| Versioning | Immutable versions with parent references |
| ML checks | Later module; warnings and recommendations first |

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