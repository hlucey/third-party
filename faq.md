---

copyright:
  years: 2015, 2019
lastupdated: "2019-01-30"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}
{:faq: data-hd-content-type="faq"}
{:note: .note}

# FAQs
{: #3p-faqs}

## What are the different metering options for plans?
{: #metering}
{: faq}

{{site.data.keyword.Bluemix}} supports multiple models for aggregating offering usage. Offering providers measure various metrics on the provisioned instances and submit those measures to the metering service. The rating service aggregates the submitted usage into different buckets (instance, resource group, and account) based on the model that offering providers choose. The aggregation and rating models for all the metrics in a plan are contained in the metering and rating definition documents for the plan.

You're required to automate hourly usage submission by using the metering service API if you offer a metered plan.
{: note}

For more information on metering, see [Metering integration](/docs/third-party?topic=third-party-meteringintera#meteringintera). For more information about submitting metered usage, see [Submitting usage for metered plans](/docs/third-party?topic=third-party-submitusage#submitusage).

## How can I generate a new {{site.data.keyword.Bluemix_notm}} Identity and Access Management API Key?
{: #iam-creds}
{: faq}

You're given your API Key when you enable IAM. It is critical that you save the API Key. The value is not shown again. If you lose your API Key, you can delete the key and create a new one. For more information, see [Manage service ID API keys](/docs/iam?topic=iam-serviceidapikeys#serviceidapikeys). 


