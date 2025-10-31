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


