# 🚀 Loan Default Analysis & Financial Risk Dashboard

Welcome to the **Loan Default Analysis** project! This is an end-to-end **Power BI** analytics solution for analyzing loan risk, default trends, and applicant demographics across a large financial portfolio.  

![ETL](https://img.shields.io/badge/ETL-4CAF50?style=flat-square) ![Data Gateway](https://img.shields.io/badge/Gateway-FFAA00?style=flat-square) ![Visualization](https://img.shields.io/badge/Visualization-00BCD4?style=flat-square) ![MS Excel](https://img.shields.io/badge/MS_Excel-217346?style=flat-square&logo=microsoft-excel&logoColor=white) ![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=microsoft-sql-server&logoColor=white) ![Power BI](https://img.shields.io/badge/PowerBI-0078D7?style=flat-square&logo=power-bi&logoColor=white) ![DAX](https://img.shields.io/badge/DAX-FF4F00?style=flat-square&logo=microsoft-power-bi&logoColor=white) ![Incremental Refresh](https://img.shields.io/badge/Incremental_Refresh-009688?style=flat-square) ![Dataflow](https://img.shields.io/badge/Dataflow-0078D7?style=flat-square&logo=microsoft-azure&logoColor=white)

<img width="1303" height="755" alt="Screenshot 2026-02-16 132246" src="https://github.com/user-attachments/assets/2ecca0ed-e1c1-41ca-900f-d45712b7302a" />
<img width="1292" height="757" alt="Screenshot 2026-02-16 165244" src="https://github.com/user-attachments/assets/2d52a1fa-2357-4714-85c0-d7e8db5cd513" />
<img width="1411" height="823" alt="Screenshot 2026-02-16 162850" src="https://github.com/user-attachments/assets/0875042e-35eb-4319-88a9-92b963b2464e" />

---

## 📖 Project Overview
Financial institutions face significant risks from loan defaults. This project demonstrates:

* Secure data connectivity via **On-Premises Data Gateway**  
* Automated **Incremental Refresh** for large datasets  
* Advanced **DAX modeling** for dynamic KPIs  
* Interactive visualizations for **risk profiling and demographic insights**  

**Dataset:** 255,347 loan records covering multiple years, income brackets, and employment types.

---

## ⭐ STAR Method Summary

**Situation:** Need to monitor loan portfolio risk and identify high-risk demographics.  

**Task:** Build a scalable, automated BI solution with interactive dashboards.  

**Action:**  
* Configured **DF1 Gateway** for cloud-to-local data refresh.  
* Built **Dataflows** with **Incremental Refresh** (5 years stored, 10 days refreshed).  
* Engineered **custom columns** for Age Groups & Income Brackets.  
* Developed advanced **DAX measures**: YOY Default Changes, YTD Loan Amounts, Median Loan by Segment.  
* Designed **3-page dashboard**: Loan Overview, Demographics, Financial Risk Metrics.  

**Result:**  
* Automated daily reporting at 6:30 AM  
* Identified high-risk segments: **Unemployed (3.39% default)**  
* Highlighted historical spike in defaults: **2016 (11.75%)**  
* Total loan portfolio visualized: **32.58 Billion**

---



## 🎯 Key KPIs & Insights

-- 1. Average Income by Employment Type
-- Calculates the average income per employment category while keeping the context
Average Income by Employment Type =
CALCULATE(
    AVERAGE('Loan_default'[Income]),
    ALLEXCEPT('Loan_default', 'Loan_default'[EmploymentType])
)


-- 2. YOY Default Loans Change
-- Computes Year-over-Year change in the number of defaulted loans
YOY Default Loans Change =
VAR CurrentYearDefaults =
    CALCULATE(
        COUNTROWS(FILTER('Loan_default', 'Loan_default'[Default] = TRUE())),
        'Loan_default'[Year] = YEAR(MAX('Loan_default'[Loan_Date_DD_MM_YYYY]))
    )
VAR PreviousYearDefaults =
    CALCULATE(
        COUNTROWS(FILTER('Loan_default', 'Loan_default'[Default] = TRUE())),
        'Loan_default'[Year] = YEAR(MAX('Loan_default'[Loan_Date_DD_MM_YYYY])) - 1
    )
RETURN
DIVIDE(CurrentYearDefaults - PreviousYearDefaults, PreviousYearDefaults, 0) * 100


-- 3. Income Brackets (Custom Column)
-- Segments applicants into Low, Medium, High income groups
Income Bracket =
SWITCH(
    TRUE(),
    'Loan_default'[Income] < 30000, "Low Income",
    'Loan_default'[Income] >= 30000 && 'Loan_default'[Income] < 60000, "Medium Income",
    'Loan_default'[Income] >= 60000, "High Income"
)




| KPI | Value | Visual |
| --- | --- | --- |
| **Total Loan Portfolio** | 32.58B | ![Loan Total](https://media.giphy.com/media/3ohs7KViFZxXfPbYp6/giphy.gif) |
| **Average Default Rate** | 11.6% | ![Default Rate](https://media.giphy.com/media/26tPplGWjN0xLybiU/giphy.gif) |
| **Highest Default Segment** | Unemployed: 3.39% | ![Employment Risk](https://media.giphy.com/media/3oKIPwoeGErMmaI43C/giphy.gif) |
| **Peak Default Year** | 2016: 11.75% | ![Trend Analysis](https://media.giphy.com/media/xT0GqF8eb9Zw9aMwH6/giphy.gif) |

**Insights:**  
* Employment stability correlates inversely with default risk.  
* High-income adults dominate the portfolio (21.73B of 32.58B).  
* Home & Business loans are the highest volume contributors.  
* Low credit score borrowers hold the highest median loans, highlighting potential risk.

---

## 🛠️ Technical Skills & Tools


**Demonstrated Skills:**  
* Data Connectivity & ETL (Power BI Gateway, Dataflows)  
* Advanced DAX (ALLEXCEPT, CALCULATE, SUMX, MEDIANX, YOY, YTD)  
* Incremental Refresh & Scheduled Automation  
* Dashboard Design: Decomposition Trees, Ribbon/Sankey Charts, Line/Area Charts  
* Performance Optimization for 250k+ rows  

---

## 🔄 Project Flow & Architecture


1. **Data Ingestion & Profiling** – Load raw financial and demographic data  
2. **Data Transformation** – Clean, format, and create custom columns  
3. **Modeling & DAX** – Calculate KPIs, segment bins, and time-intelligence measures  
4. **Visualization** – Build interactive dashboards across 3 report pages  
5. **Deployment & Automation** – Publish to Power BI Service with **gateway and scheduled refresh**

---

## 💡 Learnings & Impact

* **Optimization Matters:** Incremental Refresh saves processing time and reduces load.  
* **Gateway Management:** Learned secure cloud-to-local data connectivity and troubleshooting.  
* **Stakeholder-Focused Design:** Separate dashboards for Marketing vs Risk Officers ensures relevant insights.  
* **Business Impact:** Enabled data-driven decisions for loan approval strategy and risk mitigation.
 
---

## 📈 Conclusion

This project is a complete demonstration of **Power BI expertise**, **data-driven decision making**, and **financial risk analysis** at scale. It is production-ready, recruiter-friendly, and highlights **end-to-end analytics capabilities** from data ingestion to automated reporting.

---

## ✍️ Author

**Vignesh Raveendran**  
*Data Engineer / Data Analyst*  

[LinkedIn](https://www.linkedin.com/in/yourprofile) | [Portfolio](https://yourportfolio.com)



