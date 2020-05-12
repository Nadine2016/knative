---

copyright:
  years: 2020
lastupdated: "2020-05-12"

keywords: about, knative

subcollection: knative

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}

# About Project Coligo
{: #kn-about}

## What is Project Coligo and why do I want to use it? 
{: #kn-what}

Project Coligo (or "Coligo")  was developed by IBM with the goal of helping you create modern, source-centric containerized, and serverless apps on top of your Kubernetes cluster. The platform is designed to address the needs of developers who today must decide what type of app they want to run in the cloud: 12-factor apps, containers, or functions. Each type of app requires an open source or proprietary solution that is tailored to these apps: Cloud Foundry for 12-factor apps, Kubernetes for containers, and OpenWhisk and others for functions. In the past, developers had to decide what approach they wanted to follow, which led to inflexibility and complexity when different types of apps had to be combined.

Coligo uses a consistent approach across programming languages and frameworks to abstract the operational burden of building, deploying, and managing workloads in Kubernetes so that developers can focus on what matters most to them: the source code. By integrating with Istio, Coligo ensures that your serverless and containerized workloads can be easily exposed on the internet, monitored, and controlled, and that your data is encrypted during transit.

### What happens behind the scenes when I create Coligo?
When you create a Coligo service, your app is automatically deployed as a Kubernetes pod in your cluster and exposed by using a Kubernetes service. To assign the public hostname, Coligo uses the IBM-provided Ingress subdomain and TLS certificate. Incoming network traffic is routed based on the default IBM-provided Ingress routing rules.

### How can I roll out a new version of my app?
When you update your application, a new version, or revision, of your app is created. This revision is assigned the same public and private hostnames as your previous version of your app. By default, all incoming network traffic is routed to the latest revision.

## Coligo terminology

### Application

An *Application* runs your code to serve HTTP requests. The Application has a private URL for incoming requests. The number of running instances of an Application are automatically scaled up or down (to zero) based on incoming workload. 

An Application contains one or more *revisions* (revision entities). A revision of your app represents an immutable version of the configuration properties of the Application. Each update of an application  configuration property creates a new revision of the Application.

### Components

*Components* are the building blocks of a Project. Components include Applications and Job definitions.

### Job definition

A *Job definition* is a template that is used to run Jobs, and the template contains workload configuration information. After a Job definition is created, one or more *Jobs* can be submitted based on the Job definition, optionally overwriting values of the Job definition.

To work with Job definitions, you can:
- Create a Job definition
- List Job definitions
- Update a Job definition
- Delete a Job definition
- Submit and run a Job based on a Job definition from the console or the CLI

### Job 

A *Job* runs your code to complete a task. A Job can run many instances, which enables work on large volumes of input data in parallel.

A Job is submitted based on a Job definition. After a Job definition is created, which contains the workload configuration, you can then run one or more Jobs that refer to the Job definition, optionally overwriting values of the Job definition.
 
Other than being a template for the Job configuration, there is no functional connection between a Job and the Job definition that is used for the Job submission. 

To work with Jobs, you can: 
- Submit (or run) a Job 
- List a Job
- Delete Job

### Project
A Project is a container for components, such as Applications and Job definitions. Use Projects to manage resources and provide access to components in the Project.

A Project:
- Provides a unique namespace for entity names
- Groups entities and allows operations to work on them at once
- Helps manage access to project resources (inbound access)
- Helps manage access to backing services (outbound access)
- Has an automatically generated certificate for TLS
- Is based on a Kubernetes namespace



