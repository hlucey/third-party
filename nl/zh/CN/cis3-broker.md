---


copyright:
  years: 2018
lastupdated: "2018-06-26"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 步骤 3：开发和托管服务代理程序

通过使用从资源管理控制台中导出的元数据，您可使用所选编程语言构建一个或多个新的服务代理程序。

服务代理程序用于管理服务的生命周期。{{site.data.keyword.Bluemix_notm}} 平台与服务代理程序进行交互，以供应和管理服务实例（服务产品的实例化）和服务绑定（应用程序与服务实例之间的关联的表示，通常包含应用程序将用于与服务实例进行通信的凭证）。提供有效的元数据值将在执行请求时创建成功的 RESTful API 响应。

您可以组合使用从资源管理控制台导出的元数据、公共 {{site.data.keyword.Bluemix_notm}} 服务代理程序样本以及资源代理程序 API 文档来开始构建代理程序。要开发代理程序，请执行以下操作：

1. 查看平台供应方案
2. 通读 OSB 规范
2. 查看 {{site.data.keyword.Bluemix_notm}} 代理程序样本
3. 使用资源代理程序 API 文档来了解 REST API 端点逻辑
4. 使用从资源管理控制台导出的元数据来通知开发
5. 查看 {{site.data.keyword.Bluemix_notm}} 平台提供的代理程序信息
6. 通读其他建议以优化开发
7. 托管代理程序
8. 测试代理程序

## 开始之前

此步骤假定您已获得批准交付 Integrated Billing 服务。如果您尚未完成 Provider Workbench 中的初始注册和批准，请参阅[入门教程](/docs/third-party/index.md)。
{: tip}

确保已开始执行步骤 1，并完成了步骤 2：
1. [编写服务文档和市场营销公告](/docs/third-party/cis1-docs-marketing.html)。
2. [在资源管理控制台中定义产品](/docs/third-party/cis2-rmc-define.html)。


## 查看 {{site.data.keyword.Bluemix_notm}} 平台供应方案

您将开发与 {{site.data.keyword.Bluemix_notm}} 平台一起使用的 Open Service Broker。请参阅[供应方案](/docs/third-party/platform.html#provisioning-scenario-pulling-it-all-together)，以了解资源创建的工作方式。

## 熟悉 OSB 规范

{{site.data.keyword.Bluemix_notm}} 使用 Open Service Broker API (OSB) `V2.12` 规范。通读并熟悉 [Open Service Broker API 规范](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")，然后使用自述文件作为指南以了解更多信息。

## 查看 {{site.data.keyword.Bluemix_notm}} 代理程序样本

[https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")

**注：**样本并不代表所有语言。例如，如果您需要样本 Python 代理程序，那么应该能够通过搜索 Google 来找到 Cloud Foundry 样本。您可能需要调整此样本来满足 OSB 需求。


## 查看 {{site.data.keyword.Bluemix_notm}} Open Service Broker API 文档

应该在了解 [{{site.data.keyword.Bluemix_notm}} Open Service Broker API](https://console.bluemix.net/apidocs/821-ibm-cloud-open-service-broker-api?&language=node#introduction){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 的基础上开发服务代理程序。熟悉代理程序 API，了解它将如何与代理程序进行交互。

{{site.data.keyword.Bluemix_notm}} Open Service Broker 扩展了 Open Service Broker 2.12 规范。
{: tip}

### 所有服务代理程序的必需端点逻辑

服务代理程序必须提供 REST API 使用的一组标准元数据值，并且 {{site.data.keyword.Bluemix_notm}} 代理程序必须包含用于以下 REST API 端点/路径的逻辑：

<dl>
  <dt>目录 (GET)</dt>
  <dd>返回代理程序中包含的目录元数据。有许多其他未返回的目录元数据值 - 这些值仅在资源管理控制台中添加并存储在 {{site.data.keyword.Bluemix_notm}}“目录”中。</dd>
  <dt>资源实例 (PUT)</dt>
  <dd>供应服务实例</dd>
  <dt>资源实例 (DELETE)</dt>
  <dd>取消供应服务实例。</dd>
  <dt>资源实例 (PATCH)</dt>
  <dd>更新服务实例。</dd>
</dl>

**关于目录 (GET) 的注释**：此端点定义代理程序与 {{site.data.keyword.Bluemix_notm}} 平台（用于代理程序支持的服务和套餐）之间的合同。此端点返回存储在代理程序中的目录元数据。这些值定义了服务与 {{site.data.keyword.Bluemix_notm}} 平台之间最少内容的供应合同。在供应时非必需的其他所有目录元数据都将存储在 {{site.data.keyword.Bluemix_notm}}“目录”中，并且对用于呈现仪表板的目录显示值（如链接、图标和 i18n 转换的元数据）的任何更新都应在资源管理控制台中进行更新，而不在代理程序中存放。代理程序中存储的任何元数据都不会显示在 {{site.data.keyword.Bluemix_notm}} 控制台或 {{site.data.keyword.Bluemix_notm}} CLI 中；控制台和 CLI 将返回在资源管理控制台内设置并存储在 {{site.data.keyword.Bluemix_notm}}“目录”中的内容。下面是目录 (GET) 应该返回的最少必需值：

```
{
       "services":[
   {
      "id": "ibmcloud-link",
           "name": "ibmcloud-link",
           "description": "An IBM provided service that enables aliasing to service instances in the {{site.data.keyword.Bluemix_notm}}.",
           "bindable": true,
           "plan_updateable": false,
           "plans": [
               {
                   "id": "ibmcloud-link-alias",
                   "name": "ibmcloud-alias",
                   "free": true,
                   "description": "The {{site.data.keyword.Bluemix_notm}} alias plan used for linking."
               }
               ]
       }]
}
```

### 可绑定服务的必需端点逻辑

如果服务可以绑定到 {{site.data.keyword.Bluemix_notm}} 中的应用程序，那么必须能够将 API 端点和凭证返回给服务使用者。可绑定服务必须使用 Open Service Broker 规范中的可绑定操作，并实现以下端点/路径：

<dl>
  <dt>绑定和凭证 (PUT)</dt>
  <dd>将服务实例绑定到应用程序。</dd>
  <dt>绑定和凭证 (DEL)</dt>
  <dd>取消服务实例与应用程序的绑定。</dd>
</dl>

### 必需的 {{site.data.keyword.Bluemix_notm}} 扩展端点

OSB 规范*不*支持禁用但尚未删除的实例状态。为了使 {{site.data.keyword.Bluemix_notm}} 能够支持可能遇到导致帐户暂挂（但尚未取消）的计费中断或其他情况的客户，{{site.data.keyword.Bluemix_notm}} 定义了扩展 API 端点，允许禁用和重新启用服务实例。**需要**以下端点扩展：

<dl>
  <dt>启用和禁用实例 (GET)</dt>
  <dd>状态 - 返回服务实例的状态。</dd>
  <dt>启用和禁用实例 (PUT)</dt>
  <dd>允许启用或禁用服务实例。</dd>
</dl>

**注**：调用禁用端点时禁用对服务实例的访问，以及调用启用端点时重新启用对服务实例的访问，是服务提供者的责任。

## 了解如何使用导出的元数据来指导代理程序开发

从资源管理控制台导出的元数据可以用作开发您自己的代理程序的指南。并非输入到资源管理控制台中的所有值都需要用于供应服务。从资源管理控制台导出的元数据定义了服务与 {{site.data.keyword.Bluemix_notm}} 平台之间最少内容的供应合同。导出的 JSON 应该提供以下值：

```
{
services :
            [
                {
                    bindable         : true,
                    description      : "Test Node Resource Service Broker Description",
                    // TODO - http://www.guidgenerator.com 生成的 GUID
                    // TODO - 此服务标识在 IBM Cloud 环境的服务产品组中必须唯一
                    id               : "df35cab6-347b-4ba5-8f39-e9c23a237f5b",
                    metadata         :
                    {
                        displayName         : "Test Node Resource Service Broker Display Name",
                        documentationUrl    : baseMetadataUrl + "documentation.html",
                        imageUrl            : baseMetadataUrl + "services.svg", // Copied from https://github.com/carbon-design-system/carbon-icons/blob/master/src/svg/services.svg
                        instructionsUrl     : baseMetadataUrl + "instructions.html",
                        longDescription     : "Test Node Resource Service Broker Long Description",
                        providerDisplayName : "Company Name",
                        supportUrl          : baseMetadataUrl + "support.html",
                        termsUrl            : baseMetadataUrl + "terms.html"
                    },
                    name             : SERVICE_NAME,
                    // TODO - 确保此值对于服务是准确的。需要下面的 PATCH of /v2/service_instances/:instance_id（如果为 true）
                    plan_updateable  : true,
                    tags             : ["lite", "tag1a", "tag1b"],
                    plans            :
                    [
                        {
                            bindable    : true,
                            description : "Test Node Resource Service Broker Plan Description",
                            free        : true,
                            // TODO - http://www.guidgenerator.com 生成的 GUID
                            // TODO - 此服务标识在 IBM Cloud 环境的服务套餐组中必须唯一
                            id          : "2a1d139b-1b05-4e33-b72e-a1f8c14be559",
                            metadata    :
                            {
                                bullets     : ["Test bullet 1", "Test bullet 2"],
                                displayName : "Lite"
                            },
                            // TODO - 此服务套餐名称在包含服务定义中必须唯一
                            name        : "lite"
                        }
                    ]
                }
            ]
}
```


OSB 服务数组必须与添加到资源管理控制台中的产品元数据完全相同。要确保在 OSB 与资源管理控制台之间进行一对一奇偶性校验，请务必将从资源管理控制台下载的 `catalog.json` 中的服务数组与代理程序中的实际服务数组进行比较。所有服务和套餐标识及名称都必须匹配。
{: tip}

## {{site.data.keyword.Bluemix_notm}} 平台提供的代理程序信息

服务代理程序将从 {{site.data.keyword.Bluemix_notm}} 平台接收以下信息：

### X-Broker-API-Originating-Identity

**用户身份头**将通过 API 源身份头提供。此请求头将包含用户的 {{site.data.keyword.Bluemix_notm}} IAM 身份。IAM 身份将为 base64 编码。{{site.data.keyword.Bluemix_notm}} 支持单个认证域：`IBMid`。`IBMid` 域使用 IBM 标识唯一标识 (IUI) 来标识 {{site.data.keyword.Bluemix_notm}} 中的用户身份。此 IUI 是服务提供者的不透明字符串。

示例：

```
X-Broker-API-Originating-Identity: ibmcloud eyJpYW1faWQiOiJJQk1pZC01MEdOUjcxN1lFIn0=
Decoded:
{"iam_id":"IBMid-50GNR717YE"}
```

### API 版本头

**API 版本头**将为 [2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。例如：`X-Broker-Api-Version: 2.12`。

### 资源实例 (PUT) body.context 和资源实例 (PATCH) body.context

`PUT /v2/service_instances/:resource_instance_id` 和 `PATCH /v2/service_instances/:resource_instance_id` 将在 **body.context** 中接收到以下值：`{ "platform": "ibmcloud", "account_id": "tracys-account-id", "crn": "resource-instance-crn" }`。

## 其他代理程序建议

### 有关使用异步与同步操作的建议

OSB API 支持同步和异步操作方式。如果操作需要的时间将少于 10 秒，那么建议使用同步响应。否则，应使用异步操作方式。OSB 规范中包含有关此内容的更多信息。

如果在尝试供应实例时异步操作需要的时间少于 10 秒，那么平台将超时。
{: tip}

### 管理不同位置代理程序的建议

用户了解其云服务的位置对于等待时间、可用性和数据存储位置非常重要。

在 {{site.data.keyword.Bluemix_notm}} 上供应服务实例时，用户将提供的其中一个必需参数是要供应该服务实例的位置。某些服务可能支持在多个位置进行供应。例如，数据库服务可支持在所有 {{site.data.keyword.Bluemix_notm}} 区域中供应，也可以支持子集。

如果第三方基于 API 的服务在其他云中实现并公开在 {{site.data.keyword.Bluemix_notm}} 中，那么该位置应该指示该服务在其他云中的位置。

上线到 {{site.data.keyword.Bluemix_notm}} 时，必须至少实现一个 OSB 代理程序，但是您可根据部署策略和要为服务支持的位置，选择具有多个代理程序。在资源管理控制台工具中，您已建立服务/套餐/位置元组与将为该元组提供操作的代理程序之间的映射。典型选项是定义单个代理程序来处理服务的所有位置，或者每个位置定义一个代理程序；此选项由服务提供者决定。

有关可用位置的列表，请查阅 [IBM 全球目录位置](https://resource-catalog.bluemix.net/search?q=kind:geography){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。如果服务需要在“全球目录”中定义其他位置，请咨询 {{site.data.keyword.Bluemix_notm}} 上线团队。


## 托管代理程序

代理程序必须作为可响应 REST API 调用的应用程序的一部分进行托管。托管位置必须符合 {{site.data.keyword.Bluemix_notm}} 安全准则。您可以在 {{site.data.keyword.Bluemix_notm}} 中进行托管，也可以在外部进行托管，只要可从 {{site.data.keyword.Bluemix_notm}} 本身公开访问托管位置即可。

要在 IBM 外部托管代理程序，必须确保该位置符合以下安全准则：
- 必须遵循传输层安全性 (TLS) 协议 V1.2
- 必须在可通过公用因特网访问的有效 HTTPS 端点上进行托管

如果要在 {{site.data.keyword.Bluemix_notm}} 中进行托管，可以在此处找到有关使用 Containers (Kubernetes) 创建应用程序的信息：[内部采用者 - 用法信息](/docs/containers/cs_internal.html#cs_internal)。

您将需要服务代理程序的托管位置才能完成下一步。移动到下一步时，确保已具有与应用程序关联的 URL 和凭证。
{: tip}

## 如何测试服务的代理程序

您应该通过对要启用的不同端点运行 curl 命令来验证代理程序。样本自述文件提供了有关对 OSB 端点运行 curl 的极佳指导信息：https://github.com/IBM/sample-resource-service-brokers/blob/master/README.md

### 如何对服务代理程序运行 curl

使用以下示例来测试代理程序 curl 响应：

```
curl -X PUT  https://<sample-service-broker>/v2/service_instances/<encoded-resource-crn> \
     -u '<your broker user>:<your broker password>' \
     -H 'content-type: application/json' \
      -d '{ "context": {"platform": "ibmcloud", \
                        "account_id": "34ff5928-c3c7-4d46-bbf6-1a5628c325d1", \
                        "resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/003e9bc3993aec710d30a5a719e57a80::resource-group:b4570a825f7f4d57aa54e8e1d9507926", \
                        "crn": "<resource-crn>", \
                        "target_crn": "<target_crn>"}, \
            "service_id": "a07f025c-90db-4652-afd1-cf4adfac93c8", \
            "plan_id": "fe442cec-2eef-41fe-9f92-58d6c094584f"}'
```

## 后续步骤

您已掌握了一些重要技能！您刚才已构建并托管符合 OSB 规范的服务代理程序。请参阅[步骤 4：开发认证流程](/docs/third-party/cis5-iam.html)。
