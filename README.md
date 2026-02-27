# Kirha Skill for Claude Code

A Claude Code skill that searches real-time data across multiple verticals using the [Kirha](https://kirha.com) platform.

## What It Does

The `/kirha` skill lets you query live data directly from Claude Code. When invoked, the agent:

1. Fetches available verticals from the [Kirha discovery service](https://discovery.kirha.com)
2. Selects the best vertical for your query
3. Calls the Kirha Search API with a refined query
4. Presents structured, sourced results

## Prerequisites

1. **Kirha API Key** — Sign up at [app.kirha.com](https://app.kirha.com) and generate an API key
2. **Set the environment variable:**
   ```bash
   export KIRHA_API_KEY="your-api-key"
   ```

## Installation

### Using the Skills CLI

```bash
npx skills add kirha/kirha-skill
```

### Manual — Personal (all projects)

```bash
git clone https://github.com/kirha/kirha-skill.git ~/.claude/skills/kirha-skill
```

### Manual — Project-level

```bash
git clone https://github.com/kirha/kirha-skill.git .claude/skills/kirha-skill
```

## Usage

```
/kirha What is the current price of Bitcoin?
/kirha Latest clinical trials for CRISPR gene therapy
/kirha Tesla SEC filings and latest news
/kirha Check if IP 203.0.113.42 has abuse reports
```

## Available Verticals

Verticals and providers are dynamic. Browse the full list at [discovery.kirha.com](https://discovery.kirha.com).

## How It Works

The skill uses two Kirha services:

- **Discovery** ([discovery.kirha.com](https://discovery.kirha.com)) — Fetched at runtime to get current verticals and provider capabilities
- **Search API** (`api.kirha.com`) — Called with your API key to execute searches

The agent autonomously picks the right vertical based on your query. For multi-domain queries, it makes sequential searches and combines results.

## License

MIT
