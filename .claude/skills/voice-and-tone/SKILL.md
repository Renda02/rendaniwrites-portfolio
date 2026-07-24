---
name: voice-and-tone
description: Checks a blog draft for one clear goal, solid structure, and a strong ending. Use when drafting or reviewing a post, or judging whether it "sounds like me."
---

## Purpose

Checks how a single post reads: does it have one goal, is it structured well, does it end strong. It does not check front matter, tags, or whether the site builds: that's out of scope here. It also doesn't check terminology or consistency across pages: see `style-check` for that.

Scope: `content/blog/` only, for now.

## When to use

- Drafting a new post under `content/blog/`.
- Reviewing an existing draft before publishing.
- Checking whether a post "sounds like me" or "has a strong ending."

Skip when: checking site-wide terminology or consistency across pages (that's `style-check`), or checking tags, description length, front matter, or whether the site builds (out of scope here).

## Body

1. **Pick one goal.** Every post does exactly one of these:
   - **Inform / update** — something changed and the reader needs to know it: what changed, why it matters to them, what's different now. Once told, stop — don't also sell something else in the same post.
   - **Educate / up-skill** — the reader should know or think something new by the end. Be clear first on what they already know, so you know what's actually new to add.
   - **Convert / act** — the reader should do something specific: click, try a workflow, reach out, subscribe. Include only what they need to see to act, nothing else.

   If a draft is doing two of these at once, that's a problem to fix, not a style choice. Name the goal before checking anything else.

2. **Check the post against 3 things:**
   - **Outcome up front** — does the post say, early on, what the reader will get out of it? About the reader, not about what you did.
   - **One strong, specific idea** — does the post have one real, specific idea (not something generic), with enough space to land, instead of being rushed or split across sections?
   - **A clear ending** — does the post end on one clear line, the thing you actually want the reader to remember? Not a list, a table, or something else competing with it.

   Score it: 2 or 3 strong means the post is ready. 0 or 1 strong means it isn't — that needs real work before anything else (SEO, front matter) is worth touching. Always name which of the 3 are strong or weak, pointing to the exact line or section — never give one overall score.

3. **Check post-type traits.**
   - **Explainer posts** (like "How Git works"): open with a question the reader's probably already asking; read like "here's what I learned," not a textbook; end by linking to a related post; close with short, plain sentences.
   - **Personal story posts** (like "How I became a solo technical writer"): the story itself pulls the reader in, no question needed to open; the single strongest detail gets its own moment, not buried in a longer paragraph; if naming people at the end, bridge back to the point first so it doesn't read as a random list; the lesson is the literal last line, nothing after it.
   - If a draft is a new type that isn't either of these, don't force it into one of these patterns — flag it as new and work out its own rules from the real draft.

4. **Check the shared-voice rules:** contractions ("don't," "you're"), not formal language; explained through real personal experience, not the abstract; image alt text that's actually descriptive, never generic.

5. **Report the review** using the Output format below. Suggest one small fix per problem — a merge, a reorder, a cut — not a full rewrite. If it's a bigger call (like which detail to lead with), flag it and let the author decide.

6. **Fold in corrections.** If the author corrects something this skill said, that correction becomes the new rule going forward — update this file's post-type or shared-voice notes so the same miss doesn't happen next time, rather than applying the fix just once.

## Inputs

- The blog draft being reviewed, from `content/blog/*.md`.
- Other posts already in `content/blog/`, for matching against the explainer/personal-story patterns above (or spotting a genuinely new post type).

## Outputs

A review report in this exact shape:

```
Post type: [explainer / personal story / new type: say what's different]
Goal: [inform / educate / convert / mixed: flag if it's doing more than one]

1. Outcome up front: [strong / weak] - [where]
2. One strong idea: [strong / weak] - [where]
3. Clear ending: [strong / weak] - [where]

Result: [X of 3 strong] -> [ready / not ready yet]

What's there: [list]
What's missing: [list]

Suggested fixes:
- ...
```

Never rewrite the whole draft — point things out, suggest small fixes, and let the author make the call. Any correction from the author gets folded back into this file's notes (per Body step 6), so the skill improves over time.

## Worked example

Reviewing `content/blog/how-git-works.md`: classified as an explainer post, goal educate/up-skill. Outcome-up-front was strong ("Did you know that Git stores your changes in 4 different locations, not two?"). One-strong-idea was flagged weak: the closing "Other essential commands" section adds `git switch`, which is about branching and doesn't fit the four-location model the rest of the post builds. Clear-ending was flagged weak: the real takeaway line isn't the last line — the post continues into a CTA sentence with a trailing anecdote clause. Result: 1 of 3 strong, not ready yet. Suggested fixes: cut or reframe the `git switch` bullet, and move the takeaway sentence so it's the literal last line.
