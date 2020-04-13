---

copyright:
  years: 2020
lastupdated: "2020-04-13"

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

# Installing, updating, and deleting the Coligo CLI
{: #kn-install-cli}

Install, update, and delete the required CLIs and set up your environment to use Coligo.
{: shortdesc}

## Install Knative plugin

## Setting up the {{site.data.keyword.cloud_notm}} CLI
{: #cli_setup}

Install the latest version of the IBM Cloud CLI.
{:shortdesc}

**Before you begin**

You must create an [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/){: external}.

1. Download and install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/reference/ibmcloud?topic=cloud-cli-install-ibmcloud-cli).

2. Log in to the {{site.data.keyword.cloud_notm}} CLI.

  ```
  ibmcloud login
  ```
  {: pre}

3. If you have more than one account, you are prompted to select which account to use. Follow the prompts or use the `target` command to select your {{site.data.keyword.cloud_notm}} account.

  ```
  ibmcloud target -c <account_id>
  ```
  {: pre}

4. You must also specify a region. You can use the `target` command to target or change regions.
  
  ```
  ibmcloud target -r <region>
  ```
  {: pre}

5. You must specify a resource group. To get a list of your resource groups, run the following command.

  ```
  ibmcloud resource groups
  ```
  {: pre}

  **Example output**

  ```
  Retrieving all resource groups under account <account_name> as email@ibm.com...
  OK
  Name      ID                                 Default Group   State   
  default   a8a12accd63b437bbd6d58fb8b462ca7   true            ACTIVE
  test      a8a12abbbd63b437cca6d58fb8b462ca7   false           ACTIVE
  ```
  {: screen}

6. Target a resource group by running the following command.

  ```
  ibmcloud target -g <resource_group>
  ```
  {: pre}

  **Example output**

  ```
  Targeted resource group default
  ```
  {: screen}

## Installing the Coligo CLI plug-in
{: #kn-install-cli-plugin}


Complete the following steps to install the Coligo CLI plug-in

1. Install the Coligo plug-in.

  ```
  ibmcloud plugin install PLUGINNAME
  ```
  {: pre}

2. Verify that the plug-in is installed.

  ```
  ibmcloud plugin list
  ```
  {: pre}

  **Example Output**

  ```
  Plugin Name          Version
  PLUGINNAME
  ```
  {: screen}

3. All Coligo commands begin with `ibmcloud coligo`. To see everything that you can do with the Coligo plug-in, run `ibmcloud coligo` with no arguments.

  ```
  ibmcloud coligo
  ```
  {: pre}
  
4. Optionally, install [`jq`](https://stedolan.github.io/jq){: external} to process JSON in the command line. This package allows you to view and parse JSON responses in the command line.

For more information about Coligo commands, see the [`ibmcloud coligo` commands](/docs/knative?topic=knative-kn-cli).


## Updating the Coligo CLI
{: #kn-update-cli}

Update the CLI periodically to take advantage of new features.

1. View your current plug-in list by running `ibmcloud plugin list` command.

   ```
   ibmcloud plugin list
   ```
   {: pre}
   
   **Example Output**
   
   ```
   Plugin Name                                 Version   Status        
   Coligo                              1.0       Update Available   
   cloud-object-storage                        1.1.0        
   container-registry                          0.1.437      
   container-service/kubernetes-service        0.4.51       
   ```
   {: screen}

2. If an update is available, run the `ibmcloud plugin update` command.

   ```
   ibmcloud plugin update coligo
   ```
   {: pre}



## Uninstalling the CLI
{: #kn-uninstall-cli}

If you no longer need the CLI, you can uninstall it.

To uninstall the CLIs

1. List the plug-ins that are installed.
   
   ```
   ibmcloud plugin list
   ```
   {: pre}
   
2. Uninstall the plug-ins. For example, to uninstall the Coligo CLI plug-in:
   
   ```
   ibmcloud plugin uninstall Coligo
   ```
   {: pre}
   
3. Verify the plug-ins were uninstalled by running the following command and checking the list of the plug-ins that are installed.

   ```
   ibmcloud plugin list
   ```
   {: pre}

The plug-ins that you deleted are not displayed in the results.
