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

# 概要: 統合請求サービスの作成
{: #overview}

このトピックでは、{{site.data.keyword.Bluemix}} でのサード・パーティー統合請求サービスの作成および公開に必要な手順を説明します。 
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} カタログでのオファリングの提供が承認されたら、リソース管理コンソールのガイド付き UI エクスペリエンスで、オファリングの作成を開始します。 カタログ・メタデータを設計し、サービス価格プランを設定し、{{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) と統合します。 

次に、リソース管理コンソールの外で、新しい Open Service Broker を構築してホストするためのコード開発を実行します。 スターター・ブローカー・サンプルと API 文書が用意されています。また、IAM を使用して認証フローを作成します。 これらの手順が完了したら、リソース管理コンソールに戻り、成果物要件のテストおよび検証を行える限定表示モードでサービスをカタログにデプロイします。 準備が整い、オファリングがすべての要件を満たすと、サービスは {{site.data.keyword.Bluemix_notm}} カタログで完全に表示されるようになります。


## プロセスの仕組み
{: #process}

統合請求サービスを提供するには、Provider Workbench、リソース管理コンソール、および選択した開発環境で作業します。 これらの手順のトラッキングには、[チェックリスト](/docs/third-party?topic=third-party-checklist#checklist)が役立ちます。

これらのステップは、ユーザーが統合請求サービスを提供することを承認済みであると想定しています。 PWB での初期登録と承認が完了していない場合は、[{{site.data.keyword.Bluemix_notm}} でのサード・パーティー・オファリングの公開についての入門](/docs/third-party/index.md?topic=third-party-get-started#get-started)を参照してください。
{: tip}

1. [文書とマーケティング発表を作成する](/docs/third-party?topic=third-party-content-tasks#content-tasks)。
2. [リソース管理コンソールでオファリングを定義する{{site.data.keyword.Bluemix_notm}}](/docs/third-party?topic=third-party-step2-define#step2-define)。
3. [サービス・ブローカーを作成してホストする](/docs/third-party?topic=third-party-step3-osb#step3-osb)。
4. [認証フローを作成する](/docs/third-party?topic=third-party-step4-iam#step4-iam)。
5. [サービスをテストする](/docs/third-party?topic=third-party-step5-pubtest#step5-pubtest)。
6. [サービスを一般公開する](/docs/third-party?topic=third-party-public-releasing#public-releasing)。

## サポート
{: #support}

統合請求サービスでは、サード・パーティー・オファリング・プロバイダーは独自のサポート・モデルを提供することが要求されます。 IBM 担当員は、お客様のサポート・モデルの使用可能化を支援し、ユーザーが {{site.data.keyword.Bluemix_notm}} サポートを使用してチケットをオープンした場合に、チケットがサード・パーティーのサポート・サイトに経路指定されるようにします。

## 継続的更新
{: #maintain}

サービスのリリース後は、{{site.data.keyword.Bluemix_notm}} 担当者と直接協力して、反復と更新を継続できます。



