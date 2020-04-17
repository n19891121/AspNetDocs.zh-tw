---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: ASP.NET和網络工具 2013.2 用於視覺工作室 2013 發行說明 |微軟文件
author: rick-anderson
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 41b0f3ad43846bc5799ecd398188b0f6ffcc0d66
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543622"
---
# <a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>適用於 Visual Studio 2013 的 ASP.NET 和 Web 工具 2013.2 版本資訊

由[微軟](https://github.com/microsoft)

## <a name="installation-notes"></a>安裝注意事項

visual Studio 2013.2 的ASP.NET和 Web 工具捆綁在主安裝程式中,可以作為[Visual Studio 2013 更新 2](https://go.microsoft.com/fwlink/?LinkId=390521)的一部分下載。

## <a name="documentation"></a>文件

有關 visual Studio 2013.2 的ASP.NET和 Web 工具的教程和其他資訊可從[ASP.NET網站](https://www.asp.net/)獲得。

## <a name="software-requirements"></a>軟體需求

視覺工作室2013.2ASP.NET和網路工具需要視覺工作室2013。

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>Visual Studio ASP.NET和 Web 工具中的新功能 2013.2

以下各節介紹版本中引入的功能。

- [ASP.NET 專案範本](#oneaspnet)
- [在 IIS Express 上啟動 Web 應用程式時支援 SSL](#ssl)
- [視覺化工作室 Web 編輯器增強功能](#vswebeditor)
- [瀏覽器連結](#browserlink)
- [在視覺化工作室中支援 Azure 應用服務 Web 應用](#waws)
- [建立新 Web 專案時建立遠端 Azure 資源](#AzureResources)
- [Web 發佈增強功能](#webpublish)
- [ASP.NET腳手架](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET Web 表單](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NET Web API 2.1.2](#webapi)
- [ASP.NET網頁 3.1.2](#webpages)
- [實體框架 6.1](#ef)
- [ASP.NET 標識 2.0.0](#identity)
- [微軟 OWIN 元件](#owin)
- [ASP.NET信號R 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>ASP.NET 專案範本

- 更新ASP.NET專案範本以支援帳戶確認和密碼重置。
- 更新ASP.NET Web API 範本以支援使用內部組織帳戶進行身份驗證。
- ASP.NET SPA 樣本現在包含基於 MVC 和伺服器端視圖的身份驗證。 該範本具有一個 WebAPI 控制器,該控制器只能由經過身份驗證的使用者訪問。

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>在 IIS Express 上啟動 Web 應用程式時支援 SSL

為了消除本地主機上流覽和調試 HTTPS 時的安全警告,我們添加了一個對話框,允許 Internet Explorer 和 Chrome 信任自簽名的 IIS Express SSL 證書。

例如,可以將 Web 專案屬性設定為使用 SSL。 單擊 F4 可彈出屬性對話方塊。 將**啟用 SSL 更改為**true。 複製 SSL URL。

![開啟 SSL 屬性](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

將 Web 專案屬性頁 Web 選項卡設定為使用基於 HTTPS 的`https://localhost:44300/`URL(SSL URL 將是 ,除非您以前創建了 SSL 網站。

![設定專案網址 (HTTPS)](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

按 CTRL+F5 執行應用程式。 按照說明信任 IIS Express 生成的自簽名證書。

![SSL 警告](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

閱讀**安全警告**對話框,然後按下「**是**」,如果要安裝表示本地主機的證書。

![安全性警告](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

該網站將以 IE 或 Chrome 顯示,瀏覽器中沒有證書警告。

![沒有警告的 HTTPS 頁面](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox 使用自己的證書存儲,因此將顯示警告。

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>視覺化工作室 Web 編輯器增強功能

- **新的JSON專案專案和編輯器**:我們已經添加了一個JSON專案專案和編輯器到可視化工作室。 當前 JSON 編輯器功能包括著色、語法驗證、大括弧完成、大綱、工具選項設置等。

    ![JSON 編輯器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    IntelliSense 現在支援[JSON 架構](http://json-schema.org/)v3 和 v4。 有一個架構組合框用於選擇現有架構、編輯本地架構路徑,或者只需將專案 JSON 檔拖放到它以獲取相對路徑即可。

    ![JSON 感知](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON 架構編輯器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **新Sass (SCSS) 編輯器**: 我們在 VS2013 RTM 中添加了 LESS,現在我們有一個 Sass 專案專案和編輯器。 Sass 編輯器功能可與 LESS 編輯器類似,包括著色、變數和 Mixins IntelliSense、註釋/註釋、快速資訊、格式設置、語法驗證、大綱、goto 定義、顏色選取器、工具選項設置等。

    ![新增項目:SCSS 樣式表](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![樣式表編輯器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **HTML、剃刀、CSS、LESS 和 Sas 文件中的新 URL 選取器:** VS 2013 在 Web 窗體頁面之外沒有 URL 選取器。 用於 HTML、Razor、CSS、LESS 和 Sas 編輯器的新 URL 選取器是一個無對話、流暢的鍵入選取器,可理解 ". 並適當篩選 img 標籤和連結的檔案清單。

    ![用於影像標記的網址選擇器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![檢視的網址選擇器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![以 CSS 的網址選擇器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **以新增更多功能更新 LESS 編輯器**
- **挖空智慧感知升級**:我們為 VS IntelliSense 添加了非標準的「敲擊」語法,"ko-vs-編輯視圖模型:「語法。 它可用於使用表單中的註釋結合到頁面上的多個檢視模型:

    ![挖空感知](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    我們還添加了對嵌套視圖模型智慧感知的支援,因此您可以深入到視圖模型上的深嵌套物件。

    `<div data-bind="text: foo.bar.baz.etc" />`

    顯示的智慧感知是 JAVAScript 物件的完整智慧感知。

    ![顯示完整 JavaScript 物件的智慧感知](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **HTML、Razor、CSS、LESS 和 Sass 文件中的新 URL 選取器**: VS 2013 在 Web 窗體頁面之外沒有 URL 選取器。 用於 HTML、Razor、CSS、LESS 和 Sas 編輯器的新 URL 選取器是一個無對話、流暢的鍵入選取器,可理解 ". 並適當篩選 img 標籤和連結的檔案清單。

    ![用於影像標記的網址選擇器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![檢視的網址選擇器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![以 CSS 的網址選擇器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>瀏覽器連結

- 瀏覽器連結現在支援 HTTPS 連接,並且將在儀表板中列出具有其他連接,只要瀏覽器信任證書。
- 靜態 HTML 源映射
- SPA 支援映射資料
- 自動更新對應資料

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>在視覺化工作室中支援 Azure 應用服務 Web 應用

- **支援 Azure 登錄。**
- **Web 應用的遠端除錯和遠端檢視**:我們現在支援[Azure 應用服務中的 Web 應用的遠端除錯](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)和伺服器資源管理員中 Web 應用內容檔的遠端檢視。

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>建立新 Web 專案時建立遠端 Azure 資源

我們在新的 Web 應用程式對話方塊上添加了[Azure"建立遠端資源"](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)複選框。 通過選擇它,您將能夠整合建立新 Web 應用程式、設定 Azure 發表網站進行測試以及透過幾個簡單步驟創建發表配置檔的體驗。

![具有 Azure 資源的新專案](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![發行到 Azure](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>Web 發佈增強功能

- 改善發佈用戶體驗。

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET腳手架

- **列舉支援:** 如果您的模型使用枚舉,則MVC基架將生成枚舉的下拉。 這使用 MVC 中的枚舉說明器。
- **引導支援**:更新了 MVC 基架中的編輯器範本,以便它們使用引導類。
- **套件支援**:MVC 和 Web API 基架將為 MVC 和 Web API 添加 5.1 套件

以下螢幕截圖演示了基架模型。

- 型號代碼:

     ![模型代碼](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- 編譯模型代碼,右鍵按一下,然後選擇 **「新增****」,新建基架專案**。

     ![新增文手架專案](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- **使用實體框架選擇具有檢視的 MVC5 控制器**:

     ![新增帶檢視的新 MVC5 控制器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- 使用模型**新增控制器**:

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- 檢查產生的代碼,例如檢視/工作日模型/Edit.cshtml 包含`@Html.EnumDropDownListFor`![: 包含 EnumDropDownList 的檢視](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- 運行頁面以查看生成的枚舉組合框,請注意,如果值可以為 null,則可以為組合框選擇一個空字串。 例如,「**建立」** 頁顯示以下內容:

    ![允許空字串的組合框](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM 將於 2014 年 4 月發布。 以下是發行說明的要點,但請查看[完整發行說明](http://docs.nuget.org/docs/release-notes/nuget-2.8),瞭解有關這些更改的詳細資訊。

- **目標 Windows Phone 8.1 應用程式**: NuGet 2.8.1 現在支援使用目標框架名字「WindowsPhoneApp」,「WPA」,「WindowsPhoneApp81」和「WPA81」定位 Windows Phone 8.1 應用程式。

- **依賴項的修補程式解析**:在解決包依賴項時,NuGet 歷來實施了選擇滿足包依賴項的最低主包和次要包版本的策略。 但是,與主要版本和次要版本不同,修補程式版本始終解析為最高版本。 儘管該行為是善意的,但它造成了安裝具有依賴關係的包缺乏確定性。
- **依賴項版本交換機**:雖然 NuGet 2.8 更改了解析依賴項的*默認*行為,但它也通過包管理器控制台中的 -依賴項版本開關增加了對依賴項解析過程的更精確控制。 該交換機允許解析對低可能版本(預設行為)、可能的最高版本或最高次要版本或修補程式版本的依賴項。 此開關僅適用於電源殼命令中的安裝包。
- **依賴項版本屬性**:除了上面詳述的 -依賴版本開關外,NuGet 還允許在 nuget.config 檔中設置新屬性,定義預設值是什麼,如果 -依賴項版本開關未在安裝包的調用中指定。 對於任何安裝套件操作,NuGet 包管理器對話方塊也會尊重此值。 要設定此值,請將下面的屬性加入到 nuget.config 檔:

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **使用 -WhatIf**預覽 NuGet 操作 :某些 NuGet 套件可以具有深層依賴項圖,因此,在安裝、卸載或更新操作期間,它可以很有説明,以便首先看到將會發生什麼。 NuGet 2.8 添加了標準 PowerShell - 如果切換到安裝包、卸載包和更新套件命令,以便可視化將應用該命令的包的整個關閉。
- **降級包**:安裝包的預發佈版本以調查新功能,然後決定回滾到最後的穩定版本的情況並不少見。 在 NuGet 2.8 之前,這是卸載預發佈包及其依賴項,然後安裝早期版本的多步驟過程。 但是,使用 NuGet 2.8,更新包現在會將整個包關閉(例如包的依賴項樹)回滾到以前的版本。
- **開發相依項**:許多不同類型的功能可以作為 NuGet 套件提供, 包括用於最佳化開發過程的工具。 這些元件雖然在開發新包方面可以發揮作用,但在以後發佈新包時,不應被視為新包的依賴項。 NuGet 2.8 使包能夠在 .nuspec 檔案中將自己識別為開發依賴項。 安裝後,此中繼資料也將加入到套件. 稍後在 nuget.exe 包期間分析該包.config 檔以分析 NuGet 依賴項時,它將排除標記為開發依賴項的這些依賴項。
- **單個包.為不同平臺配置檔**:在為多個目標平台開發應用程式時,為每個不同的生成環境使用不同的專案檔是很常見的。 在不同的項目檔中使用不同的 NuGet 包也很常見,因為包對不同平台的支持級別不同。 NuGet 2.8 透過為不同的平臺特定專案檔建立不同的套件.config 檔案,為該方案提供了改進的支援。
- **回退到本地快取**:雖然 NuGet 包通常使用遠端庫(如使用網路連接的[NuGet 庫](http://www.nuget.org))使用,但在許多情況下,用戶端未連接。 如果沒有網路連接,NuGet 客戶端將無法成功安裝包 - 即使這些包已在用戶端的電腦上本地 NuGet 快取中。 NuGet 2.8 將自動緩存回退到包管理器主控台。

    緩存回退功能不需要任何特定的命令參數。 此外,緩存回退目前僅在包管理器控制台中工作 - 該行為當前在包管理器對話框中不起作用。
- **錯誤修復**:所做的主要錯誤修復之一是更新包 -重新安裝命令的性能改進。

    除了這些功能和上述性能修復之外,NuGet 的此版本還包括許多其他錯誤修復。 在新聞稿中共處理了181個問題。 有關 NuGet 2.8 中固定的工作項目的完整清單,請檢視此版本的[NuGet 問題追蹤器](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)。

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET Web Forms

- Web 表單樣本現在展示如何對ASP.NET身份進行帳戶確認和密碼重置。
- 實體數據來源控制件和實體框架的動態數據提供程式 6。 有關詳細資訊,請參閱以下 MSDN 部落格:[實體架構 6 的動態資料提供程式和實體資料來源控制項](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)。

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [屬性路由改進](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [編輯器樣本的開機支援](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [檢視中的枚舉支援](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [對最小長度/最大長度屬性的不顯眼支援](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [在不顯眼的 Ajax 中支援「此」上下文](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- 各種[錯誤修復](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET Web API 2.1.2

- [全域錯誤處理](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [屬性路由增強功能](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [說明頁面改進](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [忽略路由支援](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON 媒體型態物質](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [更好地支援非同步濾波器](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [用戶端格式庫的查詢解析](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- 各種[錯誤修復](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET網頁 3.1.2

- 各種[錯誤修復](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>實體框架 6.1

實體框架已更新為 6.1 版,用於運行時和工具。 實體框架 (EF) 6.1 是實體框架 6 的一個小更新,包括許多錯誤修復和新功能。 有關 EF6.1 的詳細資訊(包括指向新功能的文件的連結),請參閱[實體框架版本歷史記錄](https://msdn.microsoft.com/data/jj574253)。 此版本中的新功能包括:

- **工具整合**提供建立新 EF 模型的一致方法。 此功能擴展了ADO.NET實體數據模型嚮導,以支援創建代碼優先模型,包括從現有資料庫進行反向工程。 這些功能以前在 EF 電動工具中以測試版品質提供。
- **處理事務提交失敗**提供了新的[系統.Data.Entity.基礎結構.提交失敗處理,](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx)它利用新引入的攔截事務操作的能力。 **提交失敗處理程式**允許在提交事務時自動從連接故障中恢復。
- **IndexAttribute**允許在 Code First 模型中的屬性(或屬性)上放置屬性來指定索引。 然後,代碼優先將在資料庫中創建相應的索引。
- **公共映射 API**提供對 EF 對屬性和類型如何映射到資料庫中的列和表的存取。 在以前的版本中,此 API 是內部的。
- **能夠通過 App/Web.config 檔配置攔截器**(允許在不重新編譯應用程式的情況下添加攔截器)。
- **DatabaseLogger**是一種新的攔截器,它可以輕鬆地將所有資料庫操作記錄到檔中。 與前一個功能結合使用,這允許您輕鬆打開已部署應用程式的資料庫操作日誌記錄,而無需重新編譯。
- **遷移模型更改檢測**已改進,以便更精確地遷移基架;更改檢測過程的性能也得到了極大的提高。
- **性能改進**包括初始化期間資料庫操作減少、LINQ 查詢中無效相等比較的優化、更多方案中更快的檢視生成(模型創建)以及具有多個關聯的跟蹤實體的更高效具體化。

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET 標識 2.0.0

- **雙重身份驗證**:ASP.NET標識現在支援雙重身份驗證。 在密碼洩露的情況下,雙重身份驗證為使用者帳戶提供了額外的安全層。 此外,還保護暴力攻擊兩個因數代碼。
- **帳號鎖定:** 提供一種在使用者輸入密碼或雙因素代碼不正確時鎖定使用者的方法。 可以配置無效嘗試的次數和鎖定用戶的時間跨度。 開發人員可以選擇關閉某些使用者帳戶的帳戶鎖定,以便他們在需要時關閉。
- **帳號確認:** ASP.NET身份系統現在支援帳戶確認。 這是當今大多數網站中相當常見的情況,當您在網站上註冊新帳戶時,您需要確認電子郵件,然後才能在網站中執行任何操作。 電子郵件確認是有用的,因為它可以防止創建虛假帳戶。 如果您使用電子郵件作為與網站使用者(如論壇網站、銀行、電子商務或社交網站)通信的方法,則此功能非常有用。
- **密碼重設:** 密碼重置是一項功能,用戶可以重置其密碼,如果他們忘記了他們的密碼。
- **安全戳(隨處可見):** 支援在使用者更改密碼或任何其他安全相關資訊(如刪除關聯的登錄名(如 Facebook、Google、微軟帳戶等)時為使用者重新生成安全權杖的方法。 這是必需的,以確保使用舊密碼生成的任何令牌都失效。 在示例專案中,如果更改使用者的密碼,則會為使用者生成新令牌,並且任何以前的權杖都失效。 此功能為應用程式提供了額外的安全層,因為當您更改密碼時,您將從登錄到此應用程式的任何地方(所有其他瀏覽器)註銷。
- **使主鍵的類型對使用者和角色具有擴充性**:在ASP.NET標識 1.0 中,表使用者和角色的主鍵類型是字串。 這意味著當使用實體框架在 SQL Server 中保留 ASP.NET 標識系統時,我們使用 nvarchar。 圍繞堆疊溢出的此預設實現,並根據傳入的反饋進行了許多討論。 我們提供了一個擴充性掛鉤,您可以在其中指定使用者和角色表的主鍵。 如果要遷移應用程式,並且應用程式正在存儲 UserId 是 GUID 或 int,則此擴充性掛鉤特別有用。
- **支援使用者和角色上的「可查詢」** 在 UsersStore 和 Roles Store 上新增了對 IQuery 的支援,您可以輕鬆地獲取使用者和角色清單。
- **支援透過使用者管理員移除操作**
- **對使用者名進行索引**:在ASP.NET標識實體框架實現中,我們使用 EF 6.1.0 中的新 Index 屬性在使用者名上添加了唯一索引。 這可確保使用者名始終是唯一的,並且沒有種族條件,您可以最終使用重複的使用者名。
- **增強的密碼驗證器:** 在標識 1.0 ASP.NET中附帶的密碼驗證器是一個相當基本的密碼驗證器,它只驗證了最小長度。 有一個新的密碼驗證器,使您能夠對密碼的複雜性進行更多的控制。 請注意,即使您打開此密碼中的所有設置,我們也鼓勵您為使用者帳戶啟用雙重身份驗證。
- **識別工廠中間件/建立PerOwin上下文**:

    - **使用者管理員**:您可以使用工廠實現從 OWIN 上下文中獲取使用者管理員的實例。 此模式類似於我們用於從 OWIN 上下文中獲取 SignIn 和 SignOut 的身份驗證管理器。 這是為應用程式獲取每個請求的 UserManager 實例的推薦方法。
    - **DbContextFactory:ASP.NET**識別使用實體框架在 SQL Server 中持久化標識系統。 為此,標識系統具有對應用程式 DbContext 的引用。 DbContextFactory 中間件傳回應用程式中每個請求的應用程式 DbContext 實例,您可以在應用程式中使用。
- **ASP.NET識別範例 NuGet 套件**: 範例 NuGet 套件可以使安裝和執行ASP.NET識別的樣本變得更容易,並遵循最佳實務。 這是 MVC 應用程式 ASP.NET 示例。 請在生產中部署代碼之前修改代碼以適合您的應用程式。 該示例應安裝在空ASP.NET應用程式中。 有關該包的詳細資訊,請造訪以下部落格文章:[宣佈ASP.NET標識 2.0.0 的 RTM](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Microsoft OWIN 元件

此版本中修復了許多錯誤。 有關詳細資訊,請參閱[2.1.0 版本的發行說明](https://katanaproject.codeplex.com/releases/view/113281)。

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET信號R 2.0.2

此版本中修復了許多錯誤。 有關詳細資訊,請參閱[2.0.2 版本的發行說明](https://github.com/SignalR/SignalR/releases/tag/2.0.2)。
