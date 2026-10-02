# Machine Learning for Analysts — Selected Teaching Materials

Selected materials from a multi-session introductory Machine Learning course I designed and delivered for data analysts.

The course was designed to bridge the gap between analytical work and practical machine learning. Rather than focusing primarily on model complexity, the sessions connected core ML concepts to familiar analytical and business questions: predicting numerical outcomes, classifying structured and textual data, evaluating models beyond accuracy, choosing decision thresholds, and interpreting predictions in terms of business costs.

The course began with a conceptual introduction to machine learning and progressed through hands-on Jupyter notebooks to a two-part customer churn capstone.

This repository contains the practical materials that have been preserved from the course.

> **Language:** the notebooks were written for a Russian-speaking audience, so the explanations, comments and discussion questions are in Russian. Code, metric names and identifiers are in English.

## Selected curriculum

Lesson 1 was conceptual: we discussed ML aloud and studied the core concepts using external resources, so there was no notebook. Code starts in Lesson 2, and the file numbers follow the lesson numbers.

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

All notebooks were last executed top to bottom with Python 3.14 and the versions pinned in `requirements.txt` (notably pandas 3.0.6; pandas 2.x has not been tested). Notebooks are stored without outputs. The optional SHAP cell can take several minutes.

## Data

- **All lessons except the churn capstone** generate small synthetic datasets inside the notebook. No external files are needed.
- **Telco Customer Churn** is an open teaching dataset commonly attributed to IBM (Cognos Analytics sample data; a fictional telecom company, 7,043 customers), widely distributed via [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) and GitHub. It is **not** included in this repository. `Lesson_07_Churn_00` downloads it from the public [IBM/telco-customer-churn-on-icp4d](https://github.com/IBM/telco-customer-churn-on-icp4d) repository (with the [plotly/datasets](https://github.com/plotly/datasets) mirror as a fallback); both links are pinned to specific commits. Rights to the data belong to its original owners. If neither download works, the notebook prints a warning and falls back to a synthetic dataset with random churn, so the modelling results in that case are meaningless.

## About these files

The notebooks are archived course material, not a rewritten 2026 curriculum. AI assistance was used to bring them back to their original clean, runnable state after the course, and Claude (Anthropic) helped add this archive to GitHub — thank you.

Changes relative to the preserved notebooks are small and deliberate:

- **Portability:** string dtypes in pandas 3, and matplotlib axes handling in scikit-learn's `*Display.from_predictions`, so the notebooks run on current library versions.
- **Synthetic data:** in `Lesson_05_Binary_FlightDelays` the delay signal was too weak (the random forest scored about chance level, ROC-AUC ≈ 0.49), so the sample size and effect sizes were increased. In `Lesson_04_TextClassification_Products` 18 extra phrases were added, because with 36 phrases the train and test sets shared almost no words.
- **Support for discussion questions:** where a discussion question had no output to rely on, a short cell or note was added (regression and logistic-regression coefficients, churn rate by group, an accuracy baseline in `Lesson_06`, short notes on data leakage and on feature importances).
- **Churn data:** source attribution, pinned download links, and a clear warning when the synthetic fallback is used. The `#TO-DO` cell in `Lesson_07_Churn_00` is an in-class exercise stub; its solution is in the next cell.

The models and the teaching structure were not changed.

## License

MIT — see [LICENSE](LICENSE). This covers the code and materials in this repository, not the Telco Customer Churn dataset (see Data).
