# Smart Money Data MCP

Remote MCP servers for the [smartmoney-data](https://apify.com/smartmoney-data) Apify Actors: SEC EDGAR filings, Form 4 insider trades, 13F hedge fund holdings, Congress stock trades, 13D/13G activist stakes, Form 144 planned sales, 8-K events, company financials (XBRL), short interest, dark pool volume, trading halts, PDUFA / biotech catalysts, Polymarket whales, plus an FDA recall checker.

Nothing to install. Each server is the hosted [Apify MCP server](https://docs.apify.com/platform/integrations/mcp) (`https://mcp.apify.com`, streamable HTTP) with a fixed set of Actors loaded. Data comes from official public sources (SEC EDGAR, FINRA, Nasdaq Trader, House/Senate STOCK Act disclosures, openFDA, ClinicalTrials.gov, USAspending, LDA).

## Authentication

Use an Apify API token in the `Authorization: Bearer <token>` header (get one at https://console.apify.com/account/integrations), or connect with OAuth in clients that support it. Actor runs are billed pay-per-result on your Apify account; see each Actor's page for prices.

## Servers

| Registry name | Endpoint |
|---|---|
| `io.github.wyeming95-rgb/smartmoney-data` (all 19 finance Actors) | see [`server.json`](server.json) |
| `io.github.wyeming95-rgb/openfda-recalls` | `https://mcp.apify.com/?actors=smartmoney-data/openfda` |

Single-Actor endpoint pattern: `https://mcp.apify.com/?actors=smartmoney-data/<actor-name>`. Combine several with commas: `?actors=smartmoney-data/a,smartmoney-data/b`.

### Actors

| Actor | What it returns |
|---|---|
| [sec-insider-trades-tracker](https://apify.com/smartmoney-data/sec-insider-trades-tracker) | SEC Form 4 insider buys and sells, 10b5-1 flags |
| [congress-stock-trades-tracker](https://apify.com/smartmoney-data/congress-stock-trades-tracker) | Senate and House stock trades (STOCK Act) |
| [sec-13f-hedge-fund-tracker](https://apify.com/smartmoney-data/sec-13f-hedge-fund-tracker) | Hedge fund 13F portfolios with quarter-over-quarter changes |
| [hedge-fund-13f-consensus](https://apify.com/smartmoney-data/hedge-fund-13f-consensus) | Stocks the most hedge funds bought or sold last quarter |
| [institutional-ownership-by-ticker](https://apify.com/smartmoney-data/institutional-ownership-by-ticker) | Every 13F institution holding a given stock |
| [sec-13d-13g-activist-stakes](https://apify.com/smartmoney-data/sec-13d-13g-activist-stakes) | Activist investors and 5%+ owners |
| [sec-form-144-planned-insider-sales](https://apify.com/smartmoney-data/sec-form-144-planned-insider-sales) | Form 144 planned insider sales |
| [sec-8k-material-events](https://apify.com/smartmoney-data/sec-8k-material-events) | 8-K filings classified by item |
| [sec-edgar-filings](https://apify.com/smartmoney-data/sec-edgar-filings) | 10-K, 10-Q, 8-K filings, XBRL financials, section text |
| [us-company-financials](https://apify.com/smartmoney-data/us-company-financials) | Revenue, EPS, cash flow from SEC XBRL |
| [short-squeeze-radar](https://apify.com/smartmoney-data/short-squeeze-radar) | Short interest, FTD and Reg SHO squeeze score |
| [dark-pool-volume-tracker](https://apify.com/smartmoney-data/dark-pool-volume-tracker) | FINRA ATS / off-exchange volume |
| [trading-halts-suspensions-monitor](https://apify.com/smartmoney-data/trading-halts-suspensions-monitor) | Trading halts and SEC suspensions |
| [red-flag-radar](https://apify.com/smartmoney-data/red-flag-radar) | Stock risk score from filings and halts |
| [biotech-catalyst-calendar](https://apify.com/smartmoney-data/biotech-catalyst-calendar) | PDUFA dates, trial readouts, FDA approvals |
| [washington-money-contracts-lobbying](https://apify.com/smartmoney-data/washington-money-contracts-lobbying) | Federal contracts, lobbying and Congress trades per stock |
| [smart-money-confluence-score](https://apify.com/smartmoney-data/smart-money-confluence-score) | Combined insider / activist / Congress score |
| [smart-money-watchlist-alerts](https://apify.com/smartmoney-data/smart-money-watchlist-alerts) | New insider, 13D, Form 144 and Congress events for a watchlist |
| [polymarket-smart-money](https://apify.com/smartmoney-data/polymarket-smart-money) | Polymarket whale trades and top traders |
| [openfda](https://apify.com/smartmoney-data/openfda) | FDA food, drug and device recalls (openFDA) |

## Client config example

```json
{
  "mcpServers": {
    "smartmoney-data": {
      "url": "https://mcp.apify.com/?actors=smartmoney-data/sec-insider-trades-tracker,smartmoney-data/congress-stock-trades-tracker",
      "headers": { "Authorization": "Bearer <your-apify-api-token>" }
    }
  }
}
```

Unofficial. Not affiliated with the SEC, FINRA, FDA or any other agency. Not investment advice.
