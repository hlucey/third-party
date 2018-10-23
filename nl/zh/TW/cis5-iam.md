---


copyright:
  years: 2018
lastupdated: "2018-10-12"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 步驟 4. 開發鑑別流程
{: #step4-iam}

當您定義供應項目時，資源管理主控台中的「存取管理」頁面會列出您的 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 用戶端 ID 及密碼、服務 ID 和 API 金鑰。現在，您可以使用那些值來開發鑑別流程。
{:shortdesc}

## 開始之前
{: #pre-reqs}

請確定您已完成[入門指導教學](/docs/third-party/index.html)，並且已獲准提供整合式計費服務。

## 衍生 IAM 重新導向 URI
{: #redirect-uri}

當您在資源管理主控台中定義服務時，會產生用戶端 ID，但請注意，您在當時可能沒有「重新導向 URI」。IAM 會建立設為 false 的「用戶端 ID」。在您使用「重新導向 URI」回到資源管理主控台之前，不會有真正的「用戶端 ID」。

好消息是在前一個開發步驟中，您已開發並管理 OSB（您可能已在範例分配管理系統程式碼中看到 IAM 值）。`redirect_uri` 通常是應用程式所在的主機 URL，以及可處理鑑別/授權的某個其他 URL。

 下列範例顯示重新導向 URI：

```
https://myapp.bluemix.net/integrate/auth/callback
http://localhost:3000/auth/callback <-- for testing locally
```

回到資源管理主控台，並將您的重新導向 URI 新增至 IAM 標籤：

1. 登入主控台。
2. 抓取重新導向 URI。
3. 回到資源管理主控台。
4. 從 **IAM 標籤**中，將您的重新導向 URI 貼入**重新導向 URI** 欄位。
5. 按一下**更新用戶端 ID**，以更新「用戶端 ID」。

您現在具有瞭解「重新導向 URI」且設為 true 的「用戶端 ID」！您可以在後續步驟中使用該「用戶端 ID」，以開發 OAuth 流程。

## 開發 OAuth 流程以進行鑑別
{: #oauth}


**鑑別 - 步驟 0：**呼叫 `https://iam.bluemix.net/identity/.well-known/openid-configuration`，以尋找較接近已部署應用程式之使用者介面登入的 IAM 地區端點。

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

這個要求可以在啟動應用程式時執行一次，並且在 `authorization_endpoint` 失敗的情況下再次執行。您現在可以在短時間內快取 `authorization_endpoint` 值，並在快取過期或發生錯誤之後重新整理。


**鑑別 - 步驟 1：**當使用者導覽至 `dashboard_url` 時，會將瀏覽器重新導向至 `<authorization_endpoint>?client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&response-type=code&state=<your-resource-instance-id>`


-> 會顯示登入提示

-> 使用者輸入認證

-> 重新導向 URI 的瀏覽器回呼，提供 "code" 回應參數及 "state" 值


**鑑別 - 步驟 2：**交換存取記號的代碼

### POST <token_endpoint>
{: #post}

#### 標頭：
{: #headers1}

  - Authorization: Basic *[client id]:[client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### 使用參數：
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

### 回應：
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

  請務必儲存此回應中所傳回的使用者 access_token，因為下次使用者授權期間會使用它。

請參閱範例分配管理系統中的範例：https://github.com/IBM/sample-resource-service-brokers

## 立即驗證使用者授權
{: #validate}

1. 與 IAM 通訊，以取得 API 金鑰的存取記號。
2. 驗證使用者的服務實例授權 (/v2/authz POST)。

### 授權 - 步驟 1：使用「API 金鑰」取得 {{site.data.keyword.Bluemix_notm}} IAM 記號。
{: #iam_token_using_api_key}

### POST /identity/token

#### 標頭：
{: #headers2}

  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### 使用參數：
{: #parameters2}

  - grant_type=urn:ibm:params:oauth:grant-type:apikey
  - response_type=cloud_iam
  - apikey=*[API 金鑰]*

```
curl -k -X POST \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "response_type=cloud_iam" \
  --data-urlencode "apikey=<apikey>" \
  "https://iam.bluemix.net/identity/token"
```
{: codeblock}

### 回應：
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

**附註：**此記號的有效時間是一小時，而且可以在這一小時的時間範圍期間重複使用所需的次數。強烈建議您快取此記號，以避免在每次存取 `dashboard_url` 時都執行此要求。


### 授權 - 步驟 2：驗證使用者的服務實例授權 (/v2/authz POST)
{: #step-2-authorization}

既然您已鑑別使用者並且具有自己的存取記號，就需要驗證使用者可以存取服務儀表板。首先，您需要使用者存取記號中所含的一些資訊，使用者存取記號將在步驟 2.1 解碼。然後，在步驟 2.2 使用該資訊來呼叫 IAM，確認使用者是否獲得授權存取儀表板。

**步驟 2.1**：將使用者的存取記號解碼（在前一段找到的`**鑑別 - 步驟 2：**交換存取記號的代碼`期間所傳回。）
   存取記號是一個 JWT 記號，可以使用任何遵循 JWT 的程式庫來解碼。例如，請參閱[範例分配管理系統程式碼](https://github.com/IBM/sample-resource-service-brokers)中所含的程式庫。將記號解碼之後，格式顯示於下一節；請擷取 `iam_id` 及 `scope` 欄位，在下個步驟中會使用它們：

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

**步驟 2.2**：呼叫 IAM，確認使用者是否獲得授權存取儀表板

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

請參閱範例分配管理系統中的範例：https://github.com/IBM/sample-resource-service-brokers

## 協力廠商採用者的 IAM 記號範圍設定
{: #token_scoping}

使用用戶端 ID 所建立的使用者存取記號只能用來存取您的服務 API。使用此記號的其他雲端 API 要求會導致拒絕存取，即使使用者已配置適當的原則也是一樣。

在協力廠商整合期間，將會使用記號範圍，確保記號具有完成使用者目標所需的最小存取範圍。為了方便此作業，IAM 記號存取會以建立記號的用戶端 ID 為基礎。如果 IAM 記號是由協力廠商服務所建立，則一般使用者將無法執行某些 API 和功能，即使使用者已配置適當的原則也一樣。

對授權的影響（所有 `https://iam.bluemix.net/v2/authz` 呼叫）就是，需要在主旨中傳遞 `scope` 資訊。此資訊包含在 `scope` 宣告的 IAM 記號（base64 編碼）內。

下節是已在授權呼叫中新增之內容的範例：
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

這適用於所有用法 (`user, serviceId, crn`)，而且所有 `subject.attributes` 都需要一個範圍。

## 後續步驟
{: #next-steps}

該將所有項目組合在一起了！回到資源管理主控台，以受限可見性發佈您的服務，並在型錄中驗證您的供應項目。請參閱：[發佈及測試服務](/docs/third-party/cis4-rmc-publish.html)。
