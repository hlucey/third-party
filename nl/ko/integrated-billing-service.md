---


copyright:
  years: 2018
lastupdated: "2018-06-28"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 개요: 통합 청구 서비스 개발
{: #overview}

이 주제는 {{site.data.keyword.Bluemix_notm}}에서 써드파티 통합 청구 서비스를 개발하고 공개하는 데 필요한 단계를 안내하도록 구성되었습니다. {{site.data.keyword.Bluemix_notm}} 카탈로그에 오퍼링을 제공하도록 승인된 후에는 가이드 UI 환경인 리소스 관리 콘솔(리소스 관리 콘솔)에서 오퍼링 개발을 시작합니다. 리소스 관리 콘솔 내에서 카탈로그 메타데이터를 설계하고, 서비스 가격 책정 플랜을 설정하며, IBM Cloud Access Management(IAM)와 통합합니다. 다음으로 리소스 관리 콘솔의 외부에서 코드 개발을 수행하여 새로운 Open Service Broker(스타터 브로커 샘플 및 API 문서가 제공됨)를 빌드하고 호스팅하며, IAM을 사용하여 인증 플로우를 개발합니다. 이러한 단계가 완료된 후에는 리소스 관리 콘솔로 돌아가 제한된 가시성 모드로 서비스를 카탈로그에 배치합니다. 이를 통해 여러 개의 제공 가능한 요구사항을 테스트하고 유효성 검증할 수 있습니다. 준비가 되고 오퍼링이 모든 요구사항을 충족하면 서비스가 {{site.data.keyword.Bluemix_notm}} 카탈로그에 완전히 표시됩니다!


## 통합 청구 서비스를 제공하기 위해 수행해야 하는 작업

PWB, 리소스 관리 콘솔 및 이러한 목표를 제공하기 위해 선택한 개발 환경을 사용하여 작업하게 됩니다. 이러한 단계를 추적하려면 [체크리스트](/docs/third-party/checklist.html#checklist)를 참조하십시오.

다음 단계는 상위 레벨의 온보딩 프로세스를 요약합니다.

다음 단계에서는 사용자가 통합 청구 서비스를 제공하도록 승인되었다고 가정합니다. PWB의 초기 등록 및 승인을 완료하지 않은 경우 [{{site.data.keyword.Bluemix_notm}}의 써드파티 오퍼링 공개 시작하기](/docs/third-party/index.md)를 참조하십시오.
{: tip}

1. [작성자: 서비스 문서 및 마케팅 공지사항 작성(PWB)](/docs/third-party/cis1-docs-marketing.html)
2. [정의: 리소스 관리 콘솔 {{site.data.keyword.Bluemix_notm}}에서 오퍼링 정의](/docs/third-party/cis2-rmc-define.html)
3. [개발: Open Service Broker API 스펙을 사용하여 하나 이상의 서비스 브로커 개발 및 호스팅](/docs/third-party/cis3-broker.html)
4. [IAM: 인증 플로우(OAuth) 개발, 사용자 권한 유효성 검증(v2/authz) 및 경로 재지정 URI 제공](/docs/third-party/cis5-iam.html)
5. [공개 및 테스트: OSB를 리소스 관리 콘솔에 연결, 제한된 가시성 모드로 서비스를 {{site.data.keyword.Bluemix_notm}} 카탈로그에 공개, 오퍼링 테스트](/docs/third-party/cis4-rmc-publish.html).
6. [GA에 서비스 승인 요청](/docs/third-party/cis6-ga.html)

## 지원

통합 청구 서비스에서는 써드파티 서비스 제공자가 고유 지원 모델을 제공해야 합니다. IBM 담당자는 지원 모델을 사용할 수 있도록 도울 것이며, 사용자가 {{site.data.keyword.Bluemix_notm}} 지원에 티켓을 여는 경우 {{site.data.keyword.Bluemix_notm}} 지원은 이 티켓을 써드파티 지원 사이트로 라우팅합니다.

## 지속적 업데이트

서비스가 릴리스되면 {{site.data.keyword.Bluemix_notm}} 담당자와 직접 작업하여 지속적으로 업데이트를 작성하고 이를 반복할 수 있습니다.



