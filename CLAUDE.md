# F_BETS -- Football Value Betting System

## What This Project Is

A daily value-betting analysis system for football (soccer). Claude analyses odds, stats, xG data, injuries, and expert predictions to find bets where the bookmaker's odds undervalue the true probability of an outcome.

## How Daily Sessions Work

1. User asks for today's value bets
2. Claude pulls fixtures, odds, form data, injuries, and expert predictions
3. Claude calculates where assessed probability > implied probability by >5%
4. Claude outputs ranked picks with full reasoning and linked sources
5. Picks are logged in `tracking/picks/YYYY-MM-DD.md`

## Key Documents

- `PLAN.md` -- full system architecture and phased roadmap
- `docs/DATA_SOURCES.md` -- all APIs, data sources, and access details
- `docs/MCP_SETUP.md` -- MCP server configuration
- `docs/DAILY_WORKFLOW.md` -- step-by-step daily process

## Data Sources (Quick Reference)

### Odds
- **The Odds API** (MCP) -- live odds from 15+ bookmakers
- **Odds-API.io** -- supplementary odds (100 req/hour free)

### Stats
- **API-Football** (MCP) -- fixtures, standings, team stats, injuries (1,200+ leagues)
- **Football-Data.org** -- standings, fixtures (top 10 leagues free)

### Advanced Stats (xG)
- **FBref** (web fetch) -- StatsBomb-powered xG, xA, advanced metrics
- **Understat** (web fetch) -- neural-network xG model, team trends

### Predictions & Expert
- **FiveThirtyEight SPI** (web fetch) -- match probabilities from Soccer Power Index
- **OddAlerts AI** (web fetch) -- AI predictions with value edge %
- **Infogol/Timeform** (web fetch) -- Opta-powered xG analysis

### Injuries
- **API-Football injuries endpoint** -- programmatic injury data
- **Knocks and Bans** (web fetch) -- availability updates (EPL focus)

## League Coverage

EPL, Championship, La Liga, Bundesliga, Serie A, Ligue 1, Champions League, Europa League

## Value Thresholds

- **Min edge to bet:** 5% (assessed prob vs implied prob)
- **Sweet spot:** 8-15% edge
- **Max stake:** 3 units per bet
- **Max daily exposure:** 10 units
- **Max picks per day:** 5

## Probability Weighting (Phase 1)

Since we use external models rather than our own:
- FiveThirtyEight SPI: 30%
- xG-implied probability: 30%
- Market consensus: 25%
- Expert/AI consensus: 15%

## Pick Format

Every pick must include:
1. Match, market, odds, bookmaker
2. Value rating (1-5 stars) and edge %
3. Confidence level and stake
4. Thesis (2-3 sentences)
5. Supporting data with sources
6. Key risks
7. Linked sources for every claim

## Tracking

- Daily picks: `tracking/picks/YYYY-MM-DD.md`
- Weekly reviews: `tracking/results/week-YYYY-WXX.md`
- Monthly reviews: `tracking/results/month-YYYY-MM.md`

## Commands

- **Daily analysis:** "Find today's value bets"
- **Specific league:** "What are the best EPL bets this weekend?"
- **Review:** "Review this week's picks and calculate ROI"
- **Deep dive:** "Analyse [Team A] vs [Team B] in detail"
