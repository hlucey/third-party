---

copyright:

  years: 2018, 2019

lastupdated: "2019-02-25"

keywords: billing service, resource management console, Open Service Broker, end-to-end 

subcollection: third-party

---

{:right: .ph data-hd-position='right'}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# 全工程のチェックリスト
{: #checklist}

以下のチェックリストを利用して、統合請求サービスの定義、開発、公開に必要なすべてのタスクをトラッキングできます。
{:shortdesc}

## サービスの定義
{: #define}

| タスク | サブタスク | 説明 | 環境 |
|------| ----------| ------------|-----|
| {{site.data.keyword.Bluemix}} プラットフォームに関する理解 | ☐ プロビジョニング・レイヤー、{{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM)、カタログ、Open Service Broker、および計量サービスが連携する仕組みを理解している。 | {{site.data.keyword.Bluemix_notm}} 紹介サービスと異なり、統合請求サービスでは、{{site.data.keyword.Bluemix_notm}} プラットフォームを使用してサービス・インスタンスの作成、バインド、削除、課金を行います。 開発を円滑に開始するために、プラットフォームを含む重要コンポーネントに関する[詳細を参照してください](/docs/third-party?topic=third-party-how-it-works#how-it-works)。 | 資料 |
| {{site.data.keyword.Bluemix_notm}} Provider Workbench でのオファリングの登録 | ☐ コンテンツ・タスクを完了した。 <br><br>☐ 統合請求サービスとしてオファリングを公開する承認を得た。 <br><br> ☐ 資料 URL の値が含まれる E メールを受け取った。 <br><br> | 最初のステップは、Provider Workbench でオファリングを登録することです。 詳しくは、『[入門チュートリアル](/docs/third-party?topic=third-party-get-started#get-started)』を参照してください。 | Provider Workbench |
| {{site.data.keyword.Bluemix_notm}} 資料の公開 | ☐ Provider Workbench でガイダンス・タスクを開始した。 <br><br>☐ `資料 URL` を受け取った。 <br><br> ☐ 資料を正常に公開した。 <br><br> | Web サイトにホストされたサード・パーティー資料は優れています。 しかし、{{site.data.keyword.Bluemix_notm}} で統合請求サービスを提供するため、{{site.data.keyword.Bluemix_notm}} 統合請求のエクスペリエンスでカスタマイズされた資料を提供する必要があります。 詳しくは、[資料の作成](/docs/third-party?topic=third-party-content-tasks#content-tasks)を参照してください。 | Provider Workbench |
| マーケティング発表の公開 | ☐ Provider Workbench でマーケティング・タスクを開始した。 <br><br>  ☐ マーケティング発表を正常に公開した。 <br><br>  | {{site.data.keyword.Bluemix_notm}} ニュースレターおよびソーシャル・メディア・チャネルを通じてサービスの利用可能を発表するマーケティング販促用品を作成します。 詳しくは、[マーケティング発表の作成](/docs/third-party?topic=third-party-announcement#announcement)を参照してください。 | Provider Workbench |
| リソース管理コンソールでのオファリングの登録 | ☐ 一意的で意味の分かる `service-name` をリソース名で定義した。<br><br>  ☐ リソース管理コンソールにレコードがあることを正常に検証した。 <br><br>  | リソース管理コンソールを使用して、固有のオファリングを作成します。 詳しくは、[オファリングの登録手順](/docs/third-party?topic=third-party-register#register)を参照してください。 | リソース管理コンソール |
| リソース管理コンソールの「オファリング」ページの入力 | ☐ Provider Workbench オファリング E メールで提供された値を使用して、資料 URL および手順 URL を正しく設定した。 <br><br>  ☐ 請求および支払いの条項を含まない固有の「サービスのご利用条件」ページをポイントする URL を指定した。<br><br>  ☐ **「プラン変更のサポート (Plan changes supported?)」**が有効かどうかを、理解した上で正しく指定した。 ☐ サービスが「バインド可能」かどうかを、理解した上で正しく指定した。| {{site.data.keyword.Bluemix_notm}} タイルに表示されるカタログ・メタデータをリソース管理コンソールで指定します。 詳しくは、[オファリング・メタデータの入力手順](/docs/third-party?topic=third-party-offering-metadata#offering-metadata)を参照してください。 | リソース管理コンソール |
| リソース管理コンソールの「アクセス管理」ページの入力 | ☐ IAM を正常に有効にした。 <br><br>  ☐ 自分用に作成されたワンタイム生成 IAM API キーを保存した。 この API キーはリソース管理コンソールに保管されず、後で取得できないことを理解している。<br><br> ☐ Open Service Broker を開発してホストし、その後でリダイレクト URI を導出するまで、「アクセス管理」ページに入力できないことを理解している。<br><br> ☐ Open Service Broker をホストした後、IAM ページに戻り、このページの入力を正常に完了した。| リソース管理コンソールで {{site.data.keyword.Bluemix_notm}} IAM にオファリングを登録します。 IAM を使用すると、両方のプラットフォーム・サービスに関してユーザーをセキュアに認証でき、また {{site.data.keyword.Bluemix_notm}} プラットフォーム全体で一貫してリソースへのアクセスを制御できます。 詳しくは、[IAM への登録手順](/docs/third-party?topic=third-party-reg-iam#reg-iam)を参照してください。 | リソース管理コンソール |
| リソース管理コンソールでの 1 つ以上の価格プランの作成 | ☐ 固有の名前で無料プランを指定した。<br><br>  ☐ (オプション) IBM 担当員と協力して、有料プラン (サブスクリプションまたは従量制) を定義した。従量制プランを作成するにはデフォルトのサブスクリプション・プランの削除が必要であることを理解している。<br><br> ☐ (オプション) 自動の毎時使用量送信のホスティングと開発が必要であることを理解している。| サービスについてどのように課金しますか? リソース管理コンソールでは、無料または有料プランが提供されます。 詳しくは、[料金プランの作成手順](/docs/third-party?topic=third-party-pricing-plan#pricing-plan)を参照してください。 | リソース管理コンソール |
| リソース管理コンソールからのカタログ・メタデータのエクスポート | ☐ リソース管理コンソールの「オファリング」ページと「料金」ページに指定するメタデータの一部は、エクスポートされて Open Service Broker に指定される必要があることを理解している。 <br><br>  ☐ 「デプロイメント」ページから `catalog.json` ファイルを入手した。サービス配列を Open Service Broker のメタデータにマップする準備ができている。<br><br> | リソース管理コンソールでサービスを定義したので、`catalog.json` ファイルをダウンロードして使用し、Open Service Broker の開発に情報を提供することができます。 詳しくは、[メタデータのエクスポート手順](/docs/third-party?topic=third-party-export-metadata#export-meta)を参照してください。 | リソース管理コンソール |
{: caption="表 1. 統合請求サービスの定義" caption-side="top"}

## サービスの開発
{: #develop}

| タスク | サブタスク | 説明 | 環境 |
|------| ----------| ------------|-----|
| Open Service Broker バージョン 2.12 仕様に関する理解 | ☐ Open Service Broker 仕様を読み、自身の Open Service Broker を開発する必要があることを理解している。 <br><br>  |  サービス・ブローカーは、サービスのライフサイクルを管理します。 {{site.data.keyword.Bluemix_notm}} プラットフォームと Open Service Broker との相互作用によって、サービス・インスタンスおよびサービス・バインディングの作成と管理が行われます。 詳しくは、[サービス・ブローカーの開発とホスティング](/docs/third-party?topic=third-party-step3-osb#step3-osb)を参照してください。 | 資料 |
| {{site.data.keyword.Bluemix_notm}} ブローカー・サンプルの表示 | ☐ リポジトリーを複製し、ブローカー・サンプルを参照した。これらのサンプルを使用して開発を始める準備ができている。 <br><br>  |  [https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") | コード例 |
| {{site.data.keyword.Bluemix_notm}} Open Service Broker API 資料の確認 | ☐ Open Service Broker のコードがサポートしなければならない必須のエンドポイントがいくつかあることを理解している。 <br><br>  ☐ {{site.data.keyword.Bluemix_notm}} 内のアプリにバインドできるサービスは、API エンドポイントと資格情報をサービス・ユーザーに返す必要があることを理解している。 <br><br> ☐ サービス・インスタンスの無効化と再有効化を許可する拡張 API エンドポイントが {{site.data.keyword.Bluemix_notm}} で定義されたことを理解している。 |  {{site.data.keyword.Bluemix_notm}} Open Service Broker は、Open Service Broker 2.12 仕様を拡張します。 サービス・ブローカーが使用しなければならない必須のエンドポイントに関する[詳細を参照してください](/docs/third-party?topic=third-party-docs#docs)。 | 資料 |
| カタログ・メタデータを使用してサービス・ブローカーの開発を開始 | ☐ リソース管理コンソールで指定したメタデータの一部は、エクスポートされて Open Service Broker で指定される必要があることを理解している。  <br><br>  ☐ `catalog.json` ファイルにリストされた必須の GUID と他の必須値をサンプル Open Service Broker のサービス配列に追加した。 | リソース管理コンソールから `catalog.json` ファイルをダウンロードした後、それを使用して Open Service Broker の開発に情報を提供します。 詳しくは、[エクスポートされたメタデータを使用して開発をガイドする手順](/docs/third-party?topic=third-party-use-metadata#use-metadata)を参照してください。 | 開発環境と資料 |
| Open Service Broker のホスト | ☐ サービス・ブローカーのホストされるロケーションは、Transport Layer Security (TLS) プロトコル・バージョン 1.2 に従う必要があることを理解している。 <br><br> | サービス・ブローカーは、REST API 呼び出しに応答できるアプリの一部としてホストされなければなりません。 また、ホストされるロケーションは、{{site.data.keyword.Bluemix_notm}} のセキュリティー・ガイドラインに適合する必要があります。 詳しくは、[サービス・ブローカーをホストする手順](/docs/third-party?topic=third-party-host#host)を参照してください。 | 開発環境と資料 |
| ホストされた Open Service Broker のテスト | ☐ ホストされたサービス・ブローカーに対して curl コマンドを実行することによって、サービス・ブローカーがサポートする各 API エンドポイントを検証した。 <br><br> | 有効化する各エンドポイントに対して curl コマンドを実行することによって、サービス・ブローカーを検証します。 詳しくは、[サービス・ブローカーのテスト手順](/docs/third-party?topic=third-party-host#broker-test)を参照してください。| 開発環境と資料 |
| IAM リダイレクト URI の導出と設定 | ☐ Open Service Broker のホストされるロケーションといくつかの認証情報を使用して、IAM リダイレクト URI を正常に導出した。 <br><br> ☐ リダイレクト URI を指定し、クライアント ID を正しく設定することによって、「アクセス管理」ページの入力を正常に完了した。 <br><br> | リソース管理コンソールでサービスを定義するときにクライアント ID を生成しますが、その時点ではリダイレクト URI を入手していなかった可能性が高いことに注意してください。 クライアント ID は `false` に設定されます。 リダイレクト URI を取得してリソース管理コンソールに戻るまでは、クライアント ID は true に設定されません。 詳しくは、[リダイレクト URI の導出手順](/docs/third-party?topic=third-party-redirect-uri#redirect-uri)を参照してください。 | 開発環境とリソース管理コンソール |
| 認証のための Open Authorization (OAuth) フローの作成 | ☐ IAM は Open ID Connect (OIDC) をサポートすることを理解している。 <br><br> ☐ IAM 地域エンドポイントを検出し、`dashboard_url` から、アセンブルされたリダイレクト URI にユーザーを正常にリダイレクトした。また、認証で使用できるように、応答で戻されたユーザーの `access_token` を保管した。 <br><br> | サービス・ダッシュボードにアクセスするユーザーは、正しく認証されなければなりません。 IAM を使用して、OAuth トークン・ベースの認証および許可を作成します。 詳しくは、[OAuth フローの作成手順](/docs/third-party?topic=third-party-oauth#oauth)を参照してください。 | 開発環境と資料|
| ユーザー許可の検証 | ☐ API キーのアクセス・トークンを取得できる。 <br><br> ☐ サービス・インスタンスへのユーザーの許可を検証できる。 <br><br> | 認証のための OAuth フローを作成した後、サービスのユーザーがサービス・ダッシュボードにアクセスできるように、ユーザーが正しく許可されていることを検証する必要があります。 詳しくは、[検証手順](/docs/third-party?topic=third-party-validate#validate)を参照してください。 | 開発環境と資料 |
{: caption="表 2. 統合請求サービスの開発" caption-side="top"}

## サービスの公開およびテスト
{: #pubtest}

| タスク | サブタスク | 説明 | 環境 |
|------| ----------| ------------|-----|
| 限定表示モードでのサービスの公開 | ☐ リソース管理コンソールの「デプロイメント」ページで、ホストされた Open Service Broker を正常に登録した。 <br><br> ☐ 新しいデプロイメントを正常に作成し、1 つ以上の地域にオファリングを公開した。 <br><br> |  これで、ホストされたサービス・ブローカーは Open Service Broker 仕様を満たしていて、サービスを {{site.data.keyword.Bluemix_notm}} カタログに公開できます。 詳しくは、[サービスの公開手順](/docs/third-party?topic=third-party-publish#publish)を参照してください。 | リソース管理コンソール |
| オファリングのテスト | ☐ カタログで自分のサービスを確認できる。 <br><br> ☐ サービス・インスタンス・ダッシュボードからの認証を検証した。 <br><br> ☐ カタログにサービスが正しく表示されることを検証した。 <br><br> ☐ プランを選択し、サービス・インスタンスを作成することができる。 <br><br> ☐ サービス・インスタンスを削除することができる。 <br><br> ☐ サービスを別のアプリケーションに接続できる。 <br><br> ☐ サービスを切断し、接続を削除できる。 <br><br>  ☐ サービス・キーを生成し、そのサービス・キーを削除することができる。 <br><br> ☐ IBM 担当員と作業して、エンドポイントの有効化と無効化がオファリングで正しくサポートされていることを検証した。 <br><br> ☐ オファリングには従量制プランがあるため、使用量送信を正常にテストした。 | これで、ホストされたサービス・ブローカーは Open Service Broker 仕様を満たしていて、サービスを {{site.data.keyword.Bluemix_notm}} カタログに公開できます。 詳しくは、[サービスのテスト手順](/docs/third-party?topic=third-party-test-your-service#test)を参照してください。 | {{site.data.keyword.Bluemix_notm}} コンソール |
{: caption="表 3. 統合請求サービスの公開とテスト" caption-side="top"}

