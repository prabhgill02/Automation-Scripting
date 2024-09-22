# Automation-Scripting


## Documentation

```hcl
# Set the required provider and versions
# required_providers: This defines the necessary provider for this Terraform configuration.
# docker provider:
# source = "kreuzwerker/docker" tells Terraform to download the Docker provider from the kreuzwerker namespace (a commonly used Docker provider for Terraform).
# version = ">= 2.13.0" ensures Terraform uses version 2.13.0 or newer of the Docker provider.

terraform {
  required_providers {
    # We recommend pinning to the specific version of the Docker Provider you're using
    # since new versions are released frequently
    docker = {
      source  = "kreuzwerker/docker"
      version = "3.0.2"
    }
  }
}


# Configure the docker provider
# This block defines how Terraform will interact with Docker:
# npipe is the connection method that Terraform will use to talk to Docker.

# provider "docker" {
# }

# Create a docker image resource
# -> docker pull nginx:latest

resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = true
}

# Create a docker container resource
# -> same as 'docker run --name nginx -p8080:80 -d nginx:latest'
resource "docker_container" "nginx" {
  name    = "nginx"
  image   = docker_image.nginx.image_id

  ports {
    external = 8080
    internal = 80
  }
}
```

