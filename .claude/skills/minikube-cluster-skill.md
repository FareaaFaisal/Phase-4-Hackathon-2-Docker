### **Skill: Minikube Local Kubernetes Cluster Management**

#### **Purpose**

To define the procedures and best practices for installing, configuring, and managing a local Kubernetes cluster using Minikube for the Todo Chatbot project, enabling efficient development and testing of Kubernetes deployments. This skill ensures that Minikube operations are spec-driven and interpretable by AI agents.

#### **Capabilities**

An engineer with this skill can:

*   Install and configure Minikube and its prerequisites (Docker/Podman, `kubectl`, `helm`) on a local development machine.
*   Start and stop Minikube clusters with specified configurations (e.g., driver, memory, CPU).
*   Configure `kubectl` and Helm to interact seamlessly with the Minikube cluster context.
*   Deploy containerized applications (frontend and backend) to Minikube using Helm charts.
*   Access deployed services from the host machine using various exposure methods like NodePort, LoadBalancer, and Ingress.
*   Verify the status and health of Kubernetes pods, deployments, and services within the Minikube cluster.
*   Execute commands for debugging and inspecting local cluster resources (e.g., viewing logs, events, resource descriptions).
*   Follow spec-driven instructions for Minikube operations that can be interpreted and executed by AI agents.

#### **Best Practices**

*   **Driver Selection:** Choose the appropriate Minikube driver (e.g., Docker, Podman, Hyperkit, VirtualBox) based on the host operating system and local setup. The Docker driver is generally preferred for its simplicity and wide adoption.
*   **Resource Allocation:** Allocate sufficient CPU and memory to the Minikube cluster to ensure smooth operation of deployed applications and avoid resource contention. It's recommended to start with at least 2 CPUs and 4GB of memory.
*   **Context Management:** Always explicitly set the `kubectl` context to Minikube (`kubectl config use-context minikube`) to avoid accidentally operating on a different Kubernetes cluster.
*   **Service Exposure:** For local development, NodePort is often the simplest way to expose services directly. Use Ingress for more advanced routing, path-based access, and domain mapping within Minikube. Be aware that LoadBalancer services in Minikube typically require an addon like `metallb`.
*   **Version Compatibility:** Ensure that Minikube, `kubectl`, and Helm client versions are compatible with each other and the Kubernetes version provisioned by Minikube.
*   **Cleanup:** Regularly stop (`minikube stop`) and delete (`minikube delete`) Minikube clusters when not in active use to free up local machine resources.
*   **Spec-Driven Operations:** All Minikube commands and configurations should be derived from and align with project specifications and deployment plans to ensure automated and reproducible actions by AI agents.

#### **Commands Examples**

*   **Install Minikube (Illustrative, specific to OS - example for Windows):**
    *   `curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-windows-amd64.exe`
    *   `move minikube-windows-amd64.exe C:\minikube\minikube.exe` (Assuming `C:\minikube` is in PATH)

*   **Start Cluster with Docker Driver:**
    *   `minikube start --driver=docker --memory=4096mb --cpus=2 --disk=20g`

*   **Stop Cluster:**
    *   `minikube stop`

*   **Delete Cluster:**
    *   `minikube delete`

*   **Set `kubectl` Context to Minikube:**
    *   `kubectl config use-context minikube`

*   **Deploy Helm Chart:**
    *   `helm install my-app ./my-app-chart` (Assuming `./my-app-chart` is the path to your chart)

*   **Access Service via NodePort (get URL):**
    *   `minikube service <service-name> --url`

*   **Check Pod Status:**
    *   `kubectl get pods -n <namespace> -o wide`

*   **View Pod Logs:**
    *   `kubectl logs <pod-name> -n <namespace>`

*   **Describe Kubernetes Resource:**
    *   `kubectl describe deployment <deployment-name> -n <namespace>`

*   **Enable Ingress Addon:**
    *   `minikube addons enable ingress`
