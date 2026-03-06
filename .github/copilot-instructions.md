# Copilot Instructions For This Repository

## Project Context

- This repository is a Hugo static site.
- Main language is French (`languageCode = "fr"`).
- Theme is Congo (`github.com/jpanther/congo/v2`).
- Content focus: cloud, DevOps, projects, CV.

## Source Of Truth

- Edit source files only.
- Do not manually edit generated output in `public/`.
- Do not manually edit generated assets in `resources/_gen/` unless explicitly requested.
- Prefer updating files under `content/`, `config/`, `layouts/`, `assets/`, and `static/`.

## Content Conventions

- Keep editorial text in French by default.
- Use clear, technical writing style (cloud, infra, DevOps topics).
- Keep existing front matter style in touched files.
- For new content pages, prefer YAML front matter (`---`) to align with current section pages.
- Use realistic publication dates in `YYYY-MM-DD`.
- Keep `draft: true` for work-in-progress pages unless asked to publish.
- Reuse existing shortcodes and structure patterns (for example `{{< lead >}} ... {{< /lead >}}`).

## Site Structure

- Main sections are under `content/posts/`, `content/projets/`, and `content/cv/`.
- Section landing pages usually use `_index.md`.
- Project pages are typically organized as `content/projets/<project-slug>/_index.md` with optional `assets/` folder.
- Menu configuration is in `config/_default/menus.toml`.

## Configuration Conventions

- Base config is split across `config/_default/*.toml`.
- Keep existing file names and paths as-is, including `config/_default/laguages.toml`.
- Preserve existing theme options unless a change is explicitly requested.

## Build And Validation

- Build command: `hugo` (run from repository root).
- CI deploy workflow: `.github/workflows/deploy.yml`.
- Deployment publishes generated content from `public/` to `gh-pages`.

## Editing Expectations

- Make minimal, targeted changes.
- Preserve existing tone and structure in modified pages.
- Do not introduce unrelated refactors.
- When changing content organization, ensure internal links and section coherence remain correct.
