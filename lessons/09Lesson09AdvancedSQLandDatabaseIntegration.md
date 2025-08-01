# Lesson 09 — Advanced SQL and Database Integration

## Overview

No overview provided

## Learning Objectives

- Students will deepen their understanding of SQL by learning advanced techniques such as subqueries, complex `JOIN`s, aggregation with functions, and using `HAVING` for conditional filtering. This lesson also introduces performance optimization techniques, transactions, parameterized queries, window functions, and more.

## Topics Covered

- 1. Subqueries: Embedding queries within other SQL statements for dynamic filtering or calculations.
- 2. Complex JOINs: Using INNER and LEFT JOINs across multiple related tables.
- 3. Aggregation Functions: Using `MIN()`, `MAX()`, `AVG()`, `COUNT()` with `GROUP BY`.
- 4. Aggregation with HAVING: Filtering grouped results using `HAVING` after aggregation.
- 5. Performance Optimization: Creating indexes to speed up frequent queries.
- 6. Transactions and Rollbacks: Ensuring consistency with `BEGIN`, `COMMIT`, and `ROLLBACK`.
- 7. Parameterized Queries: Preventing SQL injection using safe input handling with placeholders.
- 8. Window Functions: Applying `RANK()`, `ROW_NUMBER()`, and `OVER()` for row-level analytics.
- 9. Date and Time Functions: Calculating durations and extracting date components using `JULIANDAY()` and related functions.
- 10. Python Integration: Writing and executing SQL queries within Python scripts using `sqlite3`.

## Status

pending

## Assignment

Assignment for Lesson 9

### Objective

No objective specified

### Expected Capabilities

Expected capabilities will be defined as the lesson progresses.

### Instructions

Instructions will be provided when the lesson is generated.

### Tasks

#### Task 1: Task 1


# **Advanced SQL and Database Integration**

---

## **Lesson Overview**

**Learning Objective**:  
Students will deepen their understanding of SQL by learning advanced techniques such as subqueries, complex `JOIN`s, aggregation with functions, and using the `HAVING` clause for conditional filtering.

---

## **Assignment Instructions**

You create the code for this assignment in your python_homework/assignment9 folder.  You may want to have two VSCode terminal sessions.  In one, you have changed directories to `assignment9`.  This is the session where you will run your code.  In the other terminal session, you will run `sqlcommand.py` from the `python_homework` folder.  You need to have the working directory set differently, so that each program will be able to find `db/lesson.db`.  Be sure to create an `assignment9` git branch before you start.  As usual, mark the code that completes each task with a comment line.

### **Preparation and Practice**

You have already experimented with the `sqlcommand.py` program.  Run it again, and practice what you've learned.  You can do SELECT, INSERT, UPDATE and DELETE.  The SELECT statements can have JOIN, GROUP BY, ORDER BY, subqueries, HAVING, etc.  Practice these until you feel familiar with them.

For each of the following tasks, you first use the sqlcommand command line to get the right SQL statement.  Then you add it to your program.

**Help Available!**  

This lesson combines a lot of concepts that have been presented only briefly. You may find these tasks a little challenging.  If you get stuck, 1:1 mentors are available to answer your questions.  Appointments are available in the [1:1 Mentor Table](https://airtable.com/appoSRJMlXH9KvE6w/shrQinGb1phZYwdiL)

---

### **Task 1: Complex JOINs with Aggregation**

1. **Problem Statement**:  
   Find the total price of each of the first 5 orders.  There are several steps.  You need to join the orders table with the line_items table and the products table.  You need to GROUP_BY the order_id.  You need to select the order_id and the SUM of the product price times the line_item quantity.  Then, you ORDER BY order_id and LIMIT 5.  You don't need a subquery. Print out the order_id and the total price for each of the rows returned.

2. **Deliverable**: 
   - Within the python_homework folder, create an `assignment9` branch.  Change to the `assignment9` folder.
   - Get the SQL statement working in sqlcommand.
   - Within the `assignment9` folder, create `advanced_sql.py`. This should open the database, issue the SQL statement, print out the result, and close the database.
   - test your program.

---

### **Task 2: Understanding Subqueries**

1. **Problem Statement**:  
   For each customer, find the average price of their orders.  This can be done with a subquery. You compute the price of each order as in part 1, but you return the customer_id and the total_price.  That's the subquery. You need to return the total price using `AS total_price`, and you need to return the customer_id with `AS customer_id_b`, for reasons that will be clear in a moment.  In your main statement, you left join the customer table with the results of the subquery, using `ON customer_id = customer_id_b`.  You aliased the customer_id column in the subquery so that the column names wouldn't collide.  Then group by customer_id -- this `GROUP BY` comes *after* the subquery -- and get the average of the total price of the customer orders.  Return the customer name and the average_total_price.

2. **Deliverable**:  
   - Again, get the SQL statement working in sqlcommand.
   - Add code to `advanced_sql.py` to print out the result.

---

### **Task 3: An Insert Transaction Based on Data**

1. **Problem Statement**:  
   You want to create a new order for the customer named Perez and Sons.  The employee creating the order is Miranda Harris.  The customer wants 10 of each of the 5 least expensive products.  You first need to do a SELECT statement to retrieve the customer_id, another to retrieve the product_ids of the 5 least expensive products, and another to retrieve the employee_id.  Then, you create the order record and the 5 line_item records comprising the order.  You have to use the customer_id, employee_id, and product_id values you obtained from the SELECT statements. You have to use the order_id for the order record you created in the line_items records. The inserts must occur within the scope of one transaction. Then, using a SELECT with a JOIN, print out the list of line_item_ids for the order along with the quantity and product name for each.

   You want to make sure that the foreign keys in the INSERT statements are valid.  So, add this line to your script, right after the database connection:
   ```
   conn.execute("PRAGMA foreign_keys = 1")
   ```

   In general, when creating a record, you don't want to specify the primary key.  So leave that column name off your insert statements.  SQLite will assign a unique primary key for you.  But, you need the order_id for the order record you insert to be able to insert line_item records for that order.  You can have this value returned by adding the following clause to the INSERT statement for the order:
   ```
   RETURNING order_id
   ```

2. **Deliverable**:   
   - Get this working in sqlcommand.  (Note that sqlcommand does not provide a way to begin and end transactions, so for sqlcommand, the creation of the order and line_item records are separate transactions.)
   - Use sqlcommand to delete the line_items records for the order you created.  (This is one delete statement.)  Delete also the order record you created.
   - Add statements for the complete transaction and the subsequent SELECT statement into `advanced_py.sql`, and to print out the result of the SELECT.
   - Test your program.

---

### **Task 4: Aggregation with HAVING**

1. **Problem Statement**:  
   Find all employees associated with more than 5 orders.  You want the first_name, the last_name, and the count of orders.  You need to do a `JOIN` on the employees and orders tables, and then use GROUP BY, COUNT, and HAVING.

2. **Deliverable**:  
   - Get it working in sqlcommand.
   - Add code `advanced_sql.py` to print out the employee_id, first_name, last_name, and an order count for each of the employees with more than 5 orders.
   - Test your program.

### Submit Your Assignment on GitHub**  

📌 **Follow these steps to submit your work:**  

#### **1️⃣ Add, Commit, and Push Your Changes**  
- Within your python_homework folder, do a git add and a git commit for the files you have created, so that they are added to the `assignment9` branch.
- Push that branch to GitHub. 

#### **2️⃣ Create a Pull Request**  
- Log on to your GitHub account.
- Open your `python_homework` repository.
- Select your `assignment9` branch.  It should be one or several commits ahead of your main branch.
- Create a pull request.

#### **3️⃣ Submit Your GitHub Link**  
- Your browser now has the link to your pull request.  Copy that link. 
- Paste the URL into the **assignment submission form**. 

---

### **Resources**
- [SQLite Documentation](https://www.sqlite.org/docs.html)
- [Python `sqlite3` Library Documentation](https://docs.python.org/3/library/sqlite3.html)
```


```

```

### Submission Instructions

Please submit on time

### Checklist

Checklist will be provided when the lesson is generated.

### Check for Understanding

Understanding checks will be provided when the lesson is generated.

## Subsections

### Lesson 9

# **Lesson 09 — Advanced SQL and Database Integration**

## **Lesson Overview**
**Learning objective:** Students will deepen their understanding of SQL by learning advanced techniques such as subqueries, complex `JOIN`s, aggregation with functions, and using `HAVING` for conditional filtering. This lesson also introduces performance optimization techniques, transactions, parameterized queries, window functions, and more.

**Topics:**
1. Subqueries: Embedding queries within other SQL statements for dynamic filtering or calculations.
2. Complex JOINs: Using INNER and LEFT JOINs across multiple related tables.
3. Aggregation Functions: Using `MIN()`, `MAX()`, `AVG()`, `COUNT()` with `GROUP BY`.
4. Aggregation with HAVING: Filtering grouped results using `HAVING` after aggregation.
5. Performance Optimization: Creating indexes to speed up frequent queries.
6. Transactions and Rollbacks: Ensuring consistency with `BEGIN`, `COMMIT`, and `ROLLBACK`.
7. Parameterized Queries: Preventing SQL injection using safe input handling with placeholders.
8. Window Functions: Applying `RANK()`, `ROW_NUMBER()`, and `OVER()` for row-level analytics.
9. Date and Time Functions: Calculating durations and extracting date components using `JULIANDAY()` and related functions.
10. Python Integration: Writing and executing SQL queries within Python scripts using `sqlite3`.

---

## **8.1 Understanding Subqueries**

### **Overview**
Subqueries are nested SQL queries used to perform intermediate calculations or selections before the main query executes.

### **Key Concepts:**
- Use subqueries to fetch results dynamically within another query.
- Common use cases include finding maximum, minimum, or aggregated values.

### **Example:**
Find the highest-paid employee in each department using a subquery.
```sql
SELECT department_id, employee_id, salary
FROM Employees AS e
WHERE salary = (
    SELECT MAX(salary)
    FROM Employees
    WHERE department_id = e.department_id
);
```

### **Implementation in Python:**
```python
# Example using SQLite
conn = sqlite3.connect("company.db")
cursor = conn.cursor()

# Execute the query
query = """
SELECT department_id, employee_id, salary
FROM Employees AS e
WHERE salary = (
    SELECT MAX(salary)
    FROM Employees
    WHERE department_id = e.department_id
);
"""
cursor.execute(query)
print(cursor.fetchall())

conn.close()
```

---

## **8.2 Complex JOINs**

### **Overview**
Complex `JOIN`s allow you to retrieve data from multiple related tables.

### **Steps:**
1. Create a `Projects` table and insert sample data.
2. Use a `JOIN` to combine employee and project information through the department field.

### **Key Concepts:**
- `INNER JOIN`: Retrieves records with matching values in both tables.
- `LEFT JOIN`: Retrieves all records from the left table and matching records from the right.

### **SQL Example: Create and Populate a Projects Table**
```sql
CREATE TABLE Projects (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    department TEXT NOT NULL
);

INSERT INTO Projects (name, department) VALUES
('Project A', 'HR'),
('Project B', 'IT'),
('Project C', 'Finance');
```

### **SQL Example: Complex JOIN**
List employees working in departments responsible for a specific project:
```sql
SELECT Employees.name, Projects.name AS project_name
FROM Employees
JOIN Projects ON Employees.department = Projects.department
WHERE Projects.name = 'Project A';
```

---

## **8.3 Aggregation**

### **Overview**
Aggregation functions like `MIN()`, `MAX()`, `COUNT()`, and `AVG()` allow you to summarize data across groups.

### **Task:**
Calculate the minimum and maximum salaries and the number of employees in each department.

### **SQL Example:**
```sql
SELECT department_id, 
       MIN(salary) AS min_salary, 
       MAX(salary) AS max_salary, 
       COUNT(employee_id) AS num_employees
FROM Employees
GROUP BY department_id;
```

### **Key Notes:**
- Use `GROUP BY` to organize results by department.
- Ensure fields in the `SELECT` clause are either aggregated or part of the `GROUP BY`.

---

## **8.4 Aggregation with HAVING**

### **Overview**
The `HAVING` clause filters aggregated results after the `GROUP BY` operation.

### **Task:**
List all departments where the average salary exceeds 70,000 and display the department manager.

### **SQL Example:**
```sql
SELECT d.department_name, 
       d.manager_id, 
       AVG(e.salary) AS avg_salary
FROM Departments AS d
JOIN Employees AS e ON d.department_id = e.department_id
GROUP BY d.department_id
HAVING AVG(e.salary) > 70000;
```

### **Key Notes:**
- Use `HAVING` instead of `WHERE` to filter aggregated results.
- Combine `JOIN`s and `GROUP BY` for advanced aggregations.

---

## **8.5 Performance Optimization: Indexing**

### **Overview**
SQL queries can sometimes be slow if they involve large tables. Indexes can be created on columns that are frequently used in `WHERE`, `JOIN`, or `ORDER BY` clauses to speed up query performance.

### **SQL Example:**
```sql
CREATE INDEX idx_department ON Employees(department_id);
```

This creates an index on the `department_id` column to speed up queries that filter by department.

---

## **8.6 Transactions and Rollbacks**

### **Overview**
Transactions ensure that multiple database operations are completed successfully before committing them. If an error occurs, you can roll back the changes to keep the database in a consistent state.

### **Example:**
```python
# Start a transaction
conn = sqlite3.connect("company.db")
cursor = conn.cursor()

try:
    cursor.execute("INSERT INTO Employees (name, department_id) VALUES ('John Doe', 2)")
    cursor.execute("INSERT INTO Employees (name, department_id) VALUES ('Jane Smith', 3)")
    conn.commit()  # Commit transaction
except Exception as e:
    conn.rollback()  # Rollback transaction if there's an error
    print("Error:", e)

conn.close()
```

---

## **8.7 Parameterized Queries to Prevent SQL Injection**

### **Overview**
SQL injection can be prevented by using parameterized queries, ensuring that user input is treated safely.

### **Example:**
```python
cursor.execute("SELECT * FROM Employees WHERE department_id = ?;", (department_id,))
```

This ensures that `department_id` is treated as a parameter and not part of the SQL statement itself.  If any part of the SQL statement comes from the end user or other untrusted source, always put that part in a parameter so that it can be sanitized to strip out rogue SQL.  Don't do it like this:

```python
cursor.execute(f"SELECT * FROM Employees WHERE department_id = {department_id};")
# or, equally bad:
cursor.execute("SELECT * FROM Employees WHERE department_id = " + department_id + ";")
```

---

## **8.8 Window Functions**

### **Overview**
SQL window functions allow for advanced analysis over a specified range of rows. For example, calculating the rank of employees within a department based on salary.

### **SQL Example:**
```sql
SELECT name, salary, department_id,
       RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rank
FROM Employees;
```

---

## **8.9 Date and Time Functions**

### **Overview**
SQL provides functions for manipulating and querying date and time data, which are useful when working with time-based analysis.

### **SQL Example:**
```sql
SELECT name, date_of_birth, 
       JULIANDAY('now') - JULIANDAY(date_of_birth) AS age_in_days
FROM Employees;
```

---

## **8.10 Implementing All Techniques in Python**

### **Implementation Tips**

1. **Test Queries Separately:**
   - Write and test each query independently in your script or database interface before integrating into Python.

2. **Iterative Debugging:**
   - Verify intermediate outputs (e.g., after `JOIN` or subquery execution).

3. **Error Handling in Python:**
   - Use `try-except` blocks to handle database connection errors.

### **Example Python Script:**
```python
import sqlite3

# Connect to the database
conn = sqlite3.connect("company.db")
cursor = conn.cursor()

# Aggregation with HAVING
query = """
SELECT d.department_name, 
       d.manager_id, 
       AVG(e.salary) AS avg_salary
FROM Departments AS d
JOIN Employees AS e ON d.department_id = e.department_id
GROUP BY d.department_id
HAVING AVG(e.salary) > 70000;
"""

# Execute and fetch results
cursor.execute(query)
results = cursor.fetchall()
print(results)

conn.close()
```

---

## **Summary**

In this lesson, you’ve learned:
1. How to use subqueries to dynamically fetch values for other queries.
2. How to use complex `JOIN`s to integrate data from multiple tables.
3. How to use aggregation functions to summarize data across groups.
4. How to apply `HAVING` for conditional filtering on aggregated data.
5. How to optimize performance with indexes.
6. How to use transactions and rollbacks to ensure data consistency.
7. How to prevent SQL injection with parameterized queries.
8. How to use window functions for advanced analytics.
9. How to handle date and time data for time-based analysis.

For further exploration, refer to the [SQLite Documentation](https://www.sqlite.org/docs.html) and Python's `sqlite3` library documentation.


**Video URL:** No video available

**Code Examples:**

No code examples available

**External Links:**

No external links available

**Quizzes:**

No quizzes available

## Supplemental Videos

No supplemental videos available

## References

No references available

## Podcast URL

No podcast available