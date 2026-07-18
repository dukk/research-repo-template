# CLAUDE.md

**First: read [AGENTS.md](AGENTS.md)** — it is the canonical agent guide (shared with Cursor, Gemini, and external A2A agents). Everything there applies. This file adds only Claude Code specifics.

## Project skills and subagents

After `pnpm link-harness`, Claude paths resolve to the shared trees:

- `.claude/skills/` → `.agents/skills/`
- `.claude/agents/` → `.agents/agents/`

See the skill and subagent tables in [AGENTS.md](AGENTS.md).

## Working style

- Prefer editing `research/` concepts over inventing parallel docs outside the OKF bundle.
- When adding concepts, keep `research/index.md` and `research/log.md` in sync; keep `topics/index.md` in sync when topics change.
- Use `/okf-author`, `/research-task`, `/topic-intake`, `/publish-digest`, and `/research-audit` skills for those workflows.

## Scheduled headless runs

This repo is designed to be driven by scheduled `claude -p` invocations (see "Scheduling autonomous runs" in AGENTS.md). When invoked as a specific persona, load the matching `.claude/agents/<name>.md` and stay within its Boundaries — especially the human-approval gates for `start-experiment`, `share-results`, and `approve-topic`.
