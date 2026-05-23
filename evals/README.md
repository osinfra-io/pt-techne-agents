# Agent Evals

Tests the Nomos Agent's behavior using [promptfoo](https://promptfoo.dev) — sends scenarios through the GitHub Models API and asserts the model makes the correct tool calls.

## Running Locally

```bash
brew install promptfoo

cd pt-techne-agents
ANTHROPIC_API_KEY=<your-key> promptfoo eval -c evals/promptfooconfig.yaml --no-cache
```

View results in the browser:

```bash
promptfoo view
```

## How It Works

```none
promptfooconfig.yaml
  → loads agent system prompt from .github/agents/techne-nomos.agent.md
  → defines MCP tool schemas (matching the agent's tool list)
  → sends user messages to Anthropic API (Claude Sonnet)
  → asserts on tool calls returned by the model
```

Each test scenario verifies the agent's **first-turn behavior** given a user message:

- Which tools it calls (and doesn't call)
- Whether it respects safety constraints (no PR without confirmation)
- Whether it avoids fabricating data

## Adding Scenarios

Add a new `tests:` entry in `evals/promptfooconfig.yaml`:

```yaml
- description: "Descriptive name for what you're testing"
  vars:
    message: "The user's request"
  assert:
    - type: is-valid-openai-tools-call
    - type: javascript
      value: |
        const calls = Array.isArray(output) ? output : (output.tool_calls || []);
        return calls.some(c => (c.function?.name || c.name) === 'expected_tool');
```

## Feedback Loop

When evals fail in CI:

1. The promptfoo action posts a comment on the PR with pass/fail results
2. Failures indicate the agent prompt or tool descriptions need improvement
3. Common fixes:
   - **Wrong tool called** → improve tool descriptions
   - **Wrong order** → add sequencing guidance to agent prompt
   - **Missing tool call** → agent prompt doesn't mention the step clearly enough
4. Fix → re-run evals → confirm pass

## Rate Limits

Anthropic's API has generous rate limits compared to GitHub Models. No `--delay` flag is needed for typical usage.
