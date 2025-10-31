# Terraform-Demo

Terraform is an infrastructure as code tool that lets you build, change, and version infrastructure safely and efficiently. This includes low-level components like compute instances, storage, and networking, as well as high-level components like DNS entries and SaaS features.

<img width="2048" height="644" alt="image" src="https://github.com/user-attachments/assets/07a49980-7388-45e1-95e7-6eb4c3525cc0" />


Terraform creates and manages resources on cloud platforms and other services through their application programming interfaces (APIs). 
Providers enable Terraform to work with virtually any platform or service with an accessible API.


The core Terraform workflow consists of three stages:

Write: You define resources, which may be across multiple cloud providers and services. 
For example, you might create a configuration to deploy an application on virtual machines in a Virtual Private Cloud (VPC) network with security groups and a load balancer.


Plan: Terraform creates an execution plan describing the infrastructure it will create, update, or destroy based on the existing infrastructure and your configuration.


Apply: On approval, Terraform performs the proposed operations in the correct order, respecting any resource dependencies. 

For example, if you update the properties of a VPC and change the number of virtual machines in that VPC, Terraform will recreate the VPC before scaling the virtual machines.

Case: 01

Meta-arguments in Terraform: 

Meta-arguments in Terraform are special, built-in arguments that control the behavior of resources and modules, rather than configuring resource-specific attributes. They provide a way to manage the lifecycle, dependencies, and instantiation of infrastructure objects.
Here are the key meta-arguments in Terraform: 
count: Used to create multiple identical instances of a resource or module. It accepts a whole number, and each instance is managed individually by Terraform.
Code

    resource "aws_instance" "example" {
      count = 3
      ami           = "ami-0abcdef1234567890"
      instance_type = "t2.micro"
    }
for_each: Provides a more flexible way to create multiple instances, allowing iteration over a set or map of values. This enables the creation of customized resources based on the unique keys and values in the collection.
Code

    resource "aws_s3_bucket" "website_buckets" {
      for_each = toset(["my-first-bucket", "my-second-bucket"])
      bucket = each.value
    }
depends_on: Establishes explicit dependencies between resources or modules. This ensures that a specific resource or module is created or updated only after its dependencies are fulfilled, even if Terraform's implicit dependency analysis doesn't capture it.
Code

    resource "aws_instance" "web" {
      # ...
      depends_on = [aws_db_instance.main_db]
    }
lifecycle: Controls the behavior of resource creation, updates, and destruction. It includes arguments like prevent_destroy, create_before_destroy, and ignore_changes to customize how Terraform manages resource changes.
Code

    resource "aws_instance" "example" {
      # ...
      lifecycle {
        prevent_destroy = true
        ignore_changes = [tags]
      }
    }
provider: Specifies which provider configuration should be used for a particular resource or module, especially when multiple configurations of the same provider are defined.
Code

    resource "aws_instance" "example" {
      provider = aws.us_east_1
      # ...
    }
Meta-arguments are essential for building complex and robust infrastructure as code with Terraform, enabling efficient management of resource lifecycles and dependencies.


