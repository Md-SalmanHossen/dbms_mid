
### **Relational Algebra Questions from Your Midterms**

#### **From Exam 222**【10†source】

1. Write relational algebra for the query:
    
    - Show `Student_ID`, `Student_Name`, and `Course_Name` for students whose `Student_ID` is greater or equal to 550, considering only courses from the "CSE" department.
2. Write the output relation for:
    
    ΠStudent_ID,Course_ID,Department(σCourse_ID>1151(Course×Students))\Pi_{Student\_ID, Course\_ID, Department}(\sigma_{Course\_ID > 1151} (Course \times Students))

---

#### **From Exam 223**【11†source】

1. Write relational algebra for the query:
    
    - Show all book information except the year of publication along with the publisher name where the publisher has a specific location and ID is greater than 50.
2. Write the output relation for:
    
    ΠPublisher_ID,Book_Name,Year((σYear<2000(Book))×(σLocation=′Chittagong′(Publisher)))\Pi_{Publisher\_ID, Book\_Name, Year}((\sigma_{Year < 2000}(Book)) \times (\sigma_{Location = 'Chittagong'}(Publisher)))

---

#### **From Exam 231**【12†source**

1. Using the schema:
    - **Players(Player_ID, Name, Team_ID, Age, Matches_Played)**
    - **Teams(Team_ID, Name, Country, Trophy_Count)**  
        Write relational algebra for:
    - Find names of players who are older than 25 years and play for teams with more than 5 trophies.

---

#### **From Exam 232**【30†source**

1. Using the schema:
    - **Employees(Emp_ID, Name, Age, Salary, Dept_ID)**
    - **Departments(Dept_ID, Name, Location)**  
        Write relational algebra for:
    - Retrieve names of employees whose salaries exceed the average salary in their respective departments.

---

#### **From Exam 233**【31†source】

1. Using the schema:
    - **Matches(Match_ID, Date, Team_A, Team_B, Result)**
    - **Teams(Team_ID, Name, Country)**  
        Write relational algebra for:
    - Retrieve the dates of all matches where "Team Australia" was involved.

---

#### **From Exam 241**【32†source】

1. Write relational algebra to:
    - Find all passengers who have traveled on trips costing more than 5,000 TK.

---

---

### **Solutions to Midterm Relational Algebra Questions**

#### **Exam 222**

1. **Query**:
    
    ΠStudent_ID,Student_Name,Course_Name(σStudent_ID≥550∧Department=′CSE′(Students⋈Courses))\Pi_{Student\_ID, Student\_Name, Course\_Name}(\sigma_{Student\_ID \geq 550 \wedge Department = 'CSE'}(Students \bowtie Courses))
2. **Output Relation**: The projection will display:
    
    - `Student_ID`, `Course_ID`, and `Department` from the Cartesian product of `Students` and `Courses` where `Course_ID > 1151`.

---

#### **Exam 223**

1. **Query**:
    
    ΠBook_Name,Publisher_Name(σPublisher_ID>50∧Location=′SpecificLocation′(Books⋈Publishers))\Pi_{Book\_Name, Publisher\_Name}(\sigma_{Publisher\_ID > 50 \wedge Location = 'SpecificLocation'}(Books \bowtie Publishers))
2. **Output Relation**: Displays:
    
    - `Publisher_ID`, `Book_Name`, and `Year` for books published before 2000 by publishers located in "Chittagong."

---

#### **Exam 231**

1. **Players older than 25 in teams with more than 5 trophies**: ΠName(σAge>25∧Trophy_Count>5(Players⋈Teams))\Pi_{Name}(\sigma_{Age > 25 \wedge Trophy\_Count > 5}(Players \bowtie Teams))

---

#### **Exam 232**

1. **Employees earning above their department average**: ΠName(σSalary>AVG(Salary)(Employees⋈Departments))\Pi_{Name}(\sigma_{Salary > AVG(Salary)}(Employees \bowtie Departments))

---

#### **Exam 233**

1. **Dates of matches involving "Team Australia"**: ΠDate(σTeam_A=′TeamAustralia′∨Team_B=′TeamAustralia′(Matches))\Pi_{Date}(\sigma_{Team\_A = 'Team Australia' \vee Team\_B = 'Team Australia'}(Matches))

---

#### **Exam 241**

1. **Passengers on trips costing more than 5,000 TK**: ΠPassenger_Name(σCost>5000(Trips))\Pi_{Passenger\_Name}(\sigma_{Cost > 5000}(Trips))

---

---

### **Additional Practice Questions**

#### **Question 1: Basic Selection and Projection**

Given:

- **Students(Student_ID, Name, Major, Age)**
- **Enrollments(Student_ID, Course_ID, Semester, Grade)**  
    Write relational algebra to:

1. Retrieve the names of students enrolled in the "Fall 2023" semester.
2. Find the names and majors of students who are older than 21.

---

#### **Question 2: Join and Aggregation**

Given:

- **Employees(Emp_ID, Name, Salary, Dept_ID)**
- **Departments(Dept_ID, Dept_Name, Location)**  
    Write relational algebra to:

1. Retrieve names of employees working in the "HR" department.
2. Find the department name and the total salary of employees in each department.

---

#### **Question 3: Complex Filtering**

Given:

- **Orders(Order_ID, Customer_ID, Product_ID, Order_Date, Quantity)**
- **Products(Product_ID, Name, Price, Category)**  
    Write relational algebra to:

1. Retrieve the names of products ordered more than 50 times.
2. Find the categories of products generating total revenue above 10,000.

---

### **Solutions to Additional Practice**

#### **Question 1 Solutions**

1. Students enrolled in "Fall 2023":
    
    ΠName(σSemester=′Fall2023′(Students⋈Enrollments))\Pi_{Name}(\sigma_{Semester = 'Fall 2023'}(Students \bowtie Enrollments))
2. Students older than 21:
    
    ΠName,Major(σAge>21(Students))\Pi_{Name, Major}(\sigma_{Age > 21}(Students))

---

#### **Question 2 Solutions**

1. Employees in "HR":
    
    ΠName(σDept_Name=′HR′(Employees⋈Departments))\Pi_{Name}(\sigma_{Dept\_Name = 'HR'}(Employees \bowtie Departments))
2. Total salary per department:
    
    ΠDept_Name,ΣSalary(Employees⋈Departments)\Pi_{Dept\_Name, \Sigma Salary}(Employees \bowtie Departments)

---

#### **Question 3 Solutions**

1. Products ordered more than 50 times:
    
    ΠProduct_Name(σCOUNT(Quantity)>50(Orders⋈Products))\Pi_{Product\_Name}(\sigma_{COUNT(Quantity) > 50}(Orders \bowtie Products))
2. Categories generating revenue above 10,000:
    
    ΠCategory(σSUM(Price×Quantity)>10000(Orders⋈Products))\Pi_{Category}(\sigma_{SUM(Price \times Quantity) > 10000}(Orders \bowtie Products))

---
