### **Skill: Kubernetes Deployment for Todo Chatbot**

#### **Purpose**

To deploy and manage the Todo Chatbot on a local Kubernetes cluster. This skill focuses on using Minikube and Helm charts for reproducible, version-controlled deployments, including pod management, service exposure, and scaling.

#### **Capabilities**

An engineer with this skill can:

*   Containerize frontend and backend applications using Docker.
*   Create and manage Helm charts for deploying applications to Kubernetes.
*   Deploy applications to a local Minikube cluster.
*   Manage application replicas, autoscaling, and resource allocation (requests and limits).
*   Expose services to be accessible from outside the cluster using NodePort, LoadBalancer, or Ingress.
*   Perform rolling updates and rollbacks for deployments.
*   Implement and manage health checks (liveness and readiness probes).
*   Utilize AI-assisted tools (`kubectl-ai`, `kagent`) for cluster management and troubleshooting.

#### **Best Practices**

*   **Declarative Configuration:** All Kubernetes resources MUST be defined declaratively in Helm charts. Avoid manual `kubectl` commands for creating or modifying resources in a production-like workflow.
*   **Chart Reusability:** Create separate, reusable charts for the frontend and backend to allow for independent deployment and scaling.
*   **Health Checks:** All deployments MUST include liveness and readiness probes to ensure traffic is only routed to healthy pods and to allow for automatic recovery.
*   **Resource Management:** Define sensible resource requests and limits for all containers to ensure stable performance and prevent resource starvation.
*   **Rolling Updates:** Configure deployment strategies to use rolling updates to ensure zero-downtime deployments.
*   **Service Exposure:** Use ClusterIP services for internal communication and Ingress (or NodePort for local development) to expose services externally. Avoid using LoadBalancer for local Minikube deployments unless a specific metallb-like setup is in place.
*   **AI-Assisted Operations:** Use `kubectl-ai` for complex queries and troubleshooting, and `kagent` for monitoring and automated actions, where appropriate.

#### **File Structure**

A standardized file structure for Helm charts should be followed.

```
/helm
├── backend/
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
│       ├── _helpers.tpl
│       ├── deployment.yaml
│       └── service.yaml
└── frontend/
    ├── Chart.yaml
    ├── values.yaml
    └── templates/
        ├── _helpers.tpl
        ├── deployment.yaml
        ├── ingress.yaml
        └── service.yaml
```

#### **Common Patterns**

*   **Helm-based Deployment:** Using `helm install` and `helm upgrade` as the standard procedure for deploying and updating the application.
*   **Values Overrides:** Using separate `values.yaml` files or `--set` flags to manage environment-specific configurations without modifying the chart templates.
*   **Readiness Probes for Zero-Downtime:** Implementing readiness probes that check for application readiness (e.g., database connection) before a pod is marked as ready to receive traffic, ensuring smooth rolling updates.
