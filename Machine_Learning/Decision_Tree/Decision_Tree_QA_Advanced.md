# Decision Tree - Advanced Interview Questions & Answers

## Why are Decision Trees considered high variance models?

Decision Trees are highly sensitive to small changes in training data.

A slight change in the dataset can result in:

* Different splits
* Different tree structures
* Different predictions

This instability is referred to as high variance.

Example:

Adding a few new observations may completely change upper-level splits and produce a very different tree.

This is one of the primary reasons Random Forest was developed.

---

## Why do Decision Trees overfit so easily?

Decision Trees continue splitting until stopping criteria are reached.

If unrestricted, the tree can:

* Memorize training examples
* Learn noise
* Create highly specific rules

Example:

Instead of learning:

"Customers with low credit scores tend to default"

the tree may learn:

"Customers aged 42 with income $58,932 and exactly 3 credit cards default"

which does not generalize well.

---

## How would you monitor a Decision Tree in production?

### Model Metrics

Monitor:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC
* PR-AUC

### Data Quality

Monitor:

* Missing values
* Data quality issues
* Unexpected categories

### Drift Monitoring

Monitor:

* Data Drift
* Feature Drift
* Population Stability Index (PSI)

### Business Metrics

Examples:

* Fraud Detection Rate
* Default Rate
* Churn Reduction
* Conversion Rate

---

## How do you select max_depth?

There is no universal value.

Selection depends on:

* Dataset size
* Noise level
* Complexity of patterns

Typical approach:

1. Train multiple trees
2. Use Cross Validation
3. Evaluate train vs validation performance
4. Choose depth that balances bias and variance

General intuition:

Small depth:

* Higher bias
* Lower variance

Large depth:

* Lower bias
* Higher variance

---

## What is Cost Complexity Pruning?

Cost Complexity Pruning is a post-pruning technique used in CART.

Idea:

Balance:

* Tree complexity
* Predictive performance

Instead of selecting the largest possible tree, branches are removed if their contribution to performance is too small.

Benefits:

* Reduced overfitting
* Better generalization
* Smaller trees

---

## Why are Decision Trees unstable?

Decision Trees use greedy splitting.

A small change in data can alter:

* Information Gain
* Gini Reduction

which may change the chosen split.

This effect propagates down the tree.

Result:

Small data changes may produce dramatically different trees.

Random Forest reduces this instability through averaging.

---

## What is Surrogate Splitting?

Surrogate Splitting is a technique used when the primary split variable contains missing values.

Example:

Primary Split:

Income > 50,000

Income is missing.

Alternative variable:

Credit Score

can act as a surrogate split.

Benefits:

* Improved robustness
* Better handling of missing data

Note:

Scikit-Learn does not implement surrogate splits directly.

---

## Decision Tree vs Logistic Regression

| Aspect                  | Decision Tree | Logistic Regression |
| ----------------------- | ------------- | ------------------- |
| Boundary                | Non-Linear    | Linear              |
| Scaling Required        | No            | Recommended         |
| Interpretability        | High          | High                |
| Variance                | High          | Low                 |
| Bias                    | Low           | High                |
| Feature Interactions    | Automatic     | Manual              |
| Probability Calibration | Often Poorer  | Usually Better      |

Use Logistic Regression when:

* Explainability is important
* Relationship is approximately linear
* Probability calibration matters

Use Decision Trees when:

* Non-linear relationships exist
* Complex interactions exist
* Rule-based decisions are preferred

---

## Decision Tree vs Random Forest

Decision Tree:

* Single Tree
* High Variance
* Easier to Explain
* Faster

Random Forest:

* Ensemble of Trees
* Lower Variance
* Better Accuracy
* More Robust

Random Forest improves generalization by averaging multiple trees.

---

## Decision Tree vs XGBoost

Decision Tree:

* Single model
* Easier to explain
* Lower accuracy

XGBoost:

* Ensemble of boosted trees
* Higher predictive performance
* More complex
* More difficult to interpret

XGBoost typically wins when predictive accuracy is the primary goal.

---

## How does class imbalance affect Decision Trees?

When one class dominates:

Example:

* Fraud = 1%
* Non-Fraud = 99%

The tree may focus primarily on the majority class.

Consequences:

* High Accuracy
* Poor Recall

Solutions:

* Class Weights
* Oversampling
* SMOTE
* Undersampling

---

## What happens when a Decision Tree becomes too deep?

Benefits:

* Captures more patterns
* Reduces bias

Problems:

* Memorizes noise
* Overfits training data
* Poor generalization

Deep trees usually have:

* Very high training accuracy
* Lower validation accuracy

---

## What happens when a Decision Tree is too shallow?

Benefits:

* Simpler model
* Better stability

Problems:

* Misses patterns
* Underfits

Symptoms:

* Low training accuracy
* Low validation accuracy

---

## What is Greedy Optimization?

Decision Trees choose the best split at the current node.

They do not evaluate every possible tree structure.

This is called greedy optimization.

Advantages:

* Fast
* Computationally efficient

Disadvantages:

* Does not guarantee globally optimal trees

---

## What is the objective of a Decision Tree?

Objective:

Create child nodes that are as pure as possible.

For Classification:

Minimize impurity.

Common metrics:

* Gini Impurity
* Entropy

For Regression:

Minimize prediction error.

Common metric:

* Mean Squared Error

---

## Why does Random Forest outperform a single Decision Tree?

A single tree has:

* Low Bias
* High Variance

Random Forest:

* Trains many trees
* Uses bootstrap sampling
* Uses feature randomness
* Averages predictions

Result:

* Lower variance
* Better generalization
* More stable predictions

---

## Can Decision Trees extrapolate?

No.

Decision Trees cannot extrapolate beyond observed ranges.

Example:

Training Data:

Income:

30k to 150k

Prediction Request:

Income = 500k

The tree can only predict using regions observed during training.

This is especially important in regression problems.

---

## Why do Decision Trees perform automatic feature selection?

During training, only informative features are selected for splits.

Unimportant variables may never appear in the tree.

This is one reason Decision Trees require less feature engineering than Logistic Regression.

---

## How would you explain Decision Trees to a business executive?

A Decision Tree works like a sequence of business rules.

Example:

If Income > $50,000

AND

Credit Score > 700

THEN

Approve Loan

Each prediction can be explained through a series of simple decisions.

This transparency makes Decision Trees attractive in:

* Banking
* Insurance
* Healthcare
* Risk Management

---

# Senior Data Scientist Summary

Decision Trees are:

* Non-parametric
* Rule-based
* Highly interpretable
* Capable of learning non-linear relationships
* Low Bias
* High Variance
* Prone to overfitting

Their biggest weakness is instability.

Random Forest was specifically designed to address this weakness by reducing variance through ensemble learning.

Understanding Decision Trees thoroughly is essential because they form the foundation of:

* Random Forest
* Gradient Boosting
* XGBoost
* LightGBM
* CatBoost
