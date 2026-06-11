# Prediction of ICU Length of Stay Using Early Clinical Data

This repository contains the GitHub submission demo for our STATS 170B capstone
project. The project uses first-24-hour ICU features to demonstrate two related
prediction tasks:

- binary classification: `short` ICU stay versus `longer` ICU stay
- three-way classification: `short`, `medium`, or `long` ICU stay

The models were trained offline on local MIMIC-IV-derived features. MIMIC-IV
data is restricted and cannot be shared publicly, so this repository includes
saved fitted model artifacts, metadata, a small synthetic input sample, and a
runnable notebook. No real patient-level MIMIC-IV data is included.

## Files

- `project.ipynb`
  - Main runnable notebook. It loads the saved models from `models/saved/`,
    loads the synthetic demo data from `data/sample/`, computes predictions, and
    displays example evaluation plots.
- `project.html`
  - HTML export of `project.ipynb` with all outputs already shown.
- `requirements.txt`
  - Python packages needed to run the notebook.
- `data/sample/fake_icu_los_sample.csv`
  - Small synthetic dataset used only to demonstrate inference. It is fake data,
    not patient data.
- `models/saved/random_forest_short_stay_model_compressed.joblib`
  - Saved scikit-learn Pipeline for binary short-stay classification using a
    Random Forest classifier.
- `models/saved/logistic_regression_short_stay_model.joblib`
  - Saved scikit-learn Pipeline for binary short-stay classification using
    Logistic Regression.
- `models/saved/random_forest_three_class_los_model_compressed.joblib`
  - Saved scikit-learn Pipeline for three-way LOS classification using a Random
    Forest classifier.
- `models/saved/logistic_regression_three_class_los_model.joblib`
  - Saved scikit-learn Pipeline for three-way LOS classification using Logistic
    Regression.
- `models/saved/*_metadata.json`
  - Metadata files for each saved model, including target label, classes,
    feature columns, and offline train/test row counts.
- `source_code/`
  - Supporting preprocessing, modeling, visualization, and report code from the
    broader project. This folder is included for reference only; the runnable
    final submission is `project.ipynb` at the repository root.

## How to Run

Create an environment and install dependencies:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Run the notebook:

```bash
jupyter notebook project.ipynb
```

Then choose **Run All**.

You can also run it from the command line:

```bash
jupyter nbconvert --to notebook --execute project.ipynb --output project_rerun.ipynb --ExecutePreprocessor.timeout=60
```

Regenerate the HTML export:

```bash
jupyter nbconvert --to html project.ipynb --output project.html
```

The notebook is designed to run in under 1 minute because it loads saved models
instead of training them.

## Notes on Restricted Data

The full pipeline used MIMIC-IV tables from PhysioNet, including ICU stay,
admission, chart-event, lab-event, radiology-note, input/output-event,
prescription, and procedure-event data. Those files are not included because
they are restricted and too large for GitHub.

The fake CSV in this repository was hand-created from the model schema so that
reviewers can verify that the saved models load and produce predictions.
Both demo tasks use the same synthetic ICU rows: the binary label groups
three-way `medium` and `long` stays as `longer`.

The full feature-engineering and model-training pipeline was run offline on
restricted MIMIC-IV-derived data and is not included in this repository. This
GitHub submission is a runnable demonstration of the saved fitted models using
a small synthetic sample with the same feature schema.

The metrics shown in `project.ipynb` are computed only on the synthetic demo
rows. They are intended to verify that the saved models load, run, and produce
interpretable outputs; they should not be interpreted as held-out clinical
performance estimates. Final model evaluation and interpretation are reported
in the final project report.
