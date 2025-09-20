# Product Requirements Document (PRD)

## National Personal Health Record (PHR) System for India

### 1. Introduction & Vision

**1.1. The Problem:** In India, a citizen's medical history is fragmented across numerous hospitals, clinics, and labs, often in paper format. This leads to redundant testing, delays in care, incomplete medical histories during emergencies, and prevents patients from truly owning their health data.

**1.2. The Vision:** To create a "single source of truth" for every Indian citizen's health journey. We envision a secure, patient-centric digital platform, aligned with the Ayushman Bharat Digital Mission (ABDM), that consolidates all health records under a unique Ayushman Bharat Health Account (ABHA) ID. This system will empower patients, improve clinical decision-making for doctors, and create a robust foundation for public health in India.

### 2. Goals & Objectives

- **Empower Patients:** Give citizens seamless access to and control over their lifelong health records.
- **Improve Healthcare Delivery:** Provide healthcare professionals with a holistic view of a patient's history to enable better, faster, and safer medical care.
- **Increase Efficiency:** Reduce healthcare costs by eliminating unnecessary and repetitive diagnostic tests.
- **Strengthen Public Health:** Generate anonymized, aggregated data to aid in policy-making and the management of public health crises.

### 3. User Personas

1. **The Patient (Citizen):**
    - **Name:** Priya, a 35-year-old mother in a tier-2 city.
    - **Needs:** To manage her children's vaccination schedules, access her elderly parents' lab reports, and easily share her medical history with a new specialist without carrying a physical file. She is concerned about the privacy of her family's health data.
2. **The Healthcare Provider (Doctor):**
    - **Name:** Dr. Sharma, a general physician in a busy urban clinic.
    - **Needs:** To get a quick, comprehensive medical history of a new patient to make an accurate diagnosis. The system must be fast, intuitive, and integrate with his existing clinic management software.
3. **The Emergency Responder:**
    - **Name:** A paramedic team responding to a road accident.
    - **Needs:** Immediate, read-only access to an unconscious patient's critical information—such as blood type, known allergies, and pre-existing conditions—to provide life-saving care.
4. **The Health Facility Administrator:**
    - **Name:** An administrator at a small, rural clinic.
    - **Needs:** A simple, low-cost way to comply with national digital health standards without needing to hire an IT team or purchase expensive servers.

### 4. Features & User Stories

**4.1. Patient Module ("MyABHA")**

- **Feature: Unified Health Dashboard**
    - *User Story:* As Priya, I want to log in securely with my ABHA ID and see a timeline of my entire health history, including doctor visits, prescriptions, lab results, and vaccination records.
- **Feature: Granular Consent Management**
    - *User Story:* As Priya, I want to grant a specific doctor view-access to my records for only 48 hours, and I want to be able to revoke that access at any time.

**4.2. Provider Module ("Provider Gateway")**

- **Feature: Patient Record Access**
    - *User Story:* As Dr. Sharma, when a patient gives me their ABHA ID, I want to request access and instantly view their consolidated medical history.
- **Feature: Simplified Data Upload**
    - *User Story:* As an administrator at a rural clinic, I want a simple web interface to upload a patient's new lab report to the national network without managing my own database.

### 5. Success Metrics

- Percentage of healthcare providers (of all sizes) integrated with the system.
- Number of health records linked per active user.
- Reduction in the number of repeat diagnostic tests ordered nationwide.
- Patient and provider satisfaction scores (NPS).

### 6. Technical Architecture & Stack

- **Platform:** A **Progressive Web App (PWA)** will be the primary platform to ensure maximum accessibility and compatibility.
- **Frontend:** The user interface will be built with **React.js** and bundled with **Vite**.
- **Backend:** A **microservice architecture** will be implemented using **Java (Spring Boot)**.
- **Architecture:** A **Hybrid Federated Architecture** will be used to maximize adoption. It combines self-hosted databases for large institutions and a centrally managed **"Health Data Fiduciary Service"** for smaller providers.
- **Database:** A **polyglot persistence** approach will be used:
    - **PostgreSQL** for the relational data in the central registry.
    - **MongoDB** for the semi-structured HL7 FHIR data in both self-hosted nodes and the central fiduciary service.


