---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: ASP.NET和網络工具發行說明 2013.1 可視化工作室 2012 |微軟文件
author: rick-anderson
description: 本文件介紹了 Visual Studio 2012 的 ASP.NET 和網路工具 2013.1 的發佈。
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543570"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>適用於 Visual Studio 2012 的 ASP.NET 和 Web 工具 2013.1 版本資訊

由[微軟](https://github.com/microsoft)

> 本文件介紹了 Visual Studio 2012 的 ASP.NET 和網路工具 2013.1 的發佈。

## <a name="contents"></a>內容

- [安裝說明](#install)
- [軟體要求](#requirements)
- 視覺工作室 2012 年 ASP.NET 和網路工具 2013.1 中的新功能

    - [Bootstrap](#bootstrap)
    - [範本](#templates)

        - [ASP.NET MVC 5 樣本](#mvc5template)
        - [ASP.NET Web API 2 範本](#apitemplate)
        - [專案範本](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET腳手架](#scaffold)
    - [剃刀編輯器](#razor)
    - [NuGet 2.7](#nuget)
- 已知問題和重大變更

    - [ASP.NET腳手架](#issuescaffolding)

        - [MVC 與 Web API 基架 - HTTP 404,找不到錯誤](#404issue)
        - [Visual Studio Express 2012 用於 Web 在新增文手架專案後停止工作](#expressissue)
    - [ASP.NET剃刀 3](#issuerazor)

        - [使用「使用」或「F5」檢視 cshtml 檔會導致伺服器錯誤](#browseissue)
        - [Url 重寫和蒂爾德 (*)](#rewriteissue)
    - [範本](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>安裝注意事項

[安裝](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids)ASP.NET和網路工具 2013.1 用於視覺工作室 2012。

<a id="requirements"></a>
## <a name="software-requirements"></a>軟體需求

您必須有 Visual Studio 2012 或 Visual Studio Express 2012 用於 Web。

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>視覺工作室 2012 年 ASP.NET 和網路工具 2013.1 中的新功能

<a id="bootstrap"></a>
### <a name="bootstrap"></a>啟動程序

當您文手架 MVC 5 控制器與檢視時,檢視的標記使用[Bootstrap](http://getbootstrap.com/)。

<a id="templates"></a>
### <a name="templates"></a>範本

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET MVC 5 樣本

我們添加了一個新的 MVC 5 範本。 它引用最新的 MVC 5 NuGet 套件,您可以使用基架添加控制器和檢視。

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>ASP.NET Web API 2 範本

我們添加了一個新的 Web API 2 範本。 它引用最新的 Web API 2 NuGet 套件,您可以使用基架添加控制器和檢視。

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>項目範本

我們為 MVC 5 檢視、網頁 (Razor 3) 和 Web API 2 控制器添加了新的專案範本。 他們在添加新項的同時,將相關的 NuGet 包安裝到專案中。

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

當您使用實體框架建構 MVC 或 Web API 控制器時,我們使用框架 6。 有關實體框架的詳細資訊,請參閱[實體框架版本歷史記錄](https://msdn.com/data/jj574253)。

您還可以下載並安裝可視化工作室的實體框架 6 工具 2012。 請參考[實體框架](https://msdn.com/data/ee712906#tooling)。

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET腳手架

ASP.NET基架是ASP.NET Web 應用程式的代碼生成框架。 它可以輕鬆地向與數據模型交互的專案添加樣板代碼。

在 Visual Studio 的早期版本中,基架僅限於 ASP.NET MVC 專案。 使用此更新,您現在可以對任何ASP.NET專案(包括 Web 窗體)使用基架。 此更新不支援為 Web 窗體專案生成頁面,但仍可以通過向專案添加 MVC 依賴項來使用 Web 窗體的腳手架。 將在將來的更新中添加對生成 Web 窗體頁面的支援。

使用基架時,我們確保在專案中安裝了所有必需的依賴項。 例如,如果從ASP.NET Web 窗體專案開始,然後使用基架添加 Web API 控制器,則所需的 NuGet 包和引用將自動添加到專案中。

要將 MVC 基架加入 Web 窗體專案,請新增**新的文手架,** 並在對話框視窗中選擇**MVC 5 相依項 。** 基架 MVC 有兩個選項;最小和完整。 如果選擇「最小」,則只有 ASP.NET MVC 的 NuGet 包和引用添加到專案中。 如果選擇"完整"選項,則添加最小依賴項以及 MVC 專案所需的內容檔。

支援基架非同步控制器使用實體框架6中的新異步功能。

有關詳細資訊和教程,請參閱[ASP.NET 腳手架概述](../2013/aspnet-scaffolding-overview.md)。 這些教程顯示了視覺工作室 2013 的腳手架,但它們也適用於 Visual Studio 2012 的ASP.NET和網路工具 2013.1。

<a id="razor"></a>
### <a name="razor-editor"></a>剃刀編輯器

有了這個更新,Visual Studio 2012 現在支援 Razor 3 工具/編輯。

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 包含一組豐富的新功能,在[NuGet 2.7 發行說明](http://docs.nuget.org/docs/release-notes/nuget-2.7)中對此進行了詳細介紹。

此版本的 NuGet 消除了使用者顯式允許 NuGet 還原缺少的包的需要。 安裝 NuGet 2.7 時,使用者隱式同意自動還原丟失的包。 使用者可以通過 Visual Studio 中的 NuGet 設定明確選擇退出包恢復。 此更改簡化了包還原的工作方式。

## <a name="known-issues-and-breaking-changes"></a>已知問題和重大變更

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET腳手架

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 與 Web API 基架 - HTTP 404,找不到錯誤

如果在向專案添加基架項時遇到錯誤,則專案可能會處於不一致狀態。 對基架所做的一些更改將回滾,但其他更改(如已安裝的 NuGet 包)將不會回滾。 如果路由配置更改回滾,則使用者在導航到基架專案時將收到 HTTP 404 錯誤。

要修復 MVC 的此錯誤,請添加新的腳手架項並選擇 MVC 5 依賴項(最小或完整)。 此過程將添加專案所需的所有更改。

要修復 Web API 的此錯誤,本文:

1. 將以下 WebApiConfig 類添加到專案中。

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. 在 Global.asax\_中的應用程式 啟動方法中設定 WebApiConfig.註冊,如下所示:

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>Visual Studio Express 2012 用於 Web 在新增文手架專案後停止工作

如果 Web 的 Visual Studio Express 2012 在使用實體框架添加基架專案(例如 Web API 2 控制器具有操作的操作,使用實體框架)後停止工作,則 Visual Studio Express 可能無法載入依賴於 System.Web.擴展的程式集的本機映射。

要更正此問題,請將 Visual Studio Express 設定為使用 System.Web.擴展的 MSIL 映射:

1. 在管理員模式下打開命令提示。
2. 到 %程式檔案%\微軟視覺工作室 11.0_Common7_IDE 或 %程式檔 (x86)%\微軟視覺工作室 11.0_Common7_IDE (對於 64 位元視窗)。
3. 在文字編輯器中打開 VWDExpress.exe.config。
4. &lt;&gt;在/&lt;設定&gt;執行時 元素下新增以下行:  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. 重新啟動視覺化工作室快速 2012 為 Web.

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET剃刀 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>使用「使用」或「F5」檢視 cshtml 檔會導致伺服器錯誤

當您在 Visual Studio 2012 中創建 MVC 5 專案(或在 Visual Studio 2012 中打開在 Visual Studio 2013 中建立的 MVC 5 專案)並嘗試使用「瀏覽」或 F5 查看 cshtml 檔時,您將收到一個錯誤,指出 **"/' 應用程式中的伺服器錯誤**"。 伺服器試著瀏覽到`http://localhost:XXXX/Views/../XXXX.cshtml`

要解決此問題,請將專案中的 **「開始操作」** 設定更改為 **「特定頁面**」 。 您無需為頁面提供值。

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

進行此變更後,選擇 F5 將瀏覽到應用程式`http://localhost:XXXX`的根目錄 ( 。 此行為與 Visual Studio 2013 中的 MVC 5 專案的行為不同,其中 **「當前頁面」** 設定將啟動打開頁面。

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Url 重寫和蒂爾德 (*)

升級到ASP.NET Razor 3 或 ASP.NET MVC 5 後,如果使用 URL 重寫,則波浪(*)表示法可能不再正常工作。 URL 重寫會影響&lt;HTML 元素(如 A/、SCRIPT/、LINK/&gt;&lt;&gt;&lt;&gt;等)中的波浪線(*)表示法,因此波浪線不再映射到根目錄。

例如,如果將**asp.net/content**請求重寫為**asp.net,**&lt;則 a href_"/內容/"中的 href 屬性將&gt;解析為 **/內容/內容/** 而不是**/**。 要禁止此更改,可以在每個網頁或 Global.asax 中的**\_應用程式 BeginRequest**中將**IIS\_WasUrl 重寫**上下文設置為 false。

<a id="templateissue"></a>
### <a name="templates"></a>範本

當您在 Windows 8.1 或 Windows Server 2012 R2 上使用 Visual Studio 2012 創建 ASP.NET MVC 專案時,Visual Studio 會顯示一條錯誤消息,指出"為 ASP.NET 4.5 配置 Web [url] 失敗"。

![設定錯誤](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

您會看到此錯誤,因為 Visual Studio 2012 在 Windows 這些版本上安裝時不會啟用 ASP.NET 4.5 功能。 要啟用 ASP.NET 4.5,請執行打開[或關閉"打開"Windows 功能](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)中描述的步驟。

![開啟或關閉 Windows 功能](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

或者,您可以通過命令行啟用ASP.NET 4.5。

1. 在管理員模式下打開命令提示。
2. 運行以下命令以啟用 ASP.NET 4.5。  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
