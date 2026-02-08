### **Skill: AI-Assisted DevOps for Kubernetes**

#### **Purpose**

To define the standards and practices for using a suite of AI-powered tools (Gordon, `kubectl-ai`, `kagent`) to deploy, manage, and monitor the Todo Chatbot application on a local Minikube cluster. This skill emphasizes a spec-driven approach where all instructions are actionable by AI agents.

#### **Capabilities**

An engineer with this skill can:

*   Utilize Gordon AI to intelligently build, tag, run, and optimize Docker images for both frontend and backend applications.
*   Employ `kubectl-ai` to perform Kubernetes operations such as deploying pods and services, scaling applications, and debugging failing pods using natural language commands.
*   Use `kagent` for AI-driven analysis of cluster health, monitoring resource usage, and receiving optimization recommendations.
*   Execute a fully spec-driven, AI-assisted deployment workflow, from containerization to cluster management, with no manual steps.
*   Manage the application lifecycle within a local Minikube development context using these AI tools.

#### **Best Practices**

*   **Spec-Driven Commands:** All interactions with AI agents MUST be driven by clear, unambiguous instructions derived from specifications or technical plans. Avoid ad-hoc manual commands to ensure reproducibility.
*   **Verify AI Actions:** While AI agents automate tasks, their outcomes MUST be verified with subsequent commands. For example, after `kubectl-ai` deploys a service, a follow-up command should confirm the service is running and configured correctly.
*   **Context is Key:** Provide sufficient context to the AI agents. For `kubectl-ai`, this means specifying namespaces, deployment names, and desired states. For Gordon, it means providing the correct application source directory.
*   **Iterative Optimization:** Use the insights from `kagent` and Gordon to iteratively improve resource allocations in Helm charts and optimize Dockerfiles.
*   **Local Focus (Minikube):** Tailor commands for a Minikube environment. This includes using `minikube image load` to make local Docker images available to the cluster, avoiding the need for a remote registry.

---

### **AI Agent Command Examples**

#### **Gordon AI (Docker Operations)**

*   **Task:** Build a Docker image for the backend.
    *   **Command:** `gordon build --app-dir ./backend --image-name todo-backend:v1.0.0`
    *   **Expected Outcome:** Gordon analyzes the backend source code, generates an optimized Dockerfile (if one doesn't exist), builds the Docker image, and tags it as `todo-backend:v1.0.0`.

*   **Task:** Optimize an existing Docker image.
    *   **Command:** `gordon optimize --image todo-backend:v1.0.0`
    *   **Expected Outcome:** Gordon analyzes the image and provides specific recommendations for improvement, such as using a smaller base image, re-ordering layers to improve caching, or identifying potential security vulnerabilities.

*   **Task:** Make the local image available to Minikube.
    *   **Command:** `minikube image load todo-backend:v1.0.0`
    *   **Expected Outcome:** The `todo-backend:v1.0.0` image is loaded into the Minikube cluster's internal Docker daemon, making it available for deployments.

#### **kubectl-ai (Kubernetes Management)**

*   **Task:** Deploy an application from a local image.
    *   **Command:** `kubectl ai "deploy the image todo-frontend:v1.0.0 as a deployment named frontend with 3 replicas, ensuring imagePullPolicy is set to Never"`
    *   **Expected Outcome:** `kubectl-ai` generates and applies the Kubernetes YAML for a Deployment resource. The resulting pods will use the local `todo-frontend:v1.0.0` image.

*   **Task:** Scale an existing deployment.
    *   **Command:** `kubectl ai "scale the frontend deployment to 5 replicas"`
    *   **Expected Outcome:** The number of pods in the `frontend` deployment is increased from 3 to 5. `kubectl` will report `deployment.apps/frontend scaled`.

*   **Task:** Debug a failing pod.
    *   **Command:** `kubectl ai "why is the pod backend-deployment-xyz-12345 crashing?"`
    *   **Expected Outcome:** `kubectl-ai` analyzes the pod's logs, events, and configuration, then provides a human-readable summary of the likely cause of the crash loop (e.g., "The pod is in a crash loop due to a configuration error: secret 'db-credentials' not found.").

#### **Kagent (AI-Driven Cluster Analysis)**

*   **Task:** Get a health overview of a namespace.
    *   **Command:** `kagent analyze --namespace default --output summary`
    *   **Expected Outcome:** `kagent` provides a concise health summary of the `default` namespace, highlighting any pods with high resource usage, excessive restarts, or other anomalous behavior.

*   **Task:** Recommend resource allocation changes.
    *   **Command:** `kagent optimize-resources --deployment backend`
    *   **Expected Outcome:** `kagent` analyzes the historical resource usage of the `backend` deployment and recommends updated CPU and memory requests/limits (e.g., "Recommendation for deployment 'backend': set cpu request to 150m and memory limit to 256Mi to improve efficiency.").
