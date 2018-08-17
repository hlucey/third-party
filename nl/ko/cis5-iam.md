---


copyright:
  years: 2018
lastupdated: "2018-07-27"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 4단계: 인증 플로우 개발

오퍼링을 정의했을 때 리소스 관리 콘솔 - **액세스 관리** 페이지에서 {{site.data.keyword.Bluemix_notm}} IAM(Identity and Access Management) 클라이언트 ID 및 시크릿, 서비스 ID와 API 키를 제공했습니다. 이제 해당 값을 사용하여 다음 단계를 완료해야 합니다.

1. `dashboard_url`에 대한 처리 방법에 따라 경로 재지정 URI를 파생시키고 리소스 관리 콘솔로 돌아가 경로 재지정 URI를 IAM 탭에 추가합니다. 이렇게 하면 클라이언트 ID가 업데이트됩니다.
2. 인증을 위한 OAuth 플로우를 개발합니다. 경로 재지정 uri, 클라이언트 ID 및 클라이언트 시크릿을 매개변수로 `token_endpoint` IAM Rest API에 사용하여 이 플로우를 완료합니다.
3. 사용자 권한 유효성 검증:
   1. IAM과 통신하여 API 키에서 액세스 토큰을 받음
   2. `authorization_endpoint`(/v2/authz POST)를 사용하여 서비스 대시보드에 대한 사용자 권한 유효성 검증

이 단계에서는 사용자가 통합 청구 서비스를 제공하도록 승인되었다고 가정합니다. PWB의 초기 등록 및 승인을 아직 완료하지 않은 경우 [{{site.data.keyword.Bluemix_notm}}에서 써드파티 오퍼링 공개 시작하기](/docs/third-party/index.html)를 참조하십시오.
{: tip}

## 시작하기 전에

1단계를 시작했는지 확인하고 2와 3단계를 완료했는지 확인하십시오.
1. [서비스 문서 및 마케팅 공지사항 작성](/docs/third-party/cis1-docs-marketing.html).
2. [리소스 관리 콘솔의 오퍼링 정의](/docs/third-party/cis2-rmc-define.html).
3. [서비스 브로커 개발 및 호스트](/docs/third-party/cis3-broker.html).


## IAM 경로 재지정 URI 파생(리소스 관리 콘솔: IAM 페이지)

 리소스 관리 콘솔에서 서비스를 정의했으면 클라이언트 ID를 생성한 것입니다. 그러나 이 때 경로 재지정 URI는 없었을 가능성이 큽니다. 이는 IAM이 false로 설정된 클라이언트 ID를 생성했음을 의미합니다. 경로 재지정 URI를 사용하여 리소스 관리 콘솔로 돌아가기 전에는 true 클라이언트 ID를 가질 수 없습니다.

좋은 소식은 이전 개발 단계에서 OSB를 개발하여 호스팅했다는 것입니다(샘플 브로커 코드에서 IAM 값을 확인했을 것입니다). `redirect_uri`는 앱이 있는 호스트 url이며 여기에는 일반적으로 인증/권한 부여를 처리하는 일부 추가 url이 있습니다.

 다음은 경로 재지정 URI의 예입니다.

```
https://myapp.bluemix.net/integrate/auth/callback
http://localhost:3000/auth/callback <-- for testing locally
```

리소스 관리 콘솔로 돌아가 경로 재지정 URI를 IAM 탭에 추가하십시오.

1. 콘솔에 로그인하십시오.
2. 경로 재지정 URI를 복사하십시오.
3. 리소스 관리 콘솔로 돌아가십시오.
4. **IAM 탭**에서 경로 재지정 URI를 **경로 재지정 URI** 필드에 붙여넣으십시오.
5. **클라이언트 ID 업데이트**를 클릭하여 클라이언트 ID를 업데이트하십시오.

이제 경로 재지정 URI를 알고 있고 true로 설정된 클라이언트 ID를 가지고 있어야 합니다! 다음 단계에서 이 클라이언트 ID를 사용하여 OAuth 플로우를 개발할 수 있습니다.

##  인증을 위한 OAuth 플로우 개발
{: #oauth}


**인증 - 0단계:** `https://iam.bluemix.net/identity/.well-known/openid-configuration`을 호출하여 개발한 애플리케이션에 가까운 UI 로그인의 IAM 지역 엔드포인트를 찾으십시오.

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

이 요청은 애플리케이션이 시작될 때 한 번 수행되며, `authorization_endpoint`가 실패하면 다시 수행될 수 있습니다. 짧은 시간 동안 `authorization_endpoint` 값을 캐시할 수 있어야 하며 캐시가 만료되거나 오류가 발생한 후에는 새로 고치기를 수행해야 합니다.


**인증 - 1단계:** 사용자가 `dashboard_url`을 탐색할 때 브라우저를 다음으로 경로 재지정하십시오. `<authorization_endpoint>?client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&response-type=code&state=<your-resource-instance-id>`


-> 로그인 프롬프트가 표시됩니다.

-> 사용자가 신임 정보를 입력합니다.

-> 브라우저에서 "code" 응답 매개변수 및 "state" 값을 제공하는 uri를 경로 재지정하도록 콜백합니다.


**인증 - 2단계:** 액세스 토큰 호출을 위한 코드 교환

### POST <token_endpoint>

#### 헤더:
{: #headers1}

  - Authorization: Basic *[client id]:[client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### 매개변수 사용:
{: #parameters1}

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

### 응답:
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

  다음 사용자 권한 부여 중에 사용되므로 이 응답에서 리턴된 사용자의 access_token을 저장하십시오.

샘플 브로커의 예제를 확인하십시오(https://github.com/IBM/sample-resource-service-brokers).

## 사용자 권한의 유효성 검증 시작
{: #validate}

1. IAM과 통신하여 API 키의 액세스 토큰을 받음
2. 서비스 인스턴스에 대한 사용자 권한 유효성 검증(/v2/authz POST)

### 인증 - 1단계: API 키를 사용하여 {{site.data.keyword.Bluemix_notm}} IAM 토큰 가져오기
{: #iam_token_using_api_key}

### POST/ID/토큰

#### 헤더:
{: #headers2}

  - Authorization: Basic *[client id]:[client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### 매개변수 사용:
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
  "https://iam-region2.bluemix.net/identity/token"
```
{: codeblock}

### 응답:
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

**참고:** 이 토큰은 1시간 동안 유효하며 1시간 동안 필요한 만큼 여러 번 재사용할 수 있습니다. `dashboard_url`에 대한 모든 액세스에 이 요청을 수행하지 않도록 이 토큰을 캐싱할 것을 권장합니다.


### 인증 - 2단계: 서비스 인스턴스에 대한 사용자 권한 유효성 검증(/v2/authz POST)

이제 사용자를 인증하고 고유 액세스 토큰을 가지고 있습니다. 사용자가 서비스 대시보드에 액세스할 수 있는지 검증해야 합니다. 먼저 2.1단계에서 디코드할 사용자 액세스 토큰에 있는 몇 가지 정보가 필요합니다. 그런 다음, 이 정보로 IAM을 호출하여 사용자가 단계 2.2의 대시보드에 액세스 권한이 있는지 확인합니다.

**2.1단계**: 사용자 액세스 토큰(위에서 찾은 `**인증 - 2단계:** 액세스 토큰에 대한 코드 교환` 중에 리턴됨)을 디코드합니다.
   이는 JWT 준수 라이브러리를 사용하여 디코드할 수 있는 JWT 토큰입니다. 예를 들어, [샘플 브로커 코드](https://github.com/IBM/sample-resource-service-brokers)에 있는 라이브러리를 참조하십시오.
   토큰이 디코드되면 형식은 다음과 같습니다. 다음 단계에서 사용할 `iam_id` 및 `scope` 필드를 추출해야 합니다.

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

**2.2단계**: IAM을 호출하여 사용자가 대시보드에 액세스할 권한이 있는지 여부 확인

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

샘플 브로커의 예제를 확인하십시오(https://github.com/IBM/sample-resource-service-brokers).

## 써드파티 채택자를 위한 {{site.data.keyword.Bluemix_notm}} IAM(Identity and Access Management) 토큰 범위
{: #token_scoping}

사용자 클라이언트 ID로 생성된 사용자 액세스 토큰은 사용자의 서비스 API에 액세스하기 위해서만 사용될 수 있습니다. 이 토큰을 사용하는 다른 클라우드 API에 대해 요청하면 사용자가 적절한 정책을 구성한 경우에도 액세스가 거부됩니다.

써드파티 통합의 일부로서 토큰 범위는 토큰이 사용자의 목표를 달성하는 데 필요한 최소 액세스 범위를 가지고 있는지 확인하는 데 사용됩니다. 이를 용이하게 하기 위해 IAM 토큰은 토큰을 생성한 클라이언트 ID에 따라 액세스 권한을 가집니다. 이는 IAM 토큰이 써드파티 서비스에 의해 작성된 경우 사용자가 적절한 정책을 구성했더라도 일반 사용자가 특정 API 및 기능을 실행할 수 없음을 의미합니다.

권한(`https://iam.bluemix.net/v2/authz`에 대한 모든 호출)에 대한 영향은 이 주제의 `scope` 정보를 전달해야 하는지로 알 수 있습니다. 이 정보는 `scope` 항에 있는 IAM 토큰(base64 인코딩)에 포함되어 있습니다.

권한 부여 호출에 추가된 항목의 예는 다음과 같습니다.
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

이는 모든 사용량(`사용자, serviceId, crn`)에 적용되며 모든 `subject.attributes`에 범위가 필요합니다.

## 다음 단계

이제 모든 것을 함께 사용해야 할 단계입니다! 리소스 관리 콘솔로 돌아가 제한된 가시성 모드로 서비스를 공개하고 카탈로그에서 오퍼링을 유효성 검증하십시오. [서비스 공개 및 테스트](/docs/third-party/cis4-rmc-publish.html)를 참조하십시오.
