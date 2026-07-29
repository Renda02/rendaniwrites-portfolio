---
date: 2026-07-29
title: "How I built this"
description: "A technically correct AI suggestion, aimed at the wrong reader, and how I caught it."
tags: ["technical-writing", "ai-workflows", "docs-as-code"]
---

A title suggestion I got from an AI skill was clear, specific, and confidently reasoned. It was also aimed at the wrong reader, and I only caught it by reading closely enough to check. That's what this post is actually about: not a tour of the tooling behind this site, but the moment a technically correct answer still needed a human to say no.

## My vision

A few months ago, I was part of a team building an agent to draft technical documentation. The drafts came fast. The problem showed up whenever a human gave feedback: the agent would either regenerate the whole document from scratch and lose everything that was already right, or barely touch it and ignore what we'd just told it. There was no middle ground, and every round trip cost more tokens than the last.

That experience left me with questions that stuck:

- Can you depend on what AI wrote after multiple rounds of changes?
- Can you trace where a piece of information came from?
- Who owns it when it's wrong?
- Who makes sure it stays accurate as the product changes under it?

This repo is my answer, built at the smallest possible scale I could test it at: one person, one pipeline, and a hard rule that nothing ships without a human reviewing it first.

That ruled out building another agent from a description of the task. If a tool has never watched the work done correctly, it has nothing to calibrate against, which is exactly how you end up regenerating everything or ignoring feedback with no middle ground. So the rule for anything that became a skill here was the same one that caused the original problem, reversed: do the task yourself first, live, and correct it in real time when it's wrong. Only once there's an actual successful run do you write the skill, and it gets written from that specific session, not from describing the task in the abstract.

## The pipeline

I built this with Claude Code, planning each day's work one task at a time, each one its own short-lived branch, merged and reviewed on its own.

The pipeline has two layers: a deterministic layer and a judgment layer. Neither one is fixed by default. Both got shaped, and reshaped, by decisions I made along the way.

**Deterministic layer.** Runs automatically, triggered by a pull request or a scheduled job, as part of continuous integration (CI). Some of these gate the merge outright. Most don't, matching how much is actually at stake on a personal portfolio versus a team docs pipeline.

| Workflow | Runs when | What it does | If it fails |
|---|---|---|---|
| `vale.yml` | A pull request changes content | Checks spelling, terminology, and style | Comments on the pull request. Doesn't block it |
| `check-image-naming.yml` | A pull request adds an image | Checks the naming pattern | Blocks the pull request, with a visible red X |
| `auto-update-pr.yml` | Changes land on main | Syncs other open pull requests | Runs silently, unless a conflict needs me |
| `stale-pr-notice.yml` | Every Monday | Flags pull requests untouched for 2 weeks | A notice only. I decide what to do |
| `repo-visualizer.yml` | Changes land on main | Redraws the repo diagram | Cosmetic. Nothing else breaks |

These were among the first workflows I added, before the site even had a working homepage.

**Judgment layer.** 3 Claude skills, each one triggered either by typing its name directly or by asking something Claude recognizes as its territory, never on its own, unprompted. None of them rewrites a draft outright. Each skill reads the whole piece, names what's weak, and suggests one small fix, then hands the decision back to me.

| Skill | Runs when | What it does |
|---|---|---|
| `style-check` | I run it mid-draft | Catches site-wide inconsistency Vale structurally can't |
| `voice-and-tone` | I run it before publishing | Scores a draft on outcome, one idea, and ending |
| `site-updates` | I run it after a batch of commits | Drafts a changelog entry from the diff |

One of these, `voice-and-tone`, has a standing instruction that when I correct something, that correction gets folded back into the skill file itself, not just fixed once. That matters because product terms don't stay fixed either: as the product evolves, so does its language, and this is the loop that's supposed to catch up when it does.

## What I learned

None of the architecture above is the interesting part, though. Tooling is easy to copy. What isn't easy to copy is judgment, and judgment only shows up in the moments where a technically correct answer still needed a human to say no.

Reviewing the localization case study, `voice-and-tone` scored the draft 3 of 3 on its own framework and suggested the title lean into the idea doing the most work in the piece: "The Embedded Localization Pipeline." It wasn't wrong that the idea was strong. It was wrong about who'd be reading the title. Someone scanning a list of case studies for "has this person localized documentation before" needs that stated plainly, not inferred from the word "pipeline." I rejected the suggestion and landed on "Documentation Localization" instead, a plainer, less clever title that says exactly what a hiring manager is scanning for.

## Conclusion

It wasn't a dramatic failure. It was the ordinary kind: a suggestion that was correct on its own terms but missing context only I had.

What made it recoverable was that I read the output closely enough to catch it, and was willing to override a technically correct answer when it solved the wrong problem. The pipeline catches what a rule can catch. It can't catch the difference between a suggestion that's technically right and one that's actually wrong for this specific case.

Trust and consistency don't come from the tooling alone. They still need judgment, every time. That's still mine to decide.

## Further reading

For the technical mechanics, see [this site's pipeline overview](/pipeline) and [this repository's README on GitHub](https://github.com/Renda02/rendaniwrites-portfolio).
