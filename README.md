# Modular AWS VPC Infrastructure via Terraform

A production-ready, automated Infrastructure as Code (IaC) repository that provisions a secure baseline networking environment in Amazon Web Services (AWS). Built entirely with HashiCorp Terraform (HCL), this project demonstrates cloud architecture best practices, modular variable design, and strict DevSecOps state security.

---

## 🏗️ Architecture Overview

This Terraform configuration automatically provisions the following foundational AWS resources:
* **Virtual Private Cloud (VPC):** A logically isolated network space (`10.0.0.0/16`).
* **Public Subnet:** Designed for internet-facing resources (`10.0.1.0/24`).
* **Internet Gateway (IGW):** Attached to the VPC to enable outbound and inbound internet traffic.
* **Dynamic Outputs:** Automatically retrieves and displays newly generated Resource IDs upon successful deployment.

---

## 📂 Repository Structure

* 📄 `main.tf` — Core infrastructure declarations (Provider, VPC, Subnets, IGW).
* 📄 `variables.tf` — Parameterized variables (Regions, CIDR blocks) making the code modular and reusable.
* 📄 `outputs.tf` — Console outputs for critical data (VPC ID, Subnet ID) needed by downstream applications.
* 📄 `.gitignore` — Strict DevSecOps rules preventing the leakage of `.tfstate` files, local variables, and cloud credentials into version control.

---

## 🛡️ Security & DevSecOps

To prevent cloud credential leakage and architectural exposure, this repository strictly enforces security perimeters via `.gitignore`. 
* **State Files Blocked:** `*.tfstate` and `*.tfstate.backup` are permanently ignored to ensure no sensitive infrastructure metadata is exposed to the public.
* **Variables Blocked:** `*.tfvars` files are excluded to prevent accidental uploads of AWS access keys or private deployment variables.

---

## 🚀 How to Deploy & Run

### Prerequisites
Before running this code, ensure you have the following installed on your local machine:
* [Terraform](https://developer.hashicorp.com/terraform/downloads) (v1.0.0+)
* [AWS CLI](https://aws.amazon.com/cli/) (Configured with an active IAM user utilizing `aws configure`)

### Step 1: Clone the Repository
```bash
git clone [https://github.com/kushalrajb/aws-terraform-infrastructure.git](https://github.com/kushalrajb/aws-terraform-infrastructure.git)
cd aws-terraform-infrastructure
```

### Step 2: Initialize Terraform
This command downloads the required AWS provider plugins and sets up the local working directory.
```bash
terraform init
```

### Step 3: Review the Execution Plan
This command generates a preview of all the AWS resources Terraform is about to create. It is a safety check to ensure the code behaves as expected before spending money or altering cloud environments.
```bash
terraform plan
```

### Step 4: Provision the Infrastructure
Execute the plan and build the architecture in your AWS account. You will be prompted to type `yes` to confirm.
```bash
terraform apply
```
*Note: Once complete, Terraform will output your new `vpc_id` and `public_subnet_id` in the terminal.*

### Step 5: Clean Up (Teardown)
To avoid incurring unnecessary AWS charges, destroy all infrastructure created by this project once your testing is complete. You will be prompted to type `yes` to confirm.
```bash
terraform destroy
```
