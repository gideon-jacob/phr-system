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
    - **Name:** A hospital administrator.
    - **Needs:** A clear, standardized process for integrating the hospital's information system (HIS) with the national PHR network and a plan for digitizing decades of paper-based records.

### 4. Features & User Stories

**4.1. Patient Module ("MyABHA")**

- **Feature: Unified Health Dashboard**
    - *User Story:* As Priya, I want to log in securely with my ABHA ID and see a timeline of my entire health history, including doctor visits, prescriptions, lab results, and vaccination records.
- **Feature: Granular Consent Management**
    - *User Story:* As Priya, I want to grant a specific doctor view-access to my records for only 48 hours, and I want to be able to revoke that access at any time.
- **Feature: Family Profile Linking**
    - *User Story:* As Priya, I want to link my children's and parents' ABHA profiles to mine so I can help manage their health records from one place, with their consent.
- **Feature: Multilingual & Accessible UI**
    - *User Story:* As a user from a rural area, I want to be able to use the web platform in my native language and access my basic health information even with poor internet connectivity, which is achievable through its Progressive Web App (PWA) capabilities.

**4.2. Provider Module ("Provider Gateway")**

- **Feature: Patient Record Access**
    - *User Story:* As Dr. Sharma, when a patient gives me their ABHA ID, I want to request access and instantly view their consolidated medical history, including records from other hospitals, via a secure web portal.
- **Feature: Digital Health Record Upload**
    - *User Story:* As Dr. Sharma, I want to be able to seamlessly upload a new prescription or diagnosis report from my computer directly to the patient's PHR, making it a permanent part of their record.

**4.3. Emergency Access Module**

- **Feature: Emergency Profile Access**
    - *User Story:* As a paramedic, I want to scan a QR code on an accident victim's card or phone to immediately see their emergency profile containing allergies, blood type, and emergency contacts. This access must be automatically logged and audited.

**4.4. System & Interoperability**

- **Feature: Data Standardization & Integration**
    - The system must define clear standards for data exchange, allowing different hospital software (HIS, LIS) to communicate and share data securely.
- **Feature: Legacy Data Digitization**
    - The system must provide tools and guidelines for hospitals to scan and digitize historical paper records, linking them to the correct ABHA ID.

### 5. Success Metrics

- Percentage of the Indian population with an active PHR.
- Number of health records linked per active user.
- Average time saved by doctors per consultation.
- Reduction in the number of repeat diagnostic tests ordered nationwide.
- Patient and provider satisfaction scores (NPS).

### 6. Technical Architecture & Stack

- **Platform:** A **Progressive Web App (PWA)** will be the primary platform to ensure maximum accessibility, offline capabilities, and compatibility across all devices.
- **Frontend:** The user interface will be built with **React.js** and bundled with **Vite**.
- **Backend:** A **microservice architecture** will be implemented using **Java (Spring Boot)**.
- **Database:** A **polyglot persistence** approach will be used:
    - **PostgreSQL** for the relational data in the central registry (users, consents).
    - **MongoDB** for the semi-structured HL7 FHIR data at the federated hospital nodes.

