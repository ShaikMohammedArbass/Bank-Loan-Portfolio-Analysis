## 🏦 Bank Loan Portfolio Analysis

An end-to-end Python analysis of a consumer loan portfolio — evaluating overall lending performance, and pinpointing exactly where and why loans default, across time, geography, term, grade, and purpose.

## Short Description

The **Bank Loan Portfolio Analysis** is a Python notebook (pandas, seaborn, matplotlib, plotly) built to evaluate a bank's loan book: how much has been funded and collected, what share of the portfolio is healthy vs. defaulted, and which segments carry the most credit risk. Rather than stopping at descriptive KPIs, the analysis is deliberately risk-focused — every volume metric (funded amount, applications, received amount) is paired with a charge-off-rate view, so the notebook answers "where is the money" as well as "where is the risk." This is intended for credit risk analysts, loan operations teams, and anyone evaluating portfolio-level lending performance.

## Tech Stack

The analysis was built using the following tools and libraries:

- **🐍 Python** — Core language for data loading, transformation, and analysis.
- **🐼 pandas / NumPy** — Data cleaning, aggregation, and MTD/date-based filtering logic.
- **📊 Matplotlib / Seaborn** — Static charts: trend lines, bar charts, donut chart.
- **🌐 Plotly Express** — Interactive treemap for the home-ownership breakdown.
- **📓 Jupyter Notebook** — Development and reporting environment, run end-to-end top to bottom.
- **📁 File Format** — `.ipynb` for the analysis, `.xlsx` for the source dataset.

## Data Source

*Source: Consumer loan-level dataset (`financial_loan.xlsx`).*

38,576 loan records issued in 2021, covering the borrower (state, employment length, home ownership), the loan itself (amount, term, purpose, grade, sub-grade, interest rate, installment), and the outcome (loan status, total payment received). A data-quality check confirmed no duplicate rows and only one column (`emp_title`) with missing values.

## Features / Highlights

- **Business Problem**

  Loan-level data on its own tells a bank how much it has lent and collected, but not *why* some loans default and others don't. Questions like:

  - What share of the portfolio is actually performing?
  - Does loan term, grade, or purpose predict default risk?
  - Are losses concentrated in specific states?

  ...require going a layer deeper than simple volume totals.

- **Goal of the Analysis**

  To build a reusable, well-documented notebook that:
  - Reports standard lending KPIs (funded amount, received amount, interest rate, DTI) both all-time and month-to-date.
  - Classifies the portfolio into Good Loans (Current/Fully Paid) vs. Bad Loans (Charged Off) and quantifies the gap between funded and recovered amounts.
  - Ranks default (charge-off) rate — not just volume — by state, term, grade, and purpose to isolate real risk drivers.

- **Walkthrough of Key Sections**

  - **Data Quality Check:** Confirms 0 duplicate rows, 1 column with missing values (`emp_title`), and sane ranges for interest rate (5.42%–24.59%) and DTI (0%–29.99%) before trusting any KPI built on top.
  - **Core KPIs (All-time & MTD):** Total Loan Applications, Total Funded Amount, Total Amount Received, Average Interest Rate, Average DTI — each with a December 2021 month-to-date companion figure.
  - **Good Loan vs. Bad Loan Metrics:** 86.18% of the portfolio is Good (Current/Fully Paid); 13.82% is Bad (Charged Off) — representing $65.53M funded against only $37.28M recovered.
  - **Monthly Trends (Line/Area Charts):** Funded amount, received amount, and application volume all trend upward through 2021, peaking in December.
  - **Regional Analysis (Horizontal Bar):** Funding by state, led by California, New York, and Texas.
  - **Term, Employment Length, Purpose, Home Ownership:** Funded-amount breakdowns by loan term (donut chart), employment length, loan purpose, and home ownership (interactive treemap).
  - **Key Findings — Default Rate by Segment:** Goes beyond volume to rank charge-off rate itself by state, purpose, term, and grade (states filtered to 50+ loans to avoid small-sample noise).

- **Business Impact & Insights**

  - **Term risk:** 60-month loans default at **22.34%** — more than double the rate of 36-month loans (**10.71%**) — making term length alone a strong underwriting signal.
  - **Grade risk:** Default rate rises almost monotonically from Grade A (**5.70%**) to Grade G (**31.31%**), validating the existing grading system while flagging the E/F/G tail as disproportionately risky.
  - **Purpose risk:** `small_business` loans default at **25.62%**, well above the portfolio average, followed by `renewable_energy` (18.09%) and `educational` (15.87%).
  - **Geographic concentration:** Nevada (20.95%), Alaska (19.23%), and South Dakota (17.46%) show the highest default rates among states with meaningful volume.
  - **Recommendation:** Underwriting or pricing tightening should prioritize the compounding case — 60-month, small-business-purpose loans in higher-risk states — rather than treating each risk factor independently.

## Screenshots / Demos

**Monthly Funded Amount Trend**

![Monthly Funded Amount Trend](screenshots/01-monthly-funded-amount-trend.png)

**Total Funded Amount by State**

![Total Funded Amount by State](screenshots/04-funded-amount-by-state.png)

**Total Funded Amount by Loan Term**

![Total Funded Amount by Loan Term](screenshots/05-funded-amount-by-term.png)

**Total Funded Amount by Loan Purpose**

![Total Funded Amount by Loan Purpose](screenshots/07-funded-amount-by-purpose.png)

*(Additional charts — received-amount trend, applications trend, employment length, and the interactive home-ownership treemap — are available by running the notebook.)*

## Repository Contents

| File | Description |
|---|---|
| `Bank-Loan-Portfolio-Analysis.ipynb` | Jupyter notebook with the full analysis, pre-executed with outputs and charts |
| `Bank-Loan-Dataset.xlsx` | Source dataset (38,576 loan records) |
| `screenshots/` | PNG exports of key charts from the notebook |

## How to Run

```bash
pip install pandas numpy matplotlib seaborn plotly openpyxl jupyter
jupyter notebook Bank-Loan-Portfolio-Analysis.ipynb
```

The notebook reads `Bank-Loan-Dataset.xlsx` from the same folder, so no path changes are needed — clone the repo and run top to bottom.
