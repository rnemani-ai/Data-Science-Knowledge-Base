# 05_Senior_DS_Story_Bank.md

# Story 01 - Found A Data Quality Issue

## Primary Competencies

- Data Quality
- Root Cause Analysis
- Problem Solving
- Cross-functional Collaboration

---

## Interview Questions This Story Answers

- Tell me about a time you found a data quality issue.
- Describe a challenging data problem.
- How do you validate data before building AI solutions?
- Tell me about a time you prevented a major issue.

---

## Situation

While working on an Enterprise Document Intelligence solution for a **Global CPG Company**, our goal was to automate extraction of key information from supplier claims, trade agreements, and invoices using OCR and Large Language Models.

The documents came from multiple suppliers and retailers and varied significantly in quality. Some were digitally generated PDFs, while others were scanned copies, handwritten forms, or multi-page documents containing nested tables.

During early testing, we noticed that extraction accuracy was inconsistent across document types even though the OCR pipeline appeared to be functioning correctly.

---

## Task

My responsibility was to identify the root cause of the inconsistent extraction quality before the solution was deployed to business users.

Since downstream financial validation depended entirely on accurate extraction, even small errors in fields such as invoice numbers, quantities, or effective dates could lead to incorrect claim processing.

---

## Actions

Rather than immediately modifying prompts or changing models, I first validated the incoming data.

I created a profiling script that analyzed document characteristics including:

- OCR confidence scores
- Missing pages
- Image resolution
- Rotation angles
- Presence of handwritten text
- Table density
- Blank or duplicated pages

This analysis revealed several data quality issues:

- Some scanned documents had very low OCR confidence.
- Certain PDFs contained duplicate pages.
- Multiple invoices were uploaded upside down.
- Some documents were incomplete because the final page was missing.
- Several supplier templates used inconsistent field names for the same business concept.

Instead of forcing the LLM to process poor-quality input, I introduced a validation layer before extraction.

The pipeline now:

- Checked OCR confidence.
- Verified page completeness.
- Detected rotated pages.
- Standardized common field names.
- Flagged documents failing quality checks for manual review.

This ensured only reliable inputs entered the LLM pipeline.

---

## Result

After implementing these validation checks:

- Extraction accuracy improved significantly.
- Manual rework reduced considerably.
- Business users gained confidence because poor-quality documents were identified upfront rather than producing unreliable outputs.
- The validation layer became a reusable component for future document processing pipelines.

---

## Business Impact

Rather than trying to solve every problem with AI, we improved overall system reliability by improving input quality.

This reduced downstream processing errors and contributed to reducing document processing time from approximately **20 minutes to under 2 minutes**, supporting an estimated annual business value of nearly **$19M**.

---

## Why This Was A Senior DS Contribution

The important realization was that the model wasn't the problem—the data was.

Instead of optimizing prompts prematurely, I stepped back, investigated the full pipeline, identified upstream quality issues, and introduced preventive controls.

This is an example of treating AI systems as end-to-end products rather than isolated models.

---

## What I Learned

One lesson I've carried forward is that improving data quality often delivers a larger return than improving model complexity.

Good models cannot compensate for poor input data, especially in enterprise AI systems.

---

## Possible Follow-up Questions

- How did you measure OCR quality?
- Why didn't you simply retrain the model?
- What thresholds did you use for validation?
- Which data quality issue had the largest impact?
- How did business users react to documents being flagged?

---

# Story 02 - Discovered Data Leakage

## Primary Competencies

- Machine Learning
- Data Leakage Detection
- Model Validation
- Critical Thinking

---

## Interview Questions This Story Answers

- Tell me about a time you found data leakage.
- How do you detect leakage?
- Describe a model that performed suspiciously well.
- Tell me about preventing a production issue.

---

## Situation

In an earlier engagement with a **Large Telecommunications Provider**, we were developing a machine learning solution to detect fraudulent service activations.

The objective was to replace a static rule-based system with a predictive fraud detection model capable of identifying complex fraud patterns while reducing false positives.

During model evaluation, one of our early experiments produced unexpectedly high validation performance.

The model achieved an AUC that seemed unusually good compared to historical rule-based performance.

---

## Task

Rather than celebrating the results, I wanted to verify whether the model had genuinely learned fraud patterns or whether information from the future had unintentionally leaked into the training process.

Since fraud models directly influence operational decisions, deploying a leaked model would have created serious business risk.

---

## Actions

I performed a detailed feature audit.

Instead of looking only at feature importance, I reviewed:

- When each feature became available.
- Whether the feature existed before prediction time.
- How each feature was engineered.
- Whether historical and future events had been mixed.

During this review, I identified that one engineered feature indirectly incorporated information that was only available after account activation.

Although the feature wasn't the target variable itself, it contained future information that would never exist during real-time prediction.

I removed the feature, rebuilt the training pipeline, and revalidated the model using strictly time-aware train-test splits.

I also documented feature availability rules so future feature engineering would follow the same principles.

---

## Result

Model performance became more realistic, but we gained confidence that it would generalize well in production.

More importantly, we avoided deploying a model that would have appeared highly accurate during testing but failed in real-world fraud detection.

---

## Business Impact

Preventing leakage protected the credibility of the project.

It ensured business stakeholders trusted reported performance and reduced the risk of costly production failures caused by overly optimistic validation metrics.

---

## Why This Was A Senior DS Contribution

Senior Data Scientists don't optimize for the highest validation score.

They optimize for models that perform reliably in production.

Recognizing suspiciously good results and investigating them demonstrated engineering judgment rather than simply chasing metrics.

---

## What I Learned

One lesson I've learned is that unusually high model performance should always trigger curiosity rather than excitement.

In enterprise machine learning, realistic performance is often more valuable than impressive validation numbers.

---

## Possible Follow-up Questions

- How did you identify the leakage?
- What types of leakage have you seen?
- How do you prevent leakage in feature engineering?
- Why are time-based splits important?
- What governance practices did you introduce afterward?

# Story 03 - Improved Model Performance

## Primary Competencies

- Machine Learning
- Prompt Engineering
- Experimentation
- Performance Optimization
- Business Thinking

---

## Interview Questions This Story Answers

- Tell me about a time you improved model performance.
- Describe an optimization you made.
- Tell me about an ML model that wasn't performing well.
- How do you improve AI system performance?

---

## Situation

While building an Enterprise Document Intelligence solution for a **Global CPG Company**, our objective was to automatically extract structured information from supplier claims, invoices, and trade agreements.

Although the initial pipeline worked well for clean documents, performance dropped significantly on scanned documents, handwritten notes, and multi-page tables. The LLM occasionally missed fields, extracted incorrect values, or produced inconsistent outputs.

Simply changing to a larger model wasn't an option because of latency and cost constraints.

---

## Task

My goal was to improve extraction accuracy while keeping inference time low and maintaining a cost-effective solution that could scale across thousands of documents every month.

---

## Actions

Rather than assuming the model was the problem, I broke the pipeline into individual components and evaluated each stage independently.

### 1. Improved OCR Routing

Instead of sending every document through the same OCR engine, I introduced a hybrid routing strategy.

- Clean digital PDFs → Open-source OCR
- Complex layouts, handwriting, tables → Azure Document Intelligence

This improved OCR quality while reducing processing costs.

---

### 2. Better Prompt Engineering

I redesigned our prompts by:

- Using few-shot examples
- Grouping related fields together
- Providing explicit extraction instructions
- Asking the model to return structured JSON

Instead of asking the LLM to extract every field at once, we extracted logically related groups such as:

- Product Information
- Pricing
- Dates
- Addresses

This reduced hallucinations and improved consistency.

---

### 3. Overlapping Chunking

Large documents exceeded token limits.

To preserve context, I implemented overlapping chunking with a safety buffer so information split across pages wasn't lost.

For example:

Invoice Number

continued onto next page

still remained available to the model.

---

### 4. Validation Layer

After extraction we added rule-based validation.

Examples:

- UPC length validation
- Date format checks
- Missing mandatory fields
- Numeric range validation

Any suspicious outputs were automatically flagged for manual review.

---

### 5. Temperature Optimization

For deterministic fields such as:

- Invoice Number
- Dates
- Product Codes

we reduced temperature close to zero to improve consistency.

---

## Result

The combined improvements produced significant gains.

- Higher extraction accuracy
- Reduced hallucinations
- More stable outputs across document types
- Lower manual review effort
- Faster document processing

The solution successfully processed highly variable enterprise documents while remaining scalable.

---

## Business Impact

Processing time reduced from approximately **20 minutes to under 2 minutes per document**.

The solution was projected to generate nearly **$19M in annual savings** while improving business confidence in AI-assisted document processing.

---

## Why This Was A Senior DS Contribution

Instead of focusing on a single model, I optimized the complete AI pipeline.

I viewed the solution as an end-to-end system involving OCR quality, prompt engineering, chunking strategy, validation, and business workflows rather than treating the LLM as a black box.

---

## What I Learned

In enterprise AI, the biggest improvements rarely come from changing the model.

They come from improving the surrounding pipeline.

Prompt engineering, preprocessing, validation, and business rules often contribute more than simply upgrading to a larger LLM.

---

## Possible Follow-up Questions

- Why GPT-3.5 instead of GPT-4?
- Why not fine-tune a model?
- How did you reduce hallucinations?
- Why use overlapping chunking?
- Which optimization delivered the biggest improvement?

---

# Story 04 - Engineered A Valuable Feature

## Primary Competencies

- Feature Engineering
- Business Understanding
- Machine Learning
- Domain Knowledge

---

## Interview Questions This Story Answers

- Tell me about a valuable feature you engineered.
- What's the best feature you've created?
- How do you approach feature engineering?
- Give an example where domain knowledge improved a model.

---

## Situation

During a fraud detection project for a **Large Telecommunications Provider**, we were developing a machine learning solution to identify fraudulent service activations.

The existing rule engine relied primarily on simple checks such as whether the activation location matched the expected network location.

Although useful, these rules generated many false positives because legitimate operational scenarios could also trigger mismatches.

---

## Task

My responsibility was to identify behavioral features that better separated fraudulent activity from legitimate customer behavior.

Rather than relying on static business rules, we wanted features that captured how fraudsters behaved over time.

---

## Actions

I worked closely with fraud investigators and domain experts to understand common fraud patterns.

Instead of focusing only on raw fields, we engineered behavioral features.

Some of the most valuable features included:

### CMTS Mismatch Score

Instead of a simple yes/no mismatch flag, we created a feature representing the relationship between intended and actual activation locations.

This provided much richer information than a binary indicator.

---

### Activation Velocity

Rather than counting activations, we calculated:

- Activations within 1 day
- Activations within 7 days
- Activations within 30 days

High activation velocity became a strong fraud indicator.

---

### MAC Address Reuse

We engineered features capturing repeated device usage across multiple customer accounts.

This helped identify potential credential sharing and fraudulent account creation.

---

### Delinquency History

Instead of using only current billing status, we captured historical delinquency patterns and streaks.

Historical behavior proved far more predictive than current status alone.

---

### Cluster-Based Risk

We performed unsupervised clustering to identify groups of similar customer behavior.

The resulting cluster label became an additional feature for our supervised fraud model.

This helped capture behavioral patterns that individual features could not.

---

## Result

These engineered features significantly improved model discrimination.

The final model detected substantially more fraudulent entities than the legacy rule engine while reducing false positives.

More importantly, investigators could understand why accounts were flagged because the features were intuitive and explainable.

---

## Business Impact

The fraud platform moved beyond static rules toward behavioral intelligence.

This enabled earlier fraud detection, reduced manual investigations, and supported millions of dollars in potential savings.

---

## Why This Was A Senior DS Contribution

I wasn't simply creating mathematical transformations.

The strongest features came from combining business knowledge with machine learning.

Understanding how fraud actually occurs allowed us to build features that generalized better than manually crafted rules.

---

## What I Learned

Feature engineering isn't about creating more features.

It's about creating features that capture business behavior.

Good features often outperform more complex algorithms trained on weak inputs.

---

## Possible Follow-up Questions

- Which feature contributed the most?
- How did you measure feature importance?
- How did SHAP help?
- Why not let XGBoost learn everything automatically?
- How did you avoid leakage during feature engineering?

