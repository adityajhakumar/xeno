
## Best Interview Questions for Schlumberger (Power BI / Data Analyst) + Sample Answers

These questions combine what their employees have reported, what roles like this usually need, and the job description you sent. After the question, I’ll give a model answer (you should modify to your experience).

---

### 1. **“Tell me about a past project where you used Power BI to solve a business problem. What was the problem, what approach did you take, and what was the result?”**

**Why they ask it:** They want to see your end-to-end ability: understanding business needs, gathering data, modeling it, visualising, and impact.

**Sample Answer:**

> In my last role, the sales department of our company noticed that while overall revenue was increasing, one geographic region was underperforming. I was asked to investigate.
>
> **Situation:** The Northern region’s quarterly growth was flat over 3 quarters, despite large marketing spend.
>
> **Task:** Use data from CRM, sales, and marketing tools to identify causes, and build a dashboard they could monitor in future.
>
> **Action:** I connected multiple data sources (SQL database for sales, Excel for marketing campaign data, web analytics data), then used Power Query to clean and transform data (standardising region names, filling missing values). I created a data model using a star schema (fact table: sales, dimension tables: region, time, campaign). Then I built a Power BI dashboard with visuals showing trend over time, comparisons between regions, top products, campaign ROI, and used DAX measures to compute region growth vs target, campaign performance, etc. I also set up row-level security so only management sees all regions; regional managers see only theirs.
>
> **Result:** We discovered that the marketing spend in the Northern region had low ROI because many campaigns were not localised and customers responded poorly. After adjusting campaigns (more local content, region-specific offers), growth in that region improved by \~12% in the next quarter. Also, the dashboard became a regular tool for weekly review, helping avoid future mismatches in strategy vs performance.

---

### 2. **“How do you optimize Power BI reports for performance when working with large datasets?”**

**Why they ask it:** Schlumberger works with big data (oil & gas, field sensors, operations). Slow reports = bad.

**Sample Answer:**

> Some of the techniques I follow:
>
> * Use **Import Mode** vs DirectQuery only when possible, because Import is faster; for real-time needs, DirectQuery is necessary but I minimise queries.
> * Filter at the source (SQL) so only needed rows/columns are brought in. Avoid loading unused columns.
> * Implement **incremental refresh** for large tables to update only changed data.
> * Use star schema data modelling: fact tables + dimension tables; avoid many-to-many relationships if possible.
> * Minimise use of bi-directional relationships unless needed.
> * Optimize DAX: prefer SUMX, ADDCOLUMNS carefully; reduce nested calculations; store intermediate results in variables.
> * Avoid complex visuals (e.g., too many visuals on one page, high cardinality visuals).
> * Use query folding in Power Query so transformation steps translate into native source queries.

---

### 3. **“Explain what a star schema is and why it’s useful. Could you compare it with snowflake schema in context of data modeling for BI?”**

**Sample Answer:**

> A **star schema** has a central fact table (e.g. Sales) and multiple dimension tables (e.g. Date, Product, Customer, Region). Each dimension directly links to the fact via foreign keys.
>
> A **snowflake schema** is more normalized: dimension tables are normalized into sub-dimensions; e.g. Customer → CustomerDemographics → Location etc.
>
> **Why star schema is often preferred in BI / Power BI**:
>
> * Simpler relationships; easier for end users to understand and navigate.
> * Better performance generally, because fewer joins and simpler model.
> * Easier to maintain and easier to write queries / DAX measures.
>
> Snowflake can save storage space (less redundancy), but often at cost of complexity and performance. In Schlumberger’s environment (lots of sensor / operational / field data), simpler model helps for speed and clarity.

---

### 4. **“What is DAX? Give examples of some DAX functions you often use. Also, explain the difference between a calculated column and a measure.”**

**Sample Answer:**

> DAX (Data Analysis Expressions) is the formula language used in Power BI / Power Pivot / SSAS Tabular. It allows you to define calculations (measures, calculated columns, tables) over your data model.
>
> Some DAX functions I use often:
>
> * `SUM`, `AVERAGE`, `COUNTROWS` for basic aggregation.
> * `CALCULATE` to change filter context (e.g., Sales in last year, or Sales for a specific product).
> * `FILTER` to define dynamic subsets.
> * `ALL`, `ALLEXCEPT`, `REMOVEFILTERS` to override filters (e.g. computing “% of total”).
> * Time intelligence functions (e.g. `DATESYTD`, `SAMEPERIODLASTYEAR`).
>
> **Calculated Column vs Measure:**
>
> * *Calculated Column* is computed row-by-row in a table; stored in the data model; its value does not change based on filters in visuals. Good for data classification, grouping, consistent label, etc.
> * *Measure* is a dynamic calculation: its value depends on context (filters, slicers, rows/columns in visuals). Measures are not stored for each row, but calculated on the fly when visuals are rendered.

---

### 5. **“How would you implement security in Power BI reports, especially if different users must see different subsets of data?”**

**Sample Answer:**

> There are multiple layers:
>
> 1. **Row-Level Security (RLS)** — define roles in Power BI Desktop, define DAX filter expressions so that, for example, a regional manager only sees their region. Then deploy to Power BI Service and assign users to roles.
> 2. **Workspace & Permissions** — control who has access to datasets, who can edit reports, who can only view.
> 3. **Data source security** — ensure that back-end databases also have proper access controls.
> 4. **Data masking / anonymization** if sensitive data involved.
> 5. **Audit logs** / governance practices: tracking who accessed what, making sure reports are up-to-date.

---

### 6. **“What is the difference between Power Query and Power BI modeling (Data Model / DAX)? Give use cases when you’d do transformations in Power Query vs when in DAX.”**

**Sample Answer:**

> **Power Query** is an ETL tool: used for data ingestion, cleaning, transformation, merging tables, shaping data before loading into the model. These steps happen before the data gets loaded into the model. Use it for tasks like: changing data types, renaming columns, merging data sources, pivot/unpivot, filtering rows, etc.
>
> **Modeling / DAX** is after the data is loaded. Used for calculations, aggregations, context-based filtering, dynamic measures. Use DAX when you need: dynamic aggregations depending on user filters, time intelligence, ranking, percent of total, etc.
>
> **Use case:** Suppose you have raw sales data with lots of non-sales columns. I’d use Power Query to remove unwanted columns, filter unwanted rows, maybe group some values. Then in DAX I’d compute sales metrics (e.g. sales growth, yoy growth), and define measures.

---

### 7. **“Scenario: You are given data from two systems: one for field operations (sensor readings) and one for financials. They have inconsistent timestamp formats, missing values, and different granularities. How would you combine them in a BI model to get useful insights?”**

**Sample Answer:**

> This is a realistic challenge, especially in oil & gas / field work. My steps:
>
> * First, explore the datasets: identify key columns (timestamps, IDs), see differences in formats and granularity (e.g. sensor data maybe by minute, financial by day or month).
> * Data cleaning: standardize timestamp formats (e.g. all to UTC or local consistent timezone), handle missing values (drop, impute, or mark as missing depending on business importance).
> * Aggregate / downsample high-granularity data (e.g. sensor data aggregated to hourly/daily so that it matches financial data granularity).
> * Create dimension tables (Date/Time) that can link both datasets.
> * Use Power Query for transformations (format conversions, joins, standardization).
> * In data model, create relationships via standard dimensions (e.g. time, location). Fact tables for sensor data and financials.
> * Build visuals that allow comparison (e.g. sensor performance vs cost over time, factory yield vs cost). Use DAX measures to compute derived metrics.

---

### 8. **“What statistical techniques or analytics do you use (beyond visualization) to drive insights? Give an example.”**

**Sample Answer:**

> Depending on situation, I use techniques like regression analysis (linear regression) to see trend and forecast, correlation to see which variables move together, time series analysis (seasonality, trends), clustering (to group similar items or customers), anomaly detection (identify outliers).
>
> **Example:** In a previous project, I used time series forecasting to predict monthly maintenance cost for machinery. I cleaned the historical cost data, detected seasonality (higher repairs during monsoon), then used regression + time series decomposition. The forecast helped the operations team budget better and pre-schedule maintenance, saving unexpected costs.

---

### 9. **Behavioral question: “Tell me about a time you had to explain complex technical results to non-technical stakeholders. How did you ensure they understood and acted on it?”**

**Sample Answer:**

> In my internship, I had data showing that some production equipment was giving lower yield owing to poor calibration, but the technical report was full of metrics that management couldn’t understand. I created a summary dashboard with visuals (trend lines, KPI cards), used analogies (“this is like your car’s performance dropping when tyres are underinflated”), avoided jargon, explained the impact (lost production, cost) rather than only technical numbers. I also prepared a one-page slide with key takeaways and recommendations. Because of that, management approved a calibration schedule, which increased output by 5%.

---

### 10. **“What are some current challenges in the oil & gas / resource extraction / field operations business that data analysis / BI can help solve? How would you use BI tools in that context?”**

**Why ask this:** Schlumberger works in oil/gas/energy, so showing domain awareness helps.

**Sample Answer:**

> Some challenges: equipment downtime, predictive maintenance, safety incidents, optimizing resource allocation, environmental monitoring, efficient drilling operations, cost management.
>
> Using BI, one could:
>
> * Use sensor data + historical maintenance data to build dashboards that predict when equipment is likely to fail → reduce downtime.
> * Combine weather / geological / sensor inputs to monitor safety risks in field operations.
> * Monitor drilling / production efficiency in real time to adjust operations quickly.
> * Visualise cost / budget vs actual over operations, to ensure cost controls.

---

## Extra Specific Questions Reported at Schlumberger

From people who interviewed there, these have come up:

* Questions about **DBMS**, **OOPS**, **Operating Systems** (esp. in tech rounds). ([Glassdoor][1])
* Deep Power BI questions: modelling, DAX, visuals, performance, data sources. ([Glassdoor][1])
* Sometimes coding / data-structures questions. ([Glassdoor][1])

---

## Tips to Tailor Answers for Schlumberger

* Highlight any experience with **operations / field data / sensors / hardware** if you have it — because Schlumberger works heavily in field operations.
* Be precise about data size (how many rows, how many tables), because performance matters.
* Talk about collaboration: with engineering / operations / finance teams (since they likely cross-functional).
* Emphasize safety / quality / reliability, since those are critical in oil and gas.

---
