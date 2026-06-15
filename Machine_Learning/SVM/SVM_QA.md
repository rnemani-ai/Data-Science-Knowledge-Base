# Support Vector Machine (SVM) - Interview Questions & Answers

## What is SVM?

Support Vector Machine (SVM) is a supervised machine learning algorithm primarily used for classification tasks.

Its objective is to find the optimal hyperplane that separates classes while maximizing the margin between them.

It can also be used for regression (SVR).

---

## Why is SVM called a Maximum Margin Classifier?

SVM does not simply find a boundary between classes.

Instead, it finds the boundary that maximizes the distance between the closest observations of both classes.

This distance is called the margin.

Larger margins generally lead to better generalization.

---

## What is a Hyperplane?

A hyperplane is the decision boundary that separates classes.

Examples:

1 Feature:

Point

2 Features:

Line

3 Features:

Plane

More than 3 Features:

Hyperplane

SVM's objective is to find the optimal hyperplane.

---

## What is Margin?

Margin is the distance between the hyperplane and the nearest observations from each class.

Goal:

```text
Maximize Margin
```

Benefits:

* Better generalization
* Lower overfitting risk
* Improved robustness

---

## What are Support Vectors?

Support Vectors are the data points closest to the decision boundary.

These observations determine:

* Hyperplane position
* Margin width

Without support vectors, the optimal boundary changes.

---

## Why are they called Support Vectors?

Because they support or define the optimal hyperplane.

The majority of observations do not directly determine the boundary.

Only support vectors have the greatest influence.

---

## What happens if a Support Vector is removed?

The decision boundary may change significantly.

This is because support vectors directly define the optimal margin.

---

## What happens if a non-Support Vector is removed?

Usually very little changes.

These points are typically far from the decision boundary.

---

## What is Hard Margin SVM?

Hard Margin SVM assumes:

Perfect class separation.

Requirements:

* No overlap
* No noise
* No misclassification

Goal:

Maximize margin while maintaining zero training errors.

---

## Why is Hard Margin SVM rarely used?

Real-world datasets often contain:

* Noise
* Outliers
* Overlapping classes

Hard Margin SVM becomes too restrictive.

Soft Margin SVM is generally preferred.

---

## What is Soft Margin SVM?

Soft Margin SVM allows some misclassification.

Benefits:

* Handles noisy data
* Better generalization
* More realistic assumptions

Most practical SVM implementations use Soft Margin SVM.

---

## What is the C Parameter?

One of the most important SVM hyperparameters.

C controls:

Tradeoff between:

* Margin size
* Classification errors

---

## What happens when C is very large?

Large C:

* Strong penalty for errors
* Smaller margin
* Lower training error
* Higher overfitting risk

Model becomes more aggressive.

---

## What happens when C is very small?

Small C:

* Larger margin
* More tolerance for mistakes
* Better generalization
* Higher bias

Model becomes more conservative.

---

## What is the Kernel Trick?

Kernel Trick allows SVM to solve non-linear problems without explicitly transforming data.

Instead of manually creating higher-dimensional features:

SVM computes similarities in higher-dimensional space.

Benefits:

* Handles complex relationships
* Efficient computation
* Powerful decision boundaries

---

## Why do we need Kernels?

Many datasets are not linearly separable.

Example:

Fraud vs Non-Fraud customers.

A straight line cannot separate classes effectively.

Kernels enable non-linear decision boundaries.

---

## What is a Linear Kernel?

Linear Kernel:

No transformation.

Best when:

Data is approximately linearly separable.

Advantages:

* Fast
* Simple
* Interpretable

---

## What is a Polynomial Kernel?

Creates polynomial decision boundaries.

Captures:

* Quadratic relationships
* Cubic relationships
* Higher-order interactions

More flexible than Linear Kernel.

---

## What is an RBF Kernel?

RBF:

Radial Basis Function Kernel

Most commonly used kernel.

Advantages:

* Handles highly non-linear relationships
* Flexible decision boundaries
* Strong performance in practice

---

## Why is RBF so popular?

Because it performs well without requiring extensive feature engineering.

It can model highly complex boundaries automatically.

---

## What is a Sigmoid Kernel?

Inspired by neural networks.

Produces sigmoid-shaped decision boundaries.

Less commonly used in practice.

---

## What is Gamma?

Gamma controls how far the influence of a training observation extends.

Think of Gamma as:

```text
How much attention should we pay to nearby points?
```

---

## What happens when Gamma is high?

High Gamma:

* Complex boundaries
* Tight decision regions
* Higher overfitting risk

Model becomes highly sensitive.

---

## What happens when Gamma is low?

Low Gamma:

* Smooth boundaries
* Simpler model
* Better generalization

Model becomes less sensitive.

---

## Difference Between C and Gamma?

### C

Controls:

```text
Margin vs Classification Errors
```

---

### Gamma

Controls:

```text
Boundary Complexity
```

Simple memory trick:

```text
C
=
Cost of Errors

Gamma
=
Geometry of Boundary
```

---

## Why is Feature Scaling Important for SVM?

SVM relies heavily on distance calculations.

Example:

Income:

```text
10,000 - 100,000
```

Age:

```text
20 - 60
```

Income dominates the distance calculation.

Scaling ensures all features contribute fairly.

---

## Does SVM require Scaling?

Yes.

Strongly recommended.

Common methods:

* StandardScaler
* MinMaxScaler

---

## Can SVM handle non-linear relationships?

Yes.

Through kernels.

Most commonly:

RBF Kernel.

---

## Is SVM Parametric or Non-Parametric?

Generally considered non-parametric.

The complexity depends on support vectors rather than a fixed number of parameters.

---

## Can SVM perform regression?

Yes.

Support Vector Regression (SVR).

Instead of classification:

Predicts continuous values.

Examples:

* House Prices
* Claim Amounts
* Demand Forecasting

---

## What is Support Vector Regression (SVR)?

SVR extends SVM to regression problems.

Goal:

Find a function that predicts values while allowing small prediction errors within a tolerance band.

---

## How does SVM handle outliers?

Outliers can strongly influence support vectors.

As a result:

SVM may become sensitive to outliers.

Mitigation:

* Outlier treatment
* Soft Margin
* Smaller C

---

## What are the strengths of SVM?

* Strong theoretical foundation
* Effective in high-dimensional spaces
* Works well on small and medium datasets
* Powerful non-linear modeling
* Good generalization

---

## What are the weaknesses of SVM?

* Sensitive to scaling
* Sensitive to hyperparameters
* Slow on large datasets
* Difficult interpretation
* Probability estimates may require calibration

---

## SVM vs Logistic Regression

| Aspect           | Logistic Regression          | SVM            |
| ---------------- | ---------------------------- | -------------- |
| Goal             | Probability Estimation       | Maximum Margin |
| Output           | Probability                  | Class Boundary |
| Scaling          | Recommended                  | Critical       |
| Non-Linearity    | Requires Feature Engineering | Kernel Trick   |
| Interpretability | Higher                       | Lower          |

---

## SVM vs Decision Tree

| Aspect           | SVM          | Decision Tree |
| ---------------- | ------------ | ------------- |
| Scaling          | Required     | Not Required  |
| Boundary         | Smooth       | Rule-Based    |
| Interpretability | Lower        | Higher        |
| Non-Linearity    | Kernel-Based | Natural       |

---

## SVM vs XGBoost

| Aspect              | SVM          | XGBoost        |
| ------------------- | ------------ | -------------- |
| Dataset Size        | Small-Medium | Medium-Large   |
| Feature Engineering | Important    | Less Important |
| Training Speed      | Slower       | Faster         |
| Explainability      | Moderate     | Moderate       |

---

## When would you use SVM?

Use when:

* High-dimensional data
* Medium-sized datasets
* Text classification
* Clear class separation

Examples:

* Spam Detection
* Sentiment Analysis
* Medical Diagnosis

---

# Quick Revision

SVM:

* Finds optimal hyperplane
* Maximizes margin
* Uses support vectors
* Supports non-linear classification
* Uses kernel trick
* Soft Margin preferred
* C controls error penalty
* Gamma controls boundary complexity
* Scaling is critical

---

# Senior Data Scientist Summary

Most Important Interview Insight:

**Logistic Regression tries to estimate probabilities.**

**SVM tries to maximize the margin between classes.**

Second Most Important Insight:

**Only Support Vectors define the boundary.**

This is why the algorithm is called Support Vector Machine.
