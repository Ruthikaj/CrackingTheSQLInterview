That's a solid set of database interview questions. I'll break them down with clear explanations, real-world examples, and SQL queries where needed.  

---

## **1. Difference Between SQL and NoSQL Databases**
| Feature         | SQL (Relational DB) | NoSQL (Non-Relational DB) |
|---------------|------------------|------------------|
| **Structure**  | Structured, Table-based | Unstructured/Semi-structured (JSON, Key-Value, Graph, etc.) |
| **Schema**     | Fixed schema, predefined columns | Dynamic schema, flexible structure |
| **Scalability**| Vertical (Adding resources to a single server) | Horizontal (Distributed architecture, sharding) |
| **Transactions** | ACID-compliant (strong consistency) | BASE model (Eventual consistency) |
| **Use Case**   | Banking, e-commerce (where transactions require consistency) | Big Data, IoT, social media (scalability over consistency) |
| **Examples**   | MySQL, PostgreSQL, SQL Server | MongoDB, Cassandra, Redis |

**When to use what?**  
- **SQL**: When strict data consistency is required (e.g., banking).  
- **NoSQL**: When scalability and flexibility are needed (e.g., real-time analytics, social networks).

---

## **2. Which Database for Transactions?**
For transactions, **SQL (Relational Databases like MySQL, PostgreSQL, etc.)** is preferred because it supports **ACID** properties, ensuring data integrity.  
NoSQL databases, though faster, often use **eventual consistency**, which may not be suitable for financial transactions.

---

## **3. ACID Properties & Application in a Project**
### **ACID Principle:**
1. **Atomicity**: All operations in a transaction must succeed or none should happen.  
   - *Example*: If a bank transfer ($100 from A to B) fails midway, no money should be deducted.
2. **Consistency**: The database remains valid before and after transactions.  
   - *Example*: Ensuring balance updates follow business rules.
3. **Isolation**: Transactions run independently without affecting each other.  
   - *Example*: Two users withdrawing money from the same account should not interfere.
4. **Durability**: Once a transaction is committed, it must be permanent.  
   - *Example*: Even if a system crashes, a completed money transfer should not be lost.

**Applying to a project:**  
- Use **BEGIN TRANSACTION, COMMIT, ROLLBACK** in SQL for atomic operations.  
- Use **locking mechanisms** or **isolation levels** to prevent concurrency issues.

---

## **4. SQL & Joins**
SQL (**Structured Query Language**) is used to manage relational databases.

### **Types of Joins**
| Join Type | Description | Example Use Case |
|-----------|------------|------------------|
| **INNER JOIN** | Returns matching records from both tables | Fetch employees with department details |
| **LEFT JOIN** | Returns all records from left table + matched records from right | Fetch all employees and their departments (if assigned) |
| **RIGHT JOIN** | Returns all records from right table + matched records from left | Fetch all departments and their employees (if any) |
| **FULL OUTER JOIN** | Returns all records when there is a match in either table | Fetch all employees and departments, even if unmatched |
| **SELF JOIN** | Joins a table with itself | Finding employees with the same manager |

### **Use of SELF JOIN in SQL**
Used when comparing records within the same table.  
**Example:** Finding employees reporting to the same manager:
```sql
SELECT e1.name AS Employee, e2.name AS Manager
FROM Employee e1
JOIN Employee e2 ON e1.manager_id = e2.emp_id;
```

---

## **5. Fraudulent Debit Transaction in a Bank**
If a fraudulent transaction occurs:
1. **If a third party used the PIN**:  
   - No issue with the system, the bank must investigate.
2. **If multiple fraudulent transactions happen in a short span**:  
   - Possible system bug → Investigate logs, check timestamps.  
   - Run **modular code testing** and **exception handling**.
   - Use **real-time fraud detection systems** (flagging multiple withdrawals in seconds).

---

## **6. Handling “Memory Full” in a Database**
**Short-term Fixes:**  
✅ **Normalization** to reduce redundancy  
✅ **Optimize Indexing** to reduce space  
✅ **Identify Memory Leaks** and fix inefficient queries  
✅ **Check Fragmentation** and compact storage  

**Long-term Fixes:**  
✅ **Move to Cloud Databases** (AWS RDS, Azure SQL, etc.)  
✅ **Sharding** (Splitting large tables across databases)  
✅ **Replication & Load Balancing** to distribute load  

---

## **7. Hashing, Indexing, and Normalization**
- **Hashing**: Converts data into a fixed-size value for fast lookups (used in password storage).  
- **Indexing**: Creates an efficient data retrieval mechanism using **B-Trees, Hash Indexes**.  
- **Normalization**: Reduces redundancy in a database.

### **Normalization Levels**
| Normal Form | Description | Example |
|-------------|------------|---------|
| **1NF** | No duplicate rows, atomic columns | Splitting "Full Name" into "First Name" and "Last Name" |
| **2NF** | 1NF + No Partial Dependencies | Removing redundant department names from an employee table |
| **3NF** | 2NF + No Transitive Dependencies | Storing department info separately from employees |
| **BCNF** | Advanced 3NF ensuring strict dependency rules | Useful in multi-key relationships |

---

## **8. How to Delete Duplicate Entries from a Table**
### **Approach:**
Find duplicate rows using `ROW_NUMBER()` and delete those not having the minimum `id`.

```sql
WITH CTE AS (
    SELECT *, ROW_NUMBER() OVER (PARTITION BY column1, column2 ORDER BY id) AS rn
    FROM table_name
)
DELETE FROM table_name WHERE id IN (SELECT id FROM CTE WHERE rn > 1);
```

---

## **9. ER Diagram for an Attendance Management System**
### Entities:
1. **Student** (student_id, name, class)  
2. **Attendance** (attendance_id, student_id, date, status)  
3. **Class** (class_id, teacher_id)  
4. **Teacher** (teacher_id, name)  

### Relationships:
- A **student** attends multiple **classes**.
- A **teacher** manages a **class**.
- **Attendance** is recorded for **students**.

---

## **10. SQL Query for Employee Grade & Second Highest Salary**
```sql
SELECT grade, MAX(salary) AS Second_Highest_Salary
FROM (
    SELECT grade, salary, DENSE_RANK() OVER (PARTITION BY grade ORDER BY salary DESC) AS rnk
    FROM Employee
) t
WHERE rnk = 2
AND grade = '3';
```

---

## **11. SQL Keys (Example: Student Database)**
| Key Type | Description | Example |
|----------|------------|---------|
| **Primary Key** | Uniquely identifies each row | student_id in Student table |
| **Foreign Key** | Links two tables | student_id in Attendance table |
| **Candidate Key** | Unique column that could be a primary key | (student_id, email) |
| **Composite Key** | Primary key using multiple columns | (student_id, class_id) |
| **Super Key** | Set of keys including primary key | (student_id, name) |

---

## **12. Data Storage in Databases & ACID Properties**
Data is stored in **tables, indexes, B-Trees, heaps, or JSON (NoSQL)**.  
ACID properties ensure data consistency in relational databases.

---

## **13. SQL Commands (DDL, DML, DCL, TCL)**
| Category | Commands | Use Case |
|----------|---------|----------|
| **DDL** (Data Definition) | CREATE, ALTER, DROP | Define table structures |
| **DML** (Data Manipulation) | INSERT, UPDATE, DELETE | Modify data |
| **DCL** (Data Control) | GRANT, REVOKE | Set permissions |
| **TCL** (Transaction Control) | COMMIT, ROLLBACK, SAVEPOINT | Manage transactions |

---

## **14. Difference Between Recovery & Restoration**
| Concept | Definition |
|---------|-----------|
| **Recovery** | Restoring data after a failure using transaction logs |
| **Restoration** | Reloading a full backup (requires backup files) |

---

These answers will impress interviewers with structured, precise, and in-depth responses. Need any refinements? 🚀
