---

copyright:
  years: 2018
lastupdated: "2018-07-02"

---

{:right: .ph data-hd-position='right'}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}

# 엔드-투-엔드 체크리스트
{: #checklist}

다음 체크리스트를 사용하여 통합 청구 서비스를 정의, 개발 및 공개하는 데 필요한 모든 태스크를 추적할 수 있습니다.

## 오퍼링 정의

|태스크 | 서브태스크 |설명 |환경 |
|------| ----------| ------------|-----|
| {{site.data.keyword.Bluemix_notm}} 플랫폼 알아보기 | ☐ {{site.data.keyword.Bluemix_notm}} 플랫폼에 대해 프로비저닝 계층, {{site.data.keyword.Bluemix_notm}} IAM, 카탈로그, OSB 및 측정 서비스가 모두 함께 작동하는 방식을 알고 있습니다. | {{site.data.keyword.Bluemix_notm}} 추천 서비스와 달리, 통합 청구 서비스는 {{site.data.keyword.Bluemix_notm}} 플랫폼을 사용하여 서비스 인스턴스를 작성, 바인드, 삭제하고 요금을 부과합니다. 개발을 보다 신속하게 시작하려면 플랫폼을 구성하는 중요한 컴포넌트를 [알아보십시오](/docs/third-party/platform.html#what-is-the-ibm-cloud-platform-)! |문서 |
| PWB에 등록 | ☐ PWB에서 **컨텐츠 태스크**를 완료했습니다. <br><br>☐ 내 오퍼링을 통합 청구 서비스로 공개하기 위한 승인을 받았습니다. <br><br> ☐ 내 문서 URL 값이 있는 초기 이메일을 받았습니다. <br><br> | 첫 번째 단계는 오퍼링을 {{site.data.keyword.Bluemix_notm}} PWB에 등록하는 것입니다. 태스크 완료에 대한 자세한 정보는 [튜토리얼 시작하기](/docs/third-party/index.html#get-started)를 참조하십시오. | PWB |
| {{site.data.keyword.Bluemix_notm}} 문서 작성 및 공개 | ☐ PWB에서 **안내 태스크(문서)**를 시작했습니다. <br><br>☐ 내 `문서 URL`을 받았습니다. <br><br> ☐ 내 문서를 공개했습니다. <br><br> | 웹 사이트에 호스팅된 써드파티 문서가 훌륭한 것을 알고 있습니다. 그러나 지금 통합 청구 서비스를 {{site.data.keyword.Bluemix_notm}}에 제공하고 있으므로 {{site.data.keyword.Bluemix_notm}} 통합 청구 환경에 맞게 사용자 정의된 문서를 제공해야 합니다. PWB는 이 태스크를 안내하고 https://console.bluemix.net/docs/ 사이트에 문서를 공개할 수 있도록 지원합니다. 태스크 완료에 대한 자세한 정보는 [시작하기 문서 작성](/docs/third-party/cis1-docs-marketing.html#docs)을 참조하십시오. | PWB |
| 마케팅 공지사항 작성 및 공개 | ☐ PWB에서 **마케팅 태스크(공지사항)**를 시작했습니다. <br><br>  ☐ 내 공지사항을 공개했습니다. <br><br>  | {{site.data.keyword.Bluemix_notm}} 뉴스레터 및 소셜 미디어 채널을 통해 서비스에 대한 가용성을 알리는 마케팅 자료를 작성합니다. PWB는 이 태스크를 안내합니다. 추가 세부사항은 [시작하기 문서 작성](/docs/third-party/cis1-docs-marketing.html#announcement)을 참조하십시오. | PWB |
| 리소스 관리 콘솔에서 서비스 등록 | ☐ 고유하고 의미 있는 `service-name`을 내 **리소스 이름**으로 정의했습니다.<br><br>  ☐ 이를 저장하고 리소스 관리 콘솔에 레코드를 가지고 있음을 검증했습니다. <br><br>  | 리소스 관리 콘솔을 통해 고유한 오퍼링을 작성할 수 있습니다. [안내](/docs/third-party/cis2-rmc-define.html#register-your-offering-by-using-the-resource-management-console-rmc-)에 따라 오퍼링을 등록합니다. | 리소스 관리 콘솔 |
| 리소스 관리 콘솔에서 **오퍼링** 페이지 완료 | ☐ 내 PWB 오퍼링 메일에서 제공된 값을 사용하여 내 **문서 URL** 및 **지시사항 URL**을 올바르게 설정했습니다.<br><br>  ☐ 내 회사 TOS 페이지가 아니지만 청구 또는 지불 조항이 없는 고유한 TOS 페이지인 **서비스 이용 약관** URL을 제공했습니다.<br><br>  ☐ **플랜 변경 지원**을 사용하는지 여부를 알고 있고 올바르게 지정했습니다. ☐ 내 서비스가 **바인드 가능**한지 여부를 알고 있고 올바르게 지정했습니다.| {{site.data.keyword.Bluemix_notm}} 타일에 표시되는 리소스 관리 콘솔에 카탈로그 메타데이터를 제공합니다. 여기에는 서비스 이용 약관과 같은 중요한 URL과, 정보 글머리 기호 등 오퍼링에 대해 의미 있는 세부사항이 포함되어 있습니다. [안내](/docs/third-party/cis2-rmc-define.html#enter-your-offering-metadata-rmc-offering-page-)에 따라 오퍼링의 필수 및 권장 카탈로그 메타데이터를 설정합니다. | 리소스 관리 콘솔 |
| 리소스 관리 콘솔에서 **액세스 관리** 페이지 완료 | ☐ IAM을 사용하도록 설정했습니다.<br><br>  ☐ 리소스 관리 콘솔 UI에서 작성한 일회용으로 생성된 IAM API 키를 저장했으며 이 API 키는 리소스 관리 콘솔에 저장되어 있지 않고 나중에 이를 검색할 수 없음을 알고 있습니다.<br><br> ☐ 이후 단계에서 OSB를 개발하고 호스팅한 후 내 경로 재지정 URI를 파생시키기 전에는 액세스 관리 페이지를 완료할 수 없음을 알고 있습니다.<br><br> ☐ 내 OSB를 작성하고 호스팅한 후에 IAM 페이지로 돌아가 **경로 재지정 URI 추가**를 클릭하고 내 파생된 값을 추가하여 페이지를 완료했습니다.| 리소스 관리 페이지에서 오퍼링을 {{site.data.keyword.Bluemix_notm}} IAM(Identity and Access Management)에 등록합니다. IAM을 사용하면 두 플랫폼 서비스 모두에 대해 안전하게 사용자를 인증하고 {{site.data.keyword.Bluemix_notm}} 플랫폼에서 일관되게 리소스에 대한 액세스를 제어할 수 있습니다. (다시 돌아가서 경로 재지정 URI를 사용하도록 설정합니다). [안내](/docs/third-party/cis2-rmc-define.html#register-with-identity-and-access-management-rmc-iam-page-)에 따라 오퍼링의 초기 액세스 관리를 사용으로 설정합니다. | 리소스 관리 콘솔 |
| 리소스 관리 콘솔에서 하나 이상의 가격 책정 플랜 개발 | ☐ 고유한 이름을 가진 무료 사용제를 제공했습니다.<br><br>  ☐ (선택사항) IBM 담당자와 함께 유료 사용제(구독 또는 측정량 기반)를 정의했으며 측정량 기반 플랜을 작성하기 위해 기본 구독 플랜을 제거해야 함을 알고 있습니다.<br><br> ☐ (선택사항) {{site.data.keyword.Bluemix_notm}} 플랫폼 측정 서비스를 사용하여 자동화된 매시간 사용량 제출을 호스팅하고 개발하는 데 필요한 측정량 기반 플랜을 알고 있습니다.| 오퍼링에 대한 요금을 어떻게 부과합니까? 리소스 관리 콘솔은 무료 또는 유료(구독 및 측정량 기반) 사용제를 제공합니다. [안내](/docs/third-party/cis2-rmc-define.html#develop-a-pricing-plan-rmc-pricing-page-)에 따라 오퍼링의 가격 책정 플랜을 정의합니다. | 리소스 관리 콘솔 |
| 리소스 관리 콘솔에서 카탈로그 메타데이터 내보내기| ☐ 리소스 관리 콘솔 **오퍼링** 및 **가격 책정** 페이지에서 제공한 메타데이터 중 일부를 내 OSB로 내보내어 제공했음을 알고 있습니다. 리소스 관리 콘솔에서 값을 내보내어 리소스 관리 콘솔에서 생성한 내 서비스 및 플랜 ID와 같은 중요한 GUID를 맵핑하고, 플랫폼 프로비저닝 계층이 이 프로비저닝 계약을 내 `catalog GET` 엔드포인트의 응답에서 읽을 수 있도록 이 GUID를 내 OSB에 제공할 수 있습니다. <br><br>  ☐ 리소스 관리 콘솔 **배치** 페이지에서 `catalog.json` 파일을 받았으며 서비스 배열을 내 OSB의 메타데이터에 맵핑할 준비가 되었습니다.<br><br> |이제 리소스 관리 콘솔에서 서비스를 정의했으므로 catalog.json 파일을 다운로드하고 이를 사용하여 Open Service Broker를 개발할 수 있습니다. catalog.json에는 브로커에 호스팅되어야 하는 메타데이터가 포함되어 있습니다. 이러한 값은 브로커가 지원하는 서비스 및 플랜에 대한 브로커와 IBM Cloud 플랫폼 간의 계약을 정의합니다. [안내](/docs/third-party/cis2-rmc-define.html#export-your-metadata-as-json-rmc-deployments-page-)에 따라 카탈로그 메타데이터를 내보냅니다. | 리소스 관리 콘솔 |
{: caption="표1. 통합 청구 오퍼링 정의" caption-side="top"}

## 오퍼링 개발

|태스크 | 서브태스크 |설명 |환경 |
|------| ----------| ------------|-----|
| Open Service Broker(OSB) 스펙 버전 2.12 알아보기 | ☐ OSB 스펙을 읽었으며 내 OSB를 개발해야 함을 알고 있습니다. <br><br>  | 서비스 브로커는 서비스 라이프사이클을 관리합니다. {{site.data.keyword.Bluemix_notm}} 플랫폼은 Open Service Broker와 상호작용하여 서비스 인스턴스(서비스 오퍼링의 인스턴스화) 및 서비스 바인딩(애플리케이션과 서비스 인스턴스 간의 연관 표시, 보통 애플리케이션이 서비스 인스턴스와 통신하는 데 사용할 신임 정보가 포함됨)을 프로비저닝하고 관리합니다. 버전 2.12 스펙에 대해 [알아보기](/docs/third-party/cis3-broker.html#become-familiar-with-the-osb-specification) |문서 |
| {{site.data.keyword.Bluemix_notm}} 브로커 샘플 보기 | ☐ 복제본을 복제했으며 브로커 샘플을 보고 해당 샘플을 사용하여 개발을 시작할 준비가 되었습니다. <br><br>  | [https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘") | 코드 예제 |
| {{site.data.keyword.Bluemix_notm}} Open Service Broker API 문서 보기 | ☐ 내 OSB의 코드에서 지원해야 하는 몇 가지 필수 엔드포인트가 있음을 알고 있습니다. <br><br>  내 서비스를 {{site.data.keyword.Bluemix_notm}}의 애플리케이션에 바인드할 수 있으면 API 엔드포인트와 신임 정보를 서비스 이용자에게 리턴할 수 있어야 함을 알고 있습니다. <br><br> ☐ {{site.data.keyword.Bluemix_notm}}에서 서비스 인스턴스를 사용 안함으로 설정했다가 다시 사용하도록 설정할 수 있는 확장 API 엔드포인트를 정의했음을 알고 있습니다. 내 OSB를 확장하여 **인스턴스 사용 및 사용 안함(GET 및 PUT)**을 정의해야 합니다. | {{site.data.keyword.Bluemix_notm}} Open Service Broker는 Open Service Broker 2.12 스펙을 확장합니다. 브로커에서 사용해야 하는 필수 엔드포인트에 대해 [알아보기](/docs/third-party/cis3-broker.html#view-our-resource-broker-api-documentation) |문서 |
| 카탈로그 메타데이터를 사용하여 브로커 개발 시작 | ☐ 리소스 관리 콘솔 **오퍼링** 및 **가격 책정** 페이지에서 제공한 메타데이터 중 일부를 내 OSB로 내보내어 제공했음을 알고 있습니다. 리소스 관리 콘솔에서 값을 내보내어 리소스 관리 콘솔에서 생성한 내 서비스 및 플랜 ID와 같은 중요한 GUID를 맵핑하고, 플랫폼 프로비저닝 계층이 이 프로비저닝 계약을 내 `catalog GET` 엔드포인트의 응답에서 읽을 수 있도록 이 GUID를 내 OSB에 제공할 수 있습니다. <br><br>  ☐ 내 `catalog.json` 파일에 나열된 필수 GUID 및 기타 필수 값을 내 샘플 OSB의 서비스 배열에 추가했습니다. | 리소스 관리 콘솔에서 `catalog.json` 파일을 다운로드한 후 이를 사용하여 Open Service Broker를 개발할 수 있습니다. catalog.json에는 브로커에 호스팅되어야 하는 메타데이터가 포함되어 있습니다. 이러한 값은 브로커가 지원하는 서비스 및 플랜에 대한 브로커와 IBM Cloud 플랫폼 간의 프로비저닝 계약을 정의합니다. [안내](/docs/third-party/cis3-broker.html#learn-how-to-use-the-exported-metadata-to-guide-your-broker-development)에 따라 내보낸 카탈로그 메타데이터를 OSB에 추가합니다. | 개발 환경 및 문서 |
| OSB 호스트 | ☐ 내 브로커의 호스트 위치가 TLS(Transport Layer Security) 프로토콜 버전 1.2를 준수해야 함을 알고 있습니다. 또한 내 브로커가 공용 인터넷에서 액세스할 수 있는 올바른 HTTP 엔드포인트에 호스팅되어야 합니다. <br><br> | 브로커는 REST API 호출에 응답할 수 있는 애플리케이션의 일부로 호스팅되어야 합니다. 또한 호스트 위치는 IBM Cloud 보안 가이드라인을 준수해야 합니다. [안내](/docs/third-party/cis3-broker.html#host-your-brokers)에 따라 브로커를 호스팅합니다. | 개발 환경 및 문서 |
| 호스팅된 OSB 테스트 | ☐ 호스팅된 브로커에 대해 curl 명령을 실행하고 응답을 유효성 검증하여 내 브로커가 지원하는 API 엔드포인트 각각을 유효성 검증했습니다. <br><br> | 사용하려는 다른 엔드포인트에 대해 curl 명령을 실행하여 브로커의 유효성을 검증해야 합니다. [안내](/docs/third-party/cis3-broker.html#how-to-test-your-service-s-broker)에 따라 브로커를 호스팅합니다.| 개발 환경 및 문서 |
| IAM 경로 재지정 URI 파생 및 설정 | ☐ 내 OSB의 호스트 위치 및 일부 인증 정보를 사용하여 내 IAM 경로 재지정 URL을 파생시켰습니다. <br><br> ☐ 내 **경로 재지정 URI**를 지정하고 내 클라이언트 ID를 올바르게 설정하여 리소스 관리 콘솔 **액세스 관리** 페이지를 완료했습니다. <br><br> | 리소스 관리 콘솔에서 서비스를 정의했으면 클라이언트 ID를 생성한 것입니다. 그러나 이 때 경로 재지정 URI는 없었을 가능성이 큽니다. 이는 IAM이 `false`로 설정된 클라이언트 ID를 생성했음을 의미합니다. **경로 재지정 URI**를 사용하여 리소스 관리 콘솔로 돌아가기 전에는 true 클라이언트 ID를 가질 수 없습니다. [안내](/docs/third-party/cis5-iam.html#derive-your-iam-redirect-uri-resource-management-console-iam-page-)에 따라 IAM 경로 재지정 URI를 파생시키고 설정합니다. | 개발 환경 및 리소스 관리 콘솔 |
| 인증을 위한 OAuth 플로우 개발 | ☐ IAM에서 OIDC(Open ID Connect)를 지원함을 알고 있습니다. <br><br> ☐ 내 IAM 지역 엔드포인트를 검색했으며 사용자를 `dashboard_url`에서 조합된 내 경로 재지정 URI로 경로 재지정하고, 인증하는 중에 사용할 수 있도록 리턴된 사용자의 `access_token`을 내 응답에 저장합니다. <br><br> | 서비스 대시보드를 방문하는 사용자는 올바르게 인증되어야 합니다. {{site.data.keyword.Bluemix_notm}} IAM(Identity and Access Management)을 사용하여 오픈 권한 부여 토큰 기반 인증 및 권한 부여를 개발합니다. [안내](/docs/third-party/cis5-iam.html#oauth)에 따라 인증을 위한 OAuth 플로우를 개발합니다. | 개발 환경 및 문서|
| 사용자 권한 유효성 검증 | ☐ IAM과 통신하여 API 키에 대한 액세스 토큰을 받을 수 있습니다. <br><br> ☐ 서비스 인스턴스에 대한 사용자 권한을 유효성 검증할 수 있습니다(/v2/authz POST). <br><br> | 인증을 위한 OAuth 플로우를 개발한 후 사용자가 올바르게 권한 부여되었는지 유효성 검증하여 서비스 사용자가 서비스 대시보드에 액세스할 수 있도록 해야 합니다. [안내](/docs/third-party/cis5-iam.html#validate)에 따라 사용자 권한을 유효성 검증합니다. | 개발 환경 및 문서 |
{: caption="표2. 통합 청구 오퍼링 개발" caption-side="top"}

## 오퍼링 공개 및 테스트

|태스크 | 서브태스크 |설명 |환경 |
|------| ----------| ------------|-----|
| 제한된 가시성 모드로 오퍼링 공개 | ☐ 내 호스팅된 OSB를 리소스 관리 콘솔 **개발** 페이지에 등록했습니다. <br><br> ☐ 새 배치를 리소스 관리 콘솔 **배치** 페이지에 작성했으며 내 오퍼링을 하나 이상의 지역에 공개했습니다. <br><br> | 이제 OSB 스펙에 맞는 브로커를 호스팅하게 되었으므로 리소스 관리 콘솔로 돌아가 서비스를 {{site.data.keyword.Bluemix_notm}} 카탈로그에 공개할 수 있습니다. [안내](/docs/third-party/cis4-rmc-publish.html#publish-your-service-to-ibm-cloud)에 따라 오퍼링을 제한된 가시성 모드로 공개합니다. | 리소스 관리 콘솔 |
| 오퍼링 테스트 | ☐ 내 화이트리스트 계정으로 로그인하여 https://console.bluemix.net 카탈로그에서 내 서비스를 볼 수 있습니다. <br><br> ☐ 서비스 인스턴스 대시보드에서 인증을 유효성 검증했습니다. <br><br> ☐ 내 오퍼링이 카탈로그에 올바르게 표시되는지 검증했습니다. <br><br> ☐ 프로비저닝 작업을 유효성 검증했습니다. 플랜을 선택하고 서비스 인스턴스를 작성할 수 있습니다. <br><br> 디프로비저닝 작업을 검증했습니다. 서비스 인스턴스를 삭제할 수 있습니다. <br><br> ☐ 바인드 작업을 유효성 검증했습니다. **연결**을 클릭하여 내 서비스를 다른 애플리케이션에 연결할 수 있습니다. <br><br> ☐ 바인드 해제 작업을 유효성 검증했습니다. 내 서비스 연결을 끊고 연결을 삭제할 수 있습니다. <br><br>  ☐ 서비스 키 작성 및 서비스 키 삭제 작업을 유효성 검증했습니다. **신임 정보**를 클릭하고 서비스 키를 생성하며 해당 서비스 키를 삭제할 수 있습니다. <br><br> ☐ 내 IBM 담당자와 함께 내 오퍼링이 사용 및 사용 안함 엔드포인트를 지원하는지 검증했습니다. <br><br> ☐ 내 오퍼링에 측정량 기반 플랜이 있으므로 사용량 API에 대한 curl을 수행한 후 사용량에 따라 정확한 가격을 올바르게 리턴하여 사용량 제출을 테스트했으며, 자동화된 사용량 시간별 제출을 사용하여 내 서비스 인스턴스를 프로비저닝하는 모든 사용자를 지원하는지 테스트했습니다. | 이제 OSB 스펙에 맞는 브로커를 호스팅하게 되었으므로 리소스 관리 콘솔로 돌아가 서비스를 {{site.data.keyword.Bluemix_notm}} 카탈로그에 공개할 수 있습니다. [안내](/docs/third-party/cis4-rmc-publish.html#test-your-deployed-offering)에 따라 개발된 서비스를 테스트합니다. | {{site.data.keyword.Bluemix_notm}} 콘솔 |
{: caption="표3. 통합 청구 오퍼링 공개 및 테스트" caption-side="top"}

