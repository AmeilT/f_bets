# F_BETS: Football Value Betting System

## Vision

A daily value-betting analysis system for football (soccer) that identifies the best value bets across major leagues by combining odds data, statistical models, expert predictions, and advanced metrics (xG, form, injuries). No proprietary models -- we leverage the best available tools, APIs, and MCP servers to surface actionable insights backed by sources.

## Core Principles

1. **Value over volume** -- only surface bets where the implied probability from odds is significantly lower than our assessed probability
2. **Source everything** -- every recommendation must cite data sources, expert opinions, or statistical backing
3. **No proprietary models (Phase 1)** -- use existing prediction models (FiveThirtyEight SPI, xG models, AI platforms) rather than building our own
4. **Bankroll discipline** -- include Kelly Criterion or flat-stake sizing with every pick
5. **Track everything** -- log all picks with outcomes for ROI analysis

---

## Architecture Overview

```
                    +-----------------------+
                    |   Daily Session       |
                    |   (Claude + MCPs)     |
                    +-----------+-----------+
                                |
                +---------------+---------------+
                |               |               |
        +-------v------+ +-----v-------+ +-----v-------+
        | Odds Layer   | | Stats Layer | | Expert Layer|
        | (The Odds    | | (API-Foot,  | | (538, AI    |
        |  API, Betfair| |  FBref, xG) | |  platforms) |
        |  MCP)        | | (Football   | |             |
        +--------------+ |  MCP)       | +-------------+
                         +-------------+
                                |
                    +-----------v-----------+
                    |   Analysis Engine     |
                    |   (Claude reasoning)  |
                    +-----------+-----------+
                                |
                    +-----------v-----------+
                    |   Output: Daily Picks |
                    |   + Tracking Log      |
                    +-----------------------+
```

## Phase 1: Foundation (Current)

### Goal
Get the system running with free-tier tools to produce daily value bet recommendations.

### Data Stack (Free Tier)

| Layer | Tool | Purpose | Cost |
|-------|------|---------|------|
| **Odds** | The Odds API | Live odds from 15+ bookmakers | Free (500 req/month) |
| **Odds** | The Odds API MCP Server | Natural language odds queries | Free |
| **Stats** | API-Football | Match data, lineups, form, injuries | Free tier |
| **Stats** | API-Football MCP Server | Natural language stats queries | Free |
| **Stats** | Football-Data.org | Standings, fixtures, results | Free (top 10 leagues) |
| **xG** | Understat (web) | Expected goals data | Free |
| **xG** | FBref (web) | StatsBomb-powered advanced stats | Free |
| **Predictions** | FiveThirtyEight SPI | Match probabilities, team ratings | Free |
| **Predictions** | OddAlerts AI | AI predictions with value edges | Free |
| **Expert** | Infogol/Timeform | Expert xG-based analysis | Free (web) |
| **Expert** | BettingExpert | Community tipster picks | Free |
| **Weather** | Metcheck/WWO | Match-day weather conditions | Free |
| **Injuries** | Knocks and Bans | Injury/availability data | Free |

### MCP Servers to Configure

1. **The Odds API MCP** -- real-time odds comparison across bookmakers
2. **API-Football MCP** -- fixtures, standings, team stats, player stats
3. **Soccerdata MCP** -- live scores and match details
4. **Web Fetch** -- for scraping Understat, FBref, FiveThirtyEight, Infogol
5. **Cloudbet Sports MCP** -- additional market data (educational)

### League Coverage (Phase 1)

- English Premier League
- English Championship
- Spanish La Liga
- German Bundesliga
- Italian Serie A
- French Ligue 1
- UEFA Champions League
- UEFA Europa League

---

## Phase 2: Enhanced (Month 2+)

### Upgrades
- **The Odds API paid tier** ($25/month) -- more requests, historical odds
- **API-Football paid tier** ($19/month) -- full historical data
- **Betfair API** (GBP 299 one-off) -- exchange odds for true market probability
- **OddsWarehouse** ($39-79 one-off) -- historical odds for backtesting
- **Sportmonks** (EUR 39/month) -- xG API access, deeper stats

### New Capabilities
- Historical ROI tracking dashboard
- Closing line value (CLV) analysis
- Line movement alerts
- Arbitrage detection
- Player prop analysis

---

## Phase 3: Proprietary Edge (Month 4+)

### Build Our Own
- Custom xG model trained on StatsBomb open data
- Poisson regression for match outcome probabilities
- Form-weighted Elo ratings
- Injury impact quantification model
- Weather impact model

---

## Daily Workflow

### Morning Routine (Match Day -1 or Match Day)

1. **Fixtures scan** -- pull today's/tomorrow's fixtures across target leagues
2. **Odds snapshot** -- capture current odds from multiple bookmakers
3. **Stats gathering** -- team form, H2H, home/away splits, xG trends
4. **Injury check** -- confirmed team news, suspensions, returns
5. **Expert consensus** -- FiveThirtyEight probabilities, AI predictions, tipster picks
6. **Weather check** -- conditions that could affect play style
7. **Value calculation** -- compare implied odds probability vs assessed probability
8. **Output picks** -- ranked by confidence with full reasoning and sources

### Pick Format

```markdown
## Pick: [Team A] vs [Team B] -- [Market] @ [Odds] ([Bookmaker])

**Value Rating:** [1-5 stars]
**Confidence:** [Low/Medium/High]
**Stake:** [Units based on Kelly/flat]

### Why This Bet

[2-3 sentence thesis]

### Data Backing

- **xG Form (last 5):** Team A 1.8 xG/game, Team B 1.2 xG/game (Understat)
- **FiveThirtyEight SPI:** Team A 68% win prob vs implied 55% from odds
- **H2H:** Team A won 4 of last 5 at home (API-Football)
- **Injuries:** Team B missing key CB (Knocks and Bans)
- **Expert consensus:** 3/4 AI models favour Team A (OddAlerts, 538, Infogol)

### Key Risks

- [Risk 1]
- [Risk 2]

### Sources

- [Source 1 with link]
- [Source 2 with link]
```

---

## Bankroll Management

### Rules

1. **Starting bankroll:** Define units (e.g., 1 unit = 1% of bankroll)
2. **Max stake:** 3 units per bet
3. **Daily max exposure:** 10 units
4. **Staking method:** Flat stakes (Phase 1), Kelly Criterion (Phase 2+)
5. **Stop loss:** Pause if bankroll drops 20% in a week

### Value Threshold

- **Minimum edge:** Bet only when assessed probability exceeds implied probability by >5%
- **Sweet spot:** 8-15% edge -- enough margin for model error
- **Avoid:** Edges >25% (likely a data error or trap line)

---

## Tracking & Accountability

### What We Track

| Field | Description |
|-------|-------------|
| Date | Match date |
| Match | Teams |
| League | Competition |
| Market | Bet type (1X2, O/U, BTTS, etc.) |
| Selection | Our pick |
| Odds | At time of pick |
| Bookmaker | Where the odds were found |
| Stake | Units wagered |
| Edge | Estimated % edge |
| Confidence | Low/Med/High |
| Result | W/L/V/P |
| P&L | Profit/loss in units |
| CLV | Closing line value |
| Notes | Key reasoning summary |

### Review Cadence

- **Daily:** Log results, update P&L
- **Weekly:** Review hit rate, ROI, identify patterns
- **Monthly:** Deep review -- which leagues/markets are profitable, adjust strategy

---

## File Structure

```
f_bets/
├── PLAN.md                      # This file -- system overview
├── CLAUDE.md                    # Context for Claude daily sessions
├── docs/
│   ├── DATA_SOURCES.md          # Detailed API/source reference
│   ├── MCP_SETUP.md             # MCP server configuration guide
│   └── DAILY_WORKFLOW.md        # Step-by-step daily process
├── tracking/
│   ├── picks/                   # Daily pick logs (YYYY-MM-DD.md)
│   └── results/                 # Weekly/monthly summaries
├── config/
│   └── mcp_servers.json         # MCP server configuration
└── scripts/                     # Helper scripts (Phase 2+)
```

---

## Success Metrics

### Phase 1 Targets (First 2 Months)

- **Volume:** 3-8 value picks per matchday
- **Hit rate:** Track actual vs predicted (target: positive CLV)
- **ROI:** Positive ROI after 100+ bets (even 2-5% ROI is excellent)
- **Process:** Consistent daily analysis with sourced reasoning

### Long-Term Targets

- **Positive CLV:** Consistently beating closing lines (the real measure of edge)
- **5%+ ROI** over 500+ bets
- **Diversified edge** across multiple leagues and markets
