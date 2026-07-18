# Tasks

Work queue for the research agents. One YAML file per task in `queue/`; sizes and actuals reconciled in `ledger.md`; valid types in `task-types.yaml`.

## Lifecycle

```
proposed → estimating → estimated → (pending-approval →) approved → in-progress → done
                                                       ↘ rejected
```

1. **proposed** — anyone (human or agent) drops a task file in `queue/`.
2. **estimating** — the manager polls researchers; each records an independent Fibonacci estimate under `estimates:` (anchor 13; adjust up/down in Fibonacci steps for unknown unknowns).
3. **estimated** — the manager records the consensus as `size:`. If the spread is more than two Fibonacci steps, the manager re-polls with the outliers' reasoning shared.
4. **pending-approval** — required when `size` exceeds `budget.yaml` `auto_approve.max_task_points`, or the type is listed in `human_approval_required`. The manager writes `approvals/pending/<task-id>.md` and waits.
5. **approved** — auto-approved within budget, or human-approved (possibly with adjustments the manager must apply back to the task file).
6. **in-progress** → **done** — a researcher executes the task, commits findings to `research/`, and records `effort_actual:` on the same scale.

## Task file format

See `queue/T-0001.yaml` for a worked example. Required fields: `id`, `topic`, `type`, `status`, `description`. Estimation fields: `estimates` (map of agent → points), `size`. Completion fields: `assignee`, `effort_actual`, `outputs` (paths under `research/`).

## Ledger

`ledger.md` is the manager's running reconciliation: points budgeted, spent (actuals), and estimate-vs-actual drift per researcher. Drift feeds back into prioritization next period.
