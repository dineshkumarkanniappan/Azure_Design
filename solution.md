
# Azure Cloud Infrastructure Design #

**Landing Zone:**

The landing zone represents the initial environment setup where all resources will be deployed. In Azure, this is often organized using the following components:

+ Tenant: Azure Active Directory (AAD) Tenant - Represents your organization's identity and access management.

+ Management Group: Organizational structure for managing Azure resources. It helps in applying policies and governance across subscriptions.

**Sample**
![AKS Landing Zone](./source/AKS_Landingzone.png)


**Platform landing zone:** 

A platform landing zone is a subscription that provides shared services (identity, connectivity, management) to applications in application landing zones. Consolidating these shared services often improves operational efficiency. One or more central teams manage the platform landing zones. In the conceptual architecture (see figure 1), the "Identity subscription", "Management subscription", and "Connectivity subscription" represent three different platform landing zones. The conceptual architecture shows these three platform landing zones in detail. It depicts representative resources and policies applied to each platform landing zone.

**Application landing zone:** 

An application landing zone is a subscription for hosting an application. You pre-provision application landing zones through code and use management groups to assign policy controls to them. In the conceptual architecture (see figure 1), the "Landing zone A1 subscription" and "Landing zone A2 subscription" represent two different application landing zones. The conceptual architecture shows only the "Landing zone A2 subscription" in detail. It depicts representative resources and policies applied to the application landing zone.

**Sample** 
![alt text](./source/management_group.png)

**AKS Private Cluster**

![AKS Private Cluster](./source/AKS-private-cluster.jpg)

**AKS PCI Baseline Architecture**

![Baseline Architecture](https://camo.githubusercontent.com/bff2c59f8c39ff5fdde854e92f22bf6cb8be96da065fa0c6fe8c540b5400e6b0/68747470733a2f2f6c6561726e2e6d6963726f736f66742e636f6d2f617a7572652f6172636869746563747572652f7265666572656e63652d617263686974656374757265732f636f6e7461696e6572732f616b732f696d616765732f7365637572652d626173656c696e652d6172636869746563747572652e737667)

[PCI Baseline](https://github.com/mspnp/aks-baseline)

**Deployment Workflow**

![Deployment Workflow](https://learn.microsoft.com/en-us/azure/architecture/guide/aks/media/aks-cicd-azure-pipelines-architecture.svg#lightbox)