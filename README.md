# Kirha Skill for Claude Code

A Claude Code skill that searches real-time data across 7 verticals using the Kirha platform.

## What It Does

The `/kirha` skill lets you query live data directly from Claude Code. When invoked, the agent:

1. Fetches available verticals from the Kirha discovery service
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

### Personal (all projects)

```bash
mkdir -p ~/.claude/skills/kirha
cp kirha-skill/SKILL.md ~/.claude/skills/kirha/
cp kirha-skill/verticals-reference.md ~/.claude/skills/kirha/
cp -r kirha-skill/examples ~/.claude/skills/kirha/
```

### Project-level

```bash
mkdir -p .claude/skills/kirha
cp kirha-skill/SKILL.md .claude/skills/kirha/
cp kirha-skill/verticals-reference.md .claude/skills/kirha/
cp -r kirha-skill/examples .claude/skills/kirha/
```

### WebFetch Permission

Add `discovery.kirha.com` to your allowed WebFetch domains in `.claude/settings.local.json`:

```json
{
  "permissions": {
    "allow": [
      "WebFetch(domain:discovery.kirha.com)"
    ]
  }
}
```

## Usage

```
/kirha What is the current price of Bitcoin?
/kirha Latest clinical trials for CRISPR gene therapy
/kirha Tesla SEC filings and latest news
/kirha Check if IP 203.0.113.42 has abuse reports
```

## Available Verticals

| Vertical | Slug | Key Providers | Use For |
|---|---|---|---|
| Crypto | `crypto` | Coingecko, DefiLlama, Dune, Zerion | Token prices, DeFi, wallets, on-chain data |
| Medical | `medical` | PubMed, ClinicalTrials, OpenFDA, Arxiv | Research papers, trials, drug data |
| Company | `company` | Sec, Marketstack, Apollo, Linkedin | Stock data, filings, company profiles |
| News | `news` | Polymarket, X, Web Search, GoogleScholar | Current events, sentiment, predictions |
| CyberSec | `cybersec` | Shodan, AbuseIPDB, Github | IP scans, vulnerabilities, threat intel |
| Adtech | `adtech` | Google Ads, Apollo, Firecrawl | Ad campaigns, keywords, competitor ads |
| Insurance | `insurance` | Open Weather, Aviationstack, Winston | Weather risk, flights, claims analysis |

## How It Works

The skill uses two Kirha services:

- **Discovery** (`discovery.kirha.com`) — Fetched via WebFetch to get current verticals and provider info
- **Search API** (`api.kirha.com`) — Called via curl with your API key to execute searches

The agent autonomously picks the right vertical based on your query. For multi-domain queries, it makes sequential searches and combines results.
