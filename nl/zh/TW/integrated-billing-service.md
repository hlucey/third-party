---


copyright:
  years: 2018
lastupdated: "2018-06-28"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 概觀：開發整合式計費服務
{: #overview}

本主題的設計旨在引導您完成在 {{site.data.keyword.Bluemix_notm}} 中開發及發佈協力廠商「整合式計費服務」所需的步驟。您獲准在 {{site.data.keyword.Bluemix_notm}} 型錄中提供供應項目之後，您將會在資源管理主控台（一種引導式使用者介面體驗）中開始開發供應項目。在資源管理主控台內，您將設計型錄 meta 資料、設定服務定價方案，以及與 IBM Cloud Access Management (IAM) 整合。接下來，在資源管理主控台外部，您將執行程式碼開發來建置及管理新的 Open Service Broker（將提供入門範本分配管理系統範例及 API 文件），而且您將使用 IAM 來開發鑑別流程。完成這些步驟之後，您將回到資源管理主控台，以可讓您測試及驗證多個可交付需求的受限可見性模式，將服務部署至型錄。當您備妥且供應項目符合所有需求時，您的服務將在 {{site.data.keyword.Bluemix_notm}} 型錄中變為完全可見！


## 我需要做什麼才能提供整合式計費服務？

您可以使用 PWB、資源管理主控台及您選擇的開發環境來實現這些目標。請參閱[核對清單](/docs/third-party/checklist.html#checklist)，以協助追蹤這些步驟。

下列步驟彙總高階的上線處理程序：

這些步驟假設您已獲准提供「整合式計費服務」。如果您尚未在 PWB 中完成起始登錄及核准，則請參閱：[在 {{site.data.keyword.Bluemix_notm}} 中開始發佈協力廠商供應項目](/docs/third-party/index.md)
{: tip}

1. [編寫：編寫服務文件及行銷公告 (PWB)](/docs/third-party/cis1-docs-marketing.html)
2. [定義：在資源管理主控台 {{site.data.keyword.Bluemix_notm}} 中定義供應項目](/docs/third-party/cis2-rmc-define.html)
3. [開發：使用 Open Service Broker API 規格開發及管理一個以上的服務分配管理系統](/docs/third-party/cis3-broker.html)
4. [IAM：開發鑑別流程 (OAuth)、驗證使用者授權 (v2/authz)，以及衍生重新導向 URI](/docs/third-party/cis5-iam.html)
5. [發佈及測試：將 OSB 連接至資源管理主控台、以有限可見性模式將服務發佈至 {{site.data.keyword.Bluemix_notm}} 型錄，然後測試供應項目](/docs/third-party/cis4-rmc-publish.html)。
6. [要求核准服務 GA](/docs/third-party/cis6-ga.html)

## 支援

整合式計費服務需要協力廠商服務提供者自行提供支援模型。您的 IBM 業務代表將協助啟用您的支援模型，並確保如果使用者開啟具有 {{site.data.keyword.Bluemix_notm}} 支援的問題單，則 {{site.data.keyword.Bluemix_notm}} 支援會將問題單遞送至協力廠商支援網站。

## 持續更新

發行您的服務之後，即可繼續反覆運算，並直接與 {{site.data.keyword.Bluemix_notm}} 業務代表合作來進行更新。



