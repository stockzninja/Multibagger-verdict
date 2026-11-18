# Contributing to Multibagger Verdict

Contributions are welcome, especially improvements that make the analysis more reproducible and less susceptible to hindsight bias.

## Good contributions

- Cite original, dated filings for any claims about stocks or investment frameworks.
- Add sector-specific accounting checks with a clear rationale.
- Add point-in-time test cases including unsuccessful and delisted companies.
- Document false positives, ambiguity and missing-data handling.
- Propose rubric changes with holdout evidence, not only famous winners; run the four negative cases in `references/rubric.md` and report whether any turns into a YES.
- Help run the protocol in `references/evaluation.md`: a point-in-time document corpus for NSE formation dates is the main missing piece.

## Please avoid

- Claims of guaranteed returns or arbitrary probability estimates.
- Calling a historical winner a successful backtest without period-correct data.
- Sharing proprietary paid datasets or confidential company information.
- Presenting unverified allegations as findings.

For substantive changes, describe the problem, evidence, proposed rubric adjustment, and likely failure cases.
