---

copyright:
  years: 2020
lastupdated: "2020-05-15"

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

# Managing application workloads
{: #application-workloads}

An *Application* runs your code to serve HTTP requests. An Application has a URL for incoming requests. The number of running instances of an Application are automatically scaled up or down (to zero) based on incoming workload. An Application contains one or more *revisions* (revision entities). A revision represents an immutable version of the configuration properties of the Application. Each update of an application configuration property creates a new revision of the Application.
{: #shortdesc} 

## Deploying application workloads
{: #knative-deploy-app}

Deploy your app with Coligo.
{: shortdesc}

**Before you begin**

* Set up your [Coligo](/docs/knative?topic=knative-kn-install-cli) environment
* [Target a project](/docs/knative?topic=knative-manage-project)
* Create your application as an image file

### Deploying an application from console
{: #deploy-app-console}

The following steps describe how to deploy an application by using the Coligo console.
{: shortdesc}

1. Open the [Coligo dashboard](https://cloud.ibm.com/knative/overview).
2. Select a project from the list of available projects. You can also [create a new one](/docs/knative?topic=knative-manage-project).
3. From the Projects page, click the name of your project to open the project component page. 
4. From your project component page, select **Create component**.
5. Select **Application** as your component type. 
6. Enter a name for your application and enter the location for your container image.  For example, enter `ibmcom/helloworld` for container image. Click **Deploy**. 
  When you use this example, your sample application uses the `ibmcom/helloworld` image, reads the environment variable `TARGET`, and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned.
7. After the application status changes to **Ready**, you can run your application by clicking **Test application**. To see the running application, click **Application URL**.  

You have created and deployed an application to Coligo and tested it out using the console.

### Deploying an application from CLI
{: #deploy-app-cli}

Deploy your application from the CLI with the `coligo application create` command. 
{: shortdesc}

```
ibmcloud coligo application create --name NAME --image IMAGE
```
{: pre}

<table>
   <caption>application create components</caption>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>application create</code></td>
   <td>The command to create your application.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the job to be run. This value is required. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique within the project.</td>
   </tr>
   <tr>
   <td><code>--image</code></td>
   <td>The name of the image used for this application. This value is required. The format for the image must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`.</td>
   </tr>
   <tr>
   <td><code>--concurrency</code></td>
   <td>If your code is written in a way that it can handle multiple concurrent
requests, set concurrency to the maximum number of requests that
a single instance should handle concurrently. The number of
instances will be increased when existing instances are reaching
this limit.
<p>If your code should work on a single request at a time,
  set concurrency to 1 and each request will get its own instance.</p>
<p>The maximum number of overall concurrent requests that the app component
can work on concurrently is determined by "the maximum number of concurrent
requests per instance" times "the maximum number of instances":
  max_instances x max_concurrency.</p></td>
   </tr>
   <tr>
   <td><code>--cpu</code></td>
   <td>The amount of CPU set for the application. The default value is 1. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--memory</code></td>
   <td>The amount of memory set for the application. The default value is 64 M. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--minscale</code></td>
   <td>The minimum number of instances that can be used for this application. The default value is 1. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--maxscale</code></td>
   <td>The maximum number of instances that can be used for this application. The default value is 1. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--timeout</code></td>
   <td>The amount of time that can pass before the application must succeed or fail. The default value is 360 seconds. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--concurrency</code></td>
   <td></td>
   </tr>
   <tr>
   <td><code>--registry-secret</code></td>
   <td>The name of the secret for the image. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--project</code></td>
   <td>The name of the project to contain this application. If this value is not set, then the current project is used. This value is optional.</td>
   </tr>
   </table>

## Accessing your service
{: #access-service}

After your service deploys, you can access it through a URL.
{: shortdesc}

From the console, your application URL is available from the components page and on the application details page.

From the CLI, run `coligo application get` to find the URL. 

```
ibmcloud coligo application get --name NAME
```
{: pre}

## Updating your app
{: #update-app}

An Application contains one or more *revisions*. A revision represents an immutable version of the configuration properties of the Application. Each update of an application configuration property creates a new revision of the Application.
{: shortdesc} 

To create a revision of the application, modify the application. 

For example, update the application that you created in [Deploying an application from console](#deploy-app-console) to add an environmental variable.

1. Navigate to your application page. One way to navigate to your application page is to: 
   * Locate the Projects page. 
   * Click the name of your project to open the project component page.
   * Click the name of your application to open the application page.
2. Click **Env. Variables**.
3. Click **Add Environmental Variables** and enter `TARGET` for name and `Stranger` for value.
4. Click **Save and deploy** to save your change and run the application revision.
5. After the application status changes to **Ready**, you can test the application revision by clicking **Test application**. To see the running application, click **Application URL**. `Hello Stranger` is displayed.

## Application status
{: #app-status}

The following table shows the possible status that your application might have.

| Status | Description |
| ------ | ------------|
| Deploying | The application is deploying, but one or more of the images has not been created. This includes time before being scheduled as well as time spent downloading images over the network, which could take a while. |
| Ready | The application is deployed and ready to use. |
| Ready (with warnings) | The application revision failed but the original deployment is available. |
| Failed | The application deployment has terminated, and at least one instance has terminated in failure. That is, the instance either exited with non-zero status or was terminated by the system.
| Unknown |	For some reason the state of the application could not be obtained, typically due to an error in communicating with the host. |

## Viewing job logs
{: #view-app-logs}

After your application has deployed, find the logs.
{: shortdesc}

Logs for application from the console are available from the application window by clicking **View logs**.

You can view logs from the CLI by using the `coligo application logs` command. 

```
ibmcloud coligo application logs --name NAME --pod PODINDEX
```
{: pre}

