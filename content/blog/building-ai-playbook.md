---
date: 2026-02-06
title: "How I built an AI playbook for clear communication"
description: "What an AI playbook actually is, and how I built one to stop rewriting the same stakeholder update for every audience."
tags: ["ai playbook", "communication", "cross-functional-collaboration", "productivity"]
---

Have you ever tried to delegate something, only to think: never mind, it's faster if I just do it myself?

That's what happens when the instructions only ever lived in your head. A playbook writes them down once, so handing the task off, whether to a person or to AI, stops being slower than doing it yourself.

## What is an AI playbook

Think of it like an employee handbook, but for AI: instead of explaining a task from memory each time, you write it down once, and AI follows it the same way a new hire would follow a handbook.

Every playbook breaks down the same way:

- **Trigger**: what kicks it off
- **Inputs**: what AI needs from you each time
- **Steps**: your actual process, broken into tasks
- **Outputs**: what AI hands back to you

A playbook isn't something you get right the first time, either. You write an instruction, run it, and see where the output misses: too formal, too long, the wrong detail emphasized. Then you tighten the instruction and run it again. It's never really finished. It's just accurate enough, for now, for the task you built it for.

---

I put this into practice by building Master Your Message (MYM), an AI playbook for one specific repeat task: communicating with stakeholders. I built it during Rachel Woods' Think Like an AI Operator Challenge, and it's become my daily tool for stakeholder communication. It's live as a Custom GPT: you can [try it yourself](https://chatgpt.com/g/g-69336ddacc8481919cf45c2120c6b6b8-mym-master-your-message/).

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

**Trigger**: You need to send a message to a stakeholder.

**Inputs**: MYM needs three things before it drafts anything: who you're talking to, what you need from them, and how you're sending it. It asks for whatever's missing, and only that. If your first message already answers two of the three, it asks just the one that's left; if you give a vague answer, it tells you exactly what it still needs before it'll draft.

**Steps**:

1. **Safety check.** Before generating anything, MYM screens for two different kinds of risk, with two different responses:
   - **Sensitive info or unprofessional language** (passwords, tokens, customer names, confidential details, profanity, harassment): MYM pauses and asks you to rephrase, then continues.
   - **Legal, HR, or compliance risk** (firing someone, terminating a contract, reporting misconduct, medical information, security breaches): MYM **won't draft anything**. It stops and directs you to your manager or HR instead. This isn't a message a playbook should be writing for you.

2. **Framework selection.** Based on your answers, MYM matches your scenario to the right structure:
   - **Bottom Line Up Front (BLUF)**: for executives needing decisions
   - **Point-Reason-Example-Point (PREP)**: for technical recommendations
   - **Observation-Impact-Question**: for feedback in 1:1s
   - **Before-After-Bridge**: for showcasing results

3. **Draft.** MYM writes the message using the selected framework's structure. For BLUF: the ask up front, 2-3 sentences of context, then next steps. For PREP: point, reason, example, restated point.

4. **Quality check.** Before delivering, MYM checks that the ask is in the first 1-2 sentences, that it follows the framework, and that it's free of AI fluff. If any check fails, it flags the draft and offers to regenerate.

**Outputs**:
- Framework-structured message, ready to copy and send: no labels, no placeholders left in
- The framework choice named and explained, so you know why it picked BLUF over PREP
- A record of which framework fit which scenario, so the same decision doesn't have to be re-made next time

This is also why MYM doesn't need a separate playbook for every message type. A status update, a risk escalation, and a piece of feedback all share the same trigger, inputs, and safety/quality steps. Only the framework in step 2 changes. One playbook, several outputs, instead of a stack of near-identical documents.

MYM will also show its work on request. Ask why it picked a framework, and it doesn't just name one: it maps your own draft back onto the framework's structure line by line ("Point: ...", "Reason: ...") and explains why each piece fits your scenario. It's not just drafting the message; it's teaching you the framework using your own words as the example.

---

## Example

I asked MYM to help propose a Crowdin integration to our infrastructure team. Here's what came out the other end:

> "Hi [Tech Lead], I'd like to propose integrating Crowdin into our translation workflow. I believe this integration would automate translation updates, reduce the manual effort involved in checking and syncing translations, and make the overall process more reliable and efficient. For example, instead of manually verifying translation changes across environments, Crowdin could automatically synchronize updates with our repositories, helping us keep translations current while reducing the risk of missed or inconsistent updates. Given these benefits, I'd like to align with our infrastructure and architecture before moving forward. Do you think this approach would fit our current setup, or are there any considerations we should evaluate first?"

Here's the context that produced it. My input was a single messy sentence: I wanted to propose a Crowdin integration to a tech lead, to automate translation updates and cut down manual checks, sent via Slack, aiming for alignment on our infrastructure. MYM pulled the audience, goal, and format out of that on its own.

It also told me why it picked PREP over the other three frameworks, before drafting anything: *"Based on your playbook, this is a PREP scenario because you're proposing a technical solution and seeking alignment on an architectural direction."* Not BLUF, because this wasn't a yes/no decision for an executive. Not Observation-Impact-Question, because this isn't feedback. Not Before-After-Bridge, because there's no result to show yet, just a recommendation to make the case for.

The structure underneath the draft above is Point, Reason, Example, Point:

- **Point**: the ask up front ("I'd like to propose integrating Crowdin...")
- **Reason**: why it matters ("would automate translation updates, reduce the manual effort...")
- **Example**: concrete proof ("instead of manually verifying translation changes... Crowdin could automatically synchronize")
- **Point**: the ask restated as a question ("Do you think this approach would fit...")

106 words, no labels, ready to send: less than half the roughly 185 words an unstructured "just write this up" draft runs to, where the actual ask doesn't show up until the last sentence.

MYM also handles messages that don't specify audience or format up front. Asked to draft a proposal to a compliance manager about audit training, with no format stated, it inferred the details and said so before drafting: *"Format: I'm assuming this is an email."* Then it delivered a BLUF-style draft and offered to adjust it shorter, more formal, or for Slack instead.

That's an easy case, though: there was enough context to infer the gap. When a request is missing more than that, MYM doesn't guess; it stops and asks. I once wrote: *"I want to send project update to my manager about API migrations and ask support in getting infra involved to assist with domain switch... I will be sending an email."* No status update, no clarity on who else might be reading it. I answered two of the three details it needed in my next message. It came back asking only for what was still missing: *"One detail still missing: What is the current status of the API migrations?"* Only once I'd answered that did it draft anything. It won't paper over a vague ask with a generic draft. It makes you answer the questions first.

---

## The results

Time isn't really the honest measure here: MYM drafts in seconds once it has your answers. The payoff is the reader's, not mine. A clear message with the ask up front and only the necessary context means they don't have to read it twice to figure out what you want. That's the whole case for a playbook like this: not speed, but not making the reader do the work you skipped.

If you're wondering where your own playbook might be hiding, check five places: your standard operating procedures, your calendar (what do you do every week without fail?), your to-do list (what keeps showing up?), your project planning (what do you re-explain at the start of every project?), and your wish list (what have you been meaning to systematize but haven't?). Mine was sitting in plain sight. I just hadn't written it down yet.
