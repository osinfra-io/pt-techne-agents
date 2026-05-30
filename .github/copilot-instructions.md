# Repository instructions for pt-techne-agents

This file applies to every change in this repo. Read it together with the
platform- and techne-team instructions, both of which are loaded by Copilot
automatically:

- `pt-ai-context/.github/instructions/platform-group.instructions.md` — platform-wide
  conventions (commits, PRs, labels, full-SHA action pins, "keep it simple").
- `techne/pt-techne-ai-context/.github/instructions/techne-team.instructions.md` —
  techne team conventions.

## What this repo is

The catalog of GitHub Copilot agents for the osinfra-io platform. Each agent in
`.github/agents/*.agent.md` is a self-serve interface to a platform capability —
the agent drives a conversation, calls platform tools, and opens pull requests on
the user's behalf.

| Path | Purpose |
|------|---------|
| `.github/agents/techne-nomos.agent.md` | The Nomos agent — onboard teams, manage members/repositories, request infrastructure, configure platform resources |
| `evals/` | [promptfoo](https://promptfoo.dev) evaluations for agent first-turn behavior |

## Agent files

- Each agent is a Markdown file with YAML frontmatter (`name`, `description`,
  `tools`). The `tools` list names every tool the agent may call.
- **The MCP tools an agent references must exist.** Any `pt-techne-mcp-server/<tool>`
  entry in the `tools` frontmatter must match a tool registered in
  `osinfra-io/pt-techne-mcp-server` (`cmd/pt-techne-mcp-server/main.go`). When a tool
  name, parameter, or return shape changes there, update the agent prompt to match.
- The agent never hand-writes HCL or `.tfvars` — the MCP server's renderers are the
  only write path. Prompts must route all `teams/*.tfvars`, docs, and `helpers.tofu`
  changes through the corresponding MCP tool.
- Keep the prompt's internal flow labels (operation numbers, group numbers) out of
  user-facing responses.

## Evals

- `evals/promptfooconfig.yaml` defines first-turn behavior tests run against the
  agent prompt. Add a `tests:` entry following the existing pattern when changing
  startup or identity-lookup behavior.
- Run locally: `promptfoo eval -c evals/promptfooconfig.yaml --no-cache` (requires
  `ANTHROPIC_API_KEY`). See `evals/README.md`.
- `.github/workflows/promptfoo.yml` runs the evals on pull requests that touch
  `.github/agents/**` or `evals/**`.

## Conventions

- GitHub Actions must use full 40-character commit SHAs with an inline version
  comment: `uses: action/name@<sha>  # vX.Y.Z`.
- `SECURITY.md` is managed by `osinfra-io/pt-logos` — do not edit it directly.
- Follow markdownlint when editing Markdown (line length and inline HTML rules are
  disabled platform-wide).
