# Data Files

These files are the minimum data inputs required to reproduce the notebook:

- `rohlik_model_ready.csv`: cleaned modeling table used for forecasting.
- `inventory.csv`: product metadata used to verify Prague_1 SKU categories.
- `sales_train_prague1.csv`: Prague_1-only sales history subset used to reproduce selected SKU rankings.

The original public dataset does not include true inventory positions, order quantities, lead times, disposal records, or internal accounting costs. The project therefore evaluates forecast-based stocking policies under stated assumptions rather than actual operational losses.
