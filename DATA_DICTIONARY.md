# Data Dictionary — UCI Online Retail

| Column | Meaning | Initial considerations |
|---|---|---|
| `InvoiceNo` | Unique invoice/transaction identifier | Values beginning with `C` indicate cancellations |
| `StockCode` | Product identifier | Treat as a code/category, not a measurement |
| `Description` | Product description | May contain missing or inconsistent text |
| `Quantity` | Number of units on an invoice line | Negative values may represent returns |
| `InvoiceDate` | Date and time of the transaction | Convert to datetime before time analysis |
| `UnitPrice` | Unit price in GBP | Inspect zero or unusual values |
| `CustomerID` | Customer identifier | Some records may have missing IDs |
| `Country` | Customer's country | Useful for geographic summaries |

## Derived measure

`LineRevenue = Quantity × UnitPrice`

This measure represents recorded line revenue in GBP. It is not profit and should not be described as profit.

## Questions to resolve during analysis

- Are there duplicate invoice lines?
- How many records have missing customer IDs or descriptions?
- How should cancellation invoices and negative quantities be represented?
- Are there zero or negative unit prices?
- Should customer-level analysis exclude records without customer IDs?

Do not make cleaning decisions until the raw data has been inspected and the impact of each decision is understood.
