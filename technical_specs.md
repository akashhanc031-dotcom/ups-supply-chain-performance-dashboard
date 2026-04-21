# Technical Specifications

## 1. Data Cleaning & Transformation (Power Query)
- **Header Standardization:** Fixed inconsistent naming conventions in the raw source.
- **Data Type Correction:** Converted date strings to datetime objects and cost/revenue to currency.
- **EDA:** Analyzed distribution of delivery days to identify outliers.

## 2. Calculated Columns (Logic)
- **Profit:** `[Revenue] - [Cost]`
- **Delivery_Days:** `DATEDIFF([ship_date], [delivery_date], DAY)`
- **Delay_Flag:** `IF([delivery_date] > [expected_date], "Delayed", "On-Time")`

## 3. Key Measures (DAX)
- **Total Revenue:** `SUM(Table[Revenue])`
- **Total Profit:** `SUM(Table[Profit])`
- **Total Deliveries:** `COUNTROWS(Orders)`
- **Delayed Deliveries** `CALCULATE([Total Deliveries], Orders[Delay_Flag] = "Delayed")`
- **Delay %** `DIVIDE([Delayed Deliveries], [Total Deliveries])`
