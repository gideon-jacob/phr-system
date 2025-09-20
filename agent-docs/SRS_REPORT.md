# Software Requirements Specification (SRS)

## National Personal Health Record (PHR) System for India

### 1. Introduction

**1.1. Purpose**
This document provides a detailed specification for the National Personal Health Record (PHR) System. It describes the system's functional and non-functional requirements, its architecture, and the technology stack that will be used for its development.

**1.2. Scope**
The system will provide a unified, secure, and interoperable platform for all Indian citizens to access and manage their health records. It will serve patients, healthcare providers, and administrators. The primary interface for users will be a Progressive Web App (PWA) accessible from any modern web browser.

**1.3. Definitions & Acronyms**

- **PHR:** Personal Health Record
- **ABDM:** Ayushman Bharat Digital Mission
- **ABHA:** Ayushman Bharat Health Account
- **PWA:** Progressive Web App
- **FHIR:** Fast Healthcare Interoperability Resources
- **HIS:** Hospital Information System

### 2. Overall Description

**2.1. Product Perspective**
The PHR system is a patient-centric platform built upon the ABDM framework. It operates on a hybrid architecture, combining federated and centralized elements to ensure maximum participation and security. It securely connects to distributed data sources and aggregates information in real-time based on a multi-tiered consent model.

**2.2. Product Functions**

- Secure user authentication and registration via ABHA ID.
- Aggregation and chronological display of federated health records, based on explicit consent.
- Granular, time-bound consent management for data sharing.
- Secure intra-facility access for healthcare providers to view their own patient data.
- A standardized mechanism for healthcare facilities to upload digital health records.

**2.3. User Characteristics**
The system is designed for a diverse user base, ranging from tech-savvy urban citizens to individuals with limited digital literacy in rural areas. The UI must be intuitive, multilingual, and adhere to accessibility standards.

### 3. System Features (Functional Requirements)

**3.1. Patient Module ("MyABHA")**

- **3.1.1 Authentication:** Users shall be able to log in using their ABHA ID and a two-factor authentication (OTP).
- **3.1.2 Health Dashboard:** The system shall display a consolidated view of all linked health records, sortable by date, record type, and facility.
- **3.1.3 Consent Management:** The system shall provide an interface for patients to grant, view, and revoke data access consents for specific providers to access their federated (cross-facility) health records.

**3.2. Provider Module ("Provider Gateway")**

- **3.2.1 Intra-Facility Data Access:** The system shall permit authenticated healthcare professionals within a facility to view and manage all patient records *created by and stored within their own facility* without requiring real-time patient consent for each access. This serves as the primary patient management function.
- **3.2.2 Federated Record Request:** Authenticated providers shall be able to request access to a patient's records from *other* federated healthcare providers. This action requires explicit, time-bound consent from the patient.
- **3.2.3 Unified View:** Upon receiving patient consent, the system shall fetch records from external data sources and display them in a unified view alongside the provider's own internal records for that patient.
- **3.2.4 Record Submission:** Providers shall be able to upload new health records (e.g., prescriptions, lab reports) in a standardized FHIR format to their own data store (Tier 1 or Tier 2).

### 4. Non-Functional Requirements

**4.1. Performance**

- The PWA shall achieve a First Contentful Paint (FCP) of under 2.5 seconds on a 3G network connection.
- API response times for data aggregation shall not exceed 5 seconds.

**4.2. Usability & Accessibility**

- The user interface shall be responsive and functional across all major screen sizes (mobile, tablet, desktop).
- The PWA shall support offline access to previously viewed records and basic profile information using Service Workers.
- The application must be compliant with WCAG 2.1 AA accessibility standards.

**4.3. Security**

- All data in transit shall be encrypted using TLS 1.3.
- All data at rest within all data stores shall be encrypted using AES-256.
- The system shall maintain a detailed, immutable audit log of all data access events.

**4.4. Interoperability**

- All health data exchange must conform to the **HL7 FHIR R4** standard.

### 5. System Architecture & Technology Stack

**5.1. Architecture**
The system uses a **Hybrid Federated Architecture** to balance security, autonomy, and ease of adoption.

- **Central Registry:** A central service manages identity, authentication, consent for federated sharing, and pointers to the location of health records. It **does not** store the health records themselves.
- **Tier 1: Self-Hosted Federated Nodes:** Large, technically capable hospitals and labs can host their own secure, FHIR-compliant databases.
- **Tier 2: Managed Health Data Fiduciary Service:** To support smaller providers without IT infrastructure, the system will offer a secure, centrally managed, multi-tenant cloud database.

**5.2. Technology Stack**

- **Client-Side (Frontend):**
    - **Framework:** A Progressive Web App (PWA) built with **React.js (v18+)**.
    - **Build Tool:** **Vite** for fast development and optimized production builds.
- **Server-Side (Backend):**
    - **Architecture:** Microservices.
    - **Languages/Frameworks:** **Java (Spring Boot)**.
    - **API:** RESTful APIs compliant with the FHIR standard.
- **Database:** The system will employ a **polyglot persistence** strategy.
    - **Central Registry:** **PostgreSQL** will be used for its ACID compliance to manage user identities, consents, and audit logs.
    - **Health Data Stores (Both Tiers):** **MongoDB** will be the database of choice for its flexibility in storing complex, semi-structured HL7 FHIR resources.
- **Standards:** HL7 FHIR R4, SNOMED CT, LOINC.


