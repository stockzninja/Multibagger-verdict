# Changelog

## v1.1 (unreleased)

Hardening pass: make the skill's claims checkable and its gaps visible.

- **Required-inputs schema** (`references/inputs.md`): every field the rubric needs, mandatory or optional, acceptable source type, and the action when missing. Missing mandatory fields now stop at INSUFFICIENT EVIDENCE with the fields named. The skill states that it retrieves no data and must be paired with a filings/market-data tool.
- **Source and number tags**: every figure carries `[F]`, `[M]`, `[U]` or `[A]`; a URL may appear only if retrieved in the session, otherwise `[document type, date, not retrieved]`.
- **Scenario math before scoring**: the bear/base/bull table is built first from tagged inputs, and the 15-point valuation pillar is assigned by a fixed mapping from the resulting multiples, with a cap when the bull case relies on re-rating. The YES rule now references the mapped pillar.
- **Validation protocol** (`references/evaluation.md`): point-in-time formation dates 2010–2021, random sample plus forced inclusion of delisted and severe-loss names, document-date discipline, outcome labels, metrics, baselines and a reporting template. README gains a results table that reads "Not yet run".
- **Negative cases** (`references/rubric.md`): four Indian companies that later failed, each with a pre-failure as-of date, the public documents available then, the rubric walked through, and the rule that should have caught it.
- **Reporting basis**: one paragraph on consolidated vs standalone; never mixed, stated in the header.
- **Housekeeping**: install command now names this repository; MIT license added; maintainer named; "framework" replaced by "research checklist" where a predictive claim could be read in.
- **Investor names** moved from `SKILL.md` and the README opening to a footnote in `references/research.md`; the underlying ideas stay inside the pillar descriptions.
- Example output updated to the new format.

## v1.0

Initial release.
