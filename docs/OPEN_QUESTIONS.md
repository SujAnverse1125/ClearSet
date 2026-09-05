# ClearSet Planning Questions and Answers

The questions below were raised during planning. They now have working answers so implementation can begin. The answers are intentionally conservative and can be revised after testing with real datasets.

## Product

- **First test case:** Choose one real CSV or Parquet dataset from a personal project before implementation.
- **Smallest useful workflow:** Profile it, detect missing values and duplicates, preview one selected fix, validate it, create a version, and export the result.
- **Expected size:** Support small and medium local files first; measure the actual bottleneck before selecting a distributed engine.
- **Deployment:** Local-only first, with hosted workspaces as a later deployment mode.

## Cleaning behavior

- **Safe recommendations:** Standardize column names, normalize casing, detect duplicates, report missing values, and suggest type conversions when confidence is high.
- **High-risk operations:** Dropping rows, changing identifiers, imputing labels, and modifying target or feature columns.
- **Conflicting recommendations:** Present alternatives with evidence, risk, affected-row count, and expected quality impact; require an explicit choice.
- **Lineage identifiers:** Use a stable row identifier when available; otherwise store a reproducible selection rule and parent/output hashes.

## Quality

- **First rules:** Missingness, types, ranges, formats, categories, duplicates, uniqueness, consistency, and integrity.
- **Rule format:** Start with Pandera and structured JSON; add UI rule editing after the core workflow works.
- **Score configuration:** Use explainable defaults and allow project-level weights later.
- **Type overrides:** Let users override inferred types in a saved project schema.

## Machine learning

- **ML framework:** Keep the first ML module framework-neutral and operate on tabular data.
- **Target and split:** The user selects the target column and configures or supplies the train/test split.
- **Cleanlab:** Keep it optional until the general data-quality workflow is stable.
- **First ML checks:** Label validity, train/test overlap, target leakage indicators, class imbalance, and exact or near duplicates.

## Security and privacy

- **Sensitive data:** Assume that personal projects may contain PII and avoid sending local data to external services by default.
- **Hosted requirement:** PII detection, encryption, access control, and deletion policies are required before hosted deployment.
- **Deletion:** Deleting a dataset must remove its original, versions, reports, previews, and metadata, subject to backup retention.
- **Accounts:** Add accounts and workspace permissions when collaboration or hosted storage begins.

## Operations

- **Worker threshold:** Begin with direct execution and move to background jobs when files or concurrent operations make the API unresponsive; measure this threshold.
- **Performance metrics:** Track profiling time, transformation time, memory use, queue time, failure rate, and rows processed per second.
- **Retention:** Keep data until the user deletes it locally; make hosted retention configurable.
- **Backup:** Hosted deployments need scheduled metadata and object-storage backups plus a tested restore procedure.

## Release quality

- **Fixtures:** Include a real representative dataset plus small synthetic cases for missing values, types, duplicates, invalid values, and outliers.
- **Connector tests:** Test format detection, schema inference, sampling, reading, writing, encoding, malformed input, and round trips.
- **Determinism:** Run the same recipe twice and compare output hashes, schema, row counts, and quality results.
- **Visible failures:** Show failed jobs, validation failures, unsupported types, malformed files, resource limits, and rollback status.

## Revisit triggers

Revisit these answers after the first real dataset, when local processing becomes slow, when more than one user needs access, or before accepting sensitive data in a hosted environment.