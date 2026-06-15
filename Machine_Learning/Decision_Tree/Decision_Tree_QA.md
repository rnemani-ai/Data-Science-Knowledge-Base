# Decision Tree - Interview Questions & Answers

## What is a Decision Tree?

A Decision Tree is a supervised machine learning algorithm used for both classification and regression problems.

It works by recursively splitting data into smaller subsets based on feature values until a prediction can be made.

The structure resembles a tree with:

* Root Node
* Internal Nodes
* Branches
* Leaf Nodes

Decision Trees are highly interpretable and can capture non-linear relationships.

---

## Why are Decision Trees called non-parametric models?

Decision Trees are called non-parametric because they do not assume a specific functional form or distribution for the data.

Unlike Linear Regression or Logistic Regression, they do not assume:

* Linearity
* Normality
* Homoscedasticity

They learn patterns directly from the data through recursive splitting.

---

## What is the output of a Decision Tree?

### Classification

Output:

* Class Label
* Probability

Example:

Probability(Default) = 0.85

Prediction = Default

---

### Regression

Output:

Numerical Value

Example:

Predicted House Price = $450,000

---

## Why don't Decision Trees require feature scaling?

Decision Trees split data based on thresholds.

Example:

Income > 50,000

Scaling changes the value but not the relative ordering of observations.

Because splits depend on ordering rather than distance calculations, scaling does not affect tree construction.

This is why:

* Standardization is not required
* Normalization is not required

for Decision Trees.

---

## What is Entropy?

Entropy is a measure of impurity or disorder in a dataset.

Interpretation:

Low Entropy:

* Pure node
* Mostly one class

High Entropy:

* Mixed classes

Examples:

All Positive Class:

Entropy = 0

50% Positive, 50% Negative:

Entropy = Maximum

The goal is to reduce entropy after each split.

---

## What is Information Gain?

Information Gain measures how much uncertainty is reduced after a split.

Formula intuition:

Information Gain = Parent Entropy - Child Entropy

The split that produces the highest Information Gain is selected.

Higher Information Gain:

Better split.

---

## What is Gini Impurity?

Gini Impurity measures how often a randomly selected observation would be incorrectly classified.

Interpretation:

Lower Gini:

Better split.

Pure Node:

Gini = 0

Mixed Node:

Higher Gini

Most modern implementations use Gini Impurity.

---

## Difference Between Entropy and Gini Impurity

| Aspect                  | Entropy            | Gini        |
| ----------------------- | ------------------ | ----------- |
| Based On                | Information Theory | Probability |
| Computation             | More Expensive     | Faster      |
| Range                   | 0 to 1             | 0 to 0.5    |
| Default in Scikit-Learn | No                 | Yes         |

In practice:

Both often produce very similar trees.

---

## What is Information Gain used for?

Information Gain helps determine the best feature and threshold for splitting a node.

The feature producing the largest reduction in impurity is selected.

Example:

Possible Splits:

* Income
* Age
* Credit Score

The feature with the highest Information Gain becomes the next split.

---

## What is Recursive Splitting?

Decision Trees repeatedly split the dataset into smaller subsets.

Process:

1. Find best split.
2. Split data.
3. Repeat on child nodes.
4. Continue until stopping criteria are met.

This process is called recursive partitioning.

---

## What is CART?

CART stands for:

Classification And Regression Trees

Characteristics:

* Binary Splits
* Uses Gini Impurity for Classification
* Used by Scikit-Learn
* Foundation for Random Forest

Most production implementations are based on CART.

---

## Difference Between ID3, C4.5, and CART

| Algorithm | Split Type | Criterion  |
| --------- | ---------- | ---------- |
| ID3       | Multi-way  | Entropy    |
| C4.5      | Multi-way  | Gain Ratio |
| CART      | Binary     | Gini       |

Modern ML libraries primarily use CART.

---

## Why do Decision Trees overfit?

Decision Trees have low bias and high variance.

If allowed to grow without restrictions, they may memorize noise and training examples.

Symptoms:

* Very high training accuracy
* Poor test performance

---

## How can overfitting be prevented?

Common approaches:

* Limit max_depth
* Increase min_samples_leaf
* Increase min_samples_split
* Use pruning
* Use Random Forest

---

## What is Pruning?

Pruning is the process of reducing the size of a Decision Tree to improve generalization.

Goal:

Remove branches that provide little predictive value.

Benefits:

* Reduced overfitting
* Better generalization
* Simpler model

---

## What is Pre-Pruning?

Pre-Pruning stops the tree from growing further.

Examples:

* max_depth
* min_samples_leaf
* min_samples_split

Advantages:

* Faster training
* Smaller trees

Disadvantages:

* May stop growth too early

---

## What is Post-Pruning?

Post-Pruning grows the full tree first and then removes unnecessary branches.

Advantages:

* Often produces better generalization
* More robust than pre-pruning

Disadvantages:

* Higher computational cost

---

## How do Decision Trees handle numerical variables?

The algorithm evaluates possible thresholds.

Example:

Income > 50,000

Income > 75,000

Income > 100,000

The threshold producing the best impurity reduction is selected.

---

## How do Decision Trees handle categorical variables?

Categorical variables are typically encoded before training.

Common approaches:

* One-Hot Encoding
* Ordinal Encoding

The tree then evaluates splits using the encoded values.

---

## Can Decision Trees handle non-linear relationships?

Yes.

This is one of their biggest advantages.

Unlike Logistic Regression, Decision Trees naturally learn:

* Non-linear patterns
* Feature interactions
* Complex decision boundaries

without manual feature engineering.

---

## What are leaf nodes?

Leaf nodes are terminal nodes in the tree.

They contain:

Classification:

* Predicted class
* Class probabilities

Regression:

* Predicted numerical value

No further splitting occurs.

---

## What are the stopping criteria in a Decision Tree?

Common stopping criteria:

* max_depth reached
* min_samples_split reached
* min_samples_leaf reached
* Pure node achieved

These prevent uncontrolled tree growth.

---

## Why are Decision Trees interpretable?

Every prediction can be traced through a sequence of rules.

Example:

Income > 50,000

Credit Score > 700

Debt Ratio < 30%

Prediction:

No Default

This rule-based structure makes Decision Trees highly explainable.

---

# Quick Revision

Decision Tree:

* Supervised Learning
* Classification & Regression
* Non-Parametric
* No Scaling Required
* Uses Recursive Splitting
* Uses Gini or Entropy
* High Interpretability
* Low Bias
* High Variance
* Prone to Overfitting
* Foundation for Random Forest and XGBoost
