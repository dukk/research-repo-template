---
name: topic-intake
description: >-
  Propose or validate a research topic in topics/: required frontmatter and
  sections, seed references, and routing through human approval. Use when
  creating a topic, reviewing a proposed one, or promoting one to approved.
---

# Topic intake

## Creating a topic

1. Copy `topics/_template/` to `topics/<kebab-case-slug>/`.
2. Fill `topic.md` frontmatter: `type: Topic`, `title`, `description`, `tags`, `timestamp`, `status: proposed`, `priority` (`low | medium | high`), `budget_points` (Fibonacci-scale points per period this topic may consume).
3. Fill every section — a good topic has all of: **Problem statement**, **Motivating questions**, **Interested in**, **Not interested in**, **Success criteria**, **Constraints**. The interest filters are the whole point: they are how the topic owner avoids other people's filters and bias.
4. Seed `references.md` with at least a few primary sources, ongoing feeds, and (ideally) anti-references with the reason for skepticism.
5. Add the topic to `topics/index.md` with its status badge.
6. Run `pnpm okf:check` — it validates topic structure.

## Quality bar

A topic is ready for approval when a researcher could, from `topic.md` alone, decide in under a minute whether a given source is in scope. Vague topics ("keep up with AI") should be split or sharpened before routing for approval.

## Approval routing

- New topics always start `status: proposed`. Researchers must not act on proposed topics.
- The manager creates an `approve-topic` task and writes `approvals/pending/<task-id>.md` summarizing the topic, its budget ask, and overlap with existing topics.
- On human approval (possibly with adjustments — e.g. reduced `budget_points`), the manager sets `status: approved`, applies adjustments, and may begin breaking the topic into tasks.

## Lifecycle

`proposed → approved → active → paused | done`. Only humans approve; the manager may move approved topics between `active`/`paused` for budget reasons and must log why in `tasks/ledger.md`.
