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