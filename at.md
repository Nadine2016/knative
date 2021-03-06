---

copyright:
  years: 2020
lastupdated: "2020-04-13"

keywords: knative, activity tracker for knative, LogDNA for knative, knative events, knative security, audit logs for knative, viewing knative events, knative events

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

# Auditing events for Coligo 
{: #at_events}

As a security officer, auditor, or manager, you can use the Activity Tracker service to track how users and applications interact with the Coligo service in {{site.data.keyword.cloud}}.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see the [getting started tutorial for {{site.data.keyword.at_full_notm}}](/docs/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).







## List of management events
{: #at_actions}



| Action             | Description      | 
|--------------------|------------------|
| kms.secrets.create | Create a key     | 
{: caption="Table 1. Actions that generate management events" caption-side="top"}

## List of data events
{: #at_actions_data}



| Action                           | Description                        | 
|----------------------------------|------------------------------------|
| cloud-object-storage.object.list | List the objects in the bucket     | 
{: caption="Table 2. Actions that generate data events" caption-side="top"}






## Events for component X
{: #at_actions_x}

| Action                           | Description                        | 
|----------------------------------|------------------------------------|
|                                  |                                    |
{: caption="Table 1. Lists of management events" caption-side="top"}
{: #{componentX}-table-1}
{: tab-title="Management events"}
{: tab-group="{componentX}"}
{: class="simple-tab-table"}
{: row-headers}

| Action                           | Description                        | 
|----------------------------------|------------------------------------|
|                                  |                                    |
{: caption="Table 2. Lists of data events" caption-side="top"}
{: #{componentX}-table-2}
{: tab-title="Data events"}
{: tab-group="{componentX}"}
{: class="simple-tab-table"}
{: row-headers}

## Events for component Y
{: #at_actions_x}

| Action                           | Description                        | 
|----------------------------------|------------------------------------|
|                                  |                                    |
{: caption="Table 1. Lists of management events" caption-side="top"}
{: #{componentY}-table-1}
{: tab-title="Management events"}
{: tab-group="{componentY}"}
{: class="simple-tab-table"}
{: row-headers}

| Action                           | Description                        | 
|----------------------------------|------------------------------------|
|                                  |                                    |
{: caption="Table 2. Lists of data events" caption-side="top"}
{: #{componentY}-table-2}
{: tab-title="Data events"}
{: tab-group="{componentY}"}
{: class="simple-tab-table"}
{: row-headers}


## Viewing events
{: #at_ui}

 



Events are available in the **Frankfurt** location. 

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_full_notm}} service in the `eu-de` location. For more information, see [Launching the web UI through the IBM Cloud UI](/docs/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2).




Events that are generated by an instance of the _YourServiceName_ service are automatically forwarded to the {{site.data.keyword.at_full_notm}} service instance that is available in the same location.

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_full_notm}} service in the same location where your service instance is available. For more information, see [Launching the web UI through the IBM Cloud UI](/docs/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2).


## Analyzing events
{: #at_events_iam_analyze}



