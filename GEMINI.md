# GEMINI.md

**First: read [AGENTS.md](AGENTS.md)** — it is the canonical agent guide (shared with Cursor, Claude, and external A2A agents). Everything there applies. This file adds only Gemini CLI specifics.

## Skills and subagents

- Skills: Gemini reads [`.agents/skills/`](.agents/skills/) natively.
- Subagents: after `pnpm link-harness`, `.gemini/agents/` → `.agents/agents/`.

See the skill and subagent tables in [AGENTS.md](AGENTS.md).

## Working style

- Treat `research/` as the OKF bundle root for progressive disclosure (`index.md` first); check `topics/index.md` before starting research work.
- Run `pnpm okf:check` after structural edits — it also validates `topics/` and `tasks/`.
- Prefer activating `okf-author`, `research-task`, `topic-intake`, `publish-digest`, or `research-audit` for those tasks.
- Respect the human-approval gates: never execute `start-experiment`, `share-results`, or `approve-topic` without a resolved approval.
