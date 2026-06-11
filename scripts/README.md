## Offline Supporting Scripts

This folder contains a trimmed set of scripts from the broader project workflow.
They document the main preprocessing, modeling, and visualization steps used
offline during development.

These scripts are provided for reference only. They require restricted
MIMIC-IV-derived files under `data/raw/` and intermediate feature files under
`data/processed/`, which are not included in this repository. The runnable
GitHub submission is the root-level `project.ipynb`, which loads saved fitted
models and a small synthetic sample.

Some offline scripts require additional packages beyond the notebook demo
environment, including `duckdb`, `seaborn`, and `lifelines`.

The retained scripts are organized as:

- `preprocessing/`: first-24-hour feature builders for chart, lab, input,
  output, prescription, and procedure event data.
- `models/`: baseline, binary short-stay, three-way LOS, radiology-feature, and
  Cox survival modeling scripts.
- `visualizations/`: selected scripts for model comparison, confusion matrices,
  feature importance, and Cox-model figures.
