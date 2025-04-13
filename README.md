# Sales Forecasting for German Drug Stores

This project focuses on predicting daily sales for 1,115 drug stores located across Germany. By utilizing historical data and store-specific attributes, the project aims to create accurate sales forecasts to support stock management, enhance customer satisfaction, and drive business profitability.

## Project Overview

The dataset includes historical sales data from January 2013 to July 2015 along with detailed store-level metadata such as promotional activities, holiday schedules, competition metrics, and assortment levels.

The key objective is to develop a robust predictive model that can estimate daily sales while handling challenges like missing data and feature complexity. The project includes thorough data preprocessing, exploratory data analysis (EDA), and machine learning modeling.

## Repository Structure

| File | Description |
|------|-------------|
| `DrugStore-Prediction.ipynb` | Main Python notebook containing code for data preprocessing, feature engineering, EDA, model training, and prediction. |
| `analysis_and_methodology.md` | Detailed description of the analysis strategy, EDA findings, modeling techniques, and performance evaluation. |
| `Dataset.zip` | Compressed folder containing the original data files: `train.csv`, `test.csv`, and `store.csv`. |
  | `train.csv` | Historical sales data from 01/01/2013 to 31/07/2015. Contains fields like store ID, sales, number of customers, promotions, and holidays. |
  | `test.csv` | Identical format to `train.csv`, covering the period 01/08/2015 to 17/09/2015, but without sales and customer values. |
  | `store.csv` | Metadata for each store, including store type, assortment level, competition details, and participation in ongoing promotions. |

## Tools Used

- Python
- Pandas, NumPy, Matplotlib, Seaborn
- Scikit-learn
- Jupyter Notebook

## Model Summary

A Random Forest Regressor was selected as the final model due to its ability to handle non-linear relationships and its robust performance in regression tasks. Feature importance was analyzed to guide business decisions.

The model achieved strong predictive performance on validation data:
- **R² Score:** 0.88 (initial model), improved to 0.98 with customer prediction augmentation.
- **RMSE:** Significantly reduced after enhancement.

## Key Highlights

- Integration of multiple datasets using a left join on the store index.
- Robust feature engineering including temporal, promotional, and competition-based variables.
- Strategic feature selection based on correlation and business logic.
- Handling of missing values using median/mode imputation and custom encodings.

---

For an in-depth look into the methodology, EDA insights, and results, refer to [`analysis_and_methodology.md`](./analysis_and_methodology.md).
