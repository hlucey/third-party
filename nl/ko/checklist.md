---

copyright:
  years: 2018
lastupdated: "2018-09-05"

---

{:right: .ph data-hd-position='right'}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# 엔드-투-엔드 체크리스트
{: #checklist}

다음 체크리스트를 사용하여 통합 청구 서비스를 정의, 개발 및 공개하는 데 필요한 모든 태스크를 추적할 수 있습니다.
{:shortdesc}

## 서비스 정의
{: #define}

|태스크 | 서브태스크 |설명 |환경 |
|------| ----------| ------------|-----|
| {{site.data.keyword.Bluemix}} 플랫폼 알아보기 | ☐ 프로비저닝 계층, {{site.data.keyword.Bluemix_notm}} Identity and Access Management(IAM), 카탈로그, Open Service Broker 및 측정 서비스가 함께 작동하는 방식을 알고 있습니다. | {{site.data.keyword.Bluemix_notm}} 추천 서비스와 달리, 통합 청구 서비스는 {{site.data.keyword.Bluemix_notm}} 플랫폼을 사용하여 서비스 인스턴스를 작성, 바인드, 삭제하고 요금을 부과합니다. 개발을 보다 신속하게 시작하려면 플랫폼을 구성하는 중요한 컴포넌트에 대해 [알아보십시오](/docs/third-party/platform.html#how-it-works). |문서 |
| {{site.data.keyword.Bluemix_notm}} Provider Workbench에 오퍼링 등록. | ☐ 컨텐츠 태스크를 완료했습니다. <br><br>☐ 내 오퍼링을 통합 청구 서비스로 공개하기 위한 승인을 받았습니다. <br><br> ☐ 내 문서 URL 값이 있는 이메일을 받았습니다. <br><br> | 첫 번째 단계는 Provider Workbench에 오퍼링을 등록하는 것입니다. 세부사항은 [튜토리얼 시작하기](/docs/third-party/index.html#get-started)를 참조하십시오. | Provider Workbench |
| {{site.data.keyword.Bluemix_notm}} 문서 공개. | ☐ Provider Workbench에서 안내 태스크를 시작했습니다. <br><br>☐ 내 `Documentation URL`을 받았습니다. <br><br> ☐ 내 문서를 공개했습니다. <br><br> | 웹 사이트에 호스팅된 서드파티 문서가 훌륭한 것을 알고 있습니다. 하지만 통합 청구 서비스를 {{site.data.keyword.Bluemix_notm}}에 제공하고 있으므로 {{site.data.keyword.Bluemix_notm}} 통합 청구 환경에 맞게 사용자 정의된 문서를 제공해야 합니다. 세부사항은 [문서 작성](/docs/third-party/cis1-docs-marketing.html#docs)을 참조하십시오. | Provider Workbench |
| 마케팅 공지사항 공개. | ☐ Provider Workbench에서 마케팅 태스크를 시작했습니다. <br><br>  ☐ 내 마케팅 공지사항을 공개했습니다. <br><br>  | {{site.data.keyword.Bluemix_notm}} 뉴스레터 및 소셜 미디어 채널을 통해 서비스에 대한 가용성을 알리는 마케팅 자료를 작성합니다. 세부사항은 [마케팅 공지사항 작성](/docs/third-party/cis1-docs-marketing.html#announcement)을 참조하십시오. | Provider Workbench |
| 리소스 관리 콘솔에서 오퍼링 등록. | ☐ 고유하고 의미 있는 `service-name`을 내 리소스 이름으로 정의했습니다.<br><br>  리소스 관리 콘솔에 레코드를 가지고 있음을 검증했습니다. <br><br>  | 리소스 관리 콘솔을 사용하여 고유 오퍼링을 작성합니다. 세부사항은 [오퍼링 등록 단계](/docs/third-party/cis2-rmc-define.html#register)를 참조하십시오. | 리소스 관리 콘솔 |
| 리소스 관리 콘솔에서 오퍼링 페이지 완료. | ☐ 내 Provider Workbench 오퍼링 이메일에 제공되는 값을 사용하여 내 문서 URL 및 지시사항 URL을 올바르게 설정했습니다. <br><br>  ☐ 청구 또는 지불 조항이 없는 고유한 서비스 이용 약관 페이지를 가리키는 URL을 제공했습니다.<br><br>  ☐ **플랜 변경 지원**을 사용하는지 여부를 알고 있고 올바르게 지정했습니다. ☐ 내 서비스가 바인드 가능한지 여부를 알고 있고 올바르게 지정했습니다.| {{site.data.keyword.Bluemix_notm}} 타일에 표시된 리소스 관리 콘솔에 카탈로그 메타데이터를 제공하십시오. 세부사항은 [오퍼링 메타데이터 입력 단계](/docs/third-party/cis2-rmc-define.html#offering-metadata)를 참조하십시오. | 리소스 관리 콘솔 |
| 리소스 관리 콘솔에서 액세스 관리 페이지 완료. | ☐ IAM을 사용으로 설정했습니다. <br><br>  ☐ 작성된 일회성 IAM API 키를 저장했으며 이 API 키는 리소스 관리 콘솔에 저장되지 않아 나중에 이를 검색할 수 없음을 알고 있습니다.<br><br> ☐ Open Service Broker를 개발하고 호스팅한 후 내 경로 재지정 URI를 파생시킬 때까지는 액세스 관리 페이지를 완료할 수 없음을 알고 있습니다.<br><br> ☐ 내 Open Service Broker를 호스팅한 후 IAM 페이지로 돌아가 페이지를 완료했습니다.|리소스 관리 콘솔의 {{site.data.keyword.Bluemix_notm}} IAM에 오퍼링을 등록하십시오. IAM을 사용하면 두 플랫폼 서비스 모두에 대해 안전하게 사용자를 인증하고 {{site.data.keyword.Bluemix_notm}} 플랫폼에서 일관되게 리소스에 대한 액세스를 제어할 수 있습니다. 세부사항은 [IAM에 등록 단계](/docs/third-party/cis2-rmc-define.html#reg-iam)를 참조하십시오. | 리소스 관리 콘솔 |
| 리소스 관리 콘솔에서 하나 이상의 가격 플랜 개발. | ☐ 고유한 이름을 가진 무료 플랜을 제공했습니다.<br><br>  ☐ (선택사항) IBM 담당자와 함께 유료 플랜(구독 또는 측정량 기반)을 정의했으며 측정량 기반 플랜을 작성하기 위해 기본 구독 플랜을 제거해야 함을 알고 있습니다.<br><br> ☐ (선택사항) 자동화된 매시간 사용량 제출을 호스팅하고 개발해야 함을 알고 있습니다.| 서비스에 대한 요금을 어떻게 부과합니까? 리소스 관리 콘솔은 무료 또는 유료 플랜을 제공합니다. 세부사항은 [가격 플랜 개발 단계](/docs/third-party/cis2-rmc-define.html#pricing-plan)를 참조하십시오. | 리소스 관리 콘솔 |
| 리소스 관리 콘솔에서 카탈로그 메타데이터 내보내기. | ☐ 리소스 관리 콘솔 오퍼링 및 가격 페이지에서 제공한 메타데이터 중 일부를 내 Open Service Broker로 내보내어 제공해야 함을 알고 있습니다. <br><br>  ☐ 배치 페이지에서 `catalog.json` 파일을 받았으며 서비스 배열을 내 Open Service Broker의 메타데이터에 맵핑할 준비가 되었습니다.<br><br> |리소스 관리 콘솔에서 서비스를 정의했으므로 `catalog.json` 파일을 다운로드하고 이를 사용하여 Open Service Broker의 개발을 알릴 수 있습니다. 세부사항은 [메타데이터 내보내기 단계](/docs/third-party/cis2-rmc-define.html#export-metadata)를 참조하십시오. | 리소스 관리 콘솔 |
{: caption="표 1. 통합 청구 서비스 정의" caption-side="top"}

## 서비스 개발
{: #develop}

|태스크 | 서브태스크 |설명 |환경 |
|------| ----------| ------------|-----|
| Open Service Broker 스펙 버전 2.12에 대해 알아보기. | ☐ Open Service Broker 스펙을 읽었으며 내 Open Service Broker를 개발해야 함을 알고 있습니다. <br><br>  | 서비스 브로커는 서비스 라이프사이클을 관리합니다. {{site.data.keyword.Bluemix_notm}} 플랫폼은 Open Service Broker와 상호작용하여 서비스 인스턴스 및 서비스 바인딩을 프로비저닝하고 관리합니다. 세부사항은 [서비스 브로커 개발 및 호스팅](/docs/third-party/cis3-broker.html#step3-osb)을 참조하십시오. |문서 |
| {{site.data.keyword.Bluemix_notm}} 브로커 샘플 보기. | ☐ 저장소를 복제했으며 브로커 샘플을 찾아보고 이 샘플을 사용하여 개발을 시작할 준비가 되었습니다. <br><br>  | [https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘") | 코드 예제 |
| {{site.data.keyword.Bluemix_notm}} Open Service Broker API 문서 보기. | ☐ 내 Open Service Broker의 코드에서 지원해야 하는 몇 가지 필수 엔드포인트가 있음을 알고 있습니다. <br><br>  ? 내 서비스를 {{site.data.keyword.Bluemix_notm}}의 앱에 바인드할 수 있으면 API 엔드포인트와 인증 정보를 내 서비스 사용자에게 리턴할 수 있어야 함을 알고 있습니다. <br><br> ☐ {{site.data.keyword.Bluemix_notm}}에서 서비스 인스턴스를 사용 안함으로 설정했다가 다시 사용으로 설정할 수 있는 확장 API 엔드포인트를 정의했음을 알고 있습니다. | {{site.data.keyword.Bluemix_notm}} Open Service Broker는 Open Service Broker 2.12 스펙을 확장합니다. 서비스 브로커에서 사용해야 하는 필수 엔드포인트에 대해 [알아보기](/docs/third-party/cis3-broker.html#docs)를 수행하십시오. |문서 |
| 카탈로그 메타데이터를 사용하여 서비스 브로커 개발 시작. | ☐ 리소스 관리 콘솔에서 제공한 메타데이터 중 일부를 내 Open Service Broker로 내보내어 제공해야 함을 알고 있습니다.  <br><br>  ☐ 내 `catalog.json` 파일에 나열된 필수 GUID 및 기타 필수 값을 내 샘플 Open Service Broker의 서비스 배열에 추가했습니다. | 리소스 관리 콘솔에서 `catalog.json` 파일을 다운로드한 후 이를 사용하여 Open Service Broker의 개발을 알릴 수 있습니다. 세부사항은 [내보낸 메타데이터를 사용하여 개발을 안내하는 단계](/docs/third-party/cis3-broker.html#use-metadata)를 참조하십시오. | 개발 환경 및 문서 |
| Open Service Broker 호스팅. | ☐ 내 서비스 브로커의 호스팅된 위치가 TLS(Transport Layer Security) 프로토콜 버전 1.2를 따라야 함을 알고 있습니다. <br><br> | 서비스 브로커는 REST API 호출에 응답할 수 있는 앱의 일부로 호스팅되어야 합니다. 또한 호스트 위치는 {{site.data.keyword.Bluemix_notm}} 보안 가이드라인을 준수해야 합니다. 세부사항은 [서비스 브로커 호스팅 단계](/docs/third-party/cis3-broker.html#host)를 참조하십시오. | 개발 환경 및 문서 |
| 호스팅된 Open Service Broker 테스트. | ☐ 호스팅된 서비스 브로커에 대해 curl 명령을 실행하여 내 서비스 브로커가 지원하는 각 API 엔드포인트를 유효성 검증했습니다. <br><br> | 사용하는 다른 엔드포인트에 대해 curl 명령을 실행하여 서비스 브로커의 유효성을 검증하십시오. 세부사항은 [서비스 브로커 테스트 단계](/docs/third-party/cis3-broker.html#test)를 참조하십시오.| 개발 환경 및 문서 |
| IAM 경로 재지정 URI 파생 및 설정. | ☐ 내 Open Service Broker의 호스팅된 위치 및 일부 인증 정보를 사용하여 내 IAM 경로 재지정 URI를 파생했습니다. <br><br> ☐ 내 경로 재지정 URI를 지정하고 내 클라이언트 ID를 올바르게 설정하여 액세스 관리 페이지를 완료했습니다. <br><br> | 리소스 관리 콘솔에서 서비스를 정의하면 클라이언트 ID를 생성하는 것입니다. 그러나 이 때 경로 재지정 URI는 없을 가능성이 큽니다. 즉, 클라이언트 ID가 `false`로 설정됩니다. 경로 재지정 URI를 사용하여 리소스 관리 콘솔로 돌아갈 때까지 클라이언트 ID를 가질 수 없습니다. 세부사항은 [경로 재지정 URI 파생 단계](/docs/third-party/cis5-iam.html#redirect-uri)를 참조하십시오. | 개발 환경 및 리소스 관리 콘솔 |
| 인증을 위한 오픈 권한 부여(OAuth) 플로우 개발. | ☐ IAM에서 OIDC(Open ID Connect)를 지원함을 알고 있습니다. <br><br> ☐ 내 IAM 지역 엔드포인트를 검색했으며 사용자를 `dashboard_url`에서 조합된 내 경로 재지정 URI로 경로 재지정하고, 인증하는 중에 사용할 수 있도록 리턴된 사용자의 `access_token`을 내 응답에 저장합니다. <br><br> | 서비스 대시보드를 방문하는 사용자는 올바르게 인증되어야 합니다. IAM을 사용하여 OAuth 토큰 기반 인증 및 권한 부여를 개발하십시오. 세부사항은 [OAuth 플로우 개발 단계](/docs/third-party/cis5-iam.html#oauth)를 참조하십시오. | 개발 환경 및 문서|
| 사용자 권한 유효성 검증. | ☐ API 키에 대한 액세스 토큰을 받을 수 있습니다. <br><br> ☐ 서비스 인스턴스에 대한 사용자의 권한을 유효성 검증할 수 있습니다. <br><br> | 인증을 위한 OAuth 플로우를 개발한 후 사용자가 올바르게 권한 부여되었는지 유효성 검증하여 서비스 사용자가 서비스 대시보드에 액세스할 수 있도록 해야 합니다. 세부사항은 [유효성 검증 단계](/docs/third-party/cis5-iam.html#validate)를 참조하십시오. | 개발 환경 및 문서 |
{: caption="표 2. 통합 청구 서비스 개발" caption-side="top"}

## 서비스 공개 및 테스트
{: #pubtest}

|태스크 | 서브태스크 |설명 |환경 |
|------| ----------| ------------|-----|
| 제한된 가시성 모드로 서비스 공개. | ☐ 내 호스팅된 Open Service Broker를 리소스 관리 콘솔의 배치 페이지에서 등록했습니다. <br><br> ☐ 새 배치를 작성했으며 하나 이상의 지역에 내 오퍼링을 공개했습니다. <br><br> | 호스팅된 서비스 브로커가 Open Service Broker 스펙을 충족하므로 서비스를 {{site.data.keyword.Bluemix_notm}} 카탈로그에 공개할 수 있습니다. 세부사항은 [서비스 공개 단계](/docs/third-party/cis4-rmc-publish.html#publish)를 참조하십시오. | 리소스 관리 콘솔 |
| 오퍼링 테스트. | ☐ 카탈로그에서 내 서비스를 볼 수 있습니다. <br><br> ☐ 서비스 인스턴스 대시보드에서 인증을 유효성 검증했습니다. <br><br> ☐ 내 서비스가 카탈로그에 올바르게 표시되는지 검증했습니다. <br><br> ☐ 플랜을 선택하고 서비스 인스턴스를 작성할 수 있습니다. <br><br> ☐ 서비스 인스턴스를 삭제할 수 있습니다. <br><br> ☐ 내 서비스를 다른 애플리케이션에 연결할 수 있습니다. <br><br> ☐ 내 서비스 연결을 끊고 연결을 삭제할 수 있습니다. <br><br>  ☐ 서비스 키를 생성하고 이 서비스 키를 삭제할 수 있습니다. <br><br> ☐ 내 IBM 담당자와 함께 내 오퍼링이 사용 및 사용 안함 엔드포인트를 지원하는지 검증했습니다. <br><br> ☐ 내 오퍼링에 측정량 기반 플랜이 있으므로 사용량 제출을 테스트했습니다. | 호스팅된 서비스 브로커가 Open Service Broker 스펙을 충족하므로 서비스를 {{site.data.keyword.Bluemix_notm}} 카탈로그에 공개할 수 있습니다. 세부사항은 [서비스 테스트 단계](/docs/third-party/cis4-rmc-publish.html#test)를 참조하십시오. | {{site.data.keyword.Bluemix_notm}} 콘솔 |
{: caption="표 3. 통합 청구 서비스 공개 및 테스트" caption-side="top"}

