# Techne Agents

[![Copilot Agent](https://img.shields.io/badge/Copilot%20Agent-Enabled-6E40C9?style=for-the-badge&logo=githubcopilot&logoColor=white)](https://github.com/osinfra-io/pt-techne-agents/tree/main/.github/agents)
[![Promptfoo](https://img.shields.io/github/actions/workflow/status/osinfra-io/pt-techne-agents/promptfoo.yml?style=for-the-badge&logo=github&label=Promptfoo)](https://github.com/osinfra-io/pt-techne-agents/actions/workflows/promptfoo.yml)

## Purpose

This repository contains the Nomos GitHub Copilot agent, its plugin manifest, and prompt evaluations. Nomos is the self-service interface for team onboarding and platform configuration; it validates requests through `pt-techne-mcp-server` and proposes changes through pull requests.

## Agents

| Agent | Description |
|---|---|
| [nomos.agent.md](.github/agents/nomos.agent.md) | The self-serve interface to the osinfra.io platform — onboard teams, manage members and repositories, request infrastructure, and configure platform resources |

## Install as a plugin

The Nomos agent and its `pt-techne-mcp-server` tools are packaged as the `techne-agents` GitHub Copilot CLI plugin ([`plugin.json`](plugin.json) + [`.mcp.json`](.mcp.json)). Install it from the osinfra-io marketplace:

```bash
copilot plugin marketplace add osinfra-io/pt-ai-plugins
copilot plugin install techne-agents@osinfra-io
```

Installation wires up the agent and its version-pinned MCP server together. Docker must be available, and `NOMOS_GITHUB_TOKEN` must be set for GitHub-backed tools. See [pt-techne-mcp-server](https://github.com/osinfra-io/pt-techne-mcp-server#configuration) for token scopes and operational configuration.

This plugin is indexed by the [`pt-ai-plugins`](https://github.com/osinfra-io/pt-ai-plugins) marketplace, which references this repository directly — the agent stays canonical here so its [Promptfoo evaluations](.github/workflows/promptfoo.yml) keep testing the real file.
