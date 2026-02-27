# Kirha Verticals Reference

Verticals and providers change over time. Always fetch the latest data from the discovery service rather than relying on hardcoded lists.

## Discovery Endpoints

- **Verticals list:** `https://discovery.kirha.com/verticals/list.mdx` — all verticals with slugs, descriptions, and example prompts
- **Providers list:** `https://discovery.kirha.com/providers/list.mdx` — all providers and their capabilities per vertical
- **Vertical detail:** `https://discovery.kirha.com/verticals/{slug}.mdx` — deep dive into a specific vertical's providers and use cases

## Disambiguation Strategy

When a query could match multiple verticals:

1. **Check the query's intent** — is the user looking for raw data, news, research, or risk assessment?
2. **Cross-reference providers** — use the providers list to see which vertical has the data sources that best serve the query
3. **Fetch vertical detail pages** — compare `https://discovery.kirha.com/verticals/{slug}.mdx` for the top candidates
4. **Default to the most specific vertical** — prefer the vertical whose providers directly serve the data type over a general one

**Common disambiguation patterns:**

| Query Intent | How to Decide |
|---|---|
| Price/financial data for a public company | Look for verticals with stock market or SEC-related providers |
| Price/data for a crypto token | Look for verticals with blockchain or DeFi providers |
| Academic/clinical research | Look for verticals with PubMed, ClinicalTrials, or similar providers |
| Security scanning or threat intel | Look for verticals with IP scanning or vulnerability providers |
| Current events or sentiment | Look for verticals with news, social media, or prediction market providers |
| Risk assessment or weather | Look for verticals with weather, transportation, or insurance providers |
| Ad campaigns or marketing intel | Look for verticals with advertising or keyword research providers |

**Multi-vertical queries:** When a query spans two domains (e.g., "Tesla stock and latest news"), plan sequential searches — one per relevant vertical — and combine the results.
