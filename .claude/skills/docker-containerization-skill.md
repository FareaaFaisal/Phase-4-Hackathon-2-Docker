### **Skill: Docker Containerization**

#### **Purpose**

To containerize the frontend and backend applications using Docker, with a focus on leveraging Gordon AI for assisted Docker commands, ensuring portable and reproducible application environments.

#### **Capabilities**

An engineer with this skill can:

*   Create optimized Dockerfiles for both frontend (e.g., Next.js) and backend (e.g., FastAPI) applications.
*   Build and tag Docker images for various environments and versions.
*   Push Docker images to a specified container registry (e.g., local Minikube registry, Docker Hub, or other cloud registries).
*   Utilize Gordon AI for generating or optimizing Dockerfiles, suggesting best practices, and assisting with Docker commands.
*   Manage multi-stage Docker builds to create smaller and more secure images.
*   Ensure environment variables are correctly injected into containers at runtime.
*   Handle sensitive information securely by integrating with container orchestration secrets mechanisms.
*   Perform basic container runtime operations (start, stop, remove, inspect).
*   Implement container health checks (e.g., `HEALTHCHECK` instruction in Dockerfile).

#### **Best Practices**

*   **Multi-Stage Builds:** Always use multi-stage Dockerfiles to separate build-time dependencies from runtime dependencies, resulting in smaller, more efficient, and more secure images.
*   **`.dockerignore`:** Utilize `.dockerignore` files to exclude unnecessary files and directories (e.g., `node_modules`, `.git`, temporary files) from the build context, significantly speeding up builds and reducing image size.
*   **Image Optimization:** Follow best practices for Docker image optimization, such as choosing appropriate slim base images, consolidating `RUN` commands to reduce layers, and cleaning up build artifacts.
*   **Non-Root Users:** Run container processes as non-root users (`USER` instruction) to enhance security and minimize potential attack surfaces.
*   **Environment Variables:** Inject configuration through environment variables rather than baking them into the image. For sensitive data, use container orchestration secrets management (e.g., Kubernetes Secrets).
*   **Liveness/Readiness Checks:** Prepare applications for health checks within containers by exposing appropriate endpoints and configuring `HEALTHCHECK` instructions in Dockerfiles.
*   **Gordon AI Integration:** Leverage Gordon AI to automate repetitive Docker tasks, suggest Dockerfile improvements, perform image vulnerability scanning, and provide recommendations for image optimization.

#### **File Structure**

A standardized file structure where Dockerfiles reside within their respective service directories.

```
/
├── backend/
│   ├── Dockerfile             # Dockerfile for the backend application
│   └── .dockerignore          # Files to ignore during backend image build
├── frontend/
│   ├── Dockerfile             # Dockerfile for the frontend application
│   └── .dockerignore          # Files to ignore during frontend image build
└── .gordonai/                 # (Optional) Configuration or scripts specific to Gordon AI
    └── config.yaml
```

#### **Common Patterns**

*   **Standardized Dockerfile Templates:** Maintaining a set of standardized Dockerfile templates for different types of applications (e.g., Node.js, Python FastAPI) to ensure consistency and accelerate development.
*   **Automated Image Builds:** Integrating Docker image builds into CI/CD pipelines, triggered by code changes in the application repositories.
*   **Local Registry Usage:** Pushing images to a local Docker registry (e.g., Minikube's built-in registry) for seamless integration with local Kubernetes development workflows.
*   **Versioned Images:** Tagging Docker images with meaningful version numbers (e.g., `v1.0.0`, `git-commit-sha`) and environment indicators (e.g., `latest`, `dev`, `staging`).
