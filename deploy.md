---

copyright:
  years: 2020
lastupdated: "2020-04-15"

keywords: knative

subcollection: knative

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Deploying application workloads
{: #knative-deploy-app}

Deploy your app with Coligo.
{: #shortdesc} 

## What kind of services can I deploy? 


## Can I keep my service private?


## Can I use my own custom domain or IP address?


**Before you begin**:
* Set up your [Coligo](/docs/knative?topic=knative-kn-install-cli) environment
* [Target a project](/docs/knative?topic=knative-manage-project)
* Application as an image file

## Deploying an application from console
{: #deploy-app-console}

The following steps describe how to deploy an application using the Coligo console.
1. Access the Coligo.
2. Select a project from the list of available projects. You can also [create a new one](/docs/knative?topic=knative-manage-project).
3. From the Projects page, click the name of your project to open the project component page. 
4. From your project component page, select **Create component**.
5. Select **Application** as your component type. 
6. Enter a name for your application and enter the location for your container image.  For example, enter `docker.io/ibmcom/kn-helloworld` for container image. Click **Create**. 
  When using this example, your sample application uses the `docker.io/ibmcom/kn-helloworld` image, reads the environment variable `TARGET` and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned.
7. After the application status changes to **Ready**, you can run your application by clicking **Send Request** and viewing the results in the **Requests** window.
8. To create a revision of the application, modify the application.  Using the sample application:
   a. Click **Env. Variables**.
   b. Click **Add Environmental Variables** and enter `TARGET` for name and `Stranger` for value.
   c. Click **Save** to save your change.
   d. Run the application again. `Hello Stranger` is displayed in the **Requests** window.

You have created and deployed an application to Coligo and tested it out using the console. Using the sample application, you created a revision by adding an environmental variable and tested out that revision.

## Deploying an application from CLI
{: #deploy-app-cli}

## Accessing your service
{: #access-service}

## Improving your application performance
{: #app-performance}
