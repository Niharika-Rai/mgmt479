# Data Visualization & Business Analytics Portfolio (Tableau)

**Niharika Rai** · Purdue University · MGMT 47900: Data Visualization (Spring 2026)

This repository holds my Tableau work from Purdue's MGMT 479 data visualization course. It contains two graded assignments, one team project and one individual capstone project. Across this work I took raw, messy public datasets and turned them into interactive dashboards and data stories. Each one was built for a specific business audience: venture capital executives, financial analysts at a major bank, and public health stakeholders.

Each project follows the same workflow an analyst uses on the job:

> **Define the business question → clean and model the data → build interactive visuals → turn the findings into a recommendation.**

---

## Highlights for Recruiters

| | |
|---|---|
| **Tools** | Tableau Desktop (2025.3), Excel, CSV/XLSX/Hyper data sources |
| **Core skills** | Data cleaning, calculated fields, Level of Detail (LOD) expressions, parameters, dashboard actions, data blending and joins, storytelling |
| **Business analysis** | Growth metrics (YoY, CAGR, median growth), segmentation, BCG-style strategic quadrant analysis, market prioritization |
| **Scale** | 4 Tableau workbooks · 27 worksheets · 5 dashboards · 2 story presentations (14 story points) · 40+ calculated fields |
| **Communication** | Two 7-page written analytical reports that turn charts into executive recommendations |
| **Collaboration** | Delivered a team project with a 5-person analytics team |

---

## Repository Structure

```
mgmt479/
├── assignments/
│   ├── Assignment 2.twbx        # Olympic medals × country demographics: joins, maps, dashboard actions
│   └── Assignment 3.twbx        # US COVID-19 × population: data blending, LODs, parameters
├── group_project/
│   ├── Group Project.twbx       # Global startup success analysis (interactive story)
│   └── MGMT 479 Group Project Report.pdf
└── individual_project/
    ├── Individual Project.twbx  # JPMorgan Chase branch network analysis (interactive story)
    └── MGMT 479 Individual Project Report.pdf
```

> **How to view:** `.twbx` files are packaged Tableau workbooks that include their data. Open them in [Tableau Desktop](https://www.tableau.com/products/desktop) or the free [Tableau Public](https://public.tableau.com/app/discover) / [Tableau Reader](https://www.tableau.com/products/reader). The PDF reports can be read directly on GitHub.

---

## Featured Project 1 (Individual Capstone): *How Did JPMorgan Chase Build and Grow Its Branch Network?*

📁 [`individual_project/`](individual_project/) · Dataset: [Chase Bank Branch Deposits 2010–2016 (Kaggle)](https://www.kaggle.com/datasets/chasebank/bank-deposits)

### Business problem
**Audience:** Financial analysts at JPMorgan Chase advising executives on where to grow the retail branch network next.

I analyzed **5,400+ branch records across 26 states** covering 7 years of deposit history (2010–2016) to answer six strategic questions. The questions run from *"Where are the branches and how big are they?"* to *"Where should the bank invest next?"*

### What I built
One **executive summary dashboard** and a **7-point interactive Tableau Story**. The dashboard has **6 cross-filtering dashboard actions**: clicking a state, city or branch type updates every other view.

| # | Visualization | Business question answered |
|---|---|---|
| 1 | **Symbol map** (lat/long, sized by deposits) | Where is deposit wealth geographically concentrated? |
| 2 | **Multi-series line chart** | Do organic branches outperform acquired ones over time? |
| 3 | **Dual-axis bar + line chart** | Which states are high-value and which are high-growth? |
| 4 | **Top-N ranked bar chart** (parameter-driven, Top 15) | Which cities drive total deposits? |
| 5 | **Treemap** | Does branch count translate into deposit wealth? |
| 6 | **Strategic quadrant scatter plot** with reference lines | Where should the bank invest next? |

### Technical work
- **Feature engineering with calculated fields:** Total Deposits, Branch Origin (Organic vs. Acquired, derived from null acquisition dates), Branch Type, and City-State keys.
- **Financial metrics built from scratch:**
  - *Average Year-over-Year Growth Rate*, with divide-by-zero guards (`IIF(... > 0, ..., NULL)`)
  - *Compound Annual Growth Rate (CAGR)*: `([2016 Deposits] / [2010 Deposits]) ^ (1/6) - 1`
- **Automated segmentation logic:** a calculated field sorts every state into **Star / Growth Opportunity / Cash Cow / Question Mark**, using deposit and CAGR thresholds. This is a BCG-matrix-style framework applied to bank branch strategy.
- **Parameters** for a configurable Top-N ranking, and **reference lines** that draw the quadrant boundaries.

### Key insights delivered
- **Organic branches beat acquired ones.** Organic branches averaged **$247K → $306K** in deposits versus **$105K → $174K** for acquired branches, and the gap widened after 2013.
- **High value and high growth rarely go together.** New York leads in deposits per branch (**$4.0M**) but grows modestly, while Georgia has the lowest deposits and the highest YoY growth (**24.8%**).
- **Scale does not equal performance.** California has the most branches (**999**), but New York holds more deposit wealth with only **739** branches.
- **Recommendation:** move investment away from saturated "Cash Cow" markets like New York and toward high-CAGR **Growth Opportunity** states (Georgia, Colorado, Florida, Nevada, New Jersey, Arizona).

---

## Featured Project 2 (Team Project): *How Is Startup Success Determined?*

📁 [`group_project/`](group_project/) · Dataset: [Global Startup Dataset (Kaggle)](https://www.kaggle.com/datasets/adarsh2626/startup-dataset)

### Business problem
**Audience:** Executives at venture capital firms (e.g., Andreessen Horowitz, Sequoia, Accel, General Catalyst) who need to quickly identify startups likely to produce a high ROI.

Working in a **5-person analytics team**, we studied **500+ startups across 30+ countries and 11 industries** (AI/ML, FinTech, HealthTech, SaaS, BioTech, CleanTech and more), using 3 years of revenue history and each company's outcome (Successful / Acquired / Failed).

### What we built
**Two interactive dashboards** and a **7-point Tableau Story** that ends in a framework of key startup success indicators.

| # | Visualization | Business question answered |
|---|---|---|
| 1 | **Parameter-driven horizontal bar chart** (toggle Individual vs. Team founders) | Which founders generate the highest short-term revenue? |
| 2 | **Treemap** | Where do startups cluster by country and outcome? |
| 3 | **Bubble chart** | Which countries produce startups that scale by Year 3? |
| 4 | **Cohort line chart** (median growth by launch year) | How do growth and volatility differ between successful and failed startups? |
| 5 | **Scatter/bubble plot** | Which regions combine high startup volume with high success rates? |
| 6 | **Stacked area chart** | How has the mix of startup outcomes changed from 2002 to 2022? |

### Technical work
- **Cleaning messy text data into numbers:** revenue was stored as text such as `"$1.2M"` and `"$850K"`. Nested `IF / CONTAINS / REPLACE / FLOAT` calculations convert it into numeric values for all three revenue years, with null and empty-string handling.
- **String parsing:** used `SPLIT` and `TRIM` to break a comma-separated founders field into separate founders, then counted founders per company to tell solo founders apart from founding teams.
- **Interactive parameter logic:** an *Individual/Team* parameter changes both the dimension and the measure on the founder chart. Calculated "implementor" fields make this work.
- **Derived metrics:** Year 1 → Year 2 growth %, Total Revenue, Average Year 3 Revenue, Success Flag / Success Rate, and distinct startup counts (`COUNTD`).
- **Geographic grouping:** a custom calculated field maps countries into regions (North America, Europe, Asia-Pacific, etc.).
- **Medians instead of means** in the growth analysis, so extreme startup outliers don't distort the trend.
- **4 cross-filtering dashboard actions** that link regions, countries, outcomes and founders.

### Key insights delivered
- **UAE, India and Japan** lead in the number of successful startups. **UK, South Korea and France** lead in average Year 3 revenue, which is the point where a startup has either scaled or plateaued.
- **Successful startups show higher and more consistent median growth.** Failed startups show the most volatility.
- **Asia-Pacific** has both the most startups and the largest total revenue. **Latin America** stands out as a possible untapped market.
- **Outcome:** a 9-factor framework of success indicators (Year 3 revenue, median growth, low volatility, founder credibility, government funding, R&D investment, and more) that VCs can use to screen high-ROI investments.

---

## Skill-Building Assignments

### Assignment 2: Olympic Medals × Country Demographics
📁 [`assignments/Assignment 2.twbx`](assignments/)
- **Joined two tables** (Olympic Medals and Country Demographics) with **left joins** to combine sports results with economic and population data.
- Built **8 worksheets**: a horizontal bar chart with a reference line, a symbol map, a scatter plot, a treemap, a bubble chart, a grouped vertical bar chart and a heatmap.
- Created calculated fields for **Population Density**, a combined **Country_Region** key, and an **Infant Mortality bucket** (High/Low) that segments countries.
- Built **2 dashboards** with **filter, highlight and hyperlink actions** to make exploration interactive.

### Assignment 3: US COVID-19 Cases × Population
📁 [`assignments/Assignment 3.twbx`](assignments/)
- **Blended two separate data sources** (county-level COVID-19 cases/deaths and 2018 US population estimates) on FIPS codes.
- Wrote **Level of Detail (LOD) expressions**:
  - `{FIXED [date], [state], [county], [fips] : SUM([cases])}` to fix case counts at a specific grain
  - `{FIXED [state] : SUM([deaths])} >= 500` as a state-level filter that keeps only states above a death threshold
- Built a **dynamic measure selector**: a parameter plus a `CASE` statement lets users switch a time-series chart between **cases and deaths**, and the chart title updates to match.
- Added a **Top N parameter** and hierarchical drill-downs (State → County → FIPS).

*(Assignment 1 covered data visualization in Excel and is not included here.)*

---

## Skills Demonstrated

**Data preparation and modeling**
- Joins, multi-source data blending, Tableau extracts (`.hyper`)
- Cleaning text fields into numeric values, string parsing, null and zero-division handling
- Custom groupings and classification logic

**Analytical calculations**
- Row-level and aggregate calculated fields
- LOD expressions (`FIXED`)
- Financial and growth metrics: YoY growth, CAGR, median growth, success rates
- Segmentation frameworks (strategic quadrant / BCG-style)

**Interactive design**
- Parameters (Top N, measure switching, category toggles)
- Dashboard actions (filter, highlight, hyperlink) for cross-filtering
- Dynamic titles, reference lines, dual-axis charts
- Tableau Stories for guided, step-by-step presentations

**Chart types used:** bar (horizontal, vertical, grouped, Top N), line, dual-axis, area (stacked), scatter, bubble, symbol map, treemap, heatmap

**Business communication**
- Framing analysis around a specific stakeholder and their decisions
- Writing up insights as clear, actionable recommendations in executive reports
- Teamwork on a multi-person analytics project

---

## About Me

I'm a student at **Purdue University** interested in **data analytics, business intelligence and data-driven strategy**. I like turning complex datasets into clear stories that help people make better decisions. I'm currently looking for **internship and full-time opportunities** in data analytics, business analytics, BI and consulting roles.

📫 Feel free to reach out through my GitHub profile. I'd love to connect!

---

### Acknowledgments
Course: MGMT 47900 – Data Visualization, Purdue University, taught by Dr. Alok Chaturvedi.
Group project team: Aidan Hershberger, Arman Hyder, Evan Hunt, Niharika Rai, Tyler Wichman.
Datasets are publicly available on Kaggle and are used for educational purposes.
