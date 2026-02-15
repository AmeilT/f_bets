# Daily Workflow: Finding Value Bets

Step-by-step process for each daily session with Claude.

---

## Quick Start Prompt

Copy-paste this to kick off a daily session:

> "Let's find today's value bets. Check fixtures across EPL, La Liga, Bundesliga, Serie A, Ligue 1, and Champions League/Europa League. Pull odds, xG form, injuries, and expert predictions. Give me your best value picks with full reasoning and sources."

---

## Step-by-Step Process

### Step 1: Fixture Scan (2 min)

**What:** Identify all matches in target leagues for today/tomorrow.

**Sources:**
- API-Football MCP: upcoming fixtures
- Football-Data.org: fixture list with kick-off times

**Output:** List of matches to analyse, filtered by:
- Leagues we cover
- Kick-off time (enough time to place bets)
- Market liquidity (skip very minor matches)

---

### Step 2: Odds Snapshot (3 min)

**What:** Capture current odds from multiple bookmakers for each match.

**Sources:**
- The Odds API MCP: odds from 15+ bookmakers
- Calculate implied probabilities from odds

**Key Markets:**
| Market | Description | Good For |
|--------|-------------|----------|
| 1X2 | Match result (Home/Draw/Away) | Main market, most liquid |
| Over/Under 2.5 | Total goals | Correlates well with xG |
| BTTS | Both teams to score | xG for/against analysis |
| Asian Handicap | Spread betting | Removes draw, tighter odds |
| Double Chance | Two outcomes covered | Lower risk plays |

**Output:** Odds matrix per match with implied probabilities.

---

### Step 3: Form & Stats (5 min)

**What:** Gather recent performance data for each team.

**Sources:**
- API-Football MCP: last 5-10 match results, season stats
- FBref (web fetch): xG, xGA per match (last 5-10 games)
- Understat (web fetch): team xG trends, over/underperformance
- Football-Data.org: league standings, home/away records

**Key Metrics:**
| Metric | Why It Matters |
|--------|---------------|
| xG per game (last 5) | Underlying attacking quality |
| xGA per game (last 5) | Underlying defensive quality |
| xG difference | Net quality indicator |
| Actual goals vs xG | Over/underperformance (regression candidate) |
| Home/away splits | Some teams are drastically different |
| H2H record | Historical matchup patterns |
| Goals scored/conceded | For O/U and BTTS markets |
| Clean sheet % | For BTTS market |
| Shots on target | Process indicator |

---

### Step 4: Injury & Team News (3 min)

**What:** Check who's missing and how it affects the team.

**Sources:**
- API-Football MCP: injuries endpoint
- Knocks and Bans (web fetch): availability updates
- Injuries and Suspensions (web fetch): broader coverage

**Key Considerations:**
- Is the star striker/playmaker out? (huge xG impact)
- Defensive injuries? (affects xGA, BTTS, O/U)
- Goalkeeper injury? (massive impact on clean sheet probability)
- Rotation risk? (CL/EL midweek = weakened weekend lineup)
- Returning players? (positive boost often underpriced)

---

### Step 5: Expert & Model Consensus (5 min)

**What:** Compare what prediction models and experts are saying.

**Sources:**
- FiveThirtyEight SPI (web fetch): match probabilities
- OddAlerts AI (web fetch): predictions with value edges
- Infogol/Timeform (web fetch): xG-based previews
- BettingExpert (web): community tipster consensus

**What We're Looking For:**
- **Consensus:** When 3+ sources agree, confidence increases
- **Divergence from odds:** When models say 60% but odds imply 50% = potential value
- **Contrarian signals:** When one respected model disagrees with the market -- dig deeper

---

### Step 6: Value Calculation (5 min)

**What:** Compare our assessed probability against the bookmaker's implied probability.

**Formula:**
```
Implied Probability = 1 / Decimal Odds
Value = (Assessed Probability - Implied Probability) / Implied Probability

Example:
- Our assessment: Team A has 65% chance to win
- Best odds: 1.80 (implied probability = 55.6%)
- Value edge: (0.65 - 0.556) / 0.556 = 16.9% edge
```

**Value Thresholds:**
| Edge | Action |
|------|--------|
| < 5% | Skip -- not enough margin for error |
| 5-8% | Marginal -- only with high confidence |
| 8-15% | Sweet spot -- bet with standard stake |
| 15-25% | Strong value -- consider 2x stake |
| > 25% | Suspicious -- verify data, could be trap line |

**Aggregation Method (Phase 1):**
Since we're not building our own model, we weight sources:
- FiveThirtyEight SPI probability: 30%
- xG-implied probability (from form): 30%
- Market consensus (average of all bookmaker odds): 25%
- Expert/AI platform consensus: 15%

---

### Step 7: Weather Check (1 min)

**What:** Check if weather could affect the match.

**Sources:**
- Metcheck (web fetch): UK matches
- World Weather Online (web fetch): European matches

**Impact Matrix:**
| Condition | Effect |
|-----------|--------|
| Heavy rain | Fewer goals, more errors, favours defensive teams |
| Strong wind | Fewer goals, disrupts passing teams |
| Extreme heat | Fatigue in second half, favours deeper squads |
| Snow/ice | Chaos -- avoid betting or back unders |
| Perfect conditions | No adjustment needed |

---

### Step 8: Output Picks (5 min)

**What:** Compile final picks with full reasoning.

**Format per pick:**

```markdown
## PICK: [Match] -- [Market] @ [Odds] ([Bookmaker])

**Value Rating:** ★★★★☆ (4/5)
**Edge:** ~12%
**Confidence:** High
**Stake:** 2 units

### Thesis
[2-3 sentences on why this bet has value]

### Data
- xG form: [Team stats from Understat/FBref]
- Model probability: [538 / AI predictions]
- Implied vs assessed: [Odds implied X% vs our Y%]
- H2H: [Historical record]
- Team news: [Key absences/returns]
- Weather: [If relevant]

### Risks
- [Primary risk]
- [Secondary risk]

### Sources
- [Linked sources for each data point]
```

**Pick Limits:**
- Maximum 5 picks per day (quality over quantity)
- At least 1 must be from a "secondary" league (not EPL)
- No more than 2 picks from the same match

---

## Post-Session: Logging

After picks are made, log them in `tracking/picks/YYYY-MM-DD.md`:

```markdown
# Picks: [Date]

## Summary
- Total picks: X
- Total stake: X units
- Leagues: [list]

## Picks
[Copy of each pick from above]

## Results (fill in after matches)
| # | Match | Selection | Odds | Stake | Result | P&L |
|---|-------|-----------|------|-------|--------|-----|
| 1 | ... | ... | ... | ... | ... | ... |
```

---

## Weekly Review Prompt

> "Let's review this week's picks. Look at our tracking logs in tracking/picks/ for the last 7 days. Calculate hit rate, ROI, and CLV. Identify which leagues and markets performed best. What should we adjust?"

---

## Monthly Review Prompt

> "Monthly deep review. Analyse all picks from tracking/ for the past month. Calculate overall ROI, hit rate by league, hit rate by market, average edge on winners vs losers. Compare our assessed probabilities vs actual outcomes. Are we calibrated? What patterns emerge? What changes should we make to our approach?"
