# Reuse Guide

Use this repository as a starting point for a new demand-forecasting or cost-aware inventory case study. The public project root is the stable baseline; `Archive/` contains historical coursework and production iterations and is not part of the reusable core.

## Fast Start

1. Create a new branch or copy the repository before changing the current case study.
2. Replace the three local inputs described in [`data/README.md`](../data/README.md), keeping raw or restricted data out of Git.
3. Copy and rename [`notebooks/demand_forecasting_cost_aware_stocking.ipynb`](../notebooks/demand_forecasting_cost_aware_stocking.ipynb).
4. Update the notebook's scope, date split, SKU selection, features, cost assumptions, and strategy labels.
5. Run all cells from a clean kernel and review the saved outputs.
6. Export only the headline visuals needed for the new project's `figures/` folder.
7. Rewrite the README conclusions from the new evidence; do not carry forward numerical claims.

## Reusable Core

| Component | Reuse | Must be revalidated |
|---|---|---|
| Chronological train/test design | Time-series evaluation structure | Split date, leakage controls, seasonality coverage |
| ARIMA benchmark | Simple univariate baseline | Orders, convergence, and suitability for the new series |
| Prophet workflow | Feature-aware forecasting pattern | Regressors, holidays, tuning, and uncertainty behavior |
| MAE, RMSE, sMAPE | Forecast accuracy comparison | Metric aggregation level and business relevance |
| Diebold-Mariano and HAC comparisons | Statistical comparison pattern | Loss definition, lag choice, pairing, and sample size |
| Newsvendor critical fractile | Translate asymmetric costs into a target quantile | Underage/overage costs and all assumptions behind them |
| Cost-sensitivity analysis | Test decision robustness | Scenario ranges and operational plausibility |

## Decision Rule

Call this template when the new problem has chronological demand data, a forecast decision, and asymmetric over/under costs. Do not treat it as a complete replenishment system unless the new data also include inventory positions, order quantities, lead times, ordering constraints, and waste or disposal outcomes.

Minimum evidence before recommending a policy:

- a leakage-safe holdout;
- at least one credible baseline;
- forecast metrics at the decision-relevant aggregation level;
- explicit cost assumptions and sensitivity checks;
- uncertainty or statistical comparison when strategies are close;
- clear separation between scenario-based penalties and audited financial impact.

Stop and redesign the analysis if observed sales are a poor proxy for demand, stockouts censor the target, future regressors are unavailable at forecast time, or operational constraints dominate the simple quantile decision.

## Folder Roles

```text
data/        Local inputs plus a public manifest; CSV inputs remain Git-ignored
notebooks/   Executed, reviewable analysis
figures/     Headline result visuals only
docs/        Reuse instructions and work records
Archive/     Local-only process history, earlier versions, source data, and submissions
```

## Before Publishing a Derived Project

- Remove personal, institutional, secret, and machine-specific information.
- Confirm data redistribution rights; publish a manifest and checksums when inputs cannot be shared.
- Keep only the strongest executed notebook and a small set of result visuals.
- Check every README claim against the final notebook outputs.
- Confirm a clean Git status and inspect exactly which files are tracked before pushing.

## Local Continuation Notes

- The existing `.venv/` is retained for a fast local restart but is not portable or tracked. Rebuild it from `requirements.txt` if it fails or if the Python version changes.
- `Archive/README.md` is the map for historical materials.
- The public repository is the source of truth for the portfolio version; archived copies are evidence and recovery material, not preferred working files.
