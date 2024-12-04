Your SQL queries are well-structured and cover the requirements effectively. However, I noticed some inconsistencies in the markdown syntax and query formatting, which could confuse the reader. Here's a refined version of your document with proper formatting and consistent styling for SQL code blocks and headings:

---

### _Task 3: Queries_

Below are the SQL queries for each part of _Task 3_, based on the requirements in the assignment. Queries include subqueries and other techniques as specified.

---

#### _(a)_ Find the names of all departments with instructors, removing duplicates.

```sql
SELECT DISTINCT d.dept_name
FROM department d
JOIN instructor i ON d.dept_name = i.dept_name;
```

---

#### _(b)_ Find the names of all instructors in the History department.

```sql
SELECT name
FROM instructor
WHERE dept_name = 'History';
```

---

#### _(c)_ Find the instructor_ID and department_name of all instructors associated with a department with a budget greater than $95,000.

```sql
SELECT i.ID, i.dept_name
FROM instructor i
JOIN department d ON i.dept_name = d.dept_name
WHERE d.budget > 95000;
```

---

#### _(d)_ Find all instructors in the Computer Science department with salaries more than $80,000.

```sql
SELECT name
FROM instructor
WHERE dept_name = 'Computer Science' AND salary > 80000;
```

---

#### _(e)_ List the names of instructors along with the titles of courses that they teach.

```sql
SELECT i.name, c.title
FROM instructor i
JOIN teaches t ON i.ID = t.ID
JOIN course c ON t.course_id = c.course_id;
```

---

#### _(f)_ Find the names of all instructors who have a higher salary than some instructors in the Computer Science department.

```sql
SELECT DISTINCT i1.name
FROM instructor i1
WHERE i1.salary > ANY (
    SELECT i2.salary
    FROM instructor i2
    WHERE i2.dept_name = 'Computer Science'
);
```

---

#### _(g)_ Find the names of all instructors whose salary is greater than at least one instructor in the Biology department.

```sql
SELECT DISTINCT i1.name
FROM instructor i1
WHERE i1.salary > ANY (
    SELECT i2.salary
    FROM instructor i2
    WHERE i2.dept_name = 'Biology'
);
```

---

#### _(h)_ Find the names of all departments whose building name includes the substring Watson.

```sql
SELECT dept_name
FROM department
WHERE building LIKE '%Watson%';
```

---

#### _(i)_ List in alphabetical order the names of all instructors.

```sql
SELECT name
FROM instructor
ORDER BY name;
```

---

#### _(j)_ Find the names of instructors with salary amounts between $90,000 and $100,000.

```sql
SELECT name
FROM instructor
WHERE salary BETWEEN 90000 AND 100000;
```

---

#### _(k)_ Find the instructor names and the courses they taught for all instructors in the Biology department who have taught some course.

```sql
SELECT i.name, c.title
FROM instructor i
JOIN teaches t ON i.ID = t.ID
JOIN course c ON t.course_id = c.course_id
WHERE i.dept_name = 'Biology';
```

---

#### _(l)_ Find the set of all courses taught either in Fall 2009 or in Spring 2010, or both.

```sql
SELECT DISTINCT course_id
FROM section
WHERE (semester = 'Fall' AND year = 2009)
   OR (semester = 'Spring' AND year = 2010);
```

---

#### _(m)_ Find the set of all courses taught in Fall 2009 as well as in Spring 2010.

```sql
SELECT course_id
FROM section
WHERE semester = 'Fall' AND year = 2009
INTERSECT
SELECT course_id
FROM section
WHERE semester = 'Spring' AND year = 2010;
```

---

#### _(n)_ Find all courses taught in Fall 2009 but not in Spring 2010.

```sql
SELECT course_id
FROM section
WHERE semester = 'Fall' AND year = 2009
EXCEPT
SELECT course_id
FROM section
WHERE semester = 'Spring' AND year = 2010;
```

---

#### _(o)_ Find all instructors whose salary is null.

```sql
SELECT name
FROM instructor
WHERE salary IS NULL;
```

---

#### _(p)_ Find courses offered in Fall 2009 and in Spring 2010 Semester.

```sql
SELECT course_id
FROM section
WHERE (semester = 'Fall' AND year = 2009)
   OR (semester = 'Spring' AND year = 2010);
```

---

#### _(q)_ Find courses offered in Fall 2009 but not in Spring 2010.

```sql
SELECT course_id
FROM section
WHERE semester = 'Fall' AND year = 2009
AND course_id NOT IN (
    SELECT course_id
    FROM section
    WHERE semester = 'Spring' AND year = 2010
);
```

---

#### _(r)_ Find the total number of (distinct) students who have taken course sections taught by the instructor with ID 10101.

```sql
SELECT COUNT(DISTINCT t.ID)
FROM takes t
JOIN teaches ts ON t.course_id = ts.course_id AND t.sec_id = ts.sec_id
WHERE ts.ID = 10101;
```

---

#### _(s)_ Find the names of instructors with salaries greater than that of some (at least one) instructor in the Biology department.

```sql
SELECT DISTINCT i1.name
FROM instructor i1
WHERE i1.salary > ANY (
    SELECT i2.salary
    FROM instructor i2
    WHERE i2.dept_name = 'Biology'
);
```

---

#### _(t)_ Find the names of all instructors whose salary is greater than the salary of all instructors in the Biology department.

```sql
SELECT DISTINCT i1.name
FROM instructor i1
WHERE i1.salary > ALL (
    SELECT i2.salary
    FROM instructor i2
    WHERE i2.dept_name = 'Biology'
);
```

---

#### _(u)_ Find all courses taught in both the Fall 2009 semester and the Spring 2010 semester.

```sql
SELECT course_id
FROM section
WHERE semester = 'Fall' AND year = 2009
INTERSECT
SELECT course_id
FROM section
WHERE semester = 'Spring' AND year = 2010;
```

---

#### _(v)_ Find all students who have taken all courses offered in the Biology department.

```sql
SELECT s.ID
FROM student s
WHERE NOT EXISTS (
    SELECT c.course_id
    FROM course c
    WHERE c.dept_name = 'Biology'
    AND c.course_id NOT IN (
        SELECT t.course_id
        FROM takes t
        WHERE t.ID = s.ID
    )
);
```

---

#### _(w)_ Find all courses that were offered at most once in 2009.

```sql
SELECT course_id
FROM section
WHERE year = 2009
GROUP BY course_id
HAVING COUNT(*) <= 1;
```

---

Would you like additional comments, further optimizations, or adjustments?