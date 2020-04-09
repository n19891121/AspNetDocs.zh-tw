---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 使用視覺化工作室ASP.NET Web 部署:Web.config 檔案轉換 |微軟文件
author: tdykstra
description: 本教學系列介紹如何將ASP.NET Web 應用程式部署到 Azure 應用服務 Web 應用或第三方託管供應商(由 usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676122"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a><span data-ttu-id="95f21-103">使用視覺化工作室ASP.NET Web 部署:Web.config 檔案轉換</span><span class="sxs-lookup"><span data-stu-id="95f21-103">ASP.NET Web Deployment using Visual Studio: Web.config File Transformations</span></span>

<span data-ttu-id="95f21-104">湯姆[·戴克斯特拉](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="95f21-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="95f21-105">下載初學者專案</span><span class="sxs-lookup"><span data-stu-id="95f21-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="95f21-106">本教學系列介紹如何使用 Visual Studio 2012 或 Visual Studio 2010 將ASP.NET Web 應用程式部署到 Azure 應用服務 Web 應用或第三方託管供應商。</span><span class="sxs-lookup"><span data-stu-id="95f21-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="95f21-107">有關該系列的資訊,請參閱[系列中的第一個教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="95f21-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="95f21-108">概觀</span><span class="sxs-lookup"><span data-stu-id="95f21-108">Overview</span></span>

<span data-ttu-id="95f21-109">本教學介紹如何在將*Web.config 檔部署到*不同目標環境時自動執行更改 Web.config 檔的過程。</span><span class="sxs-lookup"><span data-stu-id="95f21-109">This tutorial shows you how to automate the process of changing the *Web.config* file when you deploy it to different destination environments.</span></span> <span data-ttu-id="95f21-110">大多數應用程式在*Web.config 檔中*具有設置,在部署應用程式時必須不同。</span><span class="sxs-lookup"><span data-stu-id="95f21-110">Most applications have settings in the *Web.config* file that must be different when the application is deployed.</span></span> <span data-ttu-id="95f21-111">自動進行這些更改的過程使每次部署時都不必手動執行這些更改,這非常繁瑣且容易出錯。</span><span class="sxs-lookup"><span data-stu-id="95f21-111">Automating the process of making these changes keeps you from having to do them manually every time you deploy, which would be tedious and error prone.</span></span>

<span data-ttu-id="95f21-112">鬧鐘:如果您收到錯誤訊息或內容在瀏覽此教學時不起作用,請務必檢視[故障排除頁面](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="95f21-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a><span data-ttu-id="95f21-113">Web.設定轉換與 Web 部署參數</span><span class="sxs-lookup"><span data-stu-id="95f21-113">Web.config transformations versus Web Deploy parameters</span></span>

<span data-ttu-id="95f21-114">有兩種方法可以自動變更*Web.config*檔設定的過程[:Web.config 轉換](https://msdn.microsoft.com/library/dd465326.aspx)與[Web 部署參數](https://msdn.microsoft.com/library/ff398068.aspx)。</span><span class="sxs-lookup"><span data-stu-id="95f21-114">There are two ways to automate the process of changing *Web.config* file settings: [Web.config transformations](https://msdn.microsoft.com/library/dd465326.aspx) and [Web Deploy parameters](https://msdn.microsoft.com/library/ff398068.aspx).</span></span> <span data-ttu-id="95f21-115">*Web.config*轉換檔包含 XML 標籤,用於指定在部署*Web.config*檔時如何更改該檔。</span><span class="sxs-lookup"><span data-stu-id="95f21-115">A *Web.config* transformation file contains XML markup that specifies how to change the *Web.config* file when it is deployed.</span></span> <span data-ttu-id="95f21-116">您可以為特定生成配置和特定發佈設定檔指定不同的更改。</span><span class="sxs-lookup"><span data-stu-id="95f21-116">You can specify different changes for specific build configurations and for specific publish profiles.</span></span> <span data-ttu-id="95f21-117">預設產生設定是除錯和發表,您可以創建自定義生成配置。</span><span class="sxs-lookup"><span data-stu-id="95f21-117">The default build configurations are Debug and Release, and you can create custom build configurations.</span></span> <span data-ttu-id="95f21-118">發佈配置檔通常對應於目標環境。</span><span class="sxs-lookup"><span data-stu-id="95f21-118">A publish profile typically corresponds to a destination environment.</span></span> <span data-ttu-id="95f21-119">(您將瞭解有關在["作為測試環境"教程部署到 IIS](deploying-to-iis.md)中的發表配置檔的更多資訊。</span><span class="sxs-lookup"><span data-stu-id="95f21-119">(You'll learn more about publish profiles in the [Deploying to IIS as a Test Environment](deploying-to-iis.md) tutorial.)</span></span>

<span data-ttu-id="95f21-120">Web Deploy 參數可用於指定在部署期間必須配置的許多不同類型的設置,包括*Web.config 檔中*的設置。</span><span class="sxs-lookup"><span data-stu-id="95f21-120">Web Deploy parameters can be used to specify many different kinds of settings that must be configured during deployment, including settings that are found in *Web.config* files.</span></span> <span data-ttu-id="95f21-121">當用於指定*Web.config*檔更改時,Web Deploy 參數的設置更為複雜,但在部署之前不知道要設置的值時,這些參數很有用。</span><span class="sxs-lookup"><span data-stu-id="95f21-121">When used to specify *Web.config* file changes, Web Deploy parameters are more complex to set up, but they are useful when you do not know the value to be set until you deploy.</span></span> <span data-ttu-id="95f21-122">例如,在企業環境中,您可以創建*部署包*並將其交給 IT 部門的人員以在生產中安裝,並且此人必須能夠輸入您不知道的連接字串或密碼。</span><span class="sxs-lookup"><span data-stu-id="95f21-122">For example, in an enterprise environment, you might create a *deployment package* and give it to a person in the IT department to install in production, and that person has to be able to enter connection strings or passwords that you do not know.</span></span>

<span data-ttu-id="95f21-123">對於本教學系列介紹的方案,您事先知道必須對*Web.config*檔執行的所有操作,因此無需使用 Web Deploy 參數。</span><span class="sxs-lookup"><span data-stu-id="95f21-123">For the scenario that this tutorial series covers, you know in advance everything that has to be done to the *Web.config* file, so you do not need to use Web Deploy parameters.</span></span> <span data-ttu-id="95f21-124">您將設定一些因所使用的生成配置而異的轉換,以及一些因使用的發佈配置檔而異的轉換。</span><span class="sxs-lookup"><span data-stu-id="95f21-124">You'll configure some transformations that differ depending on the build configuration used, and some that differ depending on the publish profile used.</span></span>

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a><span data-ttu-id="95f21-125">在 Azure 中指定 Web.設定設定</span><span class="sxs-lookup"><span data-stu-id="95f21-125">Specifying Web.config settings in Azure</span></span>

<span data-ttu-id="95f21-126">如果要更改的*Web.config*檔`<connectionStrings>`設定`<appSettings>`位於 或 元素中,並且如果要在 Azure 應用服務中部署到 Web 應用,則可以在部署期間自動更改另一個選項。</span><span class="sxs-lookup"><span data-stu-id="95f21-126">If the *Web.config* file settings that you want to change are in the `<connectionStrings>` or the `<appSettings>` element, and if you are deploying to Web Apps in Azure App Service, you have another option for automating changes during deployment.</span></span> <span data-ttu-id="95f21-127">您可以在 Web 應用程式的管理門戶頁的 **「設定」** 選項卡中輸入要在 Azure 中生效的設定(向下滾動到**應用設定**和**連接字串**部分)。</span><span class="sxs-lookup"><span data-stu-id="95f21-127">You can enter the settings that you want to take effect in Azure in the **Configure** tab of the management portal page for your web app (scroll down to the **app settings** and **connection strings** sections).</span></span> <span data-ttu-id="95f21-128">部署專案時,Azure 會自動應用更改。</span><span class="sxs-lookup"><span data-stu-id="95f21-128">When you deploy the project, Azure automatically applies the changes.</span></span> <span data-ttu-id="95f21-129">有關詳細資訊,請參閱[Windows Azure 網站:應用程式字串和連接字串的工作原理](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)。</span><span class="sxs-lookup"><span data-stu-id="95f21-129">For more information, see [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).</span></span>

## <a name="default-transformation-files"></a><span data-ttu-id="95f21-130">預設轉換檔案</span><span class="sxs-lookup"><span data-stu-id="95f21-130">Default transformation files</span></span>

<span data-ttu-id="95f21-131">在**解決方案資源管理員**中,展開*Web.config*以檢視*Web.Debug.config*和*Web.Release.config*為兩個預設生成設定預設創建的轉換檔。</span><span class="sxs-lookup"><span data-stu-id="95f21-131">In **Solution Explorer**, expand *Web.config* to see the *Web.Debug.config* and *Web.Release.config* transformation files that are created by default for the two default build configurations.</span></span>

![Web.config_transform_files](web-config-transformations/_static/image1.png)

<span data-ttu-id="95f21-133">您可以通過右鍵單擊 Web.config 檔並從上下文選單中選擇 **「添加設定轉換」** 來建立自定義生成配置的轉換檔。</span><span class="sxs-lookup"><span data-stu-id="95f21-133">You can create transformation files for custom build configurations by right-clicking the Web.config file and choosing **Add Config Transforms** from the context menu.</span></span> <span data-ttu-id="95f21-134">對於本教程,您不需要執行此操作,並且功能表選項已禁用,因為您尚未創建任何自定義生成配置。</span><span class="sxs-lookup"><span data-stu-id="95f21-134">For this tutorial you don't need to do that, and the menu option is disabled, because you haven't created any custom build configurations.</span></span>

<span data-ttu-id="95f21-135">稍後,您將再創建三個轉換檔,每個檔用於測試、暫存和生產發佈配置檔。</span><span class="sxs-lookup"><span data-stu-id="95f21-135">Later you'll create three more transformation files, one each for the test, staging, and production publish profiles.</span></span> <span data-ttu-id="95f21-136">在發佈配置檔轉換檔中處理的設置的典型示例是 WCF 終結點,用於測試和生產。</span><span class="sxs-lookup"><span data-stu-id="95f21-136">A typical example of a setting that you would handle in a publish profile transformation file because it depends on the destination environment is a WCF endpoint that is different for test versus production.</span></span> <span data-ttu-id="95f21-137">在建立與它們一起的發佈設定檔後,您將在以後的教程中創建發佈設定檔轉換檔。</span><span class="sxs-lookup"><span data-stu-id="95f21-137">You'll create publish profile transformation files in later tutorials after you create the publish profiles that they go with.</span></span>

## <a name="disable-debug-mode"></a><span data-ttu-id="95f21-138">關閉除錯模式</span><span class="sxs-lookup"><span data-stu-id="95f21-138">Disable debug mode</span></span>

<span data-ttu-id="95f21-139">屬性是相依於產生設定而非目標環境的設定範`debug`例 。</span><span class="sxs-lookup"><span data-stu-id="95f21-139">An example of a setting that depends on build configuration rather than destination environment is the `debug` attribute.</span></span> <span data-ttu-id="95f21-140">對於發佈生成,您通常希望禁用調試,而不管要部署到哪個環境。</span><span class="sxs-lookup"><span data-stu-id="95f21-140">For a Release build, you typically want debugging disabled regardless of which environment you are deploying to.</span></span> <span data-ttu-id="95f21-141">因此,預設情況下,Visual Studio 專案範本創建*Web.Release.config*轉換`debug`檔,這些轉換`compilation`檔案的代碼從 元素中刪除該屬性。</span><span class="sxs-lookup"><span data-stu-id="95f21-141">Therefore, by default the Visual Studio project templates create *Web.Release.config* transform files with code that removes the `debug` attribute from the `compilation` element.</span></span> <span data-ttu-id="95f21-142">下面是預設的*Web.Release.config*:除了註釋掉的一些範例轉換程式碼外`compilation`,它還在元素`debug`中包括刪除 屬性的代碼:</span><span class="sxs-lookup"><span data-stu-id="95f21-142">Here is the default *Web.Release.config*: in addition to some sample transformation code that is commented out, it includes code in the `compilation` element that removes the `debug` attribute:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

<span data-ttu-id="95f21-143">該`xdt:Transform="RemoveAttributes(debug)"`屬性指定您希望從已`debug`部署`system.web/compilation`的*Web.config*檔中的元素中刪除該屬性。</span><span class="sxs-lookup"><span data-stu-id="95f21-143">The `xdt:Transform="RemoveAttributes(debug)"` attribute specifies that you want the `debug` attribute to be removed from the `system.web/compilation` element in the deployed *Web.config* file.</span></span> <span data-ttu-id="95f21-144">這將在每次部署發佈版本時完成。</span><span class="sxs-lookup"><span data-stu-id="95f21-144">This will be done every time you deploy a Release build.</span></span>

## <a name="limit-error-log-access-to-administrators"></a><span data-ttu-id="95f21-145">限制管理者的錯誤紀錄</span><span class="sxs-lookup"><span data-stu-id="95f21-145">Limit error log access to administrators</span></span>

<span data-ttu-id="95f21-146">如果應用程式執行時發生錯誤,應用程式將顯示一個通用錯誤頁,以代替系統生成的錯誤頁,並且它使用[Elmah NuGet 套件](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)進行錯誤日誌記錄和報告。</span><span class="sxs-lookup"><span data-stu-id="95f21-146">If there's an error while the application runs, the application displays a generic error page in place of the system-generated error page, and it uses the [Elmah NuGet package](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) for error logging and reporting.</span></span> <span data-ttu-id="95f21-147">應用程式`customErrors` *Web.config*檔案中的元素指定錯誤頁:</span><span class="sxs-lookup"><span data-stu-id="95f21-147">The `customErrors` element in the application *Web.config* file specifies the error page:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

<span data-ttu-id="95f21-148">要查看錯誤頁,請暫時將`mode``customErrors`元素的屬性從"僅遠端"更改為"打開",並從 Visual Studio 運行應用程式。</span><span class="sxs-lookup"><span data-stu-id="95f21-148">To see the error page, temporarily change the `mode` attribute of the `customErrors` element from "RemoteOnly" to "On" and run the application from Visual Studio.</span></span> <span data-ttu-id="95f21-149">通過請求無效 URL(如*學生xxx.aspx)* 導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="95f21-149">Cause an error by requesting an invalid URL, such as *Studentsxxx.aspx*.</span></span> <span data-ttu-id="95f21-150">您看到的不是 IIS 生成的"找不到資源"錯誤頁,而是看到*泛錯誤Page.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="95f21-150">Instead of an IIS-generated "The resource cannot be found" error page, you see the *GenericErrorPage.aspx* page.</span></span>

![錯誤頁](web-config-transformations/_static/image2.png)

<span data-ttu-id="95f21-152">要檢視錯誤紀錄,請將連接埠號後網址中的所有內容取代為*elmah.axd(* 例如`http://localhost:51130/elmah.axd`),然後按 Enter:</span><span class="sxs-lookup"><span data-stu-id="95f21-152">To see the error log, replace everything in the URL after the port number with *elmah.axd* (for example, `http://localhost:51130/elmah.axd`) and press Enter:</span></span>

![ELMAH 頁面](web-config-transformations/_static/image3.png)

<span data-ttu-id="95f21-154">完成後,不要忘記將`customErrors`元素設置為"僅遠端"模式。</span><span class="sxs-lookup"><span data-stu-id="95f21-154">Don't forget to set the `customErrors` element back to "RemoteOnly" mode when you're done.</span></span>

<span data-ttu-id="95f21-155">在開發電腦上,允許免費訪問錯誤日誌頁很方便,但在生產中,這將存在安全風險。</span><span class="sxs-lookup"><span data-stu-id="95f21-155">On your development computer it's convenient to allow free access to the error log page, but in production that would be a security risk.</span></span> <span data-ttu-id="95f21-156">對於生產網站,要添加一個授權規則,該規則限制管理員對錯誤日誌的訪問,並確保該限制在測試和暫存中也正常工作。</span><span class="sxs-lookup"><span data-stu-id="95f21-156">For the production site, you want to add an authorization rule that restricts error log access to administrators, and to make sure that the restriction works you want it in test and staging also.</span></span> <span data-ttu-id="95f21-157">因此,這是每次部署發佈生成時要實現的另一個更改,因此它屬於*Web.Release.config*檔。</span><span class="sxs-lookup"><span data-stu-id="95f21-157">Therefore this is another change that you want to implement every time you deploy a Release build, and so it belongs in the *Web.Release.config* file.</span></span>

<span data-ttu-id="95f21-158">打開*Web.Release.config,*`location``configuration`並在結束 標記之前添加新元素,如下所示。</span><span class="sxs-lookup"><span data-stu-id="95f21-158">Open *Web.Release.config* and add a new `location` element immediately before the closing `configuration` tag, as shown here.</span></span>

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

<span data-ttu-id="95f21-159">屬性`Transform`值"Insert"會導致此`location`元素作為同級添加到*Web.config*`location`檔中的任何 現有元素。</span><span class="sxs-lookup"><span data-stu-id="95f21-159">The `Transform` attribute value of "Insert" causes this `location` element to be added as a sibling to any existing `location` elements in the *Web.config* file.</span></span> <span data-ttu-id="95f21-160">(已經有一個`location`元素指定**更新積分**頁的授權規則。</span><span class="sxs-lookup"><span data-stu-id="95f21-160">(There is already one `location` element that specifies authorization rules for the **Update Credits** page.)</span></span>

<span data-ttu-id="95f21-161">現在,您可以預覽轉換,以確保正確編碼它。</span><span class="sxs-lookup"><span data-stu-id="95f21-161">Now you can preview the transform to make sure that you coded it correctly.</span></span>

<span data-ttu-id="95f21-162">在**解決方案資源管理器**中,右鍵單擊*Web.Release.config,* 然後單擊 **「預覽轉換**」。</span><span class="sxs-lookup"><span data-stu-id="95f21-162">In **Solution Explorer**, right-click *Web.Release.config* and click **Preview Transform**.</span></span>

![預覽轉換選單](web-config-transformations/_static/image4.png)

<span data-ttu-id="95f21-164">將打開一個頁面,顯示左側的開發*Web.config*檔以及部署的*Web.config*檔在右側的外觀,並突出顯示更改。</span><span class="sxs-lookup"><span data-stu-id="95f21-164">A page opens that shows you the development *Web.config* file on the left and what the deployed *Web.config* file will look like on the right, with changes highlighted.</span></span>

![除錯轉換預覽](web-config-transformations/_static/image5.png)

![位置轉換預覽](web-config-transformations/_static/image6.png)

<span data-ttu-id="95f21-167">(在預覽中,您可能會注意到一些未為這些更改編寫轉換的其他更改:這些更改通常涉及刪除不影響功能的空白。</span><span class="sxs-lookup"><span data-stu-id="95f21-167">( In the preview, you might notice some additional changes that you didn't write transforms for: these typically involve the removal of white space that doesn't affect functionality.)</span></span>

<span data-ttu-id="95f21-168">部署後測試網站時,還將進行測試以驗證授權規則是否有效。</span><span class="sxs-lookup"><span data-stu-id="95f21-168">When you test the site after deployment, you'll also test to verify that the authorization rule is effective.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="95f21-169">**安全說明**切勿在生產應用程式中向公眾顯示錯誤詳細資訊,也不要將該資訊存儲在公共位置。</span><span class="sxs-lookup"><span data-stu-id="95f21-169">**Security Note** Never display error details to the public in a production application, or store that information in a public location.</span></span> <span data-ttu-id="95f21-170">攻擊者可以使用錯誤資訊來發現網站中的漏洞。</span><span class="sxs-lookup"><span data-stu-id="95f21-170">Attackers can use error information to discover vulnerabilities in a site.</span></span> <span data-ttu-id="95f21-171">如果您在自己的應用程式中使用 ELMAH,請配置 ELMAH 以最大程度地降低安全風險。</span><span class="sxs-lookup"><span data-stu-id="95f21-171">If you use ELMAH in your own application, configure ELMAH to minimize security risks.</span></span> <span data-ttu-id="95f21-172">本教程中的 ELMAH 示例不應視為推薦的配置。</span><span class="sxs-lookup"><span data-stu-id="95f21-172">The ELMAH example in this tutorial should not be considered a recommended configuration.</span></span> <span data-ttu-id="95f21-173">這是一個範例,用於說明如何處理應用程式必須能夠在中創建文件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="95f21-173">It is an example that was chosen in order to illustrate how to handle a folder that the application must be able to create files in.</span></span> <span data-ttu-id="95f21-174">有關詳細資訊,請參閱保護[ELMAH 終結點](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)。</span><span class="sxs-lookup"><span data-stu-id="95f21-174">For more information, see [securing the ELMAH endpoint](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages).</span></span>

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a><span data-ttu-id="95f21-175">在設定檔轉換檔案中要處理的設定</span><span class="sxs-lookup"><span data-stu-id="95f21-175">A setting that you'll handle in publish profile transformation files</span></span>

<span data-ttu-id="95f21-176">常見方案是具有在部署到的每個環境中必須不同的*Web.config*檔設置。</span><span class="sxs-lookup"><span data-stu-id="95f21-176">A common scenario is to have *Web.config* file settings that must be different in each environment that you deploy to.</span></span> <span data-ttu-id="95f21-177">例如,調用 WCF 服務的應用程式在測試和生產環境中可能需要不同的終結點。</span><span class="sxs-lookup"><span data-stu-id="95f21-177">For example, an application that calls a WCF service might need a different endpoint in test and production environments.</span></span> <span data-ttu-id="95f21-178">康托索大學的申請還包括這種設置。</span><span class="sxs-lookup"><span data-stu-id="95f21-178">The Contoso University application includes a setting of this kind also.</span></span> <span data-ttu-id="95f21-179">此設定控制網站頁面上的可見指示器,該指示器告訴您處於哪個環境,例如開發、測試或生產。</span><span class="sxs-lookup"><span data-stu-id="95f21-179">This setting controls a visible indicator on a site's pages that tells you which environment you are in, such as development, test, or production.</span></span> <span data-ttu-id="95f21-180">設定值確定應用程式是否會將「(Dev)」或「(測試)」追加到*Site.master*頁中的主標題:</span><span class="sxs-lookup"><span data-stu-id="95f21-180">The setting value determines whether the application will append "(Dev)" or "(Test)" to the main heading in the *Site.Master* master page:</span></span>

![環境指示器](web-config-transformations/_static/image7.png)

<span data-ttu-id="95f21-182">當應用程式在暫存或生產中運行時,環境指示器將被省略。</span><span class="sxs-lookup"><span data-stu-id="95f21-182">The environment indicator is omitted when the application is running in staging or production.</span></span>

<span data-ttu-id="95f21-183">Contoso 大學網頁讀取在*Web.config*`appSettings`檔中設定的值,以便確定應用程式在以下環境執行的環境:</span><span class="sxs-lookup"><span data-stu-id="95f21-183">The Contoso University web pages read a value that is set in `appSettings` in the *Web.config* file in order to determine what environment the application is running in:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

<span data-ttu-id="95f21-184">在測試環境中的值應為"測試",對於暫存和生產來說應為"Prod"。</span><span class="sxs-lookup"><span data-stu-id="95f21-184">The value should be "Test" in the test environment, and "Prod" for staging and production.</span></span>

<span data-ttu-id="95f21-185">轉換檔案中的以下代碼將實現此轉換:</span><span class="sxs-lookup"><span data-stu-id="95f21-185">The following code in a transform file will implement this transformation:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

<span data-ttu-id="95f21-186">`xdt:Transform`屬性值「SetAttributes」表示此轉換的目的是更改*Web.config*檔中現有元素的屬性值。</span><span class="sxs-lookup"><span data-stu-id="95f21-186">The `xdt:Transform` attribute value "SetAttributes" indicates that the purpose of this transform is to change attribute values of an existing element in the *Web.config* file.</span></span> <span data-ttu-id="95f21-187">`xdt:Locator`屬性值"Match(鍵)"表示要修改的元素是其`key`屬性與此處指定`key`的 屬性匹配的元素。</span><span class="sxs-lookup"><span data-stu-id="95f21-187">The `xdt:Locator` attribute value "Match(key)" indicates that the element to be modified is the one whose `key` attribute matches the `key` attribute specified here.</span></span> <span data-ttu-id="95f21-188">元素的唯一`add`其他屬性`value`是 ,這就是將在部署的*Web.config 檔中*更改的內容。</span><span class="sxs-lookup"><span data-stu-id="95f21-188">The only other attribute of the `add` element is `value`, and that is what will be changed in the deployed *Web.config* file.</span></span> <span data-ttu-id="95f21-189">`value`此處顯示的代碼會導致`Environment``appSettings`元素的屬性設置為部署的*Web.config*檔中的"Test"。</span><span class="sxs-lookup"><span data-stu-id="95f21-189">The code shown here causes the `value` attribute of the `Environment` `appSettings` element to be set to "Test" in the *Web.config* file that is deployed.</span></span>

<span data-ttu-id="95f21-190">此轉換屬於尚未建立的發佈設定檔轉換檔。</span><span class="sxs-lookup"><span data-stu-id="95f21-190">This transform belongs in the publish profile transform files, which you haven't created yet.</span></span> <span data-ttu-id="95f21-191">在為測試、暫存和生產環境創建發佈設定檔時,您將創建和更新實現此更改的轉換檔。</span><span class="sxs-lookup"><span data-stu-id="95f21-191">You'll create and update the transform files that implement this change when you create the publish profiles for the test, staging, and production environments.</span></span> <span data-ttu-id="95f21-192">您將在[部署到 IIS](deploying-to-iis.md)並[部署到生產](deploying-to-production.md)教程中執行此操作。</span><span class="sxs-lookup"><span data-stu-id="95f21-192">You'll do that in the [deploy to IIS](deploying-to-iis.md) and [deploy to production](deploying-to-production.md) tutorials.</span></span>

> [!NOTE]
> <span data-ttu-id="95f21-193">由於此設定位於`<appSettings>`元素中,因此在本主題前面介紹的 Azure 中,在 Azure 應用服務中部署到 Web 應用時,還有另一種用於指定轉換的替代方法。請參閱[在本主題前面指定 Azure 中的 Web.config 設定](#watransforms)。</span><span class="sxs-lookup"><span data-stu-id="95f21-193">Because this setting is in the `<appSettings>` element, you have another alternative for specifying the transformation when you're deploying to Web Apps in Azure App Service See [Specifying Web.config settings in Azure](#watransforms) earlier in this topic.</span></span>

## <a name="setting-connection-strings"></a><span data-ttu-id="95f21-194">設定連接字串</span><span class="sxs-lookup"><span data-stu-id="95f21-194">Setting connection strings</span></span>

<span data-ttu-id="95f21-195">儘管預設轉換檔包含一個範例,其中展示如何更新連接字串,但在大多數情況下,您不需要設定連接字串轉換,因為您可以在發佈設定檔中指定連接字串。</span><span class="sxs-lookup"><span data-stu-id="95f21-195">Although the default transform file contains an example that shows how to update a connection string, in most cases you do not need to set up connection string transformations, because you can specify connection strings in the publish profile.</span></span> <span data-ttu-id="95f21-196">您將在[部署到 IIS](deploying-to-iis.md)並[部署到生產](deploying-to-production.md)教程中執行此操作。</span><span class="sxs-lookup"><span data-stu-id="95f21-196">You'll do that in the [deploy to IIS](deploying-to-iis.md) and [deploy to production](deploying-to-production.md) tutorials.</span></span>

## <a name="summary"></a><span data-ttu-id="95f21-197">總結</span><span class="sxs-lookup"><span data-stu-id="95f21-197">Summary</span></span>

<span data-ttu-id="95f21-198">現在,在創建發佈設定檔之前,您已經盡可能多地使用*Web.config*轉換,並且您已經看到了部署的 Web.config 檔中的內容的預覽。</span><span class="sxs-lookup"><span data-stu-id="95f21-198">You have now done as much as you can with *Web.config* transformations before you create the publish profiles, and you've seen a preview of what will be in the deployed Web.config file.</span></span>

![位置轉換預覽](web-config-transformations/_static/image8.png)

<span data-ttu-id="95f21-200">在下面的教學中,您將處理需要設置專案屬性的部署設置任務。</span><span class="sxs-lookup"><span data-stu-id="95f21-200">In the following tutorial, you'll take care of deployment set-up tasks that require setting project properties.</span></span>

## <a name="more-information"></a><span data-ttu-id="95f21-201">相關資訊</span><span class="sxs-lookup"><span data-stu-id="95f21-201">More Information</span></span>

<span data-ttu-id="95f21-202">關於這個教學涵蓋的主題的詳細資訊,請參閱在 Visual Studio 和 ASP.NET 的 Web 部署內容映射中[使用 Web.config 轉換來更改目標 Web.config 檔或 app.config 檔中的設定](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms)。</span><span class="sxs-lookup"><span data-stu-id="95f21-202">For more information about topics covered by this tutorial, see [Using Web.config transformations to change settings in the destination Web.config file or app.config file during deployment](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) in the Web Deployment Content Map for Visual Studio and ASP.NET.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="95f21-203">[前一個](preparing-databases.md)
> [下一個](project-properties.md)</span><span class="sxs-lookup"><span data-stu-id="95f21-203">[Previous](preparing-databases.md)
[Next](project-properties.md)</span></span>
