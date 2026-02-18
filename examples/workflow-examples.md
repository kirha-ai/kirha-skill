# Kirha Skill Workflow Examples

Concrete examples showing the full `/kirha` workflow from query to response.

---

## Example 1: Crypto Query

**User input:** `/kirha bitcoin price`

### Step 1 — Discover Verticals
Fetch `https://discovery.kirha.com/verticals/list.mdx` → receives all 7 verticals with descriptions.

### Step 2 — Select Vertical
"Bitcoin price" clearly maps to the **crypto** vertical (slug: `crypto`), which includes Coingecko for token prices and market data.

### Step 3 — Call Search API
```bash
curl -s -X POST "https://api.kirha.com/chat/v1/search" \
  -H "Authorization: Bearer $KIRHA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "What is the current Bitcoin (BTC) price in USD?",
    "vertical_id": "crypto",
    "summarization": { "enable": true, "model": "kirha-flash" },
    "include_raw_data": true
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

**User input:** `/kirha GLP-1 clinical trials`

### Step 1 — Discover Verticals
Fetch verticals list → identifies **medical** vertical which includes ClinicalTrials, PubMed, and OpenFDA providers.

### Step 2 — Select Vertical
"GLP-1 clinical trials" maps directly to **medical** (slug: `medical`). The ClinicalTrials provider specifically handles trial data.

### Step 3 — Call Search API
```bash
curl -s -X POST "https://api.kirha.com/chat/v1/search" \
  -H "Authorization: Bearer $KIRHA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "Active and recruiting clinical trials for GLP-1 receptor agonists",
    "vertical_id": "medical",
    "summarization": { "enable": true, "model": "kirha-flash" },
    "include_raw_data": true
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

**User input:** `/kirha Tesla stock and latest news`

This query spans two verticals: **company** (for stock data) and **news** (for latest articles).

### Step 1 — Discover Verticals
Fetch verticals list → identifies both `company` (Marketstack for stock data, Sec for filings) and `news` (Web Search, X for articles and media).

### Step 2 — Select Verticals
Two sequential searches needed:
1. `company` — for Tesla stock price and financial data
2. `news` — for latest Tesla news articles

### Step 3a — First Search (Company)
```bash
curl -s -X POST "https://api.kirha.com/chat/v1/search" \
  -H "Authorization: Bearer $KIRHA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "Tesla (TSLA) current stock price and recent financial performance",
    "vertical_id": "company",
    "summarization": { "enable": true, "model": "kirha-flash" },
    "include_raw_data": true
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
    "summarization": { "enable": true, "model": "kirha-flash" },
    "include_raw_data": true
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

**User input:** `/kirha weather risks for Mediterranean shipping`

### Step 1 — Discover Verticals
Fetch verticals list → multiple candidates:
- **insurance** — weather data, risk analysis, transportation tracking
- **news** — could have articles about shipping disruptions
- **company** — could have shipping company data

### Step 2 — Disambiguate
"Weather risks" + "shipping" strongly aligns with the **insurance** vertical, which explicitly covers "real-time transportation tracking" and "weather" with providers like Open Weather (weather data) and Winston (risk analysis). The query is about assessing operational risk, not reading news or looking up a company.

If unsure, the agent fetches `https://discovery.kirha.com/verticals/insurance.mdx` to confirm that Open Weather and Winston can handle weather risk assessment for transportation.

Selected vertical: **insurance**

### Step 3 — Call Search API
```bash
curl -s -X POST "https://api.kirha.com/chat/v1/search" \
  -H "Authorization: Bearer $KIRHA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "Current weather risks and storm warnings affecting Mediterranean Sea shipping routes",
    "vertical_id": "insurance",
    "summarization": { "enable": true, "model": "kirha-flash" },
    "include_raw_data": true
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
