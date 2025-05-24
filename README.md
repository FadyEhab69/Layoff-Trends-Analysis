# Data Analysis Report: Layoff Trends Analysis (May 2025)

# Overview
As a data analyst, I conducted a detailed analysis of the layoffs dataset from Kaggle (https://www.kaggle.com/datasets/swaptr/layoffs-2022) to uncover trends and provide actionable insights for businesses navigating workforce reductions. Using SQL queries on the world_layoffs database, I cleaned the data and addressed key analytical questions to support strategic decision-making. This report showcases my analytical process, findings, and recommendations .

# Data Analysis Process
# Dataset Description
Table: world_layoffs.layoffs (and staged as layoffs_staging2 after cleaning).
Columns: company, location, industry, total_laid_off, percentage_laid_off, date, stage, country, funds_raised_millions.
Source: Kaggle dataset covering layoffs from 2020 to 2023.
Objective: Identify patterns in layoffs by industry, region, and company stage to inform business resilience strategies.
# Analytical Questions and Insights
1/ Total Layoffs by Industry:
Queried SELECT industry, SUM(total_laid_off) AS total_layoffs FROM world_layoffs.layoffs_staging2 GROUP BY industry ORDER BY total_layoffs DESC to rank industries by layoff volume.
Insight: Consumer and Retail sectors showed the highest layoffs, suggesting economic sensitivity in these areas.
2/ Layoff Trends by Country:
Analyzed with SELECT country, SUM(total_laid_off) AS total_layoffs, AVG(percentage_laid_off) AS avg_percentage FROM world_layoffs.layoffs_staging2 GROUP BY country ORDER BY total_layoffs DESC.
Insight: The United States led in total layoffs, with an average percentage reduction of approximately 20%, indicating widespread impact.
3/ Impact by Company Stage:
Evaluated with SELECT stage, SUM(total_laid_off) AS total_layoffs FROM world_layoffs.layoffs_staging2 GROUP BY stage ORDER BY total_layoffs DESC.
Insight: Post-IPO companies accounted for the majority of layoffs, highlighting challenges for publicly traded firms.
4/ Temporal Layoff Patterns:
Assessed monthly trends with SELECT DATE_FORMAT(date, '%Y-%m') AS month, SUM(total_laid_off) AS total_layoffs FROM world_layoffs.layoffs_staging2 GROUP BY month ORDER BY month.
Insight: April 2020 saw a peak in layoffs, likely due to the initial COVID-19 impact, with a gradual decline thereafter.
5/ High-Impact Companies:
Identified top contributors with SELECT company, SUM(total_laid_off) AS total_layoffs FROM world_layoffs.layoffs_staging2 GROUP BY company ORDER BY total_layoffs DESC LIMIT 5.
Insight: Companies like Google and Microsoft led in layoff numbers, reflecting strategic workforce adjustments in tech giants.
6/ Correlation with Funding:
Explored with SELECT funds_raised_millions, AVG(total_laid_off) AS avg_layoffs FROM world_layoffs.layoffs_staging2 WHERE funds_raised_millions IS NOT NULL GROUP BY funds_raised_millions ORDER BY funds_raised_millions.
Insight: Higher-funded companies (e.g., >$100M) showed larger average layoffs, suggesting over-expansion risks.

# Data Cleaning Process
Duplicate Removal: Identified and removed duplicate rows using ROW_NUMBER() and a CTE, ensuring data integrity (e.g., deleted 12 duplicate entries).
Standardization: Standardized industry (e.g., unified "Crypto Currency" to "Crypto"), country (removed trailing periods from "United States."), and converted date to DATE format using STR_TO_DATE.
Null Handling: Replaced blank industry values with NULL and populated where possible via self-joins; retained NULLs in total_laid_off and percentage_laid_off for EDA flexibility.
Row/Column Cleanup: Removed rows with NULL total_laid_off and percentage_laid_off, and dropped the temporary row_num column post-duplicate removal.
# Key Findings
Industry Vulnerability: Consumer and Retail sectors were hit hardest, with significant layoffs in 2020.
Geographic Concentration: The U.S. dominated layoff numbers, with tech hubs like SF Bay Area showing high activity.
Stage Sensitivity: Post-IPO firms faced the most layoffs, possibly due to market pressures.
Temporal Peaks: Early 2020 layoffs correlated with global economic disruptions, with sustained reductions into 2023.
Funding Impact: Well-funded companies experienced larger layoffs, indicating potential misalignment between capital and workforce needs.
# Recommendations
Industry Focus: Businesses in Consumer and Retail should diversify revenue streams to mitigate layoff risks.
Regional Strategy: Companies in the U.S., especially tech hubs, should monitor workforce trends and invest in retention.
Stage Planning: Pre-IPO firms should prepare for post-IPO challenges with leaner staffing models.
Timing Awareness: Plan workforce adjustments outside peak layoff periods (e.g., Q2 2020) to avoid market overreaction.
Funding Review: Assess funding allocation to avoid overstaffing relative to revenue potential.
# Analytical Skills Demonstrated
Data Cleaning: Mastered duplicate removal, data standardization, and null management using SQL.
Query Optimization: Utilized aggregations (SUM, AVG) and grouping for efficient trend analysis.
Insight Generation: Translated raw layoff data into strategic business recommendations.
Problem-Solving: Addressed data inconsistencies (e.g., industry nulls) with practical solutions.
Trend Analysis: Identified temporal and sectoral patterns to guide proactive planning.
# Conclusion
This analysis of the layoffs dataset showcases my ability to clean, query, and derive actionable insights from complex datasets using SQL. The process highlights my skills in data manipulation, trend identification, and strategic recommendation. Future analysis could incorporate predictive modeling to forecast layoff risks based on economic indicators.
