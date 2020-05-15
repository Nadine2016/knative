---

copyright:
  years: 2020
lastupdated: "2020-05-15"

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


# Project Coligo CLI
{: #kn-cli}

Run these commands to manage the entities that make up Project Coligo (or "Coligo").
{: shortdec}

## Project commands
{: #cli-project}

A project is a container for components, such as applications and job definitions. Projects enable you to manage resources and provide access to components in the project. Use project commands to create, display details, and delete projects.
{: shortdec}

You can use either `project` or `proj` in your project commands. 
To see CLI help for the project command, run `ibmcloud coligo `proj`. 
{: tip}

### `ibmcloud coligo project create`
{: #cli-project-create}

Create a project.
{: shortdec}

```
ibmcloud coligo project create --name PROJECT_NAME  [--tag TAG]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required. The name must begin with a lowercase letter, can contain letters, numbers, periods (.), and hyphens (-), and must be 35 characters or fewer. The name must start and end with a lowercase alphanumeric character. Use a name that is unique within the project.
<dt>`-t`, `--tag`</dt>
<dd>A label to assign to your resource.  This value is optional. The label must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. Specify one label per `--tag` flag.  To specify more than one label, use more than one `--tag` flag; for example, `--tag tagA --tag tagB`.</dd>
</dl>

**Example**

```
ibmcloud coligo project create --name myproject  
```
{: pre}

**Output**

```
Successfully created project myproject
```
{: screen}

### `ibmcloud coligo project current`
{: #cli-project-current}

Display the details of the project that is currently targeted. 
{: shortdec}

```
ibmcloud coligo project current
```
{: pre}

**Example**

```
ibmcloud coligo project current  
```
{: pre}

**Output**

```
Getting current project...
Region:         myproject
Region:         us-south
export KUBECONFIG=/user/myusername/.bluemix/plugins/coligo/myproject-42642513-8805-4da8-8dbf-ae4f409f8054.yaml
```
{: screen}

### `ibmcloud coligo project delete`
{: #cli-project-delete}

Delete a project.
{: shortdec}

```
ibmcloud coligo project delete --name PROJECT_NAME
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required.</dd>
</dl>

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

### `ibmcloud coligo project get`
{: #cli-project-get}

Display the details of a single project.
{: shortdec}

```
ibmcloud coligo project get --name PROJECT_NAME
```
{: pre}

**Command options**
<dl>
<dt>`PROJECT_NAME`</dt>
<dd>The name of the project. This value is required.</dd>
</dl>

**Example**

```
ibmcloud coligo project get --name myproject
```
{: pre}

**Output**

```
Getting project 'myproject'...

Name: myproject
ID: 42642513-8805-4da8-8dbf-bc4f409g9089
Status: active
Tags: []
Location: us-south
Resource Group: Default
Created: Tue, 28 Apr 2020 09:27:22 -0400
Updated: Tue, 28 Apr 2020 09:27:57 -0400

Command 'project get' performed successfully
```
{: screen}

### `ibmcloud coligo project list`
{: #cli-project-list}

List available projects.
{: shortdec}

```
ibmcloud coligo project list
```
{: pre}

**Example**

```
ibmcloud coligo project list
```
{: pre}

**Output**

```
Name            ID                                    Status         Tags   Location   Resource Group
myproject       42642513-8805-4da8-8dbf-bc4f409g9089   active               us-south   Default
new_proj        d294c0a3-30d8-49bc-b070-1921692f41d4   active               us-south   Default

Command 'project list' performed successfully
```
{: screen}

## Target command
{: #cli-target}

To work with a Coligo project, target the project. Before using the target command, you must have a project created. By targeting a project, the commands that you run are run within the specified project.  

{: shortdec}

To see CLI help for the target command, run `ibmcloud coligo target`. 
{: tip}

### `ibmcloud coligo target`
{: #cli-targetcmd}

Target a project for context.
{: shortdec}

```
ibmcloud coligo target --name PROJECT_NAME [--export KUBECONFIG] [--project-api PROJECTAPI]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required.</dd>
<dt>`-e`, `--export`</dt>
<dd>Exports and automatically appends the project configuration to the Kubernetes configuration file (`$HOME/.kube/config`).  The default value is `false`. This value is optional.</dd>
<dt>`-p`, `--project-api`</dt>
<dd>Specifies an alternate URL to use for project queries. This value is optional.</dd>
</dl>

**Example**

```
ibmcloud coligo target --name myproject
```
{: pre}

**Output**

```
Now targeting environment 'myproject' (42642513-8805-4da8-8dbf-bc4f409g9089). Set the KUBECONFIG environment variable to use kubectl with your project:
export KUBECONFIG=/user/myusername/.bluemix/plugins/coligo/myproject-42642513-8805-4da8-8dbf-bc4f409g9089.yaml
```
{: screen}

## Application commands
{: #cli-application}

Before using application commands, you must be targeting a [project](#cli-project).  An application runs your code to serve HTTP requests. The application has a URL for incoming requests. Use application commands to create, display details, and update, and delete applications. 
{: shortdec}

You can use either `application` or `app` in your application commands. 
To see CLI help for the application command, run `ibmcloud coligo app`. 
{: tip}

### `ibmcloud coligo application create`
{: #cli-application-create}

Create an application.
{: shortdec}

```
ibmcloud coligo application create --image IMAGE_REF --name APP_NAME  [--registry-secret SECRET] [--cpu CPU] [--memory MEMORY] [--timeout TIMEOUT] [--concurrency REQUESTS] [--minscale MIN_NUM] [--maxscale MAX_NUM] [--env ENV][--quiet]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required. The name must begin with a lowercase letter, can contain letters, numbers, periods (.), and hyphens (-), and must be 35 characters or fewer. The name must start and end with a lowercase alphanumeric character. Use a name that is unique within the project.
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this application. This value is required. For images in [Docker Hub](https://hub.docker.com){: external}, you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. </dd>
<dt>`--rs`, `--registry-secret`</dt>
<dd>The name of the secret for the image. This value is optional.</dd>
<dt>`-c`, `--cpu`</dt>
<dd>The amount of CPU set for the instance of the application. The default value is 1. This value is optional.</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory set for the instance of the application. The default value is 1024 M. This value is optional.</dd>
<dt>`-t`, `--timeout`</dt>
<dd>The amount of time that can pass before the application must succeed or fail. The default value is 360 seconds. This value is optional.</dd>
<dt>`--cn`, `--concurrency`</dt>
<dd>The number of requests that can be processed concurrently per instance. The default value is 1. This value is optional.</dd>
<dt>`--min`, `--minscale`</dt>
<dd>The minimum number of instances that can be used for this application. The default value is 1. This value is optional.</dd>
<dt>`--max`, `--maxscale`</dt>
<dd>The maximum number of instances that can be used for this application. The default value is 1. This value is optional.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set any environmental variables to pass to the application. Variables use a `KEY=VALUE` format. This value is optional.</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. The default value is `false`. This value is optional.</dd>
</dl>

**Example**

```
ibmcloud coligo application create --name myapp --image ibmcom/helloworld 
```
{: pre}

**Output**

```
Creating Application 'myapp'...
Successfully created application 'myapp' created. 
Run `ibmcloud coligo application get -n 'myapp'` to check the application status.
```
{: screen}

When you run `ibmcloud coligo application get -n 'myapp'` to check the application status, the URL for your application is displayed.  
{: tip}

### `ibmcloud coligo application delete`
{: #cli-application-delete}

Delete an application.
{: shortdec}

```
ibmcloud coligo application delete --name APP_NAME
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required.</dd>
</dl>

**Example**

```
ibmcloud coligo application delete --name myapp
```
{: pre}

**Output**

```
Deleted application 'myapp'
```
{: screen}

### `ibmcloud coligo application get`
{: #cli-application-get}

Display the details of an application.
{: shortdec}

```
ibmcloud coligo application get --name APP_NAME [--more-details]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required.</dd>
<dt>`--md`, `--more-details`</dt>
<dd>Specify this option to print more details about the application. The default value is `false`. This value is optional.</dd>
</dl>

**Example**

```
ibmcloud coligo application get --name myapp
```
{: pre}

**Output**

```
Name:       myapp
Namespace:  b49ca89f-g99q
Age:        19h
URL:        http://myapp.b49ca89f-g99q.us-south.knative.test.appdomain.cloud

Revisions:
  100%  @latest (myapp-zxxlr-1) [1] (19h)
        Image:  ibmcom/helloworld (pinned to be18cb)

Conditions:
  OK TYPE                   AGE REASON
  ++ Ready                  19h
  ++ ConfigurationsReady    19h
  ++ RoutesReady            19h

Command 'application get' performed successfully
```
{: screen}

### `ibmcloud coligo application update`
{: #cli-app-update}

Update an application. Updating your application creates a revision. By default, when calls are made to the application, traffic is routed to the revision.
{: shortdec}

```
ibmcloud coligo application update --name APP_NAME --image IMAGE_REF [--registry-secret SECRET] [--cpu CPU] [--memory MEMORY] [--timeout TIMEOUT] [--concurrency REQUESTS] [--minscale MIN_NUM] [--maxscale MAX_NUM] [--env ENV][--quiet]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required.</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this application. This value is required. The format for the image must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`.</dd>
<dt>`--rs`, `--registry-secret`</dt>
<dd>The name of the secret for the image. This value is optional.</dd>
<dt>`-c`, `--cpu`</dt>
<dd>The amount of CPU set for the application. The default value is 1. This value is optional.</dd>
<dt>`-m`, `--memory`</dt>
<dd>Specify to change the amount of memory set for the application. This value is optional.</dd>
<dt>`-t`, `--timeout`</dt>
<dd>The amount of time that can pass before the application must succeed or fail. The default value is 360 seconds. This value is optional.</dd>
<dt>`--cn`, `--concurrency`</dt>
<dd>The number of requests that can be processed concurrently. The default value is 1. This value is optional.</dd>
<dt>`--min`, `--minscale`</dt>
<dd>The minimum number of instances that can be used for this application. The default value is 1. This value is optional.</dd>
<dt>`--max`, `--maxscale`</dt>
<dd>The maximum number of instances that can be used for this application. The default value is 1. This value is optional.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set any environmental variables to pass to the application. Variables use a `KEY=VALUE` format. This value is optional.</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. The default value is `false`. This value is optional.</dd>
</dl>

**Example**

```
ibmcloud coligo application update --name myapp --image ibmcom/helloworld 
```
{: pre}

**Output**

```
Updating Application 'myapp' in namespace 'f0173a8d-abc3':
Application 'fmoapp' updated to latest revision 'myapp-oobym-3' and is available at URL:
http://myapp.f0173a8d-abc3.us-south.knative.appdomain.cloud
```
{: screen} -->

### `ibmcloud coligo application list`
{: #cli-application-list}

List all applications in a project. 
{: shortdec}

```
ibmcloud coligo application list
```
{: pre}

**Example**

```
ibmcloud coligo application list 
```
{: pre}

**Output**

```
NAME        URL                                                                    LATEST              AGE   CONDITIONS   READY   REASON
myapp       http://myapp.b49ca89f-g99q.us-south.knative.test.appdomain.cloud       myapp-zxxlr-1       19h   3 OK / 3     True
mytestapp   http://mytestapp.42734592-8355.us-south.knative.test.appdomain.cloud   mytestapp-qhmzn-1   20h   3 OK / 3     True
```
{: screen}



## Job definition commands
{: #cli-jobdef}

Before using job definition commands, you must be targeting a [project](#cli-project). A job definition is a template that contains workload configuration information that is used to run [jobs](#cli-job-runcmd). After creating a job definition, one or more jobs can be submitted based on the job definition, optionally overwriting values of the job definition. Use job definition commands to create, display details, update, and delete applications. 

{: shortdec}

You can use either `jobdef` or `jd` in your job definition commands. 
To see CLI help for the job definition command, run `ibmcloud coligo `jd`. 
{: tip}

### `ibmcloud coligo jobdef create`
{: #cli-jobdef-create}

Create a job definition.
{: shortdec}

```
ibmcloud coligo jobdef create --name JOBDEFINITION_NAME --image IMAGE_REF --argument ARGUMENT [--command COMMAND][--cpu CPU] [--memory MEMORY] [--env ENV]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. This value is required. The name must begin with a lowercase letter, can contain letters, numbers, periods (.), and hyphens (-), and must be 35 characters or fewer. The name must start and end with a lowercase alphanumeric character. Use a name that is unique within the project.
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this job definition. This value is required. For images in [Docker Hub](https://hub.docker.com){: external}, you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. </dd>
<dt>`-a`, `--argument`</dt>
<dd>Set any arguments for the job definition. This value is required. Specify one argument per `--argument` flag.  To specify more than one argument, use more than one `--argument` flag; for example, `-a argA -a argB`.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set any environmental variables to pass to the job definition. Variables use a `KEY=VALUE` format. This value is optional.</dd>
<dt>`-c`, `--command`</dt>
<dd>Set a command for the job definition. This value is optional.</dd>
<dt>`--cpu`</dt>
<dd>Specifies the number of CPUs to be assigned to the job definition. The default value is 1. This value is optional.</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory set for the job definition. The default value is 128 M. This value is optional.</dd>
</dl>

**Example**

The following example uses the container image `busybox` and uses the arguments `/bin/sh -c echo Hello $JOB_INDEX ENV1 is $ENV1, ENV2 is $ENV2, ENV3 is $ENV3`, assigning 128 MB as memory and 1 CPU to the container.

```
ibmcloud coligo jobdef create --image busybox --name hello --argument /bin/sh --argument "-c" --argument "echo Hello $JOB_INDEX. ENV1 is $ENV1, ENV2 is $ENV2, ENV3 is $ENV3" -e "ENV1=env1 from jobdef" -e "ENV2=env2 from jobdef" -e "ENV3=env3 from jobdef" --memory 128M --cpu 1
```
{: pre}

**Output**

```
Created successfully Job Definition 'hello'
```
{: screen}

### `ibmcloud coligo jobdef get`
{: #cli-jobdef-get}

Display the details of a job definition.
{: shortdec}

```
ibmcloud coligo jobdef get --name JOBDEFINITION_NAME
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. This value is required.</dd>
</dl>

**Example**

```
ibmcloud coligo jobdef get --name myjobdef
```
{: pre}

**Output**

```
Name:         myjobdef
Namespace:    b49ca89f-g99q
Labels:       <none>
Annotations:  <none>
API Version:  coligo.cloud.ibm.com/v1alpha1
Kind:         JobDefinition
Metadata:
  Creation Timestamp:  2020-04-16T15:21:41Z
  Generation:          1
  Resource Version:    69009760
  Self Link:           /apis/coligo.cloud.ibm.com/v1alpha1/namespaces/b49ca89f-g99q/jobdefinitions/myjobdef
  UID:                 6ac2e78c-0883-4564-9158-4c7e08762a41
Spec:
  Containers:
    Args:
      /bin/sh
      -c
      echo Hello $JOB_INDEX. ENV1 is $ENV1, ENV2 is $ENV2, ENV3 is $ENV3
    Env:
      Name:   ENV1
      Value:  env1 from jobdef
      Name:   ENV2
      Value:  env2 from jobdef
      Name:   ENV3
      Value:  env3 from jobdef
    Image:    busybox
    Name:     myjobdef
    Resources:
      Requests:
        Cpu:     1
        Memory:  128Mi
Events:          <none>

Command 'job definition get' performed successfully
```
{: screen}



### `ibmcloud coligo jobdef delete`
{: #cli-jobdef-delete}

Delete a job definition.
{: shortdec}

```
ibmcloud coligo jobdef delete --name JOBDEFINITION_NAME
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. This value is required.</dd>
</dl>

**Example**

```
ibmcloud coligo jobdef delete --name myjobdef
```
{: pre}

**Output**

```
Deleted JobDefinition 'myjobdef'
```
{: screen}

### `ibmcloud coligo jobdef list`
{: #cli-jobdef-list}

List all job definitions in a project.
{: shortdec}

```
ibmcloud coligo jobdef list
```
{: pre}

**Example**

```
ibmcloud coligo jobdef list
```
{: pre}

**Output**

```
NAME        AGE
hello       5d14h
hello2      5d14h
myjobdef    5d15h
```
{: screen}

## Job commands
{: #cli-job-runcmd}

A job runs your code to complete a task. Before using job commands, you must be targeting a [project](#cli-project) and have a [job definition](#cli-jobdef) created. Jobs are submitted based on a job definition. After a job definition is created, you can run one or more jobs that refer to the job definition, optionally overwriting values of the job definition. Use job commands to create, display details, and delete jobs. 
{: shortdec}

To see CLI help for the job commands, run `ibmcloud coligo job`. 
{: tip}

### `ibmcloud coligo job run`
{: #cli-job-run}

Run a job based on a job definition.
{: shortdec}

```
ibmcloud coligo job run --name JOBRUN_NAME --jobdef JOBDEFINITION_NAME [--image IMAGE_REF] [--cpu CPU] [--memory MEMORY] [--env ENV] [--argument ARGUMENT] [--command COMMAND] [--arraysize ARRAY] [--retrylimit RETRY] [--maxexecutiontime MAXEXECUTIONTIME]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job to be run. This value is required. The name must begin with a lowercase letter, can contain letters, numbers, periods (.), and hyphens (-), and must be 35 characters or fewer. The name must start and end with a lowercase alphanumeric character. Use a name that is unique within the project.
<dt>`--jd`, `--jobdef`</dt>
<dd>Identifies the job definition that contains the description of the job to be run. This value is required.</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this job. This value is required. For images in [Docker Hub](https://hub.docker.com){: external}, you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value overrides any `--image` value that is assigned in the job definition.</dd>
<dt>`-e`, `--env`</dt>
<dd>Specifies any environmental variables to pass to the image. Variables use a `KEY=VALUE` format. This value overrides any environmental variables that are passed in the job definition. This value is optional. </dd>
<dt>`-a`, `--argument`</dt>
<dd>Sets any arguments for the container. To specify more than one argument, use more than one `--argument` flag; for example, `-a argA -a argB`. This value overrides any arguments passed in the job definition. This value is optional.</dd>  
<dt>`-c`, `--command`</dt>
<dd>Set a command. This value overrides any commands that are passed in the job definition. This value is optional.</dd>
<dt>`--cpu`</dt>
<dd>Specifies the number of CPUs to assign to the container that is running the image. This value overrides any `--cpu` value that is assigned in the job definition. If this value is not set in the job definition or the job run, the default value is 1. This value is optional.</dd>
<dt>`-m`, `--memory`</dt>
<dd>Specifies the amount of memory to assign to the container that is running the image. This value overrides any `--memory` value that is assigned in the job definition. If this value is not set in the job definition or the job run, the default value is 128 M. This value is optional.</dd>
<dt>`--as`, `--arraysize`</dt>
<dd>Specifies the number of pods used to run the container specified by the job definition. The default value is 1. This value is optional.</dd>
<dt>`-r`, `--retrylimit`</dt>
<dd>Specifies the number of times to retry the job.  The default value is 3. This value is optional.</dd>
<dt>`--met`, `--maxexecutiontime`</dt>
<dd>Specifies the maximum execution time for the job.  The default value is 7200 seconds. This value is optional.</dd>
</dl>

**Example**

The following example creates three new pods to run the container image specified in the `hello` job definition. The resource limits and requests are applied per pod, so each of the pods gets 128 MB memory and 1 vCPU. This array job allocates 5 \* 128 MiB = 640 MiB memory and 5 \* 1 vCPU = 5 vCPUs.

```
ibmcloud coligo job run --name myjobrun --jobdef myjobdef --arraysize 5 --retrylimit 2 --memory 128M --cpu 1
```
{: pre}

**Output**

```
Creating Job 'myjobrun'...
OK
Successfully created Job 'myjobrun'
```
{: screen}

### `ibmcloud coligo job list`
{: #cli-job-list}

List all running jobs in a project.
{: shortdec}

```
ibmcloud coligo job list
```
{: pre}

**Example**

```
ibmcloud coligo job list
```
{: pre}

**Output**

```
NAME             AGE
hellojob-sjf2t   2d17h
myjobrun-gvq57   2m18s
```
{: screen}

The name of the job listed indicates the name of the job and the current revision of the job.  
{: tip}

### `ibmcloud coligo job get`
{: #cli-job-get}

Display the details of a job.
{: shortdec}

```
ibmcloud coligo job get --name JOBRUN_NAME 
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. This value is required.</dd>
</dl>

**Example**

```
ibmcloud coligo job get --name hellojob
```
{: pre}

**Output**

```
Getting Job 'myjobrun'...
Name:         myjobrun-gvq57
Namespace:    42642513-8805
Labels:       coligo.cloud.ibm.com/job-definition=myjobdef
              jobrun=myjobrun
Annotations:  coligo.cloud.ibm.com/pod-expectations: 5
API Version:  coligo.cloud.ibm.com/v1alpha1
Kind:         JobRun
Metadata:
  Creation Timestamp:  2020-05-04T17:41:37Z
  Generate Name:       myjobrun-
  Generation:          1
  Resource Version:    87729212
  Self Link:           /apis/coligo.cloud.ibm.com/v1alpha1/namespaces/42642513-8805/jobruns/myjobrun-gvq57
  UID:                 25de99f4-b4a3-4ad6-a226-06aa5cdf297c
Spec:
  Array Size:          5
  Job Definition Ref:  myjobdef
  Job Definition Spec:
    Containers:
      Image:  busybox
      Name:   myjobdef
      Resources:
        Requests:
          Cpu:         1
          Memory:      128Mi
  Max Execution Time:  7200
  Retry Limit:         2
Status:
  Completion Time:  2020-05-04T17:41:42Z
  Conditions:
    Last Probe Time:       2020-05-04T17:41:37Z
    Last Transition Time:  2020-05-04T17:41:37Z
    Status:                True
    Type:                  Pending
    Last Probe Time:       2020-05-04T17:41:40Z
    Last Transition Time:  2020-05-04T17:41:40Z
    Status:                True
    Type:                  Running
    Last Probe Time:       2020-05-04T17:41:42Z
    Last Transition Time:  2020-05-04T17:41:42Z
    Status:                True
    Type:                  Complete
  Effective Job Definition Spec:
    Containers:
      Args:
        /bin/sh
        -c
        echo Hello . ENV1 is , ENV2 is , ENV3 is
      Env:
        Name:   ENV1
        Value:  env1 from jobdef
        Name:   ENV2
        Value:  env2 from jobdef
        Name:   ENV3
        Value:  env3 from jobdef
      Image:    busybox
      Name:     myjobdef
      Resources:
        Requests:
          Cpu:     1
          Memory:  128Mi
  Start Time:      2020-05-04T17:41:37Z
  Succeeded:       5
Events:
  Type    Reason     Age                   From                  Message
  ----    ------     ----                  ----                  -------
  Normal  Updated    3m57s (x9 over 4m1s)  batch-job-controller  Updated JobRun "myjobrun-gvq57"
  Normal  Completed  3m57s                 batch-job-controller  JobRun completed successfully

Command 'job get' performed successfully
```
{: screen}

### `ibmcloud coligo job logs`
{: #cli-job-logs}

Display the logs of one job.
{: shortdec}

```
ibmcloud coligo job logs --name JOBRUN_NAME [--pod POD]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. This value is required.</dd>
<dt>`-p`, `--pod`</dt>
<dd>The job pod index. The default value is 0. This value is optional. </dd>
</dl>

**Example**

```
ibmcloud coligo job logs --name myjobrun
```
{: pre}

**Output**

```
Logging Job 'myjobrun' on Pod 0...

Hello . ENV1 is , ENV2 is , ENV3 is

Command 'job logs' performed successfully
```
{: screen}

### `ibmcloud coligo job delete`
{: #cli-job-delete}
Delete the job.
{: shortdec}

```
ibmcloud coligo job delete --name JOBRUN_NAME
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. This value is required.</dd>
</dl>

**Example**

```
ibmcloud coligo job delete --name myjobrun
```
{: pre}

**Output**

```
Deleting Job 'myjobrun'...

Deleted Job 'myjobrun'
```
{: screen}

## Secret commands
{: #cli-secrets}

Create Coligo secrets. 
{: shortdec}

To see CLI help for the secret commands, run `ibmcloud coligo secret`. 
{: tip}

### `ibmcloud coligo secret create` (Generic)
{: #cli-secret-create-generic}

Create a generic secret from a value pair or from a file.
{: shortdec}

```
ibmcloud coligo secret create --name SECRETNAME  --from-literal NAME=VALUE | --from-file PATH_TO_FILE
```
{: pre}

**Command options**
<dl>
<dt>`--name`</dt>
<dd>The name of the secret. This value is required. The name must begin with a lowercase letter, can contain letters, numbers, periods (.), and hyphens (-), and must be 35 characters or fewer. The name must start and end with a lowercase alphanumeric character. Use a name that is unique within the project.</dd>
<dt>`-f`, `--from-file value`</dt>
<dd>Include this flag to create a generic secret from a file. You must provide the path to the file as a value. If you do not use this flag, you must use the `--from-literal` flag.</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Include this flag to create a generic secret from a value pair. The format must be `NAME=VALUE`.  If you do not use this flag, you must use the `--from-file` flag.</dd>
</dl>

**Example**

- The following example creates a secret that is named `mysecret-fromliteral` with a username and password value pair.

  ```
  ibmcloud coligo secret create --name mysecret-fromliteral --from-literal username=devuser --from-literal password='S!B\*d$zDsb'
  ```
  {: pre}

  **Output**

  ```
  Creating Generic Secret...
  secret/mysecret-fromliteral created
  Generic Secret created successfully
  ```
  {: screen}

- The following example creates a secret that is named `mysecret-fromfile` with values from a file.

  ```
  ibmcloud coligo secret create --name mysecret-fromfile  --from-file ./username.txt --from-file ./password.txt
  ```
  {: pre}

  **Output**

  ```
  Creating Generic Secret...
  secret/mysecret-fromfile created

  Generic Secret created successfully
  ```
  {: screen}

### `ibmcloud coligo secret create` (Image pull)
{: #cli-secret-create-imgpull}

Create an image pull secret. Use image pull to access a container registry that stores the secrets.
{: shortdec}

```
ibmcloud coligo secret create --name SECRET_NAME --from-registry URL --username USERNAME --password PASSWORD
```
{: pre}

**Command options**
<dl>
<dt>`--name`</dt>
<dd>The name of the secret. This value is required. The name must begin with a lowercase letter, can contain letters, numbers, periods (.), and hyphens (-), and must be 35 characters or fewer. The name must start and end with a lowercase alphanumeric character. Use a name that is unique within the project.</dd>
<dt>`-r`, `--from-registry`</dt>
<dd>Provide the URL of the image registry that contains the secret. This value is required.</dd>
<dt>`-u`, `--username`</dt>
<dd>Provide the username for the secret in the registry. This value is required.</dd>
<dt>`-p`, `--password`</dt>
<dd>Provide the password for the secret in the registry. This value is required.</dd>
</dl>

**Example**

```
ibmcloud coligo secret create --name mysecret-fromimage --from-registry us.icr.io --username myusername --password 39c-fa445-9773ac48a92
```
{: pre}

**Output**

```
Creating Image Secret...
secret/mysecret-fromimage created

Image Secret created successfully
```
{: screen}

### `ibmcloud coligo secret delete`
{: #cli-secret-delete}

Delete a secret.
{: shortdec}

```
ibmcloud coligo secret delete --name SECRETNAME
```
{: pre}

**Command options**
<dl>
<dt>`--name`</dt>
<dd>The name of the secret. This value is required.</dt>
</dl>

**Example**

```
ibmcloud coligo secret delete mysecret
```
{: pre}

**Output**

```
Deleting Secret mysecret...

Successfully deleted secret 'mysecret'.
```
{: screen}



## Configmap commands
{: #cli-configmap}

Use configmap commands to create, display details, and delete configmaps. 
{: shortdec}

You can use either `configmap` or `cm` in your configmap commands. 
To see CLI help for the configmap commands, run `ibmcloud coligo configmap`.
{: tip}

### `ibmcloud coligo configmap create`
{: #cli-configmap-create}

Create a configmap.
{: shortdec}

```
ibmcloud coligo configmap create --name CONFIGMAPNAME  --from-literal NAME=VALUE | --from-file PATH_TO_FILE
```
{: pre}

**Command options**
<dl>
<dt>`--name`</dt>
<dd>The name of the configmap. This value is required. The name must begin with a lowercase letter, can contain letters, numbers, periods (.), and hyphens (-), and must be 35 characters or fewer. The name must start and end with a lowercase alphanumeric character. Use a name that is unique within the project.</dd>
<dt>`-f`, `--from-file value`</dt>
<dd>Include this flag to create a configmap from a file. You must provide the path to the file as a value. If you do not use this flag, you must use the `--from-literal` flag.</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Include this flag to create a configmap from a value pair. The format must be `NAME=VALUE`.  If you do not use this flag, you must use the `--from-file` flag.</dd>
</dl>

**Examples**

- The following example creates a configmap that is named `configmap-fromliteral` with a username and password value pair.

  ```
  ibmcloud coligo configmap create --name configmap-fromliteral --from-literal username=devuser --from-literal password='S!B99d$Y2Ksb'
  ```
  {: pre}

  **Output**

  ```
  Creating Configmap 'configmap-fromliteral'...

  Successfully created configmap 'configmap-fromliteral'. Run `ibmcloud coligo configmap get -n 'configmap-fromliteral'` to see more details.
  ```
  {: screen}
  
- The following example creates a configmap that is named `configmap-fromfile` with values from a file.

  ```
  ibmcloud coligo configmap create --name configmap-fromfile  --from-file ./username.txt --from-file ./password.txt
  ```
  {: pre}

  **Output**

  ```
  Creating Configmap 'configmap-fromfile'...

  Successfully created configmap 'configmap-fromfile'. Run `ibmcloud coligo configmap get -n 'configmap-fromfile'` to see    more details.
  ```
  {: screen}

### `ibmcloud coligo configmap get`
{: #cli-configmap-get}

Display the details of a configmap.
{: shortdec}

```
ibmcloud coligo configmap get --name CONFIGMAPNAME 
```
{: pre}

**Command options**
<dl>
<dt>`--name`</dt>
<dd>The name of the configmap. This value is required.</dd>
</dl>

**Example**

```
ibmcloud coligo configmap get --name configmap-fromliteral 
```
{: screen}

**Output**

```
Getting Configmap 'configmap-fromliteral'...

Name:        configmap-fromliteral
Namespace:   401de621-cc61
Labels:      <none>
Annotations: <none>

Data
====
username:
password:
----
S!B99d$Y2Ksb
devuser
Events:  <none>

Successfully performed 'configmap get configmap-fromliteral' command
```
{: screen}

### `ibmcloud coligo configmap update`
{: #cli-configmap-update}

Update a configmap.
{: shortdec}

```
ibmcloud coligo configmap update --name CONFIGMAPNAME  --from-literal NAME=VALUE | --from-file PATH_TO_FILE
```
{: pre}

**Command options**
<dl>
<dt>`--name`</dt>
<dd>The name of the configmap. This value is required. The name must begin with a lowercase letter, can contain letters, numbers, periods (.), and hyphens (-), and must be 35 characters or fewer. The name must start and end with a lowercase alphanumeric character. Use a name that is unique within the project.</dd>
<dt>`-f`, `--from-file value`</dt>
<dd>Include this flag to update a configmap from a file. You must provide the path to the file as a value. If you do not use this flag, you must use the `--from-literal` flag.</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Include this flag to update a configmap from a value pair. The format must be `NAME=VALUE`.  If you do not use this flag, you must use the `--from-file` flag.</dd>
</dl>

**Examples**

- The following example updates a configmap that is named `configmap-fromliteral` with a username and password value pair.

  ```
  ibmcloud coligo configmap update --name configmap-fromliteral --from-literal username=devuser --from-literal password='S!B99d$Y2Ksb'
  ```
  {: pre}

  **Output**

  ```
  Updating Configmap configmap-fromliteral...
  OK
  Successfully updated configmap 'configmap-fromliteral'. Run `ibmcloud coligo configmap get -n configmap-fromliteral` to see more details.
  ```
  {: screen}
  
- The following example updates a configmap that is named `configmap-fromfile` with values from a file.

  ```
  ibmcloud coligo configmap update --name configmap-fromfile  --from-file ./username.txt --from-file ./password.txt
  ```
  {: pre}

  **Output**

  ```
  Updating Configmap configmap-fromfile...
  OK
  Successfully updated configmap 'configmap-fromfile'. Run `ibmcloud coligo configmap get -n configmap-fromfile` to see more details.

  ```
  {: screen}

### `ibmcloud coligo configmap list`
{: #cli-configmap-list}

List all configmaps in a project.  
{: shortdec}

```
ibmcloud coligo configmap list
```
{: pre}

**Example**

```
ibmcloud coligo configmap list 
```
{: pre}

**Output**

```
Listing Configmaps...
Name                    Data   Age
configmap-fromfile      2      19m13s
configmap-fromliteral   2      16m12s

Command 'configmap list' performed successfully
```
{: screen}


### `ibmcloud coligo configmap delete`
{: #cli-configmap-delete}

Delete a configmap.
{: shortdec}

```
ibmcloud coligo configmap delete --name CONFIGMAPNAME
```
{: pre}

**Command options**
<dl>
<dt>`--name`</dt>
<dd>The name of the configmap. This value is required.</dd>
</dl>

**Example**

```
ibmcloud coligo configmap delete --name configmap-fromliteral
```
{: pre}

**Output**

```
Deleting Configmap 'configmap-fromliteral'...

Successfully deleted configmap 'configmap-fromliteral'
```
{: screen}
