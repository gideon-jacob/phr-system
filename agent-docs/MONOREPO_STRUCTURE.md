# Monorepo High-Level Structure

This document outlines the proposed structure for the National PHR System monorepo. It serves as the single source of truth for the project's codebase organization.

## 1. Root Directory Structure

```text
/
├── apps/                   # Deployable applications
│   ├── patient-web/        # Patient PWA (React + Vite + Redux)
│   ├── provider-web/       # Provider Gateway (React + Vite + Redux)
│   ├── api-gateway/        # Spring Cloud Gateway (Entry Point)
│   ├── central-registry/   # Central Registry Service (Spring Boot)
│   ├── fiduciary-shared-service/    # Multi-Tenant Health Data Service (Spring Boot)
│   └── fiduciary-dedicated-service/ # Single-Tenant Enterprise Node (Spring Boot)
│
├── packages/               # Shared libraries and modules
│   ├── ui-kit/             # Shared React UI components (Tailwind)
│   ├── tech-utils/         # Common TypeScript utilities
│   ├── fhir-common/        # Shared Java lib for FHIR models & validation
│   ├── security-common/    # Shared Java lib for Auth (JWT/Keycloak Adapters)
│   └── health-service-common/ # Shared Business Logic (CRUD, Mongo, base controllers)
│
├── infrastructure/         # Infrastructure as Code (IaC) & Config
│   ├── docker/             # Local development setup
│   │   ├── services/
│   │   │   ├── keycloak/   # Local Keycloak config/theme
│   │   │   └── mongo/      # Local Mongo init scripts
│   │   └── docker-compose.yml
│   ├── terraform/          # AWS Infrastructure provisioning
│   │   ├── modules/        # Reusable modules (EKS, RDS, DocDB, VPC)
│   │   └── environments/   # Per-env configs (dev, prod)
│   └── k8s/                # Kubernetes manifests / Helm Charts
│       ├── system/         # Keycloak, Ingress Controller, CertManager
│       └── services/       # Helm charts for apps/*
│
├── tools/                  # Build scripts, CI/CD templates
│   ├── jenkins/            # Jenkins Pipeline Scripts
│   │   ├── pipelines/      # Independent pipeline files per service
│   │   └── shared-lib/     # Shared Jenkins Groovy libraries
│   └── scripts/            # Helper scripts (db-seed, lint-all)
│
├── docs/                   # Project documentation
│
└── README.md
```

## 2. Applications (`/apps`)

### 2.1. Client-Side (Frontend)
*   **patient-web**:
    *   **Stack**: React.js (v18+), Vite, Redux Toolkit, Tailwind CSS.
    *   **Deployment**: AWS S3 + CloudFront.
*   **provider-web**:
    *   **Stack**: React.js (v18+), Vite, Redux Toolkit, Tailwind CSS.
    *   **Deployment**: AWS S3 + CloudFront.

### 2.2. Server-Side (Backend)
*   **api-gateway**:
    *   **Stack**: Java (Spring Boot), Spring Cloud Gateway.
    *   **Role**: Entry point behind ALB. Handles Routing, Rate Limiting, and Auth Token Validation.
*   **central-registry**:
    *   **Stack**: Java (Spring Boot), PostgreSQL.
    *   **Role**: Identity mapping, Consent Ledger.
*   **fiduciary-dedicated-service** (Enterprise Hospital Node):
    *   **Stack**: Java (Spring Boot), MongoDB.
    *   **Core**: Extends `health-service-common`.
    *   **Target**: Large Hospitals (e.g., Apollo, Fortis).
    *   **Tenancy**: **Single-Tenant / Dedicated DB**.
*   **fiduciary-shared-service** (Small Clinic SaaS):
    *   **Stack**: Java (Spring Boot), MongoDB.
    *   **Core**: Extends `health-service-common`.
    *   **Target**: Small Clinics (e.g., Dr. Sharma).
    *   **Tenancy**: **Multi-Tenant / Shared DB**.

## 3. Infrastructure & DevOps

### 3.1. Authentication & Identity
*   **Provider**: **Keycloak** (Self-Hosted on EKS).
*   **Integration**: OIDC/OAuth2.
*   **Storage**: Dedicated PostgreSQL DB for Keycloak.

### 3.2. Networking & Traffic
*   **Ingress**: AWS ALB -> Ingress Controller -> **api-gateway** Service (Port 80/443).
*   **Internal**: Service-to-Service communication via K8s ClusterIP (possibly using Service Mesh or Feign Client).

### 3.3. Infrastructure as Code (IaC)
*   **Tool**: Terraform.
*   **Target**: AWS.
*   **Resources**: EKS, RDS (Postgres), DocumentDB (Mongo), ElastiCache (Redis for Gateway Ratelimit), S3.

### 3.4. CI/CD Strategy
*   **Tool**: Jenkins.
*   **Pipelines**: Independent pipelines located in `tools/jenkins/pipelines/`.
*   **Artifacts**: Docker Images (ECR), Static Assets (S3).

## 4. Shared Libraries (`/packages`)

*   **security-common**: Contains Keycloak adapters, Spring Security configs, and JWT parsing logic to be used by all microservices.
