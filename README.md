SQL Exploratory Data Analysis – Layoffs Dataset
Project Overview

This project focuses on performing Exploratory Data Analysis (EDA) on a global layoffs dataset using MySQL.

The analysis explores layoffs across companies, industries, funding stages, and time periods to identify major trends, companies with the highest layoffs, and periods with significant workforce reductions.

The analysis was performed on the cleaned layoffs_staging2 table.

Objectives
Analyze the overall scale of layoffs.
Identify companies with the highest number of layoffs.
Find industries most affected by layoffs.
Analyze layoffs by year and month.
Compare layoffs across different company stages.
Identify companies with the highest average percentage of employees laid off.
Calculate cumulative layoffs over time.
Find the top 5 companies with the highest layoffs for each year.
Tools & Technologies
MySQL
SQL
CTEs (Common Table Expressions)
Window Functions
Aggregations
GROUP BY
DENSE_RANK()
Date Functions
String Functions
Analysis Performed
1. Dataset Overview

Examined the cleaned dataset to understand its structure and available data.

SELECT *
FROM layoffs_staging2;
2. Maximum Layoffs

Identified the maximum number of employees laid off and the highest percentage of layoffs recorded.

SELECT MAX(total_laid_off), MAX(percentage_laid_off)
FROM layoffs_staging2;
3. Companies With 100% Layoffs

Identified companies where 100% of the workforce was laid off and sorted them by funding raised.

SELECT *
FROM layoffs_staging2
WHERE percentage_laid_off = 1
ORDER BY funds_raised_millions DESC;
4. Total Layoffs by Company

Calculated total layoffs for each company to identify companies with the largest workforce reductions.

SELECT company, SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY company
ORDER BY 2 DESC;
5. Date Range

Determined the earliest and latest dates available in the dataset.

SELECT MIN(`date`), MAX(`date`)
FROM layoffs_staging2;
6. Layoffs by Industry

Analyzed total layoffs across different industries.

SELECT industry, SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY industry
ORDER BY 2 DESC;
7. Yearly Layoff Trends

Calculated total layoffs for each year to identify periods with higher workforce reductions.

SELECT YEAR(`date`), SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY YEAR(`date`)
ORDER BY 1 DESC;
8. Layoffs by Company Stage

Analyzed layoffs according to the company's funding or business stage.

SELECT stage, SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY stage
ORDER BY 2 DESC;
9. Average Layoff Percentage by Company

Calculated the average percentage of employees laid off by each company.
