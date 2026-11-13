# Reading the data

How the scanner's data fits together. Use it in step 2 to work out which data paints the
picture a member is after. Counts are from 2026-11-12 among about 1,050 liquid tickers
(Avg Option Volume 1,000+).

## The principle

**A metric describes a situation. It never gives a verdict.** The same reading can be a
warning for one trade and the opportunity for another. Very high IV after a shock looks
dangerous to someone selling premium on routine, and like opportunity to someone who sells
after a panic. So: understand the trade, describe the situation where it works, and turn each
part into a filter. Then tell the member the other way to read the same list: that's their risk.

## The five questions

Every filter answers one of these. A scan usually takes an answer from each, in order.

| # | Question | Role | Go-to filters |
|---|---|---|---|
| 1 | Can I trade it? | Cleanup | Asset Type, Avg Option Volume, Price, Market Cap, Weekly Contract |
| 2 | Is something distorting the numbers? | Cleanup | IV30d Event, Earnings Date, Merger & Acquisition, Sector (Healthcare) |
| 3 | What is this ticker's character over time? | Where to fish | Avg VRP 4y, VRP Win Rate 4y (NE versions for stocks), VRP Backtest Avg Return, Earnings Short Straddle Return |
| 4 | What situation is it in right now? | The main signal | IV percentiles, IV30d & NERV20d Ratio, IV changes, Skew Percentile, FWDFCT3060, IEM & AvgMove Ratio |
| 5 | What can go wrong? | Mostly columns | Implied Move 1d, RV, VRP Backtest Max Loss, Max Move |

## Earnings in or out

Settle this first on any stock scan: it decides which versions of the metrics make sense.

| | Earnings OUT (most scans) | Earnings IN (earnings trades) |
|---|---|---|
| Set | IV30d Event = No and Earnings Date = None | Earnings Date = window · Earnings Confirmed = Yes · Earnings History min 8 |
| Where IV stands | NEIV30d Percentile | Skip: it is high for every stock before earnings |
| The cushion | IV30d & NERV20d Ratio | IEM & AvgMove Ratio |
| Character | Avg NEVRP 4y, NEVRP Win Rate 4y | Earnings Short Straddle Return |
| What can go wrong | Implied Move 1d | Max Move, IV10d Crush |

"NE" means non-event: earnings taken out of the calculation. For stocks, prefer NE versions
whenever earnings are out. ETFs have no earnings: use the plain versions.

IV30d Event and Earnings Date are separate lists: hundreds of stocks have earnings priced in
with no date listed. That's why "no earnings" needs both filters.

## Four kinds of "expensive"

"Expensive options" can mean four different things:

| Expensive against... | Filter | Answers |
|---|---|---|
| its own past | IV30d Percentile (NEIV30d for stocks) | Is IV high for this ticker? |
| how much the stock moves | IV30d & NERV20d Ratio | Do options charge more than the stock is delivering? |
| its history | Avg VRP 4y, VRP Win Rate 4y | Have options here been overpriced year after year? |
| later expiries | FWDFCT3060 | Is the near month dearer than what follows? |

(For earnings: the priced move, IEM, against the stock's usual move, Avg Move.)

When they agree, the case is strong. When they disagree, the disagreement tells you something.

## Three dials and seven situations

Many premium ideas come down to three dials:
- **Where IV stands** (IV percentile): low under 30, middle 30–70, high over 70.
- **The cushion** (IV30d & NERV20d Ratio): above 1.1 options charge more than the stock is
  moving; below 0.9 the stock is outrunning its options.
- **Character** (Avg VRP 4y with VRP Win Rate 4y): a "payer" has positive VRP and a win rate
  over 60; an "outrunner" has negative VRP and a win rate under 50.

| Situation | How to find it | Seller's reading | Buyer's reading | Liquid tickers |
|---|---|---|---|---|
| **Steady premium** | percentile 30–70 · ratio min 1.05 · Avg VRP 4y min 1 · win rate min 60 | The bread-and-butter sale. No spike needed | Little to do | 49 |
| **Braced** | percentile min 70 · ratio min 1.2 | Fat premium, but ask what the market expects. With no event, the richest sale | Usually overpaying | 73 (23 with no event) |
| **Aftershock** | percentile min 80 · ratio max 0.9 | Something big just happened. Often a good moment to sell, as fear outlasts the move, if it's over | Cheap next to what the stock is doing, if the move continues | 48 |
| **Sleepy** | percentile max 30 · ratio min 1.1 | Small, dependable premium; suits covered calls | Cheap in dollars, but nothing is moving | 32 |
| **Coiled** | percentile max 20 · ratio max 0.9 | Little premium, no cushion | The classic buy: cheap options on a stock that is moving | 127 |
| **Waking up** | percentile 30–70 · ratio max 0.8 | A warning: no cushion | Early entry before IV catches up | 120 |
| **Outrunner** (a character, not a moment) | Avg VRP 4y max −1 · win rate max 50 | Avoid, or defined risk only | Hunting ground for long volatility | 214 |

**Is the aftershock over?** IV30d Chng 1d at or below 0 means fear is draining. Above +3%
means it's still building, and selling is catching a falling knife.

**What is "braced" waiting for?** If it's earnings, use the earnings logic. If it's a deal or
biotech news, the fear is probably deserved. If nothing is visible, it's either simply rich or
someone knows something: smaller size or defined risk.

**Cheap options need a reason to move.** Ask the member for theirs, and add it if the scanner
can see it (a trend, unusual volume, an earnings date coming).

## Signals move together

On 2026-11-12, after a choppy stretch, realized volatility was above implied for most tickers:
the middle IV/RV ratio was 0.85 and the middle IV30RV20 Percentile was 16. In calm markets the
same thresholds let through several times as many names. So a threshold isn't "strict" by
itself: give the setting and let the list size guide the member.

## Match the time frame

| Trade length | Use the IV, percentile and change for | Calendar pair |
|---|---|---|
| 1–2 weeks, weeklies | 10d (and Weekly Contract Yes) | 2030 |
| 2–4 weeks | 20d | 2030 or 3060 |
| 30–45 days (default) | 30d | 3060 |
| 2–3 months | 60d or 90d | 3090 or 6090 |
| 4 months and more | 90d, 180d, 365d | 90180 |

If the member gives no time frame, use 30d and say so. The IV-against-realized ratios exist
only for 30-day IV, so for weeklies sort by the 30-day ratio and show IV10d as a column.

## Common traps

- **High IV percentile on a tiny IV.** Bond funds can rank high at an IV under 10. Show IV30d
  beside the percentile.
- **History-only scans ignore today.** A stock with great VRP history can have IV at the 3rd
  percentile right now. Tell the member to prefer names whose IV30d & NERV20d Ratio is above 1.
- **Biotech dominates high-IV lists.** Drug-trial news causes huge jumps that aren't earnings.
  Ask whether they want those; if not, leave out Healthcare.
- **Foreign companies trading in the US** (Sony, SAP, HSBC, BHP) often top VRP-history scans.
  Mention it; some members want US names only.
- **Two share classes** (GOOGL and GOOG) both appear. Same company.
