## **🔑 SQL Keys - The Backbone of Databases (Detailed Explanation with Examples)**  

SQL **Keys** are essential for maintaining the integrity, uniqueness, and relationships between records in a relational database. They help ensure **data consistency and avoid duplication**.

---

## **📌 Types of Keys in SQL**
### 🎯 **Quick Mnemonic to Remember Keys**  
🔹 **"PUN-FCA"** → **P**rimary, **U**nique, **N**atural, **F**oreign, **C**andidate, **A**lternate

| Key Type           | Ensures | Real-World Example |
|--------------------|---------|--------------------|
| **Primary Key** (PK) | Uniqueness & Identity | Student Roll Number 🎓 |
| **Unique Key**     | Uniqueness but allows NULL | Social Security Number (SSN) |
| **Foreign Key** (FK) | Relationship between tables | Order linked to Customer |
| **Candidate Key**  | A potential PK | Passport Number OR SSN |
| **Alternate Key**  | A rejected Candidate Key | If SSN is not PK, it is AK |
| **Composite Key**  | Uniqueness with multiple columns | Flight (Airline + FlightNumber) |
| **Surrogate Key**  | System-generated unique identifier | Auto-generated UserID |
| **Super Key**      | Uniqueness but can have extra columns | (RollNumber, Name) |
| **Natural Key**    | Real-world unique identifier | Employee Email 📧 |

---

## **🔹 1. Primary Key (PK)**
✅ Ensures **uniqueness** and **cannot be NULL**.  
📌 **Use case:** Identifying each row uniquely (e.g., Employee ID, Student Roll Number).

🔹 **Table: Employees**
```sql
CREATE TABLE Employees (
    emp_id INT PRIMARY KEY, -- Unique, Non-NULL
    name VARCHAR(50),
    department VARCHAR(30)
);
```
🔹 **When to Use?**  
- When a table needs a unique identifier.  
- To reference in other tables (as a Foreign Key).

🔹 **Why?**  
- Guarantees unique records.
- Helps with indexing and fast lookups.

---

## **🔹 2. Unique Key**
✅ Ensures **uniqueness** but allows **NULL values**.  
📌 **Use case:** Fields like Email, Passport Number, or SSN.

🔹 **Table: Users**
```sql
CREATE TABLE Users (
    user_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE, -- Ensures unique emails
    phone_number VARCHAR(15)
);
```
🔹 **When to Use?**  
- When a field should be unique **but can be NULL** (e.g., an optional alternative ID).

🔹 **Why?**  
- Allows flexibility while preventing duplicates.

---

## **🔹 3. Foreign Key (FK)**
✅ Establishes **relationships** between tables.  
📌 **Use case:** Orders linked to Customers.

🔹 **Table: Orders (Linked to Customers)**
```sql
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(50)
);

CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    amount DECIMAL(10,2),
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id) -- Ensures data integrity
);
```
🔹 **When to Use?**  
- When creating **one-to-many** relationships (e.g., One Customer → Many Orders).  
- When enforcing **referential integrity** (an Order cannot exist without a valid Customer).  

🔹 **Why?**  
- Prevents orphan records (an Order without a Customer).  
- Maintains consistency between related tables.

---

## **🔹 4. Candidate Key**
✅ A **potential** Primary Key.  
📌 **Use case:** A table has multiple unique columns (e.g., Passport Number, SSN).

🔹 **Example Table: Citizens**
```sql
CREATE TABLE Citizens (
    citizen_id INT PRIMARY KEY,
    passport_number VARCHAR(20) UNIQUE,
    ssn VARCHAR(20) UNIQUE
);
```
🔹 **When to Use?**  
- When a table has multiple **uniquely identifying attributes**, and one must be chosen as PK.

🔹 **Why?**  
- Helps in database design by identifying alternate keys.

---

## **🔹 5. Alternate Key**
✅ A **Candidate Key** that was **not chosen** as PK.  
📌 **Use case:** If Passport Number is not the PK, it becomes an **Alternate Key**.

🔹 **Example:**  
```sql
ALTER TABLE Citizens ADD CONSTRAINT alt_key UNIQUE (passport_number);
```

🔹 **When to Use?**  
- When a table has multiple possible unique identifiers.

🔹 **Why?**  
- Maintains alternative unique constraints.

---

## **🔹 6. Composite Key**
✅ A key made of **multiple columns**.  
📌 **Use case:** A Flight has a unique **Airline + Flight Number** combination.

🔹 **Table: Flights**
```sql
CREATE TABLE Flights (
    airline VARCHAR(50),
    flight_number VARCHAR(10),
    departure_date DATE,
    PRIMARY KEY (airline, flight_number) -- Composite Key
);
```
🔹 **When to Use?**  
- When a single column **cannot** uniquely identify records.

🔹 **Why?**  
- Helps in scenarios where **combined values** make each row unique.

---

## **🔹 7. Surrogate Key**
✅ A **system-generated** unique identifier (Auto-Increment).  
📌 **Use case:** Auto-generated User ID instead of a Natural Key like SSN.

🔹 **Example:**  
```sql
CREATE TABLE Users (
    user_id INT AUTO_INCREMENT PRIMARY KEY, -- Surrogate Key
    username VARCHAR(50)
);
```
🔹 **When to Use?**  
- When **natural keys are inefficient** (e.g., using Email as PK).  
- For performance benefits in indexing.

🔹 **Why?**  
- Ensures efficiency and consistency.

---

## **🔹 8. Super Key**
✅ Any key that uniquely identifies a row but **may have extra columns**.  
📌 **Use case:** A key containing redundant columns.

🔹 **Example Table: Students**
```sql
CREATE TABLE Students (
    roll_no INT,
    name VARCHAR(50),
    dob DATE,
    PRIMARY KEY (roll_no)
);
```
**Super Key Examples:**  
- `(roll_no) ✅` (Minimal Super Key = Primary Key)  
- `(roll_no, name) ❌` (Redundant, still unique)

🔹 **When to Use?**  
- Used in **database normalization** to remove unnecessary attributes.

---

## **🔹 9. Natural Key**
✅ A **real-world unique identifier** (instead of auto-generated).  
📌 **Use case:** Employee **Email** instead of an ID.

🔹 **Example:**  
```sql
CREATE TABLE Employees (
    email VARCHAR(100) PRIMARY KEY, -- Natural Key
    name VARCHAR(50)
);
```
🔹 **When to Use?**  
- When a column already ensures uniqueness **without an artificial key**.

🔹 **Why?**  
- More readable and directly meaningful.

---

## **📌 Choosing the Right Key**
| Key Type        | Use When? | Example |
|----------------|-----------|---------|
| **Primary Key** | Always needed | Student Roll Number |
| **Unique Key** | Uniqueness but allows NULL | Email Address |
| **Foreign Key** | Establishing relationships | Order linked to Customer |
| **Candidate Key** | Multiple potential PKs | SSN vs. Passport Number |
| **Alternate Key** | A rejected Candidate Key | Passport Number |
| **Composite Key** | Uniqueness needs multiple columns | (Airline, Flight Number) |
| **Surrogate Key** | Auto-generated unique ID | Auto-increment User ID |
| **Super Key** | Unique but contains extra fields | (Roll Number, Name) |
| **Natural Key** | Real-world meaningful ID | Employee Email |

---

### **🔥 Final Interview Tips**
1. **Explain key constraints clearly** (PK: Unique + Not NULL, FK: Enforces relationships).  
2. **Use real-world examples** (Customer ID, Orders, Flights, Employees).  
3. **Show practical SQL queries** to prove your understanding.  
4. **Understand when to use each key type** and why.

🚀 **You're now fully prepared to ace SQL keys in your interview!** 🔥💯
