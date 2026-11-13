# The terminal and its tickers

How the PA options terminal's Scanner behaves, and what the universe of tickers looks like.
Checked in the live terminal on 2026-11-12/13.

## The Scanner screen

Top bar, left to right:

| Control | What it does |
|---|---|
| Scanner dropdown | Pick a saved scan. "Custom Scanners" are the member's own; "Default Scanners" are PA's: ETF Premium, Earnings Premium, Earnings Look Ahead (1 week), Long Calendar Spreads |
| New Scanner | Opens "Create New Scanner": type a name, click Create, then Ok. Gives an empty scan: every ticker, no filters, no columns |
| Save | Two options: **Overwrite Current** (save this scan) and **Save As New** (save a copy under a new name) |
| Gear | "Scanner Settings": pick a scan, then the pencil to rename it or the bin to delete it |
| Refresh | Reload the data |
| Blue circle toggle | Show only favorited tickers |
| Search Ticker | Find one ticker |
| Filters: (n) | Open the filters; shows how many are set |
| Columns | Choose columns (has a search box) |
| 20 | Rows per page: 20, 50, 100, 150 |

The page header shows "Last Updated" with a time. The match count shows under "Ticker" in the
table header. Data updates during the day; open interest updates once a day.

## Filters

- Grouped in sections, in this order: Descriptive, Option, Volatility, Variance Risk Premium,
  Calendar, Earnings, Rating. Click a section to open it.
- Number filters have a **min** and a **max** box: type and press Tab. Changes apply at once.
- List filters (Asset Type, Sector, Earnings Date…) open a list to tick; it has a search box,
  which is the easiest way to find "None".
- "Clear All Filters" resets everything; "Dismiss" closes the panel.
- Filters combine with AND. Ticking several options in one list means any of them.
- Tickers with no data ("-") drop out as soon as a filter is set on that column.

**Typing values**
- Labeled **(percent)**: decimals. 0.05 = 5%; forward factor 0.16 = 16%; earnings return 1 = 100%.
- Labeled **(pts)** or unlabeled: as shown in the table. Win rate 60 = 60%; IV 40 = 40.
- **Market Cap: thousands of dollars**, despite the "(millions)" label. $10B = 10000000. The
  Market Cap column also displays values 1,000× too large (Apple shows "5.21P"): compare sizes
  relative to each other.
- **Market Type** labels are wrong (almost everything is "Mega"). Don't use it.
- Earnings Date options: Today BMO, Today AMC, Tomorrow BMO, Tomorrow AMC, This Week (the next
  7 days, today included), This Month, None. BMO = before market open, AMC = after market close.

**Retired filters** still shown but no longer used by PA (don't use them): FV30d,
IV30d & FV30d Ratio, IV30FV30 Percentile, Forecast Move 1d, Premium Rating, Calendar Rating.

## Columns and sorting

- The Columns dropdown lists every filter plus two buttons: **VRP Report** and
  **Earnings Report** (open a full analysis for the ticker). Ticker and name always show.
- The table arranges columns in its own order, not the order they were ticked.
- Click a column header once to sort lowest to highest; click again for highest to lowest.
- A saved scan keeps its filters, columns and sort.

## Scanning chosen tickers only

1. Click the blue circle beside each ticker you want (this favorites it).
2. Click the blue circle toggle in the top bar.
3. The scan now shows only favorites, with its filters still applied.

## The default scanners

| Scanner | Filters | Sort |
|---|---|---|
| ETF Premium | Asset Type ETF · Avg Option Volume min 5000 · IV30d Percentile max 95 · Avg VRP 4y min 0 · VRP Backtest Avg Return min 0 | VRP Backtest Avg Return, highest to lowest |
| Earnings Premium | Asset Type Stock · Earnings Date Today AMC + Tomorrow BMO | Earnings Short Straddle Return, highest to lowest |
| Earnings Look Ahead (1 week) | Avg Option Volume min 1000 · Earnings Date Today AMC, Tomorrow BMO, Tomorrow AMC, This Week · Earnings Confirmed Yes | By date |
| Long Calendar Spreads | Price min 5 · M&A None · every Sector except Healthcare · Avg Option Volume min 1000 · IV30d Event No · Earnings Date None · FWDFCT3060 min 0.16 | FWDFCT3060, highest to lowest |

Members can load a default, change it, and Save As New.

## The universe of tickers

- **About 2,650 tickers:** 2,263 stocks, 381 ETFs, 4 indexes (SPX, NDX, DJX, VIX).
- **Most are thin.** The middle ticker trades about 550 option contracts a day. 1,056 trade
  1,000+; 500 trade 5,000+; 240 trade 20,000+.
- **Many cheap stocks:** 626 under $10.
- **Company sizes** (stocks): 68 above $200B · 697 from $10B to $200B · 647 from $2B to $10B ·
  550 from $300M to $2B · 301 below $300M.
- **About 270 tickers have no IV data** and vanish once any IV filter is set.
- **Healthcare is the biggest sector** (416), half of it biotech.
- **Merger flag:** 703 tickers are tied to a deal, including buyers like Microsoft and Amazon.
- **VRP Backtest numbers exist for ETFs only.** Setting those filters removes every stock.

**Stocks and ETFs differ.** The middle ETF has IV30d 28 and options overpriced on 75% of days
over 4 years; the middle stock has IV30d 47 and 57%. Nine in ten ETFs have a positive 4-year
VRP; for stocks it's close to a coin flip.

**How fast scans shrink** (one filter added at a time, selling premium on stocks):
2,263 stocks → 920 with volume 1,000+ → 283 after no earnings, no deals and price 10+ →
30 with IV percentile 70+ → 5 with an IV/RV ratio of 1.1+. Cleanup removes about 9 in 10;
each signal after that cuts by 5 to 10 times.
