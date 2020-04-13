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
{:preview: .preview}
{:gif: data-image-type='gif'}

## Using Knative services to deploy a serverless app
{: #knative-deploy-app}

Deploy your serverless app as a Knative service.
{: shortdesc}

**What is a Knative service?** </br>
To deploy an app with Knative, you must specify a Knative `Service` resource. A Knative service is managed by the Knative `Serving` primitive and is responsible to manage the entire lifecycle of the workload. When you create the service, the Knative `Serving` primitive automatically creates a version for your serverless app and adds this version to the revision history of the service. Your serverless app is assigned a public URL from your Ingress subdomain in the format `<knative_service_name>-<namespace>.<ingress_subdomain>` that you can use to access the app from the internet. In addition, a private hostname is assigned to your app in the format `<knative_service_name>-<namespace>.cluster.local` that you can use to access your app from within the cluster. 

**What happens behind the scenes when I create the Knative service?**</br>
When you create a Knative service, your app is automatically deployed as a Kubernetes pod in your cluster and exposed by using a Kubernetes service. To assign the public hostname, Knative uses the IBM-provided Ingress subdomain and TLS certificate. Incoming network traffic is routed based on the default IBM-provided Ingress routing rules.

**How can I roll out a new version of my app?**</br>
When you update your Knative service, a new version of your serverless app is created. This version is assigned the same public and private hostnames as your previous version. By default, all incoming network traffic is routed to the latest version of your app. However, you can also specify the percentage of incoming network traffic that you want to route to a specific app version so that you can do A-B testing. You can split incoming network traffic between two app versions at a time, the current version of your app and the new version that you want to roll over to.  
   
## Pulling images from a private container registry
{: #knative-private-registry}

To access a container registry, your cluster must bet set up with the appropriate image pull secrets that include the credentials to authenticate with your registry. By default, Knative services can access images that are stored in {{site.data.keyword.registryshort_notm}}. To access other private registries, you must store the credentials in a Kubernetes image pull secret in your cluster. 
{: shortdesc}

1. Follow the instructions to [create an image pull secret](/docs/containers?topic=containers-images#private_images) that includes the credentials to access your private container registry.

2. Create a Knative service that uses the image pull secret. You can choose if you want to reference the image pull secret in your Knative service directly as shown in the following example, or to [add the image pull secret to the Kubernetes service account of the namespace](/docs/containers?topic=containers-images#store_imagePullSecret) where you want to deploy your Knative service. 

   Example to reference the image pull secret in your Knative service:

   ```
   apiVersion: serving.knative.dev/v1alpha1
   kind: Service
   metadata:
     name: kn-helloworld
     namespace: default
   spec:
     template:
       spec:
         containers:
         - image: docker.io/ibmcom/kn-helloworld
         imagePullSecrets:
         - name: <secret_name>
   ```
   {: codeblock}
   
3. Create the Knative service in your cluster.

   ```
   kubectl apply -f service.yaml
   ```
   {: pre}

   Example output:

   ```
   service.serving.knative.dev "kn-helloworld" created
   ```
   {: screen}

## Accessing a Knative service from another Knative service
{: #knative-access-service}

You can access your Knative service from another Knative service by using a REST API call to the URL that is assigned to your Knative service.
{: shortdesc}

1. List all Knative services in your cluster.

   ```
   kubectl get ksvc --all-namespaces
   ```
   {: pre}

2. Retrieve the **DOMAIN** that is assigned to your Knative service.

   ```
   kubect get ksvc/<knative_service_name>
   ```
   {: pre}

   Example output:

   ```
   NAME        DOMAIN                                                            LATESTCREATED     LATESTREADY       READY   REASON
   myservice   myservice-default.mycluster.us-south.containers.appdomain.cloud   myservice-rjmwt   myservice-rjmwt   True
   ```
   {: screen}

3. Use the domain name to implement a REST API call to access your Knative service. This REST API call must be part of the app for which you create a Knative service. If the Knative service that you want to access is assigned a local URL in the format `<service_name>-<namespace>.svc.cluster.local`, Knative keeps the REST API request within the cluster-internal network.

   Example code snippet in Go:

   ```go
   resp, err := http.Get("<knative_service_domain_name>")
   if err != nil {
       fmt.Fprintf(os.Stderr, "Error: %s\n", err)
   } else if resp.Body != nil {
       body, _ := ioutil.ReadAll(resp.Body)
       fmt.Printf("Response: %s\n", string(body))
   }
   ```
   {: codeblock}

## Common Knative service settings
{: #knative-service-settings}

Review common Knative service settings that you might find useful as you develop your serverless app.
{: shortdesc}

- [Using Knative services to deploy a serverless app](#using-knative-services-to-deploy-a-serverless-app)
- [Pulling images from a private container registry](#pulling-images-from-a-private-container-registry)
- [Accessing a Knative service from another Knative service](#accessing-a-knative-service-from-another-knative-service)
- [Common Knative service settings](#common-knative-service-settings)
  - [Setting the minimum and maximum number of pods](#setting-the-minimum-and-maximum-number-of-pods)
  - [Scaling your app based on CPU usage or number of requests](#scaling-your-app-based-on-cpu-usage-or-number-of-requests)
  - [Specifying the maximum number of requests per pod](#specifying-the-maximum-number-of-requests-per-pod)
  - [Changing the default container port](#changing-the-default-container-port)
  - [Changing the `scale-to-zero-grace-period`](#changing-the-scale-to-zero-grace-period)
  - [Creating private-only serverless apps](#creating-private-only-serverless-apps)
  - [Forcing the Knative service to repull a container image](#forcing-the-knative-service-to-repull-a-container-image)
- [Related links](#related-links)

### Setting the minimum and maximum number of pods
{: #knative-min-max-pods}

You can specify the minimum and maximum number of pods that you want to run for your apps by using an annotation. For example, if you don't want Knative to scale down your app to zero instances, set the minimum number of pods to 1.
{: shortdesc}

```
apiVersion: serving.knative.dev/v1alpha1
kind: Service
metadata:
  name: ...
spec:
  template:
    metadata:
      annotations:
        autoscaling.knative.dev/minScale: "1"
        autoscaling.knative.dev/maxScale: "100"
    spec:
      containers:
      - image: <image_name>
...
```
{: codeblock}

<table>
<caption>Understanding the YAML file components</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the YAML file components</th>
</thead>
<tbody>
<tr>
<td><code>autoscaling.knative.dev/minScale</code></td>
<td>Enter the minimum number of pods that you want to run in your cluster. Knative cannot scale down your app lower than the number that you set, even if no network traffic is received by your app. The default number of pods is zero.  </td>
</tr>
<tr>
<td><code>autoscaling.knative.dev/maxScale</code></td>
<td>Enter the maximum number of pods that you want to run in your cluster. Knative cannot scale up your app higher than the number that you set, even if you have more requests that your current app instances can handle. You can enter any number that you want up to the [maximum number of pods that you can run per worker node](/docs/containers?topic=containers-ibm-cloud-kubernetes-service-technology#tech_limits).</td>
</tr>
</tbody>
</table>

### Scaling your app based on CPU usage or number of requests
{: #scale-cpu-vs-number-requests}

By default, Knative scales your app based on the average number of incoming requests per pod. If the number of concurrent requests exceeds the default setting of 100 requests per pod, Knative automatically creates another instance of your pod and starts load balancing incoming requests between your instances. This behavior is also referred to as concurrency or concurrent auto-scaling. You can change the default number of requests by [specifying the number of requests per pod](#max-request-per-pod). To instruct Knative to scale your app based on CPU usage instead, use the `autoscaling.knative.dev/metric` annotation.
{: shortdesc}

```
apiVersion: serving.knative.dev/v1alpha1
kind: Service
metadata:
  name: myservice
spec:
  template:
    metadata: 
       annotations:
         autoscaling.knative.dev/metric: cpu
         autoscaling.knative.dev/target: 80
    spec:
      containers:
      - image: <image_name>
....
```
{: codeblock}

<table>
<caption>Understanding the YAML file components</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the YAML file components</th>
</thead>
<tbody>
<tr>
<td><code>autoscaling.knative.dev/metric</code></td>
<td>Instruct Knative to scale your service instances based on CPU usage. By default, the CPU threshold is set to 80 percent. If your service instance exceeds this threshold, then new services instances are automatically created by Knative. If you do not set this annotation, your Knative service is scaled based on the average number of concurrent requests by default.   </td>
</tr>
  <tr>
    <td><code>autoscaling.knative.dev/target</code></td>
    <td>Enter the CPU threshold that your app must meet before Knative scales up your service instances. By default, the threshold is set to <code>80</code>, which scales up your service instances if your app uses 80 percent of the CPU. To change the default setting, enter the CPU threshold that you want. </td>
  </tr>
</tbody>
</table>

### Specifying the maximum number of requests per pod
{: #max-request-per-pod}

You can specify the maximum number of requests that an app instance can receive and process before Knative considers to scale up your app instances. For example, if you set the maximum number of requests to 1, then your app instance can receive one request at a time. If a second request arrives before the first one is fully processed, Knative scales up another instance. By default, Knative sets the maximum number of requests for a pod to 100. 

```
apiVersion: serving.knative.dev/v1alpha1
kind: Service
metadata:
  name: myservice
spec:
  template:
    spec:
      containers:
      - image: <image_name>
      containerConcurrency: 1
....
```
{: codeblock}

<table>
<caption>Understanding the YAML file components</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the YAML file components</th>
</thead>
<tbody>
<tr>
<td><code>containerConcurrency</code></td>
<td>Enter the maximum number of requests an app instance can receive at a time before Knative considers to scale up your app instances.  </td>
</tr>
</tbody>
</table>

### Changing the default container port
{: #knative-container-port}

By default, all incoming requests to your Knative service are sent to port 8080. You can change this setting by using the `containerPort` specification. 
{: shortdesc}

```
apiVersion: serving.knative.dev/v1alpha1
kind: Service
metadata:
  name: ...
spec:
  template:
    spec:
      containers:
        - image: <image_name>
          ports:
          - containerPort: <container_port>
```
{: codeblock}

### Changing the `scale-to-zero-grace-period`
{: #knative-idle-time}

Change the default time that your Knative service instance does not receive any requests before Knative scales down your service to zero instances. 
{: shortdesc}

Knative uses the `config-autoscaler` config map in the `knative-serving` namespace to determine the amount of time to wait before a stable Knative service is considered `idle` and can be scaled down to zero instances. This time is also referred to as the `scale-to-zero-grace-period`.  By default, the grace period is set to 30 seconds. However, before Knative starts counting down the seconds, the service must be considered stable for 60 seconds (`stable-window`). For example, if requests are stopped to your app, your Knative service instance is still up for the next 90 seconds (60s `stable window` + 30s `scale-to-zero-grace-period`) before Knative scales down your service to zero instances. 

If you do not want Knative to scale down your service to zero instances, set the [minimum number of pods](#knative-min-max-pods) to 1. 
{: tip}

1. Open the `config-autoscaler` config map in the `knative-serving` namespace of your cluster. The config map opens in the `vi` editor.

   ```
   kubectl edit configmap config-autoscaler -n knative-serving
   ```
   {: pre}

2. Change the default value for the `scale-to-zero-grace-period`. The new value must be configured in seconds (`s`).

   ```
   scale-to-zero-grace-period: "60s"
   ```
   {: codeblock}

3. Optional. To also change the time that your service must be considered stable, update the `stable-window` property. The new value must be configured in seconds (`s`).

   ```
   stable-window: "90s"
   ```
   {: codeblock}

4. Save your changes to the config map and close the `vi` editor. Your changes are automatically applied to existing and new Knative services. 

### Creating private-only serverless apps
{: #knative-private-only}

By default, every Knative service is assigned a public route from your Istio Ingress subdomain and a private route in the format `<service_name>.<namespace>.cluster.local`. You can use the public route to access your app from the public network. If you want to keep your service private, you can add the `serving.knative.dev/visibility` label to your Knative service. This label instructs Knative to assign a private hostname to your service only.
{: shortdesc}

```
apiVersion: serving.knative.dev/v1alpha1
kind: Service
metadata:
  name: myservice
  labels:
    serving.knative.dev/visibility: cluster-local
spec:
  template:
    spec:
      containers:
      - image: <image_name>
...
```
{: codeblock}

<table>
<caption>Understanding the YAML file components</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the YAML file components</th>
</thead>
<tbody>
<tr>
<td><code>serving.knative.dev/visibility</code></td>
  <td>If you add the <code>serving.knative.dev/visibility: cluster-local</code> label, your service is assigned only a private route in the format <code>&lt;service_name&gt;.&lt;namespace&gt;.cluster.local</code>. You can use the private hostname to access your service from within the cluster, but you cannot access your service from the public network.  </td>
</tr>
</tbody>
</table>

### Forcing the Knative service to repull a container image
{: #knative-repull-image}

The current implementation of Knative does not provide a standard way to force your Knative `Serving` component to repull a container image. To repull an image from your registry, choose between the following options:

- **Modify the Knative service `template`**: The `template` of a Knative service is used to create a revision of your Knative service. If you modify this template and for example, add the `repullFlag` annotation, Knative must create a new revision for your app. As part of creating the revision, Knative must check for container image updates. When you set `imagePullPolicy: Always`, Knative cannot use the image cache in the cluster, but instead must pull the image from your container registry.

   ```
   apiVersion: serving.knative.dev/v1alpha1
   kind: Service
   metadata:
     name: <service_name>
   spec:
     template:
       metadata:
         annotations:
           repullFlag: 123
       spec:
         containers:
         - image: <image_name>
           imagePullPolicy: Always
    ```
    {: codeblock}

    You must change the `repullFlag` value every time that you want to create a new revision of your service that pulls the latest image version from your container registry. Make sure that you use a unique value for each revision to avoid that Knative uses an old image version because of two identical Knative service configurations. 
    {: note}

- **Use tags to create unique container images**: You can use unique tags for every container image that you create and reference this image in your Knative service `container.image` configuration. In the following example, `v1` is used as the image tag. To force Knative to pull a new image from your container registry, you must change the image tag. For example, use `v2` as your new image tag.

  ```
  apiVersion: serving.knative.dev/v1alpha1
  kind: Service
  metadata:
    name: <service_name>
  spec:
    template:
      spec:
        containers:
        - image: myapp:v1
          imagePullPolicy: Always
    ```
    {: codeblock}

## Related links  
{: #knative-related-links}

- Try out this [Knative workshop ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/IBM/knative101/tree/master/workshop){: external} to deploy your first `Node.js` fibonacci app to your cluster.
  - Explore how to use the Knative `Build` primitive to build an image from a Dockerfile in GitHub and automatically push the image to your namespace in {{site.data.keyword.registrylong_notm}}.  
  - Learn how you can set up routing for network traffic from the IBM-provided Ingress subdomain to the Istio Ingress gateway that is provided by Knative.
  - Roll out a new version of your app and use Istio to control the amount of traffic that is routed to each app version.
- Explore [Knative `Eventing` ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/knative/docs/tree/master/docs/eventing/samples){: external} samples.
- Learn more about Knative with the [Knative documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/knative/docs){: external}.
