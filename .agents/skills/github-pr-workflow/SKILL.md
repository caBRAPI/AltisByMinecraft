---
name: github-pr-workflow
description: GitHub Pull Request and merge workflow for caBRAPI repositories. Use whenever making changes so nothing is committed directly to the default branch.
---

# GitHub PR & Merge Workflow

1. **Create a feature branch from `latest`:**
   ```bash
   git checkout latest
   git pull origin latest
   git checkout -b <type>/<short-description>
   ```

2. **Validate changes locally** (tests, lint, formatting, build) before pushing.

3. **Commit with Conventional Commits:**
   ```bash
   git add -A
   git commit -m "<type>: <clear description>"
   git push -u origin <type>/<short-description>
   ```

4. **Open a Pull Request to `latest`:**
   ```bash
   gh pr create \
     --base latest \
     --head <type>/<short-description> \
     --title "<type>: <clear description>" \
     --body "<summary of changes and Closes #n if applicable>"
   ```

5. **Merge and clean up:**
   ```bash
   gh pr merge <pr-number> --squash --delete-branch
   git checkout latest
   git pull origin latest
   ```

6. **Close/link any related issue** (if not auto-closed by `Closes #n`):
   ```bash
   gh issue close <issue-number> --comment "Concluído via PR #<pr-number>."
   ```
