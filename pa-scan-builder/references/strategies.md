# PA strategies as scans

Each strategy below is a starting point: the idea, who it suits, the picture the scan looks
for, the filters in terminal order, the columns and the sort. Adjust to what the member said.

The defaults from SKILL.md step 3 are already applied (Asset Type = Stock unless the strategy
is about ETFs, Merger & Acquisition = None, earnings decided). "Today" is how many tickers the
scan returned on 2026-11-13 and the first few names, to show scale only. Counts change daily:
use the too-long / too-short advice in SKILL.md step 4.

Where a strategy says **"no earnings"** it means two filters: IV30d Event = No (Volatility)
and Earnings Date = None (Earnings). **"Not Healthcare"** means ticking every Sector except
Healthcare, including "None".

---

## Selling premium

### Expensive option premiums ("Theta Gang")
- **Idea:** sell options that charge more than the stock is likely to move. No view on direction.
- **Trades:** short straddle, iron condor, short strangle, bull put spread, short put, cash-secured put. 14–30 days.
- **Suits:** $2,500+, medium risk, intermediate.
- **Picture:** a liquid stock, no earnings or deal in the way, enough IV to be worth selling,
  options priced above what the stock is delivering, and a history of options being overpriced.
- **Filters:** Price min 10 · Asset Type Stock · Merger & Acquisition None · Sector not Healthcare ·
  Avg Option Volume min 1000 · IV30d Event No · IV30d & NERV20d Ratio min 1.0 · IV30d min 20 ·
  Avg NEVRP 4y min 0 · Earnings Date None
- **Columns:** Price, Price Chng 1d, Implied Move 1d, IV30d, IV30d & NERV20d Ratio, NEIV30d Percentile, Avg NEVRP 4y
- **Sort:** IV30d & NERV20d Ratio, highest to lowest: the bigger the cushion between what options charge and what the stock does, the better.
- **Today:** 11 (HLF, NKE, CLBT, LIN, YOU). In calmer markets raise the ratio to 1.1 or 1.2.
- **Before trading:** why are options priced this way? Who is on the other side? Any news coming?
- **Managing:** close if the cushion disappears, the stock reaches the short strikes, or expiry nears.

### Iron condors on calm stocks
- **Idea:** sell premium on stocks that don't move much day to day, so the wings are less likely to be hit.
- **Picture:** calm (small expected daily move), liquid, no earnings or deals, and options
  overpriced over time. Calm is the main signal; the IV/RV cushion is a column to check.
- **Filters:** Price min 10 · Asset Type Stock · Merger & Acquisition None · Sector not Healthcare ·
  (Weekly Contract Yes for weekly condors) · Avg Option Volume min 5000 · IV30d Event No ·
  Implied Move 1d max 3 · Avg NEVRP 4y min 0 · Earnings Date None
- **Columns:** Price, Implied Move 1d, IV10d, IV30d, IV30d & NERV20d Ratio, NEIV30d Percentile, Avg NEVRP 4y, NEVRP Win Rate 4y
- **Sort:** NEVRP Win Rate 4y, highest to lowest (steadiest sellers first). Prefer names whose IV30d & NERV20d Ratio is above 1 today.
- **Today:** 15 with weeklies (VALE, ASML, NKE, FCX, SIRI). Adding IV30d & NERV20d Ratio min 1.0 left only 2 on the test day; min 0.9 left 9.
- **Short strikes:** Implied Move 1d × 2.2 is roughly a one-week move; × 4.6 roughly a month.

### Inflated IV that should fall ("Vega Gang")
- **Idea:** IV itself is too high and will come back down. Trade the level of IV over months.
- **Trades:** short 40-delta strangle, 60–365 days. $7,000+, high skill.
- **Filters:** Price min 10 · Asset Type Stock · Merger & Acquisition None · Sector not Healthcare ·
  Avg Option Volume min 2000 · IV30d Event No · IV90d Percentile min 70 · IV90d min 20 · Earnings Date None
- **Columns:** Price, IV90d, IV180d, IV90d Percentile, IV90d Chng 5d, Implied Move 1d
- **Sort:** IV90d Percentile, highest to lowest.
- **Today:** 14 (CECO, LBRT, MAT, NUE, VLO).
- **Before trading:** has the company changed in a way that makes higher IV the new normal?

### Distressed volatility (basket)
- **Idea:** sell a small amount of premium on many of the most extreme names. The basket is
  the protection: no single ticker should matter. $10,000+, expert, high risk.
- **Picture:** IV high for the stock at every time frame at once.
- **Filters:** Price min 5 · Asset Type Stock · Merger & Acquisition None · Sector not Healthcare ·
  Avg Option Volume min 1000 · IV10d, IV20d, IV30d, IV60d and IV90d Percentile each min 70 · Earnings Date None
- **Columns:** Price, Price Chng 1d, Price Chng 5d, Implied Move 1d, IV30d, IV30d Chng 1d
- **Sort:** Implied Move 1d, highest to lowest.
- **Today:** 22 (TSAT, CECO, STRL, ONTO, MNRO). A list over 50 is fine here: it's a basket at small size.
- **Managing:** size each trade so losing 100% of the premium is acceptable; that's also the stop.

### ETF premium (PA's "ETF Premium" default scanner)
- **Idea:** sell overpriced insurance on ETFs, where the seller's edge is most dependable.
- **Trades:** short straddle, iron condor, short put, bull put spread. $5,000+.
- **Filters:** Asset Type ETF · Avg Option Volume min 5000 · IV30d Percentile max 95 ·
  Avg VRP 4y min 0 · VRP Backtest Avg Return min 0
- **Columns:** Price, Price Chng 1d, Avg Option Volume, VRP Backtest Avg Return, VRP Backtest Max Loss, VRP Backtest Win Rate, VRP Report
- **Sort:** VRP Backtest Avg Return, highest to lowest.
- **Today:** 14 (DIA, XLF, IEF, LQD, TLT, IWM).
- **Note:** the IV percentile max of 95 keeps out ETFs in the middle of a blow-up. Tell the
  member to skip any leveraged or inverse fund that appears: on the test day UCO
  ("ProShares Ultra Bloomberg Crude", a 2x oil fund) made this list.

### Weekly ETF premium (hand-picked list)
- **Idea:** sell premium every week on the biggest ETFs.
- **Setup:** favorite the tickers (for example SPY, QQQ, IWM, DIA, GLD, TLT, USO: click the
  blue circle beside each), then click the circle toggle in the top bar. Optionally Weekly Contract Yes.
- **Columns:** Price, Price Chng 1d, Implied Move 1d, IV30d Percentile, IV30d & RV20d Ratio, VRP Backtest Avg Return
- **Sort:** IV30d & RV20d Ratio, highest to lowest (richest this week).

### Bullish short puts, cash-secured puts, put credit spreads
- **Idea:** bullish on the stock, but calls are too expensive to buy, so sell a put and collect the rich premium.
- **Trades:** short put 35–50 delta, cash-secured put, bull put spread. 30–45 days. $5,000+.
- **Picture:** IV high for the stock, and puts unusually expensive next to calls.
- **Filters:** Price min 10 · Asset Type Stock · Merger & Acquisition None · Avg Option Volume min 1000 ·
  IV30d Event No · NEIV30d Percentile min 50 · Skew min 1 · Skew Percentile min 60 · Earnings Date None
- **Columns:** Price, Price Chng 5d, IV30d, NEIV30d Percentile, IV30d & NERV20d Ratio, Skew Percentile, Sector
- **Sort:** NEIV30d Percentile, highest to lowest (or Skew Percentile, highest to lowest, for put spreads).
- **Today:** 43 (CAPR, CECO, LBRT, DLR, HESM). Add Market Cap min 10000000 for larger companies.
- **Before trading:** any event that could drop the stock hard? Would you be happy owning it?

### The wheel
- **Idea:** sell cash-secured puts; if assigned, own the shares and sell covered calls. Wants
  steady stocks where options are reliably overpriced.
- **Ask first:** account size and how many positions (sets the Price max).
- **Filters:** Price min 15 (max = capital per position ÷ 100, only if given) · Asset Type Stock ·
  Market Cap min 10000000 · Merger & Acquisition None · Avg Option Volume min 5000 ·
  IV30d Event No · Avg NEVRP 4y min 0 · NEVRP Win Rate 4y min 55 · Earnings Date None
- **Columns:** Price, Sector, IV30d, Implied Move 1d, IV30d & NERV20d Ratio, NEIV30d Percentile, Avg NEVRP 4y, NEVRP Win Rate 4y
- **Sort:** NEVRP Win Rate 4y, highest to lowest: steadiness first.
- **Today:** 20 without a price cap (STM, ASML, AKAM, NKE, FCX).
- **Tip:** prefer names whose IV30d & NERV20d Ratio is above 1 today.

### Covered calls
- **Idea:** own good companies and sell calls when call premium is rich. 25–40 delta, 30–45 days, rebalance monthly. $10,000+, beginner friendly.
- **Picture:** a large, liquid company the member would hold anyway, IV not depressed, calls
  not cheap next to puts.
- **Filters:** Price min 15 · Asset Type Stock · Market Cap min 10000000 · Merger & Acquisition None ·
  (Sector, if they have a preference) · Avg Option Volume min 5000 · IV30d Event No ·
  NEIV30d Percentile min 30 · Skew Percentile max 60 · Earnings Date None
- **Columns:** Price, Price Chng 5d, Market Cap, Industry, IV30d, NEIV30d Percentile, IV30d & NERV20d Ratio, Skew Percentile
- **Sort:** IV30d & NERV20d Ratio, highest to lowest (richest premium), or Market Cap, highest to lowest (biggest companies first).
- **Today:** 31 across all sectors (NKE, CPNG, GOOGL, SCHW, NFLX); 10 for Technology + Communication Services.
- **If they already own the stocks:** favorite those tickers and sort the same way.
- **Note:** GOOGL and GOOG are the same company (two share classes).

### Backspread income (ETFs)
- **Idea:** sell overpriced crash insurance on ETFs: buy 1 50-delta put, sell 2 25-delta puts, 30–60 days, roll. $10,000+.
- **Filters:** Asset Type ETF · Avg Option Volume min 5000 · IV30d Percentile min 50 · Skew min 2 · Skew Percentile min 70
- **Columns:** Price, Skew, Skew Percentile, IV30d Percentile, Avg VRP 4y
- **Sort:** Skew Percentile, highest to lowest.
- **Today:** 4 (ASHR, EWT, SOXX, SPY). Loosen Skew Percentile to 60 if needed. Skip leveraged and inverse funds.

---

## Buying options

### Cheap options ("Gamma Scalp")
- **Idea:** buy options that undercharge for a stock that can move. Many small losers, some big winners.
- **Trades:** long straddle, long call, long put. 14–30 days. $1,000+.
- **Picture:** IV low for the stock and below what the stock is actually doing.
- **Filters:** Price min 5 · Asset Type Stock · Merger & Acquisition None · Avg Option Volume min 1000 ·
  IV30d Event No · NEIV30d Percentile max 20 · IV30d & NERV20d Ratio max 0.9 · Earnings Date None
- **Columns:** Price, Price Chng 1d, Price Chng 5d, Implied Move 1d, IV30d, RV20d, NEIV30d Percentile
- **Sort:** IV30d & NERV20d Ratio, lowest to highest (cheapest against movement first), or Price Chng 5d, highest to lowest, if momentum is the reason.
- **Today:** 32 (QGEN, CART, ITUB, IOVA, ULCC).
- **Ask:** what's the reason it should move? Add it (a trend, a catalyst).

---

## Skew trades (direction with an edge)

### Bullish call spreads and call flies
- **Idea:** after hype or good news, calls get priced as if the stock will explode. Stocks
  usually trend up instead, so a structure that pays on a steady rise is cheap.
- **Trades:** call debit spread; call fly (buy 1 at-the-money call, sell 3, buy 2 further out). 0–14 days. $1,000+. Size to about 3% of the account.
- **Filters:** Price min 5 · Asset Type Stock · Merger & Acquisition None · Weekly Contract Yes ·
  Avg Option Volume min 1000 · Skew max −0.1 (calls dearer than puts) · Skew Percentile max 50
- **Columns:** Price, Price Chng 1d, Price Chng 5d, Implied Move 1d, Skew, Skew Percentile, Earnings Date
- **Sort:** Price Chng 5d, highest to lowest.
- **Today:** 23 (RUM, CAR, EXE, TMDX, ROST). Without weeklies, 74.
- **Before trading:** why will it trend, not explode? Is call volume above normal?

### Bearish put spreads and put flies
- **Idea:** the mirror image: after bad news puts are priced for a crash, when a slow decline is more likely.
- **Trades:** put debit spread, put fly. 0–14 days.
- **Filters:** Price min 5 · Asset Type Stock · Merger & Acquisition None · Avg Option Volume min 1000 ·
  Skew min 3.5 · Skew Percentile min 50 (add Weekly Contract Yes for 0–14 days)
- **Columns:** as for call spreads.
- **Sort:** Price Chng 5d, lowest to highest.
- **Today:** 14 (CGEM, NTLA, BEKE, ARCC, EXC).

### Risk reversal
- **Idea:** after bad news, puts become irrationally expensive. Sell the 25-delta put and use
  it to pay for a 25-delta call. 30–60 days. $10,000+, high risk, high skill.
- **Filters:** Price min 10 · Asset Type Stock · Merger & Acquisition None · Avg Option Volume min 1000 ·
  IV30d Event No · Skew min 2 · Skew Percentile min 80 · Earnings Date None
- **Columns:** Price, Price Chng 5d, Skew, Skew Percentile, IV30d Percentile, Sector
- **Sort:** Skew Percentile, highest to lowest.
- **Today:** 15 (CXW, MGNI, NTLA, ARCC, CAMT).
- **Before trading:** what caused it, has it happened before, and is an event still ahead?

---

## Calendars and diagonals

### Long calendar spreads (PA's "Long Calendar Spreads" default scanner)
- **Idea:** the near expiry is overpriced next to the later one. Sell the near, buy the later.
  Run it as a portfolio: a calendar on each name over the signal. $1,000+, low risk, smooth results.
- **Diagonals:** the same scan works; pick strikes as usual.
- **Filters:** Price min 5 · Asset Type Stock · Merger & Acquisition None · Sector not Healthcare ·
  Avg Option Volume min 1000 · IV30d Event No · FWDFCT3060 min 0.16, max 1 · Earnings Date None
- **Columns:** Price, Avg Option Volume, IV30d, IV60d, FWDFCT3060, FWDFCT3090, IV3060 Slope
- **Sort:** FWDFCT3060, highest to lowest.
- **Today:** 14 (CART, HLF, NXT, RPD, CL).
- **Notes:** PA treats 0.16 (16%) as a buy and 0.41 as a strong buy. Asset Type Stock keeps
  out leveraged and inverse funds, which otherwise top this list. For other expiry pairs use
  the matching FWDFCT (2030, 3090, 6090, 90180).
- **Managing:** equal capital per trade; check the forward factor on your real fills; close
  when the front expiry is 3–5 days away.

---

## Earnings

### Selling earnings premium (PA's "Earnings Premium")
- **Idea:** the market often overprices the earnings move. Sell just before the close ahead of
  the report, close early the next day. 0–7 day options. $5,000+, high risk, expert.
- **Trades:** short straddle, short strangle, iron condor (wings about 2 standard deviations out).
- **Filters:** Price min 5 · Asset Type Stock · Merger & Acquisition None · Avg Option Volume min 1000 ·
  Earnings Date Today AMC + Tomorrow BMO (or This Week to plan ahead) · Earnings Confirmed Yes ·
  Earnings History min 8 · Earnings Short Straddle Return min 0 · IEM & AvgMove Ratio min 1.2
- **Columns:** Price, Earnings Date, IEM, Avg Move, Max Move, IV10d Crush, Earnings Short Straddle Return, Earnings Report
- **Sort:** Earnings Short Straddle Return, highest to lowest.
- **Today:** 11 for the coming week (HD, FUTU, XP, LOW, ROST). Tonight's window is often 0–10.
- **Before trading:** how likely is a real surprise? Check Max Move against the IEM.

### Buying earnings movement
- **Idea:** the reverse: stocks that keep moving more than priced on earnings.
- **Trades:** long straddle into the report.
- **Filters:** as above, but Earnings Short Straddle Return max −1 · IEM & AvgMove Ratio min 0.1, max 0.9
- **Sort:** Earnings Short Straddle Return, lowest to highest.
- **Today:** 4 for the coming week (TME, POWL, PDD, JMIA).

---

## Which strategy fits what the member said

| They trade or say | Start from | Adjust |
|---|---|---|
| The wheel, cash-secured puts | The wheel | Price max from account size |
| Covered calls | Covered calls | Sector if they say one; favorites if they own the stocks |
| Put credit spreads, bull put spreads | Bullish short puts | Sort by Skew Percentile |
| Call credit spreads, bear call spreads | Bearish put spreads' picture + rich calls | NEIV30d Percentile high, Skew Percentile low |
| Iron condors, strangles, straddles (selling) | Iron condors on calm stocks, or Expensive option premiums | Weekly Contract Yes for short ones |
| Butterflies | Call or put flies if directional; Iron condors if neutral | Weekly Contract Yes for 0–14 days |
| Debit spreads | Bullish or bearish spreads | |
| Buying calls, puts or straddles | Cheap options | Ask for the reason it should move |
| Calendars, diagonals | Long calendar spreads | Match the expiry pair |
| Earnings trades | Selling or buying earnings | Tonight or this week |
| ETF income | ETF premium or Weekly ETF premium | |
| "High IV", "elevated IV" | Stocks, no earnings, NEIV30d Percentile min 90 | Ask whether biotech is welcome; add Price min 10 |
| "Where selling options has been most profitable" | Stocks, no earnings, Avg NEVRP 4y min 2, NEVRP Win Rate 4y min 70 | Sort by win rate; show the ratio to check today |
