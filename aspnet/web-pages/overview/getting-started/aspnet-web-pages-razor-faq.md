---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET網頁(剃鬚刀)常見問題 |微軟文件
author: Rick-Anderson
description: 本文列出了一些關於ASP.NET網頁(Razor)和WebMatrix的常見問題。 教學中使用的軟體版本ASP.NET網頁 (R...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: a312d1327bc88e721bf7fc7459e420e3f582c88d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543700"
---
# <a name="aspnet-web-pages-razor-faq"></a>ASP.NET Web Pages (Razor) 常見問題集

 作者：[Tom FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > 不再建議將 WebMatrix 作為 ASP.NET 網頁的整合式開發環境。 使用[視覺工作室](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio)或[視覺工作室代碼](https://code.visualstudio.com/)。
>
> 本文列出了一些關於ASP.NET網頁(Razor)和WebMatrix的常見問題。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教學中使用的軟體版本
> 
> 
> - ASP.NET網頁 (剃鬚刀) 3
> - Visual Studio 2013
> - Web矩陣 3
>   
> 
> 本教學還適用於ASP.NET網頁 2、WebMatrix 2 和 Visual Studio 2012。

- [ASP.NET網頁、ASP.NET Web 窗體和 ASP.NET MVC 之間的區別是什麼?](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [我需要 WebMatrix 才能處理網頁嗎?](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [我可以在網頁頁面上使用ASP.NET Web 窗體控件嗎?](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [是否可以不使用 WebMatrix 部署 ASP.NET 網頁網站?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [我是否要使用 Web 安全幫助程式來支援登錄?](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [ASP.NET網頁是否支援 HTML5?](#Does_ASP.NET_Web_Pages_support_HTML5)
- [我可以將 JavaScript 和 jQuery 與網頁一起使用嗎?](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [其他資源](#AdditionalResources)

有關錯誤和其他問題的問題,請參閱[ASP.NET 網頁 (Razor) 故障排除指南](https://go.microsoft.com/fwlink/?LinkId=253001)。

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>ASP.NET網頁、ASP.NET Web 窗體和 ASP.NET MVC 之間的區別是什麼?

這三種技術都是建立動態 Web 應用程式的 ASP.NET 技術:

- ASP.NET網頁側重於添加對 HTML 頁的動態(伺服器端)代碼和資料庫訪問,並具有簡單和輕量級的語法。
- ASP.NET Web 窗體基於頁面物件模型和傳統的視窗類型控制件(按鈕、清單等)。 Web 窗體使用基於事件的模型,這些模型是熟悉那些使用基於用戶端(Windows 窗體)開發的人所熟悉的。
- ASP.NET MVC 實現ASP.NET的模型檢視控制器模式。 重點是"關注點分離"(處理、數據和UI層)。

所有三個框架都得到ASP.NET團隊的充分支援,並繼續得到開發。 通常,選擇使用哪個框架取決於您的背景和ASP.NET的經驗。

ASP.NET網頁是為了讓那些已經瞭解 HTML 的用戶輕鬆地將伺服器處理添加到其頁面。 對於學生、業餘愛好者、一般對程式設計新近的人來說,這是一個不錯的選擇。 對於具有non-ASP.NET Web 技術經驗的開發人員來說,這也是一個不錯的選擇。

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>我需要 WebMatrix 才能處理網頁嗎?

否。 不再建議將 WebMatrix 作為 ASP.NET 網頁的整合式開發環境。 使用[視覺工作室](program-asp-net-web-pages-in-visual-studio.md)或[視覺工作室代碼](https://code.visualstudio.com/)。

如果不想使用 Visual Studio 或 Visual Studio 代碼,則可以使用[Microsoft Web 平臺安裝程式](https://www.microsoft.com/web/downloads/platform.aspx)單獨安裝元件產品。 您需要以下產品:

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5(也安裝 ASP.NET 網頁框架)
- IIS 快遞(網路伺服器)
- 微軟 SQL 伺服器緊湊型 4.0(資料庫)

您可以使用文字編輯器編輯 *.cshtml* (或 *.vbhtml*) 頁。

在沒有工具的情況下管理 SQL Server 緊湊資料庫 *(.sdf*檔) 有點困難。 可視化工作室包含用於管理 *.sdf*資料庫的工具。 您還可以在代碼中執行 SQL 命令以執行許多 SQL Server 管理任務。

要測試 *.cshtml*頁面而不使用整合式開發環境 (IDE),可以將它們部署到即時伺服器。 (請參閱[不使用 WebMatrix 即可部署 ASP.NET 網頁網站嗎?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)

### <a name="running-iis-express-without-using-an-ide"></a>執行 IIS 快遞而不使用 IDE

如果在電腦上將 IIS Express 安裝為 Web 伺服器,則可以使用它來測試頁面。 可以從命令列運行IIS Express並將其與特定的埠號相關聯。 然後在瀏覽器中請求 *.cshtml*檔時指定該埠。

在 Windows 中,打開具有管理員許可權的命令提示符,然後更改為*C:*程式檔_IIS Express。* (對於 64 位元系統,請使用資料夾*C:*程式檔 (x86)\IIS Express。* 然後輸入以下指令,使用網站的實際路徑:

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

您可以使用任何其他進程尚未保留的任何埠號。 (1024 以上的埠號通常是免費的。對於該`path`值,請使用 *.cshtml*檔案所在的網站資料夾的路徑。

運行此指令以設置 IIS Express 為頁面提供服務後,可以打開瀏覽器並瀏覽到 *.cshtml*檔。 使用以下的網址:

`http://localhost:35896/default.cshtml`

有關 IIS Express 命令列`iisexpress.exe /?`選項的説明 ,請在命令列處輸入。

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>我可以在網頁頁面上使用ASP.NET Web 窗體控件嗎?

否。 Web 表單控制項(如[CheckBox 控制件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox)、[驗證控制件](https://msdn.microsoft.com/library/bwd43d0x))和[GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview)控制項僅在 Web 窗體頁 *(.aspx*檔案)中工作。 這些控制者需要 Web 窗體頁面框架。

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>是否可以不使用 WebMatrix 部署 ASP.NET 網頁網站?

是。 您可以手動將網站檔案複製到伺服器(通常使用 FTP)。 如果執行手動複製,還必須複製支援 SQL Server 壓縮(資料庫)的檔。 有關詳細資訊,請參閱[沒有工具部署網頁應用程式的](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)博客條目。

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>我是否要使用 Web 安全幫助程式來支援登錄?

否。 屬於`SimpleMembership`ASP.NET 網頁的提供程式是一個選項。 屬於ASP.NET(您可能習慣於在Web窗體中使用)的安全提供程式也可用。 例如,您可以在ASP.NET網頁中使用窗體身份驗證,就像在Web窗體中一樣。 有關如何使用表單身份驗證的一個範例,請參閱 Microsoft 支援文章[「如何使用 C_.NET 在ASP.NET應用程式中實現基於表單的身份驗證](https://support.microsoft.com/kb/301240)。 要下載一個簡單的範例,請參閱[ASP.NET 版本的&amp;「登入密碼](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)」。。

有關如何使用 Windows 身份驗證的資訊,請參閱[ASP.NET 網頁中使用 Windows 身份驗證的](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)部落格文章。

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>ASP.NET網頁是否支援 HTML5?

是。 使用ASP.NET網頁 *(.cshtml*或 *.vbhtml*頁)創建的頁面本質上是 HTML 頁面,這些頁面還包含在呈現頁面之前在伺服器上運行的代碼。 只要使用者的瀏覽器支援 HTML5,就可以在 *.cshtml*或 *.vbhtml*頁面中使用 HTML5 元素。

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>我可以將 JavaScript 和 jQuery 與網頁一起使用嗎?

當然。 使用ASP.NET網頁 *(.cshtml*或 *.vbhtml*頁)創建的頁面只是包含伺服器代碼的 HTML 頁。 因此,使用 JavaScript 或 jQuery 可以在普通 HTML 頁中執行的任何操作,您也可以在 *.cshtml*或 *.vbhtml*頁中執行。

WebMatrix 中的**初學者網站**範本包含許多 jQuery 庫。 如果使用該範本創建網站,*文稿*文件包含 jQuery 核心庫 *(jquery-1.6.2.js)* 和 jQuery 驗證庫 *(jquery.validate.js*等)。

下面是一些博客文章,說明如何使用 jQuery 與ASP.NET網頁:

- [將 jQuery 善用新增到 ASP.NET網頁,使用](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/)Rachel Appel 的 WebMatrix
- [5分鐘: WebMatrix + jQuery UI + json + jQuery範本](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/)由喬納斯·埃裡克森
- 邁克·布林德的[WebMatrix 和 jQuery 表單](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>其他資源

[ASP.NET Web Pages (Razor) 疑難排解指南](https://go.microsoft.com/fwlink/?LinkId=253001)

[網站網站WebMatrix和ASP.NET網頁論壇](https://forums.asp.net/1224.aspx/1?WebMatrix)ASP.NET
