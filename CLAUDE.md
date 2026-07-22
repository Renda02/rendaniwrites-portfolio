# CLAUDE.md

@AGENTS.md

## Claude Code specific notes

- This is a Hugo site. Run `hugo server -D` locally to preview, `hugo` to build to `public/` (gitignored).
- Before committing, check that new content matches an archetype in `archetypes/` (front matter fields: date, title, tags, description).
- Don't reorganize existing folder structure unless explicitly asked — propose the change first.
- When adding a new content section, also check whether `hugo.toml` menu needs updating and whether a matching layout exists in `layouts/`.
- Follow the commit convention in `AGENTS.md`: `feat`, `fix`, `content`, `chore`, `style`, `ci`, `refactor`, `revert`. One logical change per commit.
