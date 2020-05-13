---

copyright:
  years: 2020
lastupdated: "2020-05-13"

keywords: knative

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

# FAQs
{: #kn-faqs}

Answers to common questions about the Coligo service.
{:shortdesc}


## What is Coligo? 
{: #what-is-knative}
{: faq}
{: support}

Coligo is an open source platform that was developed by IBM. The goal is to extend the capabilities of Kubernetes to help you create modern, source-centric containerized, and serverless apps on top of your Kubernetes cluster. The platform is designed to address the needs of developers who today must decide what type of app they want to run in the cloud: 12-factor apps, containers, or functions. For more information, see [About Coligo](/docs/knative?topic=knative-kn-about).

## What is a Project? 
{: #what-is-project}
{: faq}
{: support}

A *Project* in a Coligo service is used to group and organize components, such as applications or jobs.  Projects enable you to manage resources and provide access to components in the Project. You can also assign access policies to a Project.

You can think of a Project like a folder on your desktop.  A Project functions as a grouping mechanism for runtime artifacts that you want to host on the IBM Cloud. The way you group components together into Projects is based on how you want them organized.   

## What is an Application?  
{: #what-is-app}
{: faq}
{: support}

An *Application* in a Coligo service that runs your code to serve HTTP requests. Applications  are organized and run within a defined [Project](#what-is-project).

Build your code in any language, using your favorite libraries, dependencies, and tools. When you create your Application, you will specify the where your code resides. The Application has a URL for incoming requests.  

The number of running instances of an Application are automatically scaled up or down (to zero) based on incoming workload. 

An Application contains one or more *revisions* (revision entities). A revision represents an immutable version of the configuration properties of the Application. Each update of an application configuration property creates a new revision of the Application.

## What is a Job?   
{: #what-is-job}
{: faq}
{: support}

A *Job* runs your code in a Coligo service to complete a task. 

A Job is submitted based on a [Job definition](#what-is-jobdef). After a Job definition is created, which contains the workload configuration, you can then run one or more Jobs that refer to the Job definition, optionally overwriting values of the Job definition. The Job runs within a defined [Project](#what-is-project). 

A Job can run a large number of instances enabling work on large volumes of input data in parallel.

## What is a Job definition?   
{: #what-is-jobdef}
{: faq}
{: support}

A *Job definition* is a template that is used to run a [Job](#what-is-job), and the template contains workload configuration information. After creating a Job definition, you can submit one or more Jobs based on the Job definition, optionally overwriting values of the Job definition.

 ## What is the relationship between a Job and a Job definition?   
{: #what-is-jobvsjobdef}
{: faq}
{: support}

A [Job definition](#what-is-jobdef) defines the workload configuration and must be created before a *Job* can be created and run. 

A [Job](#what-is-job) can run one or more containers in a Coligo service. Multiple jobs can refer to the same Job definition.

Other than a Job definition being a template for the configuration of a Job, there is no functional connection between a Job and the Job definition that is used for the Job submission. 

