# Atlicon Consolidated Pipeline: Unifying Data After Acquisition

## Executive Summary

When Atlicon, a leading FMCG manufacturer, acquired Sports Bar (a smaller startup), they faced a critical challenge: **two companies, two separate data systems, and no unified view of the combined business**. The COO needed consolidated analytics for supply chain and inventory forecasting—fast.

**The Challenge:** Data scattered across disparate sources, manual reporting taking days, and stakeholders making decisions with incomplete information.

**The Solution:** Built an end-to-end automated data platform on Databricks that consolidates data from both companies into a single, governed lakehouse—delivering real-time insights through interactive dashboards and AI-powered analytics.

**The Impact:** Delivered in 3 weeks. Stakeholders now have a unified view of the business, automated daily updates, and self-service analytics—all on a scalable platform designed for long-term growth.

---

## The Business Challenge

After the acquisition, leadership faced three critical requirements:

1. **Unified Analytics**: Provide aggregated reporting across both Atlicon and Sports Bar operations
2. **Low Learning Curve**: Enable new team members to quickly adopt the system
3. **Long-Term Scalability**: Build a foundation that supports the combined entity for years to come

**The problem wasn't just technical—it was operational.** Finance needed consolidated revenue reports. Supply chain needed visibility into inventory across both companies. Executives needed confidence that decisions were based on complete, accurate data.

---

## The Solution: A Unified Data Platform

![System Architecture](./consolidated_pipeline/Docs/architecture_system_diagram.png)

*End-to-end pipeline: Raw data from both companies → Cloud storage → Databricks processing → Business intelligence*

### Architecture: Designed for Clarity and Growth

Built on **medallion architecture** (Bronze → Silver → Gold), the platform separates concerns clearly:

* **Bronze Layer**: Raw data ingestion from both companies (customers, products, pricing, orders)
* **Silver Layer**: Cleaned, standardized, and validated data ready for analysis
* **Gold Layer**: Business-ready tables and metrics optimized for reporting and forecasting

**Why this matters to the business:** Data quality improves at each layer. When analysts query the Gold layer, they're working with trusted, validated data—no more "which number is right?" debates in meetings.

### Technology Stack

* **Platform**: Databricks (Lakehouse architecture)
* **Storage**: Delta Lake with Unity Catalog governance
* **Compute**: Serverless (auto-scaling, cost-optimized)
* **Data Source**: AWS S3
* **Languages**: Python (PySpark), SQL

---

## Delivering Business Value

### 1. Automated Data Operations: Set It and Forget It

![Job Workflow](./consolidated_pipeline/Docs/job_task_dependency.png)

*4-task automated workflow running nightly: dimensions first, then facts*

**The business outcome:** No more manual data refreshes. Every morning, stakeholders see yesterday's data—automatically processed, validated, and ready for analysis. The pipeline runs at 11 PM daily, completing in under 10 minutes with 100% reliability.

![Job Run History](./consolidated_pipeline/Docs/job_run_history.png)

*Consistent execution: Multiple successful runs with predictable performance*

**What this solved:** Before automation, someone had to manually run reports every week—taking hours and prone to errors. Now? Zero manual intervention. The data team focuses on insights, not plumbing.

---

### 2. Executive Dashboards: Insights at a Glance

![Atlicon BI 360 Dashboard](./consolidated_pipeline/Docs/dashboard_full_view.png)

*Atlicon BI 360: Comprehensive view of revenue, products, customers, and channels*

Built **Atlicon BI 360**, an interactive dashboard that answers the questions leadership asks every week:

**"How are we performing this quarter?"**

![Monthly Revenue Trend](./consolidated_pipeline/Docs/dashboard_monthly_revenue.png)

*Revenue trends over time—spot growth or decline immediately*

**"Which products drive the business?"**

![Top Products by Revenue](./consolidated_pipeline/Docs/dashboard_top_products.png)

*Top 10 products ranked by revenue contribution*

**"Where are sales coming from?"**

![Revenue by Channel](./consolidated_pipeline/Docs/dashboard_revenue_channel.png)

*Channel breakdown showing distribution across retail, online, and distributor networks*

**"What are our key metrics?"**

![KPI Cards](./consolidated_pipeline/Docs/dashboard_kpi_cards.png)

*At-a-glance KPIs: customer count, average prices, quantities*

**The business outcome:** Executives no longer wait days for reports. They open the dashboard during meetings and see live data. When the COO asks "what's driving Q4 performance?", the answer is one click away.

#### Self-Service Exploration

![Global Filters](./consolidated_pipeline/Docs/dashboard_global_filters.png)

*Filter by category, channel, time period—explore data independently without waiting for analysts*

**What this solved:** Before, every "can you slice by category?" request meant a 2-day turnaround. Now, stakeholders filter and drill down themselves.

---

### 3. AI-Powered Analytics: Ask Questions in Plain English

![Genie Space Overview](./consolidated_pipeline/Docs/genie_space_overview.png)

*FMCG Sales and Orders Analytics: Natural language interface to the entire dataset*

Built a **Genie Space** where anyone can ask business questions without writing SQL. Analysts, finance, and operations teams now explore data conversationally.

**Example Questions Answered:**

**"Show me total revenue by quarter"**

![Revenue by Quarter](./consolidated_pipeline/Docs/genie_query_revenue_quarter.png)

*Instant quarterly revenue breakdown with automatic SQL generation*

**"What are the top 5 customers by sold quantity?"**

![Top Customers](./consolidated_pipeline/Docs/genie_query_top_customers.png)

*Customer ranking with quantities—no SQL required*

**"What are the top 5 products by revenue?"**

![Top Products](./consolidated_pipeline/Docs/genie_query_top_products.png)

*Product performance analysis in seconds*

**The business outcome:** Democratized data access. Non-technical stakeholders get answers in 30 seconds instead of submitting requests and waiting days. The data team's capacity freed up for strategic projects.

---

### 4. Data Quality: From Messy to Trustworthy

![Data Quality Transformation](./consolidated_pipeline/Docs/data_quality_transformation.png)

*Before (left): Inconsistent formats, negatives, unknowns. After (right): Standardized, validated, analysis-ready.*

**The challenge:** Raw data from both companies arrived in different formats—dates written 5 different ways, negative prices, "unknown" values littering columns.

**The solution:** Built automated validation and standardization at the Silver layer—transforming chaos into consistency.

**The business outcome:** Analysts trust the data. When Finance runs revenue reports, they're confident the numbers are accurate. No more "wait, why is this price negative?" fire drills.

---

## Project Outcomes

| Metric | Before Consolidation | After Implementation | Business Impact |
|--------|---------------------|---------------------|-----------------|
| **Reporting Lag** | 3-5 days (manual) | Next-day (automated) | Faster decisions during critical periods |
| **Data Sources** | 2 separate systems | 1 unified platform | Single source of truth for all stakeholders |
| **Analytics Access** | Data team only | Self-service for all | 75% reduction in ad-hoc report requests |
| **Pipeline Reliability** | Manual (error-prone) | 100% automated | Zero operational overhead |
| **Onboarding Time** | 3+ months | 3 weeks | Met COO's aggressive timeline |

---

## What This Project Demonstrates

### Business Acumen
* **Stakeholder Management**: Translated COO requirements into technical execution while keeping adoption simple
* **Problem Solving**: Identified that the core issue wasn't technology—it was fragmented decision-making
* **Strategic Thinking**: Built for today's needs while architecting for 5+ years of growth

### Data Communication
* **Storytelling with Data**: Designed dashboards that answer business questions, not just display numbers
* **Self-Service Enablement**: Empowered non-technical users to explore data independently
* **Executive Reporting**: Created visualizations that leadership actually uses in decision meetings

### Technical Execution
* **End-to-End Delivery**: Owned the pipeline from raw files in S3 to executive dashboards
* **Production-Grade Quality**: Built automated validation, dependency management, and fail-safe logic
* **Modern Stack Expertise**: Databricks, Delta Lake, Unity Catalog, PySpark, SQL, Genie

### Operational Excellence
* **Automation First**: Eliminated manual processes—100% hands-off daily operations
* **Scalable Design**: Medallion architecture handles 10x data growth without code changes
* **Documentation**: Clean, maintainable codebase with reusable utilities

---

## Technical Architecture Summary

### Data Flow
```
S3 (Raw CSVs) 
  ↓
Bronze Layer (Raw ingestion with audit trails)
  ↓
Silver Layer (Cleaned, validated, standardized)
  ↓
Gold Layer (Business metrics, denormalized for performance)
  ↓
Dashboards + Genie (Self-service analytics)
```

### Key Tables
* **Dimensions**: Customers, Products, Pricing, Calendar
* **Facts**: Orders (both full and incremental loads)
* **Star Schema**: Denormalized view joining all dimensions for dashboard performance

### Orchestration
* **Job**: FMCG Incremental Update run
* **Schedule**: Nightly at 11 PM (Africa/Lagos timezone)
* **Tasks**: 4 sequential notebooks (dimensions → facts)
* **Compute**: Serverless with auto-scaling

---

## Repository Structure

```
atlicon_consolidated_pipeline/
├── consolidated_pipeline/
│   ├── 1_setup/
│   │   ├── dim_date_table_creation.ipynb
│   │   ├── setup_catalog.ipynb
│   │   └── utilities.ipynb
│   ├── 2_dimension_data_processing/
│   │   ├── 1_customer_data_processing.ipynb
│   │   ├── 2_products_data_processing.ipynb
│   │   └── 3_pricing_data_processing.ipynb
│   └── 3_fact_data_processing/
│       ├── 1_full_load_fact.ipynb
│       └── 2_incremental_load_fact.ipynb
└── README.md
```

---

## Connect With Me

I'm passionate about turning data into business value—building systems that don't just work technically, but solve real organizational problems.

**LinkedIn:** [Emmanuel Okenwa](https://www.linkedin.com/in/emmanuel-okenwa/)

**Email:** greatemmanuel78@gmail.com

**GitHub Repository:** [Atlicon Consolidated Pipeline](https://github.com/your-username/atlicon_consolidated_pipeline)

---

## Key Takeaway

This project showcases more than technical skills—it demonstrates the ability to **understand business needs, translate them into scalable solutions, and deliver outcomes that stakeholders actually use**. 

In an era where AI can write code, the differentiator is understanding *what* to build, *why* it matters, and *how* to communicate the value. That's what drives real business impact.

---

*Built on Databricks | Powered by Unity Catalog, Delta Lake, PySpark, and Genie*
