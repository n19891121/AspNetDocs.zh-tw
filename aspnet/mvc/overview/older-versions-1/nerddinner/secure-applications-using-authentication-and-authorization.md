---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 使用認證與授權的安全應用程式 。微軟文件
author: rick-anderson
description: 步驟 9 演示如何添加身份驗證和授權來保護我們的 NerdDinner 應用程式,以便使用者需要註冊並登錄到網站以創建...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: d96f2763f6e62f9dd599fdb7977a97993d218305
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542569"
---
# <a name="secure-applications-using-authentication-and-authorization"></a>保護使用驗證和授權的應用程式

由[微軟](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第9步,該教程示範如何使用mVC 1 構建小型但完整的 Web 應用程式ASP.NET。
> 
> 步驟 9 演示如何添加身份驗證和授權來保護我們的 NerdDinner 應用程式,以便使用者需要註冊並登錄到網站以創建新的晚餐,並且只有主持晚宴的使用者才能稍後對其進行編輯。
> 
> 如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。

## <a name="nerddinner-step-9-authentication-and-authorization"></a>神經晚餐步驟 9:身份驗證和授權

現在,我們的NerdDinner應用程式允許任何訪問該網站的人能夠創建和編輯任何晚餐的細節。 讓我們更改此內容,以便使用者需要註冊並登錄到網站以創建新的晚餐,並添加限制,以便只有主持晚宴的使用者才能稍後對其進行編輯。

為了啟用此功能,我們將使用身份驗證和授權來保護我們的應用程式。

### <a name="understanding-authentication-and-authorization"></a>瞭解認證與授權

*身份驗證*是標識和驗證訪問應用程式的客戶端的標識的過程。 簡單地說,它是關於確定最終使用者在訪問網站時的"誰"。 ASP.NET支援對瀏覽器使用者進行身份驗證的多種方法。 對於 Internet Web 應用程式,最常用的身份驗證方法稱為"表單身份驗證」。。 表單身份驗證使開發人員能夠在其應用程式中創作 HTML 登入表單,然後根據資料庫或其他密碼認證認證最終使用者提交的使用者名/密碼。 如果使用者名/密碼組合正確,開發人員可以請求ASP.NET發出加密的 HTTP Cookie,以識別使用者在未來的請求。 我們將使用表單身份驗證來使用我們的NerdDinner應用程式。

*授權*是確定經過身份驗證的使用者是否具有訪問特定 URL/資源或執行某些操作的許可權的過程。 例如,在我們的NerdDinner應用程式中,我們希望授權只有登錄的使用者才能訪問 */Dinners/創建*URL並創建新的晚餐。 我們還希望添加授權邏輯,以便只有主持晚宴的使用者才能對其進行編輯,並拒絕對所有其他使用者進行編輯訪問。

### <a name="forms-authentication-and-the-accountcontroller"></a>表單識別識別和帳戶控制器

ASP.NET MVC 的預設 Visual Studio 專案範本在創建新 ASP.NET MVC 應用程式時自動啟用表單身份驗證。 它還會自動向專案添加預構建的帳戶登錄頁實現,從而在網站中集成安全性非常容易。

預設的 Site.master 頁在網站右上角顯示「登錄」連結,當使用者存取該網站時未進行身份驗證:

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

點選「登入」連結會將使用者帶到 */帳戶/登錄*URL:

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

尚未註冊的存取者可以透過按下「註冊」連結(該連結將他們帶到 */帳戶/註冊*URL)並允許您輸入帳戶詳細資訊來執行此操作:

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

按下「註冊」按鈕將在ASP.NET成員資格系統中創建新使用者,並使用表單身份驗證對使用者進行身份驗證。

當使用者登錄時,Site.master 會更改頁面的右上角以輸出「歡迎 [使用者名]! 消息並呈現「註銷」連結,而不是「登錄」連結。 點選「登出」連結會登出使用者:

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

上述登錄、註銷和註冊功能在帳戶控制器類中實現,該類在創建專案時由 Visual Studio 添加到我們的專案中。 帳號控制器的 UI 使用 [Views_帳戶目錄中的檢視範本] 實現:

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

帳戶控制器類使用ASP.NET表單身份驗證系統來發出加密的身份驗證 Cookie,ASP.NET成員資格 API 來存儲和驗證使用者名/密碼。 ASP.NET成員資格 API 是可擴展的,並且允許使用任何密碼憑據存儲。 ASP.NET附帶將使用者名/密碼存儲在 SQL 資料庫或活動目錄中的內置成員資格提供程式實現。

我們可以通過打開專案根目錄的"Web.config"檔並在其中查找&lt;成員&gt;資格 部分來配置我們的NerdDinner應用程式應該使用的成員供應商。 創建專案時添加的預設 Web.config 會註冊 SQL 成員資格提供程式,並將其配置為使用名為"應用程式服務"的連接字串來指定資料庫位置。

預設的「應用程式服務」 連接字串(在 Web.config&lt;&gt;檔案的連接字串部分中指定)設定為使用 SQL Express。 它指向名為「ASPNETDB」的 SQL Express 資料庫。MDF"在應用程式的"應用\_資料"目錄下。 如果首次在應用程式中使用成員資格 API 時此資料庫不存在,ASP.NET將自動建立資料庫並在其中預配適當的成員資格資料庫架構:

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

如果我們不想使用 SQL Express,而是想要使用完整的 SQL Server 實例(或連接到遠端資料庫),我們只需更新 Web.config 檔中的「應用程式服務」連接字串,並確保適當的成員資格架構已添加到它指向的資料庫。 您可以在 [Windows_Microsoft.NET_Framework_v2.0.50727] 目錄中運行"aspnet\_regsql.exe"實用程式,以將成員資格和其他ASP.NET應用程式服務的適當架構添加到資料庫中。

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>使用授權帳號授權 /Dinners/建立 URL

我們不必編寫任何代碼來為NerdDinner應用程式啟用安全的身份驗證和帳戶管理實現。 用戶可以在我們的應用程式中註冊新帳戶,以及網站登錄/註銷。

現在,我們可以向應用程式添加授權邏輯,並使用訪問者的身份驗證狀態和使用者名來控制他們在網站內可以做什麼和不能做什麼。 讓我們首先將授權邏輯添加到 DinnersController 類的"創建"操作方法。 具體來說,我們將要求訪問 */Dinner/Create* URL 的用戶必須登錄。 如果他們沒有登錄,我們會將其重定向到登錄頁面,以便他們可以登錄。

實現此邏輯非常簡單。 我們只需要將 [授權] 篩選器屬性添加到我們的"創建操作方法"中,如下所示:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC 支援建立「操作篩選器」的能力,該篩選器可用於實現可聲明應用於操作方法的可重用邏輯。 [授權] 篩選器是 ASP.NET MVC 提供的內建操作篩選器之一,它使開發人員能夠聲明授權規則應用於操作方法和控制器類。

在沒有任何參數的情況下應用時(如上文所述),[授權] 篩選器強制必須登錄執行操作方法請求的使用者,如果瀏覽器未登錄,則會自動將瀏覽器重定向到登錄 URL。 執行此操作重定向時,最初請求的 URL 將作為查詢字串參數傳遞(例如:/帳戶/LogOn?傳回Url_%2fDinners%2f創建)。 然後,帳戶控制器將在使用者登錄后將使用者重定向回最初請求的 URL。

[授權] 篩選器可以選擇支援指定"使用者"或"角色"屬性的能力,該屬性可用於要求使用者同時登錄並登錄允許的使用者或允許的安全角色的成員清單中。 例如,下面的代碼只允許兩個特定使用者「scottgu」和「billg」訪問 /Dinners/Create URL:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

不過,在代碼中嵌入特定的使用者名往往非常無法維護。 更好的方法是定義代碼所針對的更高級別的"角色",然後使用資料庫或活動目錄系統將使用者映射到角色(使實際使用者映射清單能夠從代碼外部存儲)。 ASP.NET包括內建角色管理 API 以及一組內建角色提供者(包括 SQL 和 Active Directory 的內建角色提供者),可幫助執行此使用者/角色映射。 然後,我們可以更新代碼,僅允許特定「管理員」角色中的使用者訪問 /Dinners/Create URL:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>建立晚餐時使用User.Identity.Name屬性

我們可以使用 Controller 基類上公開的 User.Identity.Name 屬性檢索請求當前登錄使用者的使用者名稱。

早些時候,當我們實現我們的Create() 操作方法的HTTP-POST版本時,我們已經將 Dinner 的「託管比」屬性硬編碼為靜態字串串。 我們現在可以更新此代碼以改用User.Identity.Name屬性,並為創建 Dinner 的主機自動添加 RSVP:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

由於我們已經向 Create() 方法添加了 [授權] 屬性,因此 ASP.NET MVC 可確保僅當訪問 /Dinners/Create URL 的使用者登錄網站時,才會執行操作方法。 因此,User.Identity.Name屬性值將始終包含有效的使用者名。

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>編輯晚餐時使用User.Identity.Name屬性

現在,讓我們添加一些限制使用者的授權邏輯,以便他們只能編輯自己託管的晚餐的屬性。

為了幫助達到這一目的,我們將首先向 Dinner 物件添加"Is託管By(使用者名)"幫助器方法(在之前構建的 Dinner.cs 部分類中)。 此說明程式方法傳回 true 或 false,具體取決於提供的使用者名稱是否與 Dinner 託管 By 屬性匹配,並封裝執行不區分大小寫的字串比較所需的邏輯:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

然後,我們將向 DinnersController 類中的 Edit() 操作方法添加 [授權] 屬性。 這將確保使用者必須登錄才能請求 */Dinners/Edit/[id]* URL。

然後,我們可以向使用 Dinner.IsHostBy(使用者名)幫助器方法的「編輯」方法添加代碼,以驗證登錄使用者是否與 Dinner 主機匹配。 如果使用者不是主機,我們將顯示"無效擁有者"視圖並終止請求。 執行此操作的代碼如下所示:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

然後,我們可以右鍵單擊 [Views_Dinners]目錄,然後選擇"&gt;添加 -視圖"功能表命令以創建新的"無效擁有者"視圖。 我們將用以下錯誤訊息填充它:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

現在,當用戶嘗試編輯他們不擁有的晚餐時,他們會得到一條錯誤消息:

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

我們可以對控制器中的 Delete() 操作方法重複相同的步驟,以鎖定刪除 Dinner 的許可權,並確保只有晚餐的主持人才能刪除它。

### <a name="showinghiding-edit-and-delete-links"></a>顯示/隱藏編輯與移除連結

我們正在從「詳細資訊」URL 連結到「晚餐控制器」類的編輯和刪除操作方法:

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

目前,我們顯示"編輯和刪除"操作連結,無論詳細資訊 URL 的訪問者是否是晚宴的東道主。 讓我們更改此內容,以便僅當訪問使用者是晚餐的擁有者時才會顯示連結。

晚餐控制器中的「詳細資訊()」操作方法檢索 Dinner 物件,然後將其作為模型物件傳遞給檢視範本:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

我們可以更新檢視範本,以便使用「晚餐.Is託管By」()幫助器方法有條件地顯示/隱藏"編輯"和"刪除"連結,如下所示:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>後續步驟

現在,讓我們來看看如何啟用經過身份驗證的使用者到RSVP的晚餐使用AJAX。

> [!div class="step-by-step"]
> [前一個](implement-efficient-data-paging.md)
> [下一個](use-ajax-to-deliver-dynamic-updates.md)
