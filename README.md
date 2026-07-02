# ISSB Climate Disclosure Analyzer (IFRS S2)

A Claude Skill for systematic climate disclosure analysis based on IFRS S2 *Climate-related Disclosures* (June 2023).

## What It Does

1. **Compliance Assessment** — Evaluates corporate climate reports against all 96 sub-clauses of IFRS S2 (ID-001 to ID-096), with granular scoring by clause type (quantitative / process / strategic / target).
2. **Investment Usefulness** — Maps disclosure quality to 12 investment model variables (revenue, COGS, WACC, terminal value, asset impairment, etc.) and assesses whether the information provides predictive increment, confirmation, or is boilerplate.
3. **Transition Plan Quality** — Synthesizes 7 dimensions (target science, action pathway, resource allocation, dependencies, governance accountability, progress tracking, carbon credit reliance) from dispersed S2 clauses into an investor-ready view.
4. **Industry-Specific Analysis** — Loads sector modules to identify the most material climate variables, frequently triggered clauses, common scoring pitfalls, and best-practice patterns for 6 industries.

## File Structure

```
issb-climate-disclosure-analyzer/
├── SKILL.md                                     # Core workflow (start here)
├── README.md                                    # This file
│
├── references/
│   ├── s2_evaluation_framework.md              # 96 sub-clauses (ID-001 to ID-096)
│   ├── best_practices.md                       # Benchmark library (12 companies)
│   ├── scoring_edge_cases.md                   # 12 high-frequency scoring pitfall rules
│   ├── evidence_schema.md                      # evidence_status / disclosure_type / standard_version definitions
│   ├── s2_version_notes.md                     # S2 version notes and jurisdiction overlay placeholders
│   └── sectors/
│       ├── sector_mining_metals.md             # Mining & Metals
│       ├── sector_financial_institutions.md    # Banks, Insurance, Asset Management
│       ├── sector_power_utilities.md           # Power & Utilities
│       ├── sector_oil_gas_chemicals.md         # Oil, Gas & Chemicals
│       ├── sector_cloud_ai_data_centers.md     # Cloud, AI & Data Centers
│       └── sector_consumer_goods_agri_food.md  # Consumer Goods, Agri-food
│
├── examples/
│   ├── diagnostic_example_full.md              # Full 96-clause diagnostic report template
│   └── diagnostic_example_short.md             # Abbreviated report template
│
├── evals/
│   ├── self-check.md                           # Output quality checklist (60+ items)
│   └── clause_count_test.md                    # 6 automated clause count validations
│
└── outputs/
    └── scorecard_schema.json                   # Structured JSON output schema (96 clauses + 12 variables + 7 dimensions)
```

## Key Design Decisions

### Scoring by Clause Type
Not all S2 clauses are created equal. The skill uses four scoring rubrics:
- **Quantitative** (metrics, financials): scored on whether actual numbers, amounts, or percentages are disclosed
- **Process/Governance** (oversight, risk management): scored on specificity of evidence (frequency, skills matrix, committee agendas)
- **Strategic/Resilience** (risk identification, business impact, scenarios): scored on whether financial transmission pathways are established
- **Target/Progress** (goals, tracking): scored on completeness of target parameters (base year, timeline, periodic tracking)

### Scoring Edge Cases
12 rules address the most common false-positive pitfalls discovered during testing — for example, "TCFD four-pillar completeness ≠ IFRS S2 compliance" and "external scenario carbon price ≠ internal carbon pricing."

### Anti-Circular Benchmarking
When the assessed company appears in the benchmark library (e.g. Zijin Mining, Microsoft), improvement recommendations automatically exclude that company's own practices.

### Red Flag Mechanism
Five conditions trigger mandatory red-flag annotations: undisclosed Scope 3 in value-chain-heavy industries, net-zero targets without capital allocation, scenario analysis without financial quantification, transition plans without resource commitment, and opaque carbon credit reliance with aggressive targets.

### Sector Modules
Each sector module answers exactly five questions: (1) most material climate risks/opportunities, (2) most frequently triggered S2 clauses, (3) most critical investment-useful metrics, (4) common scoring pitfalls, and (5) recommended best-practice patterns.

## Version

- Assessment standard: IFRS S2 Climate-related Disclosures (June 2023)
- Default version code: `IFRS_S2_2023_base`
- GHG amendments (2025) and jurisdiction overlays (HKEX, A-shares, CSRD, SEC, AASB, SSBJ) are placeholders for future extension

## Usage

Upload or provide a corporate climate/sustainability/ESG report and ask for an IFRS S2 analysis. The skill handles both full diagnostic mode (96-clause table) and abbreviated mode.

## Roadmap

- [ ] Jurisdiction overlays (HKEX, A-shares, CSRD, SEC, AASB, SSBJ mapping)
- [ ] Investor summary template (which gaps truly affect valuation / cost of capital / financing / impairment)
- [ ] Additional sector modules: Transport/Shipping/Logistics, Real Estate/Construction
- [ ] Eval cases: Zijin Mining TCFD-to-S2 readiness test sample
- [ ] Best-practice library: structured metadata upgrade (source_page, evidence_excerpt per entry)
- [ ] Best-practice library: sector-specific sub-files (banks, cloud/AI, mining, consumer goods)
