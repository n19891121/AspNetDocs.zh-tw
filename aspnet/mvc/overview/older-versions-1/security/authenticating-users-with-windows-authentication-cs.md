---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
title: 使用 Windows 身份驗證 (C#) 對使用者進行身份驗證 |微軟文件
author: rick-anderson
description: 瞭解如何在 MVC 應用程式的上下文中使用 Windows 身份驗證。 您將瞭解如何在應用程式的 Web 身份驗證中開啟 Windows 身份認證...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 418bb07e-f369-4119-b4b0-08f890f7abb2
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: fb6ba3d52d7c70d61c6aa16b4ada67cc6bdd4f96
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540736"
---
# <a name="authenticating-users-with-windows-authentication-c"></a><span data-ttu-id="b1324-104">使用 Windows 驗證驗證使用者 (C#)</span><span class="sxs-lookup"><span data-stu-id="b1324-104">Authenticating Users with Windows Authentication (C#)</span></span>

<span data-ttu-id="b1324-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b1324-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b1324-106">瞭解如何在 MVC 應用程式的上下文中使用 Windows 身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-106">Learn how to use Windows authentication in the context of an MVC application.</span></span> <span data-ttu-id="b1324-107">您將瞭解如何在應用程式的 Web 設定檔中啟用 Windows 身份驗證,以及如何使用 IIS 設定身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-107">You learn how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="b1324-108">最後,您將瞭解如何使用 [授權] 屬性將控制器操作的存取限制為特定的 Windows 使用者或組。</span><span class="sxs-lookup"><span data-stu-id="b1324-108">Finally, you learn how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

<span data-ttu-id="b1324-109">本教學的目的是說明如何利用 Internet 資訊服務中內置的安全功能來密碼保護 MVC 應用程式中的視圖。</span><span class="sxs-lookup"><span data-stu-id="b1324-109">The goal of this tutorial is to explain how you can take advantage of the security features built into Internet Information Services to password protect the views in your MVC applications.</span></span> <span data-ttu-id="b1324-110">您將瞭解如何僅允許特定 Windows 使用者或屬於特定 Windows 組的成員的使用者呼叫控制器操作。</span><span class="sxs-lookup"><span data-stu-id="b1324-110">You learn how to allow controller actions to be invoked only by particular Windows users or users who are members of particular Windows groups.</span></span>

<span data-ttu-id="b1324-111">當您構建內部公司網站(Intranet 網站)並希望使用者在瀏覽網站時能夠使用其標準 Windows 使用者名和密碼時,使用 Windows 身份驗證是有意義的。</span><span class="sxs-lookup"><span data-stu-id="b1324-111">Using Windows authentication makes sense when you are building an internal company website (an intranet site) and you want your users to be able to use their standard Windows user names and passwords when accessing the website.</span></span> <span data-ttu-id="b1324-112">如果您正在構建面向外的網站(Internet 網站),請考慮改用表單身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-112">If you are building an outwards facing website (an Internet website) consider using Forms authentication instead.</span></span>

#### <a name="enabling-windows-authentication"></a><span data-ttu-id="b1324-113">開啟 Windows 認證</span><span class="sxs-lookup"><span data-stu-id="b1324-113">Enabling Windows Authentication</span></span>

<span data-ttu-id="b1324-114">創建新ASP.NET MVC 應用程式時,預設情況下不會啟用Windows身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-114">When you create a new ASP.NET MVC application, Windows authentication is not enabled by default.</span></span> <span data-ttu-id="b1324-115">表單身份驗證是為 MVC 應用程式啟用的預設身份驗證類型。</span><span class="sxs-lookup"><span data-stu-id="b1324-115">Forms authentication is the default authentication type enabled for MVC applications.</span></span> <span data-ttu-id="b1324-116">必須透過修改 MVC 應用程式的 Web 設定 (Web.config) 檔來啟用 Windows 身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-116">You must enable Windows authentication by modifying your MVC application's web configuration (web.config) file.</span></span> <span data-ttu-id="b1324-117">尋找&lt;認證&gt;管理系統並進行修改以使用 Windows 而不是窗體身份驗證,如下所示:</span><span class="sxs-lookup"><span data-stu-id="b1324-117">Find the &lt;authentication&gt; section and modify it to use Windows instead of Forms authentication like this:</span></span>

[!code-xml[Main](authenticating-users-with-windows-authentication-cs/samples/sample1.xml)]

<span data-ttu-id="b1324-118">啟用 Windows 身份驗證後,Web 伺服器將負責對使用者進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-118">When you enable Windows authentication, your web server becomes responsible for authenticating users.</span></span> <span data-ttu-id="b1324-119">通常,在創建和部署ASP.NET MVC 應用程式時,可以使用兩種不同類型的 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b1324-119">Typically, there are two different types of web servers that you use when creating and deploying an ASP.NET MVC application.</span></span>

<span data-ttu-id="b1324-120">首先,在開發 MVC 應用程式時,您可以使用 Visual Studio 附帶的 ASP.NET 開發 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b1324-120">First, while developing an MVC application, you use the ASP.NET Development Web Server included with Visual Studio.</span></span> <span data-ttu-id="b1324-121">默認情況下,ASP.NET開發 Web 伺服器在當前 Windows 帳戶(用於登錄到 Windows 的任何帳戶)的上下文中執行所有頁面。</span><span class="sxs-lookup"><span data-stu-id="b1324-121">By default, the ASP.NET Development Web Server executes all pages in the context of the current Windows account (whatever account you used to log into Windows).</span></span>

<span data-ttu-id="b1324-122">ASP.NET開發 Web 伺服器還支援 NTLM 身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-122">The ASP.NET Development Web Server also supports NTLM authentication.</span></span> <span data-ttu-id="b1324-123">您可以透過在解決方案資源管理器視窗中右鍵單擊專案名稱並選擇「屬性」來啟用 NTLM 身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-123">You can enable NTLM authentication by right-clicking the name of your project in the Solution Explorer window and selecting Properties.</span></span> <span data-ttu-id="b1324-124">接下來,選擇 Web 選項卡並選中 NTLM 複選框(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="b1324-124">Next, select the Web tab and check the NTLM checkbox (see Figure 1).</span></span>

<span data-ttu-id="b1324-125">**圖 1 = 為 ASP.NET 開發 Web 伺服器啟用 NTLM 身份驗證**</span><span class="sxs-lookup"><span data-stu-id="b1324-125">**Figure 1 – Enabling NTLM authentication for the ASP.NET Development Web Server**</span></span>

![clip_image002](authenticating-users-with-windows-authentication-cs/_static/image1.jpg)

<span data-ttu-id="b1324-127">對於生產 Web 應用程式,使用 IIS 作為 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b1324-127">For a production web application, on the hand, you use IIS as your web server.</span></span> <span data-ttu-id="b1324-128">IIS 支援多種類型的身份驗證,包括:</span><span class="sxs-lookup"><span data-stu-id="b1324-128">IIS supports several types of authentication including:</span></span>

- <span data-ttu-id="b1324-129">基本身份驗證 – 定義為 HTTP1.0 協定的一部分。</span><span class="sxs-lookup"><span data-stu-id="b1324-129">Basic Authentication – Defined as part of the HTTP 1.0 protocol.</span></span> <span data-ttu-id="b1324-130">在 Internet 上以明文(Base64 編碼)發送使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b1324-130">Sends user names and passwords in clear text (Base64 encoded) across the Internet.</span></span> <span data-ttu-id="b1324-131">- 摘要身份驗證 – 通過互聯網發送密碼的哈希值,而不是密碼本身。</span><span class="sxs-lookup"><span data-stu-id="b1324-131">- Digest Authentication – Sends a hash of a password, instead of the password itself, across the internet.</span></span> <span data-ttu-id="b1324-132">- 整合的 Windows (NTLM) 身份驗證 – 使用視窗在 Intranet 環境中使用的最佳身份驗證類型。</span><span class="sxs-lookup"><span data-stu-id="b1324-132">- Integrated Windows (NTLM) Authentication – The best type of authentication to use in intranet environments using windows.</span></span> <span data-ttu-id="b1324-133">- 憑證身份驗證 – 使用用戶端證書啟用身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-133">- Certificate Authentication – Enables authentication using a client-side certificate.</span></span> <span data-ttu-id="b1324-134">證書映射到 Windows 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1324-134">The certificate maps to a Windows user account.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="b1324-135">有關這些不同類型的身份驗證的更詳細概述,請參閱[https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b1324-135">For a more detailed overview of these different types of authentication, see [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx).</span></span>

<span data-ttu-id="b1324-136">您可以使用 Internet 資訊服務管理器啟用特定類型的身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-136">You can use Internet Information Services Manager to enable a particular type of authentication.</span></span> <span data-ttu-id="b1324-137">請注意,對於每個操作系統,所有類型的身份驗證都不可用。</span><span class="sxs-lookup"><span data-stu-id="b1324-137">Be aware that all types of authentication are not available in the case of every operating system.</span></span> <span data-ttu-id="b1324-138">此外,如果您將 IIS 7.0 與 Windows Vista 一起使用,則需要在 Internet 資訊服務管理器中顯示不同類型的 Windows 身份驗證之前啟用這些身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-138">Furthermore, if you are using IIS 7.0 with Windows Vista, you will need to enable the different types of Windows authentication before they appear in the Internet Information Services Manager.</span></span> <span data-ttu-id="b1324-139">打開**控制面板、程式、程式和功能,打開或關閉 Windows 功能**,並展開 Internet 資訊服務節點(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="b1324-139">Open **Control Panel, Programs, Programs and Features, Turn Windows features on or off**, and expand the Internet Information Services node (see Figure 2).</span></span>

<span data-ttu-id="b1324-140">**圖 2 = 啟用 Windows IIS 功能**</span><span class="sxs-lookup"><span data-stu-id="b1324-140">**Figure 2 – Enabling Windows IIS features**</span></span>

![clip_image004](authenticating-users-with-windows-authentication-cs/_static/image2.jpg)

<span data-ttu-id="b1324-142">使用 Internet 資訊服務,您可以啟用或禁用不同類型的身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-142">Using Internet Information Services, you can enable or disable different types of authentication.</span></span> <span data-ttu-id="b1324-143">例如,圖 3 演示了在使用 IIS 7.0 時禁用匿名身份驗證和啟用集成 Windows (NTLM) 身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-143">For example, Figure 3 illustrates disabling anonymous authentication and enabling Integrated Windows (NTLM) authentication when using IIS 7.0.</span></span>

<span data-ttu-id="b1324-144">**圖 3 = 啟用整合 Windows 認證**</span><span class="sxs-lookup"><span data-stu-id="b1324-144">**Figure 3 – Enabling Integrated Windows Authentication**</span></span>

![clip_image006](authenticating-users-with-windows-authentication-cs/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a><span data-ttu-id="b1324-146">授權 Windows 使用者和群組</span><span class="sxs-lookup"><span data-stu-id="b1324-146">Authorizing Windows Users and Groups</span></span>

<span data-ttu-id="b1324-147">啟用 Windows 身份驗證後,可以使用 [授權] 屬性來控制對控制器或控制器操作的訪問。</span><span class="sxs-lookup"><span data-stu-id="b1324-147">After you enable Windows authentication, you can use the [Authorize] attribute to control access to controllers or controller actions.</span></span> <span data-ttu-id="b1324-148">此屬性可以應用於整個 MVC 控制器或特定控制器操作。</span><span class="sxs-lookup"><span data-stu-id="b1324-148">This attribute can be applied to an entire MVC controller or a particular controller action.</span></span>

<span data-ttu-id="b1324-149">例如,清單 1 中的主頁控制器公開了名為 Index()、公司機密()和 StephenSecrets() 的三個操作。</span><span class="sxs-lookup"><span data-stu-id="b1324-149">For example, the Home controller in Listing 1 exposes three actions named Index(), CompanySecrets(), and StephenSecrets().</span></span> <span data-ttu-id="b1324-150">任何人都可以調用 Index() 操作。</span><span class="sxs-lookup"><span data-stu-id="b1324-150">Anyone can invoke the Index() action.</span></span> <span data-ttu-id="b1324-151">但是,只有 Windows 本地經理組的成員才能調用公司機密()操作。</span><span class="sxs-lookup"><span data-stu-id="b1324-151">However, only members of the Windows local Managers group can invoke the CompanySecrets() action.</span></span> <span data-ttu-id="b1324-152">最後,只有名為 Stephen 的 Windows 功能變數使用者(在雷德蒙德域中)才能調用 StephenSecrets() 操作。</span><span class="sxs-lookup"><span data-stu-id="b1324-152">Finally, only the Windows domain user named Stephen (in the Redmond domain) can invoke the StephenSecrets() action.</span></span>

<span data-ttu-id="b1324-153">**清單1 = 控制器\主控制器.cs**</span><span class="sxs-lookup"><span data-stu-id="b1324-153">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](authenticating-users-with-windows-authentication-cs/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="b1324-154">由於 Windows 使用者帳戶控制 (UAC),使用 Windows Vista 或 Windows 伺服器 2008 時,本地管理員組的行為將不同於其他組。</span><span class="sxs-lookup"><span data-stu-id="b1324-154">Because of Windows User Account Control (UAC), when working with Windows Vista or Windows Server 2008, the local Administrators group will behave differently than other groups.</span></span> <span data-ttu-id="b1324-155">除非修改電腦的 UAC 設定,否則 [授權] 屬性將無法正確識別本地管理員組的成員。</span><span class="sxs-lookup"><span data-stu-id="b1324-155">The [Authorize] attribute won't correctly recognize a member of the local Administrators group unless you modify your computer's UAC settings.</span></span>

<span data-ttu-id="b1324-156">當您嘗試調用控制器操作而不具有正確的許可權時,具體會發生什麼情況取決於啟用的身份驗證類型。</span><span class="sxs-lookup"><span data-stu-id="b1324-156">Exactly what happens when you attempt to invoke a controller action without being the right permissions depends on the type of authentication enabled.</span></span> <span data-ttu-id="b1324-157">默認情況下,當使用ASP.NET開發伺服器時,只需獲得一個空白頁。</span><span class="sxs-lookup"><span data-stu-id="b1324-157">By default, when using the ASP.NET Development Server, you simply get a blank page.</span></span> <span data-ttu-id="b1324-158">該頁面提供**401 未授權**HTTP 回應狀態。</span><span class="sxs-lookup"><span data-stu-id="b1324-158">The page is served with a **401 Not Authorized** HTTP Response Status.</span></span>

<span data-ttu-id="b1324-159">另一方面,如果您使用的 IIS 禁用了匿名身份驗證並啟用了基本身份驗證,則每次請求受保護頁面時,您都會不斷收到登錄對話方塊提示(參見圖 4)。</span><span class="sxs-lookup"><span data-stu-id="b1324-159">If, on the other hand, you are using IIS with Anonymous authentication disabled and Basic authentication enabled, then you keep getting a login dialog prompt each time you request the protected page (see Figure 4).</span></span>

<span data-ttu-id="b1324-160">**圖 4 = 基本身份驗證登入對話框**</span><span class="sxs-lookup"><span data-stu-id="b1324-160">**Figure 4 – Basic authentication login dialog**</span></span>

![clip_image008](authenticating-users-with-windows-authentication-cs/_static/image4.jpg)

#### <a name="summary"></a><span data-ttu-id="b1324-162">總結</span><span class="sxs-lookup"><span data-stu-id="b1324-162">Summary</span></span>

<span data-ttu-id="b1324-163">本教程介紹了如何在ASP.NET MVC 應用程式的上下文中使用Windows身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-163">This tutorial explained how you can use Windows authentication in the context of an ASP.NET MVC application.</span></span> <span data-ttu-id="b1324-164">您學習了如何在應用程式的 Web 設定檔中啟用 Windows 身份驗證,以及如何使用 IIS 設定身份驗證。</span><span class="sxs-lookup"><span data-stu-id="b1324-164">You learned how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="b1324-165">最後,您學習了如何使用 [授權] 屬性將控制器操作的存取限制為特定的 Windows 使用者或組。</span><span class="sxs-lookup"><span data-stu-id="b1324-165">Finally, you learned how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b1324-166">[前一個](authenticating-users-with-forms-authentication-cs.md)
> [下一個](preventing-javascript-injection-attacks-cs.md)</span><span class="sxs-lookup"><span data-stu-id="b1324-166">[Previous](authenticating-users-with-forms-authentication-cs.md)
[Next](preventing-javascript-injection-attacks-cs.md)</span></span>
