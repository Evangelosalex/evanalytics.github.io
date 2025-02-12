# Data Portfolio: Excel to Power BI

![excel-to-powerbi-animated-diagram](assets/images/kaggle_to_powerbi.gif)

## Table of Contents

- [Objective](#objective)
- [Data Source](#data-source)
- [Project Stages](#project-stages)
- [Design](#design)
  - [Tools & Technologies](#tools--technologies)
- [Development](#development)
  - [Pseudocode & Workflow](#pseudocode--workflow)
  - [Data Exploration](#data-exploration)
  - [Data Cleaning & Transformation](#data-cleaning--transformation)
  - [SQL View Creation](#sql-view-creation)
- [Testing & Validation](#testing--validation)
  - [Data Quality & Integrity Checks](#data-quality--integrity-checks)
- [Visualization](#visualization)
  - [Power BI Dashboard](#power-bi-dashboard)
  - [DAX Measures](#dax-measures)
- [Analysis & Insights](#analysis--insights)
  - [Findings](#findings)
  - [Strategic Insights](#strategic-insights)
- [Recommendations](#recommendations)
  - [Projected ROI](#projected-roi)
  - [Actionable Strategies](#actionable-strategies)
- [Conclusion](#conclusion)

## Objective

### Business Challenge
The Head of Marketing aims to identify top-performing YouTubers in 2024 for optimizing marketing campaigns.

### Proposed Solution
Develop a Power BI dashboard offering real-time insights into:
- Subscriber growth trends
- Total views
- Video production frequency
- Engagement metrics

This will help drive data-driven decisions for influencer partnerships.

### User Story
As a Head of Marketing, I require a data-driven dashboard to analyze YouTube channel metrics, ensuring optimal influencer selection for impactful marketing campaigns.

## Data Source

### Dataset Requirements
Comprehensive YouTube data for UK-based influencers in 2024, including:
- Channel names
- Total subscribers
- Aggregate views
- Number of uploaded videos

### Data Acquisition
The dataset is sourced from Kaggle ([access it here](https://www.kaggle.com/datasets/bhavyadhingra00020/top-100-social-media-influencers-2024-countrywise?resource=download)).

## Project Stages
- **Design & Planning**
- **Data Processing & Transformation**
- **Testing & Quality Assurance**
- **Visualization & Reporting**
- **Strategic Analysis & Recommendations**

## Design

### Key Analytical Questions
1. Who are the top 10 YouTubers by subscriber count?
2. Which channels post the highest volume of content?
3. Which channels generate the highest views?
4. Which channels maintain strong audience retention (views per video)?
5. Which channels exhibit the highest engagement levels?

### Dashboard Components
Visualizations include:
- Interactive Tables
- Scorecards
- Treemaps
- Bar Charts

### Tools & Technologies

| Tool | Purpose |
| --- | --- |
| Excel | Initial Data Exploration |
| SQL Server | Data Cleaning & Aggregation |
| Power BI | Data Visualization & Reporting |
| GitHub | Project Version Control & Documentation |

## Development

### Pseudocode & Workflow
1. Acquire and review raw data
2. Conduct exploratory analysis in Excel
3. Import data into SQL Server
4. Clean and preprocess data via SQL queries
5. Validate data integrity through testing
6. Visualize insights in Power BI
7. Document findings & publish results

### Data Exploration
Key observations:
- Some channel identifiers need extraction.
- Dataset contains foreign language entries requiring translation.
- Certain columns are redundant and need elimination.

### Data Cleaning & Transformation
The dataset is refined by:
- Retaining only relevant fields
- Ensuring correct data types
- Removing null or inconsistent values

#### Processed Data Schema

| Column Name       | Data Type | Nullable |
|------------------|----------|----------|
| channel_name     | VARCHAR  | NO       |
| total_subscribers | INTEGER  | NO       |
| total_views     | INTEGER  | NO       |
| total_videos    | INTEGER  | NO       |


#### SQL Transformation Query
```sql
SELECT
    SUBSTRING(NOMBRE, 1, CHARINDEX('@', NOMBRE) -1) AS channel_name,
    total_subscribers,
    total_views,
    total_videos
FROM
    top_uk_youtubers_2024;
```

#### SQL View Creation
```sql
CREATE VIEW view_uk_youtubers_2024 AS
SELECT
    CAST(SUBSTRING(NOMBRE, 1, CHARINDEX('@', NOMBRE) -1) AS VARCHAR(100)) AS channel_name,
    total_subscribers,
    total_views,
    total_videos
FROM
    top_uk_youtubers_2024;
```

## Testing & Validation

### Data Quality & Integrity Checks
#### Row Count Validation
```sql
SELECT COUNT(*) AS total_rows FROM view_uk_youtubers_2024;
```
#### Column Count Verification
```sql
SELECT COUNT(*) AS column_count FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = 'view_uk_youtubers_2024';
```
#### Data Type Validation
```sql
SELECT COLUMN_NAME, DATA_TYPE FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = 'view_uk_youtubers_2024';
```

## Visualization

### Power BI Dashboard
![Power BI Dashboard](assets/images/top_uk_youtubers_2024.gif)

### DAX Measures
#### Total Subscribers (M)
```sql
Total Subscribers (M) = SUM(view_uk_youtubers_2024[total_subscribers]) / 1000000
```
#### Total Views (B)
```sql
Total Views (B) = SUM(view_uk_youtubers_2024[total_views]) / 1000000000
```
#### Average Views Per Video (M)
```sql
Average Views per Video (M) = SUM(view_uk_youtubers_2024[total_views]) / SUM(view_uk_youtubers_2024[total_videos]) / 1000000
```

## Analysis & Insights

### Findings
- **Highest Subscribers**: NoCopyrightSounds, DanTDM, Dan Rhodes
- **Most Content Uploaded**: GRM Daily, Manchester City, Yogscast
- **Highest Total Views**: DanTDM, Dan Rhodes, Mister Max
- **Highest Engagement**: Mark Ronson, Jessie J, Dua Lipa

### Strategic Insights
1. **Dan Rhodes offers the best ROI** ($1.07M per video).
2. **NoCopyrightSounds and DanTDM are strong long-term partners.**
3. **Channels with lower engagement (GRM Daily, Manchester City) should be avoided.**

## Recommendations

### Projected ROI
- Dan Rhodes: **$1.07M per video**
- Mister Max: **$1.28M per video**
- DanTDM: **$484K per video**

### Actionable Strategies
1. Initiate discussions with Dan Rhodes for strategic collaboration.
2. Define campaign structures within budget constraints.
3. Implement performance tracking and KPI-based evaluation.
4. Optimize influencer selection based on evolving insights.

## Conclusion
This project delivers a data-driven approach to identifying high-impact YouTube influencers for marketing campaigns. The recommended actions maximize ROI and engagement while mitigating risk.

