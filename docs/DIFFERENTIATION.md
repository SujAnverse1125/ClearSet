# Differentiation from Open-Source Projects

ClearSet should build on existing projects rather than compete with every one of them algorithm by algorithm.

| Project | Main strength | ClearSet difference |
| --- | --- | --- |
| OpenRefine | Interactive manual cleaning | Guided recommendations, previews, version history, and reproducible recipes |
| Great Expectations | Validation rules and documentation | Connects validation to issue explanations and approved cleaning |
| Pandera | Python dataframe schemas | Provides a web workflow for non-programmers and reusable project settings |
| ydata-profiling | Automatic reports | Connects profile findings directly to recommended actions |
| Cleanlab | ML label-error detection | Adds general-purpose cleaning and versioning around ML checks |
| Soda Core | Data-quality checks and monitoring | Focuses on interactive repair before monitoring |
| Frictionless | Dataset validation and packaging | Covers the full inspect, recommend, preview, clean, version, export lifecycle |

## Product wedge

The strongest initial niche is a local-first, privacy-friendly assistant for students, researchers, independent developers, and small teams.

## Defensible workflow

```text
Profile -> Explain -> Recommend -> Preview -> Approve -> Validate
-> Version -> Audit -> Export
```

The differentiation is not simply more cleaning algorithms. It is the connection between profiling, explainable recommendations, safe approval, validation, lineage, and reproducibility.

## Open-source strategy

Use mature libraries underneath where they are strong. ClearSet should own the orchestration, user experience, transformation plan, version model, audit history, and explanation layer. Licenses must be reviewed before distribution.