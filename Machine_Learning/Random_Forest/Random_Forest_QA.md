# Random Forest - Interview Questions & Answers

## What is Random Forest?

Random Forest is an ensemble learning algorithm that combines multiple Decision Trees to improve predictive performance and reduce overfitting.

It works by:

* Creating multiple Decision Trees
* Training them on different subsets of data
* Combining their predictions

It can be used for:

* Classification
* Regression

---

## Why was Random Forest invented?

Random Forest was developed to address the biggest weakness of Decision Trees:

High Variance

A single Decision Tree can easily overfit and is sensitive to small changes in data.

Random Forest reduces this variance by averaging predictions from many trees.

Result:

* Better generalization
* More stable predictions
* Improved performance

---

## What is Ensemble Learning?

Ensemble Learning combines predictions from multiple models to produce a better prediction.

Core idea:

A group of models is often more accurate than a single model.

Random Forest is an example of an ensemble model.

---

## What is Bagging?

Bagging stands for:

Bootstrap Aggregating

Process:

1. Create bootstrap samples.
2. Train multiple models independently.
3. Aggregate predictions.

Goal:

Reduce variance.

Random Forest is based on bagging.

---

## What is Bootstrap Sampling?

Bootstrap Sampling is random sampling with replacement.

Example:

Original Data:

```text
A B C D E
```

Bootstrap Sample:

```text
A B B D E
```

Observations:

* B appears twice
* C is missing

This creates diversity among training datasets.

---

## Why do we sample with replacement?

Sampling with replacement ensures that each bootstrap dataset is different.

Benefits:

* Diversity among trees
* Reduced correlation
* Better ensemble performance

Without replacement, all trees would become too similar.

---

## What is Feature Randomness?

Random Forest introduces randomness in feature selection.

At each split:

Only a subset of features is considered.

Example:

Available Features:

* Income
* Age
* Credit Score
* Debt Ratio
* Delinquencies

Tree may evaluate only:

* Income
* Debt Ratio

Benefits:

* Less correlation between trees
* Improved generalization

---

## Why is Feature Randomness important?

If all trees always evaluated all features:

Many trees would become very similar.

Highly correlated trees provide limited ensemble benefit.

Feature randomness increases diversity and reduces variance.

---

## How does Random Forest make predictions?

### Classification

Uses Majority Voting.

Example:

Tree 1 → Fraud

Tree 2 → Fraud

Tree 3 → Not Fraud

Tree 4 → Fraud

Final Prediction:

Fraud

---

### Regression

Uses Averaging.

Example:

Tree 1 → 100

Tree 2 → 120

Tree 3 → 110

Final Prediction:

110

---

## What is the output of Random Forest?

Classification:

* Class Label
* Probability

Regression:

* Numerical Value

---

## Why doesn't Random Forest require scaling?

Random Forest is based on Decision Trees.

Decision Trees split using thresholds.

Example:

Income > 50,000

Scaling changes magnitude but not ordering.

Therefore scaling does not affect tree structure.

---

## Does Random Forest require feature selection?

Usually no.

Random Forest automatically identifies important features during training.

However:

Feature selection may still help:

* Faster training
* Reduced memory usage
* Simpler models

---

## How does Random Forest reduce overfitting?

Three mechanisms help:

### Multiple Trees

Reduces reliance on a single model.

---

### Bootstrap Sampling

Creates different training datasets.

---

### Feature Randomness

Creates different tree structures.

Together they reduce variance and improve generalization.

---

## Why is Random Forest better than a single Decision Tree?

Decision Tree:

* Low Bias
* High Variance

Random Forest:

* Slightly Higher Bias
* Much Lower Variance

This tradeoff usually produces better test performance.

---

## What is Out-of-Bag (OOB) Error?

During bootstrap sampling:

Approximately one-third of observations are not selected for a given tree.

These observations are called:

Out-of-Bag Samples

They can be used as validation data.

Benefits:

* No separate validation dataset required
* Efficient model evaluation

---

## How is OOB Error calculated?

For each observation:

1. Collect predictions from trees that did not train on it.
2. Aggregate those predictions.
3. Compare with actual value.

The resulting error estimate is called OOB Error.

---

## What is Feature Importance?

Feature Importance measures how much a feature contributes to predictions.

Random Forest commonly uses:

### Mean Decrease in Impurity

Measures reduction in:

* Gini Impurity
* Entropy

caused by a feature.

---

### Permutation Importance

Measures performance degradation after shuffling a feature.

Generally considered more reliable.

---

## How many trees should be used?

There is no universal answer.

Common range:

100–1000 trees

Increasing trees:

* Reduces variance
* Improves stability

Eventually performance plateaus.

---

## Can Random Forest overfit?

Yes, but less frequently than Decision Trees.

Possible causes:

* Extremely deep trees
* Noisy data
* Excessive complexity

Generally Random Forest is highly resistant to overfitting.

---

## Can Random Forest handle non-linear relationships?

Yes.

This is one of its biggest strengths.

Random Forest automatically learns:

* Non-linear patterns
* Feature interactions
* Complex relationships

without explicit feature engineering.

---

## Is Random Forest parametric or non-parametric?

Random Forest is a non-parametric algorithm.

It does not assume:

* Linearity
* Normality
* Fixed functional forms

It learns directly from the data.

---

## What happens if the number of trees increases?

Benefits:

* Reduced variance
* More stable predictions

Drawbacks:

* Increased training time
* Increased memory consumption
* Increased inference latency

Performance eventually reaches diminishing returns.

---

## What are important Random Forest hyperparameters?

### n_estimators

Number of trees.

---

### max_depth

Maximum tree depth.

---

### min_samples_split

Minimum samples required for splitting.

---

### min_samples_leaf

Minimum observations in leaf node.

---

### max_features

Number of features considered at each split.

---

## How does Random Forest handle class imbalance?

Problems:

* Majority class dominates predictions.

Solutions:

* Class Weights
* Oversampling
* SMOTE
* Undersampling

Evaluation Metrics:

Prefer:

* Precision
* Recall
* F1
* PR-AUC

over Accuracy.

---

## What are the stopping criteria?

Common criteria:

* Maximum depth reached
* Minimum samples reached
* Pure node achieved

Each tree follows standard Decision Tree stopping rules.

---

## Why is Random Forest considered a strong baseline model?

Because it:

* Requires minimal feature engineering
* Handles non-linear patterns
* Handles feature interactions
* Works well on tabular data
* Produces strong performance with limited tuning

For many structured datasets, Random Forest is one of the best baseline models.

---

# Quick Revision

Random Forest:

* Ensemble of Decision Trees
* Uses Bagging
* Uses Bootstrap Sampling
* Uses Feature Randomness
* Reduces Variance
* Less Overfitting
* Handles Non-Linear Relationships
* No Scaling Required
* Strong Baseline Model
* Supports Classification and Regression
