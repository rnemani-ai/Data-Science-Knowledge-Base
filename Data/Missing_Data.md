# Section 3: Missing Data

---

# 19. How Do You Handle Missing Data?

## Interview Answer

I never treat missing values as just a data cleaning problem. My first step is understanding **why the data is missing**, because that often determines the right strategy. Sometimes missing values carry business meaning and can even become predictive features.

### My Approach

* Identify missing value percentage.
* Understand the reason for missingness.
* Determine whether it's random or systematic.
* Choose an appropriate imputation strategy.
* Validate the impact on model performance.

### Enterprise Example

In a supplier claim dataset, a missing **discount amount** might simply mean no discount was applied rather than bad data. In that case, replacing it with zero may be more appropriate than using the mean.

### Senior DS Tip

> "Don't impute first. Understand why the data is missing."

---

# 20. MCAR vs MAR vs MNAR

## Interview Answer

Understanding the type of missingness helps determine the appropriate handling strategy.

### Types

**MCAR (Missing Completely At Random)**

* Missingness is unrelated to any variable.
* Least problematic.
* Simple imputation usually works.

Example:
A sensor randomly fails.

---

**MAR (Missing At Random)**

* Missingness depends on other observed variables.

Example:
Higher-income customers are less likely to report their age.

Can often be handled with model-based imputation.

---

**MNAR (Missing Not At Random)**

* Missingness depends on the missing value itself.

Example:
Customers with very high salaries choose not to disclose income.

Usually requires domain knowledge and careful handling.

### Senior DS Tip

> "The hardest part isn't filling missing values—it's understanding why they're missing."

---

# 21. Missing Data Detection

## Interview Answer

Before deciding how to handle missing data, I quantify and understand the missingness.

### My Checklist

* Missing value percentage per feature.
* Missing value percentage per record.
* Missing value patterns.
* Correlation between missingness and target.
* Missingness by business segment.
* Missingness over time.

### Enterprise Example

If missing invoice numbers suddenly increase after a deployment, it's more likely a pipeline issue than a modeling issue.

### Senior DS Tip

> "A spike in missing values often indicates a broken pipeline, not bad data."

---

# 22. Imputation Techniques

## Interview Answer

There's no single best imputation technique. The choice depends on the feature, missingness mechanism, and business context.

### Common Techniques

* Mean Imputation
* Median Imputation
* Mode Imputation
* Constant Value
* Forward/Backward Fill (Time Series)
* KNN Imputation
* Model-Based Imputation
* Multiple Imputation

I generally start with simple techniques and move to more sophisticated methods only if they improve performance.

### Enterprise Example

For transactional data, median imputation is often more robust than mean because financial data is usually skewed.

### Senior DS Tip

> "Simple imputation often performs surprisingly well."

---

# 23. Mean vs Median Imputation

## Interview Answer

My choice depends on the distribution of the feature.

### Mean Imputation

Use when:

* Data is approximately normally distributed.
* Few outliers exist.

Pros:

* Simple
* Fast

Cons:

* Sensitive to outliers.

---

### Median Imputation

Use when:

* Data is skewed.
* Outliers exist.

Pros:

* More robust.

Cons:

* Slightly less efficient for normally distributed data.

### Rule of Thumb

* Normal Distribution → Mean
* Skewed Distribution → Median

### Senior DS Tip

> "For real-world business data, I use median more often than mean because most enterprise datasets are skewed."

---

# 24. KNN Imputation

## Interview Answer

KNN Imputation estimates missing values using similar observations.

It works well when similar records tend to have similar feature values.

### Advantages

* Preserves relationships between variables.
* Often more accurate than simple imputation.

### Limitations

* Computationally expensive.
* Doesn't scale well.
* Sensitive to feature scaling.

### When I Use It

Mostly for moderate-sized datasets where feature relationships are important.

### Senior DS Tip

> "I only consider KNN when the additional complexity is justified by better performance."

---

# 25. Model-Based Imputation

## Interview Answer

Instead of using summary statistics, model-based imputation predicts missing values using other available features.

Examples include:

* Random Forest
* XGBoost
* Regression Models

### Advantages

* Captures relationships between variables.
* Often more accurate.

### Limitations

* More computationally expensive.
* Can introduce bias if the prediction model is poor.

### Enterprise Example

Predicting missing customer income using occupation, education, location, and spending history.

### Senior DS Tip

> "Model-based imputation is useful when the missing feature is highly predictable from other variables."

---

# 26. When Should You Drop Features?

## Interview Answer

I don't drop features based only on missing value percentage.

I evaluate:

* Business importance.
* Predictive value.
* Availability in production.
* Cost of collecting the feature.

### Typical Guidelines

Drop when:

* Extremely high missing percentage (e.g., >70–80%).
* Low business value.
* Poor predictive importance.
* Difficult to collect consistently.

Keep when:

* Strong business relevance.
* Missingness itself is informative.
* High predictive power.

### Senior DS Tip

> "A feature with 60% missing values can still be valuable if the remaining 40% contains strong predictive information."

---

# 27. Missing Data In Production

## Interview Answer

Handling missing data doesn't stop after model training.

In production, I continuously monitor missing value rates because sudden increases often indicate upstream pipeline issues.

### What I Monitor

* Missing value percentage.
* Missing by feature.
* Missing by source system.
* Missing over time.
* Prediction failures caused by missing inputs.

### Actions

* Trigger alerts.
* Route incomplete records for review.
* Apply fallback logic.
* Retrain if missingness patterns change significantly.

### Enterprise Example

In a document extraction pipeline, if OCR suddenly fails to extract invoice numbers for many documents, I would investigate the OCR service before questioning the extraction model.

### Senior DS Tip

> "Missing values in production are often a data engineering problem before they're a machine learning problem."

---

# Quick Revision

## Remember

✅ Understand why data is missing before imputing.

✅ MCAR < MAR < MNAR in terms of difficulty.

✅ Median works better for skewed data.

✅ Start simple before using complex imputation.

✅ Missingness itself can be predictive.

✅ Monitor missing values continuously in production.

## Memorable Quote

> **"Missing data is information—don't throw it away without understanding why it's missing."**
