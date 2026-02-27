# Kirha Skill Workflow Examples

Concrete examples showing the full `/kirha-search` workflow from query to response.

---

## Example 1: Crypto Query

**User input:** `/kirha-search bitcoin price`

### Step 1 — Discover Verticals
Fetch `https://discovery.kirha.com/verticals/list.mdx` and `https://discovery.kirha.com/providers/list.mdx` → receives all verticals and providers.

### Step 2 — Select Vertical
"Bitcoin price" is a blockchain/token query → match it against the verticals list to find the one focused on crypto/blockchain data.

### Step 3 — Call Search API
```bash
curl -s -X POST "https://api.kirha.com/chat/v1/search" \
  -H "Authorization: Bearer $KIRHA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "What is the current Bitcoin (BTC) price in USD?",
    "vertical_id": "crypto",
  }'
```

Note: The raw query "bitcoin price" was refined to "What is the current Bitcoin (BTC) price in USD?" for better results.

### Step 4 — Present Results
```
Bitcoin is currently trading at $104,250 USD.

| Metric         | Value          |
|----------------|----------------|
| Price (USD)    | $104,250.00    |
| 24h Change     | +2.3%          |
| 24h Volume     | $38.2B         |
| Market Cap     | $2.04T         |

Data sourced via Coingecko. As of 2025-02-18 14:30 UTC.

**Follow-up suggestions:**
- "Bitcoin price chart over the last 30 days"
- "Top DeFi protocols by TVL on Bitcoin"
```

---

## Example 2: Medical Query

**User input:** `/kirha-search GLP-1 clinical trials`

### Step 1 — Discover Verticals
Fetch verticals and providers lists → identify which vertical handles biomedical/clinical data.

### Step 2 — Select Vertical
"GLP-1 clinical trials" is a biomedical/clinical query → match it to the vertical focused on medical research and clinical trial data.

### Step 3 — Call Search API
```bash
curl -s -X POST "https://api.kirha.com/chat/v1/search" \
  -H "Authorization: Bearer $KIRHA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "Active and recruiting clinical trials for GLP-1 receptor agonists",
    "vertical_id": "medical",
  }'
```

### Step 4 — Present Results
```
There are several active clinical trials investigating GLP-1 receptor agonists across obesity, diabetes, and cardiovascular applications.

**Key Trials:**
- **NCT05123456** — Phase 3 trial of semaglutide for NASH (Non-Alcoholic Steatohepatitis). Recruiting. Sponsor: Novo Nordisk. Estimated completion: Dec 2026.
- **NCT05234567** — Phase 2 trial comparing tirzepatide vs semaglutide for weight management. Active. Sponsor: Eli Lilly. 1,200 participants.
- **NCT05345678** — Phase 3 trial of orforglipron (oral GLP-1) for Type 2 diabetes. Recruiting. Estimated completion: Mar 2027.

Data sourced from ClinicalTrials.gov via Kirha.

**Follow-up suggestions:**
- "GLP-1 adverse events reported to FDA"
- "Recent PubMed papers on semaglutide cardiovascular outcomes"
```

---

## Example 3: Multi-Vertical Query

**User input:** `/kirha-search Tesla stock and latest news`

This query spans two verticals: **company** (for stock data) and **news** (for latest articles).

### Step 1 — Discover Verticals
Fetch verticals and providers lists → identify verticals for financial/corporate data and for current events/news.

### Step 2 — Select Verticals
This is a multi-vertical query. Two sequential searches needed:
1. The vertical focused on company/financial data — for Tesla stock price and financials
2. The vertical focused on news/current events — for latest Tesla articles

### Step 3a — First Search (Company)
```bash
curl -s -X POST "https://api.kirha.com/chat/v1/search" \
  -H "Authorization: Bearer $KIRHA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "Tesla (TSLA) current stock price and recent financial performance",
    "vertical_id": "company",
  }'
```

### Step 3b — Second Search (News)
```bash
curl -s -X POST "https://api.kirha.com/chat/v1/search" \
  -H "Authorization: Bearer $KIRHA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "Latest Tesla news and developments this week",
    "vertical_id": "news",
  }'
```

### Step 4 — Present Combined Results
```
## Tesla Stock

TSLA is currently trading at $352.40, up 1.8% today.

| Metric         | Value          |
|----------------|----------------|
| Price           | $352.40       |
| Day Change      | +1.8%         |
| 52-Week High    | $488.50       |
| Market Cap      | $1.13T        |

## Latest Tesla News

- **Tesla announces new Megapack factory in Shanghai** — Reuters, Feb 17. Tesla confirmed plans for a dedicated energy storage manufacturing facility.
- **TSLA Q4 earnings beat estimates** — Bloomberg, Feb 15. Revenue came in at $27.1B vs $26.3B expected.
- **Elon Musk teases robotaxi launch timeline** — The Verge, Feb 14. Updated guidance suggests mid-2026 for commercial deployment.

**Follow-up suggestions:**
- "Tesla SEC filings from the last quarter"
- "Tesla prediction market odds for robotaxi launch"
```

---

## Example 4: Ambiguous Query

**User input:** `/kirha-search weather risks for Mediterranean shipping`

### Step 1 — Discover Verticals
Fetch verticals and providers lists → multiple candidates could match: verticals covering weather/risk, news, or company data.

### Step 2 — Disambiguate
"Weather risks" + "shipping" is about operational risk assessment, not reading news or looking up a company. Check the verticals list for one focused on weather, transportation, and risk analysis.

If unsure, fetch `https://discovery.kirha.com/verticals/{slug}.mdx` for each candidate to compare their providers and confirm which one has weather and risk assessment capabilities.

Select the vertical whose providers best handle weather-based risk analysis for transportation.

### Step 3 — Call Search API
```bash
curl -s -X POST "https://api.kirha.com/chat/v1/search" \
  -H "Authorization: Bearer $KIRHA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "Current weather risks and storm warnings affecting Mediterranean Sea shipping routes",
    "vertical_id": "insurance",
  }'
```

### Step 4 — Present Results
```
## Mediterranean Shipping Weather Risk Assessment

Current conditions show moderate risk for Mediterranean shipping routes, with a developing low-pressure system near the Balearic Islands.

**Active Warnings:**
- Storm warning for the western Mediterranean (Balearic Sea) — winds 45-60 km/h, wave height 3-4m. Valid through Feb 19.
- Heavy rainfall alert for the Ligurian coast — 80-120mm expected over 24h.
- No active warnings for the eastern Mediterranean (Aegean, Levantine Sea).

**Risk Summary:**
- **Western Med routes (Barcelona-Marseille-Genoa):** Elevated risk. Delays likely Feb 18-19.
- **Central Med routes (Sicily-Malta-Tunisia):** Low risk. Normal operations.
- **Eastern Med routes (Piraeus-Istanbul-Alexandria):** Low risk. Calm seas expected.

Data sourced via Open Weather and Winston risk analysis.

**Follow-up suggestions:**
- "Flight status for cargo flights to Barcelona today"
- "Historical weather disruption patterns for Mediterranean shipping in February"
```
