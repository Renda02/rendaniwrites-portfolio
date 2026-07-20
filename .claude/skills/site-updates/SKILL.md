---
name: site-updates
description: Append a reader-facing "what's new" summary to the repo's CHANGELOG.md, built from recent git history. Groups changes by reader interest (new posts, new projects, site improvements), not by commit author or software version. Not published on the live site.
---

## Purpose

Convert a noisy `git log` into a short update a reader, recruiter, or follower would actually want to see, and keep a running record of it in `CHANGELOG.md` at the repo root. This is not a versioned software release — this site has no tags and no semver history, so grouping follows what changed for a reader, not `Added`/`Changed`/`Fixed` against a version number. `CHANGELOG.md` lives at the repo root (like `AGENTS.md`), not under `content/`, so Hugo never builds or serves it — it's a private log for you, not a public site section.

## When to use

- After publishing one or more new blog posts or project case studies.
- Before sharing a periodic update (e.g. a monthly recap, a social post, a personal changelog).
- Summarising a batch of commits since the last time you wrote one of these.

Skip when: the range only contains internal-only commits (`chore`, `ci`, `refactor`, `style`, `revert`) with no reader-visible effect.

## Body

1. Find `<since>`: read `CHANGELOG.md` at the repo root for the most recent `<!-- site-updates:through <sha> -->` marker and use that `<sha>` as the start of the range. If the file has no marker yet (first run), use the oldest commit reachable or ask the user for a starting point.
2. Get the input as `git log --oneline <since>..HEAD`, using this repo's commit types from `AGENTS.md` (`feat`, `fix`, `content`, `chore`, `style`, `ci`, `refactor`, `revert`).
3. Group changes into three buckets:
   - **New posts** — `content:` commits touching `content/blog/`.
   - **New projects** — `content:` commits touching `content/projects/`.
   - **Site improvements** — `feat`/`fix` commits that are reader-visible (navigation, broken links, UI). Skip internal-only fixes (build config, CI).
4. Drop `chore`, `ci`, `refactor`, `style`, and `revert` commits entirely unless they fixed something reader-visible, such as a broken build that had taken the site down.
5. For each post or project, pull its `description` front-matter field (see `archetypes/default.md`) as the one-line summary instead of writing new prose — the summary should always match what's actually published.
6. If no bucket has any items, skip the write entirely and tell the user there's nothing to log — do not append an empty entry.
7. Cap the entry at ~20 lines, then prepend it to `CHANGELOG.md` (newest entry first, right after the file's title), ending the entry with `<!-- site-updates:through <HEAD sha> -->` so the next run knows where to resume.
8. Also print the new entry in the reply so the user sees it without opening the file.

## Inputs

- `CHANGELOG.md` at the repo root, for the last `site-updates:through` marker.
- `git log --oneline <since>..HEAD` for the target range.
- The affected content files' front matter (`title`, `description`) for posts/projects named in the range.

## Outputs

A new section prepended to `CHANGELOG.md`, in this exact shape:

```markdown
# Site update — <date or range>

**New posts**
- [Title](/blog/slug/) — description

**New projects**
- [Title](/projects/slug/) — description

**Site improvements**
- ...

<!-- site-updates:through <HEAD sha> -->
```

Omit a bucket entirely if it has no items. ~20 lines total per entry.

## Worked example

`CHANGELOG.md` has no marker yet, so `<since>` falls back to an earlier commit. Input: `git log --oneline ef4988d..HEAD`

```text
01431a9 fixing naming on the nav
cab43b6 Fixing some typos, redudancy (#13)
e543aaa Fix/blog UI (#11)
c550f62 ci: add stale PR notice and auto-update PR branch actions (#12)
```

Entry prepended to `CHANGELOG.md`:

```markdown
# Site update — July 2026

**Site improvements**
- Cleaned up navigation labels for clarity.
- Fixed blog page layout issues affecting readability.

<!-- site-updates:through 01431a9 -->
```

Note: the `ci:` commit and the typo-only fix are omitted — neither is reader-visible, and there are no `content:` commits in this range, so **New posts** and **New projects** are left out entirely.
