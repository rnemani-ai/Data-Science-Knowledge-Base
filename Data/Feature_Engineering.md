# Section 6: Feature Engineering

---

# 47. What Makes A Good Feature?

## Interview Answer

A good feature captures meaningful business information that helps the model distinguish between different outcomes.

Rather than creating many features, I focus on creating features that are predictive, available at prediction time, easy to maintain, and aligned with the business problem.

### Characteristics Of A Good Feature

- Predictive
- Business meaningful
- Available during inference
- Stable over time
- Easy to explain

### Enterprise Example

Instead of using **Total Purchases**, I might create **Average Purchase Value Over Last 90 Days**, which better captures recent customer behavior.

### Senior DS Tip

> "Good features beat complex models."

---

# 48. Feature Engineering Framework

## Interview Answer

I follow a structured framework rather than creating features randomly.

### My Framework

1. Understand the business problem.
2. Understand how decisions are made.
3. Brainstorm potential signals.
4. Create candidate features.
5. Validate feature importance.
6. Remove redundant features.
7. Ensure features are available in production.

### Questions I Always Ask

- Will this feature exist at prediction time?
- Does it leak future information?
- Does it capture business behavior?
- Is it easy to maintain?

### Senior DS Tip

> "Feature engineering should start with business understanding, not SQL."

---

# 49. Behavioral Features

## Interview Answer

Behavioral features describe how an entity behaves over time rather than its static attributes.

They're often among the most predictive features.

### Examples

Customer

- Purchase frequency
- Average order value
- Login frequency
- Time since last purchase

Supplier

- Average claim amount
- Claim submission frequency
- Approval rate

Telecommunications

- Average monthly usage
- Number of activations
- Payment consistency

### Senior DS Tip

> "Behavior predicts future behavior better than demographics."

---

# 50. Aggregation Features

## Interview Answer

Aggregation features summarize historical information into meaningful statistics.

They're especially useful when dealing with transactional data.

### Common Aggregations

- Count
- Sum
- Mean
- Median
- Maximum
- Minimum
- Standard Deviation

### Examples

Customer

- Number of purchases
- Total spend
- Average spend

Supplier

- Average claim value
- Total claims submitted
- Average processing time

### Senior DS Tip

> "Aggregation transforms raw events into meaningful business signals."

---

# 51. Ratio Features

## Interview Answer

Ratio features capture relationships between variables and are often more informative than the raw values.

### Examples

- Debt / Income
- Approved Claims / Total Claims
- Revenue / Customer
- Discount / Order Value
- Returned Items / Purchased Items

### Why They're Useful

Ratios normalize data and help compare entities of different sizes.

### Senior DS Tip

> "Ratios often reveal patterns that individual variables cannot."

---

# 52. Interaction Features

## Interview Answer

Interaction features capture relationships between two or more variables.

Sometimes two features together are much more predictive than either feature individually.

### Examples

- Income × Credit Score
- Age × Tenure
- Quantity × Unit Price
- Claim Amount × Supplier Type

### When I Use Them

Mostly with linear models where interactions aren't automatically learned.

Tree-based models often capture interactions naturally.

### Senior DS Tip

> "Interaction features help simple models learn complex relationships."

---

# 53. Time-Based Features

## Interview Answer

Time-based features capture seasonality, trends, and temporal behavior.

These are extremely valuable for most business problems.

### Common Features

- Day of Week
- Month
- Quarter
- Holiday Indicator
- Days Since Last Event
- Customer Tenure
- Rolling Average
- Lag Features

### Enterprise Example

For supplier claims, I might create **Days Since Last Claim** or **Average Claims Per Month**.

### Senior DS Tip

> "Time often contains more predictive information than people realize."

---

# 54. Domain Driven Features

## Interview Answer

The best features usually come from domain knowledge rather than automated feature generation.

I work closely with business stakeholders to understand what signals matter.

### Examples

CPG

- Claim Approval Rate
- Retailer Compliance Score
- Promotion Participation

Telecommunications

- Payment Consistency
- Device Replacement Frequency
- Service Usage Trend

### Senior DS Tip

> "Business experts often know the best features before the data scientists do."

---

# 55. Tell Me About A Feature You Created

## Interview Answer

One feature I'm particularly proud of was in a CPG document intelligence project.

The raw OCR confidence score alone wasn't very predictive, so instead of using it directly, I engineered a **Document Quality Score** by combining:

- OCR confidence
- Percentage of missing fields
- Number of extraction corrections
- Document completeness

This feature better represented the overall reliability of the extracted document and improved downstream classification performance while also helping prioritize documents for manual review.

### Why It Worked

- Combined multiple weak signals.
- Easy for business users to understand.
- Available in production.
- Improved model stability.

### Senior DS Tip

> "The best features simplify complex business behavior into a single meaningful signal."

---

# 56. Feature Engineering Pitfalls

## Interview Answer

Feature engineering can improve models significantly, but it's also one of the biggest sources of production issues.

### Common Pitfalls

- Data leakage.
- Creating features unavailable during inference.
- Over-engineering.
- Highly correlated features.
- Features with no business meaning.
- Features that are difficult to maintain.

### Best Practices

- Keep features interpretable.
- Validate with business stakeholders.
- Test in production pipelines.
- Document feature definitions.
- Continuously monitor feature drift.

### Senior DS Tip

> "A feature isn't valuable just because it improves offline accuracy—it also needs to be reliable, explainable, and maintainable."

---

# Quick Revision

## Remember

✅ Start with the business problem.

✅ Create meaningful features, not many features.

✅ Behavioral features are often highly predictive.

✅ Aggregations summarize history.

✅ Ratios normalize relationships.

✅ Interaction features help linear models.

✅ Time-based features capture trends and seasonality.

✅ Domain knowledge creates the best features.

✅ Avoid leakage during feature engineering.

## Memorable Quote

> **"Algorithms learn patterns. Feature engineering creates them."**