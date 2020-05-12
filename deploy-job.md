---

copyright:
  years: 2020
lastupdated: "2020-05-12"

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

Learn how to deploy jobs in Coligo. Jobs in Coligo are meant to run to completion as batch or standalone executables. They are not intended to provide lasting endpoints to access like a [Coligo application] does.
{: shortdesc}

## Create a job definition
{: #create-job-def}

Job definitions are templates that are used to define common job types and variables. When you deploy a job, you can override many of the variables you set in the template. You can create job definitions from the console or with the CLI.
{: shortdesc}

### Creating a job definition from the console
{: #create-job-def-ui}

Before you begin, [create a project](/docs/knative?topic=knative-manage-project).  

1. After your project is in **Active** status, click the name of your project on the Projects page.
2. From the Components page, click **Job definition** to create the job definition.
3. From the Create job definition page, provide a name for your job definition name and a container image.  You can also modify default runtime settings. 
4. Click **Create**. 

### Creating a job definition with the CLI
{: #create-job-def-cli}

Before you begin:

* [Create and target a project](/docs/knative?topic=knative-manage-project)
* Set up your [Coligo](/docs/knative?topic=knative-kn-install-cli) environment

To create a job definition with the CLI, run the `ibmcloud coligo jobdef create` command. This command requires a name and an image and also allows other optional arguments. 

The following example creates a job definition named `testjobdef` that uses the container image `ibmcom/testjob` and assigns 128 MB as memory and 1 CPU to the container.

```
ibmcloud coligo jobdef create --image ibmcom/testjob --name testjobdef --memory 128M --cpu 1
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
   <td>The name of the image used for this job definition. This value is required. For images in [Docker Hub](https://hub.docker.com/){: external}, you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the job definition. This value is required. The name must begin with a lowercase letter, can contain letters, numbers, periods (.), and hyphens (-), and must be 35 characters or fewer. The name must start and end with a lowercase alphanumeric character. Use a name that is unique within the project.</td>
   </tr>
   <tr>
   <td><code>--argument</code></td>
   <td>Set any arguments for the job definition. This value is required. Specify one argument per `--argument` flag.  To specify more than one argument, use more than one `--argument` flag; for example, `-a argA -a argB`.</td>
   </tr>
   <tr>
   <td><code>--env</code></td>
   <td>Set any environmental variables to pass to the job definition. Variables use a `KEY=VALUE` format. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--command</code></td>
   <td>Set a command for the job definition. This value is optional.</td>
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

After you create your job definitions, you can use that definition to describe the parameters for your job. You can override some parameters that are defined by the job definition. You can run your job from the console or with the CLI.
{: shortdesc}

### Running a job from the console
{: #run-job-ui}

Before you begin: 
* [Create a job definition from the console](#create-job-def-ui).
* If you want to obtain logs for your job, before you run your job, you must [configure platform logs 
  through the Observability dashboard](/docs/Log-Analysis-with-LogDNA?topic=LogDNA-config_svc_logs#config_svc_logs_ui). Be sure to review [service plan](/docs/Log-Analysis-with-LogDNA?topic=LogDNA-service_plans) information as you consider retention, search, and log usage needs.

1. From the Projects page, click on your desired project to open the Components page.  
2. From the Components page, click on the name of the job definition that you want to run your job. If you do not have any job definitions that are defined, [create a job definition](#create-job-def).
3. From your job definition page, click **Submit Job** to run a job based on the selected job definition configuration. 
4. From the Submit job page, review and optionally change configuration values such as array size, CPU, memory, number of job retries and job timeout. **Array size** specifies the number of instances or containers to run your job. 
5. Click **Submit job** to run your job. The system displays the status of the instances of your job.

### Running a job with the CLI
{: #run-job-cli}

Before you begin:

* Set up your [Coligo](/docs/knative?topic=knative-kn-install-cli) environment
* [Create a job definition](#create-job-def-cli).

To run a job with the CLI, use the `ibmcloud coligo job run` command. The following example creates three new pods to run the container image specified in the `testjobdef` job definition. The resource limits and requests are applied per pod, so each of the pods gets 128 MB memory and 1 vCPU. This array job allocates 5 \* 128 MiB = 640 MiB memory and 5 \* 1 vCPU = 5 vCPUs.

```
ibmcloud coligo job run --name testjobrun --jobdef testjobdef --arraysize 5 --retrylimit 2 --memory 128M --cpu 1
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
   <td>The name of the job to be run. This value is required. The name must begin with a lowercase letter, can contain letters, numbers, periods (.), and hyphens (-), and must be 35 characters or fewer. The name must start and end with a lowercase alphanumeric character. Use a name that is unique within the project.</td>
   </tr>
   <tr>
   <td><code>--jobdef</code></td>
   <td>Identifies the job definition that contains the description of the job to be run. This value is required.</td>
   </tr>
   <tr>
   <td><code>--image</code></td>
   <td>The name of the image used for this job. This value is required. [Docker Hub](https://hub.docker.com/){: external}, you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value overrides any `--image` value that is assigned in the job definition.</td>
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
   <td>Sets any arguments for the container. To specify more than one argument, use more than one `--argument` flag; for example, `-a argA -a argB`. This value overrides any arguments that are passed in the job definition. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--command</code></td>
   <td>Set any commands for the job. This value overrides any commands that are passed in the job definition. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--env</code></td>
   <td>Specifies any environmental variables to pass to the image. Variables use a `KEY=VALUE` format. This value overrides any environmental variables that are passed in the job definition. This value is optional.</td>
   </tr>
   </tbody></table>

## Accessing the job details
{: #access-job-details}

Find details about your job from the console or with the CLI.
{: shortdesc}

View job details in the console by clicking on the name of your job in the Jobs pane on your job definition page. Job details include status of your instances, configuration details, and environmental variables of your job. 

To view job details with the CLI, use the `ibmcloud coligo job get` command.  For example, `ibmcloud coligo job get --name hello`.

### Job status
{: #job-status}

The following table shows the possible status that your job might have.

| Status | Description |
| ------ | ------------|
| Pending | The Job has been accepted by the system, but one or more of the Container images has not been created. This status includes time before being scheduled as well as time spent downloading images over the network, which might take a while. |
| Running | The Job instances have been created. At least one instance is still running, or is in the process of starting or restarting. |
| Succeeded | All Job instances have terminated in success, and will not be restarted. |
| Failed | All Job instances have terminated, and at least one instance has terminated in failure. That is, the instance either exited with non-zero status or was terminated by the system.
| Unknown |	For some reason the state of the Job could not be obtained, typically due to an error in communicating with the host. |

## Accessing the job results
{: #access-job-results}

After your job has completed, find the results.
{: shortdesc}

Job results are available in the console from the Job Run page. The Job Run page launches automatically when you submit a job. You can also click the name of your job from the Jobs pane on the Job definition page to get the results of your job. 

## Viewing job logs
{: #view-job-logs}

After your job has completed, find the logs.
{: shortdesc}

After your job has completed, view the logs for information on your completed job.
{: shortdesc}

### Viewing job logs from the console
{: #batch-viewjobresult-ui}

Access logs for jobs that are run in the console from your job definition page. Coligo uses {{site.data.keyword.la_full}} for log management capabilities. 

If you want to obtain logs for your job, before you run your job, you must [configure platform logs through the Observability dashboard](/docs/Log-Analysis-with-LogDNA?topic=LogDNA-config_svc_logs#config_svc_logs_ui) Review [service plan](/docs/Log-Analysis-with-LogDNA?topic=LogDNA-service_plans) information as you consider retention, search, and log usage needs. 
{: important}

1. After clicking **Submit Job** to run your job, from the job run details page, click **Launch logging**.  This action launches your log for your specific job in the Observability dashboard where you can view your job log. 
2. You can also view job logs from the Job definition page. Select the job that you want from the Jobs pane, and click **Logs**. This action launches your log for the specific job your selected on the observability dashboard where you can view your job log. 

### Viewing job logs with the CLI
{: #batch-viewjobresult-cli}

To view job logs with the CLI, use the `ibmcloud coligo job logs` command. 

For example, to view the logs for our `testjobrun` job, use the command: 

```
ibmcloud coligo job logs --name testjobrun 
```
{: pre}

**Sample output**

```
Logging Job 'testjobrun' on Pod 0...

Hello World!

Command 'job logs' performed successfully
```
{: screen}


