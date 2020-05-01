---

copyright:
  years: 2020
lastupdated: "2020-05-01"

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

# Deploying application workloads
{: #knative-deploy-app-tutorial}

With this tutorial, deploy a containerized application in a serverless fashion. The application pod scales to zero when not in use.

** Before you start**

- [Set up your Coligo environment](/docs/knative?topic=knative-kn-install-cli)
- Create a docker image


## Step 1 - Assemble and deploy a knative service

1. Create a `hellworld` API server in Go.

   ```
   cat helloworld.go
   package main

   import (
      	   "fmt"
	   "log"
	   "net/http"
	   "os"
   )

   func handler(w http.ResponseWriter, r *http.Request) {
	   log.Print("Hello world received a request.")
	   target := os.Getenv("TARGET")
	   if target == "" {
	   	   target = "World"
	   }
	   fmt.Fprintf(w, "Hello %s!\n", target)
   }

   func main() {
	   log.Print("Hello world sample started.")

	   http.HandleFunc("/", handler)

	   port := os.Getenv("PORT")
	   if port == "" {
		   port = "8080"
	   }
   
	   log.Fatal(http.ListenAndServe(fmt.Sprintf(":%s", port), nil))
   }
   ```
   {: pre}

For this tutorial, the docker image file has been created for you and is available at [agrawals18/helloworld}(https://cloud.docker.com/repository/docker/agrawals18/helloworld)

If you have a sample container image that you want to use, you can replace the image reference in the next step with your docker repository, image name, and version. If you want to build the image your own with docker, see [How to run steps 4 to 6 with your own image](#optional-run-steps-1-to-4-with-your-own-image)

2.  Deploy a new knative service using `kn cli`.

    ```
    kn service create helloworld --image agrawals18/helloworld --requests-cpu 50m --requests-memory 128Mi --limits-cpu 2000m --limits-memory 4Gi

    ```
    {: pre}

   **Sample output**

   ```
   Service 'helloworld' successfully created in namespace `86f22937-67fe-42cb-b405-8dbacccb1edf`.
   Waiting for service 'helloworld' to become ready ... OK

   Service URL:
   http://helloworld-86f22937-67fe-42cb-b405-8dbacccb1edf.functions.test.appdomain.cloud
   ```
   {: screen}

## Step 2 - Call the service API

1. Get the public endpoint of the service with `kn`

   ```
   kn service list
   ```
   {: pre}

   **Sample output**

   ```
   Name         Domain                                                                                 Annotations         Conditions   Age
   helloworld  http://helloworld-86f22937-67fe-42cb-b405-8dbacccb1edf.functions.test.appdomain.cloud     -             3 OK / 3    23s

   ```
   {: screen}

2. Copy the domain URL and call the API with `curl`.

   ```
   curl http://helloworld-86f22937-67fe-42cb-b405-8dbacccb1edf.functions.test.appdomain.cloud
   ```
   {: pre}
   
   **Sample output**

   ```
      Hello World!
   ```
   {: screen}
   
Congratulations, you have successfully deployed and invoked your first service on knative!

## Step 3 - Update your service

1. Update your newly created Knative service with `kn` by providing a memory limit.

   ```
   kn service update helloworld --requests-memory 256Mi
   ```
   {: pre}
   
   **Sample output**

   ```
   Waiting for service 'helloworld' to become ready ... OK
   Service 'helloworld' updated in namespace '86f22767-67fe-42ab-b405-8dbadccb1gdf'.
   ```
   {: screen}

2. List all revisions to find the new revision. 

   ```
   kn revision list
   ```
   {: pre}
   
   **Sample output**

   ```
   NAME                SERVICE       AGE   CONDITIONS   READY   REASON
   helloworld-5jt2f    helloworld    95s   3 OK / 4     True
   helloworld-x5hns    helloworld    25m   3 OK / 4     True

   ```
   {: screen}

   From the output, you can see that there are two revisions of the `helloworld` service.

3. By default, new calls to the service are routed to the new revision. You can verify this action by listing the routes.

   ```
   kn route list
   ```
   {: pre}
   
   **Sample output**

   ```
   NAME          URL                                                                                      AGE   CONDITIONS   TRAFFIC
   helloworld    http://helloworld-86f22937-67fe-42cb-b405-8dbacccb1edf.functions.test.appdomain.cloud    26m   3 OK / 3     100% -> helloworld-5jt2f

   ```
   {: screen}

   As shown in the sample output, under TRAFFIC `100% -> helloworld-5jt2f` where `helloworld-5jt2f` is the new revision name.

4. You can find All the above resources can be listed, described, and deleted using `kn`

   ```
   kn service/revision/route delete <service name>/<revision name>/<route name>
   ```
   {: pre}
   
   **Sample output**

   ```
   Service/ Revision/ Route <service name>/<revision name>/<route name> successfully deleted in namespace '86f22937-67fe-42cb-b405-8dbacccb1edf'.
   ```
   {: screen}

### Step 4 - Scale-to-zero and Scale-from-zero

1. Call the service API:

   ```
   curl helloworld1.86f22937-67fe-42cb-b405-8dbacccb1edf.functions.test.appdomain.cloud
   ```
   {: pre}
   
   **Sample output**
   
   ```
   Hello World!
   ```
   {: screen}

2. List the pods of the service and notice that it has a running pod using `kubectl`:

   ```
   kubectl get pods
   ```
   {: pre}

   **Sample output**

   ```
   NAME                                            READY   STATUS    RESTARTS   AGE
   helloworld1-pj7tb-deployment-5579757bcd-xt4ds   2/2     Running   0          72s
   ```
   {: screen}
   
   Wait a few minutes...

3. List pods again and notice that knative has scaled the pod to zero. 

   ```
   kubectl get pods
   ```
   {: pre}

   **Sample output**

   ```
   No resources found.
   ```
   {: screen}

4. Call the service API again to scale from zero:

   ```
   curl helloworld1.86f22937-67fe-42cb-b405-8dbacccb1edf.functions.test.appdomain.cloud
   ```
   {: pre}
   
   **Sample output**
   
   ```
   Hello World!
   ```
   {: screen}

Voilà!

### What have you seen?
You have deployed an arbitrary containerized application in a serverless fashion. 
In a serverless fashion this means, that you:

1. Don't need to think about scaling, the environment **scale-from zero** to however many instances you need.
2. Don't need to pay for resources that are not used, i.e. the environment **scales-to zero** if no requests come in.

