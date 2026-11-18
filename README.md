# Multibagger Verdict

**An evidence-first Agent Skill: a research checklist and decision rule for whether a listed stock has a credible path to 3× returns over 3–7 years.**

Give your AI agent an NSE/BSE/NYSE/Nasdaq ticker. Instead of a generic stock summary, get a structured, source-tagged long-term thesis, a score out of 100, a bear/base/bull scenario table and a verdict:

**POTENTIAL MULTIBAGGER · WATCHLIST · UNLIKELY · INSUFFICIENT EVIDENCE**

> This is a reusable *research checklist*, not a trading bot, live screener, data API or prediction model. The verdict is an analytical classification, **not** a forecast, probability or recommendation to buy or sell. The skill retrieves no data itself and must be paired with a tool that returns dated filings and prices; without one, the only verdict it can give is INSUFFICIENT EVIDENCE.

## Validation status

| Run | Rubric commit | Names | Precision at YES | Recall | False-positive rate | Severe-loss at YES | Random baseline | Screen baseline |
|---|---|--:|--:|--:|--:|--:|--:|--:|
| Not yet run | — | — | — | — | — | — | — | — |

The protocol that fills this table is in [`references/evaluation.md`](references/evaluation.md). Until a row exists, nothing here has demonstrated predictive value, and the thresholds in the rubric are starting hypotheses.

## Why this exists

Finding future multibaggers is different from screening for cheap stocks or businesses with already-excellent ratios. A company's future share-price return depends on **how much its underlying economics can improve and how much an investor pays for that potential today**.

The checklist draws on published research on the concentration of long-term equity returns, on capital-allocation frameworks, and on well-documented cases such as Monster Beverage, Amazon, Constellation Software and Copart. It turns those ideas into a repeatable set of questions, a scoring rubric with one mechanically assigned pillar, and a decision rule. Sources and caveats are in [`references/research.md`](references/research.md).

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
Use Multibagger Verdict on NASDAQ:NVDA. Show the scenario table and the downside case.
```

```text
Evaluate BSE:XXXX as of March 2021 using only documents dated on or before that date.
```

*The tickers are usage examples, not endorsements or example verdicts. Replace `XXXX` with a valid ticker.* A fictional output is in [`examples/example-output.md`](examples/example-output.md).

## How it works

1. **Collect the required inputs.** [`references/inputs.md`](references/inputs.md) lists every field, whether it is mandatory, the acceptable source and what happens when it is missing. Missing mandatory fields stop the analysis at INSUFFICIENT EVIDENCE.
2. **Tag every number and source.** Each figure carries `[F]` filing, `[M]` market data, `[U]` unverified secondary or `[A]` assumption. A link may appear only if the agent actually retrieved it in the session.
3. **Identify the archetype and the upside mechanism.** Different economics need different yardsticks; a P/E re-rating is not a mechanism.
4. **Compute bear/base/bull scenarios first.** Growth, margin, exit multiple, dilution and a net-debt bridge, in a table with tagged inputs.
5. **Assign the valuation pillar by a fixed mapping** from those multiples (15 of the 100 points). The agent does not choose this pillar.
6. **Score the other six pillars** and apply governance and data-quality overrides.
7. **Give the verdict first**, then reasons, risks, the next confirmation milestone and dated sources.

### Scoring pillars

| Pillar | Points |
| --- | ---: |
| Market opportunity & scalable unit economics | 20 |
| Revenue growth, earnings quality & inflection | 20 |
| Competitive advantage, management & governance | 15 |
| Capital efficiency & reinvestment opportunities | 15 |
| Cash generation & balance-sheet resilience | 10 |
| Entry valuation & credible shareholder payoff (mapped from scenarios) | 15 |
| Catalysts & measurable confirmation | 5 |
| **Total** | **100** |

**Decision rules:** 75+ is *necessary but not sufficient* for `POTENTIAL MULTIBAGGER`; the valuation pillar must also be at least 10 under the mapping (which requires a bull case of at least 3× and a base case of at least 1.7×), evidence coverage must be adequate, and no material red flag may be unresolved. 55–74 usually means `WATCHLIST`; below 55 usually means `UNLIKELY`. **10× is a separate stretch scenario**, never the baseline.

See [`SKILL.md`](SKILL.md) for the full process and [`references/rubric.md`](references/rubric.md) for scoring anchors, four real failures walked through the rubric at a pre-failure date, and test cases.

## Installation

A skill is a folder containing `SKILL.md` with YAML frontmatter plus optional references. This repository is a **single-skill repository** with `SKILL.md` at its root.

**Via the community Skills CLI (if supported by your agent):**

```bash
npx skills add stockzninja/Multibagger-verdict
```

**Codex, manual installation:** clone or download this repo, then copy its contents into `~/.agents/skills/multibagger-verdict/` for user-wide use, or `.agents/skills/multibagger-verdict/` for a single project.

**Claude Code, manual installation:** place the skill folder in `~/.claude/skills/multibagger-verdict/` or `.claude/skills/multibagger-verdict/`.

**Other agents:** follow that product's [Agent Skills](https://agentskills.io) installation path and confirm it supports `SKILL.md`.

**Important:** installing the skill does not give the agent data. Pair it with a filings/market-data tool (an exchange API, a market-data MCP server, a terminal, or documents you supply). Publishing this repository does **not** automatically install or run the skill in ChatGPT, Codex or Claude.

## Repository structure

```text
multibagger-verdict/
├── README.md                   # For humans visiting GitHub
├── SKILL.md                    # The agent's workflow and decision rules
├── CHANGELOG.md                # What changed between versions
├── LICENSE                     # MIT
├── agents/
│   └── openai.yaml            # Optional OpenAI/Codex display metadata
├── references/
│   ├── inputs.md              # Required-inputs schema and the evidence gate
│   ├── rubric.md              # Scoring anchors, negative cases, test prompts
│   ├── evaluation.md          # Point-in-time validation protocol (not yet run)
│   └── research.md            # Sources, case studies, caveats, investor-lens footnote
├── examples/
│   └── example-output.md      # Fictional response illustration
└── CONTRIBUTING.md            # How to suggest improvements
```

## Data requirements & limitations

- **No bundled market data and no retrieval.** The agent's host tools supply filings and prices; the skill only says what to collect and how to tag it.
- **No automated buy/sell orders.** This is fundamental equity research, not an execution system.
- **No demonstrated predictive accuracy.** See the validation table above.
- **No guaranteed 3×.** Strong businesses deliver poor returns when bought at a high valuation; a `YES` is not a price target.
- **No retrospective cherry-picking.** Historical studies use only documents dated on or before the chosen date and include failed and delisted peers.
- **One reporting basis per analysis.** Consolidated when subsidiaries matter, standalone otherwise, never mixed.
- **Sector-specific yardsticks.** Banks, NBFCs, insurers, commodity producers, SaaS firms and capex-heavy manufacturers are judged on their own metrics.

## Research foundations

The checklist draws research questions, not predictive claims, from:

- [Bessembinder et al., *Long-Term Shareholder Returns: Evidence from 64,000 Global Stocks*](https://rpc.cfainstitute.org/research/financial-analysts-journal/2023/long-term-shareholder-returns-evidence-from-64000-global-stocks)
- [Chris Mayer's discussion of *100 Baggers* (CFA Society India)](https://cfasocietyindia.org/blog/iic-2021-a-conversation-with-chris-mayer-author-of-100-baggers/)
- [Motilal Oswal Wealth Creation Study — SQGLP](https://ftp.motilaloswal.com/emailer/Research/WC19-20141212-MOSL-2009-14-PG048.pdf)
- Historic company reports and letters, with case-study caveats in [`references/research.md`](references/research.md).

## Roadmap

- [ ] Run the validation protocol and fill the table above
- [ ] Compare winners with losers and delisted companies; measure false positives
- [ ] Sector-specific rubric calibration and peer baselines
- [ ] Repeatable tests for the scenario mapping, point-in-time discipline and missing-data gates
- [ ] Optional adapters for reliable filing and market-data providers

**Current status:** v1.1 research checklist. Not validated as a stock-selection method. Maintained by [stockzninja](https://github.com/stockzninja). Contributions and scrutiny welcome; read [`CONTRIBUTING.md`](CONTRIBUTING.md).

## License

MIT. See [`LICENSE`](LICENSE).
