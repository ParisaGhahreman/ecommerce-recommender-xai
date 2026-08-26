# Data Sources and Access Instructions

This repository does not redistribute raw datasets or record-level processed datasets. The files are excluded because of their size, privacy considerations, and dataset-specific licensing terms.

## 1. Retailrocket E-Commerce Dataset

### Role in this project

Retailrocket is the primary dataset used for:

- exploratory data analysis;
- data-quality checks;
- leakage-aware feature engineering;
- cart-to-purchase prediction;
- SHAP explainability;
- probability-based personalization;
- item-to-item recommendation experiments.

### Required files

Place the following files in:

```text
data/raw/
events.csv
category_tree.csv
Expected event fields
timestamp, visitorid, event, itemid event, itemid, transactionid

The event field contains view, addtocart, and transaction records.

Dataset access

Dataset page:

https://www.kaggle.com/datasets/retailrocket/ecommerce-dataset

The dataset is not included in this repository. Before use or redistribution, review the dataset page and its associated terms.

2. YooChoose RecSys Challenge 2015 Dataset
Role in this project

YooChoose is used only for external validation of an equivalent session-based click-to-purchase prediction framework.

It is not a direct replacement for Retailrocket because it contains anonymous sessions and clicks rather than persistent visitors and cart events.

Required files

Extract the YooChoose archive and place these files in:

data/raw/yoochoose/
yoochoose-clicks.dat
yoochoose-buys.dat
yoochoose-test.dat
dataset-README.txt
Direct download
https://s3-eu-west-1.amazonaws.com/yc-rdata/yoochoose-data.7z
File structures

Clicks

Session ID, Timestamp, Item ID, Category

Purchases

Session ID, Timestamp, Item ID, Price, Quantity
License

The YooChoose dataset is licensed under:

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International
(CC BY-NC-ND 4.0)

The dataset must not be redistributed through this repository. Please read dataset-README.txt after extraction and comply with the original terms.

Expected local data structure
data/
├── raw/
│   ├── events.csv
│   ├── category_tree.csv
│   └── yoochoose/
│       ├── dataset-README.txt
│       ├── yoochoose-clicks.dat
│       ├── yoochoose-buys.dat
│       └── yoochoose-test.dat
│
└── processed/
    └── Files generated automatically by the notebooks
Reproduction sequence
Download and place the Retailrocket files in data/raw/.
Download and extract the YooChoose archive into data/raw/yoochoose/.
Run the notebooks sequentially from 01_Data_Audit_and_EDA.ipynb to 08_Integrated_Personalization_Framework.ipynb.
The notebooks will create all files under data/processed/, outputs/tables/, outputs/figures/, and outputs/models/.
Data-use note

The source datasets retain their own licenses and conditions. The MIT license in this repository applies only to the project code and original documentation, not to third-party datasets.