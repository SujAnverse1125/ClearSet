# ClearSet Roadmap

## Phase 0: foundation

- Create repository structure
- Define domain models and transformation format
- Add documentation and coding standards
- Choose a representative real dataset

## Phase 1: personal MVP

- Local execution
- CSV and Parquet support
- Dataset registration
- Automatic profiling
- Missing-value and duplicate detection
- Basic type and validity checks
- Explainable recommendations
- Safe preview
- Approved transformations
- Output validation
- Immutable versions
- Local audit history
- Export cleaned file and JSON recipe

## Phase 2: reproducibility

- JSON and Excel support
- Saved cleaning recipes
- Python export
- SQL export where supported
- Version comparison
- Restore and branching from previous versions
- Custom schemas and validation rules

## Phase 3: web interface

- FastAPI backend
- React and TypeScript interface
- Dataset catalog
- Job progress
- Interactive table preview
- Quality reports
- Recommendation approval workflow
- Version timeline

## Phase 4: ML quality

- Label checks
- Leakage checks
- Class imbalance reports
- Near-duplicate detection
- Train/test overlap checks
- Cleanlab integration

## Phase 5: scale and collaboration

- PostgreSQL metadata
- S3 or MinIO storage
- Redis job queue
- Multiple workers
- Authentication and workspaces
- Permissions and project settings
- Scheduled checks
- API access and webhooks

## Definition of done for the first release

A real dataset can be profiled, issues can be understood, a fix can be previewed, the approved result can be validated and versioned, and the complete operation history can be reproduced without changing the original file.