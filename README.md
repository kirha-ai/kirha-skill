<p align="center">
  <img src="assets/banner.png" alt="KIRHA Skill" />
</p>

<p align="center">
  <a href="https://kirha.com"><b>🦋 KIRHA</b></a> &bull;
  <a href="https://docs.kirha.com"><b>📚 Documentation</b></a> &bull;
  <a href="https://app.kirha.com/auth/register"><b>🔑 Get an API key</b></a>
</p>

---

# KIRHA Skill
 
An [Agent Skill](https://agentskills.io) that gives your agent real-time data access through the [KIRHA](https://kirha.com) CLI.
One auth. The largest network of [S-tier data providers](https://app.kirha.com/providers). The right context for every query.

- **Open planner**: an [open source model](https://huggingface.co/kirha) routes every query.
- **Multi-source**: one prompt can pull context from several providers at once.
- **Real-time**: we never sync provider databases. KIRHA is just a data router.
- **Auditable**: every API call is logged in your [Log panel](https://app.kirha.com/logs).

## What It Does

The `/kirha` skill lets your agent query KIRHA, a dynamic catalog of authoritative data providers, directly from the command line. When invoked, the agent:

1. Refines the user query and calls `kirha search`, letting KIRHA pick the providers
2. Parses the structured JSON response and synthesizes the answer
3. If the results are thin, runs `kirha discovery` to find the right vertical and searches again with `--focus`

KIRHA's coverage grows continuously, so the skill is built to be domain-agnostic. It discovers what KIRHA can answer at runtime rather than listing fixed topics. Use it whenever you care about accuracy, freshness, or knowing where an answer came from.

## Prerequisites

First, install the KIRHA CLI:

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
npx skills add kirha-ai/kirha-skill
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
/kirha <your question>
```

The skill may also trigger on its own when the agent decides an authoritative source is needed, but auto-triggering is not guaranteed for every query. If you specifically want KIRHA, name it. You never have to specify a vertical.

## How It Works

The skill drives the [KIRHA CLI](https://github.com/kirha-ai/kirha-cli) end-to-end:

- **`kirha search`** runs the search across every vertical with the `fast` planning runtime by default
- **`kirha discovery`** fetches the live catalogue of verticals and providers when a search needs a `--focus`
- **`kirha plan`** previews credit cost before running expensive queries

The full workflow, including discovery rules, query refinement, the retry-with-focus loop, and error handling, lives in [`skills/kirha/SKILL.md`](skills/kirha/SKILL.md).

## License

MIT
