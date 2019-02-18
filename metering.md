---


copyright:

  years: 2017, 2019

lastupdated: "2019-01-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}

# Metering integration
{: #meteringintera}

{{site.data.keyword.Bluemix}} supports multiple models for aggregating offering usage. Offering providers measure various metrics on the provisioned instances and submit those measures to the metering service. The rating service aggregates the submitted usage into different buckets (instance, resource group, and account) based on the model that offering providers choose. The aggregation and rating models for all the metrics in a plan are contained in the metering and rating definition documents for the plan.
{:shortdesc}

The following list describes the expectations for tracking and submitting usage:

*	Third-party offering providers don't need to submit usage for free plans.
*	Third-party offering providers don't need to submit usage for monthly subscription plans.
*	For metered plans, all offering providers must submit usage hourly (Lite plans must submit every 15 minutes to 1 hour).
*	The offering provider is responsible for automating usage submission, including automation that tries failure responses again. {{site.data.keyword.Bluemix_notm}} doesn't provide a retry function for failed submissions. For more information, see the status codes and actions table in [Submitting usage records](/docs/third-party?topic=third-party-submitusage#usage-records).
*	Usage records for the current month must be submitted, at the latest, by the 2nd of the following month.
*	{{site.data.keyword.Bluemix_notm}} is configured for a monthly billing cycle and time is represented in Coordinated Universal Time (UTC).
*  Offering providers must test usage submission and validate their results to inform how the monthly billing cycle is calculated.

For general information about pricing, see [How to calculate your costs](/docs/billing-usage?topic=billing-usage-cost#cost). 

## Configuration properties
{: #configure}

The following properties define how usage submissions for offering plans are metered and rated:

<dl>
<dt>Unit</dt>
<dd>Metrics to be metered, for example, ApiCall, Bytes, Hours, Instances, and Nodes.</dd>
<dt>Aggregation</dt>
<dd>How metered unit data is compiled, for example INSTANCES_BY_MONTH, or ACTIVE_HOURS_BY_MONTH.</dd>
<dt>Metering model</dt>
<dd>How usage submission data is processed, as shown in the following table.</dd>
<dt>Resource name</dt>
<dd>The name of the resource that is being measured, for example, storage, instance, virtual server, or bytes transmitted.</dd>
<dt>Unit name</dt>
<dd>The descriptive name of the unit if the default name isn't relevant for the offering.</dd>
</dl>

## Metering model types
{: #metermodel}

The following table shows the available metering models.

|  Type | Description  |
|-----|-----|
| standard_add | Add quantity from all submitted usage records for a month. | 
| standard_max  | Maximum quantity from all submitted usage records for a month. | 
| standard_avg | Average quantity from all submitted usage records for a month. |
| dailyproration_max | Calculated daily maximum. Sum up all the days for the month. | 
| dailyproration_avg | Calculated daily average. Sum up all the days for the month. |
| monthlyproration | Calculated similar to the daily proration, but the price that is used is the plan price that is divided by the total number of days for the month (daily price). |
{: caption="Table 1. Metering model" caption-side="top"}

### Examples
{: #examples}

Note that the quantity in the dashboard in each of the following examples is before the next usage is submitted but after the current usage is processed.

#### Standard Add
{: #standard-add}

Calculate the usages for the entire month.

Formula: ADD(usages)

| Time            | Usage Sent In | Calculation | Quantity in Dashboard |
|-----------------|:-------------:| ----------- |:---------------------:|
| Day 1 (morning) | 5             | 5           | 5                     |
| Day 1 (night)   | 5             | 5 + 5       | 10                    |
| Day 2 (morning) | 5             | 10 + 5      | 15                    |
| Day 3 (morning) | 5             | 15 + 5      | 20                    |
| Day 4 (night)   | 5             | 20 + 5      | 25                    |
{: caption="Table 2. Monthly usage calculations" caption-side="top"}

#### Standard Average
{: #standard-average}

Calculate the average of the usages for the entire month. Note that submitting a zero usage also counts toward the average.

Formula: AVG(usages)

| Time            | Usage Sent In | Calculation             | Quantity in Dashboard |
|-----------------|:-------------:| ----------------------- |:---------------------:|
| Day 1 (morning) | 4             | 4 / 1                   | 4                     |
| Day 1 (night)   | 0             | (4 + 0) / 2             | 2                     |
| Day 2 (morning) | 5             | (4 + 0 + 5) / 3         | 3                     |
| Day 3 (morning) | 3             | (4 + 0 + 5 + 3) / 4     | 3                     |
| Day 4 (night)   | 3             | (4 + 0 + 5 + 3 + 3) / 5 | 3                     |
{: caption="Table 3. Average monthly usage calculations" caption-side="top"}

#### Standard Max
{: #standard-max}

Calculate the maximum of the usages for the entire month.

Formula: MAX(usages)

| Time            | Usage Sent In  | Calculation  | Quantity in Dashboard |
|-----------------|:--------------:| ------------ |:---------------------:|
| Day 1 (morning) | 5              | MAX(5)       | 5                     |
| Day 1 (night)   | 10             | MAX(5, 10)   | 10                    |
| Day 2 (morning) | 0              | MAX(10, 0)   | 10                    |
| Day 3 (morning) | 15             | MAX(10, 15)  | 15                    |
| Day 4 (night)   | 1              | MAX(15, 1)   | 15                    |
{: caption="Table 4. Maximum monthly usage calculations" caption-side="top"}

#### Daily proration Average
{: #proration-average}

Calculate the average usage for each day and average it for the month. The average of each day is added up and divided by the number of days currently passed (in UTC).

Formula: Summation(daily average) / Number of days passed in billing period

Note that the quantity might change throughout the month, but what is rated is the average usage per day.

Given a 30-day month:

| Time               | Usage Sent In    | Daily Average | Calculation                            | Quantity in Dashboard*                           |
| ------------------ | :--------------: | ------------- | ------------------                     | :----------------------------------------------: |
| Day 1 (morning)    | 8                | 8 / 1         | 8 / 1                                  | 8                                                |
| Day 1 (night)      | 3                | (8 + 3) / 2   | 5.5 / 1                                | 5.5 (On Day 1 EOD)                               |
| Day 2 (morning)    | 2                | 2 / 1         | (5.5 + 2) / 2                          | 3.75                                             |
| Day 2 (night)      | 5                | (2 + 5) / 2   | (5.5 + 3.5) / 2                        | 4.5 (On Day 2 EOD)                               |
| Day 3 to Day 15    | 1                | 1 / 1         | (5.5 + 3.5 + (1 + 13)  / 15            | 1.4666  (On Day 15 EOD)                          |
| Day 15 to Day 30   | 0                | 0 / 1         | (5.5 + 3.5 + (1 \* 12) + (0  \* 15) / 30 | 0.7333  (On Day 30 EOD)                          |
{: caption="Table 5. Average usage per day and monthly average calculations" caption-side="top"}

\* As seen on the same day as when the usage was submitted.

#### Daily proration Max
{: #daily-proration}

Calculate the maximum usage per day and average it for the month. The maximum of each day is added up and divided by the number of days currently passed (in UTC).

Formula: Summation(daily max) / number of days passed in billing period

Note that the quantity might change throughout the month, but what is rated is the maximum usage per day.

Given a 30-day month:

| Time             | Usage Sent In  | Daily Max | Calculation                    | Quantity in Dashboard* |
|------------------|:--------------:| --------- | ------------------------------ |:----------------------:|
| Day 1 (morning)  | 0              | MAX(0)    | 0 / 1                          | 0                      |
| Day 1 (night)    | 1              | MAX(0, 1) | 1 / 1                          | 1                      |
| Day 2 to Day 15  | 1              | MAX(1)    | (1 + 1 + ...) / day            | 1                      |
| Day 15 to Day 30 | 0              | MAX(0)    | (1 + (1 * 14) + 0 + ...) / day | < 1                    |
{: caption="Table 6. Maximum usage per day and monthly average calculations" caption-side="top"}

\* As seen on the same day as when the usage was submitted.

## Metering and rating scale examples
{: #scale-examples}

You can use the scaling configuration to compile the unit quantity differently from what is sent in usage submissions to what is displayed in the Usage Dashboard, and what is used for the rating and cost calculations. The following examples demonstrate these scenarios:

### You want more granularity than what users see
{: #users}

You want to send usages at a more granular level, but you want to show customers a more readable number.

For example, you might want to measure an instance's traffic in bytes and want the aggregated values in megabytes. To do this, you add a `scale` of 1024 to the **metering** configuration.

### You want more granularity than what your pricing configuration has
{: #pricing-configuration}

You price your metrics as $X / gigabyte, but you want to send them in megabytes. If your metric is priced at $1 / gigabyte, but a user uses 0.5 megabytes, they're charged $1 since your pricing is per gigabyte. You add a `scale` of 1024 to the **rating** configuration and set `clip` to `true`.

This holds true if your metric is also priced as $X per 100 API calls (or some other pack size).

### You want to scale at both metering and rating levels
{: #metering-rating}

You can add scaling to both metering and rating configurations. If you want to send in bytes but show megabytes to the user, you configure the metering scale to 1024. If your metric price is in gigabytes, you also configure the rating scale to be 1024.

## Pricing models
{: #pricing}

The following table provides detailed information about the pricing models that are available. For many of the available metrics, you select an associated pricing model.

| Model          | Description | Calculation | Example (5000 quantity) |
|:-----------------|:-------------|:----------- |:---------------------|
| Linear         | Multiply the unit price per resource (P) by the usage quantity (Q) to get the total amount (T)  | P*Q    | P=$1 T=1*5000 =$5000        |
| Proration      | Multiply the daily unit price per resource (P) by the daily usage quantity (Q) to get the total daily amount. The total charge involves cumulating the charges for all days within the month.         | T= (pd * Q1) + ...+(Pd *Qn)     | <ul><li>P= $30</li><li>Pd (daily price) =$30/30=$1 (assuming 30 days in a month)</li><li>T1= $1 * 1 =$1</li><li>T2 = $1 * 0 =$0</li><li>Tn = 1 * 1 =$1</li><li>T = $1 + $0 +...+$1 = $5000</li></ul>     |
| Simple tier (granular tier)  | A P*Q model in which the unit price for all consumption is determined by the tier the quantity falls into.           | <ul><li>If Q is <=Q1, T=P1*Q</li><li>If Q1 < Q <=Q2, T=P2*Q</li><li>If Q2 < Q <=Q3, T=P3*Q</li></ul>     |   <ul><li>Q1=1000, P1=$1</li><li>Q2=2500, P2=$0.9</li><li>Q3=10000, P3=$0.75</li><li>T=$0.75*5000=$3750</li></ul>              |
| Graduated tier (step tier)   | The price per unit varies as the quantity consumed moves into different predefined tiers. The total charge involves cumulating the charges from the previous tiers           | <ul><li>T1=P1*Q (0 < Q</li><li>If Q1 < Q <=Q2, T=T2</li><li>If Q2 < Q <=Q3, T=T3</li></ul>     | <ul><li>Q1=1000, P1=$1, T1=1*1000</li><li>Q2=1500, P2=$0.9, T2=0.9*1500</li><li>Q3=10000, P3=$0.75, T3=0.75*2500</li><li>T=1000 +1350+1875=$4225</li></ul>          |
| Block tier (up to)           | The total amount that is charged is established by an "up to" quantity that doesn't vary within the block     | <ul><li>If Q is <=Q1, T=T1</li><li>If Q1 < Q <=Q2, T=T2</li><li>If Q2 < Q <=Q3, T=T3</li></ul>    |  <ul><li>Q1=1000, T1=$0</li><li>Q2=2500, T2=2500</li><li>Q3=10000, T3=$4500</li><li>T=$4500</li></ul>            |
{: caption="Table 7. Pricing models" caption-side="top"}

