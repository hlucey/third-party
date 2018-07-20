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

# 概要: 統合請求サービスの作成
{: #overview}

このトピックは、{{site.data.keyword.Bluemix_notm}} でのサード・パーティー統合請求サービスの作成および公開に必要な手順を案内するよう設計されています。{{site.data.keyword.Bluemix_notm}} カタログでのオファリングの提供が承認されたら、リソース管理コンソールのガイド付き UI エクスペリエンスで、オファリングの作成を開始します。リソース管理コンソール内では、カタログ・メタデータの設計、サービスの料金プランのセットアップ、および IBM Cloud Access Management (IAM) との統合を行います。次に、リソース管理コンソールの外で、新しい Open Service Broker (スターター・ブローカーのサンプルと API 文書が提供されます) を構築してホストするためのコード開発を実行し、IAM を使用して認証フローを作成します。これらの手順が完了したら、リソース管理コンソールに戻り、複数の成果物要件のテストおよび検証を可能にする限定表示モードでサービスをカタログにデプロイします。準備が整い、オファリングがすべての要件を満たすと、サービスは {{site.data.keyword.Bluemix_notm}} カタログで完全に可視になります。


## 統合請求サービスを提供するためには、どのようなことが必要ですか? 

これらの目標を達成するには、PWB、リソース管理コンソール、および選択した開発環境で作業します。これらの手順のトラッキングには、[チェックリスト](/docs/third-party/checklist.html#checklist)が役立ちます。

以下の手順は、オンボーディング・プロセスの概要を要約しています。

これらのステップでは、ユーザーが統合請求サービスの提供を承認されていると想定しています。PWB での初期登録と承認がまだ完了していない場合は、[概要: {{site.data.keyword.Bluemix_notm}} での第三者オファリングの公開](/docs/third-party/index.md)を参照してください。
{: tip}

1. [作成: サービス文書とマーケティング発表を作成する (PWB)](/docs/third-party/cis1-docs-marketing.html)
2. [定義: リソース管理コンソールでオファリングを定義する<!--{{site.data.keyword.Bluemix_notm}}-->](/docs/third-party/cis2-rmc-define.html)
3. [開発: Open Service Broker API 仕様を使用して 1 つ以上のサービス・ブローカーを開発しホストする](/docs/third-party/cis3-broker.html)
4. [IAM: 認証フローを作成し (OAuth)、ユーザー許可を検証し (v2/authz)、リダイレクト URI を取得する](/docs/third-party/cis5-iam.html)
5. [公開およびテスト: OSB をリソース管理コンソールに接続し、限定表示モードで {{site.data.keyword.Bluemix_notm}} カタログへサービスを公開し、オファリングをテストする](/docs/third-party/cis4-rmc-publish.html)。
6. [サービスを GA するために承認を依頼する](/docs/third-party/cis6-ga.html)

## サポート

統合請求サービスでは、サード・パーティー・サービス・プロバイダーは独自のサポート・モデルを提供することが要求されます。IBM 担当員は、お客様のサポート・モデルの使用可能化を支援し、ユーザーが {{site.data.keyword.Bluemix_notm}} サポートを使用してチケットをオープンした場合に、{{site.data.keyword.Bluemix_notm}} サポートがそのチケットをサード・パーティーのサポート・サイトに経路指定するようにします。

## 継続的更新

サービスのリリース後は、{{site.data.keyword.Bluemix_notm}} 担当者と直接協力して、反復と更新を継続できます。



