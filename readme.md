# Azure Solution Design & Architecture

**Create an infra, network, and deployment design diagram to set up new cloud infrastructure in any cloud provider Azure/GCP.**

* *Includes (the design should start from a tenant if Azure, a project if GCP) other resources* *

    - Landing zone
    - Management Group
    - VNET
    - Connectivity Subscription / Other Subscriptions
    - Design should support Managed Kubernetes (with production ready)
 
Application Architecture

   - Microservice architecture
   - With all key components (config, gateway, and service discovery servers)
   - Application log management
 

DevSecOps Tools (any tools based on working experience)
   - Trivy
   - Docker Scout
   - ACR Defender
   - Aqua

CI (Continuous Integration)
   - Azure DevOps
   - Jenkins

Code quality
   - Sonarqube
   - Checkmarx

Artifacts Server
   - Azure Artifact

Security Check
   - Microsoft cloud security benchmark
       - Control
       - Baseline
       
CD (Continuous delivery/deployment)
   - Azure Devops
   - Helm
   - ArgoCD

---

# Azure Cloud Infrastructure Design #

**Landing Zone:**

The landing zone represents the initial environment setup where all resources will be deployed. In Azure, this is often organized using the following components:

+ Tenant: Azure Active Directory (AAD) Tenant - Represents your organization's identity and access management.

+ Management Group: Organizational structure for managing Azure resources. It helps in applying policies and governance across subscriptions.

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