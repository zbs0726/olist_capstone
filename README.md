# E-Commerce Customer Satisfaction
## An Operational Analysis of Order Fulfillment

This capstone project uses historical Olist marketplace data to examine
how fulfilment conditions and order characteristics are associated with
customer dissatisfaction.

The intended audience is marketplace operations managers. The project
supports periodic prioritisation of processes and order segments for
investigation or pilot testing. It does not estimate causal intervention
effects or provide early-warning predictions at order placement.

## Milestone 2 Scope

The current notebooks document:

- Integration of nine source tables into an order-level dataset.
- Cohort construction and the selected-review outcome.
- Data quality, missingness, timestamp anomalies, and measurement checks.
- Dependence across customers, sellers, products, regions, and periods.
- Exploratory comparisons and review-timing sensitivity.
- Proposed leakage controls, validation logic, and baseline strategy.

One analytical row represents one order. Dissatisfaction is defined
as a selected review score of 1 or 2.

The supplied data contain 99,441 orders. The preliminary delivered
and reviewed cohort contains 95,832 orders, including 12,273 low-score
orders (12.81%).

Predictive baseline implementation remains pending in the current
repository. Final model selection, tuning, validation, and intervention
evaluation are reserved for later work.

## Repository Organisation

| Path | Purpose |
| --- | --- |
| `notebooks/01_merge.ipynb` | Source loading, join checks, aggregation, feature derivation, and merged-data export |
| `notebooks/02_milestone2_analysis.ipynb` | Cohort diagnostics, exploratory tables and figures, and analytical plans |
| `requirements.txt` | Python package versions recorded from the working environment |
| `data/README.md` | Data source, access instructions, and expected local filenames |
| `.gitignore` | Python environment and temporary-file exclusions |
| `data/raw/` | Local source CSV files; not included in the repository |
| `data/derived/` | Locally generated merged data and inventories |
| `outputs/tables/` | Generated audit and analysis tables |
| `figures/` | Generated analysis figures |

## Data Access

The source is the Brazilian E-Commerce Public Dataset by Olist:

https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

Download and extract the nine CSV files into `data/raw/`, preserving
their original filenames. See [data setup instructions](data/README.md)
for the complete file list.

Raw and merged transactional data are not uploaded to this repository.

## Environment Setup

Use a Python environment compatible with the package versions in
`requirements.txt`.

From the project root, install the dependencies:

```bash
python -m pip install -r requirements.txt
```

To open the notebooks with JupyterLab, install and launch it in the
same environment:

```bash
python -m pip install jupyterlab
python -m jupyterlab
```

Select the Python kernel associated with that environment.

## Execution Order

1. Prepare the source files in `data/raw/`.
2. Open `notebooks/01_merge.ipynb`.
3. Select **Restart Kernel → Run All**, allow execution to finish,
   and save the notebook.
4. Open `notebooks/02_milestone2_analysis.ipynb`.
5. Select **Restart Kernel → Run All**, allow execution to finish,
   and save the notebook.

The merge notebook must run first. It generates:

- `data/derived/olist_orders_merged.csv`
- `data/derived/merged_column_inventory.csv`
- `data/derived/source_manifest.csv`

The analysis notebook reads these derived inputs independently of the
merge notebook's kernel state. Supporting tables and figures are
generated locally.

Open Jupyter from the project root and retain the documented folder
structure so that relative paths resolve correctly.

## Reproducibility and Analytical Limitations

- The exact upstream dataset release and original download date are
  not documented. A later download may differ from the submission
  inputs. Source manifests record filenames, row counts, and hashes.
- The outcome cohort includes delivered orders with valid selected
  reviews. Missing reviews do not indicate satisfied customers.
- Some orders have multiple reviews. A deterministic latest-review
  rule selects the provisional outcome.
- Reviews may precede delivery. Full-cohort and post-delivery-review
  comparisons represent different populations.
- Orders can share customers, sellers, products, and operational
  context; they should not automatically be treated as independent.
- ZIP-based distance is approximate and is not delivery-route length.
- Exploratory associations do not establish causal effects.
- Full-period exploratory analysis has already been conducted.
  Later internal evaluation will document this prior exposure.

## Submission Version

The Milestone 2 submission will identify this repository URL and the
exact final commit hash or release tag. The repository may continue
to change after submission; the submitted version is the grading
reference.
