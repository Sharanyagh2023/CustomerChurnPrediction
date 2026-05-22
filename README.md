# Customer Churn Prediction and Retention Strategy

## Project Title
Customer Churn Prediction and Retention Strategy for a Telecommunications Company

## Business Problem
Customer churn is a significant challenge for subscription-based businesses. This project aims to build a classification model to predict customer churn in a telecom company. The primary goal is to minimize **False Negatives** (customers predicted not to churn but who do) as losing a customer is more costly than spending resources on a loyal customer.

## Dataset Description
The dataset (`part_3_customer_churn_prediction.csv`) contains 1800 rows and 21 columns. It includes customer demographics, service information, billing details, and a target variable indicating churn status.
*   **Numerical Columns:** `Tenure`, `MonthlyCharges`, `TotalCharges`.
*   **Categorical Columns:** `Gender`, `SeniorCitizen`, `Partner`, `Dependents`, `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies`, `Contract`, `PaperlessBilling`, `PaymentMethod`, `Churn`.
*   **Target Variable:** `Churn` (binary: 'Yes'/'No').

## Data Cleaning and Preprocessing Summary
1.  **Missing Values:** 31 missing values in `TotalCharges` (corresponding to `Tenure=0`) were filled with `0` and the column was converted to `float64`.
2.  **Irrelevant Columns:** `CustomerID` was dropped.
3.  **Categorical Encoding:**
    *   `Churn` and other binary columns (`Gender`, `Partner`, `Dependents`, `PhoneService`, `PaperlessBilling`) were mapped to 0s and 1s.
    *   Service-related columns (`MultipleLines`, `OnlineSecurity`, etc.) were simplified by mapping 'No phone service'/'No internet service' to 'No', then encoded to 0s and 1s.
    *   Multi-category columns (`InternetService`, `Contract`, `PaymentMethod`) were **One-Hot Encoded** using `drop_first=True`.
4.  **Numerical Scaling:** `Tenure`, `MonthlyCharges`, and `TotalCharges` were scaled using `StandardScaler`.
5.  **Data Splitting:** The dataset was split into 80% training and 20% testing sets using `train_test_split` with `stratify=y` to maintain churn class distribution.

## EDA Insights
Key findings from the Exploratory Data Analysis:
*   **Overall Churn Rate:** Approximately **35.94%** of customers churned, indicating class imbalance.
*   **Churn by Contract Type:** **Month-to-month contracts** showed significantly higher churn rates (~52%).
*   **Churn by Tenure:** **Newer customers (0-12 months tenure)** had the highest churn rate (~42.3%), which decreased with increasing tenure.
*   **Churn by Monthly Charges:** Customers with **higher monthly charges** tended to churn more.
*   **Churn by Payment Method:** Customers using **'Electronic check'** exhibited a notably higher churn rate (~44.8%).
*   **Churn by Internet Service Type:** **'Fiber optic' internet service users** had a significantly higher churn rate (~47.8%).
*   **Churn by Senior Citizen Status:** Senior citizens showed a slightly higher churn rate (~38.2%).
*   **Relationship between Tenure, Charges, and Churn:** Short-tenure, high-monthly-charge customers represent a high-risk group.

## Models Used
1.  **Logistic Regression**
2.  **Decision Tree Classifier**

## Model Evaluation Results

| Metric (Churn=1) | Logistic Regression | Decision Tree |
| :--------------- | :------------------ | :------------ |
| Accuracy         | 0.7389              | 0.6222        |
| Precision        | 0.6606              | 0.4701        |
| Recall           | 0.5581              | 0.4264        |

## Confusion Matrix Explanation (for Churn Prediction)
*   **True Positive (TP):** Correctly predicted churners. We can intervene.
*   **True Negative (TN):** Correctly predicted non-churners. No unnecessary intervention.
*   **False Positive (FP):** Predicted churn, but customer stayed. Wasted retention efforts (less severe).
*   **False Negative (FN):** Predicted no churn, but customer churned. Missed opportunity to save customer (more costly).

## Final Model Selection
Based on the business objective, **Logistic Regression** was selected as the most suitable model. This is because **Recall for the 'Churn' class (1)** is the most crucial metric, as False Negatives (missing actual churners) are more costly. Logistic Regression achieved a higher Recall (0.5581) compared to the Decision Tree (0.4264), making it better at identifying potential churners.

## Retention Strategy
Key recommendations based on EDA and Logistic Regression insights:
1.  **Target New Customers (0-12 Months Tenure):** Implement enhanced onboarding and early intervention programs. New customers churn more; address this with personalized check-ins and proactive outreach.
2.  **Incentivize Longer-Term Contracts:** Offer attractive discounts for switching to one or two-year contracts. Month-to-month contracts lead to higher churn.
3.  **Address Fiber Optic Internet Customer Dissatisfaction:** Investigate service quality and competition for fiber optic users. These customers have a high churn rate.
4.  **Optimize Payment Method Experience (Electronic Check):** Investigate pain points and promote alternative, more stable payment methods. Electronic check users churn more frequently.
5.  **Enhance Customer Support and Security Offerings:** Actively promote and bundle services like Tech Support and Online Security. Lack of these services increases churn.
6.  **Address High Monthly Charges and Senior Citizen Needs:** Reassess value for high spenders and tailor plans for senior citizens. Both groups show elevated churn.
7.  **Implement Predictive Churn Alerts:** Develop an automated system to flag high-risk customers for personalized retention campaigns. The model identifies customers at various risk levels.

## How to Run the Project
This project is developed in a Google Colab notebook. To run it:
1.  **Open the Notebook:** Click on the provided Colab link.
2.  **Run Cells:** Execute each code cell sequentially. You can use the 'Run all' option or click the play button on each cell.
3.  **Review Outputs:** Observe the printed outputs, dataframes, and visualizations to follow the analysis and results.
