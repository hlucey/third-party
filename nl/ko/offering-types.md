---


copyright:
  years: 2018
lastupdated: "2018-07-01"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# 써드파티 오퍼링 유형
{: #offering-types}

{{site.data.keyword.Bluemix}}에서 써드파티 오퍼링을 통합 청구 서비스 또는 추천 서비스로 제공할 수 있습니다.
{:shortdesc}

써드파티 오퍼링을 통합 청구 서비스로 제공하면 사용자가 {{site.data.keyword.Bluemix_notm}} 콘솔의 카탈로그 세부사항 페이지에 나열된 다양한 IBM 가격 책정 플랜을 선택할 수 있습니다. 또한 사용자는 써드파티 오퍼링의 인스턴스를 자동으로 작성할 수 있습니다.

써드파티 오퍼링을 추천 서비스로 제공하는 경우, 사용자는 {{site.data.keyword.Bluemix_notm}} 콘솔의 카탈로그 세부사항 페이지에서 웹 사이트로 이동하게 됩니다. 웹 사이트에서 사용자는 계정을 작성하고 써드파티 오퍼링을 {{site.data.keyword.Bluemix_notm}}에서 빌드 중인 앱에 프로그래밍 방식으로 연결하는 데 필요한 적절한 신임 정보를 얻습니다.

## 오퍼링 유형 비교
{: #compare}

다음 표에서는 써드파티 오퍼링 유형의 상세한 비교 내용을 제공합니다.

|  | 통합 청구 서비스  | 추천 서비스 |
|---|---|---|
| **온보딩** | 온보딩은 Provider Workbench(PWB) 및 리소스 관리 콘솔에서 처리됩니다. 오퍼링 제공자는 Open Service Broker를 개발하고 이를 호스팅 및 테스트하며 해당 오퍼링을 일련의 셀프 서비스 단계를 통해 공개합니다. | 온보딩은 Provider Workbench에서 처리됩니다. 셀프 서비스 온보딩 프로세스는 약 2주 정도 걸립니다. |
| **배치** | {{site.data.keyword.Bluemix_notm}} 플랫폼에서 프로비저닝됩니다. | API 기반 서비스만 해당 |
| **비용 청구**  | 통합 청구 모델에서 사용자는 IBM 오퍼링과 해당 통합 써드파티 오퍼링에 모두에 대해 단일 청구서를 받습니다. | 추천 모델에서는 제공자가 사용자에게 청구하고 수익의 100% 를 보존합니다. |
| **예제** | [PowerAI](https://console.bluemix.net/catalog/services/powerai) | [Accern API](https://console.bluemix.net/catalog/services/accern-api) |
{: caption="표1. 써드파티 오퍼링 유형의 비교" caption-side="top"}

