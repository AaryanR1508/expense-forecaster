# 💸  Daily Expense Forecasting

---

## 🔹 Project Objective

The goal of this project is to develop a robust machine learning model that accurately forecasts total daily expenses based on historical transaction data. By identifying patterns in past spending, the model serves as a predictive tool to anticipate future expenditures, providing valuable insights for personal finance management.

---

## 🔹 Dataset

The analysis is based on a dataset from [Kaggle](https://www.kaggle.com/datasets/ismetsemedov/personal-budget-transactions-dataset) containing individual transactions. The key columns are:

| Column    | Description                                    |
|-----------|-----------------------------------------------|
| `date`    | Transaction timestamp                          |
| `category`| Spending category (e.g., Restaurant, Health) |
| `amount`  | Monetary value of the transaction             |

---

## 🔹 Methodology

The project followed a structured data science workflow, from data cleaning and exploration to feature engineering and modeling. The key insight from this process was that **contextual feature engineering** was critical for the model's success.

### 1. Data Cleaning and EDA

-   **Preprocessing:** The raw data was cleaned by converting timestamps to datetime objects and standardizing inconsistent category names (e.g., 'Restuarant' to 'Restaurant').
-   **Exploratory Analysis:** Initial analysis involved aggregating transactions into daily totals. This revealed that daily spending is highly volatile, with significant, unpredictable spikes. Early modeling attempts to forecast individual transactions or simple daily totals failed, yielding negative R² scores and confirming that a more sophisticated approach was needed.

### 2. Feature Engineering

The breakthrough in this project came from creating features that provided context for the model. The final feature set was constructed by:

1.  **Pivoting Categories:** Transforming the data so that each row represented a single day and each column represented the total amount spent in a specific category (e.g., `daily_total_Health`, `daily_total_Market`).
2.  **Creating Time-Series Features:** Adding features based on historical trends, including:
    -   `total_amount_lag_1`: The total spending from the previous day.
    -   `rolling_mean_7`: The average daily spending over the past 7 days.
    -   `dayofweek` and `month`: To capture weekly and seasonal patterns.

### 3. Modeling and Evaluation

-   **Algorithm:** A `RandomForestRegressor` was chosen for its robustness and ability to handle complex, non-linear relationships.
-   **Evaluation:** A strict, time-based train-test split was used. The model was trained on the first 80% of the historical data and evaluated on its ability to forecast the most recent 20%, simulating a real-world prediction scenario.

---

## 🔹 Results and Key Findings

The final model achieved a strong performance, demonstrating its ability to learn and predict spending patterns effectively.

-   **Final R² Score: 0.5992**

This score indicates that the model can explain approximately **60% of the variance** in daily spending, a significant result for noisy financial data.

### 1. Forecast vs. Actual Spending

The model successfully tracks the general trend of daily expenses and captures many of the smaller fluctuations, though it tends to underestimate the magnitude of extreme, outlier spikes.

### 2. Most Predictive Features

The feature importance analysis confirmed our hypothesis: recent spending history and contextual category data are the most powerful predictors.

-   **Top Features:** `rolling_mean_7`, `total_amount_lag_1`, `Restaurant`, and `Health`.

---

## 🔹 How to Run This Project

To replicate this analysis, follow these steps:

### 1. Prerequisites

Ensure you have Python 3 installed. All required libraries are listed in the `requirements.txt` file.

You can install all dependencies at once using pip:

```bash
pip install -r requirements.txt
```

### 2. Running the Notebook

- Clone or download this repository.

- Ensure expenses_data.csv and requirements.txt are in the root directory.

- Launch Jupyter Notebook or Jupyter Lab:

    ```bash
    jupyter notebook
    ```

- Open the expense_forecaster_final.ipynb file and run the cells in order.

---

## 🔹 Conclusion

This project successfully demonstrates that by providing a machine learning model with the right contextual features, it is possible to build a useful daily expense forecaster. The key takeaway is that understanding the composition of daily spending (i.e., which categories contributed to the total) was more important than the choice of algorithm itself.

---

### 🧑‍💻 Author

Made with 💻 and ☕ by Aaryan R.