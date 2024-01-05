
# Azure Cloud Infrastructure Design #

**Landing Zone:**

The landing zone represents the initial environment setup where all resources will be deployed. In Azure, this is often organized using the following components:

+ Tenant: Azure Active Directory (AAD) Tenant - Represents your organization's identity and access management.

+ Management Group: Organizational structure for managing Azure resources. It helps in applying policies and governance across subscriptions.

**Sample**
![alt text](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/media/ns-arch-cust-expanded.svg#lightbox)

| Landing zone (management group) |	Purpose or use |
| --- | --- |
| Corp	| The dedicated management group for corporate landing zones. This group is for workloads that require connectivity or hybrid connectivity with the corporate network via the hub in the connectivity subscription. |
| Online |	The dedicated management group for online landing zones. This group is for workloads that might require direct internet inbound/outbound connectivity or for workloads that might not require a virtual network. |
| Sandbox	| The dedicated management group for subscriptions that will only be used for testing and exploration by an organization. These subscriptions will be securely disconnected from the corporate and online landing zones. Sandboxes also have a less restrictive set of policies assigned to enable testing, exploration, and configuration of Azure services. |

**Platform landing zone:** 
A platform landing zone is a subscription that provides shared services (identity, connectivity, management) to applications in application landing zones. Consolidating these shared services often improves operational efficiency. One or more central teams manage the platform landing zones. In the conceptual architecture (see figure 1), the "Identity subscription", "Management subscription", and "Connectivity subscription" represent three different platform landing zones. The conceptual architecture shows these three platform landing zones in detail. It depicts representative resources and policies applied to each platform landing zone.

**Application landing zone:** 
An application landing zone is a subscription for hosting an application. You pre-provision application landing zones through code and use management groups to assign policy controls to them. In the conceptual architecture (see figure 1), the "Landing zone A1 subscription" and "Landing zone A2 subscription" represent two different application landing zones. The conceptual architecture shows only the "Landing zone A2 subscription" in detail. It depicts representative resources and policies applied to the application landing zone.

**Sample** 
![alt text](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/media/alz-tailor-hierarchy-default.png)

The following diagram shows a tailored Azure landing zone hierarchy. It uses examples from the preceding diagram.

![alt text](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/media/alz-tailor-hierarchy-2-additional.png)
**Subscriptions:**

Multiple subscriptions can be created based on the needs for isolation, billing, and resource separation. For instance:

+ Connectivity Subscription: Contains networking resources like virtual networks, gateways, etc.

+ Application Subscriptions: Used for hosting applications and services, including the Managed Kubernetes cluster.

**Networking:**
Networking components are crucial for establishing connectivity between various resources. In Azure, this typically includes:

+ Virtual Network (VNET): Segmented networking environment to host resources. It could be configured with subnets for different purposes (e.g., backend, frontend, Kubernetes pods).

+ Gateway/Subnet: To connect on-premises resources or provide connectivity to the internet.

+ Load Balancers: For distributing traffic to Kubernetes nodes and other services.

**Managed Kubernetes (AKS):**
Azure Kubernetes Service (AKS) will be utilized for the managed Kubernetes solution:

+ AKS Cluster: Managed Kubernetes cluster for hosting containerized applications.

+ Node Pools: Different node pools for specific workloads or resource requirements.

**Deployment Architecture:**
+ Application Workloads: Deployed and managed within the AKS Cluster.

+ Storage Services: Utilize Azure Storage for persistent storage needs of the applications.

+ Monitoring & Logging: Incorporate Azure Monitor and Azure Log Analytics for performance monitoring and logging.

**Security & Identity:**

+ Azure Active Directory Integration: Enables identity and access management for resources.

+ Network Security Groups (NSGs): Controls inbound and outbound traffic to the resources within the VNET.

+ Azure Key Vault: For securely storing and managing sensitive information like secrets, keys, and certificates.

+ Azure Security Center: Monitors and enhances the security posture of the environment.

This is a high-level overview of the Azure cloud infrastructure design for Managed Kubernetes and associated resources.

**Application Architecture:**
**Microservice Architecture:**
+ Components:
    + Config Server:
Centralized configuration management using tools like Spring Cloud Config.

+ Gateway:
    + API Gateway for routing and managing access to microservices (e.g., Netflix Zuul, Spring Cloud Gateway).

    + Service Discovery Servers:
Utilizing tools like Netflix Eureka or Consul for service registration and discovery.

**Application Log Management:**

+ Logging Infrastructure:
    + Centralized logging utilizing ELK Stack (Elasticsearch, Logstash, Kibana) or Azure-native solutions like Azure Monitor and Log Analytics.

**DevSecOps Tools:**
+ Container Security:
    + Trivy:
        + Open-source vulnerability scanner for container images.
    + Container Registry Security:
+ ACR Defender:
    + Azure Container Registry's integrated scanning and security features.
+ Aqua:
    + Provides container security for Azure Kubernetes Service (AKS).

**Continuous Integration (CI):**
+ Azure DevOps:
    + Integrated CI/CD tool offering pipelines for building, testing, and deploying applications.

**Code Quality & Static Analysis:**
+ SonarQube:
    + Performs static code analysis to enhance code quality.
+ Checkmarx:
Application security testing for identifying vulnerabilities in the code.
    + Artifact Management:

+ Azure Artifacts:
    + Repository to store and manage application artifacts, dependencies, and packages.
**Security Checks & Compliance:**
+ Microsoft Cloud Security Benchmark:
    + Offers best practices and guidelines for securing Azure resources.
+   Security Control Baseline:
    + Implements security controls and compliance standards specific to Azure.

**Continuous Delivery/Deployment (CD):**
**Deployment Tools:**
+ Azure DevOps: 
    + Handles both CI and CD pipelines.

+ Helm & ArgoCD: 
    + Used for managing Kubernetes application deployments, especially Helm charts and GitOps-based deployments through ArgoCD.

This architecture ensures a robust, scalable, and secure microservices-based application deployment within Azure's cloud infrastructure. It integrates various DevSecOps tools for continuous monitoring, security checks, and efficient deployment processes. Each tool contributes to different phases of the software development lifecycle, aiming to ensure quality, security, and compliance.

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


![Diagram](./source/Deployment_Architecture.jpeg)


## Architecture

**AKS PCI Baseline Architecture**

![alt text](https://camo.githubusercontent.com/bff2c59f8c39ff5fdde854e92f22bf6cb8be96da065fa0c6fe8c540b5400e6b0/68747470733a2f2f6c6561726e2e6d6963726f736f66742e636f6d2f617a7572652f6172636869746563747572652f7265666572656e63652d617263686974656374757265732f636f6e7461696e6572732f616b732f696d616765732f7365637572652d626173656c696e652d6172636869746563747572652e737667)

[PCI Baseline](https://github.com/mspnp/aks-baseline)


**Deployment Workflow**

![alt text](https://learn.microsoft.com/en-us/azure/architecture/guide/aks/media/aks-cicd-azure-pipelines-architecture.svg#lightbox)


**DevOps Pipeline & Jobs**

![alt text](https://miro.medium.com/v2/resize:fit:828/format:webp/1*KarJfifaVtnaR6PDyiEb-A.jpeg)

