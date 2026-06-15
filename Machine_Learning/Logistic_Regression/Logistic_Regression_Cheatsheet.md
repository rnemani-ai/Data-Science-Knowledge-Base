# Logistic Regression Cheat Sheet

## Quick Summary

| Property           | Value               |
| ------------------ | ------------------- |
| Algorithm Type     | Supervised Learning |
| Problem Type       | Classification      |
| Output             | Probability         |
| Decision Boundary  | Linear              |
| Explainability     | High                |
| Training Speed     | Fast                |
| Prediction Speed   | Fast                |
| Probability Output | Yes                 |
| Interpretability   | Excellent           |

---

# Data Preparation Requirements

| Requirement             | Needed?       |
| ----------------------- | ------------- |
| Missing Value Handling  | ✅ Yes         |
| Feature Scaling         | ✅ Recommended |
| Categorical Encoding    | ✅ Required    |
| Outlier Treatment       | ⚠ Recommended |
| Feature Selection       | ✅ Recommended |
| Multicollinearity Check | ✅ Important   |

---

# Core Workflow

```text
Features
    ↓
Linear Combination
    ↓
Log Odds
    ↓
Sigmoid Function
    ↓
Probability
    ↓
Threshold
    ↓
Prediction
```

---

# Key Formulas

### Linear Combination

z = β₀ + β₁x₁ + β₂x₂ + ... + βₙxₙ

---

### Sigmoid Function

Probability = 1 / (1 + e⁻ᶻ)

Output Range:

0 to 1

---

### Odds

Odds = p / (1-p)

Example:

p = 0.8

Odds = 4

Meaning:

Success is 4 times more likely than failure.

---

### Log Odds

Log Odds = log(p/(1-p))

Range:

-∞ to +∞

---

# Output

### Primary Output

Probability

Example:

0.85

Interpretation:

85% probability of belonging to the positive class.

---

### Secondary Output

Class Label

Default Threshold:

0.5

```text
Probability > 0.5 → Class 1

Probability ≤ 0.5 → Class 0
```

---

# Objective Function

Goal:

Maximize Likelihood

Equivalent:

Minimize Negative Log Likelihood

Technique:

Maximum Likelihood Estimation (MLE)

---

# Cost Function

### Binary Cross Entropy (Log Loss)

Purpose:

Measure how well predicted probabilities match actual outcomes.

Characteristics:

✅ Penalizes confident wrong predictions

✅ Supports probability estimation

✅ Works well with MLE

---

# Why Not Mean Squared Error?

MSE:

❌ Poor probability estimation

❌ Less effective optimization

Log Loss:

✅ Better gradients

✅ Better optimization

✅ Better probability predictions

---

# Optimization

Common Methods:

* Gradient Descent
* Stochastic Gradient Descent (SGD)
* Mini-Batch Gradient Descent

Goal:

Minimize Log Loss

---

# Assumptions

✅ Independent observations

✅ Linear relationship between features and log-odds

✅ No severe multicollinearity

✅ Adequate sample size

✅ Limited influence of extreme outliers

---

# Bias-Variance Profile

| Metric            | Level    |
| ----------------- | -------- |
| Bias              | High     |
| Variance          | Low      |
| Overfitting Risk  | Low      |
| Underfitting Risk | Moderate |

Interpretation:

* Stable model
* Good generalization
* May miss complex relationships

---

# Regularization

| Method      | Purpose              |
| ----------- | -------------------- |
| L1 (Lasso)  | Feature Selection    |
| L2 (Ridge)  | Shrinks Coefficients |
| Elastic Net | L1 + L2              |

---

# Multiclass Classification

### One-vs-Rest (OvR)

Activation:

Sigmoid

Loss:

Binary Cross Entropy

Approach:

One classifier per class.

---

### Multinomial Logistic Regression

Activation:

Softmax

Loss:

Categorical Cross Entropy

Approach:

Single model for all classes.

---

# Sigmoid vs Softmax vs Tanh

| Function | Range            | Use Case                         |
| -------- | ---------------- | -------------------------------- |
| Sigmoid  | 0 to 1           | Binary Classification            |
| Softmax  | 0 to 1 (sum = 1) | Multiclass Classification        |
| Tanh     | -1 to 1          | Hidden Layers in Neural Networks |

---

# Coefficient Interpretation

### Positive Coefficient

↑ Increases probability of positive class

---

### Negative Coefficient

↓ Decreases probability of positive class

---

### Odds Ratio

Odds Ratio = exp(coefficient)

Example:

Coefficient = 0.69

Odds Ratio ≈ 2

Interpretation:

One-unit increase doubles the odds.

---

# Evaluation Metrics

## Balanced Dataset

* Accuracy
* Precision
* Recall
* F1
* ROC-AUC

---

## Imbalanced Dataset

Preferred:

* Precision
* Recall
* F1
* PR-AUC

Avoid relying only on Accuracy.

---

# Confusion Matrix

|                 | Predicted Positive | Predicted Negative |
| --------------- | ------------------ | ------------------ |
| Actual Positive | TP                 | FN                 |
| Actual Negative | FP                 | TN                 |

---

### Precision

TP / (TP + FP)

Question:

Of predicted positives, how many were correct?

---

### Recall

TP / (TP + FN)

Question:

Of actual positives, how many did we identify?

---

### F1 Score

2 × Precision × Recall / (Precision + Recall)

Best when:

Precision and Recall both matter.

---

# Decision Boundary

Logistic Regression:

✅ Linear

Decision Tree:

✅ Non-Linear

Random Forest:

✅ Non-Linear

XGBoost:

✅ Non-Linear

Neural Networks:

✅ Highly Non-Linear

---

# Feature Engineering Checklist

Before Training:

☐ Handle Missing Values

☐ Encode Categoricals

☐ Scale Numerical Variables

☐ Check Multicollinearity

☐ Remove Leakage

☐ Handle Outliers

☐ Select Important Features

---

# Common Production Challenges

* Class Imbalance
* Feature Leakage
* Data Drift
* Feature Drift
* Threshold Selection
* Probability Calibration
* Missing Values
* Multicollinearity

---

# Monitoring Metrics

Model Metrics:

* Precision
* Recall
* F1
* ROC-AUC
* PR-AUC
* Log Loss

Data Metrics:

* Missing Values
* Feature Drift
* Population Stability Index (PSI)

Business Metrics:

* Fraud Detection Rate
* Default Rate
* Churn Rate
* Conversion Rate

---

# When To Use

✅ Binary Classification

✅ Explainability Required

✅ Regulatory Environments

✅ Probability Outputs Needed

✅ Small to Medium Datasets

✅ Fast Deployment

Examples:

* Loan Default Prediction
* Fraud Detection
* Customer Churn
* Insurance Risk Scoring
* Disease Prediction
* Marketing Conversion

---

# When Not To Use

❌ Highly Non-Linear Relationships

❌ Complex Feature Interactions

❌ Image Classification

❌ NLP Tasks

❌ Large Unstructured Data

Alternatives:

* Random Forest
* XGBoost
* Neural Networks
* Transformers

---

# Advantages

* Highly Interpretable
* Easy to Explain
* Fast Training
* Fast Inference
* Produces Probabilities
* Strong Baseline Model
* Regulatory Friendly

---

# Limitations

* Linear Decision Boundary
* Sensitive to Multicollinearity
* Limited Feature Interactions
* May Underfit Complex Data
* Requires Feature Engineering

---

# Senior Data Scientist Summary

**Use Logistic Regression when you need:**

* Explainability
* Transparency
* Regulatory Compliance
* Probability-Based Decisions
* Fast Deployment

**Think of Logistic Regression as:**

"Simple, explainable, probabilistic baseline model for structured classification problems."

**Typical Domains**

* Banking
* Insurance
* Healthcare
* Risk Management
* Fraud Analytics
* Customer Analytics
