---
name: github-actions-management
description: Manage GitHub Actions workflows, runs, and CI/CD via MCP. Use when asked to check CI status, read logs, or re-run jobs.
---

# GitHub Actions Management via MCP

Use this skill when you need to check CI/CD status, read workflow logs, re-run failed jobs, or trigger deployments.

## Available Tools

| Tool | What it does |
|------|-------------|
| `list_workflows` | List all workflow files in a repository |
| `list_runs` | List workflow runs (filter by workflow or status) |
| `get_run` | Get details of a specific workflow run |
| `get_run_logs` | Get the logs URL for a run (zip download) |
| `rerun_workflow` | Re-run an entire workflow run |
| `rerun_failed_jobs` | Re-run only the failed jobs from a run |
| `cancel_run` | Cancel an in-progress or queued run |
| `list_artifacts` | List artifacts produced by a workflow run |
| `trigger_workflow` | Trigger a workflow via `workflow_dispatch` |

## Workflow

1. Use `list_runs` with `owner` and `repo` to see recent runs and their status
2. For failed runs: `get_run` for details, then decide whether to `rerun_failed_jobs` or investigate logs
3. `trigger_workflow` requires the workflow file name and a branch — the workflow must have a `workflow_dispatch` trigger

## Key Patterns

- All tools require `owner` and `repo` parameters (e.g., `owner: "ofershap"`, `repo: "my-project"`)
- `list_runs` supports `status` filter: "completed", "in_progress", "queued", "failure", "success"
- `rerun_failed_jobs` is preferred over `rerun_workflow` — it's faster and cheaper
- `trigger_workflow` needs `workflow_id` (filename like "ci.yml") and `ref` (branch name)

## Safety

- Prefer `rerun_failed_jobs` over full `rerun_workflow` to avoid unnecessary compute
- Confirm before `cancel_run` — the user may want the run to finish
- `trigger_workflow` can trigger deployments — always confirm the target branch
