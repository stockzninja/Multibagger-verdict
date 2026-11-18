# Multibagger Verdict

**An evidence-first Agent Skill for assessing whether a listed stock has a credible path to 3× returns over 3–7 years.**

Give your AI agent an NSE/BSE/NYSE/Nasdaq ticker. Instead of a generic stock summary, get a structured, source-backed long-term investing thesis, a score out of 100, valuation scenarios and a clear verdict:

**POTENTIAL MULTIBAGGER · WATCHLIST · UNLIKELY · INSUFFICIENT EVIDENCE**

> This is a reusable *research workflow*, not a trading bot, live stock screener, financial-data API, or machine-learned prediction model. Its verdict is an analytical classification, **not** a forecast, probability or recommendation to buy or sell.

## Why this exists

Finding future multibaggers is different from screening for cheap stocks or businesses with already-excellent ratios. A company's future share-price return depends on **how much its underlying economics can improve and how much an investor pays for that potential today**.

This skill combines the *publicly described* investment philosophies associated with Vijay Kedia (SMILE), Ashish Kacholia, Mukul Agrawal and Sunil Singhania (MEETS), alongside global case-study themes from businesses such as Monster Beverage, Amazon, Nvidia, Constellation Software and Copart. It translates those ideas into a repeatable research checklist and decision rubric.

It **does not claim** to know any investor's proprietary entry criteria. The numerical thresholds and scores are research heuristics, not empirically proven screening signals.

## Example usage

After installing the skill into a compatible AI coding or agent environment:

```text
$multibagger-verdict NSE:KMEW
```

Or ask naturally:

```text
Analyze NSE:MENONBE with the Multibagger Verdict skill. Use a 5–7-year horizon.
```

```text
Use Multibagger Verdict on NASDAQ:NVDA. Show the valuation math and downside case.
```

```text
Evaluate BSE:XXXX as of March 2021 using only data available on that date.
```

*The tickers are usage examples, not endorsements or example verdicts. Replace `XXXX` with a valid ticker.*

### Example response format

```text
VERDICT: WATCHLIST — NOT YET
Stock: EXAMPLE (fictional) | Horizon: 5–7 years
Score: 69/100 | Confidence: Medium | As of: YYYY-MM-DD

Why: The business has an expanding market and improving margins,
but the current valuation assumes most of the forecast growth.

Upside math (illustrative only):
  Bear: 0.6× | Base: 1.5× | Bull: 2.8×

3 reasons: Market runway; operating leverage; improving ROIC.
3 risks: Customer concentration; expensive valuation; dilution.
Next milestone: Confirm cash conversion and new capacity utilization.
Sources: Links to dated exchange filings and financial statements.
```

The sample above is entirely hypothetical. Actual outputs must use current, attributable evidence and show assumptions rather than invent figures.

## How it works

1. **Verify the security and evidence.** Confirm exchange, ticker, price date, market cap and reporting currency. Retrieve dated exchange/SEC filings, annual reports, quarterly results, presentations and applicable credit reports.
2. **Identify the business archetype.** Emerging growth, compounder, capex/earnings inflection, cyclical recovery, acquisition compounder or a financial-sector business. Different economics require different yardsticks.
3. **Score seven dimensions (100 total).** Use the rubric below; do not award points to unverified claims.
4. **Model 3–7-year shareholder outcomes.** Build bear/base/bull scenarios tied to earnings or cash flow, exit valuation, leverage and share-count dilution; don't use a speculative P/E rerating as the entire thesis.
5. **Apply quality and risk vetoes.** Check cash conversion, receivables, taxes, auditor notes, related-party transactions, pledging, dilution, liquidity and solvency.
6. **Give the verdict first.** State the central reasons, risks, missing evidence and next confirmation milestone.

### Scoring pillars

| Pillar | Points |
| --- | ---: |
| Market opportunity & scalable unit economics | 20 |
| Revenue growth, earnings quality & inflection | 20 |
| Competitive advantage, management & governance | 15 |
| Capital efficiency & reinvestment opportunities | 15 |
| Cash generation & balance-sheet resilience | 10 |
| Entry valuation & credible shareholder payoff | 15 |
| Catalysts & measurable confirmation | 5 |
| **Total** | **100** |

**Decision rules:** A score of **75+** is *necessary but not sufficient* for `POTENTIAL MULTIBAGGER`. The skill also requires adequate primary-source evidence, no material unresolved red flags, a credible bull case of at least 3× and a reasonable base case of at least 1.7×. A 55–74 score usually means `WATCHLIST`; below 55 usually means `UNLIKELY`. Serious risks or unreliable evidence override numerical scores. **10× is a separate stretch scenario**, never the baseline.

See [`SKILL.md`](SKILL.md) for the full process and [`references/rubric.md`](references/rubric.md) for scoring anchors, exceptions and evidence requirements.

## Installation

A skill is a folder containing `SKILL.md` with YAML frontmatter plus optional references. This repository is intentionally a **single-skill repository** with `SKILL.md` at its root.

**Via the community Skills CLI (if supported by your agent):**

```bash
npx skills add buildcrafts/multibagger-verdict
```

**Codex, manual installation:** clone/download this repo, then copy its contents into `~/.agents/skills/multibagger-verdict/` for user-wide use, or `.agents/skills/multibagger-verdict/` for a single project.

**Claude Code, manual installation:** place the skill folder in `~/.claude/skills/multibagger-verdict/` or `.claude/skills/multibagger-verdict/`.

**Other agents:** follow that product's [Agent Skills](https://agentskills.io) installation path and confirm it supports `SKILL.md`. Invocation syntax and network/filing retrieval access depend on the host environment.

**Important:** Publishing this repository does **not** automatically install or run the skill in ChatGPT, Codex or Claude. Your chosen agent must load the skill and have access to trustworthy company information.

## Repository structure

```text
multibagger-verdict/
├── README.md                   # For humans visiting GitHub
├── SKILL.md                    # The agent's workflow and decision rules
├── agents/
│   └── openai.yaml            # Optional OpenAI/Codex display metadata
├── references/
│   ├── rubric.md              # Detailed scoring & evidence requirements
│   └── research.md            # Global research, case studies & caveats
├── examples/
│   └── example-output.md      # Fictional response illustration
└── CONTRIBUTING.md            # How to suggest improvements
```

## Data requirements & limitations

- **No bundled market data.** The skill instructs the agent to research recent filings and prices; actual sources depend on the tools available at runtime.
- **No automated buy/sell orders.** This is fundamental equity research, not an execution system.
- **No proven predictive accuracy.** Thresholds are deliberately transparent starting hypotheses, not optimized or statistically calibrated factors.
- **No guaranteed 3×.** Even strong businesses can deliver poor shareholder returns when bought at a high valuation; a clear `YES` is not a price target.
- **No retrospective cherry-picking.** For historical studies, use only documents and valuation data available on the selected date; include failed and delisted peers in any purported backtest.
- **Not every industry uses the same metrics.** Banks, NBFCs, insurers, commodity producers, SaaS firms and capex-heavy manufacturers require sector-specific adjustments.

## Research foundations

The framework draws research questions—not predictive claims—from:

- [Bessembinder et al., *Long-Term Shareholder Returns: Evidence from 64,000 Global Stocks*](https://rpc.cfainstitute.org/research/financial-analysts-journal/2023/long-term-shareholder-returns-evidence-from-64000-global-stocks)
- [Chris Mayer's discussion of *100 Baggers* (CFA Society India)](https://cfasocietyindia.org/blog/iic-2021-a-conversation-with-chris-mayer-author-of-100-baggers/)
- [Motilal Oswal Wealth Creation Study — SQGLP](https://ftp.motilaloswal.com/emailer/Research/WC19-20141212-MOSL-2009-14-PG048.pdf)
- Historic company reports and letters, with case-study caveats documented in [`references/research.md`](references/research.md).

## Roadmap

- [ ] Point-in-time backtests with contemporaneous financials and prices
- [ ] Compare winners with losers and delisted companies; measure false positives
- [ ] Sector-specific rubric calibration and peer baselines
- [ ] Repeatable tests for valuation scenarios, point-in-time discipline and missing-data overrides
- [ ] Optional adapters for reliable filing and market-data providers

**Current status:** v1 research framework. Not backtested as a stock-selection strategy. Contributions and constructive scrutiny are welcome; please read [`CONTRIBUTING.md`](CONTRIBUTING.md).

## License

No open-source license has been selected yet. If you intend others to copy, modify and redistribute this work, choose and add a license (for example, MIT or Apache-2.0) before promoting it as open source.
