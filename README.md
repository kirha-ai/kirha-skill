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
One API key reaches a growing network of [S-tier data providers](https://kirha.com/providers), more than 80 today, with web search as a fallback.

- **Multi-source**: one prompt can pull context from several providers at once.
- **Direct tool calls**: an agent that prefers its own routing can call any provider tool with exact parameters and skip the planner.
- **Real-time**: we never sync provider databases. KIRHA is just a data router.
- **Auditable**: every API call is logged in your [Log panel](https://app.kirha.com/logs).

## What it does

The skill teaches your agent two ways to get data from KIRHA and leaves the choice between them to the agent.

**Search.** KIRHA does the routing. The agent rewrites your question into a precise query and runs `kirha search`. KIRHA picks the providers, calls their tools and returns the data, with the tool and the parameters behind each result.

**Direct tool calls.** The agent does its own routing. It finds the tool with `kirha tools match`, reads its schema with `kirha tools get` and calls it with `kirha tools run`. Finding and reading tools is free, and so is every tool that serves public data. Only premium data costs credits.

When a search comes back thin, the agent checks which tools KIRHA called, looks for a better one, or searches again with `--focus` on one vertical.

The skill carries no list of data sources. The agent reads what KIRHA covers from the catalogue at [kirha.com/providers.md](https://kirha.com/providers.md) and [kirha.com/tools.md](https://kirha.com/tools.md), and picks up new providers without an update. Use the skill whenever you care about accuracy, freshness, or knowing where an answer came from.

## Prerequisites

Install the KIRHA CLI, version 0.2.1 or later:

```bash
curl -fsSL https://cli.kirha.com/install.sh | sh
```

Or via npm:

```bash
npm install -g @kirha/cli
```

If the CLI is already installed, `kirha upgrade` brings it up to date.

Then sign up at [app.kirha.com](https://app.kirha.com/auth/register) for 250 free credits, create an API key at [app.kirha.com/api-keys](https://app.kirha.com/api-keys) and log in:

```bash
kirha auth login --api-key <your-key>
```

## Installation

### Using the KIRHA CLI

```bash
kirha skills install
```

It detects the agents installed on your machine. To target one, pass its id from [skills.sh](https://skills.sh):

```bash
kirha skills install --agent claude-code --yes
```

### Using the Skills CLI

```bash
npx skills add kirha-ai/kirha-skill
```

### Manual

Clone the repository, then copy the skill folder into your agent's skills directory. For Claude Code, across all your projects:

```bash
git clone https://github.com/kirha-ai/kirha-skill.git
mkdir -p ~/.claude/skills && cp -r kirha-skill/skills/kirha ~/.claude/skills/kirha
```

To install it for one project only, copy it to `.claude/skills/kirha` inside that project.

## Usage

Invoke the skill explicitly with your question:

```
/kirha What does the boxed warning on Ozempic say?
/kirha Is express@4.18.0 affected by any known CVEs?
/kirha List the top 10 stablecoin yields on Ethereum
```

The skill may also trigger on its own when the agent decides an authoritative source is needed, but auto-triggering is not guaranteed for every query. If you specifically want KIRHA, name it. You never have to specify a vertical.

## How it works

The skill drives the [KIRHA CLI](https://github.com/kirha-ai/kirha-cli):

| Command | What the skill does with it |
| --- | --- |
| `kirha search` | Runs a plain-language search across every vertical |
| `kirha plan create`, `kirha plan exec` | Previews the credit cost of a search, then runs it |
| `kirha tools match` | Finds the tools that fit an intent, with their price per call |
| `kirha tools list` | Lists the tools of one provider, or the whole catalogue |
| `kirha tools get` | Reads one tool's input and output schema |
| `kirha tools run` | Calls one tool with exact parameters |

The full instructions, including query refinement, what to do when a search comes back thin and error handling, are in [`skills/kirha/SKILL.md`](skills/kirha/SKILL.md).

## License

MIT
