# Quickstart Guide: Local Kubernetes Deployment for Todo Chatbot

This guide provides step-by-step instructions for setting up and deploying the Todo Chatbot application on a local Minikube Kubernetes cluster.

## 1. Prerequisites

Ensure you have the following tools installed on your system:

*   **Minikube:** Local Kubernetes cluster.
    *   Installation: Follow official Minikube documentation for your OS.
*   **Docker:** Containerization platform (Minikube's default driver).
    *   Installation: Follow official Docker documentation.
*   **`kubectl`:** Kubernetes command-line tool.
    *   Installation: `minikube kubectl -- get po` will download and configure it.
*   **Helm:** Kubernetes package manager.
    *   Installation: Follow official Helm documentation.
*   **Gordon AI:** Docker AI Agent (Optional, but recommended for AI-assisted Docker operations).
    *   Installation: Refer to Gordon AI documentation.
*   **`kubectl-ai`:** AI-powered `kubectl` plugin (Optional, but recommended for AI-assisted K8s operations).
    *   Installation: Refer to `kubectl-ai` documentation.
*   **Kagent:** AI-driven cluster analysis tool (Optional, but recommended for AI-driven insights).
    *   Installation: Refer to Kagent documentation.

## 2. Minikube Cluster Setup

Start your Minikube cluster with appropriate resources. It's recommended to use the Docker driver for simplicity.

```bash
minikube start --driver=docker --memory=4096mb --cpus=2 --disk=20g
```

Verify that `kubectl` is configured to use the Minikube context:

```bash
kubectl config use-context minikube
kubectl get nodes
```

## 3. Application Containerization

You need to build Docker images for both the backend and frontend applications. Then, load these images into Minikube's Docker daemon.

### 3.1. Build Backend Image

Navigate to the `backend/` directory and build the Docker image.

```bash
cd backend
docker build -t todo-backend:latest .
cd ..
```

*Optional: Use Gordon AI for assisted build:*
```bash
gordon build --app-dir ./backend --image-name todo-backend:latest
```

### 3.2. Build Frontend Image

Navigate to the `frontend/` directory and build the Docker image.

```bash
cd frontend
docker build -t todo-frontend:latest .
cd ..
```

*Optional: Use Gordon AI for assisted build:*
```bash
gordon build --app-dir ./frontend --image-name todo-frontend:latest
```

### 3.3. Load Images into Minikube

Make the built images available to your Minikube cluster.

```bash
minikube image load todo-backend:latest
minikube image load todo-frontend:latest
```

## 4. Helm Chart Deployment

Deploy the backend and frontend applications using their respective Helm charts located in the `helm/` directory.

### 4.1. Deploy Backend

```bash
helm install todo-backend ./helm/backend
```

### 4.2. Deploy Frontend

```bash
helm install todo-frontend ./helm/frontend
```

## 5. Accessing the Application

The frontend application is exposed via an Ingress. First, enable the Ingress addon in Minikube:

```bash
minikube addons enable ingress
```

Then, get the URL for the Ingress:

```bash
minikube ingress list
```
Access the application by navigating to the URL provided by the `minikube ingress list` command in your web browser.

## 6. Basic Verification

Verify that your pods, deployments, and services are running as expected.

```bash
kubectl get pods
kubectl get deployments
kubectl get services
kubectl get ingress
```

*Optional: Use `kubectl-ai` for verification:*
```bash
kubectl ai "show me the status of all deployments in the default namespace"
kubectl ai "are there any pods in a crashloopbackoff state?"
```

## 7. Basic AI-Assisted Operations (Optional)

Explore how to use `kubectl-ai` and `kagent` for basic cluster management and health checks.

### 7.1. Check Cluster Health with Kagent

```bash
kagent analyze --namespace default --output summary
```

### 7.2. Debug with kubectl-ai

If a pod is failing, `kubectl-ai` can assist:
```bash
kubectl ai "why is the pod <pod-name> crashing?"
```

---
**Note:** This guide assumes default configurations. For advanced settings or troubleshooting, refer to the official documentation of Minikube, Docker, Helm, Gordon AI, `kubectl-ai`, and Kagent.
