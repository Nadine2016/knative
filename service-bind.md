---

copyright:
  years: 2020
lastupdated: "2020-05-19"

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

# Binding services to applications
{: #kn-service-binding}

Find out how to automatically bind an {{site.data.keyword.cloud_notm}} service to resources in a Coligo project.
{:shortdesc} 

## Experimental limitations
Project Coligo service bindings are under development. Please be aware of the following limitations:

1. Service bindings are supported for applications only.
2. Only one service can be bound to an application.
3. A service binding cannot be deleted individually, but is removed when the application is deleted.
4. Only pre-exisiting services can be used. (Coligo does not currently create new service instances for you).

<br/>
**What types of services can I bind to my application?**

You can add any {{site.data.keyword.cloud_notm}} service that is enabled for {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) to your application. To find a list of supported {{site.data.keyword.cloud_notm}} services, see the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog).

**What is {{site.data.keyword.cloud_notm}} service binding?**

Service binding is a quick way to create service credentials for an {{site.data.keyword.cloud_notm}} service by using its public service endpoint and storing these credentials in a Kubernetes secret in your application. To bind a service to your application, you must provision an instance of the service first. Then, use the `application bind` command to create the service credentials and the Kubernetes secret. The Kubernetes secret is automatically encrypted in etcd to protect your data.

**I already have an {{site.data.keyword.cloud_notm}} service with service credentials. Can I still use {{site.data.keyword.cloud_notm}} service binding?**

Yes, you can reuse the service credentials. To use your existing service credentials, specify the `--service-credential` flag in the `ibmcloud coligo application bind` command and provide the name of your service credentials. {{site.data.keyword.cloud_notm}} service binding automatically creates a Kubernetes secret with your existing service credentials.

## Binding an exisiting service to a Coligo application
{: #kn-bind-existing}

Before you begin:

* [Create and target a project](/docs/knative?topic=knative-manage-project). 
* Set up your [Coligo](/docs/knative?topic=knative-kn-install-cli) CLI environment.
* Create the service instance that you want to bind to your Coligo app.
  
  For example, to create an {{site.data.keyword.cos_full_notm}} service instance (Lite plan), run the following command:
  
   ```
   ibmcloud resource service-instance-create my-object-storage cloud-object-storage lite global -g Default
   ```
   {: pre}
   
* Create a Coligo application.

   For example, to create an application called `my-application` that uses the `ibmcom/helloworld` image:

   ```
   ibmcloud coligo application create --name my-application --image ibmcom/helloworld
   ```
   {: pre}


### Binding a service with new credentials
{: #kn-bind-credentials}

To bind your new service to your Coligo application and generate new service credentials, use the `application bind` command with the following options. This example binds the `my-object-storage` service instance with the app called `my-application`. New service credentials are generated for this binding action.

```
ibmcloud coligo application bind --name my-application --service-instance my-object-storage
```
{: pre}
   
<table>
<caption>application bind components</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
</thead>
<tbody>
<tr>
<td><code>application bind</code></td>
<td>The command to bind the instance to your application.</td>
</tr>
<tr>
<td><code>--name</code></td>
<td>The name of the application.</td>
</tr>
<tr>
<td><code>--service-instance</code></td>
<td>Specify the name of an existing service instance.</td>
</tr>
</table>
   
### Binding a service instance that has existing credentials
{: #kn-bind-existing-credentials}

If you've already created credentials for your service instance and want to use it for your service binding, add the `--service-credentials` option.

To find the credentials of a service instance, run `ibmcloud resource service-keys --instance-name INSTANCENAME`. To see details of a service credential, run `ibmcloud resource service-key KEYNAME`. You can find all of the service keys in your resource group by running `ibmcloud resource service-keys`
{: tip}

The following example binds the `my-object-storage` service instance with existing service credentials called `coligo-credential` to an existing app called `my-application`.

```
ibmcloud coligo application bind --name my-application --service-instance my-object-storage --service-credential coligo-credential
```
{: pre}
   
<table>
<caption>application bind components</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
</thead>
<tbody>
<tr>
<td><code>application bind</code></td>
<td>The command to bind the instance to your application.</td>
</tr>
<tr>
<td><code>--name</code></td>
<td>The name of the application.</td>
</tr>
<tr>
<td><code>--service-instance</code></td>
<td>Specify the name of an existing service instance.</td>
</tr>
<tr>
<td><code>--service-credential</code></td>
<td>The name of the service KEY credentials to bind.</td>
</tr>
</table>
