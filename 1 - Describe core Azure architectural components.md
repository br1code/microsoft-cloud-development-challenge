# Describe core Azure architectural components

In this module, you'll examine the various concepts, resources, and terminology that are necessary to work with Azure architecture. For example, you'll learn about Azure subscriptions and management groups, resource groups and Azure Resource Manager, as well as Azure regions and availability zones.

## Learning objectives

After completing this module, you'll be able to describe the benefits and usage of:

Azure subscriptions and management groups.
- Azure resources, resource groups, and Azure Resource Manager.
- Azure regions, region pairs, and availability zones.

---

## Organizing structure for resources in Azure

- **Management Groups**: Manage access, policy, and complicance for multiple subscriptions.
  - **Subscriptions**: Groups user accounts and resources for those users. Manage costs.
    - **Resource Groups**: Logical containers for Azure resources.
      - **Resources**: Instances of Azure services like VMs, storage, or databases. 

![](Assets/organizing-structure.png)

## Azure Regions

"What you use to identify the location for your resources"

They are **geographical areas on the planet that contains at least one or multiple datacenters** that are nearby and networked together with a low-latency network.

- Only available in certain regions = some services or VM features such as VM sizes or storage types.
- Global services without a particular region = services such as Azure Active Directory, Azure Traffic manager, and Azure DNS.

## Availability Zones

They are **phisically separate datacenters within an Azure Region**.

- Made up of one or more data centers.
- Set up to be an isolation boundary.
- They have independent power, cooling, and networking.
- If one zone goes down, the other continues working.

![](Assets/availability-zones.png)

Example:

- West US 2 region:
  - West US 2 - Zone 1
  - West US 2 - Zone 2
  - West US 2 - Zone 3

**Note:** Not every region has support for availability zones.

**Use Availability Zones** to run mission-critical applications and build high-availability into your application architecture by:

Co-locating your resources (compute, storage, networking, and data) within a **Zone**, and replicating them in other **Zones**.

Categories of Azure services that support Availability Zones:

- Zonal services: pin the service to a specific zone (for example, VMs, managed disks, IP addresses)
- Zone-redundant services: replicated automatically across zones (for example, zone-redundant storage, SQL dbs)
- Non-regional services: services are always available from Azure geographies and are resilient to zone-wide outages and region-wide outages.

## Azure Region Pairs

Availability zones are created using one or more datacenters. **There's a minimum of three zones within a single region**. It's possible that a disaster could cause an outage large enough to affect even two datacenters, so Azure also creates region pairs.

**Each Azure region is always paired with another region within the same geography** (such as US, Europe, or Asia) at least 300 miles away.

This approach allows for the replication of resources across a geography to help reduce interruptions due to catastrophic events. **If a region in a pair was affected** by a natural disaster, **services would automatically failover to the other region in its region pair**.

![](Assets/region-pairs.png)

Examples:

- East US and West US: These regions are located on the east and west coasts of the United States, respectively. They form a region pair within the United States geopolitical region.

- North Europe and West Europe: These regions are located in Northern Europe and Western Europe, respectively. They form a region pair within the Europe geopolitical region.

- East Asia and Southeast Asia: These regions are located in East Asia and Southeast Asia, respectively. They form a region pair within the Asia-Pacific geopolitical region.

- Brazil South and Brazil Southeast: These regions are located in southern and southeastern Brazil, respectively. They form a region pair within the Brazil geopolitical region.

Because the pair of regions is directly connected and far enough apart to be isolated from regional disasters, **you can use them to provide reliable services and data redundancy**. Some services offer automatic geo-redundant storage by using region pairs.

## Azure Resources and Azure Resource Manager

Before creating a subscription, we need to be ready to start creating resources and storing them in Resource Groups. Let's define those terms:

- Resource: **A manageable item that's available through Azure**. Virtual machines (VMs), storage accounts, web apps, databases, and virtual networks are examples of resources.
- Resource group: **A container that holds related resources** for an Azure solution. The resource group includes resources that you want to manage as a group. **You decide which resources belong in a resource group based on what makes the most sense for your organization**.

Notes: 

- A resource can only be a member of a single resource group.
- Many resources can be moved between Resource Groups with some services having specific limitations or requirements to move.
- Resource Groups can't be nested.
- Before any resource can be provisioned, you need a resource group for it to be placed in.
- If you delete a resource group, all resources contained within it are also deleted.
- Resource groups are also a scope for applying role-based access control (RBAC) permissions.

Resource Groups exist to help manage and organize your Azure resources. With Resource Groups you will get "logical grouping" by placing resources of similar usage, type, or location in a resource group.

![](Assets/resource-group.png)

**Azure Resource Manager** is the deployment and management service for Azure. It provides a management layer that enables you to create, update, and delete resources in your Azure account. You use management features like access control, locks, and tags to secure and organize your resources after deployment.

When a user sends a request from any of the Azure tools, APIs, or SDKs, **Resource Manager receives the request**. It authenticates and authorizes the request. **Resource Manager sends the request to the Azure service**, which takes the requested action. Because **all requests are handled through the same API**, you see consistent results and capabilities in all the different tools.

In other words, **all capabilities that are available in the Azure portal are also available through PowerShell, the Azure CLI, REST APIs, and client SDKs.**

![](Assets/consistent-management-layer.png)

With Resource Manager, you can:

- **Manage your infrastructure through declarative templates** (JSON files that defines what you want to deploy to Azure) rather tan scripts.
- **Deploy, manage, and monitor all the resources for your solution as a group**, rather than handling these resources individually.
- **Redeploy your solution throughout the development life cycle** and have confidence your resources are deployed in a consistent state.
- **Define the dependencies between resources** so they're deployed in the correct order.
- **Apply access control to all services** (because RBAC is natively integrated into the management platform).
- **Apply tags to resources** to logically organize all the resources in your subscription.
- **Clarify your organization's billing** by viewing costs for a group of resources that share the same tag.

## Azure Subscriptions

When starting with Azure, one of your first steps will be to create at least one **Azure subscription**. You'll use it to create your cloud-based resources in Azure.

**A subscription provides you with authenticated and authorized access to Azure products and services.**

It also allows you to provision resources.

An Azure subscription is **a logical unit of Azure services that links to an Azure account**, which is an identity in Azure Active Directory (Azure AD) or in a directory that Azure AD trusts.

Example:

- Azure Account
  - Dev Subscription
  - Test Subscription
  - Production Subscription

**An account can have one subscription or multiple subscriptions** that have different billing models and to which you apply different access-management policies. You can use Azure subscriptions to **define boundaries** around Azure products, services, and resources.

There are two types of subscription boundaries that you can use:

- **Billing boundary**: determines how an Azure account is billed for using Azure. You can create multiple subscriptions for different types of billing requirements. Azure generates separate billing reports and invoices for each subscription so that you can organize and manage costs.
- **Access control boundary**: Azure applies access-management policies at the subscription level, and you can create separate subscriptions to reflect different organizational structures (for example, a business with different departments to which you apply distinct Azure subscription policies)

You might want to create additional subscriptions for resource or billing management purposes. For example, you might choose to create additional subscriptions to separate:

- **Environments**: When managing your resources, you can choose to create subscriptions **to set up separate environments for development and testing, security, or to isolate data for compliance reasons**. This design is particularly useful because **resource access control occurs at the subscription level**.
- **Organizational structures**: You can create subscriptions to reflect different organizational structures. For example, **you could limit a team to lower-cost resources, while allowing the IT department a full range**. This design allows you to **manage and control access to the resources that users create within each subscription**.
- **Billing**:  You might want to also create additional subscriptions for billing purposes. Because **costs are first aggregated at the subscription level**, you might want to create subscriptions to manage and track costs based on your needs. For instance, **you might want to create one subscription for your production workloads and another subscription for your development and testing workloads**.
- **Subscription limits**: **Subscriptions are bound to some hard limitations**. For example, the maximum number of Azure ExpressRoute circuits per subscription is 10. Those limits should be considered as you create subscriptions on your account. **If there's a need to go over those limits in particular scenarios, you might need additional subscriptions**.

If you have multiple subscriptions, you can organize them into **invoice sections**. Each invoice section is **a line item on the invoice that shows the charges incurred that month**. For example, you might need a single invoice for your organization but want to organize charges by department, team, or project.

Depending on your needs, you can set up multiple invoices within the same billing account by creating additional billing profiles. Each billing profile has its own monthly invoice and payment method.

![](Assets/billing-structure.png)

## Azure Management Groups

If your organization has many subscriptions, you might need **a way to efficiently manage access, policies, and compliance for those subscriptions**.

Azure Management Rroups **provide a level of scope above subscriptions**.

You **organize subscriptions into containers** called management groups and apply your governance conditions to the management groups. All subscriptions within a management group automatically **inherit the conditions** applied to the management group.

**Note:** All subscriptions within a single management group must trust the same Azure AD tenant.

**Example:** 

You can build a flexible structure of management groups and subscriptions to **organize your resources into a hierarchy for unified policy and access management**. 

The following diagram shows an example of creating a hierarchy for governance by using management groups:

![](Assets/management-groups-and-subscriptions.png)

Examples:

- You can apply policies to a management group that **limits the regions available for VM creation**. This policy would be applied to all management groups, subscriptions, and resources under that management group by o**nly allowing VMs to be created in that region**.
- You could **limit VM locations to the US West Region** in a group called Production. This policy will inherit onto all the Enterprise Agreement subscriptions that are descendants of that management group and **will apply to all VMs under those subscriptions**. This security policy can't be altered by the resource or subscription owner, which allows for improved governance.
- You could provide **user access to multiple subscriptions**. By moving multiple subscriptions under that management group, **you can create one role-based access control (RBAC) assignment on the management group, which will inherit that access to all the subscriptions**. One assignment on the management group can enable users to have access to everything they need instead of scripting RBAC over different subscriptions.

Notes: 
- 10,000 management groups can be supported in a single directory.
- A management group tree can support up to six levels of depth. This limit doesn't include the root level or the subscription level.
- Each management group and subscription can support only one parent.
- Each management group can have many children.
- All subscriptions and management groups are within a single hierarchy in each directory.