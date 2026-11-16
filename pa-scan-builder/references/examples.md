# Worked examples

Five complete answers, built and tested in the live terminal on 2026-11-13. Each answer is the
whole reply, written in the chat. Match this format exactly. Ticker counts and names are from
that day and will differ when the member builds it.

---

## Example 1: the wheel

**Member:** "I want to run the wheel on solid stocks that won't blow up. 30 to 45 days."

**Before answering:** the member gave no account size, so don't cap the price. Either ask
("How much would you put into one stock?") or build without a cap and say how to add one.
This answer builds without it.

```markdown
## Wheel - Large Cap

Large, liquid stocks with no earnings or deals in the next month, where options have a steady history of being overpriced.

`Stocks only` · `$10B+ companies` · `No earnings` · `30–45 days` · `No price cap`

### Filters (9)

| Section | Filter | Set to | Why |
|---|---|---|---|
| Descriptive | Price | `min 15` | Skip cheap stocks |
| Descriptive | Asset Type | `Stock` | No leveraged funds |
| Descriptive | Market Cap | `min 10000000` | $10B+ (box takes thousands) |
| Descriptive | Merger & Acquisition | `None` | No deal in progress |
| Option | Avg Option Volume | `min 5000` | Easy fills |
| Volatility | IV30d Event | `No` | No earnings priced in |
| Variance Risk Premium | Avg NEVRP 4y | `min 0` | Overpriced on average |
| Variance Risk Premium | NEVRP Win Rate 4y | `min 55` | Overpriced on most days |
| Earnings | Earnings Date | `None` | No report next month |

### Columns (8)

Price · Sector · IV30d · Implied Move 1d · IV30d & NERV20d Ratio · NEIV30d Percentile · Avg NEVRP 4y · **NEVRP Win Rate 4y ↓**

**Sort:** NEVRP Win Rate 4y, highest to lowest (click the header twice).

### Expect

| Count | Over 50 | Under 5 |
|---|---|---|
| ~20 (changes daily) | NEVRP Win Rate 4y `min 60` | Market Cap `min 2000000`, then Avg Option Volume `min 1000` |

**Best picks:** IV30d & NERV20d Ratio above 1: options charge more than the stock is moving now.

**Note:** To fit your account, set Price max to your money per stock ÷ 100 ($5,000 → `max 50`). Microsoft and other buyers drop out with the merger filter; untick None to get them.
```

On the test day: STM, ASML, AKAM, NKE, FCX.

---

## Example 2: calendars and diagonals

**Member:** "I trade calendar spreads and diagonals. What should I look at?"

```markdown
## Calendars - FF 30/60

Stocks where the near-month options are priced well above the following month, with no earnings or deals to explain it.

`Stocks only` · `No earnings` · `No healthcare` · `Sell ~30 days, buy ~60`

### Filters (8)

| Section | Filter | Set to | Why |
|---|---|---|---|
| Descriptive | Price | `min 5` | Skip cheap stocks |
| Descriptive | Asset Type | `Stock` | Leveraged funds top it otherwise |
| Descriptive | Merger & Acquisition | `None` | Deals distort the months |
| Descriptive | Sector | `every sector except Healthcare (tick the other 11, including None)` | Biotech news is jumpy |
| Option | Avg Option Volume | `min 1000` | Both months must trade |
| Volatility | IV30d Event | `No` | No earnings in front month |
| Calendar | FWDFCT3060 | `min 0.16, max 1` | PA's signal; above 1 is a quirk |
| Earnings | Earnings Date | `None` | No report in the window |

### Columns (7)

Price · Avg Option Volume · IV30d · IV60d · FWDFCT3090 · IV3060 Slope · **FWDFCT3060 ↓**

**Sort:** FWDFCT3060, highest to lowest (click the header twice).

### Expect

| Count | Over 50 | Under 5 |
|---|---|---|
| ~14 (changes daily) | FWDFCT3060 `min 0.25` | FWDFCT3060 `min 0.10` |

**Best picks:** FWDFCT3060 above 0.41, PA's strong signal.

**Note:** For other expiries, use the matching forward factor (FWDFCT3090 for 30/90, and so on).
```

On the test day: CART, HLF, NXT, RPD, CL.

---

## Example 3: covered calls on tech

**Member:** "I do covered calls on companies I want to own. I like tech and AI."

```markdown
## Covered Calls - Tech

Large tech and communication companies with no earnings or deals next month, where IV isn't depressed and calls aren't cheap.

`Stocks only` · `$10B+ companies` · `Tech and AI` · `No earnings` · `30–45 day calls`

### Filters (10)

| Section | Filter | Set to | Why |
|---|---|---|---|
| Descriptive | Price | `min 15` | Skip cheap stocks |
| Descriptive | Asset Type | `Stock` | Companies only |
| Descriptive | Market Cap | `min 10000000` | $10B+ (box takes thousands) |
| Descriptive | Merger & Acquisition | `None` | No deal in progress |
| Descriptive | Sector | `Technology, Communication Services` | Google and Meta are Communication |
| Option | Avg Option Volume | `min 5000` | Easy fills |
| Volatility | IV30d Event | `No` | No earnings priced in |
| Volatility | NEIV30d Percentile | `min 30` | Premium not at a low |
| Volatility | Skew Percentile | `max 60` | Calls not unusually cheap |
| Earnings | Earnings Date | `None` | Don't sell across earnings |

### Columns (8)

Price · Price Chng 5d · Market Cap · Industry · IV30d · NEIV30d Percentile · Skew Percentile · **IV30d & NERV20d Ratio ↓**

**Sort:** IV30d & NERV20d Ratio, highest to lowest (click the header twice).

### Expect

| Count | Over 50 | Under 5 |
|---|---|---|
| ~10 (changes daily) | NEIV30d Percentile `min 50` | Skew Percentile `max 70`, then NEIV30d Percentile `min 20` |

**Note:** GOOGL and GOOG are the same company. Microsoft, Meta and AMD drop out with the merger filter; untick None to get them.
```

On the test day: GOOGL, GOOG, NFLX, SIRI, ACN.

---

## Example 4: elevated IV

**Member:** "Show me companies with elevated IV."

**Before answering:** ask one question: "Do you want to include biotech and other small,
news-driven stocks? They dominate this list." If there's no answer, build it and say so in a tag.

```markdown
## Elevated IV - Stocks

Stocks whose IV, with earnings taken out, is in the top 10% of its own year.

`Stocks only` · `No earnings` · `Biotech included`

### Filters (7)

| Section | Filter | Set to | Why |
|---|---|---|---|
| Descriptive | Price | `min 5` | Skip the cheapest |
| Descriptive | Asset Type | `Stock` | Companies only |
| Descriptive | Merger & Acquisition | `None` | No deal in progress |
| Option | Avg Option Volume | `min 1000` | Tradeable options |
| Volatility | IV30d Event | `No` | So it's not just earnings |
| Volatility | NEIV30d Percentile | `min 90` | Top 10% of its year |
| Earnings | Earnings Date | `None` | No report next month |

### Columns (7)

Price · Price Chng 5d · Sector · IV30d · IV30d Chng 5d · IV30d & NERV20d Ratio · **NEIV30d Percentile ↓**

**Sort:** NEIV30d Percentile, highest to lowest (click the header twice).

### Expect

| Count | Over 50 | Under 5 |
|---|---|---|
| ~23 (changes daily) | NEIV30d Percentile `min 95` | NEIV30d Percentile `min 80` |

**Best picks:** IV30d & NERV20d Ratio above 1 is a possible sale. Below 1, something just happened: sell only if IV30d Chng 5d is falling.

**Note:** IV is usually high for a reason: check the news. Set Price `min 10` to cut tiny names.
```

On the test day: BHC, DYN, SLS, PMT, TEM.

---

## Example 5: where selling options has been most profitable

**Member:** "I want to sell options on the companies where that's been most profitable."

```markdown
## Best Premium Sellers

Stocks where options have been overpriced on at least 70% of days over 4 years, by a real margin, with no earnings or deals next month.

`Stocks only` · `No earnings` · `Any company size`

### Filters (8)

| Section | Filter | Set to | Why |
|---|---|---|---|
| Descriptive | Price | `min 10` | Skip cheap stocks |
| Descriptive | Asset Type | `Stock` | Companies only |
| Descriptive | Merger & Acquisition | `None` | No deal in progress |
| Option | Avg Option Volume | `min 1000` | Tradeable options |
| Volatility | IV30d Event | `No` | No earnings priced in |
| Variance Risk Premium | Avg NEVRP 4y | `min 2` | Overpriced by 2+ points |
| Variance Risk Premium | NEVRP Win Rate 4y | `min 70` | Overpriced on 70%+ of days |
| Earnings | Earnings Date | `None` | No report next month |

### Columns (7)

Price · Sector · IV30d · NEIV30d Percentile · IV30d & NERV20d Ratio · Avg NEVRP 4y · **NEVRP Win Rate 4y ↓**

**Sort:** NEVRP Win Rate 4y, highest to lowest (click the header twice).

### Expect

| Count | Over 50 | Under 5 |
|---|---|---|
| ~19 (changes daily) | NEVRP Win Rate 4y `min 80` | NEVRP Win Rate 4y `min 60` |

**Best picks:** IV30d & NERV20d Ratio above 1. History isn't today: one test-day name had a ratio of 0.29.

**Note:** Many results are foreign companies traded in the US, and some are biotech; say if you want either left out. For ETFs, use PA's ETF Premium default scanner.
```

On the test day: QGEN, STM, NRIX, ADMA, INFY.
