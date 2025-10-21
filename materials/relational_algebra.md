
<a href="https://github.com/drshahizan/database/stargazers"><img src="https://img.shields.io/github/stars/drshahizan/database" alt="Stars Badge"/></a>
<a href="https://github.com/drshahizan/database/network/members"><img src="https://img.shields.io/github/forks/drshahizan/database" alt="Forks Badge"/></a>
<a href="https://github.com/drshahizan/database/pulls"><img src="https://img.shields.io/github/issues-pr/drshahizan/database" alt="Pull Requests Badge"/></a>
<a href="https://github.com/drshahizan/database/issues"><img src="https://img.shields.io/github/issues/drshahizan/database" alt="Issues Badge"/></a>
<a href="https://github.com/drshahizan/database/graphs/contributors"><img alt="GitHub contributors" src="https://img.shields.io/github/contributors/drshahizan/database?color=2b9348"></a>
![Visitors](https://api.visitorbadge.io/api/visitors?path=https%3A%2F%2Fgithub.com%2Fdrshahizan%2Fdatabase&labelColor=%23d9e3f0&countColor=%23697689&style=flat)

# 🇲🇾 **Relational Algebra: Concepts, Examples, Case Study, and Usage**



## **1. Introduction**

**Relational Algebra** is a **formal mathematical language** used to retrieve, manipulate, and analyze data stored in **relational databases**.
It defines a series of **operations** that take one or more tables (relations) as input and return a new table as output.

Relational Algebra serves as the **theoretical foundation for SQL (Structured Query Language)** and helps database designers and developers understand how queries are processed internally.

## **2. Major Operations in Relational Algebra (with Malaysia-based Examples)**


### **2.1 Selection (σ)**

**Definition:**
Retrieves **specific rows** from a table that satisfy a certain condition.

**Symbol:** σ (sigma)
**SQL Equivalent:** `WHERE`

**Example (Malaysia):**
Find all students from **Johor** with a **CGPA above 3.50**.

**Relation:**
`Student(StudentID, Name, Gender, State, CGPA)`

**Relational Algebra Expression:**
[
σ_{State='Johor' ∧ CGPA>3.50}(Student)
]

**Result:**

| StudentID | Name              | Gender | State | CGPA |
| --------- | ----------------- | ------ | ----- | ---- |
| S1001     | Nur Aisyah Rahman | Female | Johor | 3.85 |
| S1008     | Tan Wei Ling      | Female | Johor | 3.70 |



### **2.2 Projection (π)**

**Definition:**
Retrieves **specific columns** from a table.

**Symbol:** π (pi)
**SQL Equivalent:** `SELECT column_name`

**Example (Malaysia):**
Show only the **Name** and **CGPA** of all students.

**Expression:**
[
π_{Name, CGPA}(Student)
]

**Result:**

| Name              | CGPA |
| ----------------- | ---- |
| Nur Aisyah Rahman | 3.85 |
| Ahmad Khairul     | 3.25 |
| Tan Wei Ling      | 3.70 |


### **2.3 Union (∪)**

**Definition:**
Combines tuples from two relations and removes duplicates.

**Symbol:** ∪
**SQL Equivalent:** `UNION`

**Example (Malaysia):**
List all students from **UTM** and **UKM**.

[
UTM_Students ∪ UKM_Students
]

**Result:**
A list of all students from both universities, with duplicates removed.



### **2.4 Set Difference (−)**

**Definition:**
Finds tuples that exist in one relation but not in another.

**Symbol:** −
**SQL Equivalent:** `EXCEPT`

**Example (Malaysia):**
Find students who are **enrolled in UTM** but **not in UKM**.

[
UTM_Students − UKM_Students
]

**Result:**
All students unique to UTM.



### **2.5 Cartesian Product (×)**

**Definition:**
Combines every tuple of one relation with every tuple of another.

**Symbol:** ×
**SQL Equivalent:** `CROSS JOIN`

**Example (Malaysia):**
Combine the **Lecturer** and **Course** tables to see all possible lecturer–course pairs.

[
Lecturer × Course
]



### **2.6 Rename (ρ)**

**Definition:**
Renames the attributes or the entire relation.

**Symbol:** ρ (rho)
**SQL Equivalent:** `AS`

**Example (Malaysia):**
Rename the `Student` table to `Pelajar`.

[
ρ_{Pelajar}(Student)
]



### **2.7 Join (⋈)**

**Definition:**
Combines rows from two relations based on a **common attribute**.

**Symbol:** ⋈
**SQL Equivalent:** `JOIN`

**Example (Malaysia):**
Join **Student** and **Program** tables to show students with their programs.

[
Student ⋈_{Student.ProgramID = Program.ProgramID} Program
]



## **3. Usage of Relational Algebra**

Relational Algebra is not only theoretical — it is applied widely in **database systems**, **data analytics**, and **information management**.

Below are some key areas of usage, especially in the Malaysian context:

| **Area**                              | **Description**                                                                                      | **Example (Malaysia)**                                                                               |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **1. Database Query Optimization**    | DBMS uses relational algebra internally to interpret SQL queries and find efficient execution paths. | Optimizing student records retrieval in UTM’s Academic Management System.                            |
| **2. Data Integration**               | Helps combine data from multiple systems using joins and unions.                                     | Integrating data from MOHE (KPT), UTM, and UKM databases for national reporting.                     |
| **3. Data Warehousing & Analytics**   | Relational algebra is used to design ETL (Extract, Transform, Load) pipelines and query cubes.       | KPT’s Data Warehouse project uses relational joins to connect student, lecturer, and research data.  |
| **4. Education Management Systems**   | Used in academic databases to extract insights.                                                      | Generating semester GPA reports for UTM students.                                                    |
| **5. Decision Support Systems (DSS)** | Supports structured queries that inform management decisions.                                        | Ministry of Education (MOE) using relational algebra queries to analyze school performance data.     |
| **6. Research Data Analysis**         | Helps query structured data in academic research databases.                                          | Malaysian research repositories (MyJurnal, MyGRANTS) apply relational principles to manage metadata. |



## **4. Case Study: Academic Management System at Universiti Teknologi Malaysia (UTM)**

### **4.1 Background**

The **UTM Academic Management System (AMS)** manages all academic information including students, courses, programs, and lecturers.
Database queries based on relational algebra allow administrators to:

* Generate academic reports
* Track student progress
* Analyze enrollment by gender, faculty, and year



### **4.2 Database Schema**

| Table          | Attributes                                      |
| -------------- | ----------------------------------------------- |
| **Student**    | StudentID, Name, Gender, ProgramID, YearOfStudy |
| **Program**    | ProgramID, ProgramName, Faculty                 |
| **Course**     | CourseID, CourseName, CreditHour, ProgramID     |
| **Enrollment** | StudentID, CourseID, Grade                      |
| **Lecturer**   | LecturerID, LecturerName, Faculty               |
| **Teaching**   | LecturerID, CourseID, Semester                  |



### **4.3 Objective**

Find the **names of female students** from the **Faculty of Computing** who are enrolled in the course **“Programming Technique II.”**



### **4.4 Step-by-Step Relational Algebra Solution**

1. **Join** the tables to combine data:
   [
   Temp1 ← Student ⋈ Program ⋈ Enrollment ⋈ Course
   ]

2. **Select (σ)** only records that meet conditions:
   [
   Temp2 ← σ_{Gender='Female' ∧ Faculty='Faculty of Computing' ∧ CourseName='Programming Technique II'}(Temp1)
   ]

3. **Project (π)** the names of the selected students:
   [
   Result ← π_{Name}(Temp2)
   ]



### **4.5 SQL Equivalent**

```sql
SELECT DISTINCT S.Name
FROM Student S
JOIN Program P ON S.ProgramID = P.ProgramID
JOIN Enrollment E ON S.StudentID = E.StudentID
JOIN Course C ON E.CourseID = C.CourseID
WHERE S.Gender = 'Female'
  AND P.Faculty = 'Faculty of Computing'
  AND C.CourseName = 'Programming Technique II';
```

### **4.6 Example Output**

| Name                      |
| ------------------------- |
| Nurul Hidayah Binti Ahmad |
| Tan Li Wen                |
| Aina Sofea Binti Hassan   |

---

### **4.7 Real UTM Usage**

At UTM, similar queries are used for:

* Generating **student enrollment reports** for faculties
* Tracking **female participation in computing programs**
* Monitoring **student performance** in core programming courses
* Preparing **data for MQA accreditation** or **university audits**

For example, the Faculty of Computing can use this to monitor how many female students have successfully completed Programming Technique II, supporting UTM’s goal of encouraging gender balance in STEM education.


## **5. Summary**

| **Aspect**          | **Explanation**                                                   | **Malaysia Example**                                              |
| ------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| **Purpose**         | Framework for database queries                                    | SQL optimization and data retrieval                               |
| **Core Operations** | Selection, Projection, Union, Difference, Join, Rename, Cartesian | UTM AMS, KPT Data Warehouse                                       |
| **Advantages**      | Clear logic, structured results, query optimization               | Used in UTM, MOHE, and national analytics                         |
| **Case Study**      | UTM Academic Management System                                    | Extract female Computing students taking Programming Technique II |



### ✅ **Conclusion**

Relational Algebra provides the **logical foundation for managing and querying data** in systems such as UTM’s Academic Management System, MOHE’s national databases, and university data warehouses.
By mastering relational algebra, database professionals and students in Malaysia can better design, query, and optimize educational and governmental data systems — supporting efficient decision-making in higher education.


## Contribution 🛠️
Please create an [Issue](https://github.com/drshahizan/HPDP/issues) for any improvements, suggestions or errors in the content.

You can also contact me using [Linkedin](https://www.linkedin.com/in/drshahizan/) for any other queries or feedback.

[![Visitors](https://api.visitorbadge.io/api/visitors?path=https%3A%2F%2Fgithub.com%2Fdrshahizan&labelColor=%23697689&countColor=%23555555&style=plastic)](https://visitorbadge.io/status?path=https%3A%2F%2Fgithub.com%2Fdrshahizan)
![](https://hit.yhype.me/github/profile?user_id=81284918)



