# Agent Evals

Tests the Nomos Agent's behavior using [promptfoo](https://promptfoo.dev) with Claude Sonnet 4.6.
Two suites are provided: **first-turn** (single message → assertion) and **multi-turn**
(full simulated conversation with tool call/result sequences → assertion).

## Running Locally

```bash
brew install promptfoo
export ANTHROPIC_API_KEY=your-key-here

cd pt-techne-agents

# First-turn behavioral tests (startup, guardrails, all operations)
promptfoo eval -c evals/promptfooconfig.yaml --no-cache

# Multi-turn sequential workflow tests (onboard, add member, add repo, safety)
promptfoo eval -c evals/promptfooconfig-multiturn.yaml --no-cache

promptfoo view
```

## Suites

### `promptfooconfig.yaml` — First-turn tests

Tests the agent's response to a single user message. Covers startup flow, all operations
(1–12), safety guardrails, and edge cases. Use these to catch regressions in first-turn
routing and identity lookup behavior.

### `promptfooconfig-multiturn.yaml` — Multi-turn tests

Tests the agent's behavior across a full simulated conversation, including tool call
sequencing, confirmation gates, and question-bundling regressions. Each test provides a
pre-built conversation history (with simulated `tool_use` and `tool_result` blocks) and
asserts on the agent's response to the final user turn. No real MCP server is required —
tool responses are simulated inline.

| Test | What it validates |
|------|------------------|
| Onboard — identity lookup | After lookup, agent asks for team key; no question bundling |
| Onboard — required fields done | Optional menu/summary shown; no PR before confirmation |
| Onboard — explicit yes | `open_team_pr` and `open_team_docs_pr` are called |
| Add member — explicit confirmation | `open_team_pr` is called with the updated spec |
| Add repo — info collection | Agent asks for description/topics; no PR yet |
| Safety — yes to sub-question | "Yes" to OTF-state question does not trigger premature PR |

## Adding Scenarios

- **First-turn test:** add a `tests:` entry in `evals/promptfooconfig.yaml`.
- **Multi-turn test:** add a `tests:` entry in `evals/promptfooconfig-multiturn.yaml`.
  Provide a `conversation:` array of Anthropic message objects (role + content) including
  any simulated `tool_use` / `tool_result` blocks, then write assertions against the
  agent's response to the final user turn.
