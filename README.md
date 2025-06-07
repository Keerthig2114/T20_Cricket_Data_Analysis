# 🏏 T20 Men's Cricket World Cup - Power BI Dashboard
## 📌 Overview
This project delivers an interactive **Power BI Dashboard** that provides a deep dive into the performances of players from the **T20 Men’s Cricket World Cup 2022**. It allows users to:

- Review and compare detailed player statistics
- Filter by player roles (Openers, Finishers, Anchors, All-Rounders, Fast Bowlers)
- Select the **Best XI** based on tournament performance using custom criteria

The dashboard is built for **fans, analysts, and recruiters** interested in exploring data-driven cricket insights.


## 🌐 Data Sources
- **Match & tournament data**: [ESPN Cricinfo](https://www.espncricinfo.com/)
- **Player performance & career stats**: [Bright Data](https://brightdata.com/)


## 🛠️ Data Collection
- Used **Bright Data** to extract structured web data (JSON) for both match stats and player career records
- Data processing done in **Jupyter Notebook**
- Raw data saved in **JSON** format, then converted to **Pandas DataFrames**
- Exported to **CSV** files for analysis and visualization in Power BI


## 🧹 Data Transformation
- Cleaned and Standardized raw data using **Pandas**:
  - Corrected player name inconsistencies
  - Handled missing/null values
  - Linked match and player IDs
- Final transformation and structuring done in **Power BI Power Query**


## 🧩 Data Modeling & DAX
- Linked datasets using keys like `Match ID` and `Team`
- Created:
  - **Calculated columns**
  - **DAX measures**
  - **User-defined parameters**
- Enabled dynamic filtering, role-based comparisons, and "Best XI" selection logic


## 📊 Dashboard Highlights
- **Role-based segmentation**:
  - 🏏 Power Hitters/ Openers
  - 🛡️ Anchors
  - 🌀 All-Rounders
  - ⚡ Specialist Fast Bowlers
- Interactive slicers and tooltips
- Visual KPIs for batting, bowling, and all-round performance
- "Select Your XI" feature to evaluate team choices dynamically

## 📐 DAX Measures Used

### 🏏 Batting Metrics

- Total Runs = SUM(fact_batting_summary[runs])
- Total Innings Batted = COUNT(fact_batting_summary[match_id])
- Total Innings Dismissed = SUM(fact_batting_summary[out])
- Batting Avg = DIVIDE([Total Runs], [Total Innings Dismissed], 0)
- Total Balls Faced = SUM(fact_batting_summary[balls])
- Strike Rate = DIVIDE([Total Runs], [Total Balls Faced], 0) * 100
- Batting Position = ROUNDUP(AVERAGE(fact_batting_summary[batting_pos]), 0)
- Boundary % = DIVIDE(SUM(fact_batting_summary[Boundary runs]), [Total Runs], 0)
- Average Balls Faced = AVERAGE(fact_batting_summary[balls])


### 🎯 Bowling Metrics

- Wickets = SUM(fact_bowling_summary[wickets])
- Balls Bowled = SUM(fact_bowling_summary[balls])
- Runs Conceded = SUM(fact_bowling_summary[runs])
- Economy = DIVIDE([Runs Conceded], ([Balls Bowled] / 6), 0)
- Bowling Strike Rate = DIVIDE([Balls Bowled], [Wickets], 0)
- Bowling Average = DIVIDE([Runs Conceded], [Wickets], 0)
- Total Innings Bowled = DISTINCTCOUNT(fact_bowling_summary[match_id])
- Dot Ball % = DIVIDE(SUM(fact_bowling_summary[zeros]), SUM(fact_bowling_summary[balls]), 0)


### 👤 Player Interaction & UX Controls

- Player Selection = IF(ISFILTERED(dim_player[name]), "1", "0")
- Display Text = IF([Player Selection] = "1", " ", "Select Player(s) by clicking the player’s name to see their individual or combined strength.")
- Color Callout Value = if([Player Selection]="0", "#EB895F","#605E5C")

## 📷 Dashboard Screenshots


