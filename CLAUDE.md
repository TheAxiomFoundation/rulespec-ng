# rulespec-ng Agent Notes

This repo stores Nigeria RuleSpec source registry materials, oracle references, and encoded policy rules. Individual income tax is federal law applied uniformly nationwide, so all encoded law lives under a single `ng/` national namespace (state internal revenue services administer collection but do not set the substantive rules encoded here).

## Scope

- `ng/statutes/`: Acts of the National Assembly — the Nigeria Tax Act, 2025 (which repealed the Personal Income Tax Act, Cap. P8 LFN 2004) and other primary law needed for tax-benefit modeling.
- `ng/regulations/`: subsidiary legislation and orders made under the governing Acts.
- `ng/policies/`: Nigeria Revenue Service administrative guidance, PAYE rate surfaces, and transfer-programme rules set administratively.
- `data/corpus/`: source inventory, ingestion notes, provision locators, and promoted official-source extracts.
- `data/coverage/`: tax-benefit coverage backlog and source map.
- `data/oracles/`: executable or documentary comparison references. These are never legal authority.

## Do

- Treat the scope as a Nigeria tax-benefit surface backed by Nigeria upstream law.
- Start from the furthest upstream available source: Official Gazette prints of Acts (Federal Government Printer, Lagos) first; Nigeria Revenue Service or state IRS rate tables and circulars only after the governing Act is identified.
- Add RuleSpec under `ng/statutes/`, `ng/regulations/`, or `ng/policies/` with companion `.test.yaml` files.
- Keep source law provenance in corpus artifacts and cite those corpus paths from RuleSpec modules via `module.source_verification.corpus_citation_path` (or the plural `corpus_citation_paths` for multi-provision modules).
- Use the current Nigerian year of assessment (2026, the first year under the Nigeria Tax Act, 2025) as the validation year for encoded amounts; amounts must be corpus-grounded, never invented.
- Keep exact oracle versions in `data/oracles/oracle-index.json` if a Nigeria household oracle is ever pinned. None exists today; see the README.
- Sync `axiom-encode` and `.axiom/toolchain.toml` before substantial encoding runs.

## Do not

- Use PAYE ready-reckoners, payroll-vendor summaries, or firm tax alerts as the first legal source when an Act governs the rule.
- Invent, round, or interpolate any Nigerian monetary amount, rate band, or relief figure. Every number must come verbatim from a captured official provision.
- Migrate any external calculator's code mechanically as RuleSpec.
- Add generated source payload dumps, formula artifacts, `parameters.yaml`, or standalone YAML fixtures outside allowed RuleSpec roots.
- Hand-copy statute text into RuleSpec without a corpus `citation_path`.
