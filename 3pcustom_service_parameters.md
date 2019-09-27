---

copyright:

  years: 2019

lastupdated: "2019-09-27"

keywords: Custom service parameters, parameters, RMC, service 

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}
{:note: .note}
# Using custom service parameters
{: #service_parameters3p}

You can use service parameters to collect and add additional data points to a provisioning call when an {{site.data.keyword.Bluemix}} customer creates a service instance. The data is passed onto the service providers service broker and is used in the provisioning action that is executed by the service provider. This action supports additional preferences and configures which specific service a customer should select. 

As you start working with custom service parameters, see [Service parameter definitions and examples](/docs/third-party?topic=third-party-3p_parameter_example#service_parameters_def_examples). 

## Adding custom service parameters to your offering 

As a third-party provider, you have the option to add custom service parameters to your offering:

1. Log in to the [staging console](https://console.test.cloud.ibm.com). 
2. Go to the [RMC dashboard](https://console.test.cloud.ibm.com/onboarding/dashboard), and click the **Offering** tab. 
3. Enter a valid JSON in the **Customer Service Parameter** input field. 
The custom service parameters are published onto the Global Catalog deployment object when you are publishing a deployment for a plan. 
{: note}

After you add custom service parameters, you can go to the console page for the service to review the parameters as you create a plan.

To publish a deployment for a plan, complete the following steps: 
1. Go the [RMC dashboard](https://console.test.cloud.ibm.com/onboarding/dashboard), and click the **Deployment** tab.
2. Click **Catalog Deployments** &gt; **Add Deployment**. 
3. Select a plan to configure and click **Add**. 
4. You can edit custom service parameters in the deployment JSON. To edit the deployment JSON, click **Catalog Deployments** and select **Edit JSON**.

## Using service parameters to create customized input fields 
{: #parameters_input}

You can use service parameters to create customized input fields in the {{site.data.keyword.Bluemix_notm}} service creation user interface. The values that are entered by the user are sent to your service broker on the request to provision the service. The `parameters` attribute can be added as an array to your JSON, you can create custom input fields of the following types: text, password, dropdown, checkbox, or radio. The `parameters` attribute should be added within the `metadata.service` entry under the JSON response of `GET <resource-catalog>/api/v1/<service-id>?complete=true`.

If a parameter is set to required, the `parameters.options.value` cannot be an empty string because it violates the parameter validation.

`userDefinedService` is deprecated. Previously, when provisioning a service, custom service parameters can be added to your JSON by nesting them within the `userDefinedService` entry. Do not add these parameters under `userDefinedService`; instead, add them directly under `metadata`.
{: deprecated}

## Adding service parameters to translated metadata
{: #service_parameters_translation}

To specify custom service parameters in translated metadata, the i18n version should be placed in the `metadata.i18n.<lang>.parameters` attribute.
