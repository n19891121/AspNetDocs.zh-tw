---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: 會員 |微軟文件
author: rick-anderson
description: ASP.NET成員資格基於表單身份驗證模型從ASP.NET1.x的成功為基礎。 ASP.NET窗體身份驗證提供了一種便捷的方法來進行體形...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: ed48c11cbd483de088239bad7c2452b7fc60a1cf
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543765"
---
# <a name="membership"></a><span data-ttu-id="c1da1-104">成員資格</span><span class="sxs-lookup"><span data-stu-id="c1da1-104">Membership</span></span>

<span data-ttu-id="c1da1-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c1da1-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c1da1-106">ASP.NET成員資格基於表單身份驗證模型從ASP.NET1.x的成功為基礎。</span><span class="sxs-lookup"><span data-stu-id="c1da1-106">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="c1da1-107">ASP.NET窗體身份驗證提供了將登錄表單合併到ASP.NET應用程式中以及根據資料庫或其他數據存儲驗證使用者的便捷方法。</span><span class="sxs-lookup"><span data-stu-id="c1da1-107">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span>

<span data-ttu-id="c1da1-108">ASP.NET成員資格基於表單身份驗證模型從ASP.NET1.x的成功為基礎。</span><span class="sxs-lookup"><span data-stu-id="c1da1-108">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="c1da1-109">ASP.NET窗體身份驗證提供了將登錄表單合併到ASP.NET應用程式中以及根據資料庫或其他數據存儲驗證使用者的便捷方法。</span><span class="sxs-lookup"><span data-stu-id="c1da1-109">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span> <span data-ttu-id="c1da1-110">表單身份驗證類的成員可以處理 Cookie 進行身分驗證、檢查有效登錄、登出使用者等。但是,在ASP.NET 1.x 應用程序中實現窗體身份驗證可能需要大量代碼。</span><span class="sxs-lookup"><span data-stu-id="c1da1-110">The members of the FormsAuthentication class make it possible to handle cookies for authentication, check for a valid login, log a user out etc. However, implementing Forms authentication in an ASP.NET 1.x application can require a fair amount of code.</span></span>

<span data-ttu-id="c1da1-111">ASP.NET 2.0 中的成員資格是單獨使用窗體身份驗證的一大進步。</span><span class="sxs-lookup"><span data-stu-id="c1da1-111">Membership in ASP.NET 2.0 is a major advancement over using Forms authentication alone.</span></span> <span data-ttu-id="c1da1-112">(與表單身份驗證結合時,成員資格最可靠,但使用窗體身份驗證不是要求。正如您很快就會看到的那樣,您可以使用ASP.NET 2.0 中的ASP.NET成員資格和登錄控制項來實現強大的成員資格系統,而無需編寫大量代碼。</span><span class="sxs-lookup"><span data-stu-id="c1da1-112">(Membership is most robust when coupled with Forms authentication, but using Forms authentication is not a requirement.) As you'll soon see, you can use ASP.NET Membership and the login controls in ASP.NET 2.0 to implement a powerful membership system without writing much code at all.</span></span>

## <a name="implementing-membership-in-aspnet-20"></a><span data-ttu-id="c1da1-113">在 ASP.NET 2.0 中實施成員資格</span><span class="sxs-lookup"><span data-stu-id="c1da1-113">Implementing Membership in ASP.NET 2.0</span></span>

<span data-ttu-id="c1da1-114">成員資格通過以下四個步驟實現。</span><span class="sxs-lookup"><span data-stu-id="c1da1-114">Membership is implemented by following four steps.</span></span> <span data-ttu-id="c1da1-115">請記住,涉及許多子步驟以及可選配置,也可以實現。</span><span class="sxs-lookup"><span data-stu-id="c1da1-115">Keep in mind that there are many sub-steps that are involved as well as optional configuration that can be implemented as well.</span></span> <span data-ttu-id="c1da1-116">這些步驟旨在說明配置成員資格的大圖景。</span><span class="sxs-lookup"><span data-stu-id="c1da1-116">These steps are meant to illustrate the big picture of configuring membership.</span></span>

1. <span data-ttu-id="c1da1-117">創建成員資格資料庫(如果 SQL Server 用作成員資格存儲。</span><span class="sxs-lookup"><span data-stu-id="c1da1-117">Create your membership database (if SQL Server is used as the membership store.)</span></span>
2. <span data-ttu-id="c1da1-118">指定應用程式設定檔中的成員資格選項。</span><span class="sxs-lookup"><span data-stu-id="c1da1-118">Specify the membership options in your applications configuration files.</span></span> <span data-ttu-id="c1da1-119">(默認情況下啟用成員資格。</span><span class="sxs-lookup"><span data-stu-id="c1da1-119">(Membership is enabled by default.)</span></span>
3. <span data-ttu-id="c1da1-120">確定要使用的成員資格存儲的類型。</span><span class="sxs-lookup"><span data-stu-id="c1da1-120">Determine the type of membership store you want to use.</span></span> <span data-ttu-id="c1da1-121">選項包括：</span><span class="sxs-lookup"><span data-stu-id="c1da1-121">Options are:</span></span> 

    - <span data-ttu-id="c1da1-122">微軟 SQL 伺服器(版本 7.0 或更高版本)</span><span class="sxs-lookup"><span data-stu-id="c1da1-122">Microsoft SQL Server (version 7.0 or later)</span></span>
    - <span data-ttu-id="c1da1-123">活動目錄儲存</span><span class="sxs-lookup"><span data-stu-id="c1da1-123">Active Directory Store</span></span>
    - <span data-ttu-id="c1da1-124">自訂成員資格提供者</span><span class="sxs-lookup"><span data-stu-id="c1da1-124">Custom membership provider</span></span>
4. <span data-ttu-id="c1da1-125">配置應用程式以進行ASP.NET窗體身份驗證。</span><span class="sxs-lookup"><span data-stu-id="c1da1-125">Configure the application for ASP.NET Forms authentication.</span></span> <span data-ttu-id="c1da1-126">再次,成員資格旨在利用窗體身份驗證,但使用窗體身份驗證不是一項要求。</span><span class="sxs-lookup"><span data-stu-id="c1da1-126">Once again, Membership is designed to take advantage of Forms authentication, but using Forms authentication is not a requirement.</span></span>
5. <span data-ttu-id="c1da1-127">為成員資格定義使用者帳戶,並根據需要配置角色。</span><span class="sxs-lookup"><span data-stu-id="c1da1-127">Define user accounts for membership and configure roles if desired.</span></span>

## <a name="creating-the-membership-database"></a><span data-ttu-id="c1da1-128">建立成員資格資料庫</span><span class="sxs-lookup"><span data-stu-id="c1da1-128">Creating the Membership Database</span></span>

<span data-ttu-id="c1da1-129">如果您使用 SQL Server 7.0 或更高版本作為成員資格存儲,則可以\_使用 aspnet regsql 實用程式(從 Visual Studio .NET 2005 命令提示符中最容易使用)來配置資料庫。</span><span class="sxs-lookup"><span data-stu-id="c1da1-129">If you're using SQL Server 7.0 or later as your membership store, you can use the aspnet\_regsql utility (available most easily from the Visual Studio .NET 2005 Command Prompt) to configure your database.</span></span> <span data-ttu-id="c1da1-130">aspnet\_regsql 實用程式可用作命令提示工具或透過 GUI 精靈。</span><span class="sxs-lookup"><span data-stu-id="c1da1-130">The aspnet\_regsql utility can be used as a command prompt tool or via a GUI wizard.</span></span> <span data-ttu-id="c1da1-131">嚮導方法是配置資料庫的最簡單方法。</span><span class="sxs-lookup"><span data-stu-id="c1da1-131">The wizard method is the easiest way to configure your database.</span></span> <span data-ttu-id="c1da1-132">要存取精靈,只需執行以下指令:</span><span class="sxs-lookup"><span data-stu-id="c1da1-132">To access the wizard, simply run the following command:</span></span>

`aspnet_regsql W`

<span data-ttu-id="c1da1-133">運行該命令後,將顯示ASP.NET SQL 伺服器設置嚮導,如下所示。</span><span class="sxs-lookup"><span data-stu-id="c1da1-133">Once you run that command, you will be presented with the ASP.NET SQL Server Setup Wizard as shown below.</span></span>

![](membership/_static/image1.jpg)

<span data-ttu-id="c1da1-134">**圖 1**</span><span class="sxs-lookup"><span data-stu-id="c1da1-134">**Figure 1**</span></span>

<span data-ttu-id="c1da1-135">ASP.NET SQL 伺服器設置精靈會在嚮導中指定的實例中創建網站。</span><span class="sxs-lookup"><span data-stu-id="c1da1-135">The ASP.NET SQL Server Setup Wizard creates the Web site in the instance you specify in the wizard.</span></span> <span data-ttu-id="c1da1-136">但是,ASP.NET將使用計算機中的連接字串。</span><span class="sxs-lookup"><span data-stu-id="c1da1-136">However, ASP.NET will use the connection string in the machine.config file to connect to your database.</span></span> <span data-ttu-id="c1da1-137">預設情況下,此連接字串將指向 SQL Server 2005 實例,因此,如果您使用的是 SQL Server 2000 或 SQL Server 7.0 實例,則需要修改電腦中的連接字元串。</span><span class="sxs-lookup"><span data-stu-id="c1da1-137">By default, this connection string will point to a SQL Server 2005 instance, so if you are using a SQL Server 2000 or SQL Server 7.0 instance, you will need to modify the connection string in the machine.config file.</span></span> <span data-ttu-id="c1da1-138">該連線字串可以位於此處:</span><span class="sxs-lookup"><span data-stu-id="c1da1-138">That connection string can be located here:</span></span>

[!code-xml[Main](membership/samples/sample1.xml)]

<span data-ttu-id="c1da1-139">遺憾的是,如果不修改連接字串,ASP.NET不會給您帶來描述性錯誤。</span><span class="sxs-lookup"><span data-stu-id="c1da1-139">Unfortunately, if you don't modify the connection string, ASP.NET will not give you a descriptive error.</span></span> <span data-ttu-id="c1da1-140">它會繼續抱怨說,你還沒有創建資料庫。</span><span class="sxs-lookup"><span data-stu-id="c1da1-140">It will just continue to complain saying that you haven't created the database.</span></span> <span data-ttu-id="c1da1-141">在上面的案例中,我修改了連接字串以指向我的本地 SQL Server 2000 實例。</span><span class="sxs-lookup"><span data-stu-id="c1da1-141">In the case above, I have modified the connection string to point to my local SQL Server 2000 instance.</span></span>

## <a name="specifying-configuration-and-adding-users-and-roles"></a><span data-ttu-id="c1da1-142">指定設定與新增使用者與角色</span><span class="sxs-lookup"><span data-stu-id="c1da1-142">Specifying Configuration and Adding Users and Roles</span></span>

<span data-ttu-id="c1da1-143">設定成員資格的下一步是向應用程式的 Web.config 檔添加必要的資訊。</span><span class="sxs-lookup"><span data-stu-id="c1da1-143">The next step in configuring Membership is to add the necessary information to the web.config file of the application.</span></span> <span data-ttu-id="c1da1-144">在ASP.NET 1.x 中,由於使用較低CamelCase和缺乏 Intellisense,修改 Web.config 文件有時很困難。</span><span class="sxs-lookup"><span data-stu-id="c1da1-144">In ASP.NET 1.x, modifying the web.config file was sometimes difficult because of the use of lowerCamelCase and the lack of Intellisense.</span></span> <span data-ttu-id="c1da1-145">Visual Studio .NET 2005 使配置檔的 Intellisense 任務更加輕鬆,但 ASP.NET 2.0 透過提供用於編輯設定檔的網頁介面更進一步。</span><span class="sxs-lookup"><span data-stu-id="c1da1-145">Visual Studio .NET 2005 makes the task much easier with Intellisense for configuration files, but ASP.NET 2.0 goes one step further by providing a Web interface for editing configuration files.</span></span>

<span data-ttu-id="c1da1-146">您可以透過單擊解決方案資源管理器工具列上的ASP.NET配置按鈕來啟動 Web 介面,如下所示。</span><span class="sxs-lookup"><span data-stu-id="c1da1-146">You can launch the Web interface by clicking the ASP.NET Configuration button on the Solution Explorer toolbar as shown below.</span></span> <span data-ttu-id="c1da1-147">您還可以透過插入登入控制項時顯示的彈出視窗啟動 Web 介面。</span><span class="sxs-lookup"><span data-stu-id="c1da1-147">You can also launch the Web interface via pop-ups that are displayed when Login controls are inserted.</span></span>

![](membership/_static/image2.jpg)

<span data-ttu-id="c1da1-148">**圖 2**</span><span class="sxs-lookup"><span data-stu-id="c1da1-148">**Figure 2**</span></span>

<span data-ttu-id="c1da1-149">這將啟動下面所示的ASP.NET網站管理工具。</span><span class="sxs-lookup"><span data-stu-id="c1da1-149">This launches the ASP.NET Web Site Administration Tool shown below.</span></span> <span data-ttu-id="c1da1-150">ASP.NET網站管理是一個四選項卡介面,便於管理應用程式設置。</span><span class="sxs-lookup"><span data-stu-id="c1da1-150">The ASP.NET Web Site Administration is a four-tab interface that makes it easy to manage application settings.</span></span> <span data-ttu-id="c1da1-151">以下選項卡可用:</span><span class="sxs-lookup"><span data-stu-id="c1da1-151">The following tabs are available:</span></span>

- <span data-ttu-id="c1da1-152">**首頁**</span><span class="sxs-lookup"><span data-stu-id="c1da1-152">**Home**</span></span>
- <span data-ttu-id="c1da1-153">**安全性**配置使用者、角色和訪問許可權。</span><span class="sxs-lookup"><span data-stu-id="c1da1-153">**Security** Configure users, roles, and access.</span></span>
- <span data-ttu-id="c1da1-154">**套用**配置應用程式設置。</span><span class="sxs-lookup"><span data-stu-id="c1da1-154">**Application** Configure application settings.</span></span>
- <span data-ttu-id="c1da1-155">**供應商**配置和測試應用程式成員資格提供者。</span><span class="sxs-lookup"><span data-stu-id="c1da1-155">**Provider** Configure and test your applications membership provider.</span></span>

<span data-ttu-id="c1da1-156">網站管理工具允許您輕鬆創建新使用者、創建新角色以及管理使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="c1da1-156">The Web Site Administration Tool allows you to easily create new users, create new roles, and to manage users and roles.</span></span> <span data-ttu-id="c1da1-157">此功能在 Windows 介面中不可用。</span><span class="sxs-lookup"><span data-stu-id="c1da1-157">This ability is not available in the Windows interface.</span></span> <span data-ttu-id="c1da1-158">Windows 介面允許您輕鬆定義授權設置,並添加、刪除和管理不在網站管理工具中的提供程式。</span><span class="sxs-lookup"><span data-stu-id="c1da1-158">The Windows interface allows you to easily define authorization settings and to add, delete, and manage providers, capabilities that are not in the Web Site Administration Tool.</span></span>

<span data-ttu-id="c1da1-159">要啟動 Windows 介面,請打開 Internet 資訊服務卡入,右鍵單擊應用程式,然後選擇"屬性"。</span><span class="sxs-lookup"><span data-stu-id="c1da1-159">To launch the Windows interface, open the Internet Information Services snap-in, right-click on your application, and choose Properties.</span></span> <span data-ttu-id="c1da1-160">按下ASP.NET選項卡,然後按下「編輯配置」按鈕。</span><span class="sxs-lookup"><span data-stu-id="c1da1-160">Click the ASP.NET tab and then click the Edit Configuration button.</span></span> <span data-ttu-id="c1da1-161">(應用程式必須在 2.0 ASP.NET 下運行才能啟用"編輯配置"按鈕。</span><span class="sxs-lookup"><span data-stu-id="c1da1-161">(The application must be running under ASP.NET 2.0 for the Edit Configuration button to be enabled.</span></span> <span data-ttu-id="c1da1-162">您還可以在ASP.NET對話框中配置ASP.NET版本。ASP.NET 配置設置對話方塊如下所示。</span><span class="sxs-lookup"><span data-stu-id="c1da1-162">You can configure the ASP.NET version in the ASP.NET dialog as well.) The ASP.NET Configuration Settings dialog is displayed as shown below.</span></span>

![](membership/_static/image3.jpg)

<span data-ttu-id="c1da1-163">**圖 3**</span><span class="sxs-lookup"><span data-stu-id="c1da1-163">**Figure 3**</span></span>

<span data-ttu-id="c1da1-164">在「常規」選項卡上,將列出連接字串和應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="c1da1-164">On the General tab, connection strings and application settings are listed.</span></span> <span data-ttu-id="c1da1-165">斜體的任何設定都在父配置檔(機器.config 或更高級別的 Web.config)中定義,而斜體化的設置來自應用程式配置檔。</span><span class="sxs-lookup"><span data-stu-id="c1da1-165">Any settings in italics are defined in a parent configuration file (either the machine.config or a web.config at a higher level) and settings not in italics are from the applications configuration file.</span></span> <span data-ttu-id="c1da1-166">如果在應用程式級別添加、刪除或編輯設定,ASP.NET將在應用程式級別 Web.config 上添加、刪除或修改該設定,而不是從繼承該設定的設定檔中刪除該設定。</span><span class="sxs-lookup"><span data-stu-id="c1da1-166">If a setting is added, removed, or edited at the application level, ASP.NET will add, remove, or modify the setting at the application levels web.config instead of removing the setting from the configuration file from which it is inherited.</span></span>

<span data-ttu-id="c1da1-167">"身份驗證"選項卡如下所示。</span><span class="sxs-lookup"><span data-stu-id="c1da1-167">The Authentication tab is shown below.</span></span> <span data-ttu-id="c1da1-168">這是您將配置成員資格設置的位置。</span><span class="sxs-lookup"><span data-stu-id="c1da1-168">This is where you will configure your membership settings.</span></span> <span data-ttu-id="c1da1-169">可以在此處配置窗體身份驗證設置、成員資格提供程式和角色提供程式。</span><span class="sxs-lookup"><span data-stu-id="c1da1-169">Forms authentication settings, membership providers, and role providers can be configured here.</span></span>

![](membership/_static/image4.jpg)

<span data-ttu-id="c1da1-170">**圖 4**</span><span class="sxs-lookup"><span data-stu-id="c1da1-170">**Figure 4**</span></span>

## <a name="implementing-membership-in-your-application"></a><span data-ttu-id="c1da1-171">在應用程式中實現成員資格</span><span class="sxs-lookup"><span data-stu-id="c1da1-171">Implementing Membership in Your Application</span></span>

<span data-ttu-id="c1da1-172">實現應用程式中ASP.NET 2.0 成員資格的最簡單方法是使用提供的登錄控制項。</span><span class="sxs-lookup"><span data-stu-id="c1da1-172">The easiest way to implement ASP.NET 2.0 membership in your application is to use the provided Logon controls.</span></span> <span data-ttu-id="c1da1-173">此方法允許您實現ASP.NET 2.0 成員資格的基礎知識,而無需編寫任何代碼。</span><span class="sxs-lookup"><span data-stu-id="c1da1-173">This method allows you to implement the basics of ASP.NET 2.0 membership without writing any code at all.</span></span>

<span data-ttu-id="c1da1-174">以下登入控制項在 2.0 ASP.NET 中可用:</span><span class="sxs-lookup"><span data-stu-id="c1da1-174">The following Logon controls are available in ASP.NET 2.0:</span></span>

## <a name="login-control"></a><span data-ttu-id="c1da1-175">登入控制</span><span class="sxs-lookup"><span data-stu-id="c1da1-175">Login Control</span></span>

<span data-ttu-id="c1da1-176">登錄控制項為某人提供登錄您的成員資格系統的介面。</span><span class="sxs-lookup"><span data-stu-id="c1da1-176">The Login control provides an interface for someone to log into your membership system.</span></span> <span data-ttu-id="c1da1-177">它為您提供使用者名稱和密碼文本框和登錄按鈕。</span><span class="sxs-lookup"><span data-stu-id="c1da1-177">It provides you with a username and password textbox and a login button.</span></span> <span data-ttu-id="c1da1-178">許多其他常見功能,例如尚未註冊的使用者的連結、允許使用者在後續訪問時自動登錄的複選框、密碼提醒連結等。登錄控制件的所有功能都可透過控制的屬性進行自定義。</span><span class="sxs-lookup"><span data-stu-id="c1da1-178">Many other common features such as a link to register for people who have not yet done so, a checkbox that allows the user to automatically login on subsequent visits, a link for a password reminder, etc. All features of the Login control are customizable via the properties of the control.</span></span>

<span data-ttu-id="c1da1-179">在ASP.NET 1.x 中,開發人員在使用窗體身份驗證時必須編寫相當數量的代碼來執行查找。</span><span class="sxs-lookup"><span data-stu-id="c1da1-179">In ASP.NET 1.x, developers had to write a fair amount of code to do a lookup when using Forms authentication.</span></span> <span data-ttu-id="c1da1-180">使用ASP.NET 2.0 成員資格,無需編寫任何代碼即可驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="c1da1-180">With ASP.NET 2.0 membership, you can validate users without writing any code at all.</span></span> <span data-ttu-id="c1da1-181">ASP.NET會自動為您查找使用者。</span><span class="sxs-lookup"><span data-stu-id="c1da1-181">ASP.NET will automatically do the look-up of the user for you.</span></span> <span data-ttu-id="c1da1-182">(如果您使用登錄控制項而不使用ASP.NET成員資格,則可以使用**OnAuthenticate**方法驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="c1da1-182">(If you are using the Login control without using ASP.NET membership, you can use the **OnAuthenticate** method to validate the user.)</span></span>

## <a name="loginview-control"></a><span data-ttu-id="c1da1-183">LoginView 控制項</span><span class="sxs-lookup"><span data-stu-id="c1da1-183">LoginView Control</span></span>

<span data-ttu-id="c1da1-184">LoginView 控件是一個範本化控制項,預設情況下提供兩個範本;匿名範本和登錄範本。</span><span class="sxs-lookup"><span data-stu-id="c1da1-184">The LoginView control is a templated control that provides two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="c1da1-185">顯示的範本由使用者是否登錄到您的成員資格系統決定。</span><span class="sxs-lookup"><span data-stu-id="c1da1-185">The template that is displayed is determined by whether or not the user is logged into your membership system.</span></span> <span data-ttu-id="c1da1-186">此控件通常用於在使用者尚未登錄時顯示登錄控制項,以及使用者登錄時的登錄狀態控制項和/或其他登錄控制項。</span><span class="sxs-lookup"><span data-stu-id="c1da1-186">This control is typically used to display a Login control when a user has not yet logged in and a LoginStatus control and/or other login controls when the user has logged in.</span></span> <span data-ttu-id="c1da1-187">如果在ASP.NET應用程式中使用角色管理,則LoginView控制項可以基於使用者角色顯示特定的範本。</span><span class="sxs-lookup"><span data-stu-id="c1da1-187">If you are using role management in your ASP.NET application, the LoginView control can display a specific template based upon the users role.</span></span> <span data-ttu-id="c1da1-188">(稍後將介紹有關ASP.NET角色管理的更多內容。</span><span class="sxs-lookup"><span data-stu-id="c1da1-188">(More on ASP.NET role management will be covered later.)</span></span>

## <a name="passwordrecovery-control"></a><span data-ttu-id="c1da1-189">密碼修復控制</span><span class="sxs-lookup"><span data-stu-id="c1da1-189">PasswordRecovery Control</span></span>

<span data-ttu-id="c1da1-190">密碼修復控制項允許使用者接收包含其當前密碼的電子郵件或重置其密碼。</span><span class="sxs-lookup"><span data-stu-id="c1da1-190">The PasswordRecovery control allows users to receive an email with his or her current password or reset his or her password.</span></span> <span data-ttu-id="c1da1-191">可以恢復明文和加密的密碼並通過電子郵件發送給使用者。</span><span class="sxs-lookup"><span data-stu-id="c1da1-191">Clear text and encrypted passwords can be recovered and emailed to users.</span></span> <span data-ttu-id="c1da1-192">如果密碼已哈希,則無法恢復密碼。</span><span class="sxs-lookup"><span data-stu-id="c1da1-192">If the password is hashed, it cannot be recovered.</span></span> <span data-ttu-id="c1da1-193">相反,使用者將需要執行密碼重置。</span><span class="sxs-lookup"><span data-stu-id="c1da1-193">Instead the user will be required to perform a password reset.</span></span>

## <a name="loginstatus-control"></a><span data-ttu-id="c1da1-194">登入狀態控制</span><span class="sxs-lookup"><span data-stu-id="c1da1-194">LoginStatus Control</span></span>

<span data-ttu-id="c1da1-195">登錄狀態控制項用於向未登錄的使用者顯示登錄指示器,向目前登錄的使用者顯示登出指示器。</span><span class="sxs-lookup"><span data-stu-id="c1da1-195">The LoginStatus control is used to display a login indicator to users who are not logged in and a logout indicator to users who are currently logged in.</span></span> <span data-ttu-id="c1da1-196">"請求.已驗證"屬性用於確定要顯示的指示器。</span><span class="sxs-lookup"><span data-stu-id="c1da1-196">The Request.IsAuthenticated property is used to determine which indicator to display.</span></span> <span data-ttu-id="c1da1-197">登錄狀態控制項顯示的指示器可以是文本(透過**登錄文本**和**註銷文本**屬性實現)或圖像(透過**登錄圖像Url**和**LogoutImageUrl**屬性實現)。</span><span class="sxs-lookup"><span data-stu-id="c1da1-197">The indicator displayed by the LoginStatus control can be text (implemented via the **LoginText** and **LogoutText** properties) or images (implemented via the **LoginImageUrl** and **LogoutImageUrl** properties.)</span></span>

<span data-ttu-id="c1da1-198">當使用者通過登錄狀態控件註銷時,他或她將重定向到**LogoutPageUrl**屬性指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="c1da1-198">When a user logs out via the LoginStatus control, he or she is redirected to the URL specified by the **LogoutPageUrl** property.</span></span> <span data-ttu-id="c1da1-199">如果未設置該屬性,則刷新當前頁面。</span><span class="sxs-lookup"><span data-stu-id="c1da1-199">If that property is not set, the current page is refreshed.</span></span> <span data-ttu-id="c1da1-200">由於網站可能受窗體身份驗證保護,因此當前頁面的刷新將用戶重定向到網站的登錄頁。</span><span class="sxs-lookup"><span data-stu-id="c1da1-200">Since the site is likely protected by Forms authentication, the refresh of the current page will redirect the user to the login page for the site.</span></span>

## <a name="loginname-control"></a><span data-ttu-id="c1da1-201">登入名控制</span><span class="sxs-lookup"><span data-stu-id="c1da1-201">LoginName Control</span></span>

<span data-ttu-id="c1da1-202">"登錄名稱"控制件顯示當前登錄到網站的使用者的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="c1da1-202">The LoginName control displays the username of the user currently logged into the site.</span></span>

## <a name="createuserwizard-control"></a><span data-ttu-id="c1da1-203">建立使用者精靈控制項</span><span class="sxs-lookup"><span data-stu-id="c1da1-203">CreateUserWizard Control</span></span>

<span data-ttu-id="c1da1-204">CreateUserWizard 控制項為使用者提供註冊會員系統的便捷方式。</span><span class="sxs-lookup"><span data-stu-id="c1da1-204">The CreateUserWizard control provides users with a convenient way to register for your membership system.</span></span> <span data-ttu-id="c1da1-205">您可以通過如下所示的介面添加步驟(作為嚮導步驟的集合實現)。</span><span class="sxs-lookup"><span data-stu-id="c1da1-205">You can add steps (implemented as a collection of WizardSteps) via the interface shown below.</span></span>

![](membership/_static/image5.jpg)

<span data-ttu-id="c1da1-206">**圖 5**</span><span class="sxs-lookup"><span data-stu-id="c1da1-206">**Figure 5**</span></span>

<span data-ttu-id="c1da1-207">CreateUserWizard 是一個範本化控制項,派生自嚮導類並提供以下範本:</span><span class="sxs-lookup"><span data-stu-id="c1da1-207">The CreateUserWizard is a templated control that derives from the Wizard class and provides the following templates:</span></span>

- <span data-ttu-id="c1da1-208">**標題樣本**此範本控制嚮導標頭的外觀。</span><span class="sxs-lookup"><span data-stu-id="c1da1-208">**HeaderTemplate** This template controls the appearance of the header of the wizard.</span></span>
- <span data-ttu-id="c1da1-209">**側邊欄樣本**此範本控制嚮導側邊欄的外觀。</span><span class="sxs-lookup"><span data-stu-id="c1da1-209">**SidebarTemplate** This template controls the appearance of the sidebar of the wizard.</span></span>
- <span data-ttu-id="c1da1-210">**開機瀏覽樣本**此範本控制導航的外觀是嚮導在開始步驟。</span><span class="sxs-lookup"><span data-stu-id="c1da1-210">**StartNavigationTemplate** This template controls the appearance of the navigation are of the wizard at the start step.</span></span>
- <span data-ttu-id="c1da1-211">**步進瀏覽樣本**此範本控制在導航區域的外觀時不在開始或完成步驟中。</span><span class="sxs-lookup"><span data-stu-id="c1da1-211">**StepNavigationTemplate** This template controls the appearance of the navigation area when not in the start or finish step.</span></span>
- <span data-ttu-id="c1da1-212">**完成瀏覽樣本**此範本控制導航區域在完成步驟上的外觀。</span><span class="sxs-lookup"><span data-stu-id="c1da1-212">**FinishNavigationTemplate** This template controls the appearance of the navigation area when on the finish step.</span></span>

<span data-ttu-id="c1da1-213">此外,對於添加到嚮導的每個步驟,ASP.NET將創建一個自定義範本,其中包含該步驟的內容範本和自定義導航範本。</span><span class="sxs-lookup"><span data-stu-id="c1da1-213">Additionally, for each step that you add to the Wizard, ASP.NET will create a custom template that contains both a ContentTemplate and a CustomNavigationTemplate for that step.</span></span> <span data-ttu-id="c1da1-214">有關自訂 CreateUserWizard 的完整詳細資訊,請參閱 2005 年VS.NET文檔:</span><span class="sxs-lookup"><span data-stu-id="c1da1-214">For full details on customizing the CreateUserWizard, see the VS.NET 2005 documentation:</span></span>

## <a name="changepassword-control"></a><span data-ttu-id="c1da1-215">變更密碼控制</span><span class="sxs-lookup"><span data-stu-id="c1da1-215">ChangePassword Control</span></span>

<span data-ttu-id="c1da1-216">更改密碼控制項允許使用者更改其密碼。</span><span class="sxs-lookup"><span data-stu-id="c1da1-216">The ChangePassword control allows users to change his or her password.</span></span> <span data-ttu-id="c1da1-217">如果 DisplayUserName 屬性為 true(預設情況下為 false),則用戶可以在未登錄時更改其密碼。</span><span class="sxs-lookup"><span data-stu-id="c1da1-217">If the DisplayUserName property is true (it is false by default), the user can change his or her password when they are not logged in.</span></span> <span data-ttu-id="c1da1-218">如果使用者*已*登錄,並且 DisplayUserName 屬性為 true,則使用者將能夠更改未登錄的其他使用者的密碼,前提是他們知道該使用者的使用者 ID。</span><span class="sxs-lookup"><span data-stu-id="c1da1-218">If the user *is* already logged in and the DisplayUserName property is true, the user will be able to change the password of another user that is not logged in providing they know the user ID of that user.</span></span>

<span data-ttu-id="c1da1-219">請記住,如果您希望用戶能夠在無需登錄的情況下更改密碼,則需要確保顯示更改密碼控制項的頁面允許匿名存取。</span><span class="sxs-lookup"><span data-stu-id="c1da1-219">Keep in mind that if you want users to be able to change passwords without having to log in, you will need to ensure that the page on which the ChangePassword control is displayed allows anonymous access.</span></span> <span data-ttu-id="c1da1-220">顯然,用戶必須提供其舊密碼才能更改其密碼。</span><span class="sxs-lookup"><span data-stu-id="c1da1-220">Obviously, users will have to provide their old password in order to change their password.</span></span>

## <a name="role-management"></a><span data-ttu-id="c1da1-221">角色管理</span><span class="sxs-lookup"><span data-stu-id="c1da1-221">Role Management</span></span>

<span data-ttu-id="c1da1-222">角色管理允許您將使用者分配給特定角色,然後根據該角色限制對某些檔或資料夾的訪問。</span><span class="sxs-lookup"><span data-stu-id="c1da1-222">Role management allows you to assign users to a particular role and then restrict access to certain file or folders based on that role.</span></span> <span data-ttu-id="c1da1-223">角色管理還提供 API,以便您可以以程式設計方式確定某人的角色或確定特定角色的所有使用者並做出相應回應。</span><span class="sxs-lookup"><span data-stu-id="c1da1-223">Role management also provides an API so that you can programmatically determine someones role or determine all users in a particular role and respond accordingly.</span></span>

<span data-ttu-id="c1da1-224">角色管理不是ASP.NET成員的要求,也不是使用角色管理的要求。</span><span class="sxs-lookup"><span data-stu-id="c1da1-224">Role management is not a requirement in ASP.NET membership, nor is membership a requirement in order to use role management.</span></span> <span data-ttu-id="c1da1-225">然而,兩者互相補充得很好,開發人員可能會將它們結合使用。</span><span class="sxs-lookup"><span data-stu-id="c1da1-225">However, the two supplement each other nicely and it is likely that developers will use them in conjunction with each other.</span></span>

<span data-ttu-id="c1da1-226">要在應用程式中啟用角色管理,請對 Web.config 檔中進行以下變更:</span><span class="sxs-lookup"><span data-stu-id="c1da1-226">To enable role management in your application, make the following change in your web.config file:</span></span>

[!code-xml[Main](membership/samples/sample2.xml)]

<span data-ttu-id="c1da1-227">當**快取RolesInCookie**屬性設置為 true 時,ASP.NET緩存用戶端 Cookie 中的使用者角色成員身份。</span><span class="sxs-lookup"><span data-stu-id="c1da1-227">When the **cacheRolesInCookie** attribute is set to true, ASP.NET caches a users role membership in a cookie on the client.</span></span> <span data-ttu-id="c1da1-228">這允許在不調用角色提供程序的情況下進行角色查找。</span><span class="sxs-lookup"><span data-stu-id="c1da1-228">This allows role lookups to occur without calls into the RoleProvider.</span></span> <span data-ttu-id="c1da1-229">使用此屬性時,鼓勵開發人員確保**cookie 保護**屬性設置為" 全部"</span><span class="sxs-lookup"><span data-stu-id="c1da1-229">When using this attribute, developers are encouraged to ensure that the **cookieProtection** attribute is set to All.</span></span> <span data-ttu-id="c1da1-230">(這是默認設置。這可確保 Cookie 數據經過加密,並有助於確保 Cookie 內容未被更改。</span><span class="sxs-lookup"><span data-stu-id="c1da1-230">(This is the default setting.) This ensures that the cookie data are encrypted and helps to ensure that the cookies contents haven't been altered.</span></span> <span data-ttu-id="c1da1-231">可以使用網站管理工具添加角色。</span><span class="sxs-lookup"><span data-stu-id="c1da1-231">Roles can be added using the Web Site Administration Tool.</span></span> <span data-ttu-id="c1da1-232">它允許您輕鬆定義角色、根據這些角色配置對網站部分的訪問,並將使用者分配給角色。</span><span class="sxs-lookup"><span data-stu-id="c1da1-232">It allows you to easily define roles, configure access to parts of the site based on those roles, and assign users to roles.</span></span>

![](membership/_static/image6.jpg)

<span data-ttu-id="c1da1-233">**圖 6**</span><span class="sxs-lookup"><span data-stu-id="c1da1-233">**Figure 6**</span></span>

<span data-ttu-id="c1da1-234">如上所述,只需輸入角色的名稱,然後單擊"添加角色"即可添加新角色。</span><span class="sxs-lookup"><span data-stu-id="c1da1-234">As shown above, new roles can be added by simply entering the name of the role and then clicking Add Role.</span></span> <span data-ttu-id="c1da1-235">通過按一下現有角色清單中的相應連結,可以管理或刪除現有角色。</span><span class="sxs-lookup"><span data-stu-id="c1da1-235">Existing roles can be managed or deleted by clicking the appropriate link in the list of existing roles.</span></span>

<span data-ttu-id="c1da1-236">管理角色時,可以添加或刪除使用者,如下所示。</span><span class="sxs-lookup"><span data-stu-id="c1da1-236">When you manage a role, you can add or remove users as shown below.</span></span>

![](membership/_static/image7.jpg)

<span data-ttu-id="c1da1-237">**圖 7**</span><span class="sxs-lookup"><span data-stu-id="c1da1-237">**Figure 7**</span></span>

<span data-ttu-id="c1da1-238">通過選中「用戶處於角色」複選框,可以輕鬆地將使用者添加到特定角色。</span><span class="sxs-lookup"><span data-stu-id="c1da1-238">By checking the User Is In Role checkbox, you can easily add a user to a specific role.</span></span> <span data-ttu-id="c1da1-239">ASP.NET將自動使用適當的條目更新您的成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="c1da1-239">ASP.NET will automatically update your membership database with the appropriate entries.</span></span> <span data-ttu-id="c1da1-240">您還需要為應用程式設定訪問規則。</span><span class="sxs-lookup"><span data-stu-id="c1da1-240">You will also want to configure access rules for your application.</span></span> <span data-ttu-id="c1da1-241">ASP.NET 1.x 開發人員熟悉通過 Web.config 檔中&lt;的授權&gt;元素執行此操作,該選項在 2.0 ASP.NET 中仍然可用。</span><span class="sxs-lookup"><span data-stu-id="c1da1-241">ASP.NET 1.x developers are familiar with doing this via the &lt;authorization&gt; element in the web.config file, and that option is still available in ASP.NET 2.0.</span></span> <span data-ttu-id="c1da1-242">但是,它更易於使用網站管理工具管理訪問規則,如下所示。</span><span class="sxs-lookup"><span data-stu-id="c1da1-242">However, its easier to manage access rules using the Web Site Administration Tool as shown below.</span></span>

![](membership/_static/image8.jpg)

<span data-ttu-id="c1da1-243">**圖 8**</span><span class="sxs-lookup"><span data-stu-id="c1da1-243">**Figure 8**</span></span>

<span data-ttu-id="c1da1-244">在這種情況下,管理資料夾將突出顯示(由於該工具以淺灰色突出顯示它而難以查看),並且管理員角色已被授予訪問許可權。</span><span class="sxs-lookup"><span data-stu-id="c1da1-244">In this case, the Administration folder is highlighted (its difficult to see because the tool highlights it in light gray) and the Administrators role has been granted access.</span></span> <span data-ttu-id="c1da1-245">所有其他使用者都被拒絕。</span><span class="sxs-lookup"><span data-stu-id="c1da1-245">All other users are denied.</span></span> <span data-ttu-id="c1da1-246">您可以按下頭部圖示來選擇規則,然後使用「向上移動」 和「向下移動」按鈕來排列規則。</span><span class="sxs-lookup"><span data-stu-id="c1da1-246">You can click on the head icon to select a rule and then use the Move Up and Move Down buttons to arrange the rules.</span></span> <span data-ttu-id="c1da1-247">與ASP.NET&lt;&gt;授權 元素一樣,規則按它們出現的順序進行處理。</span><span class="sxs-lookup"><span data-stu-id="c1da1-247">As with the ASP.NET &lt;authorization&gt; element, rules are processed in the order in which they appear.</span></span> <span data-ttu-id="c1da1-248">換句話說,如果上述鏡頭中的規則順序顛倒,則任何人都無法訪問管理檔夾,因為ASP.NET遇到的第一個規則是拒絕所有人到該資料夾的規則。</span><span class="sxs-lookup"><span data-stu-id="c1da1-248">In other words, if the order of rules in the shot above were reversed, no one would have access to the Administration folder because the first rule that ASP.NET would encounter would be the rule that denies everyone to the folder.</span></span>

<span data-ttu-id="c1da1-249">ASP.NET 2.0 將 Web.config 檔添加到要為其指定訪問規則的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c1da1-249">ASP.NET 2.0 adds a web.config file to the folder for which you are specifying an access rule.</span></span> <span data-ttu-id="c1da1-250">訪問規則可以通過配置檔或通過網站管理工具進行編輯。</span><span class="sxs-lookup"><span data-stu-id="c1da1-250">Access rules can be edited via the configuration file or via the Web Site Administration Tool.</span></span> <span data-ttu-id="c1da1-251">換句話說,網站管理工具只是一個介面,可以通過該介面在使用者友好的環境中編輯配置檔。</span><span class="sxs-lookup"><span data-stu-id="c1da1-251">In other words, the Web Site Administration Tool is simply an interface through which the configuration file can be edited in a user-friendly environment.</span></span>

## <a name="using-roles-in-code"></a><span data-ttu-id="c1da1-252">在程式碼中使用角色</span><span class="sxs-lookup"><span data-stu-id="c1da1-252">Using Roles in Code</span></span>

<span data-ttu-id="c1da1-253">自版本 1.x 以來,用於角色管理的 API 未更改。</span><span class="sxs-lookup"><span data-stu-id="c1da1-253">The API for role management has not changed since version 1.x.</span></span> <span data-ttu-id="c1da1-254">**IsInRole**方法用於確定使用者是否處於特定角色。</span><span class="sxs-lookup"><span data-stu-id="c1da1-254">The **IsInRole** method is used to determine if a user is in a particular role.</span></span>

[!code-csharp[Main](membership/samples/sample3.cs)]

<span data-ttu-id="c1da1-255">ASP.NET還會創建作為當前上下文的成員的 RoleThe 實例。</span><span class="sxs-lookup"><span data-stu-id="c1da1-255">ASP.NET also creates a RolePrincipal instance as a member of the current context.</span></span> <span data-ttu-id="c1da1-256">RoleThe 物件可用於獲取使用者所屬的所有角色,如下所示:</span><span class="sxs-lookup"><span data-stu-id="c1da1-256">The RolePrincipal object can be used to obtain all of the roles to which the user belongs as follows:</span></span>

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a><span data-ttu-id="c1da1-257">將角色群組與登入檢視控制項一起使用</span><span class="sxs-lookup"><span data-stu-id="c1da1-257">Using RoleGroups with the LoginView Control</span></span>

<span data-ttu-id="c1da1-258">現在,您已經瞭解了角色管理和成員資格,讓我們簡要討論一下 LoginView 控件如何在 ASP.NET 2.0 中利用此功能。</span><span class="sxs-lookup"><span data-stu-id="c1da1-258">Now that you have an understanding of role management and membership, lets discuss briefly how the LoginView control takes advantage of this capability in ASP.NET 2.0.</span></span> <span data-ttu-id="c1da1-259">如前所述,LoginView 控件是一個範本化控制項,預設情況下包含兩個範本;預設情況下,該控件包含兩個範本。匿名範本和登錄範本。</span><span class="sxs-lookup"><span data-stu-id="c1da1-259">As previously discussed, the LoginView control is a templated control that contains two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="c1da1-260">在「登錄查看工作」對話框中,是一個連結(如下所示),允許您編輯角色組。</span><span class="sxs-lookup"><span data-stu-id="c1da1-260">Within the LoginView Tasks dialog is a link (shown below) that allows you to edit RoleGroups.</span></span>

![](membership/_static/image9.jpg)

<span data-ttu-id="c1da1-261">**圖 9**</span><span class="sxs-lookup"><span data-stu-id="c1da1-261">**Figure 9**</span></span>

<span data-ttu-id="c1da1-262">每個 RoleGroup 物件都包含一個字串陣列,用於定義角色組應用於哪些角色。</span><span class="sxs-lookup"><span data-stu-id="c1da1-262">Each RoleGroup object contains an array of strings that defines which roles that RoleGroup applies to.</span></span> <span data-ttu-id="c1da1-263">要向「登錄檢視」控制件添加新角色組,請單擊「編輯角色組」連結。</span><span class="sxs-lookup"><span data-stu-id="c1da1-263">To add a new RoleGroup to the LoginView control, click the Edit RoleGroups link.</span></span> <span data-ttu-id="c1da1-264">在上面的映射中,您可以看到我為管理員添加了新的角色組。</span><span class="sxs-lookup"><span data-stu-id="c1da1-264">In the image above, you can see that I have added a new RoleGroup for Administrators.</span></span> <span data-ttu-id="c1da1-265">通過從「檢視」下拉清單中選擇該角色組(RoleGroup{0}),我可以配置一個僅顯示給管理員角色的範本。</span><span class="sxs-lookup"><span data-stu-id="c1da1-265">By selecting that RoleGroup (RoleGroup[0]) from the Views dropdown, I can configure a template that will only be displayed to members of the Administrators role.</span></span> <span data-ttu-id="c1da1-266">在下圖中,我添加了一個新的 RoleGroup,該角色組適用於銷售角色和分發角色的成員。</span><span class="sxs-lookup"><span data-stu-id="c1da1-266">In the image below, I have added a new RoleGroup that applies to members of the Sales role and the Distribution role.</span></span> <span data-ttu-id="c1da1-267">這會將第二個角色組添加到 LoginView 任務對話方塊中的「視圖」下拉下拉,而添加到該範本的任何內容都將被「銷售」或「分發」角色中的任何使用者看到。</span><span class="sxs-lookup"><span data-stu-id="c1da1-267">This adds a second RoleGroup to the Views dropdown in the LoginView Tasks dialog and anything added to that template will be visible by any user in either the Sales or Distribution role.</span></span>

![](membership/_static/image10.jpg)

<span data-ttu-id="c1da1-268">**圖 10**</span><span class="sxs-lookup"><span data-stu-id="c1da1-268">**Figure 10**</span></span>

## <a name="overriding-the-existing-membership-provider"></a><span data-ttu-id="c1da1-269">重寫現有成員資格提供者</span><span class="sxs-lookup"><span data-stu-id="c1da1-269">Overriding the Existing Membership Provider</span></span>

<span data-ttu-id="c1da1-270">有幾種方法可以擴展ASP.NET成員資格的功能。</span><span class="sxs-lookup"><span data-stu-id="c1da1-270">There are a couple of ways that you can extend the functionality of ASP.NET membership.</span></span> <span data-ttu-id="c1da1-271">首先,您顯然可以通過繼承 SqlSasas 提供者類並重寫其方法來更改其現有功能。</span><span class="sxs-lookup"><span data-stu-id="c1da1-271">First of all, you can obviously change the existing functionality of the SqlMembershipProvider class by inheriting from it and overriding its methods.</span></span> <span data-ttu-id="c1da1-272">例如,如果要在創建使用者時實現自己的功能,可以創建自己的類,從 SqlSaasProvider 繼承,如下所示:</span><span class="sxs-lookup"><span data-stu-id="c1da1-272">For example, if you want to implement your own functionality when users are created, you can create your own class that inherits from SqlMembershipProvider as follows:</span></span>

[!code-csharp[Main](membership/samples/sample5.cs)]

<span data-ttu-id="c1da1-273">另一方面,如果要創建自己的提供程式(例如,將成員資格資訊存儲在 Access 資料庫中),則可以創建自己的提供程式。</span><span class="sxs-lookup"><span data-stu-id="c1da1-273">If, on the other hand, you want to create your own provider (to store your membership information in an Access database, for example), you can create your own provider.</span></span>

## <a name="creating-your-own-membership-provider"></a><span data-ttu-id="c1da1-274">建立您自己的成員資格提供者</span><span class="sxs-lookup"><span data-stu-id="c1da1-274">Creating Your Own Membership Provider</span></span>

<span data-ttu-id="c1da1-275">要創建自己的成員資格提供程式,首先需要創建從成員資格提供程式類繼承的類。</span><span class="sxs-lookup"><span data-stu-id="c1da1-275">To create your own membership provider, you will first need to create a class that inherits from the MembershipProvider class.</span></span> <span data-ttu-id="c1da1-276">如果使用VB.NET,Visual Studio 2005 將添加需要重寫的所有方法的存根。</span><span class="sxs-lookup"><span data-stu-id="c1da1-276">If you are using VB.NET, Visual Studio 2005 will add the stubs for all of the methods that you need to override.</span></span> <span data-ttu-id="c1da1-277">如果使用 C#,則要添加存根。</span><span class="sxs-lookup"><span data-stu-id="c1da1-277">If you are using C#, its up to you to add the stubs.</span></span>

<span data-ttu-id="c1da1-278">您需要重寫以下內容:</span><span class="sxs-lookup"><span data-stu-id="c1da1-278">You will need to override the following:</span></span>

- <span data-ttu-id="c1da1-279">應用程式名稱屬性</span><span class="sxs-lookup"><span data-stu-id="c1da1-279">ApplicationName property</span></span>
- <span data-ttu-id="c1da1-280">變更密碼功能</span><span class="sxs-lookup"><span data-stu-id="c1da1-280">ChangePassword function</span></span>
- <span data-ttu-id="c1da1-281">變更密碼問答功能</span><span class="sxs-lookup"><span data-stu-id="c1da1-281">ChangePasswordQuestionAndAnswer function</span></span>
- <span data-ttu-id="c1da1-282">建立使用者函數</span><span class="sxs-lookup"><span data-stu-id="c1da1-282">CreateUser function</span></span>
- <span data-ttu-id="c1da1-283">移除使用者功能</span><span class="sxs-lookup"><span data-stu-id="c1da1-283">DeleteUser function</span></span>
- <span data-ttu-id="c1da1-284">開啟密碼重設屬性</span><span class="sxs-lookup"><span data-stu-id="c1da1-284">EnablePasswordReset property</span></span>
- <span data-ttu-id="c1da1-285">開啟密碼擷取權</span><span class="sxs-lookup"><span data-stu-id="c1da1-285">EnablePasswordRetrieval property</span></span>
- <span data-ttu-id="c1da1-286">尋找使用者電子郵件功能</span><span class="sxs-lookup"><span data-stu-id="c1da1-286">FindUsersByEmail function</span></span>
- <span data-ttu-id="c1da1-287">尋找使用者依名稱函數</span><span class="sxs-lookup"><span data-stu-id="c1da1-287">FindUsersByName function</span></span>
- <span data-ttu-id="c1da1-288">取得所有使用者功能</span><span class="sxs-lookup"><span data-stu-id="c1da1-288">GetAllUsers function</span></span>
- <span data-ttu-id="c1da1-289">取得使用者數量上線功能</span><span class="sxs-lookup"><span data-stu-id="c1da1-289">GetNumberOfUsersOnline function</span></span>
- <span data-ttu-id="c1da1-290">取得密碼功能</span><span class="sxs-lookup"><span data-stu-id="c1da1-290">GetPassword function</span></span>
- <span data-ttu-id="c1da1-291">取得使用者功能</span><span class="sxs-lookup"><span data-stu-id="c1da1-291">GetUser function</span></span>
- <span data-ttu-id="c1da1-292">取得使用者名稱透過電子郵件功能</span><span class="sxs-lookup"><span data-stu-id="c1da1-292">GetUserNameByEmail function</span></span>
- <span data-ttu-id="c1da1-293">最大不合法密碼嘗試屬性</span><span class="sxs-lookup"><span data-stu-id="c1da1-293">MaxInvalidPasswordAttempts property</span></span>
- <span data-ttu-id="c1da1-294">最小必需的NonAlpha字元屬性</span><span class="sxs-lookup"><span data-stu-id="c1da1-294">MinRequiredNonAlphanumericCharacters property</span></span>
- <span data-ttu-id="c1da1-295">最小所需密碼長度屬性</span><span class="sxs-lookup"><span data-stu-id="c1da1-295">MinRequiredPasswordLength property</span></span>
- <span data-ttu-id="c1da1-296">密碼嘗試視窗屬性</span><span class="sxs-lookup"><span data-stu-id="c1da1-296">PasswordAttemptWindow property</span></span>
- <span data-ttu-id="c1da1-297">密碼格式屬性</span><span class="sxs-lookup"><span data-stu-id="c1da1-297">PasswordFormat property</span></span>
- <span data-ttu-id="c1da1-298">密碼強度正規表示式屬性</span><span class="sxs-lookup"><span data-stu-id="c1da1-298">PasswordStrengthRegularExpression property</span></span>
- <span data-ttu-id="c1da1-299">需要問答屬性</span><span class="sxs-lookup"><span data-stu-id="c1da1-299">RequiresQuestionAndAnswer property</span></span>
- <span data-ttu-id="c1da1-300">需要唯一電子郵件屬性</span><span class="sxs-lookup"><span data-stu-id="c1da1-300">RequiresUniqueEmail property</span></span>
- <span data-ttu-id="c1da1-301">重置密碼功能</span><span class="sxs-lookup"><span data-stu-id="c1da1-301">ResetPassword function</span></span>
- <span data-ttu-id="c1da1-302">解除鎖定使用者功能</span><span class="sxs-lookup"><span data-stu-id="c1da1-302">Unlock user function</span></span>
- <span data-ttu-id="c1da1-303">更新使用者功能</span><span class="sxs-lookup"><span data-stu-id="c1da1-303">UpdateUser function</span></span>
- <span data-ttu-id="c1da1-304">驗證使用者功能</span><span class="sxs-lookup"><span data-stu-id="c1da1-304">ValidateUser function</span></span>

<span data-ttu-id="c1da1-305">這是一個相當的清單,以C#開發人員實現。</span><span class="sxs-lookup"><span data-stu-id="c1da1-305">Thats quite a list to implement as a C# developer.</span></span> <span data-ttu-id="c1da1-306">您可能會發現在沒有任何實現的情況下在VB.NET中創建類會更容易,然後使用 .NET 反射器或類似工具將代碼轉換為 C#。</span><span class="sxs-lookup"><span data-stu-id="c1da1-306">You may find it easier to create the class in VB.NET without any implementation and then use .NET Reflector or a similar tool to convert the code to C#.</span></span>

<span data-ttu-id="c1da1-307">連接字串和其他屬性應設定為初始化方法中的預設值。</span><span class="sxs-lookup"><span data-stu-id="c1da1-307">The connection string and other properties should be set to their defaults in the Initialize method.</span></span> <span data-ttu-id="c1da1-308">(在運行時載入提供程式時,將觸發初始化方法。初始化方法的第二個參數是 System.集合.專業.NameValueCollection,它是對 Web.config&lt;&gt;檔中與自訂提供程式關聯的添加元素的引用。</span><span class="sxs-lookup"><span data-stu-id="c1da1-308">(The Initialize method is fired when the provider is loaded at runtime.) The second parameter to the Initialize method is of type System.Collections.Specialized.NameValueCollection and is a reference to the &lt;add&gt; element that is associated with your custom provider in the web.config file.</span></span> <span data-ttu-id="c1da1-309">該條目如下所示:</span><span class="sxs-lookup"><span data-stu-id="c1da1-309">That entry looks like the following:</span></span>

[!code-xml[Main](membership/samples/sample6.xml)]

<span data-ttu-id="c1da1-310">下面是初始化方法的示例。</span><span class="sxs-lookup"><span data-stu-id="c1da1-310">Here is an example of the Initialize method.</span></span>

[!code-csharp[Main](membership/samples/sample7.cs)]

<span data-ttu-id="c1da1-311">為了驗證使用者提交登錄表單時,您需要使用驗證使用者方法。</span><span class="sxs-lookup"><span data-stu-id="c1da1-311">In order to validate the user when they submit your login form, you will need to use the ValidateUser method.</span></span> <span data-ttu-id="c1da1-312">當用戶按一下登錄控制項中的登錄按鈕時,將觸發此方法。</span><span class="sxs-lookup"><span data-stu-id="c1da1-312">This method fires when the user clicks the login button in the Login control.</span></span> <span data-ttu-id="c1da1-313">您將在此方法中放置執行使用者查找的代碼。</span><span class="sxs-lookup"><span data-stu-id="c1da1-313">You will place your code that does the user lookup in this method.</span></span>

<span data-ttu-id="c1da1-314">正如您所看到的,編寫自己的成員資格提供程式並不困難,允許您擴展ASP.NET 2.0 的強大功能。</span><span class="sxs-lookup"><span data-stu-id="c1da1-314">As you can see, writing your own membership provider is not difficult and allows you to extend this powerful functionality of ASP.NET 2.0.</span></span>
