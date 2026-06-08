# D2C Customer Churn Intelligence

## Part 2: RFM Segmentation & Retention Strategy

### Objective

The objective of this project is to identify customer groups requiring different retention interventions before deploying a machine learning churn prediction model.

Customers were segmented using RFM (Recency, Frequency, Monetary) analysis and enriched with behavioral and support-related signals to develop actionable retention strategies and campaign prioritization recommendations.

---

## Business Problem

Customer retention is often more cost-effective than customer acquisition. Before building predictive churn models, businesses need an interpretable framework to identify valuable customers, understand behavioral patterns, and prioritize retention investments.

This project uses transaction history, support interactions, customer engagement signals, and purchasing behavior to create meaningful customer segments and recommend targeted retention actions.

---

## Dataset

The analysis uses the following datasets:

| Dataset                  | Description                                  |
| ------------------------ | -------------------------------------------- |
| customers.csv            | Customer demographic and profile information |
| orders.csv               | Customer purchase transactions               |
| support_tickets.csv      | Customer support interactions                |
| web_events_snapshot.csv  | Website and engagement activity              |
| intervention_history.csv | Previous campaign information                |
| churn_labels.csv         | Observed churn outcomes                      |

---

## Methodology

### 1. Data Preparation

* Loaded and validated all datasets
* Converted date columns to datetime format
* Handled missing values
* Removed future order records occurring after the snapshot date to prevent data leakage

### 2. RFM Feature Engineering

RFM features were created using customer order history:

* **Recency** → Days since last purchase
* **Frequency** → Total number of orders
* **Monetary** → Total customer spending

### 3. Additional Behavioral Features

To improve segmentation quality, RFM metrics were combined with additional behavioral and support signals:

* Return Rate
* Average Discount Usage
* Category Diversity
* Support Ticket Count
* Support Sentiment
* Average Resolution Time
* Website Sessions
* Campaign Clicks
* Email Opens
* Last Visit Activity

### 4. RFM Scoring

Customers were assigned R, F, and M scores using quintile-based scoring.

* R Score: 1–5
* F Score: 1–5
* M Score: 1–5

Combined scores were used as the foundation for customer segmentation.

### 5. Customer Segmentation

Segments were created using both RFM scores and behavioral indicators.

| Segment             |
| ------------------- |
| Champions           |
| Loyal Customers     |
| Potential Loyalists |
| New Customers       |
| Promising           |
| Regular Customers   |
| Discount Sensitive  |
| At Risk             |
| Dormant             |
| High Value Unhappy  |

### Segmentation Logic

* High R, F, M → Champions
* High Frequency customers → Loyal Customers
* Recently active customers with growth potential → Potential Loyalists
* First-time recent buyers → New Customers
* Moderate engagement customers → Promising
* Average behavior customers → Regular Customers
* High discount dependency → Discount Sensitive
* High-value customers with declining activity → At Risk
* Long inactive customers → Dormant
* High-value customers with negative support experience → High Value Unhappy

---

## Churn Validation

Segment quality was validated using observed churn outcomes from the provided churn dataset.

Key findings:

* Champions exhibited the lowest churn risk.
* Loyal Customers demonstrated strong retention behavior.
* Dormant customers showed the highest churn rate.
* At Risk and High Value Unhappy customers represented major retention opportunities.

This validation confirmed that the segmentation framework aligns with real customer outcomes.

---

## Campaign Budget Prioritization

To allocate a limited retention budget, segments were ranked using:

**Priority Score = Customer Count × Average Monetary Value × Churn Rate**

This prioritization balances:

* Revenue impact
* Segment size
* Churn probability

Highest priority segments:

1. High Value Unhappy
2. At Risk
3. Loyal Customers
4. Potential Loyalists
5. Champions

---

## Repository Structure

```text
part2-rfm-retention-strategy/
│
├── data/
│   ├── customers.csv
│   ├── orders.csv
│   ├── support_tickets.csv
│   ├── web_events_snapshot.csv
│   ├── intervention_history.csv
│   └── churn_labels.csv
│
├── outputs/
│   ├── charts/
│   └── tables/
│
├── rfm_segmentation.ipynb
├── segments.csv
├── retention_strategy.md
├── manual_review_cases.md
├── requirements.txt
├── README.md
└── .gitignore
```

---

## Outputs

### Notebook

**rfm_segmentation.ipynb**

Contains:

* Data preparation
* Leakage prevention
* RFM feature engineering
* Behavioral feature creation
* RFM scoring
* Customer segmentation
* Segment analysis
* Churn validation
* Retention recommendations

### Segment File

**segments.csv**

Contains:

* customer_id
* segment_name
* recency
* frequency
* monetary
* return_rate
* avg_discount
* ticket_count
* category_diversity
* churn_next_60d

### Strategy Report

**retention_strategy.md**

Contains:

* Segment descriptions
* Retention actions
* Expected business value
* Budget prioritization strategy

### Manual Review Report

**manual_review_cases.md**

Contains:

* 10+ customer cases
* Ambiguous retention decisions
* Dataset-backed business reasoning

---

## Key Business Insights

* Customer behavior varies significantly across segments.
* High-value customers with poor support experiences represent the highest revenue risk.
* Dormant and At Risk customers exhibit the strongest churn tendencies.
* Discount dependency is associated with increased retention risk.
* Personalized interventions are more effective than blanket promotional campaigns.

---

## Conclusion

RFM analysis combined with behavioral and support signals successfully identified customer groups with significantly different churn risks and business value.

Champions and Loyal Customers demonstrated the strongest retention and revenue contribution, while Dormant, At Risk, and High Value Unhappy customers represented the highest retention priority. Churn validation confirmed that the proposed segmentation aligns closely with observed customer outcomes.

The resulting segmentation framework provides an interpretable and actionable foundation for customer retention decisions before deploying a predictive machine learning model.
