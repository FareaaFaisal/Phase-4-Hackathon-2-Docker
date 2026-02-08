# Tasks: Application Deployment Modernization

**Input**: Design documents from `/specs/004-k8s-deployment/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/, quickstart.md

**Tests**: Test tasks are included as part of the verification process.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Phase 1: Setup (Project Initialization)

**Purpose**: General setup tasks and environment preparation for Minikube and core tools.

- [ ] T001 Install Minikube and its prerequisites (Docker, kubectl, Helm).
- [ ] T002 Start Minikube cluster using `minikube start --driver=docker --memory=4096mb --cpus=2 --disk=20g`.
- [ ] T003 Configure `kubectl` and Helm to use Minikube context using `kubectl config use-context minikube`.

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Create core infrastructure components before any user story implementation.

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

- [ ] T004 Create `helm/` directory at repository root.
- [ ] T005 Create `.gordonai/` directory at repository root.
- [ ] T006 Create `.kubectl-ai/` directory at repository root.
- [ ] T007 Create `.kagent/` directory at repository root.

**Checkpoint**: Foundation ready - user story implementation can now begin in parallel

---

## Phase 3: User Story 1 - Package Application for Consistent Deployment (Priority: P1) 🎯 MVP

**Goal**: The application's components (frontend and backend) are packaged into standardized, isolated units.

**Independent Test**: The frontend and backend packages can be created and run locally, demonstrating that they contain all necessary dependencies to function in isolation.

### Implementation for User Story 1

- [ ] T008 [US1] Create Dockerfile for backend application in `backend/Dockerfile`.
- [ ] T009 [P] [US1] Build backend Docker image `todo-backend:latest` using `docker build -t todo-backend:latest ./backend`.
- [ ] T010 [P] [US1] Load backend Docker image `todo-backend:latest` into Minikube using `minikube image load todo-backend:latest`.
- [ ] T011 [US1] Create Dockerfile for frontend application in `frontend/Dockerfile`.
- [ ] T012 [P] [US1] Build frontend Docker image `todo-frontend:latest` using `docker build -t todo-frontend:latest ./frontend`.
- [ ] T013 [P] [US1] Load frontend Docker image `todo-frontend:latest` into Minikube using `minikube image load todo-frontend:latest`.
- [ ] T014 [US1] Verify backend Docker image starts locally using `docker run --rm -p 8000:8000 todo-backend:latest`.
- [ ] T015 [US1] Verify frontend Docker image starts locally using `docker run --rm -p 3000:3000 todo-frontend:latest`.

**Checkpoint**: At this point, User Story 1 should be fully functional and testable independently

---

## Phase 4: User Story 2 - Orchestrate Application Deployment (Priority: P2)

**Goal**: Deploy and manage the packaged application units in an automated, orchestrated environment.

**Independent Test**: The packaged units can be deployed to a local orchestration platform, and the platform reports them as running and healthy.

### Implementation for User Story 2

- [ ] T016 [US2] Create Helm chart for backend application in `helm/backend/`.
- [ ] T017 [P] [US2] Create Helm chart for frontend application in `helm/frontend/`.
- [ ] T018 [US2] Deploy backend using Helm chart with `helm install todo-backend ./helm/backend`.
- [ ] T019 [US2] Deploy frontend using Helm chart with `helm install todo-frontend ./helm/frontend`.
- [ ] T020 [US2] Enable Minikube Ingress addon using `minikube addons enable ingress`.
- [ ] T021 [US2] Verify backend and frontend deployments are running and healthy using `kubectl get deployments` and `kubectl get services`.

**Checkpoint**: At this point, User Stories 1 AND 2 should both work independently

---

## Phase 5: User Story 3 - Manage Deployment as Code (Priority: P3)

**Goal**: The entire deployment configuration is defined declaratively and stored in version control.

**Independent Test**: The entire application can be deployed to the orchestration platform using only the configuration files from the repository.

### Implementation for User Story 3

- [ ] T022 [US3] Access frontend application via Ingress URL using `minikube ingress list` to get URL.
- [ ] T023 [US3] Perform functional validation of the Todo Chatbot (create, read, update, delete tasks).
- [ ] T024 [US3] Use `kubectl-ai` to verify deployment status and troubleshoot (e.g., `kubectl ai "show all pods"`).
- [ ] T025 [US3] Use `kagent` for AI-driven resource optimization recommendations (e.g., `kagent optimize-resources --deployment todo-backend`).

**Checkpoint**: All user stories should now be independently functional

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories and documentation.

- [ ] T026 Populate `quickstart.md` with deployment instructions.
- [ ] T027 Document architectural decisions from `plan.md` in `history/adr/` (e.g., Docker Image Strategy, Replica Strategy, Helm Chart Structure, Service Exposure, AI-Agent Usage).
- [ ] T028 Update `README.md` with Phase IV deployment instructions and links to quickstart.
- [ ] T029 Clean up temporary files or unused configurations.

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Stories (Phase 3+)**: All depend on Foundational phase completion
  - User stories can then proceed in parallel (if staffed)
  - Or sequentially in priority order (P1 → P2 → P3)
- **Polish (Final Phase)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) - No dependencies on other stories
- **User Story 2 (P2)**: Can start after Foundational (Phase 2) - May integrate with US1 but should be independently testable
- **User Story 3 (P3)**: Can start after Foundational (Phase 2) - May integrate with US1/US2 but should be independently testable

### Within Each User Story

- Core implementation before verification.
- Tasks involving file creation/modification before commands that use those files.

### Parallel Opportunities

- Tasks T009, T010 can run in parallel with T012, T013.
- Tasks T005, T006, T007 can run in parallel.
- Tasks T016, T017 can run in parallel.
- Once Foundational phase completes, all user stories can start in parallel (if team capacity allows).

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1.  Complete Phase 1: Setup
2.  Complete Phase 2: Foundational (CRITICAL - blocks all stories)
3.  Complete Phase 3: User Story 1
4.  **STOP and VALIDATE**: Test User Story 1 independently
5.  Deploy/demo if ready

### Incremental Delivery

1.  Complete Setup + Foundational → Foundation ready
2.  Add User Story 1 → Test independently → Deploy/Demo (MVP!)
3.  Add User Story 2 → Test independently → Deploy/Demo
4.  Add User Story 3 → Test independently → Deploy/Demo
5.  Each story adds value without breaking previous stories

### Parallel Team Strategy

With multiple developers:

1.  Team completes Setup + Foundational together
2.  Once Foundational is done:
    -   Developer A: User Story 1
    -   Developer B: User Story 2
    -   Developer C: User Story 3
3.  Stories complete and integrate independently

---

## Notes

-   [P] tasks = different files, no dependencies
-   [Story] label maps task to specific user story for traceability
-   Each user story should be independently completable and testable
-   Verify tests fail before implementing
-   Commit after each task or logical group
-   Stop at any checkpoint to validate story independently
-   Avoid: vague tasks, same file conflicts, cross-story dependencies that break independence
