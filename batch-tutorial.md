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

# Deploying jobs
{: #kn-deploy-job-tutorial}

With this tutorial, deploy a batch job using the Coligo CLI or the console. 

The Coligo platform provides support for running batch *jobs*. Batch jobs are standalone executables or run-to-completion workloads. Jobs are not intended to provide lasting endpoints to access like a [Coligo application] does. 

A job runs one or more job containers according to the job definition, which contains the workload configuration. After a job definition is created, you can then run one or more jobs that refer to the job definition, optionally overwriting values of the job definition. A job is complete after all the job containers have completed.

Before you begin:
* Coligo is available in the console at [Coligo overview](https://cloud.ibm.com/knative/overview){: external}. 
* If you use the CLI, [set up your Coligo environment](/docs/knative?topic=knative-kn-install-cli).


## Step 1. Create a job definition
{: #batch-jobdef}

Job definitions are templates that define common job types and variables. When you deploy a job, you can override many of the variables you set in the template. You can create job definitions from the console or with the CLI.
{: shortdesc}

### Creating a job definition from the console
{: #batch-jobdef-ui}

Before you begin: [Create a project](/docs/knative?topic=knative-manage-project).

1. After your project is in **Active** status, click the name of your project on the Projects page. 
2. From the Components page, click **Job definition** to create the job definition. 
3. From the Create job definition page, provide a name for your job definition name and a container image reference. You can also modify default runtime settings. You can specify the sample container image reference `ibmcom/testjob`.
4. Click **Create**. 

### Creating a job definition with the CLI
{: #batch-jobdef-cli}

Before you begin:
* [Create and work with a project](/docs/knative?topic=knative-manage-project)
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

## Step 2. Run a job
{: #batch-runjob}

After you create your job definition, the job definition is used to describe the parameters for your job.  Run your job from the console or with the CLI. When you run your job, you can override some parameters that are defined by the job definition.
{: shortdesc}

### Running a job from the console
{: #batch-runjob-ui}

Before you begin: [create a job definition from the console](#batch-jobdef-ui).


1. Navigate to your job definition page. For example:
   1. From the Projects page, click on your desired project to open the Components page.  
   2. From the Components page, click on the name of the job definition that you want to run your job. If you do not have any job definitions defined, [create a job definition](#batch-jobdef-cli). 
2. From your job definition page, click **Submit Job** to run a job based on the selected job definition configuration. 
3. From the Submit job page, review and optionally change configuration values such as array size, CPU, memory, number of job retries and job timeout. **Array size** specifies the number of instances or containers to run your job. 
5. Click **Submit job** to run your job. The system displays the status of the instances of your job.

### Running a job with the CLI
{: #batch-runjob-cli}

Before you begin: [create a job definition with the CLI](#batch-jobdef-cli).

To run a job with the CLI, use the `ibmcloud coligo job run` command. 

The following example creates three new pods to run the container image specified in the `testjobdef` job definition. The resource limits and requests are applied per pod, so each of the pods gets 128 MB memory and 1 vCPU. This array job allocates 5 \* 128MiB = 640 MiB memory and 5 \* 1 vCPU = 5 vCPUs.

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
   <td>Sets any arguments for the container. To specify more than one argument, use more than one `--argument` flag; for example, `-a argA -a argB`. This value overrides any arguments passed in the job definition. This value is optional.</td>
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

## Step 3. Access job details
{: #batch-accessjobdetails}

Find details about your job from the console or with the CLI.
{: shortdesc}

### Accessing job details from the console
{: #batch-accessjobdetails-ui}

View job details in the console by clicking on the name of your job in the Jobs pane on your job definition page. Job details include status of your instances, configuration details, and environmental variables of your job. 

### Accessing job details with the CLI
{: #batch-accessjobdetails-cli}

To view job details with the CLI, use the `ibmcloud coligo job get` command. 

For example, `ibmcloud coligo job get --name testjobrun`.

**Sample output**

```
Getting Job 'testjobrun'...
Name:         testjobrun-w6rmp
Namespace:    ae2f5ad7-6196
Labels:       coligo.cloud.ibm.com/job-definition=testjobdef
              jobrun=testjobrun
Annotations:  coligo.cloud.ibm.com/pod-expectations: 5
API Version:  coligo.cloud.ibm.com/v1alpha1
Kind:         JobRun
Metadata:
  Creation Timestamp:  2020-05-08T00:13:10Z
  Generate Name:       testjobrun-
  Generation:          1
  Resource Version:    92429386
  Self Link:           /apis/coligo.cloud.ibm.com/v1alpha1/namespaces/ae2f5ad7-6196/jobruns/testjobrun-w6rmp
  UID:                 cce00a2d-8db1-44fd-bf17-fda22e863911
Spec:
  Array Size:          5
  Job Definition Ref:  testjobdef
  Job Definition Spec:
    Containers:
      Image:  ibmcom/testjob
      Name:   testjobdef
      Resources:
        Requests:
          Cpu:         1
          Memory:      128Mi
  Max Execution Time:  7200
  Retry Limit:         2
Status:
  Completion Time:  2020-05-08T00:13:51Z
  Conditions:
    Last Probe Time:       2020-05-08T00:13:46Z
    Last Transition Time:  2020-05-08T00:13:46Z
    Status:                True
    Type:                  Pending
    Last Probe Time:       2020-05-08T00:13:50Z
    Last Transition Time:  2020-05-08T00:13:50Z
    Status:                True
    Type:                  Running
    Last Probe Time:       2020-05-08T00:13:51Z
    Last Transition Time:  2020-05-08T00:13:51Z
    Status:                True
    Type:                  Complete
  Effective Job Definition Spec:
    Containers:
      Image:  ibmcom/testjob
      Name:   testjobdef
      Resources:
        Requests:
          Cpu:     1
          Memory:  128Mi
  Start Time:      2020-05-08T00:13:46Z
  Succeeded:       5
Events:
  Type    Reason     Age                            From                  Message
  ----    ------     ----                           ----                  -------
  Normal  Updated    <invalid> (x5 over <invalid>)  batch-job-controller  Updated JobRun "testjobrun-w6rmp"
  Normal  Completed  <invalid>                      batch-job-controller  JobRun completed successfully


Command 'job get' performed successfully
```
{: screen}

## Step 4.  View job results 
{: #batch-viewjobresult}

After your job has completed, view the logs for information on your completed job.
{: shortdesc}

### Viewing job results from the console
{: #batch-viewjobresult-ui}

Access logs for jobs that are run in the console from your job definition page. Click **View logs**. 

### Viewing job results with the CLI
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


2020-05-08 00:13:49 Envs:
GOLANG_VERSION=1.13.5
GOPATH=/go
HELLOWORLD_QZCST_1_PORT=tcp://172.21.77.219:80
HELLOWORLD_QZCST_1_PORT_80_TCP=tcp://172.21.77.219:80
HELLOWORLD_QZCST_1_PORT_80_TCP_ADDR=172.21.77.219
HELLOWORLD_QZCST_1_PORT_80_TCP_PORT=80
HELLOWORLD_QZCST_1_PORT_80_TCP_PROTO=tcp
HELLOWORLD_QZCST_1_PRIVATE_PORT=tcp://172.21.208.175:80
HELLOWORLD_QZCST_1_PRIVATE_PORT_8022_TCP=tcp://172.21.208.175:8022
HELLOWORLD_QZCST_1_PRIVATE_PORT_8022_TCP_ADDR=172.21.208.175
HELLOWORLD_QZCST_1_PRIVATE_PORT_8022_TCP_PORT=8022
HELLOWORLD_QZCST_1_PRIVATE_PORT_8022_TCP_PROTO=tcp
HELLOWORLD_QZCST_1_PRIVATE_PORT_80_TCP=tcp://172.21.208.175:80
HELLOWORLD_QZCST_1_PRIVATE_PORT_80_TCP_ADDR=172.21.208.175
HELLOWORLD_QZCST_1_PRIVATE_PORT_80_TCP_PORT=80
HELLOWORLD_QZCST_1_PRIVATE_PORT_80_TCP_PROTO=tcp
Hello World!
HELLOWORLD_QZCST_1_PRIVATE_PORT_9090_TCP=tcp://172.21.208.175:9090
HELLOWORLD_QZCST_1_PRIVATE_PORT_9090_TCP_ADDR=172.21.208.175
HELLOWORLD_QZCST_1_PRIVATE_PORT_9090_TCP_PORT=9090
HELLOWORLD_QZCST_1_PRIVATE_PORT_9090_TCP_PROTO=tcp
HELLOWORLD_QZCST_1_PRIVATE_PORT_9091_TCP=tcp://172.21.208.175:9091
HELLOWORLD_QZCST_1_PRIVATE_PORT_9091_TCP_ADDR=172.21.208.175
HELLOWORLD_QZCST_1_PRIVATE_PORT_9091_TCP_PORT=9091
HELLOWORLD_QZCST_1_PRIVATE_PORT_9091_TCP_PROTO=tcp
HELLOWORLD_QZCST_1_PRIVATE_SERVICE_HOST=172.21.208.175
HELLOWORLD_QZCST_1_PRIVATE_SERVICE_PORT=80
HELLOWORLD_QZCST_1_PRIVATE_SERVICE_PORT_HTTP=80
HELLOWORLD_QZCST_1_PRIVATE_SERVICE_PORT_HTTP_AUTOMETRIC=9090
HELLOWORLD_QZCST_1_PRIVATE_SERVICE_PORT_HTTP_QUEUEADM=8022
HELLOWORLD_QZCST_1_PRIVATE_SERVICE_PORT_HTTP_USERMETRIC=9091
HELLOWORLD_QZCST_1_SERVICE_HOST=172.21.77.219
HELLOWORLD_QZCST_1_SERVICE_PORT=80
HELLOWORLD_QZCST_1_SERVICE_PORT_HTTP=80
HOME=/root
HOSTNAME=testjobrun-w6rmp-0-0
JOB_INDEX=0
KUBERNETES_PORT=tcp://172.21.0.1:443
KUBERNETES_PORT_443_TCP=tcp://172.21.0.1:443
KUBERNETES_PORT_443_TCP_ADDR=172.21.0.1
KUBERNETES_PORT_443_TCP_PORT=443
KUBERNETES_PORT_443_TCP_PROTO=tcp
KUBERNETES_SERVICE_HOST=172.21.0.1
KUBERNETES_SERVICE_PORT=443
KUBERNETES_SERVICE_PORT_HTTPS=443
PATH=/go/bin:/usr/local/go/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

Command 'job logs' performed successfully
```
{: screen}

Congratulations! You have created a job definition, run a job, and viewed details and results of the job.

For more information, see [deploying a job](/docs/knative?topic=knative-kn-job-deploy).
