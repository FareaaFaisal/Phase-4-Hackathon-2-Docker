<!--
    Sync Impact Report
    - Version change: 3.0.0 -> 4.0.0
    - Modified principles: All principles updated for Phase-4.
    - Added sections:
        - Principle: Containerization Mandate
        - Principle: Kubernetes-First Orchestration
        - Principle: Declarative GitOps with Helm
        - Principle: AI-Augmented Operations
        - Principle: Service-Based Architecture
        - Principle: Immutability of Application Code
    - Removed sections:
        - All Phase-3 principles have been superseded by Phase-4 deployment goals.
    - Templates requiring updates:
        - ⚠ pending: README.md (to add Phase-4 deployment instructions)
        - ⚠ pending: .specify/templates/plan-template.md (to reflect k8s planning)
        - ⚠ pending: .specify/templates/tasks-template.md (to include deployment tasks)
    - Follow-up TODOs: None
-->
# Phase IV – Local Kubernetes Deployment Constitution

**Version**: 4.0.0
**Ratification Date**: 2026-02-08
**Last Amended**: 2026-02-08

## Core Principles

### Containerization Mandate
**Description**: All frontend and backend services MUST be containerized using Docker. The use of AI-assisted tools like Gordon AI for Dockerfile generation and image building is preferred.
**Rationale**: To ensure a consistent and reproducible deployment environment, isolating application dependencies and simplifying the path to orchestration.

### Kubernetes-First Orchestration
**Description**: The entire application stack MUST be deployed and managed on a local Kubernetes cluster (Minikube).
**Rationale**: To build operational experience with the industry-standard container orchestrator and enable scalable, resilient deployments.

### Declarative GitOps with Helm
**Description**: All Kubernetes resources MUST be defined declaratively using Helm charts. These charts are the source of truth and MUST be versioned in the project repository.
**Rationale**: To enable automated, repeatable, and traceable deployments, treating infrastructure as code.

### AI-Augmented Operations
**Description**: Operational tasks such as cluster management, scaling, and troubleshooting SHOULD leverage AI-driven tools like `kubectl-ai` and `kagent`.
**Rationale**: To accelerate operational workflows, automate complex tasks, and gain deeper insights into the cluster's state and performance.

### Service-Based Architecture
**Description**: Communication between the frontend and backend pods MUST be managed via Kubernetes Services and Ingress to ensure reliable service discovery and routing within the cluster.
**Rationale**: To decouple services and create a scalable, resilient microservices architecture that is native to Kubernetes.

### Immutability of Application Code
**Description**: The existing Phase III application source code for the frontend and backend MUST NOT be modified. This phase is strictly focused on packaging and deploying the existing application.
**Rationale**: To isolate the scope of work to infrastructure and deployment, preventing the introduction of application-level bugs and ensuring a stable target for containerization.

## Key Standards

- **Local Cluster**: Minikube
- **Containerization**: Docker
- **Helm Chart Structure**: Separate charts for `frontend` and `backend`.
- **AI Tooling**:
    - **Docker**: Gordon AI
    - **Kubernetes**: kubectl-ai, kagent
- **Networking**: Kubernetes Services and Ingress.

## Constraints

- **Local Deployment Only**: All deployments are to be on a local Minikube instance. Cloud deployment is out of scope for Phase IV.
- **No Application Code Changes**: Focus remains on the "ops" part of DevOps. Do not modify Next.js or FastAPI application logic.

## Validation & Testing Requirements

- Frontend and Backend applications must be successfully containerized.
- Helm charts must successfully deploy the application to Minikube.
- The frontend must be accessible from the host machine and successfully communicate with the backend service within the cluster.
- `kubectl-ai` and `kagent` commands must successfully interact with the deployed application and cluster.

## Success Criteria

- A complete, working deployment of the Phase III application is running on a local Minikube cluster.
- All deployment artifacts (Dockerfiles, Helm charts) are committed to the repository.
- A clear set of instructions is available for another developer to replicate the deployment.