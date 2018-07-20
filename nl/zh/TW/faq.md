---

copyright:
  years: 2015, 2018
lastupdated: "2018-03-15"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# 常見問題 (FAQ)
{: #3p-faqs}

請參閱下列「常見問題」，以釐清常見問題。

## 方案的不同計量選項為何？
{: #metering}

{{site.data.keyword.Bluemix}} 支援聚集供應項目用量的多種模型。供應項目提供者會測量已佈建實例的各種度量值，並將這些測量提交給計量服務。分級服務會根據供應項目提供者所選擇的模型，將已提交的用量聚集到不同的儲存區（實例、資源群組及帳戶）。方案中所有度量值的聚集及分級模型包含在方案的計量及分級定義文件中。

**附註：**如果您提供計量方案，則需要使用計量服務 API 自動執行每小時用量提交。

如需計量的相關資訊，請參閱：[計量整合](/docs/third-party/metering.html#meteringintera)。

如需提交計量用量的相關資訊，請參閱：[提交計量方案的用量](/docs/third-party/submitusage.html#submitusage)

## 我遺失 {{site.data.keyword.Bluemix_notm}} Identity and Access Management API 金鑰。如何產生另一個 API 金鑰？
{: #iam-creds}

當您**啟用 IAM** 時，就會為您指定「API 金鑰」。您必須儲存「API 金鑰」。此值不會再次顯示。如果您遺失「API 金鑰」，則可以刪除該金鑰，然後建立新金鑰：[管理服務 ID API 金鑰](/docs/iam/serviceid_keys.html#serviceidapikeys)


