# Software Requirements Specification (SRS)

## National Personal Health Record (PHR) System for India

### 1. Introduction

**1.1. Purpose**
This document provides a detailed specification for the National Personal Health Record (PHR) System. It describes the system's functional and non-functional requirements, its architecture, and the technology stack that will be used for its development.

**1.2. Scope**
The system will provide a unified, secure, and interoperable **open-source platform** for all Indian citizens to access and manage their health records. It will serve patients, healthcare providers, administrators, and third-party developers. The primary interface for users will be a Progressive Web App (PWA) accessible from any modern web browser. The system is designed as **PHR infrastructure** that can be deployed, customized, and extended by governments, hospitals, and health-tech startups. Comprehensive REST APIs enable external applications to integrate PHR functionality without building the entire stack from scratch.

**1.3. Definitions & Acronyms**

- **PHR:** Personal Health Record
- **ABDM:** Ayushman Bharat Digital Mission
- **ABHA:** Ayushman Bharat Health Account
- **PWA:** Progressive Web App
- **FHIR:** Fast Healthcare Interoperability Resources
- **HIS:** Hospital Information System
- **API:** Application Programming Interface
- **REST:** Representational State Transfer
- **SDK:** Software Development Kit
- **Open-Core:** Business model combining open-source core with paid enterprise features

### 2. Overall Description

**2.1. Product Perspective**
The PHR system is a patient-centric, **open-source platform** built upon the ABDM framework. It operates on a hybrid architecture, combining federated and centralized elements to ensure maximum participation and security. It securely connects to distributed data sources and aggregates information in real-time based on a multi-tiered consent model. Unlike closed PHR applications, this system is designed as **deployable infrastructure** that can be audited, customized, and extended by any organization. It provides comprehensive APIs for third-party integration, enabling a developer ecosystem around PHR functionality.

**2.2. Product Functions**

- Secure user authentication and registration via ABHA ID.
- Aggregation and chronological display of federated health records, based on explicit consent.
- Granular, time-bound consent management for data sharing.
- Secure intra-facility access for healthcare providers to view their own patient data.
- A standardized mechanism for healthcare facilities to upload digital health records.
- **Comprehensive REST APIs** for third-party integration and external app development.
- **Plugin/extension system** for custom modules and integrations.
- **Webhook support** for real-time event notifications.
- **Self-hosting capabilities** with Docker and Kubernetes deployment options.
- **Developer documentation** including API references, integration guides, and SDK examples.

**2.3. User Characteristics**
The system is designed for a diverse user base, ranging from tech-savvy urban citizens to individuals with limited digital literacy in rural areas. The UI must be intuitive, multilingual, and adhere to accessibility standards. Additionally, the system serves **developers and technical integrators** who require clear API documentation, SDKs, and extension mechanisms to build on top of the PHR platform.

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

**3.3. Developer API Module**

- **3.3.1 REST API Endpoints:** The system shall expose comprehensive REST APIs for:
    - ABHA authentication and user verification
    - Consent request and management
    - Health record retrieval (with patient consent)
    - Health record submission
    - Webhook registration and management
- **3.3.2 API Documentation:** The system shall provide OpenAPI/Swagger documentation with interactive testing capabilities.
- **3.3.3 API Versioning:** All APIs shall be versioned to ensure backward compatibility.
- **3.3.4 Rate Limiting:** The system shall implement configurable rate limiting per API key/tenant.
- **3.3.5 Webhook System:** The system shall support webhook registration for events including:
    - Consent granted/revoked
    - New health record added
    - ABHA profile updated
- **3.3.6 SDK Support:** The system shall provide client SDKs for common languages (JavaScript, Python, Java).

**3.4. Plugin/Extension System**

- **3.4.1 Plugin Architecture:** The system shall support a modular plugin architecture allowing third-party developers to extend functionality without modifying core code.
- **3.4.2 Plugin Types:** The system shall support plugins for:
    - Custom data sources (HIS/EHR connectors)
    - Custom workflows (teleconsultation, insurance claims)
    - Analytics and reporting modules
    - Integration adapters (lab systems, pharmacy systems)
- **3.4.3 Plugin Registry:** The system shall maintain a registry of installed plugins with version management.
- **3.4.4 Plugin Isolation:** Plugins shall run in isolated contexts to prevent interference with core functionality.

**3.5. Deployment & Operations**

- **3.5.1 Self-Hosting:** The system shall be deployable on-premises or in private cloud environments.
- **3.5.2 Container Support:** The system shall provide Docker images and Docker Compose configurations.
- **3.5.3 Orchestration:** The system shall provide Kubernetes manifests for production deployments.
- **3.5.4 Configuration Management:** The system shall support environment-based configuration via files and environment variables.
- **3.5.5 Monitoring:** The system shall expose health check endpoints and metrics for monitoring tools.

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
- APIs shall follow REST principles and use standard HTTP methods.
- The system shall support standard authentication mechanisms (OAuth 2.0, JWT).

**4.5. Extensibility**

- The plugin system shall allow third-party extensions without requiring core code modifications.
- APIs shall be stable and versioned to prevent breaking changes for integrators.
- The system shall provide clear extension points and hooks for customization.

**4.6. Developer Experience**

- API documentation shall be comprehensive, with examples for common use cases.
- The system shall provide sandbox environments for testing integrations.
- Error messages shall be clear and actionable for developers.
- The codebase shall follow consistent coding standards and include inline documentation.

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
    - **API:** RESTful APIs compliant with the FHIR standard, documented with OpenAPI/Swagger.
- **Database:** The system will employ a **polyglot persistence** strategy.
    - **Central Registry:** **PostgreSQL** will be used for its ACID compliance to manage user identities, consents, and audit logs.
    - **Health Data Stores (Both Tiers):** **MongoDB** will be the database of choice for its flexibility in storing complex, semi-structured HL7 FHIR resources.
- **Standards:** HL7 FHIR R4, SNOMED CT, LOINC.
- **Deployment:**
    - **Containerization:** Docker for packaging all services.
    - **Orchestration:** Kubernetes for production-grade deployments.
    - **Infrastructure as Code:** Terraform/Ansible templates for automated provisioning.
- **API Gateway:** For routing, rate limiting, and API key management.
- **Message Queue:** For asynchronous processing and webhook delivery (e.g., RabbitMQ, Kafka).

### 6. Open-Core Model Implementation

**6.1. Community Edition (Open Source)**
The following components shall be open-source under a permissive license (Apache 2.0 or MIT):
- Core PHR engine (patient records, consent management)
- ABDM/ABHA integration layer
- Basic REST APIs
- Standard UI components
- Self-hosting deployment scripts
- Basic documentation

**6.2. Enterprise Edition (Proprietary)**
The following features shall be available only in the paid enterprise edition:
- Advanced multi-tenant management console
- Enterprise-grade audit and compliance dashboards
- Advanced analytics and reporting
- Premium integrations (HIS/EHR, insurance, lab/pharmacy hubs)
- Priority support and SLAs
- Advanced security features (SSO, LDAP integration)

**6.3. Licensing Strategy**
- Community edition: Apache 2.0 or MIT license
- Enterprise edition: Commercial license with per-tenant or per-user pricing
- Plugin marketplace: Developers choose their own licensing for plugins


