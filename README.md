# Predicting Customer Churn for Interconnect Telecom Using Boosting Models

## Project Description

**Objective:**
The primary goal of this project is to develop a predictive model to identify customers of Interconnect, a telecom service provider, who are likely to churn. By identifying these at-risk customers early, Interconnect can implement targeted retention strategies, such as offering special promotions or customized service plans.

**Background:**
Interconnect offers landline and internet services, along with optional features like technical support, cloud backup, streaming services, and security software. Customers have a choice between month-to-month, one-year, or two-year contracts and utilize various billing methods. The marketing team has provided data encompassing customer demographics, subscription plans, service usage (internet and phone), and contract details. The target variable for prediction is customer churn, indicated by an `EndDate` other than 'No'.

## Approach

This project follows these key steps:

1.  **Data Integration & Cleaning:** Multiple datasets were merged, and fields such as `TotalCharges` were cleaned. Categorical variables were encoded, and missing values were appropriately handled.
2.  **Exploratory Data Analysis (EDA):** The project involved understanding the distribution of churn and identifying key features correlated with churn, such as contract type, payment method, and billing preferences.
3.  **Feature Engineering:** Relevant features were converted to numeric types, and one-hot encoding was applied to multi-class categorical variables.
4.  **Model Training:** Several boosting models were trained, including Gradient Boosting, XGBoost, LightGBM, and CatBoost. These models were evaluated using AUC-ROC and accuracy metrics.
5.  **Model Evaluation:** The performance of the trained models was compared to select the most effective algorithm for potential deployment.

## Key Metrics

* **AUC-ROC:** This metric is used to measure the model's capability to distinguish between customers who churned and those who did not.

## Technologies & Libraries Used

Based on the notebook, the project utilizes the following Python libraries:

* pandas
* numpy
* matplotlib
* seaborn
* scikit-learn (for model selection, preprocessing, and metrics)
* xgboost

## How to Use

1.  Clone the repository:
    ```bash
    git clone 
    ```
2.  Navigate to the project directory:
    ```bash
    ```
3.  Install the necessary dependencies:
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn xgboost jupyter
    ```
4.  Open the Jupyter Notebook:
    ```bash
    jupyter notebook notebook.ipynb
    ```

## Results and Insights

The EDA revealed that customers on month-to-month contracts and those using Fiber optic internet services tend to have higher churn rates. The Gradient Boosting Model (GBM) initially showed strong performance on the validation set, but a drop in AUC-ROC on the test set (from 0.8611 to 0.8122) suggested some overfitting. Key predictors identified by the GBM model included "TotalCharges," "InternetService_Fiber optic," and "Type_Two year" contract.

## Future Work

* Further hyperparameter tuning or regularization of the GBM model to address overfitting and improve generalization.
* Additional feature engineering.
* Exploring other modeling techniques or ensemble methods.

 
 # Summary Report

This report summarizes the project on predicting customer churn for Interconnect Telecom, based on the provided Jupyter Notebook. The project aimed to build a predictive model to identify customers likely to churn, enabling targeted retention strategies.

#### Project Plan and Execution

1. **Data Integration & Cleaning:** This step involved merging multiple datasets (contract.csv, personal.csv, internet.csv, phone.csv). The TotalCharges field was converted to a numeric type, and missing values were handled by filling NaNs with 0. Missing values in InternetService and related features (like OnlineSecurity, OnlineBackup, etc.), as well as MultipleLines, were filled with 'No', based on the assumption that these customers did not subscribe to those services.

2. **Exploratory Data Analysis (EDA):** The EDA focused on understanding churn distribution and identifying key features associated with churn. This included analyzing churn rates by contract type, internet service, and the distribution of monthly and total charges for churned vs. non-churned customers. A correlation analysis was also performed.

3. **Feature Engineering:** A binary target variable 'churn' was created based on the 'EndDate' column. Binary categorical features were label encoded, and multi-class categorical features (Type, gender, InternetService, PaymentMethod) were one-hot encoded to prepare the data for modeling. Unnecessary columns like customerID, BeginDate, and EndDate were dropped before splitting the data.

4. **Model Training:** Four different classification models were trained:
    Gradient Boosting Machine (GBM)
    
    XGBoost
    
    LightGBM
    
    Random Forest Hyperparameter tuning for these models was performed using RandomizedSearchCV with AUC-ROC as the primary scoring metric. The data was split into training (70%), validation (15%), and testing (15%) sets for robust model development and evaluation.

5. **Model Evaluation:** Models were evaluated on the validation set using AUC-ROC and accuracy scores. The Gradient Boosting Machine (GBM) was selected as the best-performing model on the validation set. This chosen GBM model was then further evaluated on the separate test set.

#### Difficulties Encountered and Solutions
Several data-related challenges were addressed:

**Missing TotalCharges:** 11 missing values in TotalCharges were identified. These were filled with 0, assuming that these customers might not have been billed yet or there was an error in data entry.

**Missing Internet Service and MultipleLines Data:** A significant number of missing values (1526 for internet-related columns, 682 for MultipleLines) were handled by filling them with 'No'. This was based on the assumption that missing data in these columns indicated the customer did not have the respective service.

**LightGBM Training Warnings:** During LightGBM model training, warnings like "No further splits with positive gain, best gain: -inf" and "Found whitespace in feature_names, replace with underlines" were observed. The whitespace issue was likely handled automatically by LightGBM, and the "No further splits" warning is a common occurrence in boosting models, indicating that further improvements in some tree branches couldn't be found with the current parameters.

**Overfitting of GBM Model:** A key difficulty identified in the conclusion was the drop in the GBM model's performance from the validation set (AUC-ROC: 0.8611) to the test set (AUC-ROC: 0.8122). This indicated some overfitting. The suggested solutions included further hyperparameter tuning or regularization of the GBM model.

**Fix Imbalances:** It was difficult to apply SMOTE to resolve imbalance issues to improve model quality. After applying SMOTE, there was a significant decrease in model quality.

#### Key Steps in Solving the Task

The critical steps in this churn prediction project included:

**Systematic Data Preprocessing:** This involved merging disparate datasets, converting data types (e.g., TotalCharges to numeric), and a reasoned approach to handling missing values for several key features.

**Effective Feature Engineering:** Creating the 'churn' target variable and transforming categorical features into a numerical format (label encoding and one-hot encoding) were crucial for model training.

**Insightful Exploratory Data Analysis:** Visualizing churn patterns against contract types, internet services, and charge amounts helped understand potential churn drivers.

**Rigorous Model Training and Selection:** The project involved training multiple models and using RandomizedSearchCV for hyperparameter optimization, focusing on AUC-ROC. The subsequent evaluation of both validation and test sets led to the selection of the final model.

**Identification of Model Limitations:** Recognizing the overfitting issue with the final GBM model and suggesting paths for improvement is a key part of a data science project lifecycle.

#### Final Model and Quality Score

The Gradient Boosting Machine (GBM) was selected as the final model.
On the validation set, the GBM model achieved:
* Accuracy: 0.7973 (reported as 0.7992 in the markdown after cell 217, but cell 217 output for GBM shows 0.7973)
*AUC-ROC: 0.8605 (reported as 0.8611 in the markdown after cell 217, but cell 217 output for GBM shows 0.8605)

On the test set, the final GBM model demonstrated the following quality scores:
*Accuracy: 0.7881
*AUC-ROC: 0.8122

The project concluded that while the GBM model provided a strong foundation, further refinement could enhance its robustness and predictive accuracy.
    
