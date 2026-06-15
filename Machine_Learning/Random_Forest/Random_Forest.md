# Random Forest

## What is Random Forest?

Random Forest is an ensemble machine learning algorithm that combines multiple Decision Trees to improve predictive performance and reduce overfitting.

It can be used for:

* Classification
* Regression

Examples:

* Fraud Detection
* Customer Churn Prediction
* Loan Default Prediction
* Insurance Risk Assessment
* Product Recommendation

Unlike a single Decision Tree, Random Forest combines predictions from many trees to produce a more robust and stable prediction.

---

# Data Preparation Requirements

| Requirement             | Needed?                     | Notes |
| ----------------------- | --------------------------- | ----- |
| Missing Value Handling  | ⚠ Depends on implementation |       |
| Feature Scaling         | ❌ Not Required              |       |
| Categorical Encoding    | ✅ Required                  |       |
| Outlier Treatment       | ❌ Usually Not Required      |       |
| Feature Selection       | ❌ Usually Not Required      |       |
| Multicollinearity Check | ❌ Not Important             |       |
| Explainability          | Moderate                    |       |
| Probability Output      | ✅ Yes                       |       |

---

# Intuition

Imagine asking 100 experts instead of relying on a single expert.

A single expert may make mistakes.

If most experts independently arrive at the same conclusion, confidence in the decision increases.

Random Forest follows the same principle.

Instead of one Decision Tree:

```text
Decision Tree
```

we train:

```text
100 Decision Trees
```

and combine their predictions.

This usually produces:

* Better accuracy
* Better generalization
* Lower variance

---

# Why Do We Need Random Forest?

Decision Trees have a major weakness:

High Variance

A small change in data can produce a very different tree.

Consequences:

* Overfitting
* Unstable predictions
* Poor generalization

Random Forest addresses this problem by:

* Training multiple trees
* Using different subsets of data
* Using different subsets of features
* Aggregating predictions

Result:

More stable predictions and better performance.

---

# Internal Working

Random Forest works in five major steps.

## Step 1: Bootstrap Sampling

Random subsets of training data are created.

Sampling is performed with replacement.

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

This is allowed.

---

## Step 2: Train Multiple Decision Trees

Each bootstrap sample trains a different Decision Tree.

Example:

```text
Tree 1
Tree 2
Tree 3
...
Tree 100
```

Each tree sees different data.

---

## Step 3: Feature Randomness

At every split:

Random Forest considers only a subset of available features.

Example:

Available Features:

* Income
* Credit Score
* Age
* Debt Ratio
* Delinquencies

Instead of evaluating all features, the tree may randomly consider only:

* Income
* Age

This creates diversity among trees.

---

## Step 4: Generate Predictions

Each tree generates its own prediction.

Example:

Tree 1 → Fraud

Tree 2 → Fraud

Tree 3 → Not Fraud

Tree 4 → Fraud

---

## Step 5: Aggregate Predictions

Classification:

Majority Voting

Result:

Fraud

Regression:

Average Prediction

Example:

100

120

110

Final Prediction:

110

---

# Bootstrap Sampling

Bootstrap Sampling is random sampling with replacement.

Purpose:

Create diverse training datasets.

Benefits:

* Reduces variance
* Improves robustness
* Supports ensemble learning

---

# Bagging

Bagging stands for:

Bootstrap Aggregating

Process:

1. Create bootstrap samples.
2. Train models independently.
3. Aggregate predictions.

Goal:

Reduce variance.

Random Forest is a bagging-based algorithm.

---

# Feature Randomness

Random Forest introduces randomness at the feature level.

At each split:

Only a subset of features is considered.

Benefits:

* Reduces correlation among trees
* Increases diversity
* Improves ensemble performance

---

# Voting and Aggregation

## Classification

Majority Vote

Example:

```text
Fraud
Fraud
Fraud
Not Fraud
Fraud
```

Final Prediction:

Fraud

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

Final Prediction:

115

---

# What Is The Output?

Classification:

* Class Label
* Probability

Regression:

* Numerical Value

---

# How To Interpret The Output

Example:

Probability(Default) = 0.92

Interpretation:

92% of trees collectively support the positive class.

Higher probabilities generally indicate stronger model confidence.

---

# Objective Function

There is no single global objective function.

Each individual Decision Tree optimizes:

Classification:

* Gini Impurity
* Entropy

Regression:

* Mean Squared Error

Random Forest combines predictions from all trees.

---

# Optimization

Random Forest uses:

* Bootstrap Sampling
* Feature Randomness
* Aggregation

instead of gradient-based optimization.

Unlike Logistic Regression:

No Gradient Descent is used.

---

# Assumptions

Random Forest makes very few assumptions.

Advantages:

* No linearity assumption
* No normality assumption
* No homoscedasticity assumption

Works well on complex data.

---

# Feature Engineering Considerations

## Scaling

Not required.

Trees split using thresholds rather than distances.

---

## Missing Values

Handle before training unless implementation supports missing values.

---

## Encoding

Required.

Common Approaches:

* One-Hot Encoding
* Ordinal Encoding

---

## Feature Selection

Usually unnecessary.

Random Forest performs implicit feature selection.

---

## Outliers

Generally robust.

Outliers rarely affect splits significantly.

---

# Feature Importance

Random Forest can estimate feature importance.

Common Methods:

## Mean Decrease in Impurity

Measures total impurity reduction contributed by a feature.

---

## Permutation Importance

Measures performance degradation when a feature is shuffled.

Generally more reliable.

---

# Out-of-Bag (OOB) Error

Since bootstrap samples are used:

Approximately one-third of observations are not selected for a given tree.

These observations are called:

Out-of-Bag Samples

They can be used as a validation set.

Benefits:

* No separate validation dataset required
* Faster model evaluation

---

# Bias-Variance Profile

| Metric   | Level           |
| -------- | --------------- |
| Bias     | Low to Moderate |
| Variance | Low             |

Compared to Decision Trees:

Decision Tree:

* Low Bias
* High Variance

Random Forest:

* Slightly Higher Bias
* Much Lower Variance

Result:

Better generalization.

---

# Overfitting

Random Forest is less prone to overfitting than a single Decision Tree.

Reasons:

* Multiple trees
* Averaging
* Random feature selection

However:

Extremely large forests can still overfit.

---

# Underfitting

Can occur when:

* Too few trees
* Excessive restrictions
* Small max_depth

Symptoms:

* Poor train performance
* Poor test performance

---

# When Should You Use Random Forest?

Use when:

✅ Non-linear relationships exist

✅ High predictive accuracy is needed

✅ Mixed feature types exist

✅ Interpretability is somewhat important

✅ Strong baseline model is required

Examples:

* Fraud Detection
* Customer Churn
* Credit Risk
* Insurance Claims
* Product Recommendations

---

# When Should You Avoid Random Forest?

Avoid when:

❌ Real-time latency is critical

❌ Explainability is extremely important

❌ Dataset is extremely large

Alternatives:

* Logistic Regression
* XGBoost
* LightGBM

---

# Advantages

* Strong predictive performance
* Handles non-linear relationships
* Reduces overfitting
* Robust to outliers
* Minimal feature engineering
* Handles large feature spaces

---

# Limitations

* Less interpretable than a single tree
* Larger memory footprint
* Slower inference
* Feature importance can be misleading

---

# Common Production Challenges

* Large model size
* Inference latency
* Data drift
* Feature drift
* Class imbalance
* Feature importance misinterpretation

---

# Key Takeaways

* Ensemble of Decision Trees
* Uses Bagging
* Uses Bootstrap Sampling
* Uses Feature Randomness
* Reduces Variance
* Improves Generalization
* Strong Baseline Model
* Widely Used in Industry
* Foundation for Understanding Ensemble Learning
