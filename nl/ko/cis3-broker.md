---

copyright:

  years: 2018, 2019

lastupdated: "2019-02-25"

keywords: service brokers, IBM Cloud platform, new service brokers, hosting service broker 

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# 3단계. 서비스 브로커 개발 및 호스팅
{: #step3-osb}

리소스 관리 콘솔에서 내보낸 메타데이터를 사용하여 선택한 프로그래밍 언어로 하나 이상의 새 서비스 브로커를 빌드할 수 있습니다.
{:shortdesc}

서비스 브로커는 서비스 라이프사이클을 관리합니다. {{site.data.keyword.Bluemix_notm}} 플랫폼은 서비스 브로커와 상호작용하여 서비스 인스턴스 및 서비스 바인딩을 프로비저닝하고 관리합니다. 요청이 수행될 때 성공적인 RESTful API 응답을 작성하도록 올바른 메타데이터 값을 제공할 수 있습니다.

리소스 관리 콘솔, {{site.data.keyword.Bluemix_notm}} 서비스 브로커 샘플 및 리소스 브로커 API 문서에서 내보낸 메타데이터의 조합을 사용하여 브로커를 빌드할 수 있습니다.

## 시작하기 전에
{: #broker-pre-reqs}

1단계를 시작하고 2단계를 완료했는지 확인하십시오.
1. [서비스 문서 및 마케팅 공지사항 작성](/docs/third-party?topic=third-party-content-tasks#content-tasks).
2. [리소스 관리 콘솔의 오퍼링 정의](/docs/third-party?topic=third-party-step2-define#step2-define).


## {{site.data.keyword.Bluemix_notm}} 플랫폼 프로비저닝 시나리오 보기
{: #scenario}

{{site.data.keyword.Bluemix_notm}} 플랫폼에서 작동하는 Open Service Broker를 개발합니다. 리소스 작성이 작동하는 방식을 이해하려면 [프로비저닝 시나리오](/docs/third-party?topic=third-party-how-it-works#provision2)를 참조하십시오.

## OSB 스펙 알아보기
{: #learn-osb}

{{site.data.keyword.Bluemix_notm}}는 Open Service Broker API(OSB) `버전 2.12` 스펙을 사용합니다. [Open Broker API 스펙](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")을 읽고 숙지한 후 readme 파일을 가이드로 사용하여 자세히 알아보십시오.

## {{site.data.keyword.Bluemix_notm}} 브로커 샘플 보기
{: #samples}

[https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")

샘플에서 모든 언어가 표시되지는 않습니다. 예를 들어, 샘플 Python 브로커가 필요한 경우 Google을 검색하여 Cloud Foundry 샘플을 찾을 수 있어야 합니다. OSB 요구사항을 충족하려면 이 샘플을 조정해야 합니다.
{: note}

## {{site.data.keyword.Bluemix_notm}} Open Service Broker API 문서 보기
{: #docs}

서비스 브로커는 [{{site.data.keyword.Bluemix_notm}} Open Service Broker API](https://{DomainName}/apidocs/ibm-cloud-osb-api){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")에 대한 이해를 바탕으로 개발되어야 합니다. 브로커 API 및 브로커 API가 브로커와 상호작용하는 방식을 숙지하십시오.

{{site.data.keyword.Bluemix_notm}} Open Service Broker는 Open Service Broker 2.12 스펙을 확장합니다.
{: tip}

### 모든 서비스 브로커에 대한 필수 엔드포인트 로직
{: #endpoint-sb}

서비스 브로커는 REST API가 이용하는 메타데이터 값의 표준 세트를 제공해야 하며 {{site.data.keyword.Bluemix_notm}} 브로커에는 다음 REST API 엔드포인트 또는 경로에 대한 로직이 있어야 합니다.

<dl>
  <dt>카탈로그(GET)</dt>
  <dd>브로커에 포함된 카탈로그 메타데이터를 리턴합니다. 많은 추가 카탈로그 메타데이터 값이 리턴되지 않습니다. 이러한 값은 리소스 관리 콘솔 내에서만 추가되고 {{site.data.keyword.Bluemix_notm}} 카탈로그 내에 저장됩니다.</dd>
  <dt>리소스 인스턴스(PUT)</dt>
  <dd>서비스 인스턴스를 프로비저닝합니다.</dd>
  <dt>리소스 인스턴스(DELETE)</dt>
  <dd>서비스 인스턴스를 디프로비저닝합니다.</dd>
  <dt>리소스 인스턴스(PATCH)</dt>
  <dd>서비스 인스턴스를 업데이트합니다.</dd>
</dl>

**카탈로그(GET)에 대한 참고**: 이 엔드포인트는 브로커가 지원하는 서비스 및 플랜에 대한 브로커와 {{site.data.keyword.Bluemix_notm}} 플랫폼 간의 계약을 정의합니다. 이 엔드포인트는 브로커 내에 저장된 카탈로그 메타데이터를 리턴합니다. 이러한 값은 서비스와 {{site.data.keyword.Bluemix_notm}} 플랫폼 간의 최소 프로비저닝 계약을 정의합니다. 프로비저닝하는 데 필요하지 않은 모든 추가 카탈로그 메타데이터는 {{site.data.keyword.Bluemix_notm}} 카탈로그에 저장됩니다. 링크, 아이콘 및 i18n 변환 메타데이터와 같은 대시보드를 렌더링하는 데 사용되는 카탈로그 표시 값에 대한 업데이트는 소스 관리 콘솔에서 업데이트해야 하며 브로커에 포함되지 않습니다. 브로커에 저장된 메타데이터는 {{site.data.keyword.Bluemix_notm}} 콘솔이나 {{site.data.keyword.Bluemix_notm}} CLI에 표시되지 않습니다. 콘솔과 CLI에서는 리소스 관리 콘솔에서 설정하고 {{site.data.keyword.Bluemix_notm}} 카탈로그에 저장된 항목을 리턴합니다. 다음 섹션에서는 카탈로그(GET)가 리턴하는 최소 필수 값을 보여줍니다.

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

### 바인드 가능 서비스에 대한 필수 엔드포인트 로직
{: #bindable}

서비스를 {{site.data.keyword.Bluemix_notm}}의 애플리케이션에 바인드할 수 있으면 API 엔드포인트와 인증 정보를 서비스 이용자에게 리턴할 수 있어야 합니다. 바인드 가능 서비스는 Open Service Broker 스펙의 바인드 가능 조작을 사용해야 하며 다음의 엔드포인트 또는 경로를 구현해야 합니다.

<dl>
  <dt>바인딩 및 인증 정보(PUT)</dt>
  <dd>서비스 인스턴스를 애플리케이션에 바인드합니다.</dd>
  <dt>바인딩 및 인증 정보(DEL)</dt>
  <dd>서비스 인스턴스를 애플리케이션에서 바인드 해제합니다.</dd>
</dl>

### 필수 {{site.data.keyword.Bluemix_notm}} 확장 엔드포인트
{: #extension} 

OSB 스펙은 사용 안함 상태이지만 아직 삭제되지 않은 인스턴스 상태를 지원하지 않습니다. {{site.data.keyword.Bluemix_notm}}가 청구 누락 또는 계정 일시 중단(단 아직 취소는 아님)을 유발하는 기타 상황을 경험할 수 있는 고객을 지원할 수 있도록, {{site.data.keyword.Bluemix_notm}}는 서비스 인스턴스가 사용 안함 및 다시 사용으로 설정되도록 허용하는 확장 API 엔드포인트를 정의했습니다. 다음 엔드포인트 확장은 **필수**입니다.

<dl>
  <dt>인스턴스 사용 및 사용 안함(GET)</dt>
  <dd>상태 - 서비스 인스턴스의 상태를 리턴합니다.</dd>
  <dt>인스턴스 사용 및 사용 안함(PUT)</dt>
  <dd>서비스 인스턴스를 사용 또는 사용 안함으로 설정할 수 있습니다.</dd>
</dl>

사용 안함 엔드포인트가 시작될 때 서비스 인스턴스에 대한 액세스를 사용 안함으로 설정하고 사용 엔드포인트가 시작될 때 해당 액세스를 다시 사용으로 설정하는 것은 서비스 제공자의 책임입니다.
{: note}

## 내보낸 메타데이터를 사용하여 브로커 개발을 안내하는 방법 알아보기
{: #use-metadata}

리소스 관리 콘솔에서 내보낸 메타데이터를 사용자 고유의 브로커 개발을 위한 안내서로 사용할 수 있습니다. 리소스 관리 콘솔에 입력한 모든 값이 서비스를 프로비저닝하는 데 필요하지는 않습니다. 리소스 관리 콘솔에서 내보낸 메타데이터는 서비스와 {{site.data.keyword.Bluemix_notm}} 플랫폼 간의 최소 프로비저닝 계약을 정의합니다. 내보낸 JSON에서는 다음 값을 제공합니다.

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


OSB 서비스 어레이는 리소스 관리 콘솔에 추가한 오퍼링 메타데이터와 같아야 합니다. OSB와 리소스 관리 콘솔 간에 일대일 패리티를 보장하기 위해 리소스 관리 콘솔에서 브로커의 실제 서비스 어레이로 다운로드한 `catalog.json`에 있는 서비스 어레이를 비교하는 것이 중요합니다. 모든 서비스와 플랜 ID 및 이름이 일치해야 합니다.
{: tip}

## {{site.data.keyword.Bluemix_notm}} 플랫폼에서 제공하는 브로커 정보
{: #broker info}

서비스 브로커 또는 브로커는 {{site.data.keyword.Bluemix_notm}} 플랫폼에서 다음 정보를 수신합니다.

### X-Broker-API-Originating-Identity
{: #x-broker}

**사용자 ID 헤더**는 API 원본 ID 헤더를 통해 제공됩니다. 이 요청 헤더는 사용자의 {{site.data.keyword.Bluemix_notm}} IAM ID를 포함합니다. IAM ID는 base64로 인코딩됩니다. {{site.data.keyword.Bluemix_notm}}는 단일 인증 영역 `IBMid`를 지원합니다. `IBMid` 영역은 IBM ID 고유 ID(IUI)를 사용하여 {{site.data.keyword.Bluemix_notm}}에서 사용자 ID를 식별합니다. 이 IUI는 서비스 제공자에게 불투명한 문자열로 표시됩니다.

예제:

```
X-Broker-API-Originating-Identity: ibmcloud eyJpYW1faWQiOiJJQk1pZC01MEdOUjcxN1lFIn0=
Decoded:
{"iam_id":"IBMid-50GNR717YE"}
```

### API 버전 헤더
{: #api-header}

**API 버전 헤더**는 [2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")가 됩니다. 예: `X-Broker-Api-Version: 2.12`.

### 리소스 인스턴스(PUT) body.context 및 리소스 인스턴스(PATCH) body.context
{: #put}

`PUT /v2/service_instances/:resource_instance_id` 및 `PATCH /v2/service_instances/:resource_instance_id`는 **body.context**에서 다음 값을 받습니다. `{ "platform": "ibmcloud", "account_id": "tracys-account-id", "crn": "resource-instance-crn" }`

## 추가 브로커 권장사항
{: #more-info}

### 동기 대신 비동기 오퍼레이션 사용에 대한 권장사항
{: #asynch-ops}

OSB API는 동기 및 비동기 모드의 오퍼레이션을 모두 지원합니다. 오퍼레이션에 걸리는 시간이 10초 미만인 경우 동기 응답이 권장됩니다. 그렇지 않으면 비동기 모드의 오퍼레이션을 사용해야 합니다. 자세한 정보는 OSB 스펙에 포함되어 있습니다.

인스턴스를 프로비저닝하는 중에 비동기 오퍼레이션에 10초 미만이 걸리는 경우 플랫폼이 제한시간 초과됩니다.
{: tip}

### 위치에서 브로커를 관리하기 위한 권장사항
{: #managing-broker}

사용자는 대기 시간, 가용성 및 데이터 주거성(data residency)에 대한 클라우드 서비스의 위치를 이해하는 것이 중요합니다.

{{site.data.keyword.Bluemix_notm}}에서 인스턴스를 프로비저닝할 때 사용자가 제공하는 필수 매개변수 중 하나는 서비스 인스턴스를 프로비저닝하려는 위치입니다. 일부 서비스는 다중 위치의 프로비저닝을 지원할 수 있습니다. 예를 들어, 데이터베이스 서비스는 모든 {{site.data.keyword.Bluemix_notm}} 지역에서 프로비저닝되는 것을 지원하거나 서브세트의 영역을 지원할 수 있습니다.

서드파티 API 기반 서비스가 다른 클라우드에서 구현되고 {{site.data.keyword.Bluemix_notm}}에 노출되는 경우 위치는 다른 클라우드에 있는 서비스의 위치를 표시해야 합니다.

{{site.data.keyword.Bluemix_notm}}에 온보딩하는 경우 하나 이상의 OSB 브로커를 구현해야 합니다. 배치 전략 및 서비스에 대해 지원할 위치에 따라 둘 이상의 브로커가 있을 수 있습니다. 리소스 관리 콘솔 도구 내에서 서비스/플랜/위치 튜플과 해당 튜플에 대한 오퍼레이션을 서비스할 브로커 사이에 맵핑을 설정했습니다. 일반적인 선택사항은 서비스의 모든 위치를 서비스할 단일 브로커를 정의하거나 위치별 브로커를 정의하는 것입니다. 이 선택사항은 서비스 제공자가 선택합니다.

사용 가능한 위치 목록은 [IBM Global Catalog 위치](https://globalcatalog.cloud.ibm.com/search?q=kind:geography){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")를 참조하십시오. 서비스가 Global Catalog에서 추가 위치의 정의를 요구하는 경우에는 {{site.data.keyword.Bluemix_notm}} 온보딩 팀에 문의하십시오.


## 브로커 호스트
{: #host}

브로커는 REST API 호출에 응답할 수 있는 애플리케이션의 일부로 호스팅되어야 합니다. 또한 호스트 위치는 {{site.data.keyword.Bluemix_notm}} 보안 가이드라인을 준수해야 합니다. {{site.data.keyword.Bluemix_notm}}에서 호스팅되거나, {{site.data.keyword.Bluemix_notm}} 자체에서 공용으로 액세스할 수 있는 경우 외부에서 호스팅될 수 있습니다.

IBM 외부에서 브로커를 호스팅하려면 다음 보안 가이드라인을 충족해야 합니다.
- TLS(Transport Layer Security) 프로토콜 버전 1.2를 준수해야 함
- 공용 인터넷에서 액세스할 수 있는 올바른 HTTP 엔드포인트에서 호스팅되어야 함

다음 단계를 완료하려면 서비스 브로커의 호스트 위치가 필요합니다. 다음 단계로 이동할 때 앱과 연관된 URL과 인증 정보를 준비해 두십시오.
{: tip}

## 서비스 브로커를 테스트하는 방법
{: #broker-test}

사용하려는 다른 엔드포인트에 대해 curl 명령을 실행하여 브로커의 유효성을 검증해야 합니다. 샘플 readme 파일에서는 OSB 엔드포인트에 대해 curl을 수행하기 위한 우수한 지침을 제공합니다. [https://github.com/IBM/sample-resource-service-brokers/blob/master/README.md](https://github.com/IBM/sample-resource-service-brokers/blob/master/README.md){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")

### 서비스 브로커에 대해 curl을 수행하는 방법
{: #curl-broker}
다음 예제를 사용하여 브로커 curl 응답을 테스트하십시오.

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

## 다음 단계
{: #cis3-next-steps}

일부 중요한 스킬을 획득했습니다! OSB 스펙을 충족하는 서비스 브로커를 구현하고 호스팅했습니다. [4단계: 인증 플로우 개발](/docs/third-party?topic=third-party-step4-iam#step4-iam)을 참조하십시오.
