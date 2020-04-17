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
# <a name="aspnet-web-pages-razor-faq"></a><span data-ttu-id="6630c-104">ASP.NET Web Pages (Razor) 常見問題集</span><span class="sxs-lookup"><span data-stu-id="6630c-104">ASP.NET Web Pages (Razor) FAQ</span></span>

<span data-ttu-id="6630c-105"> 作者：[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6630c-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> > [!NOTE] 
> > <span data-ttu-id="6630c-106">不再建議將 WebMatrix 作為 ASP.NET 網頁的整合式開發環境。</span><span class="sxs-lookup"><span data-stu-id="6630c-106">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="6630c-107">使用[視覺工作室](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio)或[視覺工作室代碼](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="6630c-107">Use [Visual Studio](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
>
> <span data-ttu-id="6630c-108">本文列出了一些關於ASP.NET網頁(Razor)和WebMatrix的常見問題。</span><span class="sxs-lookup"><span data-stu-id="6630c-108">This article lists some frequently asked questions about ASP.NET Web Pages (Razor) and WebMatrix.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6630c-109">本教學中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="6630c-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="6630c-110">ASP.NET網頁 (剃鬚刀) 3</span><span class="sxs-lookup"><span data-stu-id="6630c-110">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="6630c-111">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="6630c-111">Visual Studio 2013</span></span>
> - <span data-ttu-id="6630c-112">Web矩陣 3</span><span class="sxs-lookup"><span data-stu-id="6630c-112">WebMatrix 3</span></span>
>   
> 
> <span data-ttu-id="6630c-113">本教學還適用於ASP.NET網頁 2、WebMatrix 2 和 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="6630c-113">This tutorial also works with ASP.NET Web Pages 2, WebMatrix 2, and Visual Studio 2012.</span></span>

- [<span data-ttu-id="6630c-114">ASP.NET網頁、ASP.NET Web 窗體和 ASP.NET MVC 之間的區別是什麼?</span><span class="sxs-lookup"><span data-stu-id="6630c-114">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [<span data-ttu-id="6630c-115">我需要 WebMatrix 才能處理網頁嗎?</span><span class="sxs-lookup"><span data-stu-id="6630c-115">Do I need WebMatrix in order to work with Web Pages?</span></span>](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [<span data-ttu-id="6630c-116">我可以在網頁頁面上使用ASP.NET Web 窗體控件嗎?</span><span class="sxs-lookup"><span data-stu-id="6630c-116">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [<span data-ttu-id="6630c-117">是否可以不使用 WebMatrix 部署 ASP.NET 網頁網站?</span><span class="sxs-lookup"><span data-stu-id="6630c-117">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [<span data-ttu-id="6630c-118">我是否要使用 Web 安全幫助程式來支援登錄?</span><span class="sxs-lookup"><span data-stu-id="6630c-118">Do I have to use the WebSecurity helper to support logins?</span></span>](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [<span data-ttu-id="6630c-119">ASP.NET網頁是否支援 HTML5?</span><span class="sxs-lookup"><span data-stu-id="6630c-119">Does ASP.NET Web Pages support HTML5?</span></span>](#Does_ASP.NET_Web_Pages_support_HTML5)
- [<span data-ttu-id="6630c-120">我可以將 JavaScript 和 jQuery 與網頁一起使用嗎?</span><span class="sxs-lookup"><span data-stu-id="6630c-120">Can I use JavaScript and jQuery with Web Pages?</span></span>](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [<span data-ttu-id="6630c-121">其他資源</span><span class="sxs-lookup"><span data-stu-id="6630c-121">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="6630c-122">有關錯誤和其他問題的問題,請參閱[ASP.NET 網頁 (Razor) 故障排除指南](https://go.microsoft.com/fwlink/?LinkId=253001)。</span><span class="sxs-lookup"><span data-stu-id="6630c-122">For questions about errors and other issues, see the [ASP.NET Web Pages (Razor) Troubleshooting Guide](https://go.microsoft.com/fwlink/?LinkId=253001).</span></span>

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a><span data-ttu-id="6630c-123">ASP.NET網頁、ASP.NET Web 窗體和 ASP.NET MVC 之間的區別是什麼?</span><span class="sxs-lookup"><span data-stu-id="6630c-123">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>

<span data-ttu-id="6630c-124">這三種技術都是建立動態 Web 應用程式的 ASP.NET 技術:</span><span class="sxs-lookup"><span data-stu-id="6630c-124">All three are ASP.NET technologies for creating dynamic web applications:</span></span>

- <span data-ttu-id="6630c-125">ASP.NET網頁側重於添加對 HTML 頁的動態(伺服器端)代碼和資料庫訪問,並具有簡單和輕量級的語法。</span><span class="sxs-lookup"><span data-stu-id="6630c-125">ASP.NET Web Pages focuses on adding dynamic (server-side) code and database access to HTML pages, and features simple and lightweight syntax.</span></span>
- <span data-ttu-id="6630c-126">ASP.NET Web 窗體基於頁面物件模型和傳統的視窗類型控制件(按鈕、清單等)。</span><span class="sxs-lookup"><span data-stu-id="6630c-126">ASP.NET Web Forms is based on a page object model and traditional window-type controls (buttons, lists, etc.).</span></span> <span data-ttu-id="6630c-127">Web 窗體使用基於事件的模型,這些模型是熟悉那些使用基於用戶端(Windows 窗體)開發的人所熟悉的。</span><span class="sxs-lookup"><span data-stu-id="6630c-127">Web Forms uses an event-based model that's familiar to those who've worked with client-based (Windows forms) development.</span></span>
- <span data-ttu-id="6630c-128">ASP.NET MVC 實現ASP.NET的模型檢視控制器模式。</span><span class="sxs-lookup"><span data-stu-id="6630c-128">ASP.NET MVC implements the model-view-controller pattern for ASP.NET.</span></span> <span data-ttu-id="6630c-129">重點是"關注點分離"(處理、數據和UI層)。</span><span class="sxs-lookup"><span data-stu-id="6630c-129">The emphasis is on "separation of concerns" (processing, data, and UI layers).</span></span>

<span data-ttu-id="6630c-130">所有三個框架都得到ASP.NET團隊的充分支援,並繼續得到開發。</span><span class="sxs-lookup"><span data-stu-id="6630c-130">All three frameworks are fully supported and continue to be developed by the ASP.NET team.</span></span> <span data-ttu-id="6630c-131">通常,選擇使用哪個框架取決於您的背景和ASP.NET的經驗。</span><span class="sxs-lookup"><span data-stu-id="6630c-131">In general, the choice of which framework to use depends on your background and experience with ASP.NET.</span></span>

<span data-ttu-id="6630c-132">ASP.NET網頁是為了讓那些已經瞭解 HTML 的用戶輕鬆地將伺服器處理添加到其頁面。</span><span class="sxs-lookup"><span data-stu-id="6630c-132">ASP.NET Web Pages in particular was designed to make it easy for people who already know HTML to add server processing to their pages.</span></span> <span data-ttu-id="6630c-133">對於學生、業餘愛好者、一般對程式設計新近的人來說,這是一個不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="6630c-133">It's a good choice for students, hobbyists, people in general who are new to programming.</span></span> <span data-ttu-id="6630c-134">對於具有non-ASP.NET Web 技術經驗的開發人員來說,這也是一個不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="6630c-134">It can also be a good choice for developers who have experience with non-ASP.NET web technologies.</span></span>

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a><span data-ttu-id="6630c-135">我需要 WebMatrix 才能處理網頁嗎?</span><span class="sxs-lookup"><span data-stu-id="6630c-135">Do I need WebMatrix in order to work with Web Pages?</span></span>

<span data-ttu-id="6630c-136">否。</span><span class="sxs-lookup"><span data-stu-id="6630c-136">No.</span></span> <span data-ttu-id="6630c-137">不再建議將 WebMatrix 作為 ASP.NET 網頁的整合式開發環境。</span><span class="sxs-lookup"><span data-stu-id="6630c-137">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="6630c-138">使用[視覺工作室](program-asp-net-web-pages-in-visual-studio.md)或[視覺工作室代碼](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="6630c-138">Use [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>

<span data-ttu-id="6630c-139">如果不想使用 Visual Studio 或 Visual Studio 代碼,則可以使用[Microsoft Web 平臺安裝程式](https://www.microsoft.com/web/downloads/platform.aspx)單獨安裝元件產品。</span><span class="sxs-lookup"><span data-stu-id="6630c-139">If you don't want to use either Visual Studio or Visual Studio Code, you can install the component products individually using [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span> <span data-ttu-id="6630c-140">您需要以下產品:</span><span class="sxs-lookup"><span data-stu-id="6630c-140">You need the following products:</span></span>

- <span data-ttu-id="6630c-141">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="6630c-141">Microsoft .NET Framework 4.5</span></span>
- <span data-ttu-id="6630c-142">ASP.NET MVC 5(也安裝 ASP.NET 網頁框架)</span><span class="sxs-lookup"><span data-stu-id="6630c-142">ASP.NET MVC 5 (which installs the ASP.NET Web Pages framework as well)</span></span>
- <span data-ttu-id="6630c-143">IIS 快遞(網路伺服器)</span><span class="sxs-lookup"><span data-stu-id="6630c-143">IIS Express (the web server)</span></span>
- <span data-ttu-id="6630c-144">微軟 SQL 伺服器緊湊型 4.0(資料庫)</span><span class="sxs-lookup"><span data-stu-id="6630c-144">Microsoft SQL Server Compact 4.0 (the database)</span></span>

<span data-ttu-id="6630c-145">您可以使用文字編輯器編輯 *.cshtml* (或 *.vbhtml*) 頁。</span><span class="sxs-lookup"><span data-stu-id="6630c-145">You can use a text editor to edit *.cshtml* (or *.vbhtml*) pages.</span></span>

<span data-ttu-id="6630c-146">在沒有工具的情況下管理 SQL Server 緊湊資料庫 *(.sdf*檔) 有點困難。</span><span class="sxs-lookup"><span data-stu-id="6630c-146">Managing SQL Server Compact databases (*.sdf* files) without a tool is a bit harder.</span></span> <span data-ttu-id="6630c-147">可視化工作室包含用於管理 *.sdf*資料庫的工具。</span><span class="sxs-lookup"><span data-stu-id="6630c-147">Visual Studio containds tools for managing *.sdf* databases.</span></span> <span data-ttu-id="6630c-148">您還可以在代碼中執行 SQL 命令以執行許多 SQL Server 管理任務。</span><span class="sxs-lookup"><span data-stu-id="6630c-148">You can also run SQL commands in code to perform many SQL Server management tasks.</span></span>

<span data-ttu-id="6630c-149">要測試 *.cshtml*頁面而不使用整合式開發環境 (IDE),可以將它們部署到即時伺服器。</span><span class="sxs-lookup"><span data-stu-id="6630c-149">To test *.cshtml* pages without using an integrated development environment (IDE), you can deploy them to a live server.</span></span> <span data-ttu-id="6630c-150">(請參閱[不使用 WebMatrix 即可部署 ASP.NET 網頁網站嗎?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)</span><span class="sxs-lookup"><span data-stu-id="6630c-150">(See [Can I deploy an ASP.NET Web Pages site without using WebMatrix?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))</span></span>

### <a name="running-iis-express-without-using-an-ide"></a><span data-ttu-id="6630c-151">執行 IIS 快遞而不使用 IDE</span><span class="sxs-lookup"><span data-stu-id="6630c-151">Running IIS Express without using an IDE</span></span>

<span data-ttu-id="6630c-152">如果在電腦上將 IIS Express 安裝為 Web 伺服器,則可以使用它來測試頁面。</span><span class="sxs-lookup"><span data-stu-id="6630c-152">If you install IIS Express on your computer as a web server, you can use that to test the pages.</span></span> <span data-ttu-id="6630c-153">可以從命令列運行IIS Express並將其與特定的埠號相關聯。</span><span class="sxs-lookup"><span data-stu-id="6630c-153">You can run IIS Express from the command line and associate it with a specific port number.</span></span> <span data-ttu-id="6630c-154">然後在瀏覽器中請求 *.cshtml*檔時指定該埠。</span><span class="sxs-lookup"><span data-stu-id="6630c-154">You then specify that port when you request *.cshtml* files in your browser.</span></span>

<span data-ttu-id="6630c-155">在 Windows 中,打開具有管理員許可權的命令提示符,然後更改為*C:*程式檔_IIS Express。\*</span><span class="sxs-lookup"><span data-stu-id="6630c-155">In Windows, open a command prompt with administrator privileges and change to *C:\Program Files\IIS Express.*</span></span> <span data-ttu-id="6630c-156">(對於 64 位元系統,請使用資料夾*C:*程式檔 (x86)\IIS Express。\* 然後輸入以下指令,使用網站的實際路徑:</span><span class="sxs-lookup"><span data-stu-id="6630c-156">(For 64-bit systems, use the folder *C:\Program Files (x86)\IIS Express.)* Then enter the following command, using the actual path to your site:</span></span>

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

<span data-ttu-id="6630c-157">您可以使用任何其他進程尚未保留的任何埠號。</span><span class="sxs-lookup"><span data-stu-id="6630c-157">You can use any port number that isn't already reserved by some other process.</span></span> <span data-ttu-id="6630c-158">(1024 以上的埠號通常是免費的。對於該`path`值,請使用 *.cshtml*檔案所在的網站資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="6630c-158">(Port numbers above 1024 are typically free.) For the `path` value, use the path of the website folder where the *.cshtml* files are.</span></span>

<span data-ttu-id="6630c-159">運行此指令以設置 IIS Express 為頁面提供服務後,可以打開瀏覽器並瀏覽到 *.cshtml*檔。</span><span class="sxs-lookup"><span data-stu-id="6630c-159">After you run this command to set up IIS Express to serve your pages, you can open a browser and browse to a *.cshtml* file.</span></span> <span data-ttu-id="6630c-160">使用以下的網址:</span><span class="sxs-lookup"><span data-stu-id="6630c-160">Use a URL like the following:</span></span>

`http://localhost:35896/default.cshtml`

<span data-ttu-id="6630c-161">有關 IIS Express 命令列`iisexpress.exe /?`選項的説明 ,請在命令列處輸入。</span><span class="sxs-lookup"><span data-stu-id="6630c-161">For help with IIS Express command line options, enter `iisexpress.exe /?` at the command line.</span></span>

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a><span data-ttu-id="6630c-162">我可以在網頁頁面上使用ASP.NET Web 窗體控件嗎?</span><span class="sxs-lookup"><span data-stu-id="6630c-162">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>

<span data-ttu-id="6630c-163">否。</span><span class="sxs-lookup"><span data-stu-id="6630c-163">No.</span></span> <span data-ttu-id="6630c-164">Web 表單控制項(如[CheckBox 控制件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox)、[驗證控制件](https://msdn.microsoft.com/library/bwd43d0x))和[GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview)控制項僅在 Web 窗體頁 *(.aspx*檔案)中工作。</span><span class="sxs-lookup"><span data-stu-id="6630c-164">Web Forms controls like the [CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) control, the [validation controls](https://msdn.microsoft.com/library/bwd43d0x), and the [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) control only work in Web Forms pages (*.aspx* files).</span></span> <span data-ttu-id="6630c-165">這些控制者需要 Web 窗體頁面框架。</span><span class="sxs-lookup"><span data-stu-id="6630c-165">These controls require the Web Forms page framework.</span></span>

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a><span data-ttu-id="6630c-166">是否可以不使用 WebMatrix 部署 ASP.NET 網頁網站?</span><span class="sxs-lookup"><span data-stu-id="6630c-166">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>

<span data-ttu-id="6630c-167">是。</span><span class="sxs-lookup"><span data-stu-id="6630c-167">Yes.</span></span> <span data-ttu-id="6630c-168">您可以手動將網站檔案複製到伺服器(通常使用 FTP)。</span><span class="sxs-lookup"><span data-stu-id="6630c-168">You can manually copy website files to a server (typically by using FTP).</span></span> <span data-ttu-id="6630c-169">如果執行手動複製,還必須複製支援 SQL Server 壓縮(資料庫)的檔。</span><span class="sxs-lookup"><span data-stu-id="6630c-169">If you perform a manual copy, you also have to copy the files that support SQL Server Compact (the database).</span></span> <span data-ttu-id="6630c-170">有關詳細資訊,請參閱[沒有工具部署網頁應用程式的](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)博客條目。</span><span class="sxs-lookup"><span data-stu-id="6630c-170">For details, see the blog entry [Deploying Web Pages applications without a tool](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317).</span></span>

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a><span data-ttu-id="6630c-171">我是否要使用 Web 安全幫助程式來支援登錄?</span><span class="sxs-lookup"><span data-stu-id="6630c-171">Do I have to use the WebSecurity helper to support logins?</span></span>

<span data-ttu-id="6630c-172">否。</span><span class="sxs-lookup"><span data-stu-id="6630c-172">No.</span></span> <span data-ttu-id="6630c-173">屬於`SimpleMembership`ASP.NET 網頁的提供程式是一個選項。</span><span class="sxs-lookup"><span data-stu-id="6630c-173">The `SimpleMembership` provider that is part of ASP.NET Web Pages is one option.</span></span> <span data-ttu-id="6630c-174">屬於ASP.NET(您可能習慣於在Web窗體中使用)的安全提供程式也可用。</span><span class="sxs-lookup"><span data-stu-id="6630c-174">The security providers that are part of ASP.NET (that you might be used to working with in Web Forms) are also available.</span></span> <span data-ttu-id="6630c-175">例如,您可以在ASP.NET網頁中使用窗體身份驗證,就像在Web窗體中一樣。</span><span class="sxs-lookup"><span data-stu-id="6630c-175">For example, you can use forms authentication in ASP.NET Web Pages just as you would in Web Forms.</span></span> <span data-ttu-id="6630c-176">有關如何使用表單身份驗證的一個範例,請參閱 Microsoft 支援文章[「如何使用 C_.NET 在ASP.NET應用程式中實現基於表單的身份驗證](https://support.microsoft.com/kb/301240)。</span><span class="sxs-lookup"><span data-stu-id="6630c-176">For one example of how to use forms authentication, see the Microsoft Support article [How To Implement Forms-Based Authentication in Your ASP.NET Application by Using C#.NET](https://support.microsoft.com/kb/301240).</span></span> <span data-ttu-id="6630c-177">要下載一個簡單的範例,請參閱[ASP.NET 版本的&amp;「登入密碼](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)」。。</span><span class="sxs-lookup"><span data-stu-id="6630c-177">To download a simple example, see [ASP.NET version of "Login &amp; Password](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).</span></span>

<span data-ttu-id="6630c-178">有關如何使用 Windows 身份驗證的資訊,請參閱[ASP.NET 網頁中使用 Windows 身份驗證的](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)部落格文章。</span><span class="sxs-lookup"><span data-stu-id="6630c-178">For information about how to use Windows authentication, see the blog post [Using Windows authentication in ASP.NET Web Pages](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298).</span></span>

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a><span data-ttu-id="6630c-179">ASP.NET網頁是否支援 HTML5?</span><span class="sxs-lookup"><span data-stu-id="6630c-179">Does ASP.NET Web Pages support HTML5?</span></span>

<span data-ttu-id="6630c-180">是。</span><span class="sxs-lookup"><span data-stu-id="6630c-180">Yes.</span></span> <span data-ttu-id="6630c-181">使用ASP.NET網頁 *(.cshtml*或 *.vbhtml*頁)創建的頁面本質上是 HTML 頁面,這些頁面還包含在呈現頁面之前在伺服器上運行的代碼。</span><span class="sxs-lookup"><span data-stu-id="6630c-181">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are essentially HTML pages that also contain code that runs on the server, before the page is rendered.</span></span> <span data-ttu-id="6630c-182">只要使用者的瀏覽器支援 HTML5,就可以在 *.cshtml*或 *.vbhtml*頁面中使用 HTML5 元素。</span><span class="sxs-lookup"><span data-stu-id="6630c-182">As long as the user's browser supports HTML5, you can use HTML5 elements in a *.cshtml* or *.vbhtml* page.</span></span>

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a><span data-ttu-id="6630c-183">我可以將 JavaScript 和 jQuery 與網頁一起使用嗎?</span><span class="sxs-lookup"><span data-stu-id="6630c-183">Can I use JavaScript and jQuery with Web Pages?</span></span>

<span data-ttu-id="6630c-184">當然。</span><span class="sxs-lookup"><span data-stu-id="6630c-184">Absolutely.</span></span> <span data-ttu-id="6630c-185">使用ASP.NET網頁 *(.cshtml*或 *.vbhtml*頁)創建的頁面只是包含伺服器代碼的 HTML 頁。</span><span class="sxs-lookup"><span data-stu-id="6630c-185">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are just HTML pages with server code in them.</span></span> <span data-ttu-id="6630c-186">因此,使用 JavaScript 或 jQuery 可以在普通 HTML 頁中執行的任何操作,您也可以在 *.cshtml*或 *.vbhtml*頁中執行。</span><span class="sxs-lookup"><span data-stu-id="6630c-186">Therefore, anything you can do in a normal HTML page by using JavaScript or jQuery you can also do in a *.cshtml* or *.vbhtml* page.</span></span>

<span data-ttu-id="6630c-187">WebMatrix 中的**初學者網站**範本包含許多 jQuery 庫。</span><span class="sxs-lookup"><span data-stu-id="6630c-187">The **Starter Site** template in WebMatrix contains a number of jQuery libraries.</span></span> <span data-ttu-id="6630c-188">如果使用該範本創建網站,*文稿*文件包含 jQuery 核心庫 *(jquery-1.6.2.js)* 和 jQuery 驗證庫 *(jquery.validate.js*等)。</span><span class="sxs-lookup"><span data-stu-id="6630c-188">If you create a site by using that template, the *Scripts* folder contains a jQuery core library (*jquery-1.6.2.js)* and libraries for jQuery validation (*jquery.validate.js*, etc.).</span></span>

<span data-ttu-id="6630c-189">下面是一些博客文章,說明如何使用 jQuery 與ASP.NET網頁:</span><span class="sxs-lookup"><span data-stu-id="6630c-189">Here are some blog posts that illustrate ways to use jQuery with ASP.NET Web Pages:</span></span>

- <span data-ttu-id="6630c-190">[將 jQuery 善用新增到 ASP.NET網頁,使用](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/)Rachel Appel 的 WebMatrix</span><span class="sxs-lookup"><span data-stu-id="6630c-190">[Adding jQuery Goodness to ASP.NET Web Pages using WebMatrix](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) by Rachel Appel</span></span>
- <span data-ttu-id="6630c-191">[5分鐘: WebMatrix + jQuery UI + json + jQuery範本](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/)由喬納斯·埃裡克森</span><span class="sxs-lookup"><span data-stu-id="6630c-191">[5 min: WebMatrix + jQuery UI + json + jQuery templates](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) by Jonas Eriksson</span></span>
- <span data-ttu-id="6630c-192">邁克·布林德的[WebMatrix 和 jQuery 表單](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)</span><span class="sxs-lookup"><span data-stu-id="6630c-192">[WebMatrix And jQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) by Mike Brind</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="6630c-193">其他資源</span><span class="sxs-lookup"><span data-stu-id="6630c-193">Additional Resources</span></span>

[<span data-ttu-id="6630c-194">ASP.NET Web Pages (Razor) 疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="6630c-194">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>](https://go.microsoft.com/fwlink/?LinkId=253001)

<span data-ttu-id="6630c-195">[網站網站WebMatrix和ASP.NET網頁論壇](https://forums.asp.net/1224.aspx/1?WebMatrix)ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6630c-195">[WebMatrix and ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix) on the ASP.NET website</span></span>
