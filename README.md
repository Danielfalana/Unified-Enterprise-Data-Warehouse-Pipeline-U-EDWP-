# **Unified Enterprise Data Warehouse Pipeline (U‑EDWP)**  
*A Metadata‑Driven, Incremental, and Audit‑Enabled ETL Framework Built with Azure Data Factory*

---

## 📘 **Overview**
The **Unified Enterprise Data Warehouse Pipeline (U‑EDWP)** is a production‑grade, metadata‑driven ETL framework designed to integrate multiple OLTP systems into a centralized Enterprise Data Warehouse (EDW). Built using **Azure Data Factory**, **Data Flows**, **Azure SQL**, and **ADLS**, the solution delivers a **single source of truth** for analytics, reporting, and business intelligence.

This project demonstrates end‑to‑end data engineering capabilities including ingestion, orchestration, incremental loading, deduplication, SCD handling, fact/dimension loading, data quality validation, and ETL auditing.

---

## 📌 **Problem Statement**
Organizations often operate with multiple operational systems — HR, POS, store operations, finance, and more — each optimized for transactions but not analytics. This leads to:

- Fragmented data across systems  
- Inconsistent reporting logic  
- No unified view of customers, employees, stores, or transactions  
- Manual data preparation and duplicated effort  
- Lack of historical tracking  
- Poor data quality and low trust  

To solve this, the business requires a **centralized, governed, analytics‑ready repository** that integrates all OLTP sources into a unified EDW.

**U‑EDWP provides this by consolidating all operational data into a single source of truth.**

---

## 📌 **Key Features**
- Metadata‑driven ingestion  
- Watermark‑based incremental loading  
- Conformed and role‑playing dimensions  
- SCD Type 1 and Type 2 implementation  
- Deduplication and data quality enforcement  
- Fact and dimension loading  
- Centralized data quality rules engine  
- Error handling and retry logic  
- ETL metrics and auditing framework  
- Modular, scalable pipeline execution  

---

# 📐 **System Architecture (Text‑Based Diagram)**

            +---------------------------+
            |      OLTP Source Systems  |
            |  (HR, POS, Store Ops, etc.) 
            +-------------+-------------+
                          |
                          v
            +---------------------------+
            |     Azure Data Factory    |
            |   Metadata-Driven Ingest  |
            +-------------+-------------+
                          |
            +-------------v-------------+
            |         Staging Area      |
            |  Raw + Cleaned Structures |
            +-------------+-------------+
                          |
                          v
            +---------------------------+
            |     ADF Data Flows        |
            |  - Deduplication          |
            |  - Lookups                |
            |  - Hashing                |
            |  - SCD Type 1 & 2         |
            |  - Derived Columns        |
            +-------------+-------------+
                          |
                          v
            +---------------------------+
            |   Enterprise Data Warehouse|
            |  (Dimensions & Facts)      |
            +-------------+-------------+
                          |
                          v
            +---------------------------+
            |   ETL Metrics & Auditing  |
            |  Pre/Post Counts, Flags   |
            +-------------+-------------+
                          |
                          v
            +---------------------------+
            |     BI & Analytics Layer  |
            | (Power BI, Reporting Apps)|
            +---------------------------+


---

# ⚙️ **How It Works**

## **1. Data Modeling**
A dimensional model supports multiple business processes:

- Misconduct  
- Absenteeism  
- Overtime  
- Sales  
- Promotions  
- Purchasing  

With conformed dimensions:

- **DimDate**, **DimTime**, **Employee**, **Store**, **Product**, **Customer**

  <p align="center">
  <img src="Data Physical Model structure/Data Model.png" width="50%">   
</p>

---

## **2. Pipeline Orchestration**
A master orchestration pipeline controls the entire ETL lifecycle:

- Parameterized datasets  
- Metadata lookup for table‑driven ingestion  
- ForEach loops to iterate through tables  
- Switch activities to route data to the correct flow  
- Modular pipelines for staging, dimensions, and facts  

---

## **3. Incremental Load Framework (Implemented)**
A fully functional **watermark‑based incremental ingestion** mechanism ensures that only new or changed records are processed for large tables.

### **Capabilities**
- Watermark table stores last successful load timestamp  
- Dynamic filtering using ModifiedDate/UpdatedAt  
- Supports append‑only and upsert patterns  
- Automatically updates watermark after successful loads  
- Integrated into parameterized ADF pipelines  

---

## **4. Data Quality Rules Engine (Implemented)**
A centralized rules engine validates data before it enters the EDW.

### **Validation Rules**
- Null checks  
- Referential integrity checks  
- Threshold checks  
- Duplicate detection  
- Business rule validations  

### **How It Works**
- Rules stored in metadata tables  
- ADF pipelines read rules dynamically  
- Data Flows apply rules at runtime  
- Failed rows routed to quarantine tables  
- Metrics logged for each rule execution  

---

## **5. Deduplication Framework**
A dedicated data flow removes duplicates using:

- Window functions  
- Business key grouping  
- Row ranking  
- Filtering to retain the latest valid record  

---

## **6. SCD Type 1 & Type 2**
### **Type 1 (Overwrite)**
Used for attributes where history is not required (e.g., Promotion details).

### **Type 2 (Historical Tracking)**
Used for attributes where change history matters (e.g., Employee role, store assignment).

ADF Data Flows implement:

- Hash comparison  
- Change detection  
- Effective dates  
- Current flag logic  
- Insert/update routing  

---

## **7. Pipeline Execution Framework**
Execution follows a structured sequence:

1. Load OLTP → Staging  
2. Apply incremental logic  
3. Load Staging → EDW Dimensions  
4. Apply SCD logic  
5. Load Staging → EDW Facts  
6. Run data quality checks  
7. Record ETL metrics  

---

## **8. Error Handling & Retry Logic (Implemented)**
Robust operational safeguards ensure reliability.

### **Features**
- Try/Catch patterns  
- Automatic retry policies  
- Failure routing to error pipelines  
- Logging of error messages, activity names, run IDs, timestamps  

---

## **9. ETL Metrics & Auditing**
A dedicated metrics table captures:

- Pre‑count  
- Post‑count  
- Insert/update counts  
- Pass/fail flags  
- Load timestamps  
- Pipeline/environment identifiers  

---

# 🛠️ **Technologies Used**

### **Azure Services**
- Azure Data Factory  
- ADF Data Flows  
- Azure SQL Database / Synapse SQL  
- Azure Storage / ADLS Gen2  

### **Data Engineering Concepts**
- Dimensional modeling  
- Conformed dimensions  
- SCD Type 1 & Type 2  
- Metadata‑driven ETL  
- Incremental loading  
- Deduplication  
- Hashing for change detection  
- Fact/dimension loading  
- Data quality rules engine  
- ETL auditing  

### **Languages & Tools**
- SQL
- Scala (Spark-based transformations & utilities)
- ADF Expressions  
- JSON  
- GitHub  

---

# 🏁 **Conclusion**
The **Unified Enterprise Data Warehouse Pipeline (U‑EDWP)** demonstrates a complete, production‑ready data engineering solution built on Azure. It integrates multiple OLTP systems, enforces data quality, applies advanced transformation logic, and delivers a trusted single source of truth for analytics.

This project highlights your ability to design and implement enterprise‑level ETL frameworks — from modeling to orchestration to auditing — making it a powerful addition to your portfolio and a strong demonstration of real‑world data engineering expertise.
            
