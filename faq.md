---

copyright:
  years: 2020
lastupdated: "2020-04-17"

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

## What is Project? 
{: #what-is-project}
{: faq}
{: support}

A *project* in a Coligo service is used to group and organize components, such as applications or jobs. You can also assign access policies to a project.

## What is an Application?  
{: #what-is-app}
{: faq}
{: support}

An *application* in a Coligo service is containerized code that is called through an HTTP request. Build your applications in any language, using your favorite libraries, dependencies and tools. When not in use, your application autoscales to zero. Applications are organized by projects.

## What is a Job?   
{: #what-is-job}
{: faq}
{: support}

A *job* can run one or more containers in a Coligo service.  A *job definition* defines the workload configuration and must be created before the *job* can be created and run. Multiple jobs can refer to a job definition.  Once your job definition defines the workload configuration, you can create multiple job runs that refer to this job definition, optionally overwriting some of the properties specified in the job definition. The job runs within a defined *project*. 

## What am I charged for when I use Coligo ?   
{: #what-is-billing}
{: faq}
{: support}

placeholder 

