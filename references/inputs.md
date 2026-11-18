# Required inputs: Multibagger Verdict v1.1

The skill retrieves nothing itself. Before scoring, the agent must have the fields below from a tool or from documents the user supplied. Each value carries a tag in the output: `[F: document, date]` filing or annual report; `[M: source, timestamp]` market data; `[U: source]` unverified secondary source; `[A]` assumption.

**Gate.** If any *mandatory* field is missing, cannot be corroborated against a filing, or is available only as an undated aggregator figure, the verdict is INSUFFICIENT EVIDENCE and the output lists the missing fields by name. Optional fields that are missing are marked N/A and earn no points. Nothing is ever filled from memory, from "typical" values, or from a prior session.

## Identity and market data

| Field | Mandatory | Acceptable source | If missing |
|---|:--:|---|---|
| Ticker, exchange, ISIN | yes | exchange master, filing cover page | stop: resolve with the user |
| As-of date | yes | user or today's date | stop |
| Price with timestamp | yes | `[M]` exchange or market-data tool; never recalled | stop |
| Market capitalization | yes | `[M]`, or price × diluted shares `[F]` | stop |
| Diluted share count, plus outstanding warrants/ESOPs/convertibles | yes | latest filing, shareholding pattern | stop |
| Reporting currency and fiscal-year end | yes | annual report | stop |
| Reporting basis (consolidated/standalone) and why | yes | annual report | stop |
| Free float, average daily traded value, surveillance status (ASM/GSM) | optional | exchange | N/A; confidence Low for microcaps |

## Financial history (same basis throughout)

| Field | Mandatory | Acceptable source | If missing |
|---|:--:|---|---|
| Sales, EBIT (or operating profit), PAT, diluted EPS: 5 fiscal years (minimum 3) | yes | audited annual reports `[F]` | stop below 3 years |
| Cash flow from operations and capex: same years | yes (nonfinancials) | annual reports `[F]` | stop |
| Net debt or net cash, and debt maturity profile | yes (nonfinancials) | annual report notes, rating report | stop |
| Latest quarterly results and the year-ago quarter, same basis | yes | exchange filing `[F]` | stop |
| Receivables, inventory, payables (for working-capital days) | optional | annual report | N/A; cash pillar capped at 50% |
| Cash taxes paid vs tax expense | optional | cash-flow statement | N/A |
| Segment or product mix, volumes vs price | optional | annual report, presentation | N/A; runway pillar capped at 50% |
| Order book / contracted revenue with execution period | optional | filings, presentations | N/A |

Financial-sector businesses replace the nonfinancial rows with: NIM or spread, ROA and ROE, capital adequacy, GNPA/NNPA or stage-3 ratio, provision coverage, funding mix and concentration, ALM profile. All mandatory when the archetype is (f).

## Ownership and governance

| Field | Mandatory | Acceptable source | If missing |
|---|:--:|---|---|
| Promoter holding and pledged share of it, last 4 quarters | yes | shareholding pattern filings `[F]` | stop |
| Statutory auditor, tenure, any resignation, qualifications or emphasis of matter in the last 3 years | yes | annual reports, exchange filings | stop |
| Related-party transactions: size relative to sales and profit | yes | annual report notes | stop |
| Regulatory actions, divergence reports, exchange notices, going-concern language | yes (if any exist) | regulator or exchange filings | record "none found in sources checked" with the list of sources |
| Contingent liabilities | optional | annual report notes | N/A |
| Credit rating and outlook, with date | optional | rating agency `[F]` | N/A |

## Valuation inputs

| Field | Mandatory | Acceptable source | If missing |
|---|:--:|---|---|
| Entry multiple (P/E, EV/EBITDA or P/B as fits the archetype) computed from tagged inputs | yes | derived | stop |
| Peer or own-history multiple range, dated | optional | `[M]` or `[U]` | N/A; exit multiple then `[A]` and pillar picks the lower end |
| Growth, margin and dilution assumptions for each scenario | yes | derived, each `[A]` with a one-line reason | stop |

## Output requirement

List at the end of the output which mandatory fields came from `[F]` or `[M]` sources, which were `[U]`, and which were `[A]`. If more than 30% of mandatory fields are `[U]` or `[A]`, confidence is Low and a YES verdict is not available.
