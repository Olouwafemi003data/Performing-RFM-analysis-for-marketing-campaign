# Performing-RFM-analysis-for-marketing-campaign
Segment customers by Recency, Frequency and Monetary value to decide who to reward, reactivate or stop investing in.

### Why RFM ?   

Cohort analysis: not possible, the data has only one date per customer (enrolment), not repeated purchase dates.

Correlation analysis: describes relationships between variables but does not say which customers to target.

RFM: the three dimensions exist in the data and segments can be linked to campaign response.

Input :	data/marketing_campaign_clean.csv
Output : 	data/customers_rfm.csv (R, F, M, scores, segment, response) 

### Definitions

Recency :  days since last purchase (lower is better) 

Frequency : NumWebPurchases + NumCatalogPurchases + NumStorePurchases (deal purchases are already included in these channels)

Monetary : Sum of the six Mnt... spending columns over 2 years

Scores :	Quintiles from 1 to 5, 5 = best (recency ranking is reversed)

### Interpretation 

What the data looks like
• 2,240 customers were scored, with ≈1.36 million in total two-year spending.

• The typical customer bought 49 days ago, made 12.5 purchases and spent 606. 14.9% (≈334 customers) accepted the last campaign offer.

• Spending is skewed to the right: the mean (606) is well above the median (396). The top 20% of customers generate 52.3% of spending. This is concentrated, but less extreme than a classic 80/20 pattern.

• The scoring logic is correct. In the sample rows, 16 days since the last purchase gives R = 5 and 94 days gives R = 1, so recency is reversed as intended. Frequency and monetary scores move together, which is normal in RFM.


1. Value sits in three segments. Champions, Loyal Customers and At Risk are 59.7% of customers but 95.4% of spending. The other three segments are 40.3% of customers and only 4.6% of spending.

2. At Risk is the largest revenue pool and the biggest warning sign. These customers account for the highest spending share (39.5%, about 536,000). They spend more per head than Loyal Customers (982 vs 754) and buy often (17.4 purchases). But their last purchase was 79 days ago, against 18 days for Champions. At 17 purchases over two years, they normally buy about every six weeks, so 79 days is roughly twice their usual gap. They are still reachable: 12.3% accepted the last offer, four times the Hibernating rate.

3. Champions are the core, and they are the most responsive. They are 14.6% of customers but 30.2% of spending, with the highest income (≈72,000). Their response rate (33.3%) is 2.2× the average, and they account for about a third of all acceptances (≈109 of 334).

4. Loyal Customers are the natural pipeline to Champions. They are recent enough (37 days) and respond slightly above average (16.6%). The gap with Champions is mostly spending (754 vs 1,252).

5. Recency strongly separates responsive from unresponsive customers. Promising and Hibernating customers have nearly identical frequency (5.1 vs 5.2), spend (70 vs 70) and income (≈35,000 vs ≈34,000). The only major difference is recency (19 vs 80 days). Yet their response rates are 15.8% vs 3.1%, a fivefold gap. Timing matters more than spending level for responsiveness (this is an association, not proof of cause).

6. Income drives value, recency drives action. High-value segments have incomes of about 60,000 to 72,000, against about 32,000 to 35,000 for the low-value ones. Income is a structural factor the company cannot change. Recency is behavioural, so it is the lever marketing can act on.

7. Low-value segments cost more than they return. Need Attention and Hibernating together are 23.9% of customers, 2.7% of spending and ≈7% of acceptances. Reaching one Hibernating customer who responds takes about 32 contacts, against 3 for a Champion.


### Business impact
Targeting Champions, Loyal Customers and At Risk reaches about 60% of the base but covers 95% of spending and about three quarters of acceptances (≈253 of 334). Contact volume falls by about 40%, so marketing effort moves to the customers who generate the value.
The reactivation upside is large. Winning back just 10% of At Risk customers (≈55 people) would secure about 54,000 of two-year spending at their current average level, roughly 4% of total spending. This is an illustration, not a forecast.

### Recommendations

#### 1
At Risk
Launch a personalised win-back journey, triggered when a customer passes about 60 days without a purchase. Use offers tied to their favourite categories. Give the top spenders in this segment a personal touch.
Reactivation rate (purchase within 30 days), recovered spend, response vs the 12.3% baseline
#### 2
Champions
Protect them with a VIP programme, early access and premium bundles. Avoid blanket discounts: they already buy without them.
Recency kept below about 30 days, spend per customer, retention
#### 3
Loyal Customers
Build upsell and cross-sell offers (bundles, loyalty tiers, other categories) to close the spending gap with Champions.
Share moving up to Champions, average spend
#### 4
Promising
Run a low-cost nurture sequence: welcome emails, basket-building offers, free-shipping thresholds. Cap discount budgets, since income is low.
Purchases per customer, conversion to Loyal
#### 5
Need Attention
Send an automated, low-cost reminder to stop them sliding into Hibernating (their recency is already 49 days).
Share staying active after the reminder
#### 6
Hibernating
Spend as little as possible: one last low-cost email, then exclude them from costly channels and promotions.
Cost per acceptance


### Limitations and data checks
• Relative segments : Quintiles split customers against each other, not against an absolute standard. By construction, 40% of customers fall into the two lowest recency quintiles, which is exactly At Risk (24.4%) plus Hibernating (15.6%). Use the purchase-cycle argument above, not the segment size alone, to judge how serious the risk is.

• Response rates are not true conversion rates. The denominator is all customers, and we do not know who was contacted. Acceptance is also not revenue.

• Frequency definition : Discount purchases are assumed to be already counted in the web, catalog and store channels. The 6 customers with Frequency = 0 but Monetary > 0 suggest checking this: look at their NumDealsPurchases. The impact is negligible (0.3% of customers).

• Income outlier : The maximum income (666,666) looks like a data-entry error and can distort the average income of one segment. 

• Correlation not causation : Income, recency and response move together, but this analysis does not prove what drives what.
   
