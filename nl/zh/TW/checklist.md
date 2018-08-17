---

copyright:
  years: 2018
lastupdated: "2018-07-02"

---

{:right: .ph data-hd-position='right'}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}

# 端對端核對清單
{: #checklist}

使用下列核對清單來追蹤定義、開發及發佈整合式計費服務所需的所有作業。

## 定義供應項目

| 作業 | 子作業   | 說明        | 環境        |
|------| ----------| ------------|-----|
| 瞭解 {{site.data.keyword.Bluemix_notm}} 平台。|☐ 我瞭解 {{site.data.keyword.Bluemix_notm}} 平台的佈建層、{{site.data.keyword.Bluemix_notm}} IAM、型錄、OSB 及計量服務如何全部一起運作。|與 {{site.data.keyword.Bluemix_notm}} 轉介服務不同，整合式計費服務使用 {{site.data.keyword.Bluemix_notm}} 平台來建立、連結及刪除服務實例，以及收取其費用。[瞭解](/docs/third-party/platform.html#what-is-the-ibm-cloud-platform-)構成平台的重要元件，以便快速開始開發！| 文件 |
| 在 PWB 中登錄 | ☐ 已完成 PWB 中的**內容作業** <br><br>☐ 我已取得核准，可將我的供應項目發佈為整合式計費服務 <br><br> ☐ 我已取得具有文件 URL 值的起始電子郵件 <br><br> | 您的第一步是向 {{site.data.keyword.Bluemix_notm}} PWB 登錄供應項目。如需完成這項作業的相關資訊，請參閱[入門指導教學](/docs/third-party/index.html#get-started)。| PWB |
| 編寫及發佈 {{site.data.keyword.Bluemix_notm}} 文件 |☐ 我已在 PWB 中開始**指引作業（文件）** <br><br>☐ 我已取得`文件 URL` <br><br> ☐ 我已順利發佈我的文件 <br><br> | 我們知道您自己網站上所管理的協力廠商文件很棒。不過，既然您將在 {{site.data.keyword.Bluemix_notm}} 中提供整合式計費服務，您需要提供針對您的 {{site.data.keyword.Bluemix_notm}} 整合式計費經驗進行自訂的文件。PWB 將引導您完成此作業，並協助您將文件發佈至 `https://console.bluemix.net/docs/`。如需完成這項作業的相關資訊，請參閱：[建立入門文件](/docs/third-party/cis1-docs-marketing.html#docs) | PWB |
| 編寫及發佈行銷公告 |☐ 我已在 PWB 中開始**行銷作業（公告）** <br><br>  ☐ 我已順利發佈我的公告 <br><br>  |建立行銷文宣，以透過 {{site.data.keyword.Bluemix_notm}} 新聞信件及社交媒體頻道來發表服務可用性。PWB 將引導您完成此作業。如需詳細資料，請參閱：[建立入門文件](/docs/third-party/cis1-docs-marketing.html#announcement) | PWB |
| 在資源管理主控台中登錄服務 | ☐ 我已定義唯一且有意義的 `service-name` 作為**資源名稱**<br><br>  ☐ 我已順利儲存並驗證在資源管理主控台中有一筆記錄<br><br>  | 資源管理主控台將協助您建立唯一的供應項目。遵循[指引](/docs/third-party/cis2-rmc-define.html#register-your-offering-by-using-the-resource-management-console-rmc-)來登錄供應項目。| 資源管理主控台 |
| 完成資源管理主控台中的**供應項目**頁面 |☐ 使用在 PWB 供應項目電子郵件中提供的值，我已正確地設定**文件 URL** 及**指示 URL** <br><br>  ☐ 我已提供**服務條款** URL，且該 URL 不是我公司的「服務條款」頁面，而是不含計費或付款條款的獨特「服務條款」頁面。<br><br>  ☐ 我瞭解並正確地指定是否啟用**支援方案變更？**。☐ 我瞭解並正確地指定我的服務是否為**可連結**。|在資源管理主控台中提供將顯示於 {{site.data.keyword.Bluemix_notm}} 磚中的型錄 meta 資料（包括「服務條款」這類的重要 URL），以及您供應項目的有意義詳細資料（例如資訊項目符號及其他項目）。遵循[指引](/docs/third-party/cis2-rmc-define.html#enter-your-offering-metadata-rmc-offering-page-)來設定供應項目的必要和建議型錄 meta 資料。| 資源管理主控台 |
| 完成資源管理主控台中的**存取管理**頁面 | ☐ 我已順利啟用 IAM<br><br>  ☐ 我已儲存資源管理主控台使用者介面為我所建立的單次產生 IAM API 金鑰，而且我瞭解 API 金鑰未儲存在資源管理主控台中，因此稍後無法擷取該 API 金鑰。<br><br> ☐ 我瞭解除非在稍後的步驟開發及管理 OSB，然後衍生我的重新導向 URI，否則無法完成「存取管理」頁面。<br><br> ☐ 建立並管理我的 OSB 之後，我已回到 IAM 頁面，然後按一下**新增重新導向 URI**，並新增衍生值，順利完成頁面。| 在資源管理主控台中，向 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 登錄供應項目。IAM 可讓您安全地鑑別兩個平台服務的使用者，並跨 {{site.data.keyword.Bluemix_notm}} 平台一致地控制資源的存取（您將會返回並啟用重新導向 URI）。遵循[指引](/docs/third-party/cis2-rmc-define.html#register-with-identity-and-access-management-rmc-iam-page-)來啟用您供應項目的起始存取管理。| 資源管理主控台 |
| 在資源管理主控台中開發一個以上的定價方案 | ☐ 我已提供具有唯一名稱的免費方案。<br><br>  ☐（選用）我與 IBM 業務代表一起定義付費方案（訂閱或計量），而且我瞭解為了建立計量方案，我必須移除預設訂閱方案。<br><br> ☐（選用）我瞭解計量方案需要我使用 {{site.data.keyword.Bluemix_notm}} 平台計量服務來管理及開發自動化的每小時用量提交。| 如何對您的供應項目收費？資源管理主控台提供免費或付費（訂閱及計量）方案。遵循[指引](/docs/third-party/cis2-rmc-define.html#develop-a-pricing-plan-rmc-pricing-page-)來定義供應項目的定價方案。| 資源管理主控台 |
| 從資源管理主控台中匯出型錄 meta 資料 | ☐ 我瞭解在資源管理主控台**供應項目**及**定價**頁面中提供的一些 meta 資料，必須匯出及提供於我的 OSB 中。藉由從資源管理主控台匯出值，即可對映資源管理主控台為我產生的重要 GUID（例如我的服務和方案 ID），並在我的 OSB 中提供它們，讓平台佈建層可以從我的`型錄 GET` 端點的回應中讀取此佈建合約。<br><br>  ☐ 我已從資源管理主控台**部署**頁面取得我的 `catalog.json` 檔案，並準備好將服務陣列對映至我的 OSB 中的 meta 資料。<br><br> | 既然您已在資源管理主控台內定義服務，就可以下載 catalog.json 檔案，並使用它來通知開發您的 Open Service Broker。catalog.json 包含必須在分配管理系統中管理的 meta 資料。這些值定義分配管理系統與分配管理系統所支援服務及方案之 IBM Cloud 平台間的合約。遵循[指引](/docs/third-party/cis2-rmc-define.html#export-your-metadata-as-json-rmc-deployments-page-)來匯出型錄 meta 資料。| 資源管理主控台 |
{: caption="表 1. 定義整合式計費供應項目" caption-side="top"}

## 開發供應項目

| 作業 | 子作業   | 說明        | 環境        |
|------| ----------| ------------|-----|
| 瞭解 Open Service Broker (OSB) 規格 2.12 版 |☐ 我已閱讀 OSB 規格，並瞭解我必須自行開發 OSB。<br><br>  |  服務分配管理系統可管理服務的生命週期。{{site.data.keyword.Bluemix_notm}} 平台會與 Open Service Broker 互動，以佈建及管理服務實例（服務供應項目的實例化）和服務連結（應用程式與服務實例之間的關聯表示法，其中通常包含應用程式用來與服務實例進行通訊的認證）。[瞭解](/docs/third-party/cis3-broker.html#become-familiar-with-the-osb-specification) 2.12 版規格。| 文件 |
| 檢視 {{site.data.keyword.Bluemix_notm}} 分配管理系統範例 | ☐ 我已複製儲存庫、查看分配管理系統範例，並準備好使用這些範例來開始開發。<br><br>  |  [https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") | 程式碼範例 |
| 檢視 {{site.data.keyword.Bluemix_notm}} Open Service Broker API 文件 | ☐ 我瞭解我的 OSB 中的程式碼必須支援數個必要端點。<br><br>  ☐ 我瞭解如果服務可以連結至 {{site.data.keyword.Bluemix_notm}} 中的應用程式，則必須能夠將 API 端點及認證傳回給服務消費者。<br><br> ☐ 我瞭解 {{site.data.keyword.Bluemix_notm}} 已定義可容許停用及重新啟用服務實例的延伸 API 端點。我必須延伸我的 OSB，並定義**啟用及停用實例（GET 和 PUT）** |  {{site.data.keyword.Bluemix_notm}} Open Service Broker 延伸 Open Service Broker 2.12 規格。[瞭解](/docs/third-party/cis3-broker.html#view-our-resource-broker-api-documentation)您的分配管理系統必須使用的必要端點 | 文件 |
| 使用您的型錄 meta 資料開始開發分配管理系統 | ☐ 我瞭解在資源管理主控台**供應項目**及**定價**頁面中提供的一些 meta 資料，必須匯出及提供於我的 OSB 中。從資源管理主控台匯出值，即可對映資源管理主控台為我產生的重要 GUID（例如我的服務和方案 ID），並在我的 OSB 中提供它們，讓平台佈建層可以從我的`型錄 GET` 端點的回應中讀取此佈建合約。<br><br>  ☐ 我已將 `catalog.json` 檔案中列出的必要 GUID 及其他必要值，新增至我的範例 OSB 中的服務陣列。| 從資源管理主控台下載 `catalog.json` 檔案之後，您可以使用它來通知開發您的 Open Service Broker。catalog.json 包含必須在分配管理系統中管理的 meta 資料。這些值定義分配管理系統與分配管理系統所支援服務及方案之 IBM Cloud 平台間的佈建合約。遵循[指引](/docs/third-party/cis3-broker.html#learn-how-to-use-the-exported-metadata-to-guide-your-broker-development)，將您匯出的型錄 meta 資料新增至您的 OSB。| 開發環境及文件 |
| 管理您的 OSB | ☐ 我瞭解分配管理系統的受管理位置必須遵循「傳輸層安全 (TLS)」通訊協定 1.2 版。此外，必須在公用網際網路上可存取的有效 HTTPS 端點上，管理我的分配管理系統。<br><br> | 您的分配管理系統必須被管理來當作可回應 REST API 呼叫之應用程式的一部分。您的受管理位置必須符合 IBM Cloud 安全準則。遵循[指引](/docs/third-party/cis3-broker.html#host-your-brokers)來管理分配管理系統。| 開發環境及文件 |
| 測試受管理 OSB | ☐ 我已對受管理分配管理系統執行 curl 指令並驗證回應，來驗證我的分配管理系統所支援的每一個 API 端點 <br><br> |您應該對您要啟用的不同端點執行 curl 指令，來驗證分配管理系統。遵循[指引](/docs/third-party/cis3-broker.html#how-to-test-your-service-s-broker)來管理分配管理系統。| 開發環境及文件 |
| 衍生並設定 IAM 重新導向 URI | ☐ 我已使用 OSB 受管理位置及部分鑑別資訊，順利衍生 IAM 重新導向 URL。<br><br> ☐ 我已指定**重新導向 URI**，並正確地設定「用戶端 ID」，順利完成資源管理主控台**存取管理**頁面。<br><br> |當您在資源管理主控台中定義服務時，已產生「用戶端 ID」，但請注意，您在當時可能沒有「重新導向 URI」。這表示 IAM 已建立設為 `false` 的「用戶端 ID」。在您使用**重新導向 URI** 回到資源管理主控台之前，不會有真正的「用戶端 ID」。遵循[指引](/docs/third-party/cis5-iam.html#derive-your-iam-redirect-uri-resource-management-console-iam-page-)來衍生並設定 IAM 重新導向 URI。| 開發環境及資源管理主控台 |
| 開發 OAuth 流程以進行鑑別 | ☐ 我瞭解 IAM 支援 Open ID Connect (OIDC)。<br><br> ☐ 我已發現 IAM 區域端點，並已順利將使用者從 `dashboard_url` 重新導向至已組合的重新導向 URI，而且我在回應中儲存所傳回的使用者 `access_token`，以便在鑑別期間使用。<br><br> | 必須正確地鑑別造訪服務儀表板的使用者。使用 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 開發 Open Authorization 記號型鑑別及授權。遵循[指引](/docs/third-party/cis5-iam.html#oauth)來開發 OAuth 流程以進行鑑別。| 開發環境及文件 |
| 驗證使用者授權 | ☐ 我可以與 IAM 通訊來取得 API 金鑰的存取記號 <br><br> ☐ 我可以驗證使用者的服務實例授權 (/v2/authz POST)。<br><br> | 開發 OAuth 流程以進行鑑別之後，您必須驗證將正確地授權使用者，確定您服務的使用者可以存取您的服務儀表板。遵循[指引](/docs/third-party/cis5-iam.html#validate)來驗證使用者授權。| 開發環境及文件 |
{: caption="表 2. 開發整合式計費供應項目" caption-side="top"}

## 發佈及測試供應項目

| 作業 | 子作業   | 說明        | 環境        |
|------| ----------| ------------|-----|
| 以受限可見性模式發佈供應項目 | ☐ 我已在資源管理主控台**部署**頁面中順利登錄受管理 OSB。<br><br> ☐ 我已在資源管理主控台**部署**頁面中順利建立新的部署，並將我的供應項目發佈至一個以上的地區。<br><br> |  既然您的一個以上受管理分配管理系統符合 OSB 規格，就可以回到資源管理主控台，以將服務發佈至 {{site.data.keyword.Bluemix_notm}} 型錄。遵循[指引](/docs/third-party/cis4-rmc-publish.html#publish-your-service-to-ibm-cloud)以受限可見性模式發佈供應項目。| 資源管理主控台 |
| 測試供應項目 |☐ 使用我的白名單帳戶登入時，我可以在 https://console.bluemix.net 型錄中看到我的服務。<br><br> ☐ 我已順利從服務實例儀表板驗證鑑別。<br><br> ☐ 我已順利驗證我的供應項目正確地顯示在型錄中。<br><br> ☐ 我已順利驗證佈建有效；我可以選擇方案，並建立服務實例。<br><br> ☐ 我已順利驗證取消佈建有效；我可以刪除服務實例。<br><br> ☐ 我已順利驗證連結有效；我可以按一下**連線**，並將我的服務連接至另一個應用程式。<br><br> ☐ 我已順利驗證取消連結有效；我可以中斷服務的連線，並刪除連線。<br><br>  ☐ 我已順利驗證「建立服務金鑰」及「刪除服務金鑰」有效；我可以按一下**認證**、產生服務金鑰，然後刪除該服務金鑰。<br><br> ☐ 我已與 IBM 業務代表合作，驗證我的供應項目正確地支援啟用及停用端點。<br><br> ☐ 因為我的供應項目具有計量方案，所以我已順利測試用量提交，方法是對用量 API 進行 curl 處理並根據用量正確地傳回正確的定價，以及啟用用量的自動化每小時提交，並且支援佈建我的服務實例的所有使用者。| 既然您的一個以上受管理分配管理系統符合 OSB 規格，就可以回到資源管理主控台，以將服務發佈至 {{site.data.keyword.Bluemix_notm}} 型錄。遵循[指引](/docs/third-party/cis4-rmc-publish.html#test-your-deployed-offering)來測試已部署的服務。| {{site.data.keyword.Bluemix_notm}} 主控台 |
{: caption="表 3. 發佈並測試整合式計費供應項目" caption-side="top"}

