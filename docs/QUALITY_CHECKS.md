# Quality and ML Checks

## Standard checks

### Completeness

- Missing values
- Empty strings
- Null-heavy columns
- Missing required records

### Validity

- Invalid data types
- Values outside expected ranges
- Invalid dates
- Failed regular expressions
- Unexpected categories

### Uniqueness

- Exact duplicate rows
- Duplicate identifiers
- Repeated business keys

### Consistency

- Conflicting values for the same entity
- Inconsistent categories or casing
- Mixed units or formats
- Column relationships that do not hold

### Integrity

- Broken references
- Invalid primary-key candidates
- Unexpected row-count changes
- Schema mismatch between versions

## Quality score

The score must be explainable. A possible initial model is:

```text
quality_score =
  completeness * 0.30
  + validity * 0.25
  + uniqueness * 0.20
  + consistency * 0.15
  + integrity * 0.10
```

The UI should display each component rather than showing only one unexplained number. Weights should eventually be configurable by project.

## Machine-learning checks

ML checks should initially produce warnings and recommendations, not automatic changes.

### Labels

- Missing labels
- Invalid labels
- Unknown classes
- Conflicting labels for similar records
- Suspiciously ambiguous examples

### Leakage

- Target column included in features
- Future or post-outcome fields
- Train and test overlap
- Derived fields that reveal the target

### Imbalance

- Class distribution
- Minority-class percentage
- Rare or absent classes
- Suggested sampling or weighting strategies

### Duplicates

- Exact duplicates
- Near duplicates
- Duplicate records across train and test splits

Cleanlab and other specialized libraries should be integrated where appropriate instead of reimplementing advanced algorithms immediately.

## Validation policy

Every transformation has a precondition and postcondition. A transformation that breaks required schema or integrity rules cannot be published as a valid version.

## Type and invalid-value detection

The system should infer candidate types, measure parse success, and test values against schema constraints. It should show representative failures rather than silently coercing them. A type conversion or invalid-value replacement becomes a recommendation with confidence, affected-row count, and risk level.

Low-confidence findings remain warnings. ClearSet does not automatically modify uncertain values.