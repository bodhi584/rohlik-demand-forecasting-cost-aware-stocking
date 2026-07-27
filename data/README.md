# Data Manifest

The analysis uses data derived from the [Rohlik Sales Forecasting Challenge V2](https://www.kaggle.com/competitions/rohlik-sales-forecasting-challenge-v2). The competition page marks the dataset as subject to its competition rules, so the CSV inputs are intentionally not redistributed here.

## Required Local Inputs

Place these files in this directory for a local run, or upload them in the same order when prompted in Colab:

| File | Purpose | Expected shape |
|---|---|---:|
| `rohlik_model_ready.csv` | Ten selected Prague_1 SKU histories with modeling features | 13,958 rows, 10 columns |
| `inventory.csv` | Product and category metadata from the competition download | 5,432 rows, 8 columns |
| `sales_train_prague1.csv` | Prague_1 subset used to audit SKU sales rankings | 780,566 rows, 4 columns |

Checksums for validating an existing local copy:

```text
e1ada9e6d5af544e1ccefd7e8ef2785a78ad7784e783c4b25811a909ca7e966b  inventory.csv
45e434bf603831aadee9bba2c4d24578ed706432fab5f692f18c1495e0023104  rohlik_model_ready.csv
d6a0f4dccd578af0dc7763a2c0db252d84fb087a0f55f8d1423e853174726b8b  sales_train_prague1.csv
```

Expected schemas:

```text
rohlik_model_ready.csv
unique_id,date,warehouse,sales,sell_price_main,availability,holiday,holiday_name,day_name,total_discount

inventory.csv
unique_id,product_unique_id,name,L1_category_name_en,L2_category_name_en,L3_category_name_en,L4_category_name_en,warehouse

sales_train_prague1.csv
unique_id,date,warehouse,sales
```

The model-ready file covers the selected identifiers `525, 652, 2159, 2562, 2937, 3144, 3616, 4228, 4879, 4885` from `2020-08-01` through `2024-06-02`. The Prague_1 subset is produced by filtering the competition's `sales_train.csv` to `warehouse == "Prague_1"` and retaining `unique_id`, `date`, `warehouse`, and `sales`.

## Scope Boundary

The source dataset does not contain true inventory positions, order quantities, replenishment lead times, disposal records, or internal accounting costs. This project therefore evaluates forecast-based stocking policies under stated assumptions rather than actual operational losses.
