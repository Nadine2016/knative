---

copyright:
  years: 2020
lastupdated: "2020-04-27"

keywords: knative, data encryption in knative, data storage for knative, bring your own keys for knative, BYOK for knative, key management for knative, key encryption for knative, personal data in knative, data deletion for knative, data in knative, data security in knative

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

# Securing your data in Coligo
{: #mng-data}

Coligo provides a platform to unify the deployment of functions, applications and pre-built containers to Kubernetes-based infrastructure. As Coligo is not a data service, it does not store personal or sensitive data.
{: shortdesc}

## How your data is stored and encrypted in Coligo
{: #data-storage}

While Coligo does not store personal or sensitive data, when running Coligo, the data that is stored by Coligo includes *pointers* to container images where you will run the images as Coligo applications or batch jobs.  Coligo does not store the container image data. Instead, it uses the pointer that you provide to where your container image repository resides, which might be a public repository like DockerHub or a private IBM Container Registry. Therefore, encryption of your data in your container images is implemented and managed as part of your container image repository. 

Some data, like DockerHub credentials, batch job templates and IBM container registry APIKey are stored as part of your namespace in Coligo, within an underlying Kubernetes secret map (within your Kubernetes etcd data). For more information, see [Securing information in Kubernetes](/docs/containers?topic=containers-encryption). 
 

## Deleting your data in Coligo
{: #data-delete}

Data in images are deleted within your respective container image repository. 

To delete data that is stored within Coligo, such as DockerHub credentials, batch job templates or an IBM container registry APIKey, [delete your Coligo project](/docs/knative?topic=knative-kn-cli#cli-project-delete).   
**Example**

```
ibmcloud coligo project delete --name myproject
```
{: pre}

**Output**

```
Deleted project myproject
```
{: screen} 





