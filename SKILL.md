---
name: multibagger-verdict
description: Evaluate a listed Indian or global stock by ticker or company name for potential 3x-10x returns over 3-7 years. Use for prompts like 'multibagger verdict on TICKER', 'can STOCK become a multibagger?', 'analyze STOCK for long-term multibagger potential', or stock requests explicitly asking for a YES/NO investment-potential verdict. Research fresh company filings and valuation, score fundamental quality and growth, and conclude POTENTIAL MULTIBAGGER, WATCHLIST, UNLIKELY, or INSUFFICIENT EVIDENCE. Do not invoke for a pure price quote, financial result recap, or short-term trading question unless the user asks for multibagger potential.
---

# Multibagger Verdict v1.0

**Mission:** Assess whether a listed equity has a *credible, evidence-backed path* to >=3x total shareholder value over a 3-7 year horizon. Distinguish a truly scalable growth story from a superficially attractive screen. A 10x outcome is a **separate stretch case** and never assumed. Deliver a decisive headline, not an endless checklist. No promise of any return or exact prediction.

**Invocation:** `$multibagger-verdict <exchange:ticker>` in Codex, or `@multibagger-verdict <exchange:ticker>` if installed and supported in ChatGPT. Also match natural-language prompts described in metadata. If a user provides a company name, resolve the exact listed security and exchange first.

## Mandatory execution

1. **Date and identity**: State analysis `as of` date, ticker, listing venue, reporting currency, market capitalization, latest reliable price with timestamp, and whether data are consolidated or standalone. Do not mix calendar and fiscal years or currencies. Do not invent live price or return metrics. If the user gives a historical analysis date, use ONLY sources available on/before that date.
2. **Gather source evidence**: Prefer exchange filings/SEC filings, audited annual reports (>=3 years; ideally 5), latest quarters, investor presentations, credit-rating reports, earnings-call transcripts, and *dated* price/market cap. Screener.in / StockAnalysis / financial terminals can help source metrics but verify anomalies against filings. Source the most material assertions. If live research isn't available, do not silently rely on old cached metrics; label any result provisional and cap confidence at Low.
3. **Identify the economic archetype**: (a) early scalable growth, (b) proven compounder, (c) earnings/capex inflection, (d) cyclical/value recovery, (e) acquisitive compounder, or (f) financial-sector business. A company can fit multiple archetypes; name the primary one. Compare with peers in the same economics rather than one global ROCE rule. New IPOs can be assessed but data gaps lower confidence.
4. **Identify the *specific* upside mechanism**: sales volume, new market, share gains, pricing power, mix, operating leverage, capacity utilization, asset turns, sustainable M&A, platform/network effects, and/or debt reduction. Avoid counting simple P/E re-rating as the entire thesis. Reconcile planned capacity/order book with actual realizable revenue, margins, working capital and execution schedule.
5. **Calculate the 100-point score** using the rubric below and references/rubric.md. Show 7 component scores in detailed mode; show only total and top drivers in default concise mode. These are **decision heuristics, not empirically calibrated probabilities**. Do not allocate points for missing/uncorroborated claims.
6. **Model price-paid-to-upside**: Model bear/base/bull 3-, 5-, and/or 7-year outcomes (use 5 years by default, and 7 when long ramp-up warrants it), showing growth, margin, terminal valuation, share dilution and debt/equity bridge where relevant. Use EPS growth x (exit P/E / current P/E) x (current fully diluted shares / future shares) as a *rough* non-financial profitable-business identity; for loss-making, asset-heavy, acquisition-led, or financial companies use an appropriate valuation framework. Include net debt, future capital raises and dilution. Note sensitivity to terminal multiples and lower growth. Do not assert 3x is plausible without showing how earnings/cash flow can support the terminal enterprise/equity value. Dividend-adjusted returns when material.
7. **Check forensic vetoes and data quality**. Confirm any red flag using primary sources, avoid equating allegations with findings, and do not label a business fraudulent without strong evidence. Apply overrides below.
8. **Emit headline first** in the prescribed format, a 3-sentence rationale, 3 thesis drivers, 3 invalidation risks, and 1-2 next verification milestones. Be concise unless the user requests full research. Never treat the score as buy/sell advice or an instruction to change a portfolio.

## Scoring model (100 points total)

| Dimension | Max | Evidence to reward |
|---|---:|---|
| Addressable runway and scalable unit economics | 20 | Large *reachable* opportunity, demonstrated customer/market penetration, capacity-to-sales logic, repeatable unit economics, room to get materially larger |
| Revenue, earnings and inflection evidence | 20 | Multi-year organic sales growth, volume vs price, earnings/cash profit acceleration, leading indicators, backlog conversion; use normalized earnings for cycles |
| Competitive advantage, management and governance | 15 | Pricing power, switching costs, network/distribution edge, credible management execution, candid disclosures, clean capital allocation/related parties |
| Capital efficiency and reinvestment | 15 | ROIC/ROCE and ideally *incremental* ROIC; tangible reinvestment opportunity, sustainable high return on *new* invested capital, or evidenced post-capex ramp |
| Cash conversion and balance-sheet resilience | 10 | Multi-year cumulative CFO/PAT, working capital discipline, cash taxes, manageable debt/maturities, positive normalized FCF after maintenance capex |
| Entry valuation and achievable shareholder payoff | 15 | Conservative terminal assumptions, asymmetric downside, dilution accounted, reasonable peers/history and >=3x bull route without relying only on P/E expansion |
| Catalysts and measurable confirmation | 5 | Dated projects, signed contracts and realizable conversion, market share traction, product milestones, verified price relative strength (optional, not fundamental proof) |

**Suggested qualitative anchors:** 0 = no evidence/poor; 25% of weight = weak; 50% = mixed; 75% = good; 100% = unusually strong, independently supported. Make reasons specific. If an entire dimension lacks evidence, score 0 for that dimension and apply the evidence gate. A company with no moat and no addressable runway should not score YES simply due to low P/E.

## Historical growth anchors (diagnostic, not strict entry rules)

- TTM and trailing 3y sales CAGR >=15% is an attractive starting point for early growth. 3y normalized earnings CAGR >=20% may help a 3x thesis, but do not mechanically reject firms about to inflect.
- 3-5y cumulative CFO / cumulative PAT >=0.8 for profitable nonfinancial firms is a useful **heuristic**; evaluate stock-based compensation, working-capital seasonality, customer advances, and capex separately. CFO / EBITDA may be meaningful, but check if 'operating profit' is a valid EBITDA proxy. Cash tax paid / reported tax expense >=0.6 over 3-5 years is a forensic clue, not a universal screen or evidence of fraud in isolation.
- ROCE/ROIC >=15% can indicate capital productivity; for underutilized new plants, prefer forward *incremental* capital productivity based on verifiable ramp-up. For asset-light companies, account for expensed R&D/intangibles; for roll-ups, separate organic growth, acquired capital, goodwill and leverage.
- Net debt / normalized EBITDA <2x and interest coverage >3x are *illustrative* ranges for ordinary nonfinancials, not universal sector rules. Examine refinancing, maturity wall and working capital. Promoter pledging, dilution, equity warrants and conversion rights must be reviewed. Never rely on 'promoter holding > X%' as proof of quality.
- Contracted order book / current sales may reveal capacity, **not** automatically revenue or free cash flow. Test execution period, cancellation, margin, funding and customer risk.
- 3x over five years requires about 24.6% annual shareholder-return CAGR; 3x over seven years about 17.0%. 10x over seven years requires about 39.0%. Check whether valuation compression and dilution make business growth requirements substantially greater.

## Verdict decision rule

Apply in order:

**INSUFFICIENT EVIDENCE:** Essential current price/market cap, last audited accounts, latest results, ownership/pledge and credible valuation inputs are missing or cannot be corroborated. No confident YES/NO. Explain precise missing items. A lack of evidence is *not* a negative fundamental outcome.

**Override / governance:** A well-substantiated, material unresolved governance or solvency threat caps result at WATCHLIST, or UNLIKELY when credible evidence shows shareholder value at severe risk (e.g., admitted material accounting misstatement, insolvency not cured, recurring going-concern qualifications with no credible financing). Auditor changes, rumors, pledging or related-party dealings prompt investigation, not automatic accusations or vetoes.

**POTENTIAL MULTIBAGGER — YES:** score >=75/100, adequate evidence (>=70% rubric coverage, including finances, governance and valuation), no severe unresolved red flags, concrete growth runway with plausible 5-7 year *bull case* >=3x, and a reasonable **base-case outcome >=1.7x** with acceptable downside survival. Business growth, not a speculative terminal multiple increase, must explain most of the favorable outcome. This is a *potential* classification, not a probability estimate.

**WATCHLIST / NOT YET:** score 55-74; OR score >=75 but 3x outcome is valuation-dependent, key catalysts unproven, base case <1.7x, or governance concerns still need resolution. Name exact upgrade milestones and price/valuation conditions.

**UNLIKELY MULTIBAGGER — NO:** score <55 after adequate data; OR credible value destruction/dilution likely overwhelms growth; OR even a defensible bull case is <3x over the chosen 5-7 year horizon and no extraordinary reason supports otherwise. State if the company may still be a fine investment despite not fitting a 3x goal.

**Confidence:** High = strong primary-source trail, several cycles or 5y operating history, key risks measured and valuation scenarios well-supported. Medium = mostly primary sources but some forward uncertainties. Low = thin/newly listed, material forecast dependence, unverified inputs, or incomplete data. No '90% chance' estimates. A YES is not a buy recommendation and technical timing is a separate question.

## Quality-of-earnings / risk checks

- 3-5y cumulative reported PAT vs CFO, normalized CFO after changes in working capital; revenue recognized ahead of collection; receivables and inventory relative to sales; debtor days and write-offs; cash tax versus accrual tax; recurring exceptional gains; promoter loans and related-party transactions; audit qualifications/changes; contingent liabilities; collateral/security; pledging and insider selling; share count and warrants; customer/vendor concentration; cost capitalization; maintenance vs growth capex; employee stock-based compensation; negative cash cycles and dependence on advance collections; mergers/acquisition accounting; environmental/regulatory constraints.
- For India's microcaps, assess float, bid-ask spread, average traded value, promoter holdings, market surveillance/ASM/GSM if relevant, dilution, exchange notices and auditor quality. Liquidity is an *investability* flag, not evidence that the business cannot grow.
- Distinguish misconduct allegations from regulatory or audited findings. Cite dated source for every strong governance claim.

## Sector adjustments

- **Banks/NBFC/insurers:** DO NOT use CFO/PAT, EBITDA, debt/equity or ROCE as ordinary industrial filters. Use NIM/spread, ROA/ROE, capital adequacy, GNPA/NNPA/stage 3, provisioning, funding costs, deposits, ALM and underwriting/claims quality. Valuation via P/B, sustainable ROE, residual income or normalized earnings.
- **Manufacturing/capex/industrial/defence:** plant economics, order-to-revenue conversion, utilization, execution risk, customer advances, working capital, maintenance capex and incremental ROCE.
- **Commodity/cyclicals:** mid-cycle earnings, unit costs, replacement value, capital discipline, peak-cycle P/E trap and stress-test for downcycle.
- **SaaS/platform/software:** ARR/net retention, cohort economics, gross margin, CAC payback, SBC dilution, customer concentration, FCF, network effects and defensibility. Avoid penalizing expensed R&D with simplistic ROCE.
- **Pharma/biotech:** approvals, product portfolio, specialty versus generics, compliance observations, patent cliffs, pipeline risks, regulated-market concentration and cash-funded R&D.
- **Retail/consumer:** same-store sales, new-store payback, distribution, pricing power, inventory turns, brand strength, unit economics.
- **M&A compounders:** organic vs acquired growth, acquisition cohort returns, share issuance and leverage, goodwill impairment, integration success, allocation runway.

## Investor-style lens (non-exclusive; not claimed secret formulas)

- Vijay Kedia / SMILE: scalable small businesses, management quality, large opportunity and patience.
- Ashish Kacholia: emerging company, acceleration and management/capacity assessment; make no claim about exact private filters.
- Mukul Agrawal: industry trend, catalyst, management execution and price/valuation confirmation; don't infer exact purchase price from public holdings.
- Sunil Singhania / MEETS: earnings trajectory, leadership, event/catalyst, timing and structural opportunity.
- Chris Mayer / 100 Baggers: high return on incremental capital and capacity to reinvest for many years, often owner-oriented managers.
- Motilal Oswal / SQGLP: smaller starting size, quality, growth, longevity and reasonable entry price.
- Saurabh Mukherjea: persistent cash-generative compounders and returns on capital over time.
- Porinju / cyclical-value: undervalued improvement; use normalized economics instead of peak P/E.

Do **not** treat any style as a rigid formula allegedly employed by a named investor. Cite interviews when attributing specifics.

## Historical research and backtesting safeguards

Past winners are *hypothesis generators*, not proof that these metrics predict future winners. Use examples like Monster (distribution), Amazon (reinvestment), Nvidia (technology ecosystem), Constellation (acquisitions/ROIC), Netflix (global scalable economics), and Copart (network effects), but explicitly check what was knowable at a chosen pre-rally date and also test failed peers. Historical research must include delisted losers, survivorship-free security masters when possible, point-in-time share counts and filings, corporate actions, currency and dividend adjustment, contemporaneous valuation, liquidity, transaction costs and sell-side rules. If unavailable, label the analysis an illustrative case study, **not a backtest**. Never alter an existing paper/live investment strategy, rule hash or execution logic without a separate explicit user instruction.

## Default output (STRICT; concise)

**VERDICT: [POTENTIAL MULTIBAGGER — YES | WATCHLIST — NOT YET | UNLIKELY — NO | INSUFFICIENT EVIDENCE]**
**Stock:** TICKER (exchange) · **Horizon:** 5–7 years · **Score:** X/100 · **Confidence:** High/Medium/Low · **As of:** date
**Why:** 1-2 sentences giving central business+valuation logic.
**Upside math:** 5/7y bear/base/bull outcomes, **only if inputs supported**, and key assumptions. If not available: 'Not reliably quantifiable from available evidence'.
**3 reasons:** 3 brief points.
**3 risks:** 3 brief points, including what would *invalidate* thesis.
**Next milestone:** Specific result, contract/conversion, cash flow, governance development, or reasonable valuation price/metric to watch.
**Sources:** 2–5 dated primary links and any critical secondary data sources.

No generic disclaimer wall. If only ticker provided, do the work rather than seek permission. If ambiguous ticker genuinely cannot be resolved, request the exchange/company. Expand to a full investment memo only when requested.

See `references/rubric.md` for scoring anchors, formulas, evidence quality, and test prompts. See `references/research.md` for historical global lessons and sources.
