# ClearSet Data Model

## Dataset

Represents a logical dataset across all of its versions.

```text
Dataset
  id
  name
  description
  source_type
  created_at
  owner_id
  current_version_id
```

## Dataset version

Represents an immutable file produced from a parent version.

```text
DatasetVersion
  id
  dataset_id
  parent_version_id
  storage_uri
  content_hash
  row_count
  column_count
  schema_id
  quality_score
  created_at
```

Versions form a history tree rather than an overwrite chain, so alternative cleaning approaches can be compared.

## Issue

```text
Issue
  id
  version_id
  type
  severity
  confidence
  column_names
  affected_row_count
  evidence
  detector_name
```

## Recommendation

```text
Recommendation
  id
  issue_id
  action_type
  explanation
  risk_level
  reversible
  estimated_effect
```

## Transformation plan

Operations must be structured rather than stored only as arbitrary code.

```json
{
  "operations": [
    {
      "type": "rename_column",
      "from": "Customer Name",
      "to": "customer_name"
    },
    {
      "type": "fill_missing",
      "column": "age",
      "strategy": "median"
    }
  ]
}
```

## Audit event

Records who or what performed an operation, when it happened, which version was used, and what was produced.

```text
AuditEvent
  id
  actor_id
  dataset_id
  parent_version_id
  new_version_id
  action
  operation_summary
  timestamp
  result
```

## Lineage

For each output column, store its source column and transformations. For important operations, record affected row identifiers or a reproducible selection rule.