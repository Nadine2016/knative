---

copyright:
  years: 2020
lastupdated: "2020-05-19"

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

Project Coligo (or "Coligo") provides a platform to unify the deployment of all of your container-based applications. Whether those applications are functions, traditional 12-factor apps, batch workloads or any other container-based workloads, if they can be bundled into a container image, then Coligo can host and manage them for you - all on a Kubernetes-based infrastructure. And Coligo does this without the need for you to learn, or even know about, Kubernetes. The Coligo experience is designed so that you can focus on writing code and not on the infrastructure needed to host it.
{: shortdesc}

Project Coligo is experimental. Experimental runtimes and services might be unstable or change frequently. Be aware of [experimental limitations](/docs/knative?topic=knative-kn-limits#kn-limits_experimental).
{: important}

Coligo is available in the console at [Coligo overview](https://cloud.ibm.com/knative/overview){: external}. From this interface, you can [create your project](/docs/knative?topic=knative-manage-project) and then begin [deploying apps](/docs/knative?topic=knative-knative-deploy-app) and [running jobs](/docs/knative?topic=knative-kn-job-deploy).

Coligo also includes an [installable CLI plug-in](/docs/knative?topic=knative-kn-install-cli) where you can also [create your project](/docs/knative?topic=knative-manage-project) and then begin [deploying apps](/docs/knative?topic=knative-knative-deploy-app) and [running jobs](/docs/knative?topic=knative-kn-job-deploy).

In this topic, create your first app and run your first job from the console.



## What are Coligo projects, applications, and jobs?
{: #kn-term-summary}

Before we get started, let's become familiar with some key terms for Coligo. 

A *project* is a grouping of runtime components such as applications and job definitions. The grouping of components is up to you, but typically runtime components that are part of a larger application are grouped together. Projects are used to manage resources and provide access to components in the project. 

An *application*, or app, runs your code to serve HTTP requests. An application has a URL for incoming requests. The number of running instances of an application are automatically scaled up or down (to zero) based on incoming workload. An application contains one or more revisions. A revision represents an immutable version of the configuration properties of the application. Each update of an application configuration property creates a new revision of the application.

A *job* is a standalone executable for batch jobs and runs one or more containers according to a *job definition*.  A job definition is like a template that contains the workload configuration. After a job definition is created, you can then run one or more jobs that refer to the job definition to perform your task. 

## Creating your first Coligo app
{: #kn-hello}

Create your first Coligo app by using the [`Hello World`](https://hub.docker.com/r/ibmcom/helloworld) image in Docker Hub. When you send a request to your sample app, the app reads the environment variable `TARGET` and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned.
{: shortdesc}

1. Access [Project Coligo](https://cloud.ibm.com/knative/overview){: external}.
2. Select a project from the list of available projects. You can also [create a new one](/docs/knative?topic=knative-manage-project#create-a-project). 
3. After your project is created and the project is in `Active` status, you can create a Coligo application. Click the name of your project to open your project component page.
4. From the Components page for your project, click **Application** to open the Create Application page.
5. Enter a name for the application and specify `ibmcom/helloworld` for container image. Use a name for your application that is unique within the project. For this example, you do not need to modify the default values for **Runtime settings** or **Environment variables**.
6. Click **Deploy**. 
7. After the application status changes to **Ready**, you can test the application by clicking **Test application**. To see the running application, click **Application URL**.  

Now that our application is running, let's create a revision by adding an environment variable. From the configuration page for your application: 
1. Click **Env. variables**.
2. Click **Add environmental variable**.
3. Enter `TARGET` for name and `Stranger` for value. 
4. Click **Save and deploy** to deploy the application revision. 
5. After the application status changes to **Ready**, you can test the application revision by clicking **Test application**. To see the running application, click **Application URL**. `Hello Stranger` is displayed.
6. You can see the revisions for the application by clicking **Revisions and Traffic** from the navigation. 

Congratulations, you have deployed your first application to Coligo and tested it out. You then created a revision by adding an environment variable and ran that revision. 

## Running your first Coligo job
{: #kn-first-job}

Create your first Coligo job by using the [`ibmcom/testjob`](https://hub.docker.com/r/ibmcom/testjob) image in Docker Hub. This job prints `"Hello World"`. 
{: shortdesc}

### Creating the job definition
{: #kn-first-jobdef}

Before you run a job, you must first create a job definition. A job definition is a template for how to run your container, enabling you to specify most runtime configuration settings before you run your job. After creating the job definition, you then create a job to actually perform your task.  When you run your job, you can specify the number of instances of that specific job that you want to run as part of your job run.
{: important}

1. Access your project from the [Coligo Projects page](https://cloud.ibm.com/knative/projects){: external}. Click the name of your project on the Projects page. 
2. From the Components page, click **Job definition** to create the job definition. 
3. From the Create job definition page, provide a name for your job definition name and a container image reference. For our example, let's use the `ibmcom/testjob` container image. 
4. Click **Create**. 

### Running the job 
{: #kn-first-jobrun}

You are now ready to run your job that is based on your job definition.

1. From the job definition page, in the Jobs pane, click **Submit job**. 
2. From the Submit job pane, review and optionally change configuration values such as array size, CPU, memory, number of job retries, and job timeout. **Array size** specifies the number of instances or containers to run your job. For this example, let's specify an array size of 5 and use the other values set in the job description.
3. Click **Submit job** to run your job. The system displays the status of the instances of your job on the job details page. The job run details page displays that all 5 of the instances of my job were completed. 

When logging is enabled, the expected output of `Hello World` is displayed in the logs. To learn about running jobs with logging enabled, see [Running a job](/docs/knative?topic=knative-kn-job-deploy). 
{: tip}

Congratulations, you have created a job definition and run your job from the console. 

## Next steps
{: #kn-next}

Learn more about performing these Coligo tasks from the console or with the [Coligo CLI](/docs/knative?topic=knative-kn-install-cli):
- [Managing projects](/docs/knative?topic=knative-manage-project)
- [Deploying applications](/docs/knative?topic=knative-application-workloads)
- [Running jobs](/docs/knative?topic=knative-kn-job-deploy)
