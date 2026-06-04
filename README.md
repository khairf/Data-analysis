# Data-analysis
# End-to-End Customer Shopping Behavior Analytics

An advanced, corporate-level data analytics project that spans the entire data lifecycle—from initial business problem definition and data manipulation to advanced database querying, interactive dashboarding, formal documentation, and stakeholder presentation.

---

## 📌 Project Overview
A leading retail company sought to understand its customers' shopping behaviors to drive sales growth, enhance customer satisfaction, and build long-term brand loyalty. Management observed changing purchase patterns across different demographics, product groups, and sales channels. 

This project solves the core business question: **How can the company leverage customer transaction and profile data to identify actionable trends, improve engagement, and optimize marketing and product strategies?**

---

## 🛠️ Tech Stack & Lifecycle Tools
- **Data Cleaning & Feature Engineering:** Python (`pandas`, `Jupyter Notebook`)
- **Database Management & Advanced Analytics:** PostgreSQL (`pgAdmin`, `SQLAlchemy`, `psycopg2`)
- **Data Visualization & BI:** Power BI Desktop
- **Documentation & Communication:** Gamma AI (Presentation), Microsoft Word (Project Report), GitHub (Version Control)

---

## 🚀 Step-by-Step Implementation

### Step 1: Data Preparation & Exploration (Python)
- **Data Profiling:** Loaded raw transactional customer datasets using `pandas` to inspect structures, columns, and baseline data types (`df.info()`, `df.describe()`).
- **Smart Imputation:** Handled missing values in the `review_rating` column. Rather than applying a broad, biased global mean or median, missing values were imputed dynamically using the **median review rating within each specific product category** to preserve the natural variation of the data.
- **Data Standardization:** Re-formatted all mixed-case and spaced column headers into consistent `snake_case` to prevent syntactic errors during database staging.
- **Feature Engineering:**
  - Segmented granular continuous customer ages into uniform, distribution-driven cohorts (`young adult`, `adult`, `middle-aged`, `senior`) using quantile binning (`pd.qcut()`).
  - Transformed categorical purchase frequencies (`weekly`, `monthly`, `quarterly`) into explicit numeric day intervals (`7`, `30`, `90`) using structural dictionary mapping (`.map()`) to optimize downstream aggregate calculations.
- **Redundancy Filtering:** Statistically validated that `discount_applied` and `promo_code_used` held perfectly redundant values, resulting in dropping the duplicate column to keep the schema lean.

### Step 2: Advanced Database Analytics (SQL)
Using `SQLAlchemy`, the cleaned dataframe was automatically written into a local PostgreSQL instance as a staging table to execute complex, production-grade business queries:
1. **Demographic Revenue Contribution:** Calculated and compared absolute revenue shares generated between genders to optimize marketing spend allocation.
2. **Promotional Value Elasticity:** Isolated high-value customers who consistently bought above-average transaction values despite applying discounts.
3. **Product Health Check:** Identified top-performing items based on average ratings by explicitly type-casting double-precision data formats into precise numerics.
4. **Logistics Optimization:** Evaluated average basket values between `Standard` vs. `Express` shipping models, providing justification for deeper logistics investments if premium shipping correlates with larger spends.
5. **Subscription Viability Analysis:** Compared the transaction count, average basket size, and overall revenue between subscribed and non-subscribed groups to gauge loyalty model health.
6. **Discount Dependency Index:** Applied conditional aggregation (`SUM(CASE WHEN...) / COUNT(*) * 100`) to uncover which specific inventory items depend heavily on markdowns to convert.
7. **Customer Cohort Segmentation:** Engineered a Common Table Expression (CTE) utilizing logical `CASE WHEN` parameters to categorize the customer base into `New`, `Returning`, and `Loyal` cohorts based on historical touchpoints.
8. **Intra-Category Leaderboard:** Utilized window functions (`ROW_NUMBER() OVER (PARTITION BY category ORDER BY COUNT(customer_id) DESC)`) to pull a ranked leaderboard of the top 3 items within every distinct product category.

### Step 3: Interactive Dashboard Development (Power BI)
Built a high-fidelity, interactive business dashboard linked directly to the PostgreSQL database:
- **KPI Cards:** Built optimized card visualizations for core tracking metrics: Total Unique Customers, Average Transaction Value (USD-formatted), and Average Review Score.
- **Distribution Analysis:** Maintained clear breakdown visuals (Donut Charts) representing customer distributions by subscription profile.
- **Performance Breakdowns:** Plotted side-by-side Clustered Column Charts tracking raw Revenue vs. Total Sales Orders across item categories.
- **Demographic Matrices:** Developed Horizontal Bar Charts breaking down operational volume and dollar yields across specific age cohorts.
- **Stakeholder Interactivity:** Integrated advanced slicer trees (button grids and list-filters) across `Subscription Status`, `Gender`, `Category`, and `Shipping Type` to enable real-time parameter tuning for senior leaders.

### Step 4: Executive Reporting & Artifacts
- **Technical Report:** Documented exact code execution steps, architectural schemas, and pipeline structures.
- **Client Presentation:** Generated an executive-facing slide deck to distill technical charts into a high-level business pitch highlighting key revenue drivers (e.g., Young Adults leading spending; Express shipping yielding higher baskets).

---

## 📊 Core Business Insights & Recommendations
- **Demographic Focus:** The **Young Adult** demographic represents the primary engine of total revenue. Tailor high-impact digital campaigns specifically to this segment.
- **Shipping Monetization:** Customers choosing **Express Shipping** show a higher average spend per transaction. Accelerating fast-delivery logistics and marketing express-tier options will drive margin growth.
- **Subscription Program Hook:** Non-subscribed customers have an average single-purchase spend almost identical to active subscribers, yet they drive higher cumulative revenue due to volume. Introducing mid-tier incentive structures can effectively convert high-volume casual buyers into recurring subscribers.

---

## 📂 Repository Structure
```text
├── data/
│   └── customer_shopping_behavior.csv    # Raw & Cleaned Dataset
├── notebooks/
│   └── data_cleaning_eda.ipynb           # Python Notebook (Pandas cleaning/imputation)
├── sql/
│   └── analytical_queries.sql            # Production PostgreSQL scripts
├── dashboard/
│   └── behavior_analytics_report.pbix     # Power BI Dashboard file
├── reports/
│   ├── project_documentation.pdf         # Detailed Technical Report
│   └── executive_presentation.pdf        # Stakeholder Slide Deck
└── README.md                             # Project Documentation
