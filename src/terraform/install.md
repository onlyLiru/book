# Install Terraform

```
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
terraform --help
terraform -help plan
```

# Autocomplete

```
touch ~/.bashrc
terraform -install-autocomplete
```

# Quick start tutorial

```
open -a Docker
```

```
mkdir learn-terraform-docker-container
```

```
cd learn-terraform-docker-container
```

  ## Create main.tf

```
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 2.13.0"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "tutorial"
  ports {
    internal = 80
    external = 8000
  }
}

```

```
terraform init
```

```
terraform apply
```

- [http://localhost:8000](http://localhost:8000)

```
terraform destroy
```