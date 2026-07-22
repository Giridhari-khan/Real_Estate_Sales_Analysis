# 📊 US Real Estate Sales Analysis - Tableau Dashboard

> **An enterprise-grade data analytics project leveraging a dataset of over 526,000 property transactions to uncover market trends, geographic sales performance, and assessment valuation accuracy using Tableau.**

---
### Check Dashboard Here : [Tableau Public Live Interactive Link](https://public.tableau.com/app/profile/giridhari.khan/vizzes)

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
- Which calendar year represents the historic peak of our real estate market?
- Which specific states and towns generate the highest total sales volume?
- Which property type commands the highest consumer demand and transaction volume?
- In which towns are properties underperforming and selling below government tax valuations?- How can leadership use historical price surges to set accurate property pricing models for next year?
- Where should corporate investment capital be reallocated to maximize returns based on regional performance?

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

### Top Row: KPI Blocks & Filters.
Placed at the top of the canvas layout to offer instant performance metrics:
**Total Real Estate Revenue**: `SUM(Sale Amount)` formatted as Currency ($B).


---

# 🛠 Tools & Technologies
* **BI Platform**: Tableau Public
* **Calculated Field Analytics**: Custom Tableau Level of Detail (LOD) and Aggregation Calculations
* **Documentation Stack**: Markdown (`.md`), Git Version Control

---

# 🔄 Data Preprocessing Workflow

To ensure performance and dashboard accuracy, the following extraction data treatments are applied at the workbook data-source level:
1. **Missing Data Mitigation**: Row filters are instantiated on `Property Type` and `Residential Type` sheets to drop null values from visual encodings without omitting total row financial aggregations(I choose to keep the null for those columns ).
2. **Temporal Structuring**: `Date Recorded` is parsed through Tableau's native calendar hierarchy to extract continuous historical timelines.
3. **Financial Formatting**: Aggregated currency measures (`Sale Amount`, `Assessed Value`) are explicitly converted to billions (\$B) with custom user-facing tooltips to maximize workspace scannability.

---

# 📈 Visualizations & Sheet Configurations

#### 1. Stacked-Bar Chart: Total Sales Amount by Town
* **Rows**: `Town` 
* **Columns**: `SUM(Sale Amount)`
* **Color**: `Town` *(Using a distinct, categorical color palette)*
* **Label**: `SUM(Sale Amount)` *(Formatted as Currency in Billions with $)*
* **Title**: Total Sales Volume by Town

#### 2. Line Chart: Annual Sales Amount Trend
* **Rows**: `SUM(Sale Amount)`
* **Columns**: `YEAR(Date Recorded)`
* **Color**: `Sale Amount` 
* **Label**: `SUM(Sale Amount)` *(Constrained to line markers at min/max bounds for visual clarity)*
* **Title**: Year over Year sales

#### 3. Bar Chart: Sales Amount and Assessed Value as per Year
* **Rows**: `Sales Year`
* **Columns**: `SUM(Sale Amount) & SUM(Assessed Value)`
* **Color**: `AVG(Sales Ratio)` *(Utilizing a continuous Red-Blue Diverging ramp to show assessment variances)*
* **Label**: `SUM(Sale Amount) & SUM(Assessed Value)`
* **Title**: Sales Amount and Assessed Value as per Year
* **Filter**: Dropdown in between - Sale Amount & Assessed Value

#### 4. Pie Chart: Distribution of Property Types
* **Marks Type**: `Pie`
* **Color**: `Property Type` *(Using a distinct, categorical color palette)*
* **Angle**: `COUNT(Property Type)` or `SUM(Sale Amount)` *(to drive slice sizes)*
* **Label**: `Property Type` and `COUNT(Property Type)` *(showing text and raw volume values)*
* **Title**: Distribution of Property Types

#### 5. Treemap: Sales Volume for Residential Type
* **Marks Type**: `Square`
* **Size**: `SUM(Sale Amount)` *(to size the rectangular blocks)*
* **Color**: `Property Type` *(Using a sequential blue gradient based on sales magnitude)*
* **Label**: `Property Type` and `SUM(Sale Amount)` *(Formatted as Currency in Billions with $)*
* **Title**: Sales Volume for Residential Type

#### 6. Geographic Map: Sales Distribution by State
* **Marks Type**: `Map` *(Filled Map style)*
* **Detail**: `State` *(Geographic Role set to State/Province)*
* **Color**: `SUM(Sale Amount)` *(Using a continuous green sequential gradient color ramp)*
* **Label**: `State` and `SUM(Sale Amount)` *(Formatted as Currency in Billions with $)*
* **Title**: Sales Distribution by State

#### 7. Highlight Table / Heatmap: Average Sales Ratio
* **Rows**: `Town`
* **Columns**: `Property Type`
* **Marks Type**: `Square`
* **Color**: `AVG(Sales Ratio)` *(Using a continuous green sequential color ramp for shading background cells)*
* **Label**: `AVG(Sales Ratio)` *(Formatted as a standard decimal number showing the multiplier)*
* **Title**: Average Sales Ratio

#### 8. Text KPI Card: Total Sales
* **Marks Type**: `Text`
* **Text / Label**: `SUM(Sale Amount)` *(Formatted as a large font size, bold currency value: **$234.63B**)*
* **Title**: Total Sales


---

# 💡 Key Strategic Insights

*   **Capitalization on Market Peaks:** Corporate pricing baselines and financial projections should remain heavily anchored around the **2021 historical revenue benchmark ($40.25B)** to optimize profit margins without underpricing high-value inventory.
*   **Geographic Capital Allocation:** Investment budget, marketing spend, and inventory acquisitions should be aggressively funneled into high-performing revenue corridors like **Indiana, Alaska, and Washington**, which serve as the primary drivers of geographical market heat.
*   **Residential Volume Prioritization:** Resource management and sales operations must stay heavily weighted toward **Single Family homes**, as they completely dominate the market structure with a massive consumer footprint of over **352,000+ distinct transactions**.


---

# ▶️ How to Access the Dashboard
1. Ensure access to internet browsers or active corporate networks.
2. Navigate directly to the public interactive workbook file repository.
3. Launch the compiled dashboard on the server via [Tableau Public Live Interactive Link](https://public.tableau.com/app/profile/giridhari.khan/vizzes).
4. Utilize top-banner context controls to slice performance tracking filters dynamically by specific years or local municipalities.

---

# 📌 Business Recommendations
*   **Launch Targeted Regional Expansions:** Deploy localized marketing campaigns and establish field offices within the identified high-revenue hubs (**Indiana, Alaska, and Washington**) to capture immediate local market share and maximize return on investment.
*   **Optimize Single-Family Inventory Channels:** Streamline acquisition pipelines and vendor networks to increase the inventory portfolio of **Single Family homes**, aligning corporate supply directly with the primary consumer demand channel.
*   **Establish Data-Driven Valuation Standards:** Mandate that all future listing prices use the historical **2021 sales benchmarks** as a protective floor, preventing underpricing in high-demand zones while using sales-to-assessed ratios to flag high-risk overvalued areas.


---

# 🚀 Future Enhancements
* **Predictive Forecasting Models**: Overlaying built-in Tableau exponential smoothing models onto the continuous line chart to project coming sales volume trends.

---

## 👤 Author & Contact

**Giridhari Khan**
:- Data Analytics 

| Platform | Link |
|---|---|
| 🐙 GitHub | [github.com/Giridhari-khan](https://github.com/Giridhari-khan) |
| 💼 LinkedIn | [Linkedin](https://linkedin.com/in/your-profile) |
| 📊 Dune | [dune.com/giridharikhan](https://dune.com/giridharikhan) |
| 📧 Email | khangiridhari8967@gmail.com |
| Tableau Public | [Tableau Public](https://public.tableau.com/app/profile/giridhari.khan/vizzes) |

---

⭐ *If you found this project useful, consider giving it a star on GitHub!*
