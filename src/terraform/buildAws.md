# AWS Build Infrastructure

- Write configuration

```
mkdir learn-terraform-aws-instance
```

```
cd learn-terraform-aws-instance
```

```
touch main.tf

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
  ami           = "ami-830c94e3"
  instance_type = "t2.micro"

  tags = {
    Name = "ExampleAppServerInstance"
  }
}

```

```
terraform init 
```
Format and validate the configuration
```
terraform fmt
```

```
terraform validate
```
```
terraform apply
```
```
terraform plan
```

Inspect state

```
terraform show
```
- 手动管理状态
```
terraform state list
```


