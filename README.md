# SQL Exploratory Data Analysis – Layoffs Dataset

## Project Overview

This project focuses on performing Exploratory Data Analysis (EDA) on a global layoffs dataset using MySQL.

The analysis explores layoffs across companies, industries, company stages, and time periods to identify major trends and patterns in workforce reductions.

The analysis was performed on the cleaned `layoffs_staging2` table.

## Objectives

- Analyze overall layoffs and identify major trends.
- Identify companies with the highest number of layoffs.
- Analyze layoffs across different industries and company stages.
- Examine yearly and monthly layoff trends.
- Calculate cumulative layoffs over time.
- Identify the top 5 companies with the highest layoffs for each year.

## Tools & Technologies

- MySQL
- SQL
- Common Table Expressions (CTEs)
- Window Functions
- Aggregate Functions
- Data Analysis

## Key Analysis

### 1. Maximum Layoffs

Find the maximum number and percentage of layoffs recorded in the dataset.

```sql
SELECT 
    MAX(total_laid_off) AS max_laid_off,
    MAX(percentage_laid_off) AS max_percentage_laid_off
FROM layoffs_staging2;

**2. Companies With 100% Layoffs**

Identify companies that laid off their entire workforce and compare them based on funding raised.

```sql
SELECT *
FROM layoffs_staging2
WHERE percentage_laid_off = 1
ORDER BY funds_raised_millions DESC;

