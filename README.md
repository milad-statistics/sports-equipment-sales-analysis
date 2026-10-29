# Sports Equipment Sales Analysis

## Project Overview

This project explores sports equipment sales data in Excel using an **Ad
Hoc Analysis** approach. The goal is to investigate profit patterns
across suppliers, brands, categories, and time periods by asking focused
questions and building analytical views as needed.

This is **not a dashboard project**. The PivotTables, conditional
formatting, and chart created during the work are analytical tools used
to investigate the data, rather than components of a single final
dashboard.

## Dataset

-   **Source repository:**
    [mochen862/excel-data-analysis](https://github.com/mochen862/excel-data-analysis)
-   **Original workbook:** `data_analysis_exercise.xlsx`
-   The data includes sports equipment sales/profit information,
    including fields used for Category, Supplier, Brand, Year, Month,
    and Profit Month.

## Tools and Excel Features

-   Excel Tables
-   PivotTables
-   `SUMIFS`
-   Show Values As
-   Conditional Formatting
-   Line Chart
-   Slicer

## Analysis Workflow

### 1. Initial Data Exploration

The source data was reviewed and converted into an Excel Table to make
it easier to work with and reference in formulas.

The initial review identified: - 3 suppliers - 9 brands - 3 categories

### 2. Comparing Profit by Supplier and Brand Across Years

A PivotTable was created with the following layout:

  PivotTable Area   Field
  ----------------- -----------------
  Rows              Supplier, Brand
  Columns           Year
  Values            Sum of Profit

The value display was changed using **Show Values As → % Difference
From** to compare profit year over year.

#### Observation

The Grand Total row showed that 2021 was the only year with an increase
in total profit compared with the previous year. The overall trend in
the following years was downward.

The 2024 comparison requires caution: the dataset contains only five
months for 2024, while the other years contain all twelve months.
Therefore, comparing the total for 2024 with totals for complete years
is not an equivalent-period comparison and does not, by itself, prove
that business performance declined at the same rate.

### 3. Conditional Formatting for Profit Changes

Conditional Formatting was applied to the year-over-year
percentage-change results: - More positive values appear greener. - More
negative values appear redder.

This makes positive and negative changes easier to identify visually.

### 4. Comparing Each Brand's Share of Annual Profit

A second PivotTable was created with this layout:

  PivotTable Area          Field
  ------------------------ -----------------
  Rows / Chart Axis        Year
  Columns / Chart Legend   Brand
  Values                   Sum of Profit
  Show Values As           \% of Row Total

This displays each brand's share of the total profit for each year.

A line chart was created from this analysis, with a **Category slicer**
to filter the view by product category.

#### Observations

-   In the overall view across categories, Steel Power had the largest
    annual share in the chart.
-   When the Airbike category was selected, Apex Athletics had the
    largest share, while Sport & Sports had the smallest share.

These are observations about each brand's share of the annual total, not
necessarily its absolute profit or growth rate. If profit values or
annual totals are negative, percentage-of-total results need careful
interpretation.

### 5. Calculating Profit YTD

A new column named `Profit YTD` was added using `SUMIFS`.

It calculates cumulative profit from the beginning of the current year
through the current month, while matching the current row's: -
Category - Supplier - Brand - Year

The month condition uses a dynamic criterion such as `"<="&[@Month]`,
which includes months less than or equal to the current row's month. The
`&` joins the text comparison operator (`<=`) to the current row's month
value.

### 6. Calculating Profit MAT

A new column named `Profit MAT` was added for **Moving Annual Total**.

This measure sums profit over a rolling 12-month period ending in the
current month, within the relevant Category, Supplier, and Brand
grouping. Unlike YTD, it does not reset at the beginning of a calendar
year. Where a full 12 months of history are not available, the available
period may be shorter.

### 7. PivotTable for Moving Annual Total

A further PivotTable was created to inspect `Profit MAT`:

  PivotTable Area   Field
  ----------------- ---------------------------
  Filters           Year and Month
  Rows              Supplier, Brand, Category
  Values            Sum of Profit MAT

This view allows the moving annual profit measure to be examined for
different suppliers, brands, and categories at selected points in time.

## Key Findings So Far

-   The data contains 3 suppliers, 9 brands, and 3 categories.
-   The year-over-year profit comparison showed 2021 as the only year
    with an increase in total profit compared with the preceding year.
-   Total profit comparisons for 2024 are limited by the fact that only
    five months are present for that year.
-   Steel Power had the largest annual share in the overall brand-share
    view.
-   Within the Airbike category, Apex Athletics had the largest share
    and Sport & Sports the smallest share.
-   YTD and MAT provide complementary views: YTD measures profit
    accumulated within the current year, while MAT measures profit over
    a moving 12-month period.

## Limitations and Interpretation Notes

-   **Partial year:** 2024 contains only five months, so its total
    should not be directly compared with totals for full years. A
    like-for-like comparison of the first five months across years would
    be more appropriate.
-   **Percentage of Row Total:** This shows a brand's share of the
    year's total profit; it is not the same as absolute profit or
    year-over-year growth. Results require extra care if negative profit
    values or negative annual totals are present.
-   **MAT history:** A complete moving 12-month total requires twelve
    months of available data for the relevant grouping.

## Project Status

The current work focuses on exploratory, question-driven analysis in
Excel. The project is documented as an **Ad Hoc Analysis**, not as a
final dashboard deliverable.
