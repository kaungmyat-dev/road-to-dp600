# Get Started with Lakehouse in Microsoft Fabric

## 1. What is it?
Lakehouse in Microsoft Fabric is a **unified platform** that combines:
- The **flexible and scalable storage** of a data lake  
- The **ability to query and analyze data** like a data warehouse  

It uses **Apache Spark** and **SQL compute engines** to process and analyze data, and is built on the **OneLake storage layer**.

---

## 2. What matters?
A lakehouse gives organizations a **single place** to keep both **raw** and **structured data**, enabling:
- **Cost-effective, scalable storage** (like a data lake)  
- **Reliable, high-performance analytics** (like a data warehouse)  

It supports:
- **ACID transactional tables** (Delta Lake)  
- **Schema enforcement**  
- **Time travel** (query previous versions or roll back changes)  
- **Integration with analytics tools**: Power BI, SQL analytics endpoint, Spark notebooks  
- **Layered security controls** (workspace, item-level, row/column-level, schema-level)

This makes the lakehouse a practical foundation for both **BI** and **AI** workloads.

---

## 3. Key Points

### 3.1 Introduction to Lakehouse
- **Unified platform**: combines data lake + data warehouse capabilities.
- **Compute engines**: Apache Spark and SQL.
- **Storage layer**: OneLake.

---

### 3.2 Lakehouse Features and Capabilities

#### Traditional Analytics Problems
- **Data lake**:
  - Flexible and scalable  
  - But lacks structure and performance for analytics  
- **Data warehouse**:
  - Strong analytical capabilities  
  - But struggles with diverse data formats and is costly to scale  
- **Lakehouse**: combines abilities of both.

#### Lakehouse Data Areas
Lakehouse organizes data into **two main areas**:

1. **Tables**
   - Provide **structured, queryable data**
   - Support **SQL queries** through the **SQL analytics endpoint**
   - Enforce **schemas** and support **ACID transactions**
   - Can be accessed in **Power BI** for reporting
   - Benefit from **automatic optimization and maintenance**

2. **Files**
   - Store **raw or semi-structured data** in their **native formats**
   - Support **any file format**: CSV, JSON, Parquet, images, documents
   - Provide **flexibility** for data exploration and processing
   - Can be **staged** before transformation into tables
   - **Do not** enforce schema or support direct SQL queries

This design lets you maintain:
- **Raw data** (for compliance or reprocessing)  
- **Structured tables** (for analytics)  
within the **same lakehouse**.

You can:
- Process files using **Spark notebooks** or **Dataflows Gen2**.
- Build on **Delta Lake tables**, the heart of the lakehouse.

---

### 3.3 Delta Lake Tables

Delta Lake is an **open-source storage layer** that brings **reliability** to data lakes.

**Key advantages**:
1. **ACID transactions**  
   - Ensure data consistency even when multiple users read and write simultaneously.
2. **Schema enforcement**  
   - Validates that written data matches the table schema, preventing corrupt data.
3. **Time travel**  
   - Maintains a **transaction log** that lets you:
     - Query previous versions of your data  
     - Roll back changes
4. **Efficient updates and deletes**  
   - Support efficient update and delete operations.

---

### 3.4 Security and Access Control in Lakehouse

Fabric provides **layered access controls** to secure lakehouse data at multiple levels:

- **Workspace roles**: for people who need access to **all items** in a workspace.
- **Item-level sharing**: grant **read-only access** for specific needs (e.g., analytics, Power BI report development).
- **SQL analytics endpoint**:
  - Supports **row-level security** and **column-level security** for granular control.
- **Schema-level permissions**:
  - If you organize tables into **schemas**, you can control access by **business domain**.

**Well-organized lakehouse data** becomes the foundation of **intelligent analytics**:
- Create tables with:
  - Clear **schemas**
  - Consistent **naming conventions**
  - Descriptive **column names**
- This makes data accessible to:
  - **Human analysts**
  - **AI-powered tools**

- **Fabric IQ data agents** can:
  - Query lakehouse tables through the **SQL analytics endpoint**
  - Translate **natural language** to **SQL queries**

---

### 3.5 Ingest and Transform Data in a Lakehouse

#### Schemas in Lakehouse
- When you create a lakehouse, **schemas are enabled by default**.
  - Default schema name: **dbo**
- **Schemas** let you organize tables into **logical groups** (e.g., `it`, `marketing`, etc.).
- You can create **other schemas** as needed.
- Schema-enabled lakehouses support:
  - **Schema-level permissions**
  - **Cross-workspace queries** using namespace:  
    `workspace.lakehouse.schema.table`

#### Lakehouse Modes
You can work with a lakehouse in **two modes**:

1. **Lakehouse Explorer**
   - Allows you to:
     - Manage data
     - Upload files
     - Create tables
     - Make changes to the lakehouse

2. **SQL Analytics Endpoint**
   - Query Delta tables using **T-SQL** in **read-only mode**
   - You can:
     - Create **views**
     - Create **functions**
     - Apply **SQL security**
   - You **cannot** modify underlying data through this endpoint.

#### Ingesting Data (First Step of ETL)
Ingesting data into a lakehouse is the first step of the **ETL** (Extract, Transform, Load) process.

**Methods to bring data into a lakehouse**:

1. **Upload**
   - Upload **local files or folders** through the **lakehouse explorer**.

2. **Load to Table**
   - Select a file or folder in lakehouse explorer.
   - Choose **Load to Table** to create a **Delta table** without coding.
   - Supports **Parquet** and **CSV** files.
   - Lets you **append** or **overwrite** data into **new or existing tables**.

3. **Dataflows Gen2**
   - Import and transform data using **Power Query**.

4. **Notebook**
   - Use **Apache Spark** to ingest, transform, and load data **programmatically**.

5. **Data Factory Pipelines**
   - Use **Copy Data activity** to move data from external sources.

#### Shortcuts and Permissions
- When you access data through a **shortcut** to another **OneLake location**:
  - OneLake uses your **identity** to authorize access to the target data.
  - You must have **permission** to the target location to **read data**.

- **Schema shortcuts**:
  - Map the **entire schema** of a target table.
  - All referenced tables appear as **local tables** within the schema.

#### Transforming Data
You can transform data using:

1. **Notebooks**
   - Support **PySpark**, **SQL**, **Scala** languages.
   - Good for:
     - Complex transformations
     - Programmatic logic
     - Cross-workspace queries

2. **Dataflows Gen2**
   - Suited for users familiar with **Power BI** or **Excel**.
   - Use **Power Query** for transformations.

3. **Pipelines**
   - Provide a **visual interface** to orchestrate ETL processes.
   - Can include **multiple activities**.
   - Can run activities in **sequence** or **parallel**.

---

### 3.6 Query and Analyze Lakehouse Data

#### Query Using SQL Analytics Endpoint
- Use the **SQL analytics endpoint** to query data.
- Common use cases:
  - **Ad-hoc queries** for quick investigation
  - **BI connection** for:
    - Power BI
    - Excel
    - Azure Data Studio (for reporting)
  - **Data validation** to verify transformation results

- You can create **SQL views** to store **reusable logic**.
- SQL analytics endpoint supports:
  - **Row-level security**
  - **Column-level security**

#### Query Using Spark Notebooks
- **Notebooks** provide a **flexible, code-based environment** for querying and analyzing lakehouse data.

- You can:
  - Use **Spark SQL** with SQL syntax within a notebook cell to query lakehouse tables:  
    ```sql
    SELECT * FROM schema.table
    ```
  - Use **PySpark** with Python code to manipulate data.

- **Typical uses for Spark notebooks**:
  - **Exploratory data analysis**:
    - Investigate patterns, outliers, and relationships in data.
  - **Complex transformations**:
    - Apply business logic that is easier to express in code than in SQL.
  - **Cross-workspace queries**:
    - Use **four-part namespace**:  
      `workspace.lakehouse.schema.table`

#### Analyze and Visualize with Power BI
Power BI can connect to a lakehouse in **two main ways**:

1. **SQL Server connection** with **SQL analytics endpoint**:
   - Connect Power BI to the SQL endpoint for querying and reporting.

2. **Create a semantic model**:
   - Create a **semantic model** that references specific lakehouse tables.
   - This model defines:
     - **Relationships**
     - **Measures**
     - **Business logic**

- When you connect to a **lakehouse semantic model**, it uses **Direct Lake mode** by default.
  - **Direct Lake**:
    - Reads data directly from the lakehouse **without importing or copying**.
    - Provides **fast query performance**.

---

## Summary (Optional)
- Lakehouse = **data lake + data warehouse** in one platform.
- Core storage: **OneLake**; core tables: **Delta Lake**.
- Two data areas: **tables** (structured) and **files** (raw).
- Key features: **ACID**, **schema enforcement**, **time travel**, **efficient updates/deletes**.
- Security: **workspace roles**, **item-level**, **row/column-level**, **schema-level**.
- Ingest: **Upload**, **Load to Table**, **Dataflows Gen2**, **Notebooks**, **Data Factory Pipelines**.
- Transform: **Notebooks**, **Dataflows Gen2**, **Pipelines**.
- Query/Analyze: **SQL analytics endpoint**, **Spark notebooks**, **Power BI (Direct Lake)**.
