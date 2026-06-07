# D2C Customer Retention Strategy using RFM Segmentation

## Project Overview

This project builds a customer retention framework using RFM (Recency, Frequency, Monetary) analysis combined with behavioral and support signals.

The objective is to identify customer segments requiring retention attention before deploying a machine learning churn model.

## Dataset

The analysis uses customer order history, support interactions, engagement behavior, and campaign-related attributes provided in the assessment dataset.

## Methodology

### Step 1: RFM Feature Engineering

For each customer:

* Recency = Days since last purchase
* Frequency = Total orders placed
* Monetary = Total customer spend

### Step 2: RFM Scoring

Customers were assigned quintile-based scores:

* R Score (1–5)
* F Score (1–5)
* M Score (1–5)

Higher scores indicate stronger customer value and engagement.

### Step 3: Additional Behavioral Signals

To improve segmentation quality beyond RFM, the following signals were incorporated:

* Support ticket count
* Customer sentiment
* Return rate
* Average discount usage
* Category diversity

### Step 4: Customer Segmentation

Ten customer segments were created:

* Champions
* Loyal Customers
* Potential Loyalists
* New Customers
* Promising
* High Value Unhappy
* Discount Sensitive
* At Risk
* Dormant
* Regular Customers

### Segmentation Logic

High-value customers with strong RFM scores were classified as Champions.

Customers exhibiting high support burden and negative sentiment were classified as High Value Unhappy.

Customers with high discount dependence were classified as Discount Sensitive.

Customers with long inactivity periods were classified as At Risk or Dormant.

### Key Findings

| Segment            | Customers | Churn Rate |
| ------------------ | --------: | ---------: |
| Dormant            |       121 |      90.1% |
| At Risk            |       389 |      78.7% |
| High Value Unhappy |       112 |      72.3% |
| Champions          |       344 |      10.5% |

### Retention Prioritization

Retention budget should focus on:

1. High Value Unhappy
2. At Risk
3. Discount Sensitive

These segments provide the highest recoverable revenue opportunity.

## Repository Structure

rfm_segmentation.ipynb

segments.csv

retention_strategy.md

manual_review_cases.md

requirements.txt

outputs/charts/

outputs/tables/

## How to Run

pip install -r requirements.txt

Open:

rfm_segmentation.ipynb

and run all notebook cells.

## Author

Deepika Kumari
