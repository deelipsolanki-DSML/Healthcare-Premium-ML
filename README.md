# Predictive Health Insurance Model for S.H.I.E.L.D Insurance

## 📌 Project Overview

This project develops a machine learning system to predict **health insurance premium amounts** for an insurance firm.

The model uses customer information such as age, smoking status, medical history, BMI, insurance plan, marital status, income, and number of dependents to estimate the premium for new customers.

The project focuses not only on achieving a high **R² score**, but also on ensuring that the prediction error remains within an acceptable range for the majority of customers.

The final solution uses **model segmentation**, where customers are divided into different age-based groups and separate models are trained for each segment. The trained models are deployed through an interactive **Streamlit application** for use by insurance underwriters.

## 🎯 Problem Statement

The objective is to build a predictive model that can accurately estimate healthcare insurance premiums based on customer characteristics.

The primary project requirements were:

* Achieve an **R² score greater than 0.97**.
* Ensure that the percentage error between actual and predicted premiums is **less than 10% for at least 95% of test data**.
* Develop an interactive application that allows an underwriter to make predictions from anywhere.

The model is intended to support data-driven actuarial decisions, while final pricing decisions remain subject to professional judgment.

## 📊 Dataset

The project uses historical insurance data containing approximately **50,000 customer records**.

The dataset contains customer and insurance-related attributes that can be used to predict the annual premium amount.

The target variable is:

* `annual_premium_amount`

The available features include information related to:

* Age
* Gender
* Region
* Smoking status
* Medical history
* BMI
* Income
* Income level
* Marital status
* Employment status
* Number of dependents
* Insurance plan

## 🔍 Exploratory Data Analysis

Extensive EDA was performed to understand the relationship between customer characteristics and insurance premiums.

## ⚙️ Data Preprocessing

Several preprocessing and feature-engineering steps were performed before model training.

### Data Cleaning

* Standardized different representations of smoking status into consistent categories.
* Filled missing smoking-status values using disease status.
* Filled missing employment status using age-based patterns.
* Identified and treated outliers in age, income etc.
* Converted invalid negative dependent counts to absolute values.

### Medical History

Medical history contained multiple diseases in a single field separated by `&`.

Instead of treating this as a single categorical variable, it was separated into individual disease indicators such as:

* Diabetes
* High blood pressure
* No Disease
* Thyroid
* Heart disease

This allows a customer to have multiple disease indicators simultaneously.

### Feature Engineering & Selection

Additional feature engineering included:

* Creating a `have_disease` feature.
* Creating `n_disease`, representing the total number of diseases.
* Using correlation (`r_regression`) and mutual information to evaluate feature relevance.
* Removing **gender** and **region** due to their minimal contribution to premium prediction.

## 🤖 Machine Learning Models

Multiple models were evaluated.

### Linear Regression

Linear Regression was initially used as a baseline model.

* One-hot encoding was used for categorical variables.
* Numerical variables were scaled.
* 75% of the data was used for training and 25% for testing.
* Test R²: **0.929**

Ridge and Lasso regression were also explored, but they did not provide a meaningful improvement over the baseline.

### Random Forest

Random Forest significantly improved performance over Linear Regression.

* Initial test R²: **0.964**
* Feature-importance analysis was used to identify less useful features.
* Removing low-importance features reduced training overfitting while maintaining the same test performance.

### XGBoost

XGBoost achieved an R² score of approximately **0.972**, making it the best-performing model before error analysis and model segmentation.

Feature-importance analysis showed similar patterns to Random Forest, and a model using only the most important features maintained similar performance.

## 📈 Model Evaluation

Model performance was evaluated using:

* **R² score**
* Percentage prediction error between actual and predicted premiums

While the XGBoost model achieved an excellent **R² of 0.972**, further error analysis revealed that R² alone was not sufficient to satisfy the project's business requirement.

More than 29% of predictions had an error greater than 10%, with particularly large errors occurring in the **18–25 age group**.

This analysis led to the development of a segmented modeling approach.

## 🏆 Results

The final solution uses **Model Segmentation**.

Customers were divided into two groups:

1. **Age 18–25**
2. **All remaining age groups**

Separate models were trained for each segment. Additional training data focused on genetic risk was collected for the 18–25 group, and using the detailed disease information rather than only the total disease count further improved performance.

### Final Model Performance

| Segment        | Model         |  R² Score | Error < 10%     |
| -------------- | ------------- | --------: | --------------- |
| Age 18–25      | Random Forest | **0.985** | All predictions |
| Remaining ages | Random Forest | **0.999** | All predictions |

This segmented approach satisfied both the accuracy and prediction-error requirements of the project.

The final model was deployed as an interactive Streamlit application for practical use by insurance underwriters.

## 🛠️ Technologies Used

* **Python**
* **Pandas** – Data manipulation
* **NumPy** – Numerical computation
* **Matplotlib / Seaborn** – Data visualization
* **Scikit-learn** – Preprocessing, feature selection and machine learning
* **XGBoost** – Gradient boosting model
* **Streamlit** – Interactive web application

## 👤 Author

**Deelip Solanki**

Machine Learning / Data Science

Live Application: [Healthcare Premium ML](https://healthcare-premium-ml.streamlit.app/)
