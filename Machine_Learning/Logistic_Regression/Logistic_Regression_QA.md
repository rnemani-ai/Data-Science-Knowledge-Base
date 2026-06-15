# Regularization

Regularization is a technique used to prevent overfitting by penalizing large coefficient values.

The idea is simple:

Instead of only minimizing prediction error, the model is also penalized for becoming unnecessarily complex.

Benefits:

* Reduces overfitting
* Improves generalization
* Stabilizes coefficients
* Helps with multicollinearity

---

## L1 Regularization (Lasso)

L1 regularization adds the absolute value of coefficients to the cost function.

Behavior:

* Shrinks coefficients toward zero
* Some coefficients become exactly zero
* Performs automatic feature selection

Example:

Suppose we have:

* Income
* Credit Score
* Age
* Marital Status
* Number of Credit Cards

If Marital Status contributes very little information, L1 regularization may completely remove it from the model.

Advantages:

* Feature selection
* Simpler models
* Better interpretability

Disadvantages:

* Can remove useful features if regularization is too strong

---

## L2 Regularization (Ridge)

L2 regularization adds the squared value of coefficients to the cost function.

Behavior:

* Shrinks coefficients
* Rarely makes coefficients exactly zero
* Retains all features

Advantages:

* Reduces overfitting
* Handles multicollinearity well
* More stable than L1

Disadvantages:

* Does not perform feature selection

---

## Elastic Net

Elastic Net combines:

* L1 Regularization
* L2 Regularization

Benefits:

* Feature selection
* Better handling of correlated variables
* Often performs better than pure L1 or pure L2

---

# One-vs-Rest vs Multinomial Logistic Regression

Logistic Regression naturally handles binary classification.

However, many real-world problems involve multiple classes.

Examples:

* Insurance Claim Type
* Product Category
* Disease Category
* Customer Segment

Two common approaches are:

* One-vs-Rest (OvR)
* Multinomial Logistic Regression

---

## One-vs-Rest (OvR)

Suppose we have:

* Class A
* Class B
* Class C

OvR builds three separate binary classifiers.

Model 1:

A vs Not A

Model 2:

B vs Not B

Model 3:

C vs Not C

Final Prediction:

Choose the class with the highest probability.

### Activation Function

Uses:

Sigmoid

because each classifier is solving a binary classification problem.

### Objective Function

Binary Cross Entropy (Log Loss)

### Advantages

* Simple
* Easy to implement
* Computationally efficient
* Works well with many classes

### Disadvantages

* Probabilities may not sum to 1
* Classes are learned independently

---

## Multinomial Logistic Regression

Instead of training multiple binary classifiers, a single model predicts all classes simultaneously.

### Activation Function

Uses:

Softmax

instead of Sigmoid.

Why?

Because probabilities across all classes should sum to 1.

Example:

Class A = 0.60

Class B = 0.30

Class C = 0.10

Total = 1.00

### Objective Function

Categorical Cross Entropy

### Advantages

* Probabilities sum to 1
* More statistically consistent
* Single unified model

### Disadvantages

* Slightly more computationally expensive
* Less intuitive than OvR

---

## Sigmoid vs Softmax vs Tanh

### Sigmoid

Output Range:

0 to 1

Use Case:

Binary Classification

Output:

Probability of one class

---

### Softmax

Output Range:

0 to 1

Sum of probabilities = 1

Use Case:

Multiclass Classification

Output:

Probability distribution across all classes

---

### Tanh

Output Range:

-1 to 1

Use Case:

Historically used in neural networks

Not used as the final activation function in Logistic Regression because outputs are not probabilities.

---

## Why Not Use Tanh?

Classification probabilities must lie between:

0 and 1

Tanh outputs:

-1 to 1

Therefore:

* Sigmoid is used for binary classification
* Softmax is used for multiclass classification
* Tanh is not suitable as the final output layer for Logistic Regression

---

# Bias-Variance Profile

| Metric   | Level |
| -------- | ----- |
| Bias     | High  |
| Variance | Low   |

Interpretation:

Logistic Regression is a relatively simple model.

Advantages:

* Stable
* Less prone to overfitting
* Easier to explain
* Generalizes well

Disadvantages:

* May miss complex relationships
* May underfit complicated datasets

---

# Overfitting

Overfitting occurs when the model learns noise instead of meaningful patterns.

Symptoms:

* Excellent training performance
* Poor test performance

Logistic Regression generally has lower overfitting risk compared to:

* Decision Trees
* Random Forests
* XGBoost
* Neural Networks

Mitigation Techniques:

* Regularization
* Feature Selection
* Cross Validation
* More Training Data

---

# Underfitting

Underfitting occurs when the model is too simple to capture underlying relationships.

Example:

Customer default behavior depends on complex interactions between variables.

A linear decision boundary may not capture these patterns effectively.

Symptoms:

* Poor training performance
* Poor testing performance

Solutions:

* Better Feature Engineering
* Interaction Features
* Polynomial Features
* More Complex Models

---

# When Should You Use Logistic Regression?

Use when:

✅ Binary Classification

✅ Explainability is important

✅ Regulatory compliance is required

✅ Small to medium datasets

✅ Fast deployment is required

✅ Probability outputs are needed

Examples:

* Loan Default Prediction
* Insurance Claim Fraud
* Customer Churn
* Disease Diagnosis
* Marketing Conversion

---

# When Should You Avoid Logistic Regression?

Avoid when:

❌ Highly non-linear relationships

❌ Complex feature interactions

❌ Image Classification

❌ NLP Tasks

❌ Large-scale unstructured data

Alternatives:

* Random Forest
* XGBoost
* Neural Networks
* Transformers

---

# Advantages

* Easy to understand
* Easy to explain
* Fast training
* Fast prediction
* Produces probabilities
* Strong baseline model
* Highly interpretable
* Regulatory friendly
* Easy deployment

---

# Limitations

* Linear decision boundary
* Sensitive to multicollinearity
* Limited feature interactions
* May underperform complex models
* Requires feature engineering
* Can struggle with highly non-linear relationships

---

# Common Production Challenges

## Class Imbalance

Common in:

* Fraud Detection
* Churn Prediction
* Loan Default
* Disease Prediction

Solutions:

* Class Weights
* SMOTE
* Undersampling
* Threshold Tuning

---

## Feature Leakage

Using information unavailable at prediction time.

Impact:

* Artificially high performance
* Production failure

Mitigation:

* Temporal validation
* Feature reviews
* Business validation

---

## Data Drift

Feature distributions change over time.

Examples:

* Customer behavior changes
* Economic conditions change
* Fraud patterns evolve

Impact:

* Performance degradation

---

## Threshold Selection

Default threshold:

0.5

Production threshold should align with business objectives.

Example:

Fraud Detection:

Lower threshold to improve Recall.

Loan Approval:

Higher threshold to improve Precision.

---

## Probability Calibration

Predicted probabilities should match actual outcomes.

Example:

If 100 customers receive a score of 0.8, approximately 80 should actually belong to the positive class.

Calibration is critical for:

* Credit Risk
* Insurance Pricing
* Fraud Prioritization
* Customer Targeting

---

## Monitoring

Monitor:

* Precision
* Recall
* F1 Score
* ROC-AUC
* PR-AUC
* Log Loss
* Calibration
* Population Stability Index (PSI)
* Data Drift
* Feature Drift
