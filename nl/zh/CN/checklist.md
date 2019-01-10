---

copyright:
  years: 2018
lastupdated: "2018-09-04"

---

{:right: .ph data-hd-position='right'}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# 端到端核对表
{: #checklist}

使用以下核对表来跟踪定义、开发和发布 Integrated Billing 服务所需的所有任务。
{:shortdesc}

## 定义服务
{: #define}

|任务|子任务|描述
|环境|
|------| ----------| ------------|-----|
|了解有关 {{site.data.keyword.Bluemix}} 平台的信息。|☐ 我了解供应层、{{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM)、目录、Open Service Broker 和计量服务如何一起协作。|与 {{site.data.keyword.Bluemix_notm}} 引荐服务不同，Integrated Billing 服务使用 {{site.data.keyword.Bluemix_notm}} 平台来创建、绑定和删除服务实例以及收取服务实例的费用。[了解](/docs/third-party/platform.html#how-it-works)该平台包含的关键组件的信息以快速开始开发。|文档|
|在 {{site.data.keyword.Bluemix_notm}} Provider Workbench 中注册您的产品。| ☐ 我完成了内容任务。<br><br>☐ 我收到了批准，可将我的产品作为 Integrated Billing 服务发布。<br><br> ☐ 我收到了一封电子邮件，其中包含我的文档 URL 值。<br><br> |第一步是在 Provider Workbench 中注册您的产品。有关更多信息，请参阅[入门教程](/docs/third-party/index.html#get-started)。|Provider Workbench|
|发布 {{site.data.keyword.Bluemix_notm}} 文档。|☐ 我已在 Provider Workbench 中启动指导任务。<br><br>☐ 我收到了`文档 URL`。<br><br> ☐ 我已成功发布文档。<br><br> |我们知道您在自己 Web 站点上托管的第三方文档非常棒。但是，现在您要在 {{site.data.keyword.Bluemix_notm}} 中交付 Integrated Billing 服务，因此您需要交付针对 {{site.data.keyword.Bluemix_notm}} Integrated Billing 体验定制的文档。有关更多信息，请参阅[创建文档](/docs/third-party/cis1-docs-marketing.html#docs)。|Provider Workbench|
|发布市场营销公告。|☐ 我已在 Provider Workbench 中启动市场营销任务。<br><br>  ☐ 我已成功发布市场营销公告。<br><br>  |创建市场营销宣传材料，以通过 {{site.data.keyword.Bluemix_notm}} 新闻稿和社交媒体渠道公告您服务的可用性。有关更多信息，请参阅[创建市场营销公告](/docs/third-party/cis1-docs-marketing.html#announcement)。|Provider Workbench|
|在资源管理控制台中注册您的产品。|☐ 我已将唯一且有意义的 `service-name` 定义为资源名称。<br><br>  ☐ 我已在资源管理控制台中成功验证我有记录。<br><br>  |您可使用资源管理控制台来创建唯一的产品。有关更多信息，请参阅[注册产品的步骤](/docs/third-party/cis2-rmc-define.html#register)。|资源管理控制台|
|完成资源管理控制台中的“产品”页面。|☐ 使用在 Provider Workbench 产品电子邮件中提供的值，我已正确设置文档 URL 和指示信息 URL。<br><br>  ☐ 我已提供指向唯一“服务条款”页面的 URL，该页面中不包含计费或付费条款。<br><br>  ☐ 我了解并正确指定了是否**支持套餐更改？**已启用。☐ 我了解并正确指定了我的服务是否可绑定。|在资源管理控制台中提供 {{site.data.keyword.Bluemix_notm}} 磁贴上显示的目录元数据。有关更多信息，请参阅[输入产品元数据的步骤](/docs/third-party/cis2-rmc-define.html#offering-metadata)。|资源管理控制台|
|完成资源管理控制台中的“访问管理”页面。|☐ 我已成功启用 IAM。<br><br>  ☐ 我已保存为我创建的一次性生成的 IAM API 密钥。我了解该 API 密钥不会存储在资源管理控制台中，因此日后我无法检索该密钥。<br><br> ☐ 我了解在开发并托管 Open Service Broker，然后派生重定向 URI 之后，才能完成“访问管理”页面。<br><br> ☐ 托管 Open Service Broker 之后，我返回到 IAM 页面，并成功完成了该页面。|在资源管理控制台中向 {{site.data.keyword.Bluemix_notm}} IAM 注册您的产品。通过 IAM，您可以在整个 {{site.data.keyword.Bluemix_notm}} 平台上安全地对两个平台服务的用户进行认证并一致地控制对资源的访问权。有关更多信息，请参阅[向 IAM 注册的步骤](/docs/third-party/cis2-rmc-define.html#reg-iam)。|资源管理控制台|
|在资源管理控制台中开发一个或多个价格套餐。|☐ 我已提供具有唯一名称的免费套餐。<br><br>  ☐（可选）我与 IBM 代表合作，定义了付费套餐（预订或计量），并且我了解必须除去缺省预订套餐，才能创建计量套餐。<br><br> ☐（可选）我了解需要我托管并开发自动提交每小时使用量的功能。|您将如何对您的服务收费？资源管理控制台提供免费套餐或付费套餐。有关更多信息，请参阅[制定价格套餐的步骤](/docs/third-party/cis2-rmc-define.html#pricing-plan)。|资源管理控制台|
|从资源管理控制台中导出目录元数据。|☐ 我了解在资源管理控制台的“产品”和“定价”页面中提供的某些元数据必须导出并在 Open Service Broker 中提供。<br><br>  ☐ 我已从“部署”页面中获取 `catalog.json` 文件，并且已准备好将服务数组映射到 Open Service Broker 中的元数据。<br><br> |现在，您已在资源管理控制台中定义服务，因此可以下载 `catalog.json` 文件，并将其用于通知 Open Service Broker 的开发。有关更多信息，请参阅[导出元数据的步骤](/docs/third-party/cis2-rmc-define.html#export-metadata)。|资源管理控制台|
{: caption="表 1. 定义 Integrated Billing 服务" caption-side="top"}

## 开发服务
{: #develop}

|任务|子任务|描述
|环境|
|------| ----------| ------------|-----|
|了解 Open Service Broker V2.12 规范。|☐ 我已通读 Open Service Broker 规范，并了解我必须开发自己的 Open Service Broker。<br><br>  |服务代理程序用于管理服务的生命周期。{{site.data.keyword.Bluemix_notm}} 平台会与 Open Service Broker 进行交互，以创建和管理服务实例和服务绑定。有关更多信息，请参阅[开发和托管服务代理程序](/docs/third-party/cis3-broker.html#step3-osb)。|文档|
|查看 {{site.data.keyword.Bluemix_notm}} 代理程序样本。|☐ 我已克隆存储库，浏览了代理程序样本，并准备好使用这些样本来开始开发。<br><br>  |  [https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") |代码示例|
|查看 {{site.data.keyword.Bluemix_notm}} Open Service Broker API 文档。|☐ 我了解有多个必需端点必须得到 Open Service Broker 中代码的支持。<br><br>  ☐ 我了解，如果我的服务可以绑定到 {{site.data.keyword.Bluemix_notm}} 中的应用程序，该服务必须将 API 端点和凭证返回给服务用户。<br><br> ☐ 我了解 {{site.data.keyword.Bluemix_notm}} 定义了扩展 API 端点，允许禁用和重新启用服务实例。|{{site.data.keyword.Bluemix_notm}} Open Service Broker 扩展了 Open Service Broker 2.12 规范。[了解](/docs/third-party/cis3-broker.html#docs)有关代理程序必须使用的必需端点的信息。|文档|
|使用目录元数据开始开发服务代理程序。|☐ 我了解在资源管理控制台中提供的某些元数据必须导出并在 Open Service Broker 中提供。<br><br>  ☐ 我已将必需的 GUID 以及 `catalog.json` 文件中列出的其他必需值添加到样本 Open Service Broker 中的服务数组。|从资源管理控制台下载 `catalog.json` 文件后，可以将其用于通知 Open Service Broker 的开发。有关更多信息，请参阅[使用导出的元数据指导开发的步骤](/docs/third-party/cis3-broker.html#use-metadata)。|开发环境和文档|
|托管 Open Service Broker。|☐ 我了解服务代理程序的托管位置必须遵循传输层安全性 (TLS) 协议 V1.2。<br><br> |服务代理程序必须作为可响应 REST API 调用的应用程序的一部分进行托管。托管位置必须符合 {{site.data.keyword.Bluemix_notm}} 安全准则。有关更多信息，请参阅[托管服务代理程序的步骤](/docs/third-party/cis3-broker.html#host)。|开发环境和文档|
|测试托管的 Open Service Broker。|☐ 我已通过对托管的服务代理程序运行 curl 命令，验证了服务代理程序支持的每个 API 端点。<br><br> |通过对要启用的不同端点运行 curl 命令来验证服务代理程序。有关更多信息，请参阅[测试服务代理程序的步骤](/docs/third-party/cis3-broker.html#test)。|开发环境和文档|
|派生并设置 IAM 重定向 URI。|☐ 我已使用 Open Service Broker 的托管位置和一些认证信息成功派生 IAM 重定向 URI。<br><br> ☐ 我已通过指定重定向 URI 并正确设置客户机标识，成功完成“访问管理”页面。<br><br> |在资源管理控制台中定义服务时，您会生成客户机标识，但请注意，此时您可能并没有重定向 URI。客户机标识设置为 `false`。在使用“重定向 URI”返回到资源管理控制台之前，您不会拥有设置为 true 的客户机标识。有关更多信息，请参阅[派生重定向 URI 的步骤](/docs/third-party/cis5-iam.html#redirect-uri)。|开发环境和资源管理控制台|
|开发用于认证的开放授权 (OAuth) 流程。|☐ 我了解 IAM 支持 Open ID Connect (OIDC)。<br><br> ☐ 我已发现 IAM 区域端点，成功地将用户从 `dashboard_url` 重定向到我的已组合重定向 URI，并且我存储了响应中返回的用户 `access_token`，以便可以在认证期间使用。<br><br> |必须正确认证访问您的服务仪表板的用户。使用 IAM 开发基于 OAuth 令牌的认证和授权。有关更多信息，请参阅[开发 OAuth 流程的步骤](/docs/third-party/cis5-iam.html#oauth)。|开发环境和文档|
|验证用户授权。|☐ 我可以获取 API 密钥的访问令牌。<br><br> ☐ 我可以验证用户对服务实例的权限。<br><br> |在开发用于认证的 OAuth 流程后，必须验证是否会正确地对用户进行授权，从而确保服务的用户可以访问服务仪表板。有关更多信息，请参阅[验证的步骤](/docs/third-party/cis5-iam.html#validate)。|开发环境和文档|
{: caption="表 2. 开发 Integrated Billing 服务" caption-side="top"}

## 发布和测试服务
{: #pubtest}

|任务|子任务|描述
|环境|
|------| ----------| ------------|-----|
|以有限可视性方式发布服务。|☐ 我已在资源管理控制台的“部署”页面中成功注册托管的 Open Service Broker。<br><br> ☐ 我已成功创建新部署，并已将产品发布到一个或多个区域。<br><br> |现在，托管的服务代理程序符合 Open Service Broker 规范，因此您可以将服务发布到 {{site.data.keyword.Bluemix_notm}}“目录”。有关更多信息，请参阅[发布服务的步骤](/docs/third-party/cis4-rmc-publish.html#publish)。|资源管理控制台|
|测试产品。| ☐ 我可以在目录中看到我的服务。<br><br> ☐ 我已在服务实例仪表板中验证认证。<br><br> ☐ 我已验证我的服务在目录中会正确显示。<br><br> ☐ 我可以选择套餐并创建服务实例。<br><br> ☐ 我可以删除服务实例。<br><br> ☐ 我可以将服务连接到其他应用程序。<br><br> ☐ 我可以断开与服务的连接，然后删除连接。<br><br>  ☐ 我可以生成服务密钥，也可以删除该服务密钥。<br><br> ☐ 我与 IBM 代表合作，验证了我的产品可正确支持启用和禁用端点。<br><br> ☐ 因为我的产品具有计量套餐，所以我已成功测试使用量提交。|现在，托管的服务代理程序符合 Open Service Broker 规范，因此您可以将服务发布到 {{site.data.keyword.Bluemix_notm}}“目录”。有关更多信息，请参阅[测试服务的步骤](/docs/third-party/cis4-rmc-publish.html#test)。|{{site.data.keyword.Bluemix_notm}} 控制台|
{: caption="表 3. 发布和测试 Integrated Billing 服务" caption-side="top"}

