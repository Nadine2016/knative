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
{:preview: .preview}

# Updating Knative services 
{: #kn-update}

You can update your Knative apps with the `kn service update` command. For help, add the `-h` flag or see the [`kn service update` reference.](https://github.com/knative/client/blob/master/docs/cmd/kn_service_update.md){: external}

```
kn service update <service_name> --env <env_name>=<env_value>
```
{: pre}
