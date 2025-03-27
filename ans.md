## 🚀 **SQL & DBMS 10-Minute Cheat Sheet**  

🔹 **Mnemonic: DATABASE FAST JOIN ACID KEY RECOVERY**  
🔹 Covers **all SQL & DBMS concepts** with **queries, examples, real-world use cases, and interview questions.**  
🔹 **Perfect for last-minute revision before an interview!**  

---

## **🛢️ DATABASE - Core DBMS Concepts**  
| 🔤 Mnemonic | 📝 Concept | 🌍 Real-World Use Case | 💻 Query | 📌 Interview Q&A |
|------------|-----------|-----------------|------------|----------------------|
| **D** - Data Models | Hierarchical, Network, Relational, Object-Oriented | **Banking** - Relational DB for transactions | `CREATE TABLE Account (ID INT, Balance DECIMAL);` | **Q:** What are data models? **A:** They define how data is stored and related. |
| **A** - Attributes & Entities | Table Columns & Rows | **Students in College** 🎓 | `CREATE TABLE Student (ID INT PRIMARY KEY, Name VARCHAR(50));` | **Q:** What is an entity? **A:** A real-world object stored as a table. |
| **T** - Transactions | COMMIT, ROLLBACK | **Money Transfer** 💰 (Ensures no partial updates) | `BEGIN; UPDATE Account SET balance = balance - 500 WHERE ID=1; COMMIT;` | **Q:** Why use transactions? **A:** To ensure **consistency & integrity** of data. |
| **A** - ACID Properties | Ensures Reliability | **Flight Booking System** ✈️ | `BEGIN TRANSACTION; INSERT INTO Booking VALUES (1, 'Confirmed'); COMMIT;` | **Q:** Explain ACID? **A:** **Atomicity, Consistency, Isolation, Durability.** |
| **B** - Backup & Recovery | Restoring Data | **Cloud Backup** ☁️ | `BACKUP DATABASE myDB TO DISK = 'backup.bak';` | **Q:** How does DBMS recover from failure? **A:** Using logs and backups. |
| **A** - Anomalies & Normalization | Avoid Redundancy | **Employee Data Cleanup** | **1NF, 2NF, 3NF** | **Q:** What is normalization? **A:** Process to reduce redundancy. |
| **S** - SQL Basics | Querying Data | **Employee Salary Fetch** | `SELECT Name, Salary FROM Employee;` | **Q:** What is SQL? **A:** Structured Query Language for databases. |
| **E** - ER Model | Entity-Relationship Diagram | **Library Management** 📚 | **1:M, M:M, 1:1** | **Q:** What is an ER model? **A:** A visual representation of database structure. |

---

## **⚡ FAST - SQL Query Concepts**  
| 🔤 Mnemonic | 📝 Concept | 🌍 Use Case | 💻 Query | 📌 Interview Q&A |
|------------|-----------|------------|----------|----------------|
| **F** - Functions | SUM, AVG, COUNT | **Total Sales in a Month** 📊 | `SELECT SUM(sales) FROM Transactions WHERE MONTH(date) = 3;` | **Q:** What are aggregate functions? **A:** Functions like SUM, COUNT, AVG. |
| **A** - Aliases & Constraints | AS, NOT NULL, UNIQUE | **Rename Columns in Reports** | `SELECT Name AS "Employee Name" FROM Employee;` | **Q:** Why use aliases? **A:** To improve readability. |
| **S** - Subqueries | Nested Queries | **Find Employees Earning Above Avg Salary** | `SELECT Name FROM Employee WHERE Salary > (SELECT AVG(Salary) FROM Employee);` | **Q:** What is a subquery? **A:** A query inside another query. |
| **T** - Transactions Control | COMMIT, ROLLBACK | **Bank Transactions** 💳 | `BEGIN; UPDATE Account SET balance = balance - 500 WHERE ID=1; COMMIT;` | **Q:** Difference between COMMIT & ROLLBACK? **A:** COMMIT saves, ROLLBACK undoes. |

---

## **🤝 JOIN - SQL Joins & Relationships**  
| 🔤 Mnemonic | 📝 Concept | 🌍 Use Case | 💻 Query | 📌 Interview Q&A |
|------------|-----------|------------|----------|----------------|
| **J** - Joins | INNER, LEFT, RIGHT, FULL, SELF | **Employee-Department Relationship** | `SELECT E.Name, D.Dept_Name FROM Employee E JOIN Department D ON E.Dept_ID = D.Dept_ID;` | **Q:** Types of joins? **A:** INNER, LEFT, RIGHT, FULL. |
| **O** - ORDER BY & GROUP BY | Sorting & Aggregation | **Sort Employees by Salary** | `SELECT Name, Salary FROM Employee ORDER BY Salary DESC;` | **Q:** Difference between ORDER BY & GROUP BY? **A:** ORDER sorts, GROUP groups. |
| **I** - Indexing | Speed up Queries | **Fast Employee Lookup** 🔍 | `CREATE INDEX idx_name ON Employee(Name);` | **Q:** What is indexing? **A:** A technique to improve query performance. |
| **N** - Normalization | Reduce Redundancy | **Optimize Student Database** | **1NF - Unique Values, 2NF - No Partial Dependency, 3NF - No Transitive Dependency** | **Q:** What is normalization? **A:** A method to structure databases efficiently. |

---

## **🛑 ACID - Transaction & Consistency Principles**  
| 🔤 Mnemonic | 📝 Concept | 🌍 Use Case | 📌 Interview Q&A |
|------------|-----------|------------|----------------|
| **A** - Atomicity | All or Nothing | **Ticket Booking** 🎫 | **Q:** Why atomicity? **A:** Ensures complete transactions. |
| **C** - Consistency | Maintains Validity | **Balance Calculation** | **Q:** How does consistency work? **A:** Keeps data valid. |
| **I** - Isolation | Transactions Don’t Interfere | **Online Payments** | **Q:** What is isolation? **A:** Prevents conflicts between transactions. |
| **D** - Durability | Data Persists | **Power Failure Recovery** | **Q:** Why is durability important? **A:** Ensures committed data is never lost. |

---

## **🔑 KEY - Database Keys**  
| 🔤 Mnemonic | 📝 Concept | 🌍 Use Case | 💻 Query | 📌 Interview Q&A |
|------------|-----------|------------|----------|----------------|
| **P** - Primary Key | Unique Row ID | **Employee ID** 🆔 | `CREATE TABLE Employee (ID INT PRIMARY KEY, Name VARCHAR(50));` | **Q:** Difference between Primary & Foreign Key? **A:** Primary is unique, Foreign links tables. |
| **F** - Foreign Key | Connects Tables | **Orders linked to Customers** | `CREATE TABLE Orders (Order_ID INT, Cust_ID INT, FOREIGN KEY (Cust_ID) REFERENCES Customers(Cust_ID));` | **Q:** What is a foreign key? **A:** A key that connects tables. |
| **C** - Composite Key | Multi-Column Key | **Order + Product IDs as Key** | `PRIMARY KEY (Order_ID, Product_ID)` | **Q:** When to use Composite Keys? **A:** When uniqueness depends on multiple columns. |

---

## **🔄 RECOVERY - Performance & Optimization**  
| 🔤 Mnemonic | 📝 Concept | 🌍 Use Case | 📌 Interview Q&A |
|------------|-----------|------------|----------------|
| **R** - Redundancy Reduction | Remove Duplicates | **Employee Data Cleanup** | **Q:** How does normalization help? **A:** It removes redundancy. |
| **E** - ER Diagrams | Visual Data Representation | **E-commerce Database Design** | **Q:** Why use ER diagrams? **A:** To design efficient databases. |
| **C** - Concurrency Control | Handle Multiple Transactions | **E-Ticket Booking System** | **Q:** What is Deadlock? **A:** A situation where two transactions block each other. |
| **O** - Optimization | Indexing & Partitioning | **Fast Query Execution** | **Q:** How to speed up SQL queries? **A:** Use **indexes & partitioning**. |

---

### 🎯 **LAST-MINUTE REVISION (30 SECONDS)**  
🔹 **DATABASE** ✅ **DBMS Basics**  
🔹 **FAST** ✅ **SQL Queries**  
🔹 **JOIN** ✅ **Relations & Joins**  
🔹 **ACID** ✅ **Transaction Principles**  
🔹 **KEY** ✅ **Primary, Foreign, Composite Keys**  
🔹 **RECOVERY** ✅ **Optimization & Performance**  

🔥 **Now you're interview-ready! Go ace it!** 🚀
