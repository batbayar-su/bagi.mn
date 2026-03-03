# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A personal portfolio/resume website for Batbayar Sukhbaatar, built with **Hugo** (v0.157.0+extended) using the **Blowfish theme** (git submodule). Multilingual: English (default) and Mongolian. Hosted at https://bagi.mn/.

## Commands

```bash
# Development (Hugo server + Tailwind CSS watcher in parallel)
npm run dev

# Build production CSS only
npm run build

# Update Blowfish theme submodule
npm run update-theme

# Build the full site
hugo

# Create new content
hugo new content/posts/my-post.md
```

The dev server runs at http://localhost:1313/.

## Architecture

### Data-Driven Resume Homepage

The site is a resume/CV — not a blog. The homepage uses a custom layout (`layouts/partials/home/resume.html`) that loads structured JSON data from `data/{lang}/`:

- `bio.json` — summary statement
- `experience.json` — work history array (position, company, dates, achievements, technologies)
- `education.json` — education array (degree, institution, GPA, achievements)
- `skills.json` — categorized skills (coding, knowledge, personal)

Data is loaded per-language: `{{ $experience := index site.Data site.Language.Lang "experience" }}`. To add/edit resume content, modify the JSON files in `data/en/` and `data/mn/`.

### CSS Pipeline

Tailwind CSS is compiled from the theme's source using its CLI (not PostCSS):
- **Input**: `themes/blowfish/assets/css/main.css`
- **Output**: `assets/css/compiled/main.css`
- **Config**: `themes/blowfish/tailwind.config.js`
- The compiled CSS is checked into git. Run `npm run build` after any Tailwind class changes.

Print styles are loaded via `layouts/partials/extend-head.html` from `assets/css/print.css`.

### Theme Customization

- **Never modify** files in `themes/blowfish/` directly — it's a git submodule
- Override templates by placing files at the same path under `layouts/`
- Currently overridden: `partials/home/resume.html`, `partials/extend-head.html`
- Theme docs: https://blowfish.page/docs/

### Configuration

All Hugo config lives in `config/_default/`:
- `hugo.toml` — base URL, theme, taxonomies
- `params.toml` — Blowfish theme params (color scheme: github, dark mode default)
- `languages.en.toml` / `languages.mn.toml` — author info, social links per language
- `markup.toml` — Goldmark with HTML passthrough and math support enabled

### Multilingual

Language-specific content is organized by lang code (`en`, `mn`). Data files use `data/{lang}/`, config uses `languages.{lang}.toml`. Both languages share the same templates.
