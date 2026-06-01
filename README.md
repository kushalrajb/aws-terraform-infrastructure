# AWS Modular Infrastructure via Terraform

A production-ready, automated Infrastructure as Code (IaC) framework designed to provision baseline cloud architecture on AWS. This repository automates the creation of a secure network perimeter, compute layers with performance-optimized storage, and strict ingress/egress access controls using modular Terraform configurations.

---

## 🏗️ Repository Architecture

* 📁 **aws-terraform-infrastructure/** (Root)
  * 📄 `main` — Core AWS resource provisioning logic (VPC, EC2, Security Groups)
  * 📄 `variables` — Input variables for horizontal infrastructure scaling
  * 📄 `outputs` — Computed runtime parameters (Public IPs, VPC Resource IDs)
  * 📄 `modules` — Structural definitions for modular components
  * 📄 `.gitignore` — Strict exclusion parameters preventing local state file exposure
  * 📄 `.terraform.lock.hcl` — Provider dependency lock manifest
  * 📄 `README.md` — Project implementation architecture blueprint

---

## 🚀 Key Features

* **Elastic Compute Configuration:** Automated provisioning of EC2 instances utilizing optimized gp3 storage configurations for maximized IOPS efficiency.
* **Segregated Network Security:** Isolated Security Group matrices operating on the Principle of Least Privilege, explicitly filtering traffic across protocol domains.
* **Declarative Variable Control:** Completely decoupled parameters, allowing target regions, AMI IDs, and SSH keys to be swapped dynamically at runtime.
* **State Safety Foundations:** Formatted explicitly with native git protection loops to prevent critical infrastructure metadata from slipping into public view.

---

## 🛠️ Prerequisites

Before initiating infrastructure deployments, ensure the following tools are ready on your local node:
* **Terraform Engine** (v1.0.0+)
* **AWS CLI** authenticated via an IAM user with appropriate resource privileges
* A pre-existing **AWS SSH Key Pair** for instance access validation

---

## 🚀 Deployment Instructions

### Step 1: Clone the Codebase
```bash
git clone [https://github.com/kushalrajb/aws-terraform-infrastructure.git](https://github.com/kushalrajb/aws-terraform-infrastructure.git)
cd aws-terraform-infrastructure
```

### Step 2: Initialize Provider Dependencies
Download the designated AWS provider plugins and lock down dependency versions:
```bash
terraform init
```

### Step 3: Compile Execution Plan
Review the proposed cloud architecture changes before provisioning live resources. Pass your deployment specific parameters inline:
```bash
terraform plan \
  -var="aws_region=us-east-1" \
  -var="ami_id=ami-0c7217cdde317cfec" \
  -var="key_name=your-ssh-key"
```

### Step 4: Run Infrastructure Provisioning
Apply the blueprint directly to your AWS environment:
```bash
terraform apply \
  -var="aws_region=us-east-1" \
  -var="ami_id=ami-0c7217cdde317cfec" \
  -var="key_name=your-ssh-key" \
  --auto-approve
```

---

## 📊 Infrastructure Runtime Outputs

Once the provisioning engine finishes, the following structural details will be printed cleanly to your terminal screen:

| Output Attribute | Practical Use Case |
| :--- | :--- |
| **`instance_public_ip`** | Primary IPv4 address used to SSH into the compute layer or bind to service routes. |
| **`security_group_id`** | Firewall identifier used for attaching future services or microservice ingress points. |
| **`vpc_id`** | Core network container scope for subnets, gateways, and tracking cloud resource groups. |

---

## 🧹 Tearing Down Resources

To avoid incurring accidental AWS billing charges when your environments are no longer needed, purge the provisioned state completely with a single command:
```bash
terraform destroy --auto-approve
```
