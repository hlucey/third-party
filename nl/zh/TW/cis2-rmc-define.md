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

# 步驟 2. 在資源管理主控台中定義供應項目

資源管理主控台是一種 Web 型工具，可協助引導您將協力廠商供應項目提供至 {{site.data.keyword.Bluemix_notm}} 型錄。

既然您已獲准提供整合式計費服務，就可以前往資源管理主控台來登錄、開始開發供應項目，以及提供定價方案：
   1. 向資源管理主控台登錄服務，並驗證「摘要」頁面。
   2. 在「供應項目」頁面內，輸入您的型錄 meta 資料。
   3. 向 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 登錄供應項目。登錄會產生用來鑑別服務的用戶端 ID 及服務 ID 認證。
   4. 完成「定價」頁面，並確定 {{site.data.keyword.Bluemix_notm}} 中的服務供應項目提供正確的定價方案給客戶。您定義的方案包括可提供重要用量詳細資料的計量。
   5. 將供應項目 meta 資料匯出為 JSON 格式。


## 開始之前

此步驟假設您已獲准提供整合式計費服務。如果您尚未在 Provider Workbench 中完成起始登錄及核准，則請參閱[入門指導教學](/docs/third-party/index.html)。
{: tip}

1. 確定您已開始處理[步驟 1：編寫服務文件及行銷公告 (PWB)](/docs/third-party/cis1-docs-marketing.html)。
2. 確定您已向 {{site.data.keyword.Bluemix_notm}} 登錄。否則，請先[登錄](https://console.bluemix.net/registration)，再繼續。
3. 當您開始在資源管理主控台中工作時，請確定位於正確的帳戶中。
4. 準備 {{site.data.keyword.Bluemix_notm}} 服務名稱。

   您必須同時提供 {{site.data.keyword.Bluemix_notm}} 平台用來識別服務的服務名稱，以及客戶在 {{site.data.keyword.Bluemix_notm}} 型錄中看到的顯示名稱。

  向資源管理主控台登錄供應項目時，請準備好 {{site.data.keyword.Bluemix_notm}} 服務名稱。服務名稱不是您的顯示名稱。您的服務名稱必須遵循下列規則：
   - 必須全部為小寫
   - 不能包括空格，但可以包括連字號 (`-`)
   - 必須少於 32 個字元

   您的服務名稱應該包含您的公司名稱。如果貴公司有多個供應項目，則服務名稱應該同時包含公司及供應項目作為名稱的一部分。例如，Compose 公司有 Redis 及 Elasticsearch 的供應項目。{{site.data.keyword.Bluemix_notm}} 上這些供應項目的範例服務名稱會是 `compose-redis` 及 `compose-elasticsearch`。這兩個服務名稱都有 {{site.data.keyword.Bluemix_notm}} 型錄中所顯示的相關聯顯示名稱：*Compose Redis* 及 *Compose Elasticsearch*。另一家公司（例如，FastJetMail）只能有單一 JetMail 供應項目，在此情況下，服務名稱應該是 `fastjetmail`。

## 登錄供應項目

若要開始使用，請登入並登錄供應項目。

1. 使用 {{site.data.keyword.Bluemix_notm}} ID 登入 {{site.data.keyword.Bluemix_notm}}：[https://console.bluemix.net](https://console.bluemix.net){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。
   **警告**：您必須位於正確的 {{site.data.keyword.Bluemix_notm}} 帳戶。如果您有多個帳戶，則請確定切換至正確的帳戶。
2. 移至資源管理主控台儀表板：[https://console.bluemix.net/onboarding/dashboard](https://console.bluemix.net/onboarding/dashboard){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。
3. 按一下**新建資源**以新增資源。
4. 新增**資源名稱**。此值是您在上節中衍生的唯一 {{site.data.keyword.Bluemix_notm}} 服務名稱。
5. 處理程序進行至此，我們並不預期您有現有的受管理服務分配管理系統，請針對**分配管理系統是否已準備好匯入？**欄位選取**否**。我們將會引導您在稍後的步驟中建立分配管理系統，而在開發及管理分配管理系統之後，您將回到資源管理主控台來匯入分配管理系統。
7. 提交之後，會將您帶至**摘要**頁面。請完成任何其他*必要* 值，然後按一下**儲存**。

您可以在資源管理主控台中儲存進度，稍後再回來新增其他資訊。資源管理主控台的設計旨在協助您管理服務的生命週期，因此，如果您無法馬上取得所有欄位的所有答案也沒關係。
{: tip}

## 輸入供應項目 meta 資料

在**供應項目**頁面上，提供 {{site.data.keyword.Bluemix_notm}} 型錄中所儲存的 meta 資料值。此外，這當中有一些值需要匯出並儲存在服務分配管理系統中，而在服務分配管理系統中，它們用來進行佈建，且會傳回作為「`型錄 (GET)` 回應」的一部分。在稍後的步驟中，您將使用這些值來協助快速開始服務分配管理系統的開發。

1. 從資源管理主控台中，按一下**供應項目**頁面，然後按一下**列出頁面**標籤。**列出頁面**定義 {{site.data.keyword.Bluemix_notm}} 供應項目服務儀表板中所顯示的 meta 資料。完成所有必要值，然後按一下**儲存**。資源管理主控台將會向 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 執行服務的起始登錄。即會顯示已向 IAM 登錄服務的通知。您稍後將會使用 IAM 執行更多作業。
2. 從「供應項目」頁面中，按一下**設定**標籤。
   1. 指定您的供應項目是否容許**支援方案變更？**。預設值為**否**。如果您指定**是**，則需要延伸 Open Service Broker，以支援所佈建實例的方案變更。如果您的供應項目支援多個方案，且您想要使用者能夠變更現有已佈建實例的方案，則需要讓使用者可以更新其服務實例。如需詳細資料，請參閱 [Open Service Broker API 2.12 版](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#updating-a-service-instance){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 中的 `/v2/service_instances/{instance_id} PATCH` 端點
   2. 指定您的服務是否為**可連結**。預設值為**否**。如果您的服務可以連結至 {{site.data.keyword.Bluemix_notm}} 中的應用程式，請選取**是**。如果可連結，則必須能夠將 API 端點及認證傳回給服務消費者。開發可連結服務時，您必須使用 [Open Service Broker API 2.12 版中的可連結作業](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#binding){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。
   3. 完成其他必要欄位，然後按一下**儲存**。
3. 在導覽中，「供應項目」頁面現在應該會有一個勾號，指出您已達到完成此頁面的最低需求。如果頁面仍然標示為未完成，您應該重新開啟頁面，並檢查是否有任何未完成的*必要* 欄位。

您的起始供應項目信件會包含 Provider Workbench 所產生的服務文件 URL。您必須在**文件 URL** 及**指示 URL** 欄位中輸入該 URL
{: tip}

## 向 IAM 登錄

所有服務都需要有 IAM，才能在 {{site.data.keyword.Bluemix_notm}}上線。請參閱[何謂 IAM？](/docs/iam/index.html#what-is-cloud-iam-)，以進一步瞭解 IAM 概念及需求。

資源管理主控台會產生下列 IAM 值：
   - 服務 ID（已產生並儲存）
   - API 金鑰（已產生但未儲存 - 僅顯示一次）
   - 用戶端 ID（已產生並儲存）
   - 用戶端密碼（已產生但未儲存）

服務提供者需要提供：
   - 重新導向 URI（在您開發 OSB 之後，將會回到資源管理主控台。您將能夠從受管理服務分配管理系統的位置衍生「重新導向 URI」）

1. 從資源管理主控台中，按一下**存取管理**頁面。
2. 按一下**啟用 IAM**。資源管理主控台會向 IAM 登錄您的服務、建立「服務 ID」及「原則」，以及為您建立「API 金鑰」。此外，它還會建立不完整的「用戶端 ID」及「密碼」。在您具有重新導向 URI 之後，必須使用該重新導向 URI 來更新「用戶端 ID」。
3. 按一下**狀態**，以查看 IAM 啟用的現行狀態。

**附註**：您稍後需要回到 IAM 頁面，以提供`重新導向 URI`。在您進行一些額外的開發來建置鑑別流程之前，不會有此值。後續步驟可協助引導您識別「重新導向 URI」值。

當您**啟用 IAM** 時，會提供「API 金鑰」給您。您必須儲存「API 金鑰」。此值不會再次顯示。如果您遺失「API 金鑰」，則可以刪除該金鑰，然後建立新金鑰：[管理服務 ID API 金鑰](/docs/iam/serviceid_keys.html#serviceidapikeys)
{: tip}

## 開發定價方案

在 {{site.data.keyword.Bluemix_notm}} 中讓服務上線時，您必須定義定價方案。如果您十分瞭解如何向使用者收取服務的費用，則可以在方案中提供該資訊。不過，如果您尚未確定使用付費方案，則可以從啟用免費方案開始，然後返回並設定付費方案。

1. 從資源管理主控台中，按一下**定價**頁面。
2. 按一下**新增方案**來建立新的方案項目，然後按一下**編輯方案**來編輯方案。
   * **免費方案**：所有供應項目都可以有一個免費的「精簡方案」，讓使用者試用您的服務。免費方案會使用*精簡* 作為**顯示名稱**，並使用 *lite* 作為**程式化名稱**。針對**此方案是否免費？**，指定**是**。按一下**儲存**。您的方案會發佈至 {{site.data.keyword.Bluemix_notm}} 型錄。
   * **訂閱方案**：針對**此方案是否免費？**，指定**否**。完成必要欄位。保留預設**定價標準**度量值。提供此預設度量值，供您用來向使用者收取一次性的每月費用。按一下**儲存**。您的方案會發佈至 {{site.data.keyword.Bluemix_notm}} 型錄。儲存範例 curl 指令來提交用量。
   * **計量方案**：針對**此方案是否免費？**，指定**否**。完成必要欄位。*刪除* 預設**定價標準**訂閱度量值。按一下**新增另一個度量值**，並完成**新增定價標準**頁面，然後按一下**新增度量值**。按一下**儲存**。您的方案會發佈至 {{site.data.keyword.Bluemix_notm}} 型錄。儲存範例 curl 指令來提交用量。如需選取正確度量值的說明，請參閱[計量整合](/docs/third-party/metering.html)。
3. **定價**頁面現在應該會標示為已完成，指出您已達到完成此頁面的最低需求。

需要有服務提供者，才能自動執行所有計量方案的每小時用量提交。如需相關資訊，請參閱：[提交計量方案的用量](/docs/third-party/submitusage.html)
{: tip}

## 將 meta 資料匯出為 JSON

既然您已在資源管理主控台內定義服務，就可以下載 catalog.json 檔案，並使用它來通知開發您的 Open Service Broker。catalog.json 包含必須在分配管理系統中管理的 meta 資料。這些值定義分配管理系統與分配管理系統所支援服務及方案之 {{site.data.keyword.Bluemix_notm}} 平台間的合約。佈建不需要的所有其他型錄 meta 資料，都會儲存在 {{site.data.keyword.Bluemix_notm}} 型錄內，而且用來呈現儀表板的任何型錄顯示值更新（例如鏈結、圖示及 i18n 已翻譯 meta 資料）都應該在資源管理主控台中進行更新，而不是在分配管理系統中進行管理。您分配管理系統中所儲存的 meta 資料都不會顯示在 {{site.data.keyword.Bluemix_notm}} 主控台或 {{site.data.keyword.Bluemix_notm}} CLI 中；主控台及 CLI 會傳回資源管理主控台內所設定並儲存在 {{site.data.keyword.Bluemix_notm}} 型錄中的內容。

1. 從資源管理主控台中，開啟**部署**頁面。
2. 按一下**管理**。
3. 按一下**下載程式碼**。

儲存 `catalog.json` 檔案。您將使用它在下一節開發 Open Service Broker。

## 後續步驟

做得好！您已透過新增型錄顯示 meta 資料、向 IAM 登錄並建立一個以上的定價方案，來定義服務供應項目。接下來，您可以取得匯出的 JSON，並開始開發服務分配管理系統。請參閱[步驟 3：開發及管理服務分配管理系統](/docs/third-party/cis3-broker.html)。
