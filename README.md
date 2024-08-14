# HR-Attrition-Dashboard-Project
Mysql and power Bi

## Table of Contents
1. [Project Outline](#project-outline)
2. [Introduction](#introduction)
3. [Data Cleaning and Preparation](#data-cleaning-and-preparation)
4. [Key Metrics Visualized in the Dashboard](#key-metrics-visualized-in-the-dashboard)
5. [Detailed Analysis](#detailed-analysis)
6. [SQL Queries](#sql-queries)
7. [Insights](#insights)
8. [Conclusion and Recommendations](#conclusion-and-recommendations)
9. [Dashboard View](#dashboard-view)

## 1. Project Outline

This project focuses on creating an HR Attrition Dashboard that visualizes key metrics related to employee attrition. The analysis was conducted using SQL and Power BI, with the goal of providing insights into workforce demographics, job satisfaction, attrition rates, and more. The insights from this dashboard are intended to help HR managers and company stakeholders make data-driven decisions to improve employee retention and overall HR strategies.

## 2. Introduction

The HR Attrition Dashboard is designed to provide a comprehensive view of the company's workforce, focusing on employee attrition, job satisfaction, and departmental distribution. The dashboard enables HR professionals and stakeholders to quickly identify areas of concern and opportunities for improvement in employee retention.

## 3. Data Cleaning and Preparation

The dataset was cleaned and prepared using SQL. Key steps included:

- **Cleaning the Age column**: The Age data was examined for inconsistencies, and any necessary corrections were made to ensure accurate representation.
- **Duplicate Check and Removal**: A check was performed to identify and remove any duplicate records.
- **Null Value Handling**: Null values were examined, and necessary actions were taken to either fill or exclude them, depending on the context.

## 4. Key Metrics Visualized in the Dashboard

- **Total Employees**: The dashboard shows that there are 1,470 total employees within the organization.
- **Active Employees**: Out of the total, 1,233 employees are currently active.
- **Average Employee Age**: The average age of the employees is approximately 36.92 years.
- **Average Employee Salary**: Although the salary analysis was not explicitly performed, the dashboard shows an average salary of 6,503.
- **Attrition Rate**: The overall attrition rate within the company is 16%.

## 5. Detailed Analysis

- **Number of Employees by Department**:
  - The majority of employees work in the Research and Development department (961 employees), followed by Sales (446 employees), and Human Resources (63 employees).

- **Attrition Rate by Department**:
  - The attrition rate is highest in Research and Development (38.55%), followed by Sales (35.59%), and Human Resources (25.86%).

- **Attrition by Gender**:
  - A total of 150 male employees and 87 female employees have left the company.

- **Job Satisfaction Rating by Job Role**:
  - This analysis shows the distribution of job satisfaction levels across different job roles, with Sales Executives having a notably high count of employees rating their job satisfaction as 4.

- **Number of Employees by Job Role**:
  - The dashboard visualizes the distribution of employees across various job roles, with the highest number in Sales Executive and Research Scientist positions.

- **Total Attrition by Job Role**:
  - The roles with the highest attrition include Laboratory Technician, Sales Executive, and Research Scientist, indicating potential areas for HR intervention.

## 6. SQL Queries

```sql
CREATE DATABASE hr_attrition;
USE hr_attrition;

SELECT * FROM Hr;

SET SQL_SAFE_UPDATES = 0;
ALTER TABLE hr
CHANGE COLUMN  `AGE` Age INT;
DESCRIBE Hr;

-- Calculate the total number of employees
SELECT COUNT(*) AS TotalEmployees FROM Hr;

-- Calculate the total number of employees who left (Attrition = 'Yes')
SELECT COUNT(*) AS TotalAttrition
FROM Hr
WHERE Attrition = 'Yes';

-- Calculate the average age of employees
SELECT AVG(Age) AS AverageAge
FROM Hr;

-- Count the number of male and female employees
SELECT Gender, COUNT(*) AS TotalGender
FROM Hr
GROUP BY Gender;

-- Calculates the average, maximum, minimum salaries and the range (difference between max and min)
SELECT AVG(MonthlyIncome) AS AverageSalary, 
       MAX(MonthlyIncome) AS MaximumSalary, 
       MIN(MonthlyIncome) AS MinimumSalary, 
       MAX(MonthlyIncome) - MIN(MonthlyIncome) AS SalaryRange
FROM Hr;

-- Calculate the data by department and calculate the average salary for each department
SELECT Department, AVG(MonthlyIncome) AS AverageSalary
FROM Hr
GROUP BY Department;

-- Group the data by department and count the number of employees who have left for each department
SELECT Department, COUNT(*) AS AttritionCount
FROM Hr
WHERE Attrition = 'Yes'
GROUP BY Department;

-- Analyze attrition by Gender
SELECT Gender, COUNT(*) AS AttritionCount
FROM Hr
WHERE Attrition = 'Yes'
GROUP BY Gender;

-- Calculate the total number of employees per department
SELECT Department, COUNT(*) AS TotalEmployeesPerDepartment
FROM Hr
GROUP BY Department;

-- Calculate the total number of employees per job role
SELECT JobRole, COUNT(*) AS TotalEmployeesPerJobRole
FROM Hr
GROUP BY JobRole;

-- Calculate overall attrition rate
SELECT 
    (SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*)) * 100 AS AttritionRate
FROM Hr;

-- Calculate the total number of employees, total number of employees who have left, and the attrition rate for each Job role.
SELECT 
    JobRole,
    COUNT(*) AS TotalEmployees,
    SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) AS TotalAttrition,
    (SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*)) * 100 AS AttritionRate
FROM Hr
GROUP BY JobRole;

-- Calculate the total number of employees, total number of employees who have left, and the attrition rate for each department
SELECT 
    Department,
    COUNT(*) AS TotalEmployees,
    SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) AS TotalAttrition,
    (SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*)) * 100 AS AttritionRate
FROM Hr
GROUP BY Department;

-- Count all employees where the attrition status is 'No', indicating they are still employed
SELECT COUNT(*) AS ActiveEmployees
FROM Hr
WHERE Attrition = 'No';

-- Group the data by the EducationField column and count the number of employees who have left for each educational field
SELECT EducationField, COUNT(*) AS AttritionCount
FROM Hr
WHERE Attrition = 'Yes'
GROUP BY EducationField;
```



## 7. Insights

- Focus on areas with high attrition rates, particularly within specific departments and job roles, to develop targeted retention strategies.
- Analyze job satisfaction ratings across roles to identify areas where employee engagement and satisfaction may be improved to reduce future attrition.

## 8. Conclusion and Recommendations

The HR Attrition Dashboard provides a clear overview of the key factors contributing to employee turnover. By focusing on areas with high attrition rates, particularly within specific departments and job roles, HR managers can develop targeted retention strategies. Additionally, the analysis of job satisfaction ratings across roles can help identify areas where employee engagement and satisfaction may be improved to reduce future attrition.


## 9. Dashboard view
<img width="815" alt="Annotation 2024-08-14 132212" src="https://github.com/user-attachments/assets/7408511f-df3b-43cb-a8d4-025e8ecb379f">

