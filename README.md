# cyclistic-bike-share-analysis
Comparative behavioral analysis of 4.58M+ Cyclistic bike-share trips across 2025 using Python and Tableau.
# Cyclistic Bike-Share Case Study: Member vs. Casual Rider Behavioral Analysis

## Executive Summary
This project analyzes **4.58M+ cleaned bike-share trips** across 2025 for **Cyclistic**, a fictional bike-share company in Chicago. 

The primary business objective set by Marketing Director **Lily Moreno** is to identify key behavioral differences between **annual members** and **casual riders** to design targeted, data-backed marketing strategies aimed at converting high-volume casual riders into profitable annual members.

---

## 📊 Live Interactive Dashboard
👉 **[View the Live Cyclistic Tableau Public Dashboard](https://public.tableau.com/app/profile/jason.fair7301/viz/CyclisticAnalysis_17935763590110/Overview)**

---

## 🧭 Project Roadmap & Methodology (Ask, Prepare, Process, Analyze, Share, Act)

### 1. Ask
* **Business Problem:** Annual members generate significantly higher, more stable revenue margins than single-ride or day-pass users. Rather than relying on generic awareness campaigns to acquire new users, Cyclistic aims to convert existing casual riders into annual members.
* **Core Business Question:** How do annual members and casual riders use Cyclistic bikes differently?
* **Primary Stakeholders:** Lily Moreno (Director of Marketing) and the Cyclistic Executive Team.

### 2. Prepare
* **Data Source:** 12 monthly trip files (January–December 2025) released by Motivate International Inc. under an open data license.
* **Integrity & Privacy:** Fully anonymized data. In compliance with strict data-privacy guidelines, no Personally Identifiable Information (PII) or financial/billing information is included.
* **ROCCC Evaluation:** Reliable, Original, Comprehensive, Current (2025 full-year data), and Cited.

### 3. Process & Data Pipeline
Processing 12 months of high-volume trip logs (~4.5M+ rows) exceeds the capacity of standard spreadsheet tools (which cap out at 1,048,576 rows). To ensure reproducible, end-to-end data hygiene:
* **Ingestion:** Built a scalable Python (Pandas) ingestion script targeting required dimensions to optimize system memory.
* **Feature Engineering:**
  * Calculated `ride_length_min` from `started_at` and `ended_at`.
  * Extracted categorical time dimensions: `day_of_week`, `month`, and `hour`.
* **Data Hygiene & Outlier Filtering:**
  * Deduplicated records by `ride_id`.
  * Removed false docks and instant cancellations ($\le 1 \text{ minute}$).
  * Filtered out maintenance and stolen bike anomalies ($\ge 24 \text{ hours}$ / $1,440 \text{ minutes}$).
* **Aggregated Export:** Exported optimized dimensional summary datasets (`cyclistic_tableau_aggregated.csv` and `cyclistic_tableau_stations.csv`) to enable instantaneous dashboard responsiveness.

---

## 🔍 Key Analytical Findings

| Dimension | Annual Members (64.0% of Total) | Casual Riders (36.0% of Total) | Strategic Implication |
| :--- | :--- | :--- | :--- |
| **Primary Use Case** | Daily Commute & Transit | Recreation, Tourism & Leisure | Members prioritize utility; casual riders prioritize lakefront recreation. |
| **Trip Duration** | **12.4 minutes** (Consistent) | **24.6 minutes** (**1.98x longer**) | Casual riders pay steep per-minute fees; position annual passes as cost savings. |
| **Weekly Pattern** | Surges **Tuesday–Thursday** (commute hours) | Surges **Saturday–Sunday** (midday peak) | Member volume concentrates on weekdays; casual volume spikes on weekends. |
| **Seasonality** | Stable across 9–10 months | Extreme summer surge (**62.3%** in Jun–Sep) | Seasonal campaigns must launch aggressively May through August. |
| **Top Hubs** | Train depots, commercial corridors, universities | Navy Pier, Millennium Park, Lake Shore Drive | Casual demand is concentrated along coastal and recreational stations. |

---

## 🎯 Top 3 Strategic Recommendations (Act Phase)

1. **Launch a Seasonal Summer-to-Annual Ramp:**
   * *Evidence:* Over 62% of casual volume takes place between June and September.
   * *Strategy:* Offer a 4-month "Summer Pass" that automatically credits 100% of its cost toward an Annual Membership if the user upgrades before September 30.

2. **Geo-Targeted In-App Prompts at High-Density Waterfront Hubs:**
   * *Evidence:* Casual riders concentrate heavily at lakefront leisure stations (e.g., *Streeter Dr & Grand Ave*, *Millennium Park*) with average trip lengths exceeding 30 minutes.
   * *Strategy:* Trigger real-time mobile notifications upon docking at coastal hubs showing cost comparisons: *"You spent \$X on today's 30-minute ride. Switch to an Annual Pass and save \$Y per month."*

3. **Electric Fleet Trial & Member Perks:**
   * *Evidence:* Casual riders choose electric options at a noticeably higher rate than annual members.
   * *Strategy:* Include bundled monthly electric bike minutes or waived unlock fees in the annual membership package to incentivize tech-forward casual users to commit.
## 📑 Executive Presentation
* 📄 **[View Executive Presentation (PDF)](assets/Cyclistic_Executive_Presentation.pdf)** *(Instant browser preview)*
* 📥 **[Download PowerPoint Deck (.pptx)](assets/Cyclistic_Executive_Presentation.pptx)**
---

## 📁 Repository Structure

cyclistic-bike-share-analysis/
│
├── README.md                                  # Complete project documentation & portfolio writeup
├── cyclistic_analysis.ipynb                   # End-to-end Python pipeline (cleaning, EDA, aggregation)
├── requirements.txt                           # Environment dependencies (pandas, numpy, openpyxl)
├── .gitignore                                 # Excludes large raw data files and cache
│
├── assets/                                    # Executive deliverables & visual media
│   ├── Cyclistic_Executive_Presentation.pdf   # Primary slide deck (instant in-browser preview)
│   ├── Cyclistic_Executive_Presentation.pptx  # Editable PowerPoint source deck
│   ├── logo.png                               # Cyclistic brand asset
│   └── dashboard_preview.png                  # Full Tableau dashboard preview screenshot
│
└── exports/                                   # High-performance analytical summary tables
    ├── cyclistic_tableau_aggregated.csv       # Pre-aggregated KPIs, seasonality, and hourly curves
    ├── cyclistic_tableau_stations.csv         # Ranked station coordinates for geographic mapping
    └── Cyclistic_2025_Summary_Export.xlsx     # Multi-tab styled workbook with embedded pivot charts
