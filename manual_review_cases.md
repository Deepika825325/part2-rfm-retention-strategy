# Manual Review Cases

## Objective

While most customers can be assigned to a segment through predefined business rules, some customers require manual review because their behavior contains conflicting signals.

These customers may show characteristics of multiple segments simultaneously. The purpose of this review is to demonstrate how business judgment can complement rule-based segmentation.

---

# Case 1

## Customer ID: CUST00001

### Observations

* Frequency = 6 purchases
* Monetary Value = ₹2955.57
* Support Tickets = 2
* Average Sentiment = 0.14
* Average Discount Usage = 36.3%
* Assigned Segment = Discount Sensitive

### Why This Case Is Ambiguous

The customer behaves like a loyal repeat buyer but also relies heavily on discounts. The purchase frequency suggests strong engagement, while discount dependency suggests future churn risk if promotions are reduced.

### Recommended Action

Provide personalized product bundles rather than blanket discounts.

### Business Reasoning

The objective is to maintain spending behavior while gradually reducing dependence on promotional offers.

---

# Case 2

## Customer ID: CUST00005

### Observations

* Recency = 38 days
* Frequency = 4 purchases
* Monetary Value = ₹2550.91
* Negative Support Sentiment = -1.00
* Assigned Segment = Potential Loyalists

### Why This Case Is Ambiguous

Purchase activity suggests growth potential, but extremely negative support sentiment introduces retention risk.

### Recommended Action

Follow up with a customer service recovery campaign before sending promotional offers.

### Business Reasoning

Resolving dissatisfaction is likely to generate more value than offering additional discounts.

---

# Case 3

## Customer ID: CUST00006

### Observations

* Frequency = 5 purchases
* Monetary Value = ₹3770.16
* Ticket Count = 2
* Sentiment Score = -0.68
* Assigned Segment = Loyal Customers

### Why This Case Is Ambiguous

Customer purchasing behavior indicates loyalty, but support interactions reveal dissatisfaction.

### Recommended Action

Assign customer to proactive support outreach while maintaining loyalty benefits.

### Business Reasoning

Ignoring service issues may eventually convert a loyal customer into an at-risk customer.

---

# Case 4

## Customer ID: CUST00014

### Observations

* Frequency = 11 purchases
* Monetary Value = ₹8130.16
* Ticket Count = 2
* Sentiment Score = -0.25
* Assigned Segment = Loyal Customers

### Why This Case Is Ambiguous

Very high historical value suggests strong retention importance, yet support experience is deteriorating.

### Recommended Action

Escalate customer to premium support handling.

### Business Reasoning

The cost of intervention is significantly lower than the potential revenue loss from churn.

---

# Case 5

## Customer ID: CUST00025

### Observations

* Monetary Value = ₹4868.86
* Ticket Count = 3
* Negative Sentiment = -0.23
* Assigned Segment = High Value Unhappy

### Why This Case Is Ambiguous

Customer remains valuable despite repeated support issues.

### Recommended Action

Immediate service recovery outreach and issue resolution.

### Business Reasoning

This customer represents a high-value account with elevated churn risk.

---

# Case 6

## Customer ID: CUST00030

### Observations

* Recency = 5 days
* Frequency = 6 purchases
* Monetary Value = ₹3435.59
* Ticket Count = 2
* Sentiment = -0.42
* Assigned Segment = Champions

### Why This Case Is Ambiguous

The customer qualifies as a Champion but displays negative support sentiment.

### Recommended Action

Maintain VIP treatment while investigating support concerns.

### Business Reasoning

High-value customers should not be allowed to accumulate unresolved dissatisfaction.

---

# Case 7

## Customer ID: CUST00033

### Observations

* Recency = 12 days
* Frequency = 4 purchases
* Monetary Value = ₹2128.09
* Ticket Count = 2
* Sentiment = -0.94
* Assigned Segment = Potential Loyalists

### Why This Case Is Ambiguous

Recent activity is encouraging, but support sentiment is among the lowest observed.

### Recommended Action

Prioritize customer support recovery before engagement campaigns.

### Business Reasoning

Customer growth potential may be lost if dissatisfaction remains unresolved.

---

# Case 8

## Customer ID: CUST00034

### Observations

* Frequency = 6 purchases
* Monetary Value = ₹3353.01
* Ticket Count = 3
* Sentiment = -0.23
* Assigned Segment = Loyal Customers

### Why This Case Is Ambiguous

Strong transaction history conflicts with repeated service interactions.

### Recommended Action

Conduct targeted satisfaction outreach.

### Business Reasoning

This customer contributes meaningful revenue and should be protected from preventable churn.

---

# Case 9

## Customer ID: CUST00042

### Observations

* Frequency = 9 purchases
* Monetary Value = ₹7523.74
* Ticket Count = 6
* Sentiment = -0.46
* Assigned Segment = High Value Unhappy

### Why This Case Is Ambiguous

High spending continues despite substantial support friction.

### Recommended Action

Assign dedicated account management and service recovery.

### Business Reasoning

This customer represents one of the highest-value retention opportunities in the dataset.

---

# Case 10

## Customer ID: CUST00053

### Observations

* Frequency = 4 purchases
* Monetary Value = ₹4192.59
* Ticket Count = 2
* Sentiment = -0.57
* Assigned Segment = Potential Loyalists

### Why This Case Is Ambiguous

Strong revenue contribution suggests future loyalty potential, but customer satisfaction indicators are deteriorating.

### Recommended Action

Combine personalized recommendations with proactive support intervention.

### Business Reasoning

A successful recovery could move this customer into the Loyal Customer segment.

---

# Summary

The reviewed customers demonstrate situations where automated segmentation alone is insufficient. In most cases, conflicting signals emerge between purchasing behavior and customer experience indicators.

The review highlights the importance of combining RFM metrics with support sentiment, complaint history, and engagement signals before making final retention decisions.
