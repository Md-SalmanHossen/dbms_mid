Here’s how you can solve the provided SQL queries:

---

### **First Schema Queries:**

#### Schema:

- **Player** (id, name, position, ranking, tourn_id, age, trophy_count)
- **Tennis** (id, name, ranking, trophy_count)
- **Coach** (id, name, nationality, year_of_experience, trophy_count, ranking)
- **Match** (id, home_team, away_team, h_score, a_score, day, month, year, result, POTM)
- **Match Details** (id, mid, rating, goal, assist, key_pass, tackle_won, saves)

#### Queries:

1. **Find the player name for all the players above 25:**
    
    ```sql
    SELECT name 
    FROM Player 
    WHERE age > 25;
    ```
    
2. **Find the player name with the maximum number of POTM awards:**
    
    ```sql
    SELECT Player.name 
    FROM Player 
    INNER JOIN Match ON Player.id = Match.POTM 
    GROUP BY Player.name 
    ORDER BY COUNT(Match.POTM) DESC 
    LIMIT 1;
    ```
    
3. **Find the name and trophy count of players from the top 5 teams by ranking:**
    
    ```sql
    SELECT Player.name, Player.trophy_count 
    FROM Player 
    WHERE tourn_id IN (
        SELECT id 
        FROM Tennis 
        ORDER BY ranking ASC 
        LIMIT 5
    );
    ```
    
4. **Find coach name and total goals scored in the last 10 home matches with result = 'win' only if the coach's name is at least 5 characters long:**
    
    ```sql
    SELECT Coach.name, SUM(Match.h_score) AS total_goals 
    FROM Coach 
    INNER JOIN Match ON Coach.id = Match.home_team 
    WHERE CHAR_LENGTH(Coach.name) >= 5 
      AND Match.result = 'win' 
    ORDER BY Match.year DESC, Match.month DESC, Match.day DESC 
    LIMIT 10;
    ```
    

---

### **Second Schema Queries:**

#### Schema:

- **Employees** (employee_id, name, age, department_id)
- **Departments** (department_id, name, location)
- **Projects** (project_id, name, start_date, end_date)
- **Assignments** (assignment_id, employee_id, project_id)
- **Customers** (customer_id, name, address, phone)
- **Orders** (order_id, customer_id, project_id, order_date)

#### Queries:

1. **Change the primary key of the orders table to a composite key (order_id, customer_id, project_id):**
    
    ```sql
    ALTER TABLE Orders 
    DROP PRIMARY KEY, 
    ADD PRIMARY KEY (order_id, customer_id, project_id);
    ```
    
2. **Find the project names where the duration of the project is not more than a year:**
    
    ```sql
    SELECT name 
    FROM Projects 
    WHERE DATEDIFF(end_date, start_date) <= 365;
    ```
    
3. **Find the employee names of those employees whose age is less than the average age of all employees in their department:**
    
    ```sql
    SELECT Employees.name 
    FROM Employees 
    WHERE age < (
        SELECT AVG(age) 
        FROM Employees AS e 
        WHERE e.department_id = Employees.department_id
    );
    ```
    
4. **Find the name and address of each customer who has placed a project order, and the project name starts with a vowel or does not end with 'ca':**
    
    ```sql
    SELECT DISTINCT Customers.name, Customers.address 
    FROM Customers 
    INNER JOIN Orders ON Customers.customer_id = Orders.customer_id 
    INNER JOIN Projects ON Orders.project_id = Projects.project_id 
    WHERE (Projects.name REGEXP '^[AEIOUaeiou]') 
       OR (Projects.name NOT LIKE '%ca');
    ```
    

---

Let me know if you need further clarifications!