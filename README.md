Employee Management System (EMS)

Full-stack Employee Management System built with React + Vite, Spring Boot, Spring Data JPA, MySQL, and JWT authentication.

Main Features

Register and log in with persistent employer accounts.

Registration validation requires a valid name/email and an 8–72 character password.

JWT-based authentication for protected API endpoints.

Employee CRUD with name, age, email, phone, department, designation, salary, joining date, and status.

Input validation for employee details, attendance, and loans.

Attendance stored in MySQL, with one record per employee per date.

Attendance cannot be marked for inactive employees, before their joining date, or for future dates.

Three-state attendance: Not Marked → Present → Absent → Not Marked.

Monthly attendance register for all employees, including future dates and holidays.

Current-month payroll estimate with joining-date proration, attendance deductions, and loan EMI.

Employee loans with amount, interest, tenure, outstanding balance, and EMI affordability validation.

Company profile stored in MySQL.

Business data persists across browser refreshes and application restarts.

Technology Stack

Frontend: React 19 + Vite

Backend: Spring Boot 3.2.3 + Spring Data JPA + Spring Security

Database: MySQL

Authentication: BCrypt password hashing + signed JWT (HS256)

Database Setup

For a clean first-time installation, open MySQL Workbench and run DATABASE_RESET.sql, then DATABASE_SETUP.sql.

Warning: The reset script may delete existing database data. Back up your database before using it.

For an older EMS database, see DATABASE_MIGRATE_EMPLOYER.sql and the other migration scripts. Review the instructions in each SQL file before executing it.

Start the Backend

Open PowerShell in the backend directory:

mvn spring-boot:run

Backend URL: http://localhost:8080

Start the Frontend

Open a second PowerShell terminal in the project root:

npm install
npm run dev

Frontend URL: http://localhost:5173

The .env.example file documents the optional VITE_API_BASE variable for changing the backend URL.

Attendance Register and Holiday Rules

The Attendance page provides a monthly register for all employees.

P = Present, A = Absent, H = Holiday, F = Future, B = Before joining, and — = Not marked.

Future working dates are displayed without creating fake attendance records.

Payroll estimates exclude weekends and configured public holidays.

Maharashtra public holidays are configured for 2026. Update the list when the relevant government publishes the next year's notification.

Employee email addresses must end in @gmail.com, as validated by the frontend and backend.

Loan principal and combined active EMI limits are enforced by the backend.

Database Inspection

Select the database in MySQL Workbench and inspect the tables:

USE employee_db;
SELECT * FROM users;
SELECT * FROM employee;
SELECT * FROM attendance;
SELECT * FROM employee_loan;
SELECT * FROM company_profile;

For existing databases, review DATABASE_MIGRATION_ATTENDANCE_VIEW.sql to create read-only attendance and loan views. Review DATABASE_OPTIONAL_CLEANUP_FUTURE_ATTENDANCE.sql before using its cleanup statements.

Assignment Alignment

This project demonstrates React SPA integration with a Spring Boot REST API, JPA/MySQL persistence, CRUD operations, and JWT-protected API access.