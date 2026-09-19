# agents

Custom [pi](https://pi.dev) agent configurations: a devil's-advocate subagent built on the "seek contrary opinions" principle from Annie Duke's *Thinking in Bets*.

## Contents

| Path | What it is |
|------|------------|
| `agents/adversary.md` | `adversary` subagent — steelmanned devil's advocate that attacks the load-bearing assumptions of plans, claims, and decisions. Pinned to a local vLLM model with medium thinking (`vllm-ts/qwen3.8-27b:medium`); edit the `model:` frontmatter to point at your own provider/model. |
| `prompts/devils-advocate.md` | `/devils-advocate` prompt template — dispatches the adversary on a decision or plan and asks pi to weigh the resulting verdict instead of agreeing with either side. |

## What the adversary does

- Steelmans the position before attacking (straw men are forbidden)
- Verifies factual claims against the codebase (has `read`/`grep`/`find`/`ls`/`bash`)
- Works through falsification → base rates → pre-mortem → second-order effects → hidden costs → competing hypotheses
- Outputs a structured verdict: **Steelman → Verdict (with confidence) → Attack → What would change my mind → Base rates → The one question**
- No reflexive contrarianism: if the argument survives the attack, it says so

## Install (pi coding agent)

Requires the [subagent extension](https://github.com/earendil-works/pi/tree/main/packages/coding-agent/examples/extensions/subagent) (provides the `subagent` tool):

```bash
# Agents
mkdir -p ~/.pi/agent/agents
cp agents/*.md ~/.pi/agent/agents/

# Workflow prompt template (optional)
mkdir -p ~/.pi/agent/prompts
cp prompts/*.md ~/.pi/agent/prompts/
```

Then restart pi.

## Usage

- Natural language: `Use adversary to challenge my plan to <...>`
- Prompt template: `/devils-advocate <decision or plan>`
- Chains: `worker → adversary → worker` (implement → critique → revise) if you also have a worker agent

## Model config

The `model:` frontmatter accepts the pi `provider/model-id:<thinking>` shorthand:

```yaml
model: vllm-ts/qwen3.8-27b:medium   # local vLLM on an RTX 3090, medium thinking
```

Omit `model:` entirely to inherit the dispatching session's model and thinking level.
