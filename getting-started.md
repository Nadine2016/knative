---

copyright:
  years: 2020
lastupdated: "2020-04-24"

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

# Getting started with Coligo 
{: #getting-started}

Coligo provides a platform to unify the deployment of functions, applications, and pre-built containers to Kubernetes-based infrastructure. It provides a “one-stop-shop” experience for developers, enabling higher productivity and faster time to market. Coligo is built on open source projects such as Kubernetes, Istio, Knative, and Tekton.
{: shortdesc}

Coligo is available in the console at [Coligo overview](https://dev.console.test.cloud.ibm.com/knative/overview){: external}. From this interface, you can [create your project](/docs/knative?topic=knative-manage-project) and then begin [deploying apps](/docs/knative?topic=knative-knative-deploy-app) and [running jobs](/docs/knative?topic=knative-kn-job-deploy).

Coligo also includes an [installable CLI plug-in](/docs/knative?topic=knative-kn-install-cli).


## Creating your first Coligo app
{: #kn_hello}

Create your first Coligo app by using the [`Hello World`](docker.io/ibmcom/kn-helloworld) image in Docker Hub. When you send a request to your sample app, the app reads the environment variable `TARGET` and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned.
{: shortdesc}

1. Access the Coligo.
2. Select a project from the list of available projects. You can also [create a new one](/docs/knative?topic=knative-manage-project).
3. From your project component page, select **Create component**.
4. Select **Application** as your component type. 
5. Enter a name and `docker.io/ibmcom/kn-helloworld` for container image. Click **Create**. 
6. After the application status changes to **Ready**, you can try out your application by clicking **Send Request** and viewing the results in the **Requests** window.
7. Click **Env. Variables**.
8. Click **Add Environmental Variables** and enter `TARGET` for name and `Stranger` for value. 
9. Click **Save** and run the application again. `Hello Stranger` is displayed.

Congratulations, you have deployed your first application to Coligo and tested it out. You then created a revision by adding some environmental variables and testing out that revision.

## Next steps
{: #kn_next}

Learn more in [deploying apps](/docs/knative?topic=knative-knative-deploy-app).
