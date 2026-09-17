# Differentiation from Open-Source Projects

ClearSet should build on existing projects rather than compete with every one of them algorithm by algorithm.

| Project | Main strength | ClearSet difference |
| --- | --- | --- |
| OpenRefine | Interactive manual cleaning | Attribution of human, rule, and AI-assisted changes plus portable evidence |
| Great Expectations | Validation rules and documentation | Connects validation to issue explanations and approved cleaning |
| Pandera | Python dataframe schemas | Provides a web workflow for non-programmers and reusable project settings |
| ydata-profiling | Automatic reports | Connects profile findings directly to recommended actions |
| Cleanlab | ML label-error detection | Adds general-purpose cleaning and versioning around ML checks |
| Soda Core | Data-quality checks and monitoring | Focuses on interactive repair before monitoring |
| Frictionless | Dataset validation and packaging | Covers the full inspect, recommend, preview, clean, version, export lifecycle |

## Product wedge

The positioning is:

> ClearSet is a local-first evidence trail for dataset changes, with cleaning assistance.

The adoption wedge is local execution for students, researchers, independent developers, and analysts. The paid product hypothesis is hosted, team-based attribution for compliance, risk, data-audit, and small data teams that need to prove what changed. Local mechanics do not validate hosted demand, so the transition requires evidence from a real prospective customer.

## Defensible workflow

```text
Profile -> Explain -> Recommend -> Preview -> Approve -> Validate
-> Version -> Audit -> Export
```

The differentiation is not more cleaning algorithms. It is a portable evidence layer connecting profiling, explanations, previews, approvals and rejections, validation, immutable versions, and per-change attribution across tools.

### Unique feature set

1. **Per-change attribution and provenance** — before/after values, source, reason, reviewer, confidence, and version are connected to the operation.
2. **Tool-agnostic evidence capture** — ClearSet can record changes made by a human, deterministic rule, script, spreadsheet, or AI agent through a common event format.
3. **Rejected-suggestion history** — declined and deferred suggestions remain visible with their evidence and reviewer reason.
4. **Signed portable export bundles** — a verifier can check the source hash, transformation plan, ledger, validation result, and signature outside the originating workspace.
5. **Audience-specific explanations** — the same evidence can be rendered for an operator, executive, or auditor.

No item is treated as a proven moat yet. The test is whether the connected evidence chain helps a real reviewer make a faster or more defensible decision.

### Transition gate

Move from local validation toward hosted collaboration only when all three signals exist:

- A defined customer and budget owner has a recurring change-review problem.
- A real reviewer uses the evidence artifact and reports a faster or more defensible decision.
- The customer needs shared permissions, retention, or multi-reviewer history that local execution cannot provide.

## Open-source strategy

Use mature libraries underneath where they are strong. ClearSet should own the orchestration, user experience, transformation plan, version model, audit history, and explanation layer. Licenses must be reviewed before distribution.