# Getting Started with Terraform

Terraform is the most popular langauge for defining and provisioning infrastructure as code (IaC).

In this tutorial, you will create and initialize infrastructure using Terraform.

## Prerequisites

* The appropriate [Terraform package](https://www.terraform.io/downloads.html) installed.
* [Docker](https://www.docker.com/products/docker-desktop) installed.


## Creating Infrastructure

We recommend creating a new directory on your local machine and creating Terraform configuration code inside it.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following lines into the file.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {
    host = "unix:///var/run/docker.sock"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

## Initializing Terraform

Initialize Terraform with the `init` command. The AWS provider will be installed. 

```shell
$ terraform init
```

Check for any errors. If it ran successfully, you will receive an output similar to this.

```shell
$ terraform init

Initializing the backend...

Initializing provider plugins...
- Finding latest version of kreuzwerker/docker...
- Installing kreuzwerker/docker v2.15.0...
- Installed kreuzwerker/docker v2.15.0 (self-signed, key ID BD080C4571C6104C)

Partner and community providers are signed by their developers.
If you'd like to know more about provider signing, you can read about it here:
https://www.terraform.io/docs/cli/plugins/signing.html

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

Provision the resource with the `apply` command.

```shell
$ terraform apply
```

The command will take up to a few minutes to run and will display a message indicating that the resource was created.

## Destroying the Infrastructure

Destroy the infrastructure.

```shell
$ terraform destroy
```

Look for a message at the bottom of the output asking for confirmation. Type `yes` and hit ENTER. Terraform will destroy the resources it had created earlier.

## Next Steps

In this tutorial, you began creating infrastucture using Terraform.

Review the following resources to learn more about getting started with Terraform.

* [Introduction to Infrastructure as Code with Terraform](https://learn.hashicorp.com/tutorials/terraform/infrastructure-as-code?in=terraform/certification-associate-tutorials)

* [Install Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/certification-associate-tutorials)
