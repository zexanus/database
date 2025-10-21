
<a href="https://github.com/drshahizan/database/stargazers"><img src="https://img.shields.io/github/stars/drshahizan/database" alt="Stars Badge"/></a>
<a href="https://github.com/drshahizan/database/network/members"><img src="https://img.shields.io/github/forks/drshahizan/database" alt="Forks Badge"/></a>
<a href="https://github.com/drshahizan/database/pulls"><img src="https://img.shields.io/github/issues-pr/drshahizan/database" alt="Pull Requests Badge"/></a>
<a href="https://github.com/drshahizan/database/issues"><img src="https://img.shields.io/github/issues/drshahizan/database" alt="Issues Badge"/></a>
<a href="https://github.com/drshahizan/database/graphs/contributors"><img alt="GitHub contributors" src="https://img.shields.io/github/contributors/drshahizan/database?color=2b9348"></a>
![Visitors](https://api.visitorbadge.io/api/visitors?path=https%3A%2F%2Fgithub.com%2Fdrshahizan%2Fdatabase&labelColor=%23d9e3f0&countColor=%23697689&style=flat)

# Relational Algebra — Practice Set (Malaysia Context)

## Mini Dataset (use these schemas throughout)

**Student(StudentID, Name, Gender, State, ProgramID, YearOfStudy, CGPA)**

```
S1001, "Nur Aisyah",  F, "Johor",   P10, 2, 3.82
S1002, "Ahmad Firdaus", M, "Selangor", P20, 3, 3.10
S1003, "Tan Wei Ling", F, "Johor",   P10, 1, 3.67
S1004, "Aina Sofea",   F, "Penang",  P30, 2, 3.45
S1005, "Syafiq Razif", M, "Johor",   P10, 4, 3.25
```

**Program(ProgramID, ProgramName, Faculty)**

```
P10, "Bachelor of Computer Science", "Faculty of Computing"
P20, "Bachelor of Information Systems", "Faculty of Computing"
P30, "Bachelor of Electrical Engineering", "Faculty of Engineering"
```

**Course(CourseID, CourseName, CreditHour, ProgramID)**

```
C201, "Programming Technique I",   3, P10
C202, "Programming Technique II",  3, P10
C203, "Database Systems",          3, P20
C301, "Circuit Theory",            4, P30
```

**Enrollment(StudentID, CourseID, Grade)**

```
S1001, C201, "A-"
S1001, C202, "A"
S1003, C201, "B+"
S1003, C202, "A-"
S1005, C202, "B"
S1002, C203, "A-"
S1004, C301, "B+"
```

## Part A — Core Operations

1. **Selection (σ)**
   Write a relational algebra expression to list **Johor** students with **CGPA ≥ 3.60**.

2. **Projection (π)**
   Return only **Name** and **CGPA** of all students.

3. **Union (∪)**
   Suppose `JohorStudents` and `SelangorStudents` are derived from `Student`.
   Write a union expression that lists **all students from Johor or Selangor** without duplicates.

4. **Set Difference (−)**
   Using `Enrollment`, list **students who have taken C202** but **not C201**.

5. **Cartesian Product (×) then Selection**
   Produce all **valid Lecturer–Course** pairs if we had `Lecturer(LecturerID, LecturerName, Faculty)` and wanted to **pair only lecturers in the same faculty as the course’s program**.
   (Write the general RA using symbols; you don’t need concrete tuples.)

6. **Rename (ρ)**
   Rename `Student` to `Pelajar` and attributes to **(ID, Nama, Jantina, Negeri, Program, Tahun, PNGK)**.

7. **Natural/Theta Join (⋈)**
   Join `Student` and `Program` to show each student with their **ProgramName** and **Faculty**.

8. **Join Chain**
   Retrieve **StudentID, Name, CourseName** for **all enrollments** (join `Student`, `Enrollment`, `Course`).

## Part B — Malaysia-Flavoured Analytics

9. **Top course among Johor female students**
   Using RA, return the **CourseName(s)** most frequently taken by **female students from Johor** in the sample data.

10. **Average CGPA by Faculty**
    Using RA + aggregation notation (γ), compute the **average CGPA** of students **grouped by Faculty** (via join to `Program`).
    *(If your course hasn’t covered extended algebra/aggregation, write the pipeline up to the grouped relation and describe the final step.)*

## Part C — UTM Case Study Task

**Goal:** Find **names of female students** from the **Faculty of Computing** who are **enrolled in “Programming Technique II.”**

1. Write the **relational algebra** pipeline.
2. Provide the **SQL equivalent**.
3. Using the sample tuples, **list the resulting names**.

## Bonus Challenges (for fast finishers)

B1) **Prerequisite check (set logic):**
Students who have **C202** must also have **C201**. Using RA, produce the set of **students violating** this rule.

B2) **Cross-faculty enrollment:**
List students whose **Program Faculty** is **different** from the **Faculty of the course** they took (via `Course.ProgramID → Program.Faculty`).



# Answer Key (Separate Sheet)

**A1)** σ_{State = 'Johor' ∧ CGPA ≥ 3.60}(Student)
→ S1001, S1003

**A2)** π_{Name, CGPA}(Student)

**A3)** JohorStudents ∪ SelangorStudents

**A4)**
Let A = π_{StudentID}(σ_{CourseID='C202'}(Enrollment))
Let B = π_{StudentID}(σ_{CourseID='C201'}(Enrollment))
Result = A − B → {S1005} (since S1005 has C202 but not C201)

**A5)**
Let valid pairs be those where **course’s program faculty = lecturer’s faculty**.
( (Lecturer × Course) ⋈_{Lecturer.Faculty = Program.Faculty} Program )
Then project Lecturer–Course: π_{LecturerID, CourseID}(…)

**A6)** ρ_{Pelajar(ID, Nama, Jantina, Negeri, Program, Tahun, PNGK)}(Student)

**A7)** Student ⋈_{Student.ProgramID = Program.ProgramID} Program
Project as needed: π_{StudentID, Name, ProgramName, Faculty}(…)

**A8)**
(Student ⋈_{Student.StudentID = Enrollment.StudentID} Enrollment) ⋈_{Enrollment.CourseID = Course.CourseID} Course
Project: π_{StudentID, Name, CourseName}(…)

**B9)**
Pipeline:

* JF ← σ_{State='Johor' ∧ Gender='F'}(Student)
* JFEnroll ← JF ⋈_{StudentID}(Enrollment)
* JFCourse ← JFEnroll ⋈_{CourseID}(Course)
* Count by course: γ_{CourseName; count(*)→cnt}(JFCourse)
  From data, Johor female students: S1001, S1003. Their courses: C201, C202 (both appear twice total).
  **Answer:** “Programming Technique I” and “Programming Technique II” tie.

**B10)**

* SP ← Student ⋈_{ProgramID}(Program)
* Γ ← γ_{Faculty; avg(CGPA)→avgCGPA}(SP)
  Computations:
  Faculty of Computing students: S1001 (3.82, P10), S1002 (3.10, P20), S1003 (3.67, P10) → avg = (3.82+3.10+3.67)/3 = **3.53**
  Faculty of Engineering: S1004 (3.45) → **3.45**
  (If you round: 3.53 and 3.45)

**C — UTM Case Study**

**C1) Relational Algebra**

* T1 ← Student ⋈_{ProgramID}(Program)
* T2 ← T1 ⋈_{StudentID}(Enrollment)
* T3 ← T2 ⋈_{CourseID}(Course)
* Result ← π_{Name}(σ_{Gender='F' ∧ Faculty='Faculty of Computing' ∧ CourseName='Programming Technique II'}(T3))

**C2) SQL**

```sql
SELECT DISTINCT S.Name
FROM Student S
JOIN Program P ON S.ProgramID = P.ProgramID
JOIN Enrollment E ON S.StudentID = E.StudentID
JOIN Course C ON E.CourseID = C.CourseID
WHERE S.Gender = 'F'
  AND P.Faculty = 'Faculty of Computing'
  AND C.CourseName = 'Programming Technique II';
```

**C3) Names from sample** → **Nur Aisyah**, **Tan Wei Ling**

**B1) Bonus – Prereq violators**

* HasC202 ← π_{StudentID}(σ_{CourseID='C202'}(Enrollment)) = {S1001, S1003, S1005}
* HasC201 ← π_{StudentID}(σ_{CourseID='C201'}(Enrollment)) = {S1001, S1003}
* Violators = HasC202 − HasC201 = **{S1005}**

**B2) Bonus – Cross-faculty**

* EC ← Enrollment ⋈ Course
* ECP ← EC ⋈_{Course.ProgramID = Program.ProgramID} Program as CP (course’s faculty)
* SP ← Student ⋈_{Student.ProgramID = Program.ProgramID} Program as PS (student’s faculty)
* Join on StudentID, compare PS.Faculty ≠ CP.Faculty, then project StudentID, Name, CourseName.
  From data:

  * S1004 in P30 (Engineering) took C301 (P30 → Engineering) → same faculty
  * S1002 in P20 (Computing) took C203 (P20 → Computing) → same
  * Others in P10 took P10 courses → same
    **Answer:** **No cross-faculty cases** in this sample.


## Contribution 🛠️
Please create an [Issue](https://github.com/drshahizan/HPDP/issues) for any improvements, suggestions or errors in the content.

You can also contact me using [Linkedin](https://www.linkedin.com/in/drshahizan/) for any other queries or feedback.

[![Visitors](https://api.visitorbadge.io/api/visitors?path=https%3A%2F%2Fgithub.com%2Fdrshahizan&labelColor=%23697689&countColor=%23555555&style=plastic)](https://visitorbadge.io/status?path=https%3A%2F%2Fgithub.com%2Fdrshahizan)
![](https://hit.yhype.me/github/profile?user_id=81284918)




