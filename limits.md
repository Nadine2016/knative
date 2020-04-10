---

copyright:
  years: 2017, 2019
lastupdated: "2019-10-21"

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

# Limits
{: #kn-limits}

The following sections provide technical details about the Coligo limit settings. 

{: shortdesc}

## Application limits
{: #kn-limits_application}

The following table lists the limits for Applications.

| Category  |   Default   |   Maximum  |  Minimum  |
| --------- | ----------- | ---------- | --------- |
| CPU       |         0.1 |          8 |       .01 |
| Max scale |          10 |        250 |         0 |
| Memory    |          1G |        32G |      128M |
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
