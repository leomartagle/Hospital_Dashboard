# 🏥 XYZ Medical Center – Emergency Room Operational Analytics

![Power BI Dashboard](screenshots/dashboard_overview.png)

## 📌 Executive Summary
This interactive Power BI dashboard provides an end-to-end operational overview of patient volume, wait times, admission rates, and satisfaction metrics for **XYZ Medical Center**. Designed for hospital operations leadership, it identifies peak ER emergency hours, specialist referral bottlenecks, and patient demographic distributions to optimize staffing and reduce wait times.

---

## 🔑 Key Insights & Business Impact
* **Peak ER Demand:** Analysis reveals highest operational stress during afternoon peak windows, enabling targeted nurse and physician shift alignment.
* **Referral Bottlenecks:** **General Practice** accounts for the largest referral volume (**~1.8K patients**), highlighting key departments for process streamlining.
* **Wait Time & Satisfaction:** Tracked average wait times (**35.3 mins**) alongside patient satisfaction scores (**4.99 / 5.0**) across age groups and gender categories.

---

## 🛠️ Technical Stack & Features
* **Tool:** Power BI Desktop
* **Data Modeling:** Custom `Dim_Calendar` star-schema model with 1-to-many relationships.
* **DAX Formulas:** Advanced dynamic measures for date hierarchies, time intelligence, and custom column sorting (`Hour Sort`, `Year Month Sort`).
* **Visualizations:** 
  * Custom heat-map Matrix visual for Peak ER hours (Day of Week vs. Hour of Day).
  * Smooth continuous Line Chart for monthly patient volume trends.
  * Stacked Bar & Column charts for demographic segment breakdowns.

---

## 📊 Data Model & DAX Snippets

### Dynamic Calendar Table (`Dim_Calendar`)
```dax
Dim_Calendar = 
VAR MinDate = DATEVALUE( MIN('Hospital ER Data'[Patient Admission Date]) )
VAR MaxDate = DATEVALUE( MAX('Hospital ER Data'[Patient Admission Date]) )
RETURN
ADDCOLUMNS (
    CALENDAR ( MinDate, MaxDate ),
    "Year", YEAR ( [Date] ),
    "Month Name", FORMAT ( [Date], "MMMM" ),
    "Month Number", MONTH ( [Date] ),
    "Year Month", FORMAT ( [Date], "YYYY MMM" ),
    "Year Month Sort", YEAR ( [Date] ) * 100 + MONTH ( [Date] ),
    "Quarter", "Q" & FORMAT ( [Date], "Q" ),
    "Day of Week", FORMAT ( [Date], "dddd" ),
    "Day of Week Sort", WEEKDAY ( [Date], 2 )
)
