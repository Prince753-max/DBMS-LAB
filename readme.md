# DBMS Lab Experiments

This repository contains six database management practicals. Experiments 1 and 2 are handwritten, scanned lab records in PDF format. Experiments 3–6 include SQL source files and captured output. The SQL practicals are written for MySQL 8.

## Repository contents

| Path | Contents |
|---|---|
| [`dbms 1.pdf`](dbms%201.pdf) | Experiment 1: e-commerce ER design and diagram |
| [`dbms 2.pdf`](dbms%202.pdf) | Experiment 2: relational schema, MySQL DDL, sample data, and foreign-key validation |
| [`experiments/experiment3_code.txt`](experiments/experiment3_code.txt) | Experiment 3 SQL source |
| [`experiments/experiment3_output.txt`](experiments/experiment3_output.txt) | Experiment 3 captured output |
| [`experiments/experiment4_code.txt`](experiments/experiment4_code.txt) | Experiment 4 SQL source |
| [`experiments/experiment4_output.txt`](experiments/experiment4_output.txt) | Experiment 4 captured output |
| [`experiments/experiment5_code.txt`](experiments/experiment5_code.txt) | Experiment 5 SQL source |
| [`experiments/experiment5_output.txt`](experiments/experiment5_output.txt) | Experiment 5 captured output |
| [`experiments/experiment6_code.txt`](experiments/experiment6_code.txt) | Experiment 6 SQL source |
| [`experiments/experiment6_output.txt`](experiments/experiment6_output.txt) | Experiment 6 captured output |

## Experiment guide

### Experiment 1 — E-commerce ER diagram

**Aim:** Design an Entity–Relationship diagram for an Indian e-commerce platform, identifying entities, attributes, relationships, and cardinality.

**Entities in the scan:** Customer, Seller, Category, Product, Order, Order Item, Payment, and Address. The diagram records attributes such as customer ID/name/email/phone; product ID/name/price; order ID/date; and order-item quantity/price. It models relationships such as customers placing orders, orders containing order items, categories grouping products, sellers listing products, and customers having addresses. The handwritten cardinality notes include one-to-many and one-to-one relationships; consult the scanned diagram for the original drawing and exact notation.

**Related file:** [`dbms 1.pdf`](dbms%201.pdf)

### Experiment 2 — Relational schema and MySQL implementation

**Aim:** Convert an ER diagram into a relational schema and implement it using MySQL.

The scanned schema lists `Customer`, `Product`, `Category`, `Orders`, and `Order_Item`. It demonstrates primary keys, foreign keys, a composite key for order items, and referential integrity. The shown fields include customer contact details, product name/price/category, order date/customer, and order-item quantity/price. Sample inserts include a customer, an Electronics category, and a laptop product. An insert of an order referencing a nonexistent customer is shown as a foreign-key violation.

**Related file:** [`dbms 2.pdf`](dbms%202.pdf)

### Experiment 3 — Employee, department, and project queries

**Aim:** Create and query a normalized employee/department/project dataset using MySQL 8.

The script creates `exp3_department`, `exp3_project`, `exp3_employee`, and the many-to-many bridge table `exp3_employee_project`, with primary and foreign keys. It loads five departments, eight projects, 30 employees, and employee-project assignments. Queries demonstrate filtering and sorting, department aggregates (`COUNT`, `AVG`, `MIN`, `MAX`), `GROUP BY`/`HAVING`, salary classification with `CASE`, `LEFT JOIN`, and multi-table joins.

**Related files:** [`experiment3_code.txt`](experiments/experiment3_code.txt) and [`experiment3_output.txt`](experiments/experiment3_output.txt)

### Experiment 4 — Joins, subqueries, and query plans

**Aim:** Practice relational joins, correlated and existence subqueries, and inspect a query plan.

Queries demonstrate inner joins, left joins, a self-join to pair employees within a department, and employee/project joins. Subquery examples find employees earning above their department average, departments with employees earning at least 90,000, and employees assigned to both or only one of two projects. The final `EXPLAIN` inspects the plan for a department-average query.

**Related files:** [`experiment4_code.txt`](experiments/experiment4_code.txt) and [`experiment4_output.txt`](experiments/experiment4_output.txt)

### Experiment 5 — Views and recursive CTEs

**Aim:** Create summary and hierarchy views, demonstrate an updatable view, and produce reporting paths with a recursive common table expression.

The script creates `exp5_reporting` to represent employee-manager relationships, then defines department salary summary and employee hierarchy views. It updates a salary through a simple employee salary view. A `WITH RECURSIVE` query walks from managers to reports and builds each employee's reporting path.

**Related files:** [`experiment5_code.txt`](experiments/experiment5_code.txt) and [`experiment5_output.txt`](experiments/experiment5_output.txt)

### Experiment 6 — Stored procedures, triggers, and audit logging

**Aim:** Validate employee transfers, reject invalid salary updates, and audit salary changes.

The `transfer_employee` procedure checks that the employee and destination department exist before updating the employee's department. A `BEFORE UPDATE` trigger rejects negative salaries. An `AFTER UPDATE` trigger writes salary changes to `exp6_salary_audit`. Test procedures exercise invalid employee, invalid department, and negative salary cases.

**Related files:** [`experiment6_code.txt`](experiments/experiment6_code.txt) and [`experiment6_output.txt`](experiments/experiment6_output.txt)

## Running the SQL experiments

1. Install or connect to MySQL 8.
2. Create and select a database for the lab, for example:

   ```sql
   CREATE DATABASE dbms_lab;
   USE dbms_lab;
   ```

3. Run Experiment 3 first to create and populate the shared `exp3_*` tables. Then run Experiments 4, 5, and 6 in order; they build on that schema. Experiments 4–6 do not each provide a standalone setup script for every required object.
4. Experiment 2's SQL is included only in its handwritten PDF; transcribe and adapt it if you want to execute it.

The Experiment 3, 5, and 6 scripts use `INSERT IGNORE` and `CREATE TABLE IF NOT EXISTS` for repeatable setup. Experiment 6 drops and recreates its procedure and triggers. The Experiment 5 salary-view update changes the shared employee row, and Experiment 6's procedure and test updates also modify data. Use a fresh lab database if you want to reproduce the captured outputs from a clean starting state.

## Notes

- Experiments 1 and 2 are image-based handwritten scans, so text may be harder to search than the SQL files.
- The code and output files are plain text containing SQL and database-client output; rename them to `.sql` if your editor or MySQL workflow benefits from SQL syntax highlighting.
- Experiment 4 and later assume the `exp3_*` schema from Experiment 3 exists.
