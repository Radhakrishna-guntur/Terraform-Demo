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


Case: 08

𝐓𝐞𝐫𝐫𝐚𝐟𝐨𝐫𝐦 𝐏𝐫𝐨𝐯𝐢𝐬𝐢𝐨𝐧𝐞𝐫𝐬:

<img width="720" height="404" alt="image" src="https://github.com/user-attachments/assets/44adac85-3f19-4a8c-aa06-f3666ef98add" />

In Terraform, 𝐏𝐫𝐨𝐯𝐢𝐬𝐢𝐨𝐧𝐞𝐫𝐬 are a set of built-in functionalities that allow you to execute scripts, commands, or other configuration actions on remote resources after they’ve been created or destroyed. 

Provisioners are often used for tasks like initializing software, configuring instances, or performing post-deployment setup. There are different types of provisioners in Terraform, each serving a specific purpose. Let’s explore the main types of provisioners and how to write them:


𝟏.𝐋𝐨𝐜𝐚𝐥-𝐞𝐱𝐞𝐜 𝐏𝐫𝐨𝐯𝐢𝐬𝐢𝐨𝐧𝐞𝐫:

The `local-exec` provisioner allows you to run commands or scripts on the machine where Terraform is executed, typically your local development machine or a CI/CD server. This provisioner is often used for tasks that don’t require access to the remote resource.


Example:


<img width="407" height="218" alt="image" src="https://github.com/user-attachments/assets/8831e5f2-fa3f-4bd7-ab19-e554829f1356" />



In this example, the `local-exec` provisioner runs the `echo` command on the local machine after the AWS EC2 instance is created.

𝟐. 𝐑𝐞𝐦𝐨𝐭𝐞-𝐞𝐱𝐞𝐜 𝐏𝐫𝐨𝐯𝐢𝐬𝐢𝐨𝐧𝐞𝐫:

The `remote-exec` provisioner allows you to run commands or scripts on a remote resource over SSH or WinRM after the resource is created. This provisioner is commonly used for tasks like software installations and configuration on remote instances.


Example:


<img width="462" height="428" alt="image" src="https://github.com/user-attachments/assets/0974444a-1883-4128-a855-f1ba095b5588" />



In this example, the `remote-exec` provisioner connects to the newly created EC2 instance using SSH and executes the specified inline script.

𝟑. 𝐅𝐢𝐥𝐞 𝐏𝐫𝐨𝐯𝐢𝐬𝐢𝐨𝐧𝐞𝐫:

The `file` provisioner allows you to copy files or directories from the local machine to a remote resource after it’s created. This provisioner is useful for transferring configuration files, scripts, or other assets to a remote instance.


Example:

<img width="389" height="393" alt="image" src="https://github.com/user-attachments/assets/e9793f4a-fb78-4056-a56b-d65345d1e67b" />



In this example, the `file` provisioner copies a local file to the `/tmp` directory on the remote EC2 instance using SSH.



Case: 09

DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit-millisecond latency at any scale. Its flexible data model and reliable performance make DynamoDB a great fit for mobile, web, gaming, advertising technology, Internet of Things, and other applications.

Case: 10

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


