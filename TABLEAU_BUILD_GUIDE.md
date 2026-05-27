# Tableau Dashboard — Full Build Guide

## What You're Building

A 4-chart interactive dashboard in Tableau Public showing:
1. **Donut chart** — Movie vs TV Show split
2. **Dual-line chart** — Catalog growth over time, split by type
3. **Horizontal bar** — Top 15 content-producing countries
4. **Packed bubbles** — Content rating distribution

All 4 charts are cross-filtered: clicking any element filters the entire dashboard.

---

## Prerequisites

- [ ] Tableau Public installed (free at public.tableau.com)
- [ ] Tableau Public account created (needed to publish)
- [ ] `netflix_cleaned.csv` from the netflix-sql-analysis repo

---

## Phase 1: Connect Your Data (5 mins)

1. Open **Tableau Public**
2. Click **Connect → Text File**
3. Navigate to and select `netflix_cleaned.csv`
4. On the data source screen, verify column types:
   - `show_id` → String ✓
   - `type` → String ✓
   - `release_year` → Number (whole) ✓
   - `date_added` → Date ← if it shows as String, right-click → Change Data Type → Date
   - `year_added` → Number ✓
5. Click **Sheet 1** tab at the bottom to go to the workspace

---

## Phase 2: Chart 1 — Content Type Split (15 mins)

**Goal:** A donut chart showing 69% Movies vs 31% TV Shows

1. Right-click the **Sheet 1** tab → **Rename** → type `Content Type Split`
2. Drag `Type` to **Columns**
3. Drag `Show Id` to **Rows** → right-click it → **Measure** → **Count**
4. In the **Marks** card (left panel), change dropdown from `Automatic` to **Pie**
5. Drag `Type` to the **Color** box in Marks
6. Drag `CNT(Show Id)` to the **Angle** box in Marks
7. Drag `CNT(Show Id)` to the **Label** box in Marks → click Label → check **Show mark labels**
8. **Make it a donut:**
   - Hold `Shift` and drag a second copy of `CNT(Show Id)` to the **Size** box
   - Use the Size slider to make it smaller until a hole appears in the center
9. **Format colors:**
   - Click the **Color** box → **Edit Colors**
   - Set Movie → `#E50914` (Netflix red)
   - Set TV Show → `#564d4d` (dark grey)

---

## Phase 3: Chart 2 — Catalog Growth Over Time (15 mins)

**Goal:** Dual-line chart showing movies vs TV shows added per year, 2015–2021

1. Click the **+** at the bottom to add **Sheet 2** → rename it `Catalog Growth Over Time`
2. Drag `Date Added` to **Columns**
   - Right-click the pill → select **Year** (the *green/continuous* YEAR, not the blue discrete one)
3. Drag `Show Id` to **Rows** → right-click → **Count**
4. In Marks, change to **Line**
5. Drag `Type` to **Color** — this creates two separate lines
6. **Add a reference line:**
   - Click the **Analytics** pane (tab above the Data pane on the left)
   - Drag **Average Line** onto the chart → drop on `Table`
   - Double-click the line → Label: `Avg Annual Adds`
7. **Filter to 2015–2021:**
   - Drag `Year Added` to **Filters**
   - Select 2015 through 2021
8. **Add axis title:** Right-click Y axis → **Edit Axis** → Title: `Titles Added`

---

## Phase 4: Chart 3 — Top Content Countries (15 mins)

**Goal:** Horizontal bar chart, top 15 countries, sorted descending

1. Add **Sheet 3** → rename `Top Content Countries`
2. Drag `Country` to **Rows**
3. Drag `Show Id` → **Count** to **Columns**
4. **Filter to top 15:**
   - Drag `Country` to **Filters**
   - Go to **Top** tab → By field → Top **15** by **Count of Show Id**
   - Also add condition: Country ≠ 'Unknown'
5. **Sort:** Right-click the country axis → **Sort** → Descending by Count
6. Drag `Country` to **Color** for a colorful bar chart
7. Click the **T** button (labels) in the toolbar to add value labels
8. **Clean up titles:**
   - Right-click X axis → **Edit Axis** → Title: `Number of Titles`
   - Right-click Y axis → **Edit Axis** → Title: leave blank

---

## Phase 5: Chart 4 — Rating Bubbles (10 mins)

**Goal:** Packed bubble chart showing content rating distribution

1. Add **Sheet 4** → rename `Audience Rating Breakdown`
2. In the **Marks** card, change type to **Circle** (this enables packed bubbles)
3. Drag `Rating` to **Label** in Marks
4. Drag `Show Id` → Count to **Size** in Marks
5. Drag `Rating` to **Color** in Marks
6. Drag `Show Id` → Count to **Label** in Marks (adds counts inside bubbles)
7. Click **Label** → check **Allow labels to overlap**
8. **Filter out unknowns:**
   - Drag `Rating` to **Filters** → exclude 'Unknown' and 'Not Rated'

---

## Phase 6: Build the Dashboard (20 mins)

1. Click the **Dashboard** icon at the bottom (grid of squares) → **New Dashboard**
2. **Set size:** Dashboard menu → Size → **Automatic** (or 1200 × 800)
3. **Drag sheets onto canvas** (suggested layout):
   ```
   ┌─────────────────┬──────────────────────────┐
   │  Content Type   │  Catalog Growth           │
   │  Split (donut)  │  Over Time (line)         │
   ├─────────────────┴──────────────────────────┤
   │  Top Content Countries (bar)                │
   ├─────────────────────────────────────────────┤
   │  Audience Rating Breakdown (bubbles)        │
   └─────────────────────────────────────────────┘
   ```
4. **Add a title:**
   - Dashboard menu → **Show Title** → double-click the title area
   - Type: `Netflix Content Strategy Dashboard | 2008–2021`
5. **Make charts cross-filter:**
   - Click the **line chart** on your dashboard
   - Click the **funnel icon** (Use as Filter) that appears in the top right of the chart
   - Repeat for the bar chart
   - Now clicking a data point filters everything else!
6. **Add a text box** (optional):
   - Drag **Text** object from the left panel
   - Type a brief description: `Click any chart element to filter the full dashboard`

---

## Phase 7: Publish to Tableau Public (5 mins)

1. **File → Save to Tableau Public As...**
2. Log in with your Tableau Public account if prompted
3. Name it: `Netflix Content Analysis`
4. Click **Save**
5. Your browser will open to the live published URL:
   ```
   https://public.tableau.com/app/profile/YOURNAME/viz/NetflixContentAnalysis/...
   ```
6. **Copy that URL** — it goes:
   - In this README (replace `ADD_YOUR_TABLEAU_URL_HERE`)
   - In your resume under Projects
   - In the netflix-sql-analysis GitHub README

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Date column shows as string | Right-click column in data pane → Change Data Type → Date |
| Donut hole not appearing | Make sure you're using **Pie** mark type and a second SIZE pill |
| "Unknown" appearing in top countries | Add a filter: Country ≠ 'Unknown' |
| Bubbles not packing together | Change mark type to **Circle** (not Shape) |
| Can't publish | Make sure you created a free account at public.tableau.com |

---

## Design Tips

- **Netflix color palette:** `#E50914` (red), `#141414` (black), `#FFFFFF` (white), `#564d4d` (grey)
- **Font:** Format menu → Workbook Font → set to **Arial** or **Tableau Book**
- **Remove gridlines:** Format → Lines → Row Divider → None
- **Add padding:** Format → Cell Size → adjust for breathing room
