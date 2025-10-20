# 📊 Task 1: Data Cleaning and Preprocessing - Customer Personality Analysis

## 🎯 Objective

The goal of this task was to clean and preprocess the raw `marketing_campaign.csv` dataset, addressing common data quality issues such as missing values, inconsistent formats, and redundant data, to create a final, analysis-ready dataset. This fulfills the requirements for Task 1 of the Data Analyst Internship.

## 🗃️ Repository Contents

| File Name | Description |
| :--- | :--- |
| `marketing_campaign.csv` | The **original, raw** dataset containing various data quality issues. |
| `marketing_campaign_cleaned.csv` | The **final, cleaned** and preprocessed dataset. |
| `data_cleaning.ipynb` | The **Python code** (Jupyter Notebook) used to perform all cleaning operations with Pandas. |
| `README.md` | This summary document. |

## ✨ Summary of Data Cleaning and Preprocessing Steps

The following critical steps were executed to clean and prepare the data:

### 1. Column Standardization and Renaming

* **Header Format:** All column headers were converted to **lowercase** and sanitized (e.g., removing special characters and spaces) for consistent access (e.g., `Year_Birth` $\rightarrow$ `year_birth`).
* **Renaming:** The expenditure columns (`Mnt...`) were renamed to a more intuitive convention (`amt_...`) to improve clarity (e.g., `mntwines` $\rightarrow$ `amt_wines`).

### 2. Handling Missing Values and Data Types

* **Missing Values:** The **24 missing values** in the `income` column were identified and imputed using the **median income** ($\$51,381$), as this method is robust to outliers.
* **Data Type Fix:** The `income` column was successfully converted from a floating-point type (`float64`) to an **integer** type (`int64`).
* **Duplicates:** A check confirmed that the dataset contained **no duplicate rows**.

### 3. Date and Categorical Standardization

* **Date Format:** The `dt_customer` column was converted from an inconsistent string format to a proper **datetime object** (`datetime64[ns]`), ensuring time-based analysis is accurate.
* **Text Standardization:** In the `marital_status` column, atypical and rare entries (`Alone`, `Absurd`, `YOLO`) were standardized and grouped into a single, unified category: **`Other`**.

### 4. Feature Engineering

* **Age Calculation:** A new feature, **`age`**, was calculated by subtracting the `year_birth` from a current reference year (**2025**).
* **Redundant Column Removal:** The original **`year_birth`** column was dropped, as the derived `age` feature made it redundant.

## 🛠️ Key Transformations (Python/Pandas)

```python
# Handle Missing Income and Convert Data Type
median_income = df['income'].median()
df['income'].fillna(median_income, inplace=True)
df['income'] = df['income'].astype('int64')

# Standardize Marital Status
status_to_replace = ['Alone', 'Absurd', 'YOLO']
df['marital_status'] = df['marital_status'].replace(status_to_replace, 'Other')

# Feature Engineering: Calculate Age
current_year = 2014
df['age'] = current_year - df['year_birth']
df.drop(columns=['year_birth'], inplace=True)
