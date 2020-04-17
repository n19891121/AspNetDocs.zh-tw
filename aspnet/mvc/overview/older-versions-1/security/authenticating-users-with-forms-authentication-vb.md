---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
title: 使用表單身份驗證 (VB) 對使用者進行身份驗證 |微軟文件
author: rick-anderson
description: 瞭解如何使用 [授權] 屬性來密碼保護 MVC 應用程式中的特定頁面。 您也瞭解如何使用網站管理...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 4341f5b1-6fe5-44c5-8b8a-18fa84f80177
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: 9e3117af55db2effed20b6421c2322f1c265f1c7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540814"
---
# <a name="authenticating-users-with-forms-authentication-vb"></a><span data-ttu-id="acf98-104">使用表單驗證驗證使用者 (VB)</span><span class="sxs-lookup"><span data-stu-id="acf98-104">Authenticating Users with Forms Authentication (VB)</span></span>

<span data-ttu-id="acf98-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="acf98-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="acf98-106">瞭解如何使用 [授權] 屬性來密碼保護 MVC 應用程式中的特定頁面。</span><span class="sxs-lookup"><span data-stu-id="acf98-106">Learn how to use the [Authorize] attribute to password protect particular pages in your MVC application.</span></span> <span data-ttu-id="acf98-107">您將瞭解如何使用網站管理工具創建和管理使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="acf98-107">You learn how to use the Web Site Administration Tool to create and manage users and roles.</span></span> <span data-ttu-id="acf98-108">您還瞭解如何配置使用者帳戶和角色資訊的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="acf98-108">You also learn how to configure where user account and role information is stored.</span></span>

<span data-ttu-id="acf98-109">本教學的目的是說明如何使用表單身分驗證來密碼保護ASP.NET MVC 應用程式中的檢視。</span><span class="sxs-lookup"><span data-stu-id="acf98-109">The goal of this tutorial is to explain how you can use Forms authentication to password protect the views in your ASP.NET MVC applications.</span></span> <span data-ttu-id="acf98-110">您將瞭解如何使用網站管理工具創建使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="acf98-110">You learn how to use the Web Site Administration Tool to create users and roles.</span></span> <span data-ttu-id="acf98-111">您還學習如何防止未經授權的使用者呼叫控制器操作。</span><span class="sxs-lookup"><span data-stu-id="acf98-111">You also learn how to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="acf98-112">最後,您將瞭解如何配置使用者名和密碼的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="acf98-112">Finally, you learn how to configure where user names and passwords are stored.</span></span>

#### <a name="using-the-web-site-administration-tool"></a><span data-ttu-id="acf98-113">使用網站管理工具</span><span class="sxs-lookup"><span data-stu-id="acf98-113">Using the Web Site Administration Tool</span></span>

<span data-ttu-id="acf98-114">在做其他事情之前,我們應該從創建一些使用者和角色開始。</span><span class="sxs-lookup"><span data-stu-id="acf98-114">Before we do anything else, we should start by creating some users and roles.</span></span> <span data-ttu-id="acf98-115">創建新使用者和角色的最簡單方法是利用 Visual Studio 2008 網站管理工具。</span><span class="sxs-lookup"><span data-stu-id="acf98-115">The easiest way to create new users and roles is to take advantage of the Visual Studio 2008 Web Site Administration Tool.</span></span> <span data-ttu-id="acf98-116">您可以通過選擇選單選項 **「專案」ASP.NET 設定**啟動此工具。</span><span class="sxs-lookup"><span data-stu-id="acf98-116">You can launch this tool by selecting the menu option **Project, ASP.NET Configuration**.</span></span> <span data-ttu-id="acf98-117">或者,您可以通過單擊位於解決方案資源管理器視窗頂部的鎚子(有點可怕)圖示啟動網站管理工具(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="acf98-117">Alternatively, you can launch the Web Site Administration Tool by clicking the (somewhat scary) icon of the hammer hitting the world that appears at the top of the Solution Explorer window (see Figure 1).</span></span>

<span data-ttu-id="acf98-118">**圖 1 - 啟動網站管理工具**</span><span class="sxs-lookup"><span data-stu-id="acf98-118">**Figure 1 – Launching the Web Site Administration Tool**</span></span>

![clip_image002[4]](authenticating-users-with-forms-authentication-vb/_static/image1.jpg)

<span data-ttu-id="acf98-120">在網站管理工具中,您可以通過選擇「安全」選項卡創建新使用者和角色。按一下「**創建使用者**」連結以創建名為 Stephen 的新使用者(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="acf98-120">Within the Web Site Administration Tool, you create new users and roles by selecting the Security tab. Click the **Create user** link to create a new user named Stephen (see Figure 2).</span></span> <span data-ttu-id="acf98-121">向 Stephen 使用者提供所需的任何密碼(例如,*機密*)。</span><span class="sxs-lookup"><span data-stu-id="acf98-121">Provide the Stephen user with any password that you want (for example, *secret*).</span></span>

<span data-ttu-id="acf98-122">**圖 2 = 建立新使用者**</span><span class="sxs-lookup"><span data-stu-id="acf98-122">**Figure 2 – Creating a new user**</span></span>

![clip_image004[4]](authenticating-users-with-forms-authentication-vb/_static/image2.jpg)

<span data-ttu-id="acf98-124">通過首先啟用角色和定義一個或多個角色來創建新角色。</span><span class="sxs-lookup"><span data-stu-id="acf98-124">You create new roles by first enabling roles and defining one or more roles.</span></span> <span data-ttu-id="acf98-125">以按下 **「啟用角色」連結啟用角色**。</span><span class="sxs-lookup"><span data-stu-id="acf98-125">Enable roles by clicking the **Enable roles** link.</span></span> <span data-ttu-id="acf98-126">接下來,通過單擊 **「創建或管理角色」連結創建**名為 *「管理員*」的角色(參見圖 3)。</span><span class="sxs-lookup"><span data-stu-id="acf98-126">Next, create a role named *Administrators* by clicking the **Create or Manage roles** link (see Figure 3).</span></span>

<span data-ttu-id="acf98-127">**圖 3 • 建立新角色**</span><span class="sxs-lookup"><span data-stu-id="acf98-127">**Figure 3 – Creating a new role**</span></span>

![clip_image006[4]](authenticating-users-with-forms-authentication-vb/_static/image3.jpg)

<span data-ttu-id="acf98-129">最後,通過單擊"創建使用者"連結並在創建 Sally 時選擇管理員(參見圖 4),創建名為 Sally 的新使用者並將 Sally 與管理員角色相關聯。</span><span class="sxs-lookup"><span data-stu-id="acf98-129">Finally, create a new user named Sally and associate Sally with the Administrators role by clicking the Create User link and selecting Administrators when creating Sally (see Figure 4).</span></span>

<span data-ttu-id="acf98-130">**圖 4 = 將使用者新增到角色**</span><span class="sxs-lookup"><span data-stu-id="acf98-130">**Figure 4 – Adding a user to a role**</span></span>

![clip_image008[4]](authenticating-users-with-forms-authentication-vb/_static/image4.jpg)

<span data-ttu-id="acf98-132">當所有說和完成,你應該有兩個新的使用者叫斯蒂芬和莎莉。</span><span class="sxs-lookup"><span data-stu-id="acf98-132">When all is said and done, you should have two new users named Stephen and Sally.</span></span> <span data-ttu-id="acf98-133">您還應具有名為"管理員"的新角色。</span><span class="sxs-lookup"><span data-stu-id="acf98-133">You should also have a new role named Administrators.</span></span> <span data-ttu-id="acf98-134">Sally 是管理員角色的成員,而斯蒂芬不是。</span><span class="sxs-lookup"><span data-stu-id="acf98-134">Sally is a member of the Administrators role and Stephen is not.</span></span>

#### <a name="requiring-authorization"></a><span data-ttu-id="acf98-135">需要授權</span><span class="sxs-lookup"><span data-stu-id="acf98-135">Requiring Authorization</span></span>

<span data-ttu-id="acf98-136">在使用者調用控制器操作之前,可以通過將 [授權] 屬性添加到操作,要求使用者進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="acf98-136">You can require a user to be authenticated before the user invokes a controller action by adding the [Authorize] attribute to the action.</span></span> <span data-ttu-id="acf98-137">您可以將 [授權] 屬性應用於單個控制器操作,也可以將此屬性應用於整個控制器類。</span><span class="sxs-lookup"><span data-stu-id="acf98-137">You can apply the [Authorize] attribute to an individual controller action or you can apply this attribute to an entire controller class.</span></span>

<span data-ttu-id="acf98-138">例如,清單 1 中的控制器公開名為「公司機密」的操作。</span><span class="sxs-lookup"><span data-stu-id="acf98-138">For example, the controller in Listing 1 exposes an action named CompanySecrets().</span></span> <span data-ttu-id="acf98-139">由於此操作使用 [授權] 屬性進行修飾,因此除非對使用者進行身份驗證,否則無法調用此操作。</span><span class="sxs-lookup"><span data-stu-id="acf98-139">Because this action is decorated with the [Authorize] attribute, this action cannot be invoked unless a user is authenticated.</span></span>

<span data-ttu-id="acf98-140">**清單1 = 控制器\主控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="acf98-140">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample1.vb)]

<span data-ttu-id="acf98-141">如果您在瀏覽器的位址列中輸入 URL/Home/CompanySecrets 來呼叫公司機密()操作,而您不是經過身份驗證的使用者,則將自動重定向到登入檢視(參見圖 5)。</span><span class="sxs-lookup"><span data-stu-id="acf98-141">If you invoke the CompanySecrets() action by entering the URL /Home/CompanySecrets in the address bar of your browser, and you are not an authenticated user, then you will be redirected to the Login view automatically (see Figure 5).</span></span>

<span data-ttu-id="acf98-142">**圖 5 = 登入檢視**</span><span class="sxs-lookup"><span data-stu-id="acf98-142">**Figure 5 – The Login view**</span></span>

![clip_image010[4]](authenticating-users-with-forms-authentication-vb/_static/image5.jpg)

<span data-ttu-id="acf98-144">您可以使用「登錄」檢視輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="acf98-144">You can use the Login view to enter your user name and password.</span></span> <span data-ttu-id="acf98-145">如果您不是註冊用戶,則可以按下**註冊**連結以導航到"註冊"視圖(參見圖 6)。</span><span class="sxs-lookup"><span data-stu-id="acf98-145">If you are not a registered user then you can click the **register** link to navigate to the Register view (see Figure 6).</span></span> <span data-ttu-id="acf98-146">您可以使用"註冊"視圖創建新使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="acf98-146">You can use the Register view to create a new user account.</span></span>

<span data-ttu-id="acf98-147">**圖 6 = 寄存器檢視**</span><span class="sxs-lookup"><span data-stu-id="acf98-147">**Figure 6 – The Register view**</span></span>

![clip_image012](authenticating-users-with-forms-authentication-vb/_static/image6.jpg)

<span data-ttu-id="acf98-149">成功登錄后,您可以看到公司機密視圖(參見圖 7)。</span><span class="sxs-lookup"><span data-stu-id="acf98-149">After you successfully log in, you can see the CompanySecrets view (see Figure 7).</span></span> <span data-ttu-id="acf98-150">預設情況下,您將繼續登錄,直到關閉瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="acf98-150">By default, you will continue to be logged in until you close your browser window.</span></span>

<span data-ttu-id="acf98-151">**圖 7 = 公司機密檢視**</span><span class="sxs-lookup"><span data-stu-id="acf98-151">**Figure 7 – The CompanySecrets view**</span></span>

![clip_image014](authenticating-users-with-forms-authentication-vb/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a><span data-ttu-id="acf98-153">依使用者名稱或使用者角色授權</span><span class="sxs-lookup"><span data-stu-id="acf98-153">Authorizing by User Name or User Role</span></span>

<span data-ttu-id="acf98-154">可以使用 [授權] 屬性將對控制器操作的存取限制為一組特定使用者或一組特定的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="acf98-154">You can use the [Authorize] attribute to restrict access to a controller action to a particular set of users or a particular set of user roles.</span></span> <span data-ttu-id="acf98-155">例如,清單 2 中修改後的主控制器包含名為 StephenSecrets() 和管理員機密() 的兩個新操作。</span><span class="sxs-lookup"><span data-stu-id="acf98-155">For example, the modified Home controller in Listing 2 contains two new actions named StephenSecrets() and AdministratorSecrets().</span></span>

<span data-ttu-id="acf98-156">**清單2 = 控制器\主控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="acf98-156">**Listing 2 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample2.vb)]

<span data-ttu-id="acf98-157">只有使用者名為 Stephen 的使用者才能調用 StephenSecrets() 操作。</span><span class="sxs-lookup"><span data-stu-id="acf98-157">Only a user with the user name Stephen can invoke the StephenSecrets() action.</span></span> <span data-ttu-id="acf98-158">所有其他使用者都重定向到「登錄」視圖。</span><span class="sxs-lookup"><span data-stu-id="acf98-158">All other users get redirected to the Login view.</span></span> <span data-ttu-id="acf98-159">「使用者」屬性接受使用者帳戶名稱的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="acf98-159">The Users property accepts a comma separated list of user account names.</span></span>

<span data-ttu-id="acf98-160">只有管理員角色中的用戶可以調用管理員機密() 操作。</span><span class="sxs-lookup"><span data-stu-id="acf98-160">Only users in the Administrators role can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="acf98-161">例如,由於 Sally 是管理員組的成員,因此她可以調用管理員機密()操作。</span><span class="sxs-lookup"><span data-stu-id="acf98-161">For example, because Sally is a member of the Administrators group, she can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="acf98-162">所有其他使用者都重定向到「登錄」視圖。</span><span class="sxs-lookup"><span data-stu-id="acf98-162">All other users get redirected to the Login view.</span></span> <span data-ttu-id="acf98-163">角色屬性接受角色名稱的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="acf98-163">The Roles property accepts a comma separated list of role names.</span></span>

#### <a name="configuring-authentication"></a><span data-ttu-id="acf98-164">設定認證</span><span class="sxs-lookup"><span data-stu-id="acf98-164">Configuring Authentication</span></span>

<span data-ttu-id="acf98-165">此時,您可能想知道使用者帳戶和角色資訊的存儲位置。</span><span class="sxs-lookup"><span data-stu-id="acf98-165">At this point, you might be wondering where the user account and role information is being stored.</span></span> <span data-ttu-id="acf98-166">預設情況下,資訊存儲在 MVC 應用程式\_的應用程式數據資料夾中,名為 ASPNETDB.mdf 的 (RANU) SQL Express 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="acf98-166">By default, the information is stored in a (RANU) SQL Express database named ASPNETDB.mdf located in your MVC application's App\_Data folder.</span></span> <span data-ttu-id="acf98-167">當您開始使用成員資格時,此資料庫由ASP.NET框架自動生成。</span><span class="sxs-lookup"><span data-stu-id="acf98-167">This database is generated by the ASP.NET framework automatically when you start using membership.</span></span>

<span data-ttu-id="acf98-168">要查看解決方案資源管理器視窗中的 ASPNETDB.mdf 資料庫,首先需要選擇功能表選項"專案",顯示所有檔。</span><span class="sxs-lookup"><span data-stu-id="acf98-168">In order to see the ASPNETDB.mdf database in the Solution Explorer window, you first need to select the menu option Project, Show All Files.</span></span>

<span data-ttu-id="acf98-169">開發應用程式時,可以使用預設 SQL Express 資料庫。</span><span class="sxs-lookup"><span data-stu-id="acf98-169">Using the default SQL Express database is fine when developing an application.</span></span> <span data-ttu-id="acf98-170">但是,您很可能不希望為生產應用程式使用預設的 ASPNETDB.mdf 資料庫。</span><span class="sxs-lookup"><span data-stu-id="acf98-170">Most likely, however, you won't want to use the default ASPNETDB.mdf database for a production application.</span></span> <span data-ttu-id="acf98-171">在這種情況下,您可以通過完成以下兩個步驟來更改使用者帳戶資訊的儲存位置:</span><span class="sxs-lookup"><span data-stu-id="acf98-171">In that case, you can change where user account information is stored by completing the following two steps:</span></span>

1. <span data-ttu-id="acf98-172">將應用程式服務資料庫物件新增到生產資料庫 - 變更應用程式連接字串以指向生產資料庫</span><span class="sxs-lookup"><span data-stu-id="acf98-172">Add the Application Services database objects to your production database - Change your application connection string to point to your production database</span></span>

<span data-ttu-id="acf98-173">第一步是將所有必要的資料庫物件(表和存儲過程)添加到生產資料庫中。</span><span class="sxs-lookup"><span data-stu-id="acf98-173">The first step is to add all of the necessary database objects (tables and stored procedures) to your production database.</span></span> <span data-ttu-id="acf98-174">將這些物件添加到新資料庫的最簡單方法是利用ASP.NET SQL 伺服器設置嚮導(參見圖 8)。</span><span class="sxs-lookup"><span data-stu-id="acf98-174">The easiest way to add these objects to a new database is to take advantage of the ASP.NET SQL Server Setup Wizard (see Figure 8).</span></span> <span data-ttu-id="acf98-175">您可以透過 Microsoft Visual Studio 2008 程式組開啟 Visual Studio 2008 指令提示符並從指令提示符執行以下指令來啟動此工具:</span><span class="sxs-lookup"><span data-stu-id="acf98-175">You can launch this tool by opening the Visual Studio 2008 Command Prompt from the Microsoft Visual Studio 2008 program group and executing the following command from the command prompt:</span></span>

<span data-ttu-id="acf98-176">阿斯普內\_雷格斯</span><span class="sxs-lookup"><span data-stu-id="acf98-176">aspnet\_regsql</span></span>

<span data-ttu-id="acf98-177">**圖 8 = ASP.NET SQL 伺服器設定精靈**</span><span class="sxs-lookup"><span data-stu-id="acf98-177">**Figure 8 – The ASP.NET SQL Server Setup Wizard**</span></span>

![clip_image016](authenticating-users-with-forms-authentication-vb/_static/image8.jpg)

<span data-ttu-id="acf98-179">ASP.NET SQL 伺服器設置精靈使您能夠在網路上選擇 SQL Server 資料庫,並安裝 ASP.NET 應用程式服務所需的所有資料庫物件。</span><span class="sxs-lookup"><span data-stu-id="acf98-179">The ASP.NET SQL Server Setup Wizard enables you to select a SQL Server database on your network and install all of the database objects required by the ASP.NET application services.</span></span> <span data-ttu-id="acf98-180">資料庫伺服器不需要位於本地電腦上。</span><span class="sxs-lookup"><span data-stu-id="acf98-180">The database server is not required to be located on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="acf98-181">如果不想使用ASP.NET SQL 伺服器設定精靈,則可以在以下資料夾中找到用於添加應用程式服務資料庫物件的 SQL 文稿:</span><span class="sxs-lookup"><span data-stu-id="acf98-181">If you don't want to use the ASP.NET SQL Server Setup Wizard, then you can find SQL scripts for adding the application services database objects in the following folder:</span></span>
> 
> 
> <span data-ttu-id="acf98-182">C:[視窗]微軟.NET_框架_v2.0.50727</span><span class="sxs-lookup"><span data-stu-id="acf98-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span></span>

<span data-ttu-id="acf98-183">建立必要的資料庫物件後,需要修改 MVC 應用程式使用的資料庫連接。</span><span class="sxs-lookup"><span data-stu-id="acf98-183">After you create the necessary database objects, you need to modify the database connection used by your MVC application.</span></span> <span data-ttu-id="acf98-184">修改 Web 設定 (Web.config) 檔案中的應用程式服務連接字串,以便它指向生產資料庫。</span><span class="sxs-lookup"><span data-stu-id="acf98-184">Modify the ApplicationServices connection string in your web configuration (web.config) file so that it points to the production database.</span></span> <span data-ttu-id="acf98-185">例如,清單中修改的連接指向名為 MyProductionDB 的資料庫(原始應用程式服務連接字串已註釋掉)。</span><span class="sxs-lookup"><span data-stu-id="acf98-185">For example, the modified connection in Listing 3 points to a database named MyProductionDB (the original ApplicationServices connection string has been commented out).</span></span>

<span data-ttu-id="acf98-186">**清單3 = Web.config**</span><span class="sxs-lookup"><span data-stu-id="acf98-186">**Listing 3 – Web.config**</span></span>

[!code-xml[Main](authenticating-users-with-forms-authentication-vb/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a><span data-ttu-id="acf98-187">設定資料庫權限</span><span class="sxs-lookup"><span data-stu-id="acf98-187">Configuring Database Permissions</span></span>

<span data-ttu-id="acf98-188">如果使用整合安全連接到資料庫,則需要添加正確的 Windows 使用者帳戶作為資料庫的登錄。</span><span class="sxs-lookup"><span data-stu-id="acf98-188">If you use Integrated Security to connect to your database then you will need to add the correct Windows user account as a login to your database.</span></span> <span data-ttu-id="acf98-189">正確的帳戶取決於您是使用ASP.NET開發伺服器還是 Internet 資訊服務作為 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="acf98-189">The correct account depends on whether you are using the ASP.NET Development Server or Internet Information Services as your web server.</span></span> <span data-ttu-id="acf98-190">正確的使用者帳戶還取決於您的操作系統。</span><span class="sxs-lookup"><span data-stu-id="acf98-190">The correct user account also depends on your operating system.</span></span>

<span data-ttu-id="acf98-191">如果使用ASP.NET開發伺服器(Visual Studio 使用的預設Web伺服器),則應用程式將在Windows使用者帳戶的上下文中執行。</span><span class="sxs-lookup"><span data-stu-id="acf98-191">If you are using the ASP.NET Development Server (the default web server used by Visual Studio) then your application executes within the context of your Windows user account.</span></span> <span data-ttu-id="acf98-192">在這種情況下,您需要將 Windows 使用者帳戶添加為資料庫伺服器登錄名。</span><span class="sxs-lookup"><span data-stu-id="acf98-192">In that case, you need to add your Windows user account as a database server login.</span></span>

<span data-ttu-id="acf98-193">或者,如果您使用的是互聯網資訊服務,則需要將 ASPNET 帳戶或 NT AUTHORITY/網路服務帳戶添加為資料庫伺服器登錄名。</span><span class="sxs-lookup"><span data-stu-id="acf98-193">Alternatively, if you are using Internet Information Services then you need to add either the ASPNET account or the NT AUTHORITY/NETWORK SERVICE account as a database server login.</span></span> <span data-ttu-id="acf98-194">如果使用 Windows XP,則添加 ASPNET 帳戶作為資料庫的登錄名。</span><span class="sxs-lookup"><span data-stu-id="acf98-194">If you are using Windows XP then add the ASPNET account as a login to your database.</span></span> <span data-ttu-id="acf98-195">如果您使用的是較新的作業系統,如 Windows Vista 或 Windows Server 2008,則添加 NT AUTHORITY/網路服務帳戶作為資料庫登錄。</span><span class="sxs-lookup"><span data-stu-id="acf98-195">If you are using a more recent operating system, such as Windows Vista or Windows Server 2008, then add the NT AUTHORITY/NETWORK SERVICE account as the database login.</span></span>

<span data-ttu-id="acf98-196">您可以使用 Microsoft SQL 伺服器管理工作室向資料庫添加新使用者帳戶(參見圖 9)。</span><span class="sxs-lookup"><span data-stu-id="acf98-196">You can add a new user account to your database by using Microsoft SQL Server Management Studio (see Figure 9).</span></span>

<span data-ttu-id="acf98-197">**圖 9 = 建立新的 Microsoft SQL Server 登入名稱**</span><span class="sxs-lookup"><span data-stu-id="acf98-197">**Figure 9 – Creating a new Microsoft SQL Server login**</span></span>

![clip_image018](authenticating-users-with-forms-authentication-vb/_static/image9.jpg)

<span data-ttu-id="acf98-199">建立所需的登錄後,需要將登錄映射到具有正確資料庫角色的資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="acf98-199">After you create the required login, you need to map the login to a database user with the right database roles.</span></span> <span data-ttu-id="acf98-200">按兩下登入名並選擇「使用者映射」選項卡。選擇一個或多個應用程式服務資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="acf98-200">Double-click the login and select the User Mapping tab. Select one or more application services database roles.</span></span> <span data-ttu-id="acf98-201">例如,為了對使用者進行身份驗證,您需要啟用 aspnet\_\_成員資格 基本訪問資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="acf98-201">For example, in order to authenticate users, you need to enable the aspnet\_Membership\_BasicAccess database role.</span></span> <span data-ttu-id="acf98-202">要建立新使用者,您需要啟用 aspnet\_\_成員資格 完全訪問資料庫角色(參見圖 10)。</span><span class="sxs-lookup"><span data-stu-id="acf98-202">In order to create new users, you need to enable the aspnet\_Membership\_FullAccess database role (see Figure 10).</span></span>

<span data-ttu-id="acf98-203">**圖 10 = 新增應用程式服務資料庫角色**</span><span class="sxs-lookup"><span data-stu-id="acf98-203">**Figure 10 – Adding Application Services database roles**</span></span>

![clip_image020](authenticating-users-with-forms-authentication-vb/_static/image10.jpg)

#### <a name="summary"></a><span data-ttu-id="acf98-205">總結</span><span class="sxs-lookup"><span data-stu-id="acf98-205">Summary</span></span>

<span data-ttu-id="acf98-206">在本教學中,您學習了在構建 ASP.NET MVC 應用程式時如何使用窗體身份驗證。</span><span class="sxs-lookup"><span data-stu-id="acf98-206">In this tutorial, you learned how to use Forms authentication when building an ASP.NET MVC application.</span></span> <span data-ttu-id="acf98-207">首先,您學習了如何通過利用網站管理工具創建新使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="acf98-207">First, you learned how to create new users and roles by taking advantage of the Web Site Administration Tool.</span></span> <span data-ttu-id="acf98-208">接下來,您學習了如何使用 [授權] 屬性來防止未經授權的使用者調用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="acf98-208">Next, you learned how to use the [Authorize] attribute to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="acf98-209">最後,您學習了如何配置 MVC 應用程式以在生產資料庫中儲存使用者和角色資訊。</span><span class="sxs-lookup"><span data-stu-id="acf98-209">Finally, you learned how to configure your MVC application to store user and role information in a production database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="acf98-210">[前一個](preventing-javascript-injection-attacks-cs.md)
> [下一個](authenticating-users-with-windows-authentication-vb.md)</span><span class="sxs-lookup"><span data-stu-id="acf98-210">[Previous](preventing-javascript-injection-attacks-cs.md)
[Next](authenticating-users-with-windows-authentication-vb.md)</span></span>
