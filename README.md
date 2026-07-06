# rulespec-ng

Nigeria RuleSpec source registry.

This repository targets a Nigeria tax-benefit surface: individual income tax under the Nigeria Tax Act, 2025 (which consolidated Nigeria's tax statutes and repealed the Personal Income Tax Act, Cap. P8 LFN 2004, with effect for the 2026 year of assessment), the eligible deductions that determine chargeable income, and in later batches the social contributions and transfer programmes needed for household-level calculations.

Individual income tax in Nigeria is federal law applied uniformly nationwide (the Fourth Schedule rates and section 30 deductions are set by the Act), while collection is administered by state internal revenue services under the Nigeria Tax Administration Act, 2025. Encoded law therefore lives under a single `ng/` national namespace; a state layer would only be added if state-level substantive rules (not administration) enter scope.

The first encoded slice is the individual income-tax rate schedule (Fourth Schedule to the Act, charged by section 58) and the rent relief within section 30's eligible deductions.

## Source priority

Policy must come from the furthest upstream available source.

1. Federal Republic of Nigeria Official Gazette prints of Acts (Federal Government Printer, Lagos) — the authentic text of the Nigeria Tax Act, 2025 and later amending Acts.
2. Nigeria Revenue Service (and, for state-administered PAYE surfaces, state internal revenue service) rate tables, guides, and information circulars only after the governing Act is identified.
3. Official programme documentation for transfer programmes set administratively rather than by Act.
4. Oracles only for household-level parity tests against an external calculator that can compute the same household case, never as law.

## Oracle scope

An oracle is an executable, pinned external calculator that accepts household-level inputs and returns household-level tax-benefit outputs comparable to Axiom outputs. Aggregate simulators, distributional reports, parameter documentation, and public model summaries are not oracles for RuleSpec parity, even when they are useful as background references.

**No Nigeria household oracle is currently attached, and none is publicly distributed.** Nigeria is not a SOUTHMOD country, and no EUROMOD-platform Nigeria model is publicly available. `data/oracles/oracle-index.json` records the empty registry and candidate surfaces to watch (research models built with the Nigerian Living Standards Survey; any future TaxDev or UNU-WIDER Nigeria model). Until an oracle attaches, this repo encodes source-first from the gazette Acts, with oracle parity tests deferred.

## Layout

- `ng/statutes/`: Nigeria primary law encoded as RuleSpec (Acts of the National Assembly).
- `ng/regulations/`: subsidiary legislation and orders made under the governing Acts.
- `ng/policies/`: Nigeria Revenue Service administrative guidance and rate surfaces, and transfer-programme rules set administratively.
- `data/corpus/`: source inventory, ingestion manifests, provision locators, and promoted official extracts.
- `data/coverage/`: tax-benefit coverage backlog and official source map.
- `data/oracles/`: pinned household-level comparison references (none yet; see Oracle scope).

Durable ids use `ng:<path>#<rule>` for national rules.

## Money proof-atom coverage

Every policy-bearing monetary value — currency parameters, currency parameter-table cells, and currency literals in derived formulas — must carry a proof atom whose source cites a provision. The shared `validate-rulespec` workflow enforces this with `axiom-encode proof-validate --money-atoms-only`, reading the repo-root ratchet `known-missing-money-atoms.yaml`.

`known-missing-money-atoms.yaml` is seeded at `total_allowed: 0`: because the repo starts with no encoded monetary values, there is no backlog to burn down, and CI enforces a strict zero allowance from the first encoded module onward. Every monetary value added by encoding must ship with a proof atom citing a Nigeria provision. This floor may only be lowered, never raised.
