---
date: 2026-02-06
title: "How I built an AI playbook for clear communication"
description: "What an AI playbook actually is, and how I built one to stop rewriting the same stakeholder update for every audience."
tags: ["ai-playbook", "clear-communication", "productivity"]
---

Have you ever tried to delegate something, only to think: never mind, it's faster if I just do it myself?

That's what happens when the instructions only ever lived in your head. A playbook writes them down once, so handing the task off, whether to a person or to AI, is no longer slower than doing it yourself.

## What is an AI playbook

Think of it like an employee handbook, but for AI: instead of explaining a task from memory each time, you write it down once, and AI follows it the same way a new hire would follow a handbook.

Every playbook breaks down the same way:

- **Trigger**: what kicks it off
- **Inputs**: what AI needs from you each time
- **Steps**: your actual process, broken into tasks
- **Outputs**: what AI hands back to you

A playbook isn't something you get right the first time, either. You write the steps, give AI the instruction to run the playbook, and see where it misses: too formal, too long, the wrong detail, and then you iterate until it's just accurate enough, for now, for what you built it to do.

To create an AI playbook, you don't need a dedicated platform. Write it once, as plain text, then run it wherever you like: a chatbot, an agent, a multi-agent system, a Custom GPT, or a Project.

---

I put this into practice by building Master Your Message (MYM), an AI playbook for one specific, recurring task: communicating with stakeholders. I built it during Rachel Woods' Think Like an AI Operator Challenge, and it's become my daily tool for stakeholder communication. It's now live as a Custom GPT: you can [try MYM yourself](https://chatgpt.com/g/g-69336ddacc8481919cf45c2120c6b6b8-mym-master-your-message/).

## Why Master Your Message

If you lead cross-functional initiatives, you know explaining context differs by stakeholder.

I kept doing two things that slowed me down:
- Burying key points in long paragraphs
- Not stating my ask clearly

I kept rewriting the same update for different stakeholders. Engineers wanted technical details upfront. Marketing needed business impact. Leadership just wanted the bottom line.

The problem wasn't that I didn't know *what* to communicate. I didn't know *how* to structure it for different people.

MYM stops that rewriting. I answer three questions once, and the structure comes out right the first time: no more guessing at how to phrase it for each audience.

---

## How Master Your Message works

The MYM playbook covers every message type, a status update, a risk escalation, feedback. Only the framework changes. Everything else stays the same. Here's how it works:

**Trigger**: You need to send a message to a stakeholder.

**Inputs**: MYM needs three things before it drafts anything: who you're talking to, what you need from them, and how you're sending it. It asks for whatever's missing, and only that. If your first message already answers two of the three, it asks just the one that's left; if you give a vague answer, it tells you exactly what it still needs before it'll draft.

**Steps**:

1. **Guardrail.** Before generating anything, MYM screens for two different kinds of risk, with two different responses:
   - **Sensitive info or unprofessional language** (passwords, tokens, customer names, confidential details, profanity, harassment): MYM pauses and asks you to rephrase, then continues.
   - **Legal, HR, or regulatory risk** (firing someone, terminating a contract, reporting misconduct, medical information, security breaches): MYM **won't draft anything**. It stops and directs you to your manager or HR instead. This isn't a message a playbook should be writing for you.

2. **Framework selection.** Based on your answers, MYM matches your scenario to the right structure:
   - **Bottom Line Up Front (BLUF)**: for executives needing decisions
   - **Point-Reason-Example-Point (PREP)**: for technical recommendations
   - **Observation-Impact-Question**: for feedback in 1:1s
   - **Before-After-Bridge**: for showcasing results

3. **Draft.** MYM writes the message using the selected framework's structure. For BLUF: the ask up front, 2-3 sentences of context, then next steps. For PREP: point, reason, example, restated point.

4. **Quality check.** Before delivering, MYM checks that the ask is in the first 1-2 sentences, that it follows the framework, and that it's free of AI fluff. If any check fails, it flags the draft and offers to regenerate.

**Outputs**:
- Framework-structured message, ready to copy and send: no labels, no placeholders left in
- The framework choice named and explained
- A record of which framework fit which scenario, so the same decision doesn't have to be re-made next time

---

## Master Your Message capabilities

Across every scenario, MYM adapts to how much you give it: structuring what's already complete, inferring what it can, and asking for what's missing.

Asked to help draft a recruiter follow-up ahead of an interview, with the audience and format already given, it picked BLUF and explained why: a senior audience, an email channel, a clear ask. The result was a clean, structured draft, ready to send.

When I don't specify format or audience, it infers what it can and says so, like assuming a compliance manager proposal was an email. When there's too little to infer, it doesn't guess: for a vague API migration update, it asked for what was missing before writing a word.

---

## The results

Time isn't really the honest measure here: MYM drafts in seconds once it has your answers. The real payoff is how little time the message takes the reader to read and know what to do next. A clear message with the ask up front means they don't have to read it twice to know what you need from them. That's the whole case for a playbook like this: not speed, but not making the reader do the work you skipped.

If you're wondering where your own playbook might be hiding, check five places: your standard operating procedures, your calendar (what do you do every week without fail?), your to-do list (what keeps showing up?), your project planning (what do you re-explain at the start of every project?), and your wish list (what have you been meaning to systematize but haven't?). Mine was sitting in plain sight. I just hadn't written it down yet.
