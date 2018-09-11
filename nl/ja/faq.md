---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-28"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# FAQ
{: #3p-faqs}

## 各プランの各種計量オプションを教えてください。
{: #metering}

{{site.data.keyword.Bluemix}} は、オファリング使用量を集計するための複数のモデルをサポートしています。 オファリング・プロバイダーは、プロビジョン済みインスタンスの各種メトリックを測定し、それらの測定値を計量サービスに送信します。 レーティング・サービスは、そのオファリング・プロバイダーが選択したモデルに基づいて、送信された使用量をさまざまなバケット (インスタンス、リソース・グループ、およびアカウント) に集計します。 プラン内のすべてのメトリックの集計およびレーティングのモデルは、そのプランの計量およびレーティングの定義文書に含まれています。

**注:** 従量制プランを提供する場合は、計量サービス API を使用して、毎時の使用量の送信を自動化する必要があります。

計量について詳しくは、[計量の統合](/docs/third-party/metering.html#meteringintera)を参照してください。 計量される使用量の送信について詳しくは、[従量制プランの使用量の送信](/docs/third-party/submitusage.html#submitusage)を参照してください。

## 新しい {{site.data.keyword.Bluemix_notm}} Identity and Access Management の API キーを生成するにはどうすればよいですか。
{: #iam-creds}

IAM を有効化する時に、API キーが付与されます。 この API キーを保存することは極めて重要です。 この値は再度表示されません。 API キーを紛失した場合は、キーを削除して新規に作成できます。 詳しくは、[サービス ID API キーの管理](/docs/iam/serviceid_keys.html#serviceidapikeys)を参照してください。 


