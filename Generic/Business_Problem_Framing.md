# 04_Senior_DS_Playbook.md

# Section 1: Business & Problem Framing

---

# 1. How Do You Approach A New ML Problem?

## Interview Answer

The first thing I try to understand is the business problem, not the model.

Many machine learning projects struggle because teams jump directly into algorithm selection before defining the decision they are trying to improve.

My framework is:

### Step 1: Understand The Business Problem

Questions I ask:

* What business problem are we solving?
* What decision will this model support?
* Who are the stakeholders?
* What action will be taken based on predictions?
* How will success be measured?

Example:

Instead of saying:

> Build a churn model.

I want to understand:

> What action will be taken when a customer is predicted to churn?

Without a clear action plan, even a highly accurate model may create little business value.

---

### Step 2: Understand The Data

I evaluate:

* Data availability
* Data quality
* Data lineage
* Data representativeness
* Missing values
* Leakage risks
* Potential biases

Questions:

* Is the data trustworthy?
* Is it representative of production users?
* Is there enough signal to solve the problem?

---

### Step 3: Define Success Metrics

I define metrics before building models.

Examples:

| Business Problem       | Primary Metric           |
| ---------------------- | ------------------------ |
| Fraud Detection        | Recall                   |
| Customer Churn         | Recall + Business Impact |
| Credit Risk            | Precision + Recall       |
| Demand Forecasting     | MAE / RMSE               |
| Recommendation Systems | CTR / Conversion         |

---

### Step 4: Build A Baseline

Before introducing complexity:

* Logistic Regression
* Linear Regression
* Business Rules
* Historical Average

A baseline helps quantify the value of more sophisticated approaches.

---

### Step 5: Feature Engineering

Focus areas:

* Behavioral features
* Aggregated features
* Interaction features
* Temporal features

In many projects, feature engineering creates more value than changing algorithms.

---

### Step 6: Model Development

Examples:

* Logistic Regression
* Random Forest
* XGBoost
* LightGBM
* Neural Networks

Model choice depends on:

* Explainability requirements
* Data size
* Latency constraints
* Business risk

---

### Step 7: Validation

* Cross Validation
* Holdout Testing
* Time Series Validation (if applicable)

Avoid leakage throughout the process.

---

### Step 8: Deployment Readiness

Questions:

* Can this be monitored?
* Can this be retrained?
* Can stakeholders trust it?
* Can operations teams use it?

---

## Enterprise Perspective

One lesson I've learned is that model performance alone is not enough.

I always ask:

* How can this system fail?
* How will we detect failure?
* What business impact occurs when it fails?
* Who is accountable?

Many projects fail because teams optimize model metrics instead of business outcomes.

---

## Common Follow-Up Questions

### What if stakeholders disagree on success metrics?

I align stakeholders before model development begins.

Building a model without agreement on success criteria often leads to adoption problems later.

### What if data quality is poor?

I quantify the problem.

Sometimes improving data collection creates more value than changing algorithms.

---

## Senior DS Insight

The goal is not building the most sophisticated model.

The goal is building a solution that:

* Creates measurable business value
* Can be trusted
* Can be operated
* Can continue delivering value over time

---

# 2. How Do You Translate A Business Problem Into An ML Problem?

## Interview Answer

One of the most important responsibilities of a Senior Data Scientist is translating vague business problems into well-defined machine learning problems.

I typically follow this framework:

### Business Problem

Example:

```text
Customers are leaving and revenue is declining.
```

---

### Business Objective

Convert the problem into a measurable objective.

Example:

```text
Reduce customer churn by 10%.
```

---

### Decision To Support

Identify what decision the model will influence.

Example:

```text
Which customers should receive retention outreach?
```

---

### ML Formulation

Convert the business problem into a machine learning problem.

Examples:

| Business Problem      | ML Problem            |
| --------------------- | --------------------- |
| Churn                 | Binary Classification |
| Credit Risk           | Binary Classification |
| Demand Forecasting    | Regression            |
| Customer Segmentation | Clustering            |
| Recommendation        | Ranking               |

---

### Define Labels

Example:

```text
Churn = Customer inactive for 90 days
```

Poor label definitions often create poor models.

---

### Define Evaluation Metrics

Metrics must align with business objectives.

For churn:

* Recall
* Retention Rate
* Incremental Revenue

not just Accuracy.

---

## Enterprise Perspective

The hardest part of many ML projects is not modeling.

It is agreeing on:

* Definitions
* Labels
* Success criteria

before modeling begins.

---

## Common Follow-Up Questions

### What if the business problem is ambiguous?

I spend time refining requirements before building anything.

Ambiguity early becomes rework later.

### What if stakeholders disagree?

I facilitate alignment around measurable outcomes.

---

## Senior DS Insight

The quality of problem framing often matters more than the quality of the algorithm.

Many failed ML projects are actually poorly framed business problems.

---

# 3. How Do You Define Success Metrics?

## Interview Answer

I define success metrics based on business outcomes, not algorithm preferences.

My framework:

### Business Metric

What outcome are we trying to improve?

Examples:

* Revenue
* Retention
* Fraud Losses
* Customer Satisfaction
* Conversion Rate

---

### ML Metric

How do we measure model quality?

Examples:

* Precision
* Recall
* F1
* ROC-AUC
* MAE

---

### Operational Metric

How do we measure system reliability?

Examples:

* Latency
* Uptime
* Prediction Coverage

---

### Responsible AI Metric

When applicable:

* Fairness
* Stability
* Explainability

---

## Example

Customer Churn Model:

Business Metric:

```text
Retention Revenue
```

ML Metric:

```text
Recall
```

Operational Metric:

```text
Scoring Latency
```

---

## Enterprise Perspective

A common mistake is optimizing for ROC-AUC while ignoring business outcomes.

A model can improve AUC and still fail to create business value.

---

## Senior DS Insight

Success metrics should connect model performance to business outcomes.

Otherwise optimization becomes disconnected from impact.

---

# 4. How Do You Prioritize ML Opportunities?

## Interview Answer

Not every problem should be solved first.

I prioritize opportunities using four dimensions.

### Business Value

Questions:

* Revenue impact?
* Cost reduction?
* Risk reduction?
* Customer impact?

---

### Feasibility

Questions:

* Is data available?
* Are labels available?
* Is the problem solvable?

---

### Time To Value

Questions:

* How quickly can value be realized?
* How complex is implementation?

---

### Risk

Questions:

* Regulatory risk?
* Fairness concerns?
* Operational risk?

---

## Example Framework

| Opportunity               | Value   | Feasibility | Priority |
| ------------------------- | ------- | ----------- | -------- |
| Churn Model               | High    | High        | High     |
| Recommendation Engine     | High    | Medium      | Medium   |
| New Deep Learning Project | Unknown | Low         | Low      |

---

## Enterprise Perspective

I prefer projects that deliver measurable value quickly rather than highly sophisticated projects with uncertain outcomes.

---

## Senior DS Insight

The best project is not always the most technically interesting project.

It is the project that creates the most value per unit effort.

---

# 5. How Do You Estimate Business Impact Before Building A Model?

## Interview Answer

Before investing in model development, I estimate potential business impact.

My framework:

### Step 1: Quantify The Problem

Example:

```text
100,000 customers

10% annual churn

10,000 churned customers
```

---

### Step 2: Estimate Addressable Opportunity

Example:

```text
If intervention reaches 5,000 high-risk customers
```

---

### Step 3: Estimate Intervention Effectiveness

Example:

```text
20% reduction in churn among targeted customers
```

---

### Step 4: Estimate Financial Impact

Example:

```text
1,000 customers retained

Average annual value = $500

Estimated impact = $500,000
```

---

### Step 5: Compare Against Cost

Include:

* Development cost
* Infrastructure cost
* Operational cost
* Maintenance cost

---

## Enterprise Perspective

Business impact estimates are directional, not perfect.

Their purpose is helping prioritize investments.

---

## Common Follow-Up Questions

### What if impact is uncertain?

I provide scenarios:

* Conservative
* Expected
* Optimistic

rather than a single estimate.

---

## Senior DS Insight

Senior Data Scientists are expected to think like investors.

Every project consumes resources.

The goal is maximizing return on those resources.

---

# 04_Senior_DS_Playbook.md

# Section 1: Business & Problem Framing (Continued)

---

# 6. What Questions Do You Ask Stakeholders Before Starting A Project?

## Interview Answer

One of the biggest reasons ML projects fail is unclear expectations.

Before touching the data, I spend time understanding the problem from the stakeholder's perspective.

My goal is to understand:

* The business problem
* The decision being supported
* The expected outcome
* Constraints and risks

---

## Business Questions

### What problem are we trying to solve?

Example:

Instead of:

```text
Build a churn model
```

I want to understand:

```text
Customer retention rates are declining and we want to proactively identify at-risk customers.
```

---

### Why is this problem important?

Questions:

* Revenue impact?
* Cost impact?
* Customer experience impact?
* Regulatory impact?

---

### What action will be taken?

This is one of the most important questions.

Example:

If a customer is predicted to churn:

* Retention offer?
* Customer outreach?
* Product intervention?

A prediction without an action plan has limited value.

---

### How is the problem solved today?

Questions:

* Existing business rules?
* Manual processes?
* SME judgment?

Current solutions often become useful baselines.

---

### What does success look like?

Examples:

* Increased retention
* Reduced fraud losses
* Improved forecast accuracy
* Reduced operational costs

---

### What constraints exist?

Examples:

* Latency requirements
* Explainability requirements
* Budget constraints
* Regulatory requirements

---

## Enterprise Perspective

I often discover that the original request is not the real problem.

A stakeholder may ask for a prediction model when the underlying issue is actually poor data quality or inefficient business processes.

---

## Common Follow-Up Questions

### What if stakeholders cannot clearly define success?

I facilitate discussions until measurable success criteria are established.

Without this alignment, projects often struggle during deployment.

---

## Senior DS Insight

The earlier ambiguity is identified, the cheaper it is to resolve.

---

# 7. How Do You Handle Ambiguous Requirements?

## Interview Answer

Ambiguity is common in senior-level projects.

Rather than waiting for perfect requirements, I focus on reducing uncertainty systematically.

---

## Step 1: Identify What Is Unclear

Common areas:

* Business objective
* Success metrics
* Labels
* Constraints
* Stakeholder expectations

---

## Step 2: Convert Assumptions Into Questions

Example:

Instead of assuming:

```text
Churn means cancellation
```

I ask:

```text
How does the business define churn?
```

---

## Step 3: Create Candidate Definitions

Example:

Possible churn definitions:

* Cancellation
* Inactivity for 30 days
* Inactivity for 90 days

Review options with stakeholders.

---

## Step 4: Build Iteratively

I prefer:

```text
Small Prototype
↓
Feedback
↓
Refinement
↓
Production
```

instead of:

```text
Months Of Development
↓
Surprise Stakeholders
```

---

## Enterprise Perspective

Most ambiguity cannot be solved through modeling.

It is solved through communication.

---

## Common Follow-Up Questions

### What if stakeholders disagree?

I focus discussions on:

* Business objectives
* Tradeoffs
* Measurable outcomes

rather than opinions.

---

## Senior DS Insight

Ambiguity is normal.

The skill is not avoiding ambiguity.

The skill is reducing it efficiently.

---

# 8. How Do You Decide Whether ML Is Even Needed?

## Interview Answer

One of the most important questions I ask is:

> Do we actually need machine learning?

Not every business problem requires ML.

---

## Situations Where ML May Not Be Needed

### Simple Business Rules Work

Example:

```text
If account balance < threshold
then trigger alert
```

A rule may be sufficient.

---

### Low Decision Volume

If only a few decisions occur per month:

* Manual review may be better
* Operational complexity may outweigh benefits

---

### No Actionable Outcome

If predictions do not drive decisions:

ML may provide little value.

---

### Lack Of Reliable Data

If:

* Data is unavailable
* Labels are unavailable
* Outcomes cannot be measured

ML may not be feasible.

---

## Situations Where ML Is Valuable

### Complex Decision Making

Examples:

* Fraud Detection
* Recommendation Systems
* Churn Prediction

---

### Large Scale Decisions

Examples:

* Millions of transactions
* Millions of customers
* Large operational workloads

---

### Pattern Recognition

When business rules cannot easily capture the underlying relationships.

---

## Enterprise Perspective

I have seen organizations build ML solutions where simple business rules would have delivered most of the value at a fraction of the cost.

---

## Senior DS Insight

The best ML solution is not always ML.

The best solution is the one that creates value reliably and efficiently.

---

# 9. What Makes A Good Baseline Solution?

## Interview Answer

A baseline provides a reference point against which all future improvements are measured.

Without a baseline, it is difficult to determine whether a model is actually adding value.

---

## Characteristics Of A Good Baseline

### Simple

Examples:

* Historical Average
* Logistic Regression
* Linear Regression
* Business Rules

---

### Easy To Explain

Stakeholders should understand:

* How it works
* Why it makes predictions

---

### Easy To Reproduce

Results should be stable and repeatable.

---

### Relevant To The Business Problem

Examples:

Forecasting:

```text
Use previous month's average
```

Classification:

```text
Predict majority class
```

---

## Why Baselines Matter

Baselines answer:

```text
Is the sophisticated model actually better?
```

Many teams skip this step.

---

## Enterprise Perspective

I've seen complex models outperform baselines by only 1–2%, while requiring significantly more maintenance and infrastructure.

---

## Common Follow-Up Questions

### What if the baseline performs well?

Then I evaluate whether additional complexity is justified.

---

## Senior DS Insight

A model should not be compared against perfection.

It should be compared against the current decision-making process.

---

# 10. When Is A Simple Solution Better Than ML?

## Interview Answer

A simple solution is often preferable when it provides sufficient value with lower complexity and risk.

---

## When Simplicity Wins

### Explainability Is Critical

Examples:

* High-risk decisions
* Regulated environments
* Executive decision support

Simple models are easier to justify.

---

### Limited Data

Complex models may overfit.

Simple models often generalize better.

---

### Operational Constraints

Examples:

* Low latency requirements
* Limited infrastructure
* Small teams

---

### Marginal Performance Gains

Example:

```text
Logistic Regression = 88% Accuracy

XGBoost = 89% Accuracy
```

If operational costs increase significantly, the additional complexity may not be worthwhile.

---

### Stakeholder Adoption

A slightly less accurate model that stakeholders trust may create more business value than a highly complex model that nobody uses.

---

## Enterprise Perspective

The objective is not maximizing model sophistication.

The objective is maximizing business value.

---

## Common Follow-Up Questions

### When would you choose Logistic Regression over XGBoost?

If:

* Explainability matters
* Performance differences are small
* Operational simplicity is important

---

## Senior DS Insight

Complexity is a cost.

Every additional layer of complexity should justify itself through measurable value.

Many successful ML systems are successful because they are simple, reliable, and trusted.


