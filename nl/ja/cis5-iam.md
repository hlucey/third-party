---


copyright:
  years: 2018
lastupdated: "2018-08-28"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# ステップ 4. 認証フローの作成
{: #step4-iam}

オファリングを定義するとき、リソース管理コンソールの「アクセス管理」ページに {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) のクライアント ID と秘密鍵、サービス ID、および API キーがリストされます。それらの値を使用して認証フローを作成する準備ができました。
{:shortdesc}

## 始める前に
{: #pre-reqs}

[入門チュートリアル](/docs/third-party/index.html)を完了し、統合請求サービスの提供が承認されていることを確認してください。

## IAM リダイレクト URI の導出
{: #redirect-uri}

リソース管理コンソールでサービスを定義するときにクライアント ID を生成しますが、その時点ではリダイレクト URI はおそらく手元にないことに注意してください。IAM によって作成されるのは、false に設定されたクライアント ID です。リダイレクト URI を取得してリソース管理コンソールに戻るまでは、クライアント ID は true に設定されません。

前の作成ステップで OSB を作成してホストしています (おそらく、サンプル・ブローカー・コードに IAM の値が表示されたはずです)。 通常、`redirect_uri` は、アプリが稼働するホスト URL で、認証/許可を処理できるいくつかの追加 URL があります。

 以下はリダイレクト URI の例です。

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

これで、クライアント ID はリダイレクト URI を認識し、true に設定されます。 次のステップではそのクライアント ID を使用して OAuth フローを作成できます。

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

この要求は、アプリケーションが開始されたときに 1 度実行でき、`authorization_endpoint` が失敗した場合、再度実行できます。 この時点で、`authorization_endpoint` 値を短時間の間キャッシュに入れることができ、キャッシュの期限が切れた後、またはエラーが発生した後にリフレッシュできます。


**認証 - ステップ 1:** ユーザーが `dashboard_url` にナビゲートしたら、ブラウザーを `<authorization_endpoint>?client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&response-type=code&state=<your-resource-instance-id>` にリダイレクトします。


-> ログイン・プロンプトが表示されます

-> ユーザーが資格情報を入力します

-> ブラウザーがリダイレクト URI をコールバックし、「code」応答パラメーターと「state」値が提供されます


**認証 - ステップ 2:** アクセス・トークン呼び出しのためのコードの交換

### POST <token_endpoint>

#### ヘッダー:
{: #headers1}

  - Authorization: Basic *[client id]: [client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### パラメーターの使用:
{: #parameters1}

  - client_id=*[client id]*
  - client_secret=*[client secret]*
  - grant_type=authorization_code
  - response_type=cloud_iam
  - redirect_uri=*[same URI as redirect_uri from step 1]*
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
{: #response1}

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

1. IAM と通信して、API キーのアクセス・トークンを取得します。
2. サービス・インスタンスへのユーザーの許可を検証します (/v2/authz POST)。

### 許可 - ステップ 1: API キーを使用した {{site.data.keyword.Bluemix_notm}} IAM トークンの取得
{: #iam_token_using_api_key}

### POST /identity/token

#### ヘッダー:
{: #headers2}

  - Authorization: Basic *[client id]: [client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### パラメーターの使用:
{: #parameters2}

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
{: #response2}

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

**注:** このトークンの有効期限は 1 時間で、その 1 時間の時間フレームの間に、必要なだけ何回でも再使用できます。 `dashboard_url` へのすべてのアクセスでこの要求を行わずに済むように、このトークンはキャッシュに入れておくことを推奨します。


### 許可 - ステップ 2: サービス・インスタンスへのユーザーの許可の確認 (/v2/authz POST)

ユーザーを認証し、独自のアクセス・トークンを取得したので、次に、ユーザーがサービス・ダッシュボードにアクセスできることを確認する必要があります。 最初に、ステップ 2.1 でデコードするユーザーのアクセス・トークンに含まれているいくつかの情報が必要になります。 次に、ステップ 2.2 で、その情報を使用して IAM を呼び出し、ユーザーがダッシュボードにアクセスする権限を持っているかどうかを確認します。

**ステップ 2.1**: (前のセクションの `認証 - ステップ 2: アクセス・トークン呼び出しのためのコードの交換`で返された) ユーザーのアクセス・トークンをデコードします。
   アクセス・トークンは、任意の JWT 準拠ライブラリーを使用してデコードできる JWT トークンです。例えば、[sample broker code](https://github.com/IBM/sample-resource-service-brokers) に含まれているライブラリーを参照してください。
   トークンがデコードされた後、フォーマットは次のセクションで示されているようになります。次のステップで使用される `iam_id` フィールドと `scope` フィールドを抽出します。

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

## サード・パーティー・アダプターの IAM トークンのスコープ
{: #token_scoping}

クライアント ID を使用して作成されたユーザー・アクセス・トークンは、ユーザーのサービス API にアクセスするためだけに使用できます。 このトークンを使用して他のクラウド API への要求を行うと、ユーザーが構成済みの適切なポリシーを持っている場合でも、アクセスは拒否されます。

サード・パーティー統合の一部として、ユーザーの目的を実現するのに必要な最小アクセス・スコープをトークンが持っていることを確認するために、トークンのスコープ指定が使用されています。 これを可能にするために、IAM トークンのアクセス権限は、トークンを作成したクライアント ID に基づきます。IAM トークンがサード・パーティー・サービスによって作成された場合、エンド・ユーザーは、構成済みの適切なポリシーを持っていたとしても、特定の API および機能を実行できません。

許可へのインパクト (`https://iam.bluemix.net/v2/authz` へのすべての呼び出し) は、サブジェクトでの `scope` 情報の受け渡しが必要になることです。 この情報は、IAM トークン (base64 エンコード) 内の `scope` クレームに含まれています。

以下のセクションは、許可呼び出しに追加されるものの例です。
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
{: #next-steps}

次に、すべての事項をまとめます。 リソース管理コンソールに戻り、限定表示モードでサービスを公開して、カタログでオファリングを確認します。 [サービスの公開およびテスト](/docs/third-party/cis4-rmc-publish.html)を参照。
