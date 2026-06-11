# D2C Customer Churn Intelligence

## Part 2: RFM Segmentation & Retention Strategy

---

## Objective

The objective of this project is to identify customer groups requiring different retention interventions before deploying a machine learning churn prediction model.

Customers were segmented using RFM (Recency, Frequency, Monetary) analysis and enriched with behavioral and support-related signals to develop actionable retention strategies and campaign prioritization recommendations.

This repository is fully self-contained and can be evaluated independently without requiring any other project repository.

---

# Business Problem

Customer retention is significantly more cost-effective than customer acquisition for Direct-to-Consumer (D2C) businesses.

Before building predictive churn models, organizations need an interpretable framework to:

* Identify valuable customer groups
* Understand behavioral patterns
* Detect early churn risk
* Prioritize retention investments
* Allocate limited campaign budgets efficiently

This project combines transaction history, customer engagement data, support interactions, and purchasing behavior to create meaningful customer segments and recommend targeted retention actions.

---

# Dataset

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

# Methodology

## 1. Data Preparation

* Loaded and validated all datasets
* Converted date fields to datetime format
* Handled missing values
* Validated customer coverage across datasets
* Removed 1,872 post-snapshot transactions to prevent target leakage

---

## 2. RFM Feature Engineering

RFM features were calculated using only pre-snapshot orders.

### Recency

Number of days since the customer's last purchase.

### Frequency

Total number of purchases before the snapshot date.

### Monetary

Total gross customer spend before the snapshot date.

### RFM Scoring

Customers were assigned quintile-based scores from 1–5.

| Score Type | Interpretation        |
| ---------- | --------------------- |
| R Score    | 5 = most recent       |
| F Score    | 5 = highest frequency |
| M Score    | 5 = highest spend     |

Frequency tie-breaking was performed using:

```python
rank(method="first")
```

to ensure consistent quintile assignment.

---

## 3. Additional Behavioral Features

To improve segmentation quality beyond traditional RFM analysis, six behavioral and support-related features were engineered.

| Feature            | Purpose                        |
| ------------------ | ------------------------------ |
| return_rate        | Product return behavior        |
| avg_discount       | Discount dependency            |
| category_diversity | Breadth of purchasing behavior |
| ticket_count       | Support interaction volume     |
| avg_sentiment      | Customer satisfaction signal   |
| sessions_30d       | Recent website engagement      |

These features complement RFM by capturing engagement, satisfaction, discount sensitivity, and support experience.

---

## 4. Customer Segmentation

Ten customer segments were created using RFM scores and behavioral signals.

| Segment             | Key Criteria                                          |
| ------------------- | ----------------------------------------------------- |
| Champions           | R ≥ 4, F ≥ 4, M ≥ 4                                   |
| Loyal Customers     | R ≥ 3, F ≥ 4                                          |
| Potential Loyalists | R ≥ 4, F ≥ 2                                          |
| New Customers       | R ≥ 4, F = 1                                          |
| High Value Unhappy  | M ≥ 4, ticket_count ≥ 2, negative sentiment           |
| Discount Sensitive  | avg_discount ≥ 35%                                    |
| At Risk             | R ≤ 2 and M ≥ 3                                       |
| Dormant             | R = 1, F ≤ 2, sessions_30d = 0                        |
| Promising           | R = 3 and F ≥ 2                                       |
| Regular Customers   | Moderate RFM characteristics without dominant signals |

### Segment Rule Priority

Customers may satisfy multiple segment conditions simultaneously.

Rules are evaluated in business-priority order, with customer value and dissatisfaction indicators taking precedence over broader behavioral classifications.

---

# Churn Validation

Segment quality was validated using observed churn outcomes.

### Key Findings

| Segment             | Churn Behavior                    |
| ------------------- | --------------------------------- |
| Champions           | Lowest churn rate                 |
| Loyal Customers     | Strong retention                  |
| Potential Loyalists | Moderate churn                    |
| High Value Unhappy  | Elevated churn despite high spend |
| At Risk             | High churn probability            |
| Dormant             | Highest observed churn            |

The validation confirms that the segmentation framework aligns with real customer outcomes and successfully identifies retention-risk groups.

---

# Campaign Budget Prioritization

## Budget Assumption

For planning purposes, a retention budget of **₹500,000** is assumed.

The objective is to maximize revenue protection by prioritizing customer groups with the highest combination of:

* Revenue contribution
* Customer volume
* Churn probability
* Recovery potential

## Prioritization Method

Priority Score:

**Priority Score = Customer Count × Average Monetary Value × Churn Rate**

This approach balances:

* Revenue at risk
* Segment size
* Likelihood of churn

Higher scores indicate greater expected business impact from retention interventions.

---

## Recommended Budget Allocation

| Priority | Segment             | Allocation |
| -------- | ------------------- | ---------: |
| 1        | High Value Unhappy  |        30% |
| 2        | At Risk             |        25% |
| 3        | Loyal Customers     |        20% |
| 4        | Potential Loyalists |        15% |
| 5        | Champions           |        10% |

Dormant, New Customers, and Regular Customers receive lower-cost automated campaigns.

---

# Business Impact

The segmentation framework provides an interpretable retention decision system that can be used before predictive models are deployed.

## Key Findings

* High Value Unhappy customers represent the largest revenue preservation opportunity.
* At Risk customers require immediate win-back intervention.
* Dormant customers show the highest churn risk.
* Potential Loyalists represent the strongest growth opportunity.
* Champions and Loyal Customers generate the most stable revenue streams.

## Expected Benefits

* Increased customer lifetime value
* Reduced customer acquisition dependency
* Improved repeat purchase behavior
* Better allocation of retention budgets
* Stronger customer satisfaction outcomes

---

# Retention Strategy Overview

| Segment             | Recommended Action                      |
| ------------------- | --------------------------------------- |
| Champions           | VIP rewards and early access            |
| Loyal Customers     | Loyalty program upgrades                |
| Potential Loyalists | Cross-sell and engagement campaigns     |
| New Customers       | Onboarding journeys                     |
| Promising           | Personalized recommendations            |
| Discount Sensitive  | Discount optimization and bundle offers |
| Regular Customers   | Re-engagement campaigns                 |
| At Risk             | High-priority win-back campaigns        |
| Dormant             | Low-cost reactivation campaigns         |
| High Value Unhappy  | Immediate service recovery outreach     |

---

# Success Metrics

Retention effectiveness should be monitored using segment-specific KPIs.

| Segment             | Success Metric                    |
| ------------------- | --------------------------------- |
| Champions           | Retention Rate                    |
| Loyal Customers     | Repeat Purchase Rate              |
| Potential Loyalists | Conversion to Loyal Customers     |
| New Customers       | Second Purchase Rate              |
| Promising           | Engagement Rate                   |
| Regular Customers   | Repeat Purchase Rate              |
| Discount Sensitive  | Margin Improvement                |
| At Risk             | Reactivation Rate                 |
| Dormant             | Win-back Rate                     |
| High Value Unhappy  | Customer Satisfaction Improvement |

---

# Manual Review Framework

Automated segmentation is effective for most customers, but some cases require business judgment.

Ten customer records were reviewed manually to analyze situations such as:

* Loyalty versus discount dependency
* High-value customers with negative support experiences
* One-time high-value purchasers
* Segment-rule conflicts
* Hidden churn risk

This review demonstrates how human decision-making can complement rule-based segmentation.

---

# Results Snapshot

| Metric                        | Value              |
| ----------------------------- | ------------------ |
| Customers Segmented           | 2,400              |
| Pre-Snapshot Orders Used      | 8,137              |
| Post-Snapshot Orders Excluded | 1,872              |
| Segments Created              | 10                 |
| Non-RFM Signals Used          | 6                  |
| Manual Review Cases           | 10                 |
| Highest Churn Segment         | Dormant            |
| Highest Revenue Risk Segment  | High Value Unhappy |

---

# Repository Structure

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

# Deliverables

| File                   | Purpose                                        |
| ---------------------- | ---------------------------------------------- |
| rfm_segmentation.ipynb | Full analysis and segmentation workflow        |
| segments.csv           | Customer segment assignments with key features |
| retention_strategy.md  | Segment actions and budget prioritization      |
| manual_review_cases.md | Dataset-backed manual review analysis          |
| requirements.txt       | Reproducible environment configuration         |

---

# Technologies Used

* Python 3.11
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook

---

# Limitations

* Rule-based segmentation relies on business-defined thresholds.
* Segmentation reflects customer state at a single snapshot date.
* Segment-level relationships are associative rather than causal.
* Some behavioral signals may evolve over time.
* Churn labels were used only for validation and not for segment creation.

---

# Conclusion

RFM analysis combined with six behavioral and support-related signals successfully identified ten customer groups with distinct churn risks, engagement levels, and revenue profiles.

Champions and Loyal Customers demonstrated the strongest retention and revenue contribution, while High Value Unhappy, At Risk, and Dormant customers represented the highest retention priorities.

The resulting framework provides an interpretable, actionable, and business-focused foundation for customer retention decision-making before deploying predictive machine learning models.
