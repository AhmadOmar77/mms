# CareNow Database Design

## Entity Relationship Diagram (ERD)

### Tables Overview

#### 1. users
- id (PK)
- name
- email (unique)
- password
- phone
- role (enum: patient, doctor, admin, ambulance_driver)
- email_verified_at
- remember_token
- created_at
- updated_at

#### 2. medical_profiles
- id (PK)
- user_id (FK -> users.id)
- blood_type (enum: A+, A-, B+, B-, AB+, AB-, O+, O-)
- date_of_birth
- gender (enum: male, female)
- height (cm)
- weight (kg)
- chronic_diseases (JSON)
- allergies (JSON)
- current_medications (JSON)
- emergency_contact_name
- emergency_contact_phone
- insurance_number
- insurance_provider
- created_at
- updated_at

#### 3. doctors
- id (PK)
- user_id (FK -> users.id)
- specialization
- license_number
- years_of_experience
- clinic_address
- consultation_fee
- available_days (JSON)
- available_hours (JSON)
- bio (text)
- is_verified (boolean)
- rating (decimal)
- created_at
- updated_at

#### 4. emergency_alerts
- id (PK)
- user_id (FK -> users.id)
- latitude
- longitude
- address
- status (enum: pending, dispatched, arrived, completed, cancelled)
- ambulance_id (FK -> ambulances.id, nullable)
- dispatched_at
- arrived_at
- completed_at
- notes (text)
- created_at
- updated_at

#### 5. ambulances
- id (PK)
- vehicle_number
- driver_id (FK -> users.id)
- current_latitude
- current_longitude
- status (enum: available, busy, offline)
- vehicle_type
- equipment_list (JSON)
- created_at
- updated_at

#### 6. consultations
- id (PK)
- patient_id (FK -> users.id)
- doctor_id (FK -> doctors.id)
- appointment_date
- appointment_time
- status (enum: scheduled, completed, cancelled, no_show)
- consultation_type (enum: online, in_person)
- symptoms (text)
- diagnosis (text, nullable)
- prescription (text, nullable)
- notes (text, nullable)
- meeting_link (nullable)
- created_at
- updated_at

#### 7. messages
- id (PK)
- consultation_id (FK -> consultations.id)
- sender_id (FK -> users.id)
- message (text)
- attachment_url (nullable)
- is_read (boolean)
- created_at
- updated_at

#### 8. prescriptions
- id (PK)
- consultation_id (FK -> consultations.id)
- medication_name
- dosage
- frequency
- duration
- instructions (text)
- created_at
- updated_at

#### 9. reviews
- id (PK)
- doctor_id (FK -> doctors.id)
- patient_id (FK -> users.id)
- consultation_id (FK -> consultations.id)
- rating (1-5)
- comment (text, nullable)
- created_at
- updated_at

#### 10. notifications
- id (PK)
- user_id (FK -> users.id)
- type (enum: emergency, appointment, message, system)
- title
- message
- data (JSON, nullable)
- is_read (boolean)
- created_at
- updated_at

## Relationships

### One-to-One
- users -> medical_profiles (one user has one medical profile)
- users -> doctors (one user can be one doctor)

### One-to-Many
- users -> emergency_alerts (one user can create many emergency alerts)
- users -> consultations (as patient)
- doctors -> consultations (one doctor has many consultations)
- ambulances -> emergency_alerts (one ambulance handles many alerts)
- consultations -> messages (one consultation has many messages)
- consultations -> prescriptions (one consultation has many prescriptions)
- doctors -> reviews (one doctor has many reviews)
- users -> notifications (one user has many notifications)

### Many-to-Many
- None in current design

## Indexes

### Primary Indexes
- All tables have `id` as primary key

### Foreign Key Indexes
- medical_profiles.user_id
- doctors.user_id
- emergency_alerts.user_id
- emergency_alerts.ambulance_id
- ambulances.driver_id
- consultations.patient_id
- consultations.doctor_id
- messages.consultation_id
- messages.sender_id
- prescriptions.consultation_id
- reviews.doctor_id
- reviews.patient_id
- notifications.user_id

### Additional Indexes
- users.email (unique)
- users.role
- doctors.license_number (unique)
- emergency_alerts.status
- ambulances.status
- consultations.status
- consultations.appointment_date

## Data Types

### Enums
- user_role: patient, doctor, admin, ambulance_driver
- blood_type: A+, A-, B+, B-, AB+, AB-, O+, O-
- gender: male, female
- alert_status: pending, dispatched, arrived, completed, cancelled
- ambulance_status: available, busy, offline
- consultation_status: scheduled, completed, cancelled, no_show
- consultation_type: online, in_person
- notification_type: emergency, appointment, message, system

### JSON Fields
- chronic_diseases: ["Diabetes", "Hypertension"]
- allergies: ["Penicillin", "Peanuts"]
- current_medications: ["Aspirin 100mg", "Metformin 500mg"]
- available_days: ["Monday", "Wednesday", "Friday"]
- available_hours: {"start": "09:00", "end": "17:00"}
- equipment_list: ["Defibrillator", "Oxygen Tank"]
- notification_data: {custom data based on type}
