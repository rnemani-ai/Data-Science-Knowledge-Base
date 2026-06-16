# Section 7: Encoding & Scaling

---

# 57. One Hot Encoding

## Interview Answer

One Hot Encoding converts each category into a separate binary column. It's the safest encoding technique for nominal categorical variables because it doesn't introduce any artificial ordering.

### When I Use It

* Nominal categories
* Low cardinality features
* Linear models
* Neural Networks

### Example

Color:

* Red
* Blue
* Green

↓

| Red | Blue | Green |
| --- | ---- | ----- |
| 1   | 0    | 0     |

### Limitation

Creates many columns for high-cardinality features.

### Senior DS Tip

> "One Hot Encoding is my default choice for nominal categorical variables."

---

# 58. Label Encoding

## Interview Answer

Label Encoding assigns an integer to each category.

Example:

High → 2

Medium → 1

Low → 0

I only use it when categories are naturally ordered or when working with tree-based algorithms that don't interpret the numeric values as continuous.

### When I Use It

* Tree-based models
* Binary variables
* Ordinal categories

### Avoid For

Linear Regression

Logistic Regression

SVM

KNN

### Senior DS Tip

> "Label Encoding can unintentionally introduce order where none exists."

---

# 59. Ordinal Encoding

## Interview Answer

Ordinal Encoding is appropriate when categories have a meaningful ranking.

### Examples

Customer Satisfaction

* Poor
* Fair
* Good
* Excellent

Education

* High School
* Bachelor's
* Master's
* PhD

Unlike Label Encoding, the ordering represents real business meaning.

### Senior DS Tip

> "Only use Ordinal Encoding when the order actually exists."

---

# 60. Target Encoding

## Interview Answer

Target Encoding replaces each category with the average value of the target variable for that category.

Example:

Supplier A → 92% approval rate

Supplier B → 68% approval rate

It works well for high-cardinality features but must be applied carefully to avoid data leakage.

### Advantages

* Handles many categories.
* Reduces dimensionality.
* Often improves predictive performance.

### Risks

* Target leakage.
* Overfitting.

### Best Practice

Compute target encoding using only the training data (often with cross-validation).

### Senior DS Tip

> "Target Encoding is powerful, but leakage is its biggest risk."

---

# 61. Frequency Encoding

## Interview Answer

Frequency Encoding replaces each category with its frequency or count in the dataset.

### Example

Country

USA → 45%

Canada → 20%

Mexico → 10%

### Advantages

* Simple.
* Handles high-cardinality features.
* Doesn't create extra columns.

### Limitations

* Doesn't capture the relationship with the target.

### Senior DS Tip

> "Frequency Encoding is a lightweight alternative when One Hot Encoding becomes impractical."

---

# 62. High Cardinality Features

## Interview Answer

High-cardinality features contain many unique values, such as customer IDs, product IDs, or ZIP codes.

Using One Hot Encoding in these cases creates thousands of sparse columns and increases model complexity.

### My Approach

* Evaluate business value.
* Remove IDs with no predictive signal.
* Use Target or Frequency Encoding.
* Group rare categories into "Other."

### Enterprise Example

Instead of One Hot Encoding thousands of supplier IDs, I would consider Target Encoding or grouping infrequent suppliers.

### Senior DS Tip

> "High-cardinality features require thoughtful encoding—not automatic One Hot Encoding."

---

# 63. Why Scaling Matters

## Interview Answer

Scaling ensures numerical features are on comparable ranges, preventing variables with large magnitudes from dominating the learning process.

Distance-based and gradient-based algorithms are particularly sensitive to feature scales.

### Algorithms That Need Scaling

* Logistic Regression
* Linear Regression
* SVM
* KNN
* Neural Networks
* PCA

### Algorithms That Don't

* Decision Trees
* Random Forest
* XGBoost
* LightGBM
* CatBoost

### Senior DS Tip

> "Scaling changes the magnitude, not the information."

---

# 64. Standardization

## Interview Answer

Standardization transforms data so that it has a mean of 0 and a standard deviation of 1.

### When I Use It

* Normally distributed features.
* Gradient-based algorithms.
* PCA.

### Advantages

* Handles different feature scales.
* Widely used in ML pipelines.

### Limitations

* Sensitive to outliers.

### Senior DS Tip

> "Standardization is my default scaling method unless I have a reason to choose another."

---

# 65. Min-Max Scaling

## Interview Answer

Min-Max Scaling transforms values into a fixed range, typically between 0 and 1.

### When I Use It

* Neural Networks.
* KNN.
* Features with known minimum and maximum values.

### Advantages

* Preserves relationships.
* Bounded output.

### Limitations

* Very sensitive to outliers.

### Senior DS Tip

> "If extreme values exist, Min-Max Scaling may not be the best choice."

---

# 66. Robust Scaling

## Interview Answer

Robust Scaling uses the median and interquartile range instead of the mean and standard deviation.

This makes it much less sensitive to outliers.

### When I Use It

* Financial data.
* Transaction data.
* Highly skewed distributions.

### Advantages

* Robust to extreme values.
* Better for real-world business data.

### Senior DS Tip

> "For enterprise datasets with many outliers, Robust Scaling is often a better choice than Standardization."

---

# 67. Which Algorithms Require Scaling?

## Interview Answer

Algorithms that rely on distances or gradient optimization generally require scaling.

### Requires Scaling

* Linear Regression
* Logistic Regression
* SVM
* KNN
* Neural Networks
* PCA
* K-Means

### Why?

Because differences in feature magnitude directly affect model training.

### Senior DS Tip

> "If the algorithm measures distance or optimizes gradients, I almost always scale the data."

---

# 68. Which Algorithms Do Not?

## Interview Answer

Tree-based algorithms split data using thresholds rather than distances, so scaling has little or no impact.

### Usually No Scaling Needed

* Decision Tree
* Random Forest
* XGBoost
* LightGBM
* CatBoost

### Why?

The ordering of values matters, not their absolute magnitude.

### Enterprise Example

Whether customer income is stored as **50,000** or **0.5**, a Decision Tree will identify the same optimal split.

### Senior DS Tip

> "I don't scale data just because it's good practice—I scale it only when the algorithm benefits from it."

---

# Quick Revision

## Remember

✅ One Hot Encoding for nominal categories.

✅ Ordinal Encoding only when order exists.

✅ Target Encoding is powerful but can cause leakage.

✅ Frequency Encoding works well for high-cardinality features.

✅ Scale for distance-based and gradient-based algorithms.

✅ Don't scale tree-based models.

✅ Standardization is the default.

✅ Robust Scaling handles outliers better.

## Memorable Quote

> **"Encoding helps models understand categories. Scaling helps models compare numbers."**
