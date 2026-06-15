# Decision Tree

## What is a Decision Tree?

A Decision Tree is a supervised machine learning algorithm used for both classification and regression tasks.

It makes predictions by recursively splitting data into smaller subsets based on feature values.

The structure resembles an inverted tree:

* Root Node
* Internal Nodes
* Branches
* Leaf Nodes

Examples:

* Will a customer churn?
* Will a customer default?
* Will a claim be fraudulent?
* What will be the house price?

---

# Data Preparation Requirements

| Requirement             | Needed?                     | Notes |
| ----------------------- | --------------------------- | ----- |
| Missing Value Handling  | ⚠ Depends on implementation |       |
| Feature Scaling         | ❌ Not Required              |       |
| Categorical Encoding    | ✅ Required                  |       |
| Outlier Treatment       | ❌ Usually Not Required      |       |
| Feature Selection       | ❌ Usually Not Required      |       |
| Multicollinearity Check | ❌ Not Required              |       |
| Explainability          | ✅ High                      |       |
| Probability Output      | ✅ Yes                       |       |

---

# Intuition

Suppose a bank wants to predict whether a customer will default.

Questions might be:

Income > $50,000?

→ Yes

Credit Score > 700?

→ Yes

Prediction:

No Default

The tree keeps asking questions until it reaches a final decision.

---

# Why Do We Need Decision Trees?

Logistic Regression assumes a linear decision boundary.

Many real-world relationships are non-linear.

Decision Trees can learn:

* Non-linear patterns
* Feature interactions
* Complex business rules

without feature transformations.

---

# Internal Working

## Step 1: Start at Root Node

All observations begin at the root.

---

## Step 2: Evaluate Possible Splits

Example:

Income > 50,000

Credit Score > 700

Age > 35

The algorithm evaluates all possible splits.

---

## Step 3: Calculate Impurity Reduction

Using:

* Gini Impurity
* Entropy

The split with the highest information gain is selected.

---

## Step 4: Recursive Splitting

The process repeats until:

* Maximum depth reached
* Minimum samples reached
* Pure node achieved

---

## Step 5: Create Leaf Nodes

Leaf nodes contain final predictions.

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

Income > 50,000

AND

Credit Score > 700

→ Probability(Default) = 0.05

Interpretation:

Only 5% probability of default.

---

# Objective Function

Goal:

Create the purest possible child nodes after each split.

The algorithm attempts to maximize impurity reduction.

---

# Splitting Criteria

## Entropy

Measures impurity.

Pure Node:

Entropy = 0

Mixed Node:

Higher Entropy

---

## Information Gain

Measures reduction in entropy after splitting.

Decision Trees choose the split with maximum information gain.

---

## Gini Impurity

Most common in CART.

Formula intuition:

Measures probability of incorrect classification.

Lower Gini:

Better split.

---

# CART

Classification and Regression Trees (CART)

Characteristics:

* Binary Splits
* Uses Gini Impurity
* Most widely used implementation
* Used by Scikit-Learn

---

# ID3 vs C4.5 vs CART

| Algorithm | Splits    | Criterion  |
| --------- | --------- | ---------- |
| ID3       | Multi-way | Entropy    |
| C4.5      | Multi-way | Gain Ratio |
| CART      | Binary    | Gini       |

Most modern implementations use CART.

---

# Optimization

Decision Trees use greedy optimization.

At each split:

Choose the locally best split.

They do not search for the globally optimal tree.

---

# Assumptions

Decision Trees make very few assumptions.

Advantages:

* No linearity assumption
* No normality assumption
* No homoscedasticity assumption

This makes them highly flexible.

---

# Feature Engineering Considerations

### Scaling

Not required.

### Missing Values

Handle before training.

### Encoding

Required for categorical variables.

### Feature Selection

Generally not necessary.

### Outliers

Usually robust.

---

# Bias-Variance Profile

| Metric   | Level |
| -------- | ----- |
| Bias     | Low   |
| Variance | High  |

Interpretation:

Very flexible model.

Can easily overfit.

---

# Overfitting

One of the biggest weaknesses.

Symptoms:

* Excellent training accuracy
* Poor test accuracy

Causes:

* Deep trees
* Small leaf nodes
* Excessive splitting

---

# Underfitting

Occurs when tree is too shallow.

Causes:

* Small max_depth
* Large min_samples_split

---

# Pruning

Purpose:

Reduce overfitting.

## Pre-Pruning

Stop growth early.

Examples:

* max_depth
* min_samples_leaf
* min_samples_split

---

## Post-Pruning

Grow full tree first.

Then remove unnecessary branches.

Usually produces better generalization.

---

# When Should You Use Decision Trees?

✅ Explainability required

✅ Non-linear relationships

✅ Mixed feature types

✅ Rule-based decision making

---

# When Should You Avoid Decision Trees?

❌ Very noisy datasets

❌ Need maximum predictive performance

❌ High variance unacceptable

Alternatives:

* Random Forest
* XGBoost

---

# Advantages

* Easy to explain
* Handles non-linear relationships
* No scaling required
* Feature interactions automatically learned
* Visual interpretation possible

---

# Limitations

* High variance
* Overfitting risk
* Unstable
* Small data changes can create very different trees

---

# Common Production Challenges

* Overfitting
* Data Drift
* Concept Drift
* Tree Instability
* Class Imbalance

---

# Key Takeaways

* Non-parametric algorithm
* Works for classification and regression
* Learns non-linear relationships
* Uses recursive splitting
* High interpretability
* High variance model
* Foundation for Random Forest and XGBoost
