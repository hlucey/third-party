---

copyright:
  years: 2018
lastupdated: "2018-07-02"

---

{:right: .ph data-hd-position='right'}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}

# 全工程のチェックリスト
{: #checklist}

以下のチェックリストを利用して、統合請求サービスの定義、開発、公開に必要なすべてのタスクをトラッキングできます。

## オファリングの定義

| タスク | サブタスク | 説明 | 環境 |
|------| ----------| ------------|-----|
| {{site.data.keyword.Bluemix_notm}} プラットフォームに関する理解 | ☐ プロビジョニング層、{{site.data.keyword.Bluemix_notm}} IAM、カタログ、OSB、および計量サービスのすべてが {{site.data.keyword.Bluemix_notm}} プラットフォームのために連携する仕組みを理解している。 | {{site.data.keyword.Bluemix_notm}} 紹介サービスと異なり、統合請求サービスでは、{{site.data.keyword.Bluemix_notm}} プラットフォームを使用してサービス・インスタンスの作成、バインド、削除、課金を行います。開発を円滑に開始するために、プラットフォームを構成する重要コンポーネントに関する[詳細を参照してください](/docs/third-party/platform.html#what-is-the-ibm-cloud-platform-)。| 文書 |
| PWB への登録 | ☐ PWB で**「コンテンツ・タスク (Content Task)」**を完了した <br><br>☐ 統合請求サービスとしてオファリングを公開する承認を得た <br><br> ☐ 文書 URL の値が含まれる初期 E メールを入手した <br><br> | 最初のステップとして、{{site.data.keyword.Bluemix_notm}} PWB にオファリングを登録します。このタスクの実行に関して詳しくは、[入門チュートリアル](/docs/third-party/index.html#get-started)を参照してください。| PWB |
| {{site.data.keyword.Bluemix_notm}} 文書の作成と公開 | ☐ PWB で**「ガイダンス・タスク (文書)(Guidance Task (Documentation))」**を開始した <br><br>☐ `文書 URL` を入手した <br><br> ☐ 文書を正常に公開した <br><br> | Web サイトにホストされたサード・パーティー文書は優れています。しかし、{{site.data.keyword.Bluemix_notm}} で統合請求サービスを提供するため、{{site.data.keyword.Bluemix_notm}} 統合請求のエクスペリエンスでカスタマイズされた文書を提供する必要があります。PWB は、このタスクを通して支援を提供し、https://console.bluemix.net/docs/ に文書を公開できるようにします。このタスクの実行に関して詳しくは、[概要文書の作成](/docs/third-party/cis1-docs-marketing.html#docs)を参照してください | PWB |
| マーケティング発表の作成と公開 | ☐ PWB で**「マーケティング・タスク (発表)(Marketing Task (Announcement))」**を開始した <br><br>  ☐ 発表を正常に公開した <br><br>  | {{site.data.keyword.Bluemix_notm}} ニュースレターおよびソーシャル・メディア・チャネルを通じてサービスの利用可能を発表するマーケティング販促用品を作成します。PWB はこのタスクを通して支援を提供します。詳しくは、[概要文書の作成](/docs/third-party/cis1-docs-marketing.html#announcement)を参照してください | PWB |
| リソース管理コンソールへのサービスの登録 | ☐ 一意的で意味の分かる `service-name` を**リソース名**で定義した <br><br>  ☐ 正常に保存し、リソース管理コンソールにレコードがあることを検証した <br><br>  | リソース管理コンソールは、固有オファリングの作成を支援します。[ガイダンス](/docs/third-party/cis2-rmc-define.html#register-your-offering-by-using-the-resource-management-console-rmc-)に従ってオファリングを登録してください。 | リソース管理コンソール |
| リソース管理コンソールの**「オファリング (Offering)」**ページの入力 | ☐ PWB オファリング E メールで提供された値を使用して、**「文書 URL (Documentation URL)」** と**「手順 URL (Instruction URL)」**を正しく設定した<br><br>  ☐ **サービスのご利用条件** (TOS) の URL を指定した。これは、自分の会社の TOS ページではなく、請求および支払いの条項を含まない固有の TOS ページである。<br><br>  ☐ **「プラン変更のサポート (Plan changes supported?)」**が有効かどうかを、理解した上で正しく指定した。☐ サービスが**「バインド可能」**かどうかを、理解した上で正しく指定した。| リソース管理コンソールで {{site.data.keyword.Bluemix_notm}} タイルに表示されるカタログ・メタデータを指定します。これには、重要な URL (サービスの利用条件など) やオファリングに関する分かりやすい詳細 (リスト項目の情報) などが含まれます。[ガイダンス](/docs/third-party/cis2-rmc-define.html#enter-your-offering-metadata-rmc-offering-page-)に従って、オファリングの必須および推奨のカタログ・メタデータを設定してください。| リソース管理コンソール |
| リソース管理コンソールの**「アクセス管理 (Access Management)」**ページの入力 | ☐ IAM を正常に有効にした<br><br>  ☐ リソース管理コンソール UI で作成された一回限りの生成 IAM API キーを保存した。API キーはリソース管理コンソールに保管されず、後で取得できないことを理解している。<br><br> ☐ 後のステップで OSB を開発してホストし、リダイレクト URI を導出するまで、「アクセス管理 (Access Management)」ページを完成できないことを理解している。<br><br> ☐ OSB を作成してホストした後、IAM ページに戻り、**「リダイレクト URI の追加 (Add Redirect URI)」**をクリックして導出された値を追加することで、ページの入力を正常に完了した。| リソース管理コンソールで {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) にオファリングを登録してください。IAM を使用すると、両方のプラットフォーム・サービスに関してユーザーをセキュアに認証でき、また {{site.data.keyword.Bluemix_notm}} プラットフォーム全体で一貫してリソースへのアクセスを制御できます。 (後でここに戻って、リダイレクト URI を有効にします。)[ガイダンス](/docs/third-party/cis2-rmc-define.html#register-with-identity-and-access-management-rmc-iam-page-)に従って、オファリングの初期アクセス管理を有効にしてください。| リソース管理コンソール |
| リソース管理コンソールで 1 つ以上の料金プランを開発 | ☐ 固有の名前で無料プランを指定した。<br><br>  ☐ (オプション) IBM 担当員と作業して、有料プラン (サブスクリプションまたは従量制) を定義した。従量制プランを作成するには、デフォルトのサブスクリプション・プランの削除が必要であることを理解している。<br><br> ☐ (オプション) 従量制プランでは、{{site.data.keyword.Bluemix_notm}} プラットフォームの計量サービスを使用して、自動の毎時使用量送信をホストして開発する必要があったことを理解している。| オファリングについてどのように課金しますか? リソース管理コンソールでは、無料または有料 (サブスクリプションおよび従量制) プランが提供されます。[ガイダンス](/docs/third-party/cis2-rmc-define.html#develop-a-pricing-plan-rmc-pricing-page-)に従って、オファリングの料金プランを定義してください。| リソース管理コンソール |
| リソース管理コンソールからカタログ・メタデータをエクスポート| ☐ リソース管理コンソールの**「オファリング (Offering)」**ページと**「料金」**ページで指定したメタデータの一部は、エクスポートして OSB に指定する必要があることを理解している。リソース管理コンソールから値をエクスポートすることで、リソース管理コンソールで生成されたサービス ID およびプラン ID のような重要な GUID をマップし、OSB にそれらを指定して、プラットフォームのプロビジョニング層が `catalog GET` エンドポイントの応答からこのプロビジョニング契約を読み取れるようにすることができる。<br><br>  ☐ リソース管理コンソールの**「デプロイメント (Deployments)」**ページから `catalog.json` ファイルを入手した。サービス配列を OSB のメタデータにマップする準備ができている。<br><br> | リソース管理コンソールでサービスを定義したので、catalog.json ファイルをダウンロードして使用し、Open Service Broker の開発に情報を提供することができます。catalog.json には、ブローカーでホストする必要があるメタデータが含まれます。これらの値によって、ブローカーがサポートするサービスとプランについて、ブローカーと IBM Cloud プラットフォーム間の契約が定義されます。[ガイダンス](/docs/third-party/cis2-rmc-define.html#export-your-metadata-as-json-rmc-deployments-page-)に従って、カタログ・メタデータをエクスポートしてください。| リソース管理コンソール |
{: caption="表 1. 統合請求オファリングの定義" caption-side="top"}

## オファリングの開発

| タスク | サブタスク | 説明 | 環境 |
|------| ----------| ------------|-----|
| Open Service Broker (OSB) 仕様 バージョン 2.12 に関する理解 | ☐ OSB 仕様を読み通した。固有の OSB を開発する必要があることを理解している。<br><br>  |  サービス・ブローカーは、サービスのライフサイクルを管理します。{{site.data.keyword.Bluemix_notm}} プラットフォームは、Open Service Broker と対話して、サービス・インスタンス (サービス・オファリングのインスタンス化) とサービス・バインディング (アプリケーションとサービス・インスタンス間の関連を表すもの。多くの場合、サービス・インスタンスとの通信にアプリケーションが使用する資格情報が含まれる) をプロビジョンして管理します。バージョン 2.12 仕様に関する[詳細を参照してください](/docs/third-party/cis3-broker.html#become-familiar-with-the-osb-specification) | 文書 |
| {{site.data.keyword.Bluemix_notm}} ブローカー・サンプルの参照 | ☐ リポジトリーを複製し、ブローカー・サンプルに目を通した。これらのサンプルを使用して開発を開始する準備ができている。<br><br>  |  [https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") | コード例 |
| {{site.data.keyword.Bluemix_notm}} Open Service Broker API 文書の確認 | ☐ OSB のコードがサポートしなければならない必須のエンドポイントがいくつかあることを理解している。<br><br>  ☐ {{site.data.keyword.Bluemix_notm}} 内のアプリケーションにバインドできるサービスは、API エンドポイントと資格情報をサービス・コンシューマーに戻せなければならないことを理解している。<br><br> ☐ サービス・インスタンスの無効化と再有効化を許可する拡張 API エンドポイントが {{site.data.keyword.Bluemix_notm}} で定義されたことを理解している。OSB を拡張し、**「インスタンスの有効化と無効化 (GET および PUT) (enable and disable instances (GET and PUT))」**を定義する必要がある |  {{site.data.keyword.Bluemix_notm}} Open Service Broker は、Open Service Broker 2.12 仕様を拡張します。ブローカーが使用しなければならない必須のエンドポイントに関する[詳細を参照してください](/docs/third-party/cis3-broker.html#view-our-resource-broker-api-documentation)| 文書 |
| カタログ・メタデータを使用してブローカーの開発を開始 | ☐ リソース管理コンソールの**「オファリング (Offering)」**ページと**「料金」**ページで指定したメタデータの一部は、エクスポートして OSB に指定する必要があることを理解している。リソース管理コンソールから値をエクスポートすることで、リソース管理コンソールで生成されたサービス ID およびプラン ID のような重要な GUID をマップし、OSB にそれらを指定して、プラットフォームのプロビジョニング層が `catalog GET` エンドポイントの応答からこのプロビジョニング契約を読み取れるようにすることができる。<br><br>  ☐ `catalog.json` ファイルにリストされた必須の GUID と他の必須値をサンプル OSB のサービス配列に追加した。 | リソース管理コンソールから `catalog.json` ファイルをダウンロードした後、それを使用して Open Service Broker の開発に情報を提供します。catalog.json には、ブローカーでホストする必要があるメタデータが含まれます。これらの値によって、ブローカーがサポートするサービスとプランについて、ブローカーと IBM Cloud プラットフォーム間のプロビジョニング契約が定義されます。[ガイダンス](/docs/third-party/cis3-broker.html#learn-how-to-use-the-exported-metadata-to-guide-your-broker-development)に従って、エクスポートしたカタログ・メタデータを OSB に追加してください。| 開発環境と文書 |
| OSB のホスト | ☐ ブローカーのホストされるロケーションは、Transport Layer Security (TLS) プロトコル バージョン 1.2 に従う必要があることを理解している。さらに、ブローカーは、パブリック・インターネットでアクセスできる有効な HTTPS エンドポイントでホストされる必要がある。<br><br> | ブローカーは、REST API 呼び出しに応答できるアプリケーションの一部としてホストされなければなりません。また、ホストされるロケーションは、IBM Cloud のセキュリティー・ガイドラインに適合する必要があります。[ガイダンス](/docs/third-party/cis3-broker.html#host-your-brokers)に従って、ブローカーをホストしてください。| 開発環境と文書 |
| ホストされる OSB のテスト | ☐ ホストされるブローカーに対して curl コマンドを実行して応答を検証することで、ブローカーがサポートする各 API エンドポイントを検証した。<br><br> | 有効化するさまざまなエンドポイントに対して curl コマンドを実行することで、ブローカーを検証してください。[ガイダンス](/docs/third-party/cis3-broker.html#how-to-test-your-service-s-broker)に従って、ブローカーをホストしてください。| 開発環境と文書 |
| IAM リダイレクト URI の導出と設定 | ☐ OSB のホストされるロケーションといくつかの認証情報を使用して、IAM リダイレクト URL を正常に導出した。<br><br> ☐ **「リダイレクト URI (Redirect URI)」**を指定し、クライアント ID を正しく設定することで、リソース管理コンソールの**「アクセス管理 (Access Management)」**ページの入力を正常に完了した。<br><br> | リソース管理コンソールでサービスを定義したときに、クライアント ID を生成しましたが、その時点でリダイレクト URI はおそらく手元にありませんでした。つまり、IAM は `false` に設定されたクライアント ID を作成しました。**リダイレクト URI** を用意してリソース管理コンソールに戻るまで、真のクライアント ID はありません。[ガイダンス](/docs/third-party/cis5-iam.html#derive-your-iam-redirect-uri-resource-management-console-iam-page-)に従って、IAM リダイレクト URI を導出して設定してください。| 開発環境とリソース管理コンソール |
| 認証の OAuth フローの開発 | ☐ IAM は Open ID Connect (OIDC) をサポートすることを理解している。<br><br> ☐ IAM 地域エンドポイントを検出し、`dashboard_url` から、アセンブルされたリダイレクト URI にユーザーを正常にリダイレクトした。また、認証で使用できるように、応答で戻されたユーザーの `access_token` を保管した。<br><br> | サービス・ダッシュボードにアクセスするユーザーは、正しく認証されなければなりません。{{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) を使用して、Open Authorization トークン・ベースの認証と許可を開発します。[ガイダンス](/docs/third-party/cis5-iam.html#oauth)に従って、認証の OAuth フローを開発してください。| 開発環境と文書 |
| ユーザー許可の検証 | ☐ IAM と通信して、API キーのアクセス・トークンを入手できる <br><br> ☐ サービス・インスタンスに対するユーザーの許可を検証できる (/v2/authz POST)。 <br><br> | 認証の OAuth フローを開発したら、ユーザーが正しく許可されていることを検証し、サービスのユーザーがサービス・ダッシュボードにアクセスできるようにする必要があります。[ガイダンス](/docs/third-party/cis5-iam.html#validate)に従って、ユーザー許可を検証してください。| 開発環境と文書 |
{: caption="表 2. 統合請求オファリングの開発" caption-side="top"}

## オファリングの公開とテスト

| タスク | サブタスク | 説明 | 環境 |
|------| ----------| ------------|-----|
| 限定表示モードでオファリングを公開 | ☐ リソース管理コンソールの**「デプロイメント (Deployments)」**ページで、ホストされる OSB を正常に登録した。<br><br> ☐ リソース管理コンソールの**「デプロイメント (Deployments)」**ページで新しいデプロイメントを正常に作成し、1 つ以上の地域にオファリングを公開した。<br><br> |  OSB 仕様に適合した 1 つ以上のブローカーをホストしたので、リソース管理コンソールに戻って {{site.data.keyword.Bluemix_notm}} カタログにサービスを公開することができます。[ガイダンス](/docs/third-party/cis4-rmc-publish.html#publish-your-service-to-ibm-cloud)に従って、限定表示モードでオファリングを公開してください。| リソース管理コンソール |
| オファリングのテスト | ☐ ホワイトリストのアカウントでサインインし、https://console.bluemix.net のカタログで自分のサービスを表示できる。<br><br> ☐ サービス・インスタンス・ダッシュボードからの認証を正常に検証した。<br><br> ☐ オファリングがカタログに正しく表示されることを正常に検証した。<br><br> ☐ プロビジョニングが動作することを正常に検証した。プランを選択し、サービス・インスタンスを作成することができる。<br><br> ☐ プロビジョン解除が動作することを正常に検証した。サービス・インスタンスを削除できる。<br><br> ☐ バインドが動作することを正常に検証した。**「接続」**をクリックしてサービスを別のアプリケーションに接続できる。<br><br> ☐ アンバインドが動作することを正常に検証した。サービスを切断し、接続を削除できる。<br><br>  ☐ サービス・キーの作成とサービス・キーの削除が動作することを正常に検証した。**「資格情報」**をクリックしてサービス・キーを生成し、そのサービス・キーを削除できる。<br><br> ☐ IBM 担当員と作業して、エンドポイントの有効化と無効化がオファリングで正しくサポートされていることを検証した。<br><br> ☐ オファリングに従量制プランがあるため、使用量 の API の curl を実行して使用量に基づいた正確な料金を正しく戻すことによって、また、当該サービスのインスタンスをプロビジョンするすべてのユーザーをサポートして、使用量の自動毎時送信を有効にすることで、使用量送信を正常にテストした。|  OSB 仕様に適合した 1 つ以上のブローカーをホストしたので、リソース管理コンソールに戻って {{site.data.keyword.Bluemix_notm}} カタログにサービスを公開することができます。[ガイダンス](/docs/third-party/cis4-rmc-publish.html#test-your-deployed-offering)に従って、デプロイされたサービスをテストしてください。| {{site.data.keyword.Bluemix_notm}} コンソール |
{: caption="表 3. 統合請求オファリングの公開とテスト" caption-side="top"}

