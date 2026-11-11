# Retail Business Performance Analysis


## 1. Executive Summary

This project examines the historical transaction data of an online retailer
to understand its product performance, customer purchasing patterns,
monthly revenue trends, and geographical revenue distribution.

The analysis uses the UCI Online Retail dataset, containing transactions
recorded between December 2010 and December 2011.

After investigating data-quality issues and applying transparent
transaction filters, a merchandise dataset was prepared. A separate
sensitivity scenario excluded two independently verified fully cancelled
transactions.

Key findings include:

- The sensitivity-scenario recorded merchandise revenue was £10,047,508.36.
- The analysis covered 3,916 product stock codes.
- The top 10 products contributed 8.17% of recorded merchandise revenue.
- The top 20 identifiable customers contributed 22.78% of identifiable-customer revenue.
- The United Kingdom accounted for 84.78% of recorded merchandise revenue.
- International markets contributed 15.22%.
- Approximately 62.21% of identifiable customers purchased across multiple
  calendar months.
- November 2011 recorded the highest monthly merchandise revenue.

The findings indicate substantial geographical concentration in the
United Kingdom, alongside a broad distribution of revenue across products
and identifiable customers.

The analysis also identifies opportunities to investigate international
markets, product portfolio performance, and customer engagement.

Recorded revenue represents transaction value rather than profit.
The dataset does not contain the cost information required to assess
profitability.

All findings are limited to the historical dataset and the cleaning,
classification, and sensitivity assumptions documented in this report.

## 2. Business Problem and Objectives

### Business Problem

An online retailer generates transaction data across products,
customers, time periods, and geographical markets. However, raw
transaction records do not automatically reveal which areas contribute
most to recorded revenue or where management should investigate further.

This project uses historical transaction data to examine the retailer's
business performance and identify measurable patterns that can support
better-informed management decisions.

### Primary Business Question

Which products, customers, geographical markets, and sales periods
contribute most to the retailer's recorded revenue, and what
evidence-based actions could management consider?

### Analytical Objectives

1. Evaluate product-level recorded revenue and identify the highest-
   contributing products.
2. Examine monthly revenue, invoice activity, and changes in sales volume.
3. Investigate customer purchasing frequency and revenue concentration.
4. Compare recorded merchandise revenue across geographical markets.
5. Identify data-quality limitations that could affect interpretation.
6. Translate analytical findings into practical management
   recommendations.

### Analytical Framework

The project follows the PACE framework:

- **Plan:** Define the business question, objectives, and analytical scope.
- **Analyze:** Inspect, clean, classify, and investigate the transaction data.
- **Construct:** Develop analytical summaries, visualizations, and findings.
- **Execute:** Communicate results through a final report and
  evidence-based recommendations.

## 3. Dataset Overview

### Dataset Source

The analysis uses the Online Retail dataset published by the
UCI Machine Learning Repository.

- Dataset: Online Retail
- Source: UCI Machine Learning Repository
- DOI: https://doi.org/10.24432/C5BW33
- Original data provider: Daqing Chen
- Licence: CC BY 4.0
- Observation period: 1 December 2010 to 9 December 2011
- Original records: 541,909
- Original variables: 8

### Dataset Description

The dataset contains transaction-level records from a UK-based
online retailer.

| Variable | Description |
|---|---|
| InvoiceNo | Unique invoice identifier; cancellation invoices use a C prefix |
| StockCode | Product or transaction code |
| Description | Product or transaction description |
| Quantity | Number of units recorded in a transaction |
| InvoiceDate | Date and time of the transaction |
| UnitPrice | Unit price recorded in sterling |
| CustomerID | Customer identifier, where available |
| Country | Country associated with the transaction |

### Analytical Scope

The primary analysis focuses on merchandise transactions with:

- Positive quantities
- Positive unit prices
- Non-cancellation invoice numbers
- Stock codes other than identified special transaction codes

The resulting merchandise dataset contains 527,947 records
before the separate sensitivity adjustment.

The sensitivity scenario excludes two independently verified
fully cancelled original invoices, producing an adjusted
recorded merchandise revenue of £10,047,508.36.

The analysis retains the original raw dataset unchanged and
uses a separate processed dataset for merchandise analysis.

## 4. Data Cleaning and Methodology

### 4.1 Initial Data Inspection

The original dataset contained 541,909 transaction records and
8 variables.

Initial inspection identified:

- 135,080 records with missing CustomerID values.
- 1,454 records with missing product descriptions.
- 5,268 exact duplicate occurrences.
- 9,288 cancellation invoice records.
- Negative quantities and unusual unit-price values.
- Special transaction codes representing postage, discounts,
  manual entries, and adjustments.

### 4.2 Transaction Investigation

Several transaction categories were investigated before
constructing the merchandise dataset.

**Cancellations:** Invoice numbers beginning with C were
classified as cancellation records. All 9,288 such records
had negative quantities.

**Negative quantities without a cancellation prefix:** A
further 1,336 records had negative quantities without a C
invoice prefix. All had zero unit prices and missing
CustomerIDs. They were treated as operational or unusual
adjustment records rather than confirmed customer returns.

**Zero-price records:** A total of 2,515 records had zero
unit prices. These were excluded from the primary
revenue-generating merchandise analysis and retained for
separate data-quality consideration.

**Duplicate records:** The original dataset contained 5,268
exact duplicate occurrences. These were not automatically
removed because identical records may represent repeated
transaction lines. A deduplicated comparison showed a
recorded revenue difference of £21,740.98.

**Special transaction codes:** POST, DOT, M, D, B, and PADS
were investigated separately. These represent postage,
dotcom postage, manual entries, discounts, bad-debt
adjustments, and a special product or adjustment entry.
They were excluded from merchandise-level product analysis.

### 4.3 Merchandise Dataset Construction

The primary merchandise dataset retained records satisfying
the following conditions:

- Invoice number did not begin with C.
- Quantity was greater than zero.
- Unit price was greater than zero.
- Stock code was not one of the identified special
  transaction codes.

The resulting dataset contained 527,947 records,
representing 3,917 stock codes before product-level
aggregation.

A derived variable, LineRevenue, was calculated by
multiplying Quantity by UnitPrice.

LineRevenue represents recorded transaction value and
does not represent profit.

### 4.4 Cancellation Sensitivity Analysis

Two unusually large merchandise transactions were
independently matched to full-value cancellation invoices:

- Invoice 581483: £168,469.60.
- Invoice 541431: £77,183.60.

Their combined recorded value was £245,653.20.

Because broader automated cancellation matching produced
ambiguous and reusable matches, no additional original
transactions were automatically removed.

A separate sensitivity dataset excluded these two verified
original invoices. Its recorded merchandise revenue was
£10,047,508.36.

This is a sensitivity scenario, not a definitive
cancellation-adjusted net-sales figure.

### 4.5 Methodological Limitations

- Missing CustomerIDs limit customer-level analysis.
- Some product stock codes have multiple descriptions.
- Exact duplicate records may represent genuine repeated
  transaction lines.
- Cancellation matching could not reliably establish
  one-to-one relationships for all records.
- The dataset does not include product costs, operating
  expenses, or profit information.
- The historical observation period does not establish
  current business conditions.

These decisions were documented to preserve transparency
and avoid unsupported assumptions.

## 5. Product Performance Analysis

### 5.1 Product Revenue Overview

The sensitivity dataset was used to evaluate product-level
recorded merchandise revenue.

The analysis covered:

- 3,916 distinct product stock codes.
- 8.17% of recorded merchandise revenue from the top
  10 products.
- 12.02% from the top 20 products.
- 20.54% from the top 50 products.
- 31.37% from the top 100 products.

The results indicate that recorded merchandise revenue
was distributed across a broad product portfolio rather
than being dominated by a small number of products.

### 5.2 Highest-Contributing Products

The ten highest-contributing products by recorded
merchandise revenue in the sensitivity scenario were:

| Product | Recorded Revenue |
|---|---:|
| REGENCY CAKESTAND 3 TIER | £174,484.74 |
| WHITE HANGING HEART T-LIGHT HOLDER | £104,340.29 |
| PARTY BUNTING | £99,504.33 |
| JUMBO BAG RED RETROSPOT | £94,340.05 |
| RABBIT NIGHT LIGHT | £66,964.99 |
| PAPER CHAIN KIT 50'S CHRISTMAS | £64,952.29 |
| ASSORTED COLOUR BIRD ORNAMENT | £59,094.93 |
| CHILLI LIGHTS | £54,117.76 |
| PICNIC BASKET WICKER SMALL | £51,426.62 |
| POPCORN HOLDER | £51,354.02 |

### 5.3 Product Revenue Concentration

The cumulative revenue analysis identified the following
distribution:

| Revenue Threshold | Products Required | Share of Products |
|---|---:|---:|
| 50% | 248 | 6.33% |
| 80% | 843 | 21.53% |
| 90% | 1,352 | 34.53% |
| 95% | 1,821 | 46.50% |

Approximately 21.53% of product stock codes accounted
for 80% of recorded merchandise revenue.

This indicates some product-level revenue concentration,
although the distribution does not follow an exact
80/20 relationship.

### 5.4 Data Quality Considerations

The investigation identified unusual transactions that
could distort product rankings.

Two exceptionally large transactions were independently
verified as having corresponding full-value cancellations.
They were excluded from the sensitivity scenario.

Additionally, stock code 22502 was associated with more
than one product description. Product rankings were
therefore aggregated by stock code, while recognizing
that different descriptions may represent different
product entries.

### 5.5 Business Interpretation

Management could use these findings to:

- Monitor products contributing the largest recorded
  revenue.
- Review inventory requirements for important products.
- Investigate products with consistently low sales.
- Examine product descriptions and stock-code consistency.
- Avoid relying on revenue alone when evaluating
  product profitability.

The dataset does not provide product costs or margins,
so the analysis cannot determine which products are
the most profitable.

## 6. Monthly Sales Performance

### 6.1 Monthly Revenue Trends

Monthly recorded merchandise revenue varied throughout
the observation period.

The highest monthly revenue occurred in November 2011,
at £1,458,925.53.

The lowest occurred in December 2011, at £447,247.00.
However, December 2011 is an incomplete month, with
transactions recorded only through December 9.

Other notable monthly results included:

| Month | Recorded Revenue | Unique Invoices |
|---|---:|---:|
| September 2011 | £1,031,430.36 | 1,821 |
| October 2011 | £1,107,449.54 | 2,008 |
| November 2011 | £1,458,925.53 | 2,753 |

### 6.2 Revenue and Invoice Activity

Between September and November 2011:

- Recorded merchandise revenue increased by 41.46%.
- Unique invoice count increased by 51.18%.
- Units sold increased by 31.61%.
- Recorded revenue per invoice decreased by 6.44%.

The increase in revenue coincided with a larger number
of invoices and more units sold. Average recorded revenue
per invoice declined over the same period.

These observations describe the pattern in the data and
do not establish the cause of the changes.

### 6.3 Monthly Data Coverage

The dataset does not cover every calendar day in the
observation period.

December 2010 and December 2011 are incomplete months.
January begins on January 4, April ends on April 28,
and October begins on October 2.

December 2011 ends on December 9, making direct
comparison with full calendar months inappropriate.

### 6.4 Business Interpretation

Management could investigate:

- The increase in invoice activity during September
  to November 2011.
- Product demand during the highest-revenue months.
- Whether changes in invoice volume corresponded with
  changes in units purchased.
- Seasonal patterns across comparable complete periods.

The historical dataset alone cannot establish whether
these patterns would recur in future periods.

## 7. Customer Analysis

### 7.1 Customer Overview

The analysis identified 4,334 customers with available
CustomerIDs in the sensitivity dataset.

Customer-level analysis was restricted to records with
non-missing CustomerIDs. Consequently, the results do not
represent the entire customer population.

### 7.2 Customer Purchasing Frequency

Customer activity was measured by the number of distinct
calendar months in which each identifiable customer
recorded a purchase.

Key findings:

- 1,638 customers (37.79%) were active in one month.
- 2,696 customers (62.21%) were active across multiple
  months.
- The average customer was active in 3.01 months.
- 84 customers (1.94%) were active in 12 or 13 months.

This measures observed multi-month purchasing activity,
not a formal customer retention rate.

### 7.3 Customer Revenue Concentration

The top 10 identifiable customers contributed 16.56%
of identifiable-customer recorded merchandise revenue.

The top 20 contributed 22.78%.

The cumulative concentration analysis found:

| Revenue Threshold | Customers Required | Share of Customers |
|---|---:|---:|
| 50% | 232 | 5.35% |
| 80% | 1,166 | 26.90% |
| 90% | 1,941 | 44.79% |
| 95% | 2,628 | 60.64% |

This suggests that revenue was distributed across a
relatively broad identifiable customer base, although
a smaller group contributed a substantial share.

### 7.4 Data Limitations

Approximately 24.9% of merchandise records had missing
CustomerIDs.

Customers whose identifiers were missing could not
be reliably included in customer-level grouping.

The analysis therefore describes identifiable-customer
purchasing patterns rather than the complete customer
population.

### 7.5 Business Interpretation

Management could consider:

- Studying purchasing patterns among repeat-month customers.
- Investigating the characteristics of high-revenue customers.
- Developing customer segmentation using purchasing
  frequency and recorded revenue.
- Evaluating retention initiatives using more complete
  customer identification data.

These recommendations require further investigation.
The observed data does not establish the effectiveness
of any particular retention strategy.

## 8. Geographical Performance Analysis

### 8.1 Revenue Distribution by Country

The retailer's recorded merchandise revenue was heavily
concentrated in the United Kingdom.

The country-level analysis covered 38 countries.

| Country | Recorded Revenue | Revenue Share |
|---|---:|---:|
| United Kingdom | £8,518,060.96 | 84.78% |
| Netherlands | £283,889.34 | 2.83% |
| EIRE | £276,404.30 | 2.75% |
| Germany | £205,569.89 | 2.05% |
| France | £184,768.74 | 1.84% |

### 8.2 Domestic and International Contribution

- United Kingdom revenue share: 84.78%.
- International revenue share: 15.22%.
- Top five countries combined revenue share: 94.24%.

The results indicate substantial dependence on the
United Kingdom market.

International revenue was distributed across a number
of smaller markets, with the Netherlands, EIRE, Germany,
and France among the largest contributors after the UK.

### 8.3 Business Interpretation

Management could consider:

- Investigating the commercial potential of established
  international markets.
- Comparing order volumes and customer activity across
  countries.
- Evaluating shipping, fulfilment, and operating costs
  before considering expansion.
- Monitoring geographical revenue concentration as
  part of business risk analysis.

The dataset does not contain market-size, shipping-cost,
marketing-cost, or country-level profitability data.
Therefore, revenue contribution alone cannot establish
the attractiveness of international expansion.

## 9. Key Business Insights and Recommendations

### Insight 1: Strong Geographical Revenue Concentration

The United Kingdom contributed 84.78% of recorded
merchandise revenue, while international markets
contributed 15.22%.

**Recommendation:**
Management could investigate opportunities in
established international markets, particularly the
Netherlands, EIRE, Germany, and France. Before
committing resources, it should evaluate shipping
costs, market demand, and country-level profitability.

### Insight 2: Broad Product Revenue Distribution

The top 10 products contributed 8.17% of recorded
merchandise revenue. Approximately 21.53% of stock
codes accounted for 80% of revenue.

**Recommendation:**
Management could monitor high-contributing products
while reviewing inventory requirements and sales
performance across the wider product portfolio.
Product-level cost and margin data would be needed
to identify the most profitable products.

### Insight 3: Customer Revenue Is Distributed Across
a Broad Identifiable Customer Base

The top 20 identifiable customers contributed
22.78% of identifiable-customer recorded revenue.

**Recommendation:**
Management could develop customer segments based
on purchasing frequency and recorded revenue.
Further investigation could identify opportunities
for customer engagement and retention initiatives.

### Insight 4: Repeat-Month Purchasing Activity

Approximately 62.21% of identifiable customers
recorded purchases across multiple calendar months.

**Recommendation:**
Management could examine repeat purchasing patterns
and compare the purchasing behaviour of one-month
and multi-month customers. More complete customer
identification would improve the reliability of
this analysis.

### Insight 5: Increased Activity Toward November 2011

From September to November 2011, recorded revenue
increased by 41.46%, while invoice count increased
by 51.18%.

**Recommendation:**
Management could investigate the products, customer
segments, and transaction patterns associated with
this increase. Comparable historical periods could
help assess whether similar patterns recur.

### Overall Management Perspective

The analysis highlights geographical concentration,
product portfolio distribution, customer purchasing
patterns, and changes in monthly sales activity.

These findings can guide further investigation and
support more informed decisions. They should not
be treated as proof of profitability, causation,
or future performance.

## 10. Limitations

The findings of this project should be interpreted
within the following limitations:

1. **Historical data:** The dataset covers December 2010
   to December 2011 and does not represent current
   retail conditions.

2. **Missing customer identifiers:** Approximately
   24.9% of merchandise records have missing CustomerIDs,
   limiting customer-level analysis.

3. **Cancellation reconciliation:** Two fully cancelled
   original transactions were independently verified
   and excluded in the sensitivity scenario. Broader
   cancellation matching remained ambiguous, so the
   resulting revenue is not definitive net sales.

4. **Duplicate records:** Exact duplicate occurrences
   were investigated but not automatically removed
   because identical rows may represent repeated
   transaction lines.

5. **Profitability:** Product costs, operating expenses,
   shipping costs, and profit margins are unavailable.
   Recorded revenue cannot establish profitability.

6. **Incomplete periods:** December 2010 and December
   2011 are incomplete, limiting direct monthly
   comparisons.

7. **Descriptive analysis:** The project identifies
   patterns and associations in historical transactions.
   It does not establish causation or predict future
   business performance.

## 11. Conclusion

This project examined historical online retail
transactions to understand product performance,
monthly sales activity, customer purchasing patterns,
and geographical revenue distribution.

The analysis identified a substantial concentration
of recorded merchandise revenue in the United Kingdom,
alongside a broad distribution of revenue across
products and identifiable customers.

It also highlighted repeat-month purchasing activity
among identifiable customers and an increase in
invoice activity and recorded revenue toward
November 2011.

The data-quality investigation was an important part
of the project. It helped identify unusual transactions,
special transaction codes, duplicate records, and
cancellation-related limitations that could affect
analytical conclusions.

Overall, the project demonstrates a structured
approach to transforming raw transaction records
into documented business insights and practical
management recommendations.

Further analysis using current transaction data,
complete customer identifiers, and product cost
information could provide a stronger basis for
operational and strategic decisions.
