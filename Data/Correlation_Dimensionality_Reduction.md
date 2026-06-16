# Section 8: Correlation & Dimensionality Reduction

---

# 69. Correlation vs Causation

## Interview Answer

Correlation means two variables move together, while causation means one variable directly influences the other.

A high correlation doesn't imply a cause-and-effect relationship, so I avoid making business decisions based solely on correlation.

### Example

Ice cream sales and drowning incidents both increase during summer.

They're correlated because of temperature, not because one causes the other.

### Senior DS Tip

> "Correlation helps generate hypotheses. Business validation establishes causation."

---

# 70. Pearson Correlation

## Interview Answer

Pearson Correlation measures the strength of a **linear relationship** between two numerical variables.

Correlation ranges from **-1 to +1**.

* +1 → Perfect positive relationship
* 0 → No linear relationship
* -1 → Perfect negative relationship

### When I Use It

* Continuous numerical variables.
* Approximately linear relationships.

### Limitations

* Sensitive to outliers.
* Doesn't capture non-linear relationships.

### Senior DS Tip

> "Pearson only measures linear relationships."

---

# 71. Spearman Correlation

## Interview Answer

Spearman Correlation measures **monotonic relationships** using feature ranks instead of raw values.

Unlike Pearson, it doesn't assume linearity.

### When I Use It

* Ordinal variables.
* Skewed data.
* Non-linear but monotonic relationships.
* Data with outliers.

### Example

As experience increases, salary generally increases, although not necessarily linearly.

### Senior DS Tip

> "If the relationship isn't linear, I usually check Spearman before Pearson."

---

# 72. Multicollinearity

## Interview Answer

Multicollinearity occurs when two or more features are highly correlated.

This mainly affects linear models because it makes coefficient estimates unstable.

### Problems

* Unstable coefficients.
* Difficult interpretation.
* Increased variance.

### Algorithms Most Affected

* Linear Regression
* Logistic Regression

### Less Affected

* Decision Trees
* Random Forest
* XGBoost

### Senior DS Tip

> "Multicollinearity hurts interpretability more than prediction."

---

# 73. Variance Inflation Factor (VIF)

## Interview Answer

VIF measures how much a feature's variance is inflated because of correlation with other features.

### Rule of Thumb

* VIF < 5 → Usually acceptable.
* VIF 5–10 → Investigate.
* VIF > 10 → Strong multicollinearity.

### What I Do

* Remove redundant features.
* Combine correlated variables.
* Apply PCA if appropriate.

### Senior DS Tip

> "I mainly use VIF when building interpretable linear models."

---

# 74. Correlated Features

## Interview Answer

Highly correlated features often provide redundant information.

Whether I remove them depends on the algorithm and business context.

### Linear Models

Usually remove one of the correlated features.

### Tree-Based Models

Often keep both unless there's a business reason to simplify the model.

### Enterprise Example

Annual Income and Monthly Income are highly correlated.

Keeping both in Linear Regression usually provides little additional value.

### Senior DS Tip

> "Correlation isn't automatically bad—redundancy is."

---

# 75. Feature Selection Techniques

## Interview Answer

Feature selection improves model performance, interpretability, and training efficiency.

### Common Techniques

**Filter Methods**

* Correlation
* Chi-Square
* Mutual Information

**Wrapper Methods**

* Recursive Feature Elimination (RFE)

**Embedded Methods**

* Lasso Regression
* Random Forest Feature Importance
* XGBoost Feature Importance

### My Approach

I usually start with business knowledge, then validate using model-based importance.

### Senior DS Tip

> "Business understanding should guide feature selection—not replace it."

---

# 76. Skewness

## Interview Answer

Skewness measures the asymmetry of a distribution.

### Types

Positive Skew

* Long right tail.

Negative Skew

* Long left tail.

### Why It Matters

Highly skewed features may affect:

* Linear Regression
* Logistic Regression
* PCA

### Common Solutions

* Log Transformation.
* Box-Cox Transformation.
* Robust Scaling.

### Senior DS Tip

> "Most business data is positively skewed."

---

# 77. Kurtosis

## Interview Answer

Kurtosis measures how heavy the tails of a distribution are.

Higher kurtosis indicates more extreme observations.

### Why It Matters

* Indicates potential outliers.
* Helps understand distribution shape.
* Useful during EDA.

### Interpretation

High Kurtosis

* More extreme values.

Low Kurtosis

* Fewer extreme observations.

### Senior DS Tip

> "I use kurtosis as an indicator—not as a decision rule."

---

# 78. PCA (Principal Component Analysis)

## Interview Answer

PCA is a dimensionality reduction technique that transforms correlated features into a smaller set of uncorrelated principal components while preserving as much variance as possible.

### Why Use PCA

* Reduce dimensionality.
* Remove multicollinearity.
* Improve computational efficiency.
* Visualize high-dimensional data.

### Limitations

* Reduced interpretability.
* Components don't have direct business meaning.

### Senior DS Tip

> "I rarely use PCA when business explainability is important."

---

# 79. Explained Variance

## Interview Answer

Explained variance tells us how much information each principal component retains from the original data.

### Example

PC1 → 55%

PC2 → 25%

PC3 → 10%

The first two components explain 80% of the total variance.

### How I Use It

I retain enough components to explain around **90–95%** of the variance, depending on the use case.

### Senior DS Tip

> "The goal isn't to maximize dimensionality reduction—it's to retain useful information."

---

# 80. Curse Of Dimensionality

## Interview Answer

As the number of features increases, data becomes sparse, distances become less meaningful, and models often require significantly more data to generalize well.

### Problems

* Increased overfitting.
* Longer training times.
* Poor distance calculations.
* Higher computational cost.

### Solutions

* Feature Selection.
* PCA.
* Regularization.
* Collect more data.

### Algorithms Most Affected

* KNN
* K-Means
* SVM
* Neural Networks

### Senior DS Tip

> "More features don't necessarily create better models—only better information does."

---

# Quick Revision

## Remember

✅ Correlation ≠ Causation.

✅ Pearson → Linear relationships.

✅ Spearman → Monotonic relationships.

✅ VIF detects multicollinearity.

✅ Tree models handle correlated features better.

✅ Start feature selection with business understanding.

✅ Skewness measures asymmetry.

✅ Kurtosis measures extreme values.

✅ PCA reduces dimensions but sacrifices interpretability.

✅ More features aren't always better.

## Memorable Quote

> **"A Senior Data Scientist doesn't try to use every feature—they identify the few that truly matter."**
