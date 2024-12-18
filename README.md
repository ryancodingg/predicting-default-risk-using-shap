# predicting-default-risk-using-shap

# Credit Default Prediction Model

## 1.1 Purpose
The purpose of this project is to develop a machine learning model that predicts the likelihood of credit card default based on various customer features. The model will help financial institutions assess risk, improve lending decisions, and minimize defaults.

## 1.2 Scope
This repository contains all code, documentation, and resources to implement the credit default prediction model. The scope includes data preprocessing, exploratory data analysis (EDA), feature engineering, model development using XGBoost, and SHAP value interpretation.

## 1.3 Definitions, Acronyms, and Abbreviations
- **EDA**: Exploratory Data Analysis
- **SHAP**: SHapley Additive exPlanations
- **SMOTE**: Synthetic Minority Over-sampling Technique
- **ROC-AUC**: Receiver Operating Characteristic - Area Under Curve

---

## 2. Project Overview

### 2.1 Problem Statement
Credit default prediction is critical for financial institutions to mitigate risks. Customers with lower credit limits and poor repayment histories are more likely to default on their payments. This model aims to identify at-risk customers early, enabling institutions to take appropriate actions.

### 2.2 Stakeholders
- **Financial Institutions**: Users of the model to assess credit risk and make lending decisions.
- **Data Scientists**: Responsible for model development, data preprocessing, and feature engineering.
- **Business Analysts**: Use model predictions to inform business strategies.
- **Customers**: End-users whose data is used to train and test the model.

---

## 3. Requirements

### 3.1 Functional Requirements
- The system should be able to predict if a customer will default on their credit card payments.
- The system should display predictions with a confidence score.
- The system should allow easy integration into existing financial systems.

### 3.2 Non-Functional Requirements
- **Performance**: The model should make predictions within 3 seconds.
- **Scalability**: The model should handle large volumes of data.
- **Security**: Sensitive data must be protected during processing and storage.

---

## 4. Methodology

### 4.1 Data Collection and Preprocessing

#### 4.1.1 Cleaning Data (Missing Values, Outliers, and Inconsistencies)
Data was collected from a customer credit dataset and preprocessed by handling missing values, removing outliers, and resolving inconsistencies.

- **Missing Values**: Imputed or removed based on the nature of the missing data.
- **Outliers**: Detected and handled using IQR (Interquartile Range) or Z-scores.
- **Inconsistencies**: Standardized categorical variables and transformed text data into useful features.

### 4.2 Exploratory Data Analysis (EDA)
- **Credit Limit & Default Risk**: Defaulters had significantly lower median credit limits than non-defaulters, with median values of 100,000 NT$ and 200,000 NT$, respectively.
- **Repayment History**: A strong correlation was found between repayment statuses (PAY_0 to PAY_6), influencing future payment behavior.
- **Age Distribution**: Younger customers (20-30 years) had a higher default rate.

For detailed visualizations, check the [Google Colab EDA notebook](https://colab.research.google.com/github/ryancodingg/predicting-default-risk-using-shap/blob/main/Project2_TAP.ipynb).

### 4.3 Feature Engineering for Default Prediction

#### 4.3.1 Feature Importance of Numerical Features
Numerical features such as **credit limit**, **age**, and **repayment status** were transformed and scaled to improve model accuracy. Feature importance was assessed using SHAP values.

### 4.4 Model Development

#### 4.4.1 Implementing XGBoost
XGBoost was selected due to its robustness in handling structured data and its ability to handle class imbalance.

```python
from xgboost import XGBClassifier
model = XGBClassifier()
model.fit(X_train, y_train)
```

#### 4.4.2 Performance Metrics: Accuracy, Precision, Recall, F1-Score, ROC-AUC
The model's performance was evaluated using multiple metrics:
- **Accuracy**: Overall correctness of the model.
- **Precision**: Proportion of true positives among all predicted positives.
- **Recall**: Proportion of true positives among all actual positives.
- **F1-Score**: Harmonic mean of precision and recall.
- **ROC-AUC**: Area under the ROC curve, which measures the model’s ability to distinguish between classes.

### 4.5 SHAP Value Integration & Interpretation

#### 4.5.1 Explaining Model Predictions Using SHAP
SHAP was integrated to explain the model’s predictions by identifying the contribution of each feature to the predicted outcomes. 

#### 4.5.2 New Features Created After SHAP Analysis
Based on SHAP insights, new features were created by transforming existing ones. Features such as **repayment behavior over time** were derived to improve model interpretability.

#### 4.5.3 Visualizing Feature Impact with SHAP Plots
- **SHAP Waterfall Plot**: Used to explain how each feature contributed to a specific prediction.
- **Feature Impact**: SHAP plots were used to visualize the most influential features in predicting defaults.

[Visualize SHAP plots](https://colab.research.google.com)

#### 4.5.4 Handling Class Imbalance (SMOTE/Undersampling)
To address the class imbalance between defaulters and non-defaulters, **SMOTE (Synthetic Minority Over-sampling Technique)** was used to generate synthetic examples of the minority class.

### 4.6 Model Fairness Testing

#### 4.6.1 Assessing Model Fairness
Fairness testing was performed to ensure the model did not favor one group over another. Metrics like **equal opportunity** and **demographic parity** were assessed.

#### 4.6.2 Libraries and Techniques for Fairness Testing
The fairness of the model was evaluated using Python libraries like **AIF360** and **Fairness Indicators**, which assess fairness across different groups (e.g., age, gender).

---

## 5. Model Evaluation

### 5.1 Model Validation and Cross-Validation
The model was validated using **k-fold cross-validation** to ensure generalization across different subsets of the dataset. This helped prevent overfitting and improved the robustness of the model.

### 5.2 SHAP Insights and Adjustments to the Model
SHAP insights were used to adjust the model by focusing on high-impact features and reducing unnecessary complexity, thus improving model interpretability and performance.

---

## 6. Conclusion and Recommendations

### 6.1 Conclusion
The credit default prediction model effectively identifies customers at high risk of default based on key features like **credit limits** and **repayment history**. The integration of SHAP provides transparency, helping stakeholders understand the model's decisions.

### 6.2 Recommendations
- **Continuous Model Updates**: Retrain the model with new data to maintain accuracy.
- **Feature Expansion**: Incorporate more granular features like **spending behavior** or **transaction history** to improve predictions.
- **Real-Time Predictions**: Develop real-time prediction capabilities for dynamic credit risk assessment.

---

## 7. Future Scope

### 7.1 Future Scope
- **Deep Learning Integration**: Implement deep learning models for handling larger datasets and improving prediction accuracy.
- **Alternate Data Sources**: Integrate non-traditional data sources (e.g., social media activity) to enhance the model's predictive power.
- **Deployment to Production**: Scale the model for production environments with real-time prediction capabilities and further optimize deployment pipelines.

---

## 8. Installation

### 8.1 Prerequisites

- Python 3.x
- Required libraries can be installed using the `requirements.txt` file.

### 8.2 Installation Steps

Visit this repository:
```bash
git clone https://github.com/ryancodingg/predicting-default-risk-using-shap
```

Install dependencies:
```bash
pip install -r requirements.txt
```

Run the model:
```bash
python run_model.py
```

For Colab-based execution, visit the [Google Colab Notebook](https://colab.research.google.com/github/ryancodingg/predicting-default-risk-using-shap/blob/main/Project2_TAP.ipynb).

---

## 9. License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 10. Acknowledgments

- Neubauer, D., et al. (2022). *Understanding Credit Risk Prediction Models: Insights and Applications*. Journal of Financial Technology, 45(2), 112-130.
- Google Collaboration link - https://colab.research.google.com/github/ryancodingg/predicting-default-risk-using-shap/blob/main/Project2_TAP.ipynb
- SHAP documentation: [https://shap.readthedocs.io](https://shap.readthedocs.io)
- SMOTE implementation: [https://imbalanced-learn.org](https://imbalanced-learn.org)

---

This updated README includes comprehensive project information, from problem statement and methodology to detailed setup instructions, visual links, and references. The integration of Google Colab ensures users can quickly get started with the code and visualizations directly in the cloud environment.
