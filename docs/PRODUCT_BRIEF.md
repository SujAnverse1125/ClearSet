# ClearSet Product Brief

## Problem

People often receive datasets with missing values, inconsistent types, duplicate records, invalid values, unexpected categories, and hidden machine-learning problems. Existing tools are usually specialized: one profiles data, another validates it, and another performs manual cleaning. Users must understand several tools and may apply changes without a clear record of what happened.

## Solution

ClearSet is an evidence trail for dataset changes, with cleaning assistance. It connects inspection, issue detection, recommendations, safe previews, approval or rejection, validation, versioning, attribution, and portable export in one workflow.

## Customer thesis

- Free adoption: students, researchers, independent developers, and analysts who want a safer local cleaner
- Paid problem: compliance, risk, data-audit, and small data teams that need evidence of what a human, rule, or AI changed
- The first real validation target is one person with a recurring need to review or certify data changes

This is a hypothesis. No segment, willingness to pay, or market size is validated yet.

## Value proposition

ClearSet tells users:

- What is wrong
- Which rows and columns are affected
- Why a fix is recommended
- What alternatives exist
- What will change before it happens
- Whether the result is better after the change
- How to reproduce or undo the change

## Product promise

> ClearSet makes dataset changes reviewable, explainable, reproducible, attributable, and portable.

## Product direction

The first artifact is local because it is the fastest way to test the evidence model on real data. The intended paid product is a hosted team workflow for shared review, retention, permissions, and audit evidence. Local execution validates mechanics; it does not prove hosted demand.

## Unique feature set

The features work as one evidence chain rather than as isolated claims:

1. **Per-change attribution:** record the exact before/after change, source, reason, reviewer, confidence, and resulting version.
2. **Tool-agnostic capture:** accept standardized change evidence from ClearSet, scripts, spreadsheets, pipelines, or AI agents.
3. **Rejected and deferred decisions:** preserve suggestions that were declined or postponed, including the reviewer and reason.
4. **Signed portable exports:** package the dataset hash, plan, ledger, validation results, and signature so another party can verify the evidence independently.
5. **Audience-specific explanations:** render the same evidence for a hands-on reviewer, an executive, or an auditor.

The connected workflow is the product: suggest, review, accept or reject, reproduce, explain, and export proof. These are hypotheses to validate, not yet a proven moat.

## Non-goals for the first release

- Replacing every existing data-quality framework
- Automatic destructive cleaning without approval
- A hosted collaboration product before local evidence of demand
- Distributed processing before it is needed
- Supporting every database and cloud platform immediately
- Building advanced machine-learning algorithms from scratch

## Success criteria

Phase 0 is successful when a plain Python script can take one real CSV through this path:

```text
Upload -> Profile -> Understand issues -> Choose a recommendation
-> Preview -> Approve -> Validate -> Create version -> Export
```

The output must preserve the original, reproduce the result from a structured plan, and record whether each change was human-authored, rule-authored, or AI-suggested and human-approved, rejected, or deferred.