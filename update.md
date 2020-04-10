---

copyright:
  years: 2014, 2019
lastupdated: "2019-10-21"

keywords: knative

subcollection: functions

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Updating Knative services 
{: #kn-update}

You can update your Knative apps with the `kn service update` command. For help, add the `-h` flag or see the [`kn service update` reference.](https://github.com/knative/client/blob/master/docs/cmd/kn_service_update.md){: external}

```
kn service update <service_name> --env <env_name>=<env_value>
```
{: pre}
