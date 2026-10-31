# Sales Performance Dashboard

Using Microsoft Excel, I analysed company sales data to uncover insights on revenue, profit, product performance, regional sales, salesperson results and payment behaviour. I cleaned the dataset, added calculated columns and conditional aggregations, built 14 PivotTables and PivotCharts, and designed an interactive dashboard with a City slicer that answers key questions about how the business is performing.

## Table of Contents

- [Dashboard Preview](#dashboard-preview)
- [Introduction](#introduction)
- [Data Overview and Dataset Structure](#data-overview-and-dataset-structure)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Calculated Columns and Formulas](#calculated-columns-and-formulas)
- [Dashboard Analysis](#dashboard-analysis)
- [Conclusion](#conclusion)
- [Recommendations](#recommendations)
- [Assumptions and Limitations](#assumptions-and-limitations)
- [Tools and Repository Structure](#tools-and-repository-structure)

## Dashboard Preview

![Sales Performance Dashboard](images/dashboard.png)

*[Replace with a fresh screenshot taken after Refresh All, so the Payment and Salesperson charts match this README.]*

## Introduction

A company needs to know what drives its revenue, what drives its profit, and where those two stories differ. Without this view, heavily discounted products look like success stories, weak markets go unnoticed, and sales effort is spread without evidence.

This project analyses a sales dataset using Microsoft Excel to answer practical questions about sales performance. The analysis aims to:

- Measure total revenue, profit, orders and units sold.
- Compare revenue and profit across categories, products, cities and salespeople.
- Classify orders by value (High Value or Standard) and by profit (High Profit or Standard Profit).
- Track how revenue, profit and orders changed from January to May 2026.
- Show how customers pay, by number of orders and by revenue.
- Highlight orders above ₦1,000,000 and let the reader filter the dashboard by city.

## Data Overview and Dataset Structure

The analysis uses one sales table, with one row per order. After cleaning, the data holds **49 orders**, **8 products** in **3 categories**, **7 cities** and **10 salespeople**, with order dates from 5 January to 28 May 2026.

### Sales (main table)

| Column | Description |
|---|---|
| Order ID | Unique identifier for each order |
| Order Date | Date the order was placed |
| Ship Date | Date the order was shipped |
| Salesperson | Salesperson who made the sale |
| City | City where the sale was made |
| Product | Product sold |
| Category | Electronics, Furniture or Accessories |
| Quantity Sold | Number of units sold |
| Unit Price | Selling price per unit before discount |
| Unit Cost | Cost per unit |
| Discount % | Discount given on the order |
| Gross Sales | Quantity × Unit Price |
| Discount Amount | Gross Sales × Discount % |
| Revenue | Gross Sales less Discount Amount |
| Total Cost | Quantity × Unit Cost |
| Profit | Revenue less Total Cost |
| Customer Type | Corporate or Retail |
| Payment Method | Card, Cash or Transfer |
| **Order Value Category** | *New column:* High Value or Standard |
| **Profit Status** | *New column:* High Profit or Standard Profit |

*[Check this table against your workbook's column headings and edit if any differ.]*

## Data Cleaning and Preparation

The cleaned dataset from Week 1 is the starting point for this analysis.

| Issue | Treatment |
|---|---|
| Order ORD035 had no payment method (shown as "Unknown") | Classified as **Card**, the most common method for Retail Electronics orders (5 of 8). Affects 1.8% of revenue |
| Orders ORD033, ORD034 and ORD045 have ship dates earlier than their order dates | Flagged in an *Invalid Ship Date* column and kept in all totals |
| Order ORD004 showed different salespeople in the data and the PivotTables | Corrected to **Tolu**, as recorded in the Sales sheet, and PivotTables refreshed |

*[Add any other Week 1 cleaning steps here, such as duplicates removed, blanks filled or text standardised.]*

## Calculated Columns and Formulas

**Order Value Category**

```
High Value  if Revenue >= 1,000,000
Standard    if Revenue <  1,000,000
```

**Profit Status**

```
High Profit      if Profit >= 250,000
Standard Profit  if Profit <  250,000
```

**Conditional aggregations**

| Question | Function | Result |
|---|---|---|
| Total Revenue from Electronics | `SUMIF` | ₦23,784,550 |
| Total Revenue in Lagos | `SUMIF` | ₦14,555,450 |
| Number of transactions paid by Card | `COUNTIF` | 19 |
| Electronics transactions by Corporate customers | `COUNTIFS` | 12 |

**Conditional formatting:** all Revenue values above ₦1,000,000 are highlighted (12 orders).

## Dashboard Analysis

This section explains each part of the dashboard, with the method and the insight it gives.

### 1. Headline KPIs

**Method:** Four cards show Total Revenue, Total Profit, Total Orders and Total Units Sold, calculated from the PivotTables.

The company recorded **₦43.25M** in revenue and **₦9.37M** in profit from **49 orders** and **591 units**, an overall profit margin of **21.7%**. The average order value is ₦882,692.

### 2. Revenue by Category

**Method:** A bar chart shows total revenue for each category, from a PivotTable on Category.

Electronics lead with ₦23.8M (55.0% of revenue), followed by Furniture at ₦10.2M and Accessories at ₦9.3M. Revenue alone is misleading here. Electronics earn only 15.6% margin and 39.7% of profit, while Accessories earn 36.0% margin and 35.6% of profit.

### 3. Top 5 Products by Revenue

**Method:** A bar chart shows the five highest-earning products, using a Top 5 filter on the product PivotTable.

Laptop leads with ₦11.7M, followed by Monitor (₦8.1M), Office Chair (₦5.4M), Desk (₦4.8M) and Printer (₦3.9M). Laptop has the lowest margin of all products at 10.9%, because discounts averaging 9.6% roughly halve its 20% list-price margin.

### 4. Revenue by City

**Method:** A bar chart shows total revenue for each city.

Lagos leads with ₦14.6M (33.7%), followed by Abuja at ₦8.8M, Port Harcourt at ₦4.8M, Ibadan at ₦4.4M, Enugu at ₦4.2M, Kano at ₦3.8M and Kaduna at ₦2.7M. Lagos and Abuja together make up 54.1% of revenue. Kaduna is the smallest market but has the best margin at 29.4%.

### 5. Monthly Revenue Trend

**Method:** A line chart plots revenue by month, using the Order Date grouped by month in a PivotTable.

| Month | Revenue | Profit | Orders |
|---|---|---|---|
| January | ₦7.61M | ₦1.66M | 11 |
| February | ₦8.32M | ₦1.80M | 10 |
| March | ₦9.70M | ₦2.09M | 10 |
| April | ₦7.55M | ₦1.53M | 8 |
| May | ₦10.08M | ₦2.29M | 10 |

Revenue grew from January to March, dipped 22% in April, then reached a five-month high in May. April had the fewest orders, so the dip came from lower sales volume rather than lower prices.

### 6. Revenue by Payment Method

**Method:** A pie chart shows each payment method's share of revenue.

Card accounts for ₦20.4M (47.1%) from 19 orders, Transfer for ₦13.6M (31.5%) from 17 orders, and Cash for ₦9.2M (21.4%) from 13 orders. All 23 corporate orders were paid by card or transfer, and cash was used only by retail customers.

### 7. Salesperson Performance

**Method:** A column chart shows total revenue for each salesperson.

Tolu leads with ₦5.83M, followed by Ada (₦4.79M), Chioma (₦4.66M) and Kunle (₦4.46M). Fatima is lowest at ₦2.69M but has the best margin on the team at 29.4%. Each salesperson has 5 orders except Seyi, who has 4.

### 8. Interactivity

**Method:** A City slicer is connected to all 14 PivotTables and their charts. The KPI cards update with it, so the whole dashboard can be filtered to a single city or a group of cities.

## Conclusion

The company is growing and profitable, with a 21.7% margin on ₦43.25M of revenue. The dashboard shows that the biggest opportunities are in selling better, not only selling more:

- **Mix:** Electronics bring in the most revenue, but Accessories earn almost as much profit.
- **Discounts:** Laptops and high-value orders give away much of their margin. The 12 orders of ₦1M or more make up 41.8% of revenue but only 29.4% of profit.
- **Geography:** Lagos and Abuja carry 54.1% of revenue, while smaller cities such as Kaduna, Enugu and Kano earn higher margins.
- **Timing:** Revenue is growing but uneven, with a dip in April.
- **Payments:** Card and transfer make up 78.6% of revenue.

## Recommendations

1. **Promote Accessories.** Sell them as add-ons to Electronics orders, since they earn more than twice the profit per naira.
2. **Set a discount ceiling.** Apply it to laptops and high-value orders, with approval required above it.
3. **Grow the smaller cities.** Invest in Kaduna, Kano and Enugu to reduce dependence on Lagos, while protecting Lagos and Abuja.
4. **Investigate April.** Find out whether stock, staffing or demand held sales back, and repeat what worked in May.
5. **Prioritise card and transfer for corporate buyers.** That is where large orders come from, and cash is a retail-only habit.

## Assumptions and Limitations

- The order with a missing payment method (ORD035) was classified as Card based on the most common method for similar orders. It is an assumption, not a recorded fact.
- Three orders have ship dates earlier than their order dates. They are flagged but kept in all totals.
- The data holds 49 orders over about five months, so the findings describe patterns and do not support statistical conclusions.
- Revenue is net of discounts. Profit is revenue less product cost only, with no other business costs such as delivery or salaries.
- Order ORD039 is absent from the dataset, so Seyi has four orders instead of five.

## How to View the Dashboard

- **Quick look:** see the screenshot above.
- **Full file:** download the `.xlsx` from the `excel/` folder and open it in Microsoft Excel. The slicer and PivotCharts need desktop Excel.

## Tools and Repository Structure

**Tools:** Microsoft Excel, PivotTables, PivotCharts, Slicers, Conditional Formatting, SUMIF, COUNTIF, COUNTIFS.

```
.
├── README.md
├── excel/      # Excel workbook with the dashboard
├── report/     # full written report (Word)
└── images/     # dashboard screenshots
```

## Author

Aisha Hamza | [LinkedIn]([add link]) | [Email]([add email])
