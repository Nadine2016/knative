---

copyright:
  years: 2020
lastupdated: "2020-04-28"

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

# About Coligo
{: #kn-about}

## What is Coligo and why do I want to use it? 
{: #kn-what}

Coligo is an open source platform that was developed by IBM. The goal is to extend the capabilities of Kubernetes to help you create modern, source-centric containerized, and serverless apps on top of your Kubernetes cluster. The platform is designed to address the needs of developers who today must decide what type of app they want to run in the cloud: 12-factor apps, containers, or functions. Each type of app requires an open source or proprietary solution that is tailored to these apps: Cloud Foundry for 12-factor apps, Kubernetes for containers, and OpenWhisk and others for functions. In the past, developers had to decide what approach they wanted to follow, which led to inflexibility and complexity when different types of apps had to be combined.

Coligo uses a consistent approach across programming languages and frameworks to abstract the operational burden of building, deploying, and managing workloads in Kubernetes so that developers can focus on what matters most to them: the source code. You can use proven build processes that you are already familiar with, such as Kaniko, Dockerfile, Bazel, and others. By integrating with Istio, Coligo ensures that your serverless and containerized workloads can be easily exposed on the internet, monitored, and controlled, and that your data is encrypted during transit.

## What is serverless?

### What is Coligo?
To deploy an app with Coligo, you must specify a Knative `Service` resource. Coligo is managed by the Knative `Serving` primitive and is responsible to manage the entire lifecycle of the workload. When you create the service, the Knative `Serving` primitive automatically creates a version for your serverless app and adds this version to the revision history of the service. Your serverless app is assigned a public URL from your Ingress subdomain in the format `<service_name>-<project>.<ingress_subdomain>` that you can use to access the app from the internet. In addition, a private hostname is assigned to your app in the format `<service_name>-<project>.cluster.local` that you can use to access your app from within the cluster.

### What happens behind the scenes when I create Coligo?
When you create a Coligo service, your app is automatically deployed as a Kubernetes pod in your cluster and exposed by using a Kubernetes service. To assign the public hostname, Coligo uses the IBM-provided Ingress subdomain and TLS certificate. Incoming network traffic is routed based on the default IBM-provided Ingress routing rules.

### How can I roll out a new version of my app?
When you update your Knative service, a new version of your serverless app is created. This version is assigned the same public and private hostnames as your previous version. By default, all incoming network traffic is routed to the latest version of your app. However, you can also specify the percentage of incoming network traffic that you want to route to a specific app version so that you can do A-B testing. You can split incoming network traffic between two app versions at a time, the current version of your app and the new version that you want to roll over to. 

[Knative](https://github.com/knative/docs){: external} is an open source platform that was developed by IBM, Google, Pivotal, Red Hat, Cisco, and others. The goal is to extend the capabilities of Kubernetes to help you create modern, source-centric containerized, and serverless apps on top of your Kubernetes cluster. 
{: shortdesc}

## About Coligo

### How does Coligo work?
Knative comes with two key components, or _primitives_, that help you to deploy and manage your serverless apps in your Kubernetes cluster:

- **Serving:** The `Serving` primitive helps to deploy serverless apps as Knative services and to automatically scale them, even down to zero instances. To expose your serverless and containerized workloads, Knative uses Istio. When you install the managed Knative add-on, the managed Istio add-on is automatically installed as well. By using the traffic management and intelligent routing capabilities of Istio, you can control what traffic is routed to a specific version of your service. These capabilities make it easy for a developer to test and roll out a new app version or do A-B testing.
- **Eventing:** With the `Eventing` primitive, you can create triggers or Event Streams that other services can subscribe to. For example, you might want to start a new build of your app every time code is pushed to your GitHub master repo. Or you want to run a serverless app only if the temperature drops below freezing point. For example, the `Eventing` primitive can be integrated into your CI/CD pipeline to automate the build and deployment of apps in case a specific event occurs.

## Coligo terminology

### Application

An *Application* runs your code to serve HTTP requests. The Application has a private URL for incoming requests. The number of running instances of an Application are automatically scaled up or down (to zero) based on incoming workload. 

An Application contains one or more *revisions* (revision entities). A revision represents an immutable version of the configuration properties of the Application. Each update of an application  configuration property creates a new revision of the Application.

### Components

*Components* are the building blocks of a project and are created using a container image.  Components include Applications and Job definitions.

### Job definition

A *Job definition* is a template that is used to run Jobs, and the template contains workload configuration information. After creating a Job definition, one or more *Jobs* can be submitted based on the Job definition, optionally overwriting values of the Job definition.

To work with Job definitions, you can:
- Create a Job definition
- List Job definitions
- Update a Job definition
- Delete a Job definition
- Submit and run a Job based on a Job definition from the console

### Job 

A *Job* runs your code to complete a task. A Job can run a large number of instances enabling work on large volumes of input data in parallel.

A Job is submitted based on a Job definition. After a Job definition is created, which contains the workload configuration, you can then run one or more Jobs that refer to the Job definition, optionally overwriting values of the Job definition.
 
Other than being a template for the Job configuration, there is no functional connection between a Job and the Job definition that is used for the Job submission. 

To work with Jobs, you can: 
- Submit (or run) a Job 
- List a Job
- Delete Job

### Project
A Project is a container for components, such as Applications and Job definitions. Projects enable you to manage resources and provide access to components in the Project.

A Project:
- Provides a unique namespace for entity names
- Groups entities and allows operations to work on them at once
- Helps manage access to project resources (inbound access)
- Helps manage access to backing services (outbound access)
- Has an automatically generated certificate for TLS
- Is based on a Kubernetes namespace



