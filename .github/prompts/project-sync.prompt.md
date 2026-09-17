---
mode: agent
description: "Use when: the user wants to prepare or validate a feature for GitHub Project sync, including issue title, field values, acceptance criteria, and traceability."
---

# GitHub Project Sync

Prepare the GitHub Project sync for the selected feature.

## Checklist
- Confirm project and BE/FE repository mapping from `.env` (`GITHUB_BE_REPOSITORY`, `GITHUB_FE_REPOSITORY` and `GITHUB_DEFAULT_REPOSITORY`).
- Use the BE repository for backend issues by default and the FE repository for frontend issues; record the selected repository in the issue and report.
- Confirm Blueprint ID and feature scope.
- Draft or update issue title and summary.
- Fill required fields: Status, Priority, Type, Area, Owner, Iteration, Target date, Blueprint ID, Risk.
- Include acceptance criteria, dependencies, and traceability notes.
- Keep `GITHUB_PROJECT_DRY_RUN=true` unless the user explicitly approves live sync.

Use Vietnamese unless the user requests another language.
