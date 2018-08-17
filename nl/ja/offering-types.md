---


copyright:
  years: 2018
lastupdated: "2018-07-01"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# 第三者オファリング・タイプ
{: #offering-types}

{{site.data.keyword.Bluemix}} で第三者オファリングを統合請求サービスまたは紹介サービスとして提供することができます。
{:shortdesc}

第三者オファリングを統合請求サービスとして提供するということは、ユーザーが、{{site.data.keyword.Bluemix_notm}} コンソールのカタログ詳細ページにリストされているさまざまな IBM 料金プランから選択できることを意味します。さらに、ユーザーは、第三者オファリングのインスタンスを自動的に作成することができます。

第三者オファリングを紹介サービスとして提供した場合、ユーザーは、{{site.data.keyword.Bluemix_notm}} コンソールのカタログ詳細ページから、サービス提供者の Web サイトに誘導されます。その Web サイトから、ユーザーはアカウントを作成し、第三者オファリングを、{{site.data.keyword.Bluemix_notm}} で作成しているアプリにプログラマチックに接続する必要がある適切な資格情報を取得します。

## オファリング・タイプの比較
{: #compare}

次の表は、第三者オファリング・タイプの詳細な比較を示しています。

|  | 統合請求サービス  | 紹介サービス |
|---|---|---|
| **オンボーディング** | オンボーディングは、Provider Workbench (PWB) およびリソース管理コンソールから処理されます。オファリング・プロバイダーは、Open Service Broker を作成してそれをホストおよびテストし、一連のセルフサービス・ステップからオファリングを公開する責任があります。| オンボーディングは、Provider Workbench から処理されます。セルフサービス・オンボーディング・プロセスには約 2 週間かかります。|
| **デプロイ** | {{site.data.keyword.Bluemix_notm}} プラットフォームによってプロビジョンされます | API ベースのサービスのみ |
| **請求処理**  |  統合請求処理モデルでは、ユーザーは、IBM オファリングおよび統合された第三者オファリングの両方に対して 1 つの請求書を受け取ります。| 紹介モデルでは、プロバイダーがユーザーに請求書を出し、収益の 100% を保持します。 |
| **例** | [PowerAI](https://console.bluemix.net/catalog/services/powerai) | [Accern API](https://console.bluemix.net/catalog/services/accern-api) |
{: caption="表 1. 第三者オファリング・タイプの比較" caption-side="top"}

