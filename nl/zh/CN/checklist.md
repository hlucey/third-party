---

copyright:
  years: 2018
lastupdated: "2018-07-02"

---

{:right: .ph data-hd-position='right'}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}

# 端到端核对表
{: #checklist}

使用以下核对表来跟踪定义、开发和发布 Integrated Billing 服务所需的所有任务。

## 定义产品

|任务|子任务|描述
|环境|
|------| ----------| ------------|-----|
|了解有关 {{site.data.keyword.Bluemix_notm}} 平台的信息。|☐ 我了解供应层、{{site.data.keyword.Bluemix_notm}} IAM、目录、OSB 和计量服务如何一起协作以用于 {{site.data.keyword.Bluemix_notm}} 平台。|与 {{site.data.keyword.Bluemix_notm}} 引荐服务不同，Integrated Billing 服务使用 {{site.data.keyword.Bluemix_notm}} 平台来创建、绑定和删除服务实例以及收取服务实例的费用。[了解](/docs/third-party/platform.html#what-is-the-ibm-cloud-platform-)组成该平台的关键组成部分的信息以快速开始开发！|文档|
|在 PWB 中注册|☐ 在 PWB 中完成了**内容任务**<br><br>☐ 我已获得批准，可将我的产品作为 Integrated Billing 服务发布<br><br> ☐ 我收到了一封初始电子邮件，其中包含我的文档 URL 值<br><br> |第一步是向 {{site.data.keyword.Bluemix_notm}} PWB 注册您的产品。有关完成此任务的更多信息，请参阅[入门教程](/docs/third-party/index.html#get-started)。|PWB|
|编写并发布 {{site.data.keyword.Bluemix_notm}} 文档|☐ 我已在 PWB 中启动**指导任务（文档）**<br><br>☐ 我已获取`文档 URL`<br><br> ☐ 我已成功发布文档<br><br> |我们知道您在自己 Web 站点上托管的第三方文档非常棒。但是，现在您要在 {{site.data.keyword.Bluemix_notm}} 中交付 Integrated Billing 服务，因此您需要交付针对 {{site.data.keyword.Bluemix_notm}} Integrated Billing 体验定制的文档。PWB 将指导您完成此任务，并帮助您将文档发布到 https://console.bluemix.net/docs/。有关完成此任务的更多信息，请参阅：[创建入门文档](/docs/third-party/cis1-docs-marketing.html#docs)|PWB|
|编写并发布市场营销公告|☐ 我已在 PWB 中启动**市场营销任务（公告）**<br><br>  ☐ 我已成功发布公告<br><br>  |创建市场营销宣传材料，以通过 {{site.data.keyword.Bluemix_notm}} 新闻稿和社交媒体渠道公告您服务的可用性。PWB 将指导您完成此任务。有关更多详细信息，请参阅：[创建入门文档](/docs/third-party/cis1-docs-marketing.html#announcement)|PWB|
|在资源管理控制台中注册服务|☐ 我已将唯一且有意义的 `service-name` 定义为**资源名称**<br><br>  ☐ 我已在资源管理控制台中成功保存并验证记录<br><br>  |资源管理控制台将帮助您创建唯一的产品。请遵循[指南](/docs/third-party/cis2-rmc-define.html#register-your-offering-by-using-the-resource-management-console-rmc-)来注册您的产品。|资源管理控制台|
|完成资源管理控制台中的**产品**页面|☐ 使用在 PWB 产品电子邮件中提供的值，我已正确设置**文档 URL** 和**指令 URL**<br><br>  ☐ 我已提供**服务条款** URL，但该 URL 并不是公司 TOS 页面，而是没有计费或付费条款的独特 TOS 页面。<br><br>  ☐ 我了解并正确指定了是否**支持套餐更改？**已启用。☐ 我了解并正确指定了我的服务是否**可绑定**。|在资源管理控制台中提供将在 {{site.data.keyword.Bluemix_notm}} 磁贴中显示的目录元数据，包括关键 URL（如服务条款），以及有关产品的有意义的详细信息（如带项目符号的信息等）。请遵循[指南](/docs/third-party/cis2-rmc-define.html#enter-your-offering-metadata-rmc-offering-page-)来设置产品的必需和建议目录元数据。|资源管理控制台|
|完成资源管理控制台中的**访问管理**页面|☐ 我已成功启用 IAM<br><br>  ☐ 我已保存资源管理控制台 UI 为我创建的一次性生成的 IAM API 密钥，并且我了解该 API 密钥不会存储在资源管理控制台中，因此日后我无法检索该密钥。<br><br> ☐ 我了解在后续步骤中开发并托管 OSB，然后派生重定向 URI 之后，才能完成“访问管理”页面。<br><br> ☐ 创建并托管 OSB 之后，我返回到 IAM 页面，通过单击**添加重定向 URI** 并添加派生值成功完成了该页面。|在资源管理控制台中，向 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 注册您的产品。通过 IAM，您可以在整个 {{site.data.keyword.Bluemix_notm}} 平台上安全地对两个平台服务的用户进行认证并一致地控制对资源的访问权。（您将返回并启用重定向 URI）。请遵循[指南](/docs/third-party/cis2-rmc-define.html#register-with-identity-and-access-management-rmc-iam-page-)来启用产品的初始访问管理。|资源管理控制台|
|在资源管理控制台中开发一个或多个价格套餐|☐ 我已提供具有唯一名称的免费套餐。<br><br>  ☐（可选）我与 IBM 代表合作，定义了付费套餐（预订或计量），并且我了解为了创建计量套餐，我必须除去缺省预订套餐。<br><br> ☐（可选）我了解计量套餐需要我使用 {{site.data.keyword.Bluemix_notm}} 平台计量服务来托管并开发自动提交每小时使用量的功能。|您将如何对您的产品收费？资源管理控制台提供免费套餐或付费（预订和计量）套餐。请遵循[指南](/docs/third-party/cis2-rmc-define.html#develop-a-pricing-plan-rmc-pricing-page-)来定义产品的价格套餐。|资源管理控制台|
|从资源管理控制台中导出目录元数据|☐ 我了解在资源管理控制台的**产品**和**定价**页面中提供的某些元数据必须在 OSB 中导出并提供。通过从资源管理控制台导出值，可以映射资源管理控制台为我生成的关键 GUID（例如，我的服务和套餐标识），并在 OSB 中提供这些 GUID，以便平台供应层可以从 `catalog GET` 端点的响应中读取此供应合同。<br><br>  ☐ 我已从资源管理控制台的**部署**页面中获取 `catalog.json` 文件，并且已准备好将服务数组映射到 OSB 中的元数据。<br><br> |现在，您已在资源管理控制台中定义服务，因此可以下载 catalog.json 文件，并将其用于通知 Open Service Broker 的开发。catalog.json 包含必须在代理程序中托管的元数据。这些值定义代理程序与 IBM Cloud 平台之间的合同，用于提供代理程序支持的服务和套餐。请遵循[指南](/docs/third-party/cis2-rmc-define.html#export-your-metadata-as-json-rmc-deployments-page-)来导出目录元数据。|资源管理控制台|
{: caption="表 1. 定义 Integrated Billing 产品" caption-side="top"}

## 开发产品

|任务|子任务|描述
|环境|
|------| ----------| ------------|-----|
|了解 Open Service Broker (OSB) V2.12 规范|☐ 我已通读 OSB 规范，并了解我必须开发自己的 OSB。<br><br>  |服务代理程序用于管理服务的生命周期。{{site.data.keyword.Bluemix_notm}} 平台与 Open Service Broker 进行交互，以供应和管理服务实例（服务产品的实例化）和服务绑定（应用程序与服务实例之间的关联的表示，通常包含应用程序将用于与服务实例进行通信的凭证）。[了解](/docs/third-party/cis3-broker.html#become-familiar-with-the-osb-specification) V2.12 规范|文档|
|查看 {{site.data.keyword.Bluemix_notm}} 代理程序样本|☐ 我已克隆存储库，浏览了代理程序样本，并准备好使用这些样本来开始开发。<br><br>  |  [https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") |代码示例|
|查看 {{site.data.keyword.Bluemix_notm}} Open Service Broker API 文档|☐ 我了解有多个必需端点必须得到 OSB 中代码的支持。<br><br>  ☐ 我了解，如果我的服务可以绑定到 {{site.data.keyword.Bluemix_notm}} 中的应用程序，该服务必须能够将 API 端点和凭证返回给服务使用者。<br><br> ☐ 我了解 {{site.data.keyword.Bluemix_notm}} 定义了扩展 API 端点，允许禁用和重新启用服务实例。我必须扩展 OSB 并定义**启用和禁用实例（GET 和 PUT）**|{{site.data.keyword.Bluemix_notm}} Open Service Broker 扩展了 Open Service Broker 2.12 规范。[了解](/docs/third-party/cis3-broker.html#view-our-resource-broker-api-documentation)有关代理程序必须使用的必需端点的信息|文档|
|使用目录元数据开始开发代理程序|☐ 我了解在资源管理控制台的**产品**和**定价**页面中提供的某些元数据必须在 OSB 中导出并提供。通过从资源管理控制台导出值，可以映射资源管理控制台为我生成的关键 GUID（例如，我的服务和套餐标识），并在 OSB 中提供这些 GUID，以便平台供应层可以从 `catalog GET` 端点的响应中读取此供应合同。<br><br>  ☐ 我已将 `catalog.json` 文件中列出的必需 GUID 和其他必需值添加到样本 OSB 中的服务数组。|从资源管理控制台下载 `catalog.json` 文件后，您可以将其用于通知 Open Service Broker 的开发。catalog.json 包含必须在代理程序中托管的元数据。这些值定义代理程序与 IBM Cloud 平台之间的供应合同，用于提供代理程序支持的服务和套餐。请遵循[指南](/docs/third-party/cis3-broker.html#learn-how-to-use-the-exported-metadata-to-guide-your-broker-development)将导出的目录元数据添加到 OSB。|开发环境和文档|
|托管 OSB|☐ 我了解，代理程序的托管位置必须遵循传输层安全性 (TLS) 协议 V1.2。此外，代理程序必须在可通过公用因特网访问的有效 HTTPS 端点上进行托管。<br><br> |代理程序必须作为可响应 REST API 调用的应用程序的一部分进行托管。托管位置必须符合 IBM Cloud 安全准则。请遵循[指南](/docs/third-party/cis3-broker.html#host-your-brokers)来托管代理程序。|开发环境和文档|
|测试托管的 OSB|☐ 我已通过对托管代理程序运行 curl 命令并验证响应，从而验证代理程序支持的每个 API 端点。<br><br> |您应该通过对要启用的不同端点运行 curl 命令来验证代理程序。请遵循[指南](/docs/third-party/cis3-broker.html#how-to-test-your-service-s-broker)来托管代理程序。|开发环境和文档|
|派生并设置 IAM 重定向 URI|☐ 我已使用 OSB 的托管位置和一些认证信息成功派生 IAM 重定向 URL。<br><br> ☐ 我已通过指定**重定向 URI** 并正确设置客户机标识，成功完成资源管理控制台的**访问管理**页面。<br><br> |在资源管理控制台中定义服务时，您已生成客户机标识，但请注意，此时您可能并没有重定向 URI。这意味着 IAM 创建的是设置为 `false` 的客户机标识。在使用**重定向 URI** 返回到资源管理控制台之前，您不会拥有设置为 true 的客户机标识。请遵循[指南](/docs/third-party/cis5-iam.html#derive-your-iam-redirect-uri-resource-management-console-iam-page-)来派生并设置 IAM 重定向 URI。|开发环境和资源管理控制台|
|开发用于认证的 OAuth 流程|☐ 我了解 IAM 支持 Open ID Connect (OIDC)。<br><br> ☐ 我已发现 IAM 区域端点，成功地将用户从 `dashboard_url` 重定向到我的已组合重定向 URI，并且我存储了响应中返回的用户 `access_token`，以便可以在认证期间使用。<br><br> |必须正确认证访问您的服务仪表板的用户。使用 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 开发 Open Authorization 基于令牌的认证和授权。请遵循[指南](/docs/third-party/cis5-iam.html#oauth)来开发用于认证的 OAuth 流程。|开发环境和文档|
|验证用户授权|☐ 我可以与 IAM 通信以获取 API 密钥的访问令牌。<br><br> ☐ 我能够验证是否授予用户对服务实例的权限 (/v2/authz POST)。<br><br> |在开发用于认证的 OAuth 流程后，必须验证是否会正确地对用户进行授权，从而确保服务的用户能够访问服务仪表板。请遵循[指南](/docs/third-party/cis5-iam.html#validate)来验证用户授权。|开发环境和文档|
{: caption="表 2. 开发 Integrated Billing 产品" caption-side="top"}

## 发布和测试产品

|任务|子任务|描述
|环境|
|------| ----------| ------------|-----|
|以有限可视性方式发布产品|☐ 我已在资源管理控制台的**部署**页面中成功注册托管的 OSB。<br><br> ☐ 我已在资源管理控制台的**部署**页面中成功创建新部署，并已将产品发布到一个或多个区域。<br><br> |现在，您已拥有满足 OSB 规范的托管代理程序，您可以返回到资源管理控制台以将服务发布到 {{site.data.keyword.Bluemix_notm}}“目录”。请遵循[指南](/docs/third-party/cis4-rmc-publish.html#publish-your-service-to-ibm-cloud)，以有限可视性方式来发布产品。|资源管理控制台|
|测试产品|☐ 使用白名单帐户登录后，我可以在 https://console.bluemix.net 目录中看到我的服务。<br><br> ☐ 我已在服务实例仪表板中成功验证认证。<br><br> ☐ 我已成功验证产品在目录中会正确显示。<br><br> ☐ 我已成功验证供应可正常工作；我可以选择套餐并创建服务实例。<br><br> ☐ 我已成功验证取消供应可正常工作；我可以删除服务实例。<br><br> ☐ 我已成功验证绑定可正常工作；我可以单击**连接**并将我的服务连接到其他应用程序。<br><br> ☐ 我已成功验证取消绑定可正常工作；我可以断开与服务的连接并删除连接。<br><br>  ☐ 我已成功验证“创建服务密钥”和“删除服务密钥”可正常工作；我可以单击**凭证**，生成服务密钥，以及删除该服务密钥。<br><br> ☐ 我与 IBM 代表合作，验证了我的产品可正确支持启用和禁用端点。<br><br> ☐ 由于我的产品具有计量套餐，因此我已通过对使用量 API 执行 curl 并正确返回基于使用量的准确定价，以及启用自动提交每小时使用量的功能，成功测试了使用量提交工作，从而支持供应我服务的实例的所有用户。|现在，您已拥有满足 OSB 规范的托管代理程序，您可以返回到资源管理控制台以将服务发布到 {{site.data.keyword.Bluemix_notm}}“目录”。请遵循[指南](/docs/third-party/cis4-rmc-publish.html#test-your-deployed-offering)来测试部署的服务。|{{site.data.keyword.Bluemix_notm}} 控制台|
{: caption="表 3. 发布和测试 Integrated Billing 产品" caption-side="top"}

