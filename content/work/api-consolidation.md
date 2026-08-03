---
title: "The API consolidation"
weight: 3
description: "Led an independent migration of six public APIs from Stoplight to GitBook, consolidating API documentation onto the company's main documentation platform and domain."
role: "API Documentation Lead"
team: "Feature teams, PM, Engineering, IT"
timeline: "Two sprints, proof of concept to launch"
intro: "Retiring a legacy API documentation tool under a hard vendor deadline, and folding API reference documentation into the same platform as the rest of the company's documentation."
impactSummary: |
  Led an independent API consolidation, migrating six public APIs in two sprints onto the same platform and domain as the rest of the company's documentation.

  Delivered cost savings by retiring a redundant tool, in collaboration with cross-functional teams, launching ahead of a hard vendor contract cutoff with no room for a parallel-run window.
tags: ["api", "documentation", "consolidation", "automation", "cost-savings", "stakeholder-management", "risk-management"]
---

## Overview

This case study covers an API documentation migration I led independently: moving public documentation for six application programming interfaces (APIs) from Stoplight to GitBook.

The project followed an earlier large-scale documentation migration I also led, moving 4,000+ pages onto GitBook with zero breaking changes and 600+ redirects. This project applied the same discipline to a smaller but technically trickier scope: live, spec-driven API reference documentation.

Scope: six public APIs, all authored from OpenAPI specs and previously published through Stoplight.

Unlike some documentation migrations, this one ran without a content freeze. The company had already agreed not to renew the Stoplight contract, which set a hard deadline that made an extended freeze or parallel-run window impractical. Launch landed just one to two weeks before that contract ended.

## The problem

Stoplight published API documentation, while GitBook already published the rest of the company's documentation, including product and security docs. That split meant API documentation delivered a noticeably worse experience than everything else.

A PageSpeed Insights audit of the existing API documentation showed this concretely: a performance score of 37 out of 100 on desktop, well below modern standards, with weaker accessibility and best practices scores as well.

With no shared navigation between Stoplight and GitBook, users couldn't move easily between API docs and the rest of the documentation, another blocker to the company's goal of one unified platform.

## The goal

- Bring all documentation, including APIs, onto one documentation platform instead of maintaining two, retiring Stoplight entirely.
- Reduce the number of separate documentation sites the company maintains.
- Deliver meaningful annual cost savings: the company was already paying for GitBook, so retiring Stoplight removed a redundant cost rather than adding a new one.

What looked like a straightforward tool swap turned out to have a hidden technical blocker, one that would have broken every API's documentation if it had shipped unnoticed.

## My approach

I led and managed this migration independently within the team, from technical discovery through execution. Here is how it unfolded.

### Aligning stakeholders early

Before any technical work started, getting this migration right required aligning the right people, not just after changes landed:

- **Infrastructure sign-off first:** before contacting any feature team directly, I briefed the principal architect responsible for the API infrastructure on the migration and the changes it would require, including whether the existing service account used for documentation sync could support the new tool. Once he was comfortable with the plan, he was fine with me communicating directly with the feature teams from that point on.
- **Product owners:** I contacted the product manager (PM) who owned each affected API, so every product owner knew the migration was happening and why, ahead of any changes landing.

This structure meant I aligned the people closest to each API early, before any change reached their roadmap.

### Working through infrastructure with IT

A lesson from that earlier migration: bring IT in before finalizing the plan, not after. So here too, I brought IT in early, ahead of any production cutover, to agree on how we'd handle the domain switch and understand GitBook's limitations and what IT could support:

- A domain redirection strategy to route traffic from the old documentation location to the new one.
- The web configuration required to support those redirects securely.
- A test session on a non-production domain to validate the full redirect and publishing flow before cutting production traffic over. That testing is what let us agree on a shared launch day, so the domain redirects would go live at the same time as the migration itself, rather than leaving a window where one could break without the other.

This early involvement was necessary because GitBook, as the authoring tool, has its own limitations around custom domains and redirects. Surfacing and resolving these constraints with IT ahead of time avoided a late-stage blocker at cutover.

### Running a proof of concept first

Before committing to a full rollout, I built a proof of concept covering all six APIs in scope, migrating their documentation into GitBook. To validate the new tool from a user's perspective, I brought in an engineer from the support team to interact with the migrated documentation directly and give feedback on how it looked and worked.

Integration testing during this phase revealed a critical blocking issue in how feature teams had structured the existing OpenAPI specs.

### The challenge

GitBook generates documentation pages strictly from the `tags` property on each OpenAPI operation. Stoplight didn't require this property. As a result, the current specs, which worked fine in Stoplight, produced broken output in GitBook. Pages rendered under a generic "Default" title instead of the actual endpoint name. In the worst case, GitBook generated no page at all. This issue affected the OpenAPI spec file for every one of the six APIs in scope.

Feature teams, not the documentation team, owned each API's OpenAPI spec. Fixing it meant engaging every team to update the spec they owned.

**Before: spec without tags**
```yaml
paths:
  /api/v1/act/execute:
    post:
      summary: Trigger a remote action
      # Missing tags property
```
This output wasn't usable as public-facing reference documentation.

**After: spec with tags**
```yaml
tags:
  - name: Remote actions
    x-page-title: Trigger a remote action
    x-page-description: Trigger and query remote actions using the API.

paths:
  /api/v1/act/execute:
    post:
      tags:
        - Remote actions
      summary: Trigger a remote action
```
With a top-level tags definition and a tags property on every operation, GitBook rendered each endpoint under a correctly titled, organized section, for example "Remote actions," with subsections such as Execute, Export, and Status. This replaced the single, unorganized page GitBook generated before.

### Getting the fix into feature teams' hands

I coordinated the tagging work across all six APIs, working with each owning team to:

- Add a top-level tags definition, with a page title and description for each tag.
- Add a tags property to every operation, so GitBook could render it correctly.
- Validate rendering after the changes landed, before moving to the next API.

This didn't go smoothly for every API. One feature team was in the middle of its own priority development work when the tagging request landed, and couldn't get to it on the migration's timeline. To keep the rest of the migration on schedule, I added the required tags to that team's spec myself, and the team took over ownership of maintaining them the following sprint.

### Automating the fix for the long term

During the proof of concept, I synced specs to GitBook manually, which was fine for a prototype but risks spec drift at scale, where published documentation quietly falls out of step with the actual API. In production, though, our documentation was already automatically synced with Stoplight. So this wasn't a new capability to build; it was something we had to replicate in GitBook, or the migration would have been a step backward.

To rebuild it, I defined the requirements and worked with engineering to build a GitHub Actions workflow that publishes each API's OpenAPI spec to GitBook automatically on every change, iterating through several rounds of testing before it worked reliably in production.

- Result: documentation stays current with the source of truth, the OpenAPI spec, with the same zero-manual-step experience the team had before the migration.

## Impact

This was a documentation and domain consolidation, not a change to the underlying APIs. The APIs themselves stayed the same; only the location and publishing method of their documentation changed.

### What changed

| Before | After |
|---|---|
| Docs published via Stoplight, on a separate subdomain | Docs published via GitBook, on the company's main documentation domain |
| Manual OpenAPI spec sync during testing | Automatic sync to GitBook on every spec change, via a CI/CD workflow |
| Endpoints missing tags rendered as "Default" or not at all | Every endpoint required tags, rendering under a correctly titled, organized section |
| Performance score of 37 out of 100 (PageSpeed Insights, desktop) | Performance score of 99 out of 100 |
| Documentation split across multiple tools and domains | Documentation unified in a single tool, on a single domain |

### Key results

- Delivered cost savings: the company no longer pays to maintain API documentation in a separate tool, on top of consolidating sites.
- The CI/CD pipeline outlasted the migration itself: new APIs added afterward joined the same GitHub Actions workflow automatically, keeping their documentation in sync without repeating the manual publishing process.
- Coordinated across multiple feature teams and IT to deliver the migration with a validated, low-risk cutover.

## What I'd do differently

The friction with that one feature team points to the first thing I'd change if I ran this again: bringing feature teams into the conversation as early as I brought in IT.

With IT, I started the conversation before there was a concrete plan, working through requirements and limitations together, and even brought them into calls with GitBook directly. That early involvement surfaced questions and constraints I wouldn't have known to ask about otherwise.

I didn't extend that same early involvement to every feature team, especially the one team I hadn't worked with before and had no existing working relationship with. Looping feature teams in earlier, before they locked in their own sprint planning, would have let them account for this work upfront instead of treating it as a late addition to already-committed priorities.

The second thing I'd change: after fixing the missing tags across all six specs, I never added anything to stop the same issue from coming back. The fix relied on every feature team remembering to add a tags property to any new endpoint they created. A Spectral or Redocly CLI rule in the GitHub Actions workflow, requiring both a tags property and the x-page-title and x-page-description extensions on every operation, would have caught this automatically for any team, on any future endpoint, instead of relying on memory.
