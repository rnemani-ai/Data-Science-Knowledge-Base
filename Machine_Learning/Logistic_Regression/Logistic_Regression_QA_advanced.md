# Interview Questions and Answers

## What is Logistic Regression?

Logistic Regression is a supervised machine learning algorithm used for classification problems. It predicts the probability that an observation belongs to a particular class by modeling the relationship between input features and the log-odds of the target variable.

Unlike Linear Regression, which predicts continuous values, Logistic Regression predicts probabilities between 0 and 1.

---

## Why is it called Logistic Regression?

It is called Logistic Regression because it performs regression on the log-odds of the target variable.

The resulting value is then transformed into a probability using the logistic (sigmoid) function.

---

## Why can't Linear Regression be used for classification?

Linear Regression can generate outputs less than 0 and greater than 1.

Examples:

* -0.4
* 1.7

These are invalid probabilities.

Logistic Regression constrains predictions between 0 and 1 using the sigmoid function, making it suitable for classification.

---

## Why does Logistic Regression use Sigmoid?

The sigmoid function converts any real-valued number into a probability between 0 and 1.

Benefits:

* Valid probability output
* Smooth and differentiable
* Supports Gradient Descent optimization

---

## What is the output of Logistic Regression?

Primary Output:

Probability

Example:

Probability(Default) = 0.82

Interpretation:

The model estimates an 82% probability that the customer will default.

Secondary Output:

Class Label

After applying a threshold:

* Probability > 0.5 → Class 1
* Probability ≤ 0.5 → Class 0

---

## What are Odds?

Odds represent:

Probability of Success / Probability of Failure

Example:

Probability = 0.8

Odds = 0.8 / 0.2 = 4

Interpretation:

Success is four times more likely than failure.

---

## What are Log Odds?

Log Odds are the logarithm of odds.

Formula:

log(odds)

Why do we use them?

Probabilities are constrained between 0 and 1.

Log odds range from:

-∞ to +∞

which makes them suitable for linear modeling.

---

## What is the Sigmoid Function?

The sigmoid function transforms log-odds into probabilities.

Properties:

* Output between 0 and 1
* Smooth
* Differentiable
* Monotonic

Examples:

Input = -10 → Output ≈ 0

Input = 0 → Output = 0.5

Input = 10 → Output ≈ 1

---

## What is Maximum Likelihood Estimation (MLE)?

MLE is a statistical method used to estimate model parameters.

Objective:

Find coefficients that maximize the probability of observing the training data.

Logistic Regression uses MLE instead of directly minimizing classification errors.

---

## Why do we use Log Loss?

Log Loss measures how well predicted probabilities align with actual outcomes.

It heavily penalizes confident incorrect predictions.

Example:

Actual = 1

Prediction = 0.99

Small penalty

Actual = 1

Prediction = 0.01

Large penalty

This encourages accurate probability estimates.

---

## Why not use Mean Squared Error (MSE)?

MSE is designed for regression problems.

For Logistic Regression:

* Optimization becomes less effective
* Gradients become less informative
* Probability estimation suffers

Log Loss aligns naturally with Maximum Likelihood Estimation.

---

## What is Gradient Descent?

Gradient Descent is an optimization algorithm used to minimize the loss function.

Process:

1. Initialize coefficients
2. Calculate predictions
3. Compute loss
4. Calculate gradients
5. Update coefficients
6. Repeat until convergence

---

## What assumptions does Logistic Regression make?

* Independent observations
* Linear relationship between features and log-odds
* No severe multicollinearity
* Adequate sample size
* Limited influence from extreme outliers

Unlike Linear Regression, it does not require:

* Normally distributed features
* Homoscedasticity
* Normally distributed residuals

---

## How do you handle class imbalance?

Common approaches:

* Class Weights
* SMOTE
* Random Undersampling
* Threshold Tuning
* Precision-Recall Optimization

Choice depends on business objectives.

Example:

Fraud Detection → prioritize Recall

Loan Approval → balance Precision and Recall

---

## How do you detect multicollinearity?

Methods:

* Correlation Matrix
* Variance Inflation Factor (VIF)

Typical guideline:

VIF > 10

indicates significant multicollinearity.

---

## Why is Logistic Regression still used despite XGBoost and Neural Networks?

Because many business problems require:

* Explainability
* Auditability
* Transparency
* Regulatory Compliance

Benefits:

* Easy to explain
* Fast training
* Fast deployment
* Stable performance

Many organizations prefer interpretability over small gains in predictive accuracy.

---

# Advanced Interview Questions

## How do you interpret coefficients?

A coefficient represents the change in log-odds associated with a one-unit increase in a feature while keeping all other variables constant.

Interpretation:

Positive coefficient:

* Increases likelihood of positive class

Negative coefficient:

* Decreases likelihood of positive class

Larger magnitude:

* Stronger influence on prediction

---

## What is an Odds Ratio?

Odds Ratio = exp(coefficient)

Example:

Coefficient = 0.69

Odds Ratio = exp(0.69) ≈ 2

Interpretation:

A one-unit increase in the feature doubles the odds of the event occurring.

This is often easier for business stakeholders to understand than log-odds.

---

## What happens if assumptions are violated?

Potential consequences:

* Unstable coefficients
* Reduced interpretability
* Poor calibration
* Lower predictive performance
* Increased variance

Impact depends on the severity of the violation.

---

## Difference Between Logistic Regression and Linear Regression

| Aspect        | Linear Regression     | Logistic Regression |
| ------------- | --------------------- | ------------------- |
| Problem Type  | Regression            | Classification      |
| Output        | Continuous Value      | Probability         |
| Output Range  | -∞ to +∞              | 0 to 1              |
| Cost Function | MSE                   | Log Loss            |
| Goal          | Predict Numeric Value | Predict Probability |
| Activation    | None                  | Sigmoid             |

---

## Difference Between Logistic Regression and Naive Bayes

Logistic Regression:

* Discriminative model
* Learns decision boundary directly
* Typically higher predictive performance

Naive Bayes:

* Generative model
* Models class distributions
* Assumes feature independence
* Works well with smaller datasets

---

## Difference Between Logistic Regression and SVM

Logistic Regression:

* Produces probabilities
* Easier to interpret
* Business friendly

SVM:

* Maximizes margin
* Usually more difficult to interpret
* Does not naturally produce probabilities

---

## How do you choose the classification threshold?

Default threshold:

0.5

However, threshold selection should be driven by business goals.

Examples:

Fraud Detection:

* Lower threshold
* Higher Recall

Loan Approval:

* Higher threshold
* Better Precision

Insurance Fraud:

* Balance Recall and investigation cost

---

## Why is accuracy a bad metric for imbalanced datasets?

Example:

Fraud Rate = 1%

Predict:

All transactions = Non-Fraud

Accuracy:

99%

Fraud Detection Rate:

0%

The model completely fails despite high accuracy.

Better metrics:

* Precision
* Recall
* F1 Score
* PR-AUC

---

## What is probability calibration?

Calibration measures whether predicted probabilities reflect actual outcomes.

Example:

If 100 customers receive:

Probability = 0.8

Then approximately 80 should actually belong to the positive class.

Calibration is critical in:

* Credit Risk
* Insurance Pricing
* Fraud Prioritization
* Customer Targeting

---

## How would you monitor Logistic Regression in production?

Model Performance:

* Precision
* Recall
* F1 Score
* ROC-AUC
* PR-AUC
* Log Loss

Data Quality:

* Missing values
* Feature distribution shifts
* Data integrity checks

Drift Monitoring:

* Population Stability Index (PSI)
* Data Drift
* Feature Drift

Business Metrics:

* Default Rate
* Fraud Detection Rate
* Churn Reduction
* Conversion Rate

---

## How would you explain Logistic Regression to a business executive?

Logistic Regression estimates the likelihood of a business event occurring.

Example:

"This customer has an 85% probability of churning."

This probability score helps prioritize actions and allocate resources more effectively.

Benefits:

* Easy to understand
* Transparent
* Explainable
* Supports risk-based decision making

This is one reason Logistic Regression remains widely used in banking, insurance, healthcare, and risk management.

---

## When would you use L1 instead of L2?

Use L1 when:

* Feature selection is important
* Many features are irrelevant
* Simpler models are desired

Example:

Hundreds of variables with unknown importance.

---

## When would you use L2 instead of L1?

Use L2 when:

* Most features contain useful information
* Multicollinearity exists
* Feature elimination is not desired

Example:

Credit risk models where every feature has business significance.

---

## Difference Between Sigmoid and Softmax

Sigmoid:

* Binary classification
* Produces independent probabilities

Softmax:

* Multiclass classification
* Probabilities sum to 1

Therefore:

* Sigmoid → Binary Classification
* Softmax → Multiclass Classification

---

## When would you use One-vs-Rest?

Use when:

* Many classes exist
* Simplicity is important
* Computational efficiency is required

---

## When would you use Multinomial Logistic Regression?

Use when:

* Classes are mutually exclusive
* Probabilities should sum to 1
* A unified model is preferred

---

# Key Takeaways

* Supervised classification algorithm
* Produces probabilities using the sigmoid function
* Uses Maximum Likelihood Estimation
* Optimized using Log Loss
* High Bias, Low Variance model
* Highly interpretable and explainable
* Strong baseline model
* Widely used in banking, insurance, healthcare, and risk management
* Excellent choice when explainability is more important than marginal gains in accuracy
* One of the most frequently asked machine learning algorithms in interviews
