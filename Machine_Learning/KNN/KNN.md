# K-Nearest Neighbors (KNN)

## Algorithm Snapshot

| Attribute                       | Value                                                    |
| ------------------------------- | -------------------------------------------------------- |
| Algorithm Type                  | Supervised Learning                                      |
| Problem Type                    | Classification & Regression                              |
| Parametric / Non-Parametric     | Non-Parametric                                           |
| Linear / Non-Linear             | Non-Linear                                               |
| Training Required               | Minimal                                                  |
| Learning Style                  | Lazy Learning                                            |
| Scaling Required                | Yes (Critical)                                           |
| Encoding Required               | Yes                                                      |
| Missing Values Handling         | No                                                       |
| Outlier Sensitive               | Yes                                                      |
| Feature Engineering Requirement | Moderate                                                 |
| Bias Level                      | Depends on K                                             |
| Variance Level                  | Depends on K                                             |
| Explainability                  | High                                                     |
| Probability Output              | Yes                                                      |
| Training Speed                  | Very Fast                                                |
| Prediction Speed                | Slow                                                     |
| Typical Dataset Size            | Small to Medium                                          |
| Common Use Cases                | Recommendation Systems, Classification, Pattern Matching |

---

## What is KNN?

K-Nearest Neighbors (KNN) is a supervised machine learning algorithm used for both classification and regression.

Unlike most machine learning algorithms, KNN does not learn an explicit mathematical model during training. Instead, it stores training observations and makes predictions based on the most similar observations.

Core Idea:

> Similar observations tend to have similar outcomes.

Examples:

* Customer Churn Prediction
* Fraud Detection
* Product Recommendation
* Medical Diagnosis
* Document Classification

---

## Data Preparation Requirements

| Requirement       | Needed?       | Notes                                           |
| ----------------- | ------------- | ----------------------------------------------- |
| Missing Values    | ❌             | Must be handled before training                 |
| Feature Scaling   | ✅             | Critical because KNN uses distance calculations |
| Encoding          | ✅             | Numerical input required                        |
| Outliers          | ⚠             | Can distort distances                           |
| Feature Selection | Helpful       | Improves performance in high dimensions         |
| Multicollinearity | Not Important | Distance-based algorithm                        |
| Explainability    | High          | Easy to explain                                 |

---

## Why Do We Need KNN?

Most machine learning algorithms attempt to learn relationships between features and targets.

KNN takes a different approach.

Instead of learning a model:

```text
Learn Model
↓
Predict
```

KNN uses:

```text
Find Similar Observations
↓
Use Their Outcomes
↓
Predict
```

This makes KNN intuitive and easy to understand.

---

## Intuition

Suppose we want to predict whether a customer will default on a loan.

Historical customers:

| Income | Debt Ratio | Default |
| ------ | ---------- | ------- |
| 50K    | 20%        | No      |
| 52K    | 22%        | No      |
| 48K    | 18%        | No      |
| 120K   | 80%        | Yes     |

New Customer:

* Income = 51K
* Debt Ratio = 21%

Nearest customers:

* 50K → No
* 52K → No
* 48K → No

Prediction:

**No Default**

Reason:

Most similar customers did not default.

---

## Parametric vs Non-Parametric

### Parametric Algorithms

Examples:

* Logistic Regression
* Linear Regression

Characteristics:

* Fixed number of parameters
* Learn explicit mathematical relationships

### Non-Parametric Algorithms

Examples:

* KNN
* Decision Trees

Characteristics:

* No fixed parameter structure
* Complexity grows with data

KNN is non-parametric because it stores observations rather than learning coefficients.

---

## Eager Learning vs Lazy Learning

### Eager Learning

Algorithms:

* Logistic Regression
* Random Forest
* XGBoost
* SVM

Process:

```text
Train Model
↓
Store Parameters
↓
Predict
```

### Lazy Learning

Algorithms:

* KNN

Process:

```text
Store Training Data
↓
Predict Later
```

No actual model is built during training.

This is why KNN is called a Lazy Learner.

---

## Internal Working

KNN follows four simple steps.

### Step 1: Choose K

K represents the number of neighbors.

Example:

```text
K = 5
```

Use the 5 closest observations.

### Step 2: Calculate Distance

Calculate distance between:

* New Observation
* Historical Observations

### Step 3: Identify Nearest Neighbors

Sort observations by distance.

Select the K closest observations.

### Step 4: Generate Prediction

#### Classification

Majority Voting

Example:

```text
Fraud
Fraud
Not Fraud
Fraud
Not Fraud
```

Prediction:

```text
Fraud
```

#### Regression

Average Neighbor Values

Example:

```text
100
110
120
130
140
```

Prediction:

```text
120
```

---

## Distance Metrics

Distance calculation is the heart of KNN.

### Euclidean Distance

Most commonly used.

Represents straight-line distance.

Best for:

* Continuous numerical features

### Manhattan Distance

Also called:

```text
City Block Distance
```

Measures movement along axes.

### Minkowski Distance

Generalized version of:

* Euclidean Distance
* Manhattan Distance

### Cosine Similarity

Frequently used for:

* NLP
* Search Systems
* Document Similarity

Measures similarity based on angle rather than physical distance.

---

## Weighted KNN

Standard KNN:

```text
All Neighbors Contribute Equally
```

Weighted KNN:

```text
Closer Neighbors Have Higher Influence
```

Example:

Distance:

```text
Neighbor A = 1
Neighbor B = 10
```

Neighbor A should influence the prediction more.

Weighted KNN often performs better.

---

## Choosing K

K is the most important hyperparameter.

### Small K

Example:

```text
K = 1
```

Characteristics:

* Low Bias
* High Variance
* Higher Overfitting Risk

### Large K

Example:

```text
K = 100
```

Characteristics:

* High Bias
* Low Variance
* Higher Underfitting Risk

### Practical Approach

Use:

* Cross Validation
* Grid Search

to determine the optimal value of K.

---

## Classification vs Regression

### Classification

Output:

* Class Label
* Probability

Examples:

* Fraud / Non-Fraud
* Churn / No Churn

### Regression

Output:

Numerical Value

Examples:

* Claim Amount
* House Price
* Demand Forecast

---

## What is the Output?

### Classification

Output:

* Probability
* Class Label

Example:

```text
Fraud Probability = 0.80
Prediction = Fraud
```

### Regression

Output:

Numerical Prediction

Example:

```text
Predicted Claim Amount = $10,500
```

---

## How to Interpret Output

Suppose:

```text
K = 10
```

Neighbors:

```text
8 Fraud
2 Non-Fraud
```

Interpretation:

```text
Fraud Probability = 80%
```

Prediction:

```text
Fraud
```

---

## Objective Function

Unlike:

* Logistic Regression
* XGBoost
* Neural Networks

KNN has:

```text
No Explicit Objective Function
```

There is no optimization process.

Predictions are based directly on neighboring observations.

---

## Optimization

No model training occurs.

The algorithm simply stores observations.

Most computation happens during prediction.

---

## Assumptions

Core Assumption:

> Similar observations tend to have similar outcomes.

Nearby observations should have similar labels or values.

---

## Feature Engineering Considerations

### Scaling

Critical.

Example:

Income:

```text
10,000 – 100,000
```

Age:

```text
20 – 60
```

Without scaling:

Income dominates distance calculations.

Recommended:

* StandardScaler
* MinMaxScaler

### Encoding

Required.

Examples:

* One-Hot Encoding
* Label Encoding

### Missing Values

Must be handled before training.

### Outliers

Can significantly affect nearest-neighbor calculations.

Recommended:

* Outlier Analysis
* Robust Scaling

---

## Bias-Variance Profile

| K Value | Bias | Variance |
| ------- | ---- | -------- |
| Small K | Low  | High     |
| Large K | High | Low      |

---

## Overfitting

Typically occurs when:

```text
K = 1
```

Characteristics:

* Sensitive to noise
* Memorizes training observations

Mitigation:

* Increase K
* Cross Validation

---

## Underfitting

Typically occurs when:

```text
K is Very Large
```

Characteristics:

* Oversmoothed predictions
* Misses local patterns

Mitigation:

* Reduce K

---

## Curse of Dimensionality

One of the most important KNN concepts.

As dimensions increase:

```text
Distances Become Less Meaningful
```

Example:

2 Features:

```text
Nearest Neighbors Easy To Find
```

100 Features:

```text
Everything Appears Equally Far
```

Result:

Prediction quality deteriorates.

---

## Hyperparameters

### K

Number of neighbors.

Most important parameter.

### Distance Metric

Options:

* Euclidean
* Manhattan
* Minkowski
* Cosine

### Weight Function

Options:

* Uniform
* Distance Weighted

---

## When Should You Use KNN?

✅ Small to Medium Datasets

✅ Recommendation Systems

✅ Similarity-Based Problems

✅ Pattern Recognition

✅ Baseline Models

Examples:

* Product Recommendations
* Customer Similarity Analysis
* Medical Diagnosis

---

## When Should You Avoid KNN?

❌ Large Datasets

❌ High-Dimensional Data

❌ Low-Latency Production Systems

Alternatives:

* XGBoost
* Random Forest
* Neural Networks

---

## Advantages

* Easy to Understand
* Easy to Implement
* No Training Phase
* Naturally Handles Non-Linear Relationships
* Strong Baseline Algorithm

---

## Limitations

* Slow Predictions
* Memory Intensive
* Sensitive to Scaling
* Sensitive to Outliers
* Suffers from Curse of Dimensionality

---

## Common Production Challenges

* Prediction Latency
* Large Memory Requirements
* Feature Scaling Consistency
* Data Drift
* Feature Drift

---

## Monitoring

### Model Metrics

* Accuracy
* Precision
* Recall
* F1 Score

### Data Metrics

* Missing Values
* Feature Drift
* Scaling Consistency

### Business Metrics

* Recommendation Accuracy
* Fraud Detection Rate
* Churn Reduction

---

## Key Takeaways

* KNN is a distance-based learning algorithm.
* KNN is non-parametric.
* KNN is a lazy learner.
* No explicit training occurs.
* Scaling is critical.
* K controls the bias-variance tradeoff.
* Weighted KNN often performs better.
* Suffers from the curse of dimensionality.

---

## Senior Data Scientist Summary

Think of KNN as:

```text
Similarity-Based Learning
+
Distance Metrics
+
Lazy Learning
```

Most Important Interview Insights:

* KNN does not learn a model.
* KNN predicts using the K most similar observations.
* Small K → Low Bias, High Variance.
* Large K → High Bias, Low Variance.
* Scaling is critical because predictions depend entirely on distance calculations.
* Curse of Dimensionality is the biggest limitation of KNN.
