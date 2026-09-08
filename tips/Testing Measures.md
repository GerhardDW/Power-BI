# DAX Measure Testing Guide (DAX Studio)

## Purpose
Verify each measure returns correct results — at the grand total and within filter context.

## Setup
1. Open the PBIX in Power BI Desktop.
2. External Tools → DAX Studio (connects to the live model).
3. Confirm the connection shows your model name.

## Test 1 — Overall (grand total)
Run the measure with no filters and compare to a trusted source (SQL, Excel, manual count).

```dax
EVALUATE
ROW("Result", [Your Measure])
```
✅ Pass if the number matches the source of truth.

## Test 2 — By filter context
Slice by one dimension value and reconcile the parts back to the total.

```dax
EVALUATE
CALCULATETABLE(
    ROW("Result", [Your Measure]),
    'Dim'[Column] = "Value"
)
```
✅ Pass if the slice is correct AND all slices sum back to the grand total.

## Test 3 — Edge cases
- Blanks / nulls in the source
- Date boundaries (start/end of period)
- Filters that should return zero or BLANK

## Test Case Log
| # | Measure | Filter | Expected | Actual | Pass/Fail | Notes |
|---|---------|--------|----------|--------|-----------|-------|
| 1 | | (none) | | | | grand total |
| 2 | | Dept = X | | | | filter context |
