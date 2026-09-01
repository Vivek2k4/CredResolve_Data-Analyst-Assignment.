# CredResolve_Data-Analyst-Assignment.

Collections recovery forensics

This repository answers whether a reported month-on-month recovery improvement is real, using the supplied synthetic collections data.

For the last complete month (July 2026), the answer depends materially on definition:

| Measure | July vs June |
|---|---:|
| Raw successful cash / targeted account | +4.0% |
| Deduplicated successful cash / targeted account | -3.3% |
| Strict post-target cash / targeted account | +13.1% |
| DPD-standardised strict post-target cash / targeted account | +12.7% |

Therefore, a generic claim of “11% recovery improvement” is not independently verifiable without its metric definition and attribution rules.

## Repository map

```text
data/raw/                 Supplied source files (unchanged; ignored from source control)
data/golden/              Reproducible analytical tables created by the pipeline
sql/                      Equivalent production-oriented SQL transformations
notebooks/analysis.ipynb  Walkthrough notebook
outputs/                  Auditable monthly, segment and quality result tables, One-screen executive dashboard
reports/                  Executive memo, data-quality report and architecture
```

## Metric definitions

- **Targeted account:** a distinct account with at least one daily-targeting record in the calendar month.
- **Strict post-target recovery:** successful, payment-reference-deduplicated cash received for a targeted account on or after its first target date in the same month. This is a cohort metric, not proof that the target caused payment.
- **Payment conversion:** targeted accounts with at least one strict post-target payment / targeted accounts.
- **DPD-standardised recovery:** strict post-target recovery per targeted account, reweighted to January's DPD distribution. It removes one observable mix effect; it is not causal.
- **Last complete month:** July 2026. Source payments and targeting end on 8 August, so August is excluded from month-on-month decisions.

## Important limitations

There is no historical monthly balance snapshot, interaction cost ledger, reliable campaign-control population, or timezone on payments/targeting. The repository makes these limitations visible rather than concealing them with a single headline number.
