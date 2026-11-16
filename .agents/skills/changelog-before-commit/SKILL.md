---
name: changelog-before-commit
description: Always update CHANGELOG.md before committing changes in any caBRAPI repository.
---

# Update CHANGELOG.md Before Commit

Before running `git commit` on any feature, fix, perf, or refactor change:

1. **Update `CHANGELOG.md`** at the repository root (create it if missing) under `[Unreleased]` or the current release section.
2. **Summarize what changed** concisely using standard categories (`Added`, `Changed`, `Fixed`, `Removed`, `Security`, `Performance`).
3. **Stage `CHANGELOG.md`** together with your code changes before committing.
4. *(Skip only for trivial automated/meta-only commits if explicitly instructed with `[skip ci]`.)*