# Machine Learning for Analysts — Selected Teaching Materials

Selected materials from a multi-session introductory Machine Learning course I designed and delivered for data analysts.

The course was designed to bridge the gap between analytical work and practical machine learning. Rather than focusing primarily on model complexity, the sessions connected core ML concepts to familiar analytical and business questions: predicting numerical outcomes, classifying structured and textual data, evaluating models beyond accuracy, choosing decision thresholds, and interpreting predictions in terms of business costs.

The course began with a conceptual introduction to machine learning and progressed through hands-on Jupyter notebooks to a two-part customer churn capstone.

This repository contains the practical materials that have been preserved from the course.

> **Language:** the notebooks were written for a Russian-speaking audience, so the explanations, comments and discussion questions are in Russian. Code, metric names and identifiers are in English.

## Selected curriculum

The conceptual introduction (Lesson 1) had no notebook, so the numbering starts at 2.

| Notebook | Topic |
|---|---|
| [`Lesson_02_Datasets_and_Features`](Lesson_02_Datasets_and_Features.ipynb) | **Datasets and Feature Engineering.** Inspecting data quality, simple cleaning, encoding, and why we split data into train and test. |
| [`Lesson_03_Regression_MonthlySpend`](Lesson_03_Regression_MonthlySpend.ipynb) | **Regression — Customer Monthly Spend.** Introduction to numerical prediction with linear regression and regression metrics. |
| [`Lesson_04_TextClassification_Products`](Lesson_04_TextClassification_Products.ipynb) | **Text Classification — Product Categories.** Introduction to text representation and classification using bag-of-words and logistic regression. |
| [`Lesson_05_Binary_FlightDelays`](Lesson_05_Binary_FlightDelays.ipynb) | **Binary Classification — Flight Delays.** Classification with mixed numerical and categorical features using random forests. |
| [`Lesson_06_Metrics_CostThresholds`](Lesson_06_Metrics_CostThresholds.ipynb) | **Model Evaluation — Metrics, Thresholds & Business Costs.** Precision, recall, F1, ROC/PR analysis, decision thresholds, class imbalance, and the business consequences of false positives and false negatives. |
| [`Lesson_07_Churn_00_Prep_and_EDA`](Lesson_07_Churn_00_Prep_and_EDA.ipynb), [`Lesson_07_Churn_01_Modeling_and_Interpretation`](Lesson_07_Churn_01_Modeling_and_Interpretation.ipynb) | **Capstone — Telco Customer Churn.** A two-part exercise covering data preparation and EDA followed by logistic regression and random forest modelling, evaluation, interpretation, and optional SHAP analysis. |

## Teaching approach

The exercises were designed for analysts rather than ML engineers. Each practical task introduced a small number of new concepts and connected them to questions the audience could encounter in analytical work. Discussion prompts were used throughout the sessions to move from model outputs and metrics toward interpretation, limitations, and business decisions.

The notebooks are intentionally based on relatively simple models: the objective was to teach reasoning about ML problems and evaluation before introducing greater model complexity.

## Running the notebooks

```bash
python -m venv .venv
.venv/Scripts/activate        # Windows; on macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute --inplace Lesson_03_Regression_MonthlySpend.ipynb   # or open them in Jupyter / VS Code
```

Run the two churn notebooks in order: `Lesson_07_Churn_00` writes `telco_churn_prepared.csv`, which `Lesson_07_Churn_01` reads. The SHAP cell in `Lesson_07_Churn_01` is optional and needs `pip install -r requirements-optional.txt`.

All notebooks were last executed top to bottom with Python 3.14 and the versions pinned in `requirements.txt`. Notebooks are stored without outputs.

## Data

- **All lessons except the churn capstone** generate small synthetic datasets inside the notebook. No external files are needed.
- **Telco Customer Churn** is the IBM Cognos Analytics sample dataset (a fictional telecom company, 7,043 customers). It is **not** included in this repository. `Lesson_07_Churn_00` downloads it from the public [IBM/telco-customer-churn-on-icp4d](https://github.com/IBM/telco-customer-churn-on-icp4d) repository (with the [plotly/datasets](https://github.com/plotly/datasets) mirror as a fallback). Rights to the data belong to its original owners. If neither download works, the notebook falls back to a synthetic dataset with random churn, so the modelling results in that case are meaningless.

## About these files

The notebooks are archived course material, not a rewritten 2026 curriculum. They were preserved as they were taught; the first commit in this repository's history contains them unchanged. Later commits only fix portability issues so they run on current library versions (for example, string dtypes in pandas 3, and matplotlib axes handling in scikit-learn's `*Display.from_predictions`), and add the data attribution above. One deliberate change to the data: in `Lesson_05_Binary_FlightDelays` the synthetic delay signal was too weak (the random forest scored about chance level, ROC-AUC ≈ 0.49), so the sample size and effect sizes were increased. The teaching content, models and discussion questions were left as they were.

## License

MIT — see [LICENSE](LICENSE). This covers the code and materials in this repository, not the Telco Customer Churn dataset (see Data).
