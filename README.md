<p align="center">
  <img src="assets/banner.png" alt="Kirha CLI Skill" />
</p>

# Kirha CLI Skill

An [Agent Skill](https://agentskills.io) that gives your coding agent real-time data access through the [Kirha](https://kirha.com) CLI.

## What It Does

The `/kirha-cli` skill lets your coding agent query Kirha — a dynamic catalogue of authoritative data providers — directly from the command line. When invoked, the agent:

1. Runs `kirha discovery` to see the current catalogue of verticals and providers
2. Picks the best-matching vertical for the query dynamically (never hardcoded)
3. Refines the user query and calls `kirha search` (or `kirha task` for deep research)
4. Parses the structured JSON response and synthesizes the answer

Kirha's coverage grows continuously, so the skill is built to be domain-agnostic: it discovers what Kirha can answer at runtime rather than listing fixed topics. Use it whenever accuracy, freshness, or source-traceability matters — whether that's current data, fact-checking, documentation lookups, or anything else where an authoritative provider beats guesswork.

## Prerequisites

1. **Kirha CLI** — install with:
   ```bash
   curl -fsSL https://cli.kirha.com/install.sh | sh
   ```
   Or via npm:
   ```bash
   npm install -g @kirha/cli
   ```
2. **Kirha API key** — get one at [app.kirha.com/api-keys](https://app.kirha.com/api-keys), then either:
   ```bash
   kirha auth login --api-key <your-key>
   # or
   export KIRHA_API_KEY="your-key"
   ```

## Installation

### Using the Skills CLI

```bash
npx skills add kirha/kirha-skill
```

### Manual — Personal (all projects)

```bash
git clone https://github.com/kirha-ai/kirha-skill.git ~/.claude/skills/kirha-skill
```

### Manual — Project-level

```bash
git clone https://github.com/kirha-ai/kirha-skill.git .claude/skills/kirha-skill
```

## Usage

Invoke the skill explicitly with your question:

```
/kirha-cli <your question>
```

The skill may also trigger on its own when the agent decides an authoritative source is needed, but auto-triggering is not guaranteed for every query — if you specifically want Kirha, name it. The agent always discovers the right vertical at runtime; you never have to specify one.

## How It Works

The skill drives the [Kirha CLI](https://github.com/kirha-ai/kirha-cli) end-to-end:

- **`kirha discovery`** — fetches the live catalogue of verticals and providers so the agent always works against an up-to-date list
- **`kirha search`** — runs the search against the selected vertical with the `fast` planning runtime by default
- **`kirha task`** — deep multi-step research (takes a few minutes, costs more credits)
- **`kirha plan`** — preview credit cost before running expensive queries

The full workflow, including discovery rules, query refinement, the rediscover-and-retry loop, and error handling, lives in [`skills/kirha-cli/SKILL.md`](skills/kirha-cli/SKILL.md).

## License

MIT
