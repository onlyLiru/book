# AWS Define Input Variables
- main.tf
```
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }

  required_version = ">= 1.2.0"
}

provider "aws" {
  region  = "us-east-1"
}

resource "aws_instance" "app_server" {
  ami           = "ami-05723c3b9cf4bf4ff"
  instance_type = "t1.micro"

  tags = {
    Name = var.instance_name
  }
}
```
```
tags = {
    -    Name = "ExampleAppServerInstance"
    +    Name = var.instance_name
}
```
- Set the instance name with a variable

> Create a new file called variables.tf with a block defining a new instance_name variable.
```
variable "instance_name" {
    description = "Value of the Name tag for the EC2 instance"
    type        = string
    default     = "ExampleAppServerInstance"
}

```
>  **参数**
> - default
> - type (string,nubmer,bool,list<TYPE>,set<TYPE>,map<TYPE>,object({<ATTR NAME> = <TYPE>, ... }),tuple([<TYPE>, ...]))
> - description
> - validation   校验
> - sensitive  敏感的（如：密码）
> - nullable   非空

```
example validation: 

variable "image_id" {
  type        = string
  description = "The id of the machine image (AMI) to use for the server."

  validation {
    condition     = length(var.image_id) > 4 && substr(var.image_id, 0, 4) == "ami-"
    error_message = "The image_id value must be a valid AMI id, starting with \"ami-\"."
  }
}

```

# Assigning Values to Root Module Variables
- [In a Terraform Cloud workspace.](https://developer.hashicorp.com/terraform/cloud-docs/workspaces/variables)
- Individually, with the ``-var`` command line option.
- In variable definitions (.tfvars) files, either specified on the command line or automatically loaded.
- As environment variables.

```
terraform apply -var="image_id=ami-abc123"
terraform apply -var='image_id_list=["ami-abc123","ami-def456"]' -var="instance_type=t2.micro"
terraform apply -var='image_id_map={"us-east-1":"ami-abc123","us-east-2":"ami-def456"}'

```

```
terraform apply -var-file="testing.tfvars"
```

**这样的名字会自动加载，不需要-var-file制定名字**
- Files named exactly ``terraform.tfvars`` or ``terraform.tfvars.json``.
- Any files with names ending in ``.auto.tfvars`` or ``.auto.tfvars.json``.

**Environment Variables**
```
export TF_VAR_image_id=ami-abc123
terraform plan
```

**加载顺序**
1. Environment variables
2. The terraform.tfvars file, if present.
3. The terraform.tfvars.json file, if present.
4. Any *.auto.tfvars or *.auto.tfvars.json files, processed in lexical order of their filenames.
5. Any -var and -var-file options on the command line, in the order they are provided. (This includes variables set by a Terraform Cloud workspace.)