## Infrastructure as Code
Infrastructure as Code (IaC) is the practice of defining and managing infrastructure (networks, servers, storage, IAM, load balancers, etc.) using code - not using the user interface.

Before the advent of IaC, infrastructure management was typically a manual and time-consuming process. System administrators had to:

- Manually Configure Servers: Servers and other infrastructure components were often set up and configured manually, which could lead to inconsistencies and errors.

- Lack of Version Control: Infrastructure configurations were not typically version-controlled, making it difficult to track changes or revert to previous states.

- Limited Automation: Automation was limited to basic scripting, often lacking the robustness and flexibility offered by modern IaC tools.

- Slow Provisioning: Provisioning new resources or environments was a time-consuming process that involved multiple manual steps, leading to delays in project delivery.

- Documentation Heavy: Organizations relied heavily on documentation to record the steps and configurations required for different infrastructure setups. This documentation could become outdated quickly.

While we can technically use programming languages like Python (e.g., using boto3) to interact with AWS APIs to provision infrastructure, it introduces significant challenges compared to dedicated Infrastructure as Code (IaC) tools like Terraform. 

- To manage infrastructure through scripts, we need deep programming knowledge. As requirements grow—such as configuring VPCs, high-availability EC2 instances, and S3 endpoints—the complexity of maintaining custom code becomes substantial.

- Without IaC, we are essentially writing raw API calls. Unlike tools that use declarative templates (like CloudFormation or Terraform), custom scripts often lack built-in mechanisms to understand the state of the infrastructure, making it difficult to track what has already been created or changed.

IaC addresses these challenges by providing a systematic, automated, and code-driven approach to infrastructure management. Popular IaC tools include Terraform, AWS CloudFormation, Azure Resource Manager templates others.

### Why Terraform?
Terraform simplifies the life of a DevOps engineer by providing a universal approach to managing infrastructure, which eliminates the need to learn provider-specific tools like AWS CloudFormation, Azure Resource Manager, or OpenStack Heat templates.

- Terraform acts as a bridge; we learn one language (HashiCorp Configuration Language) and apply it to any cloud provider (e.g., AWS, Azure, GCP). It converts our code into the specific APIs required by the target platform.

- With the terraform plan command, we can perform a dry run to preview exactly what infrastructure changes will occur before actually applying them, preventing accidental misconfigurations.

- Terraform provides a consistent workflow: init (to initialize providers), plan (to review changes), apply (to deploy resources), and destroy (to safely tear down resources), making management systematic and clean.

- Terraform has a large and active user community, which means we can find answers to common questions, troubleshooting tips, and a wealth of documentation and tutorials online. Also, there are pre-built modules and configurations for a wide range of services and infrastructure components, saving us time and effort in writing custom configurations.

## Important Terminologies
- Provider: A provider is a plugin for Terraform that defines and manages resources for a specific cloud or infrastructure platform. Examples of providers include AWS, Azure, Google Cloud, and many others. We configure providers in our Terraform code to interact with the desired infrastructure platform.

- Configuration File: Terraform uses a set of configuration files (often with a `.tf` extension) written in HCL that Terraform loads together as one configuration. These files specify providers, the desired infrastructure state, variables, exported outputs etc. The primary configuration file is usually named `main.tf`, but we can use multiple configuration files as well. Terraform loads all `.tf` files in a directory (same module) and merges them. File names are for humans/organization, not execution order.

- Resource: A resource is a specific infrastructure component that we want to create and manage using Terraform. Resources can include virtual machines, databases, storage buckets, network components, and more. Each resource has a type and configuration parameters that we define in our Terraform code.

- State File: Terraform maintains a state file (often named `terraform.tfstate`) that keeps track of the current state of our infrastructure. This file is crucial for Terraform to understand what resources have been created and what changes need to be made during updates. Basically, Terraform uses state to map our code ↔ real AWS resources.
