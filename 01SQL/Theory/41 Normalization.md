# 17. Normalization

## Overview

Normalization is the process of organizing data in a database to reduce redundancy, improve data integrity, and eliminate undesirable characteristics such as insertion, update, and deletion anomalies.

The goal of normalization is to store data efficiently while maintaining consistency.

---

# Why Normalization?

Normalization helps to:

* Reduce data redundancy
* Improve data consistency
* Eliminate anomalies
* Simplify database maintenance
* Improve data integrity

---

# Problems Without Normalization

## Update Anomaly

The same information must be updated in multiple rows.

### Example

| EmpID | EmpName | Department |
| ----- | ------- | ---------- |
| 101   | John    | IT         |
| 102   | David   | IT         |

If IT changes to Information Technology, multiple rows must be updated.

---

## Insert Anomaly

Unable to insert data without additional information.

### Example

Cannot add a new department until at least one employee exists.

---

## Delete Anomaly

Deleting a record unintentionally removes important information.

### Example

Deleting the last employee in a department removes department information.

---

# First Normal Form (1NF)

## Rule

A table is in First Normal Form if:

* Each column contains atomic values.
* No repeating groups.
* Each row is unique.

---

## Before 1NF

| StudentID | Name | Subjects      |
| --------- | ---- | ------------- |
| 1         | Ram  | SQL, Python   |
| 2         | Amit | Python, Excel |

Subjects contains multiple values.

---

## After 1NF

| StudentID | Name | Subject |
| --------- | ---- | ------- |
| 1         | Ram  | SQL     |
| 1         | Ram  | Python  |
| 2         | Amit | Python  |
| 2         | Amit | Excel   |

---

## Benefits

* Removes repeating groups
* Ensures atomic values
* Improves query performance

---

# Second Normal Form (2NF)

## Rule

A table must:

* Be in 1NF
* Have no Partial Dependency

Non-key attributes must depend on the entire primary key.

---

## Example

### Before 2NF

| StudentID | CourseID | StudentName | CourseName |
| --------- | -------- | ----------- | ---------- |
| 1         | C101     | Ram         | SQL        |
| 1         | C102     | Ram         | Python     |

Primary Key:

```text
(StudentID, CourseID)
```

Problems:

* StudentName depends only on StudentID.
* CourseName depends only on CourseID.

This is Partial Dependency.

---

## After 2NF

### Student Table

| StudentID | StudentName |
| --------- | ----------- |
| 1         | Ram         |

### Course Table

| CourseID | CourseName |
| -------- | ---------- |
| C101     | SQL        |
| C102     | Python     |

### Enrollment Table

| StudentID | CourseID |
| --------- | -------- |
| 1         | C101     |
| 1         | C102     |

---

## Benefits

* Removes partial dependency
* Reduces redundancy
* Improves maintainability

---

# Third Normal Form (3NF)

## Rule

A table must:

* Be in 2NF
* Have no Transitive Dependency

Non-key attributes should depend only on the primary key.

---

## Example

### Before 3NF

| EmpID | EmpName | DeptID | DeptName |
| ----- | ------- | ------ | -------- |
| 101   | John    | D1     | IT       |

Dependency:

```text
EmpID → DeptID
DeptID → DeptName
```

DeptName depends indirectly on EmpID.

This is a Transitive Dependency.

---

## After 3NF

### Employee Table

| EmpID | EmpName | DeptID |
| ----- | ------- | ------ |
| 101   | John    | D1     |

### Department Table

| DeptID | DeptName |
| ------ | -------- |
| D1     | IT       |

---

## Benefits

* Eliminates transitive dependency
* Improves data consistency
* Reduces duplicate data

---

# Boyce-Codd Normal Form (BCNF)

## Rule

For every Functional Dependency:

```text
X → Y
```

X must be a Super Key.

BCNF is a stronger version of 3NF.

---

## Example

### Before BCNF

| Student | Course | Instructor |
| ------- | ------ | ---------- |
| Ram     | SQL    | John       |
| Amit    | SQL    | John       |
| Ram     | Python | David      |

Dependencies:

```text
(Student, Course) → Instructor
Instructor → Course
```

Instructor is not a candidate key.

BCNF violation occurs.

---

## After BCNF

### Instructor Table

| Instructor | Course |
| ---------- | ------ |
| John       | SQL    |
| David      | Python |

### Enrollment Table

| Student | Instructor |
| ------- | ---------- |
| Ram     | John       |
| Amit    | John       |
| Ram     | David      |

---

## Benefits

* Removes additional redundancy
* Handles complex functional dependencies
* Improves consistency

---

# Comparison of Normal Forms

| Normal Form | Removes                      |
| ----------- | ---------------------------- |
| 1NF         | Repeating Groups             |
| 2NF         | Partial Dependency           |
| 3NF         | Transitive Dependency        |
| BCNF        | Functional Dependency Issues |

---

# Denormalization

## Definition

Denormalization is the process of intentionally introducing redundancy into a database to improve query performance.

It combines normalized tables to reduce JOIN operations.

---

## Why Denormalization?

* Faster read operations
* Fewer JOINs
* Better reporting performance
* Improved analytical queries

---

## Example

### Normalized Structure

#### Employee

| EmpID | EmpName | DeptID |
| ----- | ------- | ------ |
| 101   | John    | D1     |

#### Department

| DeptID | DeptName |
| ------ | -------- |
| D1     | IT       |

Requires JOIN.

---

### Denormalized Structure

| EmpID | EmpName | DeptID | DeptName |
| ----- | ------- | ------ | -------- |
| 101   | John    | D1     | IT       |

No JOIN required.

---

## Advantages

* Faster query execution
* Better reporting performance
* Reduced JOIN complexity

---

## Disadvantages

* Increased redundancy
* More storage required
* Update anomalies possible
* Reduced data consistency

---

# Normalization vs Denormalization

| Feature           | Normalization | Denormalization |
| ----------------- | ------------- | --------------- |
| Redundancy        | Low           | High            |
| Storage           | Less          | More            |
| Data Integrity    | High          | Moderate        |
| Query Performance | Slower Reads  | Faster Reads    |
| Updates           | Easier        | More Complex    |
| JOIN Operations   | More          | Fewer           |

---

# Interview Questions

## What is Normalization?

Normalization is the process of organizing data to reduce redundancy and improve data integrity.

---

## What are the Types of Normalization?

* 1NF
* 2NF
* 3NF
* BCNF

---

## What is Partial Dependency?

When a non-key attribute depends on only part of a composite primary key.

---

## What is Transitive Dependency?

When a non-key attribute depends on another non-key attribute.

---

## Difference Between 3NF and BCNF?

* 3NF allows some dependency exceptions.
* BCNF requires every determinant to be a candidate key.

---

## What is Denormalization?

Denormalization is the process of adding redundancy to improve read/query performance.

---

# Summary

Normalization improves data integrity by eliminating redundancy and anomalies through 1NF, 2NF, 3NF, and BCNF. Denormalization is the opposite approach, used primarily to improve query performance in reporting and analytical systems.
