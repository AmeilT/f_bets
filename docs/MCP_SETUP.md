# MCP Server Setup Guide

How to configure Model Context Protocol servers for the F_BETS system so Claude can query football data and odds directly.

---

## Overview

MCP servers act as bridges between Claude and external APIs. Instead of manually calling APIs, we configure MCP servers so Claude can query data using natural language during daily sessions.

---

## 1. The Odds API MCP Server

### Purpose
Real-time odds comparison across bookmakers for value identification.

### Source
- **GitHub:** Search for "the-odds-api mcp server" on pulsemcp.com
- **Author:** kitchenchem

### Configuration

Add to your Claude MCP config (`.claude/mcp_servers.json` or equivalent):

```json
{
  "odds-api": {
    "command": "npx",
    "args": ["-y", "@kitchenchem/odds-api-mcp"],
    "env": {
      "ODDS_API_KEY": "<your-the-odds-api-key>"
    }
  }
}
```

### Available Tools
- Get list of available sports
- Get odds for specific events/leagues
- Compare odds across bookmakers
- Check API quota/usage

### Setup Steps
1. Sign up at https://the-odds-api.com/ (free tier: 500 req/month)
2. Copy your API key from the dashboard
3. Add the MCP config above
4. Test with: "What are the current Premier League odds for this weekend?"

---

## 2. API-Football MCP Server

### Purpose
Match data, standings, team stats, player stats, injuries, lineups.

### Source
- **PulseMCP:** API-Football MCP by Obino Paul

### Configuration

```json
{
  "api-football": {
    "command": "npx",
    "args": ["-y", "api-football-mcp"],
    "env": {
      "API_FOOTBALL_KEY": "<your-api-football-key>"
    }
  }
}
```

### Available Tools
- League standings
- Upcoming fixtures
- Team statistics
- Player statistics
- Live match info
- Injury reports

### Setup Steps
1. Sign up at https://www.api-football.com/ or via RapidAPI
2. Copy your API key
3. Add the MCP config above
4. Test with: "Show me the Premier League standings"

---

## 3. Soccerdata MCP Server

### Purpose
Real-time football data -- live scores, lineups, match details, events.

### Source
- **FloHunt:** https://www.flowhunt.io/integrations/soccerdataapi/

### Configuration

```json
{
  "soccerdata": {
    "command": "npx",
    "args": ["-y", "soccerdata-mcp"],
    "env": {
      "SOCCERDATA_API_KEY": "<your-key-if-required>"
    }
  }
}
```

### Available Tools
- Live scores
- Match lineups
- Match events (goals, cards, substitutions)
- Match details

---

## 4. Cloudbet Sports MCP Server

### Purpose
Educational/supplementary sports betting data via Cloudbet's public API.

### Source
- **GitHub:** https://github.com/cloudbet/sports-mcp-server

### Configuration

```json
{
  "cloudbet-sports": {
    "command": "npx",
    "args": ["-y", "@cloudbet/sports-mcp-server"]
  }
}
```

### Notes
- No API key required (uses public API)
- Primarily educational/demo purpose
- Good for supplementary market data

---

## 5. Web Fetch (Built-in)

### Purpose
Scrape data from websites without APIs: FBref, Understat, FiveThirtyEight, Infogol, injury sites.

### Configuration
Claude Code has WebFetch built in. No additional setup needed.

### Key URLs to Fetch

| Source | URL Pattern | Data |
|--------|------------|------|
| FiveThirtyEight | `https://projects.fivethirtyeight.com/soccer-predictions/premier-league/` | Match predictions |
| FBref EPL | `https://fbref.com/en/comps/9/schedule/Premier-League-Scores-and-Fixtures` | xG by match |
| Understat EPL | `https://understat.com/league/EPL` | Team xG trends |
| Infogol | `https://timeform.com/football` | Expert analysis |
| Knocks & Bans | `https://www.knocksandbans.com/` | Injury updates |
| OddAlerts | `https://oddalerts.com/ai-football-predictions` | AI predictions |

---

## Combined MCP Config

Full `.claude/mcp_servers.json`:

```json
{
  "mcpServers": {
    "odds-api": {
      "command": "npx",
      "args": ["-y", "@kitchenchem/odds-api-mcp"],
      "env": {
        "ODDS_API_KEY": "<YOUR_KEY>"
      }
    },
    "api-football": {
      "command": "npx",
      "args": ["-y", "api-football-mcp"],
      "env": {
        "API_FOOTBALL_KEY": "<YOUR_KEY>"
      }
    },
    "soccerdata": {
      "command": "npx",
      "args": ["-y", "soccerdata-mcp"],
      "env": {
        "SOCCERDATA_API_KEY": "<YOUR_KEY>"
      }
    },
    "cloudbet-sports": {
      "command": "npx",
      "args": ["-y", "@cloudbet/sports-mcp-server"]
    }
  }
}
```

---

## API Key Checklist

Before your first daily session, ensure you have:

- [ ] **The Odds API key** -- sign up at https://the-odds-api.com/
- [ ] **API-Football key** -- sign up at https://www.api-football.com/
- [ ] **Football-Data.org key** -- sign up at https://www.football-data.org/
- [ ] MCP servers installed and tested
- [ ] Verified each MCP responds to a test query

---

## Quota Management

### The Odds API (500 free requests/month)
- Each odds query = 1 request per sport/region
- Budget: ~16 requests/day
- Strategy: Query once per league per day, cache mentally during session

### API-Football (Free tier)
- Limited to current season data
- All endpoints accessible
- Rate limits apply

### Optimisation Tips
1. Batch queries -- ask for all fixtures in one request rather than per-match
2. Focus on matchdays -- don't query on days with no matches
3. Prioritise leagues -- EPL and Champions League first, expand if quota allows
4. Use Football-Data.org for standings/fixtures (separate free quota)
5. Use web fetch for xG data (no API quota consumed)
