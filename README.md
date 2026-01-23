# Insightful Solutions: Employee Retention & Attrition Analysis

## Executive Summary
This project analyzes workforce data for "Insightful Solutions" to identify the root causes of employee turnover. The dataset covered **1,470 employees**, revealing a total attrition rate of **16% (237 employees)**.

The goal was to provide data-driven recommendations to the HR Director to improve retention strategies and reduce hiring costs.

---

## Key Insights & Findings

### 1. The Overtime "Burnout" Factor
* **Finding:** Overtime is the strongest predictor of attrition. Employees working overtime accounted for **54% of all departures**.
* **Impact:** The attrition count for overtime workers (127) was significantly higher than for non-overtime workers (110), despite overtime workers being a smaller group.

### 2. Income & Job Role Disparities
* **Income:** Attrition is highest among employees earning between **$2,000 - $3,000 monthly**. As income rises above $6,000, retention improves drastically.
* **Roles:** "Sales Representatives" and "Laboratory Technicians" showed the highest turnover rates, indicating potential dissatisfaction with compensation or workload in these specific roles.

### 3. Demographics (Age & Gender)
* **Age:** The workforce is predominantly aged 26-35, but attrition is disproportionately high in the **18-20 and 26-30 age brackets**.
* **Gender:** Male employees accounted for **63%** of the total attrition (150 departures) compared to 37% for females.

---

## Methodology & SQL Logic
*Note: The original raw data files are confidential. Below are the SQL structures used to extract these insights.*

I used **SQL** to clean the data and segment high-risk groups, and **Excel** for the final visualization.

### A. Identifying High-Risk Roles (SQL)
To find which job roles had the highest attrition rates, I grouped data by role and calculated the percentage of leavers.

```sql
-- Sample Query: Calculate Attrition Count by Job Role
SELECT
    JobRole,
    COUNT(EmployeeNumber) AS Total_Employees,
    SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) AS Attrition_Count,
    ROUND(SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(EmployeeNumber), 2) AS Attrition_Rate
FROM hr_data
GROUP BY JobRole
ORDER BY Attrition_Rate DESC;

-- Sample Query: Overtime vs. Attrition
SELECT
    OverTime,
    COUNT(*) as Total_Count,
    SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) as Leavers
FROM hr_data
GROUP BY OverTime;

## Recommendations
Based on the data, I proposed the following strategic actions to the HR Director:

1.  **Overtime Cap & Review**: Investigate the workload of Sales Reps and Lab Techs. Implement a "burnout warning" system for employees consistently logging overtime, as this group accounts for 54% of all attrition.
2.  **Compensation Adjustment**: Review salary bands for the $2,000 - $3,000 income bracket. The data shows this is a "danger zone" for turnover, suggesting entry-level pay may not be competitive.
3.  **Career Progression**: Implement clear career pathways for the 26-35 age group. Since attrition is high here, these employees are likely leaving for better growth opportunities elsewhere.

---

## Tools Used
* **SQL**: Used for querying specific demographic cuts, identifying high-risk job roles, and calculating aggregate attrition rates from the raw dataset.
* **Excel**: Used to generate the final pivot tables and visualizations (charts) presented in the report.
