
## Technical Questions + Model Answers

---

### 1. What are the differences between *Import Mode*, *DirectQuery*, and *Composite / Live Connection* in Power BI?

**Answer:**

* **Import Mode:** Data is loaded into Power BI’s internal model. Very fast visuals, full DAX / modelling capabilities. But data refresh needs scheduling; large datasets can cause size / memory issues.
* **DirectQuery Mode:** Data stays in the source. Every time you interact (filter, visual, etc), queries run against the source. Good for near real-time / very large data. But slower, depends on source performance, and some Power BI features / DAX functions may be limited.
* **Composite / Live Connection:** Composite models allow a mix of import and DirectQuery in same report. Live Connection means connecting to an external semantic model / SSAS / Power BI dataset so you aren’t importing data, but connecting to a curated dataset.

---

### 2. What is DAX? Explain *row context* vs *filter context*.

**Answer:**

* **DAX** (Data Analysis Expressions) is the formula / expression language used in Power BI, Power Pivot, SSAS Tabular. Used for measures, calculated columns, tables.
* **Row context** refers to the current row being evaluated (e.g. in a calculated column or in iterators like `SUMX`). It’s when the expression is evaluated for each row.
* **Filter context** is any filters applied (via slicers, visuals, or via DAX functions such as `CALCULATE`) that affect which rows are visible / considered in the calculation.

Example: If I use `SUMX` over a table, I have a row context for each row in the iteration; if I wrap it inside a `CALCULATE` that filters for “Region = North”, that is a filter context.

---

### 3. What is query folding in Power Query? Why it matters, and how do you preserve it?

**Answer:**

* **Query folding** means that Power Query steps (filtering, merging, grouping, selecting columns) get translated into native queries at the data source (e.g. SQL) instead of doing everything locally in Power BI.
* **Why it matters:** It reduces data transfer, speeds up performance, lowers local resource consumption. If folding is broken early, later steps may have to load a lot more data locally and slow down refresh/processing.
* **How to preserve it:**

  1. Use transformations that are supported by the source (filter rows, remove unused columns, rename, etc.)
  2. Avoid custom transformations or complex M code that can’t be converted to native queries early.
  3. Do foldable operations first (filter by date, limit columns) before non-foldable ones.
  4. Check “View Native Query” in Power Query to see if folding still in place.

---

### 4. What is a star schema vs snowflake schema? Which is better for Power BI & why?

**Answer:**

* **Star schema:** One large central fact table (e.g. sales, sensor readings) and several dimension tables (e.g. date, product, location) directly related to the fact table.
* **Snowflake schema:** Dimension tables are normalized into multiple related tables; e.g. product dimension broken into product → category, subcategory etc.

**Which is better in Power BI:** Usually star schema is preferred because:

* Simpler relationships, easier to understand & maintain.
* Better performance: fewer joins, simpler queries, better DAX performance.
* Easier visuals and filtering.

Snowflake can save storage or reduce redundancy, but often adds complexity and slows queries/filters.

---

### 5. How would you optimize a slow Power BI report? What are the steps you’d take?

**Answer:**
Here is a checklist:

* Reduce data volume: filter data at source, remove unused rows/columns.
* Use aggregations: pre-aggregate (daily, hourly) instead of minute-level if not needed.
* Use appropriate storage mode (Import vs DirectQuery vs Composite).
* Ensure query folding is preserved.
* Optimize relationships: minimize bi-directional relationships; ensure correct cardinality; avoid many-to-many unless necessary.
* Simplify visuals: fewer visuals per page, avoid high cardinality visuals, avoid lots of slicers.
* Optimize DAX: use variables, avoid nested/time-intensive functions, simplify filter context.
* Use incremental refresh for large datasets.
* Monitor performance: use Performance Analyzer in Power BI to see which visuals / queries slow things.

---

### 6. Write a DAX measure to compute Year-Over-Year (YoY) growth in Sales.

**Answer:**

```dax
TotalSales = SUM( Sales[SalesAmount] )

SalesLastYear =
CALCULATE(
    [TotalSales],
    SAMEPERIODLASTYEAR( 'Date'[Date] )
)

YoYGrowth% =
DIVIDE(
    [TotalSales] - [SalesLastYear],
    [SalesLastYear],
    0
)
```

Explanation: `SAMEPERIODLASTYEAR` shifts the filter context; `DIVIDE` is safer for handling zero denominator.

---

### 7. How would you design a data model combining minute-level sensor data + daily financial data so dashboards are responsive for different users (managers, leadership)?

**Answer:**
(As earlier) Steps include:

* Have separate fact tables: one for sensor minute-data, one for aggregated sensor (hour/day), and one for financial daily data.
* Create shared dimension tables: Date / Time, Sensor / Source, Region, possibly Product / Cost Center.
* Use star schema: link facts to dimensions.
* Use import mode for aggregated / financial data; maybe DirectQuery or composite for minute-level sensor data if too large.
* Filter early: only few sensors, limited time periods when needed.
* Pre-aggregate heavy sensor data for most visuals; allow drill-down into minute data when needed.
* Use Row-Level Security (RLS) so region managers see only their data, leadership see all.

---

### 8. Explain what window functions are in SQL (e.g. LAG, LEAD, RANK). Give an example where you used one.

**Answer:**

* Window functions allow you to perform calculations across sets of rows related to the current row without collapsing into group results. For example, using `LAG` to see previous row’s value, `LEAD` for next, `RANK` / `DENSE_RANK` to assign ranking within partitions, etc.

**Example:**

```sql
SELECT
  sensor_id,
  reading_time,
  reading_value,
  reading_value - LAG(reading_value) OVER (PARTITION BY sensor_id ORDER BY reading_time) AS diff_from_previous
FROM SensorReadings;
```

This shows the change in sensor reading compared to the previous minute, partitioned by sensor. Useful for anomaly detection or identifying spikes.

---

### 9. How would you fetch the **nth highest salary** from a table?

**Answer:**
Two common ways:

* Using **window functions**:

```sql
SELECT Salary
FROM (
  SELECT Salary,
         DENSE_RANK() OVER (ORDER BY Salary DESC) AS SalRank
  FROM Employee
) AS Ranked
WHERE SalRank = n;
```

* Using subquery + distinct + sorting:

```sql
SELECT DISTINCT Salary
FROM Employee
ORDER BY Salary DESC
OFFSET (n-1) ROWS
FETCH NEXT 1 ROW ONLY;
```

Adapt depending on requirement (whether duplicates count or not).

---

### 10. What is Row-Level Security (RLS) in Power BI? How do you implement it?

**Answer:**

* **RLS** lets you restrict data at the row level so that different users see different slices of the data (e.g., region manager sees only his region).

**Implementation:**

1. In Power BI Desktop, define roles with filter rules on table(s). For example, define a role “NorthManager” where `Region = "North"`.
2. Use DAX in role definitions to specify filter.
3. Publish to Power BI Service.
4. Assign users/groups to roles.
5. Optionally combine with Workspace permissions.

Make sure careful with relationships so filter flows as intended; also test with “View as Role” to ensure correct.

---

### 11. What is a Common Table Expression (CTE) in SQL? When would you use it?

**Answer:**

* A **CTE** is a temporary named result set that you can reference within a SELECT, INSERT, UPDATE, or DELETE. It’s defined at the start of a query with `WITH` keyword.

* Use cases: make complex queries easier to read, break down parts of query, recursive queries, or when you need to reuse a subquery in multiple places.

Example:

```sql
WITH SalesByRegion AS (
  SELECT Region, SUM(Amount) AS TotalSales
  FROM Sales
  GROUP BY Region
)
SELECT Region, TotalSales
FROM SalesByRegion
WHERE TotalSales > 100000;
```

---

### 12. How do you handle missing or inconsistent data when integrating multiple systems (e.g. sensor system, financial system)?

**Answer:**

* Identify missing / inconsistent fields; check data types, formats (timestamps, units).
* Standardize formats (e.g. time zones, date formats).
* Decide on strategy: drop rows, fill/impute, or mark as missing.
* For high volume data, maybe discard or aggregate missing ones depending on importance.
* Use data validation / data profiling to find anomalies.
* Document assumptions.

---

### 13. What is normalization? Explain first, second, third normal forms.

**Answer:**

* **Normalization**: process of organizing database structure to reduce redundancy and improve data integrity.

* **1NF (First Normal Form):** each table cell contains only atomic (single) values, no repeating groups/arrays.

* **2NF:** meets 1NF, and every non-key attribute is fully functionally dependent on the primary key (no partial dependency).

* **3NF:** meets 2NF, and non-key attributes are *not* transitively dependent on the primary key (i.e. non-key attribute depends only on key).

Applying these helps reduce anomalies, duplication, improve consistency of data.

---

### 14. How would you write a SQL query that joins 3 tables (Customers, Orders, Payments) to find customers who have orders but haven’t made payments?

**Answer:**

```sql
SELECT c.CustomerID, c.CustomerName, o.OrderID
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
LEFT JOIN Payments p ON o.OrderID = p.OrderID
WHERE p.OrderID IS NULL;
```

This gives customers + orders where no payment exists.

---

### 15. Explain time intelligence in DAX. Give examples of functions.

**Answer:**

* **Time intelligence** refers to DAX functions that understand dates and can compute things like Year-to-Date, Month-Over-Month, Same Period Last Year etc.

* Example functions: `TOTALYTD`, `DATESYTD`, `SAMEPERIODLASTYEAR`, `PARALLELPERIOD`, `DATEADD`.

* Example use: comparing current month’s sales to same month last year:

```dax
SalesSameMonthLastYear =
CALCULATE( 
    [TotalSales],
    SAMEPERIODLASTYEAR( 'Date'[Date] )
)
```

---

### 16. What are relationships in Power BI (one-to-one, one-to-many, many-to-many)? Why are cardinality and direction important?

**Answer:**

* Relationships define how tables connect via keys.

* **One-to-many (1\:M):** common in star schemas (one dimension row linked to many fact rows).

* **Many-to-many (M\:M):** when both tables have many rows with same value; can complicate filtering.

* **Cardinality** (how many rows relate) affects performance and behavior of filters.

* **Direction/Filter propagation:** which way filter flows; default is single direction, but you can set bi-directional. Bi-directional relationships should be used carefully (can lead to ambiguous filter propagation, performance issues).

---

### 17. How do you reduce the data model size in Power BI?

**Answer:**

* Remove unused columns and rows.
* Filter data early (date filters, only relevant data).
* Convert data types appropriately (e.g. integer rather than text).
* Use summarization / aggregation instead of raw detailed data where possible.
* Avoid storing duplicate data.
* Use measures instead of many calculated columns.
* Compress data (Power BI’s VertiPaq engine helps if data is clean and well structured).

---

### 18. Explain what is “bi-directional filtering” vs “single direction filtering” in Power BI relationships.

**Answer:**

* **Single direction**: filter flows from one table to another (often from dimension to fact).

* **Bi-directional**: filters can flow both ways. Useful when you want filters on both tables to affect each other.

* But bi-directional can cause ambiguity, circular filter paths, performance problems. Should be used only if needed.

---

### 19. What are some common performance pitfalls in DAX you should avoid?

**Answer:**

* Using too many nested functions or iterators (e.g. nested `SUMX` inside `FILTER`).
* Overusing context transitions.
* Using `CALCULATE` in places where simpler aggregations suffice.
* Using very large tables without proper filtering.
* Not leveraging variables (VAR) within measures to avoid recalculation.
* Visuals with too many data points (e.g. all minute-level sensors) being rendered at the same time.

---

### 20. What kind of SQL query might you write to diagnose slow performance?

**Answer:**
You might:

* Find the longest running queries via system views / profiling.
* Check execution plan to see missing indexes or expensive joins.
* Use window functions or subqueries to break down aggregates.
* Use temp tables / CTEs to simplify complex queries.
* Avoid `SELECT *` and fetch only needed columns.

Example: find top 5 regions by churn rate or similar.

---

## Additional Questions (from Schlumberger / Real Interview Guides)

I found a few from Schlumberger Business Analyst / Data Analyst interview guides that likely overlap:

* Describe your experience with SQL. Provide an example of a complex query you wrote. ([Interview Query][1])
* Explain normalization (1NF, 2NF, 3NF). ([Interview Query][1])
* What is a correlation matrix, and how do you use it? ([Interview Query][2])
* What are common metrics used to evaluate machine learning models? (accuracy, precision, recall, F1, AUC-ROC) ([Interview Query][2])
* What is overfitting in machine learning? ([Interview Query][2])

---
