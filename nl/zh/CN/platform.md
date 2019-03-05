---


copyright:
  years: 2018, 2019
lastupdated: "2019-01-30"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# Integrated Billing 服务如何使用 {{site.data.keyword.Bluemix_notm}} 平台
{: #how-it-works}

Integrated Billing 服务不同于引荐服务。Integrated Billing 服务使用 {{site.data.keyword.Bluemix_notm}} 平台进行认证、访问、供应、计量和计费。本主题提供了 Integrated Billing 服务使用的平台组件的高级别概述。

## {{site.data.keyword.Bluemix_notm}} 供应层
{: #provisioning-layer}

供应层用于管理 {{site.data.keyword.Bluemix_notm}} 资源的生命周期。供应层负责控制和跟踪客户帐户中资源的生命周期。*资源*是一种物理或逻辑组件，可以针对应用程序或服务实例进行供应或保留。例如，资源包括数据库、帐户、处理器、内存以及存储限制。通常，由供应层跟踪的资源都会与使用量度量值和帐单相关联，但也并不总是如此。在某些情况下，资源可能会与供应层相关联，以确保资源生命周期可与帐户生命周期一起进行管理。

### 资源生命周期管理
{: #lifecycle}

供应层提供公共 API，用于控制资源从供应（创建实例）、绑定（创建访问凭证）、取消绑定（除去访问权）一直到取消供应（删除实例）的整个生命周期。此外，{{site.data.keyword.Bluemix_notm}} 平台还提供了可以管理这些资源的生命周期的 CLI 和 UI，您无需创建自己的管理工具。

供应层提供了一些 API，可帮助您管理资源生命周期的以下元素：
* 供应
* 更新资源实例
* 绑定
* 资源键
* 取消绑定
* 取消供应

## {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM)
{: #iam}

通过 Identity and Access Management (IAM)，您可以在整个 {{site.data.keyword.Bluemix_notm}} 上安全地对用户进行认证并一致地控制对所有云资源的访问权。{{site.data.keyword.Bluemix_notm}} 供应层采用了 IAM 来对针对供应层执行的操作进行认证和授权。第三方产品提供者使用 IAM 来创建认证流程 (OAuth)。有关更多信息，请参阅[什么是 IAM？](/docs/iam?topic=iam-iamoverview#iamoverview)

如果您的产品使用的是 OpenID Connect (OIDC) 库，那么 IAM 支持 OIDC 集成。OIDC 是基于 OAuth 2.0 的认证层，这是一个授权框架，可以帮助简化上线过程。有关 OIDC 的更多信息，请参阅 [Open ID Connect](http://openid.net/connect/){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。

## {{site.data.keyword.Bluemix_notm}} 目录
{: #catalog}

{{site.data.keyword.Bluemix_notm}}“目录”会存储 {{site.data.keyword.Bluemix_notm}} 控制台中显示的资源的产品定义（描述、功能、图像和 URL 等）。资源管理控制台用于定义服务必需元数据的所有方面。此元数据将发布到目录并用于显示在目录中。您可以在资源管理控制台中的**产品**和**套餐**页面中找到有关必需和可选元数据字段的详细信息。此处包含的关键项可让您快速了解这些信息。

   * 服务名称：服务的技术名称。服务名称至关重要，必须正确定义。您必须提供 {{site.data.keyword.Bluemix_notm}} 平台用于标识服务的服务名称，以及客户在 {{site.data.keyword.Bluemix_notm}}“目录”中看到的显示名称。服务名称并不是显示名称。
   * 服务显示名称：服务的用户友好名称。例如，“Compose Redis”
   * 服务标识：在对 OSB 代理程序发出的 API 调用中使用的服务的 GUID。此值必须唯一。
   * 服务图标：具有服务徽标的 SVG
   * 服务描述：将光标悬停在 {{site.data.keyword.Bluemix_notm}}“目录”用户界面中的“资源”图标上时显示的资源描述。可以为描述添加单个语句或短语。
   * 服务详细描述：目录列表页面中显示的第一段。在详细描述中，请至少使用两个句子。
   * 文档 URL：{{site.data.keyword.Bluemix_notm}} 文档的链接。您将在 PWB 中进行编写，并且 URL 值将由 PWB 为您生成。
   * 条款 URL：服务使用条款和条件的链接。请注意，对于 GDPR 用途，不要链接到现有第三方服务的条款和条件。您必须为 Integrated Billing 服务提供唯一页面。
   * 指示信息 URL：类似于“文档 URL”，也会将您指向 {{site.data.keyword.Bluemix_notm}} 文档；但是，“指示信息 URL”会将文档动态拉取到服务仪表板的“入门”选项卡中。
   * 类别：在目录中，应将服务放入其中的可用 {{site.data.keyword.Bluemix_notm}} 类别的选项。
   * 项目符号：有关服务的简短描述性亮点
   * 媒体：有关服务的截屏和视频
   * 服务套餐名称：每个套餐都具有技术名称。名称为全小写，不含空格，可以包含“-”。例如，`gold`。
   * 服务套餐显示名称：套餐的用户友好名称。例如，`Gold`。
   * 服务套餐标识：在对 OSB 代理程序发出的 API 调用中使用的服务套餐的 GUID。此值必须唯一。资源管理控制台将为您生成此值。
   * 服务套餐描述：资源套餐的描述。在 IBM Cloud“目录”中的“资源详细信息”页面上选择套餐后，会显示相应描述。
   * 服务套餐项目符号：有关服务套餐的简短描述性亮点


## Open Service Broker
{: #open-service}

服务代理程序用于管理服务的生命周期。{{site.data.keyword.Bluemix_notm}} 平台与服务代理程序进行交互，以供应和管理服务实例（服务产品的实例化）和服务绑定（应用程序与服务实例之间的关联的表示，通常包含应用程序将用于与服务实例进行通信的凭证）。提供有效的元数据值将在执行请求时创建成功的 REST API 响应。

{{site.data.keyword.Bluemix_notm}} 使用 Open Service Broker API (OSB) `V2.12` 规范。通读并熟悉 [Open Service Broker API 规范](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")，然后使用自述文件作为指南以了解更多信息。

资源控制器接收到供应资源的请求时，将调用 OSB 来验证服务类型、产品、套餐和区域可用性。资源控制器还会验证与客户帐户关联的套餐的可视性。{{site.data.keyword.Bluemix_notm}} 提供了用于扩展 OSB 规范的代理程序样本和 API 文档。浏览详细的 Integrated Billing 上线开发步骤时，可以找到有关开发和托管代理程序的更多详细信息。

## {{site.data.keyword.Bluemix_notm}} 计量服务
{: #metering-service}

如果服务提供计量套餐，那么将根据 {{site.data.keyword.Bluemix_notm}} 用户使用的资源量向其收费。例如，对于使用数据库服务的 {{site.data.keyword.Bluemix_notm}} 用户，可能会根据其应用程序使用的存储量对这些用户收费。必须执行使用量提交，才能将使用量转换为可收费记录。

所有提供计量套餐的 Integrated Billing 服务都必须使用 {{site.data.keyword.Bluemix_notm}} 计量服务来报告使用量数据。

如果提供计量套餐，那么您需要使用计量服务 API 来自动提交每小时使用量。

有关计量的更多信息，请参阅：[计量集成](/docs/third-party?topic=third-party-meteringintera#meteringintera)。有关提交计量使用量的更多信息，请参阅：[提交计量套餐的使用量](/docs/third-party?topic=third-party-submitusage#submitusage)。

## 供应方案：融会贯通
{: #provision2}

现在，我们将所有概念集中在一起，并查看有关如何使用 {{site.data.keyword.Bluemix_notm}} 平台来创建服务实例的示例。

![供应方案](images/flow-am.svg "平台如何处理服务实例创建")

用户要创建服务实例时，可以通过以下两种方式之一来进行创建：
* **CLI**：使用 `ibmcloud cli [ ibmcloud resource service-instance-create NAME SERVICE_NAME SERVICE_PLAN_NAME LOCATION ]`
* **{{site.data.keyword.Bluemix_notm}} 控制台**：用户可以选择服务和套餐并使用**创建**操作。

{{site.data.keyword.Bluemix_notm}} 平台会验证用户是否有权使用 {{site.data.keyword.Bluemix_notm}} IAM 来创建服务实例。执行此验证后，将启动服务代理程序的供应端点 (PUT /v2/resource_instances/:resource_instance_id)。执行供应时，必须满足以下规则：
* context 变量中包含 {{site.data.keyword.Bluemix_notm}} 上下文
* `X-Broker-API-Originating-Identity` 包含发起请求的用户的 IBM IAM 标识
* parameters 部分包含请求的位置（以及服务所需的更多参数）。

示例供应请求：

```
    PUT /v2/service_instances/crn%3Av1%3Abluemix%3Apublic%3Acompose-redis%3Aus-south%3Aa%2F46aa677e-e83f-4d17-a2b6-5b752564477c%3A416d769b-682d-4833-8bd7-5ef8778e5b52?accepts_incomplete=true HTTP/1.1
    Host:  https://broker.compose.cloud.ibm.com
    Authorization: basic dXNlcjpwYXNzd29yZA==
    X-Broker-Api-Version: 2.12
    X-Broker-API-Originating-Identity: ibmcloud aWJtaWQtNDU2MzQ1WA==
    {
      "service_id": "0bc9d744-6f8c-4821-9648-2278bf6925bb", // 上线中的服务 GUID
      "plan_id": "ecc19311-aba2-49f7-8198-1e450c8460d4", // 上线中的套餐 GUID
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

### 了解 {{site.data.keyword.Bluemix_notm}} `context` 参数
{: #parameter}

在先前的示例中，您可以看到在 `context` 参数中返回的元数据。{{site.data.keyword.Bluemix_notm}} 的供应上下文返回了以下内容：

* **platform**：将平台标识为“ibmcloud”

* **"account_id"**：在供应服务实例的 {{site.data.keyword.Bluemix_notm}} 中返回帐户的标识。

* **crn**：客户在 {{site.data.keyword.Bluemix_notm}} 中供应您的服务时，将创建服务实例，并且此实例由其 {{site.data.keyword.Bluemix_notm}} 资源名称 (CRN) 进行标识。CRN 将用于与 {{site.data.keyword.Bluemix_notm}} 交互的所有方面，包括供应、绑定（创建凭证和端点）、计量、仪表板显示和访问控制。从产品提供者的角度来说，CRN 很大程度上可以被视为要用于 {{site.data.keyword.Bluemix_notm}} API 的不透明字符串。还可以使用以下结构对其进行分解：

   ```
   crn:version:cname:ctype:service-name:location:scope:service-instance:resource-type:resource
   ```

   在供应样本中，我们看到 `compose-redis` 服务 CRN 为：

   ```
   crn:v1:bluemix:public:compose-redis:us-south:a/46aa677e-e83f-4d17-a2b6-5b752564477c:416d769b-682d-4833-8bd7-5ef8778e5b52::
   ```

   在此样本中，此 `compose-redis` 实例属于标识为 46aa677e-e83f-4d17-a2b6-5b752564477c 的 {{site.data.keyword.Bluemix_notm}} 帐户。该实例的唯一标识为 `416d769b-682d-4833-8bd7-5ef8778e5b52`，并且该实例在公共 {{site.data.keyword.Bluemix_notm}} 的 `us-south` 区域进行托管。

* **resource_group_crn**：返回包含服务实例的资源组。有关更多详细信息，请参阅[管理资源组](/docs/resources?topic=resources-rgs#rgs)。

   除特殊情况外，产品提供者并不关心 `resource_group_crn`。在使用该字段之前，请就您的用例向 IBM 代表进行咨询。
   {: note}

