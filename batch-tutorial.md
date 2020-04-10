---

copyright:
  years: 2020
lastupdated: "2020-10-21"

keywords: knative

subcollection: functions

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
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}

# Deploying jobs
{: #kn-deploying-jobs}

The Coligo platform provides support for run-to-completion workloads. When using the term batch, we talk about this support. Jobs are units of run-to-completion workloads Users define and submit jobs. A job runs one or more job containers according to their definition. A job is complete after all the job containers have completed,

**Before you begin**

- [Set up your coligo environment](/docs/functions?topic=functions-kn-install-cli)
- Target a project

## Create a job run

Array jobs are a perfect match for processing large volumes of independant workloads in parallel such as scaling images, rendering animation frames, ETL and many more.  




## Create a job definition

For reusability it is possible to create JobDefinition resources that serve as a template and can be referenced from JobRuns.
You can create a JobDefinition that contains the static workload configuration and then create multiple JobRuns that refer to this JobDefinition optionally overwriting some of porpoerties specified in the JobDefinition.
