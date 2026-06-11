# Manual Review Cases

## Objective

While most customers can be assigned to a segment through predefined business rules, some customers require manual review because their behavior contains conflicting signals.

These customers may show characteristics of multiple segments simultaneously, or their automated segment assignment does not reflect the full picture of their business situation. The purpose of this review is to demonstrate how business judgment can complement rule-based segmentation.

---

# Case 1

## Customer ID: CUST00001

### Conflict Type: Loyalty vs Discount Dependency

### Observations

| Feature            | Value           |
| ------------------ | --------------- |
| Frequency          | 6 purchases     |
| Monetary Value     | ₹2,955.57       |
| Support Tickets    | 2               |
| Average Sentiment  | 0.14            |
| Average Discount   | 36.3%           |
| Assigned Segment   | Discount Sensitive |

### Why This Case Is Ambiguous

This customer has a purchase frequency of 6 and a positive support sentiment, which are characteristics more consistent with Loyal Customers than Discount Sensitive. However, a 36.3% average discount rate triggered the Discount Sensitive rule. The key question is whether this customer's spending is driven by genuine brand preference or purely by promotional availability.

### Recommended Action

Introduce personalized product bundles and value-based loyalty benefits rather than continued blanket discounts. Reduce promotional exposure by 10% per campaign cycle and monitor whether purchase frequency holds.

### Business Reasoning

Reducing discount dependency without losing purchase frequency requires shifting this customer's motivation from price to product value. Bundles test whether loyalty is brand-driven or promotion-driven — if frequency drops as discounts reduce, the Discount Sensitive classification is confirmed and the strategy pivots accordingly.

---

# Case 2

## Customer ID: CUST00005

### Conflict Type: Growth Potential vs Extreme Dissatisfaction

### Observations

| Feature            | Value                |
| ------------------ | -------------------- |
| Recency            | 38 days              |
| Frequency          | 4 purchases          |
| Monetary Value     | ₹2,550.91            |
| Support Sentiment  | -1.00 (maximum negative) |
| Assigned Segment   | Potential Loyalists  |

### Why This Case Is Ambiguous

Recency and frequency suggest a customer on a growth trajectory toward Loyal Customers. However, a sentiment score of -1.00 is the most extreme negative value in the scale. This customer is actively dissatisfied at the exact moment the segmentation recommends investing in their growth. Sending a promotional campaign to a customer with maximum negative sentiment risks triggering disengagement rather than conversion.

### Recommended Action

Pause all promotional outreach. Trigger an immediate customer service recovery touchpoint — direct apology, resolution of the underlying issue, and a follow-up satisfaction check — before any commercial campaign is deployed.

### Business Reasoning

A Potential Loyalist with a sentiment score of -1.00 is a customer whose dissatisfaction is still fresh and unresolved. Promotional outreach before service recovery risks surfacing resentment rather than gratitude, and destroys the conversion opportunity. The growth potential is only accessible once the negative experience is addressed.

---

# Case 3

## Customer ID: CUST00004

### Conflict Type: At Risk Label Applied to a Single-Purchase Customer

### Observations

| Feature            | Value       |
| ------------------ | ----------- |
| Recency            | 131 days    |
| Frequency          | 1 purchase  |
| Monetary Value     | ₹1,604.04   |
| Support Tickets    | 0           |
| Average Sentiment  | 0.00        |
| Sessions (30d)     | 1           |
| Assigned Segment   | At Risk     |

### Why This Case Is Ambiguous

The At Risk rule fires because R ≤ 2 and M ≥ 3 — correct by the rule definition. However, the At Risk segment is designed for customers with strong historical value who are now declining in engagement. This customer made a single purchase 131 days ago and has never returned. There was no prior engagement to decline from. The standard At Risk intervention (personalized win-back campaign) assumes an established relationship exists — here it does not. Treating this customer as At Risk overestimates emotional affinity and wastes high-cost intervention budget.

### Recommended Action

Apply a lightweight re-engagement campaign similar to the Dormant playbook, but with messaging focused on the specific category of the original purchase. Do not deploy the full At Risk win-back package.

### Business Reasoning

Win-back campaigns assume the customer has something to return to. A customer who purchased once 131 days ago is behaviorally closer to a lapsed new customer than a declining loyal one. The ₹1,604 purchase value justifies re-engagement, but the absence of any prior relationship means the intervention cost ceiling should be lower than a true At Risk customer.

---

# Case 4

## Customer ID: CUST00014

### Conflict Type: Top-Tier Revenue Contributor with Deteriorating Support Experience

### Observations

| Feature            | Value           |
| ------------------ | --------------- |
| Frequency          | 11 purchases    |
| Monetary Value     | ₹8,130.16       |
| Support Tickets    | 2               |
| Sentiment Score    | -0.25           |
| Assigned Segment   | Loyal Customers |

### Why This Case Is Ambiguous

With 11 purchases and ₹8,130 in spend, this customer sits in the top tier of revenue contributors in the dataset. The Loyal Customers segment is correct, but the standard loyalty intervention (loyalty point acceleration, cross-sell campaigns) does not address the negative support trend. A deteriorating support experience at this spend level is an early warning that standard loyalty program mechanics will not be sufficient to hold this customer.

### Recommended Action

Escalate to premium support handling immediately. Assign a named support contact rather than the standard ticket queue. Follow up with a direct outreach acknowledging the recent experience before deploying any commercial campaign.

### Business Reasoning

With ₹8,130 in historical spend, this account warrants treatment above the standard SLA threshold. A direct escalation call costs less than one lost transaction from this customer. The two tickets with negative sentiment are not yet a crisis — but they become one if the third ticket goes unresolved.

---

# Case 5

## Customer ID: CUST00025

### Conflict Type: High Value Retained Despite Repeated Service Failures

### Observations

| Feature            | Value               |
| ------------------ | ------------------- |
| Monetary Value     | ₹4,868.86           |
| Support Tickets    | 3                   |
| Average Sentiment  | -0.23               |
| Assigned Segment   | High Value Unhappy  |

### Why This Case Is Ambiguous

The automated segment assignment is correct. The ambiguity is in the intervention timing. This customer has raised 3 tickets with consistently negative sentiment but continues to spend — suggesting they have not yet reached their churn threshold. The risk of acting too aggressively (over-compensating with large discounts or credits) is that it trains the customer to associate complaints with rewards, creating a new problem.

### Recommended Action

Immediate service recovery outreach focused on issue resolution, not compensation. Once the underlying problem is resolved and confirmed, introduce a loyalty acknowledgment (exclusive access, early product preview) rather than a monetary offer.

### Business Reasoning

Three tickets with negative sentiment while continuing to spend signals a customer who still wants the relationship to work but is approaching a tolerance limit. Recovery at this stage has a high probability of success. The intervention should resolve the friction, not pay the customer to tolerate it — compensation-first recovery risks setting a precedent that complaints generate discounts.

---

# Case 6

## Customer ID: CUST00030

### Conflict Type: Champion with Recent Negative Support Signal

### Observations

| Feature            | Value        |
| ------------------ | ------------ |
| Recency            | 5 days       |
| Frequency          | 6 purchases  |
| Monetary Value     | ₹3,435.59    |
| Support Tickets    | 2            |
| Sentiment Score    | -0.42        |
| Assigned Segment   | Champions    |

### Why This Case Is Ambiguous

This customer correctly qualifies as a Champion on RFM metrics. The ambiguity is that a sentiment score of -0.42 with 2 recent tickets is a new dissatisfaction signal, not a historical one. The customer purchased 5 days ago — meaning the negative experience is recent and the customer is still active. The standard Champion playbook (VIP rewards, early access) does not address an active complaint.

### Recommended Action

Maintain all VIP benefits and Champion-tier treatment. Simultaneously trigger a direct, non-automated support investigation into the 2 open tickets. The outreach should feel personal, not templated.

### Business Reasoning

A Champion with a sentiment score of -0.42 is a dissatisfaction signal that is both recent and resolvable. The purchase 5 days ago confirms the customer has not yet disengaged. Waiting for the next interaction to surface the complaint risks losing the customer at the moment of their highest engagement. Resolving this now costs very little relative to the replacement cost of a lost Champion.

---

# Case 7

## Customer ID: CUST00060

### Conflict Type: Discount Sensitive Classification Conflicts with Platinum Loyalty Tier

### Observations

| Feature            | Value               |
| ------------------ | ------------------- |
| Frequency          | 9 purchases         |
| Monetary Value     | ₹4,650.00           |
| Average Discount   | 41%                 |
| Loyalty Tier       | Platinum            |
| Support Tickets    | 0                   |
| Average Sentiment  | 0.00                |
| Assigned Segment   | Discount Sensitive  |

### Why This Case Is Ambiguous

The Discount Sensitive rule correctly fires due to avg_discount ≥ 0.35. However, this customer holds a Platinum loyalty tier — a designation the business itself assigned based on long-term purchase value. A Platinum member classified as Discount Sensitive creates a direct contradiction: the business has rewarded this customer as highly loyal while the segmentation model is flagging them for discount dependency. The critical question is whether this customer spent their way to Platinum through genuine brand preference, or through accumulation of heavily discounted purchases.

### Recommended Action

Review purchase history to determine whether high discount usage correlates with category exploration or concentration in a single discounted category. If spread across categories, treat as Loyal with a discount reduction plan. If concentrated in one category, treat as Discount Sensitive and reduce promotional exposure in that category specifically.

### Business Reasoning

Stripping Platinum benefits from this customer while simultaneously reducing discounts risks triggering churn from two directions at once. The correct approach is to test brand loyalty before withdrawing incentives — introduce one non-discounted purchase incentive (exclusive Platinum product access) and measure whether the customer converts without a promotion. The result disambiguates the classification.

---

# Case 8

## Customer ID: CUST00075

### Conflict Type: Dormant Classification Undersells High-Value Reactivation Opportunity

### Observations

| Feature              | Value       |
| -------------------- | ----------- |
| Recency              | 189 days    |
| Frequency            | 2 purchases |
| Monetary Value       | ₹8,940.00   |
| Average Order Value  | ₹4,470.00   |
| Support Tickets      | 0           |
| Sessions (30d)       | 0           |
| Assigned Segment     | Dormant     |

### Why This Case Is Ambiguous

The Dormant rule correctly fires: R = 1 and F ≤ 2. Standard Dormant treatment is a low-cost reactivation campaign — a comeback email with a modest promotional offer. However, this customer's average order value of ₹4,470 is approximately six times the dataset average of ₹743.90. The customer purchases infrequently but spends at an exceptionally high level when they do. Treating this customer with the same low-cost reactivation as a typical dormant customer with ₹400 in lifetime spend significantly underinvests in a potentially major reactivation.

### Recommended Action

Remove from the standard Dormant reactivation batch. Apply an At Risk-level win-back intervention — personalized outreach referencing the customer's previous purchase categories, with a high-value offer commensurate with their historical spend level (e.g., exclusive access or a concierge-style service touchpoint rather than a discount voucher).

### Business Reasoning

The Dormant segment assumes low-cost treatment is appropriate because dormant customers have low lifetime value. This customer inverts that assumption — infrequent purchase rhythm combined with very high order value means one successful reactivation could recover over ₹4,000 in a single transaction. The cost of a premium reactivation intervention is justified by the magnitude of the potential recovery.

---

# Case 9

## Customer ID: CUST00042

### Conflict Type: Extreme Support Friction Alongside Continued High Spend

### Observations

| Feature            | Value               |
| ------------------ | ------------------- |
| Frequency          | 9 purchases         |
| Monetary Value     | ₹7,523.74           |
| Support Tickets    | 6                   |
| Average Sentiment  | -0.46               |
| Assigned Segment   | High Value Unhappy  |

### Why This Case Is Ambiguous

Six support tickets despite ₹7,523 in spend suggests this customer has an exceptionally high tolerance for operational friction. The automated segment assignment is correct. The ambiguity is in understanding why a customer with 6 negative support interactions continues to spend at this level — and whether the 7th interaction will be the breaking point.

### Recommended Action

Assign a dedicated account owner rather than routing to the standard support queue. Conduct a proactive review of all 6 ticket histories to identify whether a single recurring issue is driving the repeated contacts. Resolve the root cause, not just the individual tickets.

### Business Reasoning

Six tickets with continued ₹7,523 in spend is not a signal of disengagement — it is a signal of extreme patience. Most customers would have churned after 2–3 unresolved contacts. This customer's continued spending despite friction represents a significant retained-value risk: when they do churn, it will be sudden rather than gradual, and the revenue loss will be large. Dedicated account ownership addresses the systemic issue before the patience runs out.

---

# Case 10

## Customer ID: CUST00085

### Conflict Type: New Customer Classification with Champion-Level First Order

### Observations

| Feature             | Value           |
| ------------------- | --------------- |
| Recency             | 18 days         |
| Frequency           | 1 purchase      |
| Monetary Value      | ₹7,200.00       |
| Average Discount    | 8%              |
| Support Tickets     | 0               |
| Sessions (30d)      | 11              |
| Assigned Segment    | New Customers   |

### Why This Case Is Ambiguous

The New Customer rule correctly fires: R ≥ 4 and F = 1. Standard new customer treatment is a welcome email sequence, onboarding content, and a first-to-second purchase incentive — typically a small discount or free delivery offer. However, this customer's first order of ₹7,200 places them in the top 5% of all monetary values in the dataset, at nearly 10x the average first-purchase value of comparable new customers. A standard welcome voucher of ₹100–200 is a disproportionately small response to a ₹7,200 opening spend.

### Recommended Action

Bypass the standard new customer email sequence. Fast-track into a high-value onboarding track with a dedicated personal outreach within 5 days of purchase — acknowledge the purchase specifically, offer concierge-style product guidance, and provide access to loyalty tier acceleration. Do not offer a generic discount voucher as the follow-up incentive.

### Business Reasoning

If this customer makes a second purchase at a similar value, they will immediately qualify as a Loyal Customer or Champion. The cost of losing this customer after one purchase is not the ₹7,200 already spent — it is the ₹20,000–40,000 in potential lifetime value that will never be realized. Standard new customer campaigns are calibrated for average new customer value; applying them here means the highest-potential new customer in the cohort receives the same treatment as someone who spent ₹400.

---

# Summary

The ten reviewed cases cover four distinct types of segmentation ambiguity:

| Conflict Type                                   | Cases          |
| ----------------------------------------------- | -------------- |
| Good purchase behavior + negative support experience | 2, 4, 5, 6 |
| Loyalty signal vs discount dependency           | 1, 7           |
| Segment rule mismatch with customer value profile | 3, 8, 10     |
| High tolerance for friction masking churn risk  | 9              |

The review demonstrates that automated segmentation is a necessary starting point but not a complete decision framework. RFM rules correctly classify the majority of customers. However, edge cases require human judgment — particularly when a customer's financial value, loyalty program status, or interaction history contradicts the signal that triggered their segment assignment.

The most common failure mode identified is under-investment in high-value customers who were assigned to lower-priority segments due to a single disqualifying signal (low recency, high discount, single purchase). In each such case, the appropriate response is to escalate the intervention tier rather than apply the standard segment playbook.