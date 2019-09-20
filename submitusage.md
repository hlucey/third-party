---

 
copyright:

  years: 2017, 2019

lastupdated: "2019-08-20" 

keywords: plans of the resource, use characters A, usage records, metered plans, submitting usage 

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Submitting usage for metered plans
{: #submitusage}

You're required to submit usage for all active service instances every hour. Not reporting usage can lead to the loss of revenue collection for IBM, which can cause a loss of revenue share for offering providers.
{:shortdesc}

## How the process works
{: #process-flow}

The following steps outline the process for submitting usage:

1. Submit an initial usage test through the Usage Submission REST API tool to validate that your metered plans are correctly configured.
2. Automate continuous hourly submission to the Usage Submission Rest API tool for each metered plan. You can host these automated submissions wherever you want as long as standard SSO is supported.
3. The usage records are aggregated based on the metering model, and the total quantity is displayed on the Usage Dashboard in the {{site.data.keyword.Bluemix_notm}} console.
4. The aggregated unit quantity from the metering process is used, the cost is applied, and the amount that the user owes for the service instance is calculated.
5. At the end of the month, the final calculated cost is the amount that is generated for the user.

## Prerequisites
{: #prereqs}

Review the following prerequisites for enabling metering for your service:

* The pricing catalog is updated with prices for all chargeable metrics in the plans of the resource.
* Metering and rating definitions for all the plans in the resource are verified and onboarded.

## Guidelines for submitting usage 
{: #metering_guidelines}

### Submission guidelines
{: #submission-guidelines}

Refer to the following guidelines when you use the {{site.data.keyword.Bluemix_notm}} metering service to submit resource usage data:

* The start time and end time represent the time range during which the measures were collected. The times aren't dependent on the time at which the usage record is submitted to the metering APIs.
* Usage records are facts. Don't update the usage record after you create it. A location is specified when you successfully create a usage record. If an error code is returned, see the [Status codes and required actions](/docs/third-party?topic=third-party-submitusage#usage-records) that you might have to take.
* A usage record is uniquely identified by the signature `account_id/resource_group_id/resource_instance_id/consumer_id/plan_id/region/start/end`. When a usage record is processed, any other usage record with the same signature is rejected as a duplicate.
* Don't combine the interaction with the metering service with any other services. The requests must be handled individually even if the metering starts and ends with provisioning and de-provisioning of the instance.
* The resource usage data must be submitted to the metering service once every 2 - 24 hours. How often you submit your usage data depends on how often your usage metrics change.
* Usage records must be submitted within two days from the time at which the measurement was completed. Older usage records are rejected.
* A successful submission returns a response code of 201. If any other response code is returned, update and resend the data until you receive the 201 code.

The following are best practices for submitting usage:

* It's recommended that service providers submit usage every 1 hour so that the user doesn't see a huge delay from the time that the resource was consumed and time at which the cost is reflected in their accounts.
* Retry submission of usage records only if a genuine failure with the previous request occurs. Don't resubmit usage records that were successfully accepted.

### Service ID guidelines
{: #id-guidelines}

  You must follow these guidelines when you specify the service ID by using the ID field in the resource definition:
  * Start the ID with an alphanumeric character.
  * Use characters A - Z, a - z, and 0 - 9. The only special characters that you can use are hyphens (-) and underscores (_).
  * Follow the camel case convention if the ID contains more than one word.
  * Ensure that the maximum length of the ID is 50 characters.

### Resource name guidelines
{: #resource-name}

  You must follow these guidelines when you specify the resource name by using the resources.name field in the resource definition:

  * Use only words that describe your resources. For example, **Storage** or **ApiCalls**. 
  * Follow the camel case convention if the name contains more than one word.
  * Capitalize the first character of the name.

### Resource unit name guidelines
{: #resource-unti}

  You must follow these guidelines when you specify the resource unit name by using the resources.unit.name field in the resource definition:

  * Use one word for the unit name, and use an underscore (_), instead of a space, to separate words. For example, specify **API_CALL** instead of **API CALL**.  
  * Capitalize all letters of the name.
  
### Resource unit quantity guidelines
{: #unit-quantity}

  You must follow these guidelines when you specify the resource quantity type by using the resources.unit.quantityType field in the resource definition:
  
  * Use one word for the quantity type.
  * Capitalize all letters of the quantity type.
  
### Aggregation ID guidelines
{: #aggregation}

  You must follow these guidelines when you specify the aggregation ID by using the aggregations.id field in the resource definition:

  * Capitalize all letters of the quantity type.
  * Use an underscore (_), instead of a space, to separate words.
  * Ensure that this ID starts with or matches with the value of aggregations.unit. For example, you can specify **API_CALLS_PER_MONTH** for aggregations.id and specify **API_CALLS** for aggregations.unit.

### Aggregation unit guidelines
{: #aggregation-unit}

  You must follow these guidelines when you specify the aggregation unit by using the aggregations.unit field in the resource definition:
   
  * Use singular form for the unit name.
  * Capitalize all letters of the unit name.
  * Ensure that the unit name that you specify in the aggregations.unit field is an aggregate of the unit name that you specify in the resources.unit.name field.
  
### Aggregation group guidelines
{: #aggregation-group}

  You must use lowercase letters for the aggregations.aggregationGroup field in the resource definition.
  
### Aggregation formula guidelines
{: #aggregation-formula}

  For the aggregations.formula field in the resource definition, if you want to use arithmetic operations in the formula, you must use the resource unit as one operand and use an infix arithmetic expression in the function of the formula. For example, you can use the following formula to convert Bytes to Megabytes:
  ```
  SUM({BYTE}/1048576)
  ```

## Usage submission REST API
{: #RAPIusesubmit}

{{site.data.keyword.Bluemix_notm}} users are charged based on the amount of resources that they use. For example, users that use database services might be charged based on the amount of storage that their applications use.

To use the {{site.data.keyword.Bluemix_notm}} metering service to report usage data, implement the metering service API to report usage data of your offering. See the [public API documentation](https://cloud.ibm.com/apidocs/usage-metering){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") for more details.  

You're required to automate hourly usage submission by using the metering service API. You can host your automated submission on any valid HTTPs endpoint that is accessible on the public internet.
{: tip}

## Submitting usage records
{: #usage-records}

Usage records are the smallest entities that contribute to the aggregated values of the metrics. The following table provides information about the fields that are used to construct a usage record:

| Name | Description                                           |
| ------ | ---------------------------------------------------- |
| resource_instance_id |  The ID of the resource instance.  |
| plan_id | The contract by which the usage record is aggregated and rated.   |
| start  | Time from which the usage is measured, specified in milliseconds since epoch.  |
| end  | Time to which the usage is measured, specified in milliseconds since epoch.  |
| region  | The offering provider region in which the usage is measured.  |
| measured_usage  | An array of measures with values.  |
| consumer_id | Optional. This field is required only if aggregation is required at a consumer level. Only offering providers know the consumer_id value. |
{: caption="Table 1. Fields of a usage record" caption-side="top"}

You can submit multiple usage records by using API call, and you can submit a maximum of 100 usage records per call. The response body includes the acceptance status of every usage record. Any status other than 201 is accompanied with an error code and indicates why the usage record isn't accepted. The following table lists the status codes and the required action.

| Status Code | Required Action                                       |
| ------ | ---------------------------------------------------- |
| 500 |  Try submitting the usage record again. If the problem continues, contact the BSS metering team. |
| 400 |  The usage record isn't in the correct format. Either the schema validation has failed, the measures in the usage records are incorrect, or the start and end times don't fall between the provisioned and de-provisioned times. Update the usage record and submit it again.   |
| 424  | The resource instance metadata has some issues. Update the resource instance details and submit the usage record again.  |
| 404  | The metering definition wasn't onboarded. Work with the BSS metering team to check whether the resource is onboarded and submit the usage record again.  |
| 409  | The usage record is a duplicate. Don't try submitting it again. |
{: caption="Table 2. Status codes and required actions" caption-side="top"}
{: #actions}


  
