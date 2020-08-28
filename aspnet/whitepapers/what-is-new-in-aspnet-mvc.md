---
uid: whitepapers/what-is-new-in-aspnet-mvc
title: ASP.NET MVC 2 的新功能 |Microsoft Docs
author: rick-anderson
description: 本檔說明 ASP.NET MVC 2 中引進的新功能和增強功能。 這份檔也可供下載。
ms.author: riande
ms.date: 04/20/2010
ms.assetid: 69a8d6f8-4b10-4602-8822-2d6c05fc432b
msc.legacyurl: /whitepapers/what-is-new-in-aspnet-mvc
msc.type: content
ms.openlocfilehash: ecc840c33714aa04bebcd9e413cb548eca8cc058
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045035"
---
# <a name="whats-new-in-aspnet-mvc-2"></a><span data-ttu-id="94338-104">ASP.NET MVC 2 的新功能</span><span class="sxs-lookup"><span data-stu-id="94338-104">What's New in ASP.NET MVC 2</span></span>

> <span data-ttu-id="94338-105">本檔說明 ASP.NET MVC 2 中引進的新功能和增強功能。</span><span class="sxs-lookup"><span data-stu-id="94338-105">This document describes new features and improvements introduced in ASP.NET MVC 2.</span></span> <span data-ttu-id="94338-106">這份檔也可供 [下載](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf)</span><span class="sxs-lookup"><span data-stu-id="94338-106">This document is also available for [Download](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf)</span></span>

<span data-ttu-id="94338-107">[介紹](#_TOC1) </span><span class="sxs-lookup"><span data-stu-id="94338-107">[Introduction](#_TOC1) </span></span>  
<span data-ttu-id="94338-108">[將 ASP.NET MVC 1.0 專案升級為 ASP.NET MVC 2](#_TOC2) </span><span class="sxs-lookup"><span data-stu-id="94338-108">[Upgrading an ASP.NET MVC 1.0 Project to ASP.NET MVC 2](#_TOC2) </span></span>  
<span data-ttu-id="94338-109">[新功能](#_TOC3) </span><span class="sxs-lookup"><span data-stu-id="94338-109">[New Features](#_TOC3) </span></span>  
<span data-ttu-id="94338-110">[樣板化協助程式](#_TOC3_1) </span><span class="sxs-lookup"><span data-stu-id="94338-110">[Templated Helpers](#_TOC3_1) </span></span>  
<span data-ttu-id="94338-111">[地區](#_TOC3_2) </span><span class="sxs-lookup"><span data-stu-id="94338-111">[Areas](#_TOC3_2) </span></span>  
<span data-ttu-id="94338-112">[支援非同步控制器](#_TOC3_3) </span><span class="sxs-lookup"><span data-stu-id="94338-112">[Support for Asynchronous Controllers](#_TOC3_3) </span></span>  
<span data-ttu-id="94338-113">[在動作方法參數中支援 DefaultValueAttribute](#_TOC3_4) </span><span class="sxs-lookup"><span data-stu-id="94338-113">[Support for DefaultValueAttribute in Action-Method Parameters](#_TOC3_4) </span></span>  
<span data-ttu-id="94338-114">[支援使用模型系結器來系結二進位資料](#_TOC3_5) </span><span class="sxs-lookup"><span data-stu-id="94338-114">[Support for Binding Binary Data with Model Binders](#_TOC3_5) </span></span>  
<span data-ttu-id="94338-115">[ModelMetadata 和 ModelMetadataProvider 類別](#_TOC3_6) </span><span class="sxs-lookup"><span data-stu-id="94338-115">[ModelMetadata and ModelMetadataProvider Classes](#_TOC3_6) </span></span>  
<span data-ttu-id="94338-116">[DataAnnotations 屬性的支援](#_TOC3_7) </span><span class="sxs-lookup"><span data-stu-id="94338-116">[Support for DataAnnotations Attributes](#_TOC3_7) </span></span>  
<span data-ttu-id="94338-117">[模型驗證程式提供者](#_TOC3_8) </span><span class="sxs-lookup"><span data-stu-id="94338-117">[Model-Validator Providers](#_TOC3_8) </span></span>  
<span data-ttu-id="94338-118">[用戶端驗證](#_TOC3_9) </span><span class="sxs-lookup"><span data-stu-id="94338-118">[Client-Side Validation](#_TOC3_9) </span></span>  
<span data-ttu-id="94338-119">[Visual Studio 2010 的新程式碼片段](#_TOC3_10) </span><span class="sxs-lookup"><span data-stu-id="94338-119">[New Code Snippets for Visual Studio 2010](#_TOC3_10) </span></span>  
<span data-ttu-id="94338-120">[新增 RequireHttpsAttribute 動作篩選](#_TOC3_11) </span><span class="sxs-lookup"><span data-stu-id="94338-120">[New RequireHttpsAttribute Action Filter](#_TOC3_11) </span></span>  
<span data-ttu-id="94338-121">[覆寫 HTTP 方法動詞](#_TOC3_12) </span><span class="sxs-lookup"><span data-stu-id="94338-121">[Overriding the HTTP Method Verb](#_TOC3_12) </span></span>  
<span data-ttu-id="94338-122">[樣板化 helper 的新 HiddenInputAttribute 類別](#_TOC3_13) </span><span class="sxs-lookup"><span data-stu-id="94338-122">[New HiddenInputAttribute Class for Templated Helpers](#_TOC3_13) </span></span>  
<span data-ttu-id="94338-123">[ValidationSummary Helper 方法可顯示模型層級錯誤](#_TOC3_14) </span><span class="sxs-lookup"><span data-stu-id="94338-123">[Html.ValidationSummary Helper Method Can Display Model-Level Errors](#_TOC3_14) </span></span>  
<span data-ttu-id="94338-124">[Visual Studio 中的 T4 範本會產生適用于 .NET Framework](#_TOC3_15)[API 改進](#_TOC4)目標版本的程式碼</span><span class="sxs-lookup"><span data-stu-id="94338-124">[T4 Templates in Visual Studio Generate Code that is Specific to the Target Version of the .NET Framework](#_TOC3_15)[API Improvements](#_TOC4)</span></span>  
[<span data-ttu-id="94338-125">重大變更</span><span class="sxs-lookup"><span data-stu-id="94338-125">Breaking Changes</span></span>](#_TOC5)  
[<span data-ttu-id="94338-126">免責聲明</span><span class="sxs-lookup"><span data-stu-id="94338-126">Disclaimer</span></span>](#_TOC6)  

## <a name="introduction"></a><a id="_TOC1"></a>  <span data-ttu-id="94338-127">介紹</span><span class="sxs-lookup"><span data-stu-id="94338-127">Introduction</span></span>

<span data-ttu-id="94338-128">ASP.NET MVC 2 建置於 ASP.NET MVC 1.0，並引進一組大量的增強功能和功能，著重于提升生產力。</span><span class="sxs-lookup"><span data-stu-id="94338-128">ASP.NET MVC 2 builds on ASP.NET MVC 1.0 and introduces a large set of enhancements and features that are focused on increasing productivity.</span></span> <span data-ttu-id="94338-129">此版本與 ASP.NET MVC 1.0 相容，因此您所有適用于 ASP.NET MVC 1.0 的知識、技能、程式碼和延伸模組都會繼續套用。</span><span class="sxs-lookup"><span data-stu-id="94338-129">This release is compatible with ASP.NET MVC 1.0, so all your knowledge, skills, code, and extensions for ASP.NET MVC 1.0 continue to apply.</span></span>

<span data-ttu-id="94338-130">如需有關 ASP.NET MVC 的詳細資訊，請造訪下列資源：</span><span class="sxs-lookup"><span data-stu-id="94338-130">For more information about ASP.NET MVC, visit the following resources:</span></span>

- [<span data-ttu-id="94338-131">MSDN 上的 ASP.NET MVC 檔</span><span class="sxs-lookup"><span data-stu-id="94338-131">ASP.NET MVC documentation on MSDN</span></span>](https://go.microsoft.com/fwlink/?LinkId=159758)
- [<span data-ttu-id="94338-132">ASP.NET MVC 網站</span><span class="sxs-lookup"><span data-stu-id="94338-132">The ASP.NET MVC Web site</span></span>](https://asp.net/mvc/)
- [<span data-ttu-id="94338-133">ASP.NET MVC 論壇</span><span class="sxs-lookup"><span data-stu-id="94338-133">The ASP.NET MVC forums</span></span>](https://forums.asp.net/1146.aspx)

## <a name="upgrading-an-aspnet-mvc-10-project-to-aspnet-mvc-2"></a><a id="_TOC2"></a>  <span data-ttu-id="94338-134">將 ASP.NET MVC 1.0 專案升級為 ASP.NET MVC 2</span><span class="sxs-lookup"><span data-stu-id="94338-134">Upgrading an ASP.NET MVC 1.0 Project to ASP.NET MVC 2</span></span>

<span data-ttu-id="94338-135">ASP.NET MVC 2 可以與 ASP.NET MVC 1.0 並存安裝在同一部伺服器上，如此可讓應用程式開發人員選擇何時將 ASP.NET MVC 1.0 應用程式升級至 ASP.NET MVC 2。</span><span class="sxs-lookup"><span data-stu-id="94338-135">ASP.NET MVC 2 can be installed side by side with ASP.NET MVC 1.0 on the same server, which gives application developers flexibility in choosing when to upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2.</span></span> <span data-ttu-id="94338-136">如需有關如何升級的詳細資訊，請參閱將 [ASP.NET mvc 1.0 應用程式升級至 ASP.NET mvc 2](https://go.microsoft.com/fwlink/?LinkID=185459)的檔。</span><span class="sxs-lookup"><span data-stu-id="94338-136">For information on how to upgrade, see the document [Upgrading an ASP.NET MVC 1.0 Application to ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185459).</span></span>

## <a name="new-features"></a><a id="_TOC3"></a>  <span data-ttu-id="94338-137">新功能</span><span class="sxs-lookup"><span data-stu-id="94338-137">New Features</span></span>

<span data-ttu-id="94338-138">本節說明 MVC 2 版本中引進的功能。</span><span class="sxs-lookup"><span data-stu-id="94338-138">This section describes features that have been introduced in the MVC 2 release.</span></span>

### <a name="templated-helpers"></a><a id="_TOC3_1"></a>  <span data-ttu-id="94338-139">樣板化協助程式</span><span class="sxs-lookup"><span data-stu-id="94338-139">Templated Helpers</span></span>

<span data-ttu-id="94338-140">樣板化協助程式可讓您自動建立 HTML 專案的關聯，以便編輯和顯示資料類型。</span><span class="sxs-lookup"><span data-stu-id="94338-140">Templated helpers let you automatically associate HTML elements for edit and display with data types.</span></span> <span data-ttu-id="94338-141">例如，當 view 中顯示 system.string 類型的資料時，可以自動轉譯日期選擇器 UI 元素。</span><span class="sxs-lookup"><span data-stu-id="94338-141">For example, when data of type System.DateTime is displayed in a view, a date-picker UI element can be automatically rendered.</span></span> <span data-ttu-id="94338-142">這類似于欄位範本在 ASP.NET 動態資料中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="94338-142">This is similar to how field templates work in ASP.NET Dynamic Data.</span></span> <span data-ttu-id="94338-143">如需詳細資訊，請參閱使用樣板化 helper 在 MSDN 網站上 [顯示資料](https://go.microsoft.com/fwlink/?LinkId=159062) 。</span><span class="sxs-lookup"><span data-stu-id="94338-143">For more information, see [Using Templated Helpers to Display Data](https://go.microsoft.com/fwlink/?LinkId=159062) on the MSDN Web site.</span></span>

### <a name="areas"></a><a id="_TOC3_2"></a>  <span data-ttu-id="94338-144">地區</span><span class="sxs-lookup"><span data-stu-id="94338-144">Areas</span></span>

<span data-ttu-id="94338-145">區域可讓您將大型專案組織成多個較小的區段，以便管理大型 Web 應用程式的複雜度。</span><span class="sxs-lookup"><span data-stu-id="94338-145">Areas let you organize a large project into multiple smaller sections in order to manage the complexity of a large Web application.</span></span> <span data-ttu-id="94338-146">每個區段 ( 「區域」 ) 通常代表大型網站的個別區段，並可用來將相關聯的控制器和 views 集合分組。</span><span class="sxs-lookup"><span data-stu-id="94338-146">Each section ("area") typically represents a separate section of a large Web site and is used to group related sets of controllers and views.</span></span> <span data-ttu-id="94338-147">如需詳細資訊，請參閱 MSDN 網站上的逐步解說 [：依區域組織 ASP.NET MVC 應用程式](https://go.microsoft.com/fwlink/?LinkId=158978) 。</span><span class="sxs-lookup"><span data-stu-id="94338-147">For more information, see [Walkthrough: Organizing an ASP.NET MVC Application by Areas](https://go.microsoft.com/fwlink/?LinkId=158978) on the MSDN Web site.</span></span>

<span data-ttu-id="94338-148">若要建立新的區域，請在 [方案總管中，以滑鼠右鍵按一下專案，按一下 [新增]，然後按一下 [區域]。</span><span class="sxs-lookup"><span data-stu-id="94338-148">To create a new area, in Solution Explorer, right-click the project, click Add, and then click Area.</span></span> <span data-ttu-id="94338-149">這會顯示一個對話方塊，提示您輸入區功能變數名稱稱。</span><span class="sxs-lookup"><span data-stu-id="94338-149">This displays a dialog box that prompts you for the area name.</span></span> <span data-ttu-id="94338-150">輸入區功能變數名稱稱之後，Visual Studio 會將新區域新增至專案。</span><span class="sxs-lookup"><span data-stu-id="94338-150">After you enter the area name, Visual Studio adds a new area to the project.</span></span>

<span data-ttu-id="94338-151">下圖顯示具有兩個區域、系統管理員和 Blog 的專案範例版面配置。</span><span class="sxs-lookup"><span data-stu-id="94338-151">The following figure shows an example layout for a project with two areas, Admin and Blogs.</span></span>

![](what-is-new-in-aspnet-mvc/_static/image1.png)

<span data-ttu-id="94338-152">當您建立區域時，Visual Studio 會將衍生自 AreaRegistration 的類別加入至每個區域。</span><span class="sxs-lookup"><span data-stu-id="94338-152">When you create an area, Visual Studio adds a class that derives from AreaRegistration to each area.</span></span> <span data-ttu-id="94338-153">此類別是必要的，才能註冊區域和其路由，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="94338-153">This class is required in order to register the area and its routes, as shown in the following example:</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample1.cs)]

<span data-ttu-id="94338-154">ASP.NET MVC 2 的預設專案範本包含對 global.asax 檔案程式碼中 RegisterAllAreas 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="94338-154">The default project template for ASP.NET MVC 2 includes a call to the RegisterAllAreas method in the code for the Global.asax file.</span></span> <span data-ttu-id="94338-155">這個方法會藉由尋找衍生自 AreaRegistration 類別的所有類型、具現化類型的實例，然後在實例上呼叫 RegisterArea 方法，來註冊專案中的每個區域。</span><span class="sxs-lookup"><span data-stu-id="94338-155">This method registers each area in the project by looking for all types that derive from the AreaRegistration class, instantiating an instance of the type, and then calling the RegisterArea method on the instance.</span></span> <span data-ttu-id="94338-156">下列範例顯示如何完成這項操作。</span><span class="sxs-lookup"><span data-stu-id="94338-156">The following example shows how this is done.</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample2.cs)]

<span data-ttu-id="94338-157">如果您未藉由呼叫內容來指定 RegisterArea 方法中的命名空間。命名空間： Add 方法，預設會使用註冊類別的命名空間。</span><span class="sxs-lookup"><span data-stu-id="94338-157">If you do not specify the namespace in the RegisterArea method by calling the context.Namespaces.Add method, the namespace of the registration class is used by default.</span></span>

### <a name="support-for-asynchronous-controllers"></a><a id="_TOC3_3"></a>  <span data-ttu-id="94338-158">支援非同步控制器</span><span class="sxs-lookup"><span data-stu-id="94338-158">Support for Asynchronous Controllers</span></span>

<span data-ttu-id="94338-159">ASP.NET MVC 2 現在允許控制器以非同步方式處理要求。</span><span class="sxs-lookup"><span data-stu-id="94338-159">ASP.NET MVC 2 now allows controllers to process requests asynchronously.</span></span> <span data-ttu-id="94338-160">這可能會讓經常呼叫封鎖作業的伺服器 (例如網路要求) 來改為呼叫非封鎖的對應專案，進而提升效能。</span><span class="sxs-lookup"><span data-stu-id="94338-160">This can lead to performance gains by allowing servers which frequently call blocking operations (like network requests) to call non-blocking counterparts instead.</span></span> <span data-ttu-id="94338-161">如需詳細資訊，請參閱 MSDN 上的 [使用 ASP.NET MVC 中的非同步控制器](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx) 主題。</span><span class="sxs-lookup"><span data-stu-id="94338-161">For more information, see the [Using an Asynchronous Controller in ASP.NET MVC](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx) topic on MSDN.</span></span>

### <a name="support-for-defaultvalueattribute-in-action-method-parameters"></a><a id="_TOC3_4"></a>  <span data-ttu-id="94338-162">在動作方法參數中支援 DefaultValueAttribute</span><span class="sxs-lookup"><span data-stu-id="94338-162">Support for DefaultValueAttribute in Action-Method Parameters</span></span>

<span data-ttu-id="94338-163">ComponentModel. DefaultValueAttribute 類別允許將引數參數的預設值提供給動作方法。</span><span class="sxs-lookup"><span data-stu-id="94338-163">The System.ComponentModel.DefaultValueAttribute class allows a default value to be supplied for the argument parameter to an action method.</span></span> <span data-ttu-id="94338-164">例如，假設已定義下列預設路由：</span><span class="sxs-lookup"><span data-stu-id="94338-164">For example, assume that the following default route is defined:</span></span>

[!code-json[Main](what-is-new-in-aspnet-mvc/samples/sample3.txt)]

<span data-ttu-id="94338-165">也假設已定義下列控制器和動作方法：</span><span class="sxs-lookup"><span data-stu-id="94338-165">Also assume that the following controller and action method is defined:</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample4.cs)]

<span data-ttu-id="94338-166">下列任何一個要求 Url 都會叫用上述範例中所定義的 View 動作方法。</span><span class="sxs-lookup"><span data-stu-id="94338-166">Any of the following request URLs will invoke the View action method that is defined in the preceding example.</span></span>

- <span data-ttu-id="94338-167">/Article/View/123</span><span class="sxs-lookup"><span data-stu-id="94338-167">/Article/View/123</span></span>
- <span data-ttu-id="94338-168">/Article/View/123？ page = 1 (與先前的要求有效) </span><span class="sxs-lookup"><span data-stu-id="94338-168">/Article/View/123?page=1 (Effectively the same as the previous request)</span></span>
- <span data-ttu-id="94338-169">/Article/View/123？ page = 2</span><span class="sxs-lookup"><span data-stu-id="94338-169">/Article/View/123?page=2</span></span>

<span data-ttu-id="94338-170">如果沒有 DefaultValueAttribute 屬性，則上述清單中的第一個 URL 將無法運作，因為頁面引數是未提供值的不可為 null 實值型別。</span><span class="sxs-lookup"><span data-stu-id="94338-170">Without the DefaultValueAttribute attribute, the first URL from the preceding list would not work, because the page argument is a non-nullable value type whose value has not been provided.</span></span>

<span data-ttu-id="94338-171">如果您的程式碼是以 Visual Basic 2010 或 Visual c # 2010 撰寫，您可以使用選擇性參數，而不是 DefaultValueAttribute 屬性，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="94338-171">If your code is written in Visual Basic 2010 or Visual C# 2010, you can use optional parameters instead of the DefaultValueAttribute attribute, as shown in the following example:</span></span>

[!code-vb[Main](what-is-new-in-aspnet-mvc/samples/sample5.vb)]

### <a name="support-for-binding-binary-data-with-model-binders"></a><a id="_TOC3_5"></a>  <span data-ttu-id="94338-172">支援使用模型系結器來系結二進位資料</span><span class="sxs-lookup"><span data-stu-id="94338-172">Support for Binding Binary Data with Model Binders</span></span>

<span data-ttu-id="94338-173">Html 會有兩個新的多載，可將二進位值編碼為 base-64 編碼的字串：</span><span class="sxs-lookup"><span data-stu-id="94338-173">There are two new overloads of the Html.Hidden helper that encode binary values as base-64-encoded strings:</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample6.cs)]

<span data-ttu-id="94338-174">一般用途是在視圖中内嵌物件的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="94338-174">A typical use is to embed a timestamp for an object in the view.</span></span> <span data-ttu-id="94338-175">例如，您的應用程式可能包含下列產品物件：</span><span class="sxs-lookup"><span data-stu-id="94338-175">For example, your application might include the following Product object:</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample7.cs)]

<span data-ttu-id="94338-176">編輯表單可以轉譯表單中的時間戳記屬性，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="94338-176">An edit form can render the TimeStamp property in the form as shown in the following example:</span></span>

[!code-aspx[Main](what-is-new-in-aspnet-mvc/samples/sample8.aspx)]

<span data-ttu-id="94338-177">這項標記會轉譯隱藏的輸入專案，其時間戳記值為 base-64 編碼的字串，類似于下列範例：</span><span class="sxs-lookup"><span data-stu-id="94338-177">This markup renders a hidden input element with the timestamp value as a base-64-encoded string that resembles the following example:</span></span>

[!code-html[Main](what-is-new-in-aspnet-mvc/samples/sample9.html)]

<span data-ttu-id="94338-178">此表單可能會張貼至具有 Product 類型引數的動作方法，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="94338-178">This form might be posted to an action method that has an argument of type Product, as shown in the following example:</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample10.cs)]

<span data-ttu-id="94338-179">在動作方法中，TimeStamp 屬性已正確填入，因為張貼的 base-64 編碼的字串會轉換為位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="94338-179">In the action method, the TimeStamp property is populated correctly because the posted base-64-encoded string is converted to a byte array.</span></span>

### <a name="modelmetadata-and-modelmetadataprovider-classes"></a><a id="_TOC3_6"></a>  <span data-ttu-id="94338-180">ModelMetadata 和 ModelMetadataProvider 類別</span><span class="sxs-lookup"><span data-stu-id="94338-180">ModelMetadata and ModelMetadataProvider Classes</span></span>

<span data-ttu-id="94338-181">ModelMetadataProvider 類別會提供一個抽象概念，讓您能夠在視圖內取得模型的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="94338-181">The ModelMetadataProvider class provides an abstraction for obtaining metadata for the model within a view.</span></span> <span data-ttu-id="94338-182">MVC 2 包含的預設提供者，可讓 ComponentModel. DataAnnotations 命名空間中的屬性所公開的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="94338-182">MVC 2 includes a default provider that makes available the metadata that is exposed by the attributes in the System.ComponentModel.DataAnnotations namespace.</span></span> <span data-ttu-id="94338-183">您可以建立中繼資料提供者，以提供來自其他資料存放區的中繼資料，例如資料庫或 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="94338-183">It is possible to create metadata providers that provide metadata from other data stores, such as databases or XML files.</span></span>

<span data-ttu-id="94338-184">>viewdatadictionary 類別會公開 ModelMetadata 物件，其中包含由 ModelMetadataProvider 類別從模型中解壓縮的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="94338-184">The ViewDataDictionary class exposes a ModelMetadata object that contains the metadata that is extracted from the model by the ModelMetadataProvider class.</span></span> <span data-ttu-id="94338-185">這可讓樣板化協助程式取用此中繼資料，並據以調整其輸出。</span><span class="sxs-lookup"><span data-stu-id="94338-185">This enables the templated helpers to consume this metadata and adjust their output accordingly.</span></span>

<span data-ttu-id="94338-186">如需詳細資訊，請參閱 [ModelMetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) 和 [ModelMetadataProvider](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) 類別的檔。</span><span class="sxs-lookup"><span data-stu-id="94338-186">For more information, see the documentation for the [ModelMetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) and [ModelMetadataProvider](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) classes.</span></span>

### <a name="support-for-dataannotations-attributes"></a><a id="_TOC3_7"></a>  <span data-ttu-id="94338-187">DataAnnotations 屬性的支援</span><span class="sxs-lookup"><span data-stu-id="94338-187">Support for DataAnnotations Attributes</span></span>

<span data-ttu-id="94338-188">ASP.NET MVC 2 支援使用 RangeAttribute、RequiredAttribute、StringLengthAttribute 和 RegexAttribute 驗證屬性 (在 ComponentModel. DataAnnotations 命名空間中定義，) 當您系結至模型以便提供輸入驗證時。</span><span class="sxs-lookup"><span data-stu-id="94338-188">ASP.NET MVC 2 supports using the RangeAttribute, RequiredAttribute, StringLengthAttribute, and RegexAttribute validation attributes (defined in the System.ComponentModel.DataAnnotations namespace) when you bind to a model in order to provide input validation.</span></span>

<span data-ttu-id="94338-189">如需詳細資訊，請參閱 MSDN 網站上的 how [to：使用 DataAnnotations 屬性來驗證模型資料](https://go.microsoft.com/fwlink/?LinkId=159063) 。</span><span class="sxs-lookup"><span data-stu-id="94338-189">For more information, see [How to: Validate Model Data Using DataAnnotations Attributes](https://go.microsoft.com/fwlink/?LinkId=159063) on the MSDN Web site.</span></span> <span data-ttu-id="94338-190">您可以從下載說明如何使用這些屬性的範例專案 [https://go.microsoft.com/fwlink/?LinkId=157753](https://go.microsoft.com/fwlink/?LinkId=157753) 。</span><span class="sxs-lookup"><span data-stu-id="94338-190">A sample project that illustrates the use of these attributes is available for download at [https://go.microsoft.com/fwlink/?LinkId=157753](https://go.microsoft.com/fwlink/?LinkId=157753).</span></span>

### <a name="model-validator-providers"></a><a id="_TOC3_8"></a>  <span data-ttu-id="94338-191">模型驗證程式提供者</span><span class="sxs-lookup"><span data-stu-id="94338-191">Model-Validator Providers</span></span>

<span data-ttu-id="94338-192">模型驗證提供者類別表示提供模型之驗證邏輯的抽象概念。</span><span class="sxs-lookup"><span data-stu-id="94338-192">The model-validation provider class represents an abstraction that provides validation logic for the model.</span></span> <span data-ttu-id="94338-193">ASP.NET MVC 包含以 ComponentModel DataAnnotations 命名空間中包含的驗證屬性為基礎的預設提供者。</span><span class="sxs-lookup"><span data-stu-id="94338-193">ASP.NET MVC includes a default provider based on validation attributes that are included in the System.ComponentModel.DataAnnotations namespace.</span></span> <span data-ttu-id="94338-194">您也可以建立自己的驗證提供者，來定義自訂驗證規則，以及對模型進行驗證規則的自訂對應。</span><span class="sxs-lookup"><span data-stu-id="94338-194">You can also create your own validation providers that define custom validation rules and custom mappings of validation rules to the model.</span></span> <span data-ttu-id="94338-195">如需詳細資訊，請參閱 [ModelValidatorProvider](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx) 類別的檔。</span><span class="sxs-lookup"><span data-stu-id="94338-195">For more information, see the documentation for the [ModelValidatorProvider](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx) class.</span></span>

### <a name="client-side-validation"></a><a id="_TOC3_9"></a>  <span data-ttu-id="94338-196">用戶端驗證</span><span class="sxs-lookup"><span data-stu-id="94338-196">Client-Side Validation</span></span>

<span data-ttu-id="94338-197">模型驗證程式提供者類別會將驗證中繼資料以 JSON 序列化資料的形式公開給瀏覽器，以供用戶端驗證程式庫使用。</span><span class="sxs-lookup"><span data-stu-id="94338-197">The model-validator provider class exposes validation metadata to the browser in the form of JSON-serialized data that can be consumed by a client-side validation library.</span></span> <span data-ttu-id="94338-198">ASP.NET MVC 2 包含用戶端驗證程式庫和介面卡，可支援先前所述的 DataAnnotations 命名空間驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="94338-198">ASP.NET MVC 2 includes a client validation library and adapter that supports the DataAnnotations namespace validation attributes noted earlier.</span></span> <span data-ttu-id="94338-199">提供者類別也可讓您使用其他用戶端驗證程式庫，方法是撰寫可處理 JSON 資料和呼叫替代程式庫的介面卡。</span><span class="sxs-lookup"><span data-stu-id="94338-199">The provider class also enables you to use other client-validation libraries by writing an adapter that processes the JSON data and calls into the alternate library.</span></span>

### <a name="new-code-snippets-for-visual-studio-2010"></a><a id="_TOC3_10"></a>  <span data-ttu-id="94338-200">Visual Studio 2010 的新程式碼片段</span><span class="sxs-lookup"><span data-stu-id="94338-200">New Code Snippets for Visual Studio 2010</span></span>

<span data-ttu-id="94338-201">ASP.NET MVC 2 的一組 HTML 程式碼片段會隨 Visual Studio 2010 安裝。</span><span class="sxs-lookup"><span data-stu-id="94338-201">A set of HTML code snippets for ASP.NET MVC 2 is installed with Visual Studio 2010.</span></span> <span data-ttu-id="94338-202">若要查看這些程式碼片段的清單，請選取 [工具] 功能表中的 [程式碼片段管理員]。</span><span class="sxs-lookup"><span data-stu-id="94338-202">To view a list of these snippets, in the Tools menu, select Code Snippets Manager.</span></span> <span data-ttu-id="94338-203">針對 [語言] 選取 [HTML]，並針對 [位置] 選取 [ASP.NET MVC 2]。</span><span class="sxs-lookup"><span data-stu-id="94338-203">For the language, select HTML, and for location, select ASP.NET MVC 2.</span></span> <span data-ttu-id="94338-204">如需有關如何使用程式碼片段的詳細資訊，請參閱 Visual Studio 檔。</span><span class="sxs-lookup"><span data-stu-id="94338-204">For more information about how to use code snippets, see the Visual Studio documentation.</span></span>

### <a name="new-requirehttpsattribute-action-filter"></a><a id="_TOC3_11"></a>  <span data-ttu-id="94338-205">新增 RequireHttpsAttribute 動作篩選</span><span class="sxs-lookup"><span data-stu-id="94338-205">New RequireHttpsAttribute Action Filter</span></span>

<span data-ttu-id="94338-206">ASP.NET MVC 2 包含新的 RequireHttpsAttribute 類別，可套用至動作方法和控制器。</span><span class="sxs-lookup"><span data-stu-id="94338-206">ASP.NET MVC 2 includes a new RequireHttpsAttribute class that can be applied to action methods and controllers.</span></span> <span data-ttu-id="94338-207">根據預設，篩選器會將非 SSL (HTTP) 要求重新導向至啟用 SSL 的 (HTTPS) 對等專案。</span><span class="sxs-lookup"><span data-stu-id="94338-207">By default, the filter redirects a non-SSL (HTTP) request to the SSL-enabled (HTTPS) equivalent.</span></span>

### <a name="overriding-the-http-method-verb"></a><a id="_TOC3_12"></a>  <span data-ttu-id="94338-208">覆寫 HTTP 方法動詞</span><span class="sxs-lookup"><span data-stu-id="94338-208">Overriding the HTTP Method Verb</span></span>

<span data-ttu-id="94338-209">當您使用 REST 架構樣式來建立網站時，會使用 HTTP 指令動詞來判斷要對資源執行的動作。</span><span class="sxs-lookup"><span data-stu-id="94338-209">When you build a Web site by using the REST architectural style, HTTP verbs are used to determine which action to perform for a resource.</span></span> <span data-ttu-id="94338-210">REST 要求應用程式支援完整範圍的一般 HTTP 動詞命令，包括 GET、PUT、POST 和 DELETE。</span><span class="sxs-lookup"><span data-stu-id="94338-210">REST requires that applications support the full range of common HTTP verbs, including GET, PUT, POST, and DELETE.</span></span>

<span data-ttu-id="94338-211">ASP.NET MVC 2 包含新的屬性，您可以將這些屬性套用至動作方法和該功能精簡語法。</span><span class="sxs-lookup"><span data-stu-id="94338-211">ASP.NET MVC 2 includes new attributes that you can apply to action methods and that feature compact syntax.</span></span> <span data-ttu-id="94338-212">這些屬性可讓 ASP.NET MVC 根據 HTTP 指令動詞選取動作方法。</span><span class="sxs-lookup"><span data-stu-id="94338-212">These attributes enable ASP.NET MVC to select an action method based on the HTTP verb.</span></span> <span data-ttu-id="94338-213">在下列範例中，POST 要求會呼叫第一個動作方法，而 PUT 要求會呼叫第二個動作方法。</span><span class="sxs-lookup"><span data-stu-id="94338-213">In the following example, a POST request will call the first action method and a PUT request will call the second action method.</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample11.cs)]

<span data-ttu-id="94338-214">在舊版的 ASP.NET MVC 中，這些動作方法需要更詳細的語法，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="94338-214">In earlier versions of ASP.NET MVC, these action methods required more verbose syntax, as shown in the following example:</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample12.cs)]

<span data-ttu-id="94338-215">因為瀏覽器僅支援 GET 和 POST HTTP 動詞命令，所以不可能張貼到需要不同動詞的動作。</span><span class="sxs-lookup"><span data-stu-id="94338-215">Because browsers support only the GET and POST HTTP verbs, it is not possible to post to an action that requires a different verb.</span></span> <span data-ttu-id="94338-216">因此，您無法以原生方式支援所有的 RESTful 要求。</span><span class="sxs-lookup"><span data-stu-id="94338-216">Thus it is not possible to natively support all RESTful requests.</span></span>

<span data-ttu-id="94338-217">不過，若要在 POST 作業期間支援 RESTful 要求，ASP.NET MVC 2 引進了新的 HttpMethodOverride HTML helper 方法。</span><span class="sxs-lookup"><span data-stu-id="94338-217">However, to support RESTful requests during POST operations, ASP.NET MVC 2 introduces a new HttpMethodOverride HTML helper method.</span></span> <span data-ttu-id="94338-218">這個方法會轉譯隱藏的輸入專案，讓表單有效地模擬任何 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="94338-218">This method renders a hidden input element that causes the form to effectively emulate any HTTP method.</span></span> <span data-ttu-id="94338-219">例如，藉由使用 HttpMethodOverride HTML helper 方法，您可以將表單提交顯示為 PUT 或 DELETE 要求。</span><span class="sxs-lookup"><span data-stu-id="94338-219">For example, by using the HttpMethodOverride HTML helper method, you can have a form submission appear be a PUT or DELETE request.</span></span> <span data-ttu-id="94338-220">HttpMethodOverride 的行為會影響下列屬性：</span><span class="sxs-lookup"><span data-stu-id="94338-220">The behavior of HttpMethodOverride affects the following attributes:</span></span>

- <span data-ttu-id="94338-221">HttpPostAttribute</span><span class="sxs-lookup"><span data-stu-id="94338-221">HttpPostAttribute</span></span>
- <span data-ttu-id="94338-222">HttpPutAttribute</span><span class="sxs-lookup"><span data-stu-id="94338-222">HttpPutAttribute</span></span>
- <span data-ttu-id="94338-223">HttpGetAttribute</span><span class="sxs-lookup"><span data-stu-id="94338-223">HttpGetAttribute</span></span>
- <span data-ttu-id="94338-224">HttpDeleteAttribute</span><span class="sxs-lookup"><span data-stu-id="94338-224">HttpDeleteAttribute</span></span>
- <span data-ttu-id="94338-225">AcceptVerbsAttribute</span><span class="sxs-lookup"><span data-stu-id="94338-225">AcceptVerbsAttribute</span></span>

<span data-ttu-id="94338-226">隱藏的輸入專案的名稱為 X-HTTP-方法-覆寫，且其值設定為要模擬的 HTTP 動詞。</span><span class="sxs-lookup"><span data-stu-id="94338-226">The hidden input element has its name X-HTTP-Method-Override and its value set to the HTTP verb to emulate.</span></span> <span data-ttu-id="94338-227">您也可以在 HTTP 標頭中指定覆寫值，或以名稱/值組的形式在查詢字串值中指定覆寫值。</span><span class="sxs-lookup"><span data-stu-id="94338-227">The override value can also be specified in an HTTP header or in a query string value as a name/value pair.</span></span>

<span data-ttu-id="94338-228">只有當真正的要求是 POST 要求時，才能使用覆寫。</span><span class="sxs-lookup"><span data-stu-id="94338-228">The override can only be used when the real request is a POST request.</span></span> <span data-ttu-id="94338-229">使用任何其他 HTTP 動詞命令的要求將會忽略覆寫值。</span><span class="sxs-lookup"><span data-stu-id="94338-229">The override value will be ignored for requests that use any other HTTP verb.</span></span>

### <a name="new-hiddeninputattribute-class-for-templated-helpers"></a><a id="_TOC3_13"></a>  <span data-ttu-id="94338-230">樣板化 helper 的新 HiddenInputAttribute 類別</span><span class="sxs-lookup"><span data-stu-id="94338-230">New HiddenInputAttribute Class for Templated Helpers</span></span>

<span data-ttu-id="94338-231">您可以將新的 HiddenInputAttribute 屬性套用至模型屬性，以指出在編輯器範本中顯示模型時是否應該轉譯隱藏的輸入元素。</span><span class="sxs-lookup"><span data-stu-id="94338-231">You can apply the new HiddenInputAttribute attribute to a model property to indicate whether a hidden input element should be rendered when displaying the model in an editor template.</span></span> <span data-ttu-id="94338-232"> (屬性會設定 HiddenInput) 的隱含 UIHint 值。</span><span class="sxs-lookup"><span data-stu-id="94338-232">(The attribute sets an implicit UIHint value of HiddenInput).</span></span> <span data-ttu-id="94338-233">屬性的 DisplayValue 屬性可讓您指定值是否顯示在編輯器和顯示模式中。</span><span class="sxs-lookup"><span data-stu-id="94338-233">The attribute's DisplayValue property lets you specify whether the value is displayed in editor and display modes.</span></span> <span data-ttu-id="94338-234">當 DisplayValue 設定為 false 時，不會顯示任何內容，甚至是通常會在欄位周圍的 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="94338-234">When DisplayValue is set to false, nothing is displayed, not even the HTML markup that normally surrounds a field.</span></span> <span data-ttu-id="94338-235">DisplayValue 的預設值為 true。</span><span class="sxs-lookup"><span data-stu-id="94338-235">The default value for DisplayValue is true.</span></span>

<span data-ttu-id="94338-236">您可以在下列案例中使用 HiddenInputAttribute 屬性：</span><span class="sxs-lookup"><span data-stu-id="94338-236">You might use HiddenInputAttribute attribute in the following scenarios:</span></span>

- <span data-ttu-id="94338-237">當某個視圖可讓使用者編輯物件的識別碼時，必須顯示此值以及提供隱藏的輸入專案（包含舊識別碼），以便將它傳回給控制器。</span><span class="sxs-lookup"><span data-stu-id="94338-237">When a view lets users edit the ID of an object and it is necessary to display the value as well as to provide a hidden input element that contains the old ID so that it can be passed back to the controller.</span></span>
- <span data-ttu-id="94338-238">當某個視圖可讓使用者編輯永遠不會顯示的二進位屬性，例如 timestamp 屬性。</span><span class="sxs-lookup"><span data-stu-id="94338-238">When a view lets users edit a binary property that should never be displayed, such as a timestamp property.</span></span> <span data-ttu-id="94338-239">在此情況下，不會顯示值和周圍的 HTML 標籤 (例如標籤和值) 。</span><span class="sxs-lookup"><span data-stu-id="94338-239">In that case, the value and surrounding HTML markup (such as the label and value) are not displayed.</span></span>

<span data-ttu-id="94338-240">下列範例顯示如何使用 HiddenInputAttribute 類別。</span><span class="sxs-lookup"><span data-stu-id="94338-240">The following example shows how to use the HiddenInputAttribute class.</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample13.cs)]

<span data-ttu-id="94338-241">當屬性設定為 true (或未) 指定參數時，就會發生下列情況：</span><span class="sxs-lookup"><span data-stu-id="94338-241">When the attribute is set to true (or no parameter is specified), the following occurs:</span></span>

- <span data-ttu-id="94338-242">在 [顯示範本] 中，會轉譯標籤，並向使用者顯示值。</span><span class="sxs-lookup"><span data-stu-id="94338-242">In display templates, a label is rendered and the value is displayed to the user.</span></span>
- <span data-ttu-id="94338-243">在編輯器範本中，會轉譯標籤，並在隱藏的輸入元素中轉譯值。</span><span class="sxs-lookup"><span data-stu-id="94338-243">In editor templates, a label is rendered and the value is rendered in a hidden input element.</span></span>

<span data-ttu-id="94338-244">當屬性設定為 false 時，會發生下列情況：</span><span class="sxs-lookup"><span data-stu-id="94338-244">When the attribute is set to false, the following occurs:</span></span>

- <span data-ttu-id="94338-245">在 [顯示範本] 中，不會針對該欄位轉譯任何內容。</span><span class="sxs-lookup"><span data-stu-id="94338-245">In display templates, nothing is rendered for that field.</span></span>
- <span data-ttu-id="94338-246">在編輯器範本中，不會轉譯任何標籤，而是在隱藏的輸入元素中轉譯值。</span><span class="sxs-lookup"><span data-stu-id="94338-246">In editor templates, no label is rendered and the value is rendered in a hidden input element.</span></span>

### <a name="htmlvalidationsummary-helper-method-can-display-model-level-errors"></a><a id="_TOC3_14"></a>  <span data-ttu-id="94338-247">ValidationSummary Helper 方法可顯示模型層級錯誤</span><span class="sxs-lookup"><span data-stu-id="94338-247">Html.ValidationSummary Helper Method Can Display Model-Level Errors</span></span>

<span data-ttu-id="94338-248">ValidationSummary helper 方法的新選項只顯示模型層級錯誤，而不是一律顯示所有驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="94338-248">Instead of always displaying all validation errors, the Html.ValidationSummary helper method has a new option to display only model-level errors.</span></span> <span data-ttu-id="94338-249">這可讓模型層級的錯誤顯示在驗證摘要中，並在每個欄位旁顯示欄位特定的錯誤。</span><span class="sxs-lookup"><span data-stu-id="94338-249">This enables model-level errors to be displayed in the validation summary and field-specific errors to be displayed next to each field.</span></span>

### <a name="t4-templates-in-visual-studio-generate-code-that-is-specific-to-the-target-version-of-the-net-framework"></a><a id="_TOC3_15"></a>  <span data-ttu-id="94338-250">Visual Studio 中的 T4 範本會產生特定于目標版本的程式碼 .NET Framework</span><span class="sxs-lookup"><span data-stu-id="94338-250">T4 Templates in Visual Studio Generate Code that is Specific to the Target Version of the .NET Framework</span></span>

<span data-ttu-id="94338-251">ASP.NET MVC T4 主機中的 T4 檔案可使用新的屬性，指定應用程式所使用的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="94338-251">A new property is available to T4 files from the ASP.NET MVC T4 host that specifies the version of the .NET Framework that is used by the application.</span></span> <span data-ttu-id="94338-252">這可讓 T4 範本產生 .NET Framework 版本專用的程式碼和標記。</span><span class="sxs-lookup"><span data-stu-id="94338-252">This enables T4 templates to generate code and markup that is specific to a version of the .NET Framework.</span></span> <span data-ttu-id="94338-253">在 Visual Studio 2008 中，此值一律為 .NET 3.5。</span><span class="sxs-lookup"><span data-stu-id="94338-253">In Visual Studio 2008, the value is always .NET 3.5.</span></span> <span data-ttu-id="94338-254">在 Visual Studio 2010 中，此值為 .NET 3.5 或 .NET 4。</span><span class="sxs-lookup"><span data-stu-id="94338-254">In Visual Studio 2010, the value is either .NET 3.5 or .NET 4.</span></span>

## <a name="api-improvements"></a><a id="_TOC4"></a>  <span data-ttu-id="94338-255">API 改進</span><span class="sxs-lookup"><span data-stu-id="94338-255">API Improvements</span></span>

<span data-ttu-id="94338-256">本節描述現有 ASP.NET MVC 類型和成員的變更。</span><span class="sxs-lookup"><span data-stu-id="94338-256">This section describes changes to existing ASP.NET MVC types and members.</span></span>

- <span data-ttu-id="94338-257">在控制器類別中新增受保護的虛擬 CreateActionInvoker 方法。</span><span class="sxs-lookup"><span data-stu-id="94338-257">Added a protected virtual CreateActionInvoker method in the Controller class.</span></span> <span data-ttu-id="94338-258">此方法是由控制器的 ActionInvoker 屬性所叫用，如果尚未設定任何啟動程式，則可讓啟動程式的延遲具現化。</span><span class="sxs-lookup"><span data-stu-id="94338-258">This method is invoked by the ActionInvoker property of Controller and allows for lazy instantiation of the invoker if no invoker is already set.</span></span>
- <span data-ttu-id="94338-259">在 AuthorizeAttribute 類別中新增受保護的虛擬 HandleUnauthorizedRequest 方法。</span><span class="sxs-lookup"><span data-stu-id="94338-259">Added a protected virtual HandleUnauthorizedRequest method in the AuthorizeAttribute class.</span></span> <span data-ttu-id="94338-260">這會啟用衍生自 AuthorizeAttribute 的篩選器，以控制授權失敗時的行為。</span><span class="sxs-lookup"><span data-stu-id="94338-260">This enables filters that derive from AuthorizeAttribute to control the behavior when authorization fails.</span></span>
- <span data-ttu-id="94338-261">在 ValueProviderDictionary 類別中加入新增 (字串索引鍵、物件值) 方法。</span><span class="sxs-lookup"><span data-stu-id="94338-261">Added an Add(string key, object value) method in the ValueProviderDictionary class.</span></span> <span data-ttu-id="94338-262">這可讓您使用 ValueProviderDictionary 的字典初始化運算式語法，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="94338-262">This enables you to use the dictionary initializer syntax for ValueProviderDictionary, as in the following example:</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample14.cs)]

- <span data-ttu-id="94338-263">\_在 Sys. AjaxCoNtext 類別中加入 get 物件方法。</span><span class="sxs-lookup"><span data-stu-id="94338-263">Added a get\_object method in the Sys.Mvc.AjaxContext class.</span></span> <span data-ttu-id="94338-264">這是類似于 get data 方法的 JavaScript 方法 \_ ，但如果回應的內容類型為 application/json，get 物件就會傳回 \_ json 物件。</span><span class="sxs-lookup"><span data-stu-id="94338-264">This is a JavaScript method that is similar to the get\_data method, but if the content type of the response is application/json, get\_object returns the JSON object.</span></span>
- <span data-ttu-id="94338-265">在 AuthorizationCoNtext 類別中新增 ActionDescriptor 屬性。</span><span class="sxs-lookup"><span data-stu-id="94338-265">Added an ActionDescriptor property in the AuthorizationContext class.</span></span>
- <span data-ttu-id="94338-266">加入 UrlParameter。選擇性標記，可用來解決當表單貼文中沒有屬性時，系結至包含 ID 屬性的模型時，所發生的問題。</span><span class="sxs-lookup"><span data-stu-id="94338-266">Added a UrlParameter.Optional token that can be used to work around problems when binding to a model that contains an ID property when the property is absent in a form post.</span></span> <span data-ttu-id="94338-267">如需詳細資訊，請參閱 Phil Haack 的 blog 上的專案 [ASP.NET MVC 2 選擇性 URL 參數](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="94338-267">For more detail, see the entry [ASP.NET MVC 2 Optional URL Parameters](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx) on Phil Haack's blog.</span></span>

## <a name="breaking-changes"></a><a id="_TOC5"></a>  <span data-ttu-id="94338-268">重大變更</span><span class="sxs-lookup"><span data-stu-id="94338-268">Breaking Changes</span></span>

<span data-ttu-id="94338-269">下列變更可能會導致現有的 ASP.NET MVC 1.0 應用程式發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="94338-269">The following changes might cause errors in existing ASP.NET MVC 1.0 applications.</span></span>

#### <a name="change-in-property-validation-behavior-for-classes-that-implement-idataerrorinfo"></a><span data-ttu-id="94338-270">執行 IDataErrorInfo 之類別的屬性驗證行為變更</span><span class="sxs-lookup"><span data-stu-id="94338-270">Change in property validation behavior for classes that implement IDataErrorInfo</span></span>

<span data-ttu-id="94338-271">針對使用 IDataErrorInfo 來執行驗證的模型物件，不論是否已設定新值，都會驗證每個屬性。</span><span class="sxs-lookup"><span data-stu-id="94338-271">For model objects that use IDataErrorInfo to perform validation, every property is validated, regardless of whether a new value was set.</span></span> <span data-ttu-id="94338-272">在 ASP.NET MVC 1.0 中，只會驗證具有新值集的屬性。</span><span class="sxs-lookup"><span data-stu-id="94338-272">In ASP.NET MVC 1.0, only properties that had new values set were validated.</span></span> <span data-ttu-id="94338-273">在 ASP.NET MVC 2 中，只有在所有屬性驗證程式都成功時，才會呼叫 IDataErrorInfo 的 Error 屬性。</span><span class="sxs-lookup"><span data-stu-id="94338-273">In ASP.NET MVC 2, the Error property of IDataErrorInfo is called only if all the property validators were successful.</span></span>

#### <a name="iis-script-mapping-script-is-no-longer-available-in-the-installer"></a><span data-ttu-id="94338-274">安裝程式中已不再提供 IIS 腳本對應腳本</span><span class="sxs-lookup"><span data-stu-id="94338-274">IIS script mapping script is no longer available in the installer</span></span>

<span data-ttu-id="94338-275">IIS 腳本對應腳本是命令列腳本，用來為 IIS 6 和傳統模式的 IIS 7 設定腳本對應。</span><span class="sxs-lookup"><span data-stu-id="94338-275">The IIS script-mapping script is a command-line script that is used to configure script maps for IIS 6 and for IIS 7 in Classic mode.</span></span> <span data-ttu-id="94338-276">如果您使用 Visual Studio 程式開發伺服器或在整合模式中使用 IIS 7，則不需要腳本對應腳本。</span><span class="sxs-lookup"><span data-stu-id="94338-276">The script-mapping script is not needed if you use the Visual Studio Development Server or if you use IIS 7 in Integrated mode.</span></span> <span data-ttu-id="94338-277">這些腳本在 [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)上可作為個別不支援的下載。</span><span class="sxs-lookup"><span data-stu-id="94338-277">The scripts are available as a separate unsupported download on the [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack).</span></span>

#### <a name="the-htmlsubstitute-helper-method-in-mvc-futures-is-no-longer-available"></a><span data-ttu-id="94338-278">無法再使用 MVC 中的 Html 替代 helper 方法</span><span class="sxs-lookup"><span data-stu-id="94338-278">The Html.Substitute helper method in MVC Futures is no longer available</span></span>

<span data-ttu-id="94338-279">由於 MVC 視圖引擎轉譯行為的變更，因此，Html. 替代 helper 方法無法運作且已移除。</span><span class="sxs-lookup"><span data-stu-id="94338-279">Due to changes in the rendering behavior of MVC view engines, the Html.Substitute helper method does not work and has been removed.</span></span>

#### <a name="the-ivalueprovider-interface-replaces-all-uses-of-idictionary"></a><span data-ttu-id="94338-280">IValueProvider 介面會取代 IDictionary 的所有用途</span><span class="sxs-lookup"><span data-stu-id="94338-280">The IValueProvider interface replaces all uses of IDictionary</span></span>

<span data-ttu-id="94338-281">在 MVC 1.0 中接受 IDictionary 的每個屬性或方法引數現在都接受 IValueProvider。</span><span class="sxs-lookup"><span data-stu-id="94338-281">Every property or method argument that accepted IDictionary in MVC 1.0 now accepts IValueProvider.</span></span> <span data-ttu-id="94338-282">這種變更只會影響包含自訂值提供者或自訂模型系結器的應用程式。</span><span class="sxs-lookup"><span data-stu-id="94338-282">This change affects only applications that include custom value providers or custom model binders.</span></span> <span data-ttu-id="94338-283">受此變更影響的屬性和方法的範例包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="94338-283">Examples of properties and methods that are affected by this change include the following:</span></span>

- <span data-ttu-id="94338-284">ControllerBase 和 ModelBindingCoNtext 類別的 ValueProvider 屬性。</span><span class="sxs-lookup"><span data-stu-id="94338-284">The ValueProvider property of the ControllerBase and ModelBindingContext classes.</span></span>
- <span data-ttu-id="94338-285">Controller 類別的 TryUpdateModel 方法。</span><span class="sxs-lookup"><span data-stu-id="94338-285">The TryUpdateModel methods of the Controller class.</span></span>

#### <a name="new-css-classes-were-added-in-the-sitecss-file"></a><span data-ttu-id="94338-286">已在網站 .css 檔案中新增 CSS 類別</span><span class="sxs-lookup"><span data-stu-id="94338-286">New CSS classes were added in the Site.css file</span></span>

<span data-ttu-id="94338-287">ASP.NET MVC 專案範本中的網站 .css 檔案已更新，可包含驗證功能和樣板化協助程式所使用的新樣式。</span><span class="sxs-lookup"><span data-stu-id="94338-287">The Site.css file in the ASP.NET MVC project templates has been updated to include new styles used by the validation functionality and by the templated helpers.</span></span>

#### <a name="helpers-now-return-an-mvchtmlstring-object"></a><span data-ttu-id="94338-288">Helper 現在會傳回 MvcHtmlString 物件</span><span class="sxs-lookup"><span data-stu-id="94338-288">Helpers now return an MvcHtmlString object</span></span>

<span data-ttu-id="94338-289">為了充分利用 ASP.NET 4 中的新 HTML 編碼運算式語法，HTML 協助程式的傳回型別現在是 MvcHtmlString，而不是字串。</span><span class="sxs-lookup"><span data-stu-id="94338-289">In order to take advantage of the new HTML-encoding expression syntax in ASP.NET 4, the return type for HTML helpers is now MvcHtmlString instead of a string.</span></span> <span data-ttu-id="94338-290">如果您使用 ASP.NET MVC 2 和 ASP.NET 3.5 上的新協助程式，您將無法利用 HTML 編碼語法;只有當您在 ASP.NET 4 上執行 ASP.NET MVC 2 時，才可使用新的語法。</span><span class="sxs-lookup"><span data-stu-id="94338-290">If you use ASP.NET MVC 2 and the new helpers on ASP.NET 3.5, you will not be able to take advantage of the HTML-encoding syntax; the new syntax is available only when you run ASP.NET MVC 2 on ASP.NET 4.</span></span>

#### <a name="jsonresult-now-responds-only-to-http-post-requests"></a><span data-ttu-id="94338-291">JsonResult 現在只會回應 HTTP POST 要求</span><span class="sxs-lookup"><span data-stu-id="94338-291">JsonResult now responds only to HTTP POST requests</span></span>

<span data-ttu-id="94338-292">為了減輕可能洩漏資訊的 JSON 劫持攻擊，JsonResult 類別預設只會回應 HTTP POST 要求。</span><span class="sxs-lookup"><span data-stu-id="94338-292">In order to mitigate JSON hijacking attacks that have the potential for information disclosure, by default, the JsonResult class now responds only to HTTP POST requests.</span></span> <span data-ttu-id="94338-293">傳回 JsonResult 物件之動作方法的 Ajax GET 呼叫，應改為使用 POST。</span><span class="sxs-lookup"><span data-stu-id="94338-293">Ajax GET calls to action methods that return a JsonResult object should be changed to use POST instead.</span></span> <span data-ttu-id="94338-294">如有必要，您可以藉由設定 JsonResult 的新 JsonRequestBehavior 屬性來覆寫此行為。</span><span class="sxs-lookup"><span data-stu-id="94338-294">If necessary, you can override this behavior by setting the new JsonRequestBehavior property of JsonResult.</span></span> <span data-ttu-id="94338-295">如需有關潛在惡意探索的詳細資訊，請參閱 Phil Haack 的 blog 上的 blog 文章 [JSON 劫持](http://haacked.com/archive/2009/06/25/json-hijacking.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="94338-295">For more information about the potential exploit, see the blog post [JSON Hijacking](http://haacked.com/archive/2009/06/25/json-hijacking.aspx) on Phil Haack's blog.</span></span>

#### <a name="model-and-modeltype-property-setters-on-modelbindingcontext-are-obsolete"></a><span data-ttu-id="94338-296">ModelBindingCoNtext 上的模型和 ModelType 屬性 setter 已淘汰</span><span class="sxs-lookup"><span data-stu-id="94338-296">Model and ModelType property setters on ModelBindingContext are obsolete</span></span>

<span data-ttu-id="94338-297">新的可設定 ModelMetadata 屬性已新增至 ModelBindingCoNtext 類別。</span><span class="sxs-lookup"><span data-stu-id="94338-297">A new settable ModelMetadata property has been added to the ModelBindingContext class.</span></span> <span data-ttu-id="94338-298">新屬性會封裝模型和 ModelType 屬性。</span><span class="sxs-lookup"><span data-stu-id="94338-298">The new property encapsulates both the Model and the ModelType properties.</span></span> <span data-ttu-id="94338-299">雖然模型和 ModelType 屬性已過時，但為了回溯相容性，屬性 getter 仍可運作;它們會委派給 ModelMetadata 屬性以取得值。</span><span class="sxs-lookup"><span data-stu-id="94338-299">Although the Model and ModelType properties are obsolete, for backward compatibility the property getters still work; they delegate to the ModelMetadata property to retrieve the value.</span></span>

#### <a name="changes-to-the-defaultcontrollerfactory-class-break-custom-controller-factories-that-derive-from-it"></a><span data-ttu-id="94338-300">DefaultControllerFactory 類別的變更會中斷從其衍生的自訂控制器 factory</span><span class="sxs-lookup"><span data-stu-id="94338-300">Changes to the DefaultControllerFactory class break custom controller factories that derive from it</span></span>

<span data-ttu-id="94338-301">DefaultControllerFactory 類別是藉由移除 RequestCoNtext 屬性來修正。</span><span class="sxs-lookup"><span data-stu-id="94338-301">The DefaultControllerFactory class was fixed by removing the RequestContext property.</span></span> <span data-ttu-id="94338-302">為了取代這個屬性，要求內容實例會傳遞至受保護的虛擬 GetControllerInstance 和 GetControllerType 方法。</span><span class="sxs-lookup"><span data-stu-id="94338-302">In place of this property, the request context instance is passed to the protected virtual GetControllerInstance and GetControllerType methods.</span></span> <span data-ttu-id="94338-303">此變更會影響衍生自 DefaultControllerFactory 的自訂控制器 factory。</span><span class="sxs-lookup"><span data-stu-id="94338-303">This change affects custom controller factories that derive from DefaultControllerFactory.</span></span>

<span data-ttu-id="94338-304">自訂控制器工廠通常用來提供 ASP.NET MVC 應用程式的相依性插入。</span><span class="sxs-lookup"><span data-stu-id="94338-304">Custom controller factories are often used to provide dependency injection for ASP.NET MVC applications.</span></span> <span data-ttu-id="94338-305">若要更新自訂控制器 factory 以支援 ASP.NET MVC 2，請將方法簽章或簽章變更為符合新的簽章，並使用要求內容參數，而非屬性。</span><span class="sxs-lookup"><span data-stu-id="94338-305">To update the custom controller factories to support ASP.NET MVC 2, change the method signature or signatures to match the new signatures, and use the request context parameter instead of the property.</span></span>

#### <a name="area-is-a-now-a-reserved-route-value-key"></a><span data-ttu-id="94338-306">「Area」現在是保留的路由值索引鍵</span><span class="sxs-lookup"><span data-stu-id="94338-306">"Area" is a now a reserved route-value key</span></span>

<span data-ttu-id="94338-307">路由值中的字串 "area" 現在在 ASP.NET MVC 中具有特殊意義，方法與「控制器」和「動作」相同。</span><span class="sxs-lookup"><span data-stu-id="94338-307">The string "area" in Route values now has special meaning in ASP.NET MVC, in the same way that "controller" and "action" do.</span></span> <span data-ttu-id="94338-308">其中一種方式是，如果 HTML 協助程式是以包含「區域」的路由值字典提供，則協助專家將不再于查詢字串中附加「區域」。</span><span class="sxs-lookup"><span data-stu-id="94338-308">One implication is that if HTML helpers are supplied with a route-value dictionary containing "area", the helpers will no longer append "area" in the query string.</span></span>

<span data-ttu-id="94338-309">如果您使用區域功能，請務必不要使用 {area} 做為路由 URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="94338-309">If you are using the Areas feature, make sure to not use {area} as part of your route URL.</span></span>

## <a name="disclaimer"></a><a id="_TOC6"></a>  <span data-ttu-id="94338-310">免責 聲明</span><span class="sxs-lookup"><span data-stu-id="94338-310">Disclaimer</span></span>

<span data-ttu-id="94338-311">這是一份初稿，內容在本文所述的軟體於正式商業發行前都可能有所更動。</span><span class="sxs-lookup"><span data-stu-id="94338-311">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="94338-312">本文件所含的資訊代表 Microsoft Corporation 在發行日當下對問題的看法。</span><span class="sxs-lookup"><span data-stu-id="94338-312">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="94338-313">由於 Microsoft 必須因應不斷變化的市場狀況，因此不應將此解讀為 Microsoft 方面所作出的承諾，且 Microsoft 也無法保證在發行日之後所提出任何資訊的正確性。</span><span class="sxs-lookup"><span data-stu-id="94338-313">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="94338-314">本技術白皮書僅供參考。</span><span class="sxs-lookup"><span data-stu-id="94338-314">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="94338-315">MICROSOFT 對本文件中的資訊不提供任何明示、暗示或法定擔保。</span><span class="sxs-lookup"><span data-stu-id="94338-315">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="94338-316">遵守所有適用之著作權法係使用者的責任。</span><span class="sxs-lookup"><span data-stu-id="94338-316">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="94338-317">在不限制任何依著作權本得享有之權利，未經 Microsoft Corporation 書面許可， 貴用戶不得為任何目的使用任何形式或方法 (電子形式、機械形式、影印、記錄或其他方式) 複製或傳送本文件的任何部份，也不得將本文件的任何部份儲存或放入檢索系統 (a retrieval system)。</span><span class="sxs-lookup"><span data-stu-id="94338-317">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="94338-318">在本文件所提述之內容中，可能包括 Microsoft 的專利、申請專利案件、商標、著作權，或其他智慧財產權等。</span><span class="sxs-lookup"><span data-stu-id="94338-318">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="94338-319">除非於 Microsoft 提出的任何書面授權條約中明確規定者外，提供本文件並不表示賦予台端上述專利、商標、著作權或其他智慧財產權等之任何授權。</span><span class="sxs-lookup"><span data-stu-id="94338-319">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="94338-320">除非另有說明，否則此處所描述的範例公司、組織、產品、功能變數名稱、電子郵件地址、標誌、人員、地點及事件均屬虛構，且不會與任何真實的公司、組織、產品、功能變數名稱、電子郵件地址、標誌、人員、地點或事件相關。</span><span class="sxs-lookup"><span data-stu-id="94338-320">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="94338-321">© 2010 Microsoft Corporation。</span><span class="sxs-lookup"><span data-stu-id="94338-321">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="94338-322">著作權所有，並保留一切權利。</span><span class="sxs-lookup"><span data-stu-id="94338-322">All rights reserved.</span></span>

<span data-ttu-id="94338-323">Microsoft 和 Windows 是 Microsoft Corporation 在美國及/或其他國家/地區的註冊商標或商標。</span><span class="sxs-lookup"><span data-stu-id="94338-323">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="94338-324">本文件中所提實際公司和產品，可能為各所有人所有之商標。</span><span class="sxs-lookup"><span data-stu-id="94338-324">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
