### **Skill: Helm Chart Development**

#### **Purpose**

To create reusable Helm charts for deploying applications to Kubernetes, focusing on Helm templating and values management, ensuring consistent and reproducible deployments.

#### **Capabilities**

An engineer with this skill can:

*   Design and implement Helm charts for Kubernetes deployments.
*   Define templates for Kubernetes resources such as Deployments, Services, ConfigMaps, and Secrets.
*   Parameterize Helm charts to allow configuration of replicas, image tags, environment variables, and other deployment-specific values.
*   Manage chart dependencies and subcharts effectively.
*   Utilize `helm install`, `helm upgrade`, `helm rollback`, and `helm uninstall` commands for application lifecycle management.
*   Ensure Helm charts are modular and reusable for different application components (e.g., frontend, backend).
*   Implement best practices for Helm chart structure and organization.

#### **Best Practices**

*   **Modularity:** Design charts to be modular, allowing for easy reuse and maintenance. Create separate charts for independent components like frontend and backend.
*   **Parameterization:** Externalize all configurable values into `values.yaml` files. Avoid hardcoding values directly within templates.
*   **Templating:** Use Helm's templating language effectively for dynamic resource generation, including `_helpers.tpl` for common logic and named templates.
*   **Version Control:** Keep Helm charts under version control alongside application code to ensure consistency and traceability.
*   **Security:** Handle sensitive information securely by using Kubernetes Secrets, managed via Helm (e.g., using `helm secrets` or integrating with external secrets management solutions). Avoid storing sensitive data directly in `values.yaml` or in chart templates.
*   **Testing:** Write chart tests to ensure that templates render correctly and deploy as expected, and to validate chart functionality.
*   **Documentation:** Provide clear and comprehensive `README.md` files for each chart, explaining its purpose, configurable values, and usage.

#### **File Structure**

A standardized file structure for Helm charts should be followed.

```
/charts
├── my-app/                 # Root directory for a specific application's chart
│   ├── Chart.yaml          # A YAML file containing information about the chart
│   ├── values.yaml         # The default configuration values for this chart
│   ├── templates/          # Directory of templates that will be rendered into Kubernetes manifests
│   │   ├── _helpers.tpl    # Contains reusable template snippets/partials
│   │   ├── deployment.yaml # Kubernetes Deployment resource definition
│   │   ├── service.yaml    # Kubernetes Service resource definition
│   │   ├── configmap.yaml  # Kubernetes ConfigMap resource definition
│   │   └── secret.yaml     # Kubernetes Secret resource definition
│   └── Chart.lock          # (Optional) Records dependencies for reproducible builds
```

#### **Common Patterns**

*   **`_helpers.tpl` for Reusable Logic:** Using `_helpers.tpl` to define common labels, names, and other helper functions that can be reused across multiple templates within a chart. This promotes DRY (Don't Repeat Yourself) principles.
*   **Environment-Specific Values:** Managing different deployment environments (dev, staging, prod) using separate `values.yaml` files or `--values` flag with `helm install`/`upgrade` commands, allowing environment-specific overrides.
*   **Conditional Resources:** Using `if` statements in templates to conditionally include or exclude Kubernetes resources based on `values.yaml` settings, enabling flexible chart configurations.
*   **Image Pull Policy:** Configuring `imagePullPolicy` (e.g., `Always`, `IfNotPresent`) based on deployment environment and image tag strategy.
