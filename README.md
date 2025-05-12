# Loss Given Default (LGD) Modeling for Credit Risk

## Project Overview
This project undertakes the critical task of modeling Loss Given Default (LGD) within the Banking, Financial Services, and Insurance (BFSI) sector. LGD represents the proportion of a loan exposure that a financial institution anticipates losing if a borrower defaults. Accurately estimating LGD is crucial for calculating Expected Credit Loss (ECL), a key component of the provisioning framework mandated by international banking regulations like Basel III. These regulations require banks to hold adequate capital reserves to absorb potential credit losses, thereby ensuring financial stability.

The core objective is to develop a robust statistical model using historical data to predict LGD. This involves analyzing detailed information related to loan accounts, borrower characteristics, repayment histories, and collateral values. By improving the accuracy of LGD predictions, banks can enhance their risk management practices, make more informed lending decisions, and ensure compliance with regulatory capital requirements. This project specifically focuses on building and comparing different regression models to find the best approach for estimating LGD based on the provided datasets.

## Objective
The primary goal is to construct and evaluate regression models capable of accurately predicting Loss Given Default (LGD) for individual loan accounts. LGD is calculated as the net loss following a default event, considering both the outstanding loan amount and any recovered funds (through collateral liquidation or repayments):

$$ LGD = \frac{Loan Amount - (Collateral Value + Sum of Repayments)}{Loan Amount} $$
Achieving an accurate LGD model helps banks refine their ECL calculations ($ECL = PD \times EAD \times LGD$) and improve overall credit risk management.

## Dataset
The analysis is based on three distinct datasets providing a comprehensive view of loan performance:
1.  **`loan_base.csv`**: Contains primary information about each loan account, including loan terms, amount funded, and associated borrower details.
2.  **`repayment_base.csv`**: Includes records of repayments made against loans, such as Equated Monthly Installments (EMIs) and amounts recovered through collection efforts post-default.
3.  **`monthly_balance_base.csv`**: Provides time-series data on the monthly balance statements in the borrowers' accounts, offering insights into their financial behavior.

These datasets were merged using unique loan identifiers to create a unified dataset for analysis and modeling.

## Methodology

The project followed a systematic data science workflow:

1.  **Data Integration and Preparation:**
    * Loaded the three source CSV files (`loan_base.csv`, `repayment_base.csv`, `monthly_balance_base.csv`).
    * Merged these datasets into a single analytical base table using appropriate keys (e.g., loan ID).
    * Calculated the target variable, LGD (or its complement, Recovery Rate), based on funded amounts, collateral values, and total recovered amounts.
    * Performed thorough data cleaning:
        * **Missing Value Treatment:** Identified and handled missing values using appropriate imputation strategies (e.g., imputing with median for numerical features, mode for categorical features).
        * **Outlier Detection & Treatment:** Analyzed numerical features for outliers using techniques like boxplots and interquartile range (IQR). Applied outlier treatment methods such as quantile-based 
                                             capping/flooring to mitigate their influence.

2.  **Exploratory Data Analysis (EDA):**
    * Conducted univariate analysis to understand the distribution of individual features (histograms, density plots, descriptive statistics).
    * Performed bivariate analysis to explore relationships between predictor variables and the target variable (LGD/RR), as well as relationships among predictors (scatter plots, box plots segmented by 
      categories).
    * Generated a correlation heatmap to visualize linear relationships between numerical features and identify potential multicollinearity.

3.  **Feature Engineering & Scaling:**
    * Converted categorical features into a numerical format suitable for regression models using one-hot encoding (creating dummy variables).
    * Applied feature scaling using `StandardScaler` to standardize the range of numerical features, ensuring that variables with larger values do not disproportionately influence the model.

4.  **Model Building:**
    * Split the prepared dataset into training and testing sets to evaluate model generalization performance.
    * Developed and trained multiple regression models:
        * **Linear Regression:** Served as a baseline model.
        * **Ridge Regression (L2 Regularization):** Used to handle potential multicollinearity and prevent overfitting by adding a penalty based on the squared magnitude of coefficients.
        * **Lasso Regression (L1 Regularization):** Employed to handle multicollinearity and perform automatic feature selection by shrinking some coefficients exactly to zero.
    * Checked for multicollinearity among features using the Variance Inflation Factor (VIF) and refined feature sets if necessary.

5.  **Model Evaluation:**
    * Evaluated the performance of each model on both the training and testing datasets.
    * Used standard regression metrics:
        * **R-squared (R²)**: To measure the proportion of variance in LGD explained by the model.
        * **Mean Squared Error (MSE)** and **Root Mean Squared Error (RMSE)**: To quantify the average magnitude of prediction errors.
    * Compared the performance across models to select the most suitable one based on predictive accuracy and interpretability.

