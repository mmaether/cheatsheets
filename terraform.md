# Terraform

## Installation

Follow the [Installing Terraform](https://learn.hashicorp.com/terraform/getting-started/install) page to install Terraform.

1. Download the zip file.
2. Extract to a folder, i.e. `C:\`
3. Set `PATH` environment variables.
4. Verify installation, `terraform`
5. Install AWS CLI, run `aws configure`.
6. Run `terraform init` in Terraform folder.

## Commands

Command | Function
------- | --------
`terraform` | Verifies terraform's installation, then displays help documents.
`terraform -help` | Displays help guides.
`terraform --help plan` | Displays help guide for that specific command.
`terraform init` | Initializes various local settings and data that will be used by subsequent commands.
`terraform fmt` | Formats the Terraform files to be uniform.
`terraform validate` | Checks and reports errors within modules, attribute names, and value types.
`terraform apply` | Shows and then executes the plan after approval. Can be done after editing.
`terraform show` | Displays the current state.
`terraform destroy` | Destroys all resources.
