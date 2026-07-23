---
name: portfolio-writing-style
description: Writing/editing judgment for anything under content/ (blog, projects, resume) that Vale's CI linting can't catch — site-wide terminology/language consistency, redundancy, structural consistency, tag synthesis, audience-targeted copy.
---

## Purpose

Vale runs the mechanical style checklist (`styles/Portfolio` — this site's own rules, several adapted from Google's developer documentation style guide) in CI on every PR touching any file under `content/` — em dashes, ampersands, acronym definitions, passive voice, heading case, and so on are already caught there, with zero AI reasoning involved. This applies uniformly across blog posts, project case studies, and the resume/work page, so the site reads consistently regardless of section. This skill exists for the parts Vale categorically cannot judge: whether the same term or concept is described the same way across different pages, whether a sentence restates something already said elsewhere on the page, whether a section's structure fits its neighbors, and — secondarily — which of several description drafts best serves a specific reader. Site-wide consistency (terminology, tone, phrasing) is the primary reason this skill exists; audience-targeted copywriting is a related but narrower concern for individual pieces of copy.

## When to use

- Drafting a new post under `content/blog/` or a new case study under `content/projects/`.
- Editing existing prose anywhere under `content/` (including `content/work/_index.md`, the resume page, and section `_index.md` intros) in a way that touches meaning, structure, or tone — not just fixing something Vale already flagged.
- Any content update at all, to check it uses terminology and phrasing consistent with the rest of the site (not just consistent within the one file being edited).

Skip when: the change is purely mechanical and Vale already flags it (just fix what Vale reported). Skip for non-content files (`config.toml`, `layouts/`, CSS) — this skill is about copy, not code. Skip for `AGENTS.md`-covered structure (file naming, image alt text, code-fence language).

## Body

1. **Read the target file in full** before editing — redundancy and structural-consistency judgment need the whole page, not just the paragraph being touched.
2. **Don't re-check what Vale owns.** If Vale hasn't run yet, run it locally (`vale <file>`) first and fix anything it reports before doing judgment-level work — see `references/style-rules.md` § What Vale already owns for the full list, so you're not re-deriving "is this an em dash" by hand.
3. **Apply the hybrid rules** in `references/style-rules.md` § Hybrid judgment — these are cases where Vale flags something but a fixed rule can't finish the job: semicolons Vale suggested reviewing, nominalizations Vale's word list caught, numbered-vs-bulleted list logic, list parallelism, and the "numbers as scannable stats" exception (team size/page counts/results always use numerals, even under 10, overriding Vale's baseline spell-out-0-9 rule).
4. **Run the skill-only heuristics** in `references/style-rules.md` § Skill-only judgment: cross-document redundancy, structural consistency across sections, cross-file investigation (e.g. why a Hugo template renders something a certain way — read `layouts/`, don't guess), audience-targeted copywriting for the `description` field, and narrative-to-competency tag synthesis for case studies.
5. **Verify before asserting.** Whenever a style question comes up that isn't answered by Vale's output or this reference file, WebFetch the relevant `developers.google.com/style/*` page rather than answering from memory — this caught a wrong assumption in the session that produced this skill. If it resolves a genuinely new rule worth keeping, propose adding it to `references/style-rules.md` (or as an actual Vale rule in `styles/Portfolio/`, if it's mechanical) rather than re-deriving it next time.
6. **For case studies**, do one more pass after the above: does the `tags` front matter reflect skills actually evidenced in the narrative (e.g. "stakeholder-management" from a legal/PM/engineering coordination story), not just nouns already present in the text? Cross-check the resulting vocabulary against tags already used in other `content/projects/*.md` files.
7. **Flag conflicts, don't silently resolve them.** If applying a rule here would mean rewriting already-published content site-wide, surface it to the user instead of doing it unilaterally.
8. **Report changes grouped by rule/heuristic** (e.g. "tightened the redundant sentence in Key results," "picked the outcome-first description angle") so changes are auditable.

## Inputs

- The content file(s) being drafted or edited (`content/blog/*.md`, `content/projects/*.md`).
- `references/style-rules.md` (this skill's own reference file).
- `vale <file>` output, if available, for what's already been mechanically checked.
- `AGENTS.md` (repo root) for structural conventions this skill doesn't duplicate.
- Live `developers.google.com/style/*` pages, fetched on demand when a rule needs verifying.

## Outputs

- Edited content file(s) reflecting judgment-level fixes (Vale's own mechanical fixes are separate — apply those first).
- A short changelist in the reply, grouped by rule/heuristic.
- Any newly-verified style rule flagged for the user to fold into `references/style-rules.md` or a real Vale rule.

## Worked example

Editing `content/projects/documentation-platform-migration.md`: Vale already flagged "infra" as used without its spelled-out form appearing anywhere on the page (`Portfolio.Abbreviations`) and "SSO" as worth spelling out (`Portfolio.Acronyms`) — both get fixed per Vale's report, no judgment needed. Separately, the skill's redundancy heuristic catches that a sentence in "What I'd do differently" restated something already said in "Key results" — Vale has no way to know that, since it requires holding the whole page in view. The skill also picks which of three drafted `description` sentences best sells the project to a hiring manager skimming case studies, weighing scope-of-leadership and concrete-outcome signals — a judgment call Vale can't make either.
