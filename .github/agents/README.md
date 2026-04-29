# Agents

## Prerequisites

The agents in this directory use the [GitHub MCP server](https://github.com/github/github-mcp-server) for all file and pull request operations. Configure it with a **fine-grained Personal Access Token** scoped to the `osinfra-io` organization with the following permissions:

| Permission | Access |
|---|---|
| Contents | Read and write |
| Issues | Read and write |
| Pull requests | Read and write |
| Workflows | Read and write |

Fine-grained PATs must be created at [github.com/settings/personal-access-tokens/new](https://github.com/settings/personal-access-tokens/new). When creating the token, set the resource owner to the **`osinfra-io` organization** (not individual repositories) so the token can operate across all repos the agent needs to reach.

## nomos.agent.md

The self-serve interface to the osinfra.io platform — describe what your team needs and Nomos handles the platform internals, opening a pull request with every change.

**Supported operations:**

- Onboard a new team (GCP folder hierarchy, Identity groups, GitHub teams, Datadog team)
- Add or remove members (GitHub teams, Datadog team, GCP Identity groups)
- Add or remove GitHub repositories
- Add or remove GitHub deployment environments
- Enable or disable feature flags (`enable_workflows`, `enable_opentofu_state_management`, `enable_datadog_webhook`, `enable_datadog_secrets`, `enable_google_wif_service_account`)
- Add or remove GCP projects
- Add GKE cluster locations
- Open a GitHub issue on `pt-logos`
