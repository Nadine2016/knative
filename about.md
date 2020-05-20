---

copyright:
  years: 2020
lastupdated: "2020-05-20"

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


## Coligo terminology

### Application

An *application*, or app, runs your code to serve HTTP requests. An application has a URL for incoming requests. The number of running instances of an application are automatically scaled up or down (to zero) based on incoming workload. An application contains one or more revisions. A revision represents an immutable version of the configuration properties of the application. Each update of an application configuration property creates a new revision of the application.

### Job 
A *job* is a standalone executable for batch jobs and runs one or more containers according to a *job definition*. Unlike applications which react to incoming HTTP requests, jobs are meant to be used for running container images that contain an executable designed to run one time and then exit. Rather than specifying the full configuration of a job each time it is executed, you can create a job definition which acts as a template for the job and contains the workload configuration.

Other than being a template for the job configuration, there is no functional connection between a job and the job definition that is used for the job submission. 

### Job definition

A *job definition* is a like a template that contains the workload configuration for a job. After a job definition is created, you can then run one or more jobs that refer to the job definition to perform your task.

### Project
A *project* is a grouping of runtime components such as applications and job definitions. The grouping of components is up to you, but typically runtime components that are part of a larger application are grouped together. Projects are used to manage resources and provide access to components in the project. 

A project:
- Provides a unique namespace for entity names
- Groups entities and allows operations to work on them at once
- Helps manage access to project resources (inbound access)
- Helps manage access to backing services (outbound access)
- Has an automatically generated certificate for TLS
- Is based on a Kubernetes namespace

