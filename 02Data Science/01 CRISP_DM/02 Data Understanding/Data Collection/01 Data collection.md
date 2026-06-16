
# Data Collection

## What is Data Collection?

Data Collection is the process of gathering, documenting, validating, and managing data required to solve a business problem or perform analysis.

In Data Science, data collection is one of the most critical phases because the quality of the collected data directly impacts the quality of insights and machine learning models.

---

# Data Collection Roadmap

```text
Data Collection
│
├── 1. Data Sources
│
├── 2. Primary vs Secondary Data
│
├── 3. Data Requirements
│
├── 4. Data Description
│
├── 5. Data Verification
│
└── 6. Data Version Control
```

---

# 1. Data Sources

Data Source refers to the origin from which data is obtained.

Examples:

- Databases
- APIs
- Excel Files
- Surveys
- IoT Devices
- Social Media
- Public Datasets
- ERP Systems
- CRM Systems

### Example

Customer Data may come from:

- Website
- Mobile App
- Customer Support System
- Payment Gateway

---

# 2. Primary vs Secondary Data

## Primary Data

Data collected directly from the original source for a specific purpose.

### Examples

- Surveys
- Interviews
- Experiments
- Questionnaires
- Sensor Data

### Advantages

- More accurate
- Specific to business needs
- Better control over quality

---

## Secondary Data

Data already collected by someone else and reused.

### Examples

- Kaggle Datasets
- Government Data
- Research Papers
- Census Data
- Public APIs

### Advantages

- Faster acquisition
- Lower cost
- Large amount of available data

---

# 3. Data Requirements

Data Requirements define what data is needed to solve the business problem.

Questions to ask:

- What data is needed?
- Which columns are required?
- What is the target variable?
- What time period is required?
- How much historical data is needed?

### Example

Employee Attrition Project

Required Features:

- Age
- Salary
- Department
- Experience
- Attrition Status

---

# 4. Data Description

Data Description explains the structure and meaning of the collected data.

It includes:

- Column Names
- Data Types
- Units
- Business Meaning
- Source Information

### Example

| Column | Description |
|----------|-------------|
| Age | Employee Age |
| Salary | Annual Salary |
| Experience | Years of Experience |
| Attrition | Employee Left Company |

---

# 5. Data Verification

Data Verification ensures collected data is accurate, complete, and reliable.

Common Checks:

- Missing Values
- Duplicate Records
- Invalid Values
- Incorrect Data Types
- Outliers
- Consistency Checks

### Example

Age Column:

```text
Valid Range = 18 to 65
```

If Age = 150

```text
Invalid Record
```

---

# 6. Data Version Control

Data Version Control is the process of tracking changes made to datasets over time.

Just like Git tracks code changes, Data Version Control tracks data changes.

---

## Why It Is Important

- Reproducibility
- Auditability
- Data Lineage
- Collaboration
- Rollback Capability

---

## Example

```text
customer_data_v1.csv
customer_data_v2.csv
customer_data_v3.csv
```

or

```text
Raw Data
      ↓
Cleaned Data
      ↓
Feature Engineered Data
      ↓
Model Training Data
```

---

## Popular Tools

- Git LFS
- DVC (Data Version Control)
- LakeFS
- Delta Lake

---

# Learning Outcome

After completing this section, you should understand:

- Where data comes from
- Difference between Primary and Secondary Data
- How to identify required data
- How to document datasets
- How to verify data quality
- How to manage dataset versions

---

# Next Files

```text
03_Data_Collection
│
├── README.md
│
├── 01_Data_Sources.md
├── 02_Primary_vs_Secondary_Data.md
├── 03_Data_Requirements.md
├── 04_Data_Description.md
├── 05_Data_Verification.md
└── 06_Data_Version_Control.md
```

---

# Key Takeaways

- Data Collection is the foundation of Data Science.
- Data can originate from multiple sources.
- Primary data is collected directly; secondary data is collected by others.
- Data requirements must be defined before collection.
- Every dataset should have proper documentation.
- Data verification ensures quality and reliability.
- Data version control helps track and manage dataset changes.
