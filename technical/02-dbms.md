# DBMS — Technical Study Notes

> **Why it is asked:** DBMS questions appeared in the 54th and 55th BMA papers. Primary/candidate key definitions and aggregation functions are the most repeated items (confirmed in both papers). Normalization appeared as a short note in the 55th.

---

## 1. Keys in a Relational Database

| Key type | Definition | Example (`Student` table with attrs: `ID, NID, Email, Name`) |
|---|---|---|
| **Super key** | Any set of attributes that uniquely identifies a row (can have extras) | `{ID}`, `{NID}`, `{ID, Name}`, `{ID, NID, Email}` |
| **Candidate key** | A *minimal* super key — removing any attribute breaks uniqueness | `{ID}`, `{NID}`, `{Email}` |
| **Primary key** | The one candidate key chosen as the main identifier; must be NOT NULL and UNIQUE | `{ID}` |
| **Foreign key** | An attribute in one table that references the primary key of another table | `EnrollmentTable.StudentID` references `Student.ID` |

**Difference between primary and candidate key:**  
A candidate key is *eligible* to be the primary key (all minimal, unique). The primary key is the one *selected* from the candidates. All primary keys are candidate keys; not all candidate keys become primary keys.

---

## 2. Functional Dependency

**Definition:** In a relation R, a functional dependency X → Y means the value of X *uniquely determines* the value of Y. Equivalently, no two tuples can have the same X value with different Y values.

**Example:**  
In `Student(StudentID, Name, DeptID, DeptName)`:
- `StudentID → Name` (one ID → one name)
- `StudentID → DeptID`
- `DeptID → DeptName` (department ID determines department name)

**Types:**
- **Trivial FD:** Y is a subset of X (e.g. `{A, B} → A`). Always true.
- **Non-trivial FD:** Y is not a subset of X (e.g. `StudentID → Name`). The interesting ones.
- **Transitive FD:** X → Z via X → Y → Z. (e.g. `StudentID → DeptID → DeptName` so `StudentID →(transitively) DeptName`.)
- **Partial FD:** Part of a composite key determines a non-key attribute. Violates 2NF.

---

## 3. Normalisation

Normalisation removes data redundancy and anomalies (insert / update / delete anomalies) by organising tables into a set of well-defined normal forms.

### 1NF (First Normal Form)
- All attribute values are **atomic** (no repeating groups, no multi-valued cells).
- Each column has a unique name; each row is uniquely identifiable.

*Violation example:* `Courses` column holding `"Math, Physics"` → split into separate rows.

### 2NF (Second Normal Form)
- Must be in 1NF.
- **No partial dependency:** every non-key attribute must depend on the *whole* primary key (applicable when the key is composite).

*Violation example:* Table `(StudentID, CourseID, CourseName, Grade)` — `CourseName` depends only on `CourseID`, not on the full `{StudentID, CourseID}` key. Fix: split into `Course(CourseID, CourseName)` and `Enrolment(StudentID, CourseID, Grade)`.

### 3NF (Third Normal Form)
- Must be in 2NF.
- **No transitive dependency:** no non-key attribute determines another non-key attribute.

*Violation example:* `(StudentID, DeptID, DeptName)` — `DeptName` depends on `DeptID`, not directly on `StudentID`. Fix: split into `Student(StudentID, DeptID)` and `Department(DeptID, DeptName)`.

### BCNF (Boyce–Codd Normal Form) — name only
- Stricter version of 3NF: for every FD X → Y, X must be a superkey.
- Not drilled in this exam but worth naming as "beyond 3NF".

---

## 4. Aggregation Functions

SQL aggregation functions compute a single result from a set of values.

| Function | Description | Example |
|---|---|---|
| `COUNT(col)` | Number of non-null values | `SELECT COUNT(*) FROM Student;` |
| `SUM(col)` | Total of numeric values | `SELECT SUM(Marks) FROM Result;` |
| `AVG(col)` | Arithmetic mean | `SELECT AVG(Marks) FROM Result;` |
| `MIN(col)` | Smallest value | `SELECT MIN(Marks) FROM Result;` |
| `MAX(col)` | Largest value | `SELECT MAX(Marks) FROM Result;` |

These are used with `GROUP BY` to compute per-group statistics:

```sql
SELECT DeptID, AVG(Marks) AS AvgMarks
FROM Result
GROUP BY DeptID;
```

**Aggregation in ER context:** In entity-relationship diagrams, *aggregation* means treating a relationship (and its related entities) as a higher-level entity to model relationships between relationships. Different from SQL aggregation functions — the exam's "Aggregation in database function" refers to the SQL functions above.

---

## 5. Cardinality

Cardinality in DBMS context has two meanings:

1. **Relationship cardinality:** The number of entities one instance can be associated with — **1:1**, **1:N**, **M:N**.  
   Example: One student can enrol in many courses (1:N between Student and Course).

2. **Column cardinality:** The number of distinct values in a column. A primary key has maximum cardinality (all unique); a binary `Gender` column has cardinality 2.

---

## Q&A Bank

### True / False

**T1.** A primary key cannot contain NULL values.  
→ **True**

**T2.** Every primary key is a candidate key.  
→ **True**

**T3.** Every candidate key is a primary key.  
→ **False** (Only one candidate key is chosen as the primary key.)

**T4.** The functional dependency `{A, B} → A` is a trivial dependency.  
→ **True**

**T5.** A relation in 2NF can still have transitive dependencies.  
→ **True** (Transitive dependencies are removed in 3NF, not 2NF.)

**T6.** `AVG()` ignores NULL values in SQL.  
→ **True** (All SQL aggregation functions ignore NULLs, except `COUNT(*)`.)

---

### MCQ

**Q1.** Which of the following is a minimal super key?  
(a) Super key  (b) Foreign key  (c) Candidate key  (d) Composite key  
→ **(c)** Candidate key

**Q2.** Which SQL function returns the number of rows in a table?  
(a) `SUM`  (b) `MAX`  (c) `AVG`  (d) `COUNT`  
→ **(d)** `COUNT`

**Q3.** A relation `R(A, B, C)` has functional dependencies `A → B` and `B → C`. The type of dependency `A → C` is:  
(a) Partial  (b) Trivial  (c) Transitive  (d) Multi-valued  
→ **(c)** Transitive

**Q4.** Which normal form removes partial dependencies?  
(a) 1NF  (b) 2NF  (c) 3NF  (d) BCNF  
→ **(b)** 2NF

**Q5.** A foreign key in table B references:  
(a) Any column of table A  (b) The primary key of table A  (c) A candidate key of table B  (d) The super key of table A  
→ **(b)** The primary key of table A

---

### Descriptive Q&A

**Q.** Define primary key and candidate key with examples. (8 marks)

**A.**  
**Candidate key:** A minimal set of attributes that uniquely identifies every tuple (row) in a relation. "Minimal" means no proper subset of the candidate key is itself a unique identifier.

**Primary key:** The one candidate key selected by the database designer to be the principal unique identifier for a table. It must satisfy:
- Uniqueness: no two rows have the same value
- Not null: it cannot be NULL

**Example:**  
Consider `Student(StudentID, NationalID, Email, Name)`.  
- `StudentID` alone uniquely identifies each student → candidate key.  
- `NationalID` alone also uniquely identifies each student → candidate key.  
- `Email` also qualifies → candidate key.  
- `{StudentID, Name}` uniquely identifies but is not minimal (removing `Name` still works) → super key, not candidate key.  
- The designer chooses `StudentID` as the **primary key**.

---

**Q.** Explain functional dependency in a database with an example. (8 marks)

**A.**  
A **functional dependency** (FD) is a constraint between two sets of attributes in a relation. We write X → Y (X determines Y) to mean: for any two tuples t1 and t2 in the relation, if t1[X] = t2[X] then t1[Y] = t2[Y]. In other words, knowing the value of X is enough to determine the value of Y.

**Example relation:** `Employee(EmpID, Name, DeptID, DeptName, Salary)`  
FDs present:  
- `EmpID → Name, DeptID, Salary` — Employee ID determines all personal attributes.  
- `DeptID → DeptName` — Department ID determines Department Name.  
- `EmpID →(transitively) DeptName` — via EmpID → DeptID → DeptName.

The transitive dependency `EmpID → DeptName` is a violation of 3NF, which is resolved by splitting into:
- `Employee(EmpID, Name, DeptID, Salary)`  
- `Department(DeptID, DeptName)`

---

**Q.** What are aggregation functions in a database? (5 marks)

**A.**  
SQL aggregation functions perform calculations on a set of values and return a single summary value. They are used with `SELECT` queries, often combined with `GROUP BY`.

The five standard aggregation functions are:
1. `COUNT` — counts the number of rows (or non-null values in a column).
2. `SUM` — calculates the total of a numeric column.
3. `AVG` — calculates the average (mean) of a numeric column.
4. `MIN` — returns the smallest value in a column.
5. `MAX` — returns the largest value in a column.

Example:
```sql
SELECT DeptID,
       COUNT(*) AS TotalStudents,
       AVG(CGPA)  AS AverageCGPA,
       MAX(CGPA)  AS TopCGPA
FROM Student
GROUP BY DeptID;
```
This returns the count, average CGPA, and top CGPA for each department.

---

### Common Traps

| Misconception | Correction |
|---|---|
| "Primary key and candidate key are the same thing" | A primary key is one selected candidate key; there may be others. |
| "Foreign key must be unique" | Foreign keys do NOT need to be unique (many rows can reference the same parent PK). |
| "`COUNT(col)` counts NULLs" | `COUNT(col)` skips NULLs; only `COUNT(*)` counts all rows including NULLs. |
