# AWS Query Data with Outputs

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

- variables.tf

```
variable "instance_name" {
  description = "Value of the Name tag for the EC2 instance"
  type        = string
  default     = "ExampleAppServerInstance"
}
```

- Output EC2 instance configuration

- Create a file called `outputs.tf` in your `learn-terraform-aws-instance` directory.

outputs.tf

```
output "instance_id" {
  description = "ID of the EC2 instance"
  value       = aws_instance.app_server.id
}

output "instance_public_ip" {
  description = "Public IP address of the EC2 instance"
  value       = aws_instance.app_server.public_ip
}

```

```
terraform apply
```

```
terraform output
```
