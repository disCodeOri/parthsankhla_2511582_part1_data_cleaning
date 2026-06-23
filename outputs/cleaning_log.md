# Cleaning Log

## Issues Found
- 20 exact duplicate row copies were removed.
- 12 order IDs had conflicting duplicate records and were flagged.
- 48 discount-related records required review or filling.
- 21 records had date-related issues.
- 310 records were excluded or flagged due to order/payment status.
- 80 records had sales or profit calculation mismatches.

## Cleaning Actions Performed
- Preserved the original raw workbook as `data/raw_orders.xlsx`.
- Created `data/cleaned_orders.xlsx` as the separate cleaned version.
- Standardized text fields by trimming spaces, removing stray special characters, normalizing repeated spaces, and applying consistent title case.
- Standardized `order_date` and `ship_date` into real date values.
- Added `shipping_delay_days`, `order_month`, and `order_year`.
- Filled missing `region` and `ship_mode` values as `Unknown` and flagged those records.
- Filled missing discounts as 0 only when core sales fields were available.
- Calculated `calculated_sales`, `calculated_profit`, and `profit_margin`.
- Added `data_quality_flag`, `include_completed_sales`, and `issue_notes`.

## Business Rules Applied
- Completed-sales summaries include only records with `order_status = Completed`, `payment_status = Paid`, and no invalid data flag.
- Cancelled, returned, failed, refunded, and pending records are retained in the cleaned dataset but excluded from completed-sales summaries.
- Negative discounts and discounts above 50% are flagged as invalid.
- Ship dates before order dates are flagged as invalid shipping records.
- Conflicting duplicate order IDs are retained for review and flagged.

## Assumptions
- Slash dates such as `07/27/2024` were interpreted as MM/DD/YYYY.
- Dash dates such as `28-11-2024` were interpreted as DD-MM-YYYY unless already in ISO YYYY-MM-DD format.
- Discounts above 50% were treated as unusually high because the provided rules did not specify a numeric threshold.
- Completed sales require both completed order status and paid payment status.

## Records Removed or Flagged
- Removed records: 20 exact duplicate row copies.
- Flagged records: 407 warning or invalid records.
- Invalid records: 109.
- Warning records: 298.

## Limitations
- Conflicting duplicate order IDs were not automatically resolved because the correct business record cannot be inferred safely.
- High discount threshold is an assumption and should be confirmed with business stakeholders.
