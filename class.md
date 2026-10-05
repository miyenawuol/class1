# Corrected Hospital Management System Database Assignment

```sql
-- Create database
CREATE DATABASE IF NOT EXISTS hospital_management;
USE hospital_management;

-- 1. Departments table
CREATE TABLE departments (
    department_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE,
    location VARCHAR(100) NOT NULL
);

-- 2. Doctors table
CREATE TABLE doctors (
    doctor_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    specialization VARCHAR(100) NOT NULL,
    phone VARCHAR(20) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL UNIQUE,
    department_id INT NOT NULL,
    CONSTRAINT fk_doctors_department
        FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
        ON UPDATE CASCADE
        ON DELETE RESTRICT
);

-- 3. Patients table
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

-- 4. Appointments table
CREATE TABLE appointments (
    appointment_id INT AUTO_INCREMENT PRIMARY KEY,
    patient_id INT NOT NULL,
    doctor_id INT NOT NULL,
    appointment_date DATETIME NOT NULL,
    status ENUM('Scheduled', 'Completed', 'Cancelled') DEFAULT 'Scheduled',
    reason TEXT,
    CONSTRAINT fk_appointments_patient
        FOREIGN KEY (patient_id)
        REFERENCES patients(patient_id)
        ON UPDATE CASCADE
        ON DELETE CASCADE,
    CONSTRAINT fk_appointments_doctor
        FOREIGN KEY (doctor_id)
        REFERENCES doctors(doctor_id)
        ON UPDATE CASCADE
        ON DELETE CASCADE
);

-- 5. Medical records table
CREATE TABLE medical_records (
    record_id INT AUTO_INCREMENT PRIMARY KEY,
    patient_id INT NOT NULL,
    doctor_id INT NOT NULL,
    diagnosis TEXT NOT NULL,
    treatment_plan TEXT,
    prescribed_date DATE NOT NULL,
    CONSTRAINT fk_medical_records_patient
        FOREIGN KEY (patient_id)
        REFERENCES patients(patient_id)
        ON UPDATE CASCADE
        ON DELETE CASCADE,
    CONSTRAINT fk_medical_records_doctor
        FOREIGN KEY (doctor_id)
        REFERENCES doctors(doctor_id)
        ON UPDATE CASCADE
        ON DELETE CASCADE
);

-- Sample data
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
(1, 1, 'Mild Hypertension', 'Low sodium diet and exercise', '2026-10-01'),
(2, 2, 'Routine Pediatric Checkup', 'Continue healthy diet and regular follow-up', '2026-10-02');
```

## Notes
- The SQL script is valid for MySQL.
- Foreign keys are named clearly and use proper cascade rules.
- Sample records were corrected to match the table structure.
- The script can be saved as `answer.sql` and run in MySQL Workbench or phpMyAdmin.