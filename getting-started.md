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

# Getting started with Project Coligo 
{: #getting-started}

Project Coligo (or "Coligo") provides a platform to unify the deployment of functions, applications, and pre-built containers to a Kubernetes-based infrastructure. It provides a unified experience for developers, enabling higher productivity and faster time to market. Coligo is built on open source projects such as Kubernetes, Istio, Knative, and Tekton.
{: shortdesc}

Coligo is available in the console at [Coligo overview](https://dev.console.test.cloud.ibm.com/knative/overview){: external}. From this interface, you can [create your project](/docs/knative?topic=knative-manage-project) and then begin [deploying apps](/docs/knative?topic=knative-knative-deploy-app) and [running jobs](/docs/knative?topic=knative-kn-job-deploy).

Coligo also includes an [installable CLI plug-in](/docs/knative?topic=knative-kn-install-cli).


## Creating your first Coligo app
{: #kn-hello}

Create your first Coligo app by using the [`Hello World`](docker.io/ibmcom/kn-helloworld) image in Docker Hub. When you send a request to your sample app, the app reads the environment variable `TARGET` and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned.
{: shortdesc}

1. Access the Coligo.
2. Select a project from the list of available projects. You can also [create a new one](/docs/knative?topic=knative-manage-project).
3. From your project component page, select **Create component**.
4. Select **Application** as your component type. 
5. Enter a name and `docker.io/ibmcom/kn-helloworld` for container image. Click **Create**. 
6. After the application status changes to **Ready**, you can try out your application by clicking **Send Request** and viewing the results in the **Requests** window.  
7. Now that our application is running, let's create a revision by adding an environmental variable.
   1. Click **Env. Variables**.
   2. Click **Add Environmental Variables**.
   3. Enter `TARGET` for name and `Stranger` for value. 
   4. Click **Save** and run the application again. `Hello Stranger` is displayed.
   5. You can see the revisions for the application by clicking **Revisions and Traffic** from navigation. 

Congratulations, you have deployed your first application to Coligo and tested it out. You then created a revision by adding some environmental variables and testing out that revision.

## Running your first Coligo job
{: #kn-first-job}

Create your first Coligo job by using the [Coligo CLI](/docs/knative?topic=knative-kn-install-cli). To run a job, you must first create a job definition. Then, run the job with the parameters provided by the definition. In this example, the job definition uses the container image `busybox` and runs the command `/bin/sh -c` `echo Hello $JOB_INDEX. ENV1 is $ENV1, ENV2 is $ENV2, ENV3 is $ENV3.` When this job runs, the output prints "Hello" followed by the value of the `$JOB_INDEX` and three environment parameters that are defined in `env`.

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

- [Managing projects](/docs/knative?topic=knative-knative-manage-project)
- [Deploying application workloads](/docs/knative?topic=knative-knative-deploy-app)
- [Running a job](/docs/knative?topic=knative-knative-deploy-app)
