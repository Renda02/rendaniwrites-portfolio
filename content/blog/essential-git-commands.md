---
date: 2025-01-05
title: "Git commands I use daily: From terminal fear to confident workflows"
description: "The daily Git workflow and commands I learned through trial, error, and a very patient developer."
tags: ["git", "version-control", "workflow"]
---

In my previous role as a solo tech writer for a fintech company, we worked entirely in docs-as-code. We documented everything using code workflows from Visual Studio Code. As someone who used to fear the terminal, I chose to use only the terminal. I wanted to become proficient in git commands, even if it meant breaking things.

And yes, I broke things a lot.

Lucky for me, I had a developer who became my go-to person for anything Git-related: Javier. Every time I broke something (which was frequently), he'd patiently walk me through the fix. Those messy days and his patience taught me more than any tutorial ever could. I went from avoiding the command line to embracing it, mistakes and all.

Here's my Git flow and the commands that became part of my daily workflow. These are the ones I learned through trial, error, and a very patient mentor.

---

## My daily Git flow

### 1. Always start with status
```bash
$ git status  # check branch and changes
```

This habit saved me from working on the wrong branch or committing changes to the wrong place.

### 2. Pull latest changes before creating a branch
```bash
$ git pull  # get latest changes from remote
```

Running `git pull` before creating a new branch ensures you're branching off the most recent code. This prevents merge conflicts later because you're not working on outdated code.

### 3. Create feature branches for every change
```bash
$ git checkout -b feature/update-api-docs
```

One feature, one branch. It keeps work organized and makes switching tasks easier.

### 4. Make your changes, then stage and commit
```bash
$ git add .  # stage all changes (or git add filename for specific files)
$ git commit -m "Add API endpoint documentation"
```

### 5. Push to remote and open pull request
```bash
$ git push -u origin feature/update-api-docs  # first push
$ git push  # subsequent pushes
```

Then open a pull request for the team to review.

### 6. Clean up after merge
```bash
$ git checkout main
$ git pull  # get merged changes
$ git branch -d feature/update-api-docs  # delete local branch
```

---

These 6 steps became my daily rhythm. But work doesn't always move in a straight line, and one habit outside the sequence made all the difference.

## When you need to switch branches mid-change

Say you're halfway through documenting a new API endpoint when a teammate asks you to fix a typo on a page that's already live. You don't want to commit half-finished work just to switch branches, and you don't want to lose it either.

Or say you've started changes on a branch and need to leave it before they're ready to commit, maybe to check out a different branch or review someone else's work.

The scenario I run into most often: I start making changes before realizing I'm still on `main`, or on an old branch I meant to leave behind. Stash lets me save the work, switch to (or create) the right branch, and bring the changes back without losing anything.

This is where stash comes in:
```bash
$ git stash           # save current changes temporarily
$ git checkout other-branch # switch branches
$ git stash pop       # bring changes back later
```
Think of this as my "pause and come back later" button. It's not part of the sequence above. It's the habit I reach for whenever work gets interrupted.

---

## Two more commands that came in handy

Beyond the steps above, 2 commands became part of my regular toolkit.

`git checkout --` discards unstaged changes on a file. If I'd made a mess of edits I didn't want to keep, this reverted the file to its last committed state.

`git commit --amend --no-edit` updates the last commit instead of creating a new one, without changing the commit message. Instead of piling up small "fix typo" or "forgot a file" commits, I could fold the fix into the commit it belonged to and keep a clean, focused history. More on how I actually used this below.

---

## Another tip from Javier included:

As I started committing more frequently, a pattern appeared. I'd make a commit… and then immediately realize:

- I'd missed a file
- I'd made a small typo
- I'd left out a change

That's when Javier introduced me to a simple but powerful command: `git commit --amend`

Instead of creating extra "fix" commits for tiny adjustments, I could update the previous commit and keep my history clean.

Why this worked so well for me

- it kept my commit history tidy and focused
- I didn't have to learn more complex tools right away
- it helped me think in terms of complete changes, not fragments
- it removed one more thing to worry about before merging

When to use `--amend`

- you're still working on the same logical change
- you haven't pushed the commit to the remote yet
- you want to update or extend the most recent commit

This lesson from Javier became part of my workflow. Instead of making messy commits and cleaning them up later, I got into the habit of keeping my history clean from the start. It's a small practice, but it made a big difference in how confidently I worked.

These commands and this workflow didn't come naturally. They came from breaking things, asking questions, and having someone patient enough to help me learn.

From fearing the terminal to embracing it, the journey taught me that the messy part is where the real learning happens.
