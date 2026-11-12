# Fokals MCP server

[![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/fokals/mcp-server/badge)](https://scorecard.dev/viewer/?uri=github.com/fokals/mcp-server)

Market & Company Intelligence for AI agents: what companies will likely adopt next, company health, buying signals and market feeds, from technology, hiring and funding data.

Fokals is a hosted MCP server. Add it to VS Code, GitHub Copilot, Claude, ChatGPT, Cursor or any client that supports the Model Context Protocol, and ask about any company or any market. There is nothing to install: this repository describes the server and how to connect to it.

| | |
| --- | --- |
| Server address | `https://mcp.fokals.com/mcp` |
| Transport | Streamable HTTP |
| Sign-in | OAuth (dynamic client registration), or a key from your account page as a bearer token |
| Registry name | `com.fokals/fokals` |
| Reference | [fokals.com/docs/connect](https://www.fokals.com/docs/connect) |

## What you can ask

- **Likely next.** The technologies a company is likely to add next, each with an estimated likelihood and the support behind it, or the likeliest next buyers of a product.
- **Company health.** A weekly band from signs of distress to breaking out, a distress score and a breakout score from 0 to 100, and the reasons in plain words.
- **Buying signals.** Each buying topic a company shows signs of, scored every week with the evidence behind it, so you see interest building or fading.
- **Feeds.** Every buying signal, announcement and website change across all companies from any day on, and the market figures that moved most on a day.
- **Markets.** Hiring, technologies taken up and dropped, buying topics, traffic and headcount over time, by industry, country or company size.
- **Vendor scorecards.** How many companies took up a technology and how many dropped it, month by month, with the rivals they came from and moved to.
- **Your own lists.** Enrich your accounts by website or name, find lookalikes and competitors, or find the companies that look today the way your customers did when they bought.
- **One account in depth.** Its stack and when each tool appeared, open roles, announcements, funding, headcount, traffic and recent website changes.
- **Watches.** An email when something changes at the companies you name.

Every record describes a company or a market, with nothing personal in it. Data is refreshed every day.

## Get started

1. Create an account at [fokals.com/signup](https://www.fokals.com/signup). It opens with $1 of credit, with no card and no subscription.
2. Add the server to your client (below).
3. Ask: "Which of these accounts will likely add a CRM next?" or "Find B2B software companies that started hiring this month."

### VS Code with GitHub Copilot

Run **MCP: Add Server** from the Command Palette, choose HTTP and paste `https://mcp.fokals.com/mcp`. Or add it to `.mcp.json` at the root of your workspace (or to your user `~/.copilot/mcp-config.json`):

```json
{
  "mcpServers": {
    "fokals": {
      "type": "http",
      "url": "https://mcp.fokals.com/mcp",
      "tools": ["*"]
    }
  }
}
```

When VS Code offers to authenticate the server, sign in with your Fokals account. To use a key instead, make one on your [account page](https://www.fokals.com/account), set it in your environment as `FOKALS_API_KEY`, and add a header:

```json
{
  "mcpServers": {
    "fokals": {
      "type": "http",
      "url": "https://mcp.fokals.com/mcp",
      "headers": {
        "Authorization": "Bearer ${FOKALS_API_KEY}"
      },
      "tools": ["*"]
    }
  }
}
```

### GitHub Copilot coding agent

The coding agent connects with a key. In your repository, open **Settings**, then **Copilot**, then **MCP servers**, and paste this into the MCP configuration:

```json
{
  "mcpServers": {
    "fokals": {
      "type": "http",
      "url": "https://mcp.fokals.com/mcp",
      "headers": {
        "Authorization": "Bearer $COPILOT_MCP_FOKALS_API_KEY"
      },
      "tools": ["*"]
    }
  }
}
```

Then add your key as a Copilot secret named `COPILOT_MCP_FOKALS_API_KEY`. To keep the agent to free and lower-cost tools, list them in `tools` instead of `"*"`, and set a monthly spending limit on your account page.

### Other clients

| Client | How |
| --- | --- |
| Claude and ChatGPT | In the assistant's settings, add a custom connector with `https://mcp.fokals.com/mcp`, then sign in when asked. |
| Claude Code | `claude mcp add --transport http fokals https://mcp.fokals.com/mcp`, then sign in from `/mcp`. Or add `--header "Authorization: Bearer YOUR_KEY"`. |
| Cursor | Add `{"mcpServers": {"fokals": {"url": "https://mcp.fokals.com/mcp"}}}` to `.cursor/mcp.json`, or install [Fokals for Cursor](https://github.com/fokals/cursor-plugin). |
| Any MCP client | Connect to `https://mcp.fokals.com/mcp` over Streamable HTTP and sign in with OAuth, or send `Authorization: Bearer YOUR_KEY`. |

## Tools

Free tools are marked. Every other tool is priced per company or per market question, and every answer says what it cost.

**Find companies**

| Tool | What it does |
| --- | --- |
| `count_companies` | How many companies match a set of filters, and what they would cost. Free. |
| `find_companies` | Companies by a technology they run, added, dropped or will likely adopt next, a buying topic, hiring, an announcement, industry, country or size. |
| `find_companies_by_description` | Companies whose websites describe the business you describe, the closest first. |
| `companies_described_alike` | Companies whose websites describe the same kind of business as one you name. |
| `similar_companies` | Lookalikes and competitors of a company, each with what they share. |
| `companies_like_customers` | Companies that look today the way your customers looked when they bought. |
| `identify_company` | Which company a name or a website address means. Free. |
| `search_job_postings` | Open roles by title, function, seniority, country, work mode, technology or pay. |
| `list_filters` | The values each filter takes. Free. |

**Your companies**

| Tool | What it does |
| --- | --- |
| `enrich_companies` | Your own list, by website or name, with industry, technologies, hiring and buying signals. |
| `enrich_to_file` | A long list enriched into a CSV file. |
| `company_profile` | One company in depth: what it sells and to whom, its stack and since when, open roles, buying topics, announcements, website changes. |
| `company_changes` | What is new at your companies since a date. |
| `company_health` | The weekly health band, distress and breakout scores, reasons and shifts in positioning. |
| `likely_next` | The technologies your companies will likely add next. |
| `intent_history` | Each buying topic week by week, with its score and whether it was surging. |
| `revenue_nowcast` | For US-listed companies, the likely revenue growth of a quarter just ended, before the results are out. |
| `sales_team` | The sales team a company is building, from its own job ads, with the pay each ad offers. |
| `funding_filings` | Private fundraises filed with the regulator, newest first. |
| `headcount_history` | Headcount over the years. |
| `traffic_history` | Website traffic month by month for up to 13 months. |
| `company_connections` | The customers, partners, integrations and investors a company's website names. |
| `watch_companies`, `unwatch_companies`, `watched_companies` | Emails when something changes at your companies, weekly or daily. Free to set up; each digest is priced by what it holds. |

**Markets and feeds**

| Tool | What it does |
| --- | --- |
| `market_breakdown` | How the companies that match split by industry, country, size or technology. |
| `market_trends` | How a market measure moved over time: hiring, pay, technologies, buying topics, traffic, headcount. |
| `market_movers` | The market figures that moved most on a day. |
| `vendor_scorecard` | A technology's companies gained and lost month by month, with churn and the rivals involved. |
| `sales_pay_benchmarks` | Advertised sales pay by role and country. |
| `signal_feed` | Every buying signal across all companies from a day on. |
| `announcement_feed` | Every announcement across all companies from a day on. |
| `change_feed` | Every website change across all companies from a day on. |
| `listed_securities` | Equity listings with tickers, exchanges and global identifiers. |

**Account**

| Tool | What it does |
| --- | --- |
| `account_balance` | Your balance, what you have spent and on which tools, your limit and the prices. Free. |
| `add_funds` | Adds funds with a payment token, for an agent that pays on your behalf. |
| `request_company` | Asks for a company to be added, by its website. Free. |
| `report_problem` | Reports wrong data, a tool that did not work, or an idea. Free. |

Inputs, outputs and an example for every tool: [fokals.com/docs/connect#reference](https://www.fokals.com/docs/connect#reference).

## Pricing

A prepaid balance in US dollars, with no subscription and no minimum. You pay for each company you get and each market question you ask:

- $0.04 for each company in a search or a list you bring, $0.08 for a company found by buying topic and $0.10 for a full profile, with lower prices at volume.
- The same company is free again for 30 days.
- A company that is not found costs nothing.
- A request above $0.25 shows its price first and waits for your yes.
- You can set your own monthly spending limit. Funds last 12 months from the day you add them.

Current prices: [fokals.com/pricing](https://www.fokals.com/pricing).

## The same tools in code

- HTTP API: every tool is also an endpoint at `https://api.fokals.com/v1`, on the same account, balance and prices. OpenAPI: [api.fokals.com/v1/openapi.json](https://api.fokals.com/v1/openapi.json).
- LangChain: [langchain-fokals](https://github.com/fokals/langchain-fokals) on PyPI.
- AI SDK: [@fokals/ai-sdk](https://github.com/fokals/ai-sdk) on npm.

## Support

support@fokals.com · [fokals.com](https://www.fokals.com)

## License

The configuration examples in this repository are MIT licensed. Use of the Fokals service is governed by the [Terms](https://www.fokals.com/terms).
