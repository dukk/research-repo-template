---
name: okf-author
description: >-
  Create or update OKF v0.1 document packages in research/ with correct
  frontmatter, convert.yaml, indexes, cross-links, and log entries. Use when
  committing findings, experiments, digests, or fixing OKF structure.
---

# OKF author

## When to use

- New concept package under `research/`
- Updating frontmatter, body structure, convert config, or cross-links
- Refreshing `research/index.md` or `research/log.md`

## Rules

1. Every concept is a directory with `convert.yaml` plus one or more Markdown sources (`document.md` and/or grouped files).
2. Concept Markdown (not `index.md` / `log.md`) must have YAML frontmatter with non-empty `type`.
3. Recommended fields: `title`, `description`, `tags`, `timestamp` (ISO 8601). Extensions: `status`, `audience`, `resource`. Research extensions: `topic` (topic slug), `task` (task id), `effort_estimate`, `effort_actual`, `researcher`.
4. Start by copying `templates/<type>/` into `research/<category>/<slug>/`.
5. Use kebab-case package directory names; concept ID is the path under `research/` to the package.
6. Prefer links like `[Title](/category/slug/document.md)` from the bundle root; link topics as `[Title](/../topics/<slug>/topic.md)`.
7. Configure `convert.yaml` `documents[]` when multiple sources should combine into one export.
8. Update category + root `index.md`; add a newest-first note in `research/log.md` for meaningful changes.
9. Run `pnpm okf:check` before finishing.

## Type vocabulary

`Topic`, `Finding`, `Experiment`, `SourceReview`, `Digest`, `Reference`.

## Do not

- Put research concepts outside `research/` (topics belong in `topics/`)
- Use `index.md` or `log.md` as concept package names
- Invent facts that conflict with existing concepts — surface conflicts instead
