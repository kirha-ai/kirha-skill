<p align="center">
  <img src="assets/banner.png" alt="Kirha CLI Skill" />
</p>

<p align="center">
  <a href="https://kirha.com"><b>🦋 Kirha</b></a> &bull;
  <a href="https://docs.kirha.com"><b>📚 Documentation</b></a> &bull;
  <a href="https://app.kirha.com/auth/register"><b>🔑 Get an API key</b></a>
</p>

---

# Kirha CLI Skill

An [Agent Skill](https://agentskills.io) that gives your agent real-time data access through the [Kirha](https://kirha.com) CLI.

## What It Does

The `/kirha-cli` skill lets your agent query Kirha, a dynamic catalogue of authoritative data providers, directly from the command line. When invoked, the agent:

1. Runs `kirha discovery` to see the current catalogue of verticals and providers
2. Picks the best-matching vertical for the query dynamically (never hardcoded)
3. Refines the user query and calls `kirha search` (or `kirha task` for deep research)
4. Parses the structured JSON response and synthesizes the answer

Kirha's coverage grows continuously, so the skill is built to be domain-agnostic. It discovers what Kirha can answer at runtime rather than listing fixed topics. Use it whenever you care about accuracy, freshness, or knowing where an answer came from.

## Prerequisites

First, install the Kirha CLI:

```bash
curl -fsSL https://cli.kirha.com/install.sh | sh
```

Or via npm:

```bash
npm install -g @kirha/cli
```

Then grab an API key at [app.kirha.com/api-keys](https://app.kirha.com/api-keys) and log in:

```bash
kirha auth login --api-key <your-key>
```

## Installation

### Using the Skills CLI

```bash
npx skills add kirha/kirha-skill
```

### Manual, personal (all projects)

```bash
git clone https://github.com/kirha-ai/kirha-skill.git ~/.claude/skills/kirha-skill
```

### Manual, project-level

```bash
git clone https://github.com/kirha-ai/kirha-skill.git .claude/skills/kirha-skill
```

## Usage

Invoke the skill explicitly with your question:

```
/kirha-cli <your question>
```

The skill may also trigger on its own when the agent decides an authoritative source is needed, but auto-triggering is not guaranteed for every query. If you specifically want Kirha, name it. The agent always discovers the right vertical at runtime, so you never have to specify one.

## How It Works

The skill drives the [Kirha CLI](https://github.com/kirha-ai/kirha-cli) end-to-end:

- **`kirha discovery`** fetches the live catalogue of verticals and providers so the agent always works against an up-to-date list
- **`kirha search`** runs the search against the selected vertical with the `fast` planning runtime by default
- **`kirha task`** does deep multi-step research (takes a few minutes, costs more credits)
- **`kirha plan`** previews credit cost before running expensive queries

The full workflow, including discovery rules, query refinement, the rediscover-and-retry loop, and error handling, lives in [`skills/kirha-cli/SKILL.md`](skills/kirha-cli/SKILL.md).

## License

MIT
