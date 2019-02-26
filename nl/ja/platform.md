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
{:note: .note}
{:download: .download}

# 統合請求サービスによる {{site.data.keyword.Bluemix_notm}} プラットフォームの使用方法
{: #how-it-works}

統合請求サービスは、紹介サービスとは異なります。 統合請求サービスは、認証、アクセス、プロビジョニング、計量、および請求に {{site.data.keyword.Bluemix_notm}} プラットフォームを使用します。 このトピックでは、統合請求サービスで使用されるプラットフォーム・コンポーネントの概要について説明します。

## {{site.data.keyword.Bluemix_notm}} プロビジョニング・レイヤー
{: #provisioning-layer}

プロビジョニング・レイヤーは、{{site.data.keyword.Bluemix_notm}} リソースのライフサイクルを管理します。 プロビジョニング・レイヤーは、お客様のアカウントのリソースのライフサイクルの制御およびトラッキングを担当します。 *リソース*は、アプリケーションまたはサービス・インスタンス用にプロビジョンまたは予約できる物理コンポーネントまたは論理コンポーネントです。 リソースの例としては、データベース、アカウント、プロセッサー、メモリー、およびストレージ制限などがあります。 一般に、プロビジョニング・レイヤーでトラッキングされるリソースは、使用量メトリックと請求を関連付けるよう意図されていますが、必ずしもそうとは限りません。 場合によっては、リソース・ライフサイクルをアカウント・ライフサイクルとともに管理できるように、リソースがプロビジョニング・レイヤーに関連付けられていることがあります。

### リソース・ライフサイクルの管理
{: #lifecycle}

プロビジョニング・レイヤーは、プロビジョニング (インスタンスの作成) からバインディング (アクセス資格情報の作成)、アンバインディング (アクセス権限の削除)、プロビジョニング解除 (インスタンスの削除) までのリソースのライフサイクルを制御するための一般的な API を提供します。 さらに、{{site.data.keyword.Bluemix_notm}} プラットフォームには、独自の機能の作成を必要としないこれらのリソースのライフサイクルを管理できる CLI および UI が用意されています。

プロビジョニング・レイヤーには、リソース・ライフサイクルの以下の要素の管理に役立つ API が用意されています。
* プロビジョニング
* リソース・インスタンスの更新
* バインディング
* リソース・キー
* アンバインディング
* プロビジョニング解除

## {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM)
{: #iam}

Identity Access Management (IAM) を使用すると、ユーザーを安全に認証し、{{site.data.keyword.Bluemix_notm}} 全体ですべてのクラウド・リソースへのアクセスを一貫して制御することができます。 {{site.data.keyword.Bluemix_notm}} プロビジョニング・レイヤーは、プロビジョニング・レイヤーに対して実行されるアクションの認証および許可のために IAM を採用しました。 第三者オファリングのプロバイダーは、IAM を使用して認証フロー (OAuth) を作成します。 詳しくは、[IAM とは? ](/docs/iam?topic=iam-iamoverview#iamoverview)を参照してください。

オファリングで OpenID Connect (OIDC) ライブラリーが使用されている場合、IAM は OIDC 統合をサポートします。 OIDC は、認証フレームワーク OAuth 2.0 の上で稼働する認証レイヤーで、オンボーディング・プロセスの簡素化に役立ちます。 OIDC について詳しくは、 [Open ID Connect](http://openid.net/connect/){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") を参照してください。

## {{site.data.keyword.Bluemix_notm}} カタログ
{: #catalog}

{{site.data.keyword.Bluemix_notm}} カタログは、{{site.data.keyword.Bluemix_notm}} コンソールに表示されるリソースのオファリング定義 (説明、機能、イメージ、URL など) を保管します。 サービスの必須メタデータのすべての側面を定義するために、リソース管理コンソールが使用されます。 このメタデータはカタログに公開され、カタログでの表示に使用されます。 必須およびオプションのメタデータ・フィールドの詳細は、リソース管理コンソールの**「オファリング」**ページと**「プラン」**ページにあります。 ユーザーが把握しやすくするため、主な項目はここに含まれています。

   * Service Name: サービスの技術的名前。 サービス名は重要であり、正しく定義されている必要があります。 {{site.data.keyword.Bluemix_notm}} プラットフォームがサービスの識別に使用するサービス名と、{{site.data.keyword.Bluemix_notm}} カタログで顧客に表示される表示名の両方を指定する必要があります。 サービス名は表示名ではありません。
   * Service Display Name: サービスの分かりやすい名前。 例えば、「Compose Redis」など。
   * Service ID: OSB ブローカーへの API 呼び出しで使用されるサービスの GUID。 この値は固有でなければなりません。
   * Service Icon: サービス・ロゴを含む SVG
   * Service Description: {{site.data.keyword.Bluemix_notm}} カタログのユーザー・インターフェースでリソース・アイコンの上にカーソルを移動したときに表示されるリソースの説明。 この説明には、単一の文または句を追加できます。
   * Service Detailed Description: カタログのリスト・ページに表示される最初の文節。 詳細説明には、2 文以上を検討してください。
   * Documentation URL: {{site.data.keyword.Bluemix_notm}} 文書へのリンク。 PWB で作成し、URL 値は、PWB によって自動的に生成されます。
   * Terms URL: サービスのご使用条件へのリンク。 GDPR の目的の場合は、既存のサード・パーティー・サービスのご使用条件にリンクしないでください。 代わりに、統合請求サービスの固有ページを指定する必要があります。
   * Instructions URL: Documentation URL と同様に、{{site.data.keyword.Bluemix_notm}} 文書を指します。ただし、Instructions URL は、サービスのダッシュボードの「概要 (Getting Started)」タブに動的に文書をプルします。
   * Category: カタログ内でサービスを配置する、使用可能な {{site.data.keyword.Bluemix_notm}} カテゴリーの選択。
   * Bullets: サービスに関する短い説明
   * Media: サービスに関する画面キャプチャーおよびビデオ
   * Service Plan Name: 各プランには技術的名前があります。 すべて小文字で、スペースなし、「-」を使用できます。 例えば、`gold` など。
   * Service Plan Display Name: プランの分かりやすい名前。 例えば、`Gold` など。
   * Service Plan ID: OSB ブローカーへの API 呼び出しで使用されるサービス・プランの GUID。 この値は固有でなければなりません。 リソース管理コンソールは、ユーザーの代わりにこの値を生成します。
   * Service Plan Description: リソース・プランの説明。 この説明は、IBM Cloud カタログのリソース詳細ページでプランを選択した後に表示されます。
   * Service Plan Bullets: サービス・プランに関する短い説明


## サービス・ブローカーを開く
{: #open-service}

サービス・ブローカーは、サービスのライフサイクルを管理します。 {{site.data.keyword.Bluemix_notm}} プラットフォームは、サービス・ブローカーとの相互作用により、サービス・インスタンス (サービス・オファリングをインスタンス化したもの) およびサービス・バインディング (アプリケーションとサービス・インスタンスの間の関連を表すものであり、アプリケーションがサービス・インスタンスと通信するために使用する資格情報を含んでいることが多い) をプロビジョンして管理します。 有効なメタデータ値を提供すると、要求が実行されるときに正常な REST API 応答が作成されます。

{{site.data.keyword.Bluemix_notm}} は、Open Service Broker API (OSB) `バージョン 2.12` 仕様を使用します。 [Open Broker API 仕様](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") を読んで熟知してください。詳細については、README ファイルをガイドとして使用してください。

リソース・コントローラーはリソースをプロビジョンする要求を受信すると、OSB を呼び出してサービス・タイプ、オファリング、プラン、および地域の可用性を確認します。 リソース・コントローラーは、お客様のアカウントに関連付けられたプランの可視性も確認します。 {{site.data.keyword.Bluemix_notm}} には、OSB 仕様を拡張するブローカー・サンプルと API 文書が用意されています。 ブローカーの開発およびホストのより詳細な情報は、詳細な統合請求のオンボーディング開発ステップを段階的に実行しているときに見つけることができます。

## {{site.data.keyword.Bluemix_notm}} 計量サービス
{: #metering-service}

サービスで従量制プランが提供されている場合、{{site.data.keyword.Bluemix_notm}} ユーザーは、使用したリソースの量に基づいて課金されます。 例えば、データベース・サービスを使用する {{site.data.keyword.Bluemix_notm}} ユーザーは、アプリケーションが使用するストレージの量に基づいて課金される可能性があります。 使用量を課金可能な記録に変換するためには、使用量の送信が行われる必要があります。

従量制プランを提供するすべての統合請求サービスは、使用量データを報告するために {{site.data.keyword.Bluemix_notm}} 計量サービスを使用する必要があります。

従量制プランを提供する場合は、計量サービス API を使用して、毎時の使用量の送信を自動化する必要があります。

計量について詳しくは、[計量の統合](/docs/third-party?topic=third-party-meteringintera#meteringintera)を参照してください。 計量される使用量の送信について詳しくは、[従量制プランの使用量の送信](/docs/third-party?topic=third-party-submitusage#submitusage)を参照してください。

## プロビジョニング・シナリオ: すべてをまとめる
{: #provision2}

次に、すべての概念をまとめ、{{site.data.keyword.Bluemix_notm}} プラットフォームを使用してサービス・インスタンスの作成がどのように機能するかについての例を見てみます。

![プロビジョニング・シナリオ](images/flow-am.svg "プラットフォームがサービス・インスタンスの作成をどのように処理するか")

ユーザーがサービス・インスタンスを作成するとき、次の 2 つの方法のいずれかで開始できます。
* **CLI**: `ibmcloud cli [ ibmcloud resource service-instance-create NAME SERVICE_NAME SERVICE_PLAN_NAME LOCATION ]` の使用
* **{{site.data.keyword.Bluemix_notm}} コンソール**: ユーザーは、サービスを選択し、計画し、**「作成」**操作を使用できます。

{{site.data.keyword.Bluemix_notm}} プラットフォームは、ユーザーが {{site.data.keyword.Bluemix_notm}} IAM を使用してサービス・インスタンスを作成する権限を持っていることを確認します。 この確認後、サービス・ブローカーのプロビジョン・エンドポイント (PUT /v2/resource_instances/:resource_instance_id) が開始されます。 プロビジョニングが行われるときは、以下の規則に合致している必要があります。
* {{site.data.keyword.Bluemix_notm}} コンテキストがコンテキスト変数に含まれている
* `X-Broker-API-Originating-Identity` に、要求を開始したユーザーの IBM IAM ID が含まれる
* パラメーター・セクションに、要求されたロケーション (およびサービスが必要とする追加パラメーター) が含まれる

プロビジョン要求の例:

```
    PUT /v2/service_instances/crn%3Av1%3Abluemix%3Apublic%3Acompose-redis%3Aus-south%3Aa%2F46aa677e-e83f-4d17-a2b6-5b752564477c%3A416d769b-682d-4833-8bd7-5ef8778e5b52?accepts_incomplete=true HTTP/1.1
    Host:  https://broker.compose.cloud.ibm.com
    Authorization: basic dXNlcjpwYXNzd29yZA==
    X-Broker-Api-Version: 2.12
    X-Broker-API-Originating-Identity: ibmcloud aWJtaWQtNDU2MzQ1WA==
    {
      "service_id": "0bc9d744-6f8c-4821-9648-2278bf6925bb", // your service's GUID from onboarding
      "plan_id": "ecc19311-aba2-49f7-8198-1e450c8460d4", //your plan's GUID from onboarding
      "context": {
        "platform": "ibmcloud",
        "account_id": "003e9bc3993aec710d30a5a719e57a80",
        "crn": "crn:v1:bluemix:public:compose-redis:us-south:a/003e9bc3993aec710d30a5a719e57a80:416d769b-682d-4833-8bd7-5ef8778e5b52",
        "resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/003e9bc3993aec710d30a5a719e57a80::resource-group:b4570a825f7f4d57aa54e8e1d9507926",
        "target_crn": "crn:v1:bluemix:public:resource-catalog::a/e97a8c01ac694e308ef3ad7795c7cdb3::deployment:e62e2c19-0c3b-41e3-b8b3-c71762ecd489:us-south38399"
      },
      "parameters": {
        "location": "us-south",
        "optional-param":"parameter required by your service"
      }
    }
```

### {{site.data.keyword.Bluemix_notm}} `context` パラメーターの理解
{: #parameter}

前述の例で、`context` パラメーターで返されるメタデータを確認できます。 {{site.data.keyword.Bluemix_notm}} のプロビジョン・コンテキストは、以下を返します。

* **platform**: プラットフォームを「ibmcloud」として識別します。

* **"account_id"**: サービス・インスタンスをプロビジョニングしている {{site.data.keyword.Bluemix_notm}} のアカウントの ID を返します。

* **crn**: お客様が {{site.data.keyword.Bluemix_notm}} でサービスをプロビジョンするとサービス・インスタンスが作成され、このインスタンスはその {{site.data.keyword.Bluemix_notm}} Resource Name (CRN) で識別されます。 CRN は、プロビジョニング、バインディング (資格情報およびエンドポイントの作成)、計量、ダッシュボードの表示、およびアクセス制御を含め、{{site.data.keyword.Bluemix_notm}} との相互作用のあらゆる側面で使用されます。 オファリング・プロバイダーの観点から、CRN は、{{site.data.keyword.Bluemix_notm}} API で使用される不透明なストリングとして主に扱うことができます。 また、以下の構造を使用して分解することもできます。

   ```
   crn:version:cname:ctype:service-name:location:scope:service-instance:resource-type:resource
   ```

   プロビジョニング・サンプルで、`compose-redis` サービス CRN は以下であることを確認できます。

   ```
   crn:v1:bluemix:public:compose-redis:us-south:a/46aa677e-e83f-4d17-a2b6-5b752564477c:416d769b-682d-4833-8bd7-5ef8778e5b52::
   ```

   このサンプルで、この `compose-redis` インスタンスは、ID の {{site.data.keyword.Bluemix_notm}} アカウントの一部です。 インスタンスの固有 ID は `416d769b-682d-4833-8bd7-5ef8778e5b52` で、インスタンスはパブリック {{site.data.keyword.Bluemix_notm}} の `us-south` 地域でホストされています。

* **resource_group_crn**: サービス・インスタンスを含むリソース・グループを返します。 詳しくは、[リソース・グループの管理](/docs/resources?topic=resources-rgs#rgs)を参照してください。

   オファリング・プロバイダーは、固有の状況を除き、`resource_group_crn` に関係していません。 そのフィールドを使用する前に、ご自身のユース・ケースについて IBM 担当員に相談してください。
   {: note}

