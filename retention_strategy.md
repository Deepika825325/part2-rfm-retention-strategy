# Retention Strategy & Campaign Budget Prioritization

## Objective

The objective of this retention strategy is to allocate a limited campaign budget across customer segments to maximize revenue protection and reduce customer churn.

Retention investments should be directed toward segments where the expected value of recovery exceeds the cost of engagement.

---

## Segment Overview

The RFM segmentation framework identified ten customer segments with distinct churn risks, revenue profiles, and behavioral patterns.

| Segment             | Churn Behavior                    | Revenue Profile     |
| ------------------- | --------------------------------- | ------------------- |
| Champions           | Lowest churn rate                 | Highest revenue     |
| Loyal Customers     | Strong retention                  | High revenue        |
| Potential Loyalists | Moderate churn                    | Growing revenue     |
| New Customers       | Variable                          | Early stage         |
| Promising           | Moderate                          | Moderate revenue    |
| Discount Sensitive  | Elevated churn                    | Margin at risk      |
| Regular Customers   | Moderate                          | Average revenue     |
| At Risk             | High churn probability            | High historical value |
| Dormant             | Highest observed churn            | Low recent activity |
| High Value Unhappy  | Elevated churn despite high spend | Highest revenue risk |

---

## Retention Actions by Segment

| Segment             | Recommended Action                          | Rationale                                              |
| ------------------- | ------------------------------------------- | ------------------------------------------------------ |
| Champions           | VIP rewards and early product access        | Protect highest-value customers and reinforce loyalty  |
| Loyal Customers     | Loyalty program upgrades and tier benefits  | Reward commitment and accelerate progression           |
| Potential Loyalists | Cross-sell and engagement campaigns         | Convert growing customers into loyal buyers            |
| New Customers       | Onboarding journeys and second-purchase incentives | Establish purchase habit before disengagement    |
| Promising           | Personalized product recommendations        | Nurture moderate engagement into higher frequency      |
| Discount Sensitive  | Bundle offers and value-based incentives    | Reduce margin erosion while maintaining engagement     |
| Regular Customers   | Re-engagement campaigns                     | Maintain baseline activity cost-efficiently            |
| At Risk             | High-priority win-back campaigns            | Recover high-value customers before churn occurs       |
| Dormant             | Low-cost reactivation campaigns             | Minimal spend for customers with low recovery probability |
| High Value Unhappy  | Immediate service recovery outreach         | Resolve friction before revenue loss materialises      |

### Key Principle

For High Value Unhappy and At Risk customers, **service recovery must precede financial incentives**. Offering discounts to a dissatisfied customer before resolving the underlying issue risks training the customer to associate complaints with rewards.

---

## Budget Assumption

For planning purposes, a retention budget of **₹500,000** is assumed.

The objective is to maximize revenue protection by prioritizing customer groups with the highest combination of:

* Revenue contribution
* Customer volume
* Churn probability
* Probability of successful intervention

---

## Prioritization Method

Segments were ranked using:

**Priority Score = Customer Count × Average Monetary Value × Churn Rate**

This approach balances:

* Revenue at risk
* Size of the affected customer population
* Likelihood of customer loss

Higher scores indicate greater potential business impact from retention efforts.

---

## Recommended Budget Allocation

| Priority | Segment             | Budget Allocation | Budget (₹) | Reason                                                     |
| -------- | ------------------- | ----------------: | ---------: | ---------------------------------------------------------- |
| 1        | High Value Unhappy  |               30% |    150,000 | High spend, elevated churn risk, strong recovery potential |
| 2        | At Risk             |               25% |    125,000 | Historically valuable customers with declining engagement  |
| 3        | Loyal Customers     |               20% |    100,000 | Protect recurring revenue streams                          |
| 4        | Potential Loyalists |               15% |     75,000 | High growth opportunity at moderate intervention cost      |
| 5        | Champions           |               10% |     50,000 | Reinforce satisfaction and loyalty                         |

Dormant, Regular Customers, and New Customers should receive lower-cost automated campaigns rather than intensive retention spending.

---

## Measurement Framework

To isolate true campaign-driven retention from organic customer behaviour, **10–15% of customers in each segment must be held out as a non-contact control group**.

| Group         | Treatment                          | Purpose                             |
| ------------- | ---------------------------------- | ----------------------------------- |
| Treatment     | Receives retention campaign        | Measures post-campaign behaviour    |
| Control       | No campaign contact for 60 days    | Establishes natural retention baseline |

### Why a Holdout Is Required

Without a control group, it is impossible to determine whether retention improvements were caused by the campaign or by natural customer behaviour. A customer who would have repurchased regardless of contact is not a retention win — they are a wasted campaign spend.

### Evaluation Metric

For each segment, compare the **60-day purchase rate** between the treatment and control groups:

```
Campaign Lift = Purchase Rate (Treatment) − Purchase Rate (Control)
```

A positive lift confirms the campaign generated incremental retention. A zero or negative lift indicates the intervention had no effect and budget should be reallocated.

### Minimum Holdout Sizes

| Segment             | Holdout % | Estimated Holdout Size |
| ------------------- | --------: | ---------------------: |
| High Value Unhappy  |       15% |               ~30–40   |
| At Risk             |       10% |               ~55–60   |
| Loyal Customers     |       10% |               ~40–50   |
| Potential Loyalists |       10% |               ~40–50   |
| Champions           |       15% |               ~20–30   |

Holdout sizes are small enough to limit revenue risk from non-contact while large enough to generate statistically interpretable results.

---

## Success Metrics by Segment

Retention effectiveness should be measured using segment-specific KPIs in addition to campaign lift.

| Segment             | Primary Success Metric            | Secondary Metric              |
| ------------------- | --------------------------------- | ----------------------------- |
| Champions           | Retention Rate                    | Average Order Frequency       |
| Loyal Customers     | Repeat Purchase Rate              | Tier Upgrade Rate             |
| Potential Loyalists | Conversion to Loyal Customers     | Average Order Value Growth    |
| New Customers       | Second Purchase Rate              | Time to Second Purchase       |
| Promising           | Engagement Rate                   | Session-to-Purchase Rate      |
| Discount Sensitive  | Margin Improvement                | Full-Price Purchase Rate      |
| Regular Customers   | Repeat Purchase Rate              | Campaign Response Rate        |
| At Risk             | Reactivation Rate                 | Revenue Recovered             |
| Dormant             | Win-back Rate                     | Cost per Reactivation         |
| High Value Unhappy  | Customer Satisfaction Improvement | Ticket Resolution Rate        |

---

## Expected Business Impact

If retention efforts successfully reduce churn within the highest-priority segments, the business can expect:

* Improved customer lifetime value across At Risk and High Value Unhappy segments
* Reduced customer acquisition dependency through higher repeat purchase rates
* Better campaign ROI through holdout-validated lift measurement
* Greater revenue protection from high-value customers
* Stronger customer satisfaction outcomes for dissatisfied but retained customers

Particular emphasis should be placed on High Value Unhappy and At Risk customers, where successful intervention protects both current revenue and future customer lifetime value.

---

## Strategic Recommendations

1. **Prioritize service recovery before financial incentives** for dissatisfied high-value customers — resolve friction first, reward second.
2. **Implement holdout groups** for every segment before budget deployment — measuring lift is not optional if ROI accountability is required.
3. **Allocate the majority of retention spending** toward segments with the highest revenue-at-risk priority scores.
4. **Use automated campaigns** for Dormant, Regular, and New Customers to control intervention costs.
5. **Track customer movement between segments** over time — a customer migrating from At Risk to Regular Customers is a retention success even without a purchase.
6. **Continuously refine segment rules** using observed campaign outcomes and future churn modelling results.

---

## Conclusion

The RFM segmentation framework, enhanced with seven behavioral and support signals, provides an interpretable and actionable approach for retention decision-making before machine learning deployment.

Ten distinct customer segments were identified with materially different churn risks, engagement levels, and revenue contributions. High Value Unhappy and At Risk customers represent the highest-priority retention opportunities due to their combination of customer value and churn probability.

By combining a quantified prioritization formula, segment-specific retention actions, holdout-validated measurement, and segment-level KPIs, the proposed strategy enables efficient allocation of limited retention resources while maximizing measurable business value.