# Kenyan E-Commerce Sales Performance Analysis

## 1. Business Problem

A retail business can accumulate thousands of transactions without having a clear, timely view of what those transactions mean for the business.

This is particularly important when sales are recorded across different products, orders and sales channels over several years. Although the underlying transaction data contains information about sales, quantities, discounts, returns and other charges, raw records alone do not readily answer the questions a business decision-maker needs to ask.

For this project, the problem was framed as follows:

> **How can three years of retail transaction data be transformed into a practical performance-monitoring tool that helps a decision-maker understand overall sales performance, changes over time, sales-channel contribution and the financial significance of returns?**

The objective was therefore not simply to visualise historical transactions. The objective was to turn transactional data into an **interactive decision-support view** that makes important patterns easier to monitor and investigate.

---

## 2. Business Questions

The analysis was organised around four areas of retail performance.

### Overall performance

- What are the business's total net sales?
- How many orders were processed?
- How many units were transacted?
- What is the average order value?

### Sales performance over time

- How does net sales change over the three-year period?
- Are there periods of stronger or weaker performance that deserve further investigation?

### Sales-channel performance

- Which sales channels contribute most to net sales?
- Is sales performance concentrated in particular channels?

### Returns

- What is the monetary value recorded as returns?
- How significant are returns relative to the overall sales activity?

These questions determine what is measured and displayed in the dashboard.

---

## 3. Data

The project uses an authentic retail transaction dataset covering **November 2020 to October 2023** for a Kenya-based business specialising in baby products and related items.

The dataset contains transaction-level information including:

- Order ID
- Sale ID
- Date
- Order
- Transaction type
- Sale type
- Sales channel
- Product
- Net quantity
- Gross sales
- Discounts
- Returns
- Net sales
- Shipping
- Taxes
- Total sales

The dataset therefore provides sufficient information to examine both operational activity and financial performance.

The underlying transaction data is not redistributed in this repository. The original public dataset is referenced as the source.

---

## 4. Analytical Approach

The project followed a simple decision-oriented workflow:

**Business problem → Data assessment → Data preparation → Measures → Dashboard → Interpretation**

### Step 1: Understand the data

Before building the dashboard, the dataset was reviewed to understand its structure, field definitions, completeness and consistency.

The assessment established that the loaded dataset contained approximately **29,000 transaction records** and **13,257 distinct orders**.

Particular attention was given to financial fields and the relationship between sales, discounts, returns and net sales.

A reconciliation check was also used to verify the financial relationship:

**Gross sales − Discounts + Returns − Net sales**

The check was used to confirm that the relevant transaction-level financial fields were internally consistent before they were used in the dashboard.

### Step 2: Prepare the data

The data was prepared in Power Query before being used for reporting.

The preparation focused on:

- confirming appropriate data types;
- inspecting missing values;
- checking identifier fields;
- understanding categorical fields;
- preserving the source data where there was insufficient evidence to justify imputation or restructuring;
- validating important financial relationships.

Not every field was forced into the analysis. For example, fields with substantial missingness or ambiguous business meaning were not treated as core dashboard dimensions without sufficient justification.

### Step 3: Define analytical measures

The dashboard uses DAX measures to calculate the main performance indicators rather than relying only on raw columns.

The principal measures are:

| Measure | Definition |
|---|---|
| Total Net Sales | Sum of `Net sales` |
| Total Orders | Distinct count of `Order ID` |
| Total Quantity | Sum of `Net quantity` |
| Total Returns | Sum of the `Returns` field |
| Average Order Value | Total Net Sales ÷ Total Orders |

The resulting overall figures were approximately:

- **Net Sales:** KSh 82.50 million
- **Orders:** 13,257
- **Quantity:** 38,773
- **Returns:** -KSh 689.65 thousand
- **Average Order Value:** KSh 6,223

The `Returns` field is treated as a **monetary field**, consistent with the dataset's variable information and observed values. The negative sign is retained from the source data rather than arbitrarily changing its sign.

### Step 4: Build the reporting layer

Power BI was selected because the problem requires users to interact with the data rather than consume a fixed static report.

The dashboard provides:

- KPI cards for high-level monitoring;
- a monthly net-sales trend for temporal analysis;
- a sales-channel comparison for understanding revenue contribution;
- a date-range slicer for interactive period analysis.

The model was intentionally kept simple because the reporting requirement is centred on a single transactional dataset and a focused executive overview. A more complex dimensional model would be appropriate for a larger production BI environment with multiple fact tables, dimensions or more extensive analytical requirements.

---

## 5. Dashboard

The final dashboard is designed around a simple management question:

> **How is the business performing, and where should management investigate further?**

The KPI section provides an immediate view of overall performance, while the trend and channel visuals provide context for understanding what is driving that performance.

The date slicer allows the user to move from the overall three-year view to a specific period without rebuilding the analysis.

**Dashboard preview**

![Kenyan E-Commerce Sales Performance Dashboard](https://github.com/Justo-sys/Kenyan-E-Commerce-Sales-Analysis/blob/main/Screenshot/dashboard.png)

---

## 6. What the Dashboard Provides

The dashboard is deliberately structured so that each visual has a business purpose.

| Business need | Dashboard component |
|---|---|
| Monitor overall sales performance | Net Sales KPI |
| Monitor order activity | Orders KPI |
| Monitor transaction volume | Quantity KPI |
| Monitor monetary returns | Returns KPI |
| Understand typical order size | Average Order Value KPI |
| Identify changes over time | Monthly Net Sales Trend |
| Compare sales channels | Sales by Channel |
| Examine specific periods | Date-range slicer |

The dashboard therefore acts as an interactive summary layer over the underlying transactional data.

---

## 7. Findings and Interpretation

The dashboard establishes the baseline performance of the business over the period analysed.

The business generated approximately **KSh 82.5 million in net sales across 13,257 orders**, giving an average order value of approximately **KSh 6,223**.

The next level of interpretation comes from examining how those results vary over time and across sales channels. The dashboard is therefore designed not to treat the KPI totals as the final answer, but as the starting point for investigation.

For example, a period of unusually high or low sales should lead to a further question:

> **What changed during that period?**

Likewise, a channel contributing a large share of revenue raises a different management question:

> **Is the concentration strategically desirable, or does it create dependence on one channel?**

Similarly, the return value should be considered in relation to sales activity rather than interpreted in isolation.

The purpose of the dashboard is therefore to move the user from **measurement to investigation**.

---

## 8. Business Value

The value of the dashboard is not the number of charts it contains. Its value comes from reducing the effort required to answer recurring management questions.

Instead of manually aggregating transaction records to examine different periods or channels, a decision-maker can use one interactive reporting view to:

- monitor current performance;
- compare periods;
- identify changes in sales;
- compare sales channels;
- observe the financial impact of returns; and
- determine where deeper investigation may be required.

This makes the dashboard a practical **business intelligence layer** over the transaction data.

---

## 9. Limitations

This analysis is intentionally focused on sales performance.

The dataset does not by itself provide enough information to explain *why* sales increased or decreased. For example, changes in marketing activity, inventory availability, pricing strategy, customer acquisition costs, customer demographics or operational disruptions cannot be established from the available fields alone.

Therefore, the dashboard is best interpreted as a **performance-monitoring and investigation tool**, rather than a complete causal explanation of business performance.

The analysis also does not attempt to infer information that is not directly supported by the dataset.

---

## 10. Tools

- Power BI
- Power Query
- DAX

---

## 11. Dataset Source

The project uses the public **Ecommerce Sales Data** dataset by Kanini Gichuyia, covering November 2020 to October 2023.

The dataset describes transaction activity for a Kenya-based business specialising in baby products and related items.

The original dataset is available through Kaggle.

## 12. Methodology

The analytical methodology is documented [here](documentation/methodology.md).

## 13. Dashboard

![Kenyan E-Commerce Sales Performance Dashboard](screenshots/dashboard.png)
