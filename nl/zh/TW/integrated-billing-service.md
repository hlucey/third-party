---

copyright:

  years: 2018, 2019

lastupdated: "2019-02-25"

keywords: billing service, resource management console, IBM Cloud, RMC, 

subcollection: third-party

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

接下來，在資源管理主控台之外，執行程式碼開發來建置及管理新的 Open Service Broker。提供入門範本分配管理系統範例和 API 文件，您可以使用 IAM 來開發鑑別流程。完成這些步驟之後，您會回到資源管理主控台，以受限可見性模式（可讓您測試及驗證交付項目需求）將服務部署至型錄。當您已準備好且供應項目符合所有需求時，您的服務將在 {{site.data.keyword.Bluemix_notm}} 型錄中變為完全可見！


## 處理程序運作方式
{: #process}

若要提供整合式計費服務，請使用 Provider Workbench、資源管理主控台及您選擇的開發環境。請參閱[核對清單](/docs/third-party?topic=third-party-checklist#checklist)，以協助追蹤這些步驟。

這些步驟假設您已獲准提供「整合式計費」服務。如果您尚未在 PWB 中完成起始登錄及核准，則請參閱：[在 {{site.data.keyword.Bluemix_notm}} 中開始發佈協力廠商供應項目](/docs/third-party/index.md?topic=third-party-get-started#get-started)
{: tip}

1. [建立文件及行銷公告](/docs/third-party?topic=third-party-content-tasks#content-tasks)。
2. [在資源管理主控台定義供應項目{{site.data.keyword.Bluemix_notm}}](/docs/third-party?topic=third-party-step2-define#step2-define)。
3. [開發及管理服務分配管理系統](/docs/third-party?topic=third-party-step3-osb#step3-osb)。
4. [開發鑑別流程](/docs/third-party?topic=third-party-step4-iam#step4-iam)。
5. [測試服務](/docs/third-party?topic=third-party-step5-pubtest#step5-pubtest)。
6. [公開發行服務](/docs/third-party?topic=third-party-public-releasing#public-releasing)。

## 支援
{: #support}

整合式計費服務需要協力廠商供應項目提供者自行提供支援模型。您的 IBM 業務代表可以協助您啟用支援模型，並確保如果使用者透過 {{site.data.keyword.Bluemix_notm}} 支援中心開立問題單，則問題單會遞送至協力廠商支援中心網站。

## 持續更新
{: #maintain}

發行您的服務之後，您可以繼續反覆進行，直接與 {{site.data.keyword.Bluemix_notm}} 業務代表合作來進行更新。



