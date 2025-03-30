# Library Management System using SQL 

## Project Overview

**Project Title**: Library Management System  
**Database**: `Library_Project`

This project demonstrates the implementation of a Library Management System using SQL. It includes creating and managing tables, performing CRUD operations, and executing advanced SQL queries. The goal is to showcase skills in database design, manipulation, and querying.

## Objectives

1. **Set up the Library Management System Database**: Create and populate the database with tables for branches, employees, members, books, issued status, and return status.
2. **CRUD Operations**: Perform Create, Read, Update, and Delete operations on the data.
3. **CTAS (Create Table As Select)**: Utilize CTAS to create new tables based on query results.
4. **Advanced SQL Queries**: Develop complex queries to analyse and retrieve specific data.

## Project Structure

### 1. Database Setup

- **Database Creation**: Created a database named `library_Project`.
- **Table Creation**: Created tables for branches, employees, members, books, issued status, and return status. Each table includes relevant columns and relationships.

```sql
---Create table “Branch”
CREATE TABLE Branch(
Branch_ID VARCHAR(10) PRIMARY KEY,
Manager_ID VARCHAR(10),
Branch_address VARCHAR(20),
Contact_No VARCHAR(15)
);
-- Insert values into branch table
INSERT INTO Branch(Branch_ID, Manager_ID, Branch_address, Contact_No) 
VALUES
('B001', 'E109', '123 Main St', '+919099988676'),
('B002', 'E109', '456 Elm St', '+919099988677'),
('B003', 'E109', '789 Oak St', '+919099988678'),
('B004', 'E110', '567 Pine St', '+919099988679'),
('B005', 'E110', '890 Maple St', '+919099988680');
SELECT * FROM Branch;

-- Create table "Employee"
            
CREATE TABLE Employee(
Emp_ID VARCHAR(10) PRIMARY KEY,
Emp_name  VARCHAR(20),
Emp_Position VARCHAR(20),
Salary INT,
Branch_ID VARCHAR(10),
FOREIGN KEY(Branch_ID) REFERENCES Branch(Branch_ID) ON DELETE CASCADE
);
-- Insert values into each employees table
INSERT INTO Employee(Emp_ID, Emp_name , Emp_Position, Salary, Branch_ID) 
VALUES
('E101', 'John Doe', 'Clerk', 60000.00, 'B001'),
('E102', 'Jane Smith', 'Clerk', 45000.00, 'B002'),
('E103', 'Mike Johnson', 'Librarian', 55000.00, 'B001'),
('E104', 'Emily Davis', 'Assistant', 40000.00, 'B001'),
('E105', 'Sarah Brown', 'Assistant', 42000.00, 'B001'),
('E106', 'Michelle Ramirez', 'Assistant', 43000.00, 'B001'),
('E107', 'Michael Thompson', 'Clerk', 62000.00, 'B005'),
('E108', 'Jessica Taylor', 'Clerk', 46000.00, 'B004'),
('E109', 'Daniel Anderson', 'Manager', 57000.00, 'B003'),
('E110', 'Laura Martinez', 'Manager', 41000.00, 'B005'),
('E111', 'Christopher Lee', 'Assistant', 65000.00, 'B005');
SELECT * FROM Employee;

-- Create table "Members"

CREATE TABLE Members(
Member_ID VARCHAR(10) PRIMARY KEY,
Member_Name VARCHAR(20),
Member_address VARCHAR(30),
Reg_Date DATE
);
-- Insert values into each Members table
INSERT INTO Members(Member_ID, Member_Name, Member_address, Reg_Date) 
VALUES
('C101', 'Alice Johnson', '123 Main St', '2021-05-15'),
('C102', 'Bob Smith', '456 Elm St', '2021-06-20'),
('C103', 'Carol Davis', '789 Oak St', '2021-07-10'),
('C104', 'Dave Wilson', '567 Pine St', '2021-08-05'),
('C105', 'Eve Brown', '890 Maple St', '2021-09-25'),
('C106', 'Frank Thomas', '234 Cedar St', '2021-10-15'),
('C107', 'Grace Taylor', '345 Walnut St', '2021-11-20'),
('C108', 'Henry Anderson', '456 Birch St', '2021-12-10'),
('C109', 'Ivy Martinez', '567 Oak St', '2022-01-05'),
('C110', 'Jack Wilson', '678 Pine St', '2022-02-25'),
('C118', 'Sam', '133 Pine St', '2024-06-01'),    
('C119', 'John', '143 Main St', '2024-05-01');
SELECT * FROM Members;


-- Create table "Books"

CREATE TABLE Books(
ISBN VARCHAR(30) PRIMARY KEY,
Book_Title VARCHAR(70),
Category VARCHAR(25),
Rental_Price FLOAT,
Rental_Status VARCHAR(30),
Author VARCHAR(30),
Publisher VARCHAR(35)
);
-- Inserting into books table 
INSERT INTO Books(ISBN, Book_Title, Category, Rental_Price, Rental_Status, Author, Publisher) 
VALUES
('978-0-553-29698-2', 'The Catcher in the Rye', 'Classic', 7.00, 'yes', 'J.D. Salinger', 'Little, Brown and Company'),
('978-0-330-25864-8', 'Animal Farm', 'Classic', 5.50, 'yes', 'George Orwell', 'Penguin Books'),
('978-0-14-118776-1', 'One Hundred Years of Solitude', 'Literary Fiction', 6.50, 'yes', 'Gabriel Garcia Marquez', 'Penguin Books'),
('978-0-525-47535-5', 'The Great Gatsby', 'Classic', 8.00, 'yes', 'F. Scott Fitzgerald', 'Scribner'),
('978-0-141-44171-6', 'Jane Eyre', 'Classic', 4.00, 'yes', 'Charlotte Bronte', 'Penguin Classics'),
('978-0-307-37840-1', 'The Alchemist', 'Fiction', 2.50, 'yes', 'Paulo Coelho', 'HarperOne'),
('978-0-679-76489-8', 'Harry Potter and the Sorcerers Stone', 'Fantasy', 7.00, 'yes', 'J.K. Rowling', 'Scholastic'),
('978-0-7432-4722-4', 'The Da Vinci Code', 'Mystery', 8.00, 'yes', 'Dan Brown', 'Doubleday'),
('978-0-09-957807-9', 'A Game of Thrones', 'Fantasy', 7.50, 'yes', 'George R.R. Martin', 'Bantam'),
('978-0-393-05081-8', 'A Peoples History of the United States', 'History', 9.00, 'yes', 'Howard Zinn', 'Harper Perennial'),
('978-0-19-280551-1', 'The Guns of August', 'History', 7.00, 'yes', 'Barbara W. Tuchman', 'Oxford University Press'),
('978-0-307-58837-1', 'Sapiens: A Brief History of Humankind', 'History', 8.00, 'no', 'Yuval Noah Harari', 'Harper Perennial'),
('978-0-375-41398-8', 'The Diary of a Young Girl', 'History', 6.50, 'no', 'Anne Frank', 'Bantam'),
('978-0-14-044930-3', 'The Histories', 'History', 5.50, 'yes', 'Herodotus', 'Penguin Classics'),
('978-0-393-91257-8', 'Guns, Germs, and Steel: The Fates of Human Societies', 'History', 7.00, 'yes', 'Jared Diamond', 'W. W. Norton & Company'),
('978-0-7432-7357-1', '1491: New Revelations of the Americas Before Columbus', 'History', 6.50, 'no', 'Charles C. Mann', 'Vintage Books'),
('978-0-679-64115-3', '1984', 'Dystopian', 6.50, 'yes', 'George Orwell', 'Penguin Books'),
('978-0-14-143951-8', 'Pride and Prejudice', 'Classic', 5.00, 'yes', 'Jane Austen', 'Penguin Classics'),
('978-0-452-28240-7', 'Brave New World', 'Dystopian', 6.50, 'yes', 'Aldous Huxley', 'Harper Perennial'),
('978-0-670-81302-4', 'The Road', 'Dystopian', 7.00, 'yes', 'Cormac McCarthy', 'Knopf'),
('978-0-385-33312-0', 'The Shining', 'Horror', 6.00, 'yes', 'Stephen King', 'Doubleday'),
('978-0-451-52993-5', 'Fahrenheit 451', 'Dystopian', 5.50, 'yes', 'Ray Bradbury', 'Ballantine Books'),
('978-0-345-39180-3', 'Dune', 'Science Fiction', 8.50, 'yes', 'Frank Herbert', 'Ace'),
('978-0-375-50167-0', 'The Road', 'Dystopian', 7.00, 'yes', 'Cormac McCarthy', 'Vintage'),
('978-0-06-025492-6', 'Where the Wild Things Are', 'Children', 3.50, 'yes', 'Maurice Sendak', 'HarperCollins'),
('978-0-06-112241-5', 'The Kite Runner', 'Fiction', 5.50, 'yes', 'Khaled Hosseini', 'Riverhead Books'),
('978-0-06-440055-8', 'Charlotte''s Web', 'Children', 4.00, 'yes', 'E.B. White', 'Harper & Row'),
('978-0-679-77644-3', 'Beloved', 'Fiction', 6.50, 'yes', 'Toni Morrison', 'Knopf'),
('978-0-14-027526-3', 'A Tale of Two Cities', 'Classic', 4.50, 'yes', 'Charles Dickens', 'Penguin Books'),
('978-0-7434-7679-3', 'The Stand', 'Horror', 7.00, 'yes', 'Stephen King', 'Doubleday'),
('978-0-451-52994-2', 'Moby Dick', 'Classic', 6.50, 'yes', 'Herman Melville', 'Penguin Books'),
('978-0-06-112008-4', 'To Kill a Mockingbird', 'Classic', 5.00, 'yes', 'Harper Lee', 'J.B. Lippincott & Co.'),
('978-0-553-57340-1', '1984', 'Dystopian', 6.50, 'yes', 'George Orwell', 'Penguin Books'),
('978-0-7432-4722-5', 'Angels & Demons', 'Mystery', 7.50, 'yes', 'Dan Brown', 'Doubleday'),
('978-0-7432-7356-4', 'The Hobbit', 'Fantasy', 7.00, 'yes', 'J.R.R. Tolkien', 'Houghton Mifflin Harcourt');
SELECT * FROM Books;


-- Create table "Issued_Status"

CREATE TABLE Issued_Status(
Issue_ID VARCHAR(10) PRIMARY KEY,
Issued_Member_ID VARCHAR(10), 
Issued_Book_Name VARCHAR(70),
Issued_Date DATE,
Issued_Book_ISBN VARCHAR(50), 
Issued_Empl_ID VARCHAR(10),
FOREIGN KEY(Issued_Member_ID) REFERENCES Members(Member_ID) ON DELETE SET NULL,
FOREIGN KEY(Issued_Empl_ID) REFERENCES Employee(Emp_ID) ON DELETE  SET NULL,
FOREIGN KEY(Issued_Book_ISBN) REFERENCES Books(ISBN) ON DELETE  SET NULL
);
-- inserting into issued table
INSERT INTO Issued_status(Issue_ID, Issued_Member_ID, Issued_Book_Name, Issued_Date, Issued_Book_ISBN, Issued_Empl_ID) 
VALUES
('IS106', 'C106', 'Animal Farm', '2024-03-10', '978-0-330-25864-8', 'E104'),
('IS107', 'C107', 'One Hundred Years of Solitude', '2024-03-11', '978-0-14-118776-1', 'E104'),
('IS108', 'C108', 'The Great Gatsby', '2024-03-12', '978-0-525-47535-5', 'E104'),
('IS109', 'C109', 'Jane Eyre', '2024-03-13', '978-0-141-44171-6', 'E105'),
('IS110', 'C110', 'The Alchemist', '2024-03-14', '978-0-307-37840-1', 'E105'),
('IS111', 'C109', 'Harry Potter and the Sorcerers Stone', '2024-03-15', '978-0-679-76489-8', 'E105'),
('IS112', 'C109', 'A Game of Thrones', '2024-03-16', '978-0-09-957807-9', 'E106'),
('IS113', 'C109', 'A Peoples History of the United States', '2024-03-17', '978-0-393-05081-8', 'E106'),
('IS114', 'C109', 'The Guns of August', '2024-03-18', '978-0-19-280551-1', 'E106'),
('IS115', 'C109', 'The Histories', '2024-03-19', '978-0-14-044930-3', 'E107'),
('IS116', 'C110', 'Guns, Germs, and Steel: The Fates of Human Societies', '2024-03-20', '978-0-393-91257-8', 'E107'),
('IS117', 'C110', '1984', '2024-03-21', '978-0-679-64115-3', 'E107'),
('IS118', 'C101', 'Pride and Prejudice', '2024-03-22', '978-0-14-143951-8', 'E108'),
('IS119', 'C110', 'Brave New World', '2024-03-23', '978-0-452-28240-7', 'E108'),
('IS120', 'C110', 'The Road', '2024-03-24', '978-0-670-81302-4', 'E108'),
('IS121', 'C102', 'The Shining', '2024-03-25', '978-0-385-33312-0', 'E109'),
('IS122', 'C102', 'Fahrenheit 451', '2024-03-26', '978-0-451-52993-5', 'E109'),
('IS123', 'C103', 'Dune', '2024-03-27', '978-0-345-39180-3', 'E109'),
('IS124', 'C104', 'Where the Wild Things Are', '2024-03-28', '978-0-06-025492-6', 'E110'),
('IS125', 'C105', 'The Kite Runner', '2024-03-29', '978-0-06-112241-5', 'E110'),
('IS126', 'C105', 'Charlotte''s Web', '2024-03-30', '978-0-06-440055-8', 'E110'),
('IS127', 'C105', 'Beloved', '2024-03-31', '978-0-679-77644-3', 'E110'),
('IS128', 'C105', 'A Tale of Two Cities', '2024-04-01', '978-0-14-027526-3', 'E110'),
('IS129', 'C105', 'The Stand', '2024-04-02', '978-0-7434-7679-3', 'E110'),
('IS130', 'C106', 'Moby Dick', '2024-04-03', '978-0-451-52994-2', 'E101'),
('IS131', 'C106', 'To Kill a Mockingbird', '2024-04-04', '978-0-06-112008-4', 'E101'),
('IS132', 'C106', 'The Hobbit', '2024-04-05', '978-0-7432-7356-4', 'E106'),
('IS133', 'C107', 'Angels & Demons', '2024-04-06', '978-0-7432-4722-5', 'E106'),
('IS134', 'C107', 'The Diary of a Young Girl', '2024-04-07', '978-0-375-41398-8', 'E106'),
('IS135', 'C107', 'Sapiens: A Brief History of Humankind', '2024-04-08', '978-0-307-58837-1', 'E108'),
('IS136', 'C107', '1491: New Revelations of the Americas Before Columbus', '2024-04-09', '978-0-7432-7357-1', 'E102'),
('IS137', 'C107', 'The Catcher in the Rye', '2024-04-10', '978-0-553-29698-2', 'E103'),
('IS138', 'C108', 'The Great Gatsby', '2024-04-11', '978-0-525-47535-5', 'E104'),
('IS139', 'C109', 'Harry Potter and the Sorcerers Stone', '2024-04-12', '978-0-679-76489-8', 'E105'),
('IS140', 'C110', 'Animal Farm', '2024-04-13', '978-0-330-25864-8', 'E102');
SELECT * FROM Issued_Status;

-- Create table "Return_Status"

CREATE TABLE Return_Status(
Return_ID VARCHAR(10) PRIMARY KEY,
Issued_ID VARCHAR(10), 
Return_Book_Name VARCHAR(70),
Return_Date DATE,
Return_Book_ISBN VARCHAR(20),
FOREIGN KEY(Return_Book_ISBN) REFERENCES Books(ISBN) ON DELETE CASCADE
);
-- inserting into return table
INSERT INTO Return_Status(Return_ID, Issued_ID, Return_Date) 
VALUES
('RS101', 'IS101', '2023-06-06'),
('RS102', 'IS105', '2023-06-07'),
('RS103', 'IS103', '2023-08-07'),
('RS104', 'IS106', '2024-05-01'),
('RS105', 'IS107', '2024-05-03'),
('RS106', 'IS108', '2024-05-05'),
('RS107', 'IS109', '2024-05-07'),
('RS108', 'IS110', '2024-05-09'),
('RS109', 'IS111', '2024-05-11'),
('RS110', 'IS112', '2024-05-13'),
('RS111', 'IS113', '2024-05-15'),
('RS112', 'IS114', '2024-05-17'),
('RS113', 'IS115', '2024-05-19'),
('RS114', 'IS116', '2024-05-21'),
('RS115', 'IS117', '2024-05-23'),
('RS116', 'IS118', '2024-05-25'),
('RS117', 'IS119', '2024-05-27'),
('RS118', 'IS120', '2024-05-29');
SELECT * FROM Return_Status;
```

### 2. CRUD Operations

- **Create**: Inserted sample records into the `books` table.
- **Read**: Retrieved and displayed data from various tables.
- **Update**: Updated records in the `employees` table.
- **Delete**: Removed records from the `members` table as needed.

**Task 1. Create a New Book Record**
-- "978-1-60129-456-2', 'To Kill a Mockingbird', 'Classic', 6.00, 'yes', 'Harper Lee', 'J.B. Lippincott & Co.')"

```sql

INSERT INTO Books(ISBN, Book_Title, Category, Rental_Price, Rental_Status, Author, Publisher) 
VALUES
('978-1-60129-456-2', 'To Kill a Mockingbird', 'Classic', 6.00, 'yes', 'Harper Lee', 'J.B. Lippincott & Co.');
```
**Task 2: Update an Existing Member's Address**

```sql

UPDATE Members
SET Member_address = '673 Pine ST'
WHERE Member_ID = 'C119';
```

**Task 3: Delete a Record from the Issued Status Table**
-- Objective: Delete the record with issued_id = 'IS121' from the issued_status table.

```sql

DELETE FROM Issued_Status
WHERE Issue_ID = 'IS121';
```

**Task 4: Retrieve All Books Issued by a Specific Employee**
-- Objective: Select all books issued by the employee with emp_id = 'E101'.
```sql

SELECT * 
FROM Issued_Status
WHERE Issued_Empl_ID = 'E101';
```


**Task 5: List Members Who Have Issued More Than One Book**
-- Objective: Use GROUP BY to find members who have issued more than one book.

```sql

SELECT 
      Issued_Member_ID,
      COUNT(*) AS NO_Issued_Books
FROM Issued_Status
GROUP BY Issued_Member_ID
HAVING NO_Issued_Books > 1;
      
```

### 3. CTAS (Create Table As Select)

- **Task 6: Create Summary Tables**: Used CTAS to generate new tables based on query results - each book and total book_issued_cnt**

```sql

CREATE TABLE Books_Counts
AS
SELECT
	B.ISBN,
    B.Book_Title,
    Category,
    COUNT(ST.Issued_Book_ISBN) AS No_Issued
FROM Books AS B
JOIN
issued_status AS IST
ON B.ISBN = IST.Issued_Book_ISBN
GROUP BY B.ISBN;

SELECT * FROM Books_Counts;
```


### 4. Data Analysis & Findings

The following SQL queries were used to address specific questions:

Task 7. **Retrieve All Books in a Specific Category**:

```sql
SELECT * FROM books
WHERE category = 'Classic';
```

8. **Task 8: Find Total Rental Income by Category**:

```sql

SELECT
      B.Category,
      SUM(B.Rental_Price) AS Rental_Income,
      COUNT(*)
FROM Issued_Status AS IST
JOIN 
Books AS B
ON B.ISBN = IST.Issued_Book_ISBN
GROUP BY 1;
```

9. **List Members Who Registered in the Last 180 Days**:
```sql

SELECT * 
FROM Members
WHERE Reg_Date >= CURDATE() - INTERVAL 180 DAY;
```

10. **List Employees with Their Branch Manager's Name and their branch details**:

```sql

SELECT 
      Emp.*,
      B.Manager_ID,
      Emp2.Emp_Name AS Manager
FROM Employee AS Emp
JOIN 
Branch AS B
ON 
Emp.Branch_ID = B.Branch_ID
JOIN 
Employee AS Emp2
ON
Emp2.Emp_ID = B.Manager_ID;
```
Task 11. **Create a Table of Books with Rental Price Above a Certain Threshold**:
```sql
CREATE TABLE Expensive_Books
SELECT * FROM Books
WHERE Rental_Price >= 7;
```

Task 12: **Retrieve the List of Books Not Yet Returned**
```sql

SELECT 
      ist.Issue_ID,
      ist.Issued_Member_ID,
      ist.Issued_Book_Name
FROM Issued_Status AS ist
LEFT JOIN
Return_Status AS rst
ON ist.Issue_ID = rst.Issued_ID
WHERE rst.Return_ID IS NULL;
```

**Task 13: Identify Members with Overdue Books**  
Write a query to identify members who have overdue books (assume a 30-day return period). Display the member's_id, member's name, book title, issue date, and days overdue.

```sql

SELECT 
    IST.Issued_Member_ID,
    M.Member_Name,
    B.Book_Title,
    Ist.Issued_Date,
    CURDATE() - Ist.Issued_Date AS Overdue_Days
FROM Issued_Status AS Ist
JOIN
Members AS M
ON 
Ist.Issued_Member_ID = m.Member_ID
JOIN
Books AS B
ON
B.ISBN = ist.Issued_Book_ISBN
LEFT JOIN
return_status AS Rst
ON 
ist.Issue_ID = Rst.Issued_ID;
```


**Task 14: Update Book Status on Return**  
Write a query to update the status of books in the books table to "Yes" when they are returned (based on entries in the return_status table).


```sql

DROP PROCEDURE IF EXISTS Add_Return_Records;
DELIMITER $$
CREATE PROCEDURE Add_Return_Records(
                                   IN P_Return_ID VARCHAR(15),
                                   IN P_Issued_ID VARCHAR(15),
                                   IN P_Return_Date DATE,
                                   IN P_Book_Quality VARCHAR(15)
                                   )
BEGIN
     DECLARE V_ISBN VARCHAR(50);
     DECLARE V_Book_Name VARCHAR(50);
     
     INSERT INTO Return_Status(Return_ID, Issued_ID, Return_Book_Name, Return_Date, Return_Book_ISBN)
     VALUES
     (P_Return_ID, P_Issued_ID, P_Return_Date, P_Book_Quality);
     
     SELECT Issued_Book_ISBN,
            Issued_Book_Name
	 INTO V_ISBN,
          V_Book_Name
     FROM Issued_Status
	 WHERE Issued_ID = P_Issued_ID;
         
     UPDATE Books
     SET Rental_Status = 'No'
     WHERE ISBN = V_ISBN;
     
	SELECT CONCAT('Thank you for returning the book: ', V_Book_Name) AS Message;
END $$
DELIMITER ;

```


**Task 15: Branch Performance Report**  
Create a query that generates a performance report for each branch, showing the number of books issued, the number of books returned, and the total revenue generated from book rentals.

```sql
CREATE TABLE Branch_Performance
AS
SELECT
      b.Branch_ID,
      b.Manager_ID,
      COUNT(ist.Issue_ID) AS Number_of_Books_Issued,
      COUNT(rst.Return_ID) AS Number_of_Books_Returned,
      SUM(bK.Rental_Price) AS Total_Revenue
FROM Issued_Status AS ist
JOIN
Employee AS e
ON
ist.Issued_Empl_ID = e.Emp_ID
JOIN
Branch AS b
ON 
e.Branch_ID = b.Branch_ID
LEFT JOIN
Return_Status AS rst
ON
ist.Issue_ID = rst.Issued_ID
JOIN
Books AS bk
ON
ist.Issued_Book_ISBN = bk.ISBN
GROUP BY b.Branch_ID, b.Manager_ID;

SELECT * FROM Branch_Performance;

```

**Task 16: CTAS: Create a Table of Active Members**  
Use the CREATE TABLE AS (CTAS) statement to create a new table active_members containing members who have issued at least one book in the last 2 months.

```sql

CREATE TABLE Active_Members
AS(
SELECT * FROM MEMBERS
WHERE Member_ID
IN(
SELECT
      DISTINCT Issued_Member_ID
FROM Issued_Status
WHERE Issued_Date >= '2024-10-01' - INTERVAL 6 MONTH)
);
SELECT * FROM Active_Members;
```


**Task 17: Find Employees with the Most Book Issues Processed**  
Write a query to find the top 3 employees who have processed the most book issues. Display the employee name, number of books processed, and their branch.

```sql

SELECT
      e.Emp_name,
      b.*,
      COUNT(ist.Issue_ID) AS Issued_Books
FROM Issued_Status AS ist
JOIN Employee AS e
ON 
ist.Issued_Empl_ID = e.Emp_ID
JOIN
Branch AS b
ON 
e.Branch_ID = b.Branch_ID
GROUP BY 1,2;
```
    

## Reports

- **Database Schema**: Detailed table structures and relationships.
- **Data Analysis**: Insights into book categories, employee salaries, member registration trends, and issued books.
- **Summary Reports**: Aggregated data on high-demand books and employee performance.

## Conclusion

This project demonstrates the application of SQL skills in creating and managing a library management system. It includes database setup, data manipulation, and advanced querying, providing a solid foundation for data management and analysis.

## How to Use

1. ** Clone this project repository from GitHub. 

2. **Set Up the Database**: Execute the SQL scripts in the `database_setup.sql` file to create and populate the database.
3. **Run the Queries**: Use the SQL queries in the `analysis_queries.sql` file to perform the analysis.
4. **Explore and Modify**: Customize the queries as needed to explore different aspects of the data or answer additional questions.

## Author - Wanjaueric

This project showcases SQL skills essential for database management and analysis. It highlights the ability to design, query, and manipulate relational databases effectively, ensuring data integrity, efficiency, and scalability. The project demonstrates proficiency in writing complex SQL queries, creating stored procedures, and performing data analysis tasks that are critical for real-world applications.

Thank you for your interest in this project!
