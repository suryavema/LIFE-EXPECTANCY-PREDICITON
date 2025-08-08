# Life Expectancy Prediction (Regression, Python)

Predict a country's **life expectancy** from WHO socio‑economic & health indicators using regression models.
This repo contains exploratory visualizations and a prediction notebook.

> ⚠️ **Note**: This is an academic project. Do not use the model for public‑policy or clinical decisions.

## Dataset
- `LifeExpectancyData.csv` — WHO/Kaggle dataset with features like *GDP, AdultMortality, BMI, Immunization rates,* etc.
  - Target column: `Life expectancy` (years).

## Project Files
- `LEpredictor.ipynb` — data cleaning, feature engineering, model training & evaluation.
- `Visualization.ipynb` — EDA plots (pair plots, trend lines, correlations, country‑specific views).
- `LIFE EXPECTANCY PREDICITON.pdf` — short report.
- `README.md` — this file.

## Getting Started

### 1) Environment
```bash
python -V                 # Python 3.9+ recommended
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

pip install -U pip
pip install -r requirements.txt
```

### 2) Explore the data & run models
```bash
jupyter lab
```
Open **`Visualization.ipynb`** to explore the dataset, then **`LEpredictor.ipynb`** to run the models.

### 3) Typical workflow inside `LEpredictor.ipynb`
1. Load and clean data (drop/impute NA, cast numeric types).
2. Split train/test with `train_test_split` (stratify by `Status` or use random split).
3. Scale/transform when needed (optional).
4. Train baseline **Linear Regression**; record **MAE / RMSE / R²**.
5. Try **Ridge/Lasso/ElasticNet** and **PolynomialFeatures + LinearRegression** (degree tuning).
6. Cross‑validate and compare metrics.
7. Inspect coefficients / feature importances and residual plots.
8. Save the best model and preprocessing with `joblib` (optional).

### 4) Saving and reusing a model (optional)
Inside the notebook after training:
```python
from joblib import dump, load
dump(best_model, "lifeexp_model.joblib")
# later
model = load("lifeexp_model.joblib")
```
If you used encoders/scalers, save them too and reuse the *same* pipeline at inference time.

## Project Structure
```
.
├─ LifeExpectancyData.csv
├─ LEpredictor.ipynb
├─ Visualization.ipynb
├─ LIFE EXPECTANCY PREDICITON.pdf
├─ requirements.txt
└─ README.md
```

## Evaluation
Report **MAE, RMSE, and R²** on the test split. Keep a small results table in the notebook comparing models
(e.g., Linear vs Ridge vs Lasso vs Polynomial). Add residual plots to check bias/variance patterns.

## Reproducibility tips
- Fix random seeds (`random_state=42`) for splits and models.
- Document any rows dropped or imputation strategies.
- Keep country/year filters (if any) in a config cell so results are repeatable.


## Next Steps
- Move the final training code into a `train.py` and inference into a `predict.py` CLI.
- Add a small **Streamlit**/**Gradio** app for interactive predictions.
- Add **k‑fold cross‑validation** and a simple **model selection** report.
- Use **Permutation Importance**/**SHAP** to explain predictions.
- Publish `Visualization.ipynb` as static HTML under `docs/` for easy viewing.

