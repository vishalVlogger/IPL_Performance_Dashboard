# 🏏 IPL Performance Dashboard (Power BI)

An interactive **Power BI Dashboard** analysing over 15 seasons of **Indian Premier League (IPL)** matches and deliveries.  
This project showcases data cleaning, transformation, modelling, and storytelling skills using **Power BI**, **Power Query**, and **DAX**.

---

## 📊 Project Overview

The **IPL Performance Dashboard** offers a comprehensive visual analysis of IPL matches and deliveries, providing insights at the player, team, and season levels.  
It highlights run trends, wicket distributions, boundary percentages, and toss impact — all in a single, visually engaging dashboard.

### 🔍 Key Insights
- Year-over-year IPL performance trends (Total Runs, Wickets, Matches)
- Top 10 Batsmen and Bowlers by season
- Boundary % vs Dot Ball % comparison
- Toss decision impact on match outcomes
- Venue-based match and performance distribution
- Player-level drill-through page for detailed stats

---

## 🧩 Data Sources

- **matches.csv** — Match-level data (season, teams, result, venue, etc.)
- **deliveries.csv** — Ball-by-ball data (batsman, bowler, runs, wickets, etc.)

Both datasets were sourced from public IPL datasets on [Kaggle](https://www.kaggle.com/).

---

## ⚙️ Data Preparation

Data cleaning and transformation were performed using **Power Query Editor (M)**.

### 🔧 Steps Performed
#### `matches.csv`
- Parsed `date` column to datetime format  
- Added `match_year` column for season grouping  
- Trimmed text, removed duplicates, and replaced blanks with nulls  
- Cleaned inconsistent winner and result entries  

#### `deliveries.csv`
- Converted numeric columns to correct data types  
- Created derived columns:
  - `is_wicket` → identifies if a wicket fell on a ball  
  - `ball_in_innings` → continuous ball index  
  - `is_boundary_4`, `is_boundary_6`, `is_dot`  
- Removed duplicates and standardised text columns  

> Cleaned files:  
> - `clean_matches.csv`  
> - `clean_deliveries.csv`

---

## 🧠 Data Modeling

Relationship created in Power BI:
matches[id] ────▶ deliveries[match_id]
(One-to-Many)


### Calculated Columns
- `match_year` (from date)
- `Win_Type` (Chased / Defended)

### Key DAX Measures
```DAX
Total Runs = SUM(deliveries[total_runs])
Total Wickets = CALCULATE(COUNTROWS(deliveries), deliveries[is_wicket] = TRUE())
Dot Ball % = DIVIDE(CALCULATE(COUNTROWS(deliveries), deliveries[is_dot] = TRUE()), COUNTROWS(deliveries))
Boundary % = DIVIDE(CALCULATE(COUNTROWS(deliveries), deliveries[is_boundary_4] = TRUE() || deliveries[is_boundary_6] = TRUE()), COUNTROWS(deliveries))
Strike Rate = DIVIDE(SUM(deliveries[batsman_runs]), COUNTROWS(deliveries)) * 100
Economy Rate = DIVIDE(SUM(deliveries[total_runs]), COUNTROWS(deliveries) / 6)
```

### 🎨 Dashboard Design
- Page Size: 1280 × 720 (16:9)

- Visual Layout
  | Section | Visual |	Purpose |
  |:--------|:------------|:------:|
  | Top Row	 | KPI Cards | Total Matches, Runs, Wickets, Toss Win Impact |
  | Left Panel |	Slicers	| Season, Team, Venue, Player |
  | Centre | Line & Bar Charts | Runs by Season, Top Players | 
  | Right	| Donut Charts | Dot Ball % and Boundary % |
  | Bottom | Table | Match details with player of the match and margin |

- Interactive Features
  - Slicers: Filter by Season, Team, Venue
  - Drill-through: Player Details Page
  - Bookmarks: Season Overview vs Player Focus
  - Tooltips: Runs per Over, Strike Rate by Player

### 🧾 Tools Used

| Tool                                | Purpose                            |
| ----------------------------------- | ---------------------------------- |
| **Power BI Desktop**                | Dashboard design and visualization |
| **Power Query (M)**                 | Data cleaning and transformation   |
| **DAX (Data Analysis Expressions)** | Calculated measures and KPIs       |
| **Python (pandas)**                 | Initial data preprocessing         |
| **GitHub**                          | Version control and documentation  |

### 📈 Key Learnings
- Built a strong understanding of data modelling and relationships in Power BI.
- Learned to write optimised DAX measures for performance.
- Designed a responsive dashboard layout for a professional presentation.
- Enhanced skills in data storytelling using real-world sports analytics.

### 📸 Dashboard Preview
- Link: [IPL Performance Dashboard](https://app.powerbi.com/groups/me/reports/35f4ffd4-eea2-4895-8e94-df5f75036fec/d3e802a37ef4792bdcb9?experience=power-bi)

  <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/1855a6f5-575b-44c0-9e3f-e148d228ecdc" />

### 🚀 How to Use
  - Clone this repository:
    ```git clone https://github.com/<your-username>/IPL-PowerBI-Dashboard.git```
  - Open Power BI Desktop.
  - Import clean_matches.csv and clean_deliveries.csv.
  - Apply Power Query transformations and DAX measures (included above).
  - Load data and explore the visuals interactively.

### 🧑‍💻 Author
Vishal Patil
- Power BI Developer | Data Analyst
