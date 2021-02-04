---
title: "Terraform? What's that?"
date: 2021-02-04
description: "One of the most common questions from IT Ops professionals is 'what's Terraform' and 'why is it so popular'. Let me explain you in this blog a bit about this amazing technology."
tags: [terraform, iac, infrastructure, ops, deploy, sre, devops]
---

## So... what's Terraform?

Let's start answering the question "what's Terraform". Terraform is a CLI (command line interface) tool created by [Hashicorp](https://www.hashicorp.com/), a company that provides several tools to make IT professionals lives easier. The tool is used to deploy lots different resources from a huge variety of technology stacks. You can deploy infrastructures in most of available **cloud providers** or even create new dashboards in your own Grafana instance.

Terraform helps us to have all our **infrastructure as code**. IaC is basically the process or "work methodology" of having our infrastructure defined in text/code files, so we can delete all our resources and deploy them back as nothing happened. Those files can have different file extensions, like `.tf`, `.tfstate`, `.tfvars`. This is how a `main.tf` file could look like:

```
# Configure the Azure Provider
provider "azurerm" {
  # whilst the `version` attribute is optional, we recommend pinning to a given version of the Provider
  version = "=2.40.0"
  features {}
}

# Create a resource group
resource "azurerm_resource_group" "example" {
  name     = "example-resources"
  location = "West Europe"
}

# Create a virtual network within the resource group
resource "azurerm_virtual_network" "example" {
  name                = "example-network"
  resource_group_name = azurerm_resource_group.example.name
  location            = azurerm_resource_group.example.location
  address_space       = ["10.0.0.0/16"]
}
```

Terraform is almost always used together with a version-control system. Here you can find a [Github repository](https://github.com/jason-morsley/terraform-azure-linux-virtual-machine) with a "real" example. You could just clone that repository, follow the steps from the README and with the next commands you could have your own `Linux Virtual Machine` deployed in Azure:

```
terraform init
terraform plan
terraform apply
```

## How to install Terraform

Depending on your needs there are different instructions to install Terraform. [Just click here](https://learn.hashicorp.com/tutorials/terraform/install-cli), **BUT** for MacOS users a have some tips for you as I'm a Macbook user.

Mac OS users will probably know the package manager called **Homebrew**. In case it's the first time you hear about it... where the hell have you been during this whole time? Just kidding, [click here in case you need to install it](https://brew.sh/).

There's a tool called **tfenv** that will help us to have more than one Terraform installation in our computer. Type the next commands in your terminal to install it and start using Terraform 0.14.1:

```
brew install tfenv
tfenv install 0.14.1
tfenv use 0.14.1
```

## Providers

Hey hey, I know you want to start creating your first `.tf` files, but you still need to know some things first. I will use Terraform website to describe you what are  **Providers**:

`Providers are plugins that implement resource types. Find providers for the cloud platforms and services you use, add them to your configuration, then use their resources to provision infrastructure.`

That maybe can sound a bit confusing, but let me show an example on how to use it a provider so you understand this better.

Let's think that we have our own subscription in the amazing cloud provider Azure. If we go to [Terraform registry](https://registry.terraform.io/browse/providers) you can see that there are tons of providers, but in this case we want to know more about [Azure provider](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs). I highly suggest you that you check that link, as it gives a very good explanation about how to use the provider.

One important note about providers is that **each provider has its own versioning**. This means that you Azure provider latest version can be 2.45.0 and AWS provider latest one could be 3.26.0.

**Terraform and provider versions** aren't the same. Hashicorp adds new versions to fix or add feature from the tool itself and the provider adds new versions because Azure released a new type of Cloud Database.

## The important question... why should you use Terraform?

The way we deploy infrastructure is changing. In the past we used to deploy Virtual Machines and install or the services we wanted inside them. However this isn't even the present anymore. Infrastructures are becoming completely cloud oriented, companies have bet for microservices, we don't want anymore to have a bunch of virtual machines with several services configured inside them and perform hourly or daily backups to ensure that in case of failure we will be able to restore the service. The game has changed.

Companies want to be able to deploy and destroy their infrastructure as many times as needed without impacting the service, and there is where Terraform will help us. With Terraform and the help of provisioning and CI/CD tools we are currently able to deploy and destroy Kubernetes, containers, virtual machines, functions, databases, caches, whatever we want with one click.

## Do you want to learn more about this awesome technology?

I wanted to show you a bit of what's Terraform so you can start thinking if it's a good opportunity to start using it. Let me give give you some links so you can start practising from your side:

- https://learn.hashicorp.com/tutorials/terraform/azure-build?in=terraform/azure-get-started
- https://www.terraform.io/docs/language/index.html
- https://www.terraform.io/docs/language/functions/index.html