# Portfolio writing style — reference

Companion to `../SKILL.md`. Mechanical rules live in Vale (`.vale.ini` + `styles/`), not here — this file only covers what a linter can't decide.

## Source priority

This site no longer depends on Vale's Google package at all — `.vale.ini` is just `BasedOnStyles = Portfolio`, and `styles/` only contains `styles/Portfolio/`. This was a deliberate simplification, not an oversight: `vale-cli/vale-action` fetches the full ~31-rule Google package fresh at CI runtime regardless of what's committed locally, so relying on Google's package while trying to exclude most of it turned into a real bug (`Google.FirstPerson`/`Google.We` flooded a real PR with dozens of results even after their files were deleted locally). Rather than keep fighting that, everything worth keeping was copied into `styles/Portfolio/` as permanent, frozen rule files, and the Google dependency was dropped entirely.

1. This user's personal overrides — everything in `styles/Portfolio/*.yml` is now the entire rule set, no priority conflicts to resolve against an external package anymore.
2. Google developer documentation style guide (`developers.google.com/style/*`) — still the default reference for *judgment calls* the skill makes (verify live rather than from memory), just no longer a live Vale dependency.

**Explicitly not adopted** (specific to product/API documentation, not portfolio-relevant): the "[condition], email the X team at \<address\>" support lead-in pattern; "via" restricted to "via our API"; error-message double-quote formatting convention; UI-element sentence-case rule (revisit only if a blog post ever walks through a specific tool's UI).

**A separate, fuller Vale-on-Google setup is a distinct future project**, not part of this portfolio — worth building for professional technical-writing work (e.g. a work-report or client-facing docs repo) where the full ~31-rule Google package would genuinely apply, rather than fighting it down to a handful of rules like this personal site needed.

**Vendored from Google, now permanent `styles/Portfolio/` copies (the only ones that ever fired on real content):**

| Rule | Why it earned a spot |
|---|---|
| `Acronyms` | Flags acronyms used without a spelled-out first-use form; caught real cases ("SSO", "REST") |
| `Passive` | Suggests active voice; caught 8 real instances across the case study and blog posts |
| `Contractions` | Suggests contractions ("do not" → "don't") — matches this site's informal, conversational voice; caught 1 real instance. Uses a shorter swap list than Google's original (missing "what is," "how is," "they are," "we are," "we have," "were not," "when is," "where is") — a deliberate choice to keep the original shorter list rather than Google's fuller one. |
| `Periods` | No periods in acronyms/initialisms (e.g. not "U.S.A.") — added preemptively alongside the proven three, hasn't fired yet |

Everything else Google's package offered (`Gender`, `GenderBias`, `HeadingPunctuation`, `Ordinal`, `Quotes`, `Semicolons`, `Slang`, `Spacing`, `Spelling`, and the ~17 rules already excluded before the full drop — `EmDash`, `FirstPerson`, `We`, `Headings`, `Exclamation`, `Parens`, `WordList`, `Colons`, `Latin`, `AMPM`, `DateFormat`, `Ellipses`, `OptionalPlurals`, `LyHyphens`, `Ranges`, `Units`, `OxfordComma`) was dropped rather than migrated — none had fired on real content, and migrating unproven rules "just in case" was exactly the kind of shiny-over-useful tooling this project is trying to avoid. Add more from Google's package later, one at a time, only once something real demonstrates the need.

## What Vale already owns (don't re-derive by hand)

Run `vale <file>` and fix what it reports before doing any judgment-level work. Covered mechanically, all via `styles/Portfolio/`:
em dashes · ampersands · corporate jargon ("reach out," "circle back," "touch base," "leverage") · "allow" vs. "let" · "e.g." comma placement · contractions (this site prefers them — informal, conversational voice) · acronym-used-without-definition (`Portfolio.Acronyms` for 3-5 letter caps, `Portfolio.Abbreviations` for lowercase shortenings like "infra") · heading sentence case (`Portfolio.Headings`, `warning` level — proper nouns like Git/Hugo/GitHub/Vale/API/Crowdin/Stoplight, the pronoun "I," and known names like "Javier" are exempted, but new person names will still need review since they can't be pre-listed) · "docs" vs. "documentation" (`Portfolio.DocsTerminology`, `suggestion` level — flags every instance for manual review, never auto-replaces, since informal "docs team" is fine but narrative prose sometimes reads better as "documentation") · passive voice · no periods in acronyms.

## Hybrid judgment (a fixed rule exists, but applying it needs judgment)

Not Vale-flagged anymore (no `Google.Semicolons`/nominalizations rule is vendored), but these are still fixed preferences, not open judgment calls — the "hybrid" part is applying the rule correctly, not deciding whether it applies:

- **Semicolons.** Default to splitting into two sentences unless the two clauses are tightly parallel and a semicolon genuinely reads better than a period. Never use a semicolon to join anything that isn't two independent clauses.
- **Nominalizations.** Watch for noun-of-a-verb constructions ("made the decision" → "decided") and rewrite them — judgment is in how the resulting sentence flows, not whether to do it.
- **Numbered vs. bulleted lists.** Numbered only when order matters (a process/sequence); bulleted otherwise — requires judging whether a given list is actually order-dependent.
- **List parallelism.** Items in one list should be grammatically and conceptually parallel (all gerund-led, all fragments, etc.) — a semantic/grammatical judgment, not a regex match.
- **Numbers — the "scannable stat" exception.** Default: spell out zero through nine, numerals for 10+. Override: any number functioning as a scannable stat or metric — team size, page counts, results, percentages, the kind featured in a `description` field or a "Key results" list — always uses numerals, regardless of magnitude ("a 7-person team," not "a seven-person team"). Ordinary narrative numbers follow the default.

## Skill-only judgment (no fixed rule at all, pure context)

- **Site-wide terminology and language consistency (primary).** Before or after editing any file, check how the same term, tool, or concept is described elsewhere on the site — not just within the file being edited. Examples: is "infra" always expanded the same way on first use across pages, not just on the one page being edited? Does one project call it "product manager (PM)" while another spells it differently? Is the voice/tone consistent between the resume's achievement bullets and a case study's narrative, allowing for the genre difference between the two? Vale checks a single file in isolation; only this skill compares across files.
- **Cross-document redundancy.** Scan the rest of the page (and sibling files in the same content section) for a claim or phrase restated in two places — a smell worth flagging, not necessarily auto-deleting.
- **Structural consistency.** When one section's heading/list pattern diverges from its siblings on the same page, flag it and propose a fix — but don't force uniformity if the divergence is doing real work (e.g. a "Key results" list legitimately looking different from narrative prose).
- **Iterative meaning refinement.** When working from rough or dictated user input, especially on scope/impact claims, reflect the rewritten sentence back and confirm intent rather than treating the first grammatical polish as final.
- **Cross-file investigation.** For questions about why a Hugo template renders something a certain way, grep `layouts/` and read the actual templates — don't guess from general Hugo knowledge.
- **Narrative-to-competency synthesis.** When inferring `tags` for a case study, read the full narrative and name the skill actually evidenced (e.g. "stakeholder-management"), rather than keyword-matching nouns already in the text. Cross-check against tag vocabulary already used in other `content/projects/*.md` files.
- **Audience-targeted copywriting (secondary).** When choosing between draft `description` sentences for one specific piece of content, optimize for a hiring manager skimming project listings quickly — lead with scope and concrete outcome. Don't let this override site-wide consistency; a punchy one-off phrasing that breaks how a term is used everywhere else still needs to lose to consistency.
- **Sentence length.** No fixed word cap — it depends on the section. `content/projects/` (case studies, resume-style scannability) benefits from tighter sentences; a long one is worth flagging and offering to split. `content/blog/` is conversational, first-person storytelling, where a longer flowing sentence can be the right choice — don't force a split just to hit a number there.
- **Verify against an authoritative source before asserting.** Whenever a style question isn't answered by Vale's output or this file, WebFetch the relevant `developers.google.com/style/*` page (or, for a Vale rule mechanics question, `vale.sh/docs/*`) rather than answering from memory.
