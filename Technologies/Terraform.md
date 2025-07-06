---
tags:
  - technologies
date: 2023-09-1
---
- Open source `Infrastructure-as-Code (IaC)` tool.
- Defines and provisions infrastructure using HCL language.
- Cloud-agnostic and supports AWS, Azure, GCP, [[Kubernetes]] and more.
- Use cases:
	- automating cloud infrastructure provisioning
	- enforcing consistent environments
	- managing infrastructure lifecycle (create, update, destroy)
# Components

-  Config files are written in HCL (`.tf` files) and define desired infrastructure:

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

- `Providers`: plugins that allow Terraform to interact with platforms.
- `Resources`: building blocks managed by Terraform (instances, buckets, VPCs).
- `State`: TF maintains a state file (`terraform.tfstate`) to track infrastructure.
# Deployment

- Typical deployment commands include:

```bash
terraform init # initialize working dir and download providers
terraform plan # preview changes
terraform apply # apply changes
terraform destroy # destroy infrastructure
```