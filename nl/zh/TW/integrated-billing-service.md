---


copyright:
  years: 2018
lastupdated: "2018-07-20"


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

本主題介紹在 {{site.data.keyword.Bluemix}} 中開發及發佈協力廠商整合式計費服務所需的步驟。
{:shortdesc}

您獲准在 {{site.data.keyword.Bluemix_notm}} 型錄中提供供應項目之後，將會在資源管理主控台（一種引導式使用者介面體驗）中開始開發供應項目。您會設計型錄 meta 資料、設定服務定價方案，並與 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 整合。 

接下來，在資源管理主控台之外，您執行程式碼開發來建置及管理新的 Open Service Broker（將提供入門範本分配管理系統範例及 API 文件），而且您使用 IAM 來開發鑑別流程。完成這些步驟之後，您將回到資源管理主控台，以可讓您測試及驗證多個交付物需求的受限可見性模式，將服務部署至型錄。當您已準備好且供應項目符合所有需求時，您的服務將在 {{site.data.keyword.Bluemix_notm}} 型錄中變為完全可見！


## 處理程序運作方式
{: #process}

若要提供整合式計費服務，請使用 Provider Workbench、資源管理主控台及您選擇的開發環境。請參閱[核對清單](/docs/third-party/checklist.html#checklist)，以協助追蹤這些步驟。

這些步驟假設您已獲准提供「整合式計費服務」。如果您尚未在 PWB 中完成起始登錄及核准，則請參閱：[在 {{site.data.keyword.Bluemix_notm}} 中開始發佈協力廠商供應項目](/docs/third-party/index.md)
{: tip}

1. [建立文件及行銷公告](/docs/third-party/cis1-docs-marketing.html)。
2. [在資源管理主控台中定義供應項目{{site.data.keyword.Bluemix_notm}}](/docs/third-party/cis2-rmc-define.html)。
3. [開發及管理服務分配管理系統](/docs/third-party/cis3-broker.html)。
4. [開發鑑別流程](/docs/third-party/cis5-iam.html)。
5. [測試服務](/docs/third-party/cis4-rmc-publish.html)。
6. [公開發行服務](/docs/third-party/cis6-ga.html)。

## 支援
{: #support}

整合式計費服務需要協力廠商供應項目提供者自行提供支援模型。您的 IBM 業務代表可以協助啟用您的支援模型，並確保如果使用者透過 {{site.data.keyword.Bluemix_notm}} 支援中心開立問題單，則問題單會遞送至協力廠商支援中心網站。

## 持續更新
{: #maintain}

發行您的服務之後，您可以繼續反覆進行，直接與 {{site.data.keyword.Bluemix_notm}} 業務代表合作來進行更新。



