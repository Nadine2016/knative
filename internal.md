---

copyright:
  years: 2020
lastupdated: "2020-04-30"

keywords: knative, getting started

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

# Getting started with Project Coligo for Internal adopters
{: #getting-started-internal}

Review internal only information to get access to Project Coligo (or "Coligo") 
{: shortdesc}

## Where can I find the Coligo console?

Access to Coligo console is available at [Project Coligo test](https://test.cloud.ibm.com/knative/overview){: external}. Log in with your IBM ID. 

## How do I get the CLI?

You must create an [{{site.data.keyword.cloud_notm}} account on TEST](https://test.cloud.ibm.com/){: external}. If you do not have one, you can create one by accessing the URL. If you cannot create one, ask on the #bss-account-issues channel in the IBM Cloud Platform slack.

1. Download and install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/reference/ibmcloud?topic=cloud-cli-getting-started). 

2. Install the Coligo CLI plugin

   ```
   ibmcloud plugin repo-add staging https://plugins.test.cloud.ibm.com
   ibmcloud plugin install coligo -r staging
   ```
   {: pre}


3. Install knative CLI `kn`

    * Download the kn from the [source](https://storage.googleapis.com/knative-nightly/client/latest/kn-darwin-amd64) for Mac
    * Copy it to your PATH with `mv ~/Downloads/kn-darwin* /usr/local/bin/kn`
    * Make it executable with `chmod +x /usr/local/bin/kn`

    Follow instructions at [release page](https://github.com/knative/client/blob/master/docs/README.md#installing-kn) for specific environments.
    

4. Log into Test IBM Cloud

   ```
   ibmcloud login -a https://test.cloud.ibm.com --sso
   ```
   {: pre}

5. If you have more than one account, select one from the list. 

6.  Select `us-south` as the target region.

7.  List your resource groups and select one to target

   ```
   ibmcloud resource groups
   ```
   {: pre}

8. Target a resource group.

   ```
   ibmcloud target -g <GROUP_NAME>
   ```
   {: pre}        

You can now proceed to [Managing projects](/docs/knative?topic=knative-knative-manage-project)!

## Where can I get help?

You can get help from Project Coligo #coligo-users slack channel.
