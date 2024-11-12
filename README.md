# Terraform Infrastructure Setup

This repository demonstrates the use of **Terraform** to automate the creation of cloud infrastructure resources with a modular approach. The setup is organized into **parent** and **child** modules, where child modules are responsible for defining specific resources, and the parent module integrates and manages them.

## Architecture Overview

The infrastructure is organized into the following components:

1. **Child Modules**:  
   These modules are responsible for creating individual resources such as:
   - **Resource Group**
   - **Virtual Network (VNet)**
   - **Subnet**
   - **Virtual Machine (VM)**

2. **Parent Module**:  
   The parent module orchestrates the execution of the child modules and applies the configurations defined within them. It calls each child module, passes necessary variables, and manages the overall resource provisioning.

### Terraform Modules Used:
- **Resource Group Module** (`resource_group`): Defines and creates an Azure Resource Group.
- **Virtual Network Module** (`vnet`): Defines and creates a Virtual Network (VNet) within the Resource Group.
- **Subnet Module** (`subnet`): Defines and creates a subnet within the Virtual Network.
- **Virtual Machine Module** (`vm`): Creates a Virtual Machine within the defined subnet.

## Workflow

1. **Child Module Creation**:  
   Each resource type (Resource Group, VNet, Subnet, VM) is defined as a separate Terraform child module. These modules are responsible for declaring and provisioning the corresponding infrastructure resources.

2. **Parent Module Integration**:  
   The parent module calls these child modules, passing relevant variables (e.g., names, regions, sizes) to configure the resources. It provides a higher-level abstraction and control to manage the entire infrastructure stack.

3. **Terraform Apply**:  
   After setting up the modules, the `terraform apply` command is executed from the parent module’s directory to initiate the provisioning of resources. Terraform uses the configurations from both the parent and child modules to create the infrastructure in the defined cloud provider.

## Steps to Deploy

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/your-repo.git
   cd your-repo
   ```

2. **Initialize Terraform**:
   Initialize the Terraform configuration by running:
   ```bash
   terraform init
   ```

3. **Plan the Deployment**:
   Generate an execution plan to see what resources will be created:
   ```bash
   terraform plan
   ```

4. **Apply the Configuration**:
   Apply the Terraform configuration to create the resources:
   ```bash
   terraform apply
   ```

   Confirm the action when prompted.

## Directory Structure

```bash
├── parent-module
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   ├── terraform.tfvars        # Variable values for the parent module
│   └── README.md
│
├── child-modules
│   ├── resource_group
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── README.md
│   │
│   ├── vnet
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── README.md
│   │
│   ├── subnet
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── README.md
│   │
│   └── vm
│       ├── main.tf
│       ├── variables.tf
│       ├── outputs.tf
│       └── README.md
│
├── terraform.tfvars            # Global variable values
```

### Key Files:

- **`terraform.tfvars`**:  
  This file contains variable values that are used across both the parent and child modules. You can define values like resource names, region, and other configurations that may differ between environments. This file is typically kept out of version control to ensure sensitive data (like credentials) is not exposed.

- **`parent-module/terraform.tfvars`**:  
  This is where you can set values specific to the parent module, which may include overarching configurations that affect the child modules.

- **`child-modules/<module>/variables.tf`**:  
  Each child module has its own set of variables to allow for flexible configuration.

## Key Concepts

- **Modular Approach**: The project is organized into reusable and isolated modules. Each child module focuses on creating a specific resource, making the code more maintainable and scalable.
  
- **Terraform State**: Terraform manages the state of the infrastructure through its state file, which records the actual infrastructure resources and their metadata. Ensure that the state file is stored securely and backed up.

- **Variables and Outputs**: Each module defines its own set of input variables and output values to allow for flexible resource customization and efficient integration with the parent module.

## Resources

- [Terraform Documentation](https://www.terraform.io/docs)
- [Azure Terraform Provider](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)
```

