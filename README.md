# 📊 PhonePe Transaction Analysis (2024–2026) — Power BI

An end-to-end personal data analytics project: I exported my own PhonePe (UPI) transaction history, cleaned it, modelled it, and built an interactive Power BI dashboard to understand **when, how often, and how much** I spend.

> Practice on your own data — it's the most honest dataset you'll ever analyse.

---

## 🎯 Objectives

- Understand overall spending vs. incoming money (debit vs. credit)
- Find monthly and weekday spending patterns
- Spot outliers and concentration (a few recipients taking a big share of spend)
- Segment transactions by time of day (Morning / Afternoon / Evening)
- Practice the full workflow: **clean → model → DAX → visualise → report**

---

## 🗂️ Dataset

Personal PhonePe transaction statement (PDF/export converted to a table), covering **2024–2026**.

| Column | Description |
|---|---|
| `Date` | Transaction date |
| `Time` | Transaction time |
| `Transaction Details` | Payee / payer description (e.g. "Paid to …") |
| `Transaction Type` | Debit or Credit |
| `Amount` | Transaction amount (₹) |
| `Year`, `Month`, `Month Number` | Derived date fields (Month sorted by Month Number) |
| `Weekdays`, `Week Number` | Derived day-of-week fields (Weekdays sorted by Week Number) |
| `Time of Day` | Calculated column: Morning / Afternoon / Evening (DAX) |

**Size:** 2,083 transactions

> 🔒 **Privacy note:** The raw transaction file is **not** included in this repository because it contains personal financial information. Screenshots and the report show aggregated results only.

---

## 🛠️ Tools & Skills

- **Power BI Desktop** — data model, visuals, slicers, report pages
- **Power Query** — cleaning and transformation
- **DAX** — measures and calculated columns
- **Data modelling** — sort-by-column, date hierarchies

---

## 📈 Dashboard Overview

**Page 1 – Phone Pay Transaction Analysis**
- KPI cards: Total Transactions, Total Credit, Total Debit
- Year slicer (2024 / 2025 / 2026) and **Day Shift** slicer (Time of Day)
- Monthly Payment Analysis (area chart)
- Transaction Type Analysis (bar) and Transaction Type Comparison (donut)
- Weekdays Payment Analysis (column chart)
- Transaction Details table ranked by payment amount

**Page 2 – Payments Table View** — detailed transaction table

> Add your screenshot here: `![Dashboard](images/dashboard.png)`

---

## 🔍 Key Findings

| Finding | Detail |
|---|---|
| Transactions analysed | **2,083** |
| Total debit | **₹3,04,730** |
| Total credit | **₹6,568** |
| Debit share of value | **97.89%** (credit 2.11%) |
| Peak month | **August — ₹1,06,434**, about **4× the overall monthly average** |
| Lowest months | March, July, November (each under ₹12,000) |
| Highest spend day | **Friday — ₹87,783**, followed by Sunday (₹73,558) |
| Lowest spend day | **Wednesday — ₹19,528** |
| Concentration | A single recipient accounts for **over 60%** of total debit value |

**Takeaways**
1. The account works almost entirely as an **outgoing payment channel**.
2. **August is a clear outlier** — driven by one large payment, not a general trend.
3. Spending is **concentrated on Friday and Sunday**.
4. Outside August, monthly movement is irregular with no strong seasonal trend.

---

## 🧮 DAX Used

**Time of Day (calculated column)**

```dax
Time of Day = 
VAR hr = HOUR([Time])
RETURN
SWITCH(
    TRUE(),
    hr >= 5 && hr < 12, "Morning",
    hr >= 12 && hr < 17, "Afternoon",
    "Evening"
)
```

**Time of Day Sort (controls Morning → Afternoon → Evening order)**

```dax
Time of Day Sort = 
SWITCH(
    [Time of Day],
    "Morning", 1,
    "Afternoon", 2,
    "Evening", 3
)
```

Then: *Column tools → Sort by column → Time of Day Sort*.

**Sorting Weekdays correctly:** select `Weekdays` → *Column tools → Sort by column → Week Number*.

---

## 🚀 How to Open

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/)
2. Open `Phone Pay Analysis.pbix`
3. Use the **Year** and **Day Shift** slicers to explore

*(If you fork this project, replace the data source with your own PhonePe statement.)*

---

## 💡 What I Learned

- Calculated **columns** need row context — `[Time]` inside a *measure* throws an error
- Text fields (month and weekday names) need a **numeric sort column** to display in calendar order
- Even a small personal dataset can surface real, actionable patterns

---

## 📁 Repository Structure

```
├── Phone Pay Analysis.pbix
├── PhonePe_Transaction_Report.docx
├── images/
│   └── dashboard.png
└── README.md
```

---

## 👤 Author

**Aman Kumar Sri Mali** — Data Analyst
Skills: Python · SQL · Excel · Power BI

🔗 LinkedIn: *add your profile link*

⭐ If you found this useful, give the repo a star!
