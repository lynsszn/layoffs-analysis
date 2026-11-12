# Global Layoffs Data Analysis

## Table of Content 
- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tools](#tools)
- [Data Cleaning](#data-cleaning)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Kay Findings](#key-findings)
- [Limitations](#limitations)
- [Recommendations](#recommendations)
- [Reference](#reference)

## Project Overview
This project explores global company layoffs using SQL. The aim is to prepare the dataset for analysis, identify patterns in workforce reductions, and uncover trends across companies, industries, countries and time periods.

## Data Source
- Dataset: Global Layoffs Dataset (layoffs.csv)
- Source: Alex The Analyst – MySQL YouTube Series GitHub repository.

## Tools
- MYSQL

## Data Cleaning
The dataset was prepared for analysis through:

- Identifying and removing duplicate records.
- Standardising company, industry and country values.
- Converting date values into the appropriate date format.
- Handling NULL and blank values.
- Removing records with no available layoff figures.
- Removing unnecessary columns.

## Exploratory Data Analysis
SQL queries were used to investigate:

- Companies with the highest number of layoffs.
- Industries most affected by layoffs.
- Layoffs by country.
- Annual layoffs trends.
- Layoffs by company stage.
- Monthly layoffs trends and cumulative totals.
- Companies with the highest layoffs in each year.

## Data Analysis
1. Using CTEs and ROW_NUMBER() to identify duplicates

   ```sql
   WITH duplicate_cte AS (
    SELECT *,
        ROW_NUMBER() OVER(
            PARTITION BY company, location, industry,
            total_laid_off, percentage_laid_off,
            `date`, stage, country, funds_raised_millions
        ) AS row_num
    FROM layoffs_stagging)
    SELECT *
    FROM duplicate_cte
    WHERE row_num > 1;

2. Using GROUP BY and SUM() to analyse layoffs by industry

```sql
SELECT industry, SUM(total_laid_off)
FROM layoffs_stagging2
GROUP BY industry
ORDER BY 2 DESC;
```

## Key Findings
The exploratory analysis revealed the following patterns in the global layoffs dataset:

1. Companies with the Highest Layoffs: Amazon recorded the highest cumulative layoffs, with 18,150 employees laid off, followed by Google with 12,000 and Meta with 11,000.
2. Industry Impact: The Consumer industry recorded the highest total layoffs at 46,052, followed by Retail with 43,444 and Other with 36,224.
3. Country Distribution: The United States accounted for the highest number of reported layoffs, with 258,159, significantly higher than India, which recorded 35,993.
4. Annual Layoff Trends: 2022 recorded the highest total layoffs, with 161,711 employees affected. This was followed by 2023 with 127,277, although the dataset only covers January to March 2023.
5. Monthly Layoff Trends: January 2023 recorded the highest monthly layoffs, with 84,714 employees affected, followed by November 2022 with 53,751.

## Limitations
1. Limited Workforce Information: Although the dataset contained the percentage of employees laid off by each company, it does not provide the total number of employees or company workforce size. This limited the ability to independently verify the reported layoff percentages or calculate the actual workforce remaining after layoffs.
2. Missing Values: Some records contained missing values in important columns, including total layoffs and percentage laid off. Records without both figures were excluded during cleaning, which may affect the completeness of the analysis.
3. Limited Dataset Scope: The analysis is based on the records and time period available in the supplied dataset. It may not represent all company layoffs globally.

## Recommendations
1. Improve Workforce Data Collection: Future datasets should include total employee counts before and after layoffs to provide better context for understanding the scale of workforce reductions.
2. Monitor Industry Trends: Organisations and stakeholders should pay attention to industries with consistently high layoff figures to better understand employment risks and changing workforce demands.
3. Strengthen Workforce Planning: Companies should consider regular reviews of their financial performance, funding position and workforce requirements to support more sustainable staffing decisions.

## Reference

- Alex The Analyst (Data Analysis Bootcamp)


