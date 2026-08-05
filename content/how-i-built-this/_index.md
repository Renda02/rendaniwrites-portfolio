---
title: "How I built this"
description: "How this site was built with Claude Code, and the decisions and judgment calls the tooling couldn't make for me."
---

This site shows both my professional work and demonstrates what documentation governance actually looks like once it's built into a pipeline.
 
## My vision
 
A few months ago, I was part of a team building an agent to draft technical documentation. Drafting itself was never the hard part. The agent could generate fast, confident writing without effort. What it couldn't do reliably was hold onto what was already right while incorporating new feedback, and that left me with questions I couldn't answer with generation speed alone:
 
- Can you depend on what AI wrote after multiple rounds of changes?
- Who owns it when it's wrong?
- Who makes sure it stays accurate as the product changes under it?
This repo is my answer, built at the smallest possible scale I could test it at: one person, one pipeline, and a hard rule that nothing ships without a human reviewing it first.
 
## What I built
 
I built this with Claude Code. I used Trello to track my planning, one task at a time. Every change had its own branch and merged only through a pull request.
 
The pipeline has two layers.
 
**Deterministic**: image naming, PR syncing, repo diagram, stale-PR notices, and Vale. These run on their own in continuous integration (CI), triggered by a pull request or a schedule.
 
**Probabilistic**: three Claude skills, `/site-updates`, `/style-check`, `/voice-and-tone`. Each one is triggered manually and hands the decision back to me.
 
For the full breakdown, see [the pipeline overview](/pipeline/#what-each-layer-demonstrates) and [the README](https://github.com/Renda02/rendaniwrites-portfolio).
 
## What I learned
 
What I actually learned wasn't about building documentation infrastructure. It was about understanding why I needed it before building anything, including before copying anyone else's approach to a page like this one. That's also why the skills here didn't start from a description of what a good skill should do. `voice-and-tone` came from watching a real draft get reviewed and corrected, live, and only got written down once an actual pass worked, not before. The corrections mattered more than the successes: a skill that's never been wrong hasn't actually been tested yet.
 
## Conclusion
 
Going back to the questions I opened with: can you depend on what AI wrote after multiple rounds of changes, who owns it when it's wrong, who makes sure it stays accurate as the product evolves. That's my actual answer. Not a policy that states who's accountable, but a skill built from watching a real correction happen, live, instead of from a description of what accountability should look like.
 
Models keep getting better. That's real, and it's not really the point. A better model doesn't remove the need for someone to keep checking, it just changes what's worth checking for. The correction loop and the manual review stay necessary regardless of how good the underlying model gets, because neither one exists to catch the model being incapable. They exist to catch it being confidently wrong in a way that reads as right, which a stronger model is just as capable of doing, maybe more convincingly.
 
That's the actual mechanism behind "ongoing." Not me remembering to keep checking, but the check itself changing shape every time it's wrong. Trust and consistency don't come from the tooling alone. They come from a loop that keeps updating, and someone still deciding, every time.
 
## Further reading
 
For the technical mechanics, see [this site's pipeline overview](/pipeline/#what-the-pipeline-does) and [this repository's README on GitHub](https://github.com/Renda02/rendaniwrites-portfolio).
 