# SQL Exploratory Data Analysis – Layoffs Dataset

## Project Overview

This project focuses on performing Exploratory Data Analysis (EDA) on a global layoffs dataset using MySQL.

The analysis explores layoffs across companies, industries, funding stages, and time periods to identify major trends, companies with the highest layoffs, and periods with significant workforce reductions.

The analysis was performed on the cleaned `layoffs_staging2` table.

## Objectives

- Analyze the overall scale of layoffs.
- Identify companies with the highest number of layoffs.
- Find industries most affected by layoffs.
- Analyze layoffs by year and month.
- Compare layoffs across different company stages.
- Identify companies with the highest average percentage of employees laid off.
- Calculate cumulative layoffs over time.
- Find the top 5 companies with the highest layoffs for each year.

## Tools & Technologies

- MySQL
- SQL
- CTEs (Common Table Expressions)
- Window Functions
- Aggregations
- GROUP BY
- DENSE_RANK()
- Date Functions
- String Functions

## Analysis Performed

### 1. Dataset Overview

Examined the cleaned dataset to understand its structure and available data.

```sql
SELECT *
FROM layoffs_staging2;
