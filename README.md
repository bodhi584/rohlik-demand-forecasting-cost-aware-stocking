# Demand Forecasting and Cost-Aware Stocking

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bodhi584/rohlik-demand-forecasting-cost-aware-stocking/blob/main/notebooks/demand_forecasting_cost_aware_stocking.ipynb)

[Notebook](notebooks/demand_forecasting_cost_aware_stocking.ipynb) · [Data notes](data/README.md) · [Reproduce](#reproduce-the-analysis)

**An end-to-end forecasting and decision-support case study for perishable e-grocery.**

This project uses public Rohlik e-grocery sales data to test a practical question: can a better demand forecast, paired with an explicit cost model, support better stocking decisions for perishable products?

The work moves from data audit and time-series forecasting to newsvendor quantile policies, financial-loss comparison, statistical uncertainty, and sensitivity analysis. It is designed as a reproducible portfolio case study rather than a claim about Rohlik's actual inventory operations.

> **Headline outcome:** Prophet improved out-of-sample forecast accuracy over ARIMA. Under Base ESG assumptions, cost-aware Prophet policies lowered estimated penalty by about 20% relative to ARIMA, while statistical testing did not support declaring 63.3% or 67.2% the definitive winner.

![Financial loss by forecast-based strategy](figures/financial_loss_by_strategy.png)

## At a Glance

| | |
|---|---|
| **Business problem** | Balance lost-margin risk from under-forecasting against spoilage risk from over-forecasting |
| **Analytical scope** | 10 high-volume perishable SKUs at Prague_1; 154-day out-of-sample test period |
| **Forecasting models** | ARIMA benchmark and Prophet with holiday and discount regressors |
| **Decision policies** | Prophet 50% neutral forecast plus 67.2% commercial and 63.3% ESG target quantiles |
| **Validation** | MAE, RMSE, sMAPE, Diebold-Mariano testing, paired HAC confidence intervals, and cost sensitivity analysis |
| **Tools** | Python, pandas, Prophet, statsmodels, scikit-learn, SciPy, Matplotlib, Seaborn |

## Project Components

- Audited and prepared Rohlik's public sales data for ten fast-moving perishable SKUs.
- Designed a strict chronological split: training through 31 December 2023 and testing from 1 January to 2 June 2024.
- Built a sales-only ARIMA benchmark and a feature-aware Prophet model using holidays and discounts.
- Converted under-forecast and over-forecast costs into transparent newsvendor target quantiles.
- Compared neutral and cost-aware strategies under the same 154-day evaluation window.
- Added statistical testing so small numerical differences are not overstated as meaningful wins.
- Stress-tested the conclusion across four alternative cost structures.

## Results

### 1. Prophet provides the stronger forecasting base

On the held-out period, Prophet 50% reduced MAE from `18,359.92` to `14,332.64` and RMSE from `23,736.95` to `19,636.67`. Its sMAPE was `8.11%`, compared with `10.26%` for ARIMA.

![Out-of-sample forecast accuracy](figures/forecast_accuracy.png)

### 2. Cost-aware policies improve the scenario-based decision result

Under the Base ESG assumptions, estimated total penalty fell from `EUR 6.59M` for ARIMA and `EUR 5.58M` for Prophet 50% to:

- `EUR 5.33M` for Prophet Profit Max at the 67.2% target quantile.
- `EUR 5.28M` for Prophet ESG at the 63.3% target quantile.

The ESG policy is numerically lowest in this scenario, about 20% below ARIMA. However, the paired HAC 95% confidence interval for the difference between the two tuned policies includes zero (`EUR -59K` to `EUR 164K`). The defensible conclusion is therefore that the tuned policies perform similarly under Base ESG costs; the evidence does not establish a decisive winner between 63.3% and 67.2%.

### 3. The broad conclusion survives alternative cost assumptions

All Prophet strategies remain below ARIMA in each of the four tested scenarios. The best Prophet policy changes as the under-forecast and over-forecast penalties change, which is the expected newsvendor behavior: the preferred target quantile depends on the cost ratio.

![Sensitivity analysis across four cost scenarios](figures/cost_sensitivity.png)

## Decision Interpretation

The 50%, 63.3%, and 67.2% values are **target forecast quantiles representing stocking policies**. They are not service-level measurements, reorder points, or replenishment timing rules.

The analysis answers a bounded decision question: under a shared set of cost assumptions, which forecast-based stocking policy produces the lowest estimated penalty? It does not determine when an order should be placed or reconstruct actual inventory movements.

## Repository

```text
.
├── data/                  # Reproducible analysis inputs
├── figures/               # Portfolio-ready result visuals
├── notebooks/             # Complete analysis with saved outputs
├── README.md
└── requirements.txt
```

### Main deliverables

- [Run or review the complete notebook](notebooks/demand_forecasting_cost_aware_stocking.ipynb)
- [Review the data dictionary and scope](data/README.md)

## Reproduce the Analysis

The fastest route is the **Open in Colab** button at the top of this page. The notebook contains saved outputs, so it can also be reviewed without rerunning every model.

In Colab, run the notebook from the top and upload the three files from `data/` when prompted:

1. `rohlik_model_ready.csv`
2. `inventory.csv`
3. `sales_train_prague1.csv`

For a local run, use Python 3.10 or 3.11 and install the dependencies:

```bash
pip install -r requirements.txt
jupyter notebook notebooks/demand_forecasting_cost_aware_stocking.ipynb
```

## Data and Scope

Source: [Rohlik Sales Forecasting Challenge V2](https://www.kaggle.com/competitions/rohlik-sales-forecasting-challenge-v2).

The public data include sales history and product/context features, but not on-hand inventory, order quantities, replenishment lead times, disposal records, or internal accounting costs. Consequently, the financial values in this project are **scenario-based penalties for comparing forecast policies**, not audited losses or a reconstruction of Rohlik's operations.

## Skills Demonstrated

- Business problem framing and data-scope auditing
- Time-series feature engineering and chronological validation
- ARIMA and Prophet model development
- Forecast accuracy and statistical comparison
- Newsvendor critical-fractile decision modeling
- Asymmetric cost evaluation and sensitivity analysis
- Clear communication of uncertainty and operational limits

## References

The notebook documents the methods and references used, including Rohlik's public dataset, the newsvendor framework, Prophet, forecast-accuracy measures, Diebold-Mariano testing, and HAC inference.
