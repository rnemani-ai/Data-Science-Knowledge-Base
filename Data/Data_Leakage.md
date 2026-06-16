# Section 2: Data Leakage

---

# 10. What Is Data Leakage?

## Interview Answer

Data leakage occurs when the model has access to information during training that wouldn't be available at prediction time. This leads to overly optimistic validation performance but poor production performance.

I've found that leakage is one of the most common reasons why models perform well offline but fail after deployment.

### Key Points

* Produces unrealistically high accuracy
* Doesn't generalize to production
* Often introduced during feature engineering or data preparation
* Hard to detect unless you understand the business process

### Enterprise Example

Suppose we're predicting whether a supplier claim will be approved. If we include the **final approval status** or a field updated after manual review, the model is indirectly learning the answer instead of predicting it.

### Senior DS Tip

> "Whenever I see an unusually high validation score, I first suspect leakage before celebrating the model."

---

# 11. Types Of Data Leakage

## Interview Answer

There are several common types of data leakage that I watch for.

### Common Types

* **Target Leakage** – Features contain information about the target.
* **Train-Test Leakage** – Information from the test set influences training.
* **Temporal Leakage** – Future information is used to predict past events.
* **Feature Engineering Leakage** – Features are created using future data.
* **Data Preparation Leakage** – Scaling or imputation performed before train-test split.

### Enterprise Example

Using customer lifetime value to predict customer churn is leakage because lifetime value includes future customer behavior.

### Senior DS Tip

> "Different types of leakage have the same outcome—a model that looks great during development but fails in production."

---

# 12. How Do You Detect Data Leakage?

## Interview Answer

I use both technical validation and business understanding.

If a model suddenly achieves unrealistically high accuracy, I immediately investigate whether any feature contains future information.

### My Checklist

* Review every feature definition.
* Verify when each feature becomes available.
* Check whether features are derived from the target.
* Review the feature engineering pipeline.
* Validate with business SMEs.

### Red Flags

* Extremely high accuracy.
* SHAP shows unexpected top features.
* Feature becomes available only after the prediction event.
* Large drop from validation to production.

### Enterprise Example

In a fraud project, if a feature indicates whether an account was already investigated, it's effectively revealing the answer and should never be used for prediction.

### Senior DS Tip

> "The best way to detect leakage isn't statistics—it's understanding the business timeline."

---

# 13. How Do You Prevent Data Leakage?

## Interview Answer

Prevention starts with designing the pipeline correctly rather than trying to detect leakage later.

### Best Practices

* Split train and test data before preprocessing.
* Build feature engineering only on training data.
* Use production-available features only.
* Validate feature timestamps.
* Review features with business experts.
* Use separate preprocessing pipelines for train and inference.

### Enterprise Example

For document processing, I only use fields available immediately after OCR and extraction—not information added later during manual validation.

### Senior DS Tip

> "If a feature won't exist in production at prediction time, it shouldn't exist during training either."

---

# 14. Train-Test Leakage

## Interview Answer

Train-test leakage occurs when information from the test set influences the training process.

Common causes include scaling, encoding, feature selection, or imputation before splitting the data.

### Example

Incorrect:

* Scale the entire dataset.
* Split into train and test.

Correct:

* Split first.
* Fit scaler on training data.
* Apply the same scaler to test data.

### Enterprise Example

Using all customer records to calculate global statistics before splitting introduces information from the test set into training.

### Senior DS Tip

> "Every preprocessing step should learn only from the training data."

---

# 15. Temporal Leakage

## Interview Answer

Temporal leakage happens when future information is used to predict past events.

This is especially common in fraud detection, forecasting, and recommendation systems.

### Examples

* Using next month's balance to predict today's default.
* Using future transactions to predict current fraud.
* Using post-event customer behavior for churn prediction.

### Prevention

* Respect chronological order.
* Use time-based train-test splits.
* Build features only from historical information available at prediction time.

### Enterprise Example

When predicting fraudulent activations, I would only use information available up to the activation timestamp—not any subsequent investigation results.

### Senior DS Tip

> "Always ask yourself: Would this information exist when the prediction is actually made?"

---

# 16. Target Leakage

## Interview Answer

Target leakage occurs when one or more features directly or indirectly reveal the target variable.

It's one of the easiest ways to accidentally build a model that performs exceptionally well during training but fails completely in production.

### Examples

* Loan approval date predicting loan approval.
* Final claim status predicting claim approval.
* Customer cancellation reason predicting churn.

### Prevention

* Review feature definitions.
* Understand feature generation timing.
* Remove post-outcome variables.
* Validate with domain experts.

### Senior DS Tip

> "Any feature created after the business event is immediately suspicious."

---

# 17. Leakage In Feature Engineering

## Interview Answer

Feature engineering is one of the biggest sources of leakage because it's easy to accidentally use future information while creating aggregates or rolling statistics.

### Common Examples

* Future averages.
* Future transaction counts.
* Rolling windows including future dates.
* Customer lifetime statistics.

### Best Practices

* Build features using historical data only.
* Validate timestamp logic.
* Use time-aware feature engineering pipelines.

### Enterprise Example

Instead of calculating a customer's total purchases over their lifetime, I would calculate purchases only up to the prediction date.

### Senior DS Tip

> "Good feature engineering respects the timeline."

---

# 18. Leakage In Time Series Models

## Interview Answer

Time series models are particularly vulnerable to leakage because observations are ordered.

Random train-test splitting often introduces future information into training.

### Best Practices

* Use chronological train-test splits.
* Never shuffle observations.
* Create lag features correctly.
* Use rolling or expanding window validation.

### Enterprise Example

For sales forecasting, I would train on January–October, validate on November, and test on December instead of randomly splitting observations.

### Senior DS Tip

> "In time series, respecting time is more important than maximizing accuracy."

---

# Quick Revision

## Remember

✅ Split before preprocessing.

✅ Use only production-available features.

✅ Validate timestamps.

✅ Avoid future information.

✅ Review feature engineering carefully.

✅ Use time-aware validation for sequential data.

## Memorable Quote

> **"If the model knows the future, it's not intelligence—it's leakage."**
