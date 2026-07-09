# Cursor instructions for documentation

## Project overview
This is a documentation repository. All content is written in Markdown. The goal is to maintain consistent structure, naming, and formatting across all files.

---

## File naming conventions

### Markdown files
- Always lowercase
- Words separated by hyphens
- Descriptive and concise

```
# Correct
getting-started.md
api-reference.md
release-notes.md

# Incorrect
GettingStarted.md
API_Reference.md
releaseNotes.md
```

### Image files
- Always lowercase
- Name must relate to the image content
- Add a random number suffix **only when needed to avoid a naming collision** (e.g. two images that would otherwise share the same descriptive name) — a clear, unique descriptive name on its own is fine otherwise

```
# Correct — descriptive name alone is enough
pipeline-diagram.png
release-workflow.png

# Correct — suffix used because collision would otherwise occur
pipeline-diagram-4821.png
pipeline-diagram-9034.png

# Incorrect — always avoid these regardless of suffix
image1.png
screenshot.png
diagram.png
```

---

## Content structure

### Every markdown file must have
- A single H1 title at the top
- A short description below the title
- Logical heading hierarchy (H1 → H2 → H3, never skip levels)

```markdown
# Page title

Short description of what this page covers.

## Section one

### Subsection
```

### Headings
- Use sentence case — only capitalise the first word and proper nouns
- No punctuation at the end of headings
- Keep headings short and descriptive

```markdown
# Correct
## Getting started with the platform
## API reference guide

# Incorrect
## Getting Started With The Platform
## API Reference Guide.
```

### Lists
- Use hyphens `-` for unordered lists, not `*` or `+`
- Use numbered lists only when order matters
- Keep list items parallel in structure

---

## Images

- Always use relative paths
- Include descriptive alt text
- Follow the naming convention: `content-description-XXXX.png`

```markdown
![Pipeline diagram showing GitBook to GitHub sync](../images/pipeline-diagram-4821.png)
```

---

## Code blocks

- Always specify the language
- Use fenced code blocks with triple backticks

````markdown
```bash
npm run dev
```

```yaml
name: Deploy docs
```
````

---

## When helping with this repo

1. **New files** → Always lowercase, hyphen-separated, `.md` extension
2. **New images** → Lowercase, content-related name, random number suffix
3. **Headings** → Sentence case, no end punctuation, logical hierarchy
4. **Lists** → Hyphens only, parallel structure
5. **Code** → Always fenced with language specified
6. **Alt text** → Always descriptive, never empty
7. **Links** → Use relative paths for internal docs, full URLs for external

---

## Commit conventions

Use [Conventional Commits](https://www.conventionalcommits.org/) format: `type: short description`

| Type | Use for |
|---|---|
| `feat` | New page, section, or layout feature |
| `fix` | Correcting an error — broken link, typo, wrong data, broken build |
| `content` | Adding or updating actual page content (blog posts, case studies, project pages) |
| `chore` | Maintenance that doesn't affect content or behavior — config, renames, deps |
| `style` | Formatting-only changes — CSS, markdown formatting, no content change |
| `ci` | GitHub Actions / pipeline changes (Vale, Lychee, deploy workflows) |
| `refactor` | Reorganizing without changing the output (splitting a partial, moving files) |
| `revert` | Reverting a previous commit |

Examples:
```
feat: add projects landing page
fix: correct broken link in about page
content: publish ocalization case study
chore: update hugo config menu order
style: switch heading font to sans-serif
ci: add vale and lychee link checks
```

Branch names should match the commit type: `feat/add-projects-page`, `fix/broken-nav-link`, `content/crowdin-case-study`.

---

## What to Avoid

- Avoid uppercase or camelCase file names
- Avoid skipping heading levels
- Avoid images without alt text
- Avoid code blocks without a language specifier
- Avoid generic image names like `image1.png` or `screenshot.png`
- Avoid adding a number suffix to every image out of habit — only when it's actually needed to disambiguate