# Kearl Lake Metal Exceedance Prediction Using Machine Learning

A DATA 443 team project exploring whether water-quality measurements and sampling conditions can predict metal guideline exceedances at Kearl Lake.

**Contributors:** Anna Phan, Morsal Nory, Muntaha Al-Taie, and Saif Farag.

## Project overview

The notebook compares logistic regression and random forest classifiers for mercury, methylmercury, lead, vanadium, and a combined exceedance target. Targets with only one observed class are skipped. This is an exploratory course project, not a validated environmental compliance or early-warning system.

## Methods and tools

- Python, pandas, and NumPy for data cleaning and preparation.
- Timestamp parsing, numeric conversion, and guideline-based target construction.
- scikit-learn for logistic regression and a 300-tree random forest, with balanced class weights.
- An 80/20 train/test split, stratified when possible.
- Accuracy, precision, recall, F1, ROC-AUC, classification reports, and confusion matrices.
- Matplotlib for ROC curves and feature-importance visualizations.

## Files

- [`kearl_lake_ml.ipynb`](kearl_lake_ml.ipynb): the original supplied project notebook, preserved without analytical changes.
- `requirements.txt`: packages needed to open and run the notebook; versions are not pinned because the original environment was not supplied.

## Running locally

Requires Python 3 and the original `KEARL.csv` input. Place that CSV beside the notebook. It must retain the original structure: metadata in the first row and column names in the second row. The notebook loads it with `header=None` and uses row index 1 as the header.

```bash
python -m venv .venv
source .venv/bin/activate
# Windows: .venv\Scripts\activate
python -m pip install -r requirements.txt
jupyter lab kearl_lake_ml.ipynb
```

Run cells from top to bottom. The input CSV is not included in this upload; obtain the original project dataset and verify its source and redistribution terms before adding it. A fresh execution has not been verified for this repository update.

## Results and limitations

The notebook retains its original outputs and discussion for transparency. Performance numbers should be treated as historical, exploratory results pending review and rerun. In particular:

- The random forest F1 print statement currently uses logistic-regression predictions (`y_pred_lr`) instead of `y_pred_rf`; the summary table therefore needs reconciliation with the classification reports.
- Median imputation occurs before the train/test split. A stronger evaluation would fit preprocessing on training data only, using a pipeline.
- Missing metal measurements currently become non-exceedance labels through comparison logic. Missing targets should be distinguished from observed non-exceedances.
- Detection-limit symbols are removed during numeric conversion. Censored observations need explicit handling and interpretation.
- Rare positive cases make performance estimates unstable. Related metal measurements and repeated sampling also require careful leakage checks and temporally appropriate validation.
- The plotting calls assume that the selected targets returned fitted models; a dataset with insufficient classes may require additional guards.

These issues are documented rather than silently changing the submitted coursework. Before making substantive performance claims, correct the evaluation, rerun against the original data, and update the saved outputs and discussion together.
