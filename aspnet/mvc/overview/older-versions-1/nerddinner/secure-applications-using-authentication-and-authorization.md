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
# <a name="secure-applications-using-authentication-and-authorization"></a><span data-ttu-id="262aa-103">保護使用驗證和授權的應用程式</span><span class="sxs-lookup"><span data-stu-id="262aa-103">Secure Applications Using Authentication and Authorization</span></span>

<span data-ttu-id="262aa-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="262aa-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="262aa-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="262aa-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="262aa-106">這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第9步,該教程示範如何使用mVC 1 構建小型但完整的 Web 應用程式ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="262aa-106">This is step 9 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="262aa-107">步驟 9 演示如何添加身份驗證和授權來保護我們的 NerdDinner 應用程式,以便使用者需要註冊並登錄到網站以創建新的晚餐,並且只有主持晚宴的使用者才能稍後對其進行編輯。</span><span class="sxs-lookup"><span data-stu-id="262aa-107">Step 9 shows how to add authentication and authorization to secure our NerdDinner application, so that users need to register and login to the site to create new dinners, and only the user who is hosting a dinner can edit it later.</span></span>
> 
> <span data-ttu-id="262aa-108">如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。</span><span class="sxs-lookup"><span data-stu-id="262aa-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-9-authentication-and-authorization"></a><span data-ttu-id="262aa-109">神經晚餐步驟 9:身份驗證和授權</span><span class="sxs-lookup"><span data-stu-id="262aa-109">NerdDinner Step 9: Authentication and Authorization</span></span>

<span data-ttu-id="262aa-110">現在,我們的NerdDinner應用程式允許任何訪問該網站的人能夠創建和編輯任何晚餐的細節。</span><span class="sxs-lookup"><span data-stu-id="262aa-110">Right now our NerdDinner application grants anyone visiting the site the ability to create and edit the details of any dinner.</span></span> <span data-ttu-id="262aa-111">讓我們更改此內容,以便使用者需要註冊並登錄到網站以創建新的晚餐,並添加限制,以便只有主持晚宴的使用者才能稍後對其進行編輯。</span><span class="sxs-lookup"><span data-stu-id="262aa-111">Let's change this so that users need to register and login to the site to create new dinners, and add a restriction so that only the user who is hosting a dinner can edit it later.</span></span>

<span data-ttu-id="262aa-112">為了啟用此功能,我們將使用身份驗證和授權來保護我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="262aa-112">To enable this we'll use authentication and authorization to secure our application.</span></span>

### <a name="understanding-authentication-and-authorization"></a><span data-ttu-id="262aa-113">瞭解認證與授權</span><span class="sxs-lookup"><span data-stu-id="262aa-113">Understanding Authentication and Authorization</span></span>

<span data-ttu-id="262aa-114">*身份驗證*是標識和驗證訪問應用程式的客戶端的標識的過程。</span><span class="sxs-lookup"><span data-stu-id="262aa-114">*Authentication* is the process of identifying and validating the identity of a client accessing an application.</span></span> <span data-ttu-id="262aa-115">簡單地說,它是關於確定最終使用者在訪問網站時的"誰"。</span><span class="sxs-lookup"><span data-stu-id="262aa-115">Put more simply, it is about identifying "who" the end-user is when they visit a website.</span></span> <span data-ttu-id="262aa-116">ASP.NET支援對瀏覽器使用者進行身份驗證的多種方法。</span><span class="sxs-lookup"><span data-stu-id="262aa-116">ASP.NET supports multiple ways to authenticate browser users.</span></span> <span data-ttu-id="262aa-117">對於 Internet Web 應用程式,最常用的身份驗證方法稱為"表單身份驗證」。。</span><span class="sxs-lookup"><span data-stu-id="262aa-117">For Internet web applications, the most common authentication approach used is called "Forms Authentication".</span></span> <span data-ttu-id="262aa-118">表單身份驗證使開發人員能夠在其應用程式中創作 HTML 登入表單,然後根據資料庫或其他密碼認證認證最終使用者提交的使用者名/密碼。</span><span class="sxs-lookup"><span data-stu-id="262aa-118">Forms Authentication enables a developer to author an HTML login form within their application, and then validate the username/password an end-user submits against a database or other password credential store.</span></span> <span data-ttu-id="262aa-119">如果使用者名/密碼組合正確,開發人員可以請求ASP.NET發出加密的 HTTP Cookie,以識別使用者在未來的請求。</span><span class="sxs-lookup"><span data-stu-id="262aa-119">If the username/password combination is correct, the developer can then ask ASP.NET to issue an encrypted HTTP cookie to identify the user across future requests.</span></span> <span data-ttu-id="262aa-120">我們將使用表單身份驗證來使用我們的NerdDinner應用程式。</span><span class="sxs-lookup"><span data-stu-id="262aa-120">We'll by using forms authentication with our NerdDinner application.</span></span>

<span data-ttu-id="262aa-121">*授權*是確定經過身份驗證的使用者是否具有訪問特定 URL/資源或執行某些操作的許可權的過程。</span><span class="sxs-lookup"><span data-stu-id="262aa-121">*Authorization* is the process of determining whether an authenticated user has permission to access a particular URL/resource or to perform some action.</span></span> <span data-ttu-id="262aa-122">例如,在我們的NerdDinner應用程式中,我們希望授權只有登錄的使用者才能訪問 */Dinners/創建*URL並創建新的晚餐。</span><span class="sxs-lookup"><span data-stu-id="262aa-122">For example, within our NerdDinner application we'll want to authorize that only users who are logged in can access the */Dinners/Create* URL and create new Dinners.</span></span> <span data-ttu-id="262aa-123">我們還希望添加授權邏輯,以便只有主持晚宴的使用者才能對其進行編輯,並拒絕對所有其他使用者進行編輯訪問。</span><span class="sxs-lookup"><span data-stu-id="262aa-123">We'll also want to add authorization logic so that only the user who is hosting a dinner can edit it – and deny edit access to all other users.</span></span>

### <a name="forms-authentication-and-the-accountcontroller"></a><span data-ttu-id="262aa-124">表單識別識別和帳戶控制器</span><span class="sxs-lookup"><span data-stu-id="262aa-124">Forms Authentication and the AccountController</span></span>

<span data-ttu-id="262aa-125">ASP.NET MVC 的預設 Visual Studio 專案範本在創建新 ASP.NET MVC 應用程式時自動啟用表單身份驗證。</span><span class="sxs-lookup"><span data-stu-id="262aa-125">The default Visual Studio project template for ASP.NET MVC automatically enables forms authentication when new ASP.NET MVC applications are created.</span></span> <span data-ttu-id="262aa-126">它還會自動向專案添加預構建的帳戶登錄頁實現,從而在網站中集成安全性非常容易。</span><span class="sxs-lookup"><span data-stu-id="262aa-126">It also automatically adds a pre-built account login page implementation to the project – which makes it really easy to integrate security within a site.</span></span>

<span data-ttu-id="262aa-127">預設的 Site.master 頁在網站右上角顯示「登錄」連結,當使用者存取該網站時未進行身份驗證:</span><span class="sxs-lookup"><span data-stu-id="262aa-127">The default Site.master master page displays a "Log On" link at the top-right of the site when the user accessing it is not authenticated:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

<span data-ttu-id="262aa-128">點選「登入」連結會將使用者帶到 */帳戶/登錄*URL:</span><span class="sxs-lookup"><span data-stu-id="262aa-128">Clicking the "Log On" link takes a user to the */Account/LogOn* URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

<span data-ttu-id="262aa-129">尚未註冊的存取者可以透過按下「註冊」連結(該連結將他們帶到 */帳戶/註冊*URL)並允許您輸入帳戶詳細資訊來執行此操作:</span><span class="sxs-lookup"><span data-stu-id="262aa-129">Visitors who haven't registered can do so by clicking the "Register" link – which will take them to the */Account/Register* URL and allow them to enter account details:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

<span data-ttu-id="262aa-130">按下「註冊」按鈕將在ASP.NET成員資格系統中創建新使用者,並使用表單身份驗證對使用者進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="262aa-130">Clicking the "Register" button will create a new user within the ASP.NET Membership system, and authenticate the user onto the site using forms authentication.</span></span>

<span data-ttu-id="262aa-131">當使用者登錄時,Site.master 會更改頁面的右上角以輸出「歡迎 [使用者名]!</span><span class="sxs-lookup"><span data-stu-id="262aa-131">When a user is logged-in, the Site.master changes the top-right of the page to output a "Welcome [username]!"</span></span> <span data-ttu-id="262aa-132">消息並呈現「註銷」連結,而不是「登錄」連結。</span><span class="sxs-lookup"><span data-stu-id="262aa-132">message and renders a "Log Off" link instead of a "Log On" one.</span></span> <span data-ttu-id="262aa-133">點選「登出」連結會登出使用者:</span><span class="sxs-lookup"><span data-stu-id="262aa-133">Clicking the "Log Off" link logs out the user:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

<span data-ttu-id="262aa-134">上述登錄、註銷和註冊功能在帳戶控制器類中實現,該類在創建專案時由 Visual Studio 添加到我們的專案中。</span><span class="sxs-lookup"><span data-stu-id="262aa-134">The above login, logout, and registration functionality is implemented within the AccountController class that was added to our project by Visual Studio when it created the project.</span></span> <span data-ttu-id="262aa-135">帳號控制器的 UI 使用 [Views_帳戶目錄中的檢視範本] 實現:</span><span class="sxs-lookup"><span data-stu-id="262aa-135">The UI for the AccountController is implemented using view templates within the \Views\Account directory:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

<span data-ttu-id="262aa-136">帳戶控制器類使用ASP.NET表單身份驗證系統來發出加密的身份驗證 Cookie,ASP.NET成員資格 API 來存儲和驗證使用者名/密碼。</span><span class="sxs-lookup"><span data-stu-id="262aa-136">The AccountController class uses the ASP.NET Forms Authentication system to issue encrypted authentication cookies, and the ASP.NET Membership API to store and validate usernames/passwords.</span></span> <span data-ttu-id="262aa-137">ASP.NET成員資格 API 是可擴展的,並且允許使用任何密碼憑據存儲。</span><span class="sxs-lookup"><span data-stu-id="262aa-137">The ASP.NET Membership API is extensible and enables any password credential store to be used.</span></span> <span data-ttu-id="262aa-138">ASP.NET附帶將使用者名/密碼存儲在 SQL 資料庫或活動目錄中的內置成員資格提供程式實現。</span><span class="sxs-lookup"><span data-stu-id="262aa-138">ASP.NET ships with built-in membership provider implementations that store username/passwords within a SQL database, or within Active Directory.</span></span>

<span data-ttu-id="262aa-139">我們可以通過打開專案根目錄的"Web.config"檔並在其中查找&lt;成員&gt;資格 部分來配置我們的NerdDinner應用程式應該使用的成員供應商。</span><span class="sxs-lookup"><span data-stu-id="262aa-139">We can configure which membership provider our NerdDinner application should use by opening the "web.config" file at the root of the project and looking for the &lt;membership&gt; section within it.</span></span> <span data-ttu-id="262aa-140">創建專案時添加的預設 Web.config 會註冊 SQL 成員資格提供程式,並將其配置為使用名為"應用程式服務"的連接字串來指定資料庫位置。</span><span class="sxs-lookup"><span data-stu-id="262aa-140">The default web.config added when the project was created registers the SQL membership provider, and configures it to use a connection-string named "ApplicationServices" to specify the database location.</span></span>

<span data-ttu-id="262aa-141">預設的「應用程式服務」 連接字串(在 Web.config&lt;&gt;檔案的連接字串部分中指定)設定為使用 SQL Express。</span><span class="sxs-lookup"><span data-stu-id="262aa-141">The default "ApplicationServices" connection string (which is specified within the &lt;connectionStrings&gt; section of the web.config file) is configured to use SQL Express.</span></span> <span data-ttu-id="262aa-142">它指向名為「ASPNETDB」的 SQL Express 資料庫。MDF"在應用程式的"應用\_資料"目錄下。</span><span class="sxs-lookup"><span data-stu-id="262aa-142">It points to a SQL Express database named "ASPNETDB.MDF" under the application's "App\_Data" directory.</span></span> <span data-ttu-id="262aa-143">如果首次在應用程式中使用成員資格 API 時此資料庫不存在,ASP.NET將自動建立資料庫並在其中預配適當的成員資格資料庫架構:</span><span class="sxs-lookup"><span data-stu-id="262aa-143">If this database doesn't exist the first time the Membership API is used within the application, ASP.NET will automatically create the database and provision the appropriate membership database schema within it:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

<span data-ttu-id="262aa-144">如果我們不想使用 SQL Express,而是想要使用完整的 SQL Server 實例(或連接到遠端資料庫),我們只需更新 Web.config 檔中的「應用程式服務」連接字串,並確保適當的成員資格架構已添加到它指向的資料庫。</span><span class="sxs-lookup"><span data-stu-id="262aa-144">If instead of using SQL Express we wanted to use a full SQL Server instance (or connect to a remote database), all we'd need to-do is to update the "ApplicationServices" connection string within the web.config file and make sure that the appropriate membership schema has been added to the database it points at.</span></span> <span data-ttu-id="262aa-145">您可以在 [Windows_Microsoft.NET_Framework_v2.0.50727] 目錄中運行"aspnet\_regsql.exe"實用程式,以將成員資格和其他ASP.NET應用程式服務的適當架構添加到資料庫中。</span><span class="sxs-lookup"><span data-stu-id="262aa-145">You can run the "aspnet\_regsql.exe" utility within the \Windows\Microsoft.NET\Framework\v2.0.50727\ directory to add the appropriate schema for membership and the other ASP.NET application services to a database.</span></span>

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a><span data-ttu-id="262aa-146">使用授權帳號授權 /Dinners/建立 URL</span><span class="sxs-lookup"><span data-stu-id="262aa-146">Authorizing the /Dinners/Create URL using the [Authorize] filter</span></span>

<span data-ttu-id="262aa-147">我們不必編寫任何代碼來為NerdDinner應用程式啟用安全的身份驗證和帳戶管理實現。</span><span class="sxs-lookup"><span data-stu-id="262aa-147">We didn't have to write any code to enable a secure authentication and account management implementation for the NerdDinner application.</span></span> <span data-ttu-id="262aa-148">用戶可以在我們的應用程式中註冊新帳戶,以及網站登錄/註銷。</span><span class="sxs-lookup"><span data-stu-id="262aa-148">Users can register new accounts with our application, and login/logout of the site.</span></span>

<span data-ttu-id="262aa-149">現在,我們可以向應用程式添加授權邏輯,並使用訪問者的身份驗證狀態和使用者名來控制他們在網站內可以做什麼和不能做什麼。</span><span class="sxs-lookup"><span data-stu-id="262aa-149">Now we can add authorization logic to the application, and use the authentication status and username of visitors to control what they can and can't do within the site.</span></span> <span data-ttu-id="262aa-150">讓我們首先將授權邏輯添加到 DinnersController 類的"創建"操作方法。</span><span class="sxs-lookup"><span data-stu-id="262aa-150">Let's begin by adding authorization logic to the "Create" action methods of our DinnersController class.</span></span> <span data-ttu-id="262aa-151">具體來說,我們將要求訪問 */Dinner/Create* URL 的用戶必須登錄。</span><span class="sxs-lookup"><span data-stu-id="262aa-151">Specifically, we will require that users accessing the */Dinners/Create* URL must be logged in.</span></span> <span data-ttu-id="262aa-152">如果他們沒有登錄,我們會將其重定向到登錄頁面,以便他們可以登錄。</span><span class="sxs-lookup"><span data-stu-id="262aa-152">If they aren't logged in we'll redirect them to the login page so that they can sign-in.</span></span>

<span data-ttu-id="262aa-153">實現此邏輯非常簡單。</span><span class="sxs-lookup"><span data-stu-id="262aa-153">Implementing this logic is pretty easy.</span></span> <span data-ttu-id="262aa-154">我們只需要將 [授權] 篩選器屬性添加到我們的"創建操作方法"中,如下所示:</span><span class="sxs-lookup"><span data-stu-id="262aa-154">All we need to-do is to add an [Authorize] filter attribute to our Create action methods like so:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

<span data-ttu-id="262aa-155">ASP.NET MVC 支援建立「操作篩選器」的能力,該篩選器可用於實現可聲明應用於操作方法的可重用邏輯。</span><span class="sxs-lookup"><span data-stu-id="262aa-155">ASP.NET MVC supports the ability to create "action filters" that can be used to implement re-usable logic that can be declaratively applied to action methods.</span></span> <span data-ttu-id="262aa-156">[授權] 篩選器是 ASP.NET MVC 提供的內建操作篩選器之一,它使開發人員能夠聲明授權規則應用於操作方法和控制器類。</span><span class="sxs-lookup"><span data-stu-id="262aa-156">The [Authorize] filter is one of the built-in action filters provided by ASP.NET MVC, and it enables a developer to declaratively apply authorization rules to action methods and controller classes.</span></span>

<span data-ttu-id="262aa-157">在沒有任何參數的情況下應用時(如上文所述),[授權] 篩選器強制必須登錄執行操作方法請求的使用者,如果瀏覽器未登錄,則會自動將瀏覽器重定向到登錄 URL。</span><span class="sxs-lookup"><span data-stu-id="262aa-157">When applied without any parameters (like above) the [Authorize] filter enforces that the user making the action method request must be logged in – and it will automatically redirect the browser to the login URL if they aren't.</span></span> <span data-ttu-id="262aa-158">執行此操作重定向時,最初請求的 URL 將作為查詢字串參數傳遞(例如:/帳戶/LogOn?傳回Url_%2fDinners%2f創建)。</span><span class="sxs-lookup"><span data-stu-id="262aa-158">When doing this redirect the originally requested URL is passed as a querystring argument (for example: /Account/LogOn?ReturnUrl=%2fDinners%2fCreate).</span></span> <span data-ttu-id="262aa-159">然後,帳戶控制器將在使用者登錄后將使用者重定向回最初請求的 URL。</span><span class="sxs-lookup"><span data-stu-id="262aa-159">The AccountController will then redirect the user back to the originally requested URL once they login.</span></span>

<span data-ttu-id="262aa-160">[授權] 篩選器可以選擇支援指定"使用者"或"角色"屬性的能力,該屬性可用於要求使用者同時登錄並登錄允許的使用者或允許的安全角色的成員清單中。</span><span class="sxs-lookup"><span data-stu-id="262aa-160">The [Authorize] filter optionally supports the ability to specify a "Users" or "Roles" property that can be used to require that the user is both logged in and within a list of allowed users or a member of an allowed security role.</span></span> <span data-ttu-id="262aa-161">例如,下面的代碼只允許兩個特定使用者「scottgu」和「billg」訪問 /Dinners/Create URL:</span><span class="sxs-lookup"><span data-stu-id="262aa-161">For example, the code below only allows two specific users, "scottgu" and "billg", to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

<span data-ttu-id="262aa-162">不過,在代碼中嵌入特定的使用者名往往非常無法維護。</span><span class="sxs-lookup"><span data-stu-id="262aa-162">Embedding specific user names within code tends to be pretty un-maintainable though.</span></span> <span data-ttu-id="262aa-163">更好的方法是定義代碼所針對的更高級別的"角色",然後使用資料庫或活動目錄系統將使用者映射到角色(使實際使用者映射清單能夠從代碼外部存儲)。</span><span class="sxs-lookup"><span data-stu-id="262aa-163">A better approach is to define higher-level "roles" that the code checks against, and then to map users into the role using either a database or active directory system (enabling the actual user mapping list to be stored externally from the code).</span></span> <span data-ttu-id="262aa-164">ASP.NET包括內建角色管理 API 以及一組內建角色提供者(包括 SQL 和 Active Directory 的內建角色提供者),可幫助執行此使用者/角色映射。</span><span class="sxs-lookup"><span data-stu-id="262aa-164">ASP.NET includes a built-in role management API as well as a built-in set of role providers (including ones for SQL and Active Directory) that can help perform this user/role mapping.</span></span> <span data-ttu-id="262aa-165">然後,我們可以更新代碼,僅允許特定「管理員」角色中的使用者訪問 /Dinners/Create URL:</span><span class="sxs-lookup"><span data-stu-id="262aa-165">We could then update the code to only allow users within a specific "admin" role to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a><span data-ttu-id="262aa-166">建立晚餐時使用User.Identity.Name屬性</span><span class="sxs-lookup"><span data-stu-id="262aa-166">Using the User.Identity.Name property when Creating Dinners</span></span>

<span data-ttu-id="262aa-167">我們可以使用 Controller 基類上公開的 User.Identity.Name 屬性檢索請求當前登錄使用者的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="262aa-167">We can retrieve the username of the currently logged-in user of a request using the User.Identity.Name property exposed on the Controller base class.</span></span>

<span data-ttu-id="262aa-168">早些時候,當我們實現我們的Create() 操作方法的HTTP-POST版本時,我們已經將 Dinner 的「託管比」屬性硬編碼為靜態字串串。</span><span class="sxs-lookup"><span data-stu-id="262aa-168">Earlier when we implemented the HTTP-POST version of our Create() action method we had hardcoded the "HostedBy" property of the Dinner to a static string.</span></span> <span data-ttu-id="262aa-169">我們現在可以更新此代碼以改用User.Identity.Name屬性,並為創建 Dinner 的主機自動添加 RSVP:</span><span class="sxs-lookup"><span data-stu-id="262aa-169">We can now update this code to instead use the User.Identity.Name property, as well as automatically add an RSVP for the host creating the Dinner:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

<span data-ttu-id="262aa-170">由於我們已經向 Create() 方法添加了 [授權] 屬性,因此 ASP.NET MVC 可確保僅當訪問 /Dinners/Create URL 的使用者登錄網站時,才會執行操作方法。</span><span class="sxs-lookup"><span data-stu-id="262aa-170">Because we have added an [Authorize] attribute to the Create() method, ASP.NET MVC ensures that the action method only executes if the user visiting the /Dinners/Create URL is logged in on the site.</span></span> <span data-ttu-id="262aa-171">因此,User.Identity.Name屬性值將始終包含有效的使用者名。</span><span class="sxs-lookup"><span data-stu-id="262aa-171">As such, the User.Identity.Name property value will always contain a valid username.</span></span>

### <a name="using-the-useridentityname-property-when-editing-dinners"></a><span data-ttu-id="262aa-172">編輯晚餐時使用User.Identity.Name屬性</span><span class="sxs-lookup"><span data-stu-id="262aa-172">Using the User.Identity.Name property when Editing Dinners</span></span>

<span data-ttu-id="262aa-173">現在,讓我們添加一些限制使用者的授權邏輯,以便他們只能編輯自己託管的晚餐的屬性。</span><span class="sxs-lookup"><span data-stu-id="262aa-173">Let's now add some authorization logic that restricts users so that they can only edit the properties of dinners they themselves are hosting.</span></span>

<span data-ttu-id="262aa-174">為了幫助達到這一目的,我們將首先向 Dinner 物件添加"Is託管By(使用者名)"幫助器方法(在之前構建的 Dinner.cs 部分類中)。</span><span class="sxs-lookup"><span data-stu-id="262aa-174">To help with this, we'll first add an "IsHostedBy(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="262aa-175">此說明程式方法傳回 true 或 false,具體取決於提供的使用者名稱是否與 Dinner 託管 By 屬性匹配,並封裝執行不區分大小寫的字串比較所需的邏輯:</span><span class="sxs-lookup"><span data-stu-id="262aa-175">This helper method returns true or false depending on whether a supplied username matches the Dinner HostedBy property, and encapsulates the logic necessary to perform a case-insensitive string comparison of them:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

<span data-ttu-id="262aa-176">然後,我們將向 DinnersController 類中的 Edit() 操作方法添加 [授權] 屬性。</span><span class="sxs-lookup"><span data-stu-id="262aa-176">We'll then add an [Authorize] attribute to the Edit() action methods within our DinnersController class.</span></span> <span data-ttu-id="262aa-177">這將確保使用者必須登錄才能請求 */Dinners/Edit/[id]* URL。</span><span class="sxs-lookup"><span data-stu-id="262aa-177">This will ensure that users must be logged in to request a */Dinners/Edit/[id]* URL.</span></span>

<span data-ttu-id="262aa-178">然後,我們可以向使用 Dinner.IsHostBy(使用者名)幫助器方法的「編輯」方法添加代碼,以驗證登錄使用者是否與 Dinner 主機匹配。</span><span class="sxs-lookup"><span data-stu-id="262aa-178">We can then add code to our Edit methods that uses the Dinner.IsHostedBy(username) helper method to verify that the logged-in user matches the Dinner host.</span></span> <span data-ttu-id="262aa-179">如果使用者不是主機,我們將顯示"無效擁有者"視圖並終止請求。</span><span class="sxs-lookup"><span data-stu-id="262aa-179">If the user is not the host, we'll display an "InvalidOwner" view and terminate the request.</span></span> <span data-ttu-id="262aa-180">執行此操作的代碼如下所示:</span><span class="sxs-lookup"><span data-stu-id="262aa-180">The code to do this looks like below:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

<span data-ttu-id="262aa-181">然後,我們可以右鍵單擊 [Views_Dinners]目錄,然後選擇"&gt;添加 -視圖"功能表命令以創建新的"無效擁有者"視圖。</span><span class="sxs-lookup"><span data-stu-id="262aa-181">We can then right-click on the \Views\Dinners directory and choose the Add-&gt;View menu command to create a new "InvalidOwner" view.</span></span> <span data-ttu-id="262aa-182">我們將用以下錯誤訊息填充它:</span><span class="sxs-lookup"><span data-stu-id="262aa-182">We'll populate it with the below error message:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

<span data-ttu-id="262aa-183">現在,當用戶嘗試編輯他們不擁有的晚餐時,他們會得到一條錯誤消息:</span><span class="sxs-lookup"><span data-stu-id="262aa-183">And now when a user attempts to edit a dinner they don't own, they'll get an error message:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

<span data-ttu-id="262aa-184">我們可以對控制器中的 Delete() 操作方法重複相同的步驟,以鎖定刪除 Dinner 的許可權,並確保只有晚餐的主持人才能刪除它。</span><span class="sxs-lookup"><span data-stu-id="262aa-184">We can repeat the same steps for the Delete() action methods within our controller to lock down permission to delete Dinners as well, and ensure that only the host of a Dinner can delete it.</span></span>

### <a name="showinghiding-edit-and-delete-links"></a><span data-ttu-id="262aa-185">顯示/隱藏編輯與移除連結</span><span class="sxs-lookup"><span data-stu-id="262aa-185">Showing/Hiding Edit and Delete Links</span></span>

<span data-ttu-id="262aa-186">我們正在從「詳細資訊」URL 連結到「晚餐控制器」類的編輯和刪除操作方法:</span><span class="sxs-lookup"><span data-stu-id="262aa-186">We are linking to the Edit and Delete action method of our DinnersController class from our Details URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

<span data-ttu-id="262aa-187">目前,我們顯示"編輯和刪除"操作連結,無論詳細資訊 URL 的訪問者是否是晚宴的東道主。</span><span class="sxs-lookup"><span data-stu-id="262aa-187">Currently we are showing the Edit and Delete action links regardless of whether the visitor to the details URL is the host of the dinner.</span></span> <span data-ttu-id="262aa-188">讓我們更改此內容,以便僅當訪問使用者是晚餐的擁有者時才會顯示連結。</span><span class="sxs-lookup"><span data-stu-id="262aa-188">Let's change this so that the links are only displayed if the visiting user is the owner of the dinner.</span></span>

<span data-ttu-id="262aa-189">晚餐控制器中的「詳細資訊()」操作方法檢索 Dinner 物件,然後將其作為模型物件傳遞給檢視範本:</span><span class="sxs-lookup"><span data-stu-id="262aa-189">The Details() action method within our DinnersController retrieves a Dinner object and then passes it as the model object to our view template:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

<span data-ttu-id="262aa-190">我們可以更新檢視範本,以便使用「晚餐.Is託管By」()幫助器方法有條件地顯示/隱藏"編輯"和"刪除"連結,如下所示:</span><span class="sxs-lookup"><span data-stu-id="262aa-190">We can update our view template to conditionally show/hide the Edit and Delete links by using the Dinner.IsHostedBy() helper method like below:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a><span data-ttu-id="262aa-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="262aa-191">Next Steps</span></span>

<span data-ttu-id="262aa-192">現在,讓我們來看看如何啟用經過身份驗證的使用者到RSVP的晚餐使用AJAX。</span><span class="sxs-lookup"><span data-stu-id="262aa-192">Let's now look at how we can enable authenticated users to RSVP for dinners using AJAX.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="262aa-193">[前一個](implement-efficient-data-paging.md)
> [下一個](use-ajax-to-deliver-dynamic-updates.md)</span><span class="sxs-lookup"><span data-stu-id="262aa-193">[Previous](implement-efficient-data-paging.md)
[Next](use-ajax-to-deliver-dynamic-updates.md)</span></span>
