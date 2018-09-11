---

copyright:
  years: 2018
lastupdated: "2018-07-20"

---

{:right: .ph data-hd-position='right'}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# 端對端核對清單
{: #checklist}

使用下列核對清單來追蹤定義、開發及發佈整合式計費服務所需的所有作業。{:shortdesc}

## 定義服務
{: #define}

| 作業 | 子作業   |說明| 環境        |
|------| ----------| ------------|-----|
|瞭解 {{site.data.keyword.Bluemix}} 平台。| ☐ 我瞭解佈建層、{{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM)、型錄、Open Service Broker 及計量服務如何全部一起運作。|與 {{site.data.keyword.Bluemix_notm}} 轉介服務不同，整合式計費服務使用 {{site.data.keyword.Bluemix_notm}} 平台來建立、連結及刪除服務實例，以及收取其費用。[瞭解](/docs/third-party/platform.html#what-is-the-ibm-cloud-platform-)構成平台的重要元件，以便快速開始開發。| 文件 |
| 在 {{site.data.keyword.Bluemix_notm}} Provider Workbench 登錄您的供應項目。| ☐ 我已完成內容作業。<br><br>☐ 已收到核准，可將我的供應項目發佈為整合式計費服務。<br><br> ☐ 我已收到具有文件 URL 值的電子郵件。<br><br> | 您的第一步是在 Provider Workbench 登錄供應項目。如需相關詳細資料，請參閱[入門指導教學](/docs/third-party/index.html#get-started)。| Provider Workbench |
| 發佈 {{site.data.keyword.Bluemix_notm}} 文件。| ☐ 我已在 Provider Workbench 開始指引作業。<br><br>☐ 我已收到 `Documentation URL`。<br><br> ☐ 我已順利發佈我的文件。<br><br> | 我們知道您自己網站上所管理的協力廠商文件很棒。不過，既然您將在 {{site.data.keyword.Bluemix_notm}} 中提供整合式計費服務，您需要提供針對您的 {{site.data.keyword.Bluemix_notm}} 整合式計費經驗進行自訂的文件。如需詳細資料，請參閱[建立文件](/docs/third-party/cis1-docs-marketing.html#docs)。| Provider Workbench |
|發佈行銷公告。| ☐ 我已在 Provider Workbench 開始行銷作業。<br><br>  ☐ 我已順利發佈我的行銷公告。<br><br>  |建立行銷文宣，以透過 {{site.data.keyword.Bluemix_notm}} 新聞信件及社交媒體頻道來發表服務可用性。如需詳細資料，請參閱[建立行銷公告](/docs/third-party/cis1-docs-marketing.html#announcement)。| Provider Workbench |
| 在資源管理主控台中登錄供應項目。 | ☐ 我已定義唯一且有意義的 `service-name` 作為我的資源名稱。<br><br>  ☐ 我已順利驗證在資源管理主控台中有一筆記錄。<br><br>  |您可以使用資源管理主控台來建立唯一的供應項目。如需詳細資料，請參閱[登錄供應項目的步驟](/docs/third-party/cis2-rmc-define.html#register)。| 資源管理主控台 |
| 完成資源管理主控台中的「供應項目」頁面。 | ☐ 使用在 Provider Workbench 供應項目電子郵件中提供的值，我已正確地設定文件 URL 和指示 URL。<br><br>  ☐ 我已提供指向獨特服務條款頁面且不含計費或付款條款的 URL。<br><br>  ☐ 我瞭解並正確地指定是否啟用**支援方案變更？**。☐ 我瞭解並正確地指定我的服務是否為可連結。|在顯示於 {{site.data.keyword.Bluemix_notm}} 磚的資源管理主控台中，提供型錄 meta 資料。如需詳細資料，請參閱[輸入供應項目 meta 資料的步驟](/docs/third-party/cis2-rmc-define.html#offering-metadata)。| 資源管理主控台 |
| 完成資源管理主控台中的「存取管理」頁面。 | ☐ 我已順利啟用 IAM。<br><br>  ☐ 我已儲存為我所建立的單次產生 IAM API 金鑰，而且我瞭解 API 金鑰未儲存在資源管理主控台中，因此稍後無法擷取該 API 金鑰。<br><br> ☐ 我瞭解除非開發及管理 Open Service Broker，然後衍生我的重新導向 URI，否則無法完成「存取管理」頁面。<br><br> ☐ 管理我的 Open Service Broker 之後，我已回到 IAM 頁面。| 在資源管理主控台中，向 {{site.data.keyword.Bluemix_notm}} IAM 登錄供應項目。IAM 可讓您安全地鑑別兩個平台服務的使用者，並跨 {{site.data.keyword.Bluemix_notm}} 平台一致地控制資源的存取如需詳細資料，請參閱[向 IAM 登錄的步驟](/docs/third-party/cis2-rmc-define.html#reg-iam)。| 資源管理主控台 |
| 在資源管理主控台中開發一個以上的定價方案。 | ☐ 我已提供具有唯一名稱的免費方案。<br><br>  ☐（選用）我與 IBM 業務代表一起定義付費方案（訂閱或計量），而且我瞭解為了建立計量方案，我必須移除預設訂閱方案。<br><br> ☐（選用）我瞭解我必須管理及開發自動化的每小時用量提交。| 如何對您的服務收費？資源管理主控台提供免費或付費的方案。如需詳細資料，請參閱[開發定價方案的步驟](/docs/third-party/cis2-rmc-define.html#develop-a-pricing-plan-rmc-pricing-page-)。| 資源管理主控台 |
| 從資源管理主控台中匯出型錄 meta 資料。 | ☐ 我瞭解在資源管理主控台「供應項目」及「定價」頁面中提供的一些 meta 資料，必須匯出及提供於我的 Open Service Broker 中。<br><br>  ☐ 我已從**部署**頁面取得我的 `catalog.json` 檔案，並準備好將服務陣列對映至我的 Open Service Broker 中的 meta 資料。<br><br> | 既然您已在資源管理主控台內定義服務，就可以下載 `catalog.json` 檔案，並使用它來通知開發您的 Open Service Broker。如需詳細資料，請參閱[匯出 meta 資料的步驟](/docs/third-party/cis2-rmc-define.html#export metadata)。| 資源管理主控台 |
{: caption="表 1. 定義整合式計費服務" caption-side="top"}

## 開發服務
{: #develop}

| 作業 | 子作業   |說明| 環境        |
|------| ----------| ------------|-----|
|瞭解 Open Service Broker 規格 2.12 版。|☐ 我已閱讀 Open Service Broker 規格，並瞭解我必須自行開發 Open Service Broker。<br><br>  |  服務分配管理系統可管理服務的生命週期。{{site.data.keyword.Bluemix_notm}} 平台會與 Open Service Broker 互動，以佈建及管理服務實例和服務連結。如需詳細資料，請參閱[開發及管理服務分配管理系統](/docs/third-party/cis3-broker.html#step3-osb)。| 文件 |
|檢視 {{site.data.keyword.Bluemix_notm}} 分配管理系統範例。| ☐ 我已複製儲存庫、瀏覽分配管理系統範例，並準備好使用這些範例來開始開發。<br><br>  |  [https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") | 程式碼範例 |
|檢視 {{site.data.keyword.Bluemix_notm}} Open Service Broker API 文件。| ☐ 我瞭解我的 Open Service Broker 中的程式碼必須支援數個必要端點。<br><br>  ☐ 我瞭解如果服務可以連結至 {{site.data.keyword.Bluemix_notm}} 中的應用程式，則必須能夠將 API 端點及認證傳回給服務使用者。<br><br> ☐ 我瞭解 {{site.data.keyword.Bluemix_notm}} 已定義可容許停用及重新啟用服務實例的延伸 API 端點。|  {{site.data.keyword.Bluemix_notm}} Open Service Broker 延伸 Open Service Broker 2.12 規格。[瞭解](/docs/third-party/cis3-broker.html#docs)您的服務分配管理系統必須使用的必要端點。 | 文件 |
| 使用您的型錄 meta 資料開始開發服務分配管理系統。 | ☐ 我瞭解在資源管理主控台中提供的一些 meta 資料，必須匯出及提供於我的 Open Service Broker 中。<br><br>  ☐ 我已將 `catalog.json` 檔案中列出的必要 GUID 及其他必要值，新增至我的範例 Open Service Broker 中的服務陣列。| 從資源管理主控台下載 `catalog.json` 檔案之後，您可以使用它來通知開發您的 Open Service Broker。如需詳細資料，請參閱[使用匯出的 meta 資料來引導開發的步驟](/docs/third-party/cis3-broker.html#use-metadata)。| 開發環境及文件 |
|管理 Open Service Broker。| ☐ 我瞭解服務分配管理系統的受管理位置必須遵循「傳輸層安全 (TLS)」通訊協定 1.2 版。<br><br> | 您的服務分配管理系統必須被管理來當作可回應 REST API 呼叫之應用程式的一部分。您的受管理位置必須符合 {{site.data.keyword.Bluemix_notm}} 安全準則。如需詳細資料，請參閱[管理服務分配管理系統的步驟](/docs/third-party/cis3-broker.html#host)。| 開發環境及文件 |
| 測試受管理 Open Service Broker。| ☐ 我已對受管理服務分配管理系統執行 curl 指令，來驗證我的服務分配管理系統所支援的每一個 API 端點。 <br><br> |對您要啟用的不同端點執行 curl 指令，來驗證服務分配管理系統。如需詳細資料，請參閱[測試服務分配管理系統的步驟](/docs/third-party/cis3-broker.html#test)。| 開發環境及文件 |
| 衍生並設定 IAM 重新導向 URI。 | ☐ 我已使用 Open Service Broker 受管理位置及部分鑑別資訊，順利衍生 IAM 重新導向 URI。<br><br> ☐ 我已藉由指定重新導向 URI 並正確地設定用戶端 ID，順利完成資源管理主控台「存取管理」頁面。<br><br> |當您在資源管理主控台中定義服務時，會產生用戶端 ID，但請注意，您在當時可能沒有重新導向 URI。這表示用戶端 ID 是設為 `false`。在您使用重新導向 URI 回到資源管理主控台之前，不會有真正的用戶端 ID。如需詳細資料，請參閱[衍生重新導向 URI 的步驟](/docs/third-party/cis5-iam.html#redirect-uri)。| 開發環境及資源管理主控台 |
|開發 Open Authorization (OAuth) 流程以進行鑑別。| ☐ 我瞭解 IAM 支援 Open ID Connect (OIDC)。<br><br> ☐ 我已發現 IAM 區域端點，並已順利將使用者從 `dashboard_url` 重新導向至已組合的重新導向 URI，而且我在回應中儲存所傳回的使用者 `access_token`，以便在鑑別期間使用。<br><br> | 必須正確地鑑別造訪服務儀表板的使用者。使用 IAM 開發 OAuth 記號型鑑別及授權。如需詳細資料，請參閱[開發 OAuth 流程的步驟](/docs/third-party/cis5-iam.html#oauth)。| 開發環境及文件 |
|驗證使用者授權。| ☐ 我可以取得 API 金鑰的存取記號。<br><br> ☐ 我可以驗證使用者對服務實例的授權。<br><br> | 開發 OAuth 流程以進行鑑別之後，您必須驗證已正確地授權使用者，確定您服務的使用者可以存取您的服務儀表板。如需詳細資料，請參閱[驗證的步驟](/docs/third-party/cis5-iam.html#validate)。| 開發環境及文件 |
{: caption="表 2. 開發整合式計費服務" caption-side="top"}

## 發佈及測試服務
{: #pubtest}

| 作業 | 子作業   |說明| 環境        |
|------| ----------| ------------|-----|
| 以受限可見性模式發佈服務。| ☐ 我已在資源管理主控台中順利登錄受管理的 Open Service Broker。<br><br> ☐ 我已順利建立新的部署，並將我的供應項目發佈至一個以上的地區。<br><br> |  既然您的受管理服務分配管理系統符合 Open Service Broker 規格，您可以將服務發佈至 {{site.data.keyword.Bluemix_notm}} 型錄。如需詳細資料，請參閱[發佈服務的步驟](/docs/third-party/cis4-rmc-publish.html#publish)。| 資源管理主控台 |
| 測試供應項目。| ☐ 我可以在型錄中看到我的服務。<br><br> ☐ 我已從服務實例儀表板驗證鑑別。<br><br> ☐ 我已驗證我的服務正確地顯示在型錄中。<br><br> ☐ 我可以選取方案，並建立服務實例。<br><br> ☐ 我可以刪除服務實例。<br><br> ☐ 我可以將我的服務連接至另一個應用程式。<br><br> ☐ 我可以中斷服務的連線，並刪除連線。<br><br>  ☐ 我可以產生服務金鑰及刪除該服務金鑰。<br><br> ☐ 我已與 IBM 業務代表合作，驗證我的供應項目正確地支援啟用及停用端點。<br><br> ☐ 因為我的供應項目具有方案，所以我已順利測試用量提交。|  既然您的受管理服務分配管理系統符合 Open Service Broker 規格，您可以將服務發佈至 {{site.data.keyword.Bluemix_notm}} 型錄。如需詳細資料，請參閱[測試服務的步驟](/docs/third-party/cis4-rmc-publish.html#test)。| {{site.data.keyword.Bluemix_notm}} 主控台 |
{: caption="表 3. 發佈及測試整合式計費服務" caption-side="top"}

