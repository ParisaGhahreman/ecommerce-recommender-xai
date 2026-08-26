# Explainable E-Commerce Personalization System

An explainable e-commerce personalization framework that combines:

- cart-to-purchase prediction;
- probability-based personalization actions;
- behavior-based item-to-item recommendations;
- SHAP explainability;
- temporal evaluation and external validation.

The project uses the Retailrocket e-commerce event dataset as the primary dataset and the YooChoose RecSys Challenge 2015 dataset for external validation.

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22116891.svg)](https://doi.org/10.5281/zenodo.22116891)

> **Archived release DOI:** [10.5281/zenodo.22116891](https://doi.org/10.5281/zenodo.22116891)
> **License:** MIT for project code; source datasets retain their original licenses and terms.

## Research objective

The system addresses three connected questions:

1. Can historical user, item, and user–item interaction signals predict whether a carted item will be purchased within 14 days?
2. Can behavioral item co-occurrence provide useful related-item recommendations?
3. How can predicted purchase propensity be translated into cost-aware and explainable personalization actions?

## Main contributions

- A leakage-aware cart-to-purchase prediction task based on first cart events.
- Chronological train, validation, and test splits rather than random splitting.
- Comparison of Logistic Regression, Random Forest, Decision Tree, CatBoost, and XGBoost.
- SHAP global and local explanations for the selected CatBoost model.
- External validation of an equivalent click-to-purchase framework on YooChoose.
- A session-based item-to-item recommendation prototype with temporal evaluation.
- An integrated framework that combines purchase probability, related-item suggestions, and action policies.

## Key results

### Cart-to-purchase prediction on Retailrocket

The selected CatBoost model achieved:

| Metric | Default threshold (0.50) | Selected threshold (0.25) |
|---|---:|---:|
| ROC-AUC | 0.7584 | 0.7584 |
| PR-AUC | 0.5947 | 0.5947 |
| Precision | 0.7083 | 0.4538 |
| Recall | 0.3399 | 0.7228 |
| F1-score | 0.4594 | 0.5575 |

The lower threshold was selected on a chronological validation set to prioritize recall for low-cost personalization scenarios.

### External validation on YooChoose

An equivalent session-based click-to-purchase task was evaluated on YooChoose because it contains session identifiers and clicks rather than persistent users and cart events.

| Metric | External CatBoost result |
|---|---:|
| ROC-AUC | 0.6337 |
| PR-AUC | 0.0741 |
| Recall at selected threshold | 0.2811 |
| Precision at selected threshold | 0.0811 |
| F1-score at selected threshold | 0.1259 |

### Item-to-item recommendation prototype

| Method | Coverage | Hit Rate@10 | MRR@10 |
|---|---:|---:|---:|
| Popularity baseline | 100.00% | 1.13% | 0.0025 |
| Item-to-item co-occurrence | 39.92% | 14.92% | 0.0918 |
| Hybrid co-occurrence with popularity fallback | 100.00% | 15.26% | 0.0924 |

## Project structure

```text
ecommerce-recommender-xai/
│
├── notebooks/
│   ├── 01_Data_Audit_and_EDA.ipynb
│   ├── 02_Feature_Engineering.ipynb
│   ├── 03_Cart_to_Purchase_Model.ipynb
│   ├── 04_Model_Explainability_and_XAI.ipynb
│   ├── 05_External_Validation_YooChoose.ipynb
│   ├── 06_Personalization_Strategy.ipynb
│   ├── 07_Recommendation_Prototype.ipynb
│   └── 08_Integrated_Personalization_Framework.ipynb
│
├── outputs/
│   ├── figures/
│   ├── models/
│   └── tables/
│
├── DATA_SOURCES.md
├── RESEARCH_FINDINGS.md
├── requirements.txt
├── LICENSE
└── CITATION.cff

```
Data availability

The raw and processed datasets are intentionally excluded from this repository because of file size and dataset-specific licensing terms.

This project uses:

Retailrocket E-Commerce Dataset: primary dataset for event analysis, feature engineering, cart-to-purchase prediction, explainability, and recommendation experiments.
YooChoose RecSys Challenge 2015 Dataset: external dataset for session-based click-to-purchase validation.

See DATA_SOURCES.md for download instructions, expected file locations, and dataset-license notes.

Reproducibility
Create and activate a Python environment.
Install dependencies:
pip install -r requirements.txt
Download the datasets described in DATA_SOURCES.md.
Place the raw files in the expected data/raw/ paths.
Run the notebooks sequentially from 01 to 08.

The project was developed with a chronological evaluation design. Therefore, later notebooks depend on artifacts created by earlier notebooks.

Important limitations
Product names, descriptions, prices, and a product-to-category mapping were not available for the Retailrocket item identifiers.
The recommendation prototype is behavior-based and does not represent semantic product similarity.
Predicted purchase propensity does not estimate the causal effect of a discount, reminder, or recommendation.
Financial incentives should be evaluated with controlled online A/B testing before deployment.
External validation tests an equivalent behavioral prediction framework, not direct deployment of the Retailrocket model on YooChoose.
Citation

If you use this repository, please cite it using the metadata in CITATION.cff.

Author

Parisa Ghahreman