# Methodology

## 1. Analytical Objective

The purpose of the analysis was to convert raw retail transaction records into an interactive performance-monitoring dashboard.

The analysis was guided by a business problem rather than by the capabilities of a particular software tool. The central question was:

> **How can transaction data be used to help a retail decision-maker understand business performance, identify important changes over time, compare sales channels and monitor returns?**

This led to four analytical areas:

1. overall sales performance;
2. performance over time;
3. sales-channel contribution; and
4. return activity.

---

## 2. Data Understanding

The dataset contains transaction-level records from November 2020 to October 2023.

The main variables used in the analysis were:

- `Order ID` — identifies the customer order;
- `Sale ID` — identifies an individual sale record;
- `Date` — transaction date;
- `Sale type` — type of sale transaction;
- `Sales channel` — channel through which the transaction was conducted;
- `Product` — product involved in the transaction;
- `Net quantity` — recorded transaction quantity;
- `Gross sales` — sales before relevant adjustments;
- `Discounts` — discount amount;
- `Returns` — recorded monetary return amount;
- `Net sales` — resulting net sales amount;
- `Shipping` — shipping amount;
- `Taxes` — tax component;
- `Total sales` — total recorded sales amount.

The dataset was treated as a transactional dataset in which multiple records can belong to the same order. Consequently, order volume was measured using a **distinct count of Order ID**, rather than a simple row count.

---

## 3. Data Quality Assessment

Before reporting, the data was assessed for structural and quality issues.

The assessment considered:

- number of records;
- uniqueness of identifiers;
- missing values;
- data types;
- categorical fields;
- financial field consistency; and
- plausibility of important values.

The analysis established that repeated `Order ID` values were expected because an order can contain multiple sales records.

Fields with substantial missingness or unclear analytical meaning were not automatically imputed or transformed. This was an intentional decision to avoid introducing unsupported assumptions into the analysis.

A financial reconciliation check was also performed using:

**Gross sales − Discounts + Returns − Net sales**

This was used as an internal consistency check before relying on the financial measures in the dashboard.

---

## 4. Data Preparation

Power Query was used as the data-preparation layer.

The preparation stage focused on ensuring that:

- numerical fields were treated as numerical values;
- identifiers were treated appropriately;
- the transaction date was recognised as a date/time field;
- categorical variables were retained in a form suitable for analysis;
- missingness was understood before deciding whether a field should be used;
- the source data was not unnecessarily altered.

The objective was not to clean the dataset until every imperfection disappeared. The objective was to produce a reliable analytical dataset while preserving information that may be meaningful and avoiding unsupported assumptions.

---

## 5. Measure Design

The main business indicators were implemented as DAX measures.

### Total Net Sales

```DAX
Total Net Sales =
SUM(Sales[Net sales])