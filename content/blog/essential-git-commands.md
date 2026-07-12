---
date: 2025-01-05
title: "Git commands I use daily: From terminal fear to confident workflows"
description: "The daily Git workflow and commands I learned through trial, error, and a very patient developer."
tags: ["git", "version-control", "workflow"]
---

In my previous role as a solo tech writer for a fintech company, we worked entirely in docs-as-code, documenting everything using code workflows from Visual Studio Code. As someone who used to fear the terminal, I made a choice to use only the terminal and become proficient in git commands, even if it meant breaking things.

And yes, I broke things. A lot.

Lucky for me, I had a developer who became my go-to lifeline: Javier. Every time I broke something (which was frequently), he'd patiently walk me through the fix. Those messy days and his patience taught me more than any tutorial ever could. I went from avoiding the command line to embracing it, mistakes and all.

Here's my Git flow and the commands that became part of my daily workflow. The ones I learned through trial, error, and a very patient developer.

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

One feature, one branch. Keeps work organized and makes switching tasks easier.

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

### 6. Use stash when switching tasks mid-work

Sometimes I'd be halfway through something and need to switch branches. Instead of committing half-baked changes, I stashed them:
```bash
$ git stash           # save current changes temporarily
$ git checkout other-branch # switch branches
$ git stash pop       # bring changes back later
```
Think of this as my "pause and come back later" button.

### 7. Clean up after merge
```bash
$ git checkout main
$ git pull  # get merged changes
$ git branch -d feature/update-api-docs  # delete local branch
```

---

These seven workflow steps became my daily rhythm.

## The core commands I used daily:

- `git branch` – Create, list, and delete branches (separate workspaces for different features)
- `git checkout` – Switch between branches
- `git add` – Stage changes for commit (mark files ready to save)
- `git commit` – Save changes to the local repository (your computer's version)
- `git push` – Upload local commits to a remote repository (share with the team)
- `git status` – Check what's staged, unstaged, and which branch I'm on
- `git stash` / `git stash pop` – Temporarily save and retrieve work in progress
- `git checkout --` – Discard unstaged changes
- `git commit --amend --no-edit` – Update the last commit without changing the message
- `git clone` – Create a local copy of a remote repository (the main project stored online)

---

## Another tip from Javier included:

As I started committing more frequently, a pattern appeared. I'd make a commit… and then immediately realize:

- I'd missed a file
- there was a small typo
- there was one more change I meant to include

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
