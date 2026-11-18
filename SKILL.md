---
name: multibagger-verdict
description: Evaluate a listed Indian or global stock by ticker or company name for potential 3x-10x returns over 3-7 years. Use for prompts like 'multibagger verdict on TICKER', 'can STOCK become a multibagger?', 'analyze STOCK for long-term multibagger potential', or stock requests explicitly asking for a YES/NO investment-potential verdict. Research fresh company filings and valuation, score fundamental quality and growth, and conclude POTENTIAL MULTIBAGGER, WATCHLIST, UNLIKELY, or INSUFFICIENT EVIDENCE. Do not invoke for a pure price quote, financial result recap, or short-term trading question unless the user asks for multibagger potential.
---

# Multibagger Verdict v1.1

**Mission:** Assess whether a listed equity has a *credible, evidence-backed path* to >=3x total shareholder value over a 3-7 year horizon. Distinguish a truly scalable growth story from a superficially attractive screen. A 10x outcome is a **separate stretch case** and never assumed. Deliver a decisive headline, not an endless checklist. No promise of any return or exact prediction.

**What this skill is:** a research checklist and decision rule. It retrieves no data itself. It must be paired with a tool that returns dated filings and market data (an exchange-filings API, a market-data MCP, a financial terminal, or documents the user supplies). Without such a tool the only honest verdict is INSUFFICIENT EVIDENCE. Its thresholds are unvalidated heuristics; see `references/evaluation.md` for the test that would validate them and `README.md` for the (currently empty) results table.

**Invocation:** `$multibagger-verdict <exchange:ticker>` in Codex, or `@multibagger-verdict <exchange:ticker>` if installed and supported in ChatGPT. Also match natural-language prompts described in metadata. If a user provides a company name, resolve the exact listed security and exchange first.

## Mandatory execution

1. **Date and identity.** State the analysis `as of` date, ticker, listing venue, reporting currency, market capitalization, latest reliable price with timestamp, and the reporting basis (see *Reporting basis* below). Do not mix calendar and fiscal years or currencies. Do not invent a live price or return metric. If the user gives a historical analysis date, use ONLY sources dated on/before that date.
2. **Collect the required inputs.** `references/inputs.md` lists every field, whether it is mandatory, the acceptable source type, and what to do when it is missing. Prefer exchange/SEC filings, audited annual reports (>=3 years; ideally 5), latest quarters, investor presentations, credit-rating reports, earnings-call transcripts, and *dated* price/market cap. Aggregators (Screener.in, StockAnalysis, terminals) may supply metrics, but anomalies must be checked against the filing. **Gate:** if any mandatory field is missing or cannot be corroborated, stop and return INSUFFICIENT EVIDENCE with the missing fields listed by name. Never fill a gap with a remembered or typical value.
3. **Tag every number and every source.** Each figure in the output carries one tag: `[F: document, date]` for a filing or annual report, `[M: source, timestamp]` for market data, `[U: source]` for an unverified secondary source, `[A]` for an assumption. A URL may appear only if the agent retrieved it in this session; otherwise write `[document type, date, not retrieved]`. Untagged numbers and unretrieved links are defects, not style choices.
4. **Identify the economic archetype.** (a) early scalable growth, (b) proven compounder, (c) earnings/capex inflection, (d) cyclical/value recovery, (e) acquisitive compounder, or (f) financial-sector business. A company can fit several; name the primary one. Compare with peers in the same economics rather than one global ROCE rule. New IPOs can be assessed but data gaps lower confidence.
5. **Identify the *specific* upside mechanism.** Sales volume, new market, share gains, pricing power, mix, operating leverage, capacity utilization, asset turns, sustainable M&A, platform/network effects, and/or debt reduction. Reconcile planned capacity/order book with realizable revenue, margins, working capital and execution schedule. A P/E re-rating is not a mechanism.
6. **Compute the scenarios before scoring.** Build the bear/base/bull table in *Scenario math* below from tagged inputs. The valuation pillar is then assigned by the fixed mapping in that section; the agent does not choose it.
7. **Score the other six pillars** using the rubric below and `references/rubric.md`. Show the seven component scores in detailed mode; show only the total and top drivers in default concise mode. These are **decision heuristics, not calibrated probabilities**. No points for missing or uncorroborated claims.
8. **Check forensic vetoes and data quality.** Confirm any red flag in a primary source, do not equate allegations with findings, and do not label a business fraudulent without strong evidence. Apply the overrides below.
9. **Emit the headline first** in the prescribed format, a 3-sentence rationale, 3 thesis drivers, 3 invalidation risks, and 1-2 next verification milestones. Be concise unless the user requests full research. Never treat the score as buy/sell advice or an instruction to change a portfolio.

## Reporting basis: consolidated vs standalone

Indian issuers publish both. Use **consolidated** whenever the company has subsidiaries, joint ventures or associates that are material to sales or profit; use **standalone** only when there is no consolidated statement or the subsidiaries are immaterial, and say so. Never compute a growth rate, a margin trend or a ratio across the two bases, and never compare a consolidated quarter with a standalone prior-year quarter. State the basis in the output header. If the only available series mixes bases, treat the affected fields as missing.

## Scenario math (done first; drives the valuation pillar)

Build a 5-year table (7 years when a long ramp-up warrants it; 3 years only if the user asks). Each row states its inputs with tags:

| Scenario | Revenue CAGR | Terminal margin | Terminal earnings or FCF | Exit multiple (vs entry) | Share count (dilution) | Net debt bridge | Equity value | Multiple of today's market cap |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bear | | | | | | | | |
| Base | | | | | | | | |
| Bull | | | | | | | | |

For an ordinary profitable business the identity is: multiple ≈ (1 + EPS CAGR)^years × (exit P/E ÷ entry P/E) × (shares today ÷ shares at exit), plus dividends when material. For asset-heavy or leveraged businesses use EV/EBITDA with an explicit future net-debt bridge; for financials use book value, sustainable ROE and P/B; for loss-making platforms use a path to FCF and the diluted future share count. If the inputs for the table cannot be sourced, the table reads "Not reliably quantifiable" and the evidence gate in step 2 applies.

**Fixed mapping to the valuation pillar (15 points):**

| Condition (5-year multiples, after dilution) | Points |
|---|---:|
| Base >= 1.7x and Bull >= 3.0x and Bear >= 0.7x | 13-15 |
| Base >= 1.7x and Bull >= 3.0x and Bear 0.5-0.7x | 10-12 |
| Base >= 1.7x and Bull >= 3.0x and Bear < 0.5x | 7-9 |
| Base 1.3-1.7x and Bull >= 3.0x | 6-8 |
| Base 1.3-1.7x and Bull 2.0-3.0x | 3-5 |
| Bull < 2.0x, or Base < 1.3x | 0-2 |
| Table not computable | 0, and INSUFFICIENT EVIDENCE |

Cap: if the bull case's exit multiple exceeds the entry multiple by more than 30%, the pillar is capped at 8 regardless of the row, because most of the outcome would then be re-rating rather than business growth. Within a row, pick the lower end when inputs are mostly `[A]`-tagged.

## Scoring model (100 points total)

| Dimension | Max | Evidence to reward |
|---|---:|---|
| Addressable runway and scalable unit economics | 20 | Large *reachable* opportunity, demonstrated customer/market penetration, capacity-to-sales logic, repeatable unit economics, room to get materially larger |
| Revenue, earnings and inflection evidence | 20 | Multi-year organic sales growth, volume vs price, earnings/cash profit acceleration, leading indicators, backlog conversion; normalized earnings for cycles |
| Competitive advantage, management and governance | 15 | Pricing power, switching costs, network/distribution edge, credible management execution, candid disclosures, clean capital allocation/related parties |
| Capital efficiency and reinvestment | 15 | ROIC/ROCE and ideally *incremental* ROIC; tangible reinvestment opportunity, sustainable return on *new* invested capital, or evidenced post-capex ramp |
| Cash conversion and balance-sheet resilience | 10 | Multi-year cumulative CFO/PAT, working-capital discipline, cash taxes, manageable debt/maturities, positive normalized FCF after maintenance capex |
| Entry valuation and achievable shareholder payoff | 15 | **Assigned by the fixed mapping in *Scenario math*; not scored by judgment** |
| Catalysts and measurable confirmation | 5 | Dated projects, signed contracts and realizable conversion, market-share traction, product milestones; price strength is optional and never fundamental proof |

**Anchors for the six judged pillars:** 0 = no evidence/poor; 25% of weight = weak; 50% = mixed; 75% = good; 100% = unusually strong and independently supported. Make reasons specific. If an entire dimension lacks evidence, score 0 for that dimension and apply the evidence gate. A company with no moat and no runway must not score YES because of a low P/E.

## Historical growth anchors (diagnostic, not strict entry rules)

- TTM and trailing 3y sales CAGR >=15% is an attractive starting point for early growth. 3y normalized earnings CAGR >=20% may help a 3x thesis, but do not mechanically reject firms about to inflect.
- 3-5y cumulative CFO / cumulative PAT >=0.8 for profitable nonfinancial firms is a useful **heuristic**; evaluate stock-based compensation, working-capital seasonality, customer advances and capex separately. Cash tax paid / reported tax expense >=0.6 over 3-5 years is a forensic clue, not a universal screen or evidence of fraud in isolation.
- ROCE/ROIC >=15% can indicate capital productivity; for underutilized new plants prefer forward *incremental* capital productivity based on a verifiable ramp. For asset-light companies account for expensed R&D/intangibles; for roll-ups separate organic growth, acquired capital, goodwill and leverage.
- Net debt / normalized EBITDA <2x and interest coverage >3x are *illustrative* ranges for ordinary nonfinancials. Examine refinancing, the maturity wall and working capital. Promoter pledging, dilution, warrants and conversion rights must be reviewed. Never rely on "promoter holding > X%" as proof of quality.
- Contracted order book / current sales reveals capacity, **not** revenue or free cash flow. Test execution period, cancellation, margin, funding and customer risk.
- 3x over five years requires about 24.6% annual shareholder-return CAGR; 3x over seven years about 17.0%; 10x over seven years about 39.0%. Check whether valuation compression and dilution raise the business-growth requirement.

## Verdict decision rule

Apply in order:

**INSUFFICIENT EVIDENCE:** any mandatory input in `references/inputs.md` is missing or uncorroborated, or the scenario table is not computable. No confident YES/NO. List the precise missing items. A lack of evidence is *not* a negative fundamental outcome.

**Override / governance:** a well-substantiated, material unresolved governance or solvency threat caps the result at WATCHLIST, or UNLIKELY when credible evidence shows shareholder value at severe risk (admitted material accounting misstatement, uncured insolvency, recurring going-concern qualifications with no credible financing). Auditor changes, rumours, pledging or related-party dealings prompt investigation, not automatic vetoes. A regulator-reported divergence between reported and assessed bad loans, an auditor resignation before results, or a qualified opinion is a documented finding, not a rumour, and must be addressed before any YES.

**POTENTIAL MULTIBAGGER — YES:** score >=75/100, adequate evidence (>=70% rubric coverage including finances, governance and valuation), no severe unresolved red flags, a concrete growth runway, and a valuation pillar of >=10 under the fixed mapping (which already requires Bull >=3x and Base >=1.7x). Business growth, not a terminal multiple increase, must explain most of the favourable outcome. This is a *potential* classification, not a probability estimate.

**WATCHLIST / NOT YET:** score 55-74; OR score >=75 but the valuation pillar is below 10, key catalysts are unproven, or governance concerns still need resolution. Name exact upgrade milestones and the price/valuation at which the mapping would change.

**UNLIKELY MULTIBAGGER — NO:** score <55 after adequate data; OR credible value destruction/dilution likely overwhelms growth; OR even a defensible bull case is <3x over the chosen horizon and no extraordinary reason supports otherwise. State if the company may still be a fine investment despite not fitting a 3x goal.

**Confidence:** High = strong primary-source trail, several cycles or 5y operating history, key risks measured and scenarios well-supported, few `[A]` tags. Medium = mostly primary sources but some forward uncertainties. Low = thin or newly listed, material forecast dependence, unverified inputs, or many `[A]`/`[U]` tags. No "90% chance" estimates. A YES is not a buy recommendation and timing is a separate question.

## Quality-of-earnings / risk checks

- 3-5y cumulative reported PAT vs CFO, normalized CFO after working-capital changes; revenue recognized ahead of collection; receivables and inventory relative to sales; debtor days and write-offs; cash tax versus accrual tax; recurring exceptional gains; promoter loans and related-party transactions; audit qualifications/changes; contingent liabilities; collateral/security; pledging and insider selling; share count and warrants; customer/vendor concentration; cost capitalization; maintenance vs growth capex; stock-based compensation; negative cash cycles and dependence on advances; acquisition accounting; environmental/regulatory constraints.
- For India's microcaps, assess float, bid-ask spread, average traded value, promoter holdings, ASM/GSM surveillance status, dilution, exchange notices and auditor quality. Liquidity is an *investability* flag, not evidence that the business cannot grow.
- Distinguish misconduct allegations from regulatory or audited findings. Cite a dated source for every strong governance claim.

## Sector adjustments

- **Banks/NBFC/insurers:** do NOT use CFO/PAT, EBITDA, debt/equity or ROCE as industrial filters. Use NIM/spread, ROA/ROE, capital adequacy, GNPA/NNPA/stage 3, provisioning, funding costs and concentration, deposits, ALM and underwriting/claims quality. Valuation via P/B, sustainable ROE, residual income or normalized earnings. Treat wholesale-funding dependence and regulator divergence reports as governance-grade findings.
- **Manufacturing/capex/industrial/defence:** plant economics, order-to-revenue conversion, utilization, execution risk, customer advances, working capital, maintenance capex and incremental ROCE.
- **Commodity/cyclicals:** mid-cycle earnings, unit costs, replacement value, capital discipline, peak-cycle P/E trap and a downcycle stress test.
- **SaaS/platform/software:** ARR/net retention, cohort economics, gross margin, CAC payback, SBC dilution, customer concentration, FCF, network effects and defensibility. Avoid penalizing expensed R&D with simplistic ROCE.
- **Pharma/biotech:** approvals, portfolio, specialty versus generics, compliance observations, patent cliffs, pipeline risk, regulated-market concentration and cash-funded R&D.
- **Retail/consumer:** same-store sales, new-store payback, distribution, pricing power, inventory turns, brand strength, unit economics.
- **M&A compounders:** organic vs acquired growth, acquisition cohort returns, share issuance and leverage, goodwill impairment, integration record, allocation runway.

The investor-style lenses that earlier versions listed here are summarized as a footnote in `references/research.md`; they are reading prompts, not criteria, and no named investor's method is claimed.

## Historical research and backtesting safeguards

Past winners are *hypothesis generators*, not proof that these metrics predict future winners. For any historical study, use only what was knowable at the chosen date, include failed and delisted peers, use point-in-time share counts and filings, corporate actions, currency and dividend adjustment, contemporaneous valuation, liquidity and transaction costs. `references/evaluation.md` defines the test this skill has to pass before any accuracy claim; `references/rubric.md` walks four real failures through the rubric at a pre-failure date. If the data for such a study is unavailable, label the result an illustrative case study, **not a backtest**. Never alter an existing paper/live investment strategy, rule hash or execution logic without a separate explicit user instruction.

## Default output (STRICT; concise)

**VERDICT: [POTENTIAL MULTIBAGGER — YES | WATCHLIST — NOT YET | UNLIKELY — NO | INSUFFICIENT EVIDENCE]**
**Stock:** TICKER (exchange) · **Basis:** consolidated/standalone · **Horizon:** 5–7 years · **Score:** X/100 (valuation pillar Y/15 by mapping) · **Confidence:** High/Medium/Low · **As of:** date
**Why:** 1-2 sentences giving the central business + valuation logic.
**Scenario table:** the bear/base/bull rows with tagged inputs, or "Not reliably quantifiable from available evidence".
**3 reasons:** 3 brief points, each with a tag.
**3 risks:** 3 brief points, including what would *invalidate* the thesis.
**Next milestone:** a specific result, contract conversion, cash-flow figure, governance development, or the valuation at which the mapping row changes.
**Sources:** 2–5 dated primary documents. Retrieved ones as links; others as `[document type, date, not retrieved]`.

No generic disclaimer wall. If only a ticker is provided, do the work rather than seek permission. If an ambiguous ticker genuinely cannot be resolved, request the exchange/company. Expand to a full investment memo only when requested.

See `references/inputs.md` for the required-inputs schema, `references/rubric.md` for scoring anchors, negative cases and test prompts, `references/evaluation.md` for the validation protocol, and `references/research.md` for sources and caveats.
