# XGBoost

# What is Ensemble Learning?

Ensemble Learning is a machine learning technique that combines multiple models to produce a better prediction than a single model.

Core Idea:

Instead of relying on one model, combine many models and leverage the wisdom of the crowd.

Example:

Suppose one model predicts customer churn with 75% accuracy.

Combining multiple diverse models may improve performance to 85% or higher.

Benefits:

* Better predictive performance
* Reduced overfitting
* Improved robustness
* Better generalization

---

# Why Do We Need Ensemble Learning?

Single models often have limitations.

Examples:

Decision Tree:

* High Variance
* Overfitting

Linear Models:

* High Bias
* Underfitting

Ensemble Learning attempts to combine multiple weak or moderately strong models to create a stronger overall model.

---

# Types of Ensemble Learning

There are three major categories.

## Bagging

Bagging stands for:

Bootstrap Aggregating

Idea:

Train multiple models independently and aggregate their predictions.

Example:

Random Forest

Goal:

Reduce Variance

---

## Boosting

Idea:

Train models sequentially.

Each new model learns from mistakes made by previous models.

Examples:

* AdaBoost
* Gradient Boosting
* XGBoost
* LightGBM
* CatBoost

Goal:

Reduce Bias and Improve Accuracy

---

## Stacking

Idea:

Combine predictions from multiple different models using a meta-model.

Example:

```text
Model 1 → Prediction
Model 2 → Prediction
Model 3 → Prediction
           ↓
     Meta Model
           ↓
 Final Prediction
```

Goal:

Leverage strengths of different algorithms.

---

# Ensemble Learning Landscape

```text
Ensemble Learning

├── Bagging
│      └── Random Forest
│
├── Boosting
│      ├── AdaBoost
│      ├── Gradient Boosting
│      ├── XGBoost
│      ├── LightGBM
│      └── CatBoost
│
└── Stacking
```

---

# Bagging

Bagging stands for:

Bootstrap Aggregating

Process:

1. Create bootstrap samples.
2. Train models independently.
3. Aggregate predictions.

---

## Bootstrap Sampling

Bootstrap Sampling is random sampling with replacement.

Example:

Original Dataset:

```text
A B C D E
```

Bootstrap Sample:

```text
A B B D E
```

Notice:

* B appears twice
* C is missing

This is expected.

---

## Aggregation

Classification:

Majority Voting

Regression:

Averaging

---

## Why Bagging Works

Decision Trees suffer from:

* High Variance
* Overfitting

Bagging reduces variance by averaging predictions from multiple models.

---

## Random Forest Recap

Random Forest is:

```text
Bagging
+
Feature Randomness
```

Benefits:

* Lower Variance
* Better Generalization
* Strong Baseline Performance

Limitation:

Although variance is reduced, some bias still remains.

This motivated the development of Boosting.

---

# Boosting

Unlike Bagging:

Models are not trained independently.

Models are trained sequentially.

Each new model focuses on correcting mistakes made by previous models.

Goal:

Reduce Bias and Improve Accuracy.

---

# Why Was Boosting Introduced?

Random Forest successfully reduces variance.

However:

```text
Decision Tree
      ↓
Random Forest
      ↓
Lower Variance
```

Problem:

Some prediction errors still remain.

Question:

Can we build a model that actively learns from mistakes?

This idea led to Boosting.

---

# Intuition Behind Boosting

Suppose we are predicting customer churn.

Model 1 predicts:

```text
Customer A → Wrong
Customer B → Correct
Customer C → Wrong
```

Instead of building another independent model:

The next model focuses primarily on:

```text
Customer A
Customer C
```

the observations that were previously predicted incorrectly.

Over time, the ensemble becomes increasingly accurate.

---

# Gradient Boosting

Gradient Boosting is the foundation of XGBoost.

Core Idea:

Build trees sequentially.

Each new tree learns the errors made by previous trees.

---

## Residual Learning

Suppose actual value:

```text
100
```

Prediction:

```text
80
```

Residual:

```text
20
```

The next tree attempts to learn this residual.

This process continues repeatedly.

Eventually:

Predictions become increasingly accurate.

---

# Limitations of Traditional Gradient Boosting

Although Gradient Boosting performs well, it has several challenges:

* Can overfit
* Slow training
* No built-in regularization
* Limited scalability
* Weak handling of missing values

These limitations motivated the development of XGBoost.

---

# What is XGBoost?

XGBoost stands for:

Extreme Gradient Boosting

It is an optimized implementation of Gradient Boosting designed for:

* Speed
* Accuracy
* Scalability
* Regularization
* Production Use

For many years, XGBoost dominated structured/tabular machine learning competitions and remains one of the most widely used algorithms in industry.
