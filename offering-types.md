---


copyright:
  years: 2018, 2019
lastupdated: "2019-01-04"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Third-party offering types
{: #offering-types}

You can deliver your third-party offering as an integrated billing service or a referral service in {{site.data.keyword.Bluemix}}.
{:shortdesc}

Delivering your third-party offering as an integrated billing service means that users can select from different IBM pricing plans that are listed on your catalog details page in the {{site.data.keyword.Bluemix_notm}} console. Additionally, users can automatically create an instance of your third-party offering.

When you deliver your third-party offering as a referral service, users are directed to your website from the catalog details page in the {{site.data.keyword.Bluemix_notm}} console. From your website, users create accounts and get the appropriate credentials. These credentials are needed to programmatically connect your third-party offering to an app they're building on {{site.data.keyword.Bluemix_notm}}.

## Comparing offering types
{: #compare}

The following table provides a detailed comparison of the third-party offering types.

|  | Integrated Billing Service  | Referral Service |
|---|---|---|
| **Onboarding** | Onboarding is handled through the IBM Provider workbench and the resource management console. The offering provider develops an Open Service Broker, hosting it, testing it, and publishing their offering through a series of self-service steps. | Onboarding is handled through the Provider workbench. The self-service onboarding process takes about two weeks. |
| **Deploying** | Created by the {{site.data.keyword.Bluemix_notm}} platform | API-based services only |
| **Billing**  |  In the integrated billing model, the user receives a single bill for both their IBM offering and their integrated third-party offering. | In the referral model, providers' bill the user and keep 100% of the revenue.  |
| **Example** | [PowerAI](https://{DomainName}/catalog/services/powerai){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") | [Accern API](https://{DomainName}/catalog/services/accern-api){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") |
{: caption="Table 1. Comparison of third-party offering types" caption-side="top"}

