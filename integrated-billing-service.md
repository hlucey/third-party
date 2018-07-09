---


copyright:
  years: 2018
lastupdated: "2018-06-28"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Overview: Developing an integrated billing service
{: #overview}

This topic is designed to guide you through the steps that are required to develop and publish your third-party Integrated Billing service in {{site.data.keyword.Bluemix_notm}}. After you are approved to deliver your offering in the {{site.data.keyword.Bluemix_notm}} catalog, you will start developing your offering in the resource management console (resource management console), a guided UI experience. Within the resource management console you will be designing your catalog metadata, setting up the service pricing plan(s), and integrating with IBM Cloud Access Management (IAM). Next, outside of resource management console, you'll perform code development to build and host a new open service broker (starter broker samples and API docs will be provided), and you will use IAM to develop an authentication flow. After these steps are complete, you will return to the resource management console to deploy your service into the catalog in a limited visibility mode that allows you to test and validate multiple deliverable requirements. When you are ready, and your offering meets all requirements, your service will become fully visible in the {{site.data.keyword.Bluemix_notm}} catalog!


## What do I need to do to deliver an Integrated Billing service?

You will be working through PWB, resource management console, and the development environment of your choice to deliver these objectives. See the [checklist](/docs/third-party/checklist.html#checklist) to help track these steps.

The following steps summarize the onboarding process at a high level:

These steps assume that you are approved to deliver an Integrated Billing service. If you haven't completed the initial registration and approval in PWB, see: [Getting started publishing your third-party offering in {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.md)
{: tip}

1. [Author: Author service docs and marketing announcement (PWB)](/docs/third-party/cis1-docs-marketing.html)
2. [Define: Define your offering in the resource management console {{site.data.keyword.Bluemix_notm}}](/docs/third-party/cis2-rmc-define.html)
3. [Develop: Develop and host one or more service brokers by using the Open Service Broker API specification](/docs/third-party/cis3-broker.html)
4. [IAM: Develop an authentication flow (OAuth), validate user authorization (v2/authz), and derive your redirect URI](/docs/third-party/cis5-iam.html)
5. [Publish and Test: Connect your OSB to the resource management console, publish your service in limited visibility mode to the {{site.data.keyword.Bluemix_notm}} catalog, and test your offering](/docs/third-party/cis4-rmc-publish.html).
6. [Ask for approval to GA your service](/docs/third-party/cis6-ga.html)

## Support

Integrated billing services require thrid-party service providers to provide their own support model.  Your IBM representative will help to enable your support model and ensure that if a user opens a ticket with {{site.data.keyword.Bluemix_notm}} support, {{site.data.keyword.Bluemix_notm}} support will route the ticket to the third party support site.

## Continuous updates

After your service is released, you can continue to iterate and make updates by working directly with your {{site.data.keyword.Bluemix_notm}} representative.



