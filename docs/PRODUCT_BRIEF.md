# ClearSet Product Brief

## Problem

People often receive datasets with missing values, inconsistent types, duplicate records, invalid values, unexpected categories, and hidden machine-learning problems. Existing tools are usually specialized: one profiles data, another validates it, and another performs manual cleaning. Users must understand several tools and may apply changes without a clear record of what happened.

## Solution

ClearSet is an explainable assistant that connects dataset inspection, issue detection, recommendations, safe previews, validation, versioning, and export in one workflow.

## First users

- The project owner using datasets in personal projects
- Students and researchers
- Independent developers and analysts
- Small teams that need understandable data-quality workflows

Large enterprise teams are a later audience, not the first target.

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

> ClearSet helps people understand, safely clean, validate, version, and reproduce changes to their data.

## Non-goals for the first release

- Replacing every existing data-quality framework
- Automatic destructive cleaning without approval
- Distributed processing before it is needed
- Supporting every database and cloud platform immediately
- Building advanced machine-learning algorithms from scratch

## Success criteria

The first release is successful when a user can take a real CSV or Parquet dataset through this complete path:

```text
Upload -> Profile -> Understand issues -> Choose a recommendation
-> Preview -> Approve -> Validate -> Create version -> Export
```

The user should be able to restore the original data and reproduce the cleaned result from a saved recipe.