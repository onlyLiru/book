# AWS Change Infrastructure

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
    Name = "ExampleAppServerInstance"
  }
}
```

```
terraform init
```

```
terraform apply
```

```
resource "aws_instance" "app_server" {
    -  ami           = "ami-830c94e3"
    +  ami           = "ami-08d70e59c07c61a3a"
    -  instance_type = "t2.micro"
    +  instance_type = "t1.micro"
 }
```