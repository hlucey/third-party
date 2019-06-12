---

copyright:

  years: 2018, 2019

lastupdated: "2019-05-30"

keywords: access token, client ID, Access Manage page, authentication flow 

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 步骤 4. 开发认证流程
{: #step4-iam}

定义产品时，资源管理控制台中的“访问管理”页面列出了 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 客户机标识和私钥、服务标识和 API 密钥。现在，您已准备就绪，可以使用这些值来开发认证流程。
{:shortdesc}

## 开始之前
{: #iam-pre-reqs}

确保已完成[入门教程](/docs/third-party?topic=third-party-get-started#get-started)，并且已获得交付综合计费服务的许可。

## 派生 IAM 重定向 URI
{: #redirect-uri}

在资源管理控制台中定义服务时，您会生成客户机标识，但请注意，此时您可能并没有重定向 URI。IAM 创建的是设置为 false 的客户机标识。在使用“重定向 URI”返回到资源管理控制台之前，您不会拥有设置为 true 的客户机标识。

好消息是，在先前的开发步骤中，您已开发了 OSB 并对其进行了托管（可能在样本代理程序代码中会看到 IAM 值）。`redirect_uri` 通常是应用程序所在的主机 URL，以及其他一些可以处理认证/授权的 URL。

 以下示例显示重定向 URI：

```
https://<myapp>.cloud.ibm.com/integrate/auth/callback
http://localhost:3000/auth/callback <-- for testing locally
```

返回到资源管理控制台，并将重定向 URI 添加到 IAM 选项卡：

1. 登录到控制台。
2. 抓取重定向 URI。
3. 返回到资源管理控制台。
4. 在 **IAM** 选项卡中，将重定向 URI 粘贴到**重定向 URI** 字段中。
5. 单击**更新客户机标识**以更新客户机标识。

现在，您已拥有一个能够识别重定向 URI 且设置为 true 的客户机标识！您可以在后续步骤中使用该客户机标识来开发 OAuth 流程。

## 开发用于认证的 OAuth 流程
{: #oauth}


**认证 - 步骤 0：**通过调用 `https://iam.cloud.ibm.com/identity/.well-known/openid-configuration` 来找到离已部署应用程序更近的 UI 登录的 IAM 区域端点。

```
curl -X GET \
  https://iam.cloud.ibm.com/identity/.well-known/openid-configuration
```

```
HTTP/1.1 200 OK
Content-Type: application/json
{
  "issuer": "https://iam.cloud.ibm.com/identity",
  "authorization_endpoint": "https://iam-region2.cloud.ibm.com/identity/authorize",
  "token_endpoint": "https://iam-region2.cloud.ibm.com/identity/token",
...
}
```

此请求可在应用程序启动时执行一次，并且如果 `authorization_endpoint` 失败，可再次执行此请求。现在您能够对 `authorization_endpoint` 值进行短时间高速缓存，并在高速缓存到期或遇到错误后进行刷新。


**认证 - 步骤 1：**用户导航至 `dashboard_url` 时，将浏览器重定向到 `<authorization_endpoint>?client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&response-type=code&state=<your-resource-instance-id>`

* 如果用户已登录，那么会立即对其执行重定向。浏览器执行回调以重定向 URI，从而提供“code”响应参数和“state”值。
* 如果用户未登录，那么会显示登录提示。成功登录后，浏览器会执行回调以重定向 URI，从而提供“code”响应参数和“state”值。

**认证 - 步骤 2：**用代码交换访问令牌调用

### POST <token_endpoint>
{: #token-post}

#### 头：
{: #headers1}

  - Authorization: Basic *[client id]:[client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### 参数：
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
  "https://iam-region2.cloud.ibm.com/identity/token"
```
{: codeblock}

### 响应：
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

  确保存储此响应中返回的用户 access_token，因为在接下来用户授权期间将使用此项。

请参阅[样本代理程序](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中的示例。

## 下面将验证用户授权
{: #validate}

1. 与 IAM 通信以获取 API 密钥的访问令牌。
2. 验证用户对服务实例的权限 (/v2/authz POST)。

### 授权 - 步骤 1：使用 API 密钥获取 {{site.data.keyword.Bluemix_notm}} IAM 令牌。
{: #iam_token_using_api_key}

### POST /identity/token
{: #post}

#### 头：
{: #headers2}

  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### 参数：
{: #parameters2}

  - grant_type=urn:ibm:params:oauth:grant-type:apikey
  - response_type=cloud_iam
  - apikey=*[Api key]*

```
curl -k -X POST \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "response_type=cloud_iam" \
  --data-urlencode "apikey=<apikey>" \
  "https://iam.cloud.ibm.com/identity/token"


```
{: codeblock}

### 响应：
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

**注：**此令牌一小时内有效，在一小时的时间范围内可以根据需要多次复用此令牌。强烈建议对此令牌进行高速缓存，以避免对 `dashboard_url` 的每次访问都执行此请求。


### 授权 - 步骤 2：验证是否授予用户对服务实例的权限 (/v2/authz POST)
{: #step-2-authorization}

现在，您已认证用户并拥有自己的访问令牌，接下来需要验证用户是否能够访问服务仪表板。首先，您需要用户访问令牌中包含的一些信息，在步骤 2.1 中将对该令牌解码。然后，在步骤 2.2 中，使用这些信息来调用 IAM，以检查用户是否有权访问仪表板。

**步骤 2.1**：对用户的访问令牌（在上一部分中所述的`**认证 - 步骤 2：**用代码交换访问令牌`期间返回）解码。访问令牌是可使用任何兼容 JWT 的库进行解码的 JWT 令牌。例如，请参阅[样本代理程序代码](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中包含的库。
   对令牌解码后，其格式如以下部分中所示；您需要抽取 `iam_id` 和 `scope` 字段，以在下一步中使用：

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
  "iss": "https://iam.cloud.ibm.com/identity",
  "grant_type": "urn:ibm:params:oauth:grant-type:apikey",
  "scope": "openid <your serviceName>",
  "client_id": "bx",
  "acr": 1,
  "amr": [
    "pwd"
  ]
}
```

**步骤 2.2**：调用 IAM 以检查用户是否有权访问仪表板

```
curl -X POST \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
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
  https://iam.cloud.ibm.com/v2/authz
```

请参阅[样本代理程序](https://github.com/IBM/sample-resource-service-brokers)中的示例。

## 针对第三方采用者的 IAM 令牌作用域限定
{: #token_scoping}

通过您的客户机标识创建的用户访问令牌只能用于访问您的服务 API。使用此令牌向其他云 API 发出的请求将导致访问被拒绝，即使该用户已配置相应的策略也是如此。

作为第三方集成的一部分，令牌作用域限定用于确保令牌具有实现用户目标所需的最小访问作用域。为了帮助达到此目的，IAM 令牌的访问权将基于创建令牌的客户机标识。如果 IAM 令牌是由第三方服务创建的，那么最终用户将无法运行某些 API 和功能，即使该用户已配置相应的策略也是如此。

对授权的影响（对 `https://iam.cloud.ibm.com/v2/authz` 的所有调用）需要在主题中向下传递 `scope` 信息。此信息包含在 `scope` 声明中的 IAM 令牌（base64 编码）内。

以下部分是在授权调用中添加的内容的示例：
```
  [
   {  Headers
   `Authorization` -> 表示第三方服务和/或仪表板的 JWT 令牌
   `Transaction-ID` -> "唯一的 GUID 允许我们帮助以端到端方式跟踪请求"
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

这适用于所有用途（`user、serviceId、crn`），并且所有 `subject.attributes` 都需要作用域。

## 后续步骤
{: #cis5-test}

现在该把所有内容融会贯通在一起了！返回到资源管理控制台，在有限的可视范围内发布服务，并在目录中验证产品。有关更多信息，请参阅[发布和测试服务](/docs/third-party?topic=third-party-step5-pubtest#step5-pubtest)。
