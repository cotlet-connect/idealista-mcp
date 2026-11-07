# How to connect Idealista to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Idealista account.** Idealista's official ChatGPT app and Claude connector search properties to buy or rent in Spain, Italy and Portugal. Cotlet.dev connects your own signed-in Idealista account to any AI agent, so the AI lists, checks and updates your listings for you.

## What you can ask

> List all my active listings with price, views and days online.

> Lower the price of the flat on Calle Alcalá 120 in Madrid from €385,000 to €369,000.

> Rewrite the description of my two-bedroom in Lisbon to highlight the new kitchen and the terrace. Show me the draft first.

> Which of my listings got no contacts in the last 14 days? Sort them by price.

> Add the 6 new photos to my Barcelona loft listing and put the terrace photo first.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Idealista tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"idealista":{"command":"uvx","args":["idealista-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t idealista-mcp .
docker run -i --rm -e COTLET_API_KEY idealista-mcp
```

Tools: `idealista_guide`, `idealista_status`, `idealista_open`, `idealista_read`, `idealista_click`, `idealista_type`, `idealista_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install idealista-mcp        # or run it once: uvx idealista-mcp connect
idealista-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 idealista_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 idealista_agent.py status    # is Idealista ready in your Cotlet.dev account
python3 idealista_agent.py guide     # Idealista screens and sign-in link
python3 idealista_agent.py read      # open Idealista, read the page, close the browser
python3 idealista_agent.py tools     # list Cotlet.dev tools
python3 idealista_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Idealista users

**Does Idealista have an API?**

Idealista has no public API for your own listings or contacts (checked 11 Oct 2026). Its Search API is read-only and given only after an application, and its official Claude and ChatGPT app only searches public listings, with no login. Cotlet.dev works in your own signed-in Idealista account, so your AI agent can list and update your listings with no API key and no code.

**How do I connect Idealista to ChatGPT?**

Idealista's official ChatGPT app searches properties. To work with your own listings, add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Idealista once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Idealista API key.

**Is there a way to use Claude with Idealista?**

Yes. Idealista's own Claude connector covers property search. To manage your listings, run the one-line `claude mcp add` command above in Claude Code, or add `https://cotlet.dev/mcp/v1` as a custom connector in the Claude app. Claude then works in your own Idealista account.

**Is there an Idealista MCP server?**

Idealista's official connectors focus on property search in Spain, Italy and Portugal. Cotlet.dev is a hosted MCP server that works in your own Idealista account for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [Idealista on Cotlet.dev](https://cotlet.dev/integrations/idealista-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=idealista&utm_content=find)
- [PyPI package idealista-mcp](https://pypi.org/project/idealista-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-idealista-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [Vagaro MCP](https://github.com/cotlet-connect/vagaro-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Zoopla MCP](https://github.com/cotlet-connect/zoopla-mcp)
- [Dribbble MCP](https://github.com/cotlet-connect/dribbble-mcp)
- [Hostelworld MCP](https://github.com/cotlet-connect/hostelworld-mcp)
- [Mashvisor MCP](https://github.com/cotlet-connect/mashvisor-mcp)
- [Rent Manager MCP](https://github.com/cotlet-connect/rent-manager-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/idealista-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=idealista

Start free: https://cotlet.dev/signup?app=idealista&utm_source=github&utm_medium=readme&utm_campaign=idealista
