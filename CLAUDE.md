# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
pnpm run dev      # Start dev server at http://localhost:3030
pnpm run build    # Build static SPA
pnpm run export   # Export to PDF/PPTX/PNG (requires playwright-chromium)
```

For PDF/PPTX/PNG export, install the browser dependency first:
```bash
pnpm add -D playwright-chromium
```

## Architecture

This is a [Slidev](https://sli.dev) presentation project — Markdown-driven slides with Vue components, built on Vite.

**Entry point:** `slides.md` — the main slide deck. Slides are separated by `---`. The first frontmatter block is the headmatter (deck-wide config including theme, title, transitions, and Comark syntax).

**Key directories:**
- `components/` — Custom Vue components usable directly in slides (e.g. `<Counter :count="10" />`)
- `snippets/` — TypeScript/JS files for `<<< @/snippets/file.ts` code imports and Monaco editor
- `pages/` — Additional markdown files imported via `src: ./pages/file.md` in slide frontmatter

**Slide features in use:**
- Theme: `seriph` (swap to `default` in headmatter to change)
- `comark: true` — enables Comark markdown extensions (code groups, attribute syntax)
- `v-click` / `v-after` — click-step animations
- `v-mark` — inline highlight markers (underline, circle, etc.) via Rough Notation
- `v-motion` — motion animations via `@vueuse/motion`
- `v-drag` — draggable elements, positions stored in slide frontmatter as `dragPos:`
- `{monaco}` / `{monaco-run}` — turn code blocks into live Monaco editors
- ` ```ts twoslash ` — TypeScript hover info in code blocks
- ` ````md magic-move ` — animated transitions between code blocks
- `$$...$$` — LaTeX math (KaTeX)
- ` ```mermaid ` / ` ```plantuml ` — diagram rendering

**Slide splitting:** Import external slide files with `src: ./pages/file.md` as a slide frontmatter value. The importing slide's own content is ignored — only the `src` file is rendered.

**Code snippet imports:** Use `<<< @/snippets/file.ts` to embed file content. Named regions (`#region snippet` / `#endregion snippet`) let you import just a portion.

**Deployment:** Configured for both Netlify (`netlify.toml`) and Vercel (`vercel.json`).

## Slidev Skill

A detailed skill reference is available at `.agents/skills/slidev/SKILL.md` with per-feature references in `.agents/skills/slidev/references/`. Consult these when working with specific Slidev features.
