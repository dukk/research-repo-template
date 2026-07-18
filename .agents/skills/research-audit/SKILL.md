---
name: research-audit
description: >-
  Audit the research/ OKF bundle plus topics/ and tasks/ for conformance:
  document packages, required frontmatter, topic sections, task fields,
  Fibonacci sizes, and soft-warn broken links. Use after bulk edits or
  autonomous agent runs.
---

# Research audit

## Automated check

```bash
pnpm okf:check
```

This fails (exit 1) on hard conformance errors:

- Package Markdown sources missing parseable frontmatter or empty `type`
- Invalid `documents[]` groupings / missing configured sources in `convert.yaml`
- Topics missing `topic.md`, frontmatter, `type`, or a valid `status` (`proposed | approved | active | paused | done`)
- Tasks with missing/unknown `type` (vs `tasks/task-types.yaml`), missing `topic`, or invalid `status`

It warns (non-fatal) on:

- Missing category `index.md`; Markdown outside a `convert.yaml` package
- Invalid `sources` / `assets` / `links` enum values; broken bundle-relative links
- Concepts missing recommended `title` or `description`
- Topics missing recommended sections (`Problem statement`, `Motivating questions`, `Interested in`, `Not interested in`), `priority`, or `references.md`
- Task sizes or estimates off the Fibonacci scale

## Manual review

1. Skim `research/index.md` and `topics/index.md` for progressive disclosure quality.
2. Spot-check recent findings: citations present, topic filters respected, disagreements preserved.
3. Cross-check `tasks/ledger.md` against task files: sizes, actuals, and approvals recorded.
4. If AI-generated text conflicts with an existing concept, surface it — do not silently rewrite both.

## After fixes

Re-run `pnpm okf:check` and update `research/log.md` when the audit drove structural changes.
