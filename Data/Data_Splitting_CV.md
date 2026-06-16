# Data Splitting & Cross Validation

---

# 1. Train Test Validation Split

## Interview Answer

I typically split the data into **Training**, **Validation**, and **Test** sets.

- **Training Set** → Train the model.
- **Validation Set** → Hyperparameter tuning and model selection.
- **Test Set** → Final unbiased evaluation.

A common split is **70-15-15** or **80-10-10**, depending on dataset size.

### When I Use It

- Most supervised learning problems.
- Hyperparameter tuning.
- Multiple model comparisons.

### Senior DS Tip

> "The test set should only be used once—after the final model has been selected."

---

# 2. Stratified Splits

## Interview Answer

Stratified splitting ensures the target class distribution remains consistent across the train, validation, and test sets.

This is particularly important for imbalanced classification problems.

### Example

Original Dataset

- Positive = 10%
- Negative = 90%

Every split should maintain approximately the same ratio.

### When I Use It

- Classification problems.
- Imbalanced datasets.

### Senior DS Tip

> "For classification, stratified splitting is usually my default choice."

---

# 3. Time Series Splits

## Interview Answer

For time series data, I never randomly shuffle observations.

Instead, I split the data chronologically so the model only learns from past data to predict future events.

### Example

Train

Jan–Sep

Validation

Oct

Test

Nov–Dec

### Why?

Random splits introduce temporal leakage.

### Senior DS Tip

> "Future data should never be used to predict the past."

---

# 4. Holdout Validation

## Interview Answer

Holdout validation reserves a portion of the dataset for evaluation while training on the remainder.

It's simple and computationally efficient.

### Advantages

- Fast.
- Easy to implement.

### Limitations

- Performance depends on a single split.
- Less reliable for small datasets.

### When I Use It

- Large datasets.
- Baseline models.
- Quick experimentation.

### Senior DS Tip

> "Holdout validation is fast, but Cross Validation provides a more reliable estimate."

---

# 5. K-Fold Cross Validation

## Interview Answer

K-Fold Cross Validation divides the dataset into **K equal folds**.

The model trains K times, each time using a different fold for validation.

The final performance is the average across all folds.

### Common Choice

5-Fold or 10-Fold

### Advantages

- Better estimate of model performance.
- Uses all observations for training and validation.

### Limitations

- Computationally expensive.

### Senior DS Tip

> "Cross Validation reduces the risk of making decisions based on a lucky split."

---

# 6. Stratified K-Fold

## Interview Answer

Stratified K-Fold combines K-Fold Cross Validation with stratified sampling.

Each fold preserves the class distribution.

### When I Use It

- Imbalanced classification.
- Fraud detection.
- Medical diagnosis.
- Rare event prediction.

### Why?

Without stratification, some folds may contain very few positive examples.

### Senior DS Tip

> "For imbalanced classification, I almost always prefer Stratified K-Fold."

---

# 7. Repeated K-Fold

## Interview Answer

Repeated K-Fold performs K-Fold Cross Validation multiple times using different random splits.

This provides a more stable estimate of model performance.

### Advantages

- Reduces variance.
- More reliable evaluation.

### Limitations

- Increased computation time.

### When I Use It

- Small datasets.
- Model benchmarking.
- Performance comparison.

### Senior DS Tip

> "Repeated K-Fold gives me greater confidence that the results aren't due to one particular split."

---

# 8. Time Series Cross Validation

## Interview Answer

Time Series Cross Validation respects chronological order by progressively expanding the training window.

### Example

Fold 1

Train → Jan–Mar

Validate → Apr

---

Fold 2

Train → Jan–Apr

Validate → May

---

Fold 3

Train → Jan–May

Validate → Jun

### Advantages

- Mimics production.
- Prevents temporal leakage.
- More realistic evaluation.

### Senior DS Tip

> "For forecasting problems, traditional K-Fold is incorrect."

---

# 9. Leave-One-Out Cross Validation (LOOCV)

## Interview Answer

Leave-One-Out Cross Validation trains the model on all observations except one.

This process repeats until every observation has been used as the validation sample once.

### Advantages

- Maximum use of available data.
- Nearly unbiased estimate.

### Limitations

- Extremely computationally expensive.
- High variance.
- Rarely used for large datasets.

### When I Use It

Only for very small datasets.

### Senior DS Tip

> "LOOCV is theoretically attractive but rarely practical in enterprise environments."

---

# Quick Revision

## Remember

✅ Train → Learn model parameters.

✅ Validation → Tune hyperparameters.

✅ Test → Final unbiased evaluation.

✅ Use Stratified Splits for classification.

✅ Use chronological splits for time series.

✅ K-Fold gives more reliable estimates than a single holdout.

✅ Stratified K-Fold is ideal for imbalanced classification.

✅ Time Series CV prevents temporal leakage.

✅ LOOCV is mainly useful for very small datasets.

## Memorable Quote

> **"A good model trained on a bad validation strategy can still fail in production."**


When do you use Train-Test Split versus Cross Validation?"
I'd answer:
"If I have millions of records, a simple train-validation-test split is usually sufficient because each split is already representative. For smaller datasets, I prefer K-Fold Cross Validation since it provides a more reliable estimate by evaluating the model across multiple data splits. For time-series problems, I always use chronological validation to avoid temporal leakage."

