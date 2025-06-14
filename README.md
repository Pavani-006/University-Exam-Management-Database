# 🎓 University Database Management System (RDBMS Project)

This project implements a **University Relational Database Schema** using SQL. It models various real-world academic entities like students, faculty, courses, exams, attendance, and department relationships.

## 📁 Project Structure

```sql
-- Department Table
CREATE TABLE Department (
    D_id INT PRIMARY KEY,
    D_Name VARCHAR(100)
);

-- Student Table
CREATE TABLE Student (
    S_id INT PRIMARY KEY,
    S_Name VARCHAR(100),
    D_id INT,
    FOREIGN KEY (D_id) REFERENCES Department(D_id)
);

-- Course Table
CREATE TABLE Course (
    C_id INT PRIMARY KEY,
    C_Name VARCHAR(100),
    D_id INT,
    FOREIGN KEY (D_id) REFERENCES Department(D_id)
);

-- Faculty Table
CREATE TABLE Faculty (
    F_ID INT PRIMARY KEY,
    Faculty_Name VARCHAR(100)
);

-- Teaches Table (Many-to-Many: Faculty ↔ Course)
CREATE TABLE Teaches (
    F_ID INT,
    C_id INT,
    FOREIGN KEY (F_ID) REFERENCES Faculty(F_ID),
    FOREIGN KEY (C_id) REFERENCES Course(C_id)
);

-- Exam Table
CREATE TABLE Exam (
    Exam_ID INT PRIMARY KEY,
    Subject VARCHAR(100),
    Type VARCHAR(50), -- 'Internal' or 'External'
    Date DATE,
    Duration INT,
    Faculty_id INT,
    C_id INT,
    FOREIGN KEY (Faculty_id) REFERENCES Faculty(F_ID),
    FOREIGN KEY (C_id) REFERENCES Course(C_id)
);

-- Attendance Table
CREATE TABLE Attendance (
    S_id INT,
    C_id INT,
    Attendance_Percentage DECIMAL(5,2),
    PRIMARY KEY (S_id, C_id),
    FOREIGN KEY (S_id) REFERENCES Student(S_id),
    FOREIGN KEY (C_id) REFERENCES Course(C_id)
);

-- Enrollment Table (Recommended)
CREATE TABLE Enrollment (
    S_id INT,
    C_id INT,
    PRIMARY KEY (S_id, C_id),
    FOREIGN KEY (S_id) REFERENCES Student(S_id),
    FOREIGN KEY (C_id) REFERENCES Course(C_id)
);
```

## 📌 Sample Data Insertion

```sql
-- Departments
INSERT INTO Department (D_id, D_Name) VALUES
(1, 'Computer Science'),
(2, 'Mechanical Engineering'),
(3, 'Electrical Engineering');

-- Students
INSERT INTO Student (S_id, S_Name, D_id) VALUES
(101, 'Ravi Kumar', 1),
(102, 'Anita Sharma', 2),
(103, 'Mohit Verma', 3);

-- Courses
INSERT INTO Course (C_id, C_Name, D_id) VALUES
(201, 'Data Structures', 1),
(202, 'Thermodynamics', 2),
(203, 'Circuit Theory', 3);

-- Faculty Members
INSERT INTO Faculty (F_ID, Faculty_Name) VALUES
(301, 'Dr. Ramesh'),
(302, 'Prof. Neha'),
(303, 'Dr. Singh');

-- Faculty-Course Assignments
INSERT INTO Teaches (F_ID, C_id) VALUES
(301, 201),
(302, 202),
(303, 203);

-- Exams
INSERT INTO Exam (Exam_ID, Subject, Type, Date, Duration, Faculty_id, C_id) VALUES
(401, 'Data Structures', 'Internal', '2025-06-20', 90, 301, 201),
(402, 'Thermodynamics', 'External', '2025-06-22', 120, 302, 202),
(403, 'Circuit Theory', 'Internal', '2025-06-24', 60, 303, 203);

-- Attendance Records
INSERT INTO Attendance (S_id, C_id, Attendance_Percentage) VALUES
(101, 201, 85.50),
(102, 202, 78.25),
(103, 203, 92.00);

-- Enrollments
INSERT INTO Enrollment (S_id, C_id) VALUES
(101, 201),
(102, 202),
(103, 203);
```

## 💡 Features

- Proper use of **foreign keys** to maintain referential integrity.
- Clear **entity relationships**: one-to-many (e.g., Department → Students) and many-to-many (e.g., Faculty ↔ Courses).
- Attendance and exam tracking for students.
- Modular and extensible structure for fu
