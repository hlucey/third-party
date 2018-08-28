---


copyright:
  years: 2018
lastupdated: "2018-08-21"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 步骤 2. 在资源管理控制台中定义产品

资源管理控制台是一个基于 Web 的工具，可帮助指导您将第三方产品交付到 {{site.data.keyword.Bluemix_notm}}“目录”中。

现在，您已获得批准交付 Integrated Billing 服务，也已准备好转至资源管理控制台来注册、开始开发产品，以及提供价格套餐：
   1. 向资源管理控制台注册服务，并验证“摘要”页面。
   2. 在“产品”页面中输入目录元数据。
   3. 向 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 注册产品。注册将生成用于认证服务的客户机标识和服务标识凭证。
   4. 填写“定价”页面，以确保 {{site.data.keyword.Bluemix_notm}} 中的服务产品向客户提供正确的价格套餐。您定义的套餐包括用于提供重要使用量详细信息的计量。
   5. 将产品元数据导出为 JSON 格式。


## 开始之前

此步骤假定您已获得批准交付 Integrated Billing 服务。如果您尚未完成 Provider Workbench 中的初始注册和批准，请参阅[入门教程](/docs/third-party/index.html)。
{: tip}

1. 确保您已开始工作：[步骤 1：编写服务文档和市场营销公告 (PWB)](/docs/third-party/cis1-docs-marketing.html)。
2. 确保已向 {{site.data.keyword.Bluemix_notm}} 注册。如果未注册，请先[注册](https://console.bluemix.net/registration)，然后再继续操作。
3. 在资源管理控制台中开始工作时，请确保您处于正确的帐户中。
4. 准备 {{site.data.keyword.Bluemix_notm}} 服务名称。

   您必须提供 {{site.data.keyword.Bluemix_notm}} 平台用于标识服务的服务名称，以及客户在 {{site.data.keyword.Bluemix_notm}}“目录”中看到的显示名称。

  向资源管理控制台注册产品时，准备好 {{site.data.keyword.Bluemix_notm}} 服务名称。服务名称并不是显示名称。服务名称必须遵循以下规则：
   - 必须全部为小写
   - 不能包含空格，但可以包含连字符 (`-`)
   - 必须少于 32 个字符

   服务名称应该包含您的公司名称。如果公司有多个产品，那么服务名称中应该同时包含公司和产品名称。例如，Compose 公司提供了 Redis 和 Elasticsearch 产品。这些产品在 {{site.data.keyword.Bluemix_notm}} 上的样本服务名称将为 `compose-redis` 和 `compose-elasticsearch`。这两个服务名称都具有 {{site.data.keyword.Bluemix_notm}}“目录”中显示的关联显示名称：*Compose Redis* 和 *Compose Elasticsearch*。另一家公司（例如 FastJetMail）可能只有一个 JetMail 产品，在这种情况下，服务名称应该为 `fastjetmail`。

## 注册产品

首先，请登录并注册产品。

1. 使用 {{site.data.keyword.Bluemix_notm}} 标识登录到 {{site.data.keyword.Bluemix_notm}}：[https://console.bluemix.net](https://console.bluemix.net){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。**警告**：您处于正确的 {{site.data.keyword.Bluemix_notm}} 帐户中至关重要。如果您有多个帐户，请确保切换到正确的帐户。
2. 转至资源管理控制台仪表板：[https://console.bluemix.net/onboarding/dashboard](https://console.bluemix.net/onboarding/dashboard){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。
3. 单击**新建资源**以添加资源。
4. 添加**资源名称**。此值是您在上一部分中派生的唯一 {{site.data.keyword.Bluemix_notm}} 服务名称。
5. 在此过程中，此时我们并不希望您具有现有的托管服务代理程序，请对**代理程序是否准备好导入？**字段选择**否**。在后面的步骤中，我们将指导您创建代理程序，并且在开发和托管代理程序后，您将返回到资源管理控制台以导入代理程序。
7. 提交后，您将转至**摘要**页面。填写其他任何*必需*值，然后单击**保存**。

您可以保存在资源管理控制台中的进度，以后返回来添加更多信息。资源管理控制台旨在帮助您管理服务的生命周期，因此如果您没有立即填写所有字段也没关系。
{: tip}

## 输入产品元数据

在**产品**页面上，提供存储在 {{site.data.keyword.Bluemix_notm}}“目录”中的元数据值。此外，其中的某些值需要导出并存储在服务代理程序中，这些值将用于供应，并作为 `catalog (GET)` 响应的一部分返回。您将使用这些值来帮助在后面的步骤中快速开始服务代理程序的开发。

1. 在资源管理控制台中，单击**产品**页面，然后单击**列表页面**选项卡。**列表页面**定义在 {{site.data.keyword.Bluemix_notm}} 产品的服务仪表板中显示的元数据。填写所有必需值，然后单击**保存**。资源管理控制台将向 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 初始注册您的服务。这将显示服务已向 IAM 注册的通知。稍后您将使用 IAM 执行更多操作。
2. 在“产品”页面中，单击**设置**选项卡。
   1. 指定产品是否允许**支持套餐更改？**。缺省值为**否**。如果指定**是**，那么需要扩展 Open Service Broker 以支持所供应实例的套餐更改。如果产品支持多个套餐，并且您希望用户能够更改现有供应实例的套餐，那么需要启用用户更新其服务实例的能力。有关更多详细信息，请参阅 [Open Service Broker API V2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#updating-a-service-instance){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中的 `/v2/service_instances/{instance_id} PATCH` 端点
   2. 指定服务是否**可绑定**。缺省值为**否**。如果服务可以绑定到 {{site.data.keyword.Bluemix_notm}} 中的应用程序，请选择**是**。如果可绑定，那么服务必须能够将 API 端点和凭证返回给服务使用者。开发可绑定服务时，必须使用 [Open Service Broker API V2.12 中的可绑定操作](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#binding){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")
   3. 填写其他必填字段，然后单击**保存**。
3. 现在，“产品”页面应该在导航中具有复选标记，指示您已达到完成此页面的最低需求。如果该页面仍标记为未完成，那么应该重新打开该页面，并检查是否有任何未填写的*必填*字段。

初始产品信中包含 Provider Workbench 生成的服务文档 URL。必须在**文档 URL** 和**指示信息 URL** 字段中输入该 URL
{: tip}

## 向 IAM 注册

所有要上线到 {{site.data.keyword.Bluemix_notm}} 中的服务都需要 IAM。请参阅[什么是 IAM？](/docs/iam/index.html#what-is-cloud-iam-)以了解有关 IAM 概念和需求的更多信息。

资源管理控制台会生成以下 IAM 值：
   - 服务标识（生成并存储）
   - API 密钥（生成但不存储 - 仅显示一次）
   - 客户机标识（生成并存储）
   - 客户机私钥（生成但不存储）

服务提供者需要提供：
   - 重定向 URI（开发 OSB 后，您将返回到资源管理控制台。您将能够从托管服务代理程序的位置中派生重定向 URI。）

1. 在资源管理控制台中，单击**访问管理**页面。
2. 单击**启用 IAM**。资源管理控制台会向 IAM 注册您的服务，创建服务标识和策略，并为您创建 API 密钥。此外，还会创建不完整的客户机标识和客户机私钥。在拥有重定向 URI 后，必须使用重定向 URI 对客户机标识进行更新。
3. 单击**状态**以查看 IAM 启用的当前状态。

**注**：稍后您需要返回到 IAM 页面以提供`重定向 URI`。在执行其他一些开发以构建认证流程之前，您不会拥有此值。后面的步骤将帮助指导您识别重定向 URI 值。

在**启用 IAM** 后，会向您提供 API 密钥。保存 API 密钥非常关键。该值不会再显示。如果丢失了 API 密钥，您可以删除该密钥并创建新密钥：[管理服务标识 API 密钥](/docs/iam/serviceid_keys.html#serviceidapikeys)
{: tip}

## 制定价格套餐

将服务上线到 {{site.data.keyword.Bluemix_notm}} 后，必须定义价格套餐。如果您对要如何向服务用户收费有详细的了解，那么可以在套餐中提供这些信息。但是，如果您尚未决定好付费套餐，那么一开始可以启用免费套餐，以后回来设置付费套餐。

1. 在资源管理控制台中，单击**定价**页面。
2. 单击**添加套餐**以创建新的套餐条目，然后单击**编辑套餐**以编辑套餐。
   * **免费套餐**：所有产品都可以拥有一个免费轻量套餐，允许用户试用您的服务。免费套餐使用*轻量*作为**显示名称**，使用 *lite* 作为**编程名称**。对于**此套餐是否免费？**，指定**是**。单击**保存**。您的套餐将发布到 {{site.data.keyword.Bluemix_notm}}“目录”。
   * **预订套餐**：对于**此套餐是否免费？**，指定**否**。填写必填字段。
保留缺省**定价度量值**度量值。提供的此缺省度量值用于向用户收取一次性的月度费用。单击**保存**。您的套餐将发布到 {{site.data.keyword.Bluemix_notm}}“目录”。保存用于提交使用量的样本 curl 命令。
   * **计量套餐**：对于**此套餐是否免费？**，指定**否**。填写必填字段。
*删除*缺省**定价度量值**预订度量值。单击**添加其他度量值**，填写**添加定价度量值**页面，然后单击**添加度量值**。单击**保存**。您的套餐将发布到 {{site.data.keyword.Bluemix_notm}}“目录”。保存用于提交使用量的样本 curl 命令。有关选择正确度量值的帮助，请参阅[计量集成](/docs/third-party/metering.html)。
3. 现在，**定价**页面应该标记为“完成”，指示您已达到完成此页面的最低需求。

服务提供者需要为所有计量套餐自动提交每小时使用量。有关更多信息，请参阅：[提交计量套餐的使用量](/docs/third-party/submitusage.html)
{: tip}

## 将元数据导出为 JSON

现在，您已在资源管理控制台中定义服务，因此可以下载 catalog.json 文件，并将其用于通知 Open Service Broker 的开发。catalog.json 包含必须在代理程序中托管的元数据。这些值定义代理程序与 {{site.data.keyword.Bluemix_notm}} 平台（用于代理程序支持的服务和套餐）之间的合同。在供应时非必需的其他所有目录元数据都将存储在 {{site.data.keyword.Bluemix_notm}}“目录”中，并且对用于呈现仪表板的目录显示值（如链接、图标和 i18n 转换的元数据）的任何更新都应在资源管理控制台中进行更新，而不在代理程序中存放。代理程序中存储的任何元数据都不会显示在 {{site.data.keyword.Bluemix_notm}} 控制台或 {{site.data.keyword.Bluemix_notm}} CLI 中；控制台和 CLI 将返回在资源管理控制台内设置并存储在 {{site.data.keyword.Bluemix_notm}}“目录”中的内容。

1. 在资源管理控制台中，打开**部署**页面。
2. 单击**管理**。
3. 单击**下载定义**。

保存 `catalog.json` 文件。在下一部分中，将使用此文件来开发 Open Service Broker。

## 后续步骤

加油！您已通过添加目录显示元数据，向 IAM 注册以及创建一个或多个价格套餐，定义了服务产品。接下来，可以采用导出的 JSON 并开始开发服务代理程序。请参阅[步骤 3：开发和托管服务代理程序](/docs/third-party/cis3-broker.html)。
