**Application Architecture:**
1. Microservice Architecture:

    + Config Servers: Centralized configuration management.
    + Gateway Servers: Routing and API management.
    + Service Discovery Servers: Registration and lookup of services.
2. Logging Management:

    + Centralized Logging Service: Aggregation and analysis of application logs.
    + Log Storage: Storage for logs with appropriate retention policies.

**DevSecOps Tools:**
1. CI (Continuous Integration):

    + Tool (e.g., Azure DevOps, Jenkins): Automate builds and tests on code commits.
    + Unit Tests, Integration Tests: Part of CI pipelines for quality checks.

2. Code Quality:

    + Static Code Analysis Tools + (e.g., SonarQube): 
    Identify and fix code quality issues.
    + Code Review Processes: Incorporate peer reviews in CI pipelines.

3. Artifacts Server:

    + Artifact Repository (e.g., Azure Artifacts, Nexus): 
Store build artifacts and dependencies.

4. Security Check:

    +  Static Application Security Testing (SAST), Dynamic Application Security Testing (DAST): Scanning for vulnerabilities.
    + Dependency Scanning: Identifying and patching vulnerable dependencies.
5. CD (Continuous Delivery/Deployment):

    + Deployment Orchestration (e.g., Azure Pipelines, GitLab CI/CD): Automated deployment pipelines.
    + Manual Approval Gates: Ensuring controlled releases in the deployment process.


## Architecture
**Baseline**
![alt image](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/containers/aks-microservices/images/aks.svg)

**Workflow**

The architecture consists of the following components.

1. Azure Kubernetes Service (AKS). AKS is a managed Kubernetes cluster hosted in the Azure cloud. Azure manages the Kubernetes API service, and you only need to manage the agent nodes.

2. Virtual network. By default, AKS creates a virtual network into which agent nodes are connected. You can create the virtual network first for more advanced scenarios, which lets you control things like subnet configuration, on-premises connectivity, and IP addressing. For more information, see Configure advanced networking in Azure Kubernetes Service (AKS).

    + Ingress. An ingress server exposes HTTP(S) routes to services inside the cluster. For more information, see the section API Gateway below.

    + Azure Load Balancer. After creating an AKS cluster, the cluster is ready to use the load balancer. Then, once the NGINX service is deployed, the load balancer will be configured with a new public IP that will front your ingress controller. This way, the load balancer routes internet traffic to the ingress.

3. External data stores. Microservices are typically stateless and write state to external data stores, such as Azure SQL Database or Azure Cosmos DB.

4. Microsoft Entra ID. AKS uses a Microsoft Entra identity to create and manage other Azure resources such as Azure load balancers. Microsoft Entra ID is also recommended for user authentication in client applications.

5. Azure Container Registry. Use Container Registry to store private Docker images, which are deployed to the cluster. AKS can authenticate with Container Registry using its Microsoft Entra identity. AKS doesn't require Azure Container Registry. You can use other container registries, such as Docker Hub. Just ensure your container registry matches or exceeds the service level agreement (SLA) for your workload.

6. Azure Pipelines. Azure Pipelines are part of the Azure DevOps Services and run automated builds, tests, and deployments. You can also use third-party CI/CD solutions such as Jenkins.

7. Helm. Helm is a package manager for Kubernetes, a way to bundle and generalize Kubernetes objects into a single unit that can be published, deployed, versioned, and updated.

8. Azure Monitor. Azure Monitor collects and stores metrics and logs, application telemetry, and platform metrics for the Azure services. Use this data to monitor the application, set up alerts, dashboards, and perform root cause analysis of failures. Azure Monitor integrates with AKS to collect metrics from controllers, nodes, and containers.

**Deployment Workflow**
![alt text](https://learn.microsoft.com/en-us/azure/architecture/guide/aks/media/aks-cicd-azure-pipelines-architecture.svg#lightbox)


**Application Release Pipeline & Jobs**
![alt text](https://miro.medium.com/v2/resize:fit:828/format:webp/1*KarJfifaVtnaR6PDyiEb-A.jpeg)

**Security Scanning**

![alt text](https://res.cloudinary.com/practicaldev/image/fetch/s--ANE7aULC--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_800/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cxy0j26mqjn17vqwgqyw.png)