---
name: publish-digest
description: >-
  Build digest packages from completed research and route them through
  human-approved publishing to the wiki, blog, or notification channels via
  research-apps. Use when summarizing a period of research or sharing results.
---

# Publish digest

## Building a digest

1. Collect what changed since the last digest: `research/log.md` entries, tasks marked `done` in `tasks/queue/`, and their `outputs`.
2. Copy `templates/digest/` to `research/digests/<period>/` (e.g. `2026-w29/`).
3. Summarize per topic: what was learned, what changed since last period, open questions. Link every claim to the finding package it came from; preserve researcher disagreements explicitly.
4. Update `research/digests/index.md` and `research/log.md`.
5. Run `pnpm okf:check`; optionally `pnpm convert research/digests/<period>` for PDF/HTML.

## Sharing (always human-gated)

Sharing outside this environment requires an approved `share-results` task — no exceptions. Once approved, distribute via the `research-apps` monorepo:

```bash
# Wiki serves the bundle directly once the repo is pulled — no push step
research-wiki --bundle . --port 8080

# Notify a Discord channel about the digest (dry-run first)
research-notify digest --bundle . --period 2026-w29 --dry-run
research-notify digest --bundle . --period 2026-w29 --webhook $DISCORD_WEBHOOK_URL

# Pending-approval reminders for humans
research-notify approvals --bundle .
```

Blog generation and email newsletters are stubs in `research-apps` (`packages/blog`, notify email provider) — record the intended distribution in the digest frontmatter even when the channel is not yet built.

## Record keeping

After sharing, append to the digest's `## Distribution` section: channel, timestamp, approving human (from the resolved approval file).
