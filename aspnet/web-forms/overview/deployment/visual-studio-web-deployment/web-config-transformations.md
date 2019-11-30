---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 使用 Visual Studio： web.config 檔案轉換來 ASP.NET Web 部署 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621781"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a><span data-ttu-id="dbc76-103">使用 Visual Studio： web.config 檔案轉換來 ASP.NET Web 部署</span><span class="sxs-lookup"><span data-stu-id="dbc76-103">ASP.NET Web Deployment using Visual Studio: Web.config File Transformations</span></span>

<span data-ttu-id="dbc76-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="dbc76-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="dbc76-105">下載入門專案</span><span class="sxs-lookup"><span data-stu-id="dbc76-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="dbc76-106">本教學課程系列說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商裝載提供者。</span><span class="sxs-lookup"><span data-stu-id="dbc76-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="dbc76-107">如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。</span><span class="sxs-lookup"><span data-stu-id="dbc76-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="dbc76-108">概觀</span><span class="sxs-lookup"><span data-stu-id="dbc76-108">Overview</span></span>

<span data-ttu-id="dbc76-109">本教學課程會示範如何在您*將 web.config 檔案*部署到不同的目的地環境時，自動化該檔案的變更程式。</span><span class="sxs-lookup"><span data-stu-id="dbc76-109">This tutorial shows you how to automate the process of changing the *Web.config* file when you deploy it to different destination environments.</span></span> <span data-ttu-id="dbc76-110">大部分的應用程式都有*web.config*檔案中的設定，在部署應用程式時必須不同。</span><span class="sxs-lookup"><span data-stu-id="dbc76-110">Most applications have settings in the *Web.config* file that must be different when the application is deployed.</span></span> <span data-ttu-id="dbc76-111">將進行這些變更的程式自動化，讓您不必在每次部署時都必須手動執行，這會很繁瑣且容易出錯。</span><span class="sxs-lookup"><span data-stu-id="dbc76-111">Automating the process of making these changes keeps you from having to do them manually every time you deploy, which would be tedious and error prone.</span></span>

<span data-ttu-id="dbc76-112">提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="dbc76-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a><span data-ttu-id="dbc76-113">Web.config 轉換與 Web Deploy 參數的比較</span><span class="sxs-lookup"><span data-stu-id="dbc76-113">Web.config transformations versus Web Deploy parameters</span></span>

<span data-ttu-id="dbc76-114">有兩種方式可將變更*web.config*檔案設定的程式自動化： [web.config 轉換](https://msdn.microsoft.com/library/dd465326.aspx)和[Web Deploy 參數](https://msdn.microsoft.com/library/ff398068.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dbc76-114">There are two ways to automate the process of changing *Web.config* file settings: [Web.config transformations](https://msdn.microsoft.com/library/dd465326.aspx) and [Web Deploy parameters](https://msdn.microsoft.com/library/ff398068.aspx).</span></span> <span data-ttu-id="dbc76-115">Web.config*轉換檔案*包含 XML 標記，可指定在部署 web.config 檔案時，如何*變更 web.config 檔案*。</span><span class="sxs-lookup"><span data-stu-id="dbc76-115">A *Web.config* transformation file contains XML markup that specifies how to change the *Web.config* file when it is deployed.</span></span> <span data-ttu-id="dbc76-116">您可以針對特定的組建設定和特定的發行設定檔，指定不同的變更。</span><span class="sxs-lookup"><span data-stu-id="dbc76-116">You can specify different changes for specific build configurations and for specific publish profiles.</span></span> <span data-ttu-id="dbc76-117">預設組建設定為 [Debug] 和 [Release]，而您可以建立自訂群組建設定。</span><span class="sxs-lookup"><span data-stu-id="dbc76-117">The default build configurations are Debug and Release, and you can create custom build configurations.</span></span> <span data-ttu-id="dbc76-118">發行設定檔通常會對應至目的地環境。</span><span class="sxs-lookup"><span data-stu-id="dbc76-118">A publish profile typically corresponds to a destination environment.</span></span> <span data-ttu-id="dbc76-119">（您將在[部署至 IIS 作為測試環境](deploying-to-iis.md)教學課程中深入瞭解發行設定檔）。</span><span class="sxs-lookup"><span data-stu-id="dbc76-119">(You'll learn more about publish profiles in the [Deploying to IIS as a Test Environment](deploying-to-iis.md) tutorial.)</span></span>

<span data-ttu-id="dbc76-120">Web Deploy 參數可以用來指定在部署期間必須設定的許多不同類型的設定，*包括在 web.config*檔案中找到的設定。</span><span class="sxs-lookup"><span data-stu-id="dbc76-120">Web Deploy parameters can be used to specify many different kinds of settings that must be configured during deployment, including settings that are found in *Web.config* files.</span></span> <span data-ttu-id="dbc76-121">當用來指定*web.config*檔案變更時，Web Deploy 參數會更複雜，但當您在部署之前不知道要設定的值時，它們會很有用。</span><span class="sxs-lookup"><span data-stu-id="dbc76-121">When used to specify *Web.config* file changes, Web Deploy parameters are more complex to set up, but they are useful when you do not know the value to be set until you deploy.</span></span> <span data-ttu-id="dbc76-122">例如，在企業環境中，您可能會建立*部署套件*，並將其提供給 it 部門中的人員，以在實際執行環境中安裝，而且該人員必須能夠輸入不知道的連接字串或密碼。</span><span class="sxs-lookup"><span data-stu-id="dbc76-122">For example, in an enterprise environment, you might create a *deployment package* and give it to a person in the IT department to install in production, and that person has to be able to enter connection strings or passwords that you do not know.</span></span>

<span data-ttu-id="dbc76-123">在本教學課程系列涵蓋的案例中，您事先知道必須*對 web.config 檔案*進行的所有作業，因此您不需要使用 Web Deploy 參數。</span><span class="sxs-lookup"><span data-stu-id="dbc76-123">For the scenario that this tutorial series covers, you know in advance everything that has to be done to the *Web.config* file, so you do not need to use Web Deploy parameters.</span></span> <span data-ttu-id="dbc76-124">您將會根據所使用的組建設定進行一些不同的轉換，並根據使用的發行設定檔而有所不同。</span><span class="sxs-lookup"><span data-stu-id="dbc76-124">You'll configure some transformations that differ depending on the build configuration used, and some that differ depending on the publish profile used.</span></span>

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a><span data-ttu-id="dbc76-125">在 Azure 中指定 Web.config 設定</span><span class="sxs-lookup"><span data-stu-id="dbc76-125">Specifying Web.config settings in Azure</span></span>

<span data-ttu-id="dbc76-126">如果您想要變更的*web.config*檔案設定是在 `<connectionStrings>` 或 `<appSettings>` 元素中，而且如果您要部署到 Azure App Service 中的 Web Apps，您可以選擇在部署期間自動化變更的另一個選項。</span><span class="sxs-lookup"><span data-stu-id="dbc76-126">If the *Web.config* file settings that you want to change are in the `<connectionStrings>` or the `<appSettings>` element, and if you are deploying to Web Apps in Azure App Service, you have another option for automating changes during deployment.</span></span> <span data-ttu-id="dbc76-127">您可以在 web 應用程式的管理入口網站頁面的 [**設定**] 索引標籤中，輸入您想要在 Azure 中生效的設定（向下流覽至 [**應用程式設定**] 和 [**連接字串**] 區段）。</span><span class="sxs-lookup"><span data-stu-id="dbc76-127">You can enter the settings that you want to take effect in Azure in the **Configure** tab of the management portal page for your web app (scroll down to the **app settings** and **connection strings** sections).</span></span> <span data-ttu-id="dbc76-128">當您部署專案時，Azure 會自動套用變更。</span><span class="sxs-lookup"><span data-stu-id="dbc76-128">When you deploy the project, Azure automatically applies the changes.</span></span> <span data-ttu-id="dbc76-129">如需詳細資訊，請參閱[Windows Azure 網站：應用程式字串和連接字串的運作方式](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dbc76-129">For more information, see [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).</span></span>

## <a name="default-transformation-files"></a><span data-ttu-id="dbc76-130">預設轉換檔案</span><span class="sxs-lookup"><span data-stu-id="dbc76-130">Default transformation files</span></span>

<span data-ttu-id="dbc76-131">在**方案總管**中，*展開 [web.config]* 以查看預設為兩個預設組建*設定所建立的 web.config 和 web.config* *轉換檔案。*</span><span class="sxs-lookup"><span data-stu-id="dbc76-131">In **Solution Explorer**, expand *Web.config* to see the *Web.Debug.config* and *Web.Release.config* transformation files that are created by default for the two default build configurations.</span></span>

![Web. config_transform_files](web-config-transformations/_static/image1.png)

<span data-ttu-id="dbc76-133">您可以用滑鼠右鍵按一下 Web.config 檔案，然後從內容功能表選擇 [**新增設定轉換**]，來建立自訂群組建設定的轉換檔案。</span><span class="sxs-lookup"><span data-stu-id="dbc76-133">You can create transformation files for custom build configurations by right-clicking the Web.config file and choosing **Add Config Transforms** from the context menu.</span></span> <span data-ttu-id="dbc76-134">在本教學課程中，您不需要這麼做，而且功能表選項會停用，因為您尚未建立任何自訂群組建設定。</span><span class="sxs-lookup"><span data-stu-id="dbc76-134">For this tutorial you don't need to do that, and the menu option is disabled, because you haven't created any custom build configurations.</span></span>

<span data-ttu-id="dbc76-135">稍後您將會建立三個更多的轉換檔案，分別用於測試、預備和生產發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="dbc76-135">Later you'll create three more transformation files, one each for the test, staging, and production publish profiles.</span></span> <span data-ttu-id="dbc76-136">您會在發行設定檔轉換檔案中處理的一般設定範例，因為它相依于目的地環境，是測試與實際執行的不同 WCF 端點。</span><span class="sxs-lookup"><span data-stu-id="dbc76-136">A typical example of a setting that you would handle in a publish profile transformation file because it depends on the destination environment is a WCF endpoint that is different for test versus production.</span></span> <span data-ttu-id="dbc76-137">建立發行設定檔之後，您將在稍後的教學課程中建立發佈設定檔轉換檔案。</span><span class="sxs-lookup"><span data-stu-id="dbc76-137">You'll create publish profile transformation files in later tutorials after you create the publish profiles that they go with.</span></span>

## <a name="disable-debug-mode"></a><span data-ttu-id="dbc76-138">停用 debug 模式</span><span class="sxs-lookup"><span data-stu-id="dbc76-138">Disable debug mode</span></span>

<span data-ttu-id="dbc76-139">`debug` 屬性是相依于組建設定而非目的地環境之設定的範例。</span><span class="sxs-lookup"><span data-stu-id="dbc76-139">An example of a setting that depends on build configuration rather than destination environment is the `debug` attribute.</span></span> <span data-ttu-id="dbc76-140">針對發行組建，您通常會想要停用此功能，而不論您要部署到哪個環境。</span><span class="sxs-lookup"><span data-stu-id="dbc76-140">For a Release build, you typically want debugging disabled regardless of which environment you are deploying to.</span></span> <span data-ttu-id="dbc76-141">因此，Visual Studio 專案範本預設會以從 `compilation` 專案移除 `debug` 屬性的程式碼，建立*web.config*轉換檔案。</span><span class="sxs-lookup"><span data-stu-id="dbc76-141">Therefore, by default the Visual Studio project templates create *Web.Release.config* transform files with code that removes the `debug` attribute from the `compilation` element.</span></span> <span data-ttu-id="dbc76-142">以下是預設的*web.config*：除了批註化的一些範例轉換程式碼之外，它還會在移除 `debug` 屬性的 `compilation` 元素中包含程式碼：</span><span class="sxs-lookup"><span data-stu-id="dbc76-142">Here is the default *Web.Release.config*: in addition to some sample transformation code that is commented out, it includes code in the `compilation` element that removes the `debug` attribute:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

<span data-ttu-id="dbc76-143">`xdt:Transform="RemoveAttributes(debug)"` 屬性指定您想要從已部署的*web.config*檔案中的 `system.web/compilation` 元素移除 `debug` 屬性。</span><span class="sxs-lookup"><span data-stu-id="dbc76-143">The `xdt:Transform="RemoveAttributes(debug)"` attribute specifies that you want the `debug` attribute to be removed from the `system.web/compilation` element in the deployed *Web.config* file.</span></span> <span data-ttu-id="dbc76-144">這會在您每次部署發行組建時完成。</span><span class="sxs-lookup"><span data-stu-id="dbc76-144">This will be done every time you deploy a Release build.</span></span>

## <a name="limit-error-log-access-to-administrators"></a><span data-ttu-id="dbc76-145">限制系統管理員的錯誤記錄檔存取</span><span class="sxs-lookup"><span data-stu-id="dbc76-145">Limit error log access to administrators</span></span>

<span data-ttu-id="dbc76-146">如果應用程式執行時發生錯誤，應用程式會顯示一般錯誤頁面來取代系統產生的錯誤頁面，並使用[Elmah NuGet 封裝](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)來進行錯誤記錄和報告。</span><span class="sxs-lookup"><span data-stu-id="dbc76-146">If there's an error while the application runs, the application displays a generic error page in place of the system-generated error page, and it uses the [Elmah NuGet package](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) for error logging and reporting.</span></span> <span data-ttu-id="dbc76-147">應用程式*web.config*檔案中的 `customErrors` 元素會指定錯誤頁面：</span><span class="sxs-lookup"><span data-stu-id="dbc76-147">The `customErrors` element in the application *Web.config* file specifies the error page:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

<span data-ttu-id="dbc76-148">若要查看錯誤頁面，請暫時將 `customErrors` 元素的 `mode` 屬性從 "RemoteOnly" 變更為 "On"，然後從 Visual Studio 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="dbc76-148">To see the error page, temporarily change the `mode` attribute of the `customErrors` element from "RemoteOnly" to "On" and run the application from Visual Studio.</span></span> <span data-ttu-id="dbc76-149">藉由要求不正確 URL （例如*Studentsxxx*）導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="dbc76-149">Cause an error by requesting an invalid URL, such as *Studentsxxx.aspx*.</span></span> <span data-ttu-id="dbc76-150">您會看到 [ *GenericErrorPage* ] 頁面，而不是 IIS 產生的「找不到資源」錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="dbc76-150">Instead of an IIS-generated "The resource cannot be found" error page, you see the *GenericErrorPage.aspx* page.</span></span>

![錯誤頁面](web-config-transformations/_static/image2.png)

<span data-ttu-id="dbc76-152">若要查看錯誤記錄檔，請將 URL 中的所有內容取代為*elmah. axd* （例如 `http://localhost:51130/elmah.axd`），然後按 enter 鍵：</span><span class="sxs-lookup"><span data-stu-id="dbc76-152">To see the error log, replace everything in the URL after the port number with *elmah.axd* (for example, `http://localhost:51130/elmah.axd`) and press Enter:</span></span>

![ELMAH 頁面](web-config-transformations/_static/image3.png)

<span data-ttu-id="dbc76-154">當您完成時，別忘了將 `customErrors` 元素設回 "RemoteOnly" 模式。</span><span class="sxs-lookup"><span data-stu-id="dbc76-154">Don't forget to set the `customErrors` element back to "RemoteOnly" mode when you're done.</span></span>

<span data-ttu-id="dbc76-155">在您的開發電腦上，允許免費存取錯誤記錄檔頁面，但在生產環境中會有安全性風險。</span><span class="sxs-lookup"><span data-stu-id="dbc76-155">On your development computer it's convenient to allow free access to the error log page, but in production that would be a security risk.</span></span> <span data-ttu-id="dbc76-156">針對生產網站，您想要新增授權規則來限制系統管理員的錯誤記錄檔存取，並確保限制也能在測試和接移時使用。</span><span class="sxs-lookup"><span data-stu-id="dbc76-156">For the production site, you want to add an authorization rule that restricts error log access to administrators, and to make sure that the restriction works you want it in test and staging also.</span></span> <span data-ttu-id="dbc76-157">因此，這是您每次部署發行組建時要執行的另一項變更，因此屬於*web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="dbc76-157">Therefore this is another change that you want to implement every time you deploy a Release build, and so it belongs in the *Web.Release.config* file.</span></span>

<span data-ttu-id="dbc76-158">開啟*web.config，並*在結尾 `configuration` 標記前面加入新的 `location` 元素，如下所示。</span><span class="sxs-lookup"><span data-stu-id="dbc76-158">Open *Web.Release.config* and add a new `location` element immediately before the closing `configuration` tag, as shown here.</span></span>

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

<span data-ttu-id="dbc76-159">"Insert" 的 `Transform` 屬性值會導致此 `location` 元素當做*web.config*檔案中任何現有 `location` 元素的同級加入。</span><span class="sxs-lookup"><span data-stu-id="dbc76-159">The `Transform` attribute value of "Insert" causes this `location` element to be added as a sibling to any existing `location` elements in the *Web.config* file.</span></span> <span data-ttu-id="dbc76-160">（已有一個 `location` 元素指定 [**更新信用額度**] 頁面的授權規則）。</span><span class="sxs-lookup"><span data-stu-id="dbc76-160">(There is already one `location` element that specifies authorization rules for the **Update Credits** page.)</span></span>

<span data-ttu-id="dbc76-161">現在您可以預覽轉換，以確保正確編碼。</span><span class="sxs-lookup"><span data-stu-id="dbc76-161">Now you can preview the transform to make sure that you coded it correctly.</span></span>

<span data-ttu-id="dbc76-162">在**方案總管**中，以滑鼠右鍵按一下 [ *web.config* ]，然後按一下 [**預覽轉換**]。</span><span class="sxs-lookup"><span data-stu-id="dbc76-162">In **Solution Explorer**, right-click *Web.Release.config* and click **Preview Transform**.</span></span>

![預覽轉換功能表](web-config-transformations/_static/image4.png)

<span data-ttu-id="dbc76-164">隨即開啟一個頁面，其中會顯示左側的開發 web.config 檔案，以及已醒目提示已*部署* *的 web.config 檔案*在右邊的樣子。</span><span class="sxs-lookup"><span data-stu-id="dbc76-164">A page opens that shows you the development *Web.config* file on the left and what the deployed *Web.config* file will look like on the right, with changes highlighted.</span></span>

![Debug 轉換的預覽](web-config-transformations/_static/image5.png)

![位置轉換預覽](web-config-transformations/_static/image6.png)

<span data-ttu-id="dbc76-167">（在預覽版中，您可能會注意到您未寫入轉換的一些其他變更：這些變更通常包含移除不影響功能的空白字元）。</span><span class="sxs-lookup"><span data-stu-id="dbc76-167">( In the preview, you might notice some additional changes that you didn't write transforms for: these typically involve the removal of white space that doesn't affect functionality.)</span></span>

<span data-ttu-id="dbc76-168">當您在部署後測試網站時，您也會進行測試以確認授權規則有效。</span><span class="sxs-lookup"><span data-stu-id="dbc76-168">When you test the site after deployment, you'll also test to verify that the authorization rule is effective.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="dbc76-169">**安全性注意事項**絕對不要在實際執行應用程式中顯示公用的錯誤詳細資料，或將該資訊儲存在公用位置。</span><span class="sxs-lookup"><span data-stu-id="dbc76-169">**Security Note** Never display error details to the public in a production application, or store that information in a public location.</span></span> <span data-ttu-id="dbc76-170">攻擊者可以使用錯誤資訊來探索網站中的弱點。</span><span class="sxs-lookup"><span data-stu-id="dbc76-170">Attackers can use error information to discover vulnerabilities in a site.</span></span> <span data-ttu-id="dbc76-171">如果您在自己的應用程式中使用 ELMAH，請設定 ELMAH 以將安全性風險降至最低。</span><span class="sxs-lookup"><span data-stu-id="dbc76-171">If you use ELMAH in your own application, configure ELMAH to minimize security risks.</span></span> <span data-ttu-id="dbc76-172">本教學課程中的 ELMAH 範例不應視為建議的設定。</span><span class="sxs-lookup"><span data-stu-id="dbc76-172">The ELMAH example in this tutorial should not be considered a recommended configuration.</span></span> <span data-ttu-id="dbc76-173">這是為了說明如何處理應用程式必須能夠在中建立檔案的資料夾，所選擇的範例。</span><span class="sxs-lookup"><span data-stu-id="dbc76-173">It is an example that was chosen in order to illustrate how to handle a folder that the application must be able to create files in.</span></span> <span data-ttu-id="dbc76-174">如需詳細資訊，請參閱[保護 ELMAH 端點](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)。</span><span class="sxs-lookup"><span data-stu-id="dbc76-174">For more information, see [securing the ELMAH endpoint](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages).</span></span>

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a><span data-ttu-id="dbc76-175">您將在發行設定檔轉換檔案中處理的設定</span><span class="sxs-lookup"><span data-stu-id="dbc76-175">A setting that you'll handle in publish profile transformation files</span></span>

<span data-ttu-id="dbc76-176">常見的案例是在您部署的每個環境中，都必須有不同的*web.config*檔案設定。</span><span class="sxs-lookup"><span data-stu-id="dbc76-176">A common scenario is to have *Web.config* file settings that must be different in each environment that you deploy to.</span></span> <span data-ttu-id="dbc76-177">例如，呼叫 WCF 服務的應用程式在測試和生產環境中可能需要不同的端點。</span><span class="sxs-lookup"><span data-stu-id="dbc76-177">For example, an application that calls a WCF service might need a different endpoint in test and production environments.</span></span> <span data-ttu-id="dbc76-178">Contoso 大學應用程式也包含此類型的設定。</span><span class="sxs-lookup"><span data-stu-id="dbc76-178">The Contoso University application includes a setting of this kind also.</span></span> <span data-ttu-id="dbc76-179">此設定會控制網站頁面上的可見指標，告訴您您所在的環境（例如開發、測試或生產）。</span><span class="sxs-lookup"><span data-stu-id="dbc76-179">This setting controls a visible indicator on a site's pages that tells you which environment you are in, such as development, test, or production.</span></span> <span data-ttu-id="dbc76-180">設定值會決定應用程式是否要將 "（Dev）" 或 "（Test）" 附加至*網站*主版頁面中的主要標題：</span><span class="sxs-lookup"><span data-stu-id="dbc76-180">The setting value determines whether the application will append "(Dev)" or "(Test)" to the main heading in the *Site.Master* master page:</span></span>

![環境指標](web-config-transformations/_static/image7.png)

<span data-ttu-id="dbc76-182">當應用程式在預備或生產環境中執行時，會省略環境指示器。</span><span class="sxs-lookup"><span data-stu-id="dbc76-182">The environment indicator is omitted when the application is running in staging or production.</span></span>

<span data-ttu-id="dbc76-183">Contoso 大學網頁會讀取*web.config*檔案 `appSettings` 中設定的值，以判斷應用程式執行所在的環境：</span><span class="sxs-lookup"><span data-stu-id="dbc76-183">The Contoso University web pages read a value that is set in `appSettings` in the *Web.config* file in order to determine what environment the application is running in:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

<span data-ttu-id="dbc76-184">測試環境中的值應該是「測試」，而「生產」則是用於預備與生產。</span><span class="sxs-lookup"><span data-stu-id="dbc76-184">The value should be "Test" in the test environment, and "Prod" for staging and production.</span></span>

<span data-ttu-id="dbc76-185">轉換檔案中的下列程式碼將會執行此轉換：</span><span class="sxs-lookup"><span data-stu-id="dbc76-185">The following code in a transform file will implement this transformation:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

<span data-ttu-id="dbc76-186">`xdt:Transform` 屬性值 "SetAttributes" 表示此轉換的目的是要變更*web.config*檔案中現有元素的屬性值。</span><span class="sxs-lookup"><span data-stu-id="dbc76-186">The `xdt:Transform` attribute value "SetAttributes" indicates that the purpose of this transform is to change attribute values of an existing element in the *Web.config* file.</span></span> <span data-ttu-id="dbc76-187">`xdt:Locator` 屬性值 "Match （key）" 表示要修改的專案是其 `key` 屬性符合這裡指定之 `key` 屬性的元素。</span><span class="sxs-lookup"><span data-stu-id="dbc76-187">The `xdt:Locator` attribute value "Match(key)" indicates that the element to be modified is the one whose `key` attribute matches the `key` attribute specified here.</span></span> <span data-ttu-id="dbc76-188">`add` 專案的唯一另一個屬性是 `value`，這就是在已部署的*web.config*檔案中將會變更的專案。</span><span class="sxs-lookup"><span data-stu-id="dbc76-188">The only other attribute of the `add` element is `value`, and that is what will be changed in the deployed *Web.config* file.</span></span> <span data-ttu-id="dbc76-189">此處顯示的程式碼會在*部署的 web.config*檔案中，將 `Environment` `appSettings` 元素的 `value` 屬性設定為 "Test"。</span><span class="sxs-lookup"><span data-stu-id="dbc76-189">The code shown here causes the `value` attribute of the `Environment` `appSettings` element to be set to "Test" in the *Web.config* file that is deployed.</span></span>

<span data-ttu-id="dbc76-190">這項轉換屬於尚未建立的發行設定檔轉換檔案。</span><span class="sxs-lookup"><span data-stu-id="dbc76-190">This transform belongs in the publish profile transform files, which you haven't created yet.</span></span> <span data-ttu-id="dbc76-191">當您建立測試、預備和生產環境的發行設定檔時，您將會建立並更新執行這種變更的轉換檔案。</span><span class="sxs-lookup"><span data-stu-id="dbc76-191">You'll create and update the transform files that implement this change when you create the publish profiles for the test, staging, and production environments.</span></span> <span data-ttu-id="dbc76-192">您會在[部署至 IIS](deploying-to-iis.md)和[部署至生產](deploying-to-production.md)教學課程中執行此動作。</span><span class="sxs-lookup"><span data-stu-id="dbc76-192">You'll do that in the [deploy to IIS](deploying-to-iis.md) and [deploy to production](deploying-to-production.md) tutorials.</span></span>

> [!NOTE]
> <span data-ttu-id="dbc76-193">因為此設定是在 `<appSettings>` 元素中，所以當您部署至中的 Web Apps 時，您可以使用另一個替代方式來指定轉換 Azure App Service 請參閱本主題稍早在[Azure 中指定 web.config 設定](#watransforms)。</span><span class="sxs-lookup"><span data-stu-id="dbc76-193">Because this setting is in the `<appSettings>` element, you have another alternative for specifying the transformation when you're deploying to Web Apps in Azure App Service See [Specifying Web.config settings in Azure](#watransforms) earlier in this topic.</span></span>

## <a name="setting-connection-strings"></a><span data-ttu-id="dbc76-194">設定連接字串</span><span class="sxs-lookup"><span data-stu-id="dbc76-194">Setting connection strings</span></span>

<span data-ttu-id="dbc76-195">雖然預設的轉換檔案包含示範如何更新連接字串的範例，但在大多數情況下，您不需要設定連接字串轉換，因為您可以在發行設定檔中指定連接字串。</span><span class="sxs-lookup"><span data-stu-id="dbc76-195">Although the default transform file contains an example that shows how to update a connection string, in most cases you do not need to set up connection string transformations, because you can specify connection strings in the publish profile.</span></span> <span data-ttu-id="dbc76-196">您會在[部署至 IIS](deploying-to-iis.md)和[部署至生產](deploying-to-production.md)教學課程中執行此動作。</span><span class="sxs-lookup"><span data-stu-id="dbc76-196">You'll do that in the [deploy to IIS](deploying-to-iis.md) and [deploy to production](deploying-to-production.md) tutorials.</span></span>

## <a name="summary"></a><span data-ttu-id="dbc76-197">總結</span><span class="sxs-lookup"><span data-stu-id="dbc76-197">Summary</span></span>

<span data-ttu-id="dbc76-198">在建立發行設定檔之前，您已完成*與 web.config 轉換相同*的作業，而且您已瞭解已部署的 web.config 檔案中會有哪些內容的預覽。</span><span class="sxs-lookup"><span data-stu-id="dbc76-198">You have now done as much as you can with *Web.config* transformations before you create the publish profiles, and you've seen a preview of what will be in the deployed Web.config file.</span></span>

![位置轉換預覽](web-config-transformations/_static/image8.png)

<span data-ttu-id="dbc76-200">在下列教學課程中，您將會負責需要設定專案屬性的部署設定工作。</span><span class="sxs-lookup"><span data-stu-id="dbc76-200">In the following tutorial, you'll take care of deployment set-up tasks that require setting project properties.</span></span>

## <a name="more-information"></a><span data-ttu-id="dbc76-201">更多資訊</span><span class="sxs-lookup"><span data-stu-id="dbc76-201">More Information</span></span>

<span data-ttu-id="dbc76-202">如需本教學課程涵蓋之主題的詳細資訊，請參閱在 Visual Studio 和 ASP.NET 的 Web 部署內容對應中[部署期間，使用 web.config 轉換來變更目的地 web.config 檔案或 app.config 檔案中的設定](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms)。</span><span class="sxs-lookup"><span data-stu-id="dbc76-202">For more information about topics covered by this tutorial, see [Using Web.config transformations to change settings in the destination Web.config file or app.config file during deployment](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) in the Web Deployment Content Map for Visual Studio and ASP.NET.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dbc76-203">[上一頁](preparing-databases.md)
> [下一頁](project-properties.md)</span><span class="sxs-lookup"><span data-stu-id="dbc76-203">[Previous](preparing-databases.md)
[Next](project-properties.md)</span></span>
