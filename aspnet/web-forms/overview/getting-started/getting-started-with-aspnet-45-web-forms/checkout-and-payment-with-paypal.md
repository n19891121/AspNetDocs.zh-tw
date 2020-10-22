---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: 使用 PayPal 簽出及付款 |Microsoft Docs
author: Erikre
description: 本教學課程系列將告訴您使用 ASP.NET 4.5 建立 ASP.NET Web Forms 應用程式的基本概念，並為我們提供 Microsoft Visual Studio Express 2013 .。。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345653"
---
# <a name="checkout-and-payment-with-paypal"></a>簽出與使用 PayPal 付款

依 [Erik Reitan](https://github.com/Erikre)

[下載 Wingtip 玩具範例專案 (c # ) ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 或 [下載電子書 (PDF) ](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本教學課程系列將教您如何使用 ASP.NET 4.5 和適用于 Web 的 Microsoft Visual Studio Express 2013 來建立 ASP.NET Web Forms 應用程式的基本概念。 [具有 c # 原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案可隨附于本教學課程系列。

本教學課程說明如何使用 PayPal 修改 Wingtip 玩具範例應用程式，以包含使用者授權、註冊和付款。 只有登入的使用者才有購買產品的授權。 ASP.NET 4.5 Web Form 專案範本的內建使用者註冊功能已包含許多您需要的功能。 您將會新增 PayPal 快速簽出功能。 在本教學課程中，您將使用 PayPal 開發人員測試環境，因此不會傳輸實際的資金。 在本教學課程結尾，您將會選取要新增至購物車的產品，然後按一下 [結帳] 按鈕，然後將資料傳送至 PayPal 測試網站，藉以測試應用程式。 在 PayPal 測試網站上，您將確認寄送和付款資訊，然後返回當地 Wingtip 玩具範例應用程式，以確認並完成購買。

有幾個經驗豐富的協力廠商付款處理器，專門從事可解決擴充性和安全性的線上購物。 ASP.NET 開發人員應該先考慮使用協力廠商付款解決方案的優點，再執行購物和購買解決方案。

> [!NOTE] 
> 
> Wingtip 玩具範例應用程式是設計用來顯示 ASP.NET 網頁程式開發人員可用的特定 ASP.NET 概念和功能。 這個範例應用程式未針對擴充性和安全性方面的所有可能情況進行優化。

## <a name="what-youll-learn"></a>您將學到什麼：

- 如何限制存取資料夾中的特定頁面。
- 如何從匿名購物車建立已知的購物車。
- 如何啟用專案的 SSL。
- 如何將 OAuth 提供者新增至專案。
- 如何使用 paypal 來購買使用 PayPal 測試環境的產品。
- 如何在 **DetailsView** 控制項中顯示 PayPal 的詳細資料。
- 如何使用從 PayPal 取得的詳細資料來更新 Wingtip 玩具應用程式的資料庫。

## <a name="adding-order-tracking"></a>加入訂單追蹤

在本教學課程中，您將建立兩個新的類別，以根據使用者建立的訂單來追蹤資料。 這些類別會追蹤有關運送資訊、購買總計和付款確認的資料。

### <a name="add-the-order-and-orderdetail-model-classes"></a>加入 Order 和 OrderDetail 模型類別

稍早在本教學課程系列中，您藉由在 `Category` `Product` `CartItem` [ *模型* ] 資料夾中建立、和類別，定義了類別、產品和購物車專案的架構。 現在您將新增兩個新的類別，以定義產品訂單的架構和訂單的詳細資料。

1. 在 [ **模型** ] 資料夾中，加入名為 *Order.cs*的新類別。   
   新的類別檔案會顯示在編輯器中。
2. 使用下列項目取代預設程式碼：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. 將 *OrderDetail.cs* 類別加入至 [ *模型* ] 資料夾。
4. 使用下列程式碼來取代預設程式碼：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

`Order`和 `OrderDetail` 類別包含定義用於購買和交貨之訂單資訊的架構。

此外，您還需要更新管理實體類別的資料庫內容類別，並提供資料庫的資料存取權。 若要這樣做，您要將新建立的訂單和 `OrderDetail` 模型類別加入至 `ProductContext` 類別。

1. 在 **方案總管**中，尋找並開啟 *ProductCoNtext.cs* 檔案。
2. 將反白顯示的程式碼新增至 *ProductCoNtext.cs* 檔案，如下所示：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

如先前在本教學課程系列中所述， *ProductCoNtext.cs* 檔中的程式碼會新增 `System.Data.Entity` 命名空間，讓您可以存取 Entity Framework 的所有核心功能。 這項功能包含使用強型別物件來查詢、插入、更新和刪除資料的功能。 類別中的上述程式碼會 `ProductContext` 將 Entity Framework 存取新增至新加入的 `Order` 和 `OrderDetail` 類別。

## <a name="adding-checkout-access"></a>新增簽出存取權

Wingtip 玩具範例應用程式可讓匿名使用者在購物車中審查和新增產品。 不過，當匿名使用者選擇購買他們新增至購物車的產品時，他們必須登入網站。 一旦登入之後，他們就可以存取 Web 應用程式的受限制頁面，以處理結帳和購買程式。 這些受限制的頁面都包含在應用程式的 [ *結帳* ] 資料夾中。

### <a name="add-a-checkout-folder-and-pages"></a>新增結帳資料夾和頁面

您現在將建立 *結帳* 資料夾，以及在簽出過程中，客戶將看到的頁面。 您稍後會在本教學課程中更新這些頁面。

1. 在**方案總管**中，以滑鼠右鍵按一下專案名稱 (**Wingtip 玩具**) ，然後選取 [新增**資料夾**]。 

    ![使用 PayPal 簽出及付款-新增資料夾](checkout-and-payment-with-paypal/_static/image1.png)
2. 將新資料夾命名為 *結帳*。
3. 在 [*簽出*] 資料夾上按一下滑鼠右鍵，然後選取 [**加入** - &gt; **新專案**]。 

    ![使用 PayPal 簽出及付款-新專案](checkout-and-payment-with-paypal/_static/image2.png)
4. [ **加入新項目** ] 對話方塊隨即出現。
5. 選取左側的 [ **Visual c #**  - &gt; **Web**範本] 群組。 然後，在中間窗格中，選取 **具有主版頁面的 Web 表單**，並將它命名為 *CheckoutStart .aspx*。 

    ![使用 PayPal 簽出及付款-新增專案對話方塊](checkout-and-payment-with-paypal/_static/image3.png)
6. 同樣地，選取 [ *網站* ] 檔案作為主版頁面。
7. 使用上述相同步驟，將下列其他頁面新增至 *結帳* 資料夾：   

    - CheckoutReview .aspx
    - CheckoutComplete .aspx
    - CheckoutCancel .aspx
    - CheckoutError .aspx

### <a name="add-a-webconfig-file"></a>新增 Web.config 檔案

藉由將新的 *Web.config* 檔案新增至 [ *簽出* ] 資料夾，您就可以限制存取資料夾中包含的所有頁面。

1. 以滑鼠右鍵按一下 [*結帳*] 資料夾，然後選取 [**加入**  - &gt; **新專案**]。  
   [ **加入新項目** ] 對話方塊隨即出現。
2. 選取左側的 [ **Visual c #**  - &gt; **Web**範本] 群組。 然後，在中間窗格中選取 [ **Web 設定檔**]，接受 *Web.config*的預設名稱，然後選取 [ **新增**]。
3. 使用下列內容來取代 *Web.config* 檔案中的現有 XML 內容：  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. 儲存 *Web.config* 檔案。

*Web.config*檔案指定 Web 應用程式的所有未知使用者都必須被拒絕存取 [*簽出*] 資料夾中包含的頁面。 不過，如果使用者已註冊帳戶且已登入，則使用者將會是已知的使用者，並且可以存取 [ *簽出* ] 資料夾中的頁面。

請務必注意，ASP.NET 設定會遵循階層，其中每個 *Web.config* 檔案都會將設定設定套用至其所在的資料夾以及其下的所有子目錄。

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>對專案啟用 SSL

 安全通訊端層 (SSL) 是一種定義的通訊協定，允許 Web 伺服器和 Web 用戶端透過加密，以更安全的方式進行通訊。 未使用 SSL 時，在用戶端和伺服器之間傳送的資料會開放給任何可實體存取網路的人員進行封包探查。 此外，數種常見驗證結構描述在一般的 HTTP 上並不是很安全。 尤其是，基本驗證和表單驗證會傳送未加密的認證。 為了安全的理由，這些驗證結構描述必須使用 SSL。 

1. 在 **方案總管**中，按一下 [ **WingtipToys** ] 專案，然後按 **F4** 顯示 [ **屬性** ] 視窗。
2. 將 **已啟用的 SSL** 變更為 `true` 。
3. 複製 **SSL URL** ，以便稍後使用。   
 `https://localhost:44300/`除非您先前已建立 Ssl 網站 (，否則 SSL URL 將會顯示) 。   
    ![專案屬性](checkout-and-payment-with-paypal/_static/image4.png)
4. 在 **方案總管**中，以滑鼠右鍵按一下 **WingtipToys** 專案，然後按一下 [ **屬性**]。
5. 在左側索引標籤中按一下 [Web] ****。
6. 將 **專案 Url** 變更為使用您稍早儲存的 **SSL Url** 。   
    ![專案 Web 屬性](checkout-and-payment-with-paypal/_static/image5.png)
7. 按 **CTRL+S**儲存頁面。
8. 按 **CTRL+F5** 執行應用程式。 Visual Studio 將會顯示可避開 SSL 警告的選項。
9. 按一下 [ **是** ] 以信任 IIS Express SSL 憑證並繼續。   
    ![IIS Express SSL 憑證資訊](checkout-and-payment-with-paypal/_static/image6.png)  
  隨即顯示一則安全性警告。
10. 按一下 [ **是** ] 將憑證安裝到您的 localhost。   
    ![[安全性警告] 對話方塊](checkout-and-payment-with-paypal/_static/image7.png)  
  瀏覽器視窗隨即出現。

您現在可以使用 SSL 輕鬆地在本機測試 Web 應用程式。

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>新增 OAuth 2.0 提供者

ASP.NET Web Forms 提供成員資格和驗證的增強功能選項。 這些增強功能包括 OAuth。 OAuth 是一種開放式通訊協定，可讓 Web、行動和桌面應用程式以簡單、標準的方法執行安全授權。 ASP.NET Web Forms 範本會使用 OAuth 將 Facebook、Twitter、Google 和 Microsoft 公開為驗證提供者。 雖然本教學課程僅使用 Google 作為驗證提供者，但您可以輕易修改程式碼來使用任何提供者。 實作其他提供者的步驟，與您將在本教學課程中看到的步驟極為類似。

除了驗證，本教學課程也會使用角色來實作授權。 只有您新增至 `canEdit` 角色的使用者才能建立、編輯或刪除連絡人。

> [!NOTE] 
> 
> Windows Live 應用程式只接受作用中網站的即時 URL，所以您無法使用本機網站 URL 來測試登入。

下列步驟可新增 Google 驗證提供者。

1. 開啟 *應用程式 \_ Start\Startup.Auth.cs* 檔。
2. 移除 `app.UseGoogleAuthentication()` 方法中的註解字元，然後此方法會顯示如下： 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. 瀏覽至 [Google Developers Console](https://console.developers.google.com/)。 您還需要使用您的 Google 開發人員電子郵件帳戶 (gmail.com) 登入。 如果您沒有 Google 帳戶，請選取 [ **建立帳戶** ] 連結。   
   接下來，您會看到 [ **Google 開發人員主控台**]。   
    ![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)
4. 按一下 [ **建立專案** ] 按鈕，然後輸入專案名稱和 ID (您可以) 使用預設值。 然後，按一下 [ **協定] 核取方塊** 和 [ **建立** ] 按鈕。  

    ![Google-新增專案](checkout-and-payment-with-paypal/_static/image9.png)

    幾秒鐘內即可建立新的專案，您的瀏覽器便會顯示新的專案頁面。
5. 在左側索引標籤中，按一下 [ **api &amp; 驗證**]，然後按一下 [ **認證**]。
6. 按一下 [在**OAuth**下**建立新的用戶端識別碼**]。   
   [ **建立用戶端識別碼** ] 對話方塊隨即出現。   
    ![Google -  建立用戶端識別碼](checkout-and-payment-with-paypal/_static/image10.png)
7. 在 [ **建立用戶端識別碼** ] 對話方塊中，保留應用程式類型的預設 **Web 應用程式** 。
8. 將 **授權的 JavaScript 來源** 設定為您稍早在本教學課程中使用的 ssl URL (`https://localhost:44300/` 除非您已) 建立其他 ssl 專案。   
   此 URL 會是應用程式的原始來源。 在此範例中，您將僅輸入 localhost 測試 URL。 不過，您可以輸入多個 Url 來考慮 localhost 和生產。
9. 將 [Authorized Redirect URI] **** 設定如下： 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   此值是 ASP.NET OAuth 使用者與 Google OAuth 伺服器進行通訊的 URI。 請記住您在上面使用的 SSL URL (    `https://localhost:44300/` 除非您已) 建立其他 ssl 專案。
10. 按一下 [ **建立用戶端識別碼** ] 按鈕。
11. 在 Google 開發人員主控台的左側功能表上，按一下 [ **同意畫面** ] 功能表項目，然後設定您的電子郵件地址和產品名稱。 當您完成表單時，請按一下 [ **儲存**]。
12. 按一下 [ **api** ] 功能表項目，然後按一下 [ **Google + API**] 旁邊的 [**關閉**] 按鈕。   
    接受此選項將會啟用 Google + API。
13. 您也必須將 **Owin** NuGet 套件更新為版本3.0.0。   
    從 [ **工具** ] 功能表選取 [ **nuget 封裝管理員** ]，然後選取 [ **管理方案的 nuget 套件**]。  
    從 [ **管理 NuGet 封裝** ] 視窗中，尋找 **Owin** 套件並將其更新為版本3.0.0。
14. 在 Visual Studio 中，藉 `UseGoogleAuthentication` 由複製**用戶端識別碼**和**用戶端密碼**並貼到方法中，來更新*Startup.Auth.cs*頁面的方法。 以下所示的 **用戶端識別碼** 和 **用戶端秘密** 值都是範例，因此將無法運作。 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. 按 **CTRL + F5** 來建立並執行應用程式。 按一下 [登入] **** 連結。
16. 在 [ **使用其他服務登入**] 底下，按一下 [ **Google**]。  
    ![登入](checkout-and-payment-with-paypal/_static/image11.png)
17. 如果您需要輸入認證，您會被重新導向至 Google 網站，您可以在此輸入認證。  
    ![Google - 登入](checkout-and-payment-with-paypal/_static/image12.png)
18. 輸入認證之後，系統會提示您將許可權授與您剛才建立的 web 應用程式。  
    ![專案預設服務帳戶](checkout-and-payment-with-paypal/_static/image13.png)
19. 按一下 [接受]。 您現在會重新導向回到**WingtipToys**應用程式的 [**註冊**] 頁面，您可以在其中註冊 Google 帳戶。  
    ![以您的 Google 帳戶註冊](checkout-and-payment-with-paypal/_static/image14.png)
20. 您可以選擇變更用於 Gmail 帳戶的本機電子郵件註冊名稱，但您通常會想保留預設電子郵件別名 (也就是，您用來驗證的名稱)。 按一下 [ **登入** ]，如上所示。

### <a name="modifying-login-functionality"></a>修改登入功能

如先前在本教學課程系列中所述，預設會在 ASP.NET Web Forms 範本中包含大部分的使用者註冊功能。 現在您將修改預設的 *Login .aspx* 並登錄 *.aspx* 頁面，以呼叫 `MigrateCart` 方法。 方法會將 `MigrateCart` 新登入的使用者與匿名購物車產生關聯。 藉由建立使用者和購物車的關聯，Wingtip 玩具範例應用程式將能夠在造訪之間維護使用者的購物車。

1. 在 **方案總管**中，尋找並開啟 [ *帳戶* ] 資料夾。
2. 修改名為 *Login.aspx.cs* 的程式碼後端頁面，以包含以黃色反白顯示的程式碼，使其顯示如下：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. 儲存 *Login.aspx.cs* 檔案。

目前，您可以忽略此方法沒有定義的警告 `MigrateCart` 。 您稍後會在本教學課程中將其新增。

*Login.aspx.cs*程式碼後端檔案支援登入方法。 藉由檢查登入 .aspx 頁面，您會看到此頁面包含 [登入] 按鈕，當您按一下 `LogIn` [在程式碼後端觸發處理常式] 時，就會出現此按鈕。

`Login`呼叫*Login.aspx.cs*上的方法時，會建立名為的購物車的新實例 `usersShoppingCart` 。 購物車的識別碼 (GUID) 會被抓取並設定為 `cartId` 變數。 然後， `MigrateCart` 會呼叫方法， `cartId` 並將登入使用者的名稱和名稱傳遞給這個方法。 購物車遷移後，用來識別匿名購物車的 GUID 就會取代為使用者名稱。

除了修改 *Login.aspx.cs* 程式碼後端檔案，以在使用者登入時遷移購物車，您也必須修改 *Register.aspx.cs 程式碼後端* 檔案，以便在使用者建立新帳戶並登入時遷移購物車。

1. 在 [ *帳戶* ] 資料夾中，開啟名為 *Register.aspx.cs*的程式碼後端檔案。
2. 將程式碼包含在黃色，以修改程式碼後端檔案，使其看起來像這樣：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. 儲存 *Register.aspx.cs* 檔案。 同樣地，請忽略方法的相關警告 `MigrateCart` 。

請注意，您在事件處理常式中使用的程式碼與 `CreateUser_Click` 您在方法中使用的程式碼非常類似 `LogIn` 。 當使用者註冊或登入網站時， `MigrateCart` 就會呼叫方法。

## <a name="migrating-the-shopping-cart"></a>遷移購物車

現在您已更新登入和註冊程式，您可以新增程式碼，以使用方法來遷移購物車 `MigrateCart` 。

1. 在 **方案總管**中，尋找 *邏輯* 資料夾並開啟 *ShoppingCartActions.cs* 類別檔案。
2. 將黃色反白顯示的程式碼新增至 *ShoppingCartActions.cs* 檔案中的現有程式碼，讓 *ShoppingCartActions.cs* 檔案中的程式碼顯示如下：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

`MigrateCart`方法會使用現有的 cartId 來尋找使用者的購物車。 接下來，程式碼會在所有購物車專案之間進行迴圈，並以 `CartId` `CartItem` 登入的使用者名稱取代架構) 所指定的屬性 (。

### <a name="updating-the-database-connection"></a>更新資料庫連接

如果您是使用 **預先** 建立的 Wingtip 玩具範例應用程式來進行本教學課程，則必須重新建立預設的成員資格資料庫。 藉由修改預設連接字串，就會在應用程式下次執行時建立成員資格資料庫。

1. 開啟專案根目錄中的 *Web.config* 檔案。
2. 更新預設連接字串，使其顯示如下：   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>整合 PayPal

PayPal 是以網路為基礎的計費平臺，接受依線上商家付款的款項。 本教學課程接下來將說明如何將 PayPal 的 Express 結帳功能整合到您的應用程式中。 「快速結帳」可讓您的客戶使用 PayPal 來支付已新增至購物車的專案。

### <a name="create-paypal-test-accounts"></a>建立 PayPal 測試帳戶

若要使用 PayPal 測試環境，您必須建立並驗證開發人員測試帳戶。 您將使用開發人員測試帳戶來建立買方測試帳戶和賣方測試帳戶。 開發人員測試帳號憑證也會允許 Wingtip 玩具範例應用程式存取 PayPal 測試環境。

1. 在瀏覽器中，流覽至 PayPal 開發人員測試網站：   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. 如果您沒有 PayPal 開發人員帳戶，請按一下 [ **註冊**] 並遵循註冊步驟來建立新的帳戶。 如果您有現有的 PayPal 開發人員帳戶，請按一下 [ **登入] 登**入。 您將需要 PayPal 開發人員帳戶，才能在本教學課程稍後測試 Wingtip 玩具範例應用程式。
3. 如果您剛剛註冊了 PayPal 開發人員帳戶，您可能需要使用 PayPal 來驗證您的 PayPal 開發人員帳戶。 您可以遵循 PayPal 傳送至您的電子郵件帳戶的步驟來驗證您的帳戶。 確認您的 PayPal 開發人員帳戶之後，請重新登入 PayPal 開發人員測試網站。
4. 使用您的 PayPal 開發人員帳戶登入 PayPal 開發人員網站後，您必須建立 PayPal 買方測試帳戶（如果您還沒有的話）。 若要建立買方測試帳戶，請在 PayPal 網站上按一下 [ **應用程式** ] 索引標籤，然後按一下 [ **沙箱帳戶**]。   
 [ **沙箱測試帳戶** ] 頁面會顯示。   

    > [!NOTE] 
    > 
    > PayPal 開發人員網站已供應商家測試帳戶。

    ![使用 PayPal 簽出及付款-沙箱測試帳戶](checkout-and-payment-with-paypal/_static/image15.png)
5. 在 [沙箱測試帳戶] 頁面上，按一下 [ **建立帳戶**]。
6. 在 [ **建立測試帳戶** ] 頁面上，選擇買方測試帳戶的電子郵件和您選擇的密碼。   

    > [!NOTE] 
    > 
    > 您將需要買方電子郵件地址和密碼，才能在本教學課程結束時測試 Wingtip 玩具範例應用程式。

    ![使用 PayPal 簽出及付款-沙箱測試帳戶](checkout-and-payment-with-paypal/_static/image16.png)
7. 按一下 [ **建立帳戶** ] 按鈕，以建立買方測試帳戶。  
 [ **沙箱測試帳戶** ] 頁面隨即顯示。 

    ![使用 PayPal-PayPal 帳戶簽出及付款](checkout-and-payment-with-paypal/_static/image17.png)
8. 在 [ **沙箱測試帳戶** ] 頁面上，按一下 [ **主持人** ] 電子郵件帳戶。  
    **設定檔** 和 **通知** 選項隨即出現。
9. 選取 [ **設定檔** ] 選項，然後按一下 [ **API 認證** ]，以查看您的商家測試帳戶 api 認證。
10. 將測試 API 認證複製到 [記事本]。

您將需要所顯示的傳統測試 API 認證 (使用者名稱、密碼和簽章) ，以便從 Wingtip 玩具範例應用程式對 PayPal 測試環境進行 API 呼叫。 您將在下一個步驟中新增認證。

### <a name="add-paypal-class-and-api-credentials"></a>新增 PayPal 類別和 API 認證

您會將大部分的 PayPal 程式碼放入單一類別中。 此類別包含用來與 PayPal 進行通訊的方法。 此外，您會將您的 PayPal 認證新增至此類別。

1. 在 Visual Studio 內的 Wingtip 玩具範例應用程式中，以滑鼠右鍵按一下**邏輯**資料夾，然後選取 [**加入**  - &gt; **新專案**]。   
   [ **加入新項目** ] 對話方塊隨即出現。
2. 從左邊的 [**已安裝**] 窗格的 [ **Visual c #** ] 底下，選取 [程式**代碼**]。
3. 在中間窗格中，選取 [ **類別**]。 將這個新類別命名為 **PayPalFunctions.cs**。
4. 按一下 [新增]  。  
   新的類別檔案會顯示在編輯器中。
5. 使用下列程式碼來取代預設程式碼：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. 新增商家 API 認證 (您稍早在本教學課程中所顯示的使用者名稱、密碼和簽章) ，讓您可以對 PayPal 測試環境進行函式呼叫。  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> 在此範例應用程式中，您只需將認證新增至 c # 檔案， ( .cs) 。 不過，在已實施的解決方案中，您應該考慮將設定檔中的認證加密。

NVPAPICaller 類別包含大部分的 PayPal 功能。 類別中的程式碼會提供從 PayPal 測試環境進行測試購買所需的方法。 以下是用來進行購買的三個 PayPal 函數：

- `SetExpressCheckout` 函式
- `GetExpressCheckoutDetails` 函式
- `DoExpressCheckoutPayment` 函式

`ShortcutExpressCheckout`方法會從購物車收集測試購買資訊和產品詳細資料，並呼叫 PayPal 函式 `SetExpressCheckout` 。 `GetCheckoutDetails`方法會先確認購買詳細資料，並呼叫 PayPal 函式， `GetExpressCheckoutDetails` 再進行測試購買。 方法會藉 `DoCheckoutPayment` 由呼叫 PayPal 函式，從測試環境完成測試購買 `DoExpressCheckoutPayment` 。 其餘的程式碼支援 PayPal 方法和程式，例如編碼字串、解碼字串、處理陣列，以及判斷認證。

> [!NOTE] 
> 
> PayPal 可讓您根據 [PayPal 的 API 規格](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)，包含選擇性的購買詳細資料。 藉由擴充 Wingtip 玩具範例應用程式中的程式碼，您可以包含當地語系化詳細資料、產品描述、稅、客戶服務號碼，以及許多其他選擇性欄位。

請注意， **ShortcutExpressCheckout** 方法中指定的傳回和取消 url 會使用通訊埠編號。

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

當 Visual Web Developer 使用 SSL 執行 Web 專案時，通常會使用埠44300作為網頁伺服器。 如上所示，埠號碼為44300。 當您執行應用程式時，您可能會看到不同的埠號碼。 您必須在程式碼中正確設定您的埠號碼，才能在本教學課程結束時成功執行 Wingtip 玩具範例應用程式。 本教學課程的下一節說明如何取出本機主機埠號碼，並更新 PayPal 類別。

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>更新 PayPal 類別中的 LocalHost 埠號碼

Wingtip 玩具範例應用程式會藉由流覽至 PayPal 測試網站，並返回您的 Wingtip 玩具範例應用程式的本機實例，來購買產品。 為了讓 PayPal 回到正確的 URL，您必須在上述的 PayPal 程式碼中指定本機執行範例應用程式的埠號碼。

1. 以滑鼠右鍵按一下 [**方案總管**中的專案名稱 (**WingtipToys**) ]，然後選取 [**屬性**]。
2. 在左側資料行中，選取 [ **Web** ] 索引標籤。
3. 從 [ **專案 Url** ] 方塊中取出埠號碼。
4. 如有需要，請 `returnURL` 更新 `cancelURL` PayPal 類別中的和， (`NVPAPICaller` *PayPalFunctions.cs* 檔中的) ，以使用 web 應用程式的埠號碼：   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

現在，您新增的程式碼將符合您的本機 Web 應用程式所需的埠。 PayPal 將能夠回到您本機電腦上的正確 URL。

### <a name="add-the-paypal-checkout-button"></a>新增 [PayPal 結帳] 按鈕

現在已將主要 PayPal 函式新增至範例應用程式，接下來您可以開始新增呼叫這些函式所需的標記和程式碼。 首先，您必須在 [購物車] 頁面上加入使用者將看到的 [簽出] 按鈕。

1. 開啟 *ShoppingCart .aspx* 檔案。
2. 滾動至檔案底部，然後尋找 `<!--Checkout Placeholder -->` 批註。
3. 將批註取代為 `ImageButton` 控制項，讓 mark 取代如下：  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. 在 *ShoppingCart.aspx.cs* 檔案中，在 `UpdateBtn_Click` 檔案結尾附近的事件處理常式之後，加入 `CheckOutBtn_Click` 事件處理常式：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. 此外，在 *ShoppingCart.aspx.cs* 檔案中，新增的參考 `CheckoutBtn` ，以便參考新的影像按鈕，如下所示：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. 將您的變更儲存至 *ShoppingCart .aspx* 檔和 *ShoppingCart.aspx.cs* 檔案。
7. 從功能表選取 [ **Debug** - &gt; **Build WingtipToys**]。  
   專案將會以新加入的 **ImageButton** 控制項重建。

### <a name="send-purchase-details-to-paypal"></a>將購買詳細資料傳送至 PayPal

當使用者按一下 [購物車] 頁面上的 [ **結帳** ] 按鈕時 (*ShoppingCart .Aspx*) ，他們將開始進行購買程式。 下列程式碼會呼叫購買產品所需的第一個 PayPal 函數。

1. 從 [ *結帳* ] 資料夾中，開啟名為 *CheckoutStart.aspx.cs*的程式碼後端檔案。   
   請務必開啟程式碼後端檔案。
2. 將現有的程式碼取代為下列程式碼：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

當應用程式的使用者按一下 [購物車] 頁面上的 [ **結帳** ] 按鈕時，瀏覽器會流覽至 *CheckoutStart .aspx* 頁面。 當 *CheckoutStart .aspx* 頁面載入時， `ShortcutExpressCheckout` 會呼叫方法。 此時，使用者會轉移至 PayPal 測試網站。 在 PayPal 網站上，使用者會輸入其 PayPal 認證、評論購買詳細資料、接受 PayPal 合約，然後返回此方法完成的 Wingtip 玩具範例應用程式 `ShortcutExpressCheckout` 。 當 `ShortcutExpressCheckout` 方法完成時，它會將使用者重新導向至方法中指定的 *CheckoutReview .aspx* 頁面 `ShortcutExpressCheckout` 。 這可讓使用者在 Wingtip 玩具範例應用程式內檢查訂單詳細資料。

### <a name="review-order-details"></a>審核訂單詳細資料

從 PayPal 傳回之後，Wingtip 玩具範例應用程式的 *CheckoutReview .aspx* 頁面會顯示訂單詳細資料。 此頁面可讓使用者在購買產品之前，先審核訂單詳細資料。 您必須建立 *CheckoutReview .aspx* 頁面，如下所示：

1. 在 [ *結帳* ] 資料夾中，開啟名為 *CheckoutReview*的頁面。
2. 以下列內容取代現有的標記：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. 開啟名為 *CheckoutReview.aspx.cs* 的程式碼後端頁面，並以下列程式碼取代現有的程式碼：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

**DetailsView**控制項是用來顯示從 PayPal 傳回的訂單詳細資料。 此外，上述程式碼會將訂單詳細資料儲存至 Wingtip 玩具資料庫，以做為 `OrderDetail` 物件。 當使用者按一下 [ **完成順序** ] 按鈕時，系統會將他們重新導向至 *CheckoutComplete .aspx* 頁面。

> [!NOTE] 
> 
> **提示**
> 
> 在 *CheckoutReview .aspx* 頁面的標記中，請注意， `<ItemStyle>` 標記是用來變更在頁面底部附近的 **DetailsView** 控制項中專案的樣式。 藉由在 [ **設計檢視** ] 中選取 [ **設計** ] (，方法是選取 Visual Studio) 左下角的 [設計]，然後選取 [ **detailsview** ] 控制項，然後選取 [ **智慧標籤** ] (控制項) 右上方的箭號圖示，您就可以看到 **DetailsView**工作。
> 
> ![使用 PayPal 編輯欄位簽出及付款](checkout-and-payment-with-paypal/_static/image18.png)
> 
> 藉由選取 [ **編輯欄位**]，[ **欄位** ] 對話方塊隨即出現。 在這個對話方塊中，您可以輕鬆地控制**DetailsView**控制項的視覺屬性，例如**ItemStyle**。
> 
> ![使用 PayPal 的欄位對話方塊簽出及付款](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>完成購買

*CheckoutComplete* 可讓您從 PayPal 購買。 如先前所述，使用者必須按一下 [ **完成順序** ] 按鈕，應用程式才會流覽至 *CheckoutComplete .aspx* 頁面。

1. 在 [ *結帳* ] 資料夾中，開啟名為 *CheckoutComplete*的頁面。
2. 以下列內容取代現有的標記：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. 開啟名為 *CheckoutComplete.aspx.cs* 的程式碼後端頁面，並以下列程式碼取代現有的程式碼：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

載入 *CheckoutComplete .aspx* 頁面時， `DoCheckoutPayment` 會呼叫方法。 如先前所述，此 `DoCheckoutPayment` 方法會完成從 PayPal 測試環境進行購買。 一旦 PayPal 完成訂單的購買， *CheckoutComplete* 就會向購買者顯示付款交易 `ID` 。

### <a name="handle-cancel-purchase"></a>處理取消購買

如果使用者決定取消購買，系統會將他們導向至 *CheckoutCancel .aspx* 頁面，其中會顯示其訂單已取消。

1. 開啟 [*簽出*] 資料夾中名為*CheckoutCancel*的頁面。
2. 以下列內容取代現有的標記：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>處理購買錯誤

*CheckoutError*會處理購買程式期間的錯誤。 如果發生錯誤，則 *CheckoutStart .aspx* 頁面的程式碼後端、 *CheckoutReview .Aspx* 頁面和 *CheckoutComplete .aspx* 頁面都會重新導向至 *CheckoutError .aspx* 頁面。

1. 開啟 [*簽出*] 資料夾中名為*CheckoutError*的頁面。
2. 以下列內容取代現有的標記：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

當簽出程式期間發生錯誤時，會顯示 *CheckoutError .aspx* 頁面和錯誤詳細資料。

## <a name="running-the-application"></a>執行應用程式

執行應用程式，以瞭解如何購買產品。 請注意，您將在 PayPal 測試環境中執行。 未交換實際的金錢。

1. 請確定您的所有檔案都儲存在 Visual Studio 中。
2. 開啟網頁瀏覽器並流覽至 [https://developer.paypal.com](https://developer.paypal.com/) 。
3. 使用您稍早在本教學課程中建立的 PayPal 開發人員帳戶登入。  
   若為 PayPal 的開發人員沙箱，您必須登入， [https://developer.paypal.com](https://developer.paypal.com/) 才能測試快速簽出。 這僅適用于 PayPal 的沙箱測試，不適用於 PayPal 的即時環境。
4. 在 Visual Studio 中，按 **F5** 以執行 Wingtip 玩具範例應用程式。  
   資料庫重建之後，瀏覽器會開啟並顯示 *default.aspx* 頁面。
5. 將三個不同的產品新增至購物車，方法是選取產品類別（例如「車輛」），然後按一下每個產品旁的 [ **新增至購物車** ]。  
   購物車會顯示您所選取的產品。
6. 按一下 [ **PayPal** ] 按鈕以簽出。 

    ![使用 PayPal 簽出及付款-購物車](checkout-and-payment-with-paypal/_static/image20.png)

   簽出需要您擁有 Wingtip 玩具範例應用程式的使用者帳戶。
7. 按一下頁面右側的 **Google** 連結，以現有的 gmail.com 電子郵件帳戶登入。  
   如果您沒有 gmail.com 帳戶，您可以在 [www.gmail.com](https://www.gmail.com/)建立一個用於測試用途。 您也可以按一下 [註冊]，以使用標準的本機帳戶。 

    ![使用 PayPal 簽出及付款-登入](checkout-and-payment-with-paypal/_static/image21.png)
8. 使用您的 gmail 帳戶和密碼登入。 

    ![使用 PayPal-Gmail 登入簽出及付款](checkout-and-payment-with-paypal/_static/image22.png)
9. 按一下 [ **登入** ] 按鈕，向您的 Wingtip 玩具範例應用程式使用者名稱註冊您的 gmail 帳戶。 

    ![使用 PayPal 簽出及付款-註冊帳戶](checkout-and-payment-with-paypal/_static/image23.png)
10. 在 PayPal 測試網站上，新增您稍早在本教學課程中建立的 **買方** 電子郵件地址和密碼，然後按一下 [ **登入** ] 按鈕。 

    ![使用 PayPal 簽署及付款-PayPal 登入](checkout-and-payment-with-paypal/_static/image24.png)
11. 同意 PayPal 原則，然後按一下 [ **同意並繼續** ] 按鈕。  
    請注意，只有在您第一次使用此 PayPal 帳戶時，才會顯示此頁面。 同樣地，請注意，這是一個測試帳戶，不會交換真正的金錢。 

    ![使用 PayPal 簽出及付款-PayPal 原則](checkout-and-payment-with-paypal/_static/image25.png)
12. 請參閱 PayPal 測試環境審查頁面上的訂單資訊，然後按一下 [ **繼續**]。 

    ![使用 PayPal 審核資訊簽出及付款](checkout-and-payment-with-paypal/_static/image26.png)
13. 在 [ *CheckoutReview* ] 頁面上，確認訂單數量並查看產生的交貨位址。 然後按一下 [ **完成順序** ] 按鈕。 

    ![使用 PayPal-訂單審核簽出及付款](checkout-and-payment-with-paypal/_static/image27.png)
14. **CheckoutComplete .aspx**頁面會以付款交易識別碼顯示。 

    ![使用 PayPal 簽出及付款-結帳完成](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>檢查資料庫

藉由在執行應用程式之後，在 Wingtip 玩具範例應用程式資料庫中檢查更新的資料，您可以看到應用程式已成功記錄產品的購買。

您可以使用 Visual Studio) 中的**資料庫總管**視窗 (**伺服器總管**視窗，來檢查*Wingtiptoys .mdf*資料庫檔案中包含的資料，就像您先前在本教學課程系列中所做的一樣。

1. 如果瀏覽器視窗仍處於開啟狀態，請關閉瀏覽器視窗。
2. 在 Visual Studio 中，選取**方案總管**頂端的 [**顯示所有**檔案] 圖示，以允許您展開 [**應用程式 \_ 資料**] 資料夾。
3. 展開 [ **應用程式 \_ 資料** ] 資料夾。  
 您可能需要選取該資料夾的 [ **顯示所有** 檔案] 圖示。
4. 以滑鼠右鍵按一下 *Wingtiptoys .mdf* 資料庫檔案，然後選取 [ **開啟**]。  
    **伺服器總管** 隨即顯示。
5. 展開 **[資料表]** 資料夾。
6. 以滑鼠右鍵按一下 [ **Orders**] 資料表，然後選取 [ **顯示資料表資料**]。  
 [ **Orders** ] 資料表隨即顯示。
7. 請參閱 **PaymentTransactionID** 資料行，以確認成功的交易。 

    ![使用 PayPal 簽出及付款-審核資料庫](checkout-and-payment-with-paypal/_static/image29.png)
8. 關閉 [ **Orders** ] 資料表視窗。
9. 在伺服器總管中，以滑鼠右鍵按一下 [ **OrderDetails** ] 資料表，然後選取 [ **顯示資料表資料**]。
10. 檢查 `OrderId` `Username` **OrderDetails** 資料表中的和值。 請注意，這些值符合 `OrderId` `Username` **Orders** 資料表中包含的和值。
11. 關閉 [ **OrderDetails** 資料表] 視窗。
12. 以滑鼠右鍵按一下 Wingtip 玩具資料庫檔案， (*Wingtiptoys* ]) 然後選取 [ **關閉連接**]。
13. 如果您沒有看到 [**方案總管**] 視窗，請按一下 [**伺服器總管**] 視窗底部的**方案總管**，再次顯示**方案總管**。

## <a name="summary"></a>摘要

在本教學課程中，您已新增訂單和訂單詳細資料架構來追蹤產品的購買。 您也將 PayPal 功能整合至 Wingtip 玩具範例應用程式。

## <a name="additional-resources"></a>其他資源

[ASP.NET 設定總覽](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[使用成員資格、OAuth 和 SQL Database 將安全的 ASP.NET Web Forms 應用程式部署至 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure 免費試用版](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>免責聲明

本教學課程包含範例程式碼。 這類範例程式碼是以「原樣」提供，不含任何種類的擔保。 因此，Microsoft 不保證範例程式碼的精確度、完整性或品質。 您同意以您自己的風險使用範例程式碼。 在任何情況下，Microsoft 對於任何範例程式碼、內容，包括但不限於任何範例程式碼中的任何錯誤或遺漏、內容，或是任何因使用任何範例程式碼而產生的任何錯誤或損毀，Microsoft 概不負任何影響。 您將會收到通知，並特此同意保證、儲存和保存 Microsoft 無害，以防任何遺失、索賠遺失、傷害或任何種類的損害，包括不受限制、您張貼、傳輸、使用或依賴的材質（但不限於）所 occasioned 的內容，以及您張貼、傳輸、使用或依賴的部分（但不限於）。

> [!div class="step-by-step"]
> [上一個](shopping-cart.md) 
> [下一步](membership-and-administration.md)
