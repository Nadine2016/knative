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

# Deploying the job
{: #kn-job-deploy}

Learn how to deploy your batch job. 
{: shortdesc}

## What kind of jobs can I run?

## What type of job do I want to create?

## Create a job definition
{: #create-job-def}

Job definitions are templates that you can use to define common job types. You can create job definitions from the console or with the CLI.
{: shortdesc}

### Creating a job definition from the console
{: #create-job-def-ui}

**Before you begin**:
* [Target a project](/docs/knative?topic=knative-manage-project)

1. After targeting your project, select it from the console.
2. Select Job definition. If you already have components in your project, click Create component and then Job definition.
3. Select a project to contain this job definition, a name, container image, and runtime settings. Click Create. 

### Creating a job definition with the CLI
{: #create-job-def-cli}

**Before you begin**:
* [Target a project](/docs/knative?topic=knative-manage-project)
* Set up your [Coligo](/docs/knative?topic=knative-kn-install-cli) environment

To create a job definition with the CLI, run the `ibmcloud coligo jobdef create` command. This command requires a name and an image and also allows other optional arguments. The followig example create a job definition named `hello` that uses the container image `busybox` and uses the arguments `/bin/sh -c echo Hello $JOB_INDEX ENV1 is $ENV1, ENV2 is $ENV2, ENV3 is $ENV3`, assigning 128 MB as memory and 1 CPU to the container.

```
ibmcloud coligo jobdef create --image busybox --name hello --argument /bin/sh --argument "-c" --argument "echo Hello $JOB_INDEX. ENV1 is $ENV1, ENV2 is $ENV2, ENV3 is $ENV3" -e "ENV1=env1 from jobdef" -e "ENV2=env2 from jobdef" -e "ENV2=env2 from jobdef" --memory 128M --cpu 1
```
{: pre}

## Running a job
{: #run-job}

After you create your job definitions, you can use that definition to describe the parameters for your job. You can override any parameters that are defined by the job definition. You can run your job from the console or with the CLI.
{: shortdesc}

### Running a job from the console
{: #run-job-ui}

**Before you begin**:
* [Target a project](/docs/knative?topic=knative-manage-project)

1. After targeting your project, select it from the console.
2. Select a job definition. If you do not have any jobs defined, [create a job definition](#create-job-def).
3. Specify any environmental variables or runtime changes for this specic job. These values override the values defined by the job definition. Then, click **Run job**.
4. Set any additional settings and then click **Run**.

### Running a job with the CLI
{: #run-job-cli}

**Before you begin**:
* [Target a project](/docs/knative?topic=knative-manage-project)
* Set up your [Coligo](/docs/knative?topic=knative-kn-install-cli) environment

To run a job with the CLI, use the `ibmcloud coligo job run` command. The following example creates three new pods to run the container image specified in the `hello` job definition. The resource limits and requests are applied per pod, so each of the pods gets 128 MB memory and 1 vCPU. This array job allocates 5 \* 128MiB = 640 MiB memory and 5 \* 1 vCPU = 5 vCPUs.

```
ibmcloud coligo job run --name hello --jobdef hello --arraysize 5 --retryLimit 2 --memory 128M --cpu 1
```
{: pre}

## Accessing the job details
{: #access-job-details}

Find details about you job, including  You can find details about your job from the console or with the CLI.
{: shortdesc}

View job details in the console by selecting a job. View status of your instances, configuration details, and environmental variables that your job run used.

To view job details with the CLI, use the `ibmcloud coligo job get` command.  For example, `ibmcloud coligo job get --name hello`.

## Accessing the job results
{: #access-job-results}

After your job has completed, find the results.
{: shortdesc}

## Testing your job
{: #test-job}

Before running your job, test it. 
{: shortdesc}

## Improving the performance of your job
{: #improve-job-performance}

There are several things that you can do to improve the performance of your job. 
{: shortdesc}
