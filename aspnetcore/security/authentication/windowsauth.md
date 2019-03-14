---
title: 在 ASP.NET Core 中設定 Windows 驗證
author: scottaddie
description: 了解如何在 ASP.NET Core，使用 IIS Express、 IIS 和 HTTP.sys 中設定 Windows 驗證。
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc, seodec18
ms.date: 02/25/2019
uid: security/authentication/windowsauth
ms.openlocfilehash: 15fc41efba77f88fc8129f875b85836ac1b5f886
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031935"
---
# <a name="configure-windows-authentication-in-aspnet-core"></a><span data-ttu-id="5b7fe-103">在 ASP.NET Core 中設定 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="5b7fe-103">Configure Windows Authentication in ASP.NET Core</span></span>

<span data-ttu-id="5b7fe-104">藉由[Scott Addie](https://twitter.com/Scott_Addie)和[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="5b7fe-104">By [Scott Addie](https://twitter.com/Scott_Addie) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="5b7fe-105">[Windows 驗證](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/)可以設定與裝載的 ASP.NET Core 應用程式[IIS](xref:host-and-deploy/iis/index)或是[HTTP.sys](xref:fundamentals/servers/httpsys)。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-105">[Windows Authentication](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) can be configured for ASP.NET Core apps hosted with [IIS](xref:host-and-deploy/iis/index) or [HTTP.sys](xref:fundamentals/servers/httpsys).</span></span>

<span data-ttu-id="5b7fe-106">Windows 驗證會仰賴作業系統來驗證的 ASP.NET Core 應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-106">Windows Authentication relies on the operating system to authenticate users of ASP.NET Core apps.</span></span> <span data-ttu-id="5b7fe-107">使用 Active Directory 網域身分識別或 Windows 帳戶，來識別使用者在公司網路中執行您的伺服器時，您可以使用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-107">You can use Windows Authentication when your server runs on a corporate network using Active Directory domain identities or Windows accounts to identify users.</span></span> <span data-ttu-id="5b7fe-108">Windows 驗證最適合內部網路的環境，其中使用者、 用戶端應用程式，以及網頁伺服器都屬於相同 Windows 網域。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-108">Windows Authentication is best suited to intranet environments where users, client apps, and web servers belong to the same Windows domain.</span></span>

## <a name="enable-windows-authentication-in-an-aspnet-core-app"></a><span data-ttu-id="5b7fe-109">啟用 ASP.NET Core 應用程式中的 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="5b7fe-109">Enable Windows Authentication in an ASP.NET Core app</span></span>

<span data-ttu-id="5b7fe-110">**Web 應用程式**可透過 Visual Studio 或.NET Core CLI 的範本可以設定為支援 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-110">The **Web Application** template available via Visual Studio or the .NET Core CLI can be configured to support Windows Authentication.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="5b7fe-111">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b7fe-111">Visual Studio</span></span>](#tab/visual-studio)

### <a name="use-the-windows-authentication-app-template-for-a-new-project"></a><span data-ttu-id="5b7fe-112">新的專案中使用 Windows 驗證應用程式範本</span><span class="sxs-lookup"><span data-stu-id="5b7fe-112">Use the Windows Authentication app template for a new project</span></span>

<span data-ttu-id="5b7fe-113">在 Visual Studio 中：</span><span class="sxs-lookup"><span data-stu-id="5b7fe-113">In Visual Studio:</span></span>

1. <span data-ttu-id="5b7fe-114">建立新**ASP.NET Core Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-114">Create a new **ASP.NET Core Web Application**.</span></span>
1. <span data-ttu-id="5b7fe-115">選取  **Web 應用程式**從範本清單。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-115">Select **Web Application** from the list of templates.</span></span>
1. <span data-ttu-id="5b7fe-116">選取 **變更驗證**按鈕，然後選取**Windows 驗證**。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-116">Select the **Change Authentication** button and select **Windows Authentication**.</span></span>

<span data-ttu-id="5b7fe-117">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-117">Run the app.</span></span> <span data-ttu-id="5b7fe-118">使用者名稱會出現在呈現的應用程式使用者介面。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-118">The username appears in the rendered app's user interface.</span></span>

### <a name="manual-configuration-for-an-existing-project"></a><span data-ttu-id="5b7fe-119">手動設定現有的專案</span><span class="sxs-lookup"><span data-stu-id="5b7fe-119">Manual configuration for an existing project</span></span>

<span data-ttu-id="5b7fe-120">專案的屬性可讓您以啟用 Windows 驗證並停用匿名驗證：</span><span class="sxs-lookup"><span data-stu-id="5b7fe-120">The project's properties allow you to enable Windows Authentication and disable Anonymous Authentication:</span></span>

1. <span data-ttu-id="5b7fe-121">在 Visual Studio 的專案上按一下滑鼠右鍵**方案總管**，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-121">Right-click the project in Visual Studio's **Solution Explorer** and select **Properties**.</span></span>
1. <span data-ttu-id="5b7fe-122">選取 [偵錯] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-122">Select the **Debug** tab.</span></span>
1. <span data-ttu-id="5b7fe-123">清除核取方塊**啟用匿名驗證**。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-123">Clear the check box for **Enable Anonymous Authentication**.</span></span>
1. <span data-ttu-id="5b7fe-124">選取核取方塊**啟用 Windows 驗證**。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-124">Select the check box for **Enable Windows Authentication**.</span></span>

<span data-ttu-id="5b7fe-125">或者，設定屬性，在`iisSettings`的節點*launchSettings.json*檔案：</span><span class="sxs-lookup"><span data-stu-id="5b7fe-125">Alternatively, the properties can be configured in the `iisSettings` node of the *launchSettings.json* file:</span></span>

[!code-json[](windowsauth/sample_snapshot/launchSettings.json?highlight=2-3)]

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="5b7fe-126">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="5b7fe-126">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="5b7fe-127">使用**Windows 驗證**應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-127">Use the **Windows Authentication** app template.</span></span>

<span data-ttu-id="5b7fe-128">執行[dotnet 新](/dotnet/core/tools/dotnet-new)命令搭配`webapp`引數 （ASP.NET Core Web 應用程式） 和`--auth Windows`切換：</span><span class="sxs-lookup"><span data-stu-id="5b7fe-128">Execute the [dotnet new](/dotnet/core/tools/dotnet-new) command with the `webapp` argument (ASP.NET Core Web App) and `--auth Windows` switch:</span></span>

```console
dotnet new webapp --auth Windows
```

---

<span data-ttu-id="5b7fe-129">當修改現有的專案，請確認專案檔包含的套件參考[Microsoft.AspNetCore.App 中繼套件](xref:fundamentals/metapackage-app)**或是** [Microsoft.AspNetCore.Authentication](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication/) NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-129">When modifying an existing project, confirm that the project file includes a package reference for the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) **or** the [Microsoft.AspNetCore.Authentication](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication/) NuGet package.</span></span>

## <a name="enable-windows-authentication-with-iis"></a><span data-ttu-id="5b7fe-130">啟用 iis 的 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="5b7fe-130">Enable Windows Authentication with IIS</span></span>

<span data-ttu-id="5b7fe-131">IIS 會使用[ASP.NET Core 模組](xref:host-and-deploy/aspnet-core-module)主機 ASP.NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-131">IIS uses the [ASP.NET Core Module](xref:host-and-deploy/aspnet-core-module) to host ASP.NET Core apps.</span></span> <span data-ttu-id="5b7fe-132">Windows 驗證針對透過 IIS *web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-132">Windows Authentication is configured for IIS via the *web.config* file.</span></span> <span data-ttu-id="5b7fe-133">下列各節將示範如何：</span><span class="sxs-lookup"><span data-stu-id="5b7fe-133">The following sections show how to:</span></span>

* <span data-ttu-id="5b7fe-134">提供本機*web.config*部署應用程式時，請在伺服器啟動 Windows 驗證的檔案。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-134">Provide a local *web.config* file that activates Windows Authentication on the server when the app is deployed.</span></span>
* <span data-ttu-id="5b7fe-135">使用 IIS 管理員設定*web.config*已經部署到伺服器的 ASP.NET Core 應用程式的檔案。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-135">Use the IIS Manager to configure the *web.config* file of an ASP.NET Core app that has already been deployed to the server.</span></span>

### <a name="iis-configuration"></a><span data-ttu-id="5b7fe-136">IIS 組態</span><span class="sxs-lookup"><span data-stu-id="5b7fe-136">IIS configuration</span></span>

<span data-ttu-id="5b7fe-137">如果您尚未這麼做，請啟用 IIS 可裝載 ASP.NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-137">If you haven't already done so, enable IIS to host ASP.NET Core apps.</span></span> <span data-ttu-id="5b7fe-138">如需詳細資訊，請參閱<xref:host-and-deploy/iis/index>。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-138">For more information, see <xref:host-and-deploy/iis/index>.</span></span>

<span data-ttu-id="5b7fe-139">啟用 Windows 驗證的 IIS 角色服務。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-139">Enable the IIS Role Service for Windows Authentication.</span></span> <span data-ttu-id="5b7fe-140">如需詳細資訊，請參閱 <<c0> [ 啟用 IIS 角色服務 （請參閱步驟 2） 中的 Windows 驗證](xref:host-and-deploy/iis/index#iis-configuration)。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-140">For more information, see [Enable Windows Authentication in IIS Role Services (see Step 2)](xref:host-and-deploy/iis/index#iis-configuration).</span></span>

<span data-ttu-id="5b7fe-141">根據預設，IIS Integration 中介軟體會設定來自動驗證要求。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-141">IIS Integration Middleware is configured to automatically authenticate requests by default.</span></span> <span data-ttu-id="5b7fe-142">如需詳細資訊，請參閱[裝載 ASP.NET Core 與 IIS 的 Windows 上：IIS 選項 (AutomaticAuthentication)](xref:host-and-deploy/iis/index#iis-options)。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-142">For more information, see [Host ASP.NET Core on Windows with IIS: IIS options (AutomaticAuthentication)](xref:host-and-deploy/iis/index#iis-options).</span></span>

<span data-ttu-id="5b7fe-143">ASP.NET Core 模組預設設定為轉送至應用程式的 Windows 驗證語彙基元。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-143">The ASP.NET Core Module is configured to forward the Windows Authentication token to the app by default.</span></span> <span data-ttu-id="5b7fe-144">如需詳細資訊，請參閱[ASP.NET Core 模組組態參考：AspNetCore 元素的屬性](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element)。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-144">For more information, see [ASP.NET Core Module configuration reference: Attributes of the aspNetCore element](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element).</span></span>

### <a name="create-a-new-iis-site"></a><span data-ttu-id="5b7fe-145">建立新的 IIS 站台</span><span class="sxs-lookup"><span data-stu-id="5b7fe-145">Create a new IIS site</span></span>

<span data-ttu-id="5b7fe-146">指定的名稱和資料夾，並允許它建立新的應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-146">Specify a name and folder and allow it to create a new application pool.</span></span>

### <a name="enable-windows-authentication-for-the-app-in-iis"></a><span data-ttu-id="5b7fe-147">啟用 IIS 中的應用程式的 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="5b7fe-147">Enable Windows Authentication for the app in IIS</span></span>

<span data-ttu-id="5b7fe-148">使用**任一**下列其中一個方法：</span><span class="sxs-lookup"><span data-stu-id="5b7fe-148">Use **either** of the following approaches:</span></span>

* <span data-ttu-id="5b7fe-149">[在之前發佈的應用程式的開發後端設定](#development-side-configuration-with-a-local-webconfig-file)(*建議*)</span><span class="sxs-lookup"><span data-stu-id="5b7fe-149">[Development-side configuration before publishing the app](#development-side-configuration-with-a-local-webconfig-file) (*Recommended*)</span></span>
* [<span data-ttu-id="5b7fe-150">之後發佈的應用程式的伺服器端設定</span><span class="sxs-lookup"><span data-stu-id="5b7fe-150">Server-side configuration after publishing the app</span></span>](#server-side-configuration-with-the-iis-manager)

#### <a name="development-side-configuration-with-a-local-webconfig-file"></a><span data-ttu-id="5b7fe-151">使用本機 web.config 檔案的開發後端設定</span><span class="sxs-lookup"><span data-stu-id="5b7fe-151">Development-side configuration with a local web.config file</span></span>

<span data-ttu-id="5b7fe-152">執行下列步驟**之前**您[發佈和部署您的專案](#publish-and-deploy-your-project-to-the-iis-site-folder)。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-152">Perform the following steps **before** you [publish and deploy your project](#publish-and-deploy-your-project-to-the-iis-site-folder).</span></span>

<span data-ttu-id="5b7fe-153">新增下列*web.config*至專案根目錄的檔案：</span><span class="sxs-lookup"><span data-stu-id="5b7fe-153">Add the following *web.config* file to the project root:</span></span>

[!code-xml[](windowsauth/sample_snapshot/web_2.config)]

<span data-ttu-id="5b7fe-154">專案 sdk 的發行時 (不含`<IsTransformWebConfigDisabled>`屬性設定為`true`專案檔中)，發行*web.config*檔案包含`<location><system.webServer><security><authentication>`一節。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-154">When the project is published by the SDK (without the `<IsTransformWebConfigDisabled>` property set to `true` in the project file), the published *web.config* file includes the `<location><system.webServer><security><authentication>` section.</span></span> <span data-ttu-id="5b7fe-155">如需詳細資訊`<IsTransformWebConfigDisabled>`屬性，請參閱<xref:host-and-deploy/iis/index#webconfig-file>。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-155">For more information on the `<IsTransformWebConfigDisabled>` property, see <xref:host-and-deploy/iis/index#webconfig-file>.</span></span>

#### <a name="server-side-configuration-with-the-iis-manager"></a><span data-ttu-id="5b7fe-156">伺服器端設定使用 IIS 管理員</span><span class="sxs-lookup"><span data-stu-id="5b7fe-156">Server-side configuration with the IIS Manager</span></span>

<span data-ttu-id="5b7fe-157">執行下列步驟**之後**您[發佈和部署您的專案](#publish-and-deploy-your-project-to-the-iis-site-folder)。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-157">Perform the following steps **after** you [publish and deploy your project](#publish-and-deploy-your-project-to-the-iis-site-folder).</span></span>

1. <span data-ttu-id="5b7fe-158">在 [IIS 管理員] 中，選取 IIS 站台之下**站台**節點**連線**資訊看板。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-158">In IIS Manager, select the IIS site under the **Sites** node of the **Connections** sidebar.</span></span>
1. <span data-ttu-id="5b7fe-159">按兩下**驗證**中**IIS**區域。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-159">Double-click **Authentication** in the **IIS** area.</span></span>
1. <span data-ttu-id="5b7fe-160">選取 **匿名驗證**。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-160">Select **Anonymous Authentication**.</span></span> <span data-ttu-id="5b7fe-161">選取 **停用**中**動作**資訊看板。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-161">Select **Disable** in the **Actions** sidebar.</span></span>
1. <span data-ttu-id="5b7fe-162">選取  **Windows 驗證**。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-162">Select **Windows Authentication**.</span></span> <span data-ttu-id="5b7fe-163">選取 **啟用**中**動作**資訊看板。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-163">Select **Enable** in the **Actions** sidebar.</span></span>

<span data-ttu-id="5b7fe-164">IIS 管理員在採取這些動作，會修改應用程式的*web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-164">When these actions are taken, IIS Manager modifies the app's *web.config* file.</span></span> <span data-ttu-id="5b7fe-165">A`<system.webServer><security><authentication>`節點新增與更新的設定，如`anonymousAuthentication`和`windowsAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="5b7fe-165">A `<system.webServer><security><authentication>` node is added with updated settings for `anonymousAuthentication` and `windowsAuthentication`:</span></span>

[!code-xml[](windowsauth/sample_snapshot/web_1.config?highlight=4-5)]

<span data-ttu-id="5b7fe-166">`<system.webServer>`區段新增至*web.config*由 IIS 管理員中的檔案超出應用程式的`<location>`發佈應用程式時，由.NET Core SDK 加入的區段。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-166">The `<system.webServer>` section added to the *web.config* file by IIS Manager is outside of the app's `<location>` section added by the .NET Core SDK when the app is published.</span></span> <span data-ttu-id="5b7fe-167">因為區段會新增外部`<location>`節點，設定會由任何繼承[子應用程式](xref:host-and-deploy/iis/index#sub-applications)目前的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-167">Because the section is added outside of the `<location>` node, the settings are inherited by any [sub-apps](xref:host-and-deploy/iis/index#sub-applications) to the current app.</span></span> <span data-ttu-id="5b7fe-168">若要防止繼承，移動加入`<security>`區段內的`<location><system.webServer>`SDK 所提供的一節。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-168">To prevent inheritance, move the added `<security>` section inside of the `<location><system.webServer>` section that the SDK provided.</span></span>

<span data-ttu-id="5b7fe-169">將 IIS 設定使用 IIS 管理員時，它只會影響應用程式的*web.config*伺服器上的檔案。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-169">When IIS Manager is used to add the IIS configuration, it only affects the app's *web.config* file on the server.</span></span> <span data-ttu-id="5b7fe-170">後續部署應用程式可能會覆寫伺服器上的設定，如果伺服器的複本*web.config*專案的取代*web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-170">A subsequent deployment of the app may overwrite the settings on the server if the server's copy of *web.config* is replaced by the project's *web.config* file.</span></span> <span data-ttu-id="5b7fe-171">使用**任一**下列其中一個方法來管理設定：</span><span class="sxs-lookup"><span data-stu-id="5b7fe-171">Use **either** of the following approaches to manage the settings:</span></span>

* <span data-ttu-id="5b7fe-172">使用 IIS 管理員中的設定重設*web.config*檔案之後部署上覆寫該檔案。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-172">Use IIS Manager to reset the settings in the *web.config* file after the file is overwritten on deployment.</span></span>
* <span data-ttu-id="5b7fe-173">新增*web.config 檔案*應用程式在本機使用的設定。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-173">Add a *web.config file* to the app locally with the settings.</span></span> <span data-ttu-id="5b7fe-174">如需詳細資訊，請參閱 <<c0> [ 開發後端設定](#development-side-configuration-with-a-local-webconfig-file)一節。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-174">For more information, see the [Development-side configuration](#development-side-configuration-with-a-local-webconfig-file) section.</span></span>

### <a name="publish-and-deploy-your-project-to-the-iis-site-folder"></a><span data-ttu-id="5b7fe-175">發行，並將專案部署至 IIS 的站台資料夾</span><span class="sxs-lookup"><span data-stu-id="5b7fe-175">Publish and deploy your project to the IIS site folder</span></span>

<span data-ttu-id="5b7fe-176">使用 Visual Studio 或.NET Core CLI，發行應用程式並部署到目的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-176">Using Visual Studio or the .NET Core CLI, publish and deploy the app to the destination folder.</span></span>

<span data-ttu-id="5b7fe-177">如需有關如何使用 IIS 裝載的詳細資訊，發行和部署，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="5b7fe-177">For more information on hosting with IIS, publishing, and deployment, see the following topics:</span></span>

* [<span data-ttu-id="5b7fe-178">dotnet publish</span><span class="sxs-lookup"><span data-stu-id="5b7fe-178">dotnet publish</span></span>](/dotnet/core/tools/dotnet-publish)
* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/visual-studio-publish-profiles>

<span data-ttu-id="5b7fe-179">啟動應用程式以確認 Windows 驗證正常運作。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-179">Launch the app to verify Windows Authentication is working.</span></span>

## <a name="enable-windows-authentication-with-httpsys"></a><span data-ttu-id="5b7fe-180">啟用 Windows 驗證，http.sys</span><span class="sxs-lookup"><span data-stu-id="5b7fe-180">Enable Windows Authentication with HTTP.sys</span></span>

<span data-ttu-id="5b7fe-181">雖然 Kestrel 不支援 Windows 驗證，您可以使用[HTTP.sys](xref:fundamentals/servers/httpsys)支援在 Windows 上的自我裝載的案例。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-181">Although Kestrel doesn't support Windows Authentication, you can use [HTTP.sys](xref:fundamentals/servers/httpsys) to support self-hosted scenarios on Windows.</span></span> <span data-ttu-id="5b7fe-182">下列範例會設定要搭配 Windows 驗證使用 HTTP.sys 的應用程式的 web 主機：</span><span class="sxs-lookup"><span data-stu-id="5b7fe-182">The following example configures the app's web host to use HTTP.sys with Windows Authentication:</span></span>

[!code-csharp[](windowsauth/sample_snapshot/Program.cs?highlight=9-14)]

> [!NOTE]
> <span data-ttu-id="5b7fe-183">HTTP.sys 使用 Kerberos 驗證通訊協定委派給核心模式驗證。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-183">HTTP.sys delegates to kernel mode authentication with the Kerberos authentication protocol.</span></span> <span data-ttu-id="5b7fe-184">Kerberos 和 HTTP.sys 不支援使用者模式驗證。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-184">User mode authentication isn't supported with Kerberos and HTTP.sys.</span></span> <span data-ttu-id="5b7fe-185">必須使用電腦帳戶來解密 Kerberos 權杖/票證，該權杖/票證取自 Active Directory，並由用戶端將其轉送至伺服器來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-185">The machine account must be used to decrypt the Kerberos token/ticket that's obtained from Active Directory and forwarded by the client to the server to authenticate the user.</span></span> <span data-ttu-id="5b7fe-186">請註冊主機的服務主體名稱 (SPN)，而非應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-186">Register the Service Principal Name (SPN) for the host, not the user of the app.</span></span>

> [!NOTE]
> <span data-ttu-id="5b7fe-187">HTTP.sys 不支援 Nano Server 1709 版或更新版本上。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-187">HTTP.sys isn't supported on Nano Server version 1709 or later.</span></span> <span data-ttu-id="5b7fe-188">若要使用 Windows 驗證和 HTTP.sys 使用 Nano Server，請使用[Server Core (microsoft/windowsservercore) 容器](https://hub.docker.com/r/microsoft/windowsservercore/)。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-188">To use Windows Authentication and HTTP.sys with Nano Server, use a [Server Core (microsoft/windowsservercore) container](https://hub.docker.com/r/microsoft/windowsservercore/).</span></span> <span data-ttu-id="5b7fe-189">如需有關 Server Core 的詳細資訊，請參閱[什麼是 Windows Server 中的 Server Core 安裝選項？](/windows-server/administration/server-core/what-is-server-core)。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-189">For more information on Server Core, see [What is the Server Core installation option in Windows Server?](/windows-server/administration/server-core/what-is-server-core).</span></span>

## <a name="work-with-windows-authentication"></a><span data-ttu-id="5b7fe-190">使用 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="5b7fe-190">Work with Windows Authentication</span></span>

<span data-ttu-id="5b7fe-191">匿名存取的設定狀態決定的方式`[Authorize]`和`[AllowAnonymous]`應用程式中使用屬性。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-191">The configuration state of anonymous access determines the way in which the `[Authorize]` and `[AllowAnonymous]` attributes are used in the app.</span></span> <span data-ttu-id="5b7fe-192">下列兩節會說明如何處理不允許和允許設定狀態的匿名存取。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-192">The following two sections explain how to handle the disallowed and allowed configuration states of anonymous access.</span></span>

### <a name="disallow-anonymous-access"></a><span data-ttu-id="5b7fe-193">不允許匿名存取</span><span class="sxs-lookup"><span data-stu-id="5b7fe-193">Disallow anonymous access</span></span>

<span data-ttu-id="5b7fe-194">當您啟用 Windows 驗證，並已停用匿名存取，`[Authorize]`和`[AllowAnonymous]`屬性沒有任何作用。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-194">When Windows Authentication is enabled and anonymous access is disabled, the `[Authorize]` and `[AllowAnonymous]` attributes have no effect.</span></span> <span data-ttu-id="5b7fe-195">如果 IIS 網站 （或 HTTP.sys） 設定為不允許匿名存取，要求永遠不會到達您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-195">If the IIS site (or HTTP.sys) is configured to disallow anonymous access, the request never reaches your app.</span></span> <span data-ttu-id="5b7fe-196">基於這個理由，`[AllowAnonymous]`屬性不適用。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-196">For this reason, the `[AllowAnonymous]` attribute isn't applicable.</span></span>

### <a name="allow-anonymous-access"></a><span data-ttu-id="5b7fe-197">允許匿名存取</span><span class="sxs-lookup"><span data-stu-id="5b7fe-197">Allow anonymous access</span></span>

<span data-ttu-id="5b7fe-198">當啟用 Windows 驗證和匿名存取時，使用`[Authorize]`和`[AllowAnonymous]`屬性。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-198">When both Windows Authentication and anonymous access are enabled, use the `[Authorize]` and `[AllowAnonymous]` attributes.</span></span> <span data-ttu-id="5b7fe-199">`[Authorize]`屬性可讓您安全的應用程式真正需要 Windows 驗證的項目。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-199">The `[Authorize]` attribute allows you to secure pieces of the app which truly do require Windows Authentication.</span></span> <span data-ttu-id="5b7fe-200">`[AllowAnonymous]`屬性覆寫`[Authorize]`屬性允許匿名存取的應用程式內的使用方式。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-200">The `[AllowAnonymous]` attribute overrides `[Authorize]` attribute usage within apps which allow anonymous access.</span></span> <span data-ttu-id="5b7fe-201">請參閱[簡單授權](xref:security/authorization/simple)屬性使用方式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-201">See [Simple Authorization](xref:security/authorization/simple) for attribute usage details.</span></span>

<span data-ttu-id="5b7fe-202">在 ASP.NET Core 2.x 中，`[Authorize]`屬性需要額外的設定，在*Startup.cs*挑戰進行 Windows 驗證的匿名要求。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-202">In ASP.NET Core 2.x, the `[Authorize]` attribute requires additional configuration in *Startup.cs* to challenge anonymous requests for Windows Authentication.</span></span> <span data-ttu-id="5b7fe-203">建議的設定會有些許出入所使用的 web 伺服器而有所不同。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-203">The recommended configuration varies slightly based on the web server being used.</span></span>

> [!NOTE]
> <span data-ttu-id="5b7fe-204">根據預設，缺少授權，才能存取頁面的使用者會看到空的 HTTP 403 回應。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-204">By default, users who lack authorization to access a page are presented with an empty HTTP 403 response.</span></span> <span data-ttu-id="5b7fe-205">[StatusCodePages 中介軟體](xref:fundamentals/error-handling#configure-status-code-pages)可以設定為使用者提供更好的 「 拒絕存取 」 體驗。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-205">The [StatusCodePages middleware](xref:fundamentals/error-handling#configure-status-code-pages) can be configured to provide users with a better "Access Denied" experience.</span></span>

#### <a name="iis"></a><span data-ttu-id="5b7fe-206">IIS</span><span class="sxs-lookup"><span data-stu-id="5b7fe-206">IIS</span></span>

<span data-ttu-id="5b7fe-207">如果使用 IIS，請將下列內容加入`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="5b7fe-207">If using IIS, add the following to the `ConfigureServices` method:</span></span>

```csharp
// IISDefaults requires the following import:
// using Microsoft.AspNetCore.Server.IISIntegration;
services.AddAuthentication(IISDefaults.AuthenticationScheme);
```

#### <a name="httpsys"></a><span data-ttu-id="5b7fe-208">HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="5b7fe-208">HTTP.sys</span></span>

<span data-ttu-id="5b7fe-209">如果使用 HTTP.sys，將下列內容加入`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="5b7fe-209">If using HTTP.sys, add the following to the `ConfigureServices` method:</span></span>

```csharp
// HttpSysDefaults requires the following import:
// using Microsoft.AspNetCore.Server.HttpSys;
services.AddAuthentication(HttpSysDefaults.AuthenticationScheme);
```

### <a name="impersonation"></a><span data-ttu-id="5b7fe-210">模擬</span><span class="sxs-lookup"><span data-stu-id="5b7fe-210">Impersonation</span></span>

<span data-ttu-id="5b7fe-211">ASP.NET Core 不會實作模擬。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-211">ASP.NET Core doesn't implement impersonation.</span></span> <span data-ttu-id="5b7fe-212">應用程式執行的所有要求，使用應用程式集區或處理序身分識別的應用程式的身分識別。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-212">Apps run with the app's identity for all requests, using app pool or process identity.</span></span> <span data-ttu-id="5b7fe-213">如果您需要明確地執行動作的使用者身分，使用[WindowsIdentity.RunImpersonated](xref:System.Security.Principal.WindowsIdentity.RunImpersonated*)中[終端機內嵌中介軟體](xref:fundamentals/middleware/index#create-a-middleware-pipeline-with-iapplicationbuilder)在`Startup.Configure`。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-213">If you need to explicitly perform an action on behalf of a user, use [WindowsIdentity.RunImpersonated](xref:System.Security.Principal.WindowsIdentity.RunImpersonated*) in a [terminal inline middleware](xref:fundamentals/middleware/index#create-a-middleware-pipeline-with-iapplicationbuilder) in `Startup.Configure`.</span></span> <span data-ttu-id="5b7fe-214">在此內容中執行單一動作，然後關閉 內容。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-214">Run a single action in this context and then close the context.</span></span>

[!code-csharp[](windowsauth/sample_snapshot/Startup.cs?highlight=10-19)]

<span data-ttu-id="5b7fe-215">`RunImpersonated` 不支援非同步作業，而不應該用於複雜的案例。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-215">`RunImpersonated` doesn't support asynchronous operations and shouldn't be used for complex scenarios.</span></span> <span data-ttu-id="5b7fe-216">比方說，包裝整個要求或中介軟體鏈結不支援或建議。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-216">For example, wrapping entire requests or middleware chains isn't supported or recommended.</span></span>

### <a name="claims-transformations"></a><span data-ttu-id="5b7fe-217">宣告轉換</span><span class="sxs-lookup"><span data-stu-id="5b7fe-217">Claims transformations</span></span>

<span data-ttu-id="5b7fe-218">當 IIS 同處理序模式中，裝載<xref:Microsoft.AspNetCore.Authentication.AuthenticationService.AuthenticateAsync*>不在內部呼叫以初始化使用者。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-218">When hosting with IIS in-process mode, <xref:Microsoft.AspNetCore.Authentication.AuthenticationService.AuthenticateAsync*> isn't called internally to initialize a user.</span></span> <span data-ttu-id="5b7fe-219">因此，預設會在未啟動每個驗證之後，使用 <xref:Microsoft.AspNetCore.Authentication.IClaimsTransformation> 實作來轉換宣告。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-219">Therefore, an <xref:Microsoft.AspNetCore.Authentication.IClaimsTransformation> implementation used to transform claims after every authentication isn't activated by default.</span></span> <span data-ttu-id="5b7fe-220">如需裝載同處理序時，會啟用宣告轉換的程式碼範例和詳細資訊，請參閱<xref:host-and-deploy/aspnet-core-module#in-process-hosting-model>。</span><span class="sxs-lookup"><span data-stu-id="5b7fe-220">For more information and a code example that activates claims transformations when hosting in-process, see <xref:host-and-deploy/aspnet-core-module#in-process-hosting-model>.</span></span>
