---
date: 2026-09-02
draft: true
title: "Auto-updating PR branches with GitHub Actions"
description: "A GitHub Actions workflow that keeps every open pull request branch up to date with main automatically, so CI always tests against the current state."
tags: ["github-actions", "ci-cd", "automation", "workflow"]
---

I recently checked out Elastic's [`docs-content`](https://github.com/elastic/docs-content) repo, specifically its [stale-sweep workflow](https://github.com/elastic/docs-content/blob/main/.github/workflows/docs-staleness-sweep.yml): it flags documentation pages that haven't been touched in a while and files issues to get them fixed. That reminded me of a related problem: pull requests (PRs) that stay open far longer than they should. This post walks through a small GitHub Actions workflow that updates every open PR branch automatically after each merge to `main`.

## Let's talk about branch updates for open pull requests

If you've worked in a continuous integration and delivery (CI/CD) pipeline on GitHub, you've probably had multiple open PRs sit around for a while. It's usually not because the documentation (or code) in them is wrong, but because of everything else going on around them: newer PRs merging first, quick fixes jumping the queue, `main` moving on without them. Moving faster is exactly what created the problem for me, too. As a solo technical writer, it was easy to have multiple PRs open at once, some stale for a few days while I maintained a lot of changes in parallel, with documentation work also aligned with marketing, which meant having the docs ready before a launch. None of those PRs were waiting on me. They just needed their branches kept in sync with `main` while I moved on to the next thing, and that's the one piece I ended up automating.

## What I did about it

Here's what I found helpful: a workflow that uses a GitHub Action to auto-update open PR branches. In plain terms: whenever new commits land on `main`, this catches every open PR whose branch hasn't caught up yet, and merges those new commits in automatically. It's the same thing you'd do by hand clicking "Update branch" on GitHub, just for every open PR at once. It doesn't build, test, or deploy anything. It's branch hygiene that runs alongside your actual CI/CD checks, so that when CI does run, it's testing against the real, current state of `main` instead of a stale diff.

## The workflow

The Action doing the work is [`wechuli/pull-request-updater`](https://github.com/wechuli/pull-request-updater). Here's [the actual workflow file](https://github.com/Renda02/rendaniwrites-portfolio/blob/main/.github/workflows/auto-update-pr.yml) I'm running:

```yaml
name: Auto-update PR branches
on:
  push:
    branches: [main]
jobs:
  autoupdate:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pull-requests: write
      issues: write
    steps:
      - uses: wechuli/pull-request-updater@v2
        with:
          base: main
          token: ${{ secrets.GITHUB_TOKEN }}
```

A couple of things worth knowing about how it behaves:

- **It only touches PRs that are actually behind.** If a PR's branch already contains everything on `main`, the action skips the update. It won't force an update on a PR that has nothing left to gain from one.
- **Updates run against the base branch you set.** Here that's `main`, but the action supports scoping to other bases or heads if you need it.

## The challenge this doesn't solve for you

Even with the update handled automatically, one situation still needs attention: merge conflicts. When a PR's changes collide with what's now on `main`, GitHub marks it as conflicted, and you have to resolve that before it can merge. This action can't auto-resolve a merge conflict, so on older PRs I've had to run `git rebase` by hand before they could merge. The action keeps branches current when it can, but conflict resolution still comes back to a person.

## What makes this workflow good

It's helped me maintain faster documentation releases, since PRs aren't sitting around going stale while waiting to merge. And because it's just a GitHub Actions workflow, it's reusable in concept: I can drop the same file into every docs repo I maintain, since documentation for different products often lives in separate repos. Same setup, same behavior, no rebuilding it each time.

Have you run into stale PRs piling up in your own documentation workflow, and if so, what have you tried?
