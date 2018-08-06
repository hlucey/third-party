---


copyright:
  years: 2018
lastupdated: "2018-07-20"


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

이 주제는 {{site.data.keyword.Bluemix}}에서 써드파티 통합 청구 서비스를 개발하고 공개하는 데 필요한 단계를 안내합니다.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 카탈로그에서 오퍼링을 제공하도록 승인된 후에는 안내 제공 UI 환경인 리소스 관리 콘솔에서 오퍼링 개발을 시작합니다. 사용자는 카탈로그 메타데이터를 디자인하고, 서비스 가격 책정 플랜을 설정하고, {{site.data.keyword.Bluemix_notm}} Identity and Access Management(IAM)와 통합합니다.  

그 다음에는 리소스 관리 콘솔 외부에서 코드 개발을 수행하여 새로운 Open Service Broker(스타터 브로커 샘플 및 API 문서가 제공됨)를 빌드하고 호스팅하며, IAM을 사용하여 인증 플로우를 개발합니다. 이러한 단계를 완료한 후에는 리소스 관리 콘솔로 돌아가 제한된 가시성 모드로 서비스를 카탈로그에 배치합니다. 이를 통해 여러 결과물 요구사항을 테스트하고 유효성 검증할 수 있습니다. 준비가 완료되고 오퍼링이 모든 요구사항을 만족하면 서비스가 {{site.data.keyword.Bluemix_notm}} 카탈로그에 완전히 표시됩니다. 


## 프로세스 작동 방식
{: #process}

사용자는 통합 청구 서비스를 제공하기 위해 Provider Workbench, 리소스 관리 콘솔 및 선택한 개발 환경을 사용합니다. 이러한 단계를 추적하려면 [체크리스트](/docs/third-party/checklist.html#checklist)를 참조하십시오.

1. [문서 및 마케팅 공지사항 작성](/docs/third-party/cis1-docs-marketing.html). 
2. [리소스 관리 콘솔 {{site.data.keyword.Bluemix_notm}}에서 오퍼링 정의](/docs/third-party/cis2-rmc-define.html).
3. [서비스 브로커 개발 및 호스트](/docs/third-party/cis3-broker.html).
4. [인증 플로우 개발](/docs/third-party/cis5-iam.html).
5. [서비스 테스트](/docs/third-party/cis4-rmc-publish.html). 
6. [공개적으로 서비스 릴리스](/docs/third-party/cis6-ga.html). 

이러한 단계에서는 사용자가 통합 청구 서비스를 제공하도록 승인되었다고 가정합니다. Provider Workbench에서 초기 등록 및 승인 프로세스를 완료하지 않은 경우에는 [시작하기 튜토리얼](/docs/third-party/index.md)을 참조하십시오.
{: tip}

## 지원
{: #support}

통합 청구 서비스에서는 써드파티 오퍼링 제공자가 고유 지원 모델을 제공해야 합니다. IBM 담당자는 지원 모델을 사용할 수 있도록 도울 수 있으며, 사용자가 {{site.data.keyword.Bluemix_notm}} 지원에 티켓을 여는 경우 해당 티켓이 써드파티 지원 사이트로 라우팅되도록 합니다. 

## 지속적 업데이트
{: #maintain}

서비스가 릴리스되면 {{site.data.keyword.Bluemix_notm}} 담당자와 직접 작업하여 지속적으로 업데이트를 작성하고 이를 반복할 수 있습니다.



