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
{:download: .download}

# 概述：开发 Integrated Billing 服务
{: #overview}

本主题介绍了在 {{site.data.keyword.Bluemix}} 中开发和发布第三方 Integrated Billing 服务所需的步骤。
{:shortdesc}

您获得批准在 {{site.data.keyword.Bluemix_notm}}“目录”中交付产品后，将在资源管理控制台中开始开发产品，这是指导式 UI 体验。您将设计目录元数据，设置服务价格套餐，以及与 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 相集成。 

接下来，在资源管理控制台外部，您将执行代码开发以构建和托管新的 Open Service Broker。这将提供入门模板代理程序样本和 API 文档，并且您可使用 IAM 来开发认证流程。完成这些步骤后，您将返回到资源管理控制台，以有限可视性方式将服务部署到目录中，借此您可测试和验证可交付产品需求。准备就绪并且产品满足所有需求时，服务将在 {{site.data.keyword.Bluemix_notm}}“目录”中完全可视！


## 过程工作方式
{: #process}

要交付 Integrated Billing 服务，您可使用 Provider Workbench、资源管理控制台和所选开发环境。请参阅[核对表](/docs/third-party?topic=third-party-checklist#checklist)以帮助跟踪这些步骤。

这些步骤假定您已获得批准，可交付 Integrated Billing 服务。如果您尚未完成 PWB 中的初始注册和批准，请参阅：[在 {{site.data.keyword.Bluemix_notm}} 中发布第三方产品入门](/docs/third-party/index.md?topic=third-party-get-started#get-started)
{: tip}

1. [创建文档和市场营销公告](/docs/third-party?topic=third-party-content-tasks#content-tasks)。
2. [在资源管理控制台中定义产品{{site.data.keyword.Bluemix_notm}}](/docs/third-party?topic=third-party-step2-define#step2-define)。
3. [开发和托管服务代理程序](/docs/third-party?topic=third-party-step3-osb#step3-osb)。
4. [开发认证流程](/docs/third-party?topic=third-party-step4-iam#step4-iam)。
5. [测试服务](/docs/third-party?topic=third-party-step5-pubtest#step5-pubtest)。
6. [公开发布服务](/docs/third-party?topic=third-party-public-releasing#public-releasing)。

## 支持
{: #support}

Integrated Billing 服务需要第三方产品提供者提供自己的支持模型。IBM 代表可帮助您启用支持模型，并确保如果用户向 {{site.data.keyword.Bluemix_notm}} 支持人员开具凭单，该凭单会传递到第三方支持站点。

## 持续更新
{: #maintain}

发布服务后，可以通过直接与 {{site.data.keyword.Bluemix_notm}} 代表合作来继续对服务进行迭代和更新。



