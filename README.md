# AWS-Athena

# 📊 From S3 to SQL: Serverless Data Analysis Using Amazon Athena

Query CSV data stored in Amazon S3 using SQL without creating or managing a database server.

---

## 📖 Overview

Amazon Athena is a serverless interactive query service that allows you to analyze data stored in Amazon S3 using standard SQL.

Instead of importing data into a database, Athena reads files directly from Amazon S3 and returns query results within seconds. This makes it a simple, scalable, and cost-effective solution for data analysis.

In this project, I implemented a complete Amazon Athena workflow by storing a CSV file in Amazon S3, creating an external table, and executing multiple SQL queries to analyze the data.

---

## 🎯 Objective

The objective of this project is to understand how Amazon Athena can query data stored in Amazon S3 without provisioning database servers and perform serverless data analysis using SQL.

---

# 🏗️ Architecture

> *(Add your architecture diagram here)*

![Architecture](images/architecture.png)

---

# 🛠️ AWS Services Used

- Amazon S3
- Amazon Athena
- AWS Glue Data Catalog
- IAM

---

# 📂 Project Structure

```
AWS-Athena/
│
├── employees.csv
├── README.md
├── images/
│   ├── architecture.png
│   ├── step1.png
│   ├── step2.png
│   ├── ...
│
└── documentation/
    └── Amazon_Athena_Implementation.pdf
```

---

# 📁 Dataset

This project uses a sample employee dataset.

**employees.csv**

Columns:

- id
- name
- department
- salary
- city

---

# 🚀 Implementation Steps

## Step 1 — Create an Amazon S3 Bucket

- Create a General Purpose S3 bucket.
- Choose the desired AWS Region.
- Keep the default security settings.
- Create the bucket.

---

## Step 2 — Create a Folder

Inside the bucket, create a folder named:

```
employees/
```

---

## Step 3 — Upload Dataset

Upload

```
employees.csv
```

inside the **employees/** folder.

---

## Step 4 — Configure Athena Query Results

Configure Athena to save query results in:

```
s3://athena-lab-2026/athena-results/
```

---

## Step 5 — Create Database

```sql
CREATE DATABASE company;
```

---

## Step 6 — Create External Table

```sql
CREATE EXTERNAL TABLE employees (
    id INT,
    name STRING,
    department STRING,
    salary INT,
    city STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION 's3://athena-lab-2026/employees/'
TBLPROPERTIES (
'skip.header.line.count'='1'
);
```

---

# 🔍 SQL Queries Performed

### View All Records

```sql
SELECT * FROM employees;
```

---

### Filter Employees by Department

```sql
SELECT *
FROM employees
WHERE department='IT';
```

---

### Highest Paid Employee

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 1;
```

---

### Average Salary

```sql
SELECT AVG(salary)
FROM employees;
```

---

### Count Total Employees

```sql
SELECT COUNT(*)
FROM employees;
```

---

### Count Employees by Department

```sql
SELECT department,
COUNT(*) AS total
FROM employees
GROUP BY department;
```

---

### Employees with Salary Above 60000

```sql
SELECT name,
salary
FROM employees
WHERE salary > 60000;
```

---

# 📊 Results

The implementation successfully demonstrated that Amazon Athena can directly query CSV files stored in Amazon S3.

The SQL queries returned accurate results without importing the data into any database.

Athena also automatically stored every query result and metadata file inside the configured S3 output location.

---

# 💡 Key Learnings

- Amazon Athena is completely serverless.
- No database server is required.
- Data remains inside Amazon S3.
- Athena reads files directly from S3.
- AWS Glue Data Catalog stores only table metadata.
- Query results are automatically saved back to Amazon S3.
- Standard SQL can be used to analyze CSV data.

---

# 📚 Documentation

Complete implementation guide:

📄 **Amazon_Athena_Implementation.pdf**

---

# 👨‍💻 Author

**Saiprasad Sambhaji Godge**

- RHCSA
- RHCE
- AWS Cloud Enthusiast
- Aspiring DevOps Engineer

---

⭐ If you found this project useful, feel free to star the repository.
