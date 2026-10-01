# Bank Loan Analysis – Power BI & SQL

 The project evaluates key performance indicators (KPIs) such as total loan applications, funded amounts, cash collections, interest rates, and debt-to-income (DTI) metrics across different loan statuses, geographic regions, and loan purposes. 

---

## Project Overview

The core objective of this project is to assist financial stakeholders in monitoring lending operations and assessing overall loan portfolio risk. 

* **Business Problem:** Financial institutions need visibility into loan portfolio trends, cash inflows versus outflows, borrower debt levels, and loan default rates to make data-driven lending and risk-management decisions.
* **Data Analyzed:** Historical loan dataset covering 38,576 borrower applications, including loan amounts, payment history, interest rates, DTI, loan purpose, borrower employment length, state locations, and repayment statuses.
* **Tool Usage:**
  * **SQL:** Executed queries to extract, filter, aggregate, and calculate Month-over-Month (MoM) performance and Key Performance Indicators (KPIs).
  * **Power BI:** Built multi-page interactive dashboards with custom DAX measures, slicers, and visual breakdowns to present findings effectively.

---

## Business Objectives

The project addresses several key business questions:

1. What is the total number of loan applications, total funded amount, and total cash amount collected?
2. What are the Month-to-Date (MTD) and Month-over-Month (MoM) performance metrics for applications, funding, and collections?
3. What is the average interest rate and average Debt-to-Income (DTI) ratio across borrowers?
4. How do **Good Loans** (*Fully Paid*, *Current*) compare against **Bad Loans** (*Charged Off*) in terms of funded amount, collections, and application percentages?
5. How do loan applications, funding, and collections vary by month, state, loan term, borrower employment length, and loan purpose?

---

## Dataset

* **Source File:** `financial_loan.csv`
* **Dataset Size:** 38,576 rows | 24 columns
* **Primary Key:** `id` (Unique identifier per loan application)

### Key Columns Description:

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `id` | Integer | Unique identifier for each loan application. |
| `loan_amount` | Integer | Total principal amount requested/funded for the loan. |
| `total_payment` | Integer / Decimal | Total amount collected from the borrower to date. |
| `loan_status` | Text | Repayment status (*Fully Paid*, *Charged Off*, *Current*). |
| `issue_date` | Date | Date when the loan was funded/issued. |
| `int_rate` | Decimal | Interest rate assigned to the loan. |
| `dti` | Decimal | Debt-to-Income ratio of the borrower. |
| `address_state` | Text | Borrower's state of residence. |
| `emp_length` | Text | Duration of employment reported by the borrower. |
| `purpose` | Text | Stated reason/category for the loan request. |
| `term` | Text | Duration of the loan (36 months vs. 60 months). |
| `grade` / `sub_grade` | Text | Credit risk grading assigned by the bank. |

---

---

## SQL Analysis

The SQL script `Bank_Loan_Analysis_File.sql` contains queries executed to answer overall and MTD/PMTD business queries.

### SQL Concepts Applied:
* **`SELECT` / `COUNT` / `SUM` / `AVG`:** Used for global aggregations (Total Applications, Total Funded, Total Received, Average Rates).
* **`WHERE` Filtering:** Applied to isolate specific months (`MONTH(issue_date) = 12` for MTD, `MONTH(issue_date) = 11` for PMTD) and loan statuses.
* **`GROUP BY` & `ORDER BY`:** Used to group performance by `loan_status`, `MONTH(issue_date)`, `address_state`, `term`, `emp_length`, and `purpose`.
* **`CASE` Statements:** Used to classify loans into **Good Loan** (*Fully Paid* / *Current*) vs. **Bad Loan** (*Charged Off*) categories.
* **Type Conversion:** Used `CAST` and date functions to extract months and calculate exact percentages.

---

## Key KPIs

| KPI Metric | Metric Value | MTD (Dec) Value | PMTD (Nov) Value | MoM Growth (%) |
| :--- | :--- | :--- | :--- | :--- |
| **Total Loan Applications** | **38,576** | **4,314** | **4,035** | **+6.91%** |
| **Total Funded Amount** | **$435,757,075** | **$53,981,425** | **$47,754,825** | **+13.04%** |
| **Total Amount Received** | **$473,070,933** | **$58,074,380** | **$50,132,030** | **+15.84%** |
| **Average Interest Rate** | **12.05%** | **12.36%** | **11.94%** | **+3.52%** |
| **Average DTI Ratio** | **13.33%** | **13.67%** | **13.30%** | **+2.78%** |

---

## Dashboard Overview

The Power BI solution (`Bank Loan file.pbix`) consists of three detailed dashboard pages:

### 1. Summary Dashboard
* **Primary Goal:** High-level performance tracking for executive stakeholders.
* **Key Features:** Top KPI cards (Applications, Funded Amount, Received Amount, Avg Int Rate, Avg DTI) with MTD MoM indicators.
* **Good vs. Bad Loan Section:** Donut chart and grid visuals highlighting Good vs. Bad loan applications, funded amounts, and received amounts.
* **Loan Status Grid:** Detailed summary table categorizing *Fully Paid*, *Charged Off*, and *Current* loans.

### 2. Overview Dashboard
* **Primary Goal:** Interactive exploratory analysis across multiple temporal and demographic dimensions.
* **Visuals Included:**
  * **Monthly Trend (Line Chart):** Application and funding trends across months.
  * **Regional Analysis (Filled Map):** Loan metrics distributed by US state (`address_state`).
  * **Term Analysis (Donut Chart):** Distribution between 36-month and 60-month terms.
  * **Employee Length Breakdown (Bar Chart):** Metrics by borrower tenure.
  * **Purpose Breakdown (Bar Chart):** Loans categorized by debt consolidation, credit card, home improvement, etc.

### 3. Details Dashboard
* **Primary Goal:** Granular record-level table view for operational validation.
* **Features:** Full tabular dataset view with interactive slicing controls (State, Grade, Purpose) to inspect individual loan records.

---

### Dashboard Preview
![Dashboard Preview Page 1](./Dashboard%20Preview/Dashboard%20Preview%20Page1.png)

![Dashboard Preview Page 2](./Dashboard%20Preview/Dashboard%20Preview%20Page2.png)

![Dashboard Preview Page 3](./Dashboard%20Preview/Dashboard%20Preview%20Page3.png)

## Project Structure

```text
Bank Loan Analysis/
│
├── Bank Loan file.pbix
├── Bank_Loan_Analysis_File.sql
├── financial_loan.csv
│
├── Dashboard Preview/
│   ├── Dashboard Preview Page1.png
│   ├── Dashboard Preview Page2.png
│   └── Dashboard Preview Page3.png
│
└── README.md
```

---

## How to Run the Project

1. **SQL Scripts:**
   * Load `financial_loan.csv` into your SQL Server database as table `bank_loan_data`.
   * Open `Bank_Loan_Analysis_File.sql` in SQL Server Management Studio (SSMS) or any SQL client.
   * Execute queries to verify KPI aggregations.

2. **Power BI Dashboard:**
   * Download and install **Power BI Desktop**.
   * Open `Bank Loan file.pbix`.
   * Ensure data source paths point to `financial_loan.csv` if prompting for refresh.
   * Interact with slicers across the **Summary**, **Overview**, and **Details** pages.

---

## Key Insights of Project

1. **High Overall Portfolio Performance:** Good loans (*Fully Paid* and *Current*) represent **86.18%** of total applications (33,243 applications) and **$370.22M** in funded capital.
2. **Net Collection Surplus:** The institution has collected **$473.07M** in total payments against **$435.76M** in funded principal, yielding an overall positive return driven by healthy interest accruals on good loans.
3. **Bad Debt Loss Exposure:** **13.82%** of loans were **Charged Off** (5,333 applications). Total funding for charged-off loans was **$65.53M**, with only **$37.28M** collected, resulting in a **$28.25M net principal loss**.
4. **Risk Profile Correlation:** Charged-off loans exhibited higher average interest rates (**13.88%**) and higher average DTI ratios (**14.00%**) compared to fully paid loans (**11.64%** avg interest rate and **13.17%** avg DTI).
5. **Positive Month-over-Month Growth:** MTD (December) loan applications grew by **+6.91%** MoM, funded amounts grew by **+13.04%** MoM, and cash collected grew by **+15.84%** MoM.
