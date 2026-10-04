---
name: git-commit-logically
description: Commit outstanding local git changes into coherent local commits without pushing. Use when the user asks Codex to commit the current worktree, commit all changes, split current changes into logical commits, follow repository commit-message rules, or create local commits from the current git tree.
license: "Unlicense"
metadata:
 short-description: "Commit current changes in logical groups"
---

# Git Commit Logically

Use this skill to turn the current worktree into one or more high-quality local commits. The goal is accurate grouping and repo-compliant messages, not speed.

## Hard Rules

- Do not push.
- Do not create an empty commit.
- Do not revert, discard, overwrite, or clean user changes.
- Do not make source edits while committing unless the user explicitly asked for fixes too.
- Use non-interactive git commands only.
- Read `.github/agent-commit-message-instructions.md` first when it exists, and follow it exactly.
- If commit-message instructions conflict with this skill, the repository instructions win.

## Workflow

1. Confirm the target is a git repository.

   ```powershell
   git rev-parse --show-toplevel
   git branch --show-current
   ```

If the command fails, stop and say the directory is not a git repository.

2. Read repository commit-message rules before inspecting changes.

   ```powershell
   if (Test-Path ".github/agent-commit-message-instructions.md") {
     Get-Content ".github/agent-commit-message-instructions.md"
   }
   ```

If no instruction file exists, inspect recent commits and infer the local convention:

```powershell
git log -5 --pretty=format:"%h %s"
```

3. Inspect the full outstanding tree.

   ```powershell
   git status --short --untracked-files=all
   git diff --stat
   git diff --cached --stat
   ```

Then read focused diffs until each changed path has a clear purpose:

```powershell
git diff -- <path>
git diff --cached -- <path>
```

For untracked text files, read the file. For binary files, use file names, sizes, and nearby source references to infer purpose.

4. Decide commit groups by user-visible purpose.

Prefer groups such as:

- source or behavior changes
- tests and fixtures
- docs and examples
- config, linting, formatting, or editor metadata
- dependency manifests and lockfiles
- CI, release, or packaging automation
- generated artifacts that must stay synchronized with their source

Do not split so finely that each commit loses context. Do not combine unrelated source, docs, dependency, or release changes merely because they are adjacent in the diff.

5. Stage one group at a time.

Use explicit paths:

```powershell
git add -- path/to/file another/path
```

Use patch staging only when a file contains unrelated hunks:

```powershell
git add -p -- path/to/file
```

If patch staging would require an interactive prompt, avoid it and use a non-interactive alternative such as `git diff` to reassess whether the file should stay in one commit. If a single file truly contains unrelated changes that cannot be split non-interactively, make the least misleading coherent commit and mention the constraint.

6. Verify the staged group before committing.

   ```powershell
   git diff --cached --stat
   git diff --cached --check
   git diff --cached
   ```

Run `git diff --cached` with focused paths when the staged patch is large. Do not run unrelated test or formatting commands unless the user asked for verification or the repo's commit instructions require it.

7. Commit with the repository's required message format.

Use `git commit -m` with multiple `-m` arguments for body paragraphs:

```powershell
git commit -m "type(scope): concise subject" -m "Explain the behavior or package surface changed." -m "Mention tests, docs, or generated artifacts when relevant."
```

Good commit messages explain what changed and why it belongs together. Avoid vague subjects like `update files`, `misc changes`, or `fix stuff`.

8. Repeat until the worktree is clean or only intentionally uncommitted files remain.

After each commit:

```powershell
git status --short --untracked-files=all
```

9. Report the result.

Always show the final tree state and recent commits:

```powershell
git status --short --untracked-files=all
git log -5 --oneline
```

If the tree was already clean at the start, say so and do not commit.

## Grouping Heuristics

- Keep lockfile changes with the manifest change that caused them.
- Keep tests with the source behavior they verify unless tests are a separate cleanup or test-infra change.
- Keep generated exports, snapshots, compiled assets, or docs outputs with the source-of-truth change they mirror.
- Separate mechanical formatting from behavior changes when both are present.
- Separate repo maintenance from product behavior unless the maintenance is required for the behavior to work.
- Treat deletions as their own group when they remove a feature, deprecate a surface, or clean obsolete files across multiple areas.
- Preserve user intent from already staged changes when it is clear; otherwise restage deliberately and explain the grouping.

## Safety Checks

Before each commit, confirm:

- The staged paths match only the intended group.
- The commit message follows `.github/agent-commit-message-instructions.md` or recent repo style.
- No secrets, local caches, editor temp files, build trash, or accidental large artifacts are staged.
- No unrelated user changes are being hidden by broad commands.

If the outstanding changes are ambiguous or risky to group, stop and ask a concise question rather than guessing.
