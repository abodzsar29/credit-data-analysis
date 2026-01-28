# German Renewable Energy Loan Startup - Credit Risk Analysis Case Study

**Author:** Andrew Bodzsar

## Project Overview

This project presents a data science case study for SolaraNova, a company facilitating homeowner financing for renewable energy installations (e.g., PV systems, heat pumps). As SolaraNova grows, enhancing underwriting efficiency, risk management, and loan pricing becomes essential for improving margins and scalability.

This analysis utilizes customer loan data to:
*   Evaluate key credit risk factors.
*   Uncover insights for optimizing loan pricing.
*   Predict loan repayment behaviors and the likelihood of default.

The primary analysis and model development are documented in the `DS_Project_AndrewB.ipynb` Jupyter Notebook.

## Problem Statement & Objectives

The main objective is to apply data science techniques to the provided loan dataset to improve SolaraNova's financial operations and risk assessment capabilities. The key goals include:

1.  **Data Exploration and Cleaning:** Process the raw data, handle inconsistencies (missing values, outliers), and derive meaningful summary statistics.
2.  **Risk Profiling:** Develop a system to segment customers into Low, Medium, and High-risk categories based on financial and behavioral indicators.
3.  **Predictive Modeling:** Build a predictive model to estimate loan default probability using relevant customer and loan features.
4.  **Model Integration Strategy:** Propose a framework for deploying the developed model into a live operational environment.

## Dataset Description

The analysis is based on datasets provided in CSV format:

1.  **`loandata_table - Loan Data.csv`**: The core dataset containing detailed information about each loan and customer, including:
    *   Customer demographics (age, employment years)
    *   Financial details (annual income, property value, loan amount, interest rate, debt levels)
    *   Credit information (SCHUFA score, credit lines, utilization, defaults)
    *   Installation specifics (system size, estimated production/savings)
    *   Payment behavior summaries (avg/max days late, payment standard deviation)
    *   Derived ratios (income-to-loan, debt-to-income, loan-to-value, etc.)
    *   The target variable: `default_flag`.

2.  **`schufa_credit_rating - Schufa PD 12 Distribution.csv`**: Contains mappings between SCHUFA rating levels (e.g., A, B, C) and their corresponding score ranges and Probability of Default (PD-12 Hypo).

3.  **`payment_history.csv`**: Contains a comprehensive payment tracking record with 12,000 entries. It includes customer IDs, payment and due dates, amount due, amount paid, and days late for each transaction.

Several key features within the main loan data table were derived or calculated based on relationships described in the notebook (e.g., various financial ratios, payment behavior metrics).

## Methodology & Tasks Performed

The analysis within `DS_Project_AndrewB.ipynb` proceeds as follows:

1.  **Data Exploration and Cleaning:**
    *   Loading datasets using pandas
    *   Systematic identification and imputation of missing values for `property_value`, `credit_utilization`, and `employment_years` using logical calculations or group-based statistics (medians/means).
    *   Generation of descriptive statistics for core loan characteristics.

2.  **Risk Profiling:**
    *   Implementation of a rule-based scoring system assigning points based on factors like SCHUFA score, debt-to-income ratio, payment lateness, previous defaults, and income-to-loan ratio.
    *   Segmentation of customers into **Low**, **Medium**, and **High** risk tiers based on cumulative risk scores.
    *   Analysis and visualization (using matplotlib/seaborn) of customer distribution, default rates per category, and average financial metrics (like income) across risk segments.

3.  **Predictive Modeling:**
    *   Feature selection focusing on variables likely predictive of default (e.g., `late_payments_90`, `schufa_score`, `previous_defaults`, `age`).
    *   Data splitting into stratified training (70%) and testing (30%) sets based on the `default_flag`.
    *   Feature scaling using `StandardScaler` from scikit-learn.
    *   Training a **Logistic Regression** model with balanced class weights to predict default probability.
    *   Model evaluation using standard metrics: Accuracy, AUC, Confusion Matrix, and Classification Report (Precision, Recall, F1-Score).
    *   Assessment of feature importance through model coefficients.
    *   Visualization of model performance (ROC Curve) and insights (Feature Importance, Predicted Probability Distribution).

4.  **Data Management & Model Integration:**
    *   A conceptual proposal for deploying the model, including:
        *   **Architecture:** Frontend (JS), Backend (Flask API), Database (PostgreSQL), modular services.
        *   **Data Flow:** From frontend submission to backend validation, cleaning, risk/default prediction storage, and results retrieval.
        *   **CI/CD & Monitoring:** Suggestion of tools like Docker, Kubernetes, Jenkins, Gunicorn, Nginx, Prometheus/Grafana, ELK/Sentry.
        *   **Maintenance & Retraining:** Suggestion of tools for code quality (Black/Flake8), testing (pytest), ML lifecycle (MLflow), scheduling (Airflow), and security (Bandit).

## Key Findings & Results

*   Data imputation techniques successfully addressed missing data points, creating a more complete dataset for analysis.
*   The risk profiling method demonstrated a strong ability to differentiate customer segments based on default risk, with the High-risk category showing significantly higher default rates.
*   The Logistic Regression model performed well on the test set (Accuracy ~0.99, AUC ~0.99), indicating good predictive power for loan defaults within this dataset.
*   Credit score (`schufa_score`), severe payment lateness (`late_payments_90`), and past defaults (`previous_defaults`) were identified as the most influential factors in predicting default.
*   A practical strategy for model deployment and MLOps (Machine Learning Operations) was outlined, focusing on automation, monitoring, and maintainability./<
