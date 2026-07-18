# Research Repo Template

> **Why this exists:** to buy time back. AI agents research very unusual or specific topics on a schedule, tailored to your own interest filters instead of other people's filters or bias — and you stay in the loop through budgets and approvals.

Template repository for **AI-assisted research**: a peer of [`doc-repo-template`](https://github.com/dukk/doc-repo-template) where autonomous agents research human-curated topics and commit findings as an **OKF v0.1 document bundle** under [`research/`](research/). Export tooling comes from [`@dukk/doc-repo-convert`](https://github.com/dukk/doc-repo-tools); supporting apps (wiki, notifications, blog, A2A gateway) live in the peer monorepo [`research-apps`](https://github.com/dukk/research-apps).

License: [Apache-2.0](LICENSE).

## How it works

```
topics/  ──human approves──▶  tasks/  ──planning poker──▶  budget check
   ▲                                                            │
   │                                    auto-approve ◀──────────┤────▶ approvals/pending/ (human)
   │                                                            ▼
topic proposals                                        researcher agents
                                                                │
                        publicist digests  ◀──  research/ (OKF findings)
                                │
                 human-approved sharing (wiki / blog / Discord / email)
```

- **[`topics/`](topics/)** — you curate what to research: problem statement, motivating questions, explicit *Interested in / Not interested in* filters, seed references. New topics require your approval.
- **[`tasks/`](tasks/)** — the manager agent breaks topics into tasks typed after the scientific method (extract problem statements, make observations, formulate hypothesis, choose research design, ... , share results). Researchers estimate each task planning-poker style on a Fibonacci scale anchored at 13.
- **[`budget.yaml`](budget.yaml)** — per-period effort budget in the same points. Within budget and below the cap, the manager auto-approves; experiments, external sharing, new topics, and oversized tasks come to you in **[`approvals/`](approvals/)**, where you can approve, reject, or respond with adjustments.
- **[`research/`](research/)** — findings, experiments, and digests as OKF document packages, fully cited, committed by researcher agents with different models and declared stances (Claude Opus, Claude Fable, Grok, local Qwen/Kimi over A2A) to balance bias.
- **Publicist** — summarizes completed research into digests and, with your approval, publishes via `research-apps` (wiki, Discord, blog, newsletters).

## Quick start

GitHub Packages requires a token even for public packages. Create a PAT with `read:packages` (or use `gh auth token`) and:

```bash
# PowerShell
$env:NODE_AUTH_TOKEN = (gh auth token)
# bash
export NODE_AUTH_TOKEN="$(gh auth token)"

pnpm init-repo
```

This installs dependencies, links the AI harness, checks for Pandoc, rebuilds `research/log.md`, `index.md` files, and `topics/index.md`, then runs `pnpm okf:check`. Concept and topic packages are never removed.

**Pandoc** is required for document export ([pandoc.org](https://pandoc.org/installing.html)); Mermaid CLI (`mmdc`) when a package enables it.

## Customize for your research

1. Update `package.json` `name` / `description`.
2. Copy `topics/_template/` to `topics/<slug>/`; write your problem statement, questions, interest filters, and seed `references.md`. See the sample topic [`agentic-memory-systems/`](topics/agentic-memory-systems/).
3. Set your effort budget and approval thresholds in [`budget.yaml`](budget.yaml).
4. Pick your researcher lineup in [`.agents/agents/`](.agents/agents/) — swap models, edit stances, add or remove variants.
5. Run `pnpm okf:check`.

## Running the agents

Interactively, any harness (Cursor, Claude Code, Gemini CLI) picks up the personas via [AGENTS.md](AGENTS.md). On a schedule (cron / Task Scheduler):

```bash
claude -p "Act as the research-manager agent. Process tasks/, budget.yaml, and approvals/. Commit your changes."
claude -p "Act as researcher-alpha. Execute your assigned approved tasks from tasks/queue/. Commit findings."
claude -p "Act as the publicist agent. Build this period's digest and raise share-results tasks."
```

External agents (locally hosted Qwen, Kimi K3, ...) participate through the A2A gateway in [`research-apps`](https://github.com/dukk/research-apps) instead of running as subagents.

## Human in the loop

- Pending decisions land in [`approvals/pending/`](approvals/) as Markdown files; fill in the `## Decision` section (approve / reject / adjust with scope, size, or priority changes). See [`approvals/README.md`](approvals/README.md).
- Get notified via `research-notify approvals` (Discord webhook; email stub) from `research-apps`.
- Always human-gated: approving topics, starting experiments, and sharing results outside this environment.

## Templates

Starter packages in [`templates/`](templates/): `topic`, `finding`, `experiment`, `source-review`, `digest`, `reference`.

## Convert / export

```bash
pnpm convert research/digests/2026-w29
pnpm convert --format pdf research/findings/
```

Formats: `pdf`, `docx`, `html`, `pptx`. Also `pnpm deconstruct` to import papers/reports into OKF packages (originals preserved under `.original/`).

## Conformance check

```bash
pnpm okf:check
```

Validates the OKF bundle plus `topics/` structure (required sections, status enum) and `tasks/` (types, statuses, Fibonacci sizes).

## AI harness (Cursor / Claude / Gemini / A2A)

| File / path | Role |
|-------------|------|
| [`AGENTS.md`](AGENTS.md) | Canonical agent instructions |
| [`CLAUDE.md`](CLAUDE.md) | Claude Code wrapper |
| [`GEMINI.md`](GEMINI.md) | Gemini CLI wrapper |
| [`.agents/skills/`](.agents/skills/) | Shared skills |
| [`.agents/agents/`](.agents/agents/) | Shared subagent personas |
| [`.cursor/rules/`](.cursor/rules/) | Cursor-scoped rules |

After clone, run `pnpm link-harness` (also runs on `pnpm install` via `prepare`) so `.claude/` and `.gemini/` point at the shared `.agents/` trees.
