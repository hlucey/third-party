---

copyright:

years: 2019

lastupdated: "2019-03-20"

keywords: service parameter definition, parameters, parameter example, 

subcollection: third-party
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Service parameter definitions and examples
{: #service_parameters_def_examples}

Service parameters are used to collect and add additional data points to a provisioning call when an IBM Cloud customer creates a service instance. The following sections provide examples and definitions of how service parameters can be used. To start adding custom service parameters for your offering, see [Custom service parameters for third-party](/docs/third-party?topic=third-party-service_parameters3p#service_parameters3p). 

## Service parameter examples 
{: #service_parameters_examples}

The following example illustrates how service parameters can be used to request a required text field:

  ```javascript
  {
    "metadata": {
      //...
      "service": {
        //...
        "parameters": [{
          "associations": {
            "plan": {
              "showFor": [
                "068f8a20-8b27-4049-91fe-a3ff5f505352",
                "45333bd7-79f5-475f-9b14-9fe99734592a"
              ]
            }
          },
          "description": "Subscription ID that will be use when provisioning the service instance",
          "displayname": "Subscription ID",
          "name": "subscription_id",
          "required": true,
          "type": "text"
        }]
      }
    }
  ```

Make changes to the **Service** and all the **Deployment** objects for each service plan that you want to add the parameters to. Based on the earlier example, edit all the deployments for `068f8a20-8b27-4049-91fe-a3ff5f505352` and `45333bd7-79f5-475f-9b14-9fe99734592a`.

Always validate that your changes are displayed when you request the catalog data for your service. For example, navigate to  `https://resource-catalog.stage1.ng.bluemix.net/api/v1/7045626d-55e3-4418-be11-683a26dbc1e5?complete=true` in a browser (where `7045626d-55e3-4418-be11-683a26dbc1e5` is the Watson Assistant service id).
{: important}

## Service parameter definitions
{: #service_parameters_definitions}

* **parameters**

  An array of key-value pairs that are defined by the service when the service instance is created.

  ```javascript
  "parameters": [{
    "name": "nodes",
    "displayname": "Number of Data Nodes"
  }]
  ```

  * **parameters.name**

    The key of the parameter.

  * **parameters.displayname**

    The name of the parameter that is displayed.

  * **parameters.type**

    The type of input field that is displayed by the {{site.data.keyword.Bluemix_notm}} user interface. The value can be text, password, dropdown, check box, or radio.

    **Note**: This value is required.

    ```javascript
    {
      "name": "pwd",
      "displayname": "Password",
      "type": "password"
    },
    ```

  * **parameters.options**

    A JSON structure to specify available values for dropdown, checkbox, and radio input type.

      * **parameters.options.displayname**

        The name of the dropdown, check box, or radio button that you want to display in the UI.

      * **parameters.options.value**

        The value of the parameter to be sent to the service broker when creating the service.

        ```javascript
        "options": [
          {
            "displayname": "HDFS",
            "value": "hdfs"
          },
          {
            "displayname": "YARN",
            "value": "yarn"
          },
        ]
        ```

  * **parameters.value**

    The default value of the parameter. For check box input type, it can be an array of values.

    ```javascript
    ["hfs","yarn"]
    ```

  * **parameters.layout**

    Specifies the layout of check box or radio input types. When unspecified, the default layout is horizontal.

  * **parameters.associations**

    A JSON structure to describe the interactions with price plans and/or other custom parameters

    **Note**: This value is optional, and all subsequent values that are appended to `parameters.associations.<value>` are optional.

    ```javascript
    "type": "text",
    "associations": {
      "plan": {
        "showFor": ["apsMyserviceParametersDemo-entry","apsMyserviceParametersDemo-enterprise"]
      }
    }
    ```

      * **parameters.associations.plan**

        A JSON structure to describe the interaction with price plans.

      * **parameters.associations.plan.showFor**

        An array of price plan IDs. If specified, the parameter is shown in the UI when the corresponding price plan is selected.

      * **parameters.associations.plan.optionsRefresh**

        When specified, the `optionsUrl` is called when the associated price plan is selected.

      * **parameters.associations.parameters**

        An array of JSON describing the interaction with other custom parameters.

        * **parameters.associations.parameters.name**

          The name of the other custom parameter you want to interact with.

          **Note**: Required when `parameters.associations.parameters` is in use.

        * **parameters.associations.parameters.showFor**

          An array of selected values that are associated with the custom parameter you want to interact with. This parameter shows in the UI when one of those values is selected.

        * **parameters.associations.parameters.optionsRefresh**

          When setting to true, the `optionsUrl` is called when the associated parameter value is changed and this parameter is visible in the UI.

  * **parameters.optionsUrl**

    The API that is called by the Bluemix Console to get a list of options for dropdown, check box, or radio input type. The response is a JSON that contains two fields:

      * **options**

        An array of JSON that will return `parameters.options`; for more details see the entry for `parameters.options` above.

      * **value**

        The new default value of the parameter. For more details, see the entry for `parameters.value` above.

    The Bluemix Console passes the ace_config query parameter, which contains the current org GUID, space GUID, the current value of all custom parameters and the current price plan ID. The bearer token is propagated in the header.

  * **parameters.invalidmessage**

    The message that appears when the content of the text box is invalid.

  * **parameters.description**

    The description of the parameter that is displayed to help users with the value of the parameter.

  * **parameters.required**

    A Boolean value that indicates whether the parameter must be entered in the {{site.data.keyword.Bluemix_notm}} user interface.

  * **parameters.pattern**

    Specifies a regular expression that the value is checked against.

  * **parameters.placeholder**

    Specifies a short hint that describes the expected value.

  * **parameters.readonly**

    A Boolean value that indicates whether the value of the parameter is displayed only and cannot be changed by users. The default value is false.

  * **parameters.hidden**

    A Boolean value that indicates whether the key-value pair is hidden from users. The default value is false.