# Introduction to Cloud and Public Cloud

##  What is Cloud and How Did It Emerge Initially?

To understand cloud computing, it is essential to look at how organizations managed their infrastructure historically.

### Traditional Infrastructure Setup (Pre-Cloud)

1.  **Buying Servers:** Organizations 10, 15, or 20 years ago purchased physical servers (e.g., from IBM or HP) to deploy their applications.
2.  **Creating Data Centers:** These servers were housed in a **data center**, which is a dedicated place where servers are stored, configured (network setup, wires), and maintained (ensuring the right temperature and equipment).
3.  **The Cost and Waste Problem:** These physical servers were very costly and typically came with huge configurations (e.g., 100 GB RAM and 100 CPUs). If an organization only deployed one application using a fraction of those resources (e.g., 1 GB RAM and 1 CPU), the majority of the resources (99 CPUs, 99 GB RAM) were wasted. This inefficiency meant the company was wasting significant money.

### The Emergence of Cloud (Virtualization)

The concept of cloud computing emerged from the need to solve the costly problem of wasting server resources.

1.  **Virtualization:** This concept was introduced to solve the resource wastage problem. Instead of running one application per costly physical server, virtualization allows the creation of **virtual servers** or **virtual machines** on top of the actual physical server.

2.  **Resource Efficiency:** Using virtualization, an organization could buy one high-configuration server and deploy multiple applications (e.g., 15 applications) on 15 different virtual machines, instead of buying 15 separate physical servers.

3.  **The Cloud Concept:** Once virtualization was established, system administrators could create virtual machines and share their IP addresses with developers. The developer would use the server without knowing its exact physical location (it could be in the US, Europe, or India). Because the resources are interconnected and accessible without the user needing to know the physical location, this setup is called the **Cloud**.

---

##  Public Cloud vs. Private Cloud

The core difference between public and private cloud lies in who owns and manages the underlying infrastructure.

| Feature | Private Cloud | Public Cloud |
| :--- | :--- | :--- |
| **Management** | Managed and maintained by the organization itself, often by system administrators. | Managed by external cloud providers (e.g., Amazon/AWS, Microsoft/Azure, Google/GCP). |
| **Scope** | Restricted to the organization. It is within the boundaries of the organization. | Available to anybody in the world who has an account with the provider, irrespective of the organization. |
| **Setup** | The organization buys servers, creates its own data center, and uses platforms like OpenStack or VMware Zen. | The provider buys the servers and creates infrastructure across multiple global locations. |
| **Control** | The organization has complete control over both the resources and the infrastructure. | The provider manages the data centers and ecosystem; the user has complete control over the resources they request and use. |
| **Use Case** | Often used by banking sectors or companies handling sensitive information that do not want to use external cloud platforms. | Preferred by startups and mid-scale organizations due to ease of use and reduced overhead. |
| **Billing** | It involves high upfront cost and continuous capital expenditure. | Based on a **pay as you go** model. |


---

## Why is Public Cloud So Popular?

The immense popularity of public cloud platforms like AWS, Azure, and GCP stems from key advantages they offer over the complex traditional setup.

The main drivers for organizations moving toward the public cloud are **maintenance overhead reduction** and **cost efficiency**.

### A. Maintenance Overhead Elimination (Primary Concern)

For startups and mid-scale companies, setting up and maintaining a data center is complicated and resource-intensive. Public cloud solves this by:

1.  **Avoiding Dedicated Staff:** Maintaining a data center requires a dedicated team of proficient individuals (potentially 10-15 people for larger setups, or 2-5 for smaller ones).
2.  **24/7 Management:** Data centers require continuous maintenance, 24 hours a day, 7 days a week, to ensure protection from power loss, hacking, security issues, and necessary server upgrades and patching.
3.  **Simplicity of Onboarding:** It is very easy for a company to onboard onto a public cloud platform: they simply create an account, pay the money, and organizational members can start creating and using resources immediately.

### B. Cost Benefits and Flexibility

1.  **Pay-as-You-Go:** Organizations only pay for the resources they actually use.
2.  **Avoiding Capital Expenditure:** Companies, especially startups, cannot afford the large initial costs associated with building their own data centers and the continuous costs of maintenance.
3.  **Service Expansion:** Cloud providers constantly increase their offerings (AWS started with 20–30 services and now offers over 200). This growth allows users to easily consume complex setups (like Kubernetes clusters) as simple, managed services, further easing the burden on the user.

### Popularity of AWS

AWS is highly popular because it holds the **first mover advantage**. AWS was the first company to pioneer and successfully launch the concept of the cloud, leading many companies to start their cloud journeys with Amazon Web Services 10 or 12 years ago. This head start has given AWS the **largest market share**.

---
## 🟢 AWS Global Infrastructure

AWS is **global by design**. To deliver speed, reliability, and fault tolerance, AWS builds its services on a layered structure:

1. **Region**

   * A **Region** is a physical geographic area (like "N. Virginia (us-east-1)" or "Mumbai (ap-south-1)").
   * Each region contains multiple **Availability Zones**.
   * We choose a region based on **latency, cost, and data laws** (e.g., a bank in India may prefer “ap-south-1” Mumbai to comply with data regulations).
   
2. **Availability Zone (AZ)**

   * An AZ is like a **data center cluster** with independent power, cooling, and networking.
   * Regions typically have 2–6 AZs.
   * We design apps across multiple AZs for **high availability**.
   * Example: In “Asia Pacific (Mumbai)” we have **ap-south-1a**, **ap-south-1b**, etc.

3. **Edge Locations**
   An **Edge Location** is **not a full data center** like an Availability Zone. Instead, it’s a **smaller site located in hundreds of cities around the world**. Its main job: **cache content and deliver it quickly to end users**.

   * Suppose our website is hosted in AWS **US East (N. Virginia)**.
   * A user in Delhi tries to load a picture from our site.
   * Without Edge Locations: the request travels all the way across the world, to Virginia, and back — slow and laggy.
   * With Edge Locations: AWS keeps a cached copy of that picture at an Edge Location in Delhi. Next time someone in India asks for it, it’s served locally, almost instantly.

   This system is called **Amazon CloudFront (CDN)**, and it relies on Edge Locations.

```
Asia Pacific (group)    --> This is just a geographic label
│
├── ap-south-1 (Mumbai) → Region
│      ├── ap-south-1a → AZ
│      ├── ap-south-1b → AZ
│      └── ap-south-1c → AZ
│
├── ap-southeast-1 (Singapore) → Region
         ├── ap-southeast-1a → AZ
         └── ...
```