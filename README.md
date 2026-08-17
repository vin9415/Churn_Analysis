# 📊 Customer Churn Analysis & Customer Intelligence
An end-to-end **Data Analytics project** focused on understanding customer churn, identifying high-risk customers, and measuring the potential revenue impact of customer attrition for an OTT subscription business.
The project integrates **SQL/SQLite and Python** to extract, clean, transform, analyze, visualize, and generate actionable business insights from customer, subscription, and support data.
## 🚀 Project Overview

Customer churn is one of the most important challenges for subscription-based businesses.

The objective of this project is to answer three key business questions:

* **Who** is churning or at high risk of churning?
* **Why** are customers churning?
* **When** is churn most likely to occur?

The analysis combines customer demographics, subscription information, churn scores, and customer-support interactions to identify churn patterns and potential revenue risks.

The project follows an end-to-end analytics workflow:

**SQLite Database → SQL Extraction → Python/Pandas → Data Cleaning → Feature Engineering → EDA → Visualization → Business Insights**

---

## 🎯 Business Problem

In a competitive OTT subscription market, acquiring new customers is expensive, making customer retention critical.

This project analyzes customer behavior to identify:

* Overall churn and retention rates
* Churn across different subscription plans
* Churn across states
* Monthly churn trends
* Customer tenure
* Revenue at risk from churned customers
* Customer support complaints and escalations
* Relationship between support escalations and churn
* Customers with low, medium, and high churn risk

The project is designed as a business-oriented analytics solution rather than just a technical exercise.

---

## 🛠️ Tech Stack

### Programming & Analytics

* **Python**
* **Pandas** – Data manipulation and analysis
* **NumPy** – Numerical operations and feature engineering

### Database

* **SQLite**
* **SQL**
* **sqlite3** – Python-SQLite integration

### Data Visualization

* **Matplotlib**
* **Seaborn**

### Development Environment

* **Jupyter Notebook**

---

## 🗄️ Dataset & Database Structure

The project uses a SQLite database named:

`customer_churn.db`

The database contains three relational tables:

### 1. `db_customer`

Contains customer demographic information:

* `customerid`
* `name`
* `country`
* `state`
* `gender`
* `dob`
* `interests`
* `pincode`

### 2. `db_subscription`

Contains subscription and churn-related information:

* `customerid`
* `subscription_start_date`
* `subscription_type`
* `renewal_date`
* `plan_type`
* `contract_type`
* `cancellation_date`
* `cancellation_reason`
* `monthly_charges`
* `cltv`
* `churn_score`

### 3. `db_support`

Contains customer-support information:

* `customerid`
* `complaint_date`
* `escalations`
* `csat_score`
* `comment`

The three tables are connected using `customerid`. The project report describes these three relational tables as the foundation for the customer, subscription, and support analysis.

---

## 🔄 Project Workflow

### 1. Database Connection

Connected the SQLite database with Python using `sqlite3`.

The notebook dynamically identifies the available tables and imports them into Pandas DataFrames using SQL queries.

```python
conn = sqlite3.connect('customer_churn.db')

sql_query = """
SELECT name
FROM sqlite_master
WHERE type='table'
"""

tables = pd.read_sql(sql_query, conn)
```

---

### 2. Data Extraction

Data was extracted from the relational SQLite tables and converted into Pandas DataFrames for further analysis.

The workflow follows:

**SQLite → SQL Query → Pandas DataFrame**

---

### 3. Data Cleaning

The customer, subscription, and support datasets were cleaned before analysis.

Key cleaning activities included:

* Renaming columns
* Removing unnecessary columns
* Converting date columns to datetime
* Standardizing categorical values
* Handling missing values
* Checking data types
* Performing basic data-quality checks

Examples:

* Renamed `name` → `customer_name`
* Removed `interests` and `pincode`
* Converted DOB and subscription dates to datetime
* Standardized gender values such as `Men` → `Male`
* Handled missing country values using state-country mapping

The project roadmap specifically includes datatype handling, column selection/renaming, quality checks, and missing-value treatment.

---

## ⚙️ Feature Engineering

New analytical features were created from existing data.

### Churn Flag

A binary `churn_flag` was created based on whether a customer had a cancellation date.

```python
df['churn_flag'] = np.where(
    df['cancellation_date'].notna(), 
    1, 
    0
)
```

Where:

* `1` → Customer churned
* `0` → Customer is active

### Customer Tenure

Customer tenure was calculated using:

* Cancellation date for churned customers
* Current date for active customers

### Complaint Count

The number of support complaints per customer was calculated using Pandas grouping.

### Churn Risk

Customers were segmented into three risk categories using their churn score:

| Churn Score | Risk Level |
| ----------- | ---------- |
| `< 50`      | Low        |
| `50–69`     | Medium     |
| `>= 70`     | High       |

---

## 📈 Key KPIs

The project calculates several customer and business KPIs:

| KPI                             | Description                                                |
| ------------------------------- | ---------------------------------------------------------- |
| Churn Rate                      | Percentage of customers who churned                        |
| Retention Rate                  | Percentage of customers retained                           |
| Churn by Plan                   | Churn rate across Basic, Standard and Premium plans        |
| Churn by State                  | Churn distribution across geographical regions             |
| ARPU                            | Average revenue per user                                   |
| Average Customer Tenure         | Average number of days customers remain subscribed         |
| Revenue at Risk                 | Monthly charges associated with churned customers          |
| Escalation Rate                 | Percentage of customers/interactions involving escalations |
| Average Complaints per User     | Average number of complaints per customer                  |
| Escalation vs Churn Correlation | Relationship between support escalation and churn          |
| Churn Risk                      | Low, Medium and High customer risk segmentation            |

These KPIs align with the metrics defined in the project report.

---

## 📊 Exploratory Data Analysis

The project performs EDA using Pandas, NumPy, Matplotlib and Seaborn.

Analysis includes:

* GroupBy analysis
* Aggregations
* Pivot tables
* Churn segmentation
* Plan-level analysis
* Geographic analysis
* Contract-level analysis
* Correlation analysis
* Customer risk segmentation

---

## 📉 Visualizations

Several visualizations were created to understand churn behavior.

### Monthly Churn Trend

Analyzes how the number of churned customers changes over time.

### Churn Rate by Plan Type

Compares churn rates between:

* Basic
* Standard
* Premium

### Churn by State

Identifies geographical regions with higher churn rates.

### Correlation Heatmap

Examines relationships between:

* Plan type
* Contract type
* Churn score
* Churn flag
* Churn risk
* Support escalations

### Pairplot

Used to examine pairwise relationships between selected numerical/encoded variables.

### Customer Segmentation

A categorical analysis was performed to compare monthly charges, gender, plan type and churn-risk segments.

---

## 🔍 Key Findings

The analysis produced several important findings.

### Overall Churn

* **Churn Rate:** 28.6%
* **Retention Rate:** 71.4%

### Contract Type

A significant difference was observed between monthly and annual subscribers:

* **Monthly Churn:** 55.6%
* **Annual Churn:** 8.3%

Monthly subscribers therefore show substantially higher churn risk than annual subscribers. The project report identifies this as one of the strongest findings of the analysis.

### Plan Type

Most churned customers belong to the **Basic plan**, although the project notes that this does not represent the largest revenue impact.

### Geography

The analysis identified **Karnataka** as the most affected state and **September 2024** as the month with the highest observed churn activity.

### Revenue Impact

The analysis identified approximately:

* **73.94** in monthly revenue at risk
* **2,047** in CLTV lost
* Approximately **18% revenue loss**

The project report further attributes the monthly-contract segment's higher churn to a significant portion of the identified revenue leakage.

---

## 💡 Business Recommendations

Based on the analysis, several actions can be considered:

### 1. Encourage Monthly → Annual Migration

Since monthly subscribers show substantially higher churn, the business could encourage customers to move toward annual contracts through:

* Annual-plan discounts
* Loyalty benefits
* Upgrade incentives
* Long-term subscription offers

### 2. Investigate Karnataka Churn

Investigate why Karnataka experienced higher churn.

Potential areas to examine:

* Pricing changes
* Customer complaints
* Technical issues
* Service quality
* Competitor activity

### 3. Investigate September 2024

September 2024 showed a notable increase in churn.

The business should investigate whether there were:

* Pricing changes
* Product changes
* Technical problems
* Content-related issues
* Customer-support problems

### 4. Prioritize High-Risk Customers

Customers classified as **High** or **Medium** churn risk should be prioritized based on their customer lifetime value.

Potential retention actions include:

* Email campaigns
* SMS communication
* Customer-support outreach
* Personalized retention offers
* Issue resolution

These recommendations are consistent with the action items documented in the project report.

---

## 📁 Project Structure

```text
Customer-Churn-Analysis/
│
├── churn_analysis.ipynb
├── customer_churn.db
├── exported_churn_data.csv
├── test_database.sqlite
├── Data Analytics Project - Churn Analysis Reportv.pdf
└── README.md
```

### File Description

| File                                                  | Description                                                                          |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------ |
| `churn_analysis.ipynb`                                | Complete Python analysis and visualization workflow                                  |
| `customer_churn.db`                                   | SQLite database containing customer, subscription and support tables                 |
| `exported_churn_data.csv`                             | Final processed dataset after merging and feature engineering                        |
| `test_database.sqlite`                                | SQLite database used for demonstrating SQL table creation, insertion and aggregation |
| `Data Analytics Project - Churn Analysis Reportv.pdf` | Project documentation, findings and business recommendations                         |

---

## 🧠 Skills Demonstrated

This project demonstrates practical experience in:

* SQL database interaction
* SQLite
* Python for Data Analytics
* Pandas
* NumPy
* Data Cleaning
* Data Transformation
* Feature Engineering
* Exploratory Data Analysis
* GroupBy & Aggregation
* Pivot Tables
* Data Visualization
* Correlation Analysis
* Customer Segmentation
* Churn Analysis
* Business KPI Analysis
* Revenue Impact Analysis
* Translating analytical findings into business recommendations

---

## 🔮 Future Improvements

The project can be extended by:

* Building an interactive **Power BI dashboard**
* Developing a machine-learning churn prediction model
* Creating automated customer-risk scoring
* Adding customer lifetime value segmentation
* Performing statistical significance testing
* Building an automated retention recommendation system
* Creating a scheduled reporting pipeline

---

## 📌 Project Outcome

This project demonstrates how raw relational customer data can be transformed into actionable business intelligence.

The complete workflow covers:

**Data Extraction → Data Cleaning → Feature Engineering → EDA → KPI Analysis → Visualization → Customer Segmentation → Business Recommendations**

The project identified a **28.6% overall churn rate** and a major churn disparity between monthly and annual subscribers, providing a strong basis for targeted customer-retention strategies.

---

## 👨‍💻 Author

**Vinit Kumar Pandey**

Data Analytics | Python | SQL | Pandas | NumPy | Data Visualization

---

⭐ If you found this project useful, feel free to explore the notebook and analysis.
