# Support Vector Machine (SVM) Cheat Sheet

# Quick Summary

| Property              | Value                       |
| --------------------- | --------------------------- |
| Algorithm Type        | Supervised Learning         |
| Problem Type          | Classification & Regression |
| Decision Boundary     | Hyperplane                  |
| Core Objective        | Maximum Margin Separation   |
| Non-Linearity Support | Yes (Kernels)               |
| Explainability        | Moderate                    |
| Probability Output    | Optional                    |
| Scaling Required      | Yes                         |

---

# Data Preparation Requirements

| Requirement          | Needed?                  |
| -------------------- | ------------------------ |
| Missing Values       | ❌ Handle Before Training |
| Feature Scaling      | ✅ Required               |
| Categorical Encoding | ✅ Required               |
| Outlier Treatment    | ⚠ Recommended            |
| Feature Selection    | Sometimes Helpful        |
| Multicollinearity    | Not Critical             |

---

# Core Idea

Find the:

```text
Optimal Hyperplane
```

that separates classes while maximizing:

```text
Margin
```

---

# Geometry of SVM

```text
Class A

● ● ● ●

-------------------
     Margin
-------------------

○ ○ ○ ○

Class B
```

Goal:

```text
Maximum Margin
```

---

# Key Components

## Hyperplane

Decision boundary separating classes.

Examples:

| Features | Hyperplane |
| -------- | ---------- |
| 1        | Point      |
| 2        | Line       |
| 3        | Plane      |
| >3       | Hyperplane |

---

## Margin

Distance between:

```text
Hyperplane
      &
Nearest Data Points
```

Larger Margin:

✅ Better Generalization

✅ Less Overfitting

---

## Support Vectors

Closest observations to the boundary.

They determine:

* Hyperplane
* Margin

Without support vectors:

Decision boundary changes.

---

# Why Are They Called Support Vectors?

Because they:

```text
Support
or Define
the Hyperplane
```

Most other observations have little influence.

---

# Hard Margin SVM

Requirements:

✅ Perfect Separation

❌ No Misclassification

❌ No Noise

Rarely used in practice.

---

# Soft Margin SVM

Allows:

```text
Some Misclassification
```

Benefits:

* Better Generalization
* Handles Noise
* Realistic for Production

Most common implementation.

---

# Hyperparameter: C

Controls:

```text
Margin
vs
Classification Errors
```

---

## Large C

```text
Smaller Margin
Lower Training Error
Higher Overfitting Risk
```

---

## Small C

```text
Larger Margin
Higher Bias
Better Generalization
```

---

# Kernel Trick

Enables:

```text
Non-Linear Classification
```

without explicitly creating higher-dimensional features.

---

# Why Do We Need Kernels?

Some datasets:

```text
Cannot Be Separated
Using Straight Lines
```

Kernel Trick transforms the problem into a higher-dimensional space.

---

# Common Kernels

## Linear Kernel

Use When:

✅ Approximately Linear Data

✅ High-Dimensional Data

Examples:

* Text Classification
* NLP

---

## Polynomial Kernel

Captures:

* Quadratic Relationships
* Cubic Relationships

Less common than RBF.

---

## RBF Kernel

Most commonly used.

Benefits:

* Flexible
* Handles Non-Linearity
* Strong General Performance

Default choice for many problems.

---

## Sigmoid Kernel

Inspired by neural networks.

Rarely used in practice.

---

# Hyperparameter: Gamma

Controls:

```text
Influence Radius
of Each Observation
```

---

## High Gamma

```text
Complex Boundary
Higher Variance
Higher Overfitting Risk
```

---

## Low Gamma

```text
Smooth Boundary
Higher Bias
Better Generalization
```

---

# C vs Gamma

### C

Controls:

```text
Cost of Errors
```

---

### Gamma

Controls:

```text
Geometry of Boundary
```

Interview Memory Trick:

```text
C
=
Cost

Gamma
=
Geometry
```

---

# Output

## Classification

* Class Label
* Optional Probability

Examples:

```text
Fraud
Not Fraud
```

---

## Regression (SVR)

Continuous Output

Examples:

```text
House Price
Claim Amount
Demand Forecast
```

---

# Objective

SVM Optimizes:

```text
Maximum Margin
+
Minimum Classification Error
```

---

# Feature Engineering

## Scaling

✅ Extremely Important

Common:

* StandardScaler
* MinMaxScaler

---

## Encoding

Required

Common:

* One-Hot Encoding
* Label Encoding

---

## Missing Values

Handle Before Training

---

## Outliers

Can affect Support Vectors significantly.

Recommended:

* Outlier Analysis
* Robust Scaling

---

# Bias-Variance Profile

| Metric         | Level    |
| -------------- | -------- |
| Bias           | Moderate |
| Variance       | Moderate |
| Generalization | Strong   |

---

# Overfitting

Causes:

* Large C
* High Gamma
* Complex Kernels

Mitigation:

* Lower C
* Lower Gamma
* Cross Validation

---

# Underfitting

Causes:

* Small C
* Low Gamma
* Oversimplified Kernel

Symptoms:

* Poor Train Performance
* Poor Test Performance

---

# Multi-Class Classification

SVM is naturally binary.

Common Approaches:

## One-vs-Rest (OvR)

```text
A vs Others
B vs Others
C vs Others
```

---

## One-vs-One (OvO)

```text
A vs B
A vs C
B vs C
```

Most implementations use:

```text
One-vs-One
```

---

# Evaluation Metrics

## Classification

* Accuracy
* Precision
* Recall
* F1
* ROC-AUC

---

## Regression (SVR)

* RMSE
* MAE
* R²

---

# Common Production Challenges

* Scaling Consistency
* Hyperparameter Tuning
* Large Dataset Performance
* Probability Calibration
* Data Drift

---

# When To Use

✅ Medium-Sized Datasets

✅ High-Dimensional Data

✅ Text Classification

✅ Complex Boundaries

Examples:

* Spam Detection
* Sentiment Analysis
* Medical Diagnosis
* Fraud Detection

---

# When Not To Use

❌ Extremely Large Datasets

❌ Millions of Records

❌ Real-Time Training Systems

Alternatives:

* XGBoost
* LightGBM
* Deep Learning

---

# Advantages

* Strong Generalization
* Effective in High Dimensions
* Powerful Non-Linear Modeling
* Flexible Through Kernels

---

# Limitations

* Sensitive to Scaling
* Sensitive to Hyperparameters
* Slow Training
* Difficult Interpretation

---

# SVM vs Logistic Regression

| Aspect        | Logistic Regression    | SVM            |
| ------------- | ---------------------- | -------------- |
| Goal          | Probability Estimation | Maximum Margin |
| Output        | Probability            | Boundary       |
| Scaling       | Recommended            | Critical       |
| Non-Linearity | Feature Engineering    | Kernel Trick   |

---

# SVM vs XGBoost

| Aspect              | SVM          | XGBoost        |
| ------------------- | ------------ | -------------- |
| Dataset Size        | Small-Medium | Medium-Large   |
| Scaling             | Required     | Not Required   |
| Feature Engineering | Important    | Less Important |
| Training Speed      | Slower       | Faster         |

---

# Senior Data Scientist Summary

Think of SVM as:

```text
Maximum Margin Classifier
+
Support Vectors
+
Kernel Trick
```

Remember These Interview Lines:

**Support Vectors define the decision boundary.**

**C controls error penalty.**

**Gamma controls boundary complexity.**

**Kernel Trick enables non-linear classification.**

**Logistic Regression estimates probabilities.**

**SVM maximizes margin.**
