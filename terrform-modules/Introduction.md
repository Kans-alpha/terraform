# Overview

As you manage your infrastructure with Terraform, increasingly complex configurations will be created. There is no intrinsic limit to the complexity of a single Terraform configuration file or directory, so it is possible to continue writing and updating your configuration files in a single directory. However, if you do, you may encounter one or more of the following problems:

### Understanding and navigating the configuration files will become increasingly difficult.
### Updating the configuration will become more risky, because an update to one block may cause unintended consequences to other blocks of your configuration.
### Duplication of similar blocks of configuration may increase, for example, when you configure separate dev/staging/production environments, which will cause an increasing burden when updating those parts of your configuration.
### If you want to share parts of your configuration between projects and teams, cutting and pasting blocks of configuration between projects could be error-prone and hard to maintain.

In this lab, you will learn how modules can address these problems, the structure of a Terraform module, and best practices when using and creating modules.

## What are modules for?

Here are some of the ways that modules help solve the problems listed above:

Organize configuration: Modules make it easier to navigate, understand, and update your configuration by keeping related parts of your configuration together. Even moderately complex infrastructure can require hundreds or thousands of lines of configuration to implement. By using modules, you can organize your configuration into logical components.

Encapsulate configuration: Another benefit of using modules is to encapsulate configuration into distinct logical components. Encapsulation can help prevent unintended consequences—such as a change to one part of your configuration accidentally causing changes to other infrastructure—and reduce the chances of simple errors like using the same name for two different resources.

Re-use configuration: Writing all of your configuration without using existing code can be time-consuming and error-prone. Using modules can save time and reduce costly errors by re-using configuration written either by yourself, other members of your team, or other Terraform practitioners who have published modules for you to use. You can also share modules that you have written with your team or the general public, giving them the benefit of your hard work.

Provide consistency and ensure best practices: Modules also help to provide consistency in your configurations. Consistency makes complex configurations easier to understand, and it also helps to ensure that best practices are applied across all of your configuration. For example, cloud providers offer many options for configuring object storage services, such as Amazon S3 (Simple Storage Service) or Google's Cloud Storage buckets. Many high-profile security incidents have involved incorrectly secured object storage, and because of the number of complex configuration options involved, it's easy to accidentally misconfigure these services.

Using modules can help reduce these errors. For example, you might create a module to describe how all of your organization's public website buckets will be configured, and another module for private buckets used for logging applications. Also, if a configuration for a type of resource needs to be updated, using modules allows you to make that update in a single place and have it be applied to all cases where you use that module.

What you'll learn

In this lab, you will learn how to perform the following tasks:

Use a module from the Registry

Build a module


What is a Terraform module?

A Terraform module is a set of Terraform configuration files in a single directory. Even a simple configuration consisting of a single directory with one or more .tf files is a module. When you run Terraform commands directly from such a directory, it is considered the root module. So in this sense, every Terraform configuration is part of a module. You may have a simple set of Terraform configuration files like this:

$ tree minimal-module/
.
├── LICENSE
├── README.md
├── main.tf
├── variables.tf
├── outputs.tf
In this case, when you run Terraform commands from within the minimal-module directory, the contents of that directory are considered the root module.

Calling modules

Terraform commands will only directly use the configuration files in one directory, which is usually the current working directory. However, your configuration can use module blocks to call modules in other directories. When Terraform encounters a module block, it loads and processes that module's configuration files.

A module that is called by another configuration is sometimes referred to as a "child module" of that configuration.

Local and remote modules

Modules can be loaded from either the local filesystem or a remote source. Terraform supports a variety of remote sources, including the Terraform Registry, most version control systems, HTTP URLs, and Terraform Cloud or Terraform Enterprise private module registries.

Module best practices

In many ways, Terraform modules are similar to the concepts of libraries, packages, or modules found in most programming languages, and they provide many of the same benefits. Just like almost any non-trivial computer program, real-world Terraform configurations should almost always use modules to provide the benefits mentioned above.

It is recommended that every Terraform practitioner use modules by following these best practices:

Start writing your configuration with a plan for modules. Even for slightly complex Terraform configurations managed by a single person, the benefits of using modules outweigh the time it takes to use them properly.

Use local modules to organize and encapsulate your code. Even if you aren't using or publishing remote modules, organizing your configuration in terms of modules from the beginning will significantly reduce the burden of maintaining and updating your configuration as your infrastructure grows in complexity.

Use the public Terraform Registry to find useful modules. This way you can quickly and confidently implement your configuration by relying on the work of others.

Publish and share modules with your team. Most infrastructure is managed by a team of people, and modules are an important tool that teams can use to create and maintain infrastructure. As mentioned earlier, you can publish modules either publicly or privately. You will see how to do this in a later lab in this series.
