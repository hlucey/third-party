---


copyright:
  years: 2018
lastupdated: "2018-06-29"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 통합 청구 서비스에서 {{site.data.keyword.Bluemix_notm}} 플랫폼을 사용하는 방법

통합 청구 서비스는 추천 서비스와 다릅니다. 통합 청구 서비스는 인증, 액세스, 프로비저닝, 측정 및 청구에 {{site.data.keyword.Bluemix_notm}} 플랫폼을 사용합니다. 이 주제에서는 통합 청구 서비스가 사용하는 플랫폼 컴포넌트의 상위 레벨 개요를 제공합니다.

## {{site.data.keyword.Bluemix_notm}} 프로비져닝 계층

프로비저닝 계층은 {{site.data.keyword.Bluemix_notm}} 리소스의 라이프사이클을 관리합니다. 프로비저닝 계층은 고객 계정에 있는 리스소의 라이프사이클을 제어하고 추적합니다. *리소스*는 애플리케이션 또는 서비스 인스턴스에 대해 프로비저닝되거나 예약될 수 있는 물리적 또는 논리적 컴포넌트입니다. 리소스의 예로는 데이터베이스, 계정, 프로세서, 메모리 및 스토리지 한계가 있습니다. 일반적으로 프로비저닝 계층에서 추적하는 리소스에는 연관된 사용량 메트릭과 청구가 포함되지만 항상 그렇지는 않습니다. 어떤 경우에는 리소스가 프로비저닝 계층과 연관되어 리소스 라이프사이클이 계정 라이프사이클과 함께 관리될 수 있습니다.

### 리소스 라이프사이클 관리

프로비저닝 계층은 프로비저닝(인스턴스 작성)에서부터 바인딩(액세스 신임 정보 작성), 바인딩 해제(액세스 제거), 디프로비저닝(인스턴스 삭제)까지 리소스의 라이프사이클을 제어하는 일반 API를 제공합니다. 또한 {{site.data.keyword.Bluemix_notm}} 플랫폼에서는 사용자 기능을 작성할 필요가 없는 리소스의 라이프사이클을 관리할 수 있는 UI와 CLI를 제공합니다.

프로비저닝 계층은 리소스 라이프사이클의 다음 요소를 관리하는 데 도움이 되는 API를 제공합니다.
* 프로비저닝
* 리소스 인스턴스 업데이트
* 바인딩
* 리소스 키
* 바인딩 해제
* 디프로비저닝

## {{site.data.keyword.Bluemix_notm}} IAM(Identity and Access Management)

IAM(Identity Access Management)을 사용하면 안전하게 사용자를 인증하고 {{site.data.keyword.Bluemix_notm}}에서 일관되게 모든 클라우드 리소스에 대한 액세스를 제어할 수 있습니다. {{site.data.keyword.Bluemix_notm}} 프로비저닝 계층은 프로비저닝 계층에 대해 수행된 조치의 인증 및 권한 부여를 위해 IAM을 채택했습니다. 써드파티 오퍼링 제공자는 IAM을 사용하여 인증 플로우(OAuth)를 작성합니다. 추가 세부사항은 [IAM 개념](/docs/iam/index.html#iamoverview)을 참조하십시오.

오퍼링이 OIDC(OpenID Connect) 라이브러리를 사용하는 경우 IAM은 OIDC 통합을 지원합니다. OIDC는 인증 프레임워크인 OAuth 2.0 위에 있는 인증 계층으로 온보딩 프로세스를 간소화할 수 있습니다. OIDC에 대한 자세한 정보는 [OIDC(Open ID Connect)](http://openid.net/connect/){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")를 참조하십시오.

## {{site.data.keyword.Bluemix_notm}} 카탈로그

{{site.data.keyword.Bluemix_notm}} 카탈로그는 {{site.data.keyword.Bluemix_notm}} 콘솔에 표시되는 리소스의 오퍼링 정의(설명, 기능, 이미지, URL 등)를 저장합니다. 리소스 관리 콘솔을 사용하여 서비스 필수 메타데이터의 모든 측면을 정의합니다. 이 메타데이터는 카탈로그에 공개되고 카탈로그에 표시하는 데 사용됩니다. 리소스 관리 콘솔의 **오퍼링** 및 **플랜** 페이지에서 필수 및 선택적 메타데이터 필드에 대한 자세한 정보를 볼 수 있지만 주요 항목은 여기에 포함되어 사용자의 이해를 돕습니다.

   * 서비스 이름: 서비스의 기술 이름입니다. 서비스 이름은 중요하며 올바르게 정의되어야 합니다. {{site.data.keyword.Bluemix_notm}} 플랫폼에서 서비스를 식별하는 데 사용되는 서비스 이름과 고객이 {{site.data.keyword.Bluemix_notm}} 카탈로그에서 볼 수 있는 표시 이름을 모두 제공해야 합니다. 서비스 이름이 표시 이름은 아닙니다.
   * 서비스 표시 이름: 서비스의 사용자 친화적인 이름입니다. 예: "Compose Redis"
   * 서비스 ID: OSB 브로커에 대한 API 호출에 사용되는 서비스의 GUID입니다. 이 이름은 고유한 값이어야 합니다.
   * 서비스 아이콘: 서비스 로고가 있는 SVG
   * 서비스 설명: {{site.data.keyword.Bluemix_notm}} 카탈로그 사용자 인터페이스에서 리소스 아이콘 위에 마우스를 올려 놓으면 표시되는 리소스에 대한 설명입니다. 설명을 위한 단일 문장 또는 구문을 추가할 수 있습니다.
   * 서비스 상세 설명: 카탈로그 목록 페이지에 표시되는 첫 번째 단락입니다. 자세한 설명이 되려면 최소 2개 문장을 사용하는 것이 좋습니다.
   * 문서 URL: {{site.data.keyword.Bluemix_notm}} 문서에 대한 링크입니다. 사용자가 PWB에서 작성하면 PWB에서 사용자를 위해 url 값을 생성합니다.
   * 이용 약관 URL: 사용을 위한 서비스의 이용 약관에 대한 링크입니다. GDPR 용도의 경우 기존 써드파티 서비스의 이용 약관에는 링크되지 않습니다. 대신 통합 청구 서비스의 고유 페이지를 제공해야 합니다.
   * 지시사항 URL: 문서 URL과 마찬가지로 {{site.data.keyword.Bluemix_notm}} 문서를 가리키지만 지시사항 URL은 문서를 동적으로 서비스의 대시보드에 있는 시작하기 탭으로 가져옵니다.
   * 카테고리: 서비스를 카탈로그에 배치해야 하는 사용 가능한 {{site.data.keyword.Bluemix_notm}} 카테고리를 선택합니다.
   * 글머리 기호: 서비스에 대한 간단한 설명 스파클러
   * 매체: 서비스에 대한 화면 캡처 및 동영상
   * 서비스 플랜 이름: 각 플랜에는 기술 이름이 있습니다. 모든 소문자, 공백 없음, "-"를 포함할 수 있습니다.  예: `gold`.
   * 서비스 플랜 표시 이름: 플랜의 사용자 친화적인 이름입니다. 예: `Gold`
   * 서비스 플랜 ID: OSB 브로커에 대한 API 호출에 사용되는 서비스 플랜의 GUID입니다. 이 이름은 고유한 값이어야 합니다. 리소스 관리 콘솔에서 이 값을 생성합니다.
   * 서비스 플랜 설명: 리소스 플랜에 대한 설명입니다. IBM Cloud 카탈로그의 리소스 세부사항 페이지에서 플랜을 선택하면 설명이 표시됩니다.
   * 서비스 플랜 글머리 기호: 서비스 플랜에 대한 간단한 설명 스파클러


## Open Service Broker

서비스 브로커는 서비스 라이프사이클을 관리합니다. {{site.data.keyword.Bluemix_notm}} 플랫폼은 서비스 브로커와 상호작용하여 서비스 인스턴스(서비스 오퍼링의 인스턴스화) 및 서비스 바인딩(애플리케이션과 서비스 인스턴스 간의 연관 표시, 보통 애플리케이션이 서비스 인스턴스와 통신하는 데 사용할 신임 정보가 포함됨)을 프로비저닝하고 관리합니다. 올바른 메타데이터 값을 제공하면 요청이 수행될 때 성공적인 REST API 응답이 작성됩니다.

{{site.data.keyword.Bluemix_notm}}는 Open Service Broker API(OSB) `버전 2.12` 스펙을 사용합니다. [Open Broker API 스펙](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")을 읽고 숙지한 후 readme 파일을 가이드로 사용하여 자세히 알아보십시오.

리소스 제어기가 리소스 프로비저닝 요청을 받으면 OSB를 호출하여 서비스 유형, 오퍼링, 플랜 및 지역 가용성을 유효성 검증합니다. 또한 리소스 제어기는 고객 계정과 연관된 플랜의 가시성도 유효성 검증합니다. {{site.data.keyword.Bluemix_notm}}는 OSB 스펙을 확장하는 브로커 샘플과 API 문서를 제공합니다. 자세한 통합 청구 온보딩 개발 단계를 수행하면서 브로커를 개발하고 호스팅하는 방법에 대한 자세한 정보를 볼 수 있습니다.

## {{site.data.keyword.Bluemix_notm}} 측정 서비스

서비스에서 측정량 기반 플랜을 제공하는 경우 {{site.data.keyword.Bluemix_notm}} 사용자는 사용하는 리소스의 양에 따라 요금이 부과됩니다. 예를 들어, 데이터베이스 서비스를 사용하는 {{site.data.keyword.Bluemix_notm}} 사용자는 사용자 애플리케이션이 사용하는 스토리지의 양에 따라 요금이 부과될 수 있습니다. 사용량을 요금 부과 가능 레코드로 변환하려면 사용량을 제출해야 합니다.

측정량 기반 플랜을 제공하는 모든 통합 청구 서비스는 {{site.data.keyword.Bluemix_notm}} 측정 서비스를 사용하여 사용량 데이터를 보고해야 합니다.

**참고:** 측정량 기반 플랜을 제공하는 경우 측정 서비스 API를 사용하여 시간별 사용량 제출을 자동화해야 합니다.

측정에 대한 자세한 정보는 [측정 통합](/docs/third-party/metering.html#meteringintera)을 참조하십시오. 측정된 사용량 제출에 대한 자세한 정보는 [측정량 기반 플랜을 위한 사용량 제출](/docs/third-party/submitusage.html#submitusage)을 참조하십시오.

## 프로비저닝 시나리오: 모두 함께 가져오기

이제 이전에 설명한 개념을 모두 함께 가져와서 {{site.data.keyword.Bluemix_notm}} 플랫폼을 사용하여 서비스 인스턴스를 작성하는 방법에 대한 예제를 살펴봅니다.

![프로비저닝 시나리오](images/flow-am.svg "플랫폼에서 서비스 인스턴스 작성을 처리하는 방법")

서비스 인스턴스를 작성하려는 경우 다음 두 방법 중 하나로 시작할 수 있습니다.
* **CLI**: `ibmcloud cli [ ibmcloud resource service-instance-create NAME SERVICE_NAME SERVICE_PLAN_NAME LOCATION ]` 사용
* **{{site.data.keyword.Bluemix_notm}} 콘솔**: 사용자가 서비스, 플랜을 선택하고 **작성** 오퍼레이션을 사용할 수 있습니다.

{{site.data.keyword.Bluemix_notm}} 플랫폼은 사용자가 {{site.data.keyword.Bluemix_notm}}를 사용하여 서비스 인스턴스를 작성할 수 있는 권한을 가지고 있는지 검증합니다. 이 유효성 검증이 실행되면 서비스 브로커의 프로비저닝 엔드포인트(PUT /v2/resource_instances/:resource_instance_id)가 호출됩니다. 프로비저닝이 실행될 때 다음 규칙이 충족되어야 합니다.
* {{site.data.keyword.Bluemix_notm}} 컨텍스트가 컨텍스트 변수에 포함되어야 합니다.
* `X-Broker-API-Originating-Identity`에 요청을 시작한 사용자의 IBM IAM ID가 포함됩니다.
* 매개변수 섹션에 요청된 위치(및 서비스에 필요한 추가 매개변수)가 포함됩니다.

예제 프로비저닝 요청:

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

### {{site.data.keyword.Bluemix_notm}} `context` 매개변수에 대한 이해

이전 예제에서는 `context` 매개변수에 리턴되는 메타데이터를 볼 수 있습니다. {{site.data.keyword.Bluemix_notm}}에 대한 프로비저닝 컨텍스트는 다음을 리턴합니다.

* **플랫폼**: 플랫폼을 "ibmcloud"로 식별합니다.

* **"account_id"**: 서비스 인스턴스를 프로비저닝하는 {{site.data.keyword.Bluemix_notm}}에 계정 ID를 리턴합니다.

* **crn**: 고객이 {{site.data.keyword.Bluemix_notm}}에서 서비스를 프로비저닝할 때 서비스 인스턴스가 작성되고 이 인스턴스는 CRN({{site.data.keyword.Bluemix_notm}} Resource Name)으로 식별됩니다. CRN은 프로비저닝, 바인딩(신임 정보 및 엔드포인트 작성), 측정, 대시보드 표시 및 액세스 제어 등 {{site.data.keyword.Bluemix_notm}}와 상호작용하는 모든 측면에서 사용됩니다. 오퍼링 제공자의 관점에서 CRN은 대체로 {{site.data.keyword.Bluemix_notm}} API와 함께 사용되는 불투명한 문자열로 취급될 수 있습니다. 또한 다음 구조를 사용하여 분해할 수도 있습니다.

   ```
   crn:version:cname:ctype:service-name:location:scope:service-instance:resource-type:resource
   ```

   프로비저닝 샘플에서 `compose-redis` 서비스 CRN은 다음과 같습니다.

   ```
   crn:v1:bluemix:public:compose-redis:us-south:a/46aa677e-e83f-4d17-a2b6-5b752564477c:416d769b-682d-4833-8bd7-5ef8778e5b52::
   ```

   이 샘플에서 이 `compose-redis` 인스턴스는 IDrk `46aa677e-e83f-4d17-a2b6-5b752564477c`인 {{site.data.keyword.Bluemix_notm}} 계정의 일부이고 인스턴스의 고유 ID는 `416d769b-682d-4833-8bd7-5ef8778e5b52`이며 인스턴스는 공용 {{site.data.keyword.Bluemix_notm}}의 `us-south` 지역에 호스팅됩니다.

* **resource_group_crn**: 서비스 인스턴스가 포함된 리소스 그룹을 리턴합니다. 추가 세부사항은 [리스소 그룹 관리](/docs/resources/resourcegroups.html)를 참조하십시오.

   **참고**: 오퍼링 제공자는 매우 특별한 환경을 제외하고는 `resource_group_crn`을 다루지 않아야 합니다. 해당 필드를 사용하기 전에 IBM 담당자에게 사용자 유스 케이스에 대해 문의하십시오.

