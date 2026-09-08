---
date: 2026-09-02
title: "How I keep open PRs in sync with main branch"
description: "A GitHub Actions workflow that keeps every open PR branch current with main, so CI always tests what will actually merge."
tags: ["github-actions", "ci-cd", "automation", "workflow"]
---

I checked out Elastic's [`docs-content`](https://github.com/elastic/docs-content) repo, specifically its [stale-sweep workflow](https://github.com/elastic/docs-content/blob/main/.github/workflows/docs-staleness-sweep.yml): it flags documentation pages nobody has touched in a while and files issues to get them fixed. That reminded me of a related problem: open pull requests (PRs) drifting out of date. This post walks through a GitHub Actions workflow that keeps every open PR branch current with `main` automatically, so continuous integration (CI) always tests against it.

## Why open PR branches fall behind

If you work in a docs-as-code workflow while managing multiple products, you've probably had several PRs open at once. You keep opening newer ones and merging them while the earlier ones wait on:

- a review that hasn't happened yet
- a release that hasn't shipped yet
- a change that needs a stakeholder's sign-off
- an engineer who still needs to verify a technical detail

That's all normal, and none of it means the PRs are wrong. But every merge to `main` leaves the waiting PRs a little further behind, and nothing flags it. A branch that's fallen behind still passes every check, because those checks ran against an old `main`, not the current one.

Mine just needed to stay in sync with `main` while I moved on to the next thing. That's the part I automated.

## The fix

I set up a workflow built on the [pull-request-updater](https://github.com/wechuli/pull-request-updater) action. In plain terms: whenever new commits land on `main`, it finds every open PR whose branch has fallen behind and merges them in automatically, skipping the ones already current. It doesn't build, test, or deploy anything. It's branch hygiene that runs alongside your CI checks.

Here's the [workflow file](https://github.com/Renda02/rendaniwrites-portfolio/blob/main/.github/workflows/auto-update-pr.yml) I'm running:

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
          base: main # only update PRs that target main
          token: ${{ secrets.GITHUB_TOKEN }}
```

The `base: main` line scopes it to PRs that target `main`. Leave it out and the action updates every open PR, whatever branch it's based on.

## The challenge this doesn't solve

Even with branches kept current, one thing still needs you: merge conflicts. When a PR's changes collide with what's already on `main`, GitHub marks it as conflicted, and you have to resolve it yourself before it can merge.

The [pull-request-updater](https://github.com/wechuli/pull-request-updater) action is a small addition, but it keeps every open PR branch current with `main` on its own.

Have you run into PRs piling up in your own documentation workflow? I'd like to hear what you've tried.

