---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: 將ASP.NET MVC 與不同版本的 IIS (VB) 使用 |微軟文件
author: rick-anderson
description: 在本教學中,您將瞭解如何使用ASP.NET MVC 和 URL 路由,以及不同版本的 Internet 資訊服務。 你學習不同的原則...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: 5e04ae14026e6d5dd1e603be6c52ff6876a468cf
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541997"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a>使用 ASP.NET MVC 與不同版本的 IIS (VB)

由[微軟](https://github.com/microsoft)

> 在本教學中,您將瞭解如何使用ASP.NET MVC 和 URL 路由,以及不同版本的 Internet 資訊服務。 您將學習將 ASP.NET MVC 與 IIS 7.0(經典模式)、IIS 6.0 和早期版本的 IIS 使用的不同策略。

ASP.NET MVC 框架依賴於 ASP.NET 路由來將瀏覽器請求路由到控制器操作。 為了利用ASP.NET路由,您可能需要在Web伺服器上執行其他配置步驟。 這完全取決於互聯網資訊服務 (IIS) 的版本和應用程式的請求處理模式。

以下是不同版本的 IIS 的摘要:

- IIS 7.0(整合模式) - 無需特殊配置ASP.NET路由。
- IIS 7.0(經典模式) - 您需要執行特殊配置才能使用ASP.NET路由。
- IIS 6.0 或以下 - 您需要執行特殊配置才能使用ASP.NET路由。

最新版本的IIS版本為7.5版本(在Win7上)。 IIS 7 的 IIS 包含在 Windows 伺服器 2008 和 VISTA/SP1 及更高版本中。 您還可以在 Vista 作業系統的任何版本上安裝 IIS 7.0,但家庭[https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)基本版除外 (參見 )。

IIS 7.0 支援兩種處理請求的模式。 您可以使用整合模式或傳統模式。 在整合模式下使用IIS 7.0時,無需執行任何特殊配置步驟。 但是,在經典模式下使用IIS 7.0時,您確實需要執行其他配置。

微軟 Windows 伺服器 2003 包括 IIS 6.0。 使用 Windows Server 2003 作業系統時,無法將 IIS 6.0 升級到 IIS 7.0。 使用IIS 6.0時,必須執行其他配置步驟。

微軟視窗XP專業版包括IIS 5.1。 使用IIS 5.1時,必須執行其他配置步驟。

最後,微軟 Windows 2000 和微軟 Windows 2000 專業版包括 IIS 5.0。 使用IIS 5.0時,必須執行其他配置步驟。

## <a name="integrated-versus-classic-mode"></a>整合模式與傳統模式

IIS 7.0 可以使用兩種不同的請求處理模式處理請求:集成和經典。 集成模式提供更好的性能和更多功能。 經典模式包括向後相容早期版本的IIS。

請求處理模式由應用程式池確定。 通過確定與應用程式關聯的應用程式池,可以確定特定 Web 應用程式正在使用哪種處理模式。 請遵循下列步驟：

1. 推出網際網路資訊服務管理員
2. 在「連線」視窗中,選擇應用程式
3. 在「操作」視窗中,按下 **「基本設定」** 連結以開啟「編輯應用程式」對話框(參見圖 1)
4. 請注意所選的應用程式池。

預設情況下,IIS 設定為支援兩個應用程式池:**預設 AppPool**和**經典 .NET AppPool**。 如果選擇了預設AppPool,則應用程式以整合的請求處理模式運行。 如果選擇了經典 .NET AppPool,則應用程式以經典請求處理模式運行。

[![[New Project] \(新增專案\) 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)

**圖1:** 偵測要求處理模式([按下以檢視全尺寸影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png))

請注意,您可以在"編輯應用程式"對話框中修改請求處理模式。 按下「選擇」按鈕並更改與應用程式關聯的應用程式池。 請注意,將ASP.NET應用程式從經典模式更改為集成模式時存在相容性問題。 如需詳細資訊，請參閱下列文章：

- 將 ASP.NET 1.1 升級到 Windows Vista 和 Windows 伺服器 2008 上的 IIS 7.0 --[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)

- ASP.NET與 IIS 7.0 整合 -[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

如果ASP.NET應用程式正在使用 DefaultAppPool,則無需執行任何其他步驟,就可以使ASP.NET路由(因此ASP.NET MVC)正常工作。 但是,如果ASP.NET應用程式配置為使用經典 .NET AppPool,然後繼續閱讀,您還有更多工作要做。

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>將ASP.NET MVC 與舊版本的 IIS 一起使用

如果您需要將 IIS 版本早於 IIS 7.0 的舊版本 ASP.NET MVC 使用,或者需要在傳統模式下使用 IIS 7.0,則有兩個選項。 首先,您可以修改路由表以使用文件副檔名。 例如,您請求的 URL 不是 /Store/詳細資訊,而是請求 URL,如 /Store.aspx/詳細資訊。

第二個選項是創建稱為*通配符腳本映射*的內容。 通配符文稿對應讓您能夠將每個請求映射到ASP.NET框架。

如果您無法存取 Web 伺服器(例如,您的 ASP.NET MVC 應用程式由 Internet 服務提供者託管),則需要使用第一個選項。 如果不想修改 URL 的外觀,並且可以訪問 Web 伺服器,則可以使用第二個選項。

我們將在以下部分中詳細介紹每個選項。

## <a name="adding-extensions-to-the-route-table"></a>新增於表新增延伸

獲取ASP.NET路由以使用舊版本的IIS的最簡單方法是修改Global.asax檔中的路由表。 清單1中的預設和未修改的 Global.asax 檔配置了一個名為"預設路由"的路由。

**清單1 - 全域.asax(未修改)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

通過清單 1 中設定的預設路由,您可以路由如下所示的 URL:

/首頁/索引

/產品/詳細資訊/3

/Product

遺憾的是,舊版本的IIS不會將這些請求傳遞給ASP.NET框架。 因此,這些請求不會路由到控制器。 例如,如果您對 URL/Home/Index 發出瀏覽器請求,則將在圖 2 中獲取錯誤頁。

[![[New Project] \(新增專案\) 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)

**圖2**: 收到 404 找不到錯誤([按下以檢視全尺寸影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png))

較舊版本的IIS僅將某些請求映射到ASP.NET框架。 請求必須針對具有正確檔副檔名的 URL。 例如,對 /SomePage.aspx 的請求將映射到ASP.NET框架。 但是,對 /SomePage.htm 的請求沒有。

因此,要使ASP.NET路由正常工作,我們必須修改預設路由,以便它包含映射到ASP.NET框架的檔擴展名。

這是使用名為`registermvc.wsf`的腳本完成的。 它包含在 ASP.NET MVC`C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`1 版本中 ,但截至 ASP.NET 2,此文本[http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)已移動到 ASP.NET 期貨,可在 。

執行此文本會使用IIS註冊新的.mvc擴展。 註冊 .mvc 副檔名後,您可以在 Global.asax 檔中修改路由,以便路由使用 .mvc 擴展名。

清單2中修改後的 Global.asax 檔適用於舊版本的 IIS。

**清單 2 - 全域.asax(使用延伸修改)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]

重要提示:請記住在更改 Global.asax 檔後再次建構ASP.NET MVC 應用程式。

清單2中全域.asax 檔有兩個重要更改。 現在,全域.asax 中定義了兩個路由。 預設路由(第一個路由)的 URL 模式現在如下所示:

{控制器}.mvc/{操作}/{id}

.mvc 副檔名的添加會更改ASP.NET路由模組截獲的文件類型。 透過此變更,ASP.NET MVC 應用程式現在路由如下所示的請求:

/Home.mvc/指數/

/產品.mvc/細節/3

/產品.mvc/

第二個路由,根路由,是新的。 根路由的此 URL 模式是一個空字串。 對於匹配針對應用程式根發出的請求,此路由是必需的。 例如,根路由將匹配如下所示的請求:

[http://www.YourApplication.com/](http://www.YourApplication.com/)

對路由表進行這些修改後,需要確保應用程式中的所有連結都與這些新 URL 模式相容。 換句話說,請確保所有連結都包含 .mvc 擴展。 如果使用 Html.ActionLink() 説明器方法產生連結,則不需要進行任何更改。

您可以手動向 iIS 添加新擴展 ASP.NET,而不是使用 registermvc.wcf 腳本。 自行新增新副檔名時,請確保未選取的標記為 **「驗證該檔存在」 選單 。**

## <a name="hosted-server"></a>託管伺服器

您並不總是有權訪問 Web 伺服器。 例如,如果您使用 Internet 託管供應商託管 ASP.NET MVC 應用程式,則不一定有權訪問 IIS。

在這種情況下,應使用映射到ASP.NET框架的現有文件副檔名之一。 映射到ASP.NET的檔副檔名的範例包括 .aspx、.axd 和 .ashx 副檔名。

例如,清單 3 中修改的 Global.asax 檔使用 .aspx 擴展名而不是 .mvc 擴展名。

**清單 3 - 全域.asax(使用 .aspx 擴展修改)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

清單3中的 Global.asax 檔與以前的 Global.asax 檔案完全相同,只是它使用 .aspx 擴展名而不是 .mvc 副檔名。 您不必在遠端 Web 伺服器上執行任何設定才能使用 .aspx 擴展。

## <a name="creating-a-wildcard-script-map"></a>建立通配符文稿對應

如果您不想修改ASP.NET MVC 應用程式的 URL,並且可以造訪 Web 伺服器,則有其他選項。 您可以建立通配符文本映射,將所有請求映射到 Web 伺服器 ASP.NET 框架。 這樣,您可以使用預設ASP.NET MVC 路由表與IIS 7.0(經典模式)或IIS 6.0。

請注意,此選項會導致IIS攔截針對Web伺服器的每個請求。 這包括對圖像、經典 ASP 頁面和 HTML 頁面的請求。 因此,將通配符腳本映射啟用ASP.NET確實會影響性能。

以下是為 IIS 7.0 啟用通配符文稿對應的方式:

1. 在「連線」視窗中選擇應用程式
2. 確保選擇**了 「功能」** 檢視
3. 雙擊 **「處理程式映射」** 按鈕
4. 按下 **「新增通配符文稿映射」** 連結(參見圖 3) 3
5. 輸入 aspnet\_isapi.dll 檔案的路徑 (可以從 PageHandlerFactory 文稿映射複製此路徑)
6. 輸入名稱 MVC
7. 點選 **「確定」** 按鈕

[![[New Project] \(新增專案\) 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)

**圖 3**: 使用 IIS 7.0 建立通配符文稿映射([按下以檢視全尺寸影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png))

依以下步驟建立具有 IIS 6.0 的通配符文稿映射:

1. 右鍵按一下網站並選擇"屬性"
2. 選擇**家目錄**選項卡
3. 點選 **「設定」** 按鈕
4. 選擇**映射選項**卡
5. 點選 **「插入」** 按鈕(參見圖 4)
6. 將 aspnet\_isapi.dll 的路徑貼上為可執行欄位(可以從 .aspx 檔案的文稿映射中複製此路徑)
7. 取消選擇標籤為 **「驗證檔案存在」複選框**
8. 點選 **「確定」** 按鈕

[![[New Project] \(新增專案\) 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)

**圖 4**: 使用 IIS 6.0 建立通配符文稿映射([按下以檢視全尺寸影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png))

啟用通配符文本映射後,需要修改 Global.asax 檔中的路由表,以便它包含根路由。 否則,當您請求應用程式的根頁時,您將獲得圖 5 中的錯誤頁。 您可以使用清單 4 中修改的 Global.asax 檔案。

[![[New Project] \(新增專案\) 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)

**圖 5**: 缺少根路由錯誤([按下以檢視全尺寸影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png))

**清單 4 - 全域.asax(使用根路由修改)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

為 IIS 7.0 或 IIS 6.0 啟用通配符文本映射後,可以發出適用於預設路由表的請求,如下所示:

/

/首頁/索引

/產品/詳細資訊/3

/Product

## <a name="summary"></a>總結

本教學的目的是解釋在使用舊版本的 IIS(或經典模式下的 IIS 7.0)時如何使用ASP.NET MVC。 我們討論了使ASP.NET路由與舊版本的IIS配合使用的方法:修改預設路由表或創建通配符腳本映射。

第一個選項要求您修改ASP.NET MVC 應用程式中使用的 URL。 第一個選項的一個顯著優點是,您不需要訪問 Web 伺服器來修改路由表。 這意味著,即使使用 internet 託管公司託管 ASP.NET MVC 應用程式,您也可以使用此選項。

第二個選項是創建通配符腳本映射。 第二個選項的優點是不需要修改 URL。 第二個選項的缺點是它會影響ASP.NET MVC 應用程式的性能。

> [!div class="step-by-step"]
> [上一步](using-asp-net-mvc-with-different-versions-of-iis-cs.md)
