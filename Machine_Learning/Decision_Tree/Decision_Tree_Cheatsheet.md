# Decision Tree Cheat Sheet

## Quick Summary

| Property           | Value                       |
| ------------------ | --------------------------- |
| Algorithm Type     | Supervised Learning         |
| Problem Type       | Classification & Regression |
| Decision Boundary  | Non-Linear                  |
| Explainability     | High                        |
| Training Speed     | Fast                        |
| Prediction Speed   | Fast                        |
| Probability Output | Yes                         |
| Interpretability   | Excellent                   |

---

# Data Preparation Requirements

| Requirement             | Needed?                     |
| ----------------------- | --------------------------- |
| Missing Value Handling  | ⚠ Depends on implementation |
| Feature Scaling         | ❌ Not Required              |
| Categorical Encoding    | ✅ Required                  |
| Outlier Treatment       | ❌ Usually Not Required      |
| Feature Selection       | ❌ Usually Not Required      |
| Multicollinearity Check | ❌ Not Required              |

---

# Core Workflow

```text
Dataset
    ↓
Evaluate Splits
    ↓
Calculate Impurity
    ↓
Choose Best Split
    ↓
Split Data
    ↓
Repeat Recursively
    ↓
Leaf Node
    ↓
Prediction
```

---

# Tree Components

### Root Node

Starting point of the tree.

---

### Internal Node

Decision point based on a feature.

Example:

Income > 50,000

---

### Branch

Outcome of a decision.

Example:

Yes / No

---

### Leaf Node

Final prediction.

---

# Objective

Goal:

Create the purest possible child nodes after every split.

For Classification:

Minimize impurity.

For Regression:

Minimize prediction error.

---

# Splitting Criteria

## Entropy

Measures impurity.

### Interpretation

Entropy = 0

Pure Node

Entropy = 1

Maximum Disorder

---

## Information Gain

Measures reduction in entropy.

Formula Intuition:

Information Gain = Parent Entropy − Child Entropy

Choose split with highest Information Gain.

---

## Gini Impurity

Most common splitting criterion.

Used by:

* CART
* Scikit-Learn DecisionTreeClassifier

Interpretation:

Lower Gini = Better Split

Pure Node:

Gini = 0

---

# CART

Classification And Regression Trees

Characteristics:

* Binary Splits
* Uses Gini Impurity
* Most widely used implementation

---

# ID3 vs C4.5 vs CART

| Algorithm | Split Type | Criterion  |
| --------- | ---------- | ---------- |
| ID3       | Multi-Way  | Entropy    |
| C4.5      | Multi-Way  | Gain Ratio |
| CART      | Binary     | Gini       |

---

# Output

## Classification

* Class Label
* Probability

Example:

Probability(Default) = 0.85

---

## Regression

Numerical Prediction

Example:

House Price = $450,000

---

# Assumptions

Decision Trees make very few assumptions.

No requirement for:

❌ Linearity

❌ Normality

❌ Homoscedasticity

This makes them highly flexible.

---

# Bias-Variance Profile

| Metric            | Level |
| ----------------- | ----- |
| Bias              | Low   |
| Variance          | High  |
| Overfitting Risk  | High  |
| Underfitting Risk | Low   |

Interpretation:

Flexible but unstable model.

---

# Overfitting

Common Problem

Symptoms:

* High Training Accuracy
* Low Validation Accuracy

Causes:

* Deep Trees
* Small Leaf Nodes
* Excessive Splits

Solutions:

* Pruning
* Max Depth Control
* Random Forest

---

# Underfitting

Symptoms:

* Poor Training Accuracy
* Poor Validation Accuracy

Causes:

* Shallow Trees
* Restrictive Parameters

Solutions:

* Increase Tree Depth
* Reduce Constraints

---

# Pruning

Purpose:

Reduce Overfitting

---

## Pre-Pruning

Stop tree growth early.

Parameters:

* max_depth
* min_samples_split
* min_samples_leaf

---

## Post-Pruning

Grow full tree first.

Then remove weak branches.

Usually better generalization.

---

# Feature Engineering

### Scaling

❌ Not Needed

Reason:

Trees split on thresholds, not distances.

---

### Encoding

✅ Required

Common:

* One-Hot Encoding
* Ordinal Encoding

---

### Feature Selection

⚠ Usually Not Required

Tree automatically selects important variables.

---

### Outlier Handling

❌ Usually Not Required

Trees are generally robust to outliers.

---

# Decision Boundary

Decision Tree:

✅ Non-Linear

Logistic Regression:

❌ Linear

Random Forest:

✅ Non-Linear

XGBoost:

✅ Non-Linear

Neural Networks:

✅ Highly Non-Linear

---

# Evaluation Metrics

## Classification

* Accuracy
* Precision
* Recall
* F1
* ROC-AUC
* PR-AUC

---

## Regression

* RMSE
* MAE
* R²

---

# Common Production Challenges

* Overfitting
* Class Imbalance
* Data Drift
* Feature Drift
* Tree Instability
* Concept Drift

---

# Monitoring

Monitor:

* Accuracy
* Precision
* Recall
* F1
* ROC-AUC
* PR-AUC

Data Metrics:

* Missing Values
* Feature Drift
* PSI

Business Metrics:

* Fraud Detection Rate
* Default Rate
* Churn Rate

---

# When To Use

✅ Explainability Required

✅ Non-Linear Relationships

✅ Rule-Based Decisions

✅ Mixed Data Types

✅ Quick Prototyping

Examples:

* Fraud Detection
* Credit Risk
* Churn Prediction
* Insurance Claims
* Customer Segmentation

---

# When Not To Use

❌ Very Noisy Data

❌ Need Maximum Accuracy

❌ High Variance Not Acceptable

Alternatives:

* Random Forest
* XGBoost
* Gradient Boosting

---

# Advantages

* Easy to Understand
* Easy to Explain
* Learns Non-Linear Patterns
* No Scaling Required
* Handles Feature Interactions
* Minimal Assumptions

---

# Limitations

* High Variance
* Prone to Overfitting
* Unstable
* Sensitive to Data Changes
* Lower Accuracy than Ensemble Methods

---

# Decision Tree vs Logistic Regression

| Aspect               | Decision Tree | Logistic Regression |
| -------------------- | ------------- | ------------------- |
| Boundary             | Non-Linear    | Linear              |
| Scaling              | No            | Recommended         |
| Bias                 | Low           | High                |
| Variance             | High          | Low                 |
| Interpretability     | High          | High                |
| Feature Interactions | Automatic     | Manual              |

---

# Senior Data Scientist Summary

**Use Decision Trees when:**

* Explainability matters
* Relationships are non-linear
* Business rules need transparency

**Main Strength**

Captures non-linear patterns automatically.

**Main Weakness**

High Variance and Overfitting.

**Key Interview Insight**

Decision Trees are the foundation of:

* Random Forest
* Gradient Boosting
* XGBoost
* LightGBM
* CatBoost

Understanding Decision Trees thoroughly makes learning ensemble methods much easier.
