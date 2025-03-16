# Data Preprocessing Pipeline

This repository contains a data preprocessing pipeline for customer transaction data. The pipeline performs data augmentation, dataset merging using transitive properties, feature engineering, and data consistency checks to prepare a clean, structured, and machine-learning-ready dataset.

## Project Overview

The data preprocessing pipeline consists of three main parts:

### Part 1: Data Augmentation on CSV Files

**Objective:** Expand an existing dataset using synthetic data, perturbation, and augmentation techniques.

#### Steps Taken:

#### Loading Datasets:
- `customer_transactions.csv`: Contains customer IDs, transaction histories, and purchase behaviors.

#### Handling Missing Values:
- Used LightGBM model to predict missing values.
- Applied mean, median, and mode imputation where applicable.

#### Synthetic Data Generation:
- Applied random noise to numerical transaction values.
- Used SMOTE (Synthetic Minority Over-sampling Technique) to balance the dataset.

#### Feature Value Transformation:
- Applied log transformation to correct skewed data distributions.

#### Data Expansion:
- Generated new synthetic transactions based on customer behaviors.

#### Exporting Augmented Data:
- Saved as `customer_transactions_augmented.csv`.

### Part 2: Merging Datasets with Transitive Properties

**Objective:** Merge datasets that share indirect relationships using an ID mapping file.

#### Steps Taken:

#### Loading Additional Datasets:
- `customer_social_profiles.csv`: Contains customer social media activity and purchase intent.
- `id_mapping.csv`: Links `customer_id_legacy` from transactions to `customer_id_new` in social profiles.

#### Merging Data via Transitive Properties:
- Merged `customer_transactions_augmented.csv` with `id_mapping.csv` to obtain `customer_id_new`.
- Further merged the result with `customer_social_profiles.csv`.

#### Handling Conflicts in ID Mapping:
- If multiple `customer_id_new` values were found for a single `customer_id_legacy`, kept the most recent ID based on `purchase_date`.

#### Feature Engineering & Transformation:
- Created **Customer Engagement Score** from transaction history & social media activity.
- Engineered predictive behavioral features:
  - Moving averages of transactions.
  - Time-based aggregation of purchases.
  - TF-IDF on customer reviews/social media comments.

#### Exporting Processed Data:
- Saved as `final_customer_data_PDL_6.csv`.

### Part 3: Data Consistency and Quality Checks

**Objective:** Ensure data integrity, structure, and readiness for machine learning.

#### Steps Taken:

#### Data Integrity Checks:
- Removed duplicate entries.
- Validated that all categorical values were correctly mapped.
- Ensured every transaction matched a valid social profile.

#### Statistical Summarization:
- Generated descriptive statistics for numerical columns.
- Visualized distribution of transaction amounts before and after augmentation.

#### Feature Selection for Machine Learning:
- Identified highly correlated features using a correlation heatmap.
- Selected the top 10 most important features using feature selection techniques.

#### Exporting Final Processed Data:
- Saved as `final_dataset_ready_PDL_6.csv`.

## How to Run the Notebook

### Requirements

Ensure the following Python libraries are installed:

```bash
pip install pandas numpy seaborn matplotlib scikit-learn imbalanced-learn lightgbm
```

### Running in Google Colab

1. Upload the dataset files to Google Drive.
2. Mount Google Drive in the notebook:

```python
from google.colab import drive
drive.mount('/content/drive')
```

3. Set the correct file paths and load datasets.
4. Run all notebook cells sequentially.
5. The processed CSV files will be saved in the specified directory.

## Deliverables

- **Jupyter Notebook** containing all preprocessing steps.
- **Final Processed CSV Files:**
  - `customer_transactions_augmented.csv`
  - `final_customer_data_PLD_6.csv`
  - `final_dataset_ready_PLD_6.csv`
- **Demo Video Presentation:** [Click here](https://youtu.be/gbxF_EQLwRc)

## Summary

This project effectively processes customer transaction data, merges datasets using indirect ID mapping, and performs advanced feature engineering. The final dataset is optimized for machine learning tasks, ensuring data quality, consistency, and usability.
