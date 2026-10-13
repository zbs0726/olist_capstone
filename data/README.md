# Data Source and Local Setup

## Source

This project uses the Brazilian E-Commerce Public Dataset by Olist:

https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

Download and extract the dataset from the source page. A Kaggle account
may be required. Follow the source's licence and access conditions.

Raw and merged transactional CSV files are not included in this
repository. They are stored locally and reconstructed using the
merge notebook.

## Required local files

Create a `data/raw/` folder under the project root and place these nine
CSV files directly inside it, preserving their original filenames:

```text
data/raw/olist_customers_dataset.csv
data/raw/olist_geolocation_dataset.csv
data/raw/olist_order_items_dataset.csv
data/raw/olist_order_payments_dataset.csv
data/raw/olist_order_reviews_dataset.csv
data/raw/olist_orders_dataset.csv
data/raw/olist_products_dataset.csv
data/raw/olist_sellers_dataset.csv
data/raw/product_category_name_translation.csv
```

Do not place the CSV files inside an additional nested download folder.

## Execution order

1. Run `notebooks/01_merge.ipynb` from beginning to end.
2. Run `notebooks/02_milestone2_analysis.ipynb` from beginning to end.

The merge notebook creates `data/derived/olist_orders_merged.csv`,
`data/derived/merged_column_inventory.csv`, and
`data/derived/source_manifest.csv`.

The analysis notebook reads the merged dataset and column inventory.
Both notebooks export supporting tables to `outputs/tables/`.
The analysis notebook exports figures to `figures/`.

The merged dataset is an output of the merge workflow; it does not
need to be downloaded separately.

## Input verification and limitations

The project inputs contain 99,441 orders. The merge notebook records
source filenames, row counts, and SHA-256 hashes in the source manifest
and checks keys, joins, and aggregate totals.

The exact upstream release version and original download date have
not been documented. A later source download may differ from the
files used for this submission. Compare its source manifest with
the submission manifest when checking reproducibility.

Missing reviews represent unobserved satisfaction. The delivered
and reviewed analytical cohort does not represent all marketplace
orders or all customers.
