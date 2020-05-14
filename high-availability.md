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
{:gif: data-image-type='gif'}

# Knative service high availability
{: #kn-ha}

**High-level overview of HA.  How do we ensure high availability for the services/ jobs that run on here?  What can you do in addition to make deployments highly available?** 

All Coligo general availability (GA) services have a Service Level Agreement of 99.99% availability. Coligo is a GA service that is offered in **five regions: US South, US East, Germany, Tokyo, and United Kingdom**. Each location has three different data centers for redundancy. The data for each location is kept in the three data centers near that location. If all the data centers in a location fail, the Coligo service for that location becomes unavailable.

Coligo is available only on the public cloud, but the tools that are used with Coligo can run in dedicated or public cloud environments and in on-premises environments. 

See [ensure zero downtime](/docs/overview?topic=overview-zero-downtime#zero-downtime) to learn more about the high availability and disaster recovery standards in {{site.data.keyword.cloud_notm}}. You can also find information about [Service Level Agreements](/docs/overview?topic=overview-slas). 

