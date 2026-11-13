# Worked examples

Five complete answers, built and tested in the live terminal on 2026-11-13. Match this format.
Ticker counts and names are from that day and will differ when the member builds it.

---

## Example 1: the wheel

**Member:** "I want to run the wheel on solid stocks that won't blow up. 30 to 45 days."

**Before answering:** the member gave no account size, so don't cap the price. Either ask
("How much would you put into one stock?") or build without a cap and explain how to add one.
This answer builds without it.

**Scan name:** Wheel - Large Cap
**What it finds:** large, liquid stocks with no earnings or deals in the next month, where
options have a steady history of being overpriced.
**Assumed:** 30–45 day options; no price cap (you didn't give an account size).

| # | Section | Filter | Set to | Why |
|---|---|---|---|---|
| 1 | Descriptive | Price | min 15 | Skip cheap stocks |
| 2 | Descriptive | Asset Type | Stock | Companies only, no leveraged funds |
| 3 | Descriptive | Market Cap | min 10000000 | $10 billion and up (typed in thousands) |
| 4 | Descriptive | Merger & Acquisition | None | No deal in progress |
| 5 | Option | Avg Option Volume | min 5000 | Easy fills |
| 6 | Volatility | IV30d Event | No | No earnings priced in |
| 7 | Variance Risk Premium | Avg NEVRP 4y | min 0 | Options overpriced on average over 4 years |
| 8 | Variance Risk Premium | NEVRP Win Rate 4y | min 55 | Overpriced on most days, not just a few |
| 9 | Earnings | Earnings Date | None | No report in the next month |

**Columns:** Price, Sector, IV30d, Implied Move 1d, IV30d & NERV20d Ratio, NEIV30d Percentile,
Avg NEVRP 4y, NEVRP Win Rate 4y
**Sort:** NEVRP Win Rate 4y, **highest to lowest**. For the wheel, steadiness matters more than
the biggest premium.

**What to expect:** about 20 stocks (on the test day: STM, ASML, AKAM, NKE, FCX).
- **To fit your account:** set Price max to your capital per stock ÷ 100 (for $5,000 per
  stock, max 50).
- **Too few:** lower Market Cap to 2000000 ($2 billion) and Avg Option Volume to 1000.
- **Picking today's best:** prefer names whose IV30d & NERV20d Ratio is above 1: options are
  charging more than the stock is moving right now.

**Setup**
1. Open **Scanner** in the left menu.
2. Click **New Scanner**, type **Wheel - Large Cap**, click **Create**, then **Ok**.
3. Click **Filters**.
4. Open **Descriptive**. Price: min 15. Asset Type: tick Stock. Market Cap: min 10000000.
   Merger & Acquisition: tick None.
5. Open **Option**. Avg Option Volume: min 5000.
6. Open **Volatility**. IV30d Event: tick No.
7. Open **Variance Risk Premium**. Avg NEVRP 4y: min 0. NEVRP Win Rate 4y: min 55.
8. Open **Earnings**. Earnings Date: tick None.
9. Click **Dismiss**.
10. Click **Columns**; search and tick the eight columns above.
11. Click the **NEVRP Win Rate 4y** header twice so the highest is on top.
12. Click **Save**, then **Overwrite Current**.

**Before you trade:** would you be happy owning 100 shares? Check the news, the bid-ask spread
on your strike, and that the next earnings date is after your expiry. Some big names (for
example Microsoft) are left out by the merger filter because they're buying a company; untick
None if you want them.

---

## Example 2: calendars and diagonals

**Member:** "I trade calendar spreads and diagonals. What should I look at?"

**Scan name:** Calendars - FF 30/60
**What it finds:** stocks where the near-month options are priced well above the following
month, with no earnings or deals to explain it.
**Assumed:** selling about 30 days and buying about 60 days.

| # | Section | Filter | Set to | Why |
|---|---|---|---|---|
| 1 | Descriptive | Price | min 5 | Skip cheap stocks |
| 2 | Descriptive | Asset Type | Stock | Leaves out leveraged and inverse funds, which top this list otherwise |
| 3 | Descriptive | Merger & Acquisition | None | Deals distort term structure |
| 4 | Descriptive | Sector | every sector except Healthcare (tick the other 11, including None) | Biotech news makes near-term IV jumpy |
| 5 | Option | Avg Option Volume | min 1000 | Both expiries need to trade |
| 6 | Volatility | IV30d Event | No | No earnings inside the front month |
| 7 | Calendar | FWDFCT3060 | min 0.16, max 1 | PA's calendar signal (16%); above 1 is usually a data quirk |
| 8 | Earnings | Earnings Date | None | No report in the window |

**Columns:** Price, Avg Option Volume, IV30d, IV60d, FWDFCT3060, FWDFCT3090, IV3060 Slope
**Sort:** FWDFCT3060, **highest to lowest**: the bigger the gap, the better the calendar.

**What to expect:** about 14 stocks (test day: CART, HLF, NXT, RPD, CL).
- **Too few:** lower FWDFCT3060 min to 0.10.
- **Too many:** raise it to 0.25; PA treats 0.41 as a strong signal.
- **Different expiries:** use the matching forward factor (FWDFCT3090 for 30/90, and so on).

**Setup:** New Scanner → name **Calendars - FF 30/60** → Create → Ok → Filters → Descriptive
(Price min 5; Asset Type Stock; Merger & Acquisition None; Sector: tick all except Healthcare)
→ Option (Avg Option Volume min 1000) → Volatility (IV30d Event No) → Calendar (FWDFCT3060 min
0.16, max 1) → Earnings (Earnings Date None) → Dismiss → Columns (tick the seven above) →
click the FWDFCT3060 header twice → Save → Overwrite Current.

**Before you trade:** check the forward factor on your actual fills; put equal capital in each;
close when the front expiry is 3–5 days away.

---

## Example 3: covered calls on tech

**Member:** "I do covered calls on companies I want to own. I like tech and AI."

**Scan name:** Covered Calls - Tech
**What it finds:** large tech and communication companies, no earnings or deals next month,
where IV isn't depressed and calls aren't cheap.
**Assumed:** 30–45 day calls, 25–40 delta.

| # | Section | Filter | Set to | Why |
|---|---|---|---|---|
| 1 | Descriptive | Price | min 15 | |
| 2 | Descriptive | Asset Type | Stock | |
| 3 | Descriptive | Market Cap | min 10000000 | $10 billion and up |
| 4 | Descriptive | Merger & Acquisition | None | |
| 5 | Descriptive | Sector | Technology, Communication Services | Tech and AI (Google and Meta are in Communication Services) |
| 6 | Option | Avg Option Volume | min 5000 | |
| 7 | Volatility | IV30d Event | No | |
| 8 | Volatility | NEIV30d Percentile | min 30 | Premium not at a low |
| 9 | Volatility | Skew Percentile | max 60 | Calls not unusually cheap next to puts |
| 10 | Earnings | Earnings Date | None | Don't sell a call across earnings |

**Columns:** Price, Price Chng 5d, Market Cap, Industry, IV30d, NEIV30d Percentile,
IV30d & NERV20d Ratio, Skew Percentile
**Sort:** IV30d & NERV20d Ratio, **highest to lowest**: richest premium first.

**What to expect:** about 10 (test day: GOOGL, GOOG, NFLX, SIRI, ACN).
- **Too few:** raise Skew Percentile max to 70, or lower NEIV30d Percentile min to 20.
- GOOGL and GOOG are the same company. Microsoft, Meta and AMD are left out by the merger
  filter; untick None to include them.

**Setup:** as in Example 1, with these filters, columns and sort.

**Before you trade:** only pick companies you'd hold anyway. Check the chain for your strike.

---

## Example 4: elevated IV

**Member:** "Show me companies with elevated IV."

**Ask first (one question):** "Do you want to include biotech and other small, news-driven
stocks? They dominate this list." If no answer, build it and point this out.

**Scan name:** Elevated IV - Stocks
**What it finds:** stocks whose IV, with earnings taken out, is in the top 10% of its own year.

| # | Section | Filter | Set to | Why |
|---|---|---|---|---|
| 1 | Descriptive | Price | min 5 | (min 10 to cut tiny names) |
| 2 | Descriptive | Asset Type | Stock | |
| 3 | Descriptive | Merger & Acquisition | None | |
| 4 | Option | Avg Option Volume | min 1000 | |
| 5 | Volatility | IV30d Event | No | So it's not just earnings |
| 6 | Volatility | NEIV30d Percentile | min 90 | Top 10% of its year |
| 7 | Earnings | Earnings Date | None | |

**Columns:** Price, Price Chng 5d, Sector, IV30d, NEIV30d Percentile, IV30d Chng 5d,
IV30d & NERV20d Ratio
**Sort:** NEIV30d Percentile, **highest to lowest**.

**What to expect:** about 23 (test day: BHC, DYN, SLS, PMT, TEM).
- **Reading it:** IV is usually high for a reason. If IV30d & NERV20d Ratio is above 1, options
  charge more than the stock is moving (a possible sale). Below 1, something big just happened;
  check whether IV30d Chng 5d is falling (fear draining) before selling.
- **Too many:** min 95. **Too few:** min 80.

---

## Example 5: where selling options has been most profitable

**Member:** "I want to sell options on the companies where that's been most profitable."

**Scan name:** Best Premium Sellers
**What it finds:** stocks where options have been overpriced on at least 70% of days over 4
years, by a meaningful margin, with no earnings or deals next month.

| # | Section | Filter | Set to | Why |
|---|---|---|---|---|
| 1 | Descriptive | Price | min 10 | |
| 2 | Descriptive | Asset Type | Stock | |
| 3 | Descriptive | Merger & Acquisition | None | |
| 4 | Option | Avg Option Volume | min 1000 | |
| 5 | Volatility | IV30d Event | No | |
| 6 | Variance Risk Premium | Avg NEVRP 4y | min 2 | Overpriced by 2+ vol points on average |
| 7 | Variance Risk Premium | NEVRP Win Rate 4y | min 70 | Overpriced on 70%+ of days |
| 8 | Earnings | Earnings Date | None | |

**Columns:** Price, Sector, IV30d, NEIV30d Percentile, IV30d & NERV20d Ratio, Avg NEVRP 4y,
NEVRP Win Rate 4y
**Sort:** NEVRP Win Rate 4y, **highest to lowest**.

**What to expect:** about 19 (test day: QGEN, STM, NRIX, ADMA, INFY).
- **History isn't today.** Prefer names whose IV30d & NERV20d Ratio is above 1 right now. One
  test-day name had a ratio of 0.29: a great history, but no cushion today.
- Many results are foreign companies traded in the US, and some are biotech. Say if you want
  either left out.
- **For ETFs instead:** use PA's ETF Premium default scanner (sorted by VRP Backtest Avg Return).
