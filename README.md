# 📊 Netflix Content Strategy — Tableau Dashboard

> Interactive 4-chart Tableau Public dashboard built on the Netflix titles dataset. Published live at the link below.

---

## 🔗 Live Dashboard

**➡️ [View on Tableau Public](ADD_YOUR_TABLEAU_URL_HERE)**

> *To get your own live link: follow the build guide below, publish to Tableau Public, and replace the URL above.*

---

## 📸 Dashboard Preview

The dashboard contains 4 interactive charts:

| Chart | Type | Insight |
|-------|------|---------|
| Content Type Split | Donut Chart | 69% Movies vs 31% TV Shows |
| Catalog Growth Over Time | Dual-line Chart | Year-over-year additions, peaks in 2019 |
| Top 15 Content Countries | Horizontal Bar | US + India dominate |
| Audience Rating Breakdown | Packed Bubbles | TV-MA is #1 at 36% |

**All 4 charts are cross-filtered** — clicking any element filters the entire dashboard.

---

## 🏗 Step-by-Step Build Guide

### 1. Setup
- Download **Tableau Public** (free): [public.tableau.com/downloads](https://public.tableau.com/en/s/download)
- Create a free account at [public.tableau.com](https://public.tableau.com)
- Download `netflix_cleaned.csv` from the [netflix-sql-analysis repo](https://github.com/YOURUSERNAME/netflix-sql-analysis)

### 2. Connect Data
```
Open Tableau Public
→ Connect → Text File → select netflix_cleaned.csv
→ Verify: type (String), release_year (Number), date_added (Date)
```

### 3. Chart 1 — Content Type Split (Donut)
```
Sheet 1 → rename "Content Type Split"
Columns: [Type]
Rows: COUNT([Show Id])
Marks: Pie
Color: [Type]
Angle: COUNT([Show Id])
Label: COUNT([Show Id])
Donut trick: hold Shift, drag blank pill to Size → resize small
```

### 4. Chart 2 — Catalog Growth (Line)
```
Sheet 2 → rename "Catalog Growth Over Time"
Columns: YEAR([Date Added]) — use continuous green pill
Rows: COUNT([Show Id])
Marks: Line
Color: [Type]   ← splits into Movies vs TV lines
Analytics pane → Trend Line → Linear
```

### 5. Chart 3 — Top Countries (Bar)
```
Sheet 3 → rename "Top Content Countries"
Rows: [Country]
Columns: COUNT([Show Id])
Filter: [Country] → Top 10 by COUNT([Show Id])
Sort: descending
Labels: on
```

### 6. Chart 4 — Rating Bubbles (Packed Circles)
```
Sheet 4 → rename "Audience Rating Breakdown"
Marks: Circle
Size: COUNT([Show Id])
Color: [Rating]
Label: [Rating] + COUNT([Show Id])
```

### 7. Assemble Dashboard
```
New Dashboard → size: Automatic
Drag all 4 sheets onto canvas
Title: "Netflix Content Strategy Dashboard | 2008–2021"
Make charts interactive: click line chart → funnel icon → "Use as Filter"
```

### 8. Publish
```
File → Save to Tableau Public As...
Name: "Netflix Content Analysis"
Copy the published URL → update this README
```

---

## 🛠 Tech Stack

![Tableau Public](https://img.shields.io/badge/Tableau-Public-E97627?logo=tableau&logoColor=white)
![CSV](https://img.shields.io/badge/Data-CSV-green)

---

## 📁 Data Source

- Built on the [Netflix Movies and TV Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows) dataset
- Cleaned version available in the [netflix-sql-analysis](https://github.com/YOURUSERNAME/netflix-sql-analysis) repo

---

*Part of a 3-project data analytics portfolio. See also:*
- *[Netflix SQL + Python Analysis](https://github.com/YOURUSERNAME/netflix-sql-analysis)*
- *[Spotify Streaming Era Analysis](https://github.com/YOURUSERNAME/spotify-streaming-analysis)*
