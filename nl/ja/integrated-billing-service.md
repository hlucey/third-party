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

# 概要: 統合請求サービスの作成
{: #overview}

このトピックでは、{{site.data.keyword.Bluemix}} でのサード・パーティー統合請求サービスの作成および公開に必要な手順を説明します。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} カタログでのオファリングの提供が承認されたら、リソース管理コンソールのガイド付き UI エクスペリエンスで、オファリングの作成を開始します。 カタログ・メタデータを設計し、サービス価格プランを設定し、{{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) と統合します。 

次に、リソース管理コンソールの外で、新しい Open Service Broker (スターター・ブローカーのサンプルと API 文書が提供されます) を構築してホストするためのコード開発を実行し、IAM を使用して認証フローを作成します。 これらの手順が完了したら、リソース管理コンソールに戻り、複数の成果物要件のテストおよび検証を行える限定表示モードでサービスをカタログにデプロイします。準備が整い、オファリングがすべての要件を満たすと、サービスは {{site.data.keyword.Bluemix_notm}} カタログで完全に可視になります。


## プロセスの仕組み
{: #process}

統合請求サービスを提供するには、Provider Workbench、リソース管理コンソール、および選択した開発環境で作業します。これらの手順のトラッキングには、[チェックリスト](/docs/third-party/checklist.html#checklist)が役立ちます。

1. [文書とマーケティング発表を作成する](/docs/third-party/cis1-docs-marketing.html)。
2. [リソース管理コンソール {{site.data.keyword.Bluemix_notm}} でオファリングを定義する](/docs/third-party/cis2-rmc-define.html)。
3. [サービス・ブローカーを作成してホストする](/docs/third-party/cis3-broker.html)。
4. [認証フローを作成する](/docs/third-party/cis5-iam.html)。
5. [サービスをテストする](/docs/third-party/cis4-rmc-publish.html)。
6. [サービスを一般公開する](/docs/third-party/cis6-ga.html)。

これらのステップでは、ユーザーが統合請求サービスの提供を承認されていると想定しています。 Provider Workbench での初期登録と承認が完了していない場合は、[入門チュートリアル](/docs/third-party/index.md)を参照してください。
{: tip}

## サポート
{: #support}

統合請求サービスでは、サード・パーティー・オファリング・プロバイダーは独自のサポート・モデルを提供することが要求されます。 IBM 担当員は、お客様のサポート・モデルの使用可能化を支援し、ユーザーが {{site.data.keyword.Bluemix_notm}} サポートを使用してチケットをオープンした場合に、チケットがサード・パーティーのサポート・サイトに経路指定されるようにします。

## 継続的更新
{: #maintain}

サービスのリリース後は、{{site.data.keyword.Bluemix_notm}} 担当者と直接協力して、反復と更新を継続できます。



