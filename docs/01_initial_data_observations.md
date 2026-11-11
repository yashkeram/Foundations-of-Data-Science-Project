# Initial Data Understanding — Observations

## 1. Dataset Dimensions and Date Coverage

The Online Retail dataset contains **541,909 records and 8 columns**.

The dataset covers transactions from **1 December 2010 to 9 December 2011**.

The eight columns are InvoiceNo, StockCode, Description, Quantity, InvoiceDate, UnitPrice, CustomerID, and Country.

The dataset includes transaction-level information that can support product, customer, country, and time-based business analysis.

## 2. Missing Values and Duplicate Records

| Column | Missing values |
|---|---:|
| CustomerID | 135,080 |
| Description | 1,454 |
| StockCode | 0 |
| InvoiceNo | 0 |
| Quantity | 0 |
| InvoiceDate | 0 |
| UnitPrice | 0 |
| Country | 0 |

**Total duplicate rows:** 5,268, counting duplicate occurrences after the first occurrence.

Missing CustomerID values may limit customer-level analysis, while missing product descriptions may affect product identification. Duplicate transaction lines require further investigation before removal.

## 3. Unusual Transaction Records

| Category | Records |
|---|---:|
| Cancellation invoice rows | 9,288 |
| Negative quantity rows | 10,624 |
| Zero or negative unit price rows | 2,517 |

These records may represent cancellations, product returns, free items, accounting adjustments, or other transaction events. Their business meaning must be investigated before deciding how to treat them.

## 4. Questions Requiring Investigation Before Cleaning

1. Do all invoices beginning with the letter C represent cancellations?
2. How many negative quantity records are associated with cancellation invoices?
3. What do negative quantities without a cancellation prefix represent?
4. Why do some transactions have zero or negative unit prices?
5. Are the duplicate rows genuine duplicate entries or repeated purchases within the same invoice?
6. How much do missing CustomerID values affect customer-level analysis?
7. How would excluding cancellations, returns, and unusual prices change recorded revenue?
8. Should records with missing product descriptions be retained when their StockCode is available?

## 5. Preliminary Conclusion

The dataset is sufficiently large for historical retail performance analysis, but it contains missing values, repeated records, cancellations, negative quantities, and unusual prices.

No records have been removed at this stage.

The next stage will investigate these data-quality issues, establish transparent cleaning rules, and compare key business metrics before and after cleaning.

**Data integrity principle:** The original raw dataset will remain unchanged. Any cleaning and transformation will be performed on a separate working copy, with each decision documented and justified.

## 6. Stage 2 — Data Quality Investigation Results

The investigation identified the following:

| Category | Count |
|---|---:|
| Cancellation invoice rows | 9,288 |
| Negative quantity rows | 10,624 |
| Negative quantities with cancellation prefix | 9,288 |
| Negative quantities without cancellation prefix | 1,336 |
| Zero-price records | 2,515 |
| Negative-price records | 2 |
| Duplicate occurrences | 5,268 |
| Rows belonging to duplicate groups | 10,147 |

### Key Observations

1. All 9,288 cancellation-prefixed records also have negative quantities.
2. An additional 1,336 negative quantity records do not have cancellation prefixes and require further investigation.
3. Both negative-price records are classified as "Adjust bad debt", suggesting accounting adjustments rather than ordinary product transactions.
4. There are 2,515 records with zero unit prices. Their business purpose remains to be investigated.
5. The dataset contains 5,268 duplicate occurrences, involving 10,147 rows when all members of duplicate groups are counted.

### Preliminary Cleaning Considerations

- Cancellation records should be separated from ordinary sales.
- Negative quantities without cancellation prefixes should be investigated independently.
- Bad-debt adjustments should not be treated as ordinary product sales.
- Zero-price records should be examined before exclusion.
- Duplicate records should be checked against transaction details before removal.

No records have been deleted or modified at this stage.

## 7. Investigation of Negative Quantities Without Cancellation Prefixes

A total of 1,336 records contain negative quantities without invoice numbers beginning with C.

### Quantity Statistics

| Metric | Value |
|---|---:|
| Records | 1,336 |
| Mean quantity | -154.91 |
| Median quantity | -30 |
| Minimum quantity | -9,600 |
| Maximum quantity | -1 |

### Description Analysis

The most frequent descriptions include:

- Check: 120 records
- Damages: 45 records
- Damaged: 42 records
- ?: 41 records
- Sold as set on dotcom: 20 records
- Thrown away: 9 records
- Unsaleable, destroyed: 9 records
- Wet damaged: 5 records
- Smashed: 4 records
- Missing: 3 records

### Interpretation

The descriptions suggest that these records may represent internal inventory adjustments, damaged stock, missing goods, stock disposals, or other operational corrections rather than conventional customer returns.

Many of the inspected records also have zero unit prices and missing CustomerIDs.

These interpretations require further verification. The records will remain in the raw dataset and will not automatically be classified as customer returns.

### Preliminary Decision

Negative quantities without cancellation prefixes will be kept in a separate investigation category until their impact on revenue and inventory-related metrics is understood.

## 8. Financial Impact of Non-Cancellation Negative Quantity Records

Further investigation of the 1,336 negative quantity records without cancellation prefixes revealed:

| Attribute | Result |
|---|---:|
| Total records | 1,336 |
| Zero unit price | 1,336 |
| Positive unit price | 0 |
| Negative unit price | 0 |
| Missing CustomerID | 1,336 |
| Identified CustomerID | 0 |
| Calculated line revenue | £0.00 |

### Interpretation

All 1,336 records have zero unit prices and missing CustomerIDs. Consequently, their calculated transaction revenue is zero.

These records appear consistent with operational or inventory adjustments rather than ordinary revenue-generating sales.

However, zero recorded revenue does not mean zero business impact. Damaged, missing, or discarded inventory may represent an economic loss that cannot be quantified using this dataset alone.

### Preliminary Treatment

These records will be excluded from the primary positive-sales analysis but preserved in a separate operational-adjustment category for documentation and further investigation.

## 9. Investigation of Zero-Price Transactions

A total of 2,515 records have a unit price of zero.

### Quantity Classification

| Category | Records |
|---|---:|
| Positive quantities | 1,179 |
| Negative quantities | 1,336 |
| Zero quantities | 0 |

### Customer Identification

| Category | Records |
|---|---:|
| Missing CustomerID | 2,475 |
| Identified CustomerID | 40 |

None of the zero-price records have cancellation-prefixed invoice numbers.

### Description Analysis

Frequently occurring descriptions include:

- Check: 159
- Damages: 45
- Damaged: 43
- Found: 25
- Sold as set on dotcom: 20
- Adjustment: 16
- Thrown away: 9
- Unsaleable, destroyed: 9
- Amazon: 8

Several records have missing descriptions.

### Interpretation

The zero-price records appear to contain a mixture of operational adjustments, damaged or discarded inventory, unidentified items, and potentially free or promotional goods.

The positive-quantity records require additional investigation because a positive quantity does not necessarily indicate a revenue-generating sale.

### Preliminary Treatment

Zero-price records will be retained in the raw dataset and excluded from the primary positive-revenue sales analysis. Their descriptions and transaction characteristics will be investigated separately.

The 40 records with identified CustomerIDs will also be reviewed before determining their treatment in customer-level analysis.

## 10. Investigation of Positive-Quantity, Zero-Price Records

A total of 1,179 records contained positive quantities but a unit price of zero.

Key observations:

- The average quantity was 61.58 units, while the median was 3 units.
- The maximum recorded quantity was 12,540 units, an unusually large value that requires further investigation.
- 592 records had missing product descriptions.
- Only 40 records had an identified CustomerID.
- Descriptions included product names, "amazon", "Manual", "check", "found", and "adjustment".

These records may represent complimentary or promotional goods, incomplete transaction records, or operational and administrative entries. However, the dataset does not provide enough information to confirm their exact purpose.

**Treatment decision:** Preserve all records in the raw dataset. Exclude zero-price records from the primary revenue-generating product analysis, while retaining them in a separate category for data-quality review. Do not classify them as confirmed free promotions or sales without additional evidence.

## 11. Duplicate Records and Revenue Impact

The dataset contained 5,268 exact duplicate occurrences, belonging to 4,879 distinct duplicate groups. These records were identical across all eight original columns.

A comparison of recorded revenue produced the following results:

| Metric | Result |
|---|---:|
| Original records | 541,909 |
| Exact duplicate occurrences | 5,268 |
| Records after deduplication | 536,641 |
| Original recorded revenue | £9,747,747.93 |
| Revenue after deduplication | £9,726,006.95 |
| Revenue difference | £21,740.98 |

Removing exact duplicate occurrences would reduce recorded revenue by approximately 0.223%.

However, identical transaction lines do not conclusively establish that the records are accidental duplicates. Some may represent repeated transaction entries.

**Treatment decision:** Preserve the original dataset and retain exact duplicates in the primary working dataset initially. Use a separate deduplicated version for sensitivity analysis. Report the revenue difference transparently so readers can understand the effect of this data-cleaning decision.

## 12. Investigation of Manual and Bad-Debt Entries

### Manual entries (StockCode M)

The dataset contained 571 manual entries:

| Classification | Records | Recorded value |
|---|---:|---:|
| Negative | 244 | -£146,784.46 |
| Zero | 6 | £0.00 |
| Positive | 321 | £78,110.27 |
| **Net** | **571** | **-£68,674.19** |

Several manual entries contained unusually high values. Some positive and negative entries had matching or similar amounts across nearby invoices, suggesting possible corrections, reversals, or accounting adjustments.

However, the dataset does not provide sufficient information to establish the exact purpose of every manual entry.

### Bad-debt entries (StockCode B)

Three records were identified:

- One positive entry of £11,062.06.
- Two negative entries of £11,062.06 each.
- Net recorded value: -£11,062.06.

These entries are accounting adjustments rather than ordinary merchandise transactions.

**Treatment decision:** Exclude Manual and Bad Debt entries from merchandise-level sales and product rankings. Preserve them in the original dataset and report them separately. Their recorded values should not be interpreted as business profit or loss.

## 13. Cancellation Matching and Revenue Reconciliation

An investigation was conducted to identify original merchandise transactions corresponding to cancellation records.

A preliminary matching process compared customer ID, stock code, absolute quantity, unit price, and transaction date. Within a 24-hour matching window, 679 cancellation records were matched to earlier positive transaction records.

However, 12 original transaction rows were matched more than once, demonstrating that the matching method could reuse the same original record. Inspection revealed repeated cancellation lines and multiple cancellation invoices with overlapping transaction details.

Two exceptional transactions were independently verified:

- **PAPER CRAFT, LITTLE BIRDIE:** Invoice 581483 recorded 80,995 units (£168,469.60), followed 12 minutes later by cancellation invoice C581484 for the same quantity and value.
- **MEDIUM CERAMIC TOP STORAGE JAR:** Invoice 541431 recorded 74,215 units (£77,183.60), followed 16 minutes later by cancellation invoice C541433 for the same quantity and value.

Both transactions therefore have corresponding full-value cancellations in the recorded data.

### Analytical decision

The preliminary matching results were not used to automatically remove original transaction records. The matching method does not reliably establish one-to-one invoice relationships in all cases.

The merchandise dataset retains positive non-cancellation records, including the two exceptional transactions. Their influence will be examined through sensitivity analysis, and the cancellation limitation will be disclosed in the final report.

This preserves the original transaction evidence while avoiding unsupported assumptions about which purchases were cancelled.