# Terraform DataSource
- 定义
```
data "aws_security_groups" "default" {
  filter {
    name   = "group-name"
    values = ["default"]
  }
}

data "local_file" "ssh_public_key" {
  filename = "${path.module}/id_rsa.pub"
}
```
- 使用
```
resource "aws_key_pair" "ssh" {
  key_name   = "tony"
  public_key = data.local_file.ssh_public_key.content
}

resource "aws_security_group_rule" "ssh" {
  type              = "ingress"
  from_port         = 22
  to_port           = 22
  protocol          = "tcp"
  cidr_blocks       = ["0.0.0.0/0"]
  security_group_id = data.aws_security_groups.default.ids[0]
}
```

- 注意 local_file 依赖local provider

```
local = {
    source  = "hashicorp/local"
    version = ">= 2.2.3"
}

terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }

    local = {
      source  = "hashicorp/local"
      version = ">= 2.2.3"
    }
  }

  required_version = ">= 1.3.5"
}
```