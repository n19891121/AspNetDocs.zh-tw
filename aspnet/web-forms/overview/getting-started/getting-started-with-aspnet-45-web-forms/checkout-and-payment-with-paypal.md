---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: 使用貝寶結帳和付款 |微軟文件
author: Erikre
description: 本教學系列將教您建構 ASP.NET Web 表單應用程式的基礎知識,使用ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676052"
---
# <a name="checkout-and-payment-with-paypal"></a>簽出與使用 PayPal 付款

由[埃裡克·雷坦](https://github.com/Erikre)

[下載翼尖玩具樣品專案 (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本教學系列將教您使用ASP.NET 4.5 和Microsoft Visual Studio Express 2013 為 Web 構建ASP.NET Web 表單應用程式的基礎知識。 帶有[C# 原始碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案可供本教學系列使用。

本教程介紹如何修改 Wingtip 玩具示例應用程式,以包括使用者授權、註冊和使用 PayPal 付款。 只有登錄的使用者才有權購買產品。 ASP.NET 4.5 Web 窗體專案範本的內建用戶註冊功能已經包含了您需要的大部分內容。 您將添加貝寶快速結帳功能。 在本教學中,您使用的是PayPal開發者測試環境,因此不會轉移任何實際資金。 在本教程結束時,您將通過選擇要添加到購物車的產品、按一下結帳按鈕以及將數據傳輸到 PayPal 測試網站來測試應用程式。 在PayPal測試網站上,您將確認您的運費和付款資訊,然後返回當地的Wingtip玩具樣品應用程式,以確認和完成購買。

有幾個經驗豐富的第三方支付處理器,專門從事在線購物,解決可擴展性和安全性。 ASP.NET開發人員在實施購物和購買解決方案之前應考慮使用第三方支付解決方案的優勢。

> [!NOTE] 
> 
> Wingtip Toys 示例應用程式旨在顯示ASP.NET網路開發人員可用的特定ASP.NET概念和功能。 此示例應用程式未針對可擴充性和安全性方面的所有可能情況進行優化。

## <a name="what-youll-learn"></a>您將學到什麼：

- 如何限制對資料夾中特定頁面的訪問。
- 如何從匿名購物車創建已知的購物車。
- 如何為項目啟用 SSL。
- 如何向專案添加 OAuth 提供程式。
- 如何使用PayPal使用PayPal測試環境購買產品。
- 如何在**詳細資訊查看**控件中顯示來自 PayPal 的詳細資訊。
- 如何更新翼尖玩具應用程序的資料庫與從PayPal獲得的詳細資訊。

## <a name="adding-order-tracking"></a>新增訂單追蹤

在本教學中,您將創建兩個新類來追蹤用戶創建的順序中的數據。 這些課程將跟蹤有關運輸資訊、採購總額和付款確認的數據。

### <a name="add-the-order-and-orderdetail-model-classes"></a>新增訂單及訂單詳細資訊模型類別

在本教學系列的早期,透過*在 「模型」* 資料夾`Category`中`Product`創建`CartItem`、 類別,定義類別、產品和購物車專案的架構。 現在,您將添加兩個新類來定義產品訂單的架構和訂單的詳細資訊。

1. 在**模型「 資料夾**中,添加名為*Order.cs*的新類。   
   新的類文件顯示在編輯器中。
2. 使用下列項目取代預設程式碼：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. 將*OrderDetail.cs*類別加入*模型的資料夾*。
4. 使用下列程式碼來取代預設程式碼：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

`Order`和`OrderDetail`類包含用於定義用於採購和裝運的訂單資訊的架構。

此外,您需要更新管理實體類並提供對資料庫的數據訪問的資料庫上下文類。 為此,您將新創建的 Order`OrderDetail`和模型類`ProductContext`添加到 類中。

1. 在**解決方案資源管理員中**,尋找*並開啟ProductContext.cs*檔案。
2. 將突顯的代碼加入*ProductContext.cs*檔案,如下所示:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

如本教學系列前面所述 *,ProductContext.cs*檔案中的`System.Data.Entity`代碼添加 命名空間,以便您可以存取實體框架的所有核心功能。 此功能包括透過使用強類型物件來查詢、插入、更新和刪除資料的功能。 類中的`ProductContext`上述代碼增加了實體框架對新`Order`添加 的`OrderDetail`類和 類的訪問。

## <a name="adding-checkout-access"></a>新增簽出存取權限

Wingtip玩具範例應用程式允許匿名使用者查看產品並將其添加到購物車中。 但是,當匿名用戶選擇購買他們添加到購物車的產品時,他們必須登錄到網站。 登錄後,他們可以存取處理結帳和購買過程的 Web 應用程式的受限頁面。 這些受限頁面包含在應用程式的*簽出*資料夾中。

### <a name="add-a-checkout-folder-and-pages"></a>新增結帳資料夾與頁面

現在,您將創建 *「簽出*」資料夾以及客戶在結帳過程中將看到的頁面。 本教程稍後將更新這些頁面。

1. 右鍵按一下**解決方案資源管理器**中的專案名稱 (**翼尖玩具**) 並選擇 **「添加新資料夾**」。 

    ![使用 PayPal 結帳和付款 - 新資料夾](checkout-and-payment-with-paypal/_static/image1.png)
2. 已命名新資料夾*簽出*。
3. 右鍵按下*簽出*資料夾,然後選擇「**添加新**-&gt;**專案**」。 

    ![使用PayPal結帳和付款 - 新專案](checkout-and-payment-with-paypal/_static/image2.png)
4. [ **加入新項目** ] 對話方塊隨即出現。
5. 選擇左側的**可視化 C#**  - &gt; **Web**範本組。 然後,從中間窗格中,選擇**帶有母版頁的 Web 窗體**並將其命名為 *「簽出Start.aspx*」。 

    ![使用 PayPal 結帳和付款 - 新增新項目對話框](checkout-and-payment-with-paypal/_static/image3.png)
6. 與之前一樣,選擇*Site.Master*檔作為母版頁。
7. 使用上述相同的步驟將以下其他頁面加入*到 簽出*資料夾:   

    - 簽出審查.aspx
    - 結帳完成.aspx
    - 結帳取消.aspx
    - 結帳錯誤.aspx

### <a name="add-a-webconfig-file"></a>新增 Web.config 檔案

以將新的*Web.config*檔案加入*到 簽出*資料夾,您將能夠限制對資料夾中包含的所有頁面的存取。

1. 右鍵按一*下 簽出*資料夾並選擇「**新增新** -&gt;**專案**」。。  
   [ **加入新項目** ] 對話方塊隨即出現。
2. 選擇左側的**可視化 C#**  - &gt; **Web**範本組。 然後,從中間窗格中,選擇**Web 設定檔**,接受*Web.config*的預設名稱,然後選擇 **「添加**」。
3. 使用下列內容來取代 *Web.config* 檔案中的現有 XML 內容：  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. 儲存 *Web.config* 檔案。

*Web.config 檔案*指定必須拒絕 Web 應用程式的所有未知使用者存*取 簽出*資料夾中的頁面。 但是,如果使用者已註冊了帳戶並登錄了帳戶,則他們將是已知使用者,並有權訪問 *「簽出」* 資料夾中的頁面。

請務必注意,ASP.NET配置遵循層次結構,其中每個*Web.config*檔將配置設置應用於它所在的資料夾及其下的所有子目錄。

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>對專案啟用 SSL

 安全通訊端層 (SSL) 是一種定義的通訊協定，允許 Web 伺服器和 Web 用戶端透過加密，以更安全的方式進行通訊。 未使用 SSL 時，在用戶端和伺服器之間傳送的資料會開放給任何可實體存取網路的人員進行封包探查。 此外，數種常見驗證結構描述在一般的 HTTP 上並不是很安全。 尤其是，基本驗證和表單驗證會傳送未加密的認證。 為了安全的理由，這些驗證結構描述必須使用 SSL。 

1. 在 **「解決方案資源管理器」** 中,按**一下 WingtipToys**專案,然後按**F4**顯示 **「屬性」** 視窗。
2. 將**SSL**`true`變更為 。
3. 複製 **SSL URL** ，以便稍後使用。   
 SSL URL`https://localhost:44300/`將是 除非您以前創建了 SSL 網站(如下所示)。   
    ![專案屬性](checkout-and-payment-with-paypal/_static/image4.png)
4. 在**解決方案資源管理員**中,右鍵按**一下 WingtipToys**專案,然後按下**屬性**。
5. 在左側索引標籤中按一下 [Web] ****。
6. 變更**專案網址**以使用之前保存的**SSL URL。**   
    ![專案 Web 屬性](checkout-and-payment-with-paypal/_static/image5.png)
7. 按 **CTRL+S**儲存頁面。
8. 按**Ctrl+F5**以運行應用程式。 Visual Studio 將會顯示可避開 SSL 警告的選項。
9. 按一下 [ **是** ] 以信任 IIS Express SSL 憑證並繼續。   
    ![IIS Express SSL 憑證資訊](checkout-and-payment-with-paypal/_static/image6.png)  
  隨即顯示一則安全性警告。
10. 按一下 [ **是** ] 將憑證安裝到您的 localhost。   
    ![[安全性警告] 對話方塊](checkout-and-payment-with-paypal/_static/image7.png)  
  瀏覽器視窗隨即出現。

現在,您可以使用 SSL 在本地輕鬆測試 Web 應用程式。

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>新增 OAuth 2.0 提供者

ASP.NET Web Forms 提供成員資格和驗證的增強功能選項。 這些增強功能包括 OAuth。 OAuth 是一種開放式通訊協定，可讓 Web、行動和桌面應用程式以簡單、標準的方法執行安全授權。 ASP.NET Web 表單範本使用 OAuth 公開 Facebook、Twitter、Google 和微軟作為身份驗證供應商。 雖然本教學課程僅使用 Google 作為驗證提供者，但您可以輕易修改程式碼來使用任何提供者。 實作其他提供者的步驟，與您將在本教學課程中看到的步驟極為類似。

除了驗證，本教學課程也會使用角色來實作授權。 只有您新增至 `canEdit` 角色的使用者才能建立、編輯或刪除連絡人。

> [!NOTE] 
> 
> Windows Live 應用程式僅接受工作網站的即時 URL,因此不能使用本地網站 URL 來測試登錄。

下列步驟可新增 Google 驗證提供者。

1. 打開*\_應用啟動\啟動.Auth.cs*檔。
2. 移除 `app.UseGoogleAuthentication()` 方法中的註解字元，然後此方法會顯示如下： 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. 瀏覽至 [Google Developers Console](https://console.developers.google.com/)。 您還需要使用您的 Google 開發人員電子郵件帳戶 (gmail.com) 登入。 如果您沒有 Google 帳戶，請選取 [ **建立帳戶** ] 連結。   
   接下來，您會看到 [ **Google 開發人員主控台**]。   
    ![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)
4. 按下「**建立專案**」 按鈕並輸入專案名稱和 ID(您可以使用預設值)。 然後,按一**下協定複選框**和 **「創建**」按鈕。  

    ![谷歌 - 新專案](checkout-and-payment-with-paypal/_static/image9.png)

    幾秒鐘內即可建立新的專案，您的瀏覽器便會顯示新的專案頁面。
5. 在左方選項卡中,按下**API &amp; auth,** 然後按下**認證 。**
6. 按一下**OAuth**下的**建立新用戶端 ID。**   
   [ **建立用戶端識別碼** ] 對話方塊隨即出現。   
    ![Google -  建立用戶端識別碼](checkout-and-payment-with-paypal/_static/image10.png)
7. 在 **"建立用戶端 ID'** 對話框中,保留應用程式類型的預設**Web 應用程式**。
8. 將**授權的 JavaScript 源**設定為本教學前面使用的`https://localhost:44300/`SSL 網址( 除非您建立了其他 SSL 專案)。   
   此 URL 會是應用程式的原始來源。 在此範例中，您將僅輸入 localhost 測試 URL。 但是,您可以輸入多個 URL 來考慮本地主機和生產。
9. 將 [Authorized Redirect URI] **** 設定如下： 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   此值是 ASP.NET OAuth 使用者與 Google OAuth 伺服器進行通訊的 URI。 請記住上面使用的 SSL`https://localhost:44300/`網址( 除非您創建了其他 SSL 專案)。
10. 按下「**創建用戶端 ID」** 按鈕。
11. 在 Google 開發人員控制台的左側功能表中,按一下 **「同意「螢幕**功能表項,然後設定您的電子郵寄地址和產品名稱。 填寫完表單後,按一下「**保存**」。。
12. 按**下 API**選單項,向下滾動並按**下 Google+ API**旁邊的**關閉**按鈕。   
    接受此選項將啟用 Google+ API。
13. 您還必須將**Microsoft.Owin** NuGet 包更新為 3.0.0 版。   
    從**工具選**單中,選擇**NuGet 套件管理員**,然後選擇 **「管理解決方案的 NuGet 套件**」。  
    從 **「管理 NuGet 包」** 視窗中尋找**Microsoft.Owin**套件並將其更新為版本 3.0.0。
14. 在`UseGoogleAuthentication`Visual Studio 中,通過將 用戶端**ID**和**用戶端機密**複製並貼上到方法中,更新*Startup.Auth.cs*頁的方法。 下面顯示**的用戶端 ID**和**用戶端機密**值是示例,不起作用。 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. 按**CTRL+F5**生成並運行應用程式。 按一下 [登入] **** 連結。
16. 在 **「使用其他服務登入**」下,按**一下 Google**。  
    ![登入](checkout-and-payment-with-paypal/_static/image11.png)
17. 如果您需要輸入認證，您會被重新導向至 Google 網站，您可以在此輸入認證。  
    ![Google - 登入](checkout-and-payment-with-paypal/_static/image12.png)
18. 輸入認證後,系統將提示您向剛剛建立的 Web 應用程式授予許可權。  
    ![專案預設服務帳戶](checkout-and-payment-with-paypal/_static/image13.png)
19. 按下"**接受**"。 現在,您將被重定向回**WingtipToys**應用程式的**註冊**頁面,您可以在其中註冊您的 Google 帳戶。  
    ![以您的 Google 帳戶註冊](checkout-and-payment-with-paypal/_static/image14.png)
20. 您可以選擇變更用於 Gmail 帳戶的本機電子郵件註冊名稱，但您通常會想保留預設電子郵件別名 (也就是，您用來驗證的名稱)。 點選**上所述的登入**。

### <a name="modifying-login-functionality"></a>變更登入功能

如本教學系列前面所述,預設情況下,ASP.NET Web 窗體範本中已包含許多用戶註冊功能。 現在,您將修改預設*的 Login.aspx*和*Register.aspx*`MigrateCart`頁面來調用該方法。 該方法`MigrateCart`將新登錄的使用者與匿名購物車關聯。 通過將使用者和購物車關聯,Wingtip 玩具示例應用程式將能夠在訪問之間維護用戶的購物車。

1. 在**解決方案資源管理員中**,尋找 *「帳戶」* 資料夾。
2. 修改名為*Login.aspx.cs*的代碼後面頁,以包括以黃色突出顯示的代碼,以便如下所示:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. 保存*Login.aspx.cs*檔。

現在,您可以忽略方法沒有定義的警告`MigrateCart`。 您將在本教程稍後添加它。

*Login.aspx.cs*代碼背後的文件支援登錄方法。 通過檢查 Login.aspx 頁面,您將看到此頁面包含一個「登錄」按鈕,按下該按鈕會在代碼`LogIn`後面的 處理程式觸發該按鈕。

呼叫Login.aspx.cs`Login`上的方法*Login.aspx.cs*時,將創建`usersShoppingCart`名為購物車的新實例。 購物車 (GUID) 的 ID 將檢`cartId`索並設置為 變數。 然後,調用`MigrateCart`該方法,將登錄`cartId`使用者和登錄使用者的名稱傳遞給此方法。 遷移購物車時,用於標識匿名購物車的 GUID 將替換為使用者名。

除了修改*Login.aspx.cs*代碼背後的檔以在使用者登錄時遷移購物車外,還必須修改*Register.aspx.cs代碼背後的檔*,以在使用者創建新帳戶並登錄時遷移購物車。

1. 在 *「帳戶」* 資料夾中,打開名為*Register.aspx.cs*的碼隱藏檔。
2. 以將代碼以黃色表示修改代碼後檔,以便它如下所示:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. 保存*Register.aspx.cs*檔。 再次忽略有關方法的警告`MigrateCart`。

請注意,在`CreateUser_Click`事件處理程式中使用的代碼與方法中使用的`LogIn`代碼非常相似。 當使用者註冊或登入網站時,將呼叫該方法`MigrateCart`。

## <a name="migrating-the-shopping-cart"></a>遷移購物車

現在,您已經更新了登錄和註冊過程,您可以添加代碼以使用方法`MigrateCart`遷移購物車。

1. 在**解決方案資源管理員**中,尋找*邏輯*資料夾並打開*ShoppingCartActions.cs*類檔。
2. 將以黃色突顯的代碼加入*到 ShoppingCartActions.cs*檔案中的現有代碼,以便*ShoppingCartActions.cs*檔案中的程式碼如下所示:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

該方法`MigrateCart`使用現有的購物車 Id 查找使用者的購物車。 接下來,代碼迴圈遍歷所有購物車專案,`CartId`並將屬性(`CartItem`由架構指定)替換為登錄的使用者名。

### <a name="updating-the-database-connection"></a>更新資料庫連線

如果您使用**預建**建的 Wingtip Toys 範例應用程式遵循本教學,則必須重新建立預設成員資格資料庫。 通過修改預設連接字串,將在下次應用程式運行時創建成員資料庫。

1. 開啟專案根目錄的*Web.config*檔。
2. 更新預設連接字串,使其如下所示:   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>整合貝寶

PayPal 是一個基於 Web 的計費平臺,接受在線商家的付款。 本教程接下來將介紹如何將 PayPal 的快速結帳功能集成到您的應用程式中。 快速結帳允許您的客戶使用 PayPal 支付已添加到購物車中的商品。

### <a name="create-paypal-test-accounts"></a>建立貝寶測試帳戶

要使用 PayPal 測試環境,必須創建並驗證開發人員測試帳戶。 您將使用開發人員測試帳戶創建買方測試帳戶和賣方測試帳戶。 開發人員測試帳戶認證使用者將允許翼尖玩具範例應用程式存取 PayPal 測試環境。

1. 在瀏覽器中,導航到 PayPal 開發人員測試網站:   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. 如果您沒有 PayPal 開發者帳戶,請通過單擊 **「註冊」** 並按照註冊步驟創建新帳戶。 如果您有現有的 PayPal 開發者帳戶,請通過單擊「**登錄**」 登錄。 您將需要您的PayPal開發者帳戶來測試翼尖玩具範例應用程式稍後在本教程。
3. 如果您剛剛註冊了您的PayPal開發者帳戶,您可能需要使用PayPal驗證您的PayPal開發者帳戶。 您可以按照 PayPal 發送到您的電子郵件帳戶的步驟驗證您的帳戶。 驗證您的PayPal開發者帳戶後,請返回PayPal開發者測試網站。
4. 使用 PayPal 開發者帳戶登錄 PayPal 開發者網站後,如果您還沒有,則需要創建 PayPal 買家測試帳戶。 要創建買家測試帳戶,在 PayPal 網站上單擊 **「應用程式**」選項卡,然後單擊 **「沙箱帳戶**」。   
 將顯示沙**盒測試帳戶**頁面。   

    > [!NOTE] 
    > 
    > PayPal 開發者網站已經提供了商家測試帳戶。

    ![使用 PayPal 結帳和付款 - 沙箱測試帳戶](checkout-and-payment-with-paypal/_static/image15.png)
5. 在沙箱測試帳戶頁上,按一下「**創建帳戶**」。
6. 在 **「建立測試帳戶」** 頁上選擇買家測試帳戶電子郵件和您選擇的密碼。   

    > [!NOTE] 
    > 
    > 您將需要買家電子郵件地址和密碼來測試翼尖玩具示例應用程式在本教程的末尾。

    ![使用 PayPal 結帳和付款 - 沙箱測試帳戶](checkout-and-payment-with-paypal/_static/image16.png)
7. 通過按下 **「創建帳戶**」按鈕創建買方測試帳戶。  
 將顯示 **「沙箱測試帳戶」** 頁。 

    ![使用貝寶結帳和付款 - 貝寶帳戶](checkout-and-payment-with-paypal/_static/image17.png)
8. 在**沙箱測試帳戶**頁面上,單擊**主持人**電子郵件帳戶。  
    將顯示**設定檔**和**通知**選項。
9. 選擇 **「設定檔」** 選項,然後單擊**API 認證的**以查看商家測試帳戶的 API 認證。
10. 將 TEST API 認證複製到記事本。

您需要顯示的經典測試 API 認證(使用者名稱、密碼和簽名)才能從 Wingtip Toys 範例應用程式向 PayPal 測試環境進行 API 呼叫。 您將在下一步中添加憑據。

### <a name="add-paypal-class-and-api-credentials"></a>新增貝寶類和 API 認證

您將將大多數 PayPal 代碼放入單個類中。 此類包含用於與 PayPal 通信的方法。 此外,您將將您的 PayPal 認證到此類。

1. 在 Visual Studio 中的 Wingtip 玩具範例應用程式中,右鍵單擊**邏輯**資料夾,然後選擇「**添加新** -&gt;**專案**」 。。   
   [ **加入新項目** ] 對話方塊隨即出現。
2. 在左側 **「已安裝**」窗格中的 **「可視 C#」** 下,選擇 **「代碼**」 。。
3. 從中間窗格中,選擇 **"類**"。 PayPalFunctions.cs命名此新**類。**
4. 按一下 **[新增]**。  
   新的類文件顯示在編輯器中。
5. 使用下列程式碼來取代預設程式碼：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. 添加您在本教程前面顯示的商家 API 認證(使用者名稱、密碼和簽名),以便您可以對 PayPal 測試環境進行函數調用。  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> 在此範例應用程式中,您只需向 C# 檔 (.cs) 添加認證。 但是,在實施的解決方案中,應考慮在配置檔中加密憑據。

NVPAPICaller 類包含大多數 PayPal 功能。 類中的代碼提供了從 PayPal 測試環境進行測試購買所需的方法。 以下三個 PayPal 功能用於購買:

- `SetExpressCheckout` 函式
- `GetExpressCheckoutDetails` 函式
- `DoExpressCheckoutPayment` 函式

該方法`ShortcutExpressCheckout`從購物車收集測試購買資訊和產品詳細資訊,並調`SetExpressCheckout`用 PayPal 功能。 該方法`GetCheckoutDetails`確認購買詳細資訊,並在進行`GetExpressCheckoutDetails`測試 購買之前調用 PayPal 功能。 該方法`DoCheckoutPayment`通過調用 PayPal 函數完成從測試環境`DoExpressCheckoutPayment`中購買的 測試。 其餘代碼支援 PayPal 方法和進程,例如編碼字串、解碼字串、處理陣列和確定認證。

> [!NOTE] 
> 
> PayPal允許您根據[PayPal 的API規範](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)包括可選的購買詳細資訊。 通過延伸 Wingtip Toys 範例應用程式中的代碼,您可以包括本地化詳細資訊、產品描述、稅金、客戶服務編號以及許多其他可選欄位。

請注意,**在快捷方式 ExpressCheckout**方法中指定的傳回和取消 URL 使用埠號。

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

當可視化 Web 開發人員使用 SSL 執行 Web 專案時,埠 44300 通常用於 Web 伺服器。 如上所述,埠號為 44300。 運行應用程式時,可以看到不同的埠號。 您的埠號需要在代碼中正確設置,以便您可以在本教程末尾成功運行 Wingtip Toys 示例應用程式。 本教程的下一部分將介紹如何檢索本地主機埠號並更新 PayPal 類。

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>更新 PayPal 類別的本地主機連接埠號

翼尖玩具樣品應用程式購買產品通過導航到PayPal測試網站,並返回到您的本地實例的Wingtip玩具樣品應用程式。 為了使 PayPal 傳回到正確的 URL,您需要在上面提到的 PayPal 代碼中指定本機執行的範例應用程式的連接埠號。

1. 右鍵按下**解決方案資源管理員**中的項目名稱 (**WingtipToys)** 並選擇**屬性**。
2. 在左列中,選擇 **「Web」** 選項卡。
3. 從 **「專案 Url」** 框中檢索埠號。
4. 如果需要,請更新*PayPalFunctions.cs*檔案`cancelURL`中的 PayPal 類別`NVPAPICaller`( ) 中的`returnURL`與, 以使用 Web 應用程式的連接埠號:   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

現在,您添加的代碼將與本地 Web 應用程式的預期連接埠匹配。 PayPal 將能夠返回到您本地電腦上的正確 URL。

### <a name="add-the-paypal-checkout-button"></a>新增貝寶結帳按鈕

現在,主要 PayPal 函數已添加到範例應用程式中,您可以開始添加調用這些函數所需的標記和代碼。 首先,您必須添加使用者將在購物車頁面上看到的結帳按鈕。

1. 打開*購物車.aspx*檔。
2. 捲動到檔案底部並找到`<!--Checkout Placeholder -->`註解。
3. 將註釋取代為`ImageButton`控制項,以便按照以下的標記:  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. 在*ShoppingCart.aspx.cs*檔案中`UpdateBtn_Click`,在檔案末尾的事件處理程式之後`CheckOutBtn_Click`,新增事件處理程式:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. 此外,在*ShoppingCart.aspx.cs*檔案中,添加`CheckoutBtn`對的引用,以便引用新的圖像按鈕如下:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. 將更改保存到*ShoppingCart.aspx*檔和*ShoppingCart.aspx.cs*檔。
7. 從選單中,選擇**除錯**-&gt;**建構翼尖玩具**。  
   該專案將使用新添加的**ImageButton**控制件進行重建。

### <a name="send-purchase-details-to-paypal"></a>向貝寶傳送購買詳情

當使用者單擊購物車頁面上的 **「結帳**」按鈕 *(ShoppingCart.aspx)* 時,他們將開始購買過程。 以下代碼調用購買產品所需的第一個 PayPal 函數。

1. 從*簽出*資料夾中,打開名為*CheckoutStart.aspx.cs*的代碼隱藏檔。   
   請務必打開代碼背後的檔。
2. 將現有的程式碼取代為下列程式碼：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

當應用程式的使用者按一下購物車頁面上的 **「簽出**」按鈕時,瀏覽器將導航到 *「結帳開始」.aspx*頁面。 當*簽出Start.aspx*頁面載入`ShortcutExpressCheckout`時, 將調用該方法。 此時,使用者將轉移到 PayPal 測試網站。 在PayPal網站上,使用者輸入其PayPal憑據,查看購買詳情,接受PayPal協定,並返回到`ShortcutExpressCheckout`方法完成端的 Wingtip 玩具示例應用程式。 方法完成後,它將使用者重定向到`ShortcutExpressCheckout`方法中指定的*CheckoutReview.aspx*頁面。 `ShortcutExpressCheckout` 這允許使用者從翼尖玩具示例應用程式中查看訂單詳細資訊。

### <a name="review-order-details"></a>檢視訂單詳細資訊

從PayPal返回後,Wingtip玩具示例應用程式的*結帳審查.aspx*頁面將顯示訂單詳細資訊。 此頁面允許使用者在購買產品之前查看訂單詳細資訊。 "*結帳審核.aspx"* 頁必須建立如下:

1. 在 *「簽出」* 資料夾中,打開名為 *「簽出Review.aspx」的*頁面。
2. 將現有標記取代為以下內容:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. 開啟名為*CheckoutReview.aspx.cs*的代碼後面頁,並將現有代碼取代為以下內容:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

**"詳細資訊視圖"** 控制件用於顯示從 PayPal 返回的訂單詳細資訊。 此外,上述代碼將訂單詳細資訊作為`OrderDetail`物件保存到 Wingtip Toys 資料庫。 當使用者按下「**完成訂單」** 按鈕時,他們將重定向到 *「結帳完成.aspx」* 頁。

> [!NOTE] 
> 
> **提示**
> 
> 在 *"結帳Review.aspx"* 頁的標記中,請`<ItemStyle>`注意該 標記用於更改頁面底部附近的 **「詳細資訊查看」** 控制件中的項樣式。 通過在 **「設計檢視**」中查看頁面(透過在 Visual Studio 的左下角選擇 **「設計**」),然後選擇 **「詳細資訊檢視」** 控制項,然後選擇**智慧標記**(控制器右上角的箭頭圖示),您將能夠看到 **「詳細資訊查看任務**」 。。
> 
> ![使用 PayPal 結帳和付款 - 編輯欄位](checkout-and-payment-with-paypal/_static/image18.png)
> 
> 通過選擇 **「編輯欄位**」,「**欄位」** 對話框將顯示。 在此對話框中,您可以輕鬆地控制 **「詳細資訊檢視」** 控制件的可視屬性,如**ItemStyle。**
> 
> ![使用 PayPal 結帳和付款 - 欄位對話框](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>完成購買

*結帳完成.aspx*頁面從 PayPal 進行購買。 如上所述,用戶必須先按下 **「完成訂單」** 按鈕,應用程式才能導航到 *「結帳完成.aspx」* 頁。

1. 在 *「簽出」* 資料夾中,打開名為 *「簽出完成.aspx」* 的頁面。
2. 將現有標記取代為以下內容:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. 開啟名為*CheckoutComplete.aspx.cs*的代碼後面頁,並將現有代碼取代為以下內容:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

載入*簽出完成.aspx*頁`DoCheckoutPayment`時, 將調用 該方法。 如前所述,`DoCheckoutPayment`該方法完成了從PayPal測試環境的購買。 一旦PayPal完成訂單的購買,「*結帳完成.aspx」* 頁面向購買者顯示付款`ID`交易記錄 。

### <a name="handle-cancel-purchase"></a>處理取消購買

如果用戶決定取消購買,他們將被定向到 *「結帳取消.aspx」* 頁面,在那裡他們將看到他們的訂單已被取消。

1. 在 *「簽出*」資料夾中打開名為 *「簽出取消取消.aspx」* 的頁面。
2. 將現有標記取代為以下內容:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>處理購買錯誤

購買過程中的錯誤將由 *「結帳錯誤.aspx」* 頁處理。 如果出現錯誤,"*結帳開始.aspx"* 頁、*結帳審核.aspx*頁和 *"結帳完成.aspx"* 頁的代碼將分別重定向到 *"結帳錯誤.aspx"* 頁。

1. 在*簽出*資料夾中打開名為 *「簽出錯誤.aspx」* 的頁面。
2. 將現有標記取代為以下內容:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

*簽出錯誤.aspx*頁面在結帳過程中發生錯誤時顯示錯誤詳細資訊。

## <a name="running-the-application"></a>執行應用程式

運行應用程式以查看如何購買產品。 請注意,您將在 PayPal 測試環境中運行。 沒有實際資金被兌換。

1. 請確保所有檔都保存在可視化工作室中。
2. 開啟網頁瀏覽器並瀏[https://developer.paypal.com](https://developer.paypal.com/)覽到 。
3. 使用您在本教程中之前創建的 PayPal 開發者帳戶登錄。  
   對於 PayPal 的開發人員沙箱,您[https://developer.paypal.com](https://developer.paypal.com/)需要登錄 以測試快速結帳。 這僅適用於貝寶的沙箱測試,不適用於PayPal的現場環境。
4. 在視覺工作室中,按**F5**運行翼尖玩具示例應用程式。  
   重建資料庫後,瀏覽器將打開並顯示*Default.aspx*頁面。
5. 通過選擇產品類別(如"汽車",然後單擊每個產品旁邊的 **「添加到購物車**」),將三種不同的產品添加到購物車中。  
   購物車將顯示您選擇的產品。
6. 按下 **「貝寶**」按鈕進行結帳。 

    ![使用PayPal結帳和付款 - 購物車](checkout-and-payment-with-paypal/_static/image20.png)

   簽出需要您擁有翼尖玩具範例應用程式的使用者帳戶。
7. 按一下頁面右側的**Google**連結,使用現有的gmail.com電子郵件帳戶登錄。  
   如果您沒有gmail.com帳戶,則可以在[www.gmail.com](https://www.gmail.com/)創建一個帳戶用於測試目的。 您也可以通過按一下「註冊」使用標準本地帳戶。 

    ![使用 PayPal 結帳和付款 - 登入](checkout-and-payment-with-paypal/_static/image21.png)
8. 使用 gmail 帳戶和密碼登錄。 

    ![使用PayPal結帳和付款 - Gmail登錄](checkout-and-payment-with-paypal/_static/image22.png)
9. 單擊**登錄**按鈕,使用翼尖玩具示例應用程式用戶名註冊您的 gmail 帳戶。 

    ![使用PayPal結帳和付款 - 註冊帳戶](checkout-and-payment-with-paypal/_static/image23.png)
10. 在 PayPal 測試網站上,添加您在本教學中之前創建的**買家**電子郵件地址和密碼,然後按一**下 「登錄**」按鈕。 

    ![使用貝寶結帳和付款 - 貝寶登錄](checkout-and-payment-with-paypal/_static/image24.png)
11. 同意 PayPal 政策,然後單擊 **「同意並繼續」** 按鈕。  
    請注意,此頁面僅在您首次使用此 PayPal 帳戶時顯示。 再次注意,這是一個測試帳戶,沒有真正的錢交換。 

    ![使用貝寶結帳和付款 - 貝寶政策](checkout-and-payment-with-paypal/_static/image25.png)
12. 查看 PayPal 測試環境審核頁面上的訂單資訊,然後單擊"**繼續**"。 

    ![使用 PayPal 結帳和付款 - 查看資訊](checkout-and-payment-with-paypal/_static/image26.png)
13. 在 *「結帳審核.aspx」* 頁上,驗證訂單金額並查看生成的送貨位址。 然後,按一下完成**訂單**"按鈕。 

    ![使用 PayPal 結帳和付款 - 訂單稽核](checkout-and-payment-with-paypal/_static/image27.png)
14. **"結帳完成.aspx"** 頁將顯示付款交易記錄 ID。 

    ![使用 PayPal 結帳和付款 - 結帳完成](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>檢視資料庫

通過在運行應用程式後查看 Wingtip Toys 範例應用程式資料庫中的更新數據,您可以看到應用程式已成功記錄產品的購買。

您可以使用**資料庫資源管理員**視窗(Visual Studio 中的**伺服器資源管理員**視窗)來檢查*Wingtiptoys.mdf*資料庫檔中的數據,就像本教學系列前面所做的那樣。

1. 如果瀏覽器視窗仍然打開,則關閉它。
2. 在視覺化工作室中,選擇**解決方案資源管理員**頂部的 **「顯示所有檔**」圖示,以允許您展開**\_應用資料**資料夾。
3. 展開**應用\_數據**資料夾。  
 您可能需要為資料夾選擇「**顯示所有檔案**」 圖示。
4. 右鍵按*一下 Wingtiptoys.mdf*資料庫檔案,然後選擇 **「打開**」。  
    將顯示**伺服器資源管理員**。
5. 展開 **[資料表]** 資料夾。
6. 右鍵按**下 「訂單**」表併選擇 **「顯示表數據**」。  
 將顯示 **「訂單**」表。
7. 查看 **"付款交易ID"** 列以確認成功交易。 

    ![使用 PayPal 結帳和付款 - 稽核資料庫](checkout-and-payment-with-paypal/_static/image29.png)
8. 關閉**訂單**表視窗。
9. 在「伺服器資源管理器」中,右鍵按下 **「訂單詳細資訊**」表併選擇 **「顯示表數據**」 。
10. 查看 **「訂單詳細資訊**」表中`OrderId`的`Username`和值。 請注意,這些值與 **「訂單」** 表中`OrderId`包括`Username`的和值匹配。
11. 關閉 **「訂單詳細資訊**」表視窗。
12. 右鍵按一下 Wingtip 玩具資料庫檔案 *(Wingtiptoys.mdf),* 然後選擇 **「關閉連接**」 。
13. 如果看不到**解決方案資源管理員**視窗,請按下**伺服器資源管理員**視窗底部**的解決方案資源管理員**,以再次顯示**解決方案資源管理員**。

## <a name="summary"></a>總結

在本教程中,您添加了訂單和訂單詳細資訊架構,以跟蹤產品的購買情況。 您還可以將 PayPal 功能整合到翼尖玩具範例應用程式中。

## <a name="additional-resources"></a>其他資源

[ASP.NET 設定概述](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[將具有成員資格、OAuth 和 SQL 資料庫的安全ASP.NET Web 窗體應用部署到 Azure 應用服務](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[微軟 Azure - 免費試用](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>免責聲明

本教程包含示例代碼。 此類示例代碼提供"有效",不提供任何形式的擔保。 因此,Microsoft 不保證範例代碼的準確性、完整性或品質。 您同意自行承擔使用示例代碼的風險。 在任何情況下,Microsoft 均不對任何範例代碼、內容(包括但不限於任何範例代碼、內容中的任何錯誤或遺漏)或因使用任何示例代碼而造成的任何損失或損壞承擔任何責任。 特此通知您並同意對 Microsoft 的任何和所有損失、任何損失、傷害或損害索賠進行賠償、保存和保持無害,包括但不限於您發佈、傳輸、使用或依賴的材料引起的或由您所表達的意見引起的或產生的損失、傷害或損害。

> [!div class="step-by-step"]
> [前一個](shopping-cart.md)
> [下一個](membership-and-administration.md)
