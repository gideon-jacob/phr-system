# Product Requirements Document (PRD)

## National Personal Health Record (PHR) System for India

### 1. Introduction & Vision

**1.1. The Problem:** In India, a citizen's medical history is fragmented across numerous hospitals, clinics, and labs, often in paper format. This leads to redundant testing, delays in care, incomplete medical histories during emergencies, and prevents patients from truly owning their health data.

**1.2. The Vision:** To create a "single source of truth" for every Indian citizen's health journey through an **open-source PHR infrastructure platform**. We envision a secure, patient-centric, developer-first digital platform, aligned with the Ayushman Bharat Digital Mission (ABDM), that consolidates all health records under a unique Ayushman Bharat Health Account (ABHA) ID. Unlike closed PHR apps, we provide a **deployable, auditable, and extensible monorepo** that governments, hospitals, and startups can clone, customize, and integrate with. This system will empower patients, improve clinical decision-making for doctors, enable third-party innovation through comprehensive APIs, and create a robust foundation for public health in India.

### 2. Goals & Objectives

- **Empower Patients:** Give citizens seamless access to and control over their lifelong health records.
- **Improve Healthcare Delivery:** Provide healthcare professionals with a holistic view of a patient's history to enable better, faster, and safer medical care.
- **Increase Efficiency:** Reduce healthcare costs by eliminating unnecessary and repetitive diagnostic tests.
- **Strengthen Public Health:** Generate anonymized, aggregated data to aid in policy-making and the management of public health crises.
- **Enable Open Innovation:** Provide a fully open-source, deployable PHR infrastructure that governments, hospitals, and startups can audit, customize, and extend.
- **Foster Developer Ecosystem:** Offer comprehensive, stable API documentation and an extensible plugin architecture to enable third-party integrations and innovations.
- **Build Trust Through Transparency:** Allow security audits of consent logic, ABHA flows, and data handling through open-source code.

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
5. **The Third-Party Developer:**
    - **Name:** Ravi, a developer at a health-tech startup building a chronic disease management app.
    - **Needs:** Clear, stable API documentation to integrate PHR functionality into his app without building the entire infrastructure from scratch. He wants to authenticate users via ABHA, fetch consented health records, and push new data back to the PHR system.
6. **The Government/Enterprise Adopter:**
    - **Name:** A state health department IT lead.
    - **Needs:** A deployable, auditable, ABDM-compliant PHR system that can be self-hosted, customized for state-specific workflows, and scaled to millions of users with guaranteed support and SLAs.

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

**4.3. Developer API & Integration Platform**

- **Feature: Comprehensive REST API**
    - *User Story:* As Ravi (third-party developer), I want to access well-documented REST APIs to authenticate users via ABHA, request consented health records, and submit new health data from my chronic disease management app.
- **Feature: Webhook System**
    - *User Story:* As a developer, I want to register webhooks to receive real-time notifications when a patient grants consent or new health records are added.
- **Feature: Plugin/Extension Architecture**
    - *User Story:* As a developer, I want to build custom modules (e.g., teleconsultation, insurance connectors, disease registries) that can be installed into the PHR system without modifying core code, similar to n8n extensions.

**4.4. Open-Source & Deployment**

- **Feature: Self-Hosted Deployment**
    - *User Story:* As a state health department, I want to clone the open-source repository, deploy it on my own infrastructure, and customize workflows for my state's specific requirements.
- **Feature: Docker & Kubernetes Support**
    - *User Story:* As a DevOps engineer, I want pre-configured Docker Compose and Kubernetes manifests to deploy the entire PHR stack with one command.

### 5. Success Metrics

- Percentage of healthcare providers (of all sizes) integrated with the system.
- Number of health records linked per active user.
- Reduction in the number of repeat diagnostic tests ordered nationwide.
- Patient and provider satisfaction scores (NPS).
- **Number of GitHub stars, forks, and active contributors** (community engagement).
- **Number of third-party integrations and plugins** built on the platform.
- **API adoption rate** (number of external apps using the PHR APIs).
- **Self-hosted deployments** (governments, hospitals, startups running their own instances).

### 6. Technical Architecture & Stack

- **Platform:** A **Progressive Web App (PWA)** will be the primary platform to ensure maximum accessibility and compatibility.
- **Frontend:** The user interface will be built with **React.js** and bundled with **Vite**.
- **Backend:** A **microservice architecture** will be implemented using **Java (Spring Boot)**.
- **Architecture:** A **Hybrid Federated Architecture** will be used to maximize adoption. It combines self-hosted databases for large institutions and a centrally managed **"Health Data Fiduciary Service"** for smaller providers.
- **Database:** A **polyglot persistence** approach will be used:
    - **PostgreSQL** for the relational data in the central registry.
    - **MongoDB** for the semi-structured HL7 FHIR data in both self-hosted nodes and the central fiduciary service.
- **API Layer:** RESTful APIs with comprehensive OpenAPI/Swagger documentation, versioned endpoints, and rate limiting.
- **Plugin System:** Modular extension architecture inspired by n8n, allowing third-party developers to build and distribute custom modules.
- **Deployment:** Docker containers, Kubernetes manifests, and infrastructure-as-code templates for easy self-hosting.

### 7. Open-Core Business Model

**7.1. Community Edition (Open Source)**
- Full PHR core functionality (patient records, consent management, ABDM integration)
- Basic APIs and documentation
- Self-hosting support
- Community support via GitHub

**7.2. Enterprise Edition (Paid)**
- Advanced consent and governance dashboards
- Multi-tenant management console
- Enterprise integrations (HIS/EHR, insurance/HCX, lab/pharmacy hubs)
- Advanced analytics and reporting
- Priority support and SLAs

**7.3. Managed Cloud Service (Paid)**
- Fully hosted PHR infrastructure
- Automatic scaling and monitoring
- Compliance certifications (data localization, security audits)
- Dedicated support team

**7.4. Professional Services (Paid)**
- Custom implementation and integration
- Training and onboarding
- ABDM certification assistance
- Migration from legacy systems


