---
date: 2026-09-28
draft: true
title: "How voice dictation improved my AI workflow"
description: ""
tags: ["ai", "productivity", "workflow"]
---


Think about the last time you were discussing a project with a friend or a colleague, or brainstorming an idea out loud with someone. The words flowed. You gave the background, the reasoning, the back-and-forth of actually thinking it through. All of it, naturally, without stopping to structure it.

Now think about the last time you used Claude to brainstorm an idea, but typed it in instead. You compressed it. You skipped the context. Typing is slower, so you kept it short instead of giving it everything.

AI got a fragment, and it filled in the rest. Sometimes that guess lands close enough. Other times it's off, and you spend the next few messages going back and forth, correcting what you actually meant.

**The gap wasn't the AI guessing wrong. It was how little you'd actually given it to work with.**

So I stopped typing my prompts and started talking them through.

---

## Why typing cuts context

Here's why that gap happens in the first place.

In everyday conversation, we speak at around 125 words per minute on average ([How many words per minute does the average person speak?](https://www.mentalfloss.com/language/how-many-words-per-minute-do-people-speak)). When copying text, the average computer user types about 33 words per minute. But when we're composing, thinking and typing at the same time, that drops to just 19 words per minute ([Words per minute on Wikipedia](https://en.wikipedia.org/wiki/Words_per_minute)).

You can say something more than six times faster than you can type it out. Every second you spend typing, you're compressing your thinking. Cutting context. Losing detail.

Which is exactly what ends up missing from the prompt.

---

## When I use voice dictation

I reach for voice in a few specific moments:

- When an idea hits while I'm working, and I need to brainstorm it before I lose it.
- When I'm building context for a project: talking through the plan so I have something to work from.
- When I'm drafting something like a product requirements document (PRD) or a corrective and preventive action (CAPA) report, and I need to explain the scenario: who it's for, what the problem is, and how we'll resolve it.

That's how I built a PRD. I talked through the problem out loud instead of typing fragmented notes and trying to hold all the context in my head.

Typing it would have meant: Open a new session. Type a sentence. Delete it. Type another. Rephrase. Backspace. Start over. Twenty minutes later, I'd have a PRD full of gaps, one that somehow says less than what I said out loud in a few minutes. Instead: a quick voice dump, a short cleanup, and I had something usable.

---

## How I use voice dictation

I dictate into Claude:

1. Open a new session, then tap or hold the microphone icon to record.
2. Talk through the idea like I'm explaining it to a colleague. No structure, no editing myself mid-sentence, just getting the full thought out.
3. Ask for a cleanup: "Clean this up and organize it as a [blog post / project brief / plan]."
4. Review it. Claude handles the messy-to-structured part, and my job is just the final check.

That cleanup prompt is the same one every time, so I saved it as a skill and run it with `/cleanup` instead of retyping it. It only runs when I ask for it, because not every voice dump needs cleanup.

---

Next time you're about to type a rough brief or plan into Claude, try talking it through instead. Give it everything you'd tell a colleague, not just the summary. Then let Claude structure it. It's a small change, but it's the difference between a fragment and a full picture.
