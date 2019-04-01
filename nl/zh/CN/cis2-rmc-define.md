---

copyright:

  years: 2018, 2019 

lastupdated: "2019-03-28"

keywords: billing service, resource management console, pricing plans

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

# 步骤 2. 在资源管理控制台中定义产品
{: #step2-define}

资源管理控制台是一个工具，可帮助指导您将第三方产品交付到 {{site.data.keyword.Bluemix_notm}}“目录”中。现在，您已获得交付 Integrated Billing 服务的许可，也已准备好使用资源管理控制台来注册服务、开始进行开发，以及定义价格套餐。资源管理控制台是一个基于 Web 的工具，可帮助指导您将 Integrated Billing 服务交付到 {{site.data.keyword.Bluemix_notm}}“目录”中。
{:shortdesc}

## 开始之前
{: #rmc-pre-reqs}

1. 确保您已开始执行[步骤 1：编写服务文档和市场营销公告 (PWB)](/docs/third-party?topic=third-party-content-tasks#content-tasks)。
2. 确保已向 {{site.data.keyword.Bluemix_notm}} 注册。否则，请[注册](https://cloud.ibm.com/registration){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")，然后再继续。
3. 在资源管理控制台中开始工作时，请确保您处于正确的帐户中。
4. 准备 {{site.data.keyword.Bluemix_notm}} 服务名称。您必须提供 {{site.data.keyword.Bluemix_notm}} 平台用于标识服务的服务名称，以及客户在 {{site.data.keyword.Bluemix_notm}}“目录”中看到的显示名称。

  向资源管理控制台注册产品时，准备好 {{site.data.keyword.Bluemix_notm}} 服务名称。服务名称并不是显示名称。服务名称必须遵循以下规则：
   - 必须全部为小写
   - 不能包含空格，但可以包含连字符 (`-`)
   - 必须少于 32 个字符

   服务名称必须包含公司名称。如果公司有多个产品，那么服务名称中必须同时包含公司名称和产品名称。例如，Compose 公司提供了 Redis 和 Elasticsearch 产品。这些产品在 {{site.data.keyword.Bluemix_notm}} 上的样本服务名称将为 `compose-redis` 和 `compose-elasticsearch`。这两个服务名称都包含 {{site.data.keyword.Bluemix_notm}}“目录”中显示的关联显示名称：*Compose Redis* 和 *Compose Elasticsearch*。另一家公司（例如 FastJetMail）可能只有一个 JetMail 产品，在这种情况下，服务名称必须为 `fastjetmail`。

## 注册产品
{: #register}

首先，请登录并注册产品。

1. 使用 {{site.data.keyword.Bluemix_notm}} 标识登录到 [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。**警告**：您处于正确的 {{site.data.keyword.Bluemix_notm}} 帐户中至关重要。如果您有多个帐户，请确保切换到正确的帐户。
2. 转至[资源管理控制台仪表板](https://cloud.ibm.com/onboarding/dashboard){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。
3. 单击**新建资源**以添加资源。
4. 添加**资源名称**。此值是您在上一部分中派生的唯一 {{site.data.keyword.Bluemix_notm}} 服务名称。
5. 我们的预期是您没有现有的托管服务代理程序，所以请对**代理程序是否准备好导入？**字段选择**否**。在后面的步骤中，我们将指导您如何创建代理程序。在开发和托管代理程序后，您将返回到资源管理控制台来导入代理程序。
7. 提交后，您将转至**摘要**页面。填写其他任何*必需*值，然后单击**保存**。

您可以保存资源管理控制台中的进度，以后再返回添加更多信息。资源管理控制台旨在帮助您管理服务的生命周期。如果当时没有填完所有字段，也没关系。
{: tip}

## 输入产品元数据
{: #offering-metadata}

在**目录列表**页面上，提供存储在 {{site.data.keyword.Bluemix_notm}}“目录”中的元数据值。此外，其中的某些值需要导出并存储在服务代理程序中，这些值将用于供应，并作为 `catalog (GET)` 响应的一部分返回。使用这些值，有助于在后面的步骤中快速开始开发服务代理程序。

1. 在资源管理控制台中，单击**目录列表**页面，然后单击**列表页面**选项卡。**列表页面**定义在 {{site.data.keyword.Bluemix_notm}} 产品的服务仪表板中显示的元数据。填写所有必需值，然后单击**保存**。资源管理控制台会向 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 初始注册您的服务。这将显示服务已向 IAM 注册的通知。稍后您可以使用 IAM 执行更多操作。
2. 在**目录列表**页面中，单击**设置**选项卡。
   1. 指定产品是否允许**支持套餐更改？**缺省值为**否**。如果指定**是**，那么需要扩展 Open Service Broker 以支持所供应实例的套餐更改。如果产品支持多个套餐，并且您希望用户能够更改现有所供应实例的套餐，那么需要启用相应选项，使用户能够更新其服务实例。有关更多详细信息，请参阅 [Open Service Broker API V2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#updating-a-service-instance){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中的 `/v2/service_instances/{instance_id} PATCH` 端点
   2. 指定服务是否**可绑定**。缺省值为**否**。如果服务可以绑定到 {{site.data.keyword.Bluemix_notm}} 中的应用程序，请选择**是**。如果可绑定，那么服务必须将 API 端点和凭证返回给服务使用者。开发可绑定服务时，必须使用 [Open Service Broker API V2.12 中的可绑定操作](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#binding){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")
   3. 填写其他必填字段，然后单击**保存**。
3. 现在，“产品”页面在导航中有一个复选标记，指示您已满足此页面的最低完成需求。如果该页面仍标记为“未完成”，那么必须重新打开该页面，检查是否有任何未填写的*必填*字段。

初始产品信中包含 Provider Workbench 生成的服务文档 URL。必须在**文档 URL** 和**指示信息 URL** 字段中输入该 URL
{: tip}

## 向 IAM 注册
{: #reg-iam}

所有上线到 {{site.data.keyword.Bluemix_notm}} 中的服务都需要 IAM。请参阅[什么是 IAM？](/docs/iam?topic=iam-iamoverview#iamoverview)以了解有关 IAM 概念和需求的更多信息。

资源管理控制台会生成以下 IAM 值：
   - 服务标识（生成并存储）
   - API 密钥（生成但不存储 - 仅显示一次）
   - 客户机标识（生成并存储）
   - 客户机私钥（生成但不存储）

服务提供者需要提供：
   - 重定向 URI（开发 OSB 后，您将返回到资源管理控制台。您将从托管服务代理程序的位置中派生重定向 URI。）

1. 在资源管理控制台中，单击**访问管理**页面。
2. 单击**启用 IAM**。资源管理控制台会向 IAM 注册您的服务，创建服务标识和策略，并为您创建 API 密钥。此外，还会创建不完整的客户机标识和客户机私钥。在拥有重定向 URI 后，必须使用重定向 URI 对客户机标识进行更新。
3. 单击**状态**以查看 IAM 启用的当前状态。

稍后您需要返回到 IAM 页面来提供`重定向 URI`。在执行其他一些开发以构建认证流程之前，您不会拥有此值。后面的步骤将帮助指导您识别重定向 URI 值。
{: note}

在**启用 IAM** 后，会向您提供 API 密钥。保存 API 密钥非常关键。该值不会再显示。如果丢失了 API 密钥，您可以删除该密钥并创建新密钥：[管理服务标识 API 密钥](/docs/iam?topic=iam-serviceidapikeys#serviceidapikeys)。
{: tip}

## 制定价格套餐
{: #pricing-plan}

将服务上线到 {{site.data.keyword.Bluemix_notm}} 后，必须定义价格套餐。如果您对要如何向服务用户收费有详细的了解，那么可以在套餐中提供这些信息。但是，如果您尚未决定好如何设置付费套餐，那么可以先启用免费套餐，以后再回来设置付费套餐。

1. 在资源管理控制台中，单击**定价**页面。
2. 单击**添加套餐**以创建新的套餐条目，然后单击**编辑套餐**以编辑套餐。
   * **免费套餐**：所有产品都可以拥有一个免费轻量套餐，允许用户试用您的服务。免费套餐使用*轻量*作为**显示名称**，使用 *lite* 作为**编程名称**。对于**此套餐是否免费？**，指定**是**。单击**保存**。您的套餐将发布到 {{site.data.keyword.Bluemix_notm}}“目录”。
   * **预订套餐**：对于**此套餐是否免费？**，指定**否**。填写必填字段。
保留缺省**定价度量值**度量值。提供的此缺省度量值用于向用户收取一次性的月度费用。单击**保存**。您的套餐将发布到 {{site.data.keyword.Bluemix_notm}}“目录”。保存用于提交使用量的样本 curl 命令。
   * **计量套餐**：对于**此套餐是否免费？**，指定**否**。填写必填字段。
*删除*缺省**定价度量值**预订度量值。单击**添加其他度量值**，填写**添加定价度量值**页面，然后单击**添加度量值**。单击**保存**。您的套餐将发布到 {{site.data.keyword.Bluemix_notm}}“目录”。保存用于提交使用量的样本 curl 命令。有关选择正确度量值的帮助，请参阅[计量集成](/docs/third-party?topic=third-party-content-tasks#content-tasks)。
3. 现在，**定价**页面已标记为“完成”，指示您已满足此页面的最低完成需求。

服务提供者需要为所有计量套餐自动提交每小时使用量。有关更多信息，请参阅：[提交计量套餐的使用量](/docs/third-party?topic=third-party-submitusage#submitusage)。
{: tip}

## 将元数据导出为 JSON
{: #export-metadata}

现在，您已在资源管理控制台中定义服务，因此可以下载 catalog.json 文件，并将其用于指导 Open Service Broker 的开发。catalog.json 具有必须在代理程序中托管的元数据。这些值定义代理程序与 {{site.data.keyword.Bluemix_notm}} 平台（用于代理程序支持的服务和套餐）之间的合同。供应时不需要的所有其他目录元数据都存储在 {{site.data.keyword.Bluemix_notm}}“目录”中。对用于呈现仪表板的目录显示值（如链接、图标和 i18n 转换的元数据）的任何更新都会在资源管理控制台中进行。这些更新不会存放于代理程序中。代理程序中存储的任何元数据都不会显示在 {{site.data.keyword.Bluemix_notm}} 控制台或 {{site.data.keyword.Bluemix_notm}} CLI 中。控制台和 CLI 会返回在资源管理控制台内设置并存储在 {{site.data.keyword.Bluemix_notm}}“目录”中的内容。

1. 在资源管理控制台中，打开**部署**页面。
2. 单击**管理**。
3. 单击**下载定义**。

保存 `catalog.json` 文件。在下一部分中，将使用此文件来开发 Open Service Broker。

## 后续步骤
{: #cis2-next-steps}

加油！您已通过添加目录显示元数据，向 IAM 注册以及创建一个或多个价格套餐，定义了服务产品。接下来，可以采用导出的 JSON 并开始开发服务代理程序。请参阅[步骤 3：开发和托管服务代理程序](/docs/third-party?topic=third-party-step3-osb#step3-osb)。
