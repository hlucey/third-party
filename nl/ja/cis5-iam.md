---


copyright:
  years: 2018
lastupdated: "2018-06-22"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# ステップ 4: 認証フローの作成

オファリングを定義した際、リソース管理コンソールの**「アクセス管理」**ページに、{{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) のクライアント ID と秘密鍵、サービス ID、および API キーが提供されました。次に、これらの値を使用して以下の手順を実行します。

1. `dashboard_url` の処理に基づいてリダイレクト URI を取得し、リソース管理コンソールに戻り、クライアント ID の更新を確認して、取得したリダイレクト URI を IAM タブに追加します。
2. 認証のための OAuth フローを作成します。このフローを完了するには、リダイレクト URI、クライアント ID、およびクライアント秘密鍵を `token_endpoint` IAM Rest API のパラメーターとして使用します。
3. 以下のようにしてユーザー許可を検証します。
   1. IAM と通信して API キーからアクセス・トークンを取得します
   2. `authorization_endpoint` を使用して、サービス・ダッシュボードへのユーザーの許可を検証します (/v2/authz POST)

このステップは、ユーザーが統合請求サービスを提供することを承認済みであると想定しています。PWB での初期登録と承認がまだ完了していない場合は、[概要: {{site.data.keyword.Bluemix_notm}} での第三者オファリングの公開](/docs/third-party/index.html)を参照してください。
{: tip}

## 始める前に

ステップ 1 を開始しており、ステップ 2 と 3 を完了していることを確認してください。
1. [サービス文書とマーケティング発表を作成する](/docs/third-party/cis1-docs-marketing.html)。
2. [リソース管理コンソールでオファリングを定義する](/docs/third-party/cis2-rmc-define.html)。
3. [サービス・ブローカーを作成してホストする](/docs/third-party/cis3-broker.html)。


## IAM リダイレクト URI の取得 (リソース管理コンソール: IAM ページ)

リソース管理コンソールでサービスを定義した際にクライアント ID を生成しましたが、その時点ではリダイレクト URI を取得しなかった可能性が高い点に注意してください。つまり、IAM はクライアント ID を作成しましたが、それは false に設定されています。リダイレクト URI を取得してリソース管理コンソールに戻るまでは、クライアント ID は true に設定されません。

前の作成ステップで OSB を作成してホストしています (おそらく、サンプル・ブローカー・コードに IAM の値が表示されたはずです)。通常、`redirect_uri` は、アプリが稼働するホスト URL で、認証/許可を処理するいくつかの追加 URL があります。

 いくつかのサンプル・リダイレクト URI を以下に示します。

```
https://myapp.bluemix.net/integrate/auth/callback
http://localhost:3000/auth/callback <-- for testing locally
```

以下のようにして、リソース管理コンソールに戻り、リダイレクト URI を IAM タブに追加します。

1. コンソールにサインインします。
2. リダイレクト URI をグラブします。
3. リソース管理コンソールに戻ります。
4. **「IAM」タブ**から、リダイレクト URI を**「リダイレクト URI」**フィールドに貼り付けます。
5. **「クライアント ID の更新」**をクリックして、クライアント ID を更新します。

これで、クライアント ID はリダイレクト URI を認識し、true に設定されます。次のステップではそのクライアント ID を使用して OAuth フローを作成できます。

## 認証のための OAuth フローの作成
{: #oauth}


**認証 - ステップ 0:** `https://iam.bluemix.net/identity/.well-known/openid-configuration` を呼び出して、デプロイしたアプリケーションに最も近い UI ログイン用の IAM 地域エンドポイントを見つけます。

```
curl -X GET \
  https://iam.bluemix.net/identity/.well-known/openid-configuration
```

```
HTTP/1.1 200 OK
Content-Type: application/json
{
  "issuer": "https://iam.bluemix.net/identity",
  "authorization_endpoint": "https://iam-region2.bluemix.net/identity/authorize",
  "token_endpoint": "https://iam-region2.bluemix.net/identity/token",
...
}
```

この要求は、アプリケーションが開始されたときに 1 度実行でき、`authorization_endpoint` が失敗した場合、再度実行できます。`authorization_endpoint` 値は、時間短縮のためにキャッシュに入れることができ、キャッシュの期限が切れた後、またはエラーが発生した後に最新表示できます。


**認証 - ステップ 1:** ユーザーが `dashboard_url` にナビゲートしたら、ブラウザーを `<authorization_endpoint>?client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&response-type=code&state=<your-resource-instance-id>` にリダイレクトします。


-> ログイン・プロンプトが表示されます

-> ユーザーが資格情報を入力します

-> ブラウザーがリダイレクト URI をコールバックし、「code」応答パラメーターと「state」値が提供されます


**認証 - ステップ 2:** アクセス・トークン呼び出しのためのコードの交換

### POST <token_endpoint>

#### ヘッダー:
  - Authorization: Basic *[client id]: [client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### パラメーターの使用:
  - client_id=*[client id]*
  - client_secret=*[client secret]*
  - grant_type=authorization_code
  - response_type=cloud_iam
  - redirect_uri=*[same uri as redirect_uri from step 1]*
  - code=*[code from callback]*

```
curl -k -X POST \
  -u "<your-client-id>:<your-client-secret>" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "Accept: application/json" \
  --data-urlencode "client_id=<your-client-id>" \
  --data-urlencode "client_secret=<your-client-secret>" \
  --data-urlencode "grant_type=authorization_code" \
  --data-urlencode "response_type=cloud_iam" \
  --data-urlencode "code=<code-from-the-callback>" \
  --data-urlencode "redirect_uri=<redirect_uri>" \
  "https://iam-region2.bluemix.net/identity/token"
```
{: codeblock}

### 応答:

```
{
  "access_token": "eyJraWQiOiI......XmpBTIDdR5w",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}

  この応答で返されるユーザーの access_token は、次のユーザー許可で使用されるため、必ず保管してください。

次のサンプル・ブローカーにある例を参照してください: https://github.com/IBM/sample-resource-service-brokers

## ユーザー許可の検証
{: #validate}

1. IAM と通信して、API キーのアクセス・トークンを取得します
2. サービス・インスタンスへのユーザーの許可を検証します (/v2/authz POST)

### 許可 - ステップ 1: API キーを使用した {{site.data.keyword.Bluemix_notm}} IAM トークンの取得
{: #iam_token_using_api_key}

### POST /identity/token

#### ヘッダー:
  - Authorization: Basic *[client id]: [client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### パラメーターの使用:
  - grant_type=urn:ibm:params:oauth:grant-type:apikey
  - response_type=cloud_iam
  - apikey=*[API キー]*

```
curl -k -X POST \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "response_type=cloud_iam" \
  --data-urlencode "apikey=<apikey>" \
  "https://iam-region2.bluemix.net/identity/token"
```
{: codeblock}

### 応答:

```
{
  "access_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}

**注:** このトークンの有効期限は 1 時間で、その 1 時間の時間フレームの間に、必要なだけ何回でも再使用できます。`dashboard_url` へのすべてのアクセスでこの要求を行わずに済むように、このトークンはキャッシュに入れておくことを推奨します。


### 許可 - ステップ 2: サービス・インスタンスへのユーザーの許可の確認 (/v2/authz POST)

ユーザーを認証し、独自のアクセス・トークンを取得したので、次に、ユーザーがサービス・ダッシュボードにアクセスできることを確認する必要があります。最初に、ステップ 2.1 でデコードするユーザーのアクセス・トークンに含まれているいくつかの情報が必要になります。次に、ステップ 2.2 で、その情報を使用して IAM を呼び出し、ユーザーがダッシュボードにアクセスする権限を持っているかどうかを確認します。

**ステップ 2.1**: (上記の `**Authentication - Step 2:** Exchange the code for an access token ` 中に返された) ユーザーのアクセス・トークンをデコードします。これは、任意の JWT 準拠のライブラリーを使用してデコードできる JWT トークンです。例えば、[sample broker code](https://github.com/IBM/sample-resource-service-brokers) に含まれているライブラリーを参照してください。トークンがデコードされると、フォーマットは以下のようになります。次のステップで使用する `iam_id` フィールドと `scope` フィールドの抽出が必要になります。

```
{
  "iam_id": "IBMid-XXXXXXX",
  "id": "IBMid-XXXXXXX",
  "realmid": "IBMid",
  "identifier": "XXXXXXX",
  "given_name": "Don",
  "family_name": "Quixote",
  "name": "Don Quixote",
  "email": "quixote@email.com",
  "sub": "quixote@email.com",
  "account": {
    "bss": "123123123123123"
  },
  "iat": 1522114004,
  "exp": 1522117604,
  "iss": "https://iam.bluemix.net/identity",
  "grant_type": "urn:ibm:params:oauth:grant-type:apikey",
  "scope": "openid <your serviceName>",
  "client_id": "bx",
  "acr": 1,
  "amr": [
    "pwd"
  ]
}
```

**ステップ 2.2**: IAM を呼び出して、ユーザーがダッシュボードにアクセスする権限を持っているかどうかを確認します。

```
curl -X POST \
  -H "Accept: application/json" \
  -H "Authorization: <access token from step 1>" \
  -d '[ \
    { \
      "subject" : \
      { \
        "attributes": \
        { \
          "id": "<iam_id field value from user's token>", \
          "scope": "<scope field value from user's token>" \
        } \
      }, \
      "resource" : \
      { \
        "crn" : "<resource instance CRN>" \
      }, \
      action : <your service name> + ".dashboard.view" \
    } \
  ]' \
  https://iam.bluemix.net/v2/authz
```

次のサンプル・ブローカーにある例を参照してください: https://github.com/IBM/sample-resource-service-brokers

## サード・パーティー・アダプター用の {{site.data.keyword.Bluemix_notm}} Identity and Access Management トークンのスコープ指定
{: #token_scoping}

クライアント ID を使用して作成されたユーザー・アクセス・トークンは、ユーザーのサービス API にアクセスするためだけに使用できます。このトークンを使用して他のクラウド API への要求を行うと、ユーザーが構成済みの適切なポリシーを持っている場合でも、アクセスは拒否されます。

サード・パーティー統合の一部として、ユーザーの目的を実現するのに必要な最小アクセス・スコープをトークンが持っていることを確認するために、トークンのスコープ指定が使用されています。これを可能にするために、IAM トークンは、そのトークンを作成したクライアント ID に基づいたアクセス権限を持ちます。つまり、IAM トークンがサード・パーティー・サービスによって作成された場合、構成済みの適切なポリシーをエンド・ユーザーが持っていたとしても、そのユーザーは特定の API および機能を実行できません。

許可へのインパクト (`https://iam.bluemix.net/v2/authz` へのすべての呼び出し) は、サブジェクトでの `scope` 情報の受け渡しが必要になることです。この情報は、IAM トークン (base64 エンコード) 内の `scope` クレームに含まれています。

許可呼び出しに追加された項目の例を以下に示します。
```
  [
   {  Headers
   `Authorization` -> a jwt token representing a 3rd party service and/or dashboard
   `Transaction-ID` -> "a unique guid lets us help trace the request end to end"
   `Accept` -> `application/vnd.authz.v2+json`
   `Content-Type` -> `application/json`

      Body
      "subject":{
         "attributes":{
            "id":"IBMid-123",
            "scope":"libraryservice openid"
         }
      },
      "action":"libraryservice.books.read",
      "resource":{
         "attributes":{
            "serviceName":"libraryservice",
            "serviceInstance":"12345",
            "accountId":"123456789"
         }
      }
   }
]
```
{: codeblock}

これはすべての使用法 (`user, serviceId, crn`) に適用され、すべての `subject.attributes` にスコープが必要です。

## 次のステップ

次に、すべての事項をまとめます。リソース管理コンソールに戻り、限定表示モードでサービスを公開して、カタログでオファリングを確認します。[サービスの公開およびテスト](/docs/third-party/cis4-rmc-publish.html)を参照。
