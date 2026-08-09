# mcp-server-github-actions

[![npm version](https://img.shields.io/npm/v/mcp-server-github-actions.svg)](https://www.npmjs.com/package/mcp-server-github-actions)
[![npm downloads](https://img.shields.io/npm/dm/mcp-server-github-actions.svg)](https://www.npmjs.com/package/mcp-server-github-actions)
[![CI](https://github.com/ofershap/mcp-server-github-actions/actions/workflows/ci.yml/badge.svg)](https://github.com/ofershap/mcp-server-github-actions/actions/workflows/ci.yml)
[![TypeScript](https://img.shields.io/badge/TypeScript-strict-blue.svg)](https://www.typescriptlang.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Agent Plugins](https://img.shields.io/badge/Agent_Plugins-1.0.0-0ea5e9.svg)](https://agent-plugins.org)

Manage GitHub Actions workflows from your AI assistant. List runs, read logs, re-run failed jobs, cancel builds, and trigger deployments without leaving your editor.

```bash
npx mcp-server-github-actions
```

> Works with Claude Desktop, Cursor, VS Code Copilot, and any MCP client. Requires a GitHub token with Actions permissions.

![MCP server for GitHub Actions workflows, CI/CD runs, and deployment logs](assets/demo.gif)

<sub>Demo built with <a href="https://github.com/ofershap/remotion-readme-kit">remotion-readme-kit</a></sub>

## Why

GitHub's official MCP server covers repos, issues, and PRs, but it doesn't touch Actions. That means when your CI fails, you still have to open a browser, find the run, click through to the logs, and figure out what went wrong. This server fills that gap. You can ask your assistant "why did the last CI run fail?" or "re-run the failed jobs" and get answers right where you're working. It uses the same GitHub REST API you'd use manually, just without the context switching.

## Tools

| Tool                | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| `list_workflows`    | List all workflow files in a repository                      |
| `list_runs`         | List workflow runs (optionally filter by workflow or status) |
| `get_run`           | Get details of a specific workflow run                       |
| `get_run_logs`      | Get the logs URL for a run (zip file download)               |
| `rerun_workflow`    | Re-run an entire workflow run                                |
| `rerun_failed_jobs` | Re-run only the failed jobs from a run                       |
| `cancel_run`        | Cancel an in-progress or queued run                          |
| `list_artifacts`    | List artifacts produced by a workflow run                    |
| `trigger_workflow`  | Trigger a workflow via `workflow_dispatch`                   |

## Quick Start

### Cursor

Add to your Cursor MCP settings (e.g. `~/.cursor/mcp.json` or project-level):

```json
{
  "mcpServers": {
    "github-actions": {
      "command": "npx",
      "args": ["-y", "mcp-server-github-actions"],
      "env": {
        "GITHUB_TOKEN": "<your-token>"
      }
    }
  }
}
```

### Claude Desktop

Add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "github-actions": {
      "command": "npx",
      "args": ["-y", "mcp-server-github-actions"],
      "env": {
        "GITHUB_TOKEN": "<your-token>"
      }
    }
  }
}
```

### VS Code

Add to user settings or `.vscode/mcp.json`:

```json
{
  "mcp": {
    "servers": {
      "github-actions": {
        "command": "npx",
        "args": ["-y", "mcp-server-github-actions"],
        "env": {
          "GITHUB_TOKEN": "<your-token>"
        }
      }
    }
  }
}
```

## Auth

Create a GitHub Personal Access Token:

1. **Settings** > **Developer settings** > **Personal access tokens**
2. Choose **Fine-grained tokens** (recommended) or **Tokens (classic)**
3. Fine-grained: select your repos, then enable **Actions: Read and Write**
4. Classic: enable the `repo` scope (includes Actions)

## Agent Plugins

This repo is an [Agent Plugins](https://agent-plugins.org) 1.0.0 package: `plugin.json`, portable `mcp.json`, and `skills/` ship together with the MCP server.

For Cursor, clone the repo and copy or symlink it to `~/.cursor/plugins/local/mcp-server-github-actions`, then reload the window. Skills and MCP show up under Customize > Plugins.

Agent Plugins v1 does not ship OAuth. Set `GITHUB_TOKEN` in your MCP client config (see Quick Start). One-click Cursor/VS Code install is not offered because the token must stay in env.

## FAQ

### What is mcp-server-github-actions?

An MCP server for GitHub Actions: list runs, fetch run details, re-run failed jobs, cancel runs, list artifacts, and trigger `workflow_dispatch`.

### What token do I need?

A GitHub PAT with Actions read/write on the repos you manage. Set `GITHUB_TOKEN` in the MCP server env block.

### How is this different from the official GitHub MCP?

The official server covers repos, issues, and PRs. This one focuses on workflow runs, logs URLs, reruns, and dispatch triggers.

### Can I install it as an Agent Plugin in Cursor?

Yes, via `~/.cursor/plugins/local/mcp-server-github-actions`. You still configure `GITHUB_TOKEN` in Cursor MCP settings.

### Why is there no one-click install button?

The token cannot be embedded safely in a portable install link. Use the JSON snippet under Quick Start.

## Example Prompts

- "List the last 5 workflow runs for ofershap/mcp-server-docker"
- "Show me the workflows in the microsoft/vscode repo"
- "Get details for run 12345 in owner/repo"
- "Re-run the failed jobs for run 67890 in my-org/my-repo"
- "Cancel the currently running workflow run 11111"
- "List artifacts from the latest run in owner/repo"
- "Trigger the deploy.yml workflow on the staging branch for my-org/my-app"
- "What's the status of the most recent CI run for this project?"

## Development

```bash
npm install
npm run typecheck
npm run build
npm test
npm run lint
npm run format
```

## See also

More MCP servers and developer tools on my [portfolio](https://gitshow.dev/ofershap).

## Author

[![Made by ofershap](https://gitshow.dev/api/card/ofershap)](https://gitshow.dev/ofershap)

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://linkedin.com/in/ofershap)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=flat&logo=github&logoColor=white)](https://github.com/ofershap)

---

<sub>README built with [README Builder](https://ofershap.github.io/readme-builder/)</sub>

## License

MIT © 2026 Ofer Shapira
