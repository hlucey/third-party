---

copyright:
  years: 2015, 2018
lastupdated: "2018-03-15"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# FAQs
{: #3p-faqs}

See the following Frequently Asked Questions for clarification on commonly asked questions.

## What are the different metering options for plans?
{: #metering}

{{site.data.keyword.Bluemix}} supports multiple models for aggregating offering usage. Offering providers measure various metrics on the provisioned instances and submit those measures to the metering service. The rating service aggregates the submitted usage into different buckets (instance, resource group, and account) based on the model that offering providers choose. The aggregation and rating models for all the metrics in a plan are contained in the metering and rating definition documents for the plan.

**Note:** You are required to automate hourly usage submission using metering service API if you offer a metered plan.

For more information on metering see: [Metering integration](/docs/third-party/metering.html#meteringintera).

For more information submitting metered usage see: [Submitting usage for metered plans](/docs/third-party/submitusage.html#submitusage)

## I lost my {{site.data.keyword.Bluemix_notm}} Identity and Access Management API Key. How can I generate another?
{: #iam-creds}

You are given your API Key when you **Enable IAM**. It is critical that you save the API Key. The value is not shown again. If you lose your API Key, you can delete the key and create a new one: [Manage service ID API keys](/docs/iam/serviceid_keys.html#serviceidapikeys)


