---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: 使用 ASP.NET Web API-ASP.NET 4.x 建立 RESTful Api
author: rick-anderson
description: 實習實驗室：使用 ASP.NET 4.x 中的 Web API 來為連絡人管理員應用程式建立簡單的 REST API。
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 72ce313c380547f74d5dc17d1aefbf7cf2da4bea
ms.sourcegitcommit: d4e2a07eeb2cdf19f0bfbfab4a469970bc7e1c99
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2021
ms.locfileid: "98105282"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a>使用 ASP.NET Web API 建立 RESTful Api

由 [Web Camp 小組](https://twitter.com/webcamps)

> 實習實驗室：使用 ASP.NET 4.x 中的 Web API 來為連絡人管理員應用程式建立簡單的 REST API。 您也會建立用戶端以使用 API。

在最近幾年，它已清楚指出 HTTP 不只是用來提供 HTML 網頁。 它也是一個功能強大的平臺，可用於建立 Web Api、使用幾個動詞 (GET、POST 等等) 再加上一些簡單的概念，例如 *uri* 和 *標頭*。 ASP.NET Web API 是一組可簡化 HTTP 程式設計的元件。 因為它建置於 ASP.NET MVC 執行時間之上，所以 Web API 會自動處理 HTTP 的低層級傳輸詳細資料。 同時，Web API 自然會公開 HTTP 程式設計模型。 事實上，Web API 的其中一個目標，就是 *不* 會在 HTTP 的實際情況下被抽象化。 如此一來，Web API 既有彈性又容易擴充。  REST 架構樣式已證明是利用 HTTP 的有效方式，雖然它當然不是 HTTP 的唯一有效方法。 連絡人管理員將會公開 RESTful，以便列出、新增和移除連絡人，以及其他人。 

此實驗室需要對 HTTP、REST 的基本瞭解，並假設您對 HTML、JavaScript 和 jQuery 有基本的實用知識。
> 
> > [!NOTE]
> > ASP.NET 網站有專用於 ASP.NET Web API framework 的區域 [https://asp.net/web-api](https://asp.net/web-api) 。 此網站將繼續提供與 Web API 相關的最新資訊、範例和新聞，因此，如果您想要深入瞭解如何建立可供幾乎任何裝置或開發架構使用的自訂 Web Api，請經常進行檢查。
> > 
> > 與 ASP.NET MVC 4 類似的 ASP.NET Web API，在分隔服務層與控制器之間有很大的彈性，可讓您輕鬆地使用數種可用的相依性插入架構。 
> 
> 
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在上取得 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409) 。

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在這個實際操作實驗室中，您將瞭解如何：

- 執行 RESTful Web API
- 從 HTML 用戶端呼叫 API

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>必要條件

完成此實際操作實驗室需要下列各項：

- [Microsoft Visual Studio Express 2012 For Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 或高階 (閱讀 [附錄 B](#AppendixB) 以取得如何安裝) 的指示。

<a id="Setup"></a>
### <a name="setup"></a>設定

**安裝程式碼片段**

為了方便起見，您將在此實驗室中管理的大部分程式碼都是以 Visual Studio 程式碼片段的形式提供。 若要安裝程式碼片段，請執行 **.\Source\Setup\CodeSnippets.vsi** 檔。

如果您不熟悉 Visual Studio Code 程式碼片段，並想要瞭解如何使用這些程式碼片段，您可以參考本檔 &quot; [附錄 A：使用程式碼片段](#AppendixA)的附錄 &quot; 。

<a id="Exercises"></a>
## <a name="exercises"></a>練習

此實際操作實驗室包含下列練習：

1. [練習1：建立 Read-Only Web API](#Exercise1)
2. [練習2：建立讀取/寫入 Web API](#Exercise2)
3. [練習3：使用 HTML 用戶端的 Web API](#Exercise3)

> [!NOTE]
> 每個練習都會伴隨一個 **結束** 資料夾，其中包含您在完成練習之後應取得的解決方案。 如果您需要其他協助來進行練習，您可以使用此解決方案作為指南。

完成此實驗室的預估時間： **60 分鐘**。

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a>練習1：建立 Read-Only Web API

在此練習中，您將會執行 contact manager 的唯讀 GET 方法。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a>工作 1-建立 API 專案

在這項工作中，您將使用新的 ASP.NET Web 專案範本來建立 Web API web 應用程式。

1. 執行 **Visual Studio 2012 Express For Web**，若要執行此動作，請移至 [ **開始** ]，然後輸入 **VS Express for Web** 然後按 **enter** 鍵。
2. 從 [ **檔案** ] 功能表選取 [ **新增專案**]。 選取 **Visual c # |** [專案類型] 樹狀檢視中的 [Web 專案類型]，然後選取 [ **ASP.NET MVC 4 Web 應用程式** ] 專案類型。 將專案的 [**名稱**] 設定為 [ *ContactManager* ]，並將 **方案名稱** 設定為 [*開始*]，然後按一下 **[確定]**

    ![建立新的 ASP.NET MVC 4.0 Web 應用程式專案](build-restful-apis-with-aspnet-web-api/_static/image1.png "建立新的 ASP.NET MVC 4.0 Web 應用程式專案")

    *建立新的 ASP.NET MVC 4.0 Web 應用程式專案*
3. 在 [ASP.NET MVC 4 專案類型] 對話方塊中，選取 [ **WEB API** ] 專案類型。 按一下 [確定]。

    ![指定 Web API 專案類型](build-restful-apis-with-aspnet-web-api/_static/image2.png "指定 Web API 專案類型")

    *指定 Web API 專案類型*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a>工作 2-建立連絡人管理員 API 控制器

在這項工作中，您將建立 API 方法所在的控制器類別。

1. 從專案刪除 [**控制器**] 資料夾中名為 **ValuesController.cs** 的檔案。
2. 以滑鼠右鍵按一下專案中的 [ **控制器** ] 資料夾，然後選取 [ **新增] |** 內容功能表中的控制器。

    ![將新的控制器新增至專案](build-restful-apis-with-aspnet-web-api/_static/image3.png "將新的控制器新增至專案")

    *將新的控制器新增至專案*
3. 在出現的 [ **新增控制器** ] 對話方塊中，從 [範本] 功能表選取 [ **空白 API 控制器** ]。 將控制器類別命名為 **ContactController**。 然後按一下 [ **新增]。**

    ![使用 [新增控制器] 對話方塊來建立新的 Web API 控制器](build-restful-apis-with-aspnet-web-api/_static/image4.png "使用 [新增控制器] 對話方塊來建立新的 Web API 控制器")

    *使用 [新增控制器] 對話方塊來建立新的 Web API 控制器*
4. 將下列程式碼新增至 **ContactController**。

     (程式碼片段- *WEB API 實驗室-Ex01-取得 API 方法*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. 按 **F5** 鍵來進行應用程式偵錯。 Web API 專案的預設首頁應會出現。

    ![ASP.NET Web API 應用程式的預設首頁](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API 應用程式的預設首頁")

    *ASP.NET Web API 應用程式的預設首頁*
6. 在 [Internet Explorer] 視窗中，按下 **F12** 鍵以開啟 [ **開發人員工具** ] 視窗。 按一下 [ **網路** ] 索引標籤，然後按一下 [ **開始捕獲** ] 按鈕，開始將網路流量捕獲到視窗中。

    ![開啟 [網路] 索引標籤並起始網路捕獲](build-restful-apis-with-aspnet-web-api/_static/image6.png "開啟 [網路] 索引標籤並起始網路捕獲")

    *開啟 [網路] 索引標籤並起始網路捕獲*
7. 使用 **/api/contact** 在瀏覽器的網址列中附加 URL，然後按 enter。 傳輸詳細資料將會出現在 [網路捕捉] 視窗中。 請注意，回應的 MIME 類型為 **application/json**。 這會示範預設輸出格式為 JSON。

    ![在網路視圖中查看 Web API 要求的輸出](build-restful-apis-with-aspnet-web-api/_static/image7.png "在網路視圖中查看 Web API 要求的輸出")

    *在網路視圖中查看 Web API 要求的輸出*

    > [!NOTE]
    > Internet Explorer 10 的預設行為會詢問使用者是否想要儲存或開啟 Web API 呼叫所產生的串流。 輸出將會是一個文字檔，其中包含 Web API URL 呼叫的 JSON 結果。 請勿取消對話方塊，以便透過開發人員工具視窗監看回應的內容。
8. 按一下 [ **移至詳細的視圖** ] 按鈕，以查看此 API 呼叫回應的詳細資料。

    ![切換至詳細觀點](build-restful-apis-with-aspnet-web-api/_static/image8.png "切換至詳細資料檢視")

    *切換至詳細觀點*
9. 按一下 [ **回應** 內文] 索引標籤，以查看實際的 JSON 回應文字。

    ![在網路監視器中查看 JSON 輸出文字](build-restful-apis-with-aspnet-web-api/_static/image9.png "在網路監視器中查看 JSON 輸出文字")

    *在網路監視器中查看 JSON 輸出文字*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a>工作 3-建立連絡人模型並增加連絡人控制器

在這項工作中，您將建立 API 方法所在的控制器類別。

1. 以滑鼠右鍵按一下 [ **模型** ] 資料夾，然後選取 [ **新增] |類別 ...** 從內容功能表。

    ![將新模型加入至 web 應用程式](build-restful-apis-with-aspnet-web-api/_static/image10.png "將新模型加入至 web 應用程式")

    *將新模型加入至 web 應用程式*
2. 在 [ **加入新專案** ] 對話方塊中，將新的檔案命名為 **Contact.cs** ，然後按一下 [ **新增]。**

    ![建立新的連絡人類別檔案](build-restful-apis-with-aspnet-web-api/_static/image11.png "建立新的連絡人類別檔案")

    *建立新的連絡人類別檔案*
3. 將下列反白顯示的程式碼新增至 **Contact** 類別。

     (程式碼片段- *WEB API 實驗室-Ex01-Contact 類別*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. 在 **ContactController** 類別中，選取 **Get** 方法的方法定義中的文字 **字串**，然後輸入單字 *Contact*。 一旦輸入文字，就會在字組 **連絡人** 的開頭出現一個指標。 按住 **Ctrl** 鍵，然後按下句號 (。 ) 按鍵，或按一下圖示，以在程式碼編輯器中開啟 [協助] 對話方塊，以自動填入模型命名空間的 **using** 指示詞。

    ![使用命名空間宣告的 Intellisense 協助](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    *使用命名空間宣告的 Intellisense 協助*
5. 修改 **Get** 方法的程式碼，使其傳回 Contact 模型實例的陣列。

     (程式碼片段- *WEB API 實驗室-Ex01-傳回連絡人清單*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. 按 **F5** 以在瀏覽器中進行 web 應用程式的偵錯工具。 若要查看對 API 回應輸出所做的變更，請執行下列步驟。

   1. 當瀏覽器開啟時，如果開發人員工具尚未開啟，請按 **F12** 。
   2. 按一下 [ **網路** ] 索引標籤。
   3. 按下 [ **開始捕獲** ] 按鈕。
   4. 將 URL 尾碼 **/api/contact** 新增至網址列中的 url，然後按下 **enter** 鍵。
   5. 按 [ **移至詳細的視圖** ] 按鈕。
   6. 選取 [ **回應** 內文] 索引標籤。您應該會看到代表連絡人實例陣列序列化形式的 JSON 字串。

      ![複雜 Web API 方法呼叫的 JSON 序列化輸出](build-restful-apis-with-aspnet-web-api/_static/image13.png "複雜 Web API 方法呼叫的 JSON 序列化輸出")

      *複雜 Web API 方法呼叫的 JSON 序列化輸出*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a>工作 4-將功能解壓縮至服務層

這項工作將示範如何將功能解壓縮至服務層級，讓開發人員輕鬆地將其服務功能與控制器層分開，進而允許重複使用實際執行工作的服務。

1. 在方案根目錄中建立新的資料夾，並將它命名為「it **服務**」。 若要這樣做，請以滑鼠右鍵按一下 [ **ContactManager** 專案]，**然後選取 [**  |  **新增資料夾**]、[命名 it *服務*]。

    ![正在建立服務資料夾](build-restful-apis-with-aspnet-web-api/_static/image14.png "正在建立服務資料夾")

    *正在建立服務資料夾*
2. 以滑鼠右鍵按一下 [ **服務** ] 資料夾，然後選取 [ **新增] |類別 ...** 從內容功能表。

    ![將新類別新增至服務資料夾](build-restful-apis-with-aspnet-web-api/_static/image15.png "將新類別新增至服務資料夾")

    *將新類別新增至服務資料夾*
3. 當 [ **加入新專案** ] 對話方塊出現時，將新的類別命名為 **contacts.json** ，然後按一下 [ **加入**]。

    ![建立類別檔案以包含連絡人存放庫服務層的程式碼](build-restful-apis-with-aspnet-web-api/_static/image16.png "建立類別檔案以包含連絡人存放庫服務層的程式碼")

    *建立類別檔案以包含連絡人存放庫服務層的程式碼*
4. 將 using 指示詞加入至 **ContactRepository.cs** 檔案，以包含模型命名空間。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. 將下列反白顯示的程式碼加入至 **ContactRepository.cs** 檔案，以執行 GetAllContacts 方法。

     (程式碼片段- *WEB API 實驗室-Ex01-Contact Repository*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. 開啟 **ContactController.cs** 檔案（如果尚未開啟）。
7. 將下列 using 語句加入至檔案的命名空間宣告區段。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. 將下列反白顯示的程式碼加入至 **ContactController.cs** 類別，以新增私用欄位來代表存放庫的實例，讓其他類別成員可以使用服務執行。

     (程式碼片段- *WEB API 實驗室-Ex01-Contact Controller*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. 變更 **Get** 方法，讓它利用 contact repository 服務。

     (程式碼片段- *WEB API 實驗室-Ex01-透過存放庫傳回連絡人清單*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. 將中斷點放在 **ContactController** 的 **Get** 方法定義上。

   ![將中斷點新增至連絡人控制器](build-restful-apis-with-aspnet-web-api/_static/image17.png "將中斷點新增至連絡人控制器")

   *將中斷點新增至連絡人控制器*
11. 按 **F5** 執行應用程式。
12. 當瀏覽器開啟時，請按 **F12** 來開啟開發人員工具。
13. 按一下 [ **網路** ] 索引標籤。
14. 按一下 [ **開始捕獲** ] 按鈕。
15. 在網址列中附加尾碼 **/api/contact** ，然後按 **ENTER** 以載入 api 控制器。
16. 當 **Get** 方法開始執行時，Visual Studio 2012 應該會中斷。

   ![在 Get 方法內中斷](build-restful-apis-with-aspnet-web-api/_static/image18.png "在 Get 方法內中斷")

   *在 Get 方法內中斷*
17. 按 **F5** 繼續。
18. 如果未處於焦點，返回 Internet Explorer。 請記下 [網路捕捉] 視窗。

    ![Internet Explorer 中顯示 Web API 呼叫結果的網路視圖](build-restful-apis-with-aspnet-web-api/_static/image19.png "Internet Explorer 中顯示 Web API 呼叫結果的網路視圖")

    *Internet Explorer 中顯示 Web API 呼叫結果的網路視圖*
19. 按一下 [ **移至詳細的視圖** ] 按鈕。
20. 按一下 [ **回應** 內文] 索引標籤。請注意 API 呼叫的 JSON 輸出，以及它如何代表服務層所抓取的兩個連絡人。

    ![從 [開發人員工具] 視窗中的 Web API 查看 JSON 輸出](build-restful-apis-with-aspnet-web-api/_static/image20.png "從 [開發人員工具] 視窗中的 Web API 查看 JSON 輸出")

    *從 [開發人員工具] 視窗中的 Web API 查看 JSON 輸出*

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a>練習2：建立讀取/寫入 Web API

在此練習中，您將會針對 contact manager 執行 POST 和 PUT 方法，以使用資料編輯功能來啟用它。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a>工作 1-開啟 Web API 專案

在這項工作中，您將準備增強在練習1中建立的 Web API 專案，使其可以接受使用者輸入。

1. 執行 **Visual Studio 2012 Express For Web**，若要執行此動作，請移至 [ **開始** ]，然後輸入 **VS Express for Web** 然後按 **enter** 鍵。
2. 開啟位於 **來源/Ex02-ReadWriteWebAPI/begin/** Folder 的 **開始** 解決方案。 否則，您可能會繼續使用完成上一個練習所取得的 **結束** 解決方案。

   1. 如果您已開啟提供的 **開始** 解決方案，則必須先下載一些缺少的 NuGet 套件，再繼續進行操作。 若要這樣做，請按一下 [ **專案** ] 功能表，然後選取 [ **管理 NuGet 套件**]。
   2. 在 [ **管理 NuGet 封裝** ] 對話方塊中，按一下 [ **還原** ] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**  |  **組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的優點之一，就是您不需要在專案中寄出所有的程式庫，以減少專案的大小。 使用 NuGet Power Tools，藉由在 Packages.config 檔案中指定套件版本，您將能夠在第一次執行專案時下載所有必要的程式庫。 這就是當您從此實驗室開啟現有的解決方案之後，必須執行這些步驟的原因。
3. 開啟 **Services/contacts.json .cs** 檔案。

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a>工作 2-將 Data-Persistence 功能新增至連絡人存放庫的執行

在這項工作中，您將增強在練習1中建立之 Web API 專案的 Contacts.json 類別，讓它可以保存和接受使用者輸入和新的連絡人實例。

1. 將下列常數加入至 **contacts.json** 類別，以代表此練習稍後的 web 伺服器快取專案索引鍵名稱。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. 將包含下列程式碼的函式新增至 **contacts.json** 。

     (程式碼片段- *WEB API 實驗室-Ex02-聯絡儲存* 機制的函式) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. 修改 **GetAllContacts** 方法的程式碼，如下所示。

     (程式碼片段- *WEB API 實驗室-Ex02-取得所有連絡人*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > 此範例僅供示範之用，並且會使用網頁伺服器的快取作為儲存媒體，讓多個用戶端可以同時使用這些值，而不是使用會話儲存機制或要求儲存存留期。 您可以使用 Entity Framework、XML 儲存體或任何其他種類來取代 web 伺服器快取。
4. 將名為 **SaveContact** 的新方法實作為 **contacts.json** 類別，以執行儲存連絡人的工作。 **SaveContact** 方法應該採用單一 **Contact** 參數，並傳回指出成功或失敗的布林值。

     (程式碼片段- *WEB API 實驗室-Ex02-執行 SaveContact 方法*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a>練習3：使用 HTML 用戶端的 Web API

在此練習中，您將建立 HTML 用戶端來呼叫 Web API。 此用戶端將使用 JavaScript 以 Web API 來加速資料交換，並使用 HTML 標籤將結果顯示在網頁瀏覽器中。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a>工作 1-修改索引視圖以提供 GUI 來顯示連絡人

在這項工作中，您將修改 web 應用程式的預設索引視圖，以支援在 HTML 瀏覽器中顯示現有連絡人清單的需求。

1. 開啟 **Visual Studio 2012 Express For Web （** 如果尚未開啟）。
2. 開啟位於 **來源/Ex03-ConsumingWebAPI/begin/** Folder 的 **開始** 解決方案。 否則，您可能會繼續使用完成上一個練習所取得的 **結束** 解決方案。

   1. 如果您已開啟提供的 **開始** 解決方案，則必須先下載一些缺少的 NuGet 套件，再繼續進行操作。 若要這樣做，請按一下 [ **專案** ] 功能表，然後選取 [ **管理 NuGet 套件**]。
   2. 在 [ **管理 NuGet 封裝** ] 對話方塊中，按一下 [ **還原** ] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**  |  **組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的優點之一，就是您不需要在專案中寄出所有的程式庫，以減少專案的大小。 使用 NuGet Power Tools，藉由在 Packages.config 檔案中指定套件版本，您將能夠在第一次執行專案時下載所有必要的程式庫。 這就是當您從此實驗室開啟現有的解決方案之後，必須執行這些步驟的原因。
3. 開啟位於 **Views/Home** 資料夾的 **索引. cshtml** 檔案。
4. 以識別碼 **主體** 取代 div 元素內的 HTML 程式碼，使其看起來類似下列程式碼。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. 在檔案底部新增下列 JAVAscript 程式碼，以執行 Web API 的 HTTP 要求。

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. 開啟 **ContactController.cs** 檔案（如果尚未開啟）。
7. 在 **ContactController** 類別的 **Get** 方法上放置中斷點。

    ![將中斷點放在 API 控制器的 Get 方法上](build-restful-apis-with-aspnet-web-api/_static/image21.png "將中斷點放在 API 控制器的 Get 方法上")

    *將中斷點放在 API 控制器的 Get 方法上*
8. 按 **F5** 執行專案。 瀏覽器將會載入 HTML 檔案。

    > [!NOTE]
    > 確定您正在流覽至應用程式的根 URL。
9. 一旦頁面載入且 JavaScript 執行之後，將會叫用中斷點，並在控制器中暫停程式碼執行。

    ![使用 VS Express for Web 進行 Web API 呼叫的調試](build-restful-apis-with-aspnet-web-api/_static/image22.png "使用 VS Express for Web 進行 Web API 呼叫的調試")

    *使用 Visual Studio 2012 Express for Web 進行 Web API 呼叫的偵錯工具*
10. 移除中斷點，然後按 **F5** 或偵錯工具工具列的 [ **繼續** ] 按鈕，以繼續在瀏覽器中載入此視圖。 Web API 呼叫完成後，您應該會看到從 Web API 呼叫傳回的連絡人在瀏覽器中顯示為清單專案。

    ![以清單專案形式顯示在瀏覽器中的 API 呼叫結果](build-restful-apis-with-aspnet-web-api/_static/image23.png "以清單專案形式顯示在瀏覽器中的 API 呼叫結果")

    *以清單專案形式顯示在瀏覽器中的 API 呼叫結果*
11. 停止偵錯。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a>工作 2-修改索引視圖以提供用來建立連絡人的 GUI

在這項工作中，您將繼續修改 MVC 應用程式的索引視圖。 系統會將表單新增至 HTML 網頁，以捕獲使用者輸入，並將其傳送至 Web API 以建立新的連絡人，並會建立新的 Web API 控制器方法，以從 GUI 收集日期。

1. 開啟 **ContactController.cs** 檔案。
2. 將新方法新增至名為 **Post** 的控制器類別，如下列程式碼所示。

     (程式碼片段- *WEB API 實驗室-Ex03-Post 方法*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. 如果尚未開啟，請在 Visual Studio 中開啟 [**索引]。**
4. 在您于上一個工作中新增的未排序清單之後，將下列 HTML 程式碼新增至檔案。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. 在檔底部的腳本專案中，加入下列反白顯示的程式碼來處理按鈕的 click 事件，此事件會使用 HTTP POST 呼叫將資料張貼至 Web API。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. 在 **ContactController.cs** 中，將中斷點放在 **Post** 方法上。
7. 按 **F5** 以在瀏覽器中執行應用程式。
8. 在瀏覽器中載入網頁之後，輸入新的連絡人名稱和識別碼，然後按一下 [ **儲存** ] 按鈕。

    ![在瀏覽器中載入的用戶端 HTML 檔案](build-restful-apis-with-aspnet-web-api/_static/image24.png "在瀏覽器中載入的用戶端 HTML 檔案")

    *在瀏覽器中載入的用戶端 HTML 檔案*
9. 當偵錯工具視窗在 **Post** 方法中中斷時，請查看 **contact** 參數的屬性。 這些值應該符合您在表單中輸入的資料。

    ![從用戶端傳送至 Web API 的 Contact 物件](build-restful-apis-with-aspnet-web-api/_static/image25.png "從用戶端傳送至 Web API 的 Contact 物件")

    *從用戶端傳送至 Web API 的 Contact 物件*
10. 在偵錯工具中逐步執行方法，直到已建立 **回應** 變數為止。 在偵錯工具的 [ **區域變數** ] 視窗中檢查時，您會看到已設定所有屬性。

   ![在偵錯工具中建立後的回應](build-restful-apis-with-aspnet-web-api/_static/image26.png "在偵錯工具中建立後的回應")

   *在偵錯工具中建立後的回應*
11. 如果您按 **F5** 或按一下偵錯工具中的 [ **繼續** ]，則要求將會完成。 一旦您切換回瀏覽器，新的連絡人就會新增至 **contacts.json** 執行所儲存的連絡人清單。

   ![瀏覽器會反映成功建立新的連絡人實例](build-restful-apis-with-aspnet-web-api/_static/image27.png "瀏覽器會反映成功建立新的連絡人實例")

   *瀏覽器會反映成功建立新的連絡人實例*

> [!NOTE]
> 此外，您可以遵循 [附錄 C：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式](#AppendixC)，以將此應用程式部署至 Azure。

---

<a id="Summary"></a>
## <a name="summary"></a>摘要

此實驗室為您介紹了新的 ASP.NET Web API 架構，以及使用架構 RESTful Web Api 的執行。 從這裡開始，您可以建立新的存放庫，以利用任何數目的機制來加速資料保存，並連接到該服務，而不是在此實驗室中提供的簡單範例。 Web API 支援許多額外的功能，例如從以任何支援 HTTP 和 JSON 或 XML 語言撰寫的非 HTML 用戶端啟用通訊。 也可以將 Web API 裝載在一般 web 應用程式之外的能力，也可以建立您自己的序列化格式。

ASP.NET 網站有專用於 ASP.NET Web API framework 的區域 [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api) 。 此網站將繼續提供與 Web API 相關的最新資訊、範例和新聞，因此，如果您想要深入瞭解如何建立可供幾乎任何裝置或開發架構使用的自訂 Web Api，請經常進行檢查。

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>附錄 A：使用程式碼片段

使用程式碼片段，您可以隨時取得所需的所有程式碼。 實驗室檔將會告訴您您可以使用它們的確切時機，如下圖所示。

![使用 Visual Studio 程式碼片段，將程式碼插入專案中](build-restful-apis-with-aspnet-web-api/_static/image28.png "使用 Visual Studio 程式碼片段，將程式碼插入專案中")

*使用 Visual Studio 程式碼片段，將程式碼插入專案中*

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a>若要使用鍵盤新增程式碼片段 (c #) 

1. 將游標放在您想要插入程式碼的位置。
2. 開始鍵入程式碼片段名稱 (不含空格或連字號) 。
3. 觀賞 IntelliSense 會顯示相符程式碼片段的名稱。
4. 選取正確的程式碼片段 (或繼續輸入，直到選取整個程式碼片段的名稱) 為止。
5. 按 Tab 鍵兩次，將程式碼片段插入游標位置。

    ![開始鍵入程式碼片段名稱](build-restful-apis-with-aspnet-web-api/_static/image29.png "開始鍵入程式碼片段名稱")

    *開始鍵入程式碼片段名稱*

    ![按 Tab 鍵選取反白顯示的程式碼片段](build-restful-apis-with-aspnet-web-api/_static/image30.png "按 Tab 鍵選取反白顯示的程式碼片段")

    *按 Tab 鍵選取反白顯示的程式碼片段*

    ![再次按下 Tab 鍵，程式碼片段將會展開](build-restful-apis-with-aspnet-web-api/_static/image31.png "再次按下 Tab 鍵，程式碼片段將會展開")

    *再次按下 Tab 鍵，程式碼片段將會展開*

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a>若要使用滑鼠 (c # 加入程式碼片段，請 Visual Basic 和 XML) 

1. 以滑鼠右鍵按一下您要插入程式碼片段的位置。
2. 選取 [ **插入程式碼片段** ]，接著 **My Code 程式碼片段**]。
3. 按一下清單中的相關程式碼片段，以從清單中選取相關程式碼片段。

    ![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入程式碼片段]。](build-restful-apis-with-aspnet-web-api/_static/image32.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入程式碼片段]。")

    *以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入程式碼片段]。*

    ![按一下清單中的相關程式碼片段，以從清單中選取相關程式碼片段](build-restful-apis-with-aspnet-web-api/_static/image33.png "按一下清單中的相關程式碼片段，以從清單中選取相關程式碼片段")

    *按一下清單中的相關程式碼片段，以從清單中選取相關程式碼片段*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>附錄 B：安裝適用于 Web 的 Visual Studio Express 2012

您可以使用 Microsoft Web Platform Installer 來安裝 Web 或其他 Express 版本 **的 Microsoft Visual Studio Express 2012** &quot; &quot; 。 **[](https://www.microsoft.com/web/downloads/platform.aspx)** 下列指示會引導您完成使用 *Microsoft Web Platform Installer* 安裝 *Visual studio Express 2012 for Web* 所需的步驟。

1. 移至 [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169) 。 或者，如果您已經安裝 Web Platform Installer，您可以使用 Azure SDK 來開啟並搜尋適用于 Web 的產品 &quot; <em>Visual Studio Express 2012</em> &quot; 。
2. 按一下 [ **立即安裝**]。 如果您沒有 **Web Platform Installer** 系統會將您重新導向，以先下載並安裝。
3. **Web Platform Installer** 開啟後，按一下 [**安裝**] 以啟動安裝程式。

    ![安裝 Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "安裝 Visual Studio Express")

    *安裝 Visual Studio Express*
4. 閱讀所有產品的授權和條款，然後按一下 [ **我接受** ] 繼續進行。

    ![接受授權條款](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    *接受授權條款*
5. 等候下載和安裝程式完成。

    ![安裝進度](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    *安裝進度*
6. 當安裝完成時，按一下 **[完成]**。

    ![安裝已完成](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    *安裝已完成*
7. 按一下 **[** 結束] 以關閉 Web Platform Installer。
8. 若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面並開始撰寫 &quot; **VS Express** &quot; ，然後按一下 [ **VS Express for Web** ] 磚。

    ![VS Express for Web 磚](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    *VS Express for Web 磚*

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附錄 C：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式

本附錄將示範如何從 Azure 入口網站建立新的網站，以及如何利用 Azure 所提供的 Web Deploy 發行功能，發佈您在實驗室中取得的應用程式。

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>工作 1-從 Azure 入口網站建立新的網站

1. 移至 [Azure 管理入口網站](https://manage.windowsazure.com/) ，並使用與您訂用帳戶相關聯的 Microsoft 認證登入。

    > [!NOTE]
    > 有了 Azure，您可以免費裝載10個 ASP.NET 網站，然後隨著流量成長調整規模。 您可以在 [這裡](https://aka.ms/aspnet-hol-azure)註冊。

    ![登入 Windows Azure 入口網站](build-restful-apis-with-aspnet-web-api/_static/image39.png "登入 Windows Azure 入口網站")

    *登入入口網站*
2. 按一下命令列上的 [ **新增** ]。

    ![建立新網站](build-restful-apis-with-aspnet-web-api/_static/image40.png "建立新網站")

    *建立新網站*
3. 按一下 [**計算**  |  **網站**]。 然後選取 [ **快速建立** ] 選項。 為新的網站提供可用的 URL，然後按一下 [ **建立網站**]。

    > [!NOTE]
    > Azure 是在雲端中執行的 web 應用程式，您可以控制和管理該應用程式的主機。 [快速建立] 選項可讓您從入口網站外部將已完成的 web 應用程式部署到 Azure。 它不包含設定資料庫的步驟。

    ![使用 [快速建立] 建立新的網站](build-restful-apis-with-aspnet-web-api/_static/image41.png "使用 [快速建立] 建立新的網站")

    *使用 [快速建立] 建立新的網站*
4. 等候新 **網站** 建立。
5. 建立網站之後，請按一下 [ **URL** ] 資料行底下的連結。 檢查新網站是否正常運作。

    ![流覽至新的網站](build-restful-apis-with-aspnet-web-api/_static/image42.png "流覽至新的網站")

    *流覽至新的網站*

    ![網站正在執行](build-restful-apis-with-aspnet-web-api/_static/image43.png "網站正在執行")

    *網站正在執行*
6. 返回至入口網站，然後在 [ **名稱** ] 欄下按一下網站名稱以顯示管理頁面。

    ![開啟網站管理頁面](build-restful-apis-with-aspnet-web-api/_static/image44.png "開啟網站管理頁面")

    *開啟網站管理頁面*
7. 在 [ **儀表板** ] 頁面的 [ **快速概覽** ] 區段底下，按一下 [ **下載發行設定檔** ] 連結。

    > [!NOTE]
    > *發行設定檔* 包含針對每個已啟用的發行方法，將 web 應用程式發佈至 Azure 所需的所有資訊。 發行設定檔包含 URL、使用者認證和資料庫字串，這些都是用來連接到已啟用發行方法的每個端點並進行驗證的必要資訊。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web** 和 **Microsoft Visual Studio 2012** 支援讀取發佈設定檔，以將這些程式的設定自動化，以將 Web 應用程式發佈至 Azure。

    ![下載網站發行設定檔](build-restful-apis-with-aspnet-web-api/_static/image45.png "下載網站發行設定檔")

    *下載網站發行設定檔*
8. 將發行設定檔檔案下載至已知位置。 在此練習中，您將瞭解如何使用此檔案，從 Visual Studio 將 web 應用程式發佈至 Azure。

    ![正在儲存發行設定檔](build-restful-apis-with-aspnet-web-api/_static/image46.png "正在儲存發行設定檔")

    *正在儲存發行設定檔*

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>工作 2-設定資料庫伺服器

如果您的應用程式利用 SQL Server 的資料庫，您將需要建立 SQL Database 伺服器。 如果您想要部署不使用 SQL Server 的簡單應用程式，您可以略過此工作。

1. 您將需要 SQL Database 伺服器來儲存應用程式資料庫。 您可以在 Azure 入口網站的 **SQL** database  |  **伺服器**  |  **伺服器的儀表板** 上，從您的訂用帳戶中查看 SQL Database 伺服器。 如果您沒有建立伺服器，可以使用命令列上的 [ **新增** ] 按鈕建立一個伺服器。 記下 **伺服器名稱和 URL、系統管理員登入名稱和密碼**，因為您將在下一項工作中使用它們。 請勿建立資料庫，因為它會在稍後的階段中建立。

    ![SQL Database 伺服器儀表板](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database 伺服器儀表板")

    *SQL Database 伺服器儀表板*
2. 在下一個工作中，您將從 Visual Studio 測試資料庫連線，因此您必須在伺服器的 **允許 Ip 位址** 清單中包含本機 IP 位址。 若要這樣做，請按一下 [ **設定**]，選取 [ **目前用戶端 ip 位址** ] 中的 IP 位址，並將它貼到 [ **起始 Ip 位址** ] 和 [ **結束 ip 位址** ] 文字方塊中，然後按一下 [ ![ 新增-用戶端-IP-位址-確定] ](build-restful-apis-with-aspnet-web-api/_static/image48.png) 按鈕。

    ![新增用戶端 IP 位址](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    *新增用戶端 IP 位址*
3. 一旦將 **用戶端 IP 位址** 新增至 [允許的 ip 位址] 清單，請按一下 [ **儲存** ] 以確認變更。

    ![確認變更](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    *確認變更*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>工作 3-使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式

1. 返回 ASP.NET MVC 4 方案。 在 [ **方案總管** 中，以滑鼠右鍵按一下網站專案，然後選取 [ **發行**]。

    ![發佈應用程式](build-restful-apis-with-aspnet-web-api/_static/image51.png "發行應用程式")

    *發行網站*
2. 匯入您在第一個工作中儲存的發行設定檔。

    ![匯入發行設定檔](build-restful-apis-with-aspnet-web-api/_static/image52.png "匯入發行設定檔")

    *匯入發行設定檔*
3. 按一下 [ **驗證連接**]。 驗證完成後，請按 **[下一步]**。

    > [!NOTE]
    > 當您在 [驗證連接] 按鈕旁邊出現綠色核取記號時，驗證就會完成。

    ![正在驗證連接](build-restful-apis-with-aspnet-web-api/_static/image53.png "正在驗證連接")

    *正在驗證連接*
4. 在 [ **設定** ] 頁面的 [ **資料庫** ] 區段下，按一下資料庫連接文字方塊旁的按鈕 (即 **DefaultConnection**) 。

    ![Web deploy 設定](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy 設定")

    *Web deploy 設定*
5. 設定資料庫連接，如下所示：

   - 在 [ **伺服器名稱** ] 中，輸入您的 SQL DATABASE 伺服器 URL *（使用 tcp：* prefix）。
   - 在 [ **使用者名稱** ] 中，輸入您的伺服器管理員登入名稱。
   - 在 [ **密碼** ] 中，輸入您的伺服器管理員登入密碼。
   - 輸入新的資料庫名稱，例如： *MVC4SampleDB*。

     ![正在設定目的地連接字串](build-restful-apis-with-aspnet-web-api/_static/image55.png "正在設定目的地連接字串")

     *正在設定目的地連接字串*
6. 然後按一下 [確定] 。 當系統提示您建立資料庫時，請按一下 **[是]**。

    ![建立資料庫](build-restful-apis-with-aspnet-web-api/_static/image56.png "建立資料庫字串")

    *建立資料庫*
7. 您將用來連線到 Windows Azure 中 SQL Database 的連接字串會顯示在 [預設連接] 文字方塊中。 然後按一下 [下一步]。

    ![指向 SQL Database 的連接字串](build-restful-apis-with-aspnet-web-api/_static/image57.png "指向 SQL Database 的連接字串")

    *指向 SQL Database 的連接字串*
8. 在 [ **預覽** ] 頁面中，按一下 [ **發行**]。

    ![發行 web 應用程式](build-restful-apis-with-aspnet-web-api/_static/image58.png "發行 web 應用程式")

    *發行 web 應用程式*
9. 發行程式完成之後，您的預設瀏覽器會開啟已發行的網站。

    ![發行至 Windows Azure 的應用程式](build-restful-apis-with-aspnet-web-api/_static/image59.png "發行至 Windows Azure 的應用程式")

    *發佈至 Azure 的應用程式*
