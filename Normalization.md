# **🔹 SQL NORMALIZATION - The Ultimate Guide for Interviews 🚀**  

## **📌 What is Normalization?**  
Normalization is the **process of organizing data in a database** to:  
✅ Reduce **data redundancy**  
✅ Improve **data integrity**  
✅ Optimize **storage and performance**  

💡 **Think of Normalization as Organizing a Library 📚**  
- Books are placed in the right category (like separating data properly).  
- You don't repeat the same book in multiple places (avoiding redundancy).  
- Books are linked using references (like using Foreign Keys in SQL).  

---

## **🎯 Mnemonic to Remember Normal Forms**
🔹 **"1NF → 2NF → 3NF → BCNF → 4NF → 5NF"**  
🔹 **"One Sunny Day, Bruce Feeds Five Elephants"**  
- **1NF (First Normal Form)** → Remove **Repeating Groups**  
- **2NF (Second Normal Form)** → Remove **Partial Dependency**  
- **3NF (Third Normal Form)** → Remove **Transitive Dependency**  
- **BCNF (Boyce-Codd Normal Form)** → Stronger 3NF  
- **4NF (Fourth Normal Form)** → Remove **Multi-Valued Dependency**  
- **5NF (Fifth Normal Form)** → Remove **Join Dependency**  

---

## **📌 1NF (First Normal Form) - Remove Repeating Groups**
✅ **Rule:**  
1. Each column must have **atomic (indivisible) values**.  
2. Each row must be **unique (use a Primary Key)**.  
3. No **repeating groups** (no multiple values in a column).  

📌 **Real-World Example:**  
**Scenario:** A college stores students' courses in a single column.  

❌ **Unnormalized Table (Repeating Groups)**  
| Student_ID | Name  | Courses             |
|------------|-------|--------------------|
| 101        | Alice | Math, Science      |
| 102        | Bob   | English, History   |

✅ **1NF Table (Atomic Values, No Repeating Groups)**  
| Student_ID | Name  | Course   |
|------------|-------|---------|
| 101        | Alice | Math    |
| 101        | Alice | Science |
| 102        | Bob   | English |
| 102        | Bob   | History |

### **🚀 When to Use?**  
- When a column contains multiple values (e.g., storing multiple phone numbers in a single field).  

### **🔥 Why?**  
- Improves search and filtering.  
- Prevents data inconsistency.  

---

## **📌 2NF (Second Normal Form) - Remove Partial Dependency**
✅ **Rule:**  
1. Must be in **1NF**.  
2. No **partial dependency** (A non-key column should depend on the **whole** Primary Key, not just part of it).  

📌 **Real-World Example:**  
**Scenario:** A Student_Course table where the student’s department depends only on Student_ID, not Course_ID.  

❌ **1NF Table (Partial Dependency Exists)**  
| Student_ID | Course_ID | Department  |
|------------|----------|------------|
| 101        | Math     | Science    |
| 101        | Physics  | Science    |
| 102        | History  | Arts       |

✅ **2NF Table (Splitting into Two Tables)**  
🔹 **Student Table**  
| Student_ID | Department  |
|------------|------------|
| 101        | Science    |
| 102        | Arts       |

🔹 **Enrollment Table**  
| Student_ID | Course_ID |
|------------|----------|
| 101        | Math     |
| 101        | Physics  |
| 102        | History  |

### **🚀 When to Use?**  
- When a table has a **composite primary key** and some attributes depend only on part of it.  

### **🔥 Why?**  
- Eliminates duplicate data.  
- Reduces update anomalies.  

---

## **📌 3NF (Third Normal Form) - Remove Transitive Dependency**
✅ **Rule:**  
1. Must be in **2NF**.  
2. No **transitive dependency** (A non-key column should not depend on another non-key column).  

📌 **Real-World Example:**  
**Scenario:** A company stores Employee ID, Department, and Manager Name.  

❌ **2NF Table (Transitive Dependency Exists)**  
| Emp_ID | Department | Manager |
|--------|-----------|--------|
| 201    | HR        | Alice  |
| 202    | IT        | Bob    |

Here, **Manager depends on Department**, not Emp_ID.

✅ **3NF Table (Break into Two Tables)**  
🔹 **Employee Table**  
| Emp_ID | Department_ID |
|--------|--------------|
| 201    | 1            |
| 202    | 2            |

🔹 **Department Table**  
| Department_ID | Department | Manager |
|--------------|-----------|--------|
| 1            | HR        | Alice  |
| 2            | IT        | Bob    |

### **🚀 When to Use?**  
- When a **non-key attribute** depends on another **non-key attribute**.  

### **🔥 Why?**  
- Prevents update anomalies.  
- Improves data consistency.  

---

## **📌 BCNF (Boyce-Codd Normal Form) - Stronger 3NF**
✅ **Rule:**  
1. Must be in **3NF**.  
2. Every **determinant** (a column determining another column) should be a **candidate key**.  

📌 **Real-World Example:**  
**Scenario:** A professor can teach multiple courses, but each course is assigned to only one professor.  

❌ **3NF Table (Still Has Anomaly)**  
| Prof_ID | Course | Department |
|---------|-------|-----------|
| P1      | Math  | Science   |
| P2      | History | Arts     |

Here, **Course determines Department**, but Course is not a Candidate Key.

✅ **BCNF Table (Fix the Issue)**  
🔹 **Professor Table**  
| Prof_ID | Department |
|---------|-----------|
| P1      | Science   |
| P2      | Arts      |

🔹 **Course Table**  
| Course | Department |
|-------|-----------|
| Math  | Science   |
| History | Arts    |

### **🚀 When to Use?**  
- When 3NF doesn’t remove all redundancy.  

### **🔥 Why?**  
- Ensures all determinants are candidate keys.  

---

## **📌 4NF (Fourth Normal Form) - Remove Multi-Valued Dependencies**
✅ **Rule:**  
1. Must be in **BCNF**.  
2. No **multi-valued dependency** (Each attribute must depend on the whole primary key, not just part of it).  

📌 **Real-World Example:**  
**Scenario:** A store tracks suppliers and parts they provide.  

❌ **BCNF Table (Multi-Valued Dependency)**  
| Supplier | Part   | Location |
|----------|-------|---------|
| S1       | Bolt  | NY      |
| S1       | Screw | NY      |

✅ **4NF Table (Break into Two Tables)**  
🔹 **Supplier Table**  
| Supplier | Location |
|----------|---------|
| S1       | NY      |

🔹 **Supplier_Part Table**  
| Supplier | Part   |
|----------|-------|
| S1       | Bolt  |
| S1       | Screw |

---

## **📌 5NF (Fifth Normal Form) - Remove Join Dependency**
✅ **Rule:**  
1. Must be in **4NF**.  
2. No **lossless decomposition** (Tables should not need to be joined to restore original data).  

📌 **Real-World Example:**  
**Scenario:** A company assigns employees to projects via departments.  

❌ **4NF Table (Complex Dependencies)**  
| Emp_ID | Project | Department |
|--------|--------|-----------|
| E1     | P1     | D1        |
| E1     | P2     | D1        |

✅ **5NF Table (Separate Relationships)**  
🔹 **Employee_Project Table**  
| Emp_ID | Project |
|--------|--------|
| E1     | P1     |
| E1     | P2     |

🔹 **Project_Department Table**  
| Project | Department |
|--------|-----------|
| P1     | D1        |
| P2     | D1        |

---

## **🚀 Final Interview Tips**
✅ Always **explain with real-world examples**.  
✅ Show how normalization **removes redundancy** and **improves consistency**.  
✅ Be prepared to **demonstrate with SQL tables**.  

🔥 **You're now fully prepared to ace SQL Normalization in your interview! 💯** 🚀
