---
name: release-notes
description: This skill should be used when the user asks to "write release notes", "generate a changelog", "summarize this diff for users", or wants a "what's new" entry from a git commit range or diff before a release.
version: 1.0.0
---

# Release Notes

Turns a git commit range or diff into release notes written for the person
using the product, not the person who wrote the code.

## Step 1 — get the range

If not given explicitly, ask for or infer the range (e.g. since the last
tag): `git log <last-tag>..HEAD --oneline`. Pull the full commit list and, for
anything ambiguous, `git show <sha>` to see what actually changed.

## Step 2 — categorize, then filter

Sort commits into: **Added**, **Fixed**, **Changed**, **Removed**.

Then drop anything the end user has no reason to care about, even if it's
real work: dependency bumps with no visible effect, CI config, formatting,
internal refactors, typo fixes in comments. If more than half the commits
are this kind of noise, say so — it's a sign of a maintenance release, not a
feature one, and the notes should say that plainly rather than padding out a
feature list.

## Step 3 — write two versions

### Technical CHANGELOG.md entry
Terse, one line per change, imperative mood, grouped under the four
headers, in the style of Keep a Changelog:

```
## [1.4.0] - 2026-08-15
### Added
- Export to CSV from the receipts view

### Fixed
- Crash when opening settings with no network connection
```

### Customer-facing "What's New"
Rewritten for someone who doesn't know the codebase and doesn't care that
it's a "changelog" — 3-6 bullets, benefit-first, plain language:

```
- Export your data to CSV whenever you want it
- Fixed a crash that hit anyone opening Settings offline
```

Skip internal-only fixed items entirely in this version — a user was never
going to notice a fixed race condition in a background job unless it caused
a visible symptom, so lead with the symptom ("no more duplicate
notifications") not the fix.

## Step 4 — check before handing back

- No commit hash, PR number, or internal file/module name leaked into the
  customer-facing version
- Every bullet says what changed for the user, not what changed in the code
- If nothing user-visible changed at all, say that directly rather than
  manufacturing bullet points — "internal maintenance release, no visible
  changes" is a legitimate release note
