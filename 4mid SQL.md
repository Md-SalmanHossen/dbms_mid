

---

### **SQL Questions from Your Midterms**

#### **From Exam 222**

1. Write the SQL query:
    - Show `Student_ID`, `Student_Name`, and `Course_Name` for students whose `Student_ID` is greater or equal to 550, considering only courses from the "CSE" department.

---

#### **From Exam 231**

1. Retrieve the `Player_Name` and `Team_Name` for players above the age of 25.
2. Find the name of the player who has won the maximum number of "Player of the Match" awards.
3. Calculate the average rating of players from the top 5 teams based on `Trophy_Count`.

---

#### **From Exam 232**

1. Change the primary key of the `Orders` table to include `Order_ID`, `Customer_ID`, and `Project_ID`.
2. Find project names where the duration is not more than a year.
3. List employee names whose ages are less than the average age of all employees in their department.

---

#### **From Exam 233**

1. Retrieve the first and last names of players who participated in matches against "Team England."
2. List the total runs scored by each player in matches where they scored more than 50 runs.
3. Find the match details where players from "Team Australia" took more than 5 wickets.

---

#### **From Exam 241**

1. Retrieve titles of all books along with the first and last names of their authors.
2. Calculate the total sales generated from each genre, sorted by revenue.
3. Identify customers who purchased books from more than one genre.

---

### **Solutions to Midterm SQL Questions**

#### **Exam 222**

1. **SQL Query**:
    
    ```sql
    SELECT Student_ID, Student_Name, Course_Name
    FROM Students S
    JOIN Courses C ON S.Student_ID = C.Student_ID
    WHERE S.Student_ID >= 550 AND C.Department = 'CSE';
    ```
    

---

#### **Exam 231**

1. **Players above 25**:
    
    ```sql
    SELECT Player_Name, Team_Name
    FROM Players P
    JOIN Teams T ON P.Team_ID = T.Team_ID
    WHERE P.Age > 25;
    ```
    
2. **Player with most "Man of the Match" awards**:
    
    ```sql
    SELECT Player_Name
    FROM Players P
    JOIN PlayerPerformance PP ON P.Player_ID = PP.Player_ID
    GROUP BY P.Player_ID, Player_Name
    ORDER BY COUNT(PP.ManOfTheMatch) DESC
    LIMIT 1;
    ```
    
3. **Average rating of players from top 5 teams**:
    
    ```sql
    SELECT AVG(PP.Rating) AS AvgRating
    FROM Players P
    JOIN Teams T ON P.Team_ID = T.Team_ID
    JOIN PlayerPerformance PP ON P.Player_ID = PP.Player_ID
    WHERE T.Team_ID IN (
        SELECT Team_ID
        FROM Teams
        ORDER BY T.Trophy_Count DESC
        LIMIT 5
    );
    ```
    

---

#### **Exam 232**

1. **Change primary key**:
    
    ```sql
    ALTER TABLE Orders
    DROP PRIMARY KEY,
    ADD PRIMARY KEY (Order_ID, Customer_ID, Project_ID);
    ```
    
2. **Projects lasting less than a year**:
    
    ```sql
    SELECT Project_Name
    FROM Projects
    WHERE DATEDIFF(End_Date, Start_Date) <= 365;
    ```
    
3. **Employees below average age in their department**:
    
    ```sql
    SELECT Name
    FROM Employees E
    WHERE E.Age < (
        SELECT AVG(E2.Age)
        FROM Employees E2
        WHERE E2.Department_ID = E.Department_ID
    );
    ```
    

---

#### **Exam 233**

1. **Players against "Team England"**:
    
    ```sql
    SELECT P.FirstName, P.LastName
    FROM Players P
    JOIN Matches M ON P.Player_ID = M.Player_ID
    WHERE M.Opposing_Team = 'Team England';
    ```
    
2. **Players scoring more than 50 runs**:
    
    ```sql
    SELECT Player_Name, SUM(RunsScored) AS TotalRuns
    FROM PlayerPerformance
    WHERE RunsScored > 50
    GROUP BY Player_Name
    ORDER BY TotalRuns DESC;
    ```
    
3. **Matches where "Team Australia" players took more than 5 wickets**:
    
    ```sql
    SELECT M.Date, M.Venue, M.Result, P.Player_Name, PP.WicketsTaken
    FROM Matches M
    JOIN PlayerPerformance PP ON M.Match_ID = PP.Match_ID
    JOIN Players P ON PP.Player_ID = P.Player_ID
    WHERE M.Team = 'Team Australia' AND PP.WicketsTaken > 5;
    ```
    

---

#### **Exam 241**

1. **Books and their authors**:
    
    ```sql
    SELECT B.Title, A.FirstName, A.LastName
    FROM Books B
    JOIN Authors A ON B.Author_ID = A.Author_ID;
    ```
    
2. **Total sales by genre**:
    
    ```sql
    SELECT B.Genre, SUM(O.Total_Amount) AS TotalSales
    FROM Books B
    JOIN Orders O ON B.Book_ID = O.Book_ID
    GROUP BY B.Genre
    ORDER BY TotalSales DESC;
    ```
    
3. **Customers buying from more than one genre**:
    
    ```sql
    SELECT C.FirstName, C.LastName, COUNT(DISTINCT B.Genre) AS GenreCount
    FROM Customers C
    JOIN Orders O ON C.Customer_ID = O.Customer_ID
    JOIN Books B ON O.Book_ID = B.Book_ID
    GROUP BY C.Customer_ID
    HAVING GenreCount > 1;
    ```
    

---
