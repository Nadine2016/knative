---

copyright:
  years: 2020
lastupdated: "2020-04-24"

keywords: knative, project

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
{:preview: .preview}

# Managing projects
{: #manage-project}

Learn how to create and target projects. 
{: #shortdesc} 

## What is a project?
With Coligo, you can create Identity and Access (IAM) managed projects to group components, such as applications or jobs. Then, you can create IAM access policies for the projects. For an overview of IAM, see [Managing user access](/docs/knative?topic=knative-knative-iam). Projects incur no costs, but instead serve as folders for your applications and jobs.

### How can I see what projects I can access?

You can see a list of your projects in the [Coligo console](https://cloud.ibm.com/coligo){: external}.

You can also run the [`project list`](/docs/knative?topic=knative-kn-cli#cli-project-list) command. 

```
ibmcloud coligo project list
```
{: pre}

**Example output**

```
name          type            id                                    description

```
{: screen}


### How can I see what a project contains?

You can see a list of your project components by selecting a project from [Coligo console](https://cloud.ibm.com/coligo){: external}.

You can also run the [`project get`](/docs/knative?topic=knative-kn-cli#cli-project-get) command. Replace `PROJECT_NAME` with the name of your project.

```
ibmcloud coligo project get --name PROJECT_NAME
```
{: pre}

## Create a project
You can create a project through the console or with the CLI.
{: #shortdesc} 

### Create a project through the console

1. From the [Coligo console](https://cloud.ibm.com/coligo){: external} project menu, select **Create Project**.
2. Enter a display name for the namespace and a short description, such as the actions or packages that you plan to create in this namespace.
3. Choose the resource group where you want to create the project and a location to deploy the project.
4. Click **Create**.

To view the service instance for the project resource, go to your [{{site.data.keyword.cloud_notm}} dashboard ](https://cloud.ibm.com/resources){: external} and find your namespace name in **Coligo Projects**.

You can update the name or description of the project from the **Projects Settings** page in the Coligo console.

### Create a project with the CLI

1. Install the [Coligo CLI](/docs/knative?topic=knative-kn-install-cli). Target the resource group that you want to use for the project. 

2. Create a project with the [`project create`](/docs/knative?topic=knative-kn-cli#cli-project-create) command. Optional: Include a description for your project by using the `-d` or `--description` flag. If your description is longer than one word, it must be in quotations.

  ```
  ibmcloud coligo project --name PROJECT_NAME [--description PROJ_DESC]
  ```
  {: pre}

  Example output:

  ```
  ok: created project myProject
  ```
  {: screen}

3. Verify that your new project is created with the [`project get`](/docs/knative?topic=knative-kn-cli#cli-project-get) command.

  ```
  ibmcloud coligo project get --name PROJ_NAME
  ```
  {: pre}

  Example output:

  ```
  Details of project TBD
  ```
  {: screen}

  You can also list all projects:

  ```
  ibmcloud coligo project list
  ```
  {: pre}

## Target a project
After you create a project, target it for use with Coligo. You can use the console or the CLI.
{: #shortdesc} 

### Target a project through the console

From the [Coligo console](https://cloud.ibm.com/coligo){: external} project menu, select target project.

### Target a project with the CLI
To target a project with the CLI, use the [`project target`](/docs/knative?topic=knative-kn-cli#cli-project-target) command. 

```
ibmcloud coligo project target --name PROJECT_NAME
```
{: pre}

## Delete a project
When you no longer need a project, you can delete it. Deleting a project deletes all of the components that it contains. You can use the console or the CLI.
{: #shortdesc} 

### Delete a project through the console

From the [Coligo console](https://cloud.ibm.com/coligo){: external} project menu, select delete project.

### Delete a project through the CLI
To delete a project with the CLI, use the [`project delete`](/docs/knative?topic=knative-kn-cli#cli-project-delete) command. 

```
ibmcloud coligo project delete --name PROJECT_NAME
```
{: pre}
