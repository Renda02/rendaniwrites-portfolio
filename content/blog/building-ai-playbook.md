---
date: 2026-02-06
title: "How I built an AI playbook for clear communication"
description: "What an AI playbook actually is, and how I built one to stop rewriting the same stakeholder update for every audience."
tags: ["ai-playbook", "stakeholder-communication", "productivity"]
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

---

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

MYM follows the same trigger-inputs-steps-outputs shape as any playbook. It asks who you're talking to, what you need from them, and how you're sending it, only pushing back on anything sensitive or outside what a playbook should be writing. Then it matches your answers to a structure, Bottom Line Up Front (BLUF) for executives, Point-Reason-Example-Point (PREP) for technical recommendations, and drafts against it, checking that the ask lands in the first line or two before handing it back.

What comes back is a message ready to send, plus the framework it picked and why, so you don't have to make the same call twice.

---

## Master Your Message capabilities

Across every scenario, MYM adapts to how much you give it: structuring what's already complete, inferring what it can and saying so, and asking for what's missing when there isn't enough to infer.

Give it a full brief and it drafts straight away, framework named. Give it a vague one, like an API migration update with no audience specified, and it asks before writing a word.

---

## The results

Time isn't really the honest measure here: MYM drafts in seconds once it has your answers. The real payoff is how little time the message takes the reader to read and know what to do next. A clear message with the ask up front means they don't have to read it twice to know what you need from them. That's the whole case for a playbook like this: not speed, but not making the reader do the work you skipped.

If you're wondering where your own playbook might be hiding, check five places: your standard operating procedures, your calendar, your to-do list, your project planning, and your wishlist. Mine was sitting in plain sight. I just hadn't written it down yet.
