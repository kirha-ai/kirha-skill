# Kirha Verticals Reference

Detailed reference for each vertical. Use this to disambiguate when the user's query could match multiple verticals.

---

## Insurance

**Slug:** `insurance`

Specialized data for insurance risk analysis, real-time transportation tracking, and weather monitoring. Covers flight lookup, weather-based risk assessment, and sector-specific automation.

**Providers:**
- **Winston** — Insurance-specific intelligence and risk analysis
- **Open Weather** — Real-time and historical weather data, forecasts
- **Mistral Documents** — Document analysis and extraction (e.g., claims, policies)
- **Web Search** — General web search via Exa engine
- **Aviationstack** — Flight tracking, status, and aviation data

**Best for queries about:**
- Weather-related risk or damage assessment
- Flight information and tracking
- Insurance claims analysis
- Document verification (e.g., AI-altered images)
- Natural disaster impact

**Example queries:**
- "Insurance risk related to weather at Valencia, Spain on 29 October 2024"
- "Fetch flight information for VY8006 on 24-09-2025"
- "Is this image AI-altered?" (with image URL)

---

## News

**Slug:** `news`

Real-time news aggregation, media monitoring, and content analysis. Includes article search, sentiment tracking, topic clustering, and automated news intelligence.

**Providers:**
- **Polymarket** — Prediction market data with real-time odds and volumes
- **X** — Posts, user data, engagement metrics from X/Twitter
- **Web Search** — Web search, structured queries, and news lookups via Exa
- **GoogleScholar** — Academic paper search (for research-backed news analysis)

**Best for queries about:**
- Breaking news and current events
- Media sentiment and public opinion
- Prediction market odds on events
- Social media trends and discussions
- Topic-specific news monitoring

**Example queries:**
- "Latest news about the EU AI Act"
- "What are prediction markets saying about the next US election?"
- "Trending topics on X about climate policy"
- "Recent articles on generative AI regulation"

---

## CyberSec

**Slug:** `cybersec`

Internet-connected device discovery, vulnerability scanning, and security threat intelligence. Search for exposed services, abuse reports, and security data.

**Providers:**
- **Shodan** — Internet-connected device search, IP lookups, open ports, vulnerability discovery
- **Github** — Repository search, issue tracking, contributor profiles
- **X** — Security community posts and threat discussions
- **AbuseIPDB** — IP abuse reports, malicious activity checks, confidence scoring
- **Web Search** — Security news and research via Exa

**Best for queries about:**
- IP address reputation and abuse reports
- Open ports and exposed services
- Vulnerability scanning and CVE lookups
- Security-related GitHub repositories and tools
- Threat intelligence and indicators of compromise

**Example queries:**
- "Check if IP 203.0.113.42 has any abuse reports"
- "Find open ports on 198.51.100.0/24"
- "Search for publicly accessible MongoDB servers"
- "Latest GitHub repos for CVE-2024 exploits"
- "Is this IP associated with malicious activity?"

---

## Adtech

**Slug:** `adtech`

Search intelligence for ad research and competitor analysis. Discover keywords, monitor campaigns, and uncover market trends for media strategies.

**Providers:**
- **Firecrawl** — Web scraping and content extraction
- **Apollo** — Contact and company enrichment for outreach
- **X** — Social media ad and campaign monitoring
- **Google Ads** — Ad campaign data, keyword research, competitive analysis
- **Web Search** — Market research and trend discovery via Exa

**Best for queries about:**
- Competitor ad campaigns and creatives
- Keyword research and search volume
- Ad spend analysis
- Social media advertising trends
- Market and campaign intelligence

**Example queries:**
- "Search for Tesla ads"
- "What ads is Nike running on YouTube?"
- "Show me video ads from Apple"
- "Top keywords for SaaS marketing in 2025"

---

## Crypto

**Slug:** `crypto`

Blockchain data, wallet analytics, DeFi tools, price tracking, token search, and digital asset management. The most provider-rich vertical.

**Providers:**
- **Firecrawl** — Web scraping for crypto news and data
- **Zerion** — Wallet portfolio tracking and DeFi positions
- **Dune Sim** — Simulated Dune Analytics queries
- **Xverse** — Bitcoin/Stacks wallet and ordinals
- **DefiLlama** — DeFi protocol TVL, yields, and analytics
- **Polymarket** — Crypto prediction markets
- **Coingecko** — Token prices, market data, and rankings
- **Cielo** — On-chain transaction monitoring
- **Token Terminal** — Crypto project financial metrics
- **X** — Crypto community discussions and alpha
- **Utils** — Utility tools for crypto operations
- **Web Search** — Crypto news and research via Exa
- **Dune** — On-chain analytics and SQL queries

**Best for queries about:**
- Token/coin prices and market data
- Wallet balances and transaction history
- DeFi protocol analytics (TVL, yields, volumes)
- On-chain data and blockchain queries
- NFTs, ordinals, and digital collectibles
- Crypto prediction markets

**Example queries:**
- "What's the balance of vitalik.eth over the last week?"
- "Chart me the Uniswap volume over the last week"
- "Give me the top 3 companies owning the most BTC"
- "Current Bitcoin price in USD"
- "Top DeFi protocols by TVL"

---

## Medical

**Slug:** `medical`

Biomedical intelligence for research and clinical use. Peer-reviewed literature, preprints, clinical trials, drug data, and patent information.

**Providers:**
- **Pubmed** — Biomedical literature from MEDLINE/PubMed
- **Firecrawl** — Web scraping for medical resources
- **Arxiv** — Preprints in quantitative biology and related fields
- **ChemRxiv** — Chemistry preprints
- **Mistral Documents** — Medical document analysis
- **OpenFDA** — FDA drug data, adverse events, recalls
- **Zenodo** — Open-access research datasets and publications
- **GoogleScholar** — Academic paper search with citation data
- **Patents View** — Patent search and analysis
- **ClinicalTrials** — ClinicalTrials.gov trial data
- **RxNorm** — Drug nomenclature and interaction data

**Best for queries about:**
- Clinical trial searches and results
- Drug information, interactions, and FDA data
- Peer-reviewed medical research
- Biomedical preprints and publications
- Medical patents
- Drug nomenclature and classifications

**Example queries:**
- "Latest clinical trials for CRISPR gene therapy"
- "GLP-1 receptor agonist adverse events from FDA"
- "Recent PubMed papers on mRNA vaccine efficacy"
- "Patent landscape for CAR-T cell therapy"
- "RxNorm lookup for metformin interactions"

---

## Company

**Slug:** `company`

Enriched company data for market research, prospecting, financial analysis, and due diligence. The broadest vertical with the most providers.

**Providers:**
- **Firecrawl** — Web scraping for company websites
- **Pappers** — French company registry data
- **Arxiv** — Research papers by company affiliations
- **Shodan** — Company infrastructure and exposed services
- **Linkedin** — Company and employee profiles
- **Github** — Company open-source presence
- **Marketstack** — Stock market data and historical prices
- **Mistral Documents** — Document analysis for filings and reports
- **DefiLlama** — DeFi exposure for crypto-adjacent companies
- **Fred** — Federal Reserve economic data
- **Polymarket** — Prediction markets related to companies
- **Apollo** — Company and contact enrichment
- **X** — Company mentions and executive social media
- **Transcript** — Earnings call transcripts
- **TED Europa** — European tender data
- **Web Search** — Company research via Exa
- **GoogleScholar** — Academic research by company
- **Patents View** — Company patent portfolios
- **Google Maps** — Company locations and reviews
- **Veridion** — Business data enrichment
- **Sec** — SEC filings (10-K, 10-Q, 8-K, etc.)

**Best for queries about:**
- Company profiles and financial data
- Stock prices and market performance
- SEC filings and earnings reports
- Competitor analysis and market research
- Company patents and R&D activity
- Employee and executive information
- European tenders and procurement

**Example queries:**
- "Find companies in France matching the name Decathlon"
- "Find the top 10 engineers at companies behind latest LLM patents"
- "List the 30 latest authors of research papers on RAG"
- "Tesla SEC filings from the last quarter"
- "Apple stock price over the last 6 months"

---

## Disambiguation Guide

| Query Pattern | Vertical | Reasoning |
|---|---|---|
| Token price, wallet, DeFi, blockchain | `crypto` | Blockchain-native data |
| Stock price, SEC filing, earnings, company profile | `company` | Traditional finance/corporate |
| Drug, clinical trial, PubMed, FDA | `medical` | Biomedical research |
| IP scan, CVE, vulnerability, abuse | `cybersec` | Security intelligence |
| Ad campaign, keyword, competitor ads | `adtech` | Advertising data |
| Flight, weather risk, insurance claim | `insurance` | Risk and transportation |
| Breaking news, sentiment, current events | `news` | Media and journalism |
| Company + news combo | Both `company` and `news` | Multi-vertical search |
| Crypto company financials | `company` first, `crypto` if on-chain | Depends on what data is needed |
