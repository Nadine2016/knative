---

copyright:
  years: 2020
lastupdated: "2020-04-13"

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

## What is Coligo and why do I want use it? 
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

## About {{site.data.keyword.openwhisk_short}} with Knative

### How does {{site.data.keyword.openwhisk_short}} with Knative work?
Knative comes with two key components, or _primitives_, that help you to deploy and manage your serverless apps in your Kubernetes cluster:

- **Serving:** The `Serving` primitive helps to deploy serverless apps as Knative services and to automatically scale them, even down to zero instances. To expose your serverless and containerized workloads, Knative uses Istio. When you install the managed Knative add-on, the managed Istio add-on is automatically installed as well. By using the traffic management and intelligent routing capabilities of Istio, you can control what traffic is routed to a specific version of your service, which makes it easy for a developer to test and roll out a new app version or do A-B testing.
- **Eventing:** With the `Eventing` primitive, you can create triggers or event streams that other services can subscribe to. For example, you might want to kick off a new build of your app every time code is pushed to your GitHub master repo. Or you want to run a serverless app only if the temperature drops below freezing point. For example, the `Eventing` primitive can be integrated into your CI/CD pipeline to automate the build and deployment of apps in case a specific event occurs.

## {{site.data.keyword.openwhisk_short}} terminology

<dl>
  <dt>Application</dt>
    <dd>An **application** is containerized code that is called through an HTTP request. Build your applications in any language, using your favorite libraries, dependencies and tools. When not in use, your application autoscales to zero. Applications are organized by projects.</dd>
  <dt>Component</dt>
    <dd>**Components** are the building blocks of a project and are created using a container image.  Components include applications and job definitions. </dd>
  <dt>Job definition</dt>
    <dd>A **job definition** defines the static workload configuration which can be used by or referenced by one or more job runs.  For example, for reuse, you can create JobDefinition resources that serve as a template and can be referenced from JobRuns. Once your job definition defines the workload configuration, you can create multiple job runs that refer to this job definition, optionally overwriting some of the properties specified in the JobDefinition. </dd>
  <dt>Job run</dt>
    <dd>A **job run** is the action of running a Coligo job.  Running a job requires that a job definition exist for the job. </dd> 
  <dt>Project</dt>
    <dd>**Projects** are used to group and organize components, such as applications or jobs. You can also assign access policies to a project.</dd> 
  <dt>Revision</dt>
    <dd>A **Revision** is a job that has been modified or changed. For example, you might modify environment variables.</dd> 
<dl>

