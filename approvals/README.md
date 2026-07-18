# Approvals

Human-in-the-loop inbox. The research-manager agent writes one Markdown file per decision into `pending/`; you respond by editing the `## Decision` section; the manager applies the outcome and moves the file to `resolved/`.

## What lands here

- Tasks estimated above the `auto_approve.max_task_points` cap in `budget.yaml`
- Task types flagged `human_approval: always` (`start-experiment`, `share-results`, `approve-topic`)
- New topics proposed by agents (status `proposed` in `topics/`)

## How to respond

Open the file in `pending/` and fill in the `## Decision` section:

```markdown
## Decision

status: approved        # approved | rejected | adjusted
adjustments:
  size: 8               # optional: override the estimate
  scope: >-             # optional: narrow or redirect the task
    Only cover sources from the topic's seed references.
  priority: high        # optional
notes: >-
  Free-form guidance the manager must relay to the assignee.
```

- **approved** — the manager proceeds as proposed.
- **rejected** — the manager marks the task `rejected` and records the reason in the ledger.
- **adjusted** — the manager applies your adjustments to the task file first, then proceeds. Use this to lower estimates, narrow scope, or change priority without a full reject/repropose cycle.

Notifications about new pending approvals can be sent via the `research-apps` notifier (`research-notify approvals`).
