---


copyright:
  years: 2018
lastupdated: "2018-08-23"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# ステップ 3. サービス・ブローカーの開発とホスティング
{: #step3-osb}

リソース管理コンソールからエクスポートしたメタデータを使用して、希望のプログラミング言語で新しいサービス・ブローカーを 1 つ以上作成できます。
{:shortdesc}

サービス・ブローカーは、サービスのライフサイクルを管理します。 {{site.data.keyword.Bluemix_notm}} プラットフォームは、サービス・ブローカーと対話して、サービス・インスタンス (サービス・オファリングのインスタンス化) とサービス・バインディング (アプリケーションとサービス・インスタンス間の関連を表すもの。多くの場合、サービス・インスタンスとの通信にアプリケーションが使用する資格情報が含まれる) をプロビジョンして管理します。 有効なメタデータ値を指定すると、要求の実行時に正常な RESTful API 応答が作成されます。

リソース管理コンソールからエクスポートしたメタデータ、{{site.data.keyword.Bluemix_notm}} サービス・ブローカーの公開サンプル、およびリソース・ブローカー API 文書を組み合わせて使用して、ブローカーの作成を開始できます。

## 始める前に
{: #pre-reqs}

ステップ 1 を開始しており、ステップ 2 を完了していることを確認してください。
1. [サービス文書とマーケティング発表を作成する](/docs/third-party/cis1-docs-marketing.html)。
2. [リソース管理コンソールでオファリングを定義する](/docs/third-party/cis2-rmc-define.html)。


## {{site.data.keyword.Bluemix_notm}} プラットフォーム・プロビジョニング・シナリオの参照
{: #scenario}

{{site.data.keyword.Bluemix_notm}} プラットフォームと連携して動作する Open Service Broker を開発します。[プロビジョニング・シナリオ](/docs/third-party/platform.html#provisioning-scenario-pulling-it-all-together)を参照して、リソース作成の仕組みを把握してください。

## OSB 仕様の熟知
{: #learn-osb}

{{site.data.keyword.Bluemix_notm}} は、Open Service Broker API (OSB) `バージョン 2.12` 仕様を使用します。 [Open Broker API 仕様](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") を読んで熟知してください。詳細については、README ファイルをガイドとして使用してください。

## {{site.data.keyword.Bluemix_notm}} ブローカー・サンプルの参照
{: #samples}

[https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")

**注:** サンプルでは、すべての言語が示されているわけではありません。 例えば、Python のサンプル・ブローカーが必要な場合には、Google で検索すれば Cloud Foundry のサンプルを見つけられるはずです。 OSB の要件を満たすように、このサンプルを調整する必要がある場合があります。


## {{site.data.keyword.Bluemix_notm}} Open Service Broker API 文書の確認
{: #docs}

サービス・ブローカーは、[{{site.data.keyword.Bluemix_notm}} Open Service Broker API](https://console.bluemix.net/apidocs/ibm-cloud-osb-api){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") を理解した上で開発する必要があります。 Broker API 自体と、それがブローカーとどう相互作用するかについて熟知してください。

{{site.data.keyword.Bluemix_notm}} Open Service Broker は、Open Service Broker 2.12 仕様を拡張します。
{: tip}

### すべてのサービス・ブローカーに必要なエンドポイント・ロジック

サービス・ブローカーは、REST API が取り込むメタデータ値の標準セットを提供する必要があります。また、{{site.data.keyword.Bluemix_notm}} ブローカーは、以下の REST API エンドポイント/パスのロジックを含まなければなりません。

<dl>
  <dt>カタログ (GET)</dt>
  <dd>ブローカーに含まれるカタログ・メタデータを戻します。 その他に、戻されないカタログ・メタデータ値が多くあります。そうした値は、リソース管理コンソール内でのみ追加され、{{site.data.keyword.Bluemix_notm}} カタログ内に保管されます。</dd>
  <dt>リソース・インスタンス (PUT)</dt>
  <dd>サービス・インスタンスをプロビジョンします</dd>
  <dt>リソース・インスタンス (DELETE)</dt>
  <dd>サービス・インスタンスをプロビジョン解除します。</dd>
  <dt>リソース・インスタンス (PATCH)</dt>
  <dd>サービス・インスタンスを更新します。</dd>
</dl>

**カタログ (GET) に関する注**: このエンドポイントは、ブローカーがサポートするサービスとプランについて、ブローカーと {{site.data.keyword.Bluemix_notm}} プラットフォーム間の契約を定義します。 このエンドポイントは、ブローカー内に保管されたカタログ・メタデータを戻します。 これらの値は、サービスと {{site.data.keyword.Bluemix_notm}} プラットフォーム間の最小限のプロビジョニング契約を定義します。 プロビジョニングに必要でないその他のカタログ・メタデータはすべて、{{site.data.keyword.Bluemix_notm}} カタログ内に保管され、ダッシュボードのレンダリングに使用されるカタログ表示値 (リンク、アイコン、国際化対応翻訳メタデータなど) への更新は、ブローカー内に収容されるのではなく、リソース管理コンソールで更新される必要があります。 ブローカーに保管されたメタデータは、{{site.data.keyword.Bluemix_notm}} コンソールでも {{site.data.keyword.Bluemix_notm}} CLI でも表示されません。コンソールと CLI は、リソース管理コンソール内で設定され、{{site.data.keyword.Bluemix_notm}} カタログに保管されたものを戻します。 カタログ (GET) が戻す必要がある最小限の必須値は、以下のとおりです。

```
{
       "services": [{
           "id": "ibmcloud-link",
           "name": "ibmcloud-link",
           "description": "An IBM provided service that enables aliasing to service instances in the {{site.data.keyword.Bluemix_notm}}.",
           "bindable": true,
           "plan_updateable": false,
           "plans": [
               {
                   "id": "ibmcloud-link-alias",
                   "name": "ibmcloud-alias",
                   "free": true,
                   "description": "The {{site.data.keyword.Bluemix_notm}} alias plan used for linking."
               }
               ]
       }]
}
```

### バインド可能なサービスに必要なエンドポイント・ロジック

{{site.data.keyword.Bluemix_notm}} 内のアプリケーションにバインドできるサービスは、API エンドポイントと資格情報をサービス・コンシューマーに戻せなければなりません。 バインド可能なサービスは、Open Service Broker 仕様のバインド可能な操作を使用して、以下のエンドポイント/パスを実装する必要があります。

<dl>
  <dt>バインディングと資格情報 (PUT)</dt>
  <dd>サービス・インスタンスをアプリケーションにバインドします。</dd>
  <dt>バインディングと資格情報 (DEL)</dt>
  <dd>サービス・インスタンスをアプリケーションからアンバインドします。</dd>
</dl>

### 必要な {{site.data.keyword.Bluemix_notm}} 拡張エンドポイント

OSB 仕様では、インスタンスを削除はせずに無効化した状態を*サポートしていません*。 請求の期限切れや (アカウント取り消しには至らないが) アカウント中断になる状況が発生した顧客に {{site.data.keyword.Bluemix_notm}} が対応するために、サービス・インスタンスの無効化と再有効化を許可する拡張 API エンドポイントが {{site.data.keyword.Bluemix_notm}} では定義されています。 以下のエンドポイント拡張が**必要**です。

<dl>
  <dt>インスタンスの有効化と無効化 (GET)</dt>
  <dd>状況 - サービス・インスタンスの状態を戻します。</dd>
  <dt>インスタンスの有効化と無効化 (PUT)</dt>
  <dd>サービス・インスタンスを有効化または無効化できます。</dd>
</dl>

**注**: 無効化エンドポイントが呼び出されたときにサービス・インスタンスへのアクセスを無効化すること、および有効化エンドポイントが呼び出されたときにそのアクセスを再有効化することは、サービス・プロバイダーの責任で行います。

## エクスポートされたメタデータを使用してブローカー開発をガイドする方法の理解
{: #use-metadata}

リソース管理コンソールからエクスポートしたメタデータは、ブローカー開発のガイドとして使用できます。 リソース管理コンソールに入力したすべての値が、サービスのプロビジョンに必要であるわけではありません。 リソース管理コンソールからエクスポートしたメタデータは、サービスと {{site.data.keyword.Bluemix_notm}} プラットフォーム間の最小限のプロビジョニング契約を定義します。 エクスポートした JSON は、以下の値を提供する必要があります。

```
{
services :
            [
                {
                    bindable         : true,
                    description      : "Test Node Resource Service Broker Description",
                    // TODO - GUID generated by http://www.guidgenerator.com
                    // TODO - This service id must be unique within an IBM Cloud environment's set of service offerings
                    id               : "df35cab6-347b-4ba5-8f39-e9c23a237f5b",
                    metadata         :
                    {
                        displayName         : "Test Node Resource Service Broker Display Name",
                        documentationUrl    : baseMetadataUrl + "documentation.html",
                        imageUrl            : baseMetadataUrl + "services.svg", // Copied from https://github.com/carbon-design-system/carbon-icons/blob/master/src/svg/services.svg
                        instructionsUrl     : baseMetadataUrl + "instructions.html",
                        longDescription     : "Test Node Resource Service Broker Long Description",
                        providerDisplayName : "Company Name",
                        supportUrl          : baseMetadataUrl + "support.html",
                        termsUrl            : baseMetadataUrl + "terms.html"
                    },
                    name             : SERVICE_NAME,
                    // TODO - Ensure this value is accurate for your service. Requires PATCH of /v2/service_instances/:instance_id below if true
                    plan_updateable  : true,
                    tags             : ["lite", "tag1a", "tag1b"],
                    plans            :
                    [
                        {
                            bindable    : true,
                            description : "Test Node Resource Service Broker Plan Description",
                            free        : true,
                            // TODO - GUID generated by http://www.guidgenerator.com
                            // TODO - This service plan id must be unique within an IBM Cloud environment's set of service plans
                            id          : "2a1d139b-1b05-4e33-b72e-a1f8c14be559",
                            metadata    :
                            {
                                bullets     : ["Test bullet 1", "Test bullet 2"],
                                displayName : "Lite"
                            },
                            // TODO - This service plan name must be unique within the containing service definition
                            name        : "lite"
                        }
                    ]
                }
            ]
}
```


OSB サービス配列は、リソース管理コンソールに追加したオファリング・メタデータと正確に同じでなければなりません。 OSB とリソース管理コンソールで 1 対 1 で一致するように、リソース管理コンソールからダウンロードした `catalog.json` 内のサービス配列を、ブローカー内の実際のサービス配列と比較することが重要です。 サービスとプランの ID と名前はすべて一致しなければなりません。
{: tip}

## {{site.data.keyword.Bluemix_notm}} プラットフォームで提供されるブローカー情報
{: #broker info}

サービス・ブローカーは、{{site.data.keyword.Bluemix_notm}} プラットフォームから以下の情報を受け取ります。

### X-Broker-API-Originating-Identity

**ユーザー ID ヘッダー**は、API originating identity ヘッダーによって提供されます。 この要求ヘッダーには、ユーザーの {{site.data.keyword.Bluemix_notm}} IAM ID が含まれます。 IAM ID は、Base64 でエンコードされます。 {{site.data.keyword.Bluemix_notm}} は、単一認証レルム `IBMid` をサポートします。 `IBMid` レルムは、IBMid Unique ID (IUI) を使用して、{{site.data.keyword.Bluemix_notm}} でユーザーの ID を識別します。 この IUI は、サービス・プロバイダーに内部が見えないストリングです。

例:

```
X-Broker-API-Originating-Identity: ibmcloud eyJpYW1faWQiOiJJQk1pZC01MEdOUjcxN1lFIn0=
Decoded:
{"iam_id":"IBMid-50GNR717YE"}
```

### API ヘッダー・バージョン

**API バージョン・ヘッダー**は、[2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") になります。 例えば、`X-Broker-Api-Version: 2.12` などです。

### リソース・インスタンス (PUT) の body.context とリソース・インスタンス (PATCH) の body.context

`PUT /v2/service_instances/:resource_instance_id` と `PATCH /v2/service_instances/:resource_instance_id` は、**body.context** 内の次の値を受け取ります。`{ "platform": "ibmcloud", "account_id": "tracys-account-id", "crn": "resource-instance-crn" }`

## ブローカーに関するその他の推奨
{: #more-info}

### 非同期操作と同期操作の使用に関する推奨

OSB API は、操作の同期モードと非同期モードの両方をサポートします。 操作が 10 秒未満で完了する場合は、同期応答が推奨されます。  それ以外の場合は、非同期モードの操作を使用してください。  これに関する詳細は、OSB の仕様に記載されています。

インスタンスをプロビジョンしようとして、非同期操作が 10 秒未満で完了すると、プラットフォームはタイムアウトになります。
{: tip}

### ロケーションをまたがるブローカーの管理に関する推奨

ユーザーが、待ち時間、可用性、データ常駐のためにクラウド・サービスのロケーションを理解することは重要です

{{site.data.keyword.Bluemix_notm}} でサービス・インスタンスをプロビジョンする際に、ユーザーが指定する必須パラメーターの 1 つとして、サービス・インスタンスをプロビジョンするロケーションがあります。 サービスによっては、複数ロケーションでのプロビジョニングをサポートするものもあります。 例えば、データベース・サービスが、すべての {{site.data.keyword.Bluemix_notm}} 地域でのプロビジョンをサポートする場合も、一部の地域をサポートする場合もあります。

サード・パーティーの API ベースのサービスが別のクラウドで実装されていて {{site.data.keyword.Bluemix_notm}} に公開される場合、ロケーションは、そのもう一方のクラウドにおけるサービスのロケーションを示す必要があります。

{{site.data.keyword.Bluemix_notm}} にオンボードする際には、少なくとも 1 つの OSB ブローカーを実装する必要がありますが、そのサービスにサポートするデプロイメント戦略とロケーションによっては、複数のブローカーを用意するオプションもあります。  リソース管理コンソール・ツール内で、サービス/プラン/ロケーションのタプルと、そのタプルの操作を処理するブローカーとのマッピングを設定しました。 一般的な選択肢としては、サービスのすべてのロケーションを処理する単一ブローカーを定義するか、ロケーションごとにブローカーを定義します。この選択は、サービス・プロバイダーに委ねられます。

選択可能なロケーションのリストについては、[IBM グローバル・カタログ・ロケーション](https://resource-catalog.bluemix.net/search?q=kind:geography){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") を参照してください。 サービスでグローバル・カタログに追加のロケーションを定義する必要がある場合は、{{site.data.keyword.Bluemix_notm}} オンボード・チームに相談してください。


## ブローカーのホスト
{: #host}

ブローカーは、REST API 呼び出しに応答できるアプリケーションの一部としてホストされなければなりません。 また、ホストされるロケーションは、{{site.data.keyword.Bluemix_notm}} のセキュリティー・ガイドラインに適合する必要があります。 {{site.data.keyword.Bluemix_notm}} でホストすることも、あるいは、{{site.data.keyword.Bluemix_notm}} からパブリックでアクセス可能である限り、外部でホストすることも可能です。

IBM 外部でブローカーをホストするには、以下のセキュリティー・ガイドラインに適合することを確認してください。
- Transport Layer Security (TLS) プロトコル バージョン 1.2 に従う必要があります。
- パブリック・インターネットでアクセスできる有効な HTTPS エンドポイントでホストされる必要があります。

{{site.data.keyword.Bluemix_notm}} でホストする場合は、以下に、コンテナー (Kubernetes) を使用したアプリケーションの作成に関する情報があります。[Internal Adopters - Usage information](/docs/containers/cs_internal.html#cs_internal)

次のステップを完了するには、サービス・ブローカーのホストされるロケーションが必要になります。 アプリケーションに関連付けられた URL と資格情報を準備してから、次のステップに進んでください。
{: tip}

## サービスのブローカーをテストする方法
{: #test}

有効化するさまざまなエンドポイントに対して curl コマンドを実行することで、ブローカーを検証してください。 以下のサンプルの README に、OSB エンドポイントに対する curl 実行に関する優れたガイダンスがあります。https://github.com/IBM/sample-resource-service-brokers/blob/master/README.md

### サービスのブローカーに対する curl 実行方法

ブローカーの curl 応答をテストするには、以下の例を使用してください。

```
curl -X PUT  https://<sample-service-broker>/v2/service_instances/<encoded-resource-crn> \
     -u '<your broker user>:<your broker password>' \
     -H 'content-type: application/json' \
      -d '{ "context": {"platform": "ibmcloud", \
                        "account_id": "34ff5928-c3c7-4d46-bbf6-1a5628c325d1", \
                        "resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/003e9bc3993aec710d30a5a719e57a80::resource-group:b4570a825f7f4d57aa54e8e1d9507926", \
                        "crn": "<resource-crn>", \
                        "target_crn": "<target_crn>"}, \
            "service_id": "a07f025c-90db-4652-afd1-cf4adfac93c8", \
            "plan_id": "fe442cec-2eef-41fe-9f92-58d6c094584f"}'
```

## 次のステップ

重要なスキルをいくつか習得されました。 これで、OSB 仕様に適合するサービス・ブローカーを作成してホストしました。 [ステップ 4: 認証フローの作成](/docs/third-party/cis5-iam.html)を参照してください。
