# Section 5: Imbalanced Data

---

# 38. How Do You Detect Imbalance?

## Interview Answer

The first thing I check is the class distribution. However, I don't rely only on percentages—I also consider the business impact of the minority class.

For example, a dataset with 95% negative and 5% positive classes may be perfectly normal for fraud detection, but it requires special handling during modeling and evaluation.

### My Approach

- Check class distribution.
- Visualize the target variable.
- Evaluate baseline metrics.
- Understand business costs of misclassification.

### Enterprise Example

In a document approval system, only 3% of claims may require manual review. This is naturally imbalanced, but those 3% are often the most important cases.

### Senior DS Tip

> "Class imbalance isn't the problem. Ignoring it is."

---

# 39. Why Accuracy Fails

## Interview Answer

Accuracy can be misleading when classes are imbalanced.

Imagine a dataset where only 1% of transactions are fraudulent.

A model predicting every transaction as **Not Fraud** achieves 99% accuracy but provides zero business value.

That's why I prefer metrics like Precision, Recall, F1-Score, PR-AUC, and ROC-AUC depending on the use case.

### Example

Dataset:

- 990 Legitimate
- 10 Fraud

Model predicts:

- All Legitimate

Accuracy = 99%

Recall = 0%

The model completely fails to identify fraud.

### Senior DS Tip

> "High accuracy doesn't always mean a good model."

---

# 40. Class Weighting

## Interview Answer

Instead of changing the data, class weighting changes the learning process by assigning higher penalties to mistakes on the minority class.

Most ML algorithms support class weights, making this one of the first techniques I try.

### Advantages

- No synthetic data.
- Simple to implement.
- Preserves original distribution.

### Limitations

- Doesn't always solve severe imbalance.

### When I Use It

- Logistic Regression
- SVM
- Decision Trees
- Random Forest
- XGBoost (scale_pos_weight)

### Senior DS Tip

> "I usually try class weighting before modifying the dataset."

---

# 41. Oversampling

## Interview Answer

Oversampling increases the number of minority class observations to create a more balanced training dataset.

### Common Methods

- Random Oversampling
- SMOTE
- ADASYN

### Advantages

- Improves minority class learning.
- Preserves majority class.

### Limitations

- Can increase overfitting if duplicate observations are created.

### Enterprise Example

If only 5% of supplier claims are rejected, oversampling can help the model learn rejection patterns more effectively.

### Senior DS Tip

> "Oversample only the training data—never the test set."

---

# 42. Undersampling

## Interview Answer

Undersampling balances the dataset by reducing the number of majority class observations.

### Advantages

- Faster training.
- Reduces computational cost.

### Limitations

- May discard useful information.
- Can reduce model performance if too much data is removed.

### When I Use It

- Extremely large datasets.
- When computational efficiency is important.

### Senior DS Tip

> "Undersampling is acceptable when you have millions of majority-class observations."

---

# 43. SMOTE

## Interview Answer

SMOTE (Synthetic Minority Over-sampling Technique) generates synthetic minority class samples instead of simply duplicating existing ones.

It creates new observations by interpolating between similar minority class examples.

### Advantages

- Reduces overfitting compared to random oversampling.
- Produces more diverse minority samples.

### Limitations

- Can generate unrealistic observations.
- Doesn't work well when minority classes overlap significantly.

### Enterprise Example

SMOTE can help when predicting rare supplier claim exceptions by generating additional realistic training examples.

### Senior DS Tip

> "SMOTE is useful, but I always validate whether the synthetic data actually improves generalization."

---

# 44. Threshold Optimization

## Interview Answer

The default classification threshold of 0.5 is rarely optimal.

Instead, I choose a threshold based on business objectives and the cost of false positives versus false negatives.

### Examples

Fraud Detection

- Lower threshold to catch more fraud.

Medical Diagnosis

- Lower threshold to avoid missing patients.

Marketing

- Higher threshold to avoid targeting unlikely responders.

### Senior DS Tip

> "Threshold selection is a business decision, not just a modeling decision."

---

# 45. Precision vs Recall Tradeoffs

## Interview Answer

The choice between Precision and Recall depends on which type of error is more costly.

### Precision

Question:

> Of all predicted positives, how many were actually positive?

Use when:

- False positives are expensive.

Examples:

- Spam filters
- Loan approvals
- Marketing campaigns

---

### Recall

Question:

> Of all actual positives, how many did we identify?

Use when:

- False negatives are expensive.

Examples:

- Fraud detection
- Medical diagnosis
- Manufacturing defects

### Senior DS Tip

> "Always ask the business which mistake is more expensive."

---

# 46. PR-AUC

## Interview Answer

PR-AUC (Precision-Recall Area Under the Curve) evaluates how well the model balances Precision and Recall across different thresholds.

Unlike ROC-AUC, PR-AUC focuses on the positive class, making it much more informative for highly imbalanced datasets.

### When I Use It

- Fraud Detection.
- Medical Diagnosis.
- Rare Event Prediction.
- Quality Inspection.

### ROC-AUC vs PR-AUC

| ROC-AUC | PR-AUC |
|----------|---------|
| Works well for balanced data | Better for imbalanced data |
| Considers both classes | Focuses on positive class |
| Can appear overly optimistic | Better reflects minority-class performance |

### Senior DS Tip

> "For highly imbalanced problems, I trust PR-AUC more than Accuracy or even ROC-AUC."

---

# Quick Revision

## Remember

✅ Check class distribution before modeling.

✅ Accuracy is misleading for imbalanced data.

✅ Start with class weighting.

✅ Oversample only the training set.

✅ Use undersampling when the majority class is extremely large.

✅ Validate whether SMOTE improves performance.

✅ Optimize thresholds based on business cost.

✅ Choose Precision or Recall based on business priorities.

✅ Prefer PR-AUC for highly imbalanced datasets.

## Memorable Quote

> **"An imbalanced dataset isn't difficult because one class is small—it's difficult because the business usually cares most about that small class."**