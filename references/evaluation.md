# Validation protocol (not yet run)

This document defines the test the rubric must pass before the README may claim any accuracy. Until it has been run, the README's results table stays "Not yet run" and the skill describes itself as a checklist.

## Pre-registration

1. Freeze the rubric: record the git commit hash of `SKILL.md`, `references/rubric.md` and `references/inputs.md` used for the run. Changes after the run start a new run.
2. Write down, before scoring anything, the primary metric (precision for 3x in 5 years), the sample design below and the benchmark. Do not change them after seeing results.

## Universe and formation dates

- Market: NSE main board (extend to other markets separately; do not pool).
- Formation dates: the last trading day of March and September, 2010 through 2021 (24 dates). Each gives a 5-year outcome window ending 2015-2026.
- Eligible set at each date: every stock listed on that date with at least 3 fiscal years of filings, as it stood then. The eligible set must be reconstructed from a point-in-time security master, **including** names that later delisted, were suspended or went into insolvency. If the master cannot be reconstructed, say so in the report; the run is then labelled "survivorship-biased" and cannot support a claim.
- Sample per date: 25 names drawn at random from the eligible set, plus every eligible name that delisted or lost more than 80% within the 5-year window. The forced inclusion of failures is what makes the false-positive rate meaningful.

## Information discipline

- The agent may use only documents dated on or before the formation date. The retrieval tool must be restricted to such documents (date filter or a pre-built per-date corpus); relying on the model's promise not to peek is not sufficient.
- Log every URL and document the agent touched for each name. A second pass checks each logged document's date; a run with any post-formation document is discarded for that name.
- Price, market cap and share count come from a point-in-time price store with corporate actions applied as of the formation date.

## Outcome measurement

- Outcome: 5-year total return (split, bonus and dividend adjusted) from the formation date, in INR. Delisted names use the last traded price or the resolution value, documented.
- Benchmark: Nifty Smallcap 250 Total Return Index for names below the Nifty 500 cutoff at the formation date; Nifty 500 TRI otherwise.
- Labels: `3x` (total return multiple >= 3.0), `loss` (multiple <= 0.5), `delisted`.

## Metrics to report

| Metric | Definition |
|---|---|
| Precision at YES | share of POTENTIAL MULTIBAGGER verdicts that reached 3x |
| Recall at YES | share of all 3x outcomes in the sample that received YES |
| False-positive rate | share of non-3x names that received YES |
| Severe-loss rate at YES | share of YES verdicts with multiple <= 0.5 or delisted |
| Calibration by score decile | mean 5-year multiple and 3x rate per decile of the 100-point score |
| Excess return at YES | median YES multiple minus the benchmark multiple over the same window |
| Baselines | the same metrics for (a) random selection, (b) a mechanical screen: 3y sales CAGR >= 15%, ROCE >= 15%, CFO/PAT >= 0.8, P/E below sector median |
| Coverage | share of names returning INSUFFICIENT EVIDENCE, by year |

Report every metric by formation year as well as pooled; a single pooled number hides regime dependence.

## Reporting template

```
Rubric commit: <hash>   Run date: <date>   Names scored: <n> (random <n_r>, forced failures <n_f>)
Survivorship: complete / partial (<what is missing>)
Information leaks found and discarded: <n>

                 YES   WATCH   UNLIKELY   INSUFFICIENT
count
3x rate
loss rate
median multiple
benchmark multiple

Precision at YES: x%   Recall: y%   FPR: z%   Severe-loss at YES: w%
Random baseline precision: a%   Mechanical-screen precision: b%
Calibration by decile: <table>
```

## What a result would and would not mean

A precision materially above both baselines across most formation years, with a severe-loss rate at YES no worse than the random baseline, would justify calling the rubric useful as a triage step. It would not justify calling any verdict a forecast. A result at or below the baselines means the thresholds should be revised or the skill should drop the score and keep only the checklist.

## Cost estimate

24 dates × roughly 30-35 names is 700-850 rubric runs, each needing a point-in-time document set. The corpus build is the main effort; the scoring runs are cheap once it exists.
