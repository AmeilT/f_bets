# Data Sources Reference

Complete reference for all APIs, data sources, and tools used in the F_BETS system.

---

## 1. Odds Data

### The Odds API (PRIMARY)
- **URL:** https://the-odds-api.com/
- **Docs:** https://the-odds-api.com/liveapi/guides/v4/
- **Coverage:** EPL, Championship, Bundesliga, La Liga, Serie A, Ligue 1, Champions League, Europa League, Brasileirao
- **Free tier:** 500 requests/month
- **Paid:** From $25/month (20,000 requests)
- **Features:** Live + upcoming odds from 15+ bookmakers, historical odds (back to 2020)
- **Regions:** UK, EU, US, AU bookmakers
- **Delay:** Seconds to ~1 minute during live matches
- **MCP available:** Yes

### Betfair Exchange API (PHASE 2)
- **URL:** https://developer.betfair.com/
- **Access:** Free dev key (delayed), GBP 299 for live key
- **Features:** Exchange back/lay prices, market volumes, streaming API
- **Why it matters:** Exchange odds are the closest thing to "true" market probability -- essential for CLV analysis

### Odds-API.io (SUPPLEMENTARY)
- **URL:** https://odds-api.io
- **Free tier:** 100 requests/hour (forever)
- **Features:** 250+ bookmakers, <150ms latency
- **Use case:** Supplementary odds source when The Odds API quota runs low

---

## 2. Football Stats & Data

### API-Football (PRIMARY)
- **URL:** https://www.api-football.com/
- **Docs:** https://www.api-football.com/documentation
- **Coverage:** 1,200+ leagues worldwide
- **Free tier:** Limited seasons, all endpoints accessible
- **Paid:** From $19/month
- **Key endpoints:**
  - `/fixtures` -- upcoming and past matches
  - `/fixtures/statistics` -- match stats (shots, possession, corners, etc.)
  - `/standings` -- league tables
  - `/teams/statistics` -- season aggregates
  - `/players` -- individual player stats
  - `/injuries` -- current injuries
  - `/predictions` -- built-in predictions
  - `/odds` -- pre-match odds (from bookmakers)
- **Update frequency:** 15-second livescore updates
- **MCP available:** Yes

### Football-Data.org (SUPPLEMENTARY)
- **URL:** https://www.football-data.org/
- **Coverage (free forever):** Champions League, Premier League, Eredivisie, Bundesliga, Ligue 1, Serie A, La Liga, Championship, Brasileirao, Primeira Liga
- **Rate limit:** 10 requests/minute
- **Key endpoints:**
  - `/competitions/{id}/matches` -- fixtures and results
  - `/competitions/{id}/standings` -- league tables
  - `/teams/{id}/matches` -- team fixtures
  - `/matches` -- upcoming matches across leagues

### Sportmonks (PHASE 2)
- **URL:** https://www.sportmonks.com/football-api/
- **Free tier:** Danish Superliga, Scottish Premiership only
- **European plan:** EUR 39/month -- top European leagues
- **Worldwide:** EUR 129/month -- 2,500+ leagues
- **Key feature:** Native xG data via API (unlike most competitors)

---

## 3. Advanced Stats (xG, xA, etc.)

### FBref
- **URL:** https://fbref.com/en/
- **Data source:** StatsBomb (for top leagues)
- **Access:** Web only (no API) -- use web fetch/scraping
- **Key pages:**
  - `/en/comps/{id}/schedule/` -- fixtures with xG
  - `/en/comps/{id}/stats/` -- player stats with xG, xA
  - `/en/squads/{id}/` -- team stats
  - `/en/matches/{id}/` -- match reports with shot maps
- **Coverage:** All major European leagues + MLS, Liga MX, etc.
- **Quality:** Gold standard for freely available advanced stats

### Understat
- **URL:** https://understat.com/
- **Coverage:** EPL, La Liga, Bundesliga, Serie A, Ligue 1, Russian Premier League
- **Access:** Web only (no API) -- use web fetch/scraping
- **Key data:**
  - Team xG for/against per match
  - Player xG, xA, xGChain, xGBuildup
  - Shot-level data with xG values
  - Rolling xG trends
- **Model:** Neural network trained on 100,000+ shots with 10+ parameters
- **Quality:** Excellent, widely cited by analysts

### StatsBomb Open Data
- **URL:** https://github.com/statsbomb/open-data
- **Format:** JSON event-level data
- **Coverage (free):**
  - 2018 Men's World Cup
  - 2019 Women's World Cup
  - Various women's leagues
  - Messi's entire La Liga career
- **Use case:** Research, model prototyping, educational

---

## 4. Prediction Models & Expert Sources

### FiveThirtyEight Soccer Power Index (SPI)
- **URL:** https://projects.fivethirtyeight.com/soccer-predictions/
- **Data:** https://github.com/fivethirtyeight/data/tree/master/soccer-spi
- **Files:**
  - `spi_matches_latest.csv` -- current season match predictions
  - `spi_global_rankings.csv` -- team SPI ratings
  - `spi_matches.csv` -- historical predictions (from 2016)
- **Methodology:** Based on 550,000+ matches dating to 1888
- **Quality:** Transparent, rigorous, excellent benchmark

### OddAlerts AI
- **URL:** https://oddalerts.com/ai-football-predictions
- **Features:** 300+ daily predictions with value edge calculations
- **Data inputs:** Team stats, H2H, form, market odds
- **Access:** Free web
- **Quality:** Good for consensus checking, transparent edge percentages

### Infogol (Timeform)
- **URL:** https://timeform.com/football
- **Data source:** Opta-powered
- **Coverage:** Top European leagues + Champions League
- **Features:** Live xG, betting tips, match previews
- **Access:** Free web
- **Quality:** Professional-grade analysis, trusted brand

### Sports-AI.dev
- **URL:** https://www.sports-ai.dev/
- **Features:** 100-200 value bets per day
- **Distribution:** Telegram + web
- **Quality:** High volume, good for identifying bookmaker discrepancies

### Beta5.ai
- **URL:** https://beta5.ai/
- **Features:** Daily predictions, value bets, arbitrage
- **Access:** Web + Telegram
- **Quality:** Solid supplementary source

---

## 5. Injury & Team News

### Knocks and Bans
- **URL:** https://www.knocksandbans.com/
- **Focus:** Premier League primary
- **Features:** Availability probability, daily updates
- **Quality:** Dedicated injury tracking

### Injuries and Suspensions
- **URL:** https://injuriesandsuspensions.com/
- **Coverage:** 100+ leagues
- **Features:** Daily updates, comprehensive injury lists

### Premier Injuries
- **URL:** https://www.premierinjuries.com/
- **Focus:** EPL only
- **Features:** Expected return dates, severity ratings

### SportsGambler
- **URL:** https://www.sportsgambler.com/
- **Features:** Predicted lineups, team news aggregation

### API-Football Injuries Endpoint
- **Endpoint:** `/injuries`
- **Features:** Programmatic access to injury data
- **Coverage:** Follows API-Football league coverage

---

## 6. Weather Data

### Metcheck Football
- **URL:** https://www.metcheck.com/HOBBIES/football.asp
- **Coverage:** Premier League match weather
- **Use case:** Rain/wind can affect under/over markets

### World Weather Online
- **URL:** https://www.worldweatheronline.com/football.aspx
- **Coverage:** Global football weather
- **Features:** Temperature, wind, rain probability by venue

---

## 7. Historical Data (for backtesting)

### FiveThirtyEight Historical
- **URL:** https://github.com/fivethirtyeight/data/tree/master/soccer-spi
- **Coverage:** Match predictions from 2016 onwards
- **Format:** CSV
- **Cost:** Free

### OddsWarehouse (PHASE 2)
- **URL:** https://www.oddswarehouse.com/
- **Coverage:** Multiple leagues, closing odds
- **Cost:** $39 (1 season) to $79 (10+ years)
- **Format:** CSV downloads

### Oddsbase
- **URL:** https://oddsbase.net/
- **Coverage:** 20 years of historical odds from 2004
- **Access:** Web

---

## 8. Tipster Communities

### BettingExpert
- **URL:** https://www.bettingexpert.com/
- **Features:** Tipster rankings, free predictions, track records
- **Quality:** Largest tipster community, good for consensus

### Typersi
- **URL:** https://typersi.com/
- **Features:** Tipster rankings by accuracy and consistency
- **Quality:** Good for identifying hot-streak tipsters

---

## API Key Requirements Summary

| Service | Key Required | How to Get |
|---------|-------------|------------|
| The Odds API | Yes | Sign up at the-odds-api.com |
| API-Football | Yes | Sign up at api-football.com or RapidAPI |
| Football-Data.org | Yes (free) | Sign up at football-data.org |
| FiveThirtyEight | No | Direct CSV/JSON access |
| FBref | No | Web access |
| Understat | No | Web access |
| Betfair | Yes (Phase 2) | developer.betfair.com |
| Sportmonks | Yes (Phase 2) | sportmonks.com |
