# 🏏 IPL Pulse — Cricket Analytics Dashboard

> **"Where Every Match Tells a Story — Decoded by Data."**

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Microsoft Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Project Objective](#-project-objective)
- [Dashboard Pages](#-dashboard-pages)
- [Questions & KPIs](#-questions--kpis)
- [Process](#%EF%B8%8F-process)
- [Project Insights](#-project-insights)
- [Final Conclusion](#-final-conclusion)
- [Tools Used](#%EF%B8%8F-tools-used)
- [Dataset](#-dataset)
- [Connect With Me](#-connect-with-me)

---

## 🎬 Dashboard Demo

![IPL Pulse Dashboard Demo](ipl_dashboard_demo.gif)

---

## 📌 Project Overview

**IPL Pulse** is a multi-page interactive Power BI dashboard that transforms raw Indian Premier League (IPL) match data from **2017 to 2023** into compelling, actionable insights. Covering **200 matches**, **10 teams**, and **10 iconic venues**, this project simulates a real-world sports analytics use case — exploring team strategies, player brilliance, toss dynamics, and fan attendance trends through rich visual storytelling.

---

## 🎯 Project Objective

To design and develop an end-to-end interactive Power BI dashboard that enables cricket analysts, team strategists, and enthusiasts to:

- Understand performance patterns across IPL seasons
- Evaluate the strategic impact of toss decisions on match outcomes
- Identify consistent match-winners and most impactful players
- Analyze venue-based home advantages and attendance trends
- Derive data-driven insights that go beyond scorecards

---

## 📊 Dashboard Pages

### Page 1 — IPL Executive Summary (Overview)
A high-level snapshot of tournament-wide KPIs including Total Matches, Total Runs, Avg First Innings Score, Toss Win %, Bat First Win %, and Avg Attendance — with slicers for Man of the Match and High Scoring match filter.

![IPL Executive Summary](overview.png)

---

### Page 2 — IPL Performance Analytics (Team Analysis)
Deep-dive into team vs team dynamics, toss-winner vs match-winner correlation, win margin distribution (runs vs wickets), and team-wise average inning scores.

![IPL Performance Analytics](team_analysis.png)

---

### Page 3 — Player & Venue Insights (Attendance & Players)
Spotlight on the most impactful players by Man of the Match count, home ground win advantages per team, and seasonal stadium attendance trends from 2017 to 2023.

![Player and Venue Insights](player_venue.png)

---

## ❓ Questions & KPIs

| # | Business Question | KPI / Metric |
|---|-------------------|--------------|
| 1 | How many total matches were played across all seasons? | Total Matches = **200** |
| 2 | Which team dominates the Man of the Match tally? | Most Successful Team Award Count |
| 3 | Does winning the toss give a real match advantage? | Toss Win % = **47%** |
| 4 | Do teams prefer to bat or field after winning the toss? | Toss Decision Distribution |
| 5 | Is batting first or chasing a better strategy? | Bat First Win % = **55%** |
| 6 | What is the average score set in the first innings? | Avg First Innings Score = **180.25** |
| 7 | What is the highest team score recorded? | Highest Team Score = **230** |
| 8 | Who are the most impactful players by MoM awards? | Player-wise MoM Count |
| 9 | Which teams have the strongest home ground advantage? | Team1 Home Wins by Venue |
| 10 | How has fan attendance changed season over season? | Avg Attendance = **37.63K** |
| 11 | How are matches won — by runs or by wickets? | Win Margin Distribution |
| 12 | Which teams post the highest average innings scores? | Team-wise Avg Inning Score |

---

## ⚙️ Process

### 1. 📥 Data Collection
Sourced a structured IPL match-level dataset (`IPL_Match_Data.csv`) containing **200 matches** across seasons 2017–2023, with fields covering:
- Match metadata (Season, Venue, Teams, Match Type)
- Scorecard data (Team Scores, Wickets, Overs)
- Outcome data (Winner, Win By, Win Margin)
- Player & Attendance data (Man of the Match, Stadium Attendance)

### 2. 🧹 Data Cleaning & Transformation
- Removed null/inconsistent values using **Power Query Editor**
- Standardized team names and venue labels for uniform grouping
- Created conditional columns:
  - `High_Scoring` flag (matches where Team1 Score > 200)
  - `Toss_Match_Win` (whether toss winner = match winner)
  - `Season` as a slicer-friendly dimension

### 3. 🔗 Data Modelling
- Built star-schema relationships between Match, Team, Player, and Venue dimensions
- Ensured referential integrity across all fact and dimension tables

### 4. 📐 DAX Measures
Custom measures built to power dynamic visuals:

```dax
Toss Win % =
DIVIDE(
    COUNTROWS(FILTER(Matches, Matches[Toss_Winner] = Matches[Match_Winner])),
    COUNTROWS(Matches)
) * 100

Bat First Win % =
DIVIDE(
    COUNTROWS(FILTER(Matches, Matches[Toss_Decision] = "Bat" && Matches[Toss_Winner] = Matches[Match_Winner])),
    COUNTROWS(FILTER(Matches, Matches[Toss_Decision] = "Bat"))
) * 100

Avg First Innings Score = AVERAGE(Matches[Team1_Score])

Avg Attendance = AVERAGE(Matches[Stadium_Attendance])
```

### 5. 🎨 Dashboard Design
Built 3 fully interactive report pages with a cohesive IPL-themed blue palette:

| Visual Type | Usage |
|-------------|-------|
| KPI Cards | Top-level executive metrics |
| Horizontal Bar Chart | Most Successful Teams, Most Impactful Players |
| Donut Chart | Toss Preference (Bat vs Field), Win Margin Distribution |
| Line Chart | Tournament Growth (2017–2023), Avg Attendance by Season |
| Stacked Bar Chart | Toss Winner vs Match Winner Correlation |
| Column Chart | Team-wise Avg Inning Score |
| Matrix Table | Home Ground Wins by Team & Venue |

### 6. 🎛️ Interactivity & UX
- Slicers: Man of the Match, High Scoring, Team, Toss Decision, Season, Venue
- Navigation buttons: Overview → Team Analysis → Attendance & Players
- **"Clear All Slicer"** button for one-click filter reset
- Tooltip enhancements for richer on-hover data context

---

## 💡 Project Insights

- 🏆 **Royal Challengers Bangalore** leads in Man of the Match awards with **26** — reflecting exceptional individual performances despite inconsistent team results.

- 🪙 **Toss winners chose to field 52.5% of the time**, confirming a modern T20 preference for chasing, yet winning the toss alone doesn't guarantee victory (only 47% toss-to-match win rate).

- 🏏 **Batting first teams won 55% of matches**, challenging the common narrative that chasing is always the preferred approach in T20 cricket.

- 📈 **Tournament attendance peaked around 2020–2021** at ~40K average before declining sharply in 2022–2023, likely due to venue rotations and scheduling changes post-COVID.

- ⭐ **Virat Kohli** dominates the individual impact chart with **17 Man of the Match awards** — nearly 21% more than second-placed Sunil Narine (14).

- 🏟️ **Royal Challengers Bangalore's home ground** (M. Chinnaswamy Stadium, Bangalore) records **16 Team1 wins** — the highest home advantage across all venues.

- 🎯 **55% of matches were won by wickets** versus 45% by runs, reinforcing the dominance of successful run-chases across modern IPL cricket.

- 📊 **Chennai Super Kings and Gujarat Titans** lead in average innings scoring (~185+), demonstrating consistent batting depth across seasons.

---

## ✅ Final Conclusion

The **IPL Pulse Dashboard** reveals several data-driven paradoxes in cricket strategy. While toss winners prefer to field, batting-first teams actually hold a marginal statistical edge in match outcomes — a finding that challenges conventional T20 wisdom and opens doors for further analysis.

Player consistency remains a reliable indicator of team success: Kohli, Narine, and Samson regularly appear as match-deciding performers. Additionally, home venue advantage is real and quantifiable, with certain franchises showing significantly higher win rates at their home grounds.

From a portfolio perspective, this project demonstrates proficiency in:
- **End-to-end data pipeline** (raw CSV → cleaned data → modelled → visualized)
- **Advanced DAX** for dynamic measures and KPI calculations
- **Dashboard UX design** with multi-page navigation and interactive slicers
- **Storytelling with data** to surface non-obvious, actionable insights

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| **Power BI Desktop** | Dashboard development, DAX, visuals |
| **Power Query** | Data cleaning & transformation |
| **DAX** | Custom measures & calculated columns |
| **Microsoft Excel** | Data exploration & pre-processing |

---

## 📁 Dataset

| Attribute | Detail |
|-----------|--------|
| **File** | `IPL_Match_Data.csv` |
| **Source** | IPL Match Data (Structured) |
| **Total Records** | 200 matches |
| **Seasons Covered** | 2017 – 2023 |
| **Teams** | 10 IPL franchises |
| **Venues** | 10 stadiums across India |

### 📄 Dataset Columns

| Column | Description |
|--------|-------------|
| `Match_ID` | Unique match identifier |
| `Season` | IPL season year (2017–2023) |
| `Match_Type` | League / Playoff |
| `Venue` | Stadium name and city |
| `Team1` | Home / first listed team |
| `Team2` | Away / second listed team |
| `Toss_Winner` | Team that won the toss |
| `Toss_Decision` | Bat or Field decision after toss |
| `Team1_Score` | Runs scored by Team 1 |
| `Team1_Wickets` | Wickets lost by Team 1 |
| `Team1_Overs_Played` | Overs faced by Team 1 |
| `Team2_Score` | Runs scored by Team 2 |
| `Team2_Wickets` | Wickets lost by Team 2 |
| `Team2_Overs_Played` | Overs faced by Team 2 |
| `Match_Winner` | Winning team |
| `Win_By` | Won by Runs or Wickets |
| `Win_Margin` | Margin of victory |
| `Man_of_the_Match` | Player awarded MoM |
| `Stadium_Attendance` | Number of spectators present |

### 🔍 Sample Data Preview

| Match_ID | Season | Venue | Team1 | Team2 | Toss_Decision | Match_Winner | Win_By | Win_Margin | Man_of_the_Match | Attendance |
|----------|--------|-------|-------|-------|---------------|--------------|--------|------------|------------------|------------|
| 1001 | 2017 | Narendra Modi Stadium, Ahmedabad | Gujarat Titans | Mumbai Indians | Field | Mumbai Indians | Wickets | 6 | Sunil Narine | 33,174 |
| 1002 | 2017 | MA Chidambaram Stadium, Chennai | Chennai Super Kings | RCB | Bat | RCB | Wickets | 3 | Rohit Sharma | 25,816 |
| 1003 | 2017 | Eden Gardens, Kolkata | Kolkata Knight Riders | Chennai Super Kings | Bat | KKR | Runs | 13 | Shikhar Dhawan | 59,883 |
| 1004 | 2017 | Sawai Mansingh Stadium, Jaipur | Rajasthan Royals | KKR | Field | Rajasthan Royals | Runs | 7 | Rishabh Pant | 30,237 |
| 1005 | 2017 | Sawai Mansingh Stadium, Jaipur | Rajasthan Royals | Sunrisers Hyderabad | Field | Sunrisers Hyderabad | Wickets | 7 | David Warner | 53,660 |

> 📂 Full dataset available in [`IPL_Match_Data.csv`](IPL_Match_Data.csv)

---

## 🤝 Connect With Me

If you found this project insightful, feel free to ⭐ star the repository and connect!

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/your-profile)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/your-username)

---

*Made with ❤️ and Power BI*
