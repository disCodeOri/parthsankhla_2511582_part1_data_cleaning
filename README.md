# Part 1: Business Data Cleaning, Validation & Excel Reporting

## Problem Summary
The task is to clean raw retail order-level data, validate business rules, document data quality issues, and create Excel summary reports for business review.

## Dataset Description
- Source file: `data/raw_orders.xlsx`
- Cleaned file: `data/cleaned_orders.xlsx`
- Raw rows: 932
- Rows after exact duplicate removal: 912

## Tools Used
- Node.js
- xlsx for raw workbook parsing
- ExcelJS for generated Excel workbooks

## Cleaning Steps Performed
- Preserved the raw workbook unchanged.
- Cleaned text fields including customer, segment, region, state, city, category, sub-category, ship mode, payment status, and order status.
- Standardized mixed date formats.
- Removed exact duplicate row copies.
- Flagged conflicting duplicate order IDs.
- Filled missing region and ship mode values as Unknown.
- Applied discount validation and filled missing discount values when valid.
- Added calculated sales, calculated profit, profit margin, shipping delay, order month, order year, and data quality fields.

## Business Rules Applied
- Missing region and ship mode values were filled as Unknown and flagged.
- Missing discount was treated as 0 only when other sales fields were valid.
- Negative discounts and discounts above 50% were flagged as invalid.
- Cancelled, failed, refunded, returned, and pending records were retained but excluded from completed-sales summaries.
- Ship dates before order dates were flagged as invalid.

## Summary of Data Quality Issues Found
| Metric | Count |
| --- | --- |
| Raw rows | 932 |
| Rows after exact duplicate removal | 912 |
| Clean records | 505 |
| Warning records | 298 |
| Invalid records | 109 |
| Completed sales records used in summaries | 539 |
| Non-completed/payment records excluded from completed-sales summaries | 373 |

## Summary of Final Pivot Reports
- Sales and profit by region
- Sales and profit by category and sub-category
- Order count by ship mode
- Profit margin by customer segment
- Refunded/cancelled/failed orders by region
- Monthly sales trend

## Key Business Insights
- South is the highest completed-sales region with sales of 1461555.75.
- Technology / Copiers has the strongest completed-sales profit contribution at 182201.13.
- Office Supplies / Labels needs review because it has the lowest profit contribution at 57988.76.
- 109 invalid records should be reviewed before using the dataset for final reporting.

## Assumptions and Limitations
- Slash dates were treated as MM/DD/YYYY and dash dates as DD-MM-YYYY unless ISO formatted.
- Discounts above 50% were considered unusually high.
- Conflicting duplicate order IDs were flagged rather than automatically removed.

## Screenshots Included
- `screenshots/raw_data_preview.png`
- `screenshots/cleaned_data_preview.png`
- `screenshots/pivot_summary_1.png`
- `screenshots/pivot_summary_2.png`
