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

<h2>1. Maximum Layoffs</h2>

<p>Find the maximum number and percentage of layoffs recorded in the dataset.</p>

<pre><code>SELECT 
    MAX(total_laid_off) AS max_laid_off,
    MAX(percentage_laid_off) AS max_percentage_laid_off
FROM layoffs_staging2;</code></pre>

<h2>2. Companies With 100% Layoffs</h2>

<p>Identify companies that laid off their entire workforce and compare them based on funding raised.</p>

<pre><code>SELECT *
FROM layoffs_staging2
WHERE percentage_laid_off = 1
ORDER BY funds_raised_millions DESC;</code></pre>

<h2>3. Companies With the Highest Total Layoffs</h2>

<p>Find the companies with the largest total number of layoffs.</p>

<pre><code>SELECT 
    company,
    SUM(total_laid_off) AS total_laid_off
FROM layoffs_staging2
GROUP BY company
ORDER BY total_laid_off DESC;</code></pre>

<h2>4. Layoffs by Industry</h2>

<p>Analyze which industries experienced the highest number of layoffs.</p>

<pre><code>SELECT 
    industry,
    SUM(total_laid_off) AS total_laid_off
FROM layoffs_staging2
GROUP BY industry
ORDER BY total_laid_off DESC;</code></pre>

<h2>5. Yearly Layoff Trends</h2>

<p>Analyze how layoffs changed from year to year.</p>

<pre><code>SELECT 
    YEAR(`date`) AS year,
    SUM(total_laid_off) AS total_laid_off
FROM layoffs_staging2
GROUP BY YEAR(`date`)
ORDER BY year;</code></pre>

<h2>6. Monthly Layoff Trends</h2>

<p>Analyze layoffs on a monthly basis to identify periods with significant workforce reductions.</p>

<pre><code>SELECT 
    SUBSTRING(`date`, 1, 7) AS month,
    SUM(total_laid_off) AS total_laid_off
FROM layoffs_staging2
WHERE SUBSTRING(`date`, 1, 7) IS NOT NULL
GROUP BY month
ORDER BY month;</code></pre>

<h2>7. Rolling Total of Layoffs</h2>

<p>Used a CTE and Window Function to calculate the cumulative number of layoffs over time.</p>

<pre><code>WITH Rolling_Total AS (
    SELECT 
        SUBSTRING(`date`, 1, 7) AS month,
        SUM(total_laid_off) AS total_off
    FROM layoffs_staging2
    WHERE SUBSTRING(`date`, 1, 7) IS NOT NULL
    GROUP BY month
)
SELECT 
    month,
    total_off,
    SUM(total_off) OVER (ORDER BY month) AS rolling_total
FROM Rolling_Total;</code></pre>

<h2>8. Top 5 Companies by Layoffs Each Year</h2>

<p>Used CTEs and DENSE_RANK() to identify the top 5 companies with the highest layoffs for each year.</p>

<pre><code>WITH Company_Year AS (
    SELECT 
        company,
        YEAR(`date`) AS year,
        SUM(total_laid_off) AS total_laid_off
    FROM layoffs_staging2
    GROUP BY company, YEAR(`date`)
),
Company_Year_Rank AS (
    SELECT *,
        DENSE_RANK() OVER (
            PARTITION BY year
            ORDER BY total_laid_off DESC
        ) AS ranking
    FROM Company_Year
    WHERE year IS NOT NULL
)
SELECT *
FROM Company_Year_Rank
WHERE ranking &lt;= 5;</code></pre>

Conclusion

This project demonstrates how SQL can be used to perform exploratory data analysis and extract meaningful insights from real-world data. It combines aggregation, time-based analysis, CTEs, and window functions to analyze layoff patterns across companies, industries, and years.
