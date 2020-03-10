---
uid: ajax/cdn/overview
title: Microsoft Ajax 內容傳遞網路 |Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 92fa428608d4ac2bf56d3c6dc9c50f1449295869
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544510"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="ca6e2-102">Microsoft Ajax 內容傳遞網路</span><span class="sxs-lookup"><span data-stu-id="ca6e2-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="ca6e2-103">生產應用程式不應該對 CDN 資產採取硬式相依性。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="ca6e2-104">應用程式應該測試所參考的 CDN 資產，並在 CDN 無法使用時，使用 fallback 資產。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="ca6e2-105">Microsoft Ajax CDN 除了使用 Azure CDN 以外，不提供任何 SLA。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="ca6e2-106">使用[此 GitHub 問題](https://github.com/dotnet/AspNetDocs/issues/116)報告 MICROSOFT Ajax CDN 的問題。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-106">Use [this GitHub issue](https://github.com/dotnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="ca6e2-107">目錄</span><span class="sxs-lookup"><span data-stu-id="ca6e2-107">Table of Contents</span></span>

<span data-ttu-id="ca6e2-108">**[ajax.microsoft.com 已重新命名為 ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="ca6e2-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="ca6e2-109">**[Visual Studio vsdoc 支援](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="ca6e2-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="ca6e2-110">**[從 CDN 使用 ASP.NET Ajax](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="ca6e2-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="ca6e2-111">**[使用來自 CDN 的 jQuery](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="ca6e2-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="ca6e2-112">**[從 CDN 使用 jQuery UI](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="ca6e2-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="ca6e2-113">**[CDN 上的協力廠商檔案](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="ca6e2-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="ca6e2-114">CDN 上的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="ca6e2-115">在 CDN 上的 jQuery 遷移版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="ca6e2-116">CDN 上的 jQuery UI 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="ca6e2-117">CDN 上的 jQuery 驗證版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="ca6e2-118">CDN 上的 jQuery Mobile 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="ca6e2-119">CDN 上的 jQuery 範本版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="ca6e2-120">CDN 上的 jQuery 週期版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="ca6e2-121">CDN 上的 jQuery Datatable 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="ca6e2-122">CDN 上的 Modernizr 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="ca6e2-123">CDN 上的 JSHint 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="ca6e2-124">CDN 上的挖釋版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="ca6e2-125">CDN 上的全球化版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="ca6e2-126">在 CDN 上回應版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="ca6e2-127">CDN 上的啟動程式版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="ca6e2-128">CDN 上的啟動程式 TouchCarousel 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="ca6e2-129">CDN 上的 Hammer 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="ca6e2-130">在 CDN 上 ASP.NET Web Forms 和 Ajax 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="ca6e2-131">在 CDN 上 ASP.NET MVC 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="ca6e2-132">CDN 上的 ASP.NET SignalR 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="ca6e2-133">Microsoft Ajax 內容傳遞網路（CDN）裝載熱門的協力廠商 JavaScript 程式庫（例如 jQuery），可讓您輕鬆地將它們新增至您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="ca6e2-134">例如，您可以開始使用在此 CDN 上裝載的 jQuery，只要將 &lt;腳本&gt; 標記新增至指向 ajax.aspnetcdn.com 的頁面即可。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="ca6e2-135">藉由利用 CDN，您可以大幅提升 Ajax 應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="ca6e2-136">CDN 的內容會在位於世界各地的伺服器上進行快取。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="ca6e2-137">此外，CDN 可讓瀏覽器針對位於不同網域的網站重複使用已快取的協力廠商 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="ca6e2-138">如果您需要使用安全通訊端層來服務網頁，CDN 會支援 SSL （HTTPS）。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="ca6e2-139">CDN 會裝載下列協力廠商的腳本程式庫，這些程式庫已上傳，並由這些程式庫的擁有者授權給您：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="ca6e2-140">jQuery （ www.jquery.com）</span><span class="sxs-lookup"><span data-stu-id="ca6e2-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="ca6e2-141">jQuery UI （ www.jqueryui.com）</span><span class="sxs-lookup"><span data-stu-id="ca6e2-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="ca6e2-142">jQuery Mobile （ www.jquerymobile.com）</span><span class="sxs-lookup"><span data-stu-id="ca6e2-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="ca6e2-143">jQuery 驗證（ https://jqueryvalidation.org/)</span><span class="sxs-lookup"><span data-stu-id="ca6e2-143">jQuery Validation (https://jqueryvalidation.org/)</span></span>
- <span data-ttu-id="ca6e2-144">jQuery 迴圈（ www.malsup.com/jquery/cycle/）</span><span class="sxs-lookup"><span data-stu-id="ca6e2-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="ca6e2-145">jQuery Datatable （ http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="ca6e2-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="ca6e2-146">Microsoft Ajax CDN 也包含下列已由 Microsoft 上傳的程式庫：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="ca6e2-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="ca6e2-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="ca6e2-148">ASP.NET MVC JavaScript 檔案</span><span class="sxs-lookup"><span data-stu-id="ca6e2-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="ca6e2-149">ASP.NET SignalR JavaScript 檔案</span><span class="sxs-lookup"><span data-stu-id="ca6e2-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="ca6e2-150">Microsoft 不會宣告此 CDN 上主控之任何協力廠商程式庫的擁有權。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="ca6e2-151">程式庫的著作權擁有者會將這些程式庫授權給您。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="ca6e2-152">您可能必須下載並使用這類程式庫的任何權利，僅由個別著作權擁有者授與。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="ca6e2-153">因為這些不是 Microsoft 程式庫，所以 Microsoft 不會針對此 CDN 上所裝載的協力廠商程式庫提供任何擔保或智慧財產權授權（不含默示的專利權利）。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="ca6e2-154">如果您想要提交 JavaScript 程式庫，而您的程式庫是其中一個最上層的 JavaScript 程式庫（如 http://trends.builtwith.com) 或延伸模組/外掛程式上所列出的（a）常用; 或（b）有助於在 ASP.NET 上使用，請洽詢 AjaxCDNSubmission@Microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="ca6e2-155">ajax.microsoft.com 已重新命名為 ajax.aspnetcdn.com</span><span class="sxs-lookup"><span data-stu-id="ca6e2-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="ca6e2-156">用來使用 microsoft.com 功能變數名稱的 CDN，已變更為使用 aspnetcdn.com 功能變數名稱。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="ca6e2-157">這項變更是為了提升效能，因為當瀏覽器參考 microsoft.com 網域時，它會在每個要求的網路上，傳送來自該網域的任何 cookie。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="ca6e2-158">藉由重新命名為 microsoft.com 效能以外的功能變數名稱，最多可增加25%。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="ca6e2-159">請注意，ajax.microsoft.com 會繼續運作，但建議使用 ajax.aspnetcdn.com。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="ca6e2-160">舊格式： https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="ca6e2-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="ca6e2-161">新格式： https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="ca6e2-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="ca6e2-162">Visual Studio vsdoc 支援</span><span class="sxs-lookup"><span data-stu-id="ca6e2-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="ca6e2-163">若要搭配使用 vsdoc 檔案與 Visual Studio 2008，您必須確定已安裝 VS 2008 SP1 和 vsdoc 檔案的修復程式。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="ca6e2-164">您可以從這裡取得這些資訊：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-164">You can get these from here:</span></span>

- [<span data-ttu-id="ca6e2-165">下載 Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "下載 Visual Studio 2008 SP1")
- [<span data-ttu-id="ca6e2-166">下載 Visual Studio 2008 SP1 的 vsdoc 修補程式</span><span class="sxs-lookup"><span data-stu-id="ca6e2-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "下載 Visual Studio 2008 SP1 的 vsdoc 修補程式")

<span data-ttu-id="ca6e2-167">Visual Studio 2010 支援 vsdoc 檔案，而不需要任何額外的修補程式。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="ca6e2-168">從 CDN 使用 ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="ca6e2-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="ca6e2-169">使用 ASP.NET 4 時，您可以將 ASP.NET framework 腳本的所有要求重新導向至 CDN。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="ca6e2-170">從 CDN （而不是本機 web 伺服器）抓取腳本，可以大幅提升公用 ASP.NET 網站的效能。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="ca6e2-171">使用 ScriptManager EnableCDN 屬性將所有 ASP.NET framework 腳本要求重新導向至 Microsoft Ajax CDN：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="ca6e2-172">使用來自 CDN 的 jQuery</span><span class="sxs-lookup"><span data-stu-id="ca6e2-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="ca6e2-173">您可以在 Web 應用程式中使用裝載于 CDN 上的 jQuery 腳本，方法是將下列腳本元素新增至頁面：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="ca6e2-174">CDN 也包含 jQuery 腳本的縮減版本，您可以使用下列元素來取得此版本：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="ca6e2-175">若要允許您的頁面從您自己網站上的本機路徑載入 jQuery （如果 CDN 無法使用的話），請在參考 CDN 的元素之後立即新增下列元素：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="ca6e2-176">下列範例頁面使用 jQuery 程式庫的 CDN 版本（具有回溯至本機複本），以在按一下按鈕時顯示 div 元素的內容。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="ca6e2-177">您可以造訪[jquery](http://jquery.com/)網站，深入瞭解 jquery 並下載 jquery 的本機複本。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="ca6e2-178">從 CDN 使用 jQuery UI</span><span class="sxs-lookup"><span data-stu-id="ca6e2-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="ca6e2-179">CDN 也會主控 jQuery UI 程式庫。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="ca6e2-180">JQuery UI 程式庫包含一組豐富的 widget 和效果，可供您在 ASP.NET 應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="ca6e2-181">例如，下列頁面說明如何在 ASP.NET Web Forms 應用程式的內容中使用 jQuery UI Datepicker，以顯示快顯行事曆：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="ca6e2-182">當您使用鍵盤將焦點移到文字方塊時，會顯示行事曆：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![使用 Datepicker 建立的快顯行事曆](overview/_static/image1.png)

<span data-ttu-id="ca6e2-184">請注意，您必須在上述程式碼中包含來自 CDN 的三個檔案：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="ca6e2-185">Jquery UI 程式庫 &mdash; jQuery 程式庫相依于 jQuery 程式庫。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="ca6e2-186">您必須先將 jQuery 程式庫加入至頁面，然後再新增 jQuery UI 程式庫。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="ca6e2-187">Jquery ui 程式庫 &mdash; 的 jquery ui 程式庫包含所有 jQuery UI 效果和 widget，例如上述頁面中使用的 Datepicker 小工具。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="ca6e2-188">&mdash; jQuery UI 的 jQuery UI 主題支援不同的主題。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="ca6e2-189">上一頁包含用來匯入 Redmond 主題的 CSS 檔案連結。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="ca6e2-190">所有標準 jQuery UI 主題都裝載在 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="ca6e2-191">[請造訪此頁面](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.10")，以查看每個主題的縮圖。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="ca6e2-192">若要深入瞭解 jQuery UI 程式庫，請造訪官方[JQUERY ui 網站](http://jQueryUI.com "jQuery UI 網站")。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="ca6e2-193">CDN 上的協力廠商檔案</span><span class="sxs-lookup"><span data-stu-id="ca6e2-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="ca6e2-194">CDN 會裝載一些最受歡迎的協力廠商 JavaScript 程式庫。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="ca6e2-195">Microsoft 不會宣告此 CDN 上主控之任何協力廠商程式庫的擁有權。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="ca6e2-196">程式庫的著作權擁有者會將這些程式庫授權給您。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="ca6e2-197">您可能必須下載並使用這類程式庫的任何權利，僅由個別著作權擁有者授與。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="ca6e2-198">因為這些不是 Microsoft 程式庫，所以 Microsoft 不會針對此 CDN 上所裝載的協力廠商程式庫提供任何擔保或智慧財產權授權（不含默示的專利權利）。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-199">CDN 上的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-200">下列的 jQuery 版本裝載于 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-341"></a><span data-ttu-id="ca6e2-201">jQuery 版本3.4。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-201">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="ca6e2-202">jQuery 版本3.4。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-202">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="ca6e2-203">jQuery 版本3.3。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-203">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="ca6e2-204">jQuery 版本3.2。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-204">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="ca6e2-205">jQuery 版本3.2。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-205">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="ca6e2-206">jQuery 版本3.1。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-206">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="ca6e2-207">jQuery 版本3.1。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-207">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="ca6e2-208">jQuery 版本3.0。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-208">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="ca6e2-209">jQuery 版本2.2。4</span><span class="sxs-lookup"><span data-stu-id="ca6e2-209">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="ca6e2-210">jQuery 版本2.2。3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-210">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="ca6e2-211">jQuery 版本2.2。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-211">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="ca6e2-212">jQuery 版本2.2。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-212">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="ca6e2-213">jQuery 版本2.2。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-213">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="ca6e2-214">jQuery 版本2.1。4</span><span class="sxs-lookup"><span data-stu-id="ca6e2-214">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="ca6e2-215">jQuery 版本2.1。3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-215">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="ca6e2-216">jQuery 版本2.1。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-216">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="ca6e2-217">jQuery 版本2.1。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-217">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="ca6e2-218">jQuery 版本2.1。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-218">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="ca6e2-219">jQuery 版本2.0。3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-219">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="ca6e2-220">jQuery 版本2.0。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-220">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="ca6e2-221">jQuery 2.0.1 版</span><span class="sxs-lookup"><span data-stu-id="ca6e2-221">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="ca6e2-222">jQuery 版本2.0。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-222">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="ca6e2-223">jQuery 版本1.12。4</span><span class="sxs-lookup"><span data-stu-id="ca6e2-223">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="ca6e2-224">jQuery 版本1.12。3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-224">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="ca6e2-225">jQuery 版本1.12。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-225">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="ca6e2-226">jQuery 版本1.12。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-226">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="ca6e2-227">jQuery 版本1.12。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-227">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="ca6e2-228">jQuery 版本1.11。3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-228">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="ca6e2-229">jQuery 版本1.11。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-229">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="ca6e2-230">jQuery 版本1.11。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-230">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="ca6e2-231">jQuery 版本1.11。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-231">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="ca6e2-232">jQuery 版本1.10。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-232">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="ca6e2-233">jQuery 版本1.10.1 版</span><span class="sxs-lookup"><span data-stu-id="ca6e2-233">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="ca6e2-234">jQuery 版本1.10。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-234">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="ca6e2-235">jQuery 版本1.9。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-235">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="ca6e2-236">jQuery 版本1.9。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-236">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="ca6e2-237">jQuery 版本1.8。3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-237">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="ca6e2-238">jQuery 版本1.8。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-238">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="ca6e2-239">jQuery 版本1.8。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-239">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="ca6e2-240">jQuery 版本1.8。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-240">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="ca6e2-241">jQuery 版本1.7。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-241">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="ca6e2-242">jQuery 版本1.7。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-242">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="ca6e2-243">jQuery 版本1。7</span><span class="sxs-lookup"><span data-stu-id="ca6e2-243">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="ca6e2-244">jQuery 版本1.6。4</span><span class="sxs-lookup"><span data-stu-id="ca6e2-244">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="ca6e2-245">jQuery 版本1.6。3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-245">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="ca6e2-246">jQuery 版本1.6。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-246">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="ca6e2-247">jQuery 版本1.6。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-247">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="ca6e2-248">jQuery 版本1。6</span><span class="sxs-lookup"><span data-stu-id="ca6e2-248">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="ca6e2-249">jQuery 版本1.5。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-249">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="ca6e2-250">jQuery 版本1.5。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-250">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="ca6e2-251">jQuery 版本1。5</span><span class="sxs-lookup"><span data-stu-id="ca6e2-251">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="ca6e2-252">jQuery 版本1.4。4</span><span class="sxs-lookup"><span data-stu-id="ca6e2-252">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="ca6e2-253">jQuery 版本1.4。3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-253">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="ca6e2-254">jQuery 版本1.4。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-254">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="ca6e2-255">jQuery 版本1.4。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-255">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="ca6e2-256">jQuery 版本1。4</span><span class="sxs-lookup"><span data-stu-id="ca6e2-256">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="ca6e2-257">jQuery 版本1.3。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-257">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-258">在 CDN 上的 jQuery 遷移版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-258">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-259">下列 jQuery 遷移版本裝載于 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-259">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="ca6e2-260">jQuery 遷移版本3.0。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-260">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="ca6e2-261">jQuery 遷移1.2.1 版</span><span class="sxs-lookup"><span data-stu-id="ca6e2-261">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="ca6e2-262">jQuery 遷移版本1.2。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-262">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="ca6e2-263">jQuery 遷移1.1.1 版</span><span class="sxs-lookup"><span data-stu-id="ca6e2-263">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="ca6e2-264">jQuery 遷移版本1.1。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-264">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="ca6e2-265">jQuery 遷移1.0.0 版</span><span class="sxs-lookup"><span data-stu-id="ca6e2-265">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-266">CDN 上的 jQuery UI 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-266">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-267">下列的 jQuery UI 程式庫版本裝載于此 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-267">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="ca6e2-268">按一下每個連結，以查看實際的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-268">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="ca6e2-269">jQuery UI 1.12。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-269">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "Microsoft Ajax CDN 上的 jQuery UI 1.12.1")
- [<span data-ttu-id="ca6e2-270">jQuery UI 1.12。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-270">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "Microsoft Ajax CDN 上的 jQuery UI 1.12.0")
- [<span data-ttu-id="ca6e2-271">jQuery UI 1.11。4</span><span class="sxs-lookup"><span data-stu-id="ca6e2-271">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "Microsoft Ajax CDN 上的 jQuery UI 1.11.4")
- [<span data-ttu-id="ca6e2-272">jQuery UI 1.11。3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-272">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "Microsoft Ajax CDN 上的 jQuery UI 1.11.3")
- [<span data-ttu-id="ca6e2-273">jQuery UI 1.11。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-273">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "Microsoft Ajax CDN 上的 jQuery UI 1.11.2")
- [<span data-ttu-id="ca6e2-274">jQuery UI 1.11。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-274">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "Microsoft Ajax CDN 上的 jQuery UI 1.11.1")
- [<span data-ttu-id="ca6e2-275">jQuery UI 1.11。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-275">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "Microsoft Ajax CDN 上的 jQuery UI 1.11.0")
- [<span data-ttu-id="ca6e2-276">jQuery UI 1.10。4</span><span class="sxs-lookup"><span data-stu-id="ca6e2-276">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "Microsoft Ajax CDN 上的 jQuery UI 1.10.4")
- [<span data-ttu-id="ca6e2-277">jQuery UI 1.10。3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-277">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "Microsoft Ajax CDN 上的 jQuery UI 1.10.3")
- [<span data-ttu-id="ca6e2-278">jQuery UI 1.10。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-278">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "Microsoft Ajax CDN 上的 jQuery UI 1.10.2")
- [<span data-ttu-id="ca6e2-279">jQuery UI 1.10.1 版</span><span class="sxs-lookup"><span data-stu-id="ca6e2-279">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "Microsoft Ajax CDN 上的 jQuery UI 1.10.1")
- [<span data-ttu-id="ca6e2-280">jQuery UI 1.10。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-280">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "Microsoft Ajax CDN 上的 jQuery UI 1.10.0")
- [<span data-ttu-id="ca6e2-281">jQuery UI 1.9。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-281">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "Microsoft Ajax CDN 上的 jQuery UI 1.9.2")
- [<span data-ttu-id="ca6e2-282">jQuery UI 1.9。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-282">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "Microsoft Ajax CDN 上的 jQuery UI 1.9.1")
- [<span data-ttu-id="ca6e2-283">jQuery UI 1.9。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-283">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "Microsoft Ajax CDN 上的 jQuery UI 1.9.0")
- [<span data-ttu-id="ca6e2-284">jQuery UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="ca6e2-284">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.24")
- [<span data-ttu-id="ca6e2-285">jQuery UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="ca6e2-285">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.23")
- [<span data-ttu-id="ca6e2-286">jQuery UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="ca6e2-286">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.22")
- [<span data-ttu-id="ca6e2-287">jQuery UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="ca6e2-287">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.21")
- [<span data-ttu-id="ca6e2-288">jQuery UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="ca6e2-288">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.20")
- [<span data-ttu-id="ca6e2-289">jQuery UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="ca6e2-289">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.19")
- [<span data-ttu-id="ca6e2-290">jQuery UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="ca6e2-290">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.18")
- [<span data-ttu-id="ca6e2-291">jQuery UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="ca6e2-291">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.17")
- [<span data-ttu-id="ca6e2-292">jQuery UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="ca6e2-292">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.16")
- [<span data-ttu-id="ca6e2-293">jQuery UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="ca6e2-293">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.15")
- [<span data-ttu-id="ca6e2-294">jQuery UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="ca6e2-294">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.14")
- [<span data-ttu-id="ca6e2-295">jQuery UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="ca6e2-295">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.13")
- [<span data-ttu-id="ca6e2-296">jQuery UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="ca6e2-296">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.12")
- [<span data-ttu-id="ca6e2-297">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="ca6e2-297">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.11")
- [<span data-ttu-id="ca6e2-298">jQuery UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="ca6e2-298">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.10")
- [<span data-ttu-id="ca6e2-299">jQuery UI 1.8。9</span><span class="sxs-lookup"><span data-stu-id="ca6e2-299">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.9")
- [<span data-ttu-id="ca6e2-300">jQuery UI 1.8。8</span><span class="sxs-lookup"><span data-stu-id="ca6e2-300">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.8")
- [<span data-ttu-id="ca6e2-301">jQuery UI 1.8。7</span><span class="sxs-lookup"><span data-stu-id="ca6e2-301">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.7")
- [<span data-ttu-id="ca6e2-302">jQuery UI 1.8。6</span><span class="sxs-lookup"><span data-stu-id="ca6e2-302">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "Microsoft Ajax CDN 上的 jQuery UI 1.8.6")
- [<span data-ttu-id="ca6e2-303">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="ca6e2-303">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-304">CDN 上的 jQuery 驗證版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-304">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-305">下列的[JQuery 驗證](https://jqueryvalidation.org/ "jQuery 驗證外掛程式")外掛程式版本裝載于此 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-305">The following releases of the [jQuery Validation](https://jqueryvalidation.org/ "jQuery Validation Plugin") plugin are hosted on this CDN.</span></span> <span data-ttu-id="ca6e2-306">按一下每個連結，以查看實際的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-306">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="ca6e2-307">jQuery 驗證1.19。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-307">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "jQuery 驗證1.19。1")
- [<span data-ttu-id="ca6e2-308">jQuery 驗證1.19。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-308">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "jQuery 驗證1.19。0")
- [<span data-ttu-id="ca6e2-309">jQuery 驗證1.17.0 或</span><span class="sxs-lookup"><span data-stu-id="ca6e2-309">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery 驗證1.17.0 或")
- [<span data-ttu-id="ca6e2-310">jQuery 驗證1.16。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-310">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery 驗證 1.16.0")
- [<span data-ttu-id="ca6e2-311">jQuery 驗證 busybox-1.15.1-20.el6.x86 64.rpm</span><span class="sxs-lookup"><span data-stu-id="ca6e2-311">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery 驗證 1.15.1")
- [<span data-ttu-id="ca6e2-312">jQuery 驗證1.15。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-312">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery 驗證 1.15.0")
- [<span data-ttu-id="ca6e2-313">jQuery 驗證1.14。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-313">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery 驗證 1.14.0")
- [<span data-ttu-id="ca6e2-314">jQuery 驗證1.13。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-314">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery 驗證 1.13.1")
- [<span data-ttu-id="ca6e2-315">jQuery 驗證1.13。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-315">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery 驗證 1.13.0")
- [<span data-ttu-id="ca6e2-316">jQuery 驗證1.12。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-316">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery 驗證 1.12.0")
- [<span data-ttu-id="ca6e2-317">jQuery 驗證1.11。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-317">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery 驗證 1.11.1")
- [<span data-ttu-id="ca6e2-318">jQuery 驗證1.11。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-318">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery 驗證 1.11.0")
- [<span data-ttu-id="ca6e2-319">jQuery 驗證1.10。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-319">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery 驗證 1.10.0")
- [<span data-ttu-id="ca6e2-320">jQuery 驗證1。9</span><span class="sxs-lookup"><span data-stu-id="ca6e2-320">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate 1.9 版")
- [<span data-ttu-id="ca6e2-321">jQuery 驗證1.8。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-321">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate 1.8.1 版")
- [<span data-ttu-id="ca6e2-322">jQuery 驗證1。8</span><span class="sxs-lookup"><span data-stu-id="ca6e2-322">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate 1.8 版")
- [<span data-ttu-id="ca6e2-323">jQuery 驗證1。7</span><span class="sxs-lookup"><span data-stu-id="ca6e2-323">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate 1.7 版")
- [<span data-ttu-id="ca6e2-324">jQuery Validate 1.6</span><span class="sxs-lookup"><span data-stu-id="ca6e2-324">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery 驗證 1.6")
- [<span data-ttu-id="ca6e2-325">jQuery Validate 1.5.5</span><span class="sxs-lookup"><span data-stu-id="ca6e2-325">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery 驗證 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-326">CDN 上的 jQuery Mobile 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-326">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-327">下列的 jQuery Mobile 程式庫版本裝載于此 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-327">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="ca6e2-328">按一下每個連結，以查看實際的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-328">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="ca6e2-329">jQuery Mobile 1.4。5</span><span class="sxs-lookup"><span data-stu-id="ca6e2-329">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.4.5")
- [<span data-ttu-id="ca6e2-330">jQuery Mobile 1.4。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-330">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.4.2")
- [<span data-ttu-id="ca6e2-331">jQuery Mobile 1.4。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-331">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.4.1")
- [<span data-ttu-id="ca6e2-332">jQuery Mobile 1.4。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-332">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.4.0")
- [<span data-ttu-id="ca6e2-333">jQuery Mobile 1.3。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-333">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.3.2")
- [<span data-ttu-id="ca6e2-334">jQuery Mobile 1.3。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-334">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.3.1")
- [<span data-ttu-id="ca6e2-335">jQuery Mobile 1.3。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-335">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.3.0")
- [<span data-ttu-id="ca6e2-336">jQuery Mobile 1.2。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-336">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.2.0")
- [<span data-ttu-id="ca6e2-337">jQuery Mobile 1.1。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-337">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.1.2")
- [<span data-ttu-id="ca6e2-338">jQuery Mobile 1.1。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-338">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.1.1")
- [<span data-ttu-id="ca6e2-339">jQuery Mobile 1.1。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-339">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.1.0")
- [<span data-ttu-id="ca6e2-340">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-340">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.1.0 RC2")
- [<span data-ttu-id="ca6e2-341">jQuery Mobile 1.0。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-341">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.0.1")
- [<span data-ttu-id="ca6e2-342">jQuery Mobile 1。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-342">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.0")
- [<span data-ttu-id="ca6e2-343">jQuery Mobile 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-343">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="ca6e2-344">jQuery Mobile 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-344">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.0 RC1")
- <span data-ttu-id="ca6e2-345">[jQuery Mobile 1.0 Beta 3](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.0 搶鮮版 (Beta) 3")</span><span class="sxs-lookup"><span data-stu-id="ca6e2-345">[jQuery Mobile 1.0 beta 3](jquery-mobile/cdnjquerymobile10b3.md "jQuery Mobile 1.0 Beta 3 on the Microsoft Ajax CDN")</span></span>

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-346">CDN 上的 jQuery 範本版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-346">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-347">下列的 jQuery 範本外掛程式版本裝載于此 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-347">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="ca6e2-348">按一下每個連結，以查看實際的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-348">Click each link to see the actual list of files.</span></span>

- <span data-ttu-id="ca6e2-349">[jQuery 範本搶鮮版 (Beta) 1](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery 範本搶鮮版 (Beta) 1")</span><span class="sxs-lookup"><span data-stu-id="ca6e2-349">[jQuery Templates Beta 1](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery Templates Beta 1")</span></span>

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-350">CDN 上的 jQuery 週期版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-350">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-351">下列 jQuery 迴圈外掛程式版本裝載于此 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-351">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="ca6e2-352">按一下每個連結，以查看實際的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-352">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="ca6e2-353">jQuery Cycle 2.99</span><span class="sxs-lookup"><span data-stu-id="ca6e2-353">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery 循環 2.99")
- [<span data-ttu-id="ca6e2-354">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="ca6e2-354">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery 循環 2.94")
- [<span data-ttu-id="ca6e2-355">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="ca6e2-355">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery 循環 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-356">CDN 上的 jQuery Datatable 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-356">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-357">下列的 jQuery Datatable 外掛程式版本裝載于此 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-357">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="ca6e2-358">按一下每個連結，以查看實際的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-358">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="ca6e2-359">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="ca6e2-359">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="ca6e2-360">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="ca6e2-360">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="ca6e2-361">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="ca6e2-361">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="ca6e2-362">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-362">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="ca6e2-363">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-363">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="ca6e2-364">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-364">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="ca6e2-365">jQuery DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-365">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="ca6e2-366">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-366">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-367">CDN 上的 Modernizr 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-367">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-368">下列版本的[Modernizr](http://www.modernizr.com "Modernizr")裝載于 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-368">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-369">CDN 上的 JSHint 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-369">JSHint Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-370">下列版本的[JSHint](http://www.jshint.com "JSHint")裝載于 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-370">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-371">CDN 上的挖釋版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-371">Knockout Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-372">下列的[挖](http://www.knockoutjs.com "Knockout")的版本會裝載在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-372">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-373">CDN 上的全球化版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-373">Globalize Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-374">下列[全球](https://github.com/jquery/globalize "全球化")化版本裝載于 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-374">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="ca6e2-375">全球化1.0.0 版</span><span class="sxs-lookup"><span data-stu-id="ca6e2-375">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="ca6e2-376">全球化版本0.1。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-376">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="ca6e2-377">所有文化特性</span><span class="sxs-lookup"><span data-stu-id="ca6e2-377">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="ca6e2-378">以所需的文化特性代碼（例如全球化）取代 "{culture-code}"。 en-GB （CDN = = Microsoft Files）。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-378">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-379">在 CDN 上回應版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-379">Respond Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-380">下列的[回應](https://github.com/scottjehl/Respond "回應")版本裝載于 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-380">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="ca6e2-381">回應版本1.4。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-381">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="ca6e2-382">回應版本1.4。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-382">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="ca6e2-383">回應版本1.4。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-383">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="ca6e2-384">回應版本1.3。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-384">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="ca6e2-385">回應版本1.2。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-385">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-386">CDN 上的啟動程式版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-386">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-387">下列版本的[getbootstrap.com](http://getbootstrap.com "getbootstrap.com")啟動程式裝載于 CDN：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-387">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-441"></a><span data-ttu-id="ca6e2-388">啟動程式版本4.4。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-388">Bootstrap version 4.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-431"></a><span data-ttu-id="ca6e2-389">啟動程式版本4.3。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-389">Bootstrap version 4.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-421"></a><span data-ttu-id="ca6e2-390">啟動程式版本4.2。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-390">Bootstrap version 4.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-411"></a><span data-ttu-id="ca6e2-391">啟動程式版本4.1。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-391">Bootstrap version 4.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-400"></a><span data-ttu-id="ca6e2-392">啟動程式版本4.0。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-392">Bootstrap version 4.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-341"></a><span data-ttu-id="ca6e2-393">啟動程式版本3.4。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-393">Bootstrap version 3.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-340"></a><span data-ttu-id="ca6e2-394">啟動程式版本3.4。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-394">Bootstrap version 3.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="ca6e2-395">啟動程式版本3.3。7</span><span class="sxs-lookup"><span data-stu-id="ca6e2-395">Bootstrap version 3.3.7</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="ca6e2-396">啟動程式版本3.3。6</span><span class="sxs-lookup"><span data-stu-id="ca6e2-396">Bootstrap version 3.3.6</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="ca6e2-397">啟動程式版本3.3。5</span><span class="sxs-lookup"><span data-stu-id="ca6e2-397">Bootstrap version 3.3.5</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="ca6e2-398">啟動程式版本3.3。4</span><span class="sxs-lookup"><span data-stu-id="ca6e2-398">Bootstrap version 3.3.4</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="ca6e2-399">啟動程式版本3.3。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-399">Bootstrap version 3.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="ca6e2-400">啟動程式版本3.3。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-400">Bootstrap version 3.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="ca6e2-401">啟動程式版本3.3。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-401">Bootstrap version 3.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="ca6e2-402">啟動程式版本3.2。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-402">Bootstrap version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="ca6e2-403">啟動程式版本3.1。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-403">Bootstrap version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="ca6e2-404">啟動程式版本3.1。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-404">Bootstrap version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="ca6e2-405">啟動程式版本3.0。3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-405">Bootstrap version 3.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="ca6e2-406">啟動程式版本3.0。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-406">Bootstrap version 3.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="ca6e2-407">啟動程式版本3.0。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-407">Bootstrap version 3.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="ca6e2-408">啟動程式版本3.0。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-408">Bootstrap version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="ca6e2-409">啟動程式版本2.3。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-409">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="ca6e2-410">啟動程式2.3.1 版</span><span class="sxs-lookup"><span data-stu-id="ca6e2-410">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-411">CDN 上的啟動程式 TouchCarousel 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-411">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-412">下列版本的[https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "HTTPs://github.com/ixisio/bootstrap-touch-carousel")啟動程式 TouchCarousel 版本裝載于 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-412">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="ca6e2-413">啟動程式 TouchCarousel 版本0.8.0 版</span><span class="sxs-lookup"><span data-stu-id="ca6e2-413">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-414">CDN 上的 Hammer 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-414">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-415">下列[http://hammerjs.github.io/](http://hammerjs.github.io/ "HTTP://hammerjs.github.io/") Hammer 版本裝載于 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-415">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="ca6e2-416">Hammer .js 版本2.0.4 版</span><span class="sxs-lookup"><span data-stu-id="ca6e2-416">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-417">在 CDN 上 ASP.NET Web Forms 和 Ajax 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-417">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-418">下列版本的 ASP.NET Ajax 程式庫會裝載于 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-418">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="ca6e2-419">按一下每個連結，以查看實際的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-419">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="ca6e2-420">ASP.NET Web Forms 和 Ajax 版本4.5。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-420">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web Forms 與 Ajax 4.5.2")
- [<span data-ttu-id="ca6e2-421">ASP.NET Web Forms 和 Ajax 第4版</span><span class="sxs-lookup"><span data-stu-id="ca6e2-421">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web Forms 與 Ajax 4")
- [<span data-ttu-id="ca6e2-422">ASP.NET Ajax 3.5 版</span><span class="sxs-lookup"><span data-stu-id="ca6e2-422">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-423">在 CDN 上 ASP.NET MVC 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-423">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-424">下列 ASP.NET MVC JavaScript 檔案裝載于此 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-424">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="ca6e2-425">ASP.NET MVC 5.2。3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-425">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="ca6e2-426">ASP.NET MVC 5。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-426">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="ca6e2-427">ASP.NET MVC 5。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-427">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="ca6e2-428">ASP.NET MVC 4。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-428">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="ca6e2-429">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-429">ASP.NET MVC 3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.min.js 
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.js 
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="ca6e2-430">ASP.NET MVC 2。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-430">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="ca6e2-431">ASP.NET MVC 1。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-431">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="ca6e2-432">CDN 上的 ASP.NET SignalR 版本</span><span class="sxs-lookup"><span data-stu-id="ca6e2-432">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="ca6e2-433">下列 ASP.NET SignalR JavaScript 檔案裝載于此 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="ca6e2-433">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="ca6e2-434">ASP.NET SignalR 2.2。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-434">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="ca6e2-435">ASP.NET SignalR 2.2。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-435">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="ca6e2-436">ASP.NET SignalR 2.2。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-436">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="ca6e2-437">ASP.NET SignalR 2.1。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-437">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="ca6e2-438">ASP.NET SignalR 2.0。3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-438">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="ca6e2-439">ASP.NET SignalR 2.0。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-439">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="ca6e2-440">ASP.NET SignalR 2.0。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-440">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="ca6e2-441">ASP.NET SignalR 2.0。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-441">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="ca6e2-442">ASP.NET SignalR 1.1。3</span><span class="sxs-lookup"><span data-stu-id="ca6e2-442">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="ca6e2-443">ASP.NET SignalR 1.1。2</span><span class="sxs-lookup"><span data-stu-id="ca6e2-443">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="ca6e2-444">ASP.NET SignalR 1.1。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-444">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="ca6e2-445">ASP.NET SignalR 1.1。0</span><span class="sxs-lookup"><span data-stu-id="ca6e2-445">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="ca6e2-446">ASP.NET SignalR 1.0。1</span><span class="sxs-lookup"><span data-stu-id="ca6e2-446">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="ca6e2-447">如需 CDN 使用規定的相關資訊，請參閱[Microsoft AJAX CDN 使用](https://www.asp.net/terms-of-use "Microsoft Ajax CDN 使用規定")規定。</span><span class="sxs-lookup"><span data-stu-id="ca6e2-447">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
