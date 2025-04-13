# Sales Forecasting - Analysis and Methodology

## Objective

The project aims to accurately predict daily sales for over 1,100 drug stores across Germany by using historical sales data, store characteristics, and promotional metadata. The goal is to optimize operational decisions like stock management and promotional planning.

---

## Data Preparation

### Datasets Used

- **Train Data:** Historical sales, store open/closed status, promo flags, holiday indicators, and customer counts.
- **Test Data:** Similar to training data but without sales and customers.
- **Store Data:** Metadata for each store including store type, assortment type, competition metrics, and promotion schedules.

### Data Integration

- A left join was performed using the `Store` key to merge train/test with store metadata.
- Date fields were converted to `datetime` format and decomposed into features like year, month, day, week, etc.

### Handling Missing Values

| Column | Handling Strategy |
|--------|--------------------|
| `CompetitionDistance` | Imputed with median |
| `CompetitionOpenSince*` | Imputed with mode |
| `PromoInterval` | Encoded as 'NoPromo' for missing |
| `Open` (in test data) | Imputed with mode (assumed operational) |

---

## Feature Engineering

- **Temporal Features:** Year, Month, Week, Quarter, IsWeekend
- **Competition Age:** Months since competitor store opened
- **Promotional Activity:** Days since last promotion (binned)
- **Categorical Encoding:** Label Encoding for variables like StoreType, Assortment, StateHoliday

Exploratory correlation led to the selection of the following features:
- Promo
- CompetitionDistance
- CompetitionAgeMonths
- StateHolidayEncoded
- StoreTypeEncoded
- AssortmentEncoded
- DayOfWeek

---

## 📊 Exploratory Data Analysis (EDA)

### Key Findings:

- **Promo Participation:** Significant uplift in average sales during promotions.
- **Store and Assortment Type:** StoreType 'b' and Assortment 'b' yield higher average sales.
- **Seasonality:** December sees peak sales; January experiences sharp declines.
- **Competition:** Sales drop as competition distance decreases.

Visual tools used: Bar plots, violin plots, correlation heatmaps, monthly trend graphs.

---

## Modeling Approach

### Model Chosen:
- **Random Forest Regressor**

### Reason for Selection:
- Handles non-linear relationships well
- Insensitive to feature scaling
- Provides feature importance metrics

### Model Evaluation:

- **Training-Validation Split:** 80/20 with `train_test_split`
- **Metrics:**
  - **R²:** 0.88 (initial)
  - **RMSE:** Low error magnitude, acceptable accuracy

### Enhancement:

Since customer count was highly correlated with sales (~0.9), a two-stage model was tested:
1. Predict customers
2. Use predicted customers as input for sales model

This improved:
- **R²:** to 0.983
- **RMSE:** to ~500

---

## Feature Importance

| Feature | Contribution (%) |
|---------|------------------|
| DayOfWeek | 40% |
| CompetitionDistance | 25% |
| CompetitionAgeMonths | 15% |
| Promo | 10% |
| StateHolidayEncoded + StoreTypeEncoded | 10% |

---

## Limitations

- **Customers Column:** Missing in test data, requiring estimation
- **Promotions:** Long-term promotional impact may not be fully captured
- **External Factors:** Macroeconomic events or local policies not accounted for

---

## Conclusion

This project delivers a scalable and interpretable model for sales forecasting in the retail pharmacy sector. It highlights the importance of data integration, smart feature engineering, and iterative model validation in real-world retail analytics.

---

For full code and visualizations, check [`DrugStore-Prediction.ipynb`](./DrugStore-Prediction.ipynb).
