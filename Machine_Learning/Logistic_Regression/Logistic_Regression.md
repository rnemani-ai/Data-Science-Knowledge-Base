# Logistic Regression

## What is Logistic Regression?

Logistic Regression is a supervised machine learning algorithm primarily used for classification problems. It predicts the probability that an observation belongs to a particular class.

Examples:

* Will a customer churn?
* Will a loan applicant default?
* Is a transaction fraudulent?
* Will a customer click an advertisement?

Unlike Linear Regression, which predicts continuous values, Logistic Regression predicts probabilities between 0 and 1.

---

# Data Preparation Requirements

| Requirement             | Needed?       | Notes                                                   |
| ----------------------- | ------------- | ------------------------------------------------------- |
| Missing Value Handling  | ✅ Yes         | Logistic Regression cannot handle null values directly  |
| Feature Scaling         | ✅ Recommended | Improves optimization and coefficient stability         |
| Categorical Encoding    | ✅ Required    | Model accepts only numeric features                     |
| Outlier Treatment       | ⚠ Recommended | Extreme values can impact coefficients                  |
| Feature Selection       | ✅ Recommended | Improves interpretability and reduces overfitting       |
| Multicollinearity Check | ✅ Important   | Highly correlated features can destabilize coefficients |
| Explainability          | ⭐ Excellent   | One of the most interpretable ML models                 |
| Probability Output      | ✅ Yes         | Produces calibrated probability scores                  |

---

## Feature Scaling

Required?

✅ Recommended

Why?

Logistic Regression uses Gradient Descent for optimization.

Features with very different scales can slow convergence and make optimization less efficient.

Example:

* Income = 100000
* Age = 35

Without scaling, Income dominates optimization.

Common Approaches:

* StandardScaler
* MinMaxScaler

---

## Categorical Encoding

Required?

✅ Yes

Why?

Logistic Regression can only process numerical values.

Example:

Gender

* Male
* Female

Must be converted into numeric format.

Common Approaches:

* One-Hot Encoding
* Target Encoding
* Frequency Encoding

Most Common:

One-Hot Encoding

---

## Missing Values

Required?

✅ Must be handled

Why?

Logistic Regression cannot train on null values.

Approaches:

* Mean Imputation
* Median Imputation
* Mode Imputation
* Model-Based Imputation

---

## Outlier Handling

Required?

⚠ Recommended

Why?

Extreme values can influence coefficient estimates.

Approaches:

* Winsorization
* Capping
* Log Transformation

---

## Multicollinearity Check

Required?

✅ Important

Why?

Highly correlated variables can:

* Produce unstable coefficients
* Increase variance
* Reduce interpretability

Detection:

* Correlation Matrix
* Variance Inflation Factor (VIF)

---

# Intuition

Suppose a bank wants to predict whether a customer will default on a loan.

Target Variable:

* 1 = Default
* 0 = No Default

Customer Features:

* Credit Score
* Annual Income
* Debt-to-Income Ratio
* Number of Delinquencies

Instead of directly predicting "Default" or "No Default", Logistic Regression predicts:

Probability(Default) = 0.82

Interpretation:

The model estimates an 82% probability that the customer will default.

A threshold is then applied:

* Probability > 0.5 → Default
* Probability ≤ 0.5 → No Default

---

# Why Do We Need Logistic Regression?

Linear Regression can generate values below 0 and above 1.

Example:

Predicted Default Probability = 1.7

or

Predicted Default Probability = -0.4

These are invalid probabilities.

Logistic Regression solves this problem by transforming predictions into a valid probability range between 0 and 1.

---

# Internal Working

The model works in four major steps.

## Step 1: Linear Combination

The model first computes a weighted sum of all features.

Examples:

* Credit Score
* Income
* Debt Ratio
* Delinquencies

Each feature contributes based on its coefficient.

The output at this stage can range from negative infinity to positive infinity.

---

## Step 2: Convert to Log Odds

Instead of directly modeling probability, Logistic Regression models log odds.

Why?

Because probabilities are restricted between 0 and 1.

Log odds can take any value from negative infinity to positive infinity, making them easier to model using a linear equation.

---

## Step 3: Apply Sigmoid Function

The Sigmoid Function converts log odds into a probability.

Properties:

* Output always lies between 0 and 1
* Smooth and differentiable
* Supports gradient-based optimization

Examples:

Input = -10 → Output ≈ 0

Input = 0 → Output = 0.5

Input = 10 → Output ≈ 1

---

## Step 4: Apply Threshold

Default threshold:

0.5

Example:

Probability = 0.87

Prediction = Class 1

Probability = 0.21

Prediction = Class 0

---

# What Is The Output?

Primary Output:

Probability

Example:

0.92

Interpretation:

The model estimates a 92% chance that the observation belongs to the positive class.

Secondary Output:

Class Label

Example:

* 1 = Default
* 0 = No Default

Most business systems use both:

* Probability for risk scoring
* Class label for automation

---

# How To Interpret The Output

Suppose:

Probability(Default) = 0.85

Interpretation:

The model estimates an 85% probability that the customer will default.

This does NOT mean:

"85 out of 100 identical customers will definitely default."

It means:

"Based on historical patterns, this customer exhibits characteristics similar to customers who defaulted in the past."

---

# Decision Boundary

A decision boundary separates one class from another.

In Logistic Regression:

Decision Boundary = Linear

Example:

If Probability > 0.5

Predict Class 1

Else

Predict Class 0

Compared to other models:

* Logistic Regression → Linear Boundary
* Decision Trees → Non-linear Boundary
* Random Forest → Non-linear Boundary
* XGBoost → Non-linear Boundary

---

# Objective Function

Objective:

Estimate probabilities that best explain the observed data.

Logistic Regression tries to maximize the likelihood of observing the training labels.

Equivalent Objective:

Minimize Negative Log Likelihood.

---

# Maximum Likelihood Estimation (MLE)

MLE is a statistical technique used to estimate model parameters.

Goal:

Find coefficients that maximize the probability of observing the training data.

Instead of minimizing prediction error directly, Logistic Regression searches for parameters that make the observed outcomes most likely.

This is why Logistic Regression is fundamentally a probabilistic model.

---

# Cost Function

Logistic Regression uses:

Binary Cross Entropy (Log Loss)

Purpose:

Measure how well predicted probabilities match actual outcomes.

Key Characteristic:

The model receives a large penalty when it makes confident but incorrect predictions.

Example:

Actual = 1

Prediction = 0.99

Small penalty

Actual = 1

Prediction = 0.01

Large penalty

---

# Why Not Mean Squared Error?

MSE works well for Linear Regression.

For Logistic Regression:

* Creates optimization challenges when combined with the sigmoid function
* Produces poorer gradients
* Slower convergence

Log Loss:

* Better optimization behavior
* Better probability estimation
* Aligns with Maximum Likelihood Estimation

---

# Optimization

Logistic Regression typically uses:

* Gradient Descent
* Stochastic Gradient Descent (SGD)
* Mini-Batch Gradient Descent

Goal:

Find coefficients that minimize Log Loss.

---

# Assumptions

Logistic Regression makes the following assumptions:

* Independent observations
* Linear relationship between features and log-odds
* No severe multicollinearity
* Adequate sample size
* Limited influence from extreme outliers

Unlike Linear Regression, Logistic Regression does not require:

* Normally distributed features
* Homoscedasticity
* Normally distributed residuals

Why do assumptions matter?

Violating assumptions can lead to:

* Unstable coefficients
* Reduced interpretability
* Poor calibration
* Lower predictive performance

---

# Feature Engineering Considerations

Feature engineering often has a larger impact on Logistic Regression performance than the choice of algorithm itself.

## Feature Scaling

Logistic Regression is sensitive to feature magnitudes.

Common approaches:

* Standardization
* Normalization

## Handling Missing Values

Common methods:

* Mean Imputation
* Median Imputation
* Mode Imputation
* Model-Based Imputation

## Handling Categorical Variables

Common approaches:

* One-Hot Encoding
* Target Encoding
* Frequency Encoding

## Feature Selection

Methods:

* Correlation Analysis
* VIF
* L1 Regularization
* Recursive Feature Elimination

## Interaction Features

Example:

Income × Credit Score

Captures relationships that individual variables may miss.

## Outlier Treatment

Methods:

* Capping
* Winsorization
* Log Transformation

## Multicollinearity Checks

Always check:

* Correlation Matrix
* VIF

High multicollinearity can make coefficient interpretation unreliable.
