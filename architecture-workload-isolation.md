---

copyright:
  years: 2020
lastupdated: "2020-04-13"

keywords: knative, public isolation for knative, compute isolation for knative, knative architecture, workload isolation in knative

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

# Learning about Coligo architecture and workload isolation
{: #compute-isolation}

_The short description should be a single, concise paragraph that contains one or two sentences and no more than 50 words. Summarize your offering's architecture and support for isolating one tenants' workload from another._

Review the following sample architecture for Coligo, and learn more about different isolation levels so that you can choose the solution that best meets the requirements of the workloads that you want to run in the cloud.
{: shortdesc}

## Architecture
{: #architecture}

_Review the following example: https://cloud.ibm.com/docs/containers?topic=containers-service-arch. Review the System Architecture Guide: https://pages.github.ibm.com/CloudEngineering/system_architecture/services/multitenancy.html. Provide an architectural overview diagram identifying what runs within the IBM Service Account and what runs in the customer's account._

## Workload isolation
{: #workload-isolation}

_Document how customer workloads are isolated from each other by plan. Do customer workloads run within the customer account?  Are customer workloads isolated within Kubernetes namespaces? Do customer workloads run on dedicated compute? Check out the example from Kubernetes: https://cloud.ibm.com/docs/containers?topic=containers-service-arch#worker-components_
