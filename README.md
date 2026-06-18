# Retail Inventory Demand Prediction Using Neural Networks

## Project Overview

This project was completed for **Machine Learning and Programming II**. The goal was to build a Neural Network model using Python to support a supply chain process.

The selected supply chain field is **Warehousing**. The project focuses on improving **automatic stock allocation** and reducing **supply inefficiencies** by predicting daily product demand.

The model predicts the number of units sold for retail products using historical inventory, pricing, promotional, seasonal, store, and product-related information.

## Business Problem

Retail businesses need to allocate the right amount of inventory across stores and products. If inventory is too low, the company may experience stock shortages and lost sales. If inventory is too high, the company may face unnecessary storage costs, waste, and inefficient warehouse usage.

This project uses a Neural Network regression model to predict daily `Units Sold`. These predictions can help warehouse managers make better stock-allocation and replenishment decisions.

## Dataset

The dataset used in this project is the **Retail Store Inventory Forecasting Dataset** from Kaggle.

The dataset contains daily inventory and sales records for multiple stores and products.

### Main Attributes

* `Date`
* `Store ID`
* `Product ID`
* `Category`
* `Region`
* `Inventory Level`
* `Units Sold`
* `Units Ordered`
* `Demand Forecast`
* `Price`
* `Discount`
* `Weather Condition`
* `Holiday/Promotion`
* `Competitor Pricing`
* `Seasonality`

## Target Variable

The target variable is:

```text
Units Sold
```

This variable represents the number of units sold for a product during a day.

## Supply Chain Relevance

This project supports the warehousing process by helping the company:

* Improve automatic stock allocation
* Reduce stock shortages
* Reduce excess inventory
* Improve inventory planning
* Lower storage and replenishment costs
* Improve product availability

## Methodology

The project followed these main steps:

1. Load the raw dataset
2. Isolate five rows before model development
3. Inspect the dataset for missing values, duplicate rows, data types, and unusual values
4. Clean negative values in the `Demand Forecast` column
5. Engineer date-based features
6. Select predictor variables and target variable
7. Split the data chronologically into training and testing sets
8. Scale numerical predictors
9. Encode categorical predictors
10. Scale the target variable
11. Build and train a Neural Network regression model
12. Evaluate the model using the testing dataset
13. Test the model using the five isolated rows
14. Interpret the business value of the model results

## Data Preprocessing

The preprocessing included:

* Converting the `Date` column into datetime format
* Creating date-based features:

  * `Date_Year`
  * `Date_Month`
  * `Date_DayOfWeek`
* Removing the original `Date` column after feature engineering
* Removing `Units Ordered` from the model to avoid using a replenishment decision as a demand predictor
* Replacing negative `Demand Forecast` values with zero
* Scaling numerical variables using `MinMaxScaler`
* Encoding categorical variables using `OneHotEncoder`
* Scaling the target variable, `Units Sold`, to the 0–1 range before Neural Network training

## Feature Selection

### Numerical Input Features

* `Inventory Level`
* `Demand Forecast`
* `Price`
* `Discount`
* `Holiday/Promotion`
* `Competitor Pricing`

### Categorical Input Features

* `Store ID`
* `Product ID`
* `Category`
* `Region`
* `Weather Condition`
* `Seasonality`
* `Date_Month`
* `Date_DayOfWeek`

After preprocessing, the model contained **67 processed input features**.

## Neural Network Model

A **Multi-Layer Perceptron Regressor** was used because the target variable is numerical.

### Model Architecture

| Layer        | Description                    |
| ------------ | ------------------------------ |
| Input Layer  | 67 processed input features    |
| Hidden Layer | 46 nodes                       |
| Output Layer | 1 node predicting `Units Sold` |

The hidden layer size was selected using the guideline:

```text
(2/3 × number of input nodes) + number of output nodes
```

For this project:

```text
(2/3 × 67) + 1 ≈ 46
```

The model used the `ReLU` activation function and the `adam` solver. Early stopping was enabled to reduce unnecessary training and limit overfitting.

## Model Performance

The Neural Network completed training after **35 iterations**.

Final training loss:

```text
0.000182
```

### Testing Results

| Metric                  |     Result |
| ----------------------- | ---------: |
| Mean Absolute Error     | 7.73 units |
| Root Mean Squared Error | 9.05 units |
| R² Score                |     0.9930 |

The MAE means that the model’s predictions differed from the actual daily sales values by approximately **7.73 units on average**.

The R² score of **0.9930** indicates that the model explained approximately **99.3% of the variation** in `Units Sold`.

## Five Isolated Row Test

Five observations were removed from the raw dataset before preprocessing and model training. These rows were not included in:

* training
* regular testing
* scaling
* encoding
* Neural Network fitting

After the model was trained, the same preprocessing steps were applied to the isolated rows, and the trained model predicted their `Units Sold` values.

| Store | Product | Actual Units Sold | Predicted Units Sold | Absolute Error |
| ----- | ------- | ----------------: | -------------------: | -------------: |
| S005  | P0004   |                85 |                78.27 |           6.73 |
| S003  | P0014   |                74 |                80.55 |           6.55 |
| S004  | P0011   |               107 |               117.17 |          10.17 |
| S003  | P0006   |               366 |               364.81 |           1.19 |
| S003  | P0005   |               291 |               293.10 |           2.10 |

The average absolute error for the five isolated rows was approximately:

```text
5.35 units
```

## Business Interpretation

The model generated accurate predictions for both the regular testing dataset and the isolated five-row test.

These results suggest that a Neural Network model can support warehouse decision-making by helping the company estimate daily product demand. More accurate demand predictions allow the business to allocate inventory more effectively, reduce stock shortages, avoid excessive inventory, and improve supply chain efficiency.

The `Demand Forecast` variable was included as an input because it represents an existing estimate that may be available before stock-allocation decisions are made. Therefore, the Neural Network can be interpreted as improving the existing forecast by combining it with inventory, pricing, promotional, seasonal, store, and product-related information.

## Repository Structure

```text
retail-inventory-nn-assignment/
│
├── README.md
├── PROJECT_STEPS.md
├── requirements.txt
├── .gitignore
│
├── data/
│   ├── raw/
│   │   └── retail_store_inventory.csv
│   └── processed/
│       ├── cleaned_modeling_dataset.csv
│       └── isolated_5_rows.csv
│
├── notebooks/
│   └── Assignment_1.ipynb
│
├── outputs/
│   └── isolated_5_rows_prediction_results.csv
│
└── reports/
    └── Assignment_1_Report.docx
```

## How to Run the Project

1. Clone or download the repository.
2. Install the required libraries.
3. Open the notebook:

```text
notebooks/Assignment_1.ipynb
```

4. Run the notebook cells from top to bottom.
5. Review the model evaluation results and isolated-row prediction table.

## Required Libraries

The project uses:

* pandas
* numpy
* matplotlib
* scikit-learn
* openpyxl
* jupyter

## Author

Said Huner
Machine Learning and Programming II
Summer 2026
