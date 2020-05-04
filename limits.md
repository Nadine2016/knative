---

copyright:
  years: 2020
lastupdated: "2020-05-04"

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

# Limits
{: #kn-limits}

The following sections provide technical details about the Coligo limit settings. 
{: shortdesc}

## Experimental limitations
{: #kn-limits_experimental}

During the experimental release of Project Coligo, be aware of the following limitations:

- One project per location
- Three projects per account

## Application limits
{: #kn-limits_application}

The following table lists the limits for Applications.

| Category  |   Default   |   Maximum  |  Minimum  |
| --------- | ----------- | ---------- | --------- |
| CPU       |         0.1 |          8 |      0.01 |
| Max scale |          10 |        250 |         0 |
| Memory    |         1 G |       32 G |     128 M |
| Min scale |           0 |        250 |         0 |
| Parallel  |          10 |       1000 |         0 |
| Timeout   | 300 seconds | 600 seconds|         0 |
{: caption="Application limits"}

<br />

## Job limits
{: #kn-limits_job}

The following table lists the limits for jobs. 

| Category    |         Default         |         Maximum           |  Minimum  |
| ----------- | ----------------------- | ------------------------- | --------- |
| Array size  |                       5 |                       250 |         1 |
| CPU         |                       1 |                         8 |         1 |
| Memory      |                      1G |                       32G |      128M |
| Retries     |                       2 |                         5 |         0 |
| Timeout     | 300 seconds (5 minutes) |  86400 seconds (24 hours) |         0 |
{: caption="Job limits"}
