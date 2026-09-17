# ClearSet Requirements Traceability

This file cross-checks the capabilities discussed during planning against the documentation and planned implementation.

## Requirements map

### Visible requirements flow

```text
User needs
  -> Understand data
	  -> Profiling and issue detection
  -> Clean safely
	  -> Recommendations, preview, approval, validation
  -> Preserve trust
	  -> Versions, audit log, lineage, reproducible recipes
  -> Support growth
	  -> Connectors, workers, storage, ML checks, integrations
```

The Mermaid version maps the requirement groups to the ClearSet modules that implement them.

```mermaid
flowchart LR
    Needs[User Needs] --> Understand[Understand Data]
    Needs --> Clean[Clean Safely]
    Needs --> Trust[Preserve Trust]
    Needs --> Growth[Support Growth]
    Understand --> Profiling[Profiling and Issue Detection]
    Clean --> Safe[Recommendations, Preview, Approval, Validation]
    Trust --> History[Versions, Audit, Lineage, Recipes]
    Growth --> Scale[Connectors, Workers, Storage, ML, Integrations]
```

| Requirement | Covered in | Initial status |
| --- | --- | --- |
| Automatic profiling | README, ARCHITECTURE, WORKFLOW, QUALITY_CHECKS | Phase 0 |
| Cleaning recommendations with explanations | PRODUCT_BRIEF, WORKFLOW, DIFFERENTIATION | Phase 0 |
| Safe preview before modification | README, WORKFLOW, DECISIONS | Phase 0 |
| Reversible transformations | DATA_MODEL, WORKFLOW, DECISIONS | Phase 0 |
| Attribution and rejection history | DATA_MODEL, WORKFLOW, DECISIONS | Phase 0 |
| CSV support | README, ROADMAP, ARCHITECTURE | Phase 0 |
| Excel support | ROADMAP, ARCHITECTURE | Phase 2 |
| JSON support | ROADMAP, ARCHITECTURE | Phase 2 |
| Parquet support | README, ROADMAP, ARCHITECTURE | After validation |
| Database connectors | ARCHITECTURE, SCALING, ROADMAP | Phase 5 |
| Dataset versioning | DATA_MODEL, WORKFLOW, SCALING | Phase 0 |
| Label-error checks | QUALITY_CHECKS, ROADMAP | Phase 4 |
| Leakage checks | QUALITY_CHECKS, ROADMAP | Phase 4 |
| Imbalance checks | QUALITY_CHECKS, ROADMAP | Phase 4 |
| Duplicate and near-duplicate checks | QUALITY_CHECKS, ROADMAP | Exact duplicates in Phase 0; near duplicates later |
| Non-programmer web interface | PRODUCT_BRIEF, ROADMAP, ARCHITECTURE | Phase 3 |
| Local validation privacy | PRODUCT_BRIEF, DECISIONS, OPEN_QUESTIONS | Phase 0 |
| Explainable quality score | QUALITY_CHECKS, DECISIONS | Phase 1 |
| Schema overrides and custom rules | DATA_MODEL, DECISIONS, OPEN_QUESTIONS | Phase 2 |
| Exportable recipes and reports | README, WORKFLOW, ROADMAP | Phase 0 |
| Scaling to workers and object storage | ARCHITECTURE, SCALING | Phase 5 |
| Security and PII handling | ARCHITECTURE, DECISIONS, OPEN_QUESTIONS | Before hosted deployment |

## Coverage result

The first implementation boundary is the Phase 0 validation script against one real CSV. Items marked later are intentionally documented but must not pull infrastructure or UI work ahead of that validation gate.