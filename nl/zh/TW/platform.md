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

# 整合式計費服務如何使用 {{site.data.keyword.Bluemix_notm}} 平台

整合式計費服務與轉介服務不同。整合式計費服務使用 {{site.data.keyword.Bluemix_notm}} 平台進行鑑別、存取、佈建、計量及計費。本主題提供整合式計費服務將使用之平台元件的進階概觀。

## {{site.data.keyword.Bluemix_notm}} 佈建層

佈建層管理 {{site.data.keyword.Bluemix_notm}} 資源的生命週期。佈建層負責控制及追蹤客戶帳戶中資源的生命週期。*資源* 是可以針對應用程式或服務實例佈建或保留的實體或邏輯元件。資源的範例包括資料庫、帳戶，以及處理器、記憶體和儲存空間限制。一般而言，佈建層所追蹤的資源預期會有相關聯的用量度量值及計費，但不一定都是這種情況。在某些情況下，資源可能會與佈建層相關聯，確保可以管理資源生命週期及帳戶生命週期。

### 資源生命週期管理

佈建層提供共用 API，來控制從佈建（建立實例）、連結（建立存取認證）、取消連結（移除存取權）再到取消佈建（刪除實例）的資源生命週期。此外，{{site.data.keyword.Bluemix_notm}} 平台提供 CLI 及使用者介面來管理資源的生命週期，而這些資源不需要您自行建立設施。

佈建層提供 API，協助您管理資源生命週期的下列元素：
* 佈建
* 更新資源實例
* 連結
* 資源金鑰
* 取消連結
* 取消佈建

## {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM)

Identity Access Management (IAM) 可讓您安全地鑑別使用者，並跨 {{site.data.keyword.Bluemix_notm}} 一致地控制所有雲端資源的存取。{{site.data.keyword.Bluemix_notm}} 佈建層已採用 IAM 來鑑別及授權針對佈建層所採取的動作。協力廠商供應項目提供者會使用 IAM 來建立鑑別流程 (OAuth)。如需詳細資料，請參閱[何謂 IAM？](/docs/iam/index.html#iamoverview)

如果您的供應項目使用 OpenID Connect (OIDC) 程式庫，則 IAM 支援 OIDC 整合。OIDC 是 OAuth 2.0 上的鑑別層，而 OAuth 2.0 是可協助簡化上線處理程序的授權架構。如需 OIDC 的相關資訊，請參閱 [Open ID Connect](http://openid.net/connect/){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。

## {{site.data.keyword.Bluemix_notm}} 型錄

{{site.data.keyword.Bluemix_notm}} 型錄會儲存 {{site.data.keyword.Bluemix_notm}} 主控台中所顯示資源的供應項目定義（說明、特性、影像、URL 等等）。資源管理主控台用來定義服務必要 meta 資料的所有層面。此 meta 資料會發佈至型錄，並用於顯示在型錄中。您可以在資源管理主控台的**供應項目**及**方案**頁面中找到必要及選用 meta 資料欄位的詳細資訊，但這裡會包括可幫助您快速瞭解的主要項目。

   * 服務名稱：服務的技術名稱。服務名稱十分重要，而且必須正確地定義。您必須同時提供 {{site.data.keyword.Bluemix_notm}} 平台用來識別服務的服務名稱，以及客戶在 {{site.data.keyword.Bluemix_notm}} 型錄中看到的顯示名稱。服務名稱不是您的顯示名稱。
   * 服務顯示名稱：使用者易記的服務名稱。例如，"Compose Redis"
   * 服務 ID：用於 OSB 分配管理系統之 API 呼叫的服務 GUID。這必須是唯一值。
   * 服務圖示：含服務標誌的 SVG
   * 服務說明：將游標移至 {{site.data.keyword.Bluemix_notm}} 型錄使用者介面中的資源圖示上方時所顯示的資源說明。您可以新增一個句子或一個詞組來作為說明。
   * 服務詳細說明：出現在型錄清單頁面中的第一個段落。請考慮至少使用兩個句子來作為詳細說明。
   * 文件 URL：{{site.data.keyword.Bluemix_notm}} 文件的鏈結。您將在 PWB 中編寫，而且 PWB 將為您產生 URL 值。
   * 條款 URL：服務之使用條款的鏈結。請注意，針對 GDPR 用途，請不要鏈結至您的現有協力廠商服務條款。相反地，您必須為整合式計費服務提供唯一頁面。
   * 指示 URL：與「文件 URL」類似，您將指向 {{site.data.keyword.Bluemix_notm}} 文件；不過，「指示 URL」會將您的文件動態地取回到服務儀表板的「入門」標籤中。
   * 種類：選取您的服務應該放在型錄中的可用 {{site.data.keyword.Bluemix_notm}} 種類。
   * 項目符號：服務的簡明標示符號
   * 媒體：服務的畫面擷取及視訊
   * 服務方案名稱：每一個方案都有一個技術名稱。全部小寫、沒有空格，且可以包括 "-"。例如，`gold`。
   * 服務方案顯示名稱：使用者易記的方案名稱。例如，`Gold`
   * 服務方案 ID：用於 OSB 分配管理系統之 API 呼叫的服務方案 GUID。這必須是唯一值。資源管理主控台將會為您產生此值。
   * 服務方案說明：資源方案的說明。在 IBM Cloud 型錄的資源詳細資料頁面上選取方案之後，即會顯示說明。
   * 服務方案項目符號：服務方案的簡明標示符號


## Open Service Broker

「服務分配管理系統」可管理服務的生命週期。{{site.data.keyword.Bluemix_notm}} 平台會與「服務分配管理系統」互動，以佈建及管理「服務實例」（「服務供應項目」的實例化）和「服務連結」（「應用程式」與「服務實例」之間的關聯表示法，其中通常包含「應用程式」用來與「服務實例」進行通訊的認證）。提供有效的 meta 資料值將會在執行「要求」時建立成功的「REST API 回應」。

{{site.data.keyword.Bluemix_notm}} 使用 Open Service Broker API (OSB) `2.12 版`規格。閱讀並熟悉 [Open Broker API 規格](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")，以及使用 Readme 檔作為指引以進一步瞭解。

當資源控制器接收到佈建資源要求時，會呼叫您的 OSB 來驗證服務類型、供應項目、方案及地區可用性。資源控制器也會驗證與客戶帳戶相關聯之方案的可見性。{{site.data.keyword.Bluemix_notm}} 提供分配管理系統範例以及延伸 OSB 規格的 API 文件。在您逐步閱讀詳細的整合式計費上線開發步驟時，可以找到更多有關開發及管理分配管理系統的詳細資料。

## {{site.data.keyword.Bluemix_notm}} 計量服務

如果服務提供計量方案，則會根據 {{site.data.keyword.Bluemix_notm}} 使用者所使用的資源數量來向他們收費。例如，可能會根據使用資料庫服務之 {{site.data.keyword.Bluemix_notm}} 使用者的應用程式所使用的儲存空間數量，向這些使用者收費。必須進行用量提交，才能將用量轉換為可計費的記錄。

提供計量方案的所有整合式計費服務都必須使用 {{site.data.keyword.Bluemix_notm}} 計量服務來報告用量資料。

**附註：**如果您提供計量方案，則需要使用計量服務 API 自動執行每小時用量提交。

如需計量的相關資訊，請參閱：[計量整合](/docs/third-party/metering.html#meteringintera)。如需提交計量用量的相關資訊，請參閱：[提交計量方案的用量](/docs/third-party/submitusage.html#submitusage)

## 佈建情境：組合在一起

現在，讓我們將所有先前所述的概念組合在一起，並查看如何使用 {{site.data.keyword.Bluemix_notm}} 平台來建立服務實例的範例。

![佈建情境](images/flow-am.svg "平台如何處理服務實例建立")

當使用者想要建立服務實例時，可以使用下列兩種方式之一來起始它：
* **CLI**：使用 `ibmcloud cli [ ibmcloud resource service-instance-create NAME SERVICE_NAME SERVICE_PLAN_NAME LOCATION ]`
* **{{site.data.keyword.Bluemix_notm}} 主控台**：使用者可以選取服務、規劃，並使用**建立**作業。

{{site.data.keyword.Bluemix_notm}} 平台會驗證使用者是否有權使用 {{site.data.keyword.Bluemix_notm}} IAM 來建立服務實例。進行這項驗證之後，即會呼叫服務分配管理系統的佈建端點 (PUT /v2/resource_instances/:resource_instance_id)。進行佈建時，必須符合下列規則：
* {{site.data.keyword.Bluemix_notm}} 環境定義包括在環境定義變數中
* `X-Broker-API-Originating-Identity` 將具有已起始要求之使用者的 IBM IAM ID
* parameters 區段將包括所要求的位置（以及服務所需的其他參數）。

範例佈建要求：

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

### 瞭解 {{site.data.keyword.Bluemix_notm}} `context` 參數

在前一個範例中，您可以看到 `context` 參數中所傳回的 meta 資料。{{site.data.keyword.Bluemix_notm}} 的佈建環境定義會傳回下列內容：

* **platform**：將平台識別為 "ibmcloud"

* **"account_id"**：傳回 {{site.data.keyword.Bluemix_notm}} 中將佈建服務實例的帳戶 ID。

* **crn**：當客戶在 {{site.data.keyword.Bluemix_notm}} 中佈建服務時，會建立服務實例，並透過其「{{site.data.keyword.Bluemix_notm}} 資源名稱 (CRN)」識別此實例。在與 {{site.data.keyword.Bluemix_notm}} 互動的所有層面中都會使用 CRN，包括佈建、連結（建立認證和端點）、計量、儀表板顯示及存取控制。從供應項目提供者觀點來看，CRN 大部分可以視為要與 {{site.data.keyword.Bluemix_notm}} API 搭配使用的不透明字串。也可以使用下列結構來分解它：

   ```
   crn:version:cname:ctype:service-name:location:scope:service-instance:resource-type:resource
   ```

   在佈建範例中，我們看到 `compose-redis` 服務 CRN 是：

   ```
   crn:v1:bluemix:public:compose-redis:us-south:a/46aa677e-e83f-4d17-a2b6-5b752564477c:416d769b-682d-4833-8bd7-5ef8778e5b52::
   ```

   在此範例中，此 `compose-redis` 實例是 ID 為 `46aa677e-e83f-4d17-a2b6-5b752564477c` 之 {{site.data.keyword.Bluemix_notm}} 帳戶的一部分、實例的唯一 ID 是 `416d769b-682d-4833-8bd7-5ef8778e5b52`，而實例是在公用 {{site.data.keyword.Bluemix_notm}} 的 `us-south` 地區中進行管理。

* **resource_group_crn**：傳回包含服務實例的資源群組。如需詳細資料，請參閱[管理資源群組](/docs/resources/resourcegroups.html)。

   **附註**：供應項目提供者不應該與 `resource_group_crn` 有關，但在極獨特的情況下除外。使用該欄位之前，請向 IBM 業務代表諮詢您的使用案例。

