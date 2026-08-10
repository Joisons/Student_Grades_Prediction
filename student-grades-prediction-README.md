# 🎓 Student Grades Prediction

Predicting a student's math exam score from demographic and preparation factors, and their reading/writing scores — a case study in identifying achievement-gap drivers.

**Suggested repo name:** `student-grades-prediction`

## Overview

What relates to strong exam performance — natural academic ability, preparation, or socioeconomic background? This project uses the "Students Performance in Exams" dataset to predict math score and quantify the relative contribution of test-prep completion, parental education, and a lunch-type socioeconomic proxy.

## Dataset

- **Source:** "Students Performance in Exams" dataset (mirrored via [rashida048/Datasets](https://github.com/rashida048/Datasets))
- **Size:** 1,000 students, 8 columns, no missing values
- **Target:** `math_score` (0–100)
- **Features:** `gender`, `race/ethnicity`, `parental_level_of_education`, `lunch`, `test_preparation_course`, `reading_score`, `writing_score`

## Repository Structure

```
student-grades-prediction/
├── README.md
├── requirements.txt
└── notebooks/
    └── 12_Student_Grades_Prediction.ipynb
```

## Getting Started

```bash
git clone https://github.com/<your-username>/student-grades-prediction.git
cd student-grades-prediction
pip install -r requirements.txt
jupyter notebook notebooks/12_Student_Grades_Prediction.ipynb
```

**requirements.txt**
```
pandas
numpy
matplotlib
seaborn
scikit-learn
xgboost
jupyter
```

## Methodology

1. **EDA** — score distributions, math score by gender/test-prep/parental education/lunch type, correlation between the three exam scores.
2. **Preprocessing** — `ColumnTransformer` (`StandardScaler` for the two numeric scores, `OneHotEncoder` for demographic categoricals).
3. **Model comparison** — Linear Regression, Ridge, Random Forest, Gradient Boosting, XGBoost via 5-fold CV (RMSE).
4. **Tuning** — `GridSearchCV` over Ridge's regularization strength `alpha`.
5. **Evaluation** — RMSE/MAE/R², residual plot, standardized coefficients for interpretability.

## Results

| Metric | Value |
|---|---|
| Final model | **Ridge Regression** (alpha=1) |
| **Test RMSE** | **5.39 points** |
| Test MAE | 4.21 points |
| **Test R²** | **0.881** |

**Top predictors:** reading score and writing score (general academic ability), followed by test-prep course completion and lunch type.

## Key Insights

- Reading and writing scores are overwhelmingly the strongest predictors of math score — general academic/testing ability dominates subject-specific variation.
- Test-preparation course completion has a clear, independent positive effect even after controlling for the other scores.
- Lunch type (a rough socioeconomic proxy) remains a meaningful predictor, highlighting an achievement gap worth addressing through equitable support.
- A simple regularized linear model performs as well as tree ensembles here — the underlying relationships are close to linear.

## Future Work

- Gather attendance, study-time, and prior-GPA data — stronger causal levers than demographic proxies.
- Use demographic findings to understand disparities, not to make decisions about individual students.

## Data Source & License

Dataset originally shared on Kaggle by user `spscientist`; used here for educational purposes.

## License

MIT
