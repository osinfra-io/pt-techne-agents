# Techne Agents

[![Copilot Agent](https://img.shields.io/badge/Copilot%20Agent-Enabled-6E40C9?style=for-the-badge&logo=githubcopilot&logoColor=white)](https://github.com/osinfra-io/pt-techne-agents/tree/main/.github/agents)
[![Promptfoo](https://img.shields.io/github/actions/workflow/status/osinfra-io/pt-techne-agents/promptfoo.yml?style=for-the-badge&logo=github&label=Promptfoo)](https://github.com/osinfra-io/pt-techne-agents/actions/workflows/promptfoo.yml)

## 📄 Repository Description

This repository is the catalog of GitHub Copilot agents for the osinfra-io platform. Each agent in `.github/agents/` is a self-serve interface to a platform capability — describe what you need, the agent handles the platform internals and opens a pull request with every change.

## Agents

| Agent | Description |
|---|---|
| [techne-nomos.agent.md](.github/agents/techne-nomos.agent.md) | The self-serve interface to the osinfra.io platform — onboard teams, manage members and repositories, request infrastructure, and configure platform resources |

## Install as a plugin

The Nomos agent and its `pt-techne-mcp-server` tools are packaged as the `techne-onboarding` GitHub Copilot CLI plugin ([`plugin.json`](plugin.json) + [`.mcp.json`](.mcp.json)). Install it from the osinfra-io marketplace:

```bash
copilot plugin marketplace add osinfra-io/pt-ai-plugins
copilot plugin install techne-onboarding@osinfra-io
```

Installing wires up the agent and the MCP server together in one step, replacing the manual MCP registration. Set `NOMOS_GITHUB_TOKEN` in your environment for the GitHub-backed tools — see [pt-techne-mcp-server](https://github.com/osinfra-io/pt-techne-mcp-server#configuration) for the required token scopes.

This plugin is indexed by the [`pt-ai-plugins`](https://github.com/osinfra-io/pt-ai-plugins) marketplace, which references this repository directly — the agent stays canonical here so its [Promptfoo evaluations](.github/workflows/promptfoo.yml) keep testing the real file.
