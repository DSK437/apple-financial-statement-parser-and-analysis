# apple-financial-statement-parser-and-analysis
Python tool that pulls Apple's financials from the SEC EDGAR API, builds income statement, balance sheet and cash flow tables, calculates key ratios, and flags fundamental red and green signals.
# Financial Statement Parser & Fundamental Analysis (Apple Inc.)

A Python notebook that pulls a company's annual financial data directly from the
SEC EDGAR XBRL API, structures it into clean financial statements, calculates
key ratios, and runs a rules-based check for red and green flags.

Apple (CIK 0000320193) is used as the example company.

## What it does

1. **Fetches** annual (10-K) data from the SEC EDGAR `companyfacts` API
2. **Parses** it into three statements: income statement, balance sheet and cash flow
3. **Calculates** 15+ metrics: growth, margins, ROE/ROA, current ratio, leverage,
   free cash flow, cash conversion, share count change and more
4. **Flags** red and green signals per year (for example liabilities above assets,
   operating loss, current ratio below 1, revenue decline, profit not backed by cash,
   strong margins, shrinking share count)
5. **Exports** results to CSV and PNG charts

## Example output (Apple, FY2025)

![Margin trends](apple_margin_trends.png)

| Signal type | Examples flagged |
|---|---|
| Green | Revenue growth 6.4%, gross margin 46.9%, FCF margin 23.7%, share count down 2.6% |
| Red | Liabilities 3.9x equity, current ratio 0.89 |

## Tech stack

Python, pandas, requests, matplotlib. Built and run in a Kaggle notebook.

## How to run

1. Open `your-notebook-name.ipynb` in Kaggle or Jupyter (internet access required)
2. In the setup cell, replace the `User-Agent` in `HEADERS` with your own name and email
   (the SEC requires this)
3. Run all cells top to bottom

To analyse another company, change the `CIK` value in the setup cell.

## Output files

| File | Contents |
|---|---|
| `apple_income_statement.csv` | Annual income statement |
| `apple_balance_sheet.csv` | Annual balance sheet |
| `apple_cash_flow.csv` | Annual cash flow items |
| `apple_ratios.csv` | Growth, margin and return ratios |
| `apple_metrics.csv` | Full metrics used by the flag rules |
| `apple_flags.csv` | Red and green flags by year |

## Limitations

- Flags are prompts to investigate, not verdicts. Apple triggers a few red flags for
  legitimate reasons: share buybacks shrink equity (inflating ROE and leverage
  ratios), and its marketable securities are not counted in cash, which understates
  liquidity.
- Thresholds are common rules of thumb, not investment advice.
- XBRL tag names vary between companies, so some line items may need adjusting
  when analysing a different company.

## Data source

[SEC EDGAR XBRL API](https://www.sec.gov/edgar/sec-api-documentation)

## Disclaimer

For educational and portfolio purposes only. Not investment advice.
