Here is a complete SQL script for a **Hospital Management System** database. You can save this code directly into a file named `answer.sql` in your GitHub repository.

---

### `answer.sql`

```sql
-- Create and switch to the new database
CREATE DATABASE IF NOT EXISTS hospital_management;
USE hospital_management;

-- 1. Departments Table
CREATE TABLE departments (
    department_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE,
    location VARCHAR(100) NOT NULL
);

-- 2. Doctors Table
CREATE TABLE doctors (
    doctor_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    specialization VARCHAR(100) NOT NULL,
    phone VARCHAR(20) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL UNIQUE,
    department_id INT NOT NULL,
    FOREIGN KEY (department_id) REFERENCES departments(department_id) ON DELETE CASCADE
);

-- 3. Patients Table
CREATE TABLE patients (
    patient_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    date_of_birth DATE NOT NULL,
    gender ENUM('Male', 'Female', 'Other') NOT NULL,
    phone VARCHAR(20) NOT NULL UNIQUE,
    address TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 4. Appointments Table
CREATE TABLE appointments (
    appointment_id INT AUTO_INCREMENT PRIMARY KEY,
    patient_id INT NOT NULL,
    doctor_id INT NOT NULL,
    appointment_date DATETIME NOT NULL,
    status ENUM('Scheduled', 'Completed', 'Cancelled') DEFAULT 'Scheduled',
    reason TEXT,
    FOREIGN KEY (patient_id) REFERENCES patients(patient_id) ON DELETE CASCADE,
    FOREIGN KEY (doctor_id) REFERENCES doctors(doctor_id) ON DELETE CASCADE
);

-- 5. Medical Records Table
CREATE TABLE medical_records (
    record_id INT AUTO_INCREMENT PRIMARY KEY,
    patient_id INT NOT NULL,
    doctor_id INT NOT NULL,
    diagnosis TEXT NOT NULL,
    treatment_plan TEXT,
    prescribed_date DATE NOT NULL,
    FOREIGN KEY (patient_id) REFERENCES patients(patient_id) ON DELETE CASCADE,
    FOREIGN KEY (doctor_id) REFERENCES doctors(doctor_id) ON DELETE CASCADE
);

-- Sample Data Insertion

INSERT INTO departments (name, location) VALUES
('Cardiology', 'Building A, Floor 2'),
('Pediatrics', 'Building B, Floor 1'),
('Neurology', 'Building A, Floor 3');

INSERT INTO doctors (first_name, last_name, specialization, phone, email, department_id) VALUES
('Alice', 'Smith', 'Cardiologist', '555-0101', 'alice.smith@hospital.org', 1),
('Bob', 'Jones', 'Pediatrician', '555-0102', 'bob.jones@hospital.org', 2),
('Carol', 'White', 'Neurologist', '555-0103', 'carol.white@hospital.org', 3);

INSERT INTO patients (first_name, last_name, date_of_birth, gender, phone, address) VALUES
('John', 'Doe', '1985-06-15', 'Male', '555-0201', '123 Main St, Cityville'),
('Jane', 'Smith', '1992-11-23', 'Female', '555-0202', '456 Oak Rd, Townsville');

INSERT INTO appointments (patient_id, doctor_id, appointment_date, status, reason) VALUES
(1, 1, '2026-10-10 09:00:00', 'Scheduled', 'Annual cardiac checkup'),
(2, 2, '2026-10-11 10:30:00', 'Scheduled', 'Routine checkup for child');

INSERT INTO medical_records (patient_id, doctor_id, diagnosis, treatment_plan, prescribed_date) VALUES
(1, 1, 'Mild Hypertension', 'Low sodium diet and exercise', '2026-10-01');

```

---

### Steps to Commit to GitHub

1. Create a local directory and move into it:
```bash
mkdir week-1-database-assignment
cd week-1-database-assignment

```


2. Save the SQL code above into a file named `answer.sql`.
3. Initialize git and commit your work:
```bash
git init
git add answer.sql
git commit -m "Add week 1 database assignment script"

```


4. Link to your new repository on GitHub and push:
```bash
git remote add origin https://github.com/<your-username>/week-1-database-assignment.git
git branch -M main
git push -u origin main

```