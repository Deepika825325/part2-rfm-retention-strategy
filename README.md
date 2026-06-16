# D2C Customer Churn Intelligence

## Part 2: RFM Segmentation & Retention Strategy

---

## Objective

The objective of this project is to identify customer groups requiring different retention interventions before deploying a machine learning churn prediction model.

Customers were segmented using RFM (Recency, Frequency, Monetary) analysis and enriched with seven behavioral and support-related signals to develop actionable retention strategies and campaign prioritization recommendations.

This repository is fully self-contained and can be evaluated independently without requiring any other project repository.

---

## Business Problem

Customer retention is significantly more cost-effective than customer acquisition for Direct-to-Consumer (D2C) businesses.

Before building predictive churn models, organizations need an interpretable framework to:

* Identify valuable customer groups
* Understand behavioral patterns
* Detect early churn risk
* Prioritize retention investments
* Allocate limited campaign budgets efficiently

This project combines transaction history, customer engagement data, support interactions, campaign history, and purchasing behavior to create meaningful customer segments and recommend targeted retention actions.

---

## Dataset

The analysis uses the datasets provided in the assessment package.

| Dataset                  | Description                     |   Rows |
| ------------------------ | ------------------------------- | -----: |
| customers.csv            | Customer profile information    |  2,400 |
| orders.csv               | Customer transactions           | 10,009 |
| support_tickets.csv      | Customer support interactions   |  1,921 |
| web_events_snapshot.csv  | Website activity and engagement |  2,400 |
| intervention_history.csv | Historical campaign information |  2,400 |
| churn_labels.csv         | Observed churn outcomes         |  2,400 |

**Snapshot Date:** `2025-09-30`

All feature engineering and segmentation decisions were evaluated relative to this snapshot date.

---

## Methodology

### 1. Data Preparation

* Loaded and validated all six datasets
* Converted date fields to datetime format
* Handled missing values (`loyalty_tier` → "Not Enrolled", `skin_type` → "Unknown")
* Validated customer coverage across all datasets
* Removed **1,872 post-snapshot transactions** to prevent target leakage
* Confirmed **0 customers with zero pre-snapshot orders** affected by left-join strategy

---

### 2. RFM Feature Engineering

RFM features were calculated using only pre-snapshot orders (8,137 transactions).

| Feature  | Definition                                             |
| -------- | ------------------------------------------------------ |
| Recency  | Days since customer's last purchase before snapshot date |
| Frequency | Total number of purchases before snapshot date        |
| Monetary | Total gross spend (INR) before snapshot date           |

#### RFM Scoring

Customers were assigned quintile-based scores from 1–5.

| Score | Interpretation        |
| ----- | --------------------- |
| R = 5 | Most recent           |
| F = 5 | Highest frequency     |
| M = 5 | Highest spend         |

Frequency tie-breaking used `rank(method="first")` to ensure consistent quintile assignment.

Score distribution was validated — all quintiles contain approximately equal customer counts, confirming the scoring is well-distributed across the customer base.

---

### 3. Additional Behavioral Features

Seven behavioral and support-related features were engineered to complement RFM analysis.

| Feature           | Source                   | Purpose                          |
| ----------------- | ------------------------ | -------------------------------- |
| return_rate       | orders.csv               | Product return behavior          |
| avg_discount      | orders.csv               | Discount dependency              |
| category_diversity | orders.csv              | Breadth of purchasing behavior   |
| ticket_count      | support_tickets.csv      | Support interaction volume       |
| avg_sentiment     | support_tickets.csv      | Customer satisfaction signal     |
| sessions_30d      | web_events_snapshot.csv  | Recent website engagement        |
| campaign_engaged  | intervention_history.csv | Campaign interaction history     |

`campaign_engaged` is a binary feature (1 = received any campaign, 0 = no campaign received) derived from `last_campaign_received`. It is used in the Dormant segment rule to identify customers disengaged from both the product and brand communications simultaneously.

---

### 4. Customer Segmentation

Ten customer segments were created using RFM scores and behavioral signals.

| Segment             | Key Criteria                                                          |
| ------------------- | --------------------------------------------------------------------- |
| Champions           | R ≥ 4, F ≥ 4, M ≥ 4                                                   |
| Loyal Customers     | R ≥ 3, F ≥ 4                                                          |
| Potential Loyalists | R ≥ 4, F ≥ 2                                                          |
| New Customers       | R ≥ 4, F = 1                                                          |
| High Value Unhappy  | M ≥ 4, ticket_count ≥ 2, avg_sentiment < 0                           |
| Discount Sensitive  | avg_discount ≥ 35%                                                    |
| At Risk             | R ≤ 2, M ≥ 3                                                          |
| Dormant             | R = 1, F ≤ 2, sessions_30d = 0, campaign_engaged = 0                 |
| Promising           | R = 3, F ≥ 2                                                          |
| Regular Customers   | Moderate RFM characteristics without dominant signals (residual)      |

#### Segment Rule Priority

Rules are evaluated in business-priority order. Customer value and dissatisfaction indicators take precedence over broader behavioral classifications.

#### At-Risk Threshold Sensitivity Analysis

The At-Risk segment boundary was tested across multiple thresholds:

| Rule          | Customers |
| ------------- | --------: |
| R_score ≤ 1   |       278 |
| R_score ≤ 2   |       570 |
| R_score ≤ 3   |       882 |

`R_score ≤ 2` was selected to balance coverage and segment precision without excessive overlap with the Promising segment.

---

## Churn Validation

Segment quality was validated against observed churn outcomes from `churn_labels.csv`.

| Segment             | Churn Behavior                    |
| ------------------- | --------------------------------- |
| Champions           | Lowest churn rate                 |
| Loyal Customers     | Strong retention                  |
| Potential Loyalists | Moderate churn                    |
| High Value Unhappy  | Elevated churn despite high spend |
| At Risk             | High churn probability            |
| Dormant             | Highest observed churn            |

Churn labels were used **only for validation** — not for segment creation — to prevent target leakage.

---

## Segment Distribution

Actual segment assignments from `segments.csv`:

| Segment             | Customers | % of Base |
| ------------------- | --------: | --------: |
| At Risk             |       389 |    16.21% |
| Potential Loyalists |       364 |    15.17% |
| Champions           |       344 |    14.33% |
| Discount Sensitive  |       269 |    11.21% |
| Loyal Customers     |       256 |    10.67% |
| New Customers       |       208 |     8.67% |
| Promising           |       138 |     5.75% |
| High Value Unhappy  |       112 |     4.67% |
| Regular Customers   |        59 |     2.46% |
| Dormant             |        21 |     0.88% |
| **Total**           | **2,400** |  **100%** |

---

## Campaign Budget Prioritization

### Budget Assumption

A retention budget of **₹500,000** is assumed.

### Prioritization Method

**Priority Score = Customer Count × Average Monetary Value × Churn Rate**

### Recommended Allocation

| Priority | Segment             | Allocation | Budget (₹) |
| -------- | ------------------- | ---------: | ---------: |
| 1        | High Value Unhappy  |        30% |    150,000 |
| 2        | At Risk             |        25% |    125,000 |
| 3        | Loyal Customers     |        20% |    100,000 |
| 4        | Potential Loyalists |        15% |     75,000 |
| 5        | Champions           |        10% |     50,000 |

Dormant, Regular Customers, and New Customers receive lower-cost automated campaigns.

### Measurement Framework

To isolate campaign-driven retention from organic behaviour, **10–15% of customers in each segment are held out as a non-contact control group**.

```
Campaign Lift = Purchase Rate (Treatment) − Purchase Rate (Control)
```

A positive lift confirms the campaign generated incremental retention. Full details are documented in `retention_strategy.md`.

---

## Manual Review Framework

Ten customer records were reviewed manually where the automated segment assignment was ambiguous or the standard segment playbook was inappropriate given the customer's full profile.

Case types reviewed:

| Conflict Type                                        | Cases     |
| ---------------------------------------------------- | --------- |
| Good purchase behavior + negative support experience | 2, 4, 5, 6 |
| Loyalty signal vs discount dependency                | 1, 7      |
| Segment rule mismatch with customer value profile    | 3, 8, 10  |
| High tolerance for friction masking churn risk       | 9         |

Full analysis is documented in `manual_review_cases.md`.

---

## Results Snapshot

| Metric                        | Value              |
| ----------------------------- | ------------------ |
| Customers Segmented           | 2,400              |
| Pre-Snapshot Orders Used      | 8,137              |
| Post-Snapshot Orders Excluded | 1,872              |
| Segments Created              | 10                 |
| Non-RFM Signals Used          | 7                  |
| Manual Review Cases           | 10                 |
| Highest Churn Segment         | Dormant            |
| Highest Revenue Risk Segment  | High Value Unhappy |

---

## Repository Structure

```text
part2-rfm-retention-strategy/
│
├── notebooks/
│   └── rfm_segmentation.ipynb
│
├── outputs/
│   ├── charts/
│   └── tables/
│
├── segments.csv
├── retention_strategy.md
├── manual_review_cases.md
├── requirements.txt
├── README.md
└── .gitignore
```

---

## Deliverables

| File                    | Purpose                                        |
| ----------------------- | ---------------------------------------------- |
| rfm_segmentation.ipynb  | Full analysis and segmentation workflow        |
| segments.csv            | Customer segment assignments with key features |
| retention_strategy.md   | Segment actions, budget prioritization, holdout measurement framework |
| manual_review_cases.md  | Dataset-backed manual review of 10 ambiguous cases |
| requirements.txt        | Reproducible environment configuration         |

---

## How to Run

### Clone Repository

```bash
git clone https://github.com/Deepika825325/part2-rfm-retention-strategy.git
cd part2-rfm-retention-strategy
```

### Crea

```bash
python -m venv .venv
```

### Activate Environment

**Windows**
```bash
.venv\Scripts\activate
```

**Linux / macOS**
```bash
source .venv/bin/activate
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Launch Notebook

```bash
jupyter notebook
```

Open `notebooks/rfm_segmentation.ipynb` and run all cells from top to bottom.

---

## Technologies Used

| Technology       | Purpose                                        |
| ---------------- | ---------------------------------------------- |
| Python 3.11      | Data analysis and feature engineering          |
| Pandas           | Data loading, aggregation, segmentation        |
| NumPy            | Numerical computations                         |
| Matplotlib       | Static visualization generation                |
| Seaborn          | Statistical and business-oriented charts       |
| Scikit-learn     | Quintile scoring utilities                     |
| Jupyter Notebook | Interactive exploratory analysis               |

---

## Limitations

* Rule-based segmentation relies on business-defined thresholds that may require periodic recalibration.
* Segmentation reflects customer state at a single snapshot date (2025-09-30).
* Segment-level relationships are associative rather than causal.
* `avg_sentiment` is imputed as 0 for non-ticket customers — this may underestimate dissatisfaction for customers who churned silently without raising a ticket.
* Churn labels were used only for validation and not for segment creation.

---

## Conclusion

RFM analysis combined with seven behavioral and support-related signals successfully identified ten customer groups with distinct churn risks, engagement levels, and revenue profiles.

Champions and Loyal Customers demonstrated the strongest retention and revenue contribution, while High Value Unhappy, At Risk, and Dormant customers represented the highest retention priorities.

The resulting framework provides an interpretable, actionable, and business-focused foundation for customer retention decision-making before deploying predictive machine learning models.