# Adidas P&L Analysis — From Bloomberg export to reconciled multi-year financial statements

## Visual Overview
<img width="612" height="353" alt="image" src="https://github.com/user-attachments/assets/bd63b4d5-cedb-432a-87d5-471425b4ef7c" />


---

## Case Description
This project converts a raw Bloomberg income statement export for adidas AG (FY2019–FY2023) into a fully reconciled, analysis-ready Profit & Loss statement. The source data contained hierarchical indentation, non-breaking spaces, and mixed subtotal structures. The aim was to clean and map the data into a standard financial model, calculate key performance metrics, and produce an executive-level visualization of revenue mix and EBIT margin trends.

---

## Tasks
- Extract and clean Bloomberg data for 5 fiscal years.
- Build a structured P&L with **Wholesale**, **Retail**, **Other Businesses**, and **Adjustment** as revenue segments.
- Calculate **Gross Profit**, **EBIT**, margins, and CAGR.
- Reconcile all subtotals against the source file.
- Create a stacked revenue chart with EBIT% on a secondary axis.

---

## Steps / Bookings
**Exact postings from source data (USD million):**

**FY2019**
- Wholesale: 10,003.70  
- Retail: 2,657.80  
- Other Businesses: 1,789.06  
- Adjustment: 25.10  
  → Total Revenue: 14,475.66  
- Cost of Revenue: 7,882.76 → Gross Profit: 6,592.91  
- Operating Expenses: 6,121.58  
- Other Operating Revenue: 328.09  
- EBIT: 730.68  

**FY2023**
- Wholesale: 12,087.66  
- Retail: 4,577.37  
- Other Businesses: 2,584.90  
- Adjustment: 0.00  
  → Total Revenue: 19,249.93  
- Cost of Revenue: 9,696.69 → Gross Profit: 9,553.24  
- Operating Expenses: 8,215.62  
- Other Operating Revenue: 259.37  
- EBIT: 1,665.71  

---

## Trial Balance
| FY  | Wholesale  | Retail   | Other Businesses | Adjustment | **Total Revenue** | Cost of Revenue | **Gross Profit** | Operating Expenses | Other Op. Revenue | **EBIT**  |
|----:|-----------:|--------:|-----------------:|----------:|------------------:|----------------:|-----------------:|-------------------:|------------------:|----------:|
|2019 | 10,003.70  | 2,657.80| 1,789.06         | 25.10     | 14,475.66         | 7,882.76        | 6,592.91         | 6,121.58           | 328.09            | 730.68    |
|2020 | 10,853.04  | 3,169.28| 1,883.79         | 0.00      | 15,906.11         | 8,291.34        | 7,614.77         | 6,694.10           | 298.32            | 1,199.26  |
|2021 | 12,462.05  | 3,890.39| 2,197.22         | 0.00      | 18,549.66         | 9,737.11        | 8,812.55         | 7,751.54           | 265.95            | 1,326.96  |
|2022 | 12,259.54  | 4,337.26| 2,540.89         | 0.00      | 19,137.69         | 9,663.35        | 9,474.33         | 8,248.89           | 278.59            | 1,523.77  |
|2023 | 12,087.66  | 4,577.37| 2,584.90         | 0.00      | 19,249.93         | 9,696.69        | 9,553.24         | 8,215.62           | 259.37            | 1,665.71  |

**Checks:**
- Segments + Adjustment = Total Revenue (0 diff all years)  
- Gross Profit = Revenue − Cost of Revenue (±0.01)  
- EBIT = Gross Profit − Opex + Other Op. Revenue (exact match)  

---

## Financial Statements

### Income Statement (USD million)
| FY  | Revenue   | Cost of Revenue | **Gross Profit** | Operating Expenses | Other Op. Revenue | **EBIT**  | GP%    | EBIT%  |
|----:|----------:|----------------:|-----------------:|-------------------:|------------------:|----------:|-------:|-------:|
|2019 | 14,475.66 | 7,882.76        | 6,592.91         | 6,121.58           | 328.09            | 730.68    | 45.54% | 5.05%  |
|2020 | 15,906.11 | 8,291.34        | 7,614.77         | 6,694.10           | 298.32            | 1,199.26  | 47.87% | 7.54%  |
|2021 | 18,549.66 | 9,737.11        | 8,812.55         | 7,751.54           | 265.95            | 1,326.96  | 47.51% | 7.15%  |
|2022 | 19,137.69 | 9,663.35        | 9,474.33         | 8,248.89           | 278.59            | 1,523.77  | 49.51% | 7.96%  |
|2023 | 19,249.93 | 9,696.69        | 9,553.24         | 8,215.62           | 259.37            | 1,665.71  | 49.63% | 8.65%  |

---

## Mapping / Logic
**Source to Report:**
- Bloomberg “Revenue” → Total Revenue
- Product/Brand breakdown → Wholesale, Retail, Other Businesses, Adjustment
- “Cost of Revenue” → Cost of Revenue
- “Operating Expenses” → Operating Expenses
- “Other Operating Revenue” → Other Op. Revenue
- “Operating Income” → EBIT (control figure)

**Formulas (Excel):**

    Clean item names:
    =TRIM(SUBSTITUTE($A3,CHAR(160),""))

    Two-key lookup:
    =INDEX('IS source'!$1:$1048576,
           MATCH($C3,'IS source'!$A:$A,0),
           MATCH(D$2,'IS source'!$9:$9,0))

    Gross Margin %:
    =IFERROR([@Gross Profit]/[@Revenue],0)

    CAGR calculation:
    =([@FY2023]/[@FY2019])^(1/(5-1))-1

---

## How I Built It
- **Tools:** Microsoft Excel, Bloomberg terminal export
- **Techniques:** TRIM/SUBSTITUTE for non-breaking space cleanup, 2D INDEX/MATCH lookups, controlled subtotals, custom number formats, year-by-year integrity checks
- **Visualization:** Combo chart with stacked columns for revenue segments and EBIT% line (secondary axis)

---

## What I Learned
- Managing irregular Bloomberg export formatting without breaking lookups
- Designing multi-year P&L models with built-in reconciliation controls
- Combining revenue mix visuals with profitability KPIs for executive reporting
- Leveraging helper columns to standardize and clean raw financial data

---
