# Agent Evals

Tests the Nomos Agent's first-turn behavior using [promptfoo](https://promptfoo.dev) with Claude Sonnet 4.6.

## Running Locally

```bash
brew install promptfoo
export ANTHROPIC_API_KEY=your-key-here

cd pt-techne-agents
promptfoo eval -c evals/promptfooconfig.yaml --no-cache
promptfoo view
```

## Adding Scenarios

Add a new `tests:` entry in `evals/promptfooconfig.yaml` following the existing pattern.
