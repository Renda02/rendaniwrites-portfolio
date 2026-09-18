---
date: 2026-09-19
title: "What owning a documentation platform taught me about proof of concept"
description: "The five things I test before a new tool earns a place in the pipeline, and the one that matters most."
tags: ["documentation", "proof-of-concept", "workflow", "localization", "risk-management"]
---

How do you know a new tool or workflow actually belongs in your pipeline, before you spend time babysitting it?

I've spent the last few years owning a documentation platform: not just the pages, but the infrastructure and process a team runs on every day. Every tool I added had to answer that question first, by fitting into the infrastructure already there, not building around it.

## Proving the pipeline could scale

Two projects tested that early: a migration that kept the team working through a structural change without anything breaking underneath them, and a consolidation that pulled scattered documentation into one system without forcing the team to run two systems at once.

Localization is the clearest example. It wasn't added beside the existing pipeline. It was built into it. We launched an MVP in under two sprints. A year later, the same solution is translating other documentation, and the pipeline underneath it hasn't changed.

Each one has a full case study: [the documentation migration](/work/documentation-platform-migration), [the API consolidation](/work/api-consolidation), and [the documentation localization](/work/localisation-project).

## What a proof of concept actually tests

What made these projects work, and the infrastructure underneath them scale, was the same thing every time: the proof of concept (PoC).

A PoC is a small-scale test of whether a new tool or workflow belongs in the pipeline. Here are the five things I do when I run a PoC:

- **Validate functional assumptions**: whether the concept actually solves the problem it's meant to solve
- **Test technical feasibility**: whether the existing infrastructure can support it
- **Surface potential blockers early**: the bugs and challenges you'd only find by looking, before they stop a launch
- **Collect real data, in real time**: not theoretical scenarios, but actual behavior under actual conditions
- **Check fit against team needs**: not just whether it works, but whether it works for how this team already works

That last one is the one I think matters most, whatever the tool or workflow.

Most people evaluate a tool by its features: what it can do, how impressive the capability list looks, whether it checks the boxes. What gets missed is whether any of that serves the team running it day to day.

Features aren't the same as fit. Fit means the team can run it the way they already work. Choosing features over fit is how a tool passes every check on paper and still leaves the team babysitting it later.
