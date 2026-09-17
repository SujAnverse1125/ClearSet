# ClearSet Roadmap

## Phase 0: validation script

- Choose one real CSV and one real reviewer
- Write a plain Python script with no framework
- Profile, detect, recommend, preview, apply, validate, version, and export
- Record a minimal attribution event for every applied or rejected change
- Gate: the script runs correctly on messy real data and produces evidence a real user understands

## Phase 1: deterministic CLI

- Turn the Phase 0 script into a reusable CLI
- CSV support and then Parquet if justified by the validation dataset
- Structured transformation plans as the stable product primitive
- Deterministic profiling, issue detection, recommendations, preview, approval, validation, versions, attribution, and export

## Phase 2: API wrapper

- FastAPI and SQLite around the proven engine
- `/docs` usable manually
- Saved recipes, version comparison, and custom validation rules

## Phase 3: review interface

- React and TypeScript interface
- Dataset and version catalog
- Interactive table preview
- Quality reports
- Approval and rejection workflow with reasons
- Version timeline

## Phase 4: hosted team hypothesis

- Shared workspace and multi-reviewer approval
- Hosted storage, permissions, retention, and audit export
- Enter this phase only after a defined customer reports measurable review value and a recurring shared-workflow need
- Validate willingness to pay before expanding infrastructure

## Phase 5+: scale and integrations

- PostgreSQL metadata
- S3 or MinIO storage
- Redis job queue
- Multiple workers
- Authentication and workspaces, if Phase 4 is validated
- Scheduled checks
- API access, webhooks, ML checks, and database integrations

## Definition of done for the first release

A real dataset can be profiled, issues can be understood, a fix can be previewed, the reviewer can approve or reject it with a reason, the approved result can be validated and versioned, and the complete attributed history can be reproduced without changing the original file.