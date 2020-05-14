---

copyright:
  years: 2020
lastupdated: "2020-04-24"

keywords: knative, api reference

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

# API reference
{: #api}

You can use the IBM Cloud Coligo API to create and manage your Coligo entities. To use the CLI, see [Setting up the CLI](/docs/knative?topic=knative-kn-install-cli).
{: shortdesc}

## Retrieve your Kubernetes configuration with REST API
{: #api-rest}

To retrieve your Kubernetes configuration with REST API, follow these steps:

1. Authenticate with IBM Cloud Identity and Access Management (IAM) to receive an IAM access token.
2. Query the IBM Cloud Catalog and the IBM Cloud Resource Controller to receive a GUID for your project.
3. Use the IBM Coligo API to receive a Kubernetes configuration.

### Authenticate with IBM Cloud IAM
{: #api-iam}

[Create your {{site.data.keyword.cloud_notm}} IAM access token](/docs/iam?topic=iam-iamtoken_from_apikey){: external} by making a POST request to `https://iam.cloud.ibm.com/identity/token`.

### Determine the GUID of your project
{: #api-guid}

Determine the GUID of your Coligo project by quering the IBM Cloud Catalog and IBM Cloud Resource Controller. As this GUID does not change, you need to do this step only one time. If you already know your Coligo project GUID, you can skip this step.

**CLI**

1. Log in into IBM Cloud and target a region, account, and resource group:
   
   ```
   ibmcloud login target -r REGION -c ACCOUNT_ID -g RESOURCE_GROUP
   ```
   {: pre}
 
 2. Run the `ibmcloud resource` command.
    
    ```
    ibmcloud resource service-instances --service-name knative --long
    ```
    {: pre}
    
Identify the service instance that represents your Coligo project and determine the GUID from the output.

**REST API**

Before you begin, you must have the `access_token` from the previous step.

1. Use following IBM Cloud Catalog API method: [Returns parent catalog entries](https://cloud.ibm.com/apidocs/resource-catalog/global-catalog#returns-parent-catalog-entries){: external}.

   Example:

   ```
   curl -X GET \
     'https://globalcatalog.cloud.ibm.com/api/v1?include=*&q=name:knative+active:true" \
     -H 'Authorization: Bearer ACCESS_TOKEN'
   ```
   {: pre}

   Identify the unique resource ID in the resources list. The field name is `ID` and the JSON path is `resources[].id`.
   
2. Query the IBM Cloud Resource Controller with the IBM Cloud Resource Controller API method [Get a list of all resource instances](https://cloud.ibm.com/apidocs/resource-controller/resource-controller#get-a-list-of-all-resource-instances){: external}. You must have the Coligo project name, the region that your project resides, and the unique resource ID of Coligo in the global catalog. Use the name of your Coligo project as query parameter.

   Example:

   ```
   curl -X GET \
     'https://resource-controller.cloud.ibm.com/v2/resource_instances?name=MY_PROJECT&resource_id=RESOURCE_ID' \
     -H 'Authorization: Bearer ACCESS_TOKEN'
   ```
   {: pre}

   Identify the Coligo project from your region in the result list. Find the `guid` output to use in the following steps.

### Query the IBM Coligo API
{: #api-query-api}

Before you begin, you must have the following information.

- The `access_token` and `refresh_token` from previous steps.
- The `guid` of your Coligo project.
- The region in which your Coligo project is located.

Use the [`get kubeconfig for the specified project`](https://cloud.ibm.com/apidocs/coligo#get-kubeconfig-for-the-specified-project){: external} Coligo API method to get the Kubernetes configuration.

   Example:

   ```
   curl -X GET \
     'https://resource-controller.cloud.ibm.com/v2/resource_instances?name=MY_PROJECT&resource_id=RESOURCE_ID' \
     -H 'Authorization: Bearer ACCESS_TOKEN'
   ```
   {: pre}

## Retrieving your Kubernetes configuration with the CLI
{: #api-cli}

1. Log in into IBM Cloud and target a region, account, and resource group:
   
   ```
   ibmcloud login target -r REGION -c ACCOUNT_ID -g RESOURCE_GROUP
   ```
   {: pre}
   
2. Target your Coligo project and export the Kubernetes config: 

   ```
   ibmcloud coligo target --name PROJECT --export.
   ```
   {: pre}
   
For more information about using Coligo APIs, Kubernetes API, and `kubectl`, see the following topics:

- [Coligo API](https://cloud.ibm.com/apidocs/knative){: external}
- [Kubernetes REST API](https://kubernetes.io/docs/reference/using-api/api-overview/){: external}
- [Kubernetes API concepts](https://kubernetes.io/docs/reference/using-api/api-concepts/){: external}
- [API client libraries](https://kubernetes.io/docs/reference/#api-client-libraries){: external}
- [`kubectl` command](https://kubernetes.io/docs/reference/#cli-reference){: external}

## Custom resource definition (CRD)
{: #api-crd}

The following sections list the custom resource definition methods to use with Coligo.

**Batch CRDs**

| Group | Version | Kind |
| --------- | -------- | -------- |
| coligo.cloud.ibm.com | v1alpha1 | JobDefinition |
| coligo.cloud.ibm.com | v1alpha1 | JobRun |

After retrieving the Kubernetes configuration, you can view Batch CRD details using the following methods:

1. Use `kubectl explain --api-version='coligo.cloud.ibm.com/v1alpha1' <Kind>`.
2. [Download Swagger / OpenAPI specification of CRDs](https://kubernetes.io/docs/concepts/overview/kubernetes-api/){: external}.
  
**Serving CRDs**

| Group | Version | Kind |
| --------- | -------- | -------- |
| serving.knative.dev | v1 | Configuration |
| serving.knative.dev | v1 | Revision |
| serving.knative.dev | v1 | Route |
| serving.knative.dev | v1 | Service |

For more information about these CRDS, see [Knative Serving API Specification](https://knative.dev/docs/serving/spec/knative-api-specification-1.0/){: external}.
