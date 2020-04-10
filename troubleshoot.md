---

copyright:
  years: 2020
lastupdated: "2020-1-31"

keywords: knative

subcollection: functions

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

# Troubleshooting tips
{: #kn-troubleshoot}

Use the troubleshooting tips to learn how to troubleshoot Knative service.
{: shortdesc}

## Set up an IAM policy for Functions namespace

There might be the case that you are using an IBM Cloud account to create or use a functions namespace(s) that is not owned by you.

In order to perform operations with the functions namespaces, you must have the right Access Policy applied to you as a user by the Account Owner or by someone with Admin access to the IBM Cloud Account in question. NOTE - The steps defined below can be done only by the Account Owner or someone with Admin access to the Cloud Account. For more information, see Understanding IAM and IAM Best practices.

If you wish to access existing Functions namespace for creating kn services as describe in the guide, please do the following: Visit IAM Access to provide the right access to the concerned user.
If the user already exists in the list, select the option to Assign Access. 
