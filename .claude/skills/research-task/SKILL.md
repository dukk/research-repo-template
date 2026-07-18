---
name: research-task
description: >-
  Pick up, estimate, execute, and close research tasks from tasks/queue/:
  planning poker on the Fibonacci scale (anchor 13), per-task-type playbooks
  for the scientific method pipeline, and effort reporting. Use whenever
  working a task as a researcher or coordinating one as the manager.
---

# Research task

## Estimating (planning poker)

- Scale: 1, 2, 3, 5, 8, 13, 21, 34, 55. **Anchor: 13** = a typical single-source research pass (`make-observations` on one seed reference).
- Estimate independently — do not read other agents' estimates first. Adjust up or down from the anchor in Fibonacci steps; unknown unknowns push you **up** a step, familiar ground pulls you down.
- Record under `estimates:` keyed by your agent name. `tasks/task-types.yaml` `reference_points` gives per-type calibration.
- The manager records consensus as `size:` and re-polls (with reasoning shared) when the spread exceeds two Fibonacci steps.

## Executing

Preconditions: task `status: approved`, assigned to you. Set `status: in-progress` while working. Always read the topic's `topic.md` filters and `references.md` first.

Per-type playbook:

| Type | Do | Output package |
|------|----|----------------|
| `extract-problem-statements` | Read the source; list the problems it claims exist, verbatim quotes + paraphrase | `templates/source-review/` |
| `extract-questions` | List open/unanswered questions the source raises or implies | `templates/source-review/` |
| `make-observations` | Record what the source shows (data, claims, evidence quality), not what you conclude | `templates/finding/` |
| `formulate-hypothesis` | State a falsifiable hypothesis; identify independent, dependent, and controlled variables | `templates/experiment/` (design sections only) |
| `choose-research-design` | Pick controlled / comparative / factorial; justify against the hypothesis and variables | update the experiment package |
| `select-sample-population` | Define population, sampling method, sample size, exclusions | update the experiment package |
| `create-tools-procedures` | Write the procedure, instruments, and measurement plan | update the experiment package |
| `start-experiment` | Execute the designed procedure (human-approved only) | experiment package `Results` |
| `analyze-data` | Analyze collected data; show the work, not just conclusions | experiment/finding package |
| `interpret-results` | Compare results to hypothesis; state confidence and alternative explanations | experiment package |
| `draw-conclusions` | Conclusions or recommendations, scoped to the evidence | `templates/finding/` |
| `share-results` | Hand off to the publicist / `research-apps` (human-approved only) | digest reference |

## Closing

1. Commit outputs to `research/` per the `okf-author` skill; frontmatter must carry `topic`, `task`, `researcher`, `effort_estimate`, `effort_actual`.
2. Update indexes and `research/log.md` (newest first).
3. In the task file: `status: done`, `effort_actual: <fibonacci>`, `outputs: [paths]`. Report honestly — the manager calibrates on your drift.
4. Run `pnpm okf:check`.
