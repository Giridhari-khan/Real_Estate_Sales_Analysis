# 📊 US Real Estate Sales Analysis - Tableau Dashboard

> **An enterprise-grade data analytics project leveraging a dataset of over 526,000 property transactions to uncover market trends, geographic sales performance, and assessment valuation accuracy using Tableau.**

---

# 📌 Table of Contents
- [Overview](#-overview)
- [Problem Statement](#-problem-statement)
- [Dataset Schema](#-dataset-schema)
- [Dashboard Architecture](#-dashboard-architecture)
- [Tools & Technologies](#-tools--technologies)
- [Data Preprocessing Workflow](#-data-preprocessing-workflow)
- [Visualizations & Sheet Configurations](#-visualizations--sheet-configurations)
- [Key Strategic Insights](#-key-strategic-insights)
- [How to Access the Dashboard](#-how-to-access-the-dashboard)
- [Business Recommendations](#-business-recommendations)
- [Future Enhancements](#-future-enhancements)
- [Author & Contact](#-author--contact)

---

# 📖 Overview
In the real estate sector, understanding historical transactional data is key to predicting market growth, setting public policy, and optimizing investment returns. 

This project delivers a robust **Real Estate Sales Performance & Market Analysis Dashboard** built in Tableau. By profiling **526,276 historical sales records**, the dashboard transforms complex tabular data spanning timelines, towns, and property types into interactive, high-density visual insights. It maps out geographic revenue distribution, temporal volume changes, and checks the operational accuracy of property tax assessments against true market values.

---

# ❓ Problem Statement
Asset management firms, urban planners, and tax assessors struggle to parse millions of rows of real estate data to extract clear macro-trends. This project directly addresses critical operational bottlenecks:
- Which property sectors represent the bulk of transactional liquidity?
- Are home values expanding year-over-year, or is market performance cyclical?
- Which town micro-markets generate the highest gross capital volume?
- How accurate are public municipal tax assessments compared to realized free-market sale amounts?
- Where are the regional pricing discrepancies where buyers consistently pay premiums over assessed values?

---

# 📊 Dataset Schema
The dataset consists of **526,276 entries** documenting property sales transactions with financial and spatial variables.

### Data Profiling Summary
* **RangeIndex:** 526276 entries (0 to 526275)
* **Total Columns:** 14 features

| # | Column Name | Non-Null Count | Data Type | Description |
|---|---|---|---|---|
| 0 | **Serial Number** | 526276 | int64 | Unique transactional identifier |
| 1 | **List Year** | 526276 | int64 | Year the property was indexed for market |
| 2 | **Date Recorded** | 526276 | datetime64[us] | Official date the final deed sale was logged |
| 3 | **Town** | 526276 | str | Municipal geographic market location |
| 4 | **Address** | 526273 | object | Street address of the parcel |
| 5 | **Assessed Value** | 526276 | int64 | Tax assessor’s certified valuation |
| 6 | **Sale Amount** | 526276 | float64 | Actual finalized sales market price |
| 7 | **Sales Ratio** | 526276 | float64 | Financial ratio (`Assessed Value / Sale Amount`) |
| 8 | **Property Type** | 492104 | str | Broad usage category (e.g., Residential, Commercial) |
| 9 | **Residential Type**| 480666 | str | Housing sub-classification (e.g., Single Family, Condo) |
| 10| **Non Use Code** | 162727 | str | Special operational tracking exemption codes |
| 11| **Assessor Remarks**| 127153 | object | Open-text notes left by the local municipal assessor |
| 12| **OPM remarks** | 11365 | str | Office of Policy and Management state auditor notes |
| 13| **State** | 526276 | str | Regional state boundary identifier |

---

# 📂 Dashboard Architecture
* **Canvas Size**: Fixed Desktop Layout (1400 x 900 pixels) for professional desktop grid deployment.
* **UI Color Palette**: Corporate Blue & Slate Gray with a high-contrast Diverging palette (Red-Blue) for comparative ratio analysis.
* **Global Interaction Filters**: Fixed top-banner containing context filters for `List Year`, `Town`, and `Property Type`.

### Top Row: High-Level KPI Blocks
Placed at the top of the canvas layout to offer instant performance metrics:
1. **Total Real Estate Revenue**: `SUM(Sale Amount)` formatted as Currency ($B).
2. **Systemic Pricing Accuracy**: `AVG(Sales Ratio)` to track systemic deviation from target baseline valuation.
3. **Total Transactional Liquidity**: `COUNT(Serial Number)` to track total market transaction volume.

---

# 🛠 Tools & Technologies
* **BI Platform**: Tableau Desktop / Tableau Public
* **Data Core Engine**: Tableau Hyper Extract Engine 
* **Calculated Field Analytics**: Custom Tableau Level of Detail (LOD) and Aggregation Calculations
* **Documentation Stack**: Markdown (`.md`), Git Version Control

---

# 🔄 Data Preprocessing Workflow

To ensure performance and dashboard accuracy, the following extraction data treatments are applied at the workbook data-source level:
1. **Missing Data Mitigation**: Row filters are instantiated on `Property Type` and `Residential Type` sheets to drop null values from visual encodings without omitting total row financial aggregations.
2. **Temporal Structuring**: `Date Recorded` is parsed through Tableau's native calendar hierarchy to extract continuous historical timelines.
3. **Financial Formatting**: Aggregated currency measures (`Sale Amount`, `Assessed Value`) are explicitly converted to millions (\$M) and billions (\$B) with custom user-facing tooltips to maximize workspace scannability.

---

# 📈 Visualizations & Sheet Configurations

#### 1. Bar Chart: Total Sales Volume by Property Type
* **Rows**: `Property Type` *(Filtered to exclude Null values)*
* **Columns**: `SUM(Sale Amount)`
* **Color**: `Property Type` *(Using a distinct, categorical color palette)*
* **Label**: `SUM(Sale Amount)` *(Formatted as Currency in Millions/Billions)*
* **Title**: Total Sales Volume by Property Type

#### 2. Line Chart: Annual Sales Amount Trend
* **Rows**: `SUM(Sale Amount)`
* **Columns**: `YEAR(Date Recorded)`
* **Color**: `Residential Type` *(Filtered to exclude Null values)*
* **Label**: `SUM(Sale Amount)` *(Constrained to line markers at min/max bounds for visual clarity)*
* **Title**: Annual Sales Amount Trend by Residential Type

#### 3. Horizontal Bar Chart: Top 10 Towns by Total Sales Revenue
* **Rows**: `Town` *(Sorted descending by Sale Amount, restricted via Top 10 filter engine)*
* **Columns**: `SUM(Sale Amount)`
* **Color**: `AVG(Sales Ratio)` *(Utilizing a continuous Red-Blue Diverging ramp to show assessment variances)*
* **Label**: `SUM(Sale Amount)`
* **Title**: Top 10 Towns by Total Sales Revenue

#### 4. Scatter Plot: Valuation Accuracy Analysis
* **Rows**: `SUM(Sale Amount)`
* **Columns**: `SUM(Assessed Value)`
* **Color**: `Property Type`
* **Shape**: `Property Type`
* **Detail**: `Town` *(Dropped directly into Detail shelf to distribute records across the canvas coordinates, preventing data-point overlap)*
* **Reference Line**: Analytical 1:1 Trend Line added across the grid coordinates to visualize the exact match baseline where Assessed Value equals Sale Amount.
* **Title**: Valuation Accuracy: Assessed Value vs. Actual Sale Amount

---

# 💡 Key Strategic Insights
* **Property Sector Dominance**: Residential assets hold the highest transactional share of sales volume across all historical transaction cycles.
* **Sub-Market Discrepancy**: Distinct town clusters consistently map above the 1:1 scatter plot trend line, signaling competitive geographic micro-climates where final sales premiums drastically outperform government tax assessments.
* **Sales Ratio Stability**: Aggregated divergence tracking across continuous years reveals macroeconomic timeline shifts, exposing exact quarters where local economic growth outpaces static municipal assessment lifecycles.

---

# ▶️ How to Access the Dashboard
1. Ensure access to internet browsers or active corporate networks.
2. Navigate directly to the public interactive workbook file repository.
3. Launch the compiled dashboard on the server via [Tableau Public Live Interactive Link](https://public.tableau.com/app/profile/giridhari.khan/vizzes).
4. Utilize top-banner context controls to slice performance tracking filters dynamically by specific years or local municipalities.

---

# 📌 Business Recommendations
* **Dynamic Valuation Models**: Tax administration authorities should adjust assessment formulas in the high-performing top 10 revenue towns to better match ongoing premium real estate sale values.
* **Institutional Investment Focus**: Capital investment firms can use the trend lines to track residential categories showing resilient year-over-year pricing growth.
* **Audit Triggers**: Flag any transactions that deviate significantly from the 1:1 scatter plot trend line for manual review using `Assessor Remarks` and `OPM remarks`. This helps catch typos or non-arms-length property transfers.

---

# 🚀 Future Enhancements
* **Spatial Mapping Integration**: Injecting geographic spatial shapefiles (`.shp`) to generate interactive municipal fill-maps directly within Tableau.
* **Advanced Forensic Audit Sheets**: Creating a drill-down analysis page built exclusively around `Non Use Code` and `OPM remarks` to catch outlier sales variances.
* **Predictive Forecasting Models**: Overlaying built-in Tableau exponential smoothing models onto the continuous line chart to project coming sales volume trends.

---

# 👨‍💻 Author & Contact

**Giridhari Khan** – Data Analytics Specialist

| Platform | Profile Link |
|---|---|
| 🐙 **GitHub** | [github.com/Giridhari-khan](https://github.com/Giridhari-khan) |
| 💼 **LinkedIn** | [linkedin.com/in/your-profile](https://linkedin.com/in/your-profile) |
| 📊 **Dune Analytics** | [dune.com/giridharikhan](https://dune.com/giridharikhan) |
