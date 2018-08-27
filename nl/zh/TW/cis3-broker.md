---


copyright:
  years: 2018
lastupdated: "2018-08-21"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 步驟 3. 開發及管理服務分配管理系統

您將使用從資源管理主控台匯出的 meta 資料，以您選擇的程式設計語言建置一個以上的新服務分配管理系統。

服務分配管理系統可管理服務的生命週期。{{site.data.keyword.Bluemix_notm}} 平台會與服務分配管理系統互動，以佈建及管理服務實例（服務供應項目的實例化）和服務連結（應用程式與服務實例之間的關聯表示法，其中通常包含應用程式用來與服務實例進行通訊的認證）。提供有效的 meta 資料值將會在執行「要求」時建立成功的「RESTful API 回應」。

您可以使用下列項目的組合來開始建置分配管理系統：從資源管理主控台匯出的 meta 資料、公用 {{site.data.keyword.Bluemix_notm}} 服務分配管理系統範例，以及 Resource Broker API 文件。若要開發分配管理系統，您將：

1. 檢視平台佈建情境。
2. 閱讀 OSB 規格。
2. 查看 {{site.data.keyword.Bluemix_notm}} 分配管理系統範例。
3. 使用 Resource Broker API 文件來瞭解 REST API 端點邏輯。
4. 使用您從資源管理主控台匯出的 meta 資料來通知開發。
5. 檢視 {{site.data.keyword.Bluemix_notm}} 平台提供的分配管理系統資訊。
6. 閱讀其他建議以便最佳化開發。
7. 管理分配管理系統。
8. 測試分配管理系統。

## 開始之前

此步驟假設您已獲准提供整合式計費服務。如果您尚未在 Provider Workbench 中完成起始登錄及核准，則請參閱[入門指導教學](/docs/third-party/index.md)。
{: tip}

確定您已開始步驟 1 並完成步驟 2：
1. [編寫服務文件及行銷公告](/docs/third-party/cis1-docs-marketing.html)。
2. [在資源管理主控台中定義供應項目](/docs/third-party/cis2-rmc-define.html)。


## 檢視 {{site.data.keyword.Bluemix_notm}} 平台佈建情境

您將會開發 Open Service Broker，以與 {{site.data.keyword.Bluemix_notm}} 平台搭配使用。請參閱[佈建情境](/docs/third-party/platform.html#provisioning-scenario-pulling-it-all-together)，以瞭解如何建立資源。

## 熟悉 OSB 規格

{{site.data.keyword.Bluemix_notm}} 使用 Open Service Broker API (OSB) `2.12 版`規格。閱讀並熟悉 [Open Broker API 規格](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")，以及使用 Readme 檔作為指引以進一步瞭解。

## 檢視 {{site.data.keyword.Bluemix_notm}} 分配管理系統範例

[https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")

**附註：**並非所有語言都有範例表示。例如，如果您需要範例 Python 分配管理系統，應該可以搜尋 Google，找到 Cloud Foundry 範例。您可能需要調整此範例，以符合 OSB 需求。


## 檢視 {{site.data.keyword.Bluemix_notm}} Open Service Broker API 文件

應該先瞭解 [{{site.data.keyword.Bluemix_notm}} Open Service Broker API](https://console.bluemix.net/apidocs/resource-controller){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 再開發服務分配管理系統。熟悉 Broker API，以及它如何與一個以上的分配管理系統互動。

{{site.data.keyword.Bluemix_notm}} Open Service Broker 延伸了 Open Service Broker 2.12 規格。
{: tip}

### 所有服務分配管理系統的必要端點邏輯

服務分配管理系統必須提供 REST API 所使用的一組標準 meta 資料值，而 {{site.data.keyword.Bluemix_notm}} 分配管理系統必須包含下列 REST API 端點/路徑的邏輯：

<dl>
  <dt>型錄 (GET)</dt>
  <dd>傳回分配管理系統中所含的型錄 meta 資料。有許多其他未傳回的型錄 meta 資料值 - 這些值只會在資源管理主控台內新增並儲存在「{{site.data.keyword.Bluemix_notm}} 型錄」內。</dd>
  <dt>資源實例 (PUT)</dt>
  <dd>佈建服務實例</dd>
  <dt>資源實例 (DELETE)</dt>
  <dd>取消佈建服務實例。</dd>
  <dt>資源實例 (PATCH)</dt>
  <dd>更新服務實例。</dd>
</dl>

**型錄 (GET) 的附註**：此端點定義分配管理系統與分配管理系統所支援服務及方案之 {{site.data.keyword.Bluemix_notm}} 平台間的合約。此端點會傳回分配管理系統內所儲存的型錄 meta 資料。這些值定義服務與 {{site.data.keyword.Bluemix_notm}} 平台之間的最低佈建合約。佈建不需要的所有其他型錄 meta 資料，都會儲存在 {{site.data.keyword.Bluemix_notm}} 型錄內，而且用來呈現儀表板的任何型錄顯示值更新（例如鏈結、圖示及 i18n 已翻譯 meta 資料）都應該在資源管理主控台中進行更新，而不是在分配管理系統中進行管理。您分配管理系統中所儲存的 meta 資料，都不會顯示在 {{site.data.keyword.Bluemix_notm}} 主控台或 {{site.data.keyword.Bluemix_notm}} CLI 中；主控台及 CLI 將會傳回資源管理主控台內所設定並儲存在 {{site.data.keyword.Bluemix_notm}} 型錄中的內容。這些是型錄 (GET) 應該傳回的最小必要值：

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

### 可連結服務的必要端點邏輯

如果服務可以連結至 {{site.data.keyword.Bluemix_notm}} 中的應用程式，則必須能夠將 API 端點及認證傳回給服務消費者。可連結服務必須使用 Open Service Broker 規格中的可連結作業，並實作下列端點/路徑：

<dl>
  <dt>連結及認證 (PUT)</dt>
  <dd>將服務實例連結至應用程式。</dd>
  <dt>連結及認證 (DEL)</dt>
  <dd>將您的服務實例與應用程式取消連結。</dd>
</dl>

### 必要 {{site.data.keyword.Bluemix_notm}} 延伸端點

OSB 規格*不* 支援已停用但尚未刪除的實例狀態。為了讓 {{site.data.keyword.Bluemix_notm}} 支援可能會遇到計費失誤或其他導致帳戶暫停（但尚未取消）之狀況的客戶，{{site.data.keyword.Bluemix_notm}} 定義了可容許停用及重新啟用服務實例的延伸 API 端點。下列端點延伸為**必要**：

<dl>
  <dt>啟用及停用實例 (GET)</dt>
  <dd>狀態 - 傳回服務實例的狀態。</dd>
  <dt>啟用及停用實例 (PUT)</dt>
  <dd>可讓您啟用或停用服務實例。</dd>
</dl>

**附註**：呼叫停用端點時，服務提供者必須負責停用對服務實例的存取權，並在呼叫啟用端點時重新啟用該存取權。

## 瞭解如何使用匯出的 meta 資料來引導分配管理系統開發

您從資源管理主控台匯出的 meta 資料可以用來作為自行開發分配管理系統的指引。佈建服務時並不需要您在資源管理主控台中輸入的所有值。您從資源管理主控台匯出的 meta 資料會定義服務與 {{site.data.keyword.Bluemix_notm}} 平台之間的最低佈建合約。您匯出的 json 應該提供下列值：

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


您的 OSB 服務陣列必須與您新增至資源管理主控台的供應項目 meta 資料完全相同。若要確保 OSB 與資源管理主控台之間有一對一的同位，您必須比較從資源管理主控台下載之 `catalog.json` 中的服務陣列，與分配管理系統中的實際服務陣列。所有服務及方案 ID 和名稱都必須相符。
{: tip}

## {{site.data.keyword.Bluemix_notm}} 平台提供的分配管理系統資訊

您的服務分配管理系統將會從 {{site.data.keyword.Bluemix_notm}} 平台收到下列資訊：

### X-Broker-API-Originating-Identity

**使用者身分標頭**將會透過產生身分標頭的 API 提供。此要求標頭將包含使用者的「{{site.data.keyword.Bluemix_notm}} IAM 身分」。「IAM 身分」將會以 base64 編碼。{{site.data.keyword.Bluemix_notm}} 支援單一鑑別領域：`IBMid`。`IBMid` 領域使用「IBM ID 唯一 ID (IUI)」來識別使用者在 {{site.data.keyword.Bluemix_notm}} 中的身分。此 IUI 對服務提供者來說是不可探知的字串。

範例：

```
X-Broker-API-Originating-Identity: ibmcloud eyJpYW1faWQiOiJJQk1pZC01MEdOUjcxN1lFIn0=
Decoded:
{"iam_id":"IBMid-50GNR717YE"}
```

### API 標頭版本

**API 版本標頭**將會是 [2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。例如：`X-Broker-Api-Version: 2.12`。

### 資源實例 (PUT) body.context 及資源實例 (PATCH) body.context

`PUT /v2/service_instances/:resource_instance_id` 及 `PATCH /v2/service_instances/:resource_instance_id` 將在 **body.context** 內收到下列值：`{ "platform": "ibmcloud", "account_id": "tracys-account-id", "crn": "resource-instance-crn" }`。

## 其他分配管理系統建議

### 使用非同步與同步作業的建議

OSB API 支援同步及非同步作業模式。如果您的作業將需要不到 10 秒的時間，建議使用同步回應。否則，您應該使用非同步作業模式。關於這點的資訊包含在 OSB 規格中。

如果您的非同步作業在嘗試佈建實例時需要不到 10 秒的時間，則平台會逾時。
{: tip}

### 跨位置管理分配管理系統的建議

使用者必須瞭解其雲端服務的位置，查看是否會有延遲、可用性及資料常駐等問題。

在 {{site.data.keyword.Bluemix_notm}} 上佈建服務實例時，使用者將提供的其中一個必要參數，就是他們想要佈建該服務實例的位置。部分服務可能支援在多個位置中進行佈建。例如，資料庫服務可能支援在所有 {{site.data.keyword.Bluemix_notm}} 地區中佈建，或是可能支援子集。

如果協力廠商 API 型服務是在另一個雲端中實作並公開到 {{site.data.keyword.Bluemix_notm}}，則位置應該指出服務在其他雲端中的位置。

在 {{site.data.keyword.Bluemix_notm}} 上線時，您必須實作至少一個 OSB 分配管理系統，但您可以選擇根據部署策略及服務要支援的位置，而有多個分配管理系統。在資源管理主控台工具內，您已建立服務/方案/位置值組與將處理該值組作業之分配管理系統間的對映。一般選項會是定義單一分配管理系統來處理服務的所有位置，或定義每個位置的分配管理系統；此選項取決於服務提供者。

如需可用位置的清單，請參閱 [IBM 全球型錄位置](https://resource-catalog.bluemix.net/search?q=kind:geography){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。如果您的服務需要在「全球型錄」中定義其他位置，請諮詢 {{site.data.keyword.Bluemix_notm}} 上線團隊。


## 管理分配管理系統

您的分配管理系統必須被管理來當作可回應 REST API 呼叫之應用程式的一部分。您的受管理位置必須符合 {{site.data.keyword.Bluemix_notm}} 安全準則。您可以在 {{site.data.keyword.Bluemix_notm}} 中管理，也可以在外部管理，只要可以從 {{site.data.keyword.Bluemix_notm}} 本身公開存取它即可。

若要在 IBM 外部管理分配管理系統，您必須確定符合下列安全準則：
- 必須遵循「傳輸層安全 (TLS)」通訊協定 1.2 版
- 必須在公用網際網路上可存取的有效 HTTPS 端點上管理

如果您要在 {{site.data.keyword.Bluemix_notm}} 中管理，則可以在下列位置找到使用 Containers (Kubernetes) 建立應用程式的相關資訊：[內部採用者 - 用量資訊](/docs/containers/cs_internal.html#cs_internal)。

您需要服務分配管理系統的受管理位置，才能完成下一步。移至下一步時，請備妥與您應用程式相關聯的 URL 及認證。
{: tip}

## 如何測試服務的分配管理系統

您應該對您要啟用的不同端點執行 curl 指令，來驗證分配管理系統。範例 ReadMe 提供對 OSB 端點進行 curl 處理的絕佳指引：https://github.com/IBM/sample-resource-service-brokers/blob/master/README.md

### 如何對服務的分配管理系統進行 curl 處理

下列範例用來測試您的分配管理系統 curl 回應：

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

## 後續步驟

您有一些重大技能！您剛剛建置並管理了符合 OSB 規格的服務分配管理系統。請參閱[步驟 4：開發鑑別流程](/docs/third-party/cis5-iam.html)。
