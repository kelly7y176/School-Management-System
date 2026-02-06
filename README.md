# 🎓 School Management System Database

This repository contains a complete MySQL implementation of a **School Management System**. It is designed to handle the core operational needs of an educational institution, including academic tracking, faculty management, and financial oversight.

## 📂 Project Files
*   **`school_db.sql`**: The primary script containing the schema, constraints, sample data, and business queries.
*   **`README.md`**: Project documentation and functional overview.

## 🛠️ Database Architecture
The system utilizes a relational structure with five core tables:
1.  **Students**: Basic profile and enrollment timestamps.
2.  **Teachers**: Faculty records categorized by academic departments.
3.  **Classes**: Course listings mapped to specific teachers and semesters.
4.  **Enrollments**: Junction table linking students to classes with grade tracking.
5.  **FeePayments**: Financial ledger for tracking student tuition status.

## 🚀 Installation & Usage
1. Open your SQL client (e.g., [MySQL Workbench](https://www.mysql.com) or [DBeaver](https://dbeaver.io)).
2. Create a new database: `CREATE DATABASE school_db;`.
3. Execute the `school_db.sql` script to build the tables and populate them with sample data.

## 📊 Application Queries
The project demonstrates 10 critical business processes solved through SQL:

| ID | Query Goal | Administrative Value |
|:---|:---|:---|
| **Q1** | Fee Verification | Instant check of a student's payment status. |
| **Q2** | Enrollment Workload | Analyzes average student course load per semester. |
| **Q3** | Grade Distribution | Statistics (Mean/Max/Min) per class for academic review. |
| **Q4** | Class Roster | Generates student lists for specific course IDs. |
| **Q5** | Delinquency Report | Identifies students with unpaid tuition for outreach. |
| **Q6** | Faculty Mapping | Tracks which teachers are instructing which students. |
| **Q7** | Departmental Reach | Measures student engagement across different departments. |
| **Q8** | Dean's List | Filters high-performing students (Grades > 90). |
| **Q9** | Revenue Summary | Calculates total school income from fee payments. |
| **Q10** | Performance Leader | Identifies the course with the highest academic success rate. |

## ⚙️ Constraints Applied
*   **Primary Keys**: Ensuring unique identifiers for every record.
*   **Foreign Keys**: Maintaining referential integrity between students, classes, and payments.
*   **Data Integrity**: Use of `DECIMAL` for precise financial and grade calculations.
