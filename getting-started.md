---

copyright:
  years: 2020
lastupdated: "2020-05-13"

keywords: knative, getting started, coligo

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

# Getting started with Project Coligo (Experimental)
{: #getting-started}

Project Coligo (or "Coligo") provides a platform to unify the deployment of functions, applications, and pre-built containers to a Kubernetes-based infrastructure. It provides a unified experience for developers, enabling higher productivity and faster time to market. Coligo is built on open source projects such as Kubernetes, Istio, Knative, and Tekton.
{: shortdesc}

Project Coligo is experimental. Experimental runtimes and services might be unstable or change frequently. Be aware of [experimental limitations](/docs/knative?topic=knative-kn-limits#kn-limits_experimental).
{: important}

Coligo is available in the console at [Coligo overview](https://cloud.ibm.com/knative/overview){: external}. From this interface, you can [create your project](/docs/knative?topic=knative-manage-project) and then begin [deploying apps](/docs/knative?topic=knative-knative-deploy-app) and [running jobs](/docs/knative?topic=knative-kn-job-deploy).

Coligo also includes an [installable CLI plug-in](/docs/knative?topic=knative-kn-install-cli).



## Creating your first Coligo app
{: #kn-hello}

Create your first Coligo app by using the [`Hello World`](docker.io/ibmcom/helloworld) image in Docker Hub. When you send a request to your sample app, the app reads the environment variable `TARGET` and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned.
{: shortdesc}

1. Access [Project Coligo](https://cloud.ibm.com/knative/overview){: external}.
2. Select a project from the list of available projects. You can also [create a new one](/docs/knative?topic=knative-manage-project#create-a-project). 
3. After your project is created and the project is in `Active` status, you can create a Coligo application. Click the name of your project to open your project component page.
4. From the Components page for your project, click **Application** to open the Create Application page.
5. Enter a name for the application and specify `ibmcom/helloworld` for container image. For this example, you do not need to modify the default values for **Runtime settings** or **Environment variables**.
6. Click **Deploy**. 
7. After the application status changes to **Ready**, you can test the application by clicking **Test application**. To see the running application, click **Application URL**.  
8. Now that our application is running, let's create a revision by adding an environment variable. From the configuration page for your application: 
   1. Click **Env. variables**.
   2. Click **Add environmental variable**.
   3. Enter `TARGET` for name and `Stranger` for value. 
   4. Click **Save and deploy** to run the application revision. 
   5. After the application status changes to **Ready**, you can test the application revision by clicking **Test application**. To see the running application, click **Application URL**. `Hello Stranger` is displayed.
   6. You can see the revisions for the application by clicking **Revisions and Traffic** from the navigation. 

Congratulations, you have deployed your first application to Coligo and tested it out. You then created a revision by adding an environment variable and ran that revision. 

## Running your first Coligo job
{: #kn-first-job}

Create your first Coligo job by using the [Coligo CLI](/docs/knative?topic=knative-kn-install-cli).

To run a job, you must first create a job definition. Then, run the job with the parameters provided by the definition. In this example, the job definition uses the container image `busybox` and runs the command `/bin/sh -c` `echo Hello $JOB_INDEX. ENV1 is $ENV1, ENV2 is $ENV2, ENV3 is $ENV3.` When this job runs, the output prints "Hello" followed by the value of the `$JOB_INDEX` and three environment parameters that are defined in `env`.

**Before you begin**
 - Install the [Coligo CLI](/docs/knative?topic=knative-kn-install-cli)
 - [Create](/docs/knative?topic=knative-manage-project#create-a-project) and [target](/docs/knative?topic=knative-manage-project#target-a-project)  a project.  

1. Create the job definition with the `coligo jobdef create` command.

   ```
   ibmcloud coligo jobdef create --image busybox --name myjobdef \
   --argument /bin/sh --argument "-c" \
   --argument "echo Hello $JOB_INDEX. ENV1 is $ENV1, ENV2 is $ENV2, ENV3 is $ENV3" \
   -e "ENV1=env1 from jobdef" -e "ENV2=env2 from jobdef" -e "ENV3=env3 from jobdef" \
   --memory 128M --cpu 1
   ```
   {: pre}
   
   You can view the job definition by running `ibmcloud coligo jobdef get --name myjobdef`.

2. Run the job with the `coligo job run` command

   ```
   ibmcloud coligo job run --name myjobrun --jobdef myjobdef --image busybox --arraysize 5 --retrylimit 2 \
   --argument /bin/sh --argument "-c" \
   --argument 'echo Hi $JOB_INDEX. ENV1 is $ENV1, ENV2 is $ENV2, ENV3 is $ENV3.' \
   --memory 128M
   ```
   {: pre}
   
You can view details about the job by running `ibmcloud coligo job list` to get the job identifier and then running `ibmcloud coligo job get --name <Job Identifier>`.

## Next steps
{: #kn-next}

Learn more about:

- [Managing projects](/docs/knative?topic=knative-manage-project)
- [Deploying application workloads](/docs/knative?topic=knative-application-workloads)
- [Deploying a job](/docs/knative?topic=knative-kn-job-deploy)
