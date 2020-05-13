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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:troubleshoot: data-hd-content-type='troubleshoot'}

# Troubleshooting tips
{: #kn-troubleshoot}

Use the troubleshooting tips to learn how to troubleshoot Coligo.
{: shortdesc}

## Why can't I access a project?
{: #ts-access-project}
{: troubleshoot}

You cannot access a project that was created by someone else.
{: tsSymptoms}
   
Whenever you use an IBM Cloud account to create or use a project that is not owned by you, you must be assigned proper system roles. 
{: tsCauses}

To perform operations with a project that is not owned by you, you must have `Viewer` set for `Platform Access` and `Reader` for `Service Access`. For more information, see [Managing user access](/docs/knative?topic=knative-knative-iam).
{: tsResolve}

## Why can't I create a project?
{: #ts-create-project}
{: troubleshoot}

You cannot create a project in your resource group.
{: tsSymptoms}
   
There are several reasons why you might not be able to create a project in your resource group.

- Your project name must be unique in the region. 
- You might already have a project in the region. During the Experimental release, you are limited to creating a single project in a region.
- You must have the proper platform access to create a project. 
{: tsCauses}

- If you receive a warning message about your project name not being unique, select a different name. 
- You can create only one project per region. For more information, see [Experimental release limitations](/docs/knative?topic=knative-kn-limits#kn-limits_experimental).
- In order to create a project, you must have `Administrator` set for `Platform Access` and `Reader` for `Service Access`. For more information, see [Managing user access](/docs/knative?topic=knative-knative-iam).
{: tsResolve}
