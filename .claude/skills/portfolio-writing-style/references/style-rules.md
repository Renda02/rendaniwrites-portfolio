# Portfolio writing style — reference

Companion to `../SKILL.md`. Mechanical rules live in Vale (`.vale.ini` + `styles/`), not here — this file only covers what a linter can't decide.

## Source priority

1. This user's personal overrides (`styles/Portfolio/*.yml`) — highest priority, override Google where they conflict.
2. This site's adopted deviations from Google, filtered to what's portfolio-relevant (encoded into `styles/Portfolio/`: em dash ban, "e.g." comma placement, contraction preference, single quotes in front matter).
3. Google developer documentation style guide (`developers.google.com/style/*`) — default base, verify live rather than from memory.

**Explicitly not adopted** (specific to product/API documentation, not portfolio-relevant): the "[condition], email the X team at \<address\>" support lead-in pattern; "via" restricted to "via our API"; error-message double-quote formatting convention; UI-element sentence-case rule (revisit only if a blog post ever walks through a specific tool's UI).

**Google rules excluded (deleted from `styles/Google/`, not merely disabled in `.vale.ini`), and why:**

| Rule | Why excluded |
|---|---|
| `EmDash` | Superseded by `Portfolio.EmDash` (total ban vs. Google's spacing-only check) |
| `FirstPerson`, `We` | This site is intentionally first-person narrative ("I led," "we migrated") — these rules assume neutral product docs addressing "you" |
| `Headings` | Superseded by `Portfolio.Headings` (adds "Git"/"Hugo"/"GitHub"/"Vale"/"I" exceptions, found missing when it flagged a real heading) |
| `Exclamation` | False-positived on a proper noun ("Aha!", a tool name) at error level |
| `Parens` | Too noisy for resume-style parentheticals |
| `WordList` | Too pedantic for informal personal prose (flagged "CLI," "admin") |
| `Colons` | Every real hit was a proper noun (company names) after a colon, never a real error |
| `Latin` | Contradicts `Portfolio.EgUsage` — this site keeps "e.g."/"i.e." as a deliberate deviation from Google, whose rule wanted to replace them |
| `AMPM`, `DateFormat`, `Ellipses` | No relevance to this site's writing (no time-of-day mentions, no slash-dates, ellipses may suit an informal aside) — pure error-level downside, never fired |
| `OptionalPlurals`, `LyHyphens`, `Ranges`, `Units` | Zero hits and no tie to any decision actually made for this site — generic Google defaults, not needed right away |
| `OxfordComma` | Regex heuristic can't distinguish a real list from an idiom ("mistakes and all") — its only real-content hit was a false positive |

**Google rules kept (currently in `styles/Google/`), and why:**

| Rule | Why kept |
|---|---|
| `Acronyms` | Flags acronyms used without a spelled-out first-use form; caught real cases ("SSO", "REST") |
| `Contractions` | Suggests contractions ("do not" → "don't") — matches this site's informal, conversational voice |
| `Gender`, `GenderBias` | Flags outdated binary/gendered constructs ("he/she", "mailman") — zero current relevance, but values-based and zero-conflict |
| `HeadingPunctuation` | No period at end of a heading — directly matches AGENTS.md's own existing rule |
| `Ordinal` | Spell out ordinals ("first," not "1st") in prose |
| `Passive` | Suggests active voice; matches this site's preference |
| `Periods` | No periods in acronyms/initialisms (e.g. not "U.S.A.") |
| `Quotes` | American convention: commas/periods inside quotation marks |
| `Semicolons` | Suggests reviewing every semicolon — see the soft preference under Hybrid judgment below |
| `Slang` | Flags internet slang (tl;dr, imo, fwiw) — named by the user as worth keeping |
| `Spacing` | Single space after sentence-ending punctuation — named by the user as worth keeping |
| `Spelling` | American spelling (colour → color) — matches this site's American English convention |
| `Will` | Avoid "will" in prose — matches this site's preference |

## What Vale already owns (don't re-derive by hand)

Run `vale <file>` and fix what it reports before doing any judgment-level work. Covered mechanically:
em dashes · ampersands · corporate jargon ("reach out," "circle back," "touch base," "leverage") · "allow" vs. "let" · "e.g." comma placement · contractions (this site prefers them — informal, conversational voice) · acronym-used-without-definition, both Google's built-in 3-5-letter-cap check and this site's `Portfolio.Abbreviations` conditional rule for lowercase shortenings like "infra" · heading sentence case (`Portfolio.Headings`, `warning` level — proper nouns like Git/Hugo/GitHub/Vale and the pronoun "I" are exempted, but person names will still need review since they can't be pre-listed) · "docs" vs. "documentation" (`Portfolio.DocsTerminology`, `suggestion` level — flags every instance for manual review, never auto-replaces, since informal "docs team" is fine but narrative prose sometimes reads better as "documentation") · passive voice · nominalizations (flagged, not auto-fixed — see Hybrid below) · semicolons (flagged for review, not banned — see Hybrid below).

## Hybrid judgment (Vale flags, this skill decides)

- **Semicolons.** Vale's `Google.Semicolons` rule suggests reviewing every semicolon ("use judiciously"). This site's preference: default to splitting into two sentences unless the two clauses are tightly parallel and a semicolon genuinely reads better than a period. Never use a semicolon to join anything that isn't two independent clauses.
- **Nominalizations.** Google's Vale style flags common noun-of-a-verb constructions ("made the decision" → "decided"). Rewriting still needs judgment on how the sentence flows afterward.
- **Numbered vs. bulleted lists.** Numbered only when order matters (a process/sequence); bulleted otherwise. Vale can't judge whether a given list is order-dependent.
- **List parallelism.** Items in one list should be grammatically and conceptually parallel (all gerund-led, all fragments, etc.). This is a semantic/grammatical judgment, not a regex match.
- **Numbers — the "scannable stat" exception.** Vale's baseline (via Google's style) spells out zero through nine and uses numerals for 10+. Override: any number functioning as a scannable stat or metric — team size, page counts, results, percentages, the kind featured in a `description` field or a "Key results" list — always uses numerals, regardless of magnitude ("a 7-person team," not "a seven-person team"). Ordinary narrative numbers still follow Vale's baseline.

## Skill-only judgment (Vale cannot do this at all)

- **Site-wide terminology and language consistency (primary).** Before or after editing any file, check how the same term, tool, or concept is described elsewhere on the site — not just within the file being edited. Examples: is "infra" always expanded the same way on first use across pages, not just on the one page being edited? Does one project call it "product manager (PM)" while another spells it differently? Is the voice/tone consistent between the resume's achievement bullets and a case study's narrative, allowing for the genre difference between the two? Vale checks a single file in isolation; only this skill compares across files.
- **Cross-document redundancy.** Scan the rest of the page (and sibling files in the same content section) for a claim or phrase restated in two places — a smell worth flagging, not necessarily auto-deleting.
- **Structural consistency.** When one section's heading/list pattern diverges from its siblings on the same page, flag it and propose a fix — but don't force uniformity if the divergence is doing real work (e.g. a "Key results" list legitimately looking different from narrative prose).
- **Iterative meaning refinement.** When working from rough or dictated user input, especially on scope/impact claims, reflect the rewritten sentence back and confirm intent rather than treating the first grammatical polish as final.
- **Cross-file investigation.** For questions about why a Hugo template renders something a certain way, grep `layouts/` and read the actual templates — don't guess from general Hugo knowledge.
- **Narrative-to-competency synthesis.** When inferring `tags` for a case study, read the full narrative and name the skill actually evidenced (e.g. "stakeholder-management"), rather than keyword-matching nouns already in the text. Cross-check against tag vocabulary already used in other `content/projects/*.md` files.
- **Audience-targeted copywriting (secondary).** When choosing between draft `description` sentences for one specific piece of content, optimize for a hiring manager skimming project listings quickly — lead with scope and concrete outcome. Don't let this override site-wide consistency; a punchy one-off phrasing that breaks how a term is used everywhere else still needs to lose to consistency.
- **Sentence length.** No fixed word cap — it depends on the section. `content/projects/` (case studies, resume-style scannability) benefits from tighter sentences; a long one is worth flagging and offering to split. `content/blog/` is conversational, first-person storytelling, where a longer flowing sentence can be the right choice — don't force a split just to hit a number there.
- **Verify against an authoritative source before asserting.** Whenever a style question isn't answered by Vale's output or this file, WebFetch the relevant `developers.google.com/style/*` page (or, for a Vale rule mechanics question, `vale.sh/docs/*`) rather than answering from memory.
