---
title: "Documentation pipeline"
description: "How every content change on this site moves through automated checks and a human review step before it deploys."
---

This page explains the pipeline every content change on this site goes through: which checks run on their own, which of those actually block a merge, and where a human still has to decide instead of a rule.

## What the pipeline does

The checks split into two layers: GitHub Actions run on their own in CI, and skills run manually, in Claude Code.

### GitHub Actions

| Check | When it runs | What it blocks |
|---|---|---|
| [auto-update-pr](https://github.com/Renda02/rendaniwrites-portfolio/blob/main/.github/workflows/auto-update-pr.yml) | Push to main | Nothing. Keeps other PRs from drifting out of date. |
| [Image naming](https://github.com/Renda02/rendaniwrites-portfolio/blob/main/.github/workflows/check-image-naming.yml) | Pull request adds an image | Blocks merge on a naming mismatch. |
| [Repo diagram](https://github.com/Renda02/rendaniwrites-portfolio/blob/main/.github/workflows/repo-visualizer.yml) | Push to main | Nothing. Cosmetic only. |
| [Stale PR detection](https://github.com/Renda02/rendaniwrites-portfolio/blob/main/.github/workflows/stale-pr-notice.yml) | Every Monday | Nothing. Flags PRs untouched 2+ weeks. |
| [Vale](https://github.com/Renda02/rendaniwrites-portfolio/blob/main/.github/workflows/vale.yml) | Pull request | Comments on the PR. Doesn't block merge. |

### Skills

| Check | When it runs | Command |
|---|---|---|
| [site-updates](https://github.com/Renda02/rendaniwrites-portfolio/blob/main/.claude/skills/site-updates/SKILL.md) | Run manually, after a batch of commits | `/site-updates` |
| [style-check](https://github.com/Renda02/rendaniwrites-portfolio/blob/main/.claude/skills/style-check/SKILL.md) | Run manually, mid-draft | `/style-check` |
| [voice-and-tone](https://github.com/Renda02/rendaniwrites-portfolio/blob/main/.claude/skills/voice-and-tone/SKILL.md) | Run manually, before publishing | `/voice-and-tone` |

## How a change ships

1. Create a new branch from main for every change.
2. Write content in Markdown, in this repo.
3. Preview locally with `hugo server -D`, and run the relevant skill (`/style-check`, `/voice-and-tone`) against new content before opening a PR.
4. Open a pull request. Depending on what changed, it triggers the relevant GitHub Action: Vale on any content change, image naming on new images. Netlify also builds a deploy preview to check the live page.
5. Merge to main once every check passes. Netlify deploys to production automatically. There's no persistent staging environment, so what merges is live immediately.

## What each layer demonstrates

Each layer exists to catch a specific kind of problem. Here's what each one does and why it's built this way.

### How GitHub Actions work

Each workflow triggers on an event in this repo, or a schedule.

- **auto-update-pr**: keeps every open PR synced with main automatically, so branches don't drift apart and collide with conflicts when they finally merge.
- **check-image-naming**: hard-stops a merge on a naming mismatch. Generic names like `image1.png` become untrackable once a repo has more than a few images, so this is the one rule enforced without exception.
- **stale-pr-notice**: flags any PR untouched for 2+ weeks, so a stalled branch gets finished or closed instead of becoming forgotten dead weight.
- **Vale**: runs `styles/Portfolio`, one custom rule set (some rules adapted from Google's style guide, some written from scratch) that checks spelling, terminology, and style on every PR. It's advisory only: nothing blocks a merge, since one reviewer already reads every PR.

### How skills work

All three run manually, and each adds something Vale's fixed rules can't, but nothing they touch ships without me separately reviewing and merging the pull request.

- **site-updates**: drafts the changelog from git history instead of memory.
- **style-check**: catches cross-page inconsistencies Vale can't see, like the same claim worded two different ways on different pages.
- **voice-and-tone**: scores a draft on outcome, focus, and ending before it publishes.

### Why the probabilistic layer scales differently than the deterministic one

Vale scales the same regardless of team size: the rule fires the same way for one person or ten. Skills don't. Right now I write, run, and approve everything myself, but on a team those would split into three roles, and what has to survive that split is the correction loop: whoever catches a skill being wrong has to update the skill file, or the fix stays local instead of becoming a team-wide rule.

## Repository structure

```
.claude/skills/         Claude Code skills used while writing and reviewing content
.github/workflows/      CI/CD workflow definitions
AGENTS.md               Shared instruction file for Cursor and Claude Code
archetypes/             Front matter templates for new content
assets/                 Files Hugo processes (CSS, etc.)
CLAUDE.md               Imports AGENTS.md so both tools follow the same conventions
content/                Site pages (about, work, projects, blog) in Markdown
layouts/                Hugo templates and shortcodes
static/                 Images and other files served as-is
styles/                 Vale style rules for prose linting
```

## Further reading

For the judgment calls behind this pipeline, and what I've overridden along the way, see [how I built this](/how-i-built-this). For commit conventions and full setup instructions, see [the README on GitHub](https://github.com/Renda02/rendaniwrites-portfolio).
