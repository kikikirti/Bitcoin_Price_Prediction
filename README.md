# Bitcoin Price Prediction

This project predicts whether buying Bitcoin at a given time would be profitable using machine learning techniques.

## Data Source

The data used includes Bitcoin OHLC (Open, High, Low, Close) prices from July 17, 2014, to December 29, 2022, covering 8 years of Bitcoin price movements.

## Data Exploration

The dataset contains 2,713 rows (daily records) and 7 columns (features). Here's an overview:

- **Date**: The date of the price record.
- **Open**: The opening price of Bitcoin on that day.
- **High**: The highest price of Bitcoin on that day.
- **Low**: The lowest price of Bitcoin on that day.
- **Close**: The closing price of Bitcoin on that day.
- **Volume**: The volume of Bitcoin traded.
- **Adj Close**: Adjusted closing price (later dropped as it was identical to 'Close').

The dataset does not contain any missing values.

## Exploratory Data Analysis

We visualized the data to explore trends in Bitcoin prices over time. The closing price showed an overall upward trend, especially after 2020.

We also performed feature engineering to extract additional information from the 'Date' column, creating new features for **year**, **month**, **day**, and a flag for **quarter-end**.

### Outlier Analysis

We discovered many outliers in the price data, indicating substantial price fluctuations within short time periods. This was confirmed through boxplots and visualizations of price distributions.

## Feature Engineering

New features derived from the data include:

- **open-close**: Difference between the opening and closing prices.
- **low-high**: Difference between the lowest and highest prices.
- **is_quarter_end**: A binary indicator for quarter-end days.
- **target**: A signal feature where 1 indicates that the next day’s closing price is higher than the current day (i.e., a buy signal), and 0 otherwise.

## Model Training

We trained three machine learning models to predict the target (whether the price would increase the next day):

- **Logistic Regression**
- **Support Vector Classifier (SVC)** with a polynomial kernel
- **XGBoost Classifier**

Before training, the features were standardized using **StandardScaler** to ensure stable and faster training.

The dataset was split into training (90%) and validation (10%) sets to evaluate the model's performance.

## Evaluation

The models were evaluated using the **ROC-AUC score** to measure the accuracy of predicting soft probabilities. Here are the results:

- **Logistic Regression**:
  - Training ROC-AUC: 0.53
  - Validation ROC-AUC: 0.52
- **SVC**:
  - Training ROC-AUC: 0.48
  - Validation ROC-AUC: 0.53
- **XGBoost Classifier**:
  - Training ROC-AUC: 0.92
  - Validation ROC-AUC: 0.46

Despite XGBoost achieving high accuracy on the training set, it showed signs of **overfitting**, as the validation performance was much lower. Logistic Regression showed a more stable performance between training and validation.

## Conclusion

The initial models did not perform better than random guessing (50% ROC-AUC). Possible improvements include using more advanced models or additional features to capture the complex dynamics of Bitcoin price movements. Future work may involve using larger datasets or integrating external economic indicators to enhance predictive performance.
