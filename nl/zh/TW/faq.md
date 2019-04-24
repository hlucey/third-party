---

copyright:
  years: 2015, 2019
lastupdated: "2019-01-30"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}
{:faq: data-hd-content-type="faq"}
{:note: .note}

# 常見問題 (FAQ)
{: #3p-faqs}

## 方案有哪些不同的計量選項？
{: #metering}
{: faq}

{{site.data.keyword.Bluemix}} 支援多種模型以便聚集供應項目用量。供應項目提供者會測量已佈建實例的各種度量值，並將這些測量值提交給計量服務。分級服務會根據供應項目提供者所選擇的模型，將已提交的用量聚集到不同的儲存區（實例、資源群組及帳戶）。方案中所有度量值的聚集及分級模型包含在方案的計量及分級定義文件中。

如果您提供計量方案，則必須使用計量服務 API 自動執行每小時用量提交。
{: note}

如需計量的相關資訊，請參閱[計量整合](/docs/third-party?topic=third-party-meteringintera#meteringintera)。如需提交計量用量的相關資訊，請參閱[提交計量方案的用量](/docs/third-party?topic=third-party-submitusage#submitusage)。

## 如何產生新的 {{site.data.keyword.Bluemix_notm}} Identity and Access Management API 金鑰？
{: #iam-creds}
{: faq}

當您啟用 IAM 時，就會提供「API 金鑰」給您。您務必要儲存「API 金鑰」。此值不會再次顯示。如果您遺失「API 金鑰」，則可以刪除該金鑰，然後建立新的金鑰。如需相關資訊，請參閱[管理服務 ID API 金鑰](/docs/iam?topic=iam-serviceidapikeys#serviceidapikeys)。 


