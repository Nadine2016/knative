---

copyright:
  years: 2020
lastupdated: "2020-04-29"

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

# Deploying a job
{: #kn-job-deploy}

Learn how to deploy jobs in Coligo.  Jobs in Coligo are meant to run to completion. They are not intended to provide lasting endpoints to access like a [Coligo application] does.
{: shortdesc}

## Create a job definition
{: #create-job-def}

Job definitions are templates that you can use to define common job types and variables. When you deploy a job, you can override many of the variables you set in the template. You can create job definitions from the console or with the CLI.
{: shortdesc}

### Creating a job definition from the console
{: #create-job-def-ui}

**Before you begin**:

* [Target a project](/docs/knative?topic=knative-manage-project).

1. After targeting your project, select it from the console.
2. Select Job definition. If you already have components in your project, click Create component and then Job definition.
3. Select a project to contain this job definition, a name, container image, and runtime settings. Click **Create**. 

### Creating a job definition with the CLI
{: #create-job-def-cli}

**Before you begin**:

* [Target a project](/docs/knative?topic=knative-manage-project)
* Set up your [Coligo](/docs/knative?topic=knative-kn-install-cli) environment

To create a job definition with the CLI, run the `ibmcloud coligo jobdef create` command. This command requires a name and an image and also allows other optional arguments. The following example creates a job definition named `hello` that uses the container image `ibmcom/helloworld-job` and assigns 128 MB as memory and 1 CPU to the container.

```
ibmcloud coligo jobdef create --image ibmcom/helloworld-job --name hello --memory 128M --cpu 1
```
{: pre}

<table>
   <caption>jobdef create components</caption>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>jobdef create</code></td>
   <td>The command to create your job definition.</td>
   </tr>
   <tr>
   <td><code>--image</code></td>
   <td>The name of the image used for this job. This value overrides any image that is passed in the job definition. This value is optional. The format for the image must be REGISTRY/NAMESPACE/REPOSITORY or REGISTRY/NAMESPACE/REPOSITORY:TAG.
Indicates any environmental variables to pass to the image. Variables use a KEY=VALUE format. This value overrides any environmental variables that are passed in the job definition. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the job definition. This value is required. The name must be unique within the project.</td>
   </tr>
   <tr>
   <td><code>--argument</code></td>
   <td>Set any arguments for the job definition. This value is optional. Specify one argument per `--argument` flag. To specify more than one argument, use more than one `--argument` flag; for example, `-argument argA -argument argB`.</td>
   </tr>
   <tr>
   <td><code>--env</code></td>
   <td>Set any environmental variables to pass to the job definition. Variables use a KEY=VALUE format. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--command</code></td>
   <td>Set any commands for the job definition. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--memory</code></td>
   <td>The amount of memory set for the job definition. The default value is 64 M. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--cpu</code></td>
   <td>Specifies the number of CPUs to be assigned to the job definition. The default value is 1. This value is optional.</td>
   </tr>
   </tbody></table>

## Running a job
{: #run-job}

After you create your job definitions, you can use that definition to describe the parameters for your job. You can override any parameters that are defined by the job definition. You can run your job from the console or with the CLI.
{: shortdesc}

### Running a job from the console
{: #run-job-ui}

Before you begin, [target a project](/docs/knative?topic=knative-manage-project)

1. Select your targeted project from the console.
2. Select a job definition. If you do not have any jobs defined, [create a job definition](#create-job-def).
3. Specify any environmental variables or runtime changes for this specific job. These values override the values defined by the job definition. Then, click **Run job**.
4. Set any additional settings and then click **Run**.

### Running a job with the CLI
{: #run-job-cli}

**Before you begin**

* [Target a project](/docs/knative?topic=knative-manage-project)
* Set up your [Coligo](/docs/knative?topic=knative-kn-install-cli) environment

To run a job with the CLI, use the `ibmcloud coligo job run` command. The following example creates three new pods to run the container image specified in the `hello` job definition. The resource limits and requests are applied per pod, so each of the pods gets 128 MB memory and 1 vCPU. This array job allocates 5 \* 128MiB = 640 MiB memory and 5 \* 1 vCPU = 5 vCPUs.

```
ibmcloud coligo job run --name hello --jobdef hello --arraysize 5 --retryLimit 2 --memory 128M --cpu 1
```
{: pre}

<table>
   <caption>job run components</caption>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>job run</code></td>
   <td>The command to run your job.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the job to be run. This value is required. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique within the project.</td>
   </tr>
   <tr>
   <td><code>--image</code></td>
   <td>The name of the image used for this job. This value overrides any image that is passed in the job definition. This value is optional. The format for the image must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`.
Indicates any environmental variables to pass to the image. Variables use a `KEY=VALUE` format. This value overrides any environmental variables that are passed in the job definition. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--cpu</code></td>
   <td>Specifies the number of CPUs to assign to the container that is running the image. This value overrides any `--cpu` value that is assigned in the job definition. If this value is not set in the job definition or the job run, the default value is 1. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--memory</code></td>
   <td>Specifies the amount of memory to assign to the container that is running the image. This value overrides any `--memory` value that is assigned in the job definition. If this value is not set in the job definition or the job run, the default value is 64 M. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--retrylimit</code></td>
   <td>Specifies the number of times to retry the job. The default value is 3. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--arraysize</code></td>
   <td>Indicates how may pods can be used to run the container specified by the job definition. The default value is 1. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--argument</code></td>
   <td>Sets any arguments for the container. To specify more than one argument, use more than one `--argument` flag; for example, `-a argA -a argB`. This value overrides any arguments passed in the job definition. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--command</code></td>
   <td>Set any commands for the job. This value overrides any commands that are passed in the job definition. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--env</code></td>
   <td>Set any environmental variables to pass to the job definition. Variables use a `KEY=VALUE` format. This value is optional.</td>
   </tr>
   </tbody></table>

## Accessing the job details
{: #access-job-details}

Find details about your job from the console or with the CLI.
{: shortdesc}

View job details in the console by selecting a job. View status of your instances, configuration details, and environmental variables that your job run used.

To view job details with the CLI, use the `ibmcloud coligo job get` command.  For example, `ibmcloud coligo job get --name hello`.

### Job status
{: #job-status}

The following table shows the possible status that your job might have.

| Status | Description |
| ------ | ------------|
| Pending | The Job has been accepted by the system, but one or more of the Container images has not been created. This includes time before being scheduled as well as time spent downloading images over the network, which could take a while. |
| Running | The Job instances have been created. At least one instance is still running, or is in the process of starting or restarting. |
| Succeeded | All Job instances have terminated in success, and will not be restarted. |
| Failed | All Job instances have terminated, and at least one instance has terminated in failure. That is, the instance either exited with non-zero status or was terminated by the system.
| Unknown |	For some reason the state of the Job could not be obtained, typically due to an error in communicating with the host. |

## Accessing the job results
{: #access-job-results}

After your job has completed, find the results.
{: shortdesc}

Job results are available in the console from the Job Run page. The Job Run page launches automatically when you submit a job, but you can also find it from the Job Submitted page.

## Viewing job logs
{: #view-job-logs}

After your job has completed, find the logs.
{: shortdesc}

Logs for jobs that are run in the console are available from the Job Run window by clicking **View logs**.

You can view logs from the CLI by using the 'coligo job logs' command. 

```
ibmcloud coligo job logs --name NAME --pod PODINDEX
```
{: pre}

## Improving the performance of your job
{: #improve-job-performance}

There are several things that you can do to improve the performance of your job. 
{: shortdesc}

1. Assign more memory
2. Allow your job to scale up
3. Increase your array size
