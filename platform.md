---

copyright:

  years: 2018, 2019

lastupdated: "2019-02-25"

keywords: IBM Cloud platform, integrated billing services, lifecycle of IBM Cloud resources, provisioning layer 

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# How integrated billing services use the {{site.data.keyword.Bluemix_notm}} platform
{: #how-it-works}

Integrated billing services are different from referral services. An integrated billing service uses the {{site.data.keyword.Bluemix_notm}} platform for authentication, access, provisioning, metering, and billing. This topic provides a high-level overview of the platform components your integrated billing service uses.

## The {{site.data.keyword.Bluemix_notm}} provisioning layer
{: #provisioning-layer}

The provisioning layer manages the lifecycle of {{site.data.keyword.Bluemix_notm}} resources. The provisioning layer is responsible for controlling and tracking the lifecycle of resources in a customer account. *Resources* are physical or logical components that can be provisioned or reserved for an application or service instance. Examples of resources include database, accounts, processor, memory, and storage limits. In general, resources that are tracked by the provisioning layer are intended to associate usage metrics and billing, but that isn’t always the case. In some cases, the resource might be associated to the provisioning layer to ensure that the resource lifecycle can be managed along with the account lifecycle.

### Resource lifecycle management
{: #lifecycle}

The provisioning layer provides common APIs to control the lifecycle of resources from provisioning (creating an instance) to binding (creating access credentials) to unbinding (removing access) to de-provisioning (deleting an instance). Additionally, the {{site.data.keyword.Bluemix_notm}} platform provides CLIs and a UI that can manage the lifecycle of these resources that don’t require you to create your own facilities.

The provisioning layer provides APIs to help you manage the following elements of your resource lifecycle:
* Provisioning
* Updating a resource instance
* Binding
* Resource keys
* Unbinding
* De-provisioning

## {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM)
{: #iam}

Identity Access Management (IAM) enables you to securely authenticate users and control access to all cloud resources consistently across {{site.data.keyword.Bluemix_notm}}. The {{site.data.keyword.Bluemix_notm}} provisioning layer adopted IAM for authentication and authorization of actions that are taken against the provisioning layer. Third-party offering providers use IAM to create an authentication flow (OAuth). For more information, see [What is IAM](/docs/iam?topic=iam-iamoverview#iamoverview)?

If your offering uses OpenID Connect (OIDC) libraries, IAM supports OIDC integration. OIDC is an authentication layer on top of OAuth 2.0, an authorization framework and can help simplify the onboarding process. For more information on OIDC, see [Open ID Connect](http://openid.net/connect/){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").

## {{site.data.keyword.Bluemix_notm}} catalog
{: #catalog}

The {{site.data.keyword.Bluemix_notm}} catalog stores the offering definitions (description, features, images, URLs, and so on) of the resources that are displayed in the {{site.data.keyword.Bluemix_notm}} console. The resource management console is used to define all aspects of your service's required metadata. This metadata is published to the catalog and used for display in the catalog. You can find detailed information about required and optional metadata fields in the **Offering** and **Plan** pages in the resource management console. Key items are included here to jumpstart your understanding.

   * Service Name: technical name for your service. The service name is critical and must be correctly defined. You must provide both a service name that is used to identify the service by the {{site.data.keyword.Bluemix_notm}} platform, and a display name that your customers see in the {{site.data.keyword.Bluemix_notm}} catalog. The service name isn't your display name.
   * Service Display Name: user-friendly name for your service. For example, "Compose Redis"
   * Service ID: GUID for your service that is used in API calls to your OSB broker. This value must be unique.
   * Service Icon: SVG with your service logo
   * Service Description: The description of the resource that is displayed when you hover over the resource icon in the {{site.data.keyword.Bluemix_notm}} catalog user interface. You can add a single sentence or phrase for the description.
   * Service Detailed Description: The first paragraph that appears in the catalog listing page. Consider at least two sentences for a detailed description.
   * Documentation URL: A link to your {{site.data.keyword.Bluemix_notm}} documentation. You’ll author in PWB, and your url value is generated by PWB for you.
   * Terms URL: A link to your service's terms and conditions for usage. Note that for GDPR purposes, don’t link to your existing third-party service's terms and conditions. Instead, you must provide a unique page for an integrated billing service.
   * Instructions URL: Similar to Documentation URL, you’ll point to your {{site.data.keyword.Bluemix_notm}} documentation; however, the Instructions URL dynamically pulls your documentation into a Getting Started tab in your service's dashboard.
   * Category: Selection of available {{site.data.keyword.Bluemix_notm}} categories where your service is placed in the catalog.
   * Bullets: Short descriptive sparklers about your service
   * Media: Screen captures and videos about your service
   * Service Plan Name: Each plan has a technical name. All lowercase, no spaces, can include "-". For example, `gold`.
   * Service Plan Display Name: User-friendly name for the plan. For example, `Gold`
   * Service Plan ID: GUID for your service plan that is used in API calls to your OSB broker. This value must be unique. Resource management console generates this value for you.
   * Service Plan Description: The description of the resource plan. The description is displayed after you select a plan on the resource details page in the IBM Cloud catalog
   * Service Plan Bullets: short descriptive sparklers about your service plan


## Open Service Broker
{: #open-service}

Service Brokers manage the lifecycle of services. The {{site.data.keyword.Bluemix_notm}} platform interacts with Service Brokers to provision and manage Service Instances (an instantiation of a Service Offering) and Service Bindings (the representation of an association between an Application and a Service Instance, which often include the credentials that the Application uses to communicate with the Service Instance). Providing valid metadata values create a successful REST API Response when a Request is performed.

{{site.data.keyword.Bluemix_notm}} uses the Open Service Broker API (OSB) `version 2.12` specification. Read through and familiarize yourself with the [Open Broker API spec](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon"), and use the readme file as a guide to learn more.

When the resource controller receives a request to provision a resource, it calls your OSB to validate the service type, offering, plans, and regions availability. The resource controller also validates the visibility of the plan that is associated with the customer account. {{site.data.keyword.Bluemix_notm}} provides broker samples and API docs that extends the OSB spec. You can find more details about developing and hosting your broker as you walk through the detailed integrated billing onboarding development steps.

## {{site.data.keyword.Bluemix_notm}} Metering service
{: #metering-service}

If a service offers a metered plan, {{site.data.keyword.Bluemix_notm}} users are charged based on the amount of resources that they use. For example, {{site.data.keyword.Bluemix_notm}} users that use database services might be charged based on the amount of storage that their applications use. Usage submission must occur in order for the usage to be converted into a chargeable record.

All integrated billing services that offer a metered plan must use the {{site.data.keyword.Bluemix_notm}} metering service to report usage data.

You’re required to automate hourly usage submission by using metering service API if you offer a metered plan.

For more information on metering, see: [Metering integration](/docs/third-party?topic=third-party-meteringintera#meteringintera). For more information on submitting metered usage, see: [Submitting usage for metered plans](/docs/third-party?topic=third-party-submitusage#submitusage).

## Provisioning scenario: Pulling it all together
{: #provision2}

Now let's pull all of the concepts together and look at an example of how service instance creation works by using the {{site.data.keyword.Bluemix_notm}} platform.

![Provisioning scenario](images/flow-am.svg "How the platform handles service instance creation")

When a user wants to create a service instance, they can create it in one of two ways:
* **CLI**: Using `ibmcloud cli [ ibmcloud resource service-instance-create NAME SERVICE_NAME SERVICE_PLAN_NAME LOCATION ]`
* **{{site.data.keyword.Bluemix_notm}} console**: The user can select the service, plan, and use the **Create** operation.

The {{site.data.keyword.Bluemix_notm}} platform validates that the user has permission to create the service instance by using {{site.data.keyword.Bluemix_notm}} IAM. After this validation occurs, your service broker's provision endpoint (PUT /v2/resource_instances/:resource_instance_id) is started. When provisioning occurs, the following rules must be met:
* The {{site.data.keyword.Bluemix_notm}} context is included in the context variable
* The `X-Broker-API-Originating-Identity` has the IBM IAM ID of the user that started the request
* The parameters section includes the requested location (and more parameters that are required by your service).

Example provision request:

```
    PUT /v2/service_instances/crn%3Av1%3Abluemix%3Apublic%3Acompose-redis%3Aus-south%3Aa%2F46aa677e-e83f-4d17-a2b6-5b752564477c%3A416d769b-682d-4833-8bd7-5ef8778e5b52?accepts_incomplete=true HTTP/1.1
    Host:  https://broker.compose.cloud.ibm.com
    Authorization: basic dXNlcjpwYXNzd29yZA==
    X-Broker-Api-Version: 2.12
    X-Broker-API-Originating-Identity: ibmcloud aWJtaWQtNDU2MzQ1WA==
    {
      "service_id": "0bc9d744-6f8c-4821-9648-2278bf6925bb", // your service's GUID from onboarding
      "plan_id": "ecc19311-aba2-49f7-8198-1e450c8460d4", //your plan's GUID from onboarding
      "context": {
        "platform": "ibmcloud",
        "account_id": "003e9bc3993aec710d30a5a719e57a80",
        "crn": "crn:v1:bluemix:public:compose-redis:us-south:a/003e9bc3993aec710d30a5a719e57a80:416d769b-682d-4833-8bd7-5ef8778e5b52",
        "resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/003e9bc3993aec710d30a5a719e57a80::resource-group:b4570a825f7f4d57aa54e8e1d9507926",
        "target_crn": "crn:v1:bluemix:public:resource-catalog::a/e97a8c01ac694e308ef3ad7795c7cdb3::deployment:e62e2c19-0c3b-41e3-b8b3-c71762ecd489:us-south38399"
      },
      "parameters": {
        "location": "us-south",
        "optional-param":"parameter required by your service"
      }
    }
```

### Understanding the {{site.data.keyword.Bluemix_notm}} `context` parameter
{: #parameter}

In the previous example, you can see the metadata returned in the `context` parameter. The provision context for {{site.data.keyword.Bluemix_notm}} returns the following:

* **platform**: Identifies the platform as "ibmcloud"

* **"account_id"**: Returns the ID of the account in {{site.data.keyword.Bluemix_notm}} that is provisioning the service instance.

* **crn**: When a customer provisions your service in {{site.data.keyword.Bluemix_notm}}, a service instance is created and this instance is identified by its {{site.data.keyword.Bluemix_notm}} Resource Name (CRN). The CRN is used in all aspects of the interaction with {{site.data.keyword.Bluemix_notm}} including provisioning, binding (creating credentials and endpoints), metering, dashboard display, and access control. From an offering provider perspective, the CRN can largely be treated as an opaque string to be used with the {{site.data.keyword.Bluemix_notm}} APIs. It can also be decomposed by using the following structure:

   ```
   crn:version:cname:ctype:service-name:location:scope:service-instance:resource-type:resource
   ```

   In the provisioning sample we see that the `compose-redis` service CRN is:

   ```
   crn:v1:bluemix:public:compose-redis:us-south:a/46aa677e-e83f-4d17-a2b6-5b752564477c:416d769b-682d-4833-8bd7-5ef8778e5b52::
   ```

   In this sample, this `compose-redis` instance is part of {{site.data.keyword.Bluemix_notm}} account with ID. The unique ID for the instance is `416d769b-682d-4833-8bd7-5ef8778e5b52`, and the instance is hosted in the `us-south` region of the public {{site.data.keyword.Bluemix_notm}}.

* **resource_group_crn**: Returns the resource group that includes the service instance. For more details, see [Managing resource groups](/docs/resources?topic=resources-rgs#rgs).

   Offering providers aren't concerned with the `resource_group_crn` except in unique circumstances. Consult your IBM representative on your use case before you use that field.
   {: note}

