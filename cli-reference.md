---

copyright:
  years: 2020
lastupdated: "2020-04-30"

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

# Coligo CLI
{: #kn-cli}

Run these commands to manage the entities that make up Coligo.
{: shortdec}

## Project commands
{: #cli-project}

A project is a container for components, such as applications and job definitions. Projects enable you to manage resources and provide access to components in the project. Use project commands to create, display details, and delete projects.
{: shortdec}

To see CLI help for the project command, run `ibmcloud coligo project`.
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
<dd>The name of the project. This value is required. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions.</dd>
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

Targets a Coligo project. Before using the target command, you must have a project created. By targeting a project, the commands that you run are run within the specified project.  
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
export KUBECONFIG=/users/myusername/.bluemix/plugins/coligo/myproject-42642513-8805-4da8-8dbf-bc4f409g9089.yaml
```
{: screen}

## Application commands
{: #cli-application}

Before using application commands, you must be targeting a [project](#cli-project).  An application runs your code to serve HTTP requests. The application has a private URL for incoming requests. Use application commands to create, display details, and update, and delete applications. 
{: shortdec}

 
To see CLI help for the application command, run `ibmcloud coligo application`. 
{: tip}

### `ibmcloud coligo application create`
{: #cli-application-create}

Create an application.
{: shortdec}

```
ibmcloud coligo application create --image IMAGE_REF --name APP_NAME  [--registry-secret SECRET] [--cpu CPU] [--memory MEMORY] [--timeout TIMEOUT] [--concurrency REQUESTS] [--minscale MIN_NUM] [--maxscale MAX_NUM] [--project PROJECT_NAME]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique within the project./dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this application. This value is required. [Docker Hub](https://hub.docker.com/){: external}, you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. </dd>
<dt>`--rs`, `--registry-secret`</dt>
<dd>The name of the secret for the image. This value is optional.</dd>
<dt>`-c`, `--cpu`</dt>
<dd>The amount of CPU set for the instance of the application. The default value is 1. This value is optional.</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory set for the instance of the application. The default value is 64 M. This value is optional.</dd>
<dt>`-t`, `--timeout`</dt>
<dd>The amount of time that can pass before the application must succeed or fail. The default value is 360 seconds. This value is optional.</dd>
<dt>`--cn`, `--concurrency`</dt>
<dd>The number of requests that can be processed concurrently per instance. The default value is 1. This value is optional.</dd>
<dt>`--min`, `--minscale`</dt>
<dd>The minimum number of instances that can be used for this application. The default value is 1. This value is optional.</dd>
<dt>`--max`, `--maxscale`</dt>
<dd>The maximum number of instances that can be used for this application. The default value is 1. This value is optional.</dd>
<dt>`-p`, `--project`</dt>
<dd>The name of the project to contain this application. If this value is not set, then the current project is used. This value is optional.</dd>
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
ibmcloud coligo application get --name APP_NAME
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required.</dd>
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




### `ibmcloud coligo application list`
{: #cli-application-list}

List the details of an application.
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

To see CLI help for the job definition command, run `ibmcloud coligo jobdef`.
{: tip}

### `ibmcloud coligo jobdef create`
{: #cli-jobdef-create}

Create a job definition.
{: shortdec}

```
ibmcloud coligo jobdef create --name JOBDEFINITION_NAME --image IMAGE_REF --argument ARGUMENT [--command COMMAND][--cpu CPU] [--memory MEMORY] [--env ENV] [--env-from-secret ENV_SECRET]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. This value is required. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique within the project.</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this job definition. This value is required. For images in [Docker Hub](https://hub.docker.com/){: external}, you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. </dd>
<dt>`-a`, `--argument`</dt>
<dd>Set any arguments for the job definition. This value is required. Specify one argument per `--argument` flag.  To specify more than one argument, use more than one `--argument` flag; for example, `-a argA -a argB`.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set any environmental variables to pass to the job definition. Variables use a `KEY=VALUE` format. This value is optional.</dd>
<dt>`-c`, `--command`</dt>
<dd>Set any commands for the job definition. This value is optional.</dd>
<dt>`--cpu`</dt>
<dd>Specifies the number of CPUs to be assigned to the job definition. The default value is 1. This value is optional.</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory set for the job definition. The default value is 64 M. This value is optional.</dd>
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
NAME            AGE
app-test-panz   37m
panzutotest     56m
test            69m
```
{: screen}

## Job commands
{: #cli-job-runcmd}

A job runs your code to complete a task. Before using job commands, you must be targeting a [project](#cli-project) and have a [job definition](#cli-jobdef) created. Jobs are submitted based on a job definition. After a job definition is created, you can run one or more jobs that refer to the job definition, optionally overwriting values of the jJob definition. Use job commands to create, display details, and delete jobs. 
{: shortdec}

To see CLI help for the job commands, run `ibmcloud coligo job`. 
{: tip}

### `ibmcloud coligo job run`
{: #cli-job-run}

Run a job based on a job definition.
{: shortdec}

```
ibmcloud coligo job run --name JOBRUN_NAME --jobdef JOBDEFINITION_NAME [--image IMAGE_REF] [--cpu CPU] [--memory MEMORY] [--env ENV] [--argument ARGUMENT] [--command COMMAND] [--arraysize ARRAY] [--retrylimit RETRY]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job to be run. This value is required. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique within the project. </dd>
<dt>`--jd`, `--jobdef`</dt>
<dd>Identifies the job definition that contains the description of the job to be run. This value is required.</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this job. This value is required. [Docker Hub](https://hub.docker.com/){: external}, you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value overrides any `--image` value that is assigned in the job definition.</dd>
<dt>`-e`, `--env`</dt>
<dd>Indicates any environmental variables to pass to the image. Variables use a `KEY=VALUE` format. This value overrides any environmental variables that are passed in the job definition. This value is optional. </dd>
<dt>`-a`, `--argument`</dt>
<dd>Sets any arguments for the container. To specify more than one argument, use more than one `--argument` flag; for example, `-a argA -a argB`. This value overrides any arguments passed in the job definition. This value is optional.</dd>  
<dt>`-c`, `--command`</dt>
<dd>Set any commands for the job. This value overrides any commands that are passed in the job definition. This value is optional.</dd>
<dt>`--cpu`</dt>
<dd>Specifies the number of CPUs to assign to the container that is running the image. This value overrides any `--cpu` value that is assigned in the job definition. If this value is not set in the job definition or the job run, the default value is 1. This value is optional.</dd>
<dt>`-m`, `--memory`</dt>
<dd>Specifies the amount of memory to assign to the container that is running the image. This value overrides any `--memory` value that is assigned in the job definition. If this value is not set in the job definition or the job run, the default value is 64 M. This value is optional.</dd>
<dt>`--as`, `--arraysize`</dt>
<dd>Specifies the number of pods used to run the container specified by the job definition. The default value is 1. This value is optional.</dd>
<dt>`-r`, `--retrylimit`</dt>
<dd>Specifies the number of times to retry the job.  The default value is 3. This value is optional.</dd>
</dl>

**Example**

The following example creates three new pods to run the container image specified in the `hello` JobDefinition. The resource limits and requests are applied per pod, so each of the pods gets 128 MB memory and 1 vCPU. This array job allocates 5 \* 128 MiB = 640 MiB memory and 5 \* 1 vCPU = 5 vCPUs.

```
ibmcloud coligo job run --name hello --jobdef hello --arraysize 5 --retrylimit 2 --memory 128M --cpu 1
```
{: pre}

**Output**

```
ok:
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
panzjob-hjvpz    64m
panzjob2-drzxp   64m
```
{: screen}

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
ibmcloud coligo job get --name myjobrun
```
{: pre}

**Output**

```
ok:
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
ok:
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
ok:
```
{: screen}

## Secrets commands
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
<dd>The name of the secret. This value is required. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique within the project.</dd>
<dt>`-f`, `--from-file value`</dt>
<dd>Include this flag to create a generic secret from a file. You must provide the path to the file as a value. If you do not use this flag, you must use the `--from-literal` flag.</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Include this flag to create a generic secret from a value pair. The format must be `NAME=VALUE`.  If you do not use this flag, you must use the `--from-file` flag.</dd>
</dl>

**Example**

- The following example creates a secret that is named `mySecret` with a username and a password.

  ```
  ibmcloud coligo secret create --name mySecret --from-literal username=devuser --from-literal password='S!B\*d$zDsb'
  ```
  {: pre}

- This example creates a secret that is named `generic-secret` with values from a file.
```
ibmcloud coligo secret create --name mySecret --from-file SECRET_KEY=FILENAME
```
{: pre}

**Output**

```
ok:
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
<dd>The name of the secret. This value is required. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique within the project.</dd>
<dt>`-r`, `--from-registry`</dt>
<dd>Provide the URL of the image registry that contains the secret. This value is required.</dd>
<dt>`-u`, `--username`</dt>
<dd>Provide the username for the secret in the registry. This value is required.</dd>
<dt>`-p`, `--password`</dt>
<dd>Provide the password for the secret in the registry. This value is required.</dd>
</dl>

**Example**

```
ibmcloud coligo secret create --name image.com --from-registry us.icr.io --username mykey --password 39c-fa445-9773ac48a92
```
{: pre}

**Output**

```
Image Secret correctly created
```
{: screen}

### `ibmcloud coligo secret get`
{: #cli-secret-get}

Display details of a secret.
{: shortdec}

```
ibmcloud coligo secret get SECRET_NAME
```
{: pre}

**Command options**
<dl>
<dt>`--name`</dt>
<dd>The name of the secret. This value is required.</dt>
</dl>

**Example**

```
ibmcloud coligo secret get mysecret
```
{: pre}

**Output**

```
ok:
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

### `ibmcloud coligo secret list`
{: #cli-secret-list}

List secrets.
{: shortdec}

```
ibmcloud coligo secret list
```
{: pre}

**Example**

```
ibmcloud coligo secret list
```
{: pre}

**Output**

```
ok:
```
{: screen}
