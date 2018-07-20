---


copyright:
  years: 2018
lastupdated: "2018-07-20"


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

This topic introduces you to the steps that are required to develop and publish your third-party integrated billing service in {{site.data.keyword.Bluemix}}. 
{:shortdesc}

After you're approved to deliver your offering in the {{site.data.keyword.Bluemix_notm}} catalog, you start developing your offering in the resource management console, a guided UI experience. You design your catalog metadata, set up the service pricing plans, and integrate with {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). 

Next, outside of the resource management console, you perform code development to build and host a new open service broker (starter broker samples and API docs are provided), and you use IAM to develop an authentication flow. After you complete these steps, you return to the resource management console to deploy your service to the catalog in a limited visibility mode that allows you to test and validate multiple deliverable requirements. When you are ready, and your offering meets all requirements, your service becomes fully visible in the {{site.data.keyword.Bluemix_notm}} catalog!


## How the process works
{: #process}

To deliver an integrated billing service, you work with the Provider Workbench, the resource management console, and the development environment of your choice. See the [checklist](/docs/third-party/checklist.html#checklist) to help track these steps.

1. [Create your documentation and marketing announcement](/docs/third-party/cis1-docs-marketing.html).
2. [Define your offering in the resource management console {{site.data.keyword.Bluemix_notm}}](/docs/third-party/cis2-rmc-define.html).
3. [Develop and host your service brokers](/docs/third-party/cis3-broker.html).
4. [Develop an authentication flow](/docs/third-party/cis5-iam.html).
5. [Test your service](/docs/third-party/cis4-rmc-publish.html).
6. [Publicly release your service](/docs/third-party/cis6-ga.html).

These steps assume that you are approved to deliver an integrated billing service. If you haven't completed the initial registration and approval process in the Provider Workbench, see the [getting started tutorial](/docs/third-party/index.md)
{: tip}

## Support
{: #support}

Integrated billing services require third-party offering providers to provide their own support model. Your IBM representative can help to enable your support model and ensure that if a user opens a ticket with {{site.data.keyword.Bluemix_notm}} support, the ticket is routed to the third-party support site.

## Continuous updates
{: #maintain}

After your service is released, you can continue to iterate and make updates by working directly with your {{site.data.keyword.Bluemix_notm}} representative.



