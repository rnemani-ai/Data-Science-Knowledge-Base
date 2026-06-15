# K-Nearest Neighbors (KNN) Cheat Sheet

## Algorithm Snapshot

| Attribute          | Value                       |
| ------------------ | --------------------------- |
| Type               | Supervised Learning         |
| Problems           | Classification & Regression |
| Parametric         | No                          |
| Learning Style     | Lazy Learning               |
| Scaling Required   | Yes (Critical)              |
| Encoding Required  | Yes                         |
| Missing Values     | Handle Before Training      |
| Outlier Sensitive  | Yes                         |
| Explainability     | High                        |
| Training Speed     | Very Fast                   |
| Prediction Speed   | Slow                        |
| Best Dataset Size  | Small-Medium                |
| Probability Output | Yes                         |

---

# Core Idea

> Similar observations tend to have similar outcomes.

Prediction is based on:

```text
K Nearest Neighbors
```

rather than a learned mathematical model.

---

# Why Is KNN Different?

Most ML algorithms:

```text
Train Model
↓
Learn Parameters
↓
Predict
```

KNN:

```text
Store Data
↓
Find Neighbors
↓
Predict
```

KNN is therefore called:

```text
Lazy Learning
```

---

# KNN Workflow

```text
Choose K
    ↓
Calculate Distance
    ↓
Find Nearest Neighbors
    ↓
Classification → Majority Vote
Regression → Average Value
```

---

# Classification Example

K = 5

Neighbors:

```text
Fraud
Fraud
Fraud
Not Fraud
Not Fraud
```

Prediction:

```text
Fraud
```

---

# Regression Example

K = 5

Neighbor Values:

```text
100
110
120
130
140
```

Prediction:

```text
Average = 120
```

---

# Distance Metrics

## Euclidean Distance

Most Common

```text
Straight Line Distance
```

Use for:

* Continuous Features

---

## Manhattan Distance

```text
City Block Distance
```

Use for:

* Grid-like Movement
* Sparse Data

---

## Minkowski Distance

Generalization of:

* Euclidean
* Manhattan

---

## Cosine Similarity

Measures:

```text
Angle Between Vectors
```

Used for:

* NLP
* Search
* Recommendation Systems

---

# Choosing K

## Small K

Example:

```text
K = 1
```

Characteristics:

* Low Bias
* High Variance
* Overfitting Risk

---

## Large K

Example:

```text
K = 100
```

Characteristics:

* High Bias
* Low Variance
* Underfitting Risk

---

# Bias-Variance Tradeoff

```text
Small K
↓
Low Bias
High Variance

Large K
↓
High Bias
Low Variance
```

---

# Weighted KNN

Standard KNN:

```text
All Neighbors Equal
```

Weighted KNN:

```text
Closer Neighbors
Have Higher Influence
```

Often performs better.

---

# Data Preparation Requirements

| Requirement       | Needed?       |
| ----------------- | ------------- |
| Missing Values    | ❌             |
| Scaling           | ✅ Critical    |
| Encoding          | ✅             |
| Outlier Treatment | ⚠ Recommended |
| Feature Selection | Helpful       |

---

# Why Scaling Is Critical

Example:

| Feature | Range            |
| ------- | ---------------- |
| Income  | 10,000 - 100,000 |
| Age     | 20 - 60          |

Without scaling:

```text
Income Dominates Distance
```

Recommended:

* StandardScaler
* MinMaxScaler

---

# Output

## Classification

Output:

* Class Label
* Probability

Example:

```text
Fraud Probability = 80%
Prediction = Fraud
```

---

## Regression

Output:

```text
Predicted Value
```

Example:

```text
Claim Amount = $10,000
```

---

# Objective Function

KNN has:

```text
No Explicit Objective Function
```

No optimization occurs.

No coefficients are learned.

---

# Assumption

```text
Similar Observations
↓
Similar Outcomes
```

---

# Curse of Dimensionality

Most Important KNN Concept

As dimensions increase:

```text
Distances Become Less Meaningful
```

Result:

* Poor Neighbor Selection
* Reduced Accuracy
* Poor Generalization

---

# Hyperparameters

## K

Most Important Parameter

Controls:

```text
Bias vs Variance
```

---

## Distance Metric

Options:

* Euclidean
* Manhattan
* Minkowski
* Cosine

---

## Weight Function

Options:

* Uniform
* Distance Weighted

---

# Overfitting

Usually occurs when:

```text
K = 1
```

Characteristics:

* Memorizes Noise
* High Variance

Solution:

* Increase K
* Cross Validation

---

# Underfitting

Usually occurs when:

```text
K is Very Large
```

Characteristics:

* Oversmoothed Predictions
* Misses Local Patterns

Solution:

* Reduce K

---

# Advantages

* Easy to Understand
* Easy to Implement
* No Training Phase
* Naturally Non-Linear
* Strong Baseline Algorithm

---

# Limitations

* Slow Predictions
* Memory Intensive
* Sensitive to Scaling
* Sensitive to Outliers
* Suffers from Curse of Dimensionality

---

# KNN vs Logistic Regression

| Aspect           | KNN      | Logistic Regression |
| ---------------- | -------- | ------------------- |
| Learning Style   | Lazy     | Eager               |
| Model Training   | Minimal  | Required            |
| Scaling          | Critical | Recommended         |
| Interpretability | Moderate | High                |

---

# KNN vs SVM

| Aspect                | KNN    | SVM    |
| --------------------- | ------ | ------ |
| Training Speed        | Faster | Slower |
| Prediction Speed      | Slower | Faster |
| High-Dimensional Data | Weak   | Strong |

---

# KNN vs KMeans

| Aspect          | KNN        | KMeans       |
| --------------- | ---------- | ------------ |
| Type            | Supervised | Unsupervised |
| Labels Required | Yes        | No           |
| Goal            | Prediction | Clustering   |

---

# When To Use

✅ Small-Medium Datasets

✅ Recommendation Systems

✅ Similarity-Based Problems

✅ Pattern Recognition

Examples:

* Product Recommendations
* Customer Similarity
* Medical Diagnosis

---

# When Not To Use

❌ Large Datasets

❌ High-Dimensional Data

❌ Real-Time Prediction Systems

Alternatives:

* XGBoost
* Random Forest
* Neural Networks

---

# Production Challenges

* Prediction Latency
* Memory Usage
* Feature Drift
* Scaling Consistency

---

# Senior Data Scientist Summary

Think of KNN as:

```text
Similarity-Based Learning
+
Distance Metrics
+
Lazy Learning
```

Remember:

```text
Small K
→ Low Bias
→ High Variance

Large K
→ High Bias
→ Low Variance
```

Most Important Interview Insights:

1. KNN is a Lazy Learning algorithm.
2. KNN does not learn parameters.
3. Scaling is critical.
4. K controls the bias-variance tradeoff.
5. Curse of Dimensionality is KNN's biggest limitation.
6. Prediction is expensive; training is cheap.
