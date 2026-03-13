# Student & Enrollment Microservices System

## 📌 Project Description
This project implements a **Microservices-based Student Enrollment System** using **Spring Boot, Maven, and MySQL**. The system manages students and their course enrollments through independent services communicating via **REST APIs**.

## 🏗 Architecture
The system consists of the following components:

- **API Gateway** – Routes requests to microservices  
- **Student Service** – Manages student information  
- **Enrollment Service** – Handles course enrollments  
- **CLI Client** – Command-line interface for testing APIs  
- **MySQL Databases**
  - `student_db`
  - `enrollment_db`

## 📁 Project Structure
```

project-root
│
├── gateway
│   └── API Gateway
│
├── student-service
│   └── Handles student CRUD operations
│
├── enrollment-service
│   └── Handles course enrollment operations
│
├── cli-client
│   └── Command-line testing client
│
└── sql
└── SQL File 8

````

## ⚙️ Technologies Used
- Java  
- Spring Boot  
- Maven  
- MySQL  
- REST APIs  
- Microservices Architecture  

## Database Setup

### Student Database
```sql
USE student_db;
````

Create Students Table

```sql
CREATE TABLE students (
    roll_no VARCHAR(50) PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL
);
```

View Students

```sql
SELECT * FROM students;
```

Add Roll Number Column (if required)

```sql
ALTER TABLE students ADD COLUMN roll_no VARCHAR(50) UNIQUE;
```

Drop Table (optional)

```sql
DROP TABLE IF EXISTS students;
```

### Enrollment Database

```sql
USE enrollment_db;
```

Create Enrollments Table

```sql
CREATE TABLE IF NOT EXISTS enrollments (
    student_roll_no VARCHAR(20) NOT NULL,
    student_name VARCHAR(100) NOT NULL,
    course VARCHAR(100) NOT NULL,
    credit INT NOT NULL,
    PRIMARY KEY(student_roll_no, course)
);
```

View Enrollments

```sql
SELECT * FROM enrollments;
```

Rename Column

```sql
ALTER TABLE enrollments 
CHANGE COLUMN student_id student_roll_no VARCHAR(20) NOT NULL;
```

Add Credit Column

```sql
ALTER TABLE enrollments 
ADD COLUMN credit INT NOT NULL DEFAULT 0;
```

Reset Table

```sql
TRUNCATE TABLE enrollments;
```

Drop Table

```sql
DROP TABLE enrollments;
```

## Build and Run the Project

Build the project

```bash
mvn clean install
```

Force update dependencies

```bash
mvn clean install -U
```

Compile and run

```bash
mvn clean compile exec:java
```

Run Spring Boot application

```bash
mvn spring-boot:run
```

## Running Microservices

Run each service in **separate terminals**

Start Gateway

```bash
cd gateway
mvn spring-boot:run
```

Start Student Service

```bash
cd student-service
mvn spring-boot:run
```

Start Enrollment Service

```bash
cd enrollment-service
mvn spring-boot:run
```

Run CLI Client

```bash
cd cli-client
mvn clean compile exec:java
```

## Student Service API

Base URL

```
http://localhost:8081
```

Add Student
POST `/students/add`

```json
{
  "rollNo": "103",
  "name": "Nandini Jhunjhunwal",
  "email": "nandini@example.com"
}
```

Get Student by Roll Number

```
GET /students/roll/103
```

Get All Students

```
GET /students/all
```

Update Student
PUT `/students/update/103`

```json
{
  "name": "Nandini J",
  "email": "nandini.j@example.com"
}
```

Delete Student

```
DELETE /students/delete/103
```

## Enrollment Service API

Base URL

```
http://localhost:8082
```

Enroll Student
POST `/enrollments/enroll`

```json
{
  "studentRollNo": "104",
  "course": "Mathematics",
  "credit": 3
}
```

Get All Enrollments

```
GET /enrollments/all
```

Get Student Enrollments

```
GET /enrollments/student/103
```

Update Enrollment

```
PUT /enrollments/update/103?oldCourse=Mathematics&newCourse=Physics&credit=4
```

Unenroll from Course

```
DELETE /enrollments/unenroll/103?course=Physics
```

Delete All Enrollments of a Student

```
DELETE /enrollments/student/103
```

## Testing Flow

Typical workflow:

1. Start **Gateway**
2. Start **Student Service**
3. Start **Enrollment Service**
4. Add a **Student**
5. Enroll the student in a **Course**
6. Retrieve student and enrollment data

## Author

**Nandini Jhunjhunwal**
B.Tech Computer Science

```


