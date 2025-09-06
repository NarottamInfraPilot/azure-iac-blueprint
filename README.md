![Quickstart: Use Terraform to deploy Azure Bastion | Microsoft Learn](https://github.com/Achinta1997/bastion-infra/blob/main/HLD.png)

Here’s a relevant architectural diagram illustrating an Azure Bastion deployment setup using Terraform—ideal for your README visualization.

---

Below is a draft **README.md** tailored for your GitHub repo `bastion-infra`, incorporating architecture, project structure, usage instructions, and best practices. Feel free to customize as needed:

---

```markdown
# Bastion-Infra: Secure Azure Infrastructure using Terraform & Azure DevOps

**A secure, modular Terraform-based infrastructure with Azure Bastion, deployed through Azure DevOps pipelines with integrated code security scanning.**

---

##  Architecture Overview

*(Refer to the diagram above)*

- **Azure Bastion Host** deployed in its own subnet (`AzureBastionSubnet`) to enable secure VM access (SSH/RDP) **without public IPs**.
- **Virtual Network (VNet)** divided into public and private subnets.
- **Network Security Groups (NSGs)** enforcing traffic rules.
- **Azure Storage Account** used as Terraform backend (remote `tfstate` storage).
- Security scanning integrated into the **Azure DevOps multi-stage CI/CD pipeline**.

---

##  Repo Structure

```

bastion-infra/
├── modules/
│   ├── networking/
│   ├── bastion/
│   └── backend/
├── environments/
│   └── dev/
│       ├── main.tf
│       ├── variables.tf
│       └── backend.tf
├── .azure-pipelines.yml
├── README.md
└── HLD-diagram.png

````

- **Modules:** Reusable Terraform modules (`networking`, `bastion`, `backend`).
- **Environments:** Environment-specific configurations (e.g., `dev`, `prod`).
- **Azure Pipelines YAML:** Defines CI/CD stages—validate, scan, plan, apply.
- **HLD Diagram:** Visual, high-level architecture overview.

---

##  Getting Started

### Prerequisites

- Azure Subscription and permissions (Service Principal credentials).
- Terraform CLI installed.
- Azure DevOps environment with pipeline and service connection configured.

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/Achinta1997/bastion-infra.git
   cd bastion-infra
````

2. **Customize backend configuration** (within `environments/dev/backend.tf`):

   ```hcl
   terraform {
     backend "azurerm" {
       storage_account_name = "your_storage_account"
       container_name       = "tfstate"
       key                  = "dev.terraform.tfstate"
     }
   }
   ```

3. **Initialize Terraform**

   ```bash
   cd environments/dev
   terraform init
   ```

4. **Review configuration**

   ```bash
   terraform validate
   terraform plan
   ```

5. **Apply infrastructure**

   ```bash
   terraform apply
   ```

---

## Azure DevOps CI/CD Pipeline

Pipeline stages:

* **Terraform Validate & Format** (`terraform validate`, `terraform fmt`)
* **Security Scanning** using open-source tools (e.g., tfsec, Checkov)
* **Plan Stage** for infrastructure changes
* **Approval Gates** before execution
* **Apply Stage** to create/update resources with proper RBAC and secrets management

---

## Project Highlights

* Secure Bastion deployment with **no VM public IPs**
* Modular design for **scalable and maintainable infrastructure**
* Remote backend for Terraform state
* **DevSecOps integration** via automated security scanning
* **Separate environment folders** for `dev`, `prod`, etc.

---

## Best Practices Followed

* **Module Documentation:** Each module should include its own README describing inputs/outputs (following Terraform module best practices) ([iaMachs][1], [Microsoft GitHub][2])
* **Terraform Formatting:** Code follows `terraform fmt` standards ([Hostman][3])
* **State Security:** Terraform state stored remotely and excluded from version control (.gitignore) ([Hostman][3])
* **Clear Structure:** Repo structured for clarity and maintainability ([Microsoft GitHub][2])

---

## How to Contribute

1. Fork the repository
2. Create a feature branch `feature/your-feature`
3. Commit changes and follow the proper module structure
4. Submit a pull request for review

---

## License

[MIT License](LICENSE)

---

## Feedback & Collaboration

## Feel free to open issues, discuss enhancements, or suggest improvements. Your feedback is welcome!

**Enjoy building secure infrastructure with Terraform & Azure DevOps!**

```

