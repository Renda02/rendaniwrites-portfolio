---
title: "Documentation platform migration"
description: "Learn more about how I led a team of 7 people through a documentation platform migration with zero breaking changes."
tags: ["documentation", "migration"]
---

## Background

I joined the company during a restructuring. The documentation team was merging the technical writing and training teams into one. 4 months into my new role, 2 of our technical writers left the organization. One of them had been leading the migration.

I was then assigned to lead the migration. This meant:

* Moving 4,000 to 5,000 pages of product documentation onto one platform with zero breaking changes
* Designing a new pipeline from scratch
* Establishing new ways of working between docs, the product manager, and engineering

This was my first time leading a documentation platform migration.

---

## What we were solving for

**The problem:**
- Documentation was split across disconnected tools: written and maintained in wiki pages, published separately through a publishing tool, with other content stored separately in version control
- Because these tools weren't linked, clients had to search across separate systems to find information, and splitting documentation across different platforms made it harder to find what they needed
- PM and engineering worked from different spaces with different tool constraints, which slowed collaboration

**What we were aiming for:**
- Streamline collaboration between PM and the docs team, letting PMs contribute directly through the authoring tool, with the docs team reviewing
- Move to one platform instead of several, with writing, maintaining, and publishing happening in the same place
- Make documentation easy to find, and reduce the cognitive load on users from moving between tools when searching for information

---

## Getting oriented: scoping the migration

I joined after the team had already selected the authoring tool, so choosing the tool wasn't part of my job. It was learning it fast enough to lead everyone else through it. I split my time between learning the new tool and auditing our existing documentation and migration requirements, since I needed both to plan the work.

Learning the tool also meant understanding where the team could locally maintain, write, and collaborate day to day, not just what the tool technically supported.

This scoping work surfaced the real shape of what needed to happen:
- The new tool didn't support some formatting the old tool did, like merging tables, so some content needed updates before it could move over
- 600 redirects needed mapping so links didn't break
- New domain structures needed alignment
- Engineering support was needed to build the pipeline, and infra approval was needed before we could migrate

---

## Planning the migration

Once I understood the tool and the scope, the priority shifted to enabling the team and getting everyone onboarded, while making sure other teams could keep supporting and maintaining docs and releases in the meantime.

I aligned with the PM on:
- The content freeze window and the rollback plan, both worked through together until we agreed on an approach
- The new domain structure, which was mine to own: I came up with options, tested them, and showed her how they'd work
- The pipeline design, which was mine alone

**Content freeze.** A 24-48 hour freeze window timed right after the release cycle, communicated to stakeholders in advance so no one expected content updates during launch week.

**A rollback safety net, not a hard cutover.** I kept the legacy platform running in parallel on launch day while redirects pointed to the new pages, giving a live 24-hour window to verify everything worked before disabling the legacy platform entirely.

**The end-to-end pipeline.** Content is authored in the new tool, which syncs to a develop branch in version control, then flows automatically through to production on release, with docs stored as markdown files throughout.

---

## Bringing stakeholders in early

None of those decisions worked in isolation. I also had to bring the right people in early, not just build the plan alone.

I believe in bringing docs allies in early rather than presenting a finished plan.

**Aligning on the why, not just the what.** One of the underlying reasons for this migration was to let PMs contribute directly through the authoring tool instead of going through a documentation request channel, with the docs team reviewing. That reasoning needed clear, early communication so people understood why this mattered.

**Communication channels.** My manager handled customer-facing communication with clients. I kept the team and stakeholders aligned through:
- A wiki-based one-pager tracking migration progress, accessible to anyone in the org
- A process guide covering how the team would work going forward, which I used to train 22+ PMs on the new tool before launch

**Getting technical sign-off early.** The pipeline needed sign-off from engineering and the infra team, plus IT and security approval for the SSO integration. I met directly with IT on SSO support and domain changes, and with engineering and infra on the pipeline itself, so sign-off came through without delays once we were ready to move forward.

---

## How I led the documentation team

At the time of the migration, we were a team of 7, including me: 4 technical writers and 3 people from the training team. I assigned tasks based on people's strengths rather than splitting evenly, since the team also had to keep maintaining existing documentation in parallel:

- One technical writer led content migration, working with an engineer who built a script to help move content into the new tool, and also owned information architecture, flagging anything that needed structural changes and keeping me aligned
- One technical writer led branding and the landing page redesign, aiming for consistency with the color scheme, terminology, and logo marketing was already using elsewhere
- Two training team members handled table and list cleanup. I explained the underlying rendering problem and showed them the tool, then let them decide how to split that work between themselves
- I owned all 600 redirects myself, the most detail-sensitive, highest-risk piece of the migration, manually mapped in the redirect configuration file and tested against the new repo structure

Review ran on two tracks:
- Peer-to-peer, for technical accuracy: the technical writer testing redirects verified all my redirects before launch, and minor formatting issues were peer-reviewed by the technical writer who owned information architecture
- Direct PM alignment, for anything with broader product impact: domain selection, redirect structure, breadcrumbs, and page look and feel all went through conversations with the PM before finalizing

Beyond individual workstreams, I made sure the team had a shared way of working. We defined branch naming conventions together, so everyone had a consistent approach going forward.

**Scale:**
- About 4,000-5,000 pages migrated across product, security, and restricted documentation
- 600 redirects total, accumulated from page merges, product launches retiring old URLs, and content updates over time

---

## Problem-solving under pressure

**Redirects at scale.** The new tool's redirect automation only went so far. Since URLs changed structurally across the migration, I manually mapped and tested each of the 600 redirects against the new repo paths.

**Formatting gaps.** The new tool didn't support merging tables the way the legacy tool did, so lists and tables rendered differently. I used it as a chance to collaborate with the training pair on how we'd approach tables going forward, then let them own the fix.

**Legal's redirects, post-launch.** Three links broke as a side effect of folding legal's docs into the unified knowledge base. I gave legal their own standalone space with its own domain path instead. Resolved within 24 hours.

---

## Key results

- 100% of content migrated at launch: a full lift-and-shift, no partial or phased release
- Unified writing, maintaining, and publishing into one system, eliminating manual handoffs across 2 or more tools
- Documentation became easier to find, with everything now searchable in one place instead of split across systems
- Defined a new docs lifecycle and process for the team, still in use 2+ years on
- Zero breaking changes across 4,000+ pages at launch, despite 600 redirects
- Trained and onboarded 22+ PMs onto self-serve authoring, now an active, adopted workflow
- Gained page-level feedback from readers, helping identify unclear documentation directly from user input

---

## What changed

| Before | After |
|---|---|
| Docs written in wiki pages, published separately through a publishing tool: two disconnected tools for one workflow | Writing, maintaining, collaborating, and publishing all happen in one tool |
| PMs drafted with a technical writer, then content was manually moved to the publish space | PMs and docs work in the new tool directly, with no manual handoff |
| Errors routed through a documentation request channel | PMs open a request, make the update, and tag the reviewer directly |
| Branches archived manually | Branches auto-archive on merge |
| No automated way to move content between environments | Content automatically syncs across environments on merge or release |
| Fragile version control, requiring careful manual attention | Fast, low-risk rollbacks, critical for customer-facing docs |

---

## What I'd do differently

Looking back, there are 2 things I'd change:

**Engage document owners like legal earlier and directly.** When I joined, I didn't fully understand that legal's documentation, specifically links tied to contracts, carried different stakes than general documentation. This is the same legal redirect issue mentioned earlier: I fixed it fast, but I'd rather have prevented it. If I'd built a direct line with legal from day one, instead of treating their content the same as everything else, we could have avoided the 3 contract links breaking after launch, rather than resolving it reactively within 24 hours.

**Involve engineering and infra earlier, during tool evaluation.** I joined after the team had already selected the tool. I believe involving engineering earlier could have helped surface its limitations sooner. It also would have helped us understand how much support we'd need from them during migration.
