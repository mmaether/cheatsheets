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
`terraform plan` | Tests what infrastructure would be built based on Terraform files. It does not run.
`terraform plan -out out.terraform` | The changes that Terraform plans to make will be saved to `out.terraform`.
`terraform apply` | Shows and then executes the plan after approval. Can be done after editing.
`terraform show` | Displays the current state.
`terraform graph` | Create a visual representation of a configuration or execution plan.
`terraform destroy` | Destroys all resources.

## Steps

1. Run `terraform init`
2. Run `terraform plan` or `terraform apply`
3. Run `terraform destroy`

## Variable Types

Type | Description | Example
---- | ------------ | -----------------
**String** | "Hello World" | `variable "string" {`<br>&nbsp;&nbsp;`type = string`<br>`}`
**Number** | 17 | `variable "number" {`<br>&nbsp;&nbsp;`type = number`<br>`}`
**Boolean** | Two possible values of either `true` or `false`. | `variable "number" {`<br>&nbsp;&nbsp;`type = bool`<br>`}`
**List** | A common data type that represents a countable number of ordered values, where the same value may occur more than once. | `[0, 1, 5, 2]`
Set | A set is like a list, but it doesn't keep the order you put it in and can only contain unique values. | `[5, 1, 1, 2]` becomes `[1, 2, 5]` 
**Map** | Similar to arrays, a data type composed of a collection of (key, value) pairs. | `{"key" = "value"}`
Object | An object is like a map but each element can have a different type. | `{`<br>&nbsp;&nbsp;`firstname="John"`<br>&nbsp;&nbsp;`housenumber=10` <br>`}`
Tuple | A tuple is like a list, but each element can have a different type. | `[0, "string", false]`

## Variables

- Everything in one file is not great.
- Use variables to hide secrets. 
- You don't want your AWS credentials in your git repository.
- Use variables for elements that might change, i.e. AMIs are different per region.

`provider.tf`: Includes only the provider details.

```bash
provider "aws" {
  access_key = "${var.AWS_ACCESS_KEY}"
  secret_key = "${var.AWS_SECRET_KEY}"
  region = "${var.AWS_REGION}"
}
```

`vars.tf`: Declare the variables.

```bash
variable "AWS_ACCESS_KEY" {}
variable "AWS_SECRET_KEY" {}
variable "AWS_REGION" {
  default = "us-east-1"
}
variable "AMIS" {
  type = "map"
  default= {
    us-east-1 = "ami-13be557e"
    us-west-2 = "ami-06b94666"
    eu-west-1 = "ami-0d729a60"
  }
}
```

`terraform.tfvars`: To set lots of variables, it is more convenient to specify their values in a *variable definitions* file. This file actually has the values of the variables. Include this file in the `.gitignore`.

```bash
AWS_ACCESS_KEY = ""
AWS_SECRET_KEY = ""
AWS_REGION = ""
```

`instance.tf`: 

```bash
resource "aws_instance" "example" {
  ami = "${lookup(var.AMIS, var.AWS_REGION)}"
  #ami = "ami-0d729a60"
  instance_type = "t2.micro"
}
```

You can use [Cloud Images](https://cloud-images.ubuntu.com/locator/ec2) for an easy AMI lookup site. Alternatively just Goole `ami lookup`.

## Software Provisioning

So far we've set up servers. Now we need to actually add our custom software to it. There are two ways to provision software on your instances.

1. You can build your own custom AMI and bundle your software with the image. Packer is great for this.
2. Another way is to boot standardized AMIs, and then install the software on it you need.
   1. Using file uploads
   2. Using remote execution
   3. Using automation tools like chef, puppet, ansible.

### File Uploads

File uploads is an easy way to upload a file or a script. It can be used in conjunction with remote-exec to execute a script.

```bash
resource "aws_instance" "example" {
  ami = "${lookup(var.AMIS, var.AWS_REGION)}"
  instance_type = "t2.micro"

  provisioner "file" {
    source = "app.conf"
    destination = "etc/myapp.conf"
  }
}
```

To override the SSH defaults, you can use "connection". By default ec2-user is used for the accounts.

```bash
resource "aws_instance" "example" {
  ami = "${lookup(var.AMIS, var.AWS_REGION)}"
  instance_type = "t2.micro"

  provisioner "file" {
    source = "script.sh"
    connection {
      user = "${var.instance_username}"
      password = "${var.instance_password}"
    }
  }
}
```

Typically you'll use SSH keypairs.

```bash
resource "aws_key_pair" "edward-key" {
  key_name = "mykey"
  public_key = "ssh-rsa my-public-key"
}

resource "aws_instance" "example" {
  ami = "${lookup(var.AMIS, var.AWS_REGION)}"
  instance_type = "t2.micro"
  key_name = "${aws_key_pair.mykey.key_name}"

  provisioner "file" {
    source = "script.sh"
    destination = "/opt/script.sh"
    connection {
      user = "${var.instance_username}"
      private_key = "${file(${var.path_to_private_key})}"
    }
  }
}
```

After you upload a script, you'll want to execute it. You can execute a script using `remote-exec`.

```bash
resource "aws_instance" "example" {
  ami = "${lookup(var.AMIS, var.AWS_REGION)}"
  instance_type = "t2.micro"

  provisioner "file" {
    source = "script.sh"
    destination = "/opt/script.sh"
  }

  provisioner "remote-exec" {
    inline = [
      "chmod +x /opt/script.sh",
      "/opt/script.sh arguments"
    ]
  }
}
```

To generate a key, run `ssh-keygen -f mykey`

## Output Variables

Use output to display the public IP address of an AWS resource.

```bash
resource "aws_instance" "example" {
  ami = "${lookup(var.AMIS, var.AWS_REGION)}"
  instance_type = "t2.micro"
}

output "ip" {
  value = "${aws_instance.example.public_ip}"
}
```

## Remote State

1. Add the backend code to a `.tf` file.
2. Run the initiation procession.

