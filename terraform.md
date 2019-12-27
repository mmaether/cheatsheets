# Terraform

Terraform enables you to safely and predictably create, change, and improve cloud infrastructure.

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
`terraform console` | Interactive console for Terraform interpolations. Great to debug variables.
`terraform init` | Initialize a Terrform working directory.
`terraform fmt` | Rewrites config files to canonical format.
`terraform validate` | Validates the Terraform files.
`terraform plan` | Generate and show an execution plan. It does not run.
`terraform output` | Read an output from a state file.
`terraform plan -out out.terraform` | The changes that Terraform plans to make will be saved to `out.terraform`.
`terraform apply` | Builds or changes infrastructure after approval.
`terraform show` | Inspect Terraform state or plan.
`terraform graph` | Create a visual graph of Terraform resources.
`terraform providers` | Prints a tree of the providers used in the configuration.
`terraform refresh` | Update local state file against real resources.
`terraform taint` | Manually mark a resource for recreation.
`terraform untaint` | Manually unmark a resource as tainted.
`terraform workspace` | Workspace management.
`terraform destroy` | Destroys Terraform-managed infrastructure.
`ssh-keygen -f mykey` | Generate a key named `mykey`.

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

## Files

### `main.tf`

Terraform uses configuration files that are named with the `.tf` file extension. Add Terraform code in `.tf` files for Terraform to run. These files can be named anything.

### `terraform.tfstate`

Terraform must store state about your managed infrastructure and configuration. This state is used by Terraform to map real world resources to your configuration, keep track of metadata, and to improve performance for large infrastructures. This is managed by Terraform and should not be overridden. 

This state is stored by default in a local file named `terraform.tfstate`, but it can also be stored remotely, which works better in a team environment.

Learn More

- [State](https://www.terraform.io/docs/state/index.html)
- [Purpose of Terraform State](https://www.terraform.io/docs/state/purpose.html)
- [Remote State](https://www.terraform.io/docs/state/remote.html)

## Providers

[Providers](https://www.terraform.io/docs/configuration/providers.html) refers to the cloud infrastructure provider that you're building the environment in. This must be set so Terraform knows which API to use.

```bash
# The default provider configuration
provider "aws" {
  region = "us-east-1"
  #region = var.region
}
```

### Authentication

You must provide Terraform with an account's access key and secret key. This can be tricky as this is sensitive information that we don't want to have leaked out. There are a few [methods](https://www.terraform.io/docs/providers/aws/index.html), some better than others.

#### Static Credentials

> **Warning**: Hard-coding credentials into any Terraform configuration is not recommended. Do not do this, this is to display an example.

```bash
provider "aws" {
  region     = "us-west-2"
  access_key = "my-access-key"
  secret_key = "my-secret-key"
}
```

####  Environment Variables

If you define your provider without variables, then the CLI will ask you to provide the credentials.

```bash
provider "aws" {}
```

```bash
$ export AWS_ACCESS_KEY_ID="anaccesskey"
$ export AWS_SECRET_ACCESS_KEY="asecretkey"
$ export AWS_DEFAULT_REGION="us-east-`"
$ terraform plan
```

#### Shared Credentials File

You can use an AWS credentials file to specify your [credentials](https://letslearndevops.com/2017/07/24/how-to-secure-terraform-credentials/). 

First download the AWS CLI and run `aws configure`. Enter credentials.

```bash
[mmaether@example demo] $ aws configure
AWS Access Key ID [None]: ENTER-YOUR-ACCESS-KEY-HERE
AWS Secret Access Key [None]: ENTER-YOUR-SECRET-KEY-HERE
Default region name [None]: us-easst-1
Default output format [None]: 
```

The default credential files are saved here:

- Windows: `%USERPROFILE%\.aws\credentials`
- Linux and OS X: `$HOME/.aws/credentials`

You can save multiple profiles that can be called on later.

```bash
[mmaether@example demo] $ cat ~/.aws/credentials 
[default]
aws_access_key_id = ENTER-YOUR-ACCESS-KEY-HERE
aws_secret_access_key = ENTER-YOUR-SECRET-KEY-HERE
[dev]
aws_access_key_id = ENTER-YOUR-ACCESS-KEY-HERE
aws_secret_access_key = ENTER-YOUR-SECRET-KEY-HERE
[production]
aws_access_key_id = ENTER-YOUR-ACCESS-KEY-HERE
aws_secret_access_key = ENTER-YOUR-SECRET-KEY-HERE
```

Terraform will check this location if it fails to detect credentials inline or in the environment. 

You can optionally specify a different location in the configuration by providing the `shared_credentials_file` attribute, or in the environment with the `AWS_SHARED_CREDENTIALS_FILE` variable. This method also supports a profile configuration and matching `AWS_PROFILE` environment variable:

```bash
provider "aws" {
  region                  = "us-east-1"
  shared_credentials_file = "/Users/tf_user/.aws/creds"
  profile                 = "dev"
}
```

#### Use `terraform.tfvars`

You can set up the following files:

`provider.tf`: Define the provider.

```bash
provider "aws" {
  access_key = var.aws_access_key
  secret_key = var.aws_secret_key
  region     = var.region
}

resource "aws_instance" "web-server" {
  ami           = "ami-0c2aba6c"
  instance_type = "t2.micro"
}
```

`variables.tf`: Define the variables.

```bash
variable "aws_access_key" {}

variable "aws_secret_key" {}

variable "region" {
  default = "us-east-2"
}
```

`terraform.tfvars`: Include the variables.

```bash
aws_access_key = "ENTER-YOUR-ACCESS-KEY-HERE"
aws_secret_key = "ENTER-YOUR-SECRET-KEY-HERE"
```

> Make sure to include a `.gitignore` file and add the `.tfvars` file to it. See also a recommended [terraform.gitignore](https://github.com/github/gitignore/blob/master/Terraform.gitignore).

## Variables

Variables are highly encouraged in Terraform to make the code more reusable and easier to use across a team. It's recommended to store variables in a separate file so if changes should be made for a specific environment or developer, they can simply change the one file instead of sifting through the code.

Variables can also be used for elements that might change (AMIs per region) and to hide your AWS credentials.

`provider.tf`: Declare the provider. Reference variables.

```bash
provider "aws" {
  access_key = var.AWS_ACCESS_KEY
  secret_key = var.AWS_SECRET_KEY
  region     = var.AWS_REGION
}
```

`variables.tf`: Declare the variables, define the variable type, and optionally set a default value.

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

`terraform.tfvars`: Assign the actual values of the variables. **Include this file in the `.gitignore`.**

```bash
AWS_ACCESS_KEY = ""
AWS_SECRET_KEY = ""
AWS_REGION     = ""
```

`instance.tf`: 

```bash
resource "aws_instance" "example" {
  ami           = lookup(var.AMIS, var.AWS_REGION)
  #ami          = "ami-0d729a60"
  instance_type = "t2.micro"
}
```

You can use [Cloud Images](https://cloud-images.ubuntu.com/locator/ec2) for an easy AMI lookup site. Alternatively just Google `ami lookup`.

#### Include Variables in Command Line

You can also include `-var` options on the terraform plan or terraform apply command line. 

```bash
terraform apply -var="image_id=ami-abc123"
terraform apply -var='image_id_list=["ami-abc123","ami-def456"]'
terraform apply -var='image_id_map={"us-east-1":"ami-abc123","us-east-2":"ami-def456"}'
```

You can also use `-var-file` to reference which variable file to use.

`terraform apply -auto-approve -input=false -var-file=env_vars/itxdv.tfvars`

# Resource Types

- `variable`
- `provider`
- `resource`
- [data](https://www.terraform.io/docs/configuration/data-sources.html)
- [provisioner](https://www.terraform.io/docs/provisioners/index.html)

## Functions

Terraform comes with numerous built-in [functions](https://www.terraform.io/docs/configuration/functions.html) that can be useful, including but not limited to:

- Numeric Functions: `ceil`, `floor`, `max`, `min`
- String Functions: `join`, `regex`, `replace`, `split`, `substr`, `trim`, `upper`
- Collection Functions: `concat`, `contains`, `distinct`, `length`, `slice`
- Encoding Functions: `base64encode`, `csvdecode`, `jsondecode`, `urlencode`, `yamldecode`
- Filesystem Functions: `dirname`, `basename`, `file`, `fileexists`
- Date and Time Functions: `formatdate`, `timeadd`, `timestamp`
- Hash and Crypto Functions: `base64sha256`, `filesha512`, `md5`, `sha1`
- IP Network Functions: `cidrhost`, `cidrnetmask`, `cidrsubnet`
- Type Conversion Functions: `tobool`, `tolist`, `tomap`, `tonumber` `toset`, `tostring`

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
  ami = lookup(var.AMIS, var.AWS_REGION)
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

## Output Values

Use output to display the public IP address of an AWS resource.

```bash
resource "aws_instance" "example" {
  ami           = lookup(var.AMIS, var.AWS_REGION)
  instance_type = "t2.micro"
}

output "ip" {
  value = aws_instance.example.public_ip
}
```

## Terraform Cloud

- [Overview of Terraform Cloud](https://learn.hashicorp.com/terraform/cloud-gettingstarted/tfc_overview)
- [Terraform Cloud Documentation](https://www.terraform.io/docs/cloud/index.html)
- [Connecting VCS Providers to Terraform Cloud](https://www.terraform.io/docs/cloud/vcs/index.html)
- [Cost Estimation](https://www.terraform.io/docs/cloud/getting-started/cost-estimation.html): Only appears for the $70 plan.
- [Variables in Terraform Cloud](https://www.terraform.io/docs/cloud/workspaces/variables.html)
- [Workspace Naming](https://www.terraform.io/docs/cloud/workspaces/naming.html): `<COMPONENT>-<ENVIRONMENT>-<REGION>`, i.e. `networking-prod-us-east`.


## Workspaces 

A [workspace](https://www.terraform.io/docs/state/workspaces.html) name should tell your colleagues what the workspace is for. Most workspaces are a particular environment of a particular Terraform configuration, so the name should include both the name of the configuration and the name of the environment.

As an example, if we're using a configuration named "minimum" and we're deploying it in a production environment, we can name it minimum-prod.

It's best practice to have different workspaces per environment, i.e. dev, production, QA.

## Resources

- [Terraform Best Practices](https://github.com/ozbillwang/terraform-best-practices)
- [Terraform AWS Examples](https://github.com/terraform-providers/terraform-provider-aws/tree/master/examples)
