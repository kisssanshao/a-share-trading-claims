# Testing A-Share Trading Claims | AI-assisted research

**205 trading claims about China's A-share market were catalogued; 83 were tested with data, and none was validated.** The claims come from more than 100 short videos watched between June and October 2026, plus courses, forum posts, classic methods and my own ideas. This repository records how each claim was tested, what came out, and where the evidence falls short.

The detailed documents are in Chinese; this page summarizes them. 中文版：[README.md](README.md)

> Backtest results hold only for the data and assumptions used. They do not predict the future, are not personal trading profits, and are not investment advice.

![Verdicts for the 83 claims tested with data: validated 0, failed 55, inconclusive 21, still watching 5, set as a trading rule 1, benchmark 1](figures/verdicts-en.svg)

## Three findings

1. **Costs and fill constraints eat many signals.** Short-term reversal made money in all 8 settings before costs, but only 1 stayed positive after costs. A liquidity factor returned 17.95% a year with unconstrained fills, and only 2.89% with fill constraints.

   ![Annualized returns of 8 short-term reversal settings before and after costs: all positive before costs, only one positive after costs (+2.87%)](figures/cost-reversal-en.svg)

2. **Compare against random.** Timing by the number of limit-up and limit-down stocks cut the maximum drawdown from −50.03% to −24.06%, but it did not clear the 95th-percentile threshold of random timing with the same time in the market, so the test did not show that the improvement came from timing. Picking stocks at random from the research pool and changing only the random seed gave 5-year results anywhere from −6.11% to +144.78%.
3. **Remove biases before looking at returns.** An overnight limit-up strategy that picked stocks from the limit-up list known only after the close showed +3,847.5% a year in its backtest. Using only data visible before 14:45, with stricter fill rules, turned it into −96.5%. Several early strategies built their stock pools from today's index members, which adds survivorship bias; after review they were downgraded to "still watching".

## Seven selected tests

Each test's question, method, findings, limits and decision are in [01-selected-tests.md](01-selected-tests.md) (Chinese).

| Claim | How it was tested | Key result | Decision |
|---|---|---|---|
| Tail-session overnight, 7 rules | Written as 7 explicit conditions; at 14:30 only data available at that time; costs deducted; split into 4 half-years | −73.2% a year after costs, −67.2% before; lost money in all 4 half-years | Not adopted |
| Overnight limit-up | One version picked from the limit-up list known after the close; the other used only minute data before 14:45, with stricter fill rules | +3,847.5% → −96.5% a year | Not adopted |
| Short-term reversal | CSI 800 point-in-time members; fill constraints; 8 settings | All 8 profitable before costs (2.99% to 14.23% a year); only 1 positive after costs (2.87%) | Not adopted |
| Limit-up/limit-down breadth timing | Compared with staying fully invested, and with random timing with the same time in the market | Max drawdown −50.03% → −24.06%; Sharpe 0.979, below the random-timing 95th percentile of 0.983 | Not used as a timing signal |
| Supply-chain transmission | 5 sectors, 6 chains; unrelated industry pairs as controls | 0 of 6 chains passed; the 3 strongest correlations were 0.53–0.56, and unrelated industry pairs showed similar or higher correlations (0.52, 0.59) | Not used as a trading signal |
| Contract-liability growth | Data taken by announcement date; out-of-sample 2024–2025; 20 within-industry random shuffles | Top 20% by growth: +4.8% excess return; bottom 20%: +5.2%; random control: +4.6% | Not used for stock selection |
| Weekly 10 least-active stocks | 12 parameter sets; nominated on a development period, judged on a review period against 7 gates | 14.42% a year in the review period, but the statistical lower bound of excess return was −2.65 percentage points; failed 3 gates | Not adopted; idea kept for later |

## My role

I posed the questions to test, confirmed the rules and pass criteria, reviewed the results, and decided whether to continue or stop. All code was written by AI (Claude Code and Codex): one ran the tests, the other reviewed them independently, and when they disagreed I decided which version to adopt.

## Full counts

The full catalog has 205 rows; some rows merge several similar videos.

| How it was checked | Rows | Verdicts |
|---|---|---|
| Tested with data (backtests, factor statistics or descriptive statistics) | 83 | Failed 55, inconclusive 21, still watching 5, set as a trading rule 1, benchmark 1 |
| Compared with similar methods already tested | 21 | Not separately verified 18, inconclusive 3 |
| Not tested with data | 101 | Not tested 72 (could not be written as rules, no suitable data, plan not settled, or dropped), adopted as research practice 13, set as trading rules 6, not applicable to A-shares 7, still watching 3 |

Some of the 83 were only factor or descriptive statistics, not full backtests.

## Repository layout

```text
├── README.md                   Chinese overview
├── README_EN.md                this page
├── 01-selected-tests.md        7 selected tests: question, method, findings, limits, decision
├── 02-case-tail-overnight.md   case study: the full test of one claim
├── 03-methodology.md           method, verdict labels, data notes, glossary
├── 04-full-catalog.md          all 205 claims in 16 categories, plus two appendices
├── data/claims.csv             the catalog as a filterable table (Chinese)
├── figures/                    charts (Chinese and English versions)
├── CHANGELOG.md                change log
└── LICENSE                     CC BY 4.0
```

## Data and code

The data used, sample periods and known gaps are described in the "数据说明" (data notes) section of [03-methodology.md](03-methodology.md). Code and raw data are not published: the code lives in a personal research project that depends on local data and private settings and has not been packaged to run on its own; market data come from third parties and are not redistributed here.

## Notes

- Claim names keep their original labels; the rules are our interpretation and may not match the original author's intent. Video transcripts are not included.
- No personal accounts, positions or stock recommendations.
- Material as of October 2026.
- License: [CC BY 4.0](LICENSE). Please credit the source when sharing or adapting.
