# Random Forest Cheat Sheet

## Quick Summary

| Property           | Value                       |
| ------------------ | --------------------------- |
| Algorithm Type     | Supervised Learning         |
| Problem Type       | Classification & Regression |
| Ensemble Method    | Bagging                     |
| Base Learner       | Decision Tree               |
| Decision Boundary  | Non-Linear                  |
| Explainability     | Moderate                    |
| Training Speed     | Medium                      |
| Prediction Speed   | Medium                      |
| Probability Output | Yes                         |

---

# Data Preparation Requirements

| Requirement             | Needed?                     |
| ----------------------- | --------------------------- |
| Missing Value Handling  | ⚠ Depends on implementation |
| Feature Scaling         | ❌ Not Required              |
| Categorical Encoding    | ✅ Required                  |
| Outlier Treatment       | ❌ Usually Not Required      |
| Feature Selection       | ❌ Usually Not Required      |
| Multicollinearity Check | ❌ Not Important             |

---

# Why Was Random Forest Created?

Decision Tree Problem:

```text
Low Bias
High Variance
Overfitting
```

Random Forest Solution:

```text
Multiple Trees
+
Bagging
+
Feature Randomness
=
Lower Variance
```

---

# Core Workflow

```text
Training Data
      ↓
Bootstrap Samples
      ↓
Multiple Decision Trees
      ↓
Random Feature Selection
      ↓
Predictions from Trees
      ↓
Voting / Averaging
      ↓
Final Prediction
```

---

# Key Concepts

## Bootstrap Sampling

Random Sampling With Replacement

Example:

Original:

```text
A B C D E
```

Bootstrap Sample:

```text
A B B D E
```

Purpose:

Create diverse datasets.

---

## Bagging

Bagging =

```text
Bootstrap + Aggregation
```

Steps:

1. Create bootstrap datasets
2. Train independent trees
3. Aggregate predictions

Goal:

Reduce variance.

---

## Feature Randomness

At each split:

Only a subset of features is evaluated.

Purpose:

* Reduce tree correlation
* Increase diversity
* Improve generalization

---

# Prediction Mechanism

## Classification

Majority Voting

Example:

```text
Fraud
Fraud
Not Fraud
Fraud
```

Final:

```text
Fraud
```

---

## Regression

Average Prediction

Example:

```text
100
120
110
130
```

Final:

```text
115
```

---

# Output

## Classification

* Class Label
* Probability

Example:

Probability(Default) = 0.92

---

## Regression

Numerical Value

Example:

Predicted Price = $450,000

---

# Objective

Each Tree Optimizes:

### Classification

* Gini Impurity
* Entropy

### Regression

* Mean Squared Error

Forest Goal:

Combine many trees to reduce variance.

---

# Out-of-Bag (OOB) Error

Approximately:

```text
~33%
```

of observations are not used by a given tree.

These become:

```text
Out-of-Bag Samples
```

Used as:

Validation Data

Benefits:

✅ No separate validation set

✅ Faster evaluation

---

# Feature Importance

## Mean Decrease in Impurity

Measures impurity reduction contributed by a feature.

---

## Permutation Importance

Shuffle feature values.

Measure performance drop.

Larger drop:

More important feature.

Preferred for production interpretation.

---

# Assumptions

Very few assumptions.

No requirement for:

❌ Linearity

❌ Normality

❌ Homoscedasticity

Works well on complex datasets.

---

# Bias-Variance Profile

| Metric            | Level           |
| ----------------- | --------------- |
| Bias              | Low to Moderate |
| Variance          | Low             |
| Overfitting Risk  | Low             |
| Underfitting Risk | Moderate        |

---

# Overfitting

Lower risk than Decision Trees.

Causes:

* Extremely deep trees
* Noisy data
* Excessive complexity

Mitigation:

* max_depth
* min_samples_leaf
* More trees

---

# Underfitting

Causes:

* Too few trees
* Shallow trees
* Restrictive parameters

Symptoms:

* Poor train performance
* Poor validation performance

---

# Important Hyperparameters

## n_estimators

Number of trees.

Typical:

```text
100 – 1000
```

---

## max_depth

Maximum tree depth.

Controls:

* Overfitting
* Complexity

---

## max_features

Features evaluated per split.

Classification Default:

```text
sqrt(total_features)
```

---

## min_samples_split

Minimum observations required to split.

---

## min_samples_leaf

Minimum observations in leaf node.

---

# Evaluation Metrics

## Classification

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC
* PR-AUC

---

## Regression

* RMSE
* MAE
* R²

---

# Common Production Challenges

* Class Imbalance
* Data Drift
* Feature Drift
* Large Model Size
* Inference Latency
* Feature Importance Misinterpretation

---

# Monitoring

Model Metrics:

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
* Conversion Rate

---

# When To Use

✅ Strong Baseline Model

✅ Non-Linear Relationships

✅ Mixed Data Types

✅ Tabular Data

✅ Limited Feature Engineering

Examples:

* Fraud Detection
* Credit Risk
* Churn Prediction
* Insurance Claims
* Product Recommendation

---

# When Not To Use

❌ Real-Time Ultra-Low Latency Systems

❌ Extreme Explainability Requirements

❌ Very Large Datasets

Alternatives:

* Logistic Regression
* XGBoost
* LightGBM

---

# Advantages

* Strong Predictive Performance
* Handles Non-Linear Relationships
* Reduces Overfitting
* Robust to Outliers
* Minimal Preprocessing
* Strong Baseline Model

---

# Limitations

* Less Interpretable
* Larger Memory Usage
* Slower Inference
* Cannot Extrapolate
* Often Outperformed by Boosting Algorithms

---

# Random Forest vs Decision Tree

| Aspect      | Decision Tree | Random Forest   |
| ----------- | ------------- | --------------- |
| Trees       | 1             | Many            |
| Bias        | Low           | Slightly Higher |
| Variance    | High          | Low             |
| Overfitting | High          | Lower           |
| Accuracy    | Lower         | Higher          |
| Stability   | Low           | High            |

---

# Random Forest vs XGBoost

| Aspect   | Random Forest   | XGBoost         |
| -------- | --------------- | --------------- |
| Method   | Bagging         | Boosting        |
| Training | Parallel        | Sequential      |
| Tuning   | Easier          | Harder          |
| Speed    | Faster Training | Slower Training |
| Accuracy | High            | Usually Higher  |

---

# Senior Data Scientist Summary

**Decision Tree**

```text
Low Bias
High Variance
```

↓

**Random Forest**

```text
Low Bias
Low Variance
```

↓

**XGBoost**

```text
Lower Bias
Low Variance
Higher Accuracy
```

### Key Interview Insight

Random Forest was invented to solve the biggest weakness of Decision Trees:

```text
Overfitting
High Variance
```

It achieves this through:

```text
Bagging
+
Bootstrap Sampling
+
Feature Randomness
```
