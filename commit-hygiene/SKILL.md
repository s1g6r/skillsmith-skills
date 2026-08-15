---
name: commit-hygiene
description: This skill should be used when the user asks to "write a commit message", "review my staged changes", "check my diff before committing", or wants help splitting a large changeset into cleaner commits.
version: 1.0.0
---

# Commit Hygiene

Reviews staged changes and produces a clean commit message — or, when the
diff mixes unrelated concerns, tells the user how to split it before
committing.

## Step 1 — look at what's actually staged

Run `git diff --staged` (or `git diff --cached --stat` first if the diff is
large). Don't work from what the user says they changed — read the real
diff, since staged and intended often drift apart.

## Step 2 — decide: one commit, or several

A diff belongs in one commit when every changed file serves the same single
purpose. Signs it should be split instead:

- A feature addition mixed with an unrelated refactor of existing code
- A bug fix bundled with formatting/whitespace changes across untouched
  files
- Two unrelated bugs fixed in the same commit
- Config/dependency changes mixed with feature code, when the two aren't
  causally linked

If it should split, don't just say so — give the concrete grouping (which
files or hunks go in which commit) and the `git add -p` or `git restore
--staged <file>` commands to get there.

## Step 3 — write the message

Conventional-commit style unless the repo's existing `git log` shows a
different convention (check recent commits and match it instead of
imposing conventional commits on a project that doesn't use them):

```
<type>(<scope>): <summary, imperative, ≤50 chars>

<body: what and why, wrapped ~72 chars, only if the summary line
isn't self-explanatory — don't restate the diff line by line>
```

Types: `feat`, `fix`, `refactor`, `docs`, `test`, `chore`, `perf`. Scope is
the affected area (a directory, module, or feature name), omit if the repo
doesn't use scopes.

The summary states *what changed*, the body (if present) states *why* —
never restate the diff, since `git show` already does that.

## Step 4 — output

```
SPLIT? <yes, with grouping / no>

MESSAGE
<type>(<scope>): <summary>

<body if needed>
```

If a split was recommended, list the exact commands to execute it before
the message is used.
