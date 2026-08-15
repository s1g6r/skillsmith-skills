# Skillsmith — free skills

Two Claude Code skills, free, no catch: `commit-hygiene` and
`release-notes`. If these save you time, the paid **Launch Kit** has four
more for shipping a solo app — store listings, launch video scripts,
landing page copy, and onboarding docs. **[Get the Launch Kit →
GUMROAD_URL_HERE]**

## Install

```bash
mkdir -p ~/.claude/skills
cp -r commit-hygiene release-notes ~/.claude/skills/
```

## What they do

- **`commit-hygiene`** — reads your staged changes, tells you if they
  should be split into separate commits, and writes a clean commit message
  matching your repo's existing convention.
- **`release-notes`** — turns a commit range into both a technical
  CHANGELOG entry and a plain-language "what's new" a user would actually
  want to read.

Ask Claude Code for either in plain English — "review my staged changes"
or "write release notes for this" — no need to invoke them by name.

## Feedback

Found a rough edge, or want to see a specific skill built next? Open an
issue here, or reply on whatever thread pointed you to this repo — that
feedback directly shapes what goes in the paid kit next.
