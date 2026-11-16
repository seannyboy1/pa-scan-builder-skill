# PA Scan Builder

Turn an options trading idea into a ready-to-build scan for the
[Predicting Alpha](https://predictingalpha.com) options terminal.

Tell your AI assistant what you trade, for example:

- "I run the wheel on big tech with a $20k account."
- "I trade calendar spreads and diagonals."
- "Show me stocks with elevated IV, no biotech."
- "Earnings plays this week where the market is overpricing the move."

It answers with a short report, right in the chat:

- **a name** for the scan and one line on what it finds
- **the filters** to set and exactly what to type, in the order they appear in the terminal
- **the columns** to show and **how to sort** them (highest to lowest, or lowest to highest)
- **roughly how many tickers** to expect, and what to change if you get too many or too few

Ask for click-by-click setup steps or checks before you trade if you want them.

You build the scan yourself in the terminal's Scanner; the assistant tells you how.

## How to use it

### With ChatGPT, Gemini or any assistant

1. Download [`scan-builder.md`](scan-builder.md).
2. Upload it to a new chat (or paste it in).
3. Describe the trade you want to scan for.

The file is about 155 KB. Use a current model with a large context window.

### With Claude (as a skill)

Add the [`pa-scan-builder`](pa-scan-builder) folder as a skill:

- **Claude Code:** copy the folder into `~/.claude/skills/`.
- **Claude apps:** zip the folder and upload it as a custom skill in Claude's settings.

Then just describe your trade. Claude loads the skill when it's relevant.

## What's inside

| File | What it holds |
|---|---|
| `scan-builder.md` | Everything in one file, for any assistant |
| `pa-scan-builder/SKILL.md` | The step-by-step method and the answer format |
| `pa-scan-builder/references/strategies.md` | PA's strategies as ready-made scans |
| `pa-scan-builder/references/reading-the-data.md` | How the terminal's data fits together |
| `pa-scan-builder/references/filters.md` | All 135 filters: what they mean, what to type, suggested values |
| `pa-scan-builder/references/terminal.md` | How the terminal behaves, and the tickers in it |
| `pa-scan-builder/references/examples.md` | Five complete worked answers |
| `data/scanner-filters.csv` | The full filter table as a spreadsheet |

## Good to know

- Ticker counts in the files are from November 2026. Markets move them every day: they show
  scale, not a promise.
- The scanner finds candidates. It can't see strikes, spreads or the news. You decide the trade.
