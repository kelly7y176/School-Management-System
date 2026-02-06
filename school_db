-- Create the Database 
-- CREATE DATABASE IF NOT EXISTS school_db; 
-- USE school_db; 

-- ---------------------------------------------------------
-- DATABASE IMPLEMENTATION 
-- ---------------------------------------------------------

-- 1. Refreshing Environment: Clear old versions to start fresh
-- Note: Dropping in correct order to avoid Foreign Key constraint errors
DROP TABLE IF EXISTS FeePayments;
DROP TABLE IF EXISTS Enrollments;
DROP TABLE IF EXISTS Classes;
DROP TABLE IF EXISTS Students;
DROP TABLE IF EXISTS Teachers;

-- 2. Create Tables (DDL) 
CREATE TABLE Students (
    StudentID INT NOT NULL,
    StudentName VARCHAR(100),
    Email VARCHAR(100),
    EnrollmentDate DATE
);

CREATE TABLE Teachers (
    TeacherID INT NOT NULL,
    TeacherName VARCHAR(100),
    Email VARCHAR(100),
    Department VARCHAR(50) -- ADDED: Needed for Q7
);

CREATE TABLE Classes (
    ClassID INT NOT NULL,
    ClassName VARCHAR(100),
    Semester VARCHAR(20),
    TeacherID INT
);

CREATE TABLE Enrollments (
    EnrollmentID INT NOT NULL,
    StudentID INT,
    ClassID INT,
    Grade DECIMAL(5,2)
);

CREATE TABLE FeePayments (
    PaymentID INT NOT NULL,
    StudentID INT,
    AmountPaid DECIMAL(10,2),
    PaymentDate DATE,
    Status VARCHAR(20)
);

-- 3. Add Constraints (Primary and Foreign Keys) 
-- Requirement: Separate ALTER TABLE statements 
ALTER TABLE Students ADD PRIMARY KEY (StudentID);
ALTER TABLE Teachers ADD PRIMARY KEY (TeacherID);
ALTER TABLE Classes ADD PRIMARY KEY (ClassID);
ALTER TABLE Enrollments ADD PRIMARY KEY (EnrollmentID);
ALTER TABLE FeePayments ADD PRIMARY KEY (PaymentID);

ALTER TABLE Classes ADD FOREIGN KEY (TeacherID) REFERENCES Teachers(TeacherID);
ALTER TABLE Enrollments ADD FOREIGN KEY (StudentID) REFERENCES Students(StudentID);
ALTER TABLE Enrollments ADD FOREIGN KEY (ClassID) REFERENCES Classes(ClassID);
ALTER TABLE FeePayments ADD FOREIGN KEY (StudentID) REFERENCES Students(StudentID);

-- 4. Insert Data 
-- Requirement: Enough data to demonstrate the need for a database [cite: 1, 34, 35]
INSERT INTO Students VALUES (1, 'Alice Young', 'alice@email.com', '2024-01-15');
INSERT INTO Students VALUES (2, 'Bob Smith', 'bob@email.com', '2024-01-16');
INSERT INTO Students VALUES (3, 'Charlie Brown', 'charlie@email.com', '2024-01-17');

INSERT INTO Teachers VALUES (101, 'Dr. Aris', 'aris@school.edu', 'Computer Science');
INSERT INTO Teachers VALUES (102, 'Prof. Sarah', 'sarah@school.edu', 'Mathematics');

INSERT INTO Classes VALUES (501, 'Database Systems', 'Spring 2024', 101);
INSERT INTO Classes VALUES (502, 'Calculus I', 'Spring 2024', 102);

INSERT INTO Enrollments VALUES (1, 1, 501, 85.50);
INSERT INTO Enrollments VALUES (2, 2, 501, 92.00);
INSERT INTO Enrollments VALUES (3, 3, 501, 78.00);
INSERT INTO Enrollments VALUES (4, 1, 502, 95.00);

INSERT INTO FeePayments VALUES (1001, 1, 500.00, '2024-02-01', 'Paid');
INSERT INTO FeePayments VALUES (1002, 2, 500.00, '2024-02-02', 'Paid');
INSERT INTO FeePayments VALUES (1003, 3, 0.00, NULL, 'Unpaid');

-- ---------------------------------------------------------
-- APPLICATION IMPLEMENTATION (10 QUERIES) 
-- Requirement: 10 queries for core business processes [cite: 1, 40]
-- ---------------------------------------------------------

-- Q1: Check if fee payment for Student X is up-to-date [cite: 1, 87]
SELECT StudentName, Status 
FROM Students 
JOIN FeePayments ON Students.StudentID = FeePayments.StudentID 
WHERE Students.StudentID = 3;

-- Q2: Average classes students enroll in per semester [cite: 1, 88]
-- FIXED: Added Enrollments.ClassID to avoid ambiguity
SELECT Semester, AVG(ClassCount) 
FROM (
    SELECT StudentID, Semester, COUNT(Enrollments.ClassID) as ClassCount 
    FROM Enrollments 
    JOIN Classes ON Enrollments.ClassID = Classes.ClassID 
    GROUP BY StudentID, Semester
) AS SubQuery 
GROUP BY Semester;

-- Q3: Mean, Max, and Min grade for each class [cite: 1, 91]
SELECT ClassID, AVG(Grade) as MeanGrade, MAX(Grade) as MaxGrade, MIN(Grade) as MinGrade 
FROM Enrollments 
GROUP BY ClassID;

-- Q4: List all students in a specific class (e.g., Database Systems)
SELECT StudentName 
FROM Students 
JOIN Enrollments ON Students.StudentID = Enrollments.StudentID 
WHERE ClassID = 501;

-- Q5: Identify students with unpaid fees 
SELECT StudentName, Email 
FROM Students 
JOIN FeePayments ON Students.StudentID = FeePayments.StudentID 
WHERE Status = 'Unpaid';

-- Q6: Find which teacher is teaching a specific student
SELECT DISTINCT TeacherName 
FROM Teachers 
JOIN Classes ON Teachers.TeacherID = Classes.TeacherID 
JOIN Enrollments ON Classes.ClassID = Enrollments.ClassID 
WHERE StudentID = 1;

-- Q7: Count of students enrolled in each department
-- FIXED: Using table aliases (T, C, E) and ensuring Department column exists
SELECT T.Department, COUNT(DISTINCT E.StudentID) AS StudentCount
FROM Teachers T
JOIN Classes C ON T.TeacherID = C.TeacherID
JOIN Enrollments E ON C.ClassID = E.ClassID
GROUP BY T.Department;

-- Q8: List students who scored above 90 in any class
SELECT StudentName, Grade 
FROM Students 
JOIN Enrollments ON Students.StudentID = Enrollments.StudentID 
WHERE Grade > 90;

-- Q9: Total revenue collected from fees
SELECT SUM(AmountPaid) as TotalRevenue FROM FeePayments;

-- Q10: Find the class with the highest average grade
SELECT ClassID, AVG(Grade) 
FROM Enrollments 
GROUP BY ClassID 
ORDER BY AVG(Grade) DESC LIMIT 1;
