# Smart Clinic Management System - MySQL Schema Design

## Database: smart_clinic


---

# Table: admin

Stores admin login information.

CREATE TABLE admin (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL
);


---

# Table: doctor

Stores doctor information.

CREATE TABLE doctor (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    phone VARCHAR(15) NOT NULL,
    specialization VARCHAR(100) NOT NULL,
    available_times VARCHAR(255),
    password VARCHAR(255) NOT NULL
);


---

# Table: patient

Stores patient information.

CREATE TABLE patient (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    phone VARCHAR(15) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    date_of_birth DATE
);


---

# Table: appointment

Stores appointment details between doctor and patient.

CREATE TABLE appointment (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    
    doctor_id BIGINT NOT NULL,
    patient_id BIGINT NOT NULL,
    
    appointment_time DATETIME NOT NULL,
    status VARCHAR(50) DEFAULT 'BOOKED',

    CONSTRAINT fk_doctor
        FOREIGN KEY (doctor_id)
        REFERENCES doctor(id)
        ON DELETE CASCADE,

    CONSTRAINT fk_patient
        FOREIGN KEY (patient_id)
        REFERENCES patient(id)
        ON DELETE CASCADE
);


---

# Table: prescription

Stores prescriptions given by doctors.

CREATE TABLE prescription (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,

    doctor_id BIGINT NOT NULL,
    patient_id BIGINT NOT NULL,

    medication TEXT NOT NULL,
    notes TEXT,

    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_prescription_doctor
        FOREIGN KEY (doctor_id)
        REFERENCES doctor(id),

    CONSTRAINT fk_prescription_patient
        FOREIGN KEY (patient_id)
        REFERENCES patient(id)
);


---

# Relationships Summary

doctor → appointment → patient  
doctor → prescription → patient  

admin manages doctors  
patient books appointments  
doctor creates prescriptions

---

# ER Diagram (Conceptual)

Admin
  |
Doctor ---- Appointment ---- Patient
   |
Prescription
   |
Patient

---

# Total Tables

1. admin
2. doctor
3. patient
4. appointment
5. prescription

---

# Key Features

• Proper Primary Keys  
• Foreign Key Relationships  
• Normalized Design  
• Supports Appointment Booking  
• Supports Prescription Management  
