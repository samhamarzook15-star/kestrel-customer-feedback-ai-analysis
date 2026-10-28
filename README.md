# Kestrel Motor Group — Customer Feedback Analysis

## 1. Executive summary

This project consolidates and analyses 7,086 customer-feedback records to identify recurring service issues, compare dealership and department performance, examine rating trends, and recommend improvement priorities.

The numeric-rating analysis uses 6,489 records after excluding Kestrel Ringwood, whose rating standardisation is inconsistent, and Kestrel Tamworth, which has no usable numeric ratings. Repair quality, booking and appointments, waiting time, and communication are priority areas for investigation. Cleanliness and facilities also has a low average rating, but the sample is small. Staff behaviour is a relative strength among the selected themes.

## Business Problem

Kestrel Motor Group has a large customer-feedback dataset, but inconsistent ratings, missing information, and varied customer comments make it difficult to identify the most important service issues and decide where improvements should be prioritised.

This project uses data analysis and AI-assisted techniques to address three key business questions:

1. **What is driving negative feedback?** Identify the main complaint themes and compare customer experiences across dealerships and departments.

2. **What has changed over time?** Analyse customer-rating trends to identify declines, improvements, and patterns that warrant further investigation.

3. **Where should the business focus first, and what might it be worth?** Prioritise improvement opportunities using feedback frequency, rating severity, and business relevance, then estimate potential financial significance using illustrative scenarios rather than unsupported predictions.

## 2. Approach and technology choices

Python and pandas were used to consolidate, clean, validate, and analyse feedback data. Matplotlib was used for visualisation, and the Jupyter Notebook documents the workflow. A local Ollama-hosted Qwen2.5:3b model was tested on a small sample to explore structured extraction of sentiment, positive aspects, issues, and explanations.

A VADER sentiment baseline was compared with manual labels on one 30-comment sample. The notebook records agreement on 18 of 30 comments (60%). Agreement among the 13 manually labelled negative comments was 5 of 13 (38.5%). The separate older 40-comment audit has been removed from this submission copy to avoid conflicting validation figures. This small sample is not a reliable estimate of overall model performance, but it demonstrates that the baseline can miss negative feedback. For example, an emphatic complaint about repeatedly having to chase for updates was labelled Positive by VADER. Sentiment labels are therefore not used as a headline finding in the visual summary.

## 3. Data preparation and quality

The consolidated dataset contains **7,086 records**. Of these, **1,725 records have missing comments**.

| Check / issue | Result | Treatment |
|---|---|---|
| Consolidated feedback | 7,086 records | Used as the starting point for analysis. |
| Numeric-rating analysis | 6,489 records | Numeric ratings from 1 to 5 retained after excluding Ringwood and Tamworth. |
| Ringwood rating data | Inconsistent rating standardisation | Excluded from numeric-rating analysis pending validation; no guessed ratings assigned. |
| Tamworth rating data | 143 records without usable numeric ratings | Excluded from numeric-rating analysis; text categories were not converted into guessed numeric ratings. |
| Missing comments | 1,725 records | Retained as missing; no text was fabricated. |
| Missing/unparseable dates | 10 records | Excluded from monthly trend calculations. |
| Exact duplicate rows | 47 rows | Retained; no deduplication was applied to the final consolidated dataset or visual summary. |
| Dealership-to-revenue matching | Three labels unmatched | Unmapped - KMG-IPS, Unmapped - HUNTER, and Unmapped - North Queensland were excluded from analyses requiring a reliable revenue match. |
| Department labels | Some labels ambiguous | Kept separate where their meanings could not be established confidently. |

The monthly trend covers October 2025 through September 2026 and includes **6,473 valid ratings**. This is 16 fewer than the 6,489 rating-analysis records: 10 have missing or unparseable dates, and six valid-rated records fall after the reporting window. Three are dated after 28 October 2026 (19 November, 26 November, and 1 December 2026) and should be checked as possible date errors.

### Privacy

The revised visual summary workbook contains aggregated analysis only and does not include customer-level comments. The separate CSV export has been screened for email-like text, likely Australian phone numbers, and registration values explicitly labelled with `rego`. This is limited, pattern-based screening, **not proof of complete anonymisation**. Names, addresses, unlabelled vehicle registration plates, and other identifiers may remain. Do not publish the raw source files or the CSV in a public repository without appropriate authorisation and further review.

## 4. Business findings

### 4.1 Main feedback themes

Communication was the most frequently tagged theme, with **961 tagged records** in the rating-analysis dataset. Average ratings by selected theme were:

| Theme | Average rating | Tagged records |
|---|---:|---:|
| Repair quality | 2.53/5 | 387 |
| Cleanliness and facilities | 2.59/5 | 56 |
| Booking and appointments | 2.61/5 | 250 |
| Waiting time | 2.77/5 | 511 |
| Communication | 2.84/5 | 961 |
| Parts availability | 3.04/5 | 379 |
| Pricing and billing | 3.37/5 | 558 |
| Staff behaviour | 4.02/5 | 531 |

Theme tags can overlap: one comment may be assigned multiple themes. Counts therefore represent theme-tag occurrences, not mutually exclusive groups of customers.

### 4.2 Department comparison

Service had an average rating of approximately **3.53/5**, with a **28.0% negative-rating rate** in the filtered rating-analysis dataset. Negative ratings are defined as numeric ratings of **2 or below**.

Department comparisons should be interpreted alongside sample sizes, label ambiguity, and data coverage. Uncertain department categories were not merged without reliable evidence.

### 4.3 Dealership comparison

The five lower-rated dealerships with matched service data used in the illustrative revenue scenario were:

- **Kestrel Parramatta:** 3.59/5 (479 feedback records).
- **Kestrel Box Hill:** 3.63/5 (309 feedback records).
- **Kestrel Dandenong:** 3.64/5 (484 feedback records).
- **Kestrel Southport:** 3.64/5 (250 feedback records).
- **Kestrel Essendon:** 3.64/5 (346 feedback records).

Their combined service revenue was approximately **A$19.66 million**. These results identify locations for further investigation; they do not establish why ratings differ. Three dealership labels could not be matched reliably to revenue data: Unmapped - KMG-IPS, Unmapped - HUNTER, and Unmapped - North Queensland.

## 5. Changes over time

The average rating declined from **3.95/5 in December 2025** to **3.55/5 in August 2026**, before recovering to **3.73/5 in September 2026**.

The trend warrants investigation, particularly in relation to repair quality, appointment handling, waiting times, and communication. It does not establish the cause. Further work should compare theme-level and dealership-level patterns with operational records before attributing changes to specific factors.

## 6. Recommendations

Priorities combine rating severity, frequency, sample size, and practical actionability; they are not ranked by average rating alone. Cleanliness and facilities has a low mean but only 56 tagged records, so it should be validated before broad changes are made.

| Priority | Area | Recommended action | Suggested success measures |
|---:|---|---|---|
| 1 | Repair quality | Review repeat repairs, quality checks, and unresolved repair complaints. | Repair-quality rating and repeat-repair rate. |
| 2 | Booking and appointments | Investigate appointment availability, booking accuracy, and missed appointments. | Booking rating and missed-appointment rate. |
| 3 | Waiting time | Monitor delays and improve proactive customer updates. | Waiting-time rating and on-time completion rate. |
| 4 | Communication | Set clear expectations for costs, repair progress, and follow-up. | Communication rating and customer-update compliance. |
| 5 | Cleanliness and facilities | Investigate the low average rating while accounting for the smaller sample size. | Cleanliness rating and inspection results. |
| 6 | Staff behaviour | Identify and share practices associated with stronger customer feedback. | Staff-behaviour rating and positive-feedback frequency. |

Establish baseline measures before introducing changes, pilot improvements at selected dealerships, and review results after an agreed period. This helps distinguish genuine improvement from ordinary fluctuations.

## 7. Illustrative business value

The combined service revenue of the five dealerships listed in Section 4.3 was approximately **A$19.66 million**.

| Illustrative percentage | Approximate value |
|---:|---:|
| 0.5% | A$98,281 |
| 1% | A$196,563 |
| 2% | A$393,126 |

These are hypothetical scenarios, **not forecasts, savings, or proven benefits**. They do not demonstrate that improving feedback would retain any particular percentage of revenue. Actual benefits require evidence about customer retention, operational costs, and business outcomes.

## 8. Exploratory AI experiment

A small exploratory pilot used a locally run Ollama-hosted Qwen2.5:3b model to structure selected comments into sentiment, positive aspects, issues, and explanations. The experiment exposed several limitations:

- Sarcastic feedback was sometimes classified incorrectly.
- One response inferred an unresolved part-replacement issue that the comment did not establish.
- Some responses omitted relevant positive details.
- Some outputs required human judgement even when they appeared plausible.

The VADER baseline validation in this submission agreed with manual labels on 18 of 30 comments (60%) overall and on 5 of 13 manually labelled negative comments (38.5%). Because the sample is small and manually labelled, these figures should be treated as a limited spot-check, not a robust accuracy estimate. Neither approach should be used for operational decisions without human review and further validation.

## 9. Limitations

- Ringwood rating data require validation, and Tamworth has no usable numeric ratings; both were excluded from numeric-rating analysis.
- Ten records have missing or unparseable dates, and six valid-rated records fall after the monthly reporting window; three have dates later than 28 October 2026 and should be checked as possible date errors.
- Forty-seven exact duplicate rows were retained; their effect has not been removed from the reported totals.
- Three dealership labels could not be matched reliably to revenue data.
- Ambiguous department labels require further validation before categories are combined.
- Theme tags overlap, so theme counts are not mutually exclusive.
- Average ratings may be affected by sample sizes and data coverage.
- Associations between feedback, dealership performance, and revenue do not establish causation.
- Illustrative revenue scenarios are not predictions of financial benefits.
- The AI experiments were exploratory and have not been validated as reliable classifiers.
- Pattern-based privacy screening does not prove complete anonymisation.

## 10. Reproducibility

The notebook documents the preparation and analysis workflow. To reproduce the analysis, place `PS_Data_AI_Assignment.zip` in the notebook folder or your Downloads folder, install the required Python packages, and run the notebook from the beginning. The exploratory AI cells additionally require Ollama to be installed and running locally, with the `qwen2.5:3b` model available.

The notebook includes `%pip install` cells for `vaderSentiment` and `ollama`; the core analysis also uses pandas, matplotlib, and scikit-learn. If an AI call fails because the local service or model is unavailable, the AI experiment has not completed and its outputs should not be treated as validated results.

## Tools and technologies

- **Python:** Data preparation and analysis.
- **Pandas:** Data cleaning, consolidation, and aggregation.
- **Matplotlib:** Data visualisation.
- **Jupyter Notebook:** Interactive analysis and documentation.
- **VADER Sentiment:** Exploratory rule-based sentiment baseline, with limited manual validation.
- **Ollama with Qwen2.5:3b:** Exploratory local AI experiment for structuring customer comments.

## Public Repository Files

- `Kestrel_Data_AI_Challenge_Submission_REVISED.ipynb` — Jupyter Notebook documenting data preparation, analysis, visualisations, recommendations, and the exploratory AI experiment. Saved outputs are cleared; run the notebook from the beginning in the intended environment to reproduce and validate the results.

- `Kestrel_Customer_Feedback_Visual_Summary_REVISED.xlsx` — Aggregated dashboard, feedback-theme analysis, chart data, and data-quality notes.

- `Kestrel_Customer_Feedback_Detail.xlsx` — Customer feedback dataset supplied for the assessment, containing dealership, date, department, customer rating, feedback comments, sentiment, and feedback themes.

- `README.md` — Project overview, business questions, key findings, recommendations, AI evaluation, limitations, and reproducibility instructions.

### Dataset and Privacy Note

The customer feedback dataset was supplied as synthetic assessment data and is analysed as a real-world business scenario. Pattern-based screening may remove some identifying details, but it does not guarantee complete anonymisation. The analysis also acknowledges data-quality limitations, including missing information, inconsistent ratings, and potentially invalid dates.
