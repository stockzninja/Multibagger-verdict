# Scoring and validation reference: Multibagger Verdict v1.1

## Point allocation

For each judged category score 0, 25, 50, 75 or 100% of its maximum. Intermediate values allowed only when clear reasons support them. The valuation category is not judged: it is mapped from the scenario table (see SKILL.md). Summing category points yields 0-100. Show arithmetic in full research mode. Every number cited in support of a score carries its tag (`[F]`, `[M]`, `[U]`, `[A]`); see `references/inputs.md`.

| Category | Max | 0 or weak evidence | 50% anchor | 75-100% anchor |
|---|---:|---|---|---|
| Runway | 20 | Market saturated, unrealistic TAM | Reachable growth market, weak advantage | Demonstrated penetration and sizeable realistic runway; sound unit economics |
| Growth / inflection | 20 | Stagnant/declining with no evidenced change | 10-15% organic growth or verified recovery setup | >15-20% sustainable organic sales growth, quality of earnings, leading evidence of acceleration |
| Moat / management / governance | 15 | Evidenced capital destruction or material weak governance | Average industry economics, mostly adequate controls | Defensible moat, transparent capital allocation, credible repeated execution |
| Returns / reinvestment | 15 | ROIC below cost of capital and no improvement | ROIC near cost, emerging capex utilization | Strong demonstrated incremental returns and multi-year deployment runway |
| Cash / balance sheet | 10 | Material cash-profit discrepancy or survival risk | Adequate cash conversion/financing | Multiyear cash conversion, healthy funding and stress resilience |
| Price / payoff | 15 | **Not judged.** Assigned by the fixed mapping in SKILL.md (*Scenario math*) from the bear/base/bull multiples; capped at 8 when the bull case's exit multiple exceeds entry by more than 30% | | |
| Catalysts | 5 | None or repeatedly missed | One documented milestone, uncertain timing | Multiple measurable milestones with supporting evidence |

Risk overrides and missing-data gates are in SKILL.md; do not average them away.

## Source and evidence checklist

Capture (with as-of date): price, market cap, shares diluted, sales/EBIT/PAT EPS/FCF/CFO for 3-5y, net debt/financing, return on capital, growth capex/working capital, insider equity/pledging, auditors, contingent liabilities, valuation peers, company-specific TAM/catalysts, dated management disclosures. For 10Y compounder claims, seek 10y record when available. Compare consolidated reports consistently. Mark missing as N/A, not zero, but no points for unsupported positive claims. Require filing evidence for serious risk assertions.

## Valuation examples (hypothetical only)

For a profitable company: starting fully diluted EPS=10, starting P/E=25, projected five-year EPS CAGR=25%, exit P/E=22, and shares increase 5%: return multiple ~= (1.25^5)*(22/25)/1.05 = 2.56x (excluding dividends). Strong profit growth still does NOT establish a 3x stock outcome if the entry valuation is high and equity is diluted.

For a normalized debt-heavy manufacturer use EV/EBITDA and a *future* net-debt bridge: exit equity value = terminal EBITDA x terminal EV/EBITDA - projected net debt + other adjustments. For a financial business use balance sheet/ROE/PB. For a loss-making SaaS platform use a path to FCF and diluted future shares; EV/sales alone is insufficient to prove shareholder returns.

A high ROCE at tiny scale without ability to redeploy capital is not a multibagger criterion. Very large market cap requires larger absolute future earnings and capital markets; check TAM and share required at terminal valuation.

## Adversarial self-check before any YES

1. Could 3x depend mainly on higher P/E instead of larger owner earnings?
2. Would receivables, inventory, taxes and maintenance capex consume the forecast operating cash?
3. Can a customer delay, regulator, pricing pressure or competitor destroy the thesis?
4. Is the market opportunity reachable at expected margins, not just theoretically large?
5. How much share issuance, warrants and stock compensation dilute the upside?
6. Is today a cyclical peak being misread as growth?
7. Are claims based on filings dated after the period being analyzed?
8. What are the closest failed peers and why would this company differ?
9. Do scenario multipliers reconcile to enterprise value, cash and share count?
10. Is market capitalization already too large for the proposed terminal size?

## Negative cases: real names, point-in-time (author's walk-through, to be re-verified against the listed documents)

Each case names a company that later destroyed most of its equity value, an as-of date before the failure became public, the documents that were available on that date, the score the rubric would most plausibly have produced from those documents alone, and the rule that should have caught it. Figures are deliberately omitted: fill them from the dated documents when using a case as a regression test, and record the actual rubric output. These are tests of the rubric, not statements about any person.

### 1. Manpasand Beverages (NSE: MANPASAND), as of 2018-03-31
- **Available then:** FY2015 IPO prospectus; FY2016 and FY2017 annual reports (consolidated); QIP document (2016); quarterly results through Dec-2017; shareholding patterns; the statutory auditor's FY2017 report.
- **What happened after:** the statutory auditor resigned in May 2018 days before the FY2018 results were due; in 2019 senior management was arrested in a GST-evasion case; the stock lost most of its value and was later suspended.
- **Rubric walk-through on the as-of documents:** runway and growth pillars would score high (fast reported sales growth, capacity expansion, a consumer brand in a large category). Cash and capital pillars would score low if the walk-through is done honestly: reported profit growth with weak cumulative CFO/PAT, high and rising receivables and inventory relative to sales, repeated equity raises funding capex, and a low cash-tax ratio. Governance would be scored mid without a specific finding.
- **Plausible outcome:** 60-70, WATCHLIST, with the cash-quality items as the stated milestones. A careless run that credits the growth story and skips the CFO/PAT and receivables checks produces 75+ and YES.
- **Rule that must catch it:** the cash-conversion pillar at 0-25% when cumulative CFO/PAT is weak and receivables rise faster than sales; the evidence gate if the cash-flow statement was not actually read. A YES is not possible under the v1.1 gate when those fields are `[A]`.

### 2. Vakrangee (NSE: VAKRANGEE), as of 2017-12-31
- **Available then:** FY2015-FY2017 annual reports; quarterly results through Sep-2017; the franchise-outlet ("Kendra") expansion presentations; shareholding patterns; the auditor's reports.
- **What happened after:** the stock collapsed in January-February 2018 amid questions about disclosures, trading in the shares and the quality of the reported cash; the statutory auditor resigned in April 2018 citing lack of information about certain matters; the share price fell more than 80% over 2018.
- **Rubric walk-through:** runway (rural distribution network), growth and reported returns would all score high; the business was asset-light with large reported cash. The weak points visible before the collapse: a large cash balance with little disclosure of where it sat and why it was not returned or deployed, rapid outlet-count growth that could not be independently verified, thin disclosure of unit economics per outlet, and a very high valuation that made the scenario table's base case depend on continued multiple expansion.
- **Plausible outcome:** 75+ on the judged pillars, but the v1.1 valuation mapping would score 0-5 (bull case dependent on exit multiple above entry; cap at 8 applies), bringing the total below 75 or into WATCHLIST. Under v1.0 the same inputs could produce YES.
- **Rule that must catch it:** the re-rating cap in the valuation mapping; the governance pillar at 25% when a large cash balance is not reconciled to bank confirmations or deployment plans; `[U]` tags on the outlet count when only company presentations support it.

### 3. Dewan Housing Finance (NSE: DHFL), as of 2018-08-31
- **Available then:** FY2016-FY2018 annual reports; quarterly results through Jun-2018; credit-rating reports (highest grades at the time); shareholding patterns; the FY2018 auditor's report.
- **What happened after:** the September 2018 liquidity shock after the IL&FS default hit wholesale-funded lenders; in early 2019 a media investigation alleged diversion of funds; the company defaulted on bonds in mid-2019 and entered insolvency later that year.
- **Rubric walk-through (archetype f, financial):** growth in loan book and reported ROE score well; capital adequacy was reported as adequate. The items visible before the shock: a funding mix heavily reliant on short-term wholesale borrowing against long-dated housing loans (ALM mismatch), rapid growth in developer and project loans relative to retail housing loans, and promoter-group related-party exposures. None of these were "findings" in the regulatory sense on the as-of date.
- **Plausible outcome:** 70-80 and a possible YES under v1.0. Under v1.1 the funding-mix and ALM fields are mandatory for archetype (f) and the sector adjustment treats wholesale-funding dependence as a governance-grade finding, which caps the verdict at WATCHLIST pending resolution.
- **Rule that must catch it:** the financial-sector adjustment on funding concentration and ALM; the related-party field in `references/inputs.md`; the bear-scenario requirement in the mapping (a lender whose bear case is a funding freeze does not reach Bear >= 0.5x).

### 4. CG Power and Industrial Solutions (NSE: CGPOWER), as of 2019-03-31
- **Available then:** FY2016-FY2018 annual reports; quarterly results through Dec-2018; disclosures about the sale of overseas businesses; shareholding patterns showing a high promoter pledge; the FY2018 auditor's report.
- **What happened after:** in August 2019 the board disclosed, following an internal investigation, that liabilities had been understated and advances to related parties had been made without authorization; the stock fell sharply and the promoter group lost control.
- **Rubric walk-through:** a turnaround archetype (c/d) with a plausible story (exit from loss-making overseas units, focus on the domestic power-equipment business). Visible before the disclosure: a very high pledge of promoter shares, lender actions against the promoter group's other entities, repeated delays and exceptional items around the overseas disposals, and weak cumulative cash generation.
- **Plausible outcome:** 50-65 and WATCHLIST or UNLIKELY if the pledge and the exceptional-items history are weighted; a careless run that credits the turnaround narrative reaches WATCHLIST at best under v1.1 because the base case cannot reach 1.7x without assumed margins (`[A]` tags push the valuation pillar to the lower end).
- **Rule that must catch it:** promoter-pledge field (mandatory) feeding the governance pillar at 25%; the cash-conversion pillar; the lower-end rule for `[A]`-heavy scenarios.

### Using the cases
Run each case with the skill, restricted to documents dated on or before the as-of date, and record: score by pillar, the valuation mapping row, the verdict, and whether the catching rule fired. A rubric change that turns any of these into a YES must be justified in the pull request.

## Quick internal regression test cases (not data claims)

- 84/100, clean governance, supported base 1.9x and bull 3.6x, moat: Potential Multibagger YES.
- 85/100, credible but unresolved material accounting restatement: Watchlist or Unlikely after materiality review, never simple YES.
- 78/100, base 1.3x, bull 2.4x: Watchlist / No based on evidence, never YES.
- 49/100, adequate evidence, poor economics: Unlikely NO.
- 92/100 based on five unreliable social media claims, no filings: Insufficient Evidence, not YES.
- Bank ROCE 10%, strong NIM/capital adequacy: Assess with financial-sector metrics, not universal industrial veto.
- Two-year-old manufacturing IPO with pre-commercial capex: Low confidence; recognize path but no unsupported score for future sales.
