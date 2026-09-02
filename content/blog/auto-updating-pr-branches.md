---
date: 2026-09-02
draft: true
title: "Auto-updating PR branches with GitHub Actions"
description: "A GitHub Actions workflow that keeps every open pull request branch up to date with main."
tags: ["github-actions", "ci-cd", "automation", "workflow"]
---

I recently checked out Elastic's [`docs-content`](https://github.com/elastic/docs-content) repo, specifically its [stale-sweep workflow](https://github.com/elastic/docs-content/blob/main/.github/workflows/docs-staleness-sweep.yml): it flags documentation pages that haven't been touched in a while and files issues to get them fixed. That reminded me of a related problem: open pull requests (PRs) drifting out of date. This post walks through a small GitHub Actions workflow that updates every open PR branch automatically after each merge to `main`. Set it up once and it keeps those branches current without you touching them, so CI runs against the current `main`, not a stale diff.

## Why open PR branches fall behind

If you work in a docs-as-code workflow while managing multiple products, you've probably had several PRs open at once. You keep opening new ones while the older ones are still in review or waiting on a release, and those older branches quietly fall behind `main`.

I often had PRs stale for days while I kept the documentation in step with what the product teams were shipping and worked on several changes at once. Those pull requests just needed to stay in sync with `main` while I moved on to the next thing. That's the part I automated.

## What I did about it

I set up a workflow that uses a GitHub action to auto-update open PR branches. In plain terms: whenever new commits land on `main`, this catches every open PR whose branch hasn't caught up yet, and merges those new commits in automatically. It's the same thing you'd do by hand clicking "Update branch" on GitHub, just for every open PR at once. It doesn't build, test, or deploy anything. It's branch hygiene that runs alongside your CI checks. When CI runs, it's testing the current `main`, not a stale diff.

## The workflow

I set this up with [`wechuli/pull-request-updater`](https://github.com/wechuli/pull-request-updater). Here's the [workflow file](https://github.com/Renda02/rendaniwrites-portfolio/blob/main/.github/workflows/auto-update-pr.yml) I'm running:

```yaml
name: Auto-update PR branches
on:
  push:
    branches: [main] # run after every merge to main

jobs:
  autoupdate:
    runs-on: ubuntu-latest
    permissions:
      contents: write # update the PR branch
      pull-requests: write # act on open PRs
      issues: write # comment on each PR it updates (GitHub treats PR comments as issue comments)
    steps:
      - uses: wechuli/pull-request-updater@v2
        with:
          base: main
          token: ${{ secrets.GITHUB_TOKEN }}
```

How it works:

- **It only updates PRs that are behind `main` after a merge.** Branches that are already current get skipped.
- **Updates run against the base branch you set.** Here that's `main`.

## The challenge this doesn't solve for you

Even with the update handled automatically, one situation still needs attention: merge conflicts. When a PR's changes collide with what's now on `main`, GitHub marks it as conflicted, and you have to resolve that before it can merge. This action can't auto-resolve a merge conflict, so on older PRs I've had to [drop into the terminal](/blog/essential-git-commands) and run `git rebase` by hand before they could merge. The action keeps branches current when it can, but resolving conflicts is still a manual job.

## What makes this workflow good

It's helped me ship documentation faster, because PRs aren't going stale while they wait to merge. And because it's just a GitHub Actions workflow, it's reusable. Documentation for different products often lives in separate repos, and I can drop the same file into every one of them. Same setup, same behavior, no rebuilding it each time.

Have you run into stale PRs piling up in your own documentation workflow? I'd like to hear what you've tried.

It's a small piece of automation. It just quietly keeps every open PR ready to merge while I work on something else.
