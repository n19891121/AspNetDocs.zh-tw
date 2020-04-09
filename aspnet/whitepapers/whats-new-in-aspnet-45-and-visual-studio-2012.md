---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 和視覺工作室 2012 中的新增功能 |微軟文件
author: rick-anderson
description: 本文檔介紹 ASP.NET 4.5 中引入的新功能和增強功能。 它描述了為網頁開發所做的改進...
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676283"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a><span data-ttu-id="b0553-104">ASP.NET 4.5 與 Visual Studio 2012 的新功能</span><span class="sxs-lookup"><span data-stu-id="b0553-104">What's New in ASP.NET 4.5 and Visual Studio 2012</span></span>

> <span data-ttu-id="b0553-105">本文檔介紹 ASP.NET 4.5 中引入的新功能和增強功能。</span><span class="sxs-lookup"><span data-stu-id="b0553-105">This document describes new features and enhancements that are being introduced in ASP.NET 4.5.</span></span> <span data-ttu-id="b0553-106">它還描述了在 Visual Studio 2012 中為 Web 開發所做的改進。</span><span class="sxs-lookup"><span data-stu-id="b0553-106">It also describes improvements being made for web development in Visual Studio 2012.</span></span> <span data-ttu-id="b0553-107">本文檔最初發佈於 2012 年 2 月 29 日。</span><span class="sxs-lookup"><span data-stu-id="b0553-107">This document was originally published on February 29, 2012.</span></span>

- [<span data-ttu-id="b0553-108">ASP.NET核心執行時和框架</span><span class="sxs-lookup"><span data-stu-id="b0553-108">ASP.NET Core Runtime and Framework</span></span>](#_Toc318097372)

    - [<span data-ttu-id="b0553-109">非音子讀取與寫入 HTTP 要求與回應</span><span class="sxs-lookup"><span data-stu-id="b0553-109">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>](#_Toc318097373)
    - [<span data-ttu-id="b0553-110">HTTPRequest 處理的改進</span><span class="sxs-lookup"><span data-stu-id="b0553-110">Improvements to HttpRequest handling</span></span>](#_Toc318097374)
    - [<span data-ttu-id="b0553-111">同步刷新回應</span><span class="sxs-lookup"><span data-stu-id="b0553-111">Asynchronously flushing a response</span></span>](#_Toc318097375)
    - [<span data-ttu-id="b0553-112">支援*與*系統*建立工作的*非同步模組與處理程式</span><span class="sxs-lookup"><span data-stu-id="b0553-112">Support for *await* and *Task*-Based Asynchronous Modules and Handlers</span></span>](#_Toc318097376)
    - [<span data-ttu-id="b0553-113">非同步 HTTP 模組</span><span class="sxs-lookup"><span data-stu-id="b0553-113">Asynchronous HTTP modules</span></span>](#_Toc318097377)
    - [<span data-ttu-id="b0553-114">非同步 HTTP 處理程式</span><span class="sxs-lookup"><span data-stu-id="b0553-114">Asynchronous HTTP handlers</span></span>](#_Toc318097378)
    - [<span data-ttu-id="b0553-115">新的ASP.NET要求驗證功能</span><span class="sxs-lookup"><span data-stu-id="b0553-115">New ASP.NET Request Validation Features</span></span>](#_Toc318097379)
    - [<span data-ttu-id="b0553-116">延遲("延遲")請求驗證</span><span class="sxs-lookup"><span data-stu-id="b0553-116">Deferred ("lazy") request validation</span></span>](#_Toc318097380)
    - [<span data-ttu-id="b0553-117">支援未經認證的要求</span><span class="sxs-lookup"><span data-stu-id="b0553-117">Support for unvalidated requests</span></span>](#_Toc318097381)
    - [<span data-ttu-id="b0553-118">AntiXSS 函式庫</span><span class="sxs-lookup"><span data-stu-id="b0553-118">AntiXSS Library</span></span>](#_Toc318097382)
    - [<span data-ttu-id="b0553-119">支援 WebSocket 協定</span><span class="sxs-lookup"><span data-stu-id="b0553-119">Support for WebSockets Protocol</span></span>](#_Toc318097383)
    - [<span data-ttu-id="b0553-120">捆綁和最小化</span><span class="sxs-lookup"><span data-stu-id="b0553-120">Bundling and Minification</span></span>](#_Toc318097384)
    - [<span data-ttu-id="b0553-121">Web 託管的效能改進</span><span class="sxs-lookup"><span data-stu-id="b0553-121">Performance Improvements for Web Hosting</span></span>](#_Toc_perf)

        - [<span data-ttu-id="b0553-122">關鍵性能因素</span><span class="sxs-lookup"><span data-stu-id="b0553-122">Key Performance Factors</span></span>](#_Toc_perf_1)
        - [<span data-ttu-id="b0553-123">對新效能功能的要求</span><span class="sxs-lookup"><span data-stu-id="b0553-123">Requirements for New Performance Features</span></span>](#_Toc_perf_2)
        - [<span data-ttu-id="b0553-124">共用公共程式集</span><span class="sxs-lookup"><span data-stu-id="b0553-124">Sharing Common Assemblies</span></span>](#_Toc_perf_3)
        - [<span data-ttu-id="b0553-125">使用多核 JIT 編譯,加快啟動速度</span><span class="sxs-lookup"><span data-stu-id="b0553-125">Using multi-Core JIT compilation for faster startup</span></span>](#_Toc_perf_4)
        - [<span data-ttu-id="b0553-126">調整垃圾資源以最佳化記憶體</span><span class="sxs-lookup"><span data-stu-id="b0553-126">Tuning garbage collection to optimize for memory</span></span>](#_Toc_perf_5)
        - [<span data-ttu-id="b0553-127">為 Web 應用程式預取</span><span class="sxs-lookup"><span data-stu-id="b0553-127">Prefetching for web applications</span></span>](#_Toc_perf_6)
- [<span data-ttu-id="b0553-128">ASP.NET Web 表單</span><span class="sxs-lookup"><span data-stu-id="b0553-128">ASP.NET Web Forms</span></span>](#_Toc318097385)

    - [<span data-ttu-id="b0553-129">強型別資料控制項</span><span class="sxs-lookup"><span data-stu-id="b0553-129">Strongly Typed Data Controls</span></span>](#_Toc318097386)
    - [<span data-ttu-id="b0553-130">模型繫結</span><span class="sxs-lookup"><span data-stu-id="b0553-130">Model Binding</span></span>](#_Toc318097387)

        - [<span data-ttu-id="b0553-131">選擇資料</span><span class="sxs-lookup"><span data-stu-id="b0553-131">Selecting data</span></span>](#_Toc318097388)
        - [<span data-ttu-id="b0553-132">價值提供者</span><span class="sxs-lookup"><span data-stu-id="b0553-132">Value providers</span></span>](#_Toc318097389)
        - [<span data-ttu-id="b0553-133">依控制項的值篩選</span><span class="sxs-lookup"><span data-stu-id="b0553-133">Filtering by values from a control</span></span>](#_Toc318097390)
    - [<span data-ttu-id="b0553-134">HTML 編碼資料繫結表示式</span><span class="sxs-lookup"><span data-stu-id="b0553-134">HTML Encoded Data-Binding Expressions</span></span>](#_Toc318097391)
    - [<span data-ttu-id="b0553-135">不顯眼的驗證</span><span class="sxs-lookup"><span data-stu-id="b0553-135">Unobtrusive Validation</span></span>](#_Toc318097392)
    - [<span data-ttu-id="b0553-136">HTML5 更新</span><span class="sxs-lookup"><span data-stu-id="b0553-136">HTML5 Updates</span></span>](#_Toc318097393)
- [<span data-ttu-id="b0553-137">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="b0553-137">ASP.NET MVC 4</span></span>](#_Toc318097394)
- [<span data-ttu-id="b0553-138">ASP.NET Web Pages 2</span><span class="sxs-lookup"><span data-stu-id="b0553-138">ASP.NET Web Pages 2</span></span>](#_Toc318097395)
- [<span data-ttu-id="b0553-139">視覺工作室 2012 發佈候選</span><span class="sxs-lookup"><span data-stu-id="b0553-139">Visual Studio 2012 Release Candidate</span></span>](#_Toc318097396)

    - [<span data-ttu-id="b0553-140">Visual Studio 2010 和 Visual Studio 2012 版本候選版本之間的項目共享(專案相容性)</span><span class="sxs-lookup"><span data-stu-id="b0553-140">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>](#project-compatibility)
    - [<span data-ttu-id="b0553-141">ASP.NET 4.5 網站樣本中的設定變更</span><span class="sxs-lookup"><span data-stu-id="b0553-141">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [<span data-ttu-id="b0553-142">IIS 7 中用於ASP.NET路由的本機支援</span><span class="sxs-lookup"><span data-stu-id="b0553-142">Native Support in IIS 7 for ASP.NET Routing</span></span>](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [<span data-ttu-id="b0553-143">HTML 編輯器</span><span class="sxs-lookup"><span data-stu-id="b0553-143">HTML Editor</span></span>](#_Toc318097397)

        - [<span data-ttu-id="b0553-144">智慧任務</span><span class="sxs-lookup"><span data-stu-id="b0553-144">Smart Tasks</span></span>](#_Toc318097398)
        - [<span data-ttu-id="b0553-145">WAI-ARIA 支援</span><span class="sxs-lookup"><span data-stu-id="b0553-145">WAI-ARIA support</span></span>](#_Toc318097399)
        - [<span data-ttu-id="b0553-146">新的 HTML5 碼段</span><span class="sxs-lookup"><span data-stu-id="b0553-146">New HTML5 snippets</span></span>](#_Toc318097400)
        - [<span data-ttu-id="b0553-147">擷取使用者控制項</span><span class="sxs-lookup"><span data-stu-id="b0553-147">Extract to user control</span></span>](#_Toc318097401)
        - [<span data-ttu-id="b0553-148">屬性中片段的 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="b0553-148">IntelliSense for code nuggets in attributes</span></span>](#_Toc318097402)
        - [<span data-ttu-id="b0553-149">重新命名開啟或關閉標籤時自動重新命名符合標記</span><span class="sxs-lookup"><span data-stu-id="b0553-149">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>](#_Toc318097403)
        - [<span data-ttu-id="b0553-150">事件處理程式產生</span><span class="sxs-lookup"><span data-stu-id="b0553-150">Event handler generation</span></span>](#_Toc318097404)
        - [<span data-ttu-id="b0553-151">智慧縮排</span><span class="sxs-lookup"><span data-stu-id="b0553-151">Smart indent</span></span>](#_Toc318097405)
        - [<span data-ttu-id="b0553-152">自動減少敘述完成</span><span class="sxs-lookup"><span data-stu-id="b0553-152">Auto-reduce statement completion</span></span>](#_Toc318097406)
    - [<span data-ttu-id="b0553-153">JavaScript 編輯器</span><span class="sxs-lookup"><span data-stu-id="b0553-153">JavaScript Editor</span></span>](#_Toc318097407)

        - [<span data-ttu-id="b0553-154">代碼概述</span><span class="sxs-lookup"><span data-stu-id="b0553-154">Code outlining</span></span>](#_Toc318097408)
        - [<span data-ttu-id="b0553-155">括號對稱</span><span class="sxs-lookup"><span data-stu-id="b0553-155">Brace matching</span></span>](#_Toc318097409)
        - [<span data-ttu-id="b0553-156">跳到訂</span><span class="sxs-lookup"><span data-stu-id="b0553-156">Go to Definition</span></span>](#_Toc318097410)
        - [<span data-ttu-id="b0553-157">ECMAScript5 支援</span><span class="sxs-lookup"><span data-stu-id="b0553-157">ECMAScript5 support</span></span>](#_Toc318097411)
        - [<span data-ttu-id="b0553-158">DOM 感知</span><span class="sxs-lookup"><span data-stu-id="b0553-158">DOM IntelliSense</span></span>](#_Toc318097412)
        - [<span data-ttu-id="b0553-159">VSDOC 簽署重載</span><span class="sxs-lookup"><span data-stu-id="b0553-159">VSDOC signature overloads</span></span>](#_Toc318097413)
        - [<span data-ttu-id="b0553-160">隱含參考</span><span class="sxs-lookup"><span data-stu-id="b0553-160">Implicit references</span></span>](#_Toc318097414)
    - [<span data-ttu-id="b0553-161">CSS 編輯器</span><span class="sxs-lookup"><span data-stu-id="b0553-161">CSS Editor</span></span>](#_Toc318097415)

        - [<span data-ttu-id="b0553-162">自動減少敘述完成</span><span class="sxs-lookup"><span data-stu-id="b0553-162">Auto-reduce statement completion</span></span>](#_Toc318097416)
        - [<span data-ttu-id="b0553-163">分層縮進。</span><span class="sxs-lookup"><span data-stu-id="b0553-163">Hierarchical indentation.</span></span>](#_Toc318097417)
        - [<span data-ttu-id="b0553-164">CSS 駭客支援</span><span class="sxs-lookup"><span data-stu-id="b0553-164">CSS hacks support</span></span>](#_Toc318097418)
        - [<span data-ttu-id="b0553-165">供應商指定的架構(-moz-,-webkit)</span><span class="sxs-lookup"><span data-stu-id="b0553-165">Vendor specific schemas (-moz-,-webkit)</span></span>](#_Toc318097419)
        - [<span data-ttu-id="b0553-166">評論和非評論支援</span><span class="sxs-lookup"><span data-stu-id="b0553-166">Commenting and uncommenting support</span></span>](#_Toc318097420)
        - [<span data-ttu-id="b0553-167">Color picker</span><span class="sxs-lookup"><span data-stu-id="b0553-167">Color picker</span></span>](#_Toc318097421)
        - [<span data-ttu-id="b0553-168">程式碼片段</span><span class="sxs-lookup"><span data-stu-id="b0553-168">Snippets</span></span>](#_Toc318097422)
        - [<span data-ttu-id="b0553-169">自訂區域</span><span class="sxs-lookup"><span data-stu-id="b0553-169">Custom regions</span></span>](#_Toc318097423)
    - [<span data-ttu-id="b0553-170">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="b0553-170">Page Inspector</span></span>](#_Toc318097424)
    - [<span data-ttu-id="b0553-171">出版</span><span class="sxs-lookup"><span data-stu-id="b0553-171">Publishing</span></span>](#_Toc318097425)

        - [<span data-ttu-id="b0553-172">發佈設定檔</span><span class="sxs-lookup"><span data-stu-id="b0553-172">Publish profiles</span></span>](#_Toc318097426)
        - [<span data-ttu-id="b0553-173">ASP.NET 預寫和合併</span><span class="sxs-lookup"><span data-stu-id="b0553-173">ASP.NET precompilation and merge</span></span>](#_Toc318097427)
- [<span data-ttu-id="b0553-174">IIS Express</span><span class="sxs-lookup"><span data-stu-id="b0553-174">IIS Express</span></span>](#_Toc318097428)
- [<span data-ttu-id="b0553-175">免責聲明</span><span class="sxs-lookup"><span data-stu-id="b0553-175">Disclaimer</span></span>](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a><span data-ttu-id="b0553-176">ASP.NET核心執行時和框架</span><span class="sxs-lookup"><span data-stu-id="b0553-176">ASP.NET Core Runtime and Framework</span></span>

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a><span data-ttu-id="b0553-177">非音子讀取與寫入 HTTP 要求與回應</span><span class="sxs-lookup"><span data-stu-id="b0553-177">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>

<span data-ttu-id="b0553-178">ASP.NET 4 引入了使用*HTTPRequest.Get 無緩衝區輸入流*方法將 HTTP 請求實體作為流讀取的功能。</span><span class="sxs-lookup"><span data-stu-id="b0553-178">ASP.NET 4 introduced the ability to read an HTTP request entity as a stream using the *HttpRequest.GetBufferlessInputStream* method.</span></span> <span data-ttu-id="b0553-179">此方法提供了對請求實體的流式訪問。</span><span class="sxs-lookup"><span data-stu-id="b0553-179">This method provided streaming access to the request entity.</span></span> <span data-ttu-id="b0553-180">但是,它同步執行,在請求的持續時間內將線程捆綁在一起。</span><span class="sxs-lookup"><span data-stu-id="b0553-180">However, it executed synchronously, which tied up a thread for the duration of a request.</span></span>

<span data-ttu-id="b0553-181">ASP.NET 4.5 支援在 HTTP 請求實體上非同步讀取流的功能,以及非同步刷新的能力。</span><span class="sxs-lookup"><span data-stu-id="b0553-181">ASP.NET 4.5 supports the ability to read streams asynchronously on an HTTP request entity, and the ability to flush asynchronously.</span></span> <span data-ttu-id="b0553-182">ASP.NET 4.5 還使您能夠對 HTTP 請求實體進行雙緩衝,從而更輕鬆地與下游 HTTP 處理程式(如 .aspx 頁處理程式和 ASP.NET MVC 控制器)集成。</span><span class="sxs-lookup"><span data-stu-id="b0553-182">ASP.NET 4.5 also gives you the ability to double-buffer an HTTP request entity, which provides easier integration with downstream HTTP handlers such as .aspx page handlers and ASP.NET MVC controllers.</span></span>

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a><span data-ttu-id="b0553-183">HTTPRequest 處理的改進</span><span class="sxs-lookup"><span data-stu-id="b0553-183">Improvements to HttpRequest handling</span></span>

<span data-ttu-id="b0553-184">ASP.NET 4.5 從 HTTPRequest 返回的流引用 *.Get無緩衝區輸入流*支援同步和非同步讀取方法。</span><span class="sxs-lookup"><span data-stu-id="b0553-184">The Stream reference returned by ASP.NET 4.5 from *HttpRequest.GetBufferlessInputStream* supports both synchronous and asynchronous read methods.</span></span> <span data-ttu-id="b0553-185">從*Get 無緩衝區輸入流*返回的*流*物件現在實現了 BeginRead 和 EndRead 方法。</span><span class="sxs-lookup"><span data-stu-id="b0553-185">The *Stream* object returned from *GetBufferlessInputStream* now implements both the BeginRead and EndRead methods.</span></span> <span data-ttu-id="b0553-186">非同步*的流*方法允許您以塊非同步讀取請求實體,而ASP.NET在非同步讀取迴圈的每個反覆運算之間釋放當前線程。</span><span class="sxs-lookup"><span data-stu-id="b0553-186">The asynchronous *Stream* methods let you asynchronously read the request entity in chunks, while ASP.NET releases the current thread between each iteration of an asynchronous read loop.</span></span>

<span data-ttu-id="b0553-187">ASP.NET 4.5 還添加了一種以緩衝方式讀取請求實體的配套方法 *:HTTPRequest.GetBufferedInputStream*。</span><span class="sxs-lookup"><span data-stu-id="b0553-187">ASP.NET 4.5 has also added a companion method for reading the request entity in a buffered way: *HttpRequest.GetBufferedInputStream*.</span></span> <span data-ttu-id="b0553-188">這種新的重載工作類似於*Get 無緩衝區輸入流*,支援同步讀取和異步讀取。</span><span class="sxs-lookup"><span data-stu-id="b0553-188">This new overload works like *GetBufferlessInputStream*, supporting both synchronous and asynchronous reads.</span></span> <span data-ttu-id="b0553-189">但是,在讀取時 *,GetBufferedInputStream*還會將實體位元組複製到ASP.NET內部緩衝區中,以便下游模組和處理程式仍可以訪問請求實體。</span><span class="sxs-lookup"><span data-stu-id="b0553-189">However, as it reads, *GetBufferedInputStream* also copies the entity bytes into ASP.NET internal buffers so that downstream modules and handlers can still access the request entity.</span></span> <span data-ttu-id="b0553-190">例如,如果導管中的一些上游程式碼已經使用*GetBufferedInputStream*讀取了請求實體,您仍可以使用*HttpRequest.Form*或*HTTPRequest.Files*。</span><span class="sxs-lookup"><span data-stu-id="b0553-190">For example, if some upstream code in the pipeline has already read the request entity using *GetBufferedInputStream*, you can still use *HttpRequest.Form* or *HttpRequest.Files*.</span></span> <span data-ttu-id="b0553-191">這允許您對請求執行非同步處理(例如,將大型檔上載流式傳輸到資料庫),但之後仍運行 .aspx 頁和 MVC ASP.NET控制器。</span><span class="sxs-lookup"><span data-stu-id="b0553-191">This lets you perform asynchronous processing on a request (for example, streaming a large file upload to a database), but still run .aspx pages and MVC ASP.NET controllers afterward.</span></span>

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a><span data-ttu-id="b0553-192">同步刷新回應</span><span class="sxs-lookup"><span data-stu-id="b0553-192">Asynchronously flushing a response</span></span>

<span data-ttu-id="b0553-193">當用戶端距離遙遠或具有低頻寬連接時,向 HTTP 客戶端發送回應可能需要相當長的時間。</span><span class="sxs-lookup"><span data-stu-id="b0553-193">Sending responses to an HTTP client can take considerable time when the client is far away or has a low-bandwidth connection.</span></span> <span data-ttu-id="b0553-194">通常ASP.NET緩衝回應位元組,因為它們是由應用程式創建的。</span><span class="sxs-lookup"><span data-stu-id="b0553-194">Normally ASP.NET buffers the response bytes as they are created by an application.</span></span> <span data-ttu-id="b0553-195">然後ASP.NET然後在請求處理的末尾執行累積緩衝區的單個發送操作。</span><span class="sxs-lookup"><span data-stu-id="b0553-195">ASP.NET then performs a single send operation of the accrued buffers at the very end of request processing.</span></span>

<span data-ttu-id="b0553-196">如果緩衝回應很大(例如,將大型檔流式傳輸到用戶端),則必須定期調用*HttpResponse.Flush,* 以便向用戶端發送緩衝輸出並保持記憶體使用方式控制。</span><span class="sxs-lookup"><span data-stu-id="b0553-196">If the buffered response is large (for example, streaming a large file to a client), you must periodically call *HttpResponse.Flush* to send buffered output to the client and keep memory usage under control.</span></span> <span data-ttu-id="b0553-197">但是,由於*Flush*是同步調用,因此反覆運算調用*Flush*仍會在可能長時間運行的請求的持續時間內使用線程。</span><span class="sxs-lookup"><span data-stu-id="b0553-197">However, because *Flush* is a synchronous call, iteratively calling *Flush* still consumes a thread for the duration of potentially long-running requests.</span></span>

<span data-ttu-id="b0553-198">ASP.NET 4.5 添加了使用*HttpResponse*類的*BeginFlush*和*endFlush*方法非同步執行刷新的支援。</span><span class="sxs-lookup"><span data-stu-id="b0553-198">ASP.NET 4.5 adds support for performing flushes asynchronously using the *BeginFlush* and *EndFlush* methods of the *HttpResponse* class.</span></span> <span data-ttu-id="b0553-199">使用這些方法,您可以創建非同步模組和非同步處理程式,這些模組和非同步處理程式在不捆綁作業系統線程的情況下將資料增量發送到用戶端。</span><span class="sxs-lookup"><span data-stu-id="b0553-199">Using these methods, you can create asynchronous modules and asynchronous handlers that incrementally send data to a client without tying up operating-system threads.</span></span> <span data-ttu-id="b0553-200">在*BeginFlush*和*結束刷新*調用之間,ASP.NET釋放當前線程。</span><span class="sxs-lookup"><span data-stu-id="b0553-200">In between *BeginFlush* and *EndFlush* calls, ASP.NET releases the current thread.</span></span> <span data-ttu-id="b0553-201">這大大減少了支援長時間運行的 HTTP 下載所需的活動線程總數。</span><span class="sxs-lookup"><span data-stu-id="b0553-201">This substantially reduces the total number of active threads that are needed in order to support long-running HTTP downloads.</span></span>

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a><span data-ttu-id="b0553-202">支援*await*與*工作*- 基於非非非同步模組與處理程式</span><span class="sxs-lookup"><span data-stu-id="b0553-202">Support for *await* and *Task* - Based Asynchronous Modules and Handlers</span></span>

<span data-ttu-id="b0553-203">.NET 框架 4 引入了一個非同步程式設計概念,稱為*工作*。</span><span class="sxs-lookup"><span data-stu-id="b0553-203">The .NET Framework 4 introduced an asynchronous programming concept referred to as a *task*.</span></span> <span data-ttu-id="b0553-204">工作由系統中的*工作*型態與相關類型表示 *。*</span><span class="sxs-lookup"><span data-stu-id="b0553-204">Tasks are represented by the *Task* type and related types in the *System.Threading.Tasks* namespace.</span></span> <span data-ttu-id="b0553-205">.NET Framework 4.5 基於此功能,具有編譯器增強功能,使使用*Task*物件變得簡單。</span><span class="sxs-lookup"><span data-stu-id="b0553-205">The .NET Framework 4.5 builds on this with compiler enhancements that make working with *Task* objects simple.</span></span> <span data-ttu-id="b0553-206">在 .NET 架構 4.5 中,編譯器支援兩個新關鍵字:*等待*與*非同步*。</span><span class="sxs-lookup"><span data-stu-id="b0553-206">In the .NET Framework 4.5, the compilers support two new keywords: *await* and *async*.</span></span> <span data-ttu-id="b0553-207">*await*關鍵字是語法速記,用於指示代碼段應異步等待其他代碼段。</span><span class="sxs-lookup"><span data-stu-id="b0553-207">The *await* keyword is syntactical shorthand for indicating that a piece of code should asynchronously wait on some other piece of code.</span></span> <span data-ttu-id="b0553-208">*非同步*關鍵字表示可用於將方法標記為基於任務的非同步方法的提示。</span><span class="sxs-lookup"><span data-stu-id="b0553-208">The *async* keyword represents a hint that you can use to mark methods as task-based asynchronous methods.</span></span>

<span data-ttu-id="b0553-209">*await、\*\*非同步*和*工作*物件的組合使您在 .NET 4.5 中編寫異步代碼變得更加容易。</span><span class="sxs-lookup"><span data-stu-id="b0553-209">The combination of *await*, *async*, and the *Task* object makes it much easier for you to write asynchronous code in .NET 4.5.</span></span> <span data-ttu-id="b0553-210">ASP.NET 4.5 支援這些簡化與新的 API,允許您編寫非同步 HTTP 模組和異步 HTTP 處理程式使用新的編譯器增強功能。</span><span class="sxs-lookup"><span data-stu-id="b0553-210">ASP.NET 4.5 supports these simplifications with new APIs that let you write asynchronous HTTP modules and asynchronous HTTP handlers using the new compiler enhancements.</span></span>

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a><span data-ttu-id="b0553-211">非同步 HTTP 模組</span><span class="sxs-lookup"><span data-stu-id="b0553-211">Asynchronous HTTP modules</span></span>

<span data-ttu-id="b0553-212">假設您要在返回*任務*物件的方法內執行非同步工作。</span><span class="sxs-lookup"><span data-stu-id="b0553-212">Suppose that you want to perform asynchronous work within a method that returns a *Task* object.</span></span> <span data-ttu-id="b0553-213">以下代碼示例定義了一個非同步方法,該方法進行非同步調用以下載 Microsoft 主頁。</span><span class="sxs-lookup"><span data-stu-id="b0553-213">The following code example defines an asynchronous method that makes an asynchronous call to download the Microsoft home page.</span></span> <span data-ttu-id="b0553-214">請注意在方法簽名中使用*非同步*關鍵字,並注意對*下載StringTaskAsync*的*等待*呼叫。</span><span class="sxs-lookup"><span data-stu-id="b0553-214">Notice the use of the *async* keyword in the method signature and the *await* call to *DownloadStringTaskAsync*.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

<span data-ttu-id="b0553-215">這就是您需要編寫的 - .NET Framework 將自動處理在等待下載完成時展開調用堆疊,以及在下載完成後自動還原調用堆疊。</span><span class="sxs-lookup"><span data-stu-id="b0553-215">That's all you have to write — the .NET Framework will automatically handle unwinding the call stack while waiting for the download to complete, as well as automatically restoring the call stack after the download is done.</span></span>

<span data-ttu-id="b0553-216">現在假設您要在非同步ASP.NET HTTP 模組中使用此非同步方法。</span><span class="sxs-lookup"><span data-stu-id="b0553-216">Now suppose that you want to use this asynchronous method in an asynchronous ASP.NET HTTP module.</span></span> <span data-ttu-id="b0553-217">ASP.NET 4.5 包括幫助器方法 *(EventHandlerTaskAsyncHelper*) 和新的委託類型 *(TaskEventHandler),* 可用於將基於任務的異步方法與 ASP.NET HTTP 管道公開的較舊的非同步程式設計模型集成。</span><span class="sxs-lookup"><span data-stu-id="b0553-217">ASP.NET 4.5 includes a helper method (*EventHandlerTaskAsyncHelper*) and a new delegate type (*TaskEventHandler*) that you can use to integrate task-based asynchronous methods with the older asynchronous programming model exposed by the ASP.NET HTTP pipeline.</span></span> <span data-ttu-id="b0553-218">此範例展示如何:</span><span class="sxs-lookup"><span data-stu-id="b0553-218">This example shows how:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a><span data-ttu-id="b0553-219">非同步 HTTP 處理程式</span><span class="sxs-lookup"><span data-stu-id="b0553-219">Asynchronous HTTP handlers</span></span>

<span data-ttu-id="b0553-220">在ASP.NET中編寫非同步處理程式的傳統方法是實現*IHttpAsyncHandler*介面。</span><span class="sxs-lookup"><span data-stu-id="b0553-220">The traditional approach to writing asynchronous handlers in ASP.NET is to implement the *IHttpAsyncHandler* interface.</span></span> <span data-ttu-id="b0553-221">ASP.NET 4.5 引入了可以從派生的*HttpTaskSyncHandler*非同步基類型,這使得編寫異步處理程式變得更加容易。</span><span class="sxs-lookup"><span data-stu-id="b0553-221">ASP.NET 4.5 introduces the *HttpTaskAsyncHandler* asynchronous base type that you can derive from, which makes it much easier to write asynchronous handlers.</span></span>

<span data-ttu-id="b0553-222">*HttpTaskAsyncHandler*類型是抽象的,需要您重寫*ProcessRequestAsync*方法。</span><span class="sxs-lookup"><span data-stu-id="b0553-222">The *HttpTaskAsyncHandler* type is abstract and requires you to override the *ProcessRequestAsync* method.</span></span> <span data-ttu-id="b0553-223">內部ASP.NET負責將*ProcessRequestAsync*的返回簽名(*任務*物件)與ASP.NET管道使用的舊異步程式設計模型整合。</span><span class="sxs-lookup"><span data-stu-id="b0553-223">Internally ASP.NET takes care of integrating the return signature (a *Task* object) of *ProcessRequestAsync* with the older asynchronous programming model used by the ASP.NET pipeline.</span></span>

<span data-ttu-id="b0553-224">下面的範例展示如何使用*Task*和*等待*做為非同步 HTTP 處理程式實現的一部分:</span><span class="sxs-lookup"><span data-stu-id="b0553-224">The following example shows how you can use *Task* and *await* as part of the implementation of an asynchronous HTTP handler:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a><span data-ttu-id="b0553-225">新的ASP.NET要求驗證功能</span><span class="sxs-lookup"><span data-stu-id="b0553-225">New ASP.NET Request Validation Features</span></span>

<span data-ttu-id="b0553-226">預設情況下,ASP.NET執行請求驗證 - 它會檢查在欄位、標頭、Cookie 等中尋找標記或腳本的請求。</span><span class="sxs-lookup"><span data-stu-id="b0553-226">By default, ASP.NET performs request validation — it examines requests to look for markup or script in fields, headers, cookies, and so on.</span></span> <span data-ttu-id="b0553-227">如果檢測到任何異常,ASP.NET將引發異常。</span><span class="sxs-lookup"><span data-stu-id="b0553-227">If any is detected, ASP.NET throws an exception.</span></span> <span data-ttu-id="b0553-228">這是抵禦潛在跨網站腳本攻擊的第一道防線。</span><span class="sxs-lookup"><span data-stu-id="b0553-228">This acts as a first line of defense against potential cross-site scripting attacks.</span></span>

<span data-ttu-id="b0553-229">ASP.NET 4.5 使選擇性讀取未經驗證的請求數據變得容易。</span><span class="sxs-lookup"><span data-stu-id="b0553-229">ASP.NET 4.5 makes it easy to selectively read unvalidated request data.</span></span> <span data-ttu-id="b0553-230">ASP.NET 4.5 還集成了流行的 AntiXSS 庫,該庫以前是外部庫。</span><span class="sxs-lookup"><span data-stu-id="b0553-230">ASP.NET 4.5 also integrates the popular AntiXSS library, which was formerly an external library.</span></span>

<span data-ttu-id="b0553-231">開發人員經常要求能夠有選擇地關閉其應用程式的請求驗證。</span><span class="sxs-lookup"><span data-stu-id="b0553-231">Developers have frequently asked for the ability to selectively turn off request validation for their applications.</span></span> <span data-ttu-id="b0553-232">例如,如果您的應用程式是論壇軟體,您可能希望允許使用者提交 HTML 格式的論壇帖子和評論,但仍要確保請求驗證檢查所有其他內容。</span><span class="sxs-lookup"><span data-stu-id="b0553-232">For example, if your application is forum software, you might want to allow users to submit HTML-formatted forum posts and comments, but still make sure that request validation is checking everything else.</span></span>

<span data-ttu-id="b0553-233">ASP.NET 4.5 引入了兩個功能,使您能夠輕鬆有選擇地處理未驗證的輸入:延遲("延遲")請求驗證和對未驗證請求數據的訪問。</span><span class="sxs-lookup"><span data-stu-id="b0553-233">ASP.NET 4.5 introduces two features that make it easy for you to selectively work with unvalidated input: deferred ("lazy") request validation and access to unvalidated request data.</span></span>

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a><span data-ttu-id="b0553-234">延遲("延遲")請求驗證</span><span class="sxs-lookup"><span data-stu-id="b0553-234">Deferred ("lazy") request validation</span></span>

<span data-ttu-id="b0553-235">在 ASP.NET 4.5 中,默認情況下,所有請求數據都需接受請求驗證。</span><span class="sxs-lookup"><span data-stu-id="b0553-235">In ASP.NET 4.5, by default all request data is subject to request validation.</span></span> <span data-ttu-id="b0553-236">但是,您可以將應用程式配置為延遲請求驗證,直到實際訪問請求數據。</span><span class="sxs-lookup"><span data-stu-id="b0553-236">However, you can configure the application to defer request validation until you actually access request data.</span></span> <span data-ttu-id="b0553-237">(這有時稱為延遲請求驗證,具體取決於某些數據方案的延遲載入等術語。以將*要求驗證模式*屬性設定為*httpRUntime*元素中的 4.5,可以將應用程式設定為在 Web.config 檔中使用延遲驗證,如以下範例所示:</span><span class="sxs-lookup"><span data-stu-id="b0553-237">(This is sometimes referred to as lazy request validation, based on terms like lazy loading for certain data scenarios.) You can configure the application to use deferred validation in the Web.config file by setting the *requestValidationMode* attribute to 4.5 in the *httpRUntime* element, as in the following example:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

<span data-ttu-id="b0553-238">當請求驗證模式設置為 4.5 時,請求驗證僅針對特定請求值觸發,並且僅在代碼訪問該值時觸發。</span><span class="sxs-lookup"><span data-stu-id="b0553-238">When request validation mode is set to 4.5, request validation is triggered only for a specific request value and only when your code accesses that value.</span></span> <span data-ttu-id="b0553-239">例如,如果代碼獲取了"Request.Form_"論壇\_帖子"的值,則僅針對窗體集合中該元素調用請求驗證。</span><span class="sxs-lookup"><span data-stu-id="b0553-239">For example, if your code gets the value of Request.Form["forum\_post"], request validation is invoked only for that element in the form collection.</span></span> <span data-ttu-id="b0553-240">*窗體*集合中的其他元素均未經過驗證。</span><span class="sxs-lookup"><span data-stu-id="b0553-240">None of the other elements in the *Form* collection are validated.</span></span> <span data-ttu-id="b0553-241">在ASP.NET的早期版本中,當訪問集合中的任何元素時,將觸發整個請求集合的請求驗證。</span><span class="sxs-lookup"><span data-stu-id="b0553-241">In previous versions of ASP.NET, request validation was triggered for the entire request collection when any element in the collection was accessed.</span></span> <span data-ttu-id="b0553-242">新的行為使不同的應用程式元件能夠更輕鬆地查看不同的請求數據,而不會觸發其他部分的請求驗證。</span><span class="sxs-lookup"><span data-stu-id="b0553-242">The new behavior makes it easier for different application components to look at different pieces of request data without triggering request validation on other pieces.</span></span>

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a><span data-ttu-id="b0553-243">支援未經認證的要求</span><span class="sxs-lookup"><span data-stu-id="b0553-243">Support for unvalidated requests</span></span>

<span data-ttu-id="b0553-244">僅延遲請求驗證並不能解決選擇性繞過請求驗證的問題。</span><span class="sxs-lookup"><span data-stu-id="b0553-244">Deferred request validation alone doesn't solve the problem of selectively bypassing request validation.</span></span> <span data-ttu-id="b0553-245">對"請求.Form_"論壇\_帖子"的調用仍觸發該特定請求值的請求驗證。</span><span class="sxs-lookup"><span data-stu-id="b0553-245">The call to Request.Form["forum\_post"] still triggers request validation for that specific request value.</span></span> <span data-ttu-id="b0553-246">但是,您可能希望在不觸發驗證的情況下訪問此欄位,因為您希望允許該欄位中的標記。</span><span class="sxs-lookup"><span data-stu-id="b0553-246">However, you might want to access this field without triggering validation because you want to allow markup in that field.</span></span>

<span data-ttu-id="b0553-247">為此,ASP.NET 4.5 現在支援對請求數據的未經驗證的訪問。</span><span class="sxs-lookup"><span data-stu-id="b0553-247">To allow this, ASP.NET 4.5 now supports unvalidated access to request data.</span></span> <span data-ttu-id="b0553-248">ASP.NET 4.5 在*HttpRequest*類中包括一個新的*未驗證*集合屬性。</span><span class="sxs-lookup"><span data-stu-id="b0553-248">ASP.NET 4.5 includes a new *Unvalidated* collection property in the *HttpRequest* class.</span></span> <span data-ttu-id="b0553-249">此集合提供對請求數據的所有常見值(如*窗體*、*查詢字串\*\*、Cookie*和*Url)* 的存取。</span><span class="sxs-lookup"><span data-stu-id="b0553-249">This collection provides access to all of the common values of request data, like *Form*, *QueryString*, *Cookies*, and *Url*.</span></span>

<span data-ttu-id="b0553-250">使用論壇示例,為了能夠讀取未經驗證的請求數據,首先需要將應用程式配置為使用新的請求驗證模式:</span><span class="sxs-lookup"><span data-stu-id="b0553-250">Using the forum example, to be able to read unvalidated request data, you first need to configure the application to use the new request validation mode:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

<span data-ttu-id="b0553-251">然後,您可以使用*HTTPRequest.未驗證*的屬性讀取未驗證的表單值:</span><span class="sxs-lookup"><span data-stu-id="b0553-251">You can then use the *HttpRequest.Unvalidated* property to read the unvalidated form value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> <span data-ttu-id="b0553-252">安全性 -*小心使用未經驗證的請求數據!*</span><span class="sxs-lookup"><span data-stu-id="b0553-252">Security - *Use unvalidated request data with care!*</span></span> <span data-ttu-id="b0553-253">ASP.NET 4.5 添加了未經驗證的請求屬性和集合,以便您更輕鬆地訪問非常具體的未驗證請求數據。</span><span class="sxs-lookup"><span data-stu-id="b0553-253">ASP.NET 4.5 added the unvalidated request properties and collections to make it easier for you to access very specific unvalidated request data.</span></span> <span data-ttu-id="b0553-254">但是,您仍必須對原始請求數據執行自定義驗證,以確保不會向使用者呈現危險文本。</span><span class="sxs-lookup"><span data-stu-id="b0553-254">However, you must still perform custom validation on the raw request data to ensure that dangerous text is not rendered to users.</span></span>

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a><span data-ttu-id="b0553-255">AntiXSS 函式庫</span><span class="sxs-lookup"><span data-stu-id="b0553-255">AntiXSS Library</span></span>

<span data-ttu-id="b0553-256">由於 Microsoft AntiXSS 庫的普及,ASP.NET 4.5 現在包含該庫版本 4.0 的核心編碼例程式。</span><span class="sxs-lookup"><span data-stu-id="b0553-256">Due to the popularity of the Microsoft AntiXSS Library, ASP.NET 4.5 now incorporates core encoding routines from version 4.0 of that library.</span></span>

<span data-ttu-id="b0553-257">程式碼例設計由新*系統.Web.Security.AntiXs*命名空間中的*AntiXsEncoder*類型實現。</span><span class="sxs-lookup"><span data-stu-id="b0553-257">The encoding routines are implemented by the *AntiXssEncoder* type in the new *System.Web.Security.AntiXss* namespace.</span></span> <span data-ttu-id="b0553-258">您可以通過調用類型中實現的任何靜態編碼方法直接使用*AntiXsEncoder*類型。</span><span class="sxs-lookup"><span data-stu-id="b0553-258">You can use the *AntiXssEncoder* type directly by calling any of the static encoding methods that are implemented in the type.</span></span> <span data-ttu-id="b0553-259">但是,使用新的反 XSS 例程的最簡單方法是將 ASP.NET 應用程式設定為預設使用*AntiXsEncoder*類。</span><span class="sxs-lookup"><span data-stu-id="b0553-259">However, the easiest approach for using the new anti-XSS routines is to configure an ASP.NET application to use the *AntiXssEncoder* class by default.</span></span> <span data-ttu-id="b0553-260">此,從 Web.config 檔案加入以下屬性:</span><span class="sxs-lookup"><span data-stu-id="b0553-260">To do this, add the following attribute to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

<span data-ttu-id="b0553-261">當*編碼器類型*屬性設置為使用*AntiXsEncoder*類型時,ASP.NET中的所有輸出編碼將自動使用新的編碼例程。</span><span class="sxs-lookup"><span data-stu-id="b0553-261">When the *encoderType* attribute is set to use the *AntiXssEncoder* type, all output encoding in ASP.NET automatically uses the new encoding routines.</span></span>

<span data-ttu-id="b0553-262">這些是外部 AntiXSS 函式庫中已整合到 ASP.NET 4.5 中的部分:</span><span class="sxs-lookup"><span data-stu-id="b0553-262">These are the portions of the external AntiXSS library that have been incorporated into ASP.NET 4.5:</span></span>

- <span data-ttu-id="b0553-263">*Html 編碼* *,HtmlFormUrl 編碼*, 與*html 屬性編碼*</span><span class="sxs-lookup"><span data-stu-id="b0553-263">*HtmlEncode*, *HtmlFormUrlEncode*, and *HtmlAttributeEncode*</span></span>
- <span data-ttu-id="b0553-264">*XmlAttributeEncode*和*XmlEncode*</span><span class="sxs-lookup"><span data-stu-id="b0553-264">*XmlAttributeEncode* and *XmlEncode*</span></span>
- <span data-ttu-id="b0553-265">*網址Encode*與*網址Path 編碼*(新)</span><span class="sxs-lookup"><span data-stu-id="b0553-265">*UrlEncode* and *UrlPathEncode* (new)</span></span>
- <span data-ttu-id="b0553-266">*CsEncode*</span><span class="sxs-lookup"><span data-stu-id="b0553-266">*CssEncode*</span></span>

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a><span data-ttu-id="b0553-267">支援 WebSocket 協定</span><span class="sxs-lookup"><span data-stu-id="b0553-267">Support for WebSockets Protocol</span></span>

<span data-ttu-id="b0553-268">WebSockets 協定是基於標準的網路協定,它定義了如何通過 HTTP 在用戶端和伺服器之間建立安全的即時雙向通信。</span><span class="sxs-lookup"><span data-stu-id="b0553-268">WebSockets protocol is a standards-based network protocol that defines how to establish secure, real-time bidirectional communications between a client and a server over HTTP.</span></span> <span data-ttu-id="b0553-269">Microsoft 與 IETF 和 W3C 標準機構合作,説明定義該協定。</span><span class="sxs-lookup"><span data-stu-id="b0553-269">Microsoft has worked with both the IETF and W3C standards bodies to help define the protocol.</span></span> <span data-ttu-id="b0553-270">WebSockets 協定由任何用戶端(而不僅僅是瀏覽器)支援,Microsoft 在用戶端和行動作業系統上投入大量資源支援 WebSocket 協定。</span><span class="sxs-lookup"><span data-stu-id="b0553-270">The WebSockets protocol is supported by any client (not just browsers), with Microsoft investing substantial resources supporting WebSockets protocol on both client and mobile operating systems.</span></span>

<span data-ttu-id="b0553-271">WebSockets 協定使在用戶端和伺服器之間創建長時間運行的數據傳輸變得更加容易。</span><span class="sxs-lookup"><span data-stu-id="b0553-271">WebSockets protocol makes it much easier to create long-running data transfers between a client and a server.</span></span> <span data-ttu-id="b0553-272">例如,編寫聊天應用程式要容易得多,因為您可以在用戶端和伺服器之間建立真正的長時間運行的連接。</span><span class="sxs-lookup"><span data-stu-id="b0553-272">For example, writing a chat application is much easier because you can establish a true long-running connection between a client and a server.</span></span> <span data-ttu-id="b0553-273">您不必使用定期輪詢或 HTTP 長輪詢等解決方法來類比套接字的行為。</span><span class="sxs-lookup"><span data-stu-id="b0553-273">You do not have to resort to workarounds like periodic polling or HTTP long-polling to simulate the behavior of a socket.</span></span>

<span data-ttu-id="b0553-274">ASP.NET 4.5 和 IIS 8 都支援低級 WebSocket,使 ASP.NET 開發人員能夠使用託管 API 在 WebSocket 物件上異步讀取和寫入字串和二進位數據。</span><span class="sxs-lookup"><span data-stu-id="b0553-274">ASP.NET 4.5 and IIS 8 include low-level WebSockets support, enabling ASP.NET developers to use managed APIs for asynchronously reading and writing both string and binary data on a WebSockets object.</span></span> <span data-ttu-id="b0553-275">對於ASP.NET 4.5,有一個新的*System.Web.WebSockets*命名空間,其中包含用於使用 WebSockets 協定的類型。</span><span class="sxs-lookup"><span data-stu-id="b0553-275">For ASP.NET 4.5, there is a new *System.Web.WebSockets* namespace that contains types for working with WebSockets protocol.</span></span>

<span data-ttu-id="b0553-276">瀏覽器客戶端透過建立 DOM WebSocket 物件來建立*WebSocket*連接,該物件指向 ASP.NET 應用程式中的網址,如以下範例所示:</span><span class="sxs-lookup"><span data-stu-id="b0553-276">A browser client establishes a WebSockets connection by creating a DOM *WebSocket* object that points to a URL in an ASP.NET application, as in the following example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

<span data-ttu-id="b0553-277">您可以使用任何類型的模組或處理程式在ASP.NET創建 WebSockets 終結點。</span><span class="sxs-lookup"><span data-stu-id="b0553-277">You can create WebSockets endpoints in ASP.NET using any kind of module or handler.</span></span> <span data-ttu-id="b0553-278">在前面的範例中,使用了 .ashx 檔,因為 .ashx 檔是創建處理程式的快速方法。</span><span class="sxs-lookup"><span data-stu-id="b0553-278">In the previous example, an .ashx file was used, because .ashx files are a quick way to create a handler.</span></span>

<span data-ttu-id="b0553-279">根據 WebSocket 協定,ASP.NET 應用程式透過指示請求應從 HTTP GET 請求升級到 WebSockets 請求來接受用戶端的 WebSockets 請求。</span><span class="sxs-lookup"><span data-stu-id="b0553-279">According to the WebSockets protocol, an ASP.NET application accepts a client's WebSockets request by indicating that the request should be upgraded from an HTTP GET request to a WebSockets request.</span></span> <span data-ttu-id="b0553-280">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="b0553-280">Here's an example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

<span data-ttu-id="b0553-281">*AcceptWebSocketRequest 方法*接受函數委託,因為ASP.NET解除當前 HTTP 請求,然後將控制權傳輸到函數委託。</span><span class="sxs-lookup"><span data-stu-id="b0553-281">The *AcceptWebSocketRequest* method accepts a function delegate because ASP.NET unwinds the current HTTP request and then transfers control to the function delegate.</span></span> <span data-ttu-id="b0553-282">從概念上講,這種方法類似於您使用*System.Threading.Thread*的方式,在其中定義執行後台工作的線程啟動委託。</span><span class="sxs-lookup"><span data-stu-id="b0553-282">Conceptually this approach is similar to how you use *System.Threading.Thread*, where you define a thread-start delegate in which background work is performed.</span></span>

<span data-ttu-id="b0553-283">ASP.NET和用戶端成功完成 WebSocket 握手後,ASP.NET調用您的委託,WebSockets 應用程式開始運行。</span><span class="sxs-lookup"><span data-stu-id="b0553-283">After ASP.NET and the client have successfully completed a WebSockets handshake, ASP.NET calls your delegate and the WebSockets application starts running.</span></span> <span data-ttu-id="b0553-284">以下代碼範例顯示了一個簡單的回聲應用程式,該應用程式在ASP.NET中使用內建 WebSocket 支援:</span><span class="sxs-lookup"><span data-stu-id="b0553-284">The following code example shows a simple echo application that uses the built-in WebSockets support in ASP.NET:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

<span data-ttu-id="b0553-285">.NET 4.5 中支援*await*關鍵字和基於異步任務的操作自然適合編寫 WebSockets 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0553-285">The support in .NET 4.5 for the *await* keyword and asynchronous task-based operations is a natural fit for writing WebSockets applications.</span></span> <span data-ttu-id="b0553-286">代碼示例顯示 WebSockets 請求完全非同步地在 ASP.NET 內部執行。</span><span class="sxs-lookup"><span data-stu-id="b0553-286">The code example shows that a WebSockets request runs completely asynchronously inside ASP.NET.</span></span> <span data-ttu-id="b0553-287">應用程式通過調用*await 套接字以非同步等待從用戶端發送消息。接收Async*。</span><span class="sxs-lookup"><span data-stu-id="b0553-287">The application waits asynchronously for a message to be sent from a client by calling *await socket.ReceiveAsync*.</span></span> <span data-ttu-id="b0553-288">同樣,您可以通過調用*await 套接字向客戶端發送非同步訊息。森步同步*。</span><span class="sxs-lookup"><span data-stu-id="b0553-288">Similarly, you can send an asynchronous message to a client by calling *await socket.SendAsync*.</span></span>

<span data-ttu-id="b0553-289">在瀏覽器中,應用程式通過*onmessage*功能接收 WebSocket 消息。</span><span class="sxs-lookup"><span data-stu-id="b0553-289">In the browser, an application receives WebSockets messages through an *onmessage* function.</span></span> <span data-ttu-id="b0553-290">要從瀏覽器傳送訊息,請呼叫*WebSocket* DOM 類型的*送出*方法,如以下範例所示:</span><span class="sxs-lookup"><span data-stu-id="b0553-290">To send a message from a browser, you call the *send* method of the *WebSocket* DOM type, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

<span data-ttu-id="b0553-291">將來,我們可能會發佈此功能的更新,以抽象掉 WebSocket 應用程式在此版本中所需的一些低級編碼。</span><span class="sxs-lookup"><span data-stu-id="b0553-291">In the future, we might release updates to this functionality that abstract away some of the low-level coding that is required in this release for WebSockets applications.</span></span>

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a><span data-ttu-id="b0553-292">統合和縮製</span><span class="sxs-lookup"><span data-stu-id="b0553-292">Bundling and Minification</span></span>

<span data-ttu-id="b0553-293">捆綁允許您將單個 JavaScript 和 CSS 檔合併到可以視為單個檔的捆綁包中。</span><span class="sxs-lookup"><span data-stu-id="b0553-293">Bundling lets you combine individual JavaScript and CSS files into a bundle that can be treated like a single file.</span></span> <span data-ttu-id="b0553-294">Min化透過刪除空白和其他不需要的字元來壓縮 JavaScript 和 CSS 檔。</span><span class="sxs-lookup"><span data-stu-id="b0553-294">Minification condenses JavaScript and CSS files by removing whitespace and other characters that are not required.</span></span> <span data-ttu-id="b0553-295">這些功能與 Web 窗體、ASP.NET MVC 和網頁配合使用。</span><span class="sxs-lookup"><span data-stu-id="b0553-295">These features work with Web Forms, ASP.NET MVC, and Web Pages.</span></span>

<span data-ttu-id="b0553-296">捆綁包是使用捆綁類或其子類之一的腳本捆綁包和樣式捆綁包創建的。</span><span class="sxs-lookup"><span data-stu-id="b0553-296">Bundles are created using the Bundle class or one of its child classes, ScriptBundle and StyleBundle.</span></span> <span data-ttu-id="b0553-297">配置捆綁包的實例后,只需將其添加到全域捆綁收集實例,即可向傳入請求提供該捆綁包。</span><span class="sxs-lookup"><span data-stu-id="b0553-297">After configuring an instance of a bundle, the bundle is made available to incoming requests by simply adding it to a global BundleCollection instance.</span></span> <span data-ttu-id="b0553-298">在預設範本中,捆綁配置在 Bundle Config 檔中執行。</span><span class="sxs-lookup"><span data-stu-id="b0553-298">In the default templates, bundle configuration is performed in a BundleConfig file.</span></span> <span data-ttu-id="b0553-299">此預設設定為範本使用的所有核心文本和 css 檔案建立捆綁套件。</span><span class="sxs-lookup"><span data-stu-id="b0553-299">This default configuration creates bundles for all of the core scripts and css files used by the templates.</span></span>

<span data-ttu-id="b0553-300">通過使用幾個可能的説明方法之一,從視圖中引用捆綁包。</span><span class="sxs-lookup"><span data-stu-id="b0553-300">Bundles are referenced from within views by using one of a couple possible helper methods.</span></span> <span data-ttu-id="b0553-301">為了支援在調試與發佈模式下呈現捆綁包的不同標記,ScriptBundle 和 StyleBundle 類具有幫助器方法 Render。</span><span class="sxs-lookup"><span data-stu-id="b0553-301">In order to support rendering different markup for a bundle when in debug vs. release mode, the ScriptBundle and StyleBundle classes have the helper method, Render.</span></span> <span data-ttu-id="b0553-302">在調試模式下,渲染將為捆綁包中的每個資源生成標記。</span><span class="sxs-lookup"><span data-stu-id="b0553-302">When in debug mode, Render will generate markup for each resource in the bundle.</span></span> <span data-ttu-id="b0553-303">在發佈模式下,渲染將為整個捆綁包生成單個標記元素。</span><span class="sxs-lookup"><span data-stu-id="b0553-303">When in release mode, Render will generate a single markup element for the entire bundle.</span></span> <span data-ttu-id="b0553-304">通過修改 Web.config 中編譯元素的調試屬性,可以在調試和發佈模式之間切換,如下所示:</span><span class="sxs-lookup"><span data-stu-id="b0553-304">Toggling between debug and release mode can be accomplished by modifying the debug attribute of the compilation element in web.config as shown below:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

<span data-ttu-id="b0553-305">此外,可以直接通過 BundleTable 設定啟用或禁用優化。</span><span class="sxs-lookup"><span data-stu-id="b0553-305">Additionally, enabling or disabling optimization can be set directly via the BundleTable.EnableOptimizations property.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

<span data-ttu-id="b0553-306">當檔捆綁時,它們首先按字母順序排序(它們在**解決方案資源管理器**中顯示的方式)。</span><span class="sxs-lookup"><span data-stu-id="b0553-306">When files are bundled, they are first sorted alphabetically (the way they are displayed in **Solution Explorer**).</span></span> <span data-ttu-id="b0553-307">然後組織它們,以便首先載入已知的庫及其自定義擴展(如 jQuery、MooTools 和 Dojo)。</span><span class="sxs-lookup"><span data-stu-id="b0553-307">They are then organized so that known libraries and their custom extensions (such as jQuery, MooTools, and Dojo) are loaded first.</span></span> <span data-ttu-id="b0553-308">例如,如上所述,捆綁腳本資料夾的最終順序為:</span><span class="sxs-lookup"><span data-stu-id="b0553-308">For example, the final order for the bundling of the Scripts folder as shown above will be:</span></span>

1. <span data-ttu-id="b0553-309">jquery-1.6.2.js</span><span class="sxs-lookup"><span data-stu-id="b0553-309">jquery-1.6.2.js</span></span>
2. <span data-ttu-id="b0553-310">jquery-ui.js</span><span class="sxs-lookup"><span data-stu-id="b0553-310">jquery-ui.js</span></span>
3. <span data-ttu-id="b0553-311">jquery.tools.js</span><span class="sxs-lookup"><span data-stu-id="b0553-311">jquery.tools.js</span></span>
4. <span data-ttu-id="b0553-312">a.js</span><span class="sxs-lookup"><span data-stu-id="b0553-312">a.js</span></span>

<span data-ttu-id="b0553-313">CSS 檔也按字母順序排序,然後重新組織,以便重置.css 和規範化.css 在任何其他檔之前出現。</span><span class="sxs-lookup"><span data-stu-id="b0553-313">CSS files are also sorted alphabetically and then reorganized so that reset.css and normalize.css come before any other file.</span></span> <span data-ttu-id="b0553-314">上面顯示的樣式資料夾捆綁的最終排序是:</span><span class="sxs-lookup"><span data-stu-id="b0553-314">The final sorting of the bundling of the Styles folder shown above will be this:</span></span>

1. <span data-ttu-id="b0553-315">重置.css</span><span class="sxs-lookup"><span data-stu-id="b0553-315">reset.css</span></span>
2. <span data-ttu-id="b0553-316">內容.css</span><span class="sxs-lookup"><span data-stu-id="b0553-316">content.css</span></span>
3. <span data-ttu-id="b0553-317">表單.css</span><span class="sxs-lookup"><span data-stu-id="b0553-317">forms.css</span></span>
4. <span data-ttu-id="b0553-318">globals.css</span><span class="sxs-lookup"><span data-stu-id="b0553-318">globals.css</span></span>
5. <span data-ttu-id="b0553-319">選單.css</span><span class="sxs-lookup"><span data-stu-id="b0553-319">menu.css</span></span>
6. <span data-ttu-id="b0553-320">樣式.css</span><span class="sxs-lookup"><span data-stu-id="b0553-320">styles.css</span></span>

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a><span data-ttu-id="b0553-321">Web 託管的效能改進</span><span class="sxs-lookup"><span data-stu-id="b0553-321">Performance Improvements for Web Hosting</span></span>

<span data-ttu-id="b0553-322">.NET 框架 4.5 和 Windows 8 引入了可説明您為 Web 伺服器工作負載實現顯著性能提升的功能。</span><span class="sxs-lookup"><span data-stu-id="b0553-322">The .NET Framework 4.5 and Windows 8 introduce features that can help you achieve a significant performance boost for web-server workloads.</span></span> <span data-ttu-id="b0553-323">這包括減少(高達 35%)在啟動時間和使用ASP.NET的網站託管網站的記憶體佔用量中。</span><span class="sxs-lookup"><span data-stu-id="b0553-323">This includes a reduction (up to 35%) in both startup time and in the memory footprint of web hosting sites that use ASP.NET.</span></span>

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a><span data-ttu-id="b0553-324">關鍵性能因素</span><span class="sxs-lookup"><span data-stu-id="b0553-324">Key performance factors</span></span>

<span data-ttu-id="b0553-325">理想情況下,所有網站都應處於活動狀態且處於記憶體中,以確保隨時對下一個請求做出快速回應。</span><span class="sxs-lookup"><span data-stu-id="b0553-325">Ideally, all websites should be active and in memory to assure quick response to the next request, whenever it comes.</span></span> <span data-ttu-id="b0553-326">可能影響網站回應能力的因素包括:</span><span class="sxs-lookup"><span data-stu-id="b0553-326">Factors that can affect site responsiveness include:</span></span>

- <span data-ttu-id="b0553-327">應用池回收后站點重新啟動所需的時間。</span><span class="sxs-lookup"><span data-stu-id="b0553-327">The time it takes for a site to restart after an app pool recycles.</span></span> <span data-ttu-id="b0553-328">當網站程式集不再在記憶體中時,此時需要啟動網站的 Web 伺服器進程。</span><span class="sxs-lookup"><span data-stu-id="b0553-328">This is the time it takes to launch a web server process for the site when the site assemblies are no longer in memory.</span></span> <span data-ttu-id="b0553-329">(平臺程式集仍在記憶體中,因為它們被其他網站使用。這種情況稱為「冷網站,暖框架啟動」或只是「冷網站啟動」。</span><span class="sxs-lookup"><span data-stu-id="b0553-329">(The platform assemblies are still in memory, since they are used by other sites.) This situation is referred to as "cold site, warm framework startup" or just "cold site startup."</span></span>
- <span data-ttu-id="b0553-330">網站佔用的內存量。</span><span class="sxs-lookup"><span data-stu-id="b0553-330">How much memory the site occupies.</span></span> <span data-ttu-id="b0553-331">其術語是「每個網站記憶體消耗」或「非共用工作集」。</span><span class="sxs-lookup"><span data-stu-id="b0553-331">Terms for this are "per-site memory consumption" or "unshared working set."</span></span>

<span data-ttu-id="b0553-332">新的性能改進側重於這兩個因素。</span><span class="sxs-lookup"><span data-stu-id="b0553-332">The new performance improvements focus on both of these factors.</span></span>

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a><span data-ttu-id="b0553-333">對新效能功能的要求</span><span class="sxs-lookup"><span data-stu-id="b0553-333">Requirements for New Performance Features</span></span>

<span data-ttu-id="b0553-334">新功能的要求可以分為以下幾類:</span><span class="sxs-lookup"><span data-stu-id="b0553-334">The requirements for the new features can be broken down into these categories:</span></span>

- <span data-ttu-id="b0553-335">在 .NET 框架 4 上運行的改進。</span><span class="sxs-lookup"><span data-stu-id="b0553-335">Improvements that run on the .NET Framework 4.</span></span>
- <span data-ttu-id="b0553-336">需要 .NET 框架 4.5 但可在任何版本的 Windows 上運行的改進。</span><span class="sxs-lookup"><span data-stu-id="b0553-336">Improvements that require the .NET Framework 4.5 but can run on any version of Windows.</span></span>
- <span data-ttu-id="b0553-337">僅在 Windows 8 上運行 .NET 框架 4.5 時可用的改進。</span><span class="sxs-lookup"><span data-stu-id="b0553-337">Improvements that are available only with .NET Framework 4.5 running on Windows 8.</span></span>

<span data-ttu-id="b0553-338">性能隨您能夠啟用的每個改進級別而提高。</span><span class="sxs-lookup"><span data-stu-id="b0553-338">Performance increases with each level of improvement that you are able to enable.</span></span>

<span data-ttu-id="b0553-339">一些 .NET Framework 4.5 改進還利用了適用於其他方案的更廣泛的性能功能。</span><span class="sxs-lookup"><span data-stu-id="b0553-339">Some of the .NET Framework 4.5 improvements take advantage of broader performance features that apply to other scenarios as well.</span></span>

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a><span data-ttu-id="b0553-340">共用公共程式集</span><span class="sxs-lookup"><span data-stu-id="b0553-340">Sharing Common Assemblies</span></span>

<span data-ttu-id="b0553-341">**要求**: .NET 框架 4 與視覺化工作室 11 開發人員預覽 SDK</span><span class="sxs-lookup"><span data-stu-id="b0553-341">**Requirement**: .NET Framework 4 and Visual Studio 11 Developer Preview SDK</span></span>

<span data-ttu-id="b0553-342">伺服器上的不同網站通常使用相同的幫助器程式集(例如,來自初學者工具組或範例應用程式的程式集)。</span><span class="sxs-lookup"><span data-stu-id="b0553-342">Different sites on a server often use the same helper assemblies (for example, assemblies from a starter kit or sample application).</span></span> <span data-ttu-id="b0553-343">每個網站在其 Bin 目錄中都有自己的程式集副本。</span><span class="sxs-lookup"><span data-stu-id="b0553-343">Each site has its own copy of these assemblies in its Bin directory.</span></span> <span data-ttu-id="b0553-344">即使程式集的物件代碼相同,但它們是物理上獨立的程式集,因此在冷網站啟動期間必須單獨讀取每個程式集,並單獨保存在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="b0553-344">Even though the object code for the assemblies is identical, they're physically separate assemblies, so each assembly has to be read separately during cold site startup and kept separately in memory.</span></span>

<span data-ttu-id="b0553-345">新的實習功能解決了這種低效率,減少了 RAM 要求和載入時間。</span><span class="sxs-lookup"><span data-stu-id="b0553-345">The new interning functionality solves this inefficiency and reduces both RAM requirements and load time.</span></span> <span data-ttu-id="b0553-346">使用允許 Windows 在檔案系統中保留每個程式集的單個副本,網站 Bin 資料夾中的各個程式集將替換為指向單個複本的符號連結。</span><span class="sxs-lookup"><span data-stu-id="b0553-346">Interning lets Windows keep a single copy of each assembly in the file system, and individual assemblies in the site Bin folders are replaced with symbolic links to the single copy.</span></span> <span data-ttu-id="b0553-347">如果單個網站需要程式集的不同版本,則符號連結將被程式集的新版本替換,並且只有該網站受到影響。</span><span class="sxs-lookup"><span data-stu-id="b0553-347">If an individual site needs a distinct version of the assembly, the symbolic link is replaced by the new version of the assembly, and only that site is affected.</span></span>

<span data-ttu-id="b0553-348">使用符號連結共用程式集需要一個名為 aspnet\_intern.exe 的新工具,該工具允許您創建和管理已處理程式集的存儲。</span><span class="sxs-lookup"><span data-stu-id="b0553-348">Sharing assemblies using symbolic links requires a new tool named aspnet\_intern.exe, which lets you create and manage the store of interned assemblies.</span></span> <span data-ttu-id="b0553-349">它是作為可視化工作室 11 開發人員預覽 SDK 的一部分提供的。</span><span class="sxs-lookup"><span data-stu-id="b0553-349">It is provided as a part of the Visual Studio 11 Developer Preview SDK.</span></span> <span data-ttu-id="b0553-350">(但是,假定已安裝最新的[更新](https://support.microsoft.com/kb/2468871),它將在僅安裝 .NET 框架 4 的系統上工作。</span><span class="sxs-lookup"><span data-stu-id="b0553-350">(However, it will work on a system that has only the .NET Framework 4 installed, assuming you have installed the latest [update](https://support.microsoft.com/kb/2468871).)</span></span>

<span data-ttu-id="b0553-351">為了確保所有符合條件的程式集都已暫留,您定期運行 aspnet\_intern.exe(例如,每週一次作為計劃任務)。</span><span class="sxs-lookup"><span data-stu-id="b0553-351">To make sure all eligible assemblies have been interned, you run aspnet\_intern.exe periodically (for example, once a week as a scheduled task).</span></span> <span data-ttu-id="b0553-352">典型用途如下:</span><span class="sxs-lookup"><span data-stu-id="b0553-352">A typical use is as follows:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

<span data-ttu-id="b0553-353">要查看所有選項,運行沒有參數的工具。</span><span class="sxs-lookup"><span data-stu-id="b0553-353">To see all options, run the tool with no arguments.</span></span>

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a><span data-ttu-id="b0553-354">使用多核 JIT 編譯,加快啟動速度</span><span class="sxs-lookup"><span data-stu-id="b0553-354">Using multi-Core JIT compilation for faster startup</span></span>

<span data-ttu-id="b0553-355">**要求**: .NET 框架 4.5</span><span class="sxs-lookup"><span data-stu-id="b0553-355">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="b0553-356">對於冷網站啟動,不僅必須從磁碟讀取程式集,而且必須編譯網站。</span><span class="sxs-lookup"><span data-stu-id="b0553-356">For a cold site startup, not only do assemblies have to be read from disk, but the site must be JIT-compiled.</span></span> <span data-ttu-id="b0553-357">對於複雜的網站,這可能會增加明顯的延遲。</span><span class="sxs-lookup"><span data-stu-id="b0553-357">For a complex site, this can add significant delays.</span></span> <span data-ttu-id="b0553-358">.NET Framework 4.5 中的一種新的通用技術通過在可用的處理器內核中擴展 JIT 編譯來減少這些延遲。</span><span class="sxs-lookup"><span data-stu-id="b0553-358">A new general-purpose technique in the .NET Framework 4.5 reduces these delays by spreading JIT-compilation across available processor cores.</span></span> <span data-ttu-id="b0553-359">它通過使用在以前發佈網站期間收集的信息,盡可能早地這樣做。</span><span class="sxs-lookup"><span data-stu-id="b0553-359">It does this as much and as early as possible by using information gathered during previous launches of the site.</span></span> <span data-ttu-id="b0553-360">此功能由[系統.運行時.配置檔優化.啟動配置檔](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx)方法實現。</span><span class="sxs-lookup"><span data-stu-id="b0553-360">This functionality implemented by the [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) method.</span></span>

<span data-ttu-id="b0553-361">默認情況下,使用多個內核進行 JIT 編譯 ASP.NET,因此您無需執行任何操作來利用此功能。</span><span class="sxs-lookup"><span data-stu-id="b0553-361">JIT-compiling using multiple cores is enabled by default in ASP.NET, so you do not need to do anything to take advantage of this feature.</span></span> <span data-ttu-id="b0553-362">如果要關閉此功能,請在 Web.config 檔中進行以下設定:</span><span class="sxs-lookup"><span data-stu-id="b0553-362">If you want to disable this feature, make the following setting in the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a><span data-ttu-id="b0553-363">調整垃圾資源以最佳化記憶體</span><span class="sxs-lookup"><span data-stu-id="b0553-363">Tuning garbage collection to optimize for memory</span></span>

<span data-ttu-id="b0553-364">**要求**: .NET 框架 4.5</span><span class="sxs-lookup"><span data-stu-id="b0553-364">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="b0553-365">網站運行后,其使用垃圾回收器 (GC) 堆可能是其記憶體消耗的重要因素。</span><span class="sxs-lookup"><span data-stu-id="b0553-365">Once a site is running, its use of the garbage-collector (GC) heap can be a significant factor in its memory consumption.</span></span> <span data-ttu-id="b0553-366">與任何垃圾回收器一樣,.NET框架 GC 在 CPU 時間(集合的頻率和重要性)和記憶體消耗(用於新、釋放或自由的物件的額外空間)之間進行權衡。</span><span class="sxs-lookup"><span data-stu-id="b0553-366">Like any garbage collector, the .NET Framework GC makes tradeoffs between CPU time (frequency and significance of collections) and memory consumption (extra space that is used for new, freed, or free-able objects).</span></span> <span data-ttu-id="b0553-367">對於以前的版本,我們提供了有關如何配置 GC 以實現適當平衡的指導(例如,請參閱[ASP.NET 2.0/3.5 共享主機配置](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration))。</span><span class="sxs-lookup"><span data-stu-id="b0553-367">For previous releases, we have provided guidance on how to configure the GC to achieve the right balance (for example, see [ASP.NET 2.0/3.5 Shared Hosting Configuration](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).</span></span>

<span data-ttu-id="b0553-368">對於 .NET Framework 4.5,提供工作負載定義的配置設置,該設置支援以前建議的所有 GC 設置以及為每個網站工作集提供額外性能的新調優。</span><span class="sxs-lookup"><span data-stu-id="b0553-368">For the .NET Framework 4.5, instead of multiple standalone settings, a workload-defined configuration setting is available that enables all of the previously recommended GC settings as well as new tuning that delivers additional performance for the per-site working set.</span></span>

<span data-ttu-id="b0553-369">要啟用 GC 記憶體調優,請向 Windows_Microsoft.NET_Framework_v4.0.30319_aspnet.config 檔添加以下設置:</span><span class="sxs-lookup"><span data-stu-id="b0553-369">To enable GC memory tuning, add the following setting to the Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

<span data-ttu-id="b0553-370">(如果您熟悉之前對 aspnet.config 的更改指南,請注意此設置將替換舊設置,例如,無需設置 gcServer、gc併發等。您不必刪除舊設定。</span><span class="sxs-lookup"><span data-stu-id="b0553-370">(If you're familiar with the previous guidance for changes to aspnet.config, note that this setting replaces the old settings — for example, there is no need to set gcServer, gcConcurrent, etc. You do not have to remove the old settings.)</span></span>

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a><span data-ttu-id="b0553-371">為 Web 應用程式預取</span><span class="sxs-lookup"><span data-stu-id="b0553-371">Prefetching for web applications</span></span>

<span data-ttu-id="b0553-372">**要求**: .NET 架構 4.5 在 Windows 8 上執行</span><span class="sxs-lookup"><span data-stu-id="b0553-372">**Requirement**: .NET Framework 4.5 running on Windows 8</span></span>

<span data-ttu-id="b0553-373">對於多個版本,Windows 包含一種稱為[預取器](http://en.wikipedia.org/wiki/Prefetcher)的技術,可降低應用程式啟動的磁碟讀取成本。</span><span class="sxs-lookup"><span data-stu-id="b0553-373">For several releases, Windows has included a technology known as the [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) that reduces the disk-read cost of application startup.</span></span> <span data-ttu-id="b0553-374">由於冷啟動主要針對用戶端應用程式,因此此技術未包含在 Windows Server 中,該伺服器僅包含對伺服器至關重要的元件。</span><span class="sxs-lookup"><span data-stu-id="b0553-374">Because cold startup is a problem predominantly for client applications, this technology has not been included in Windows Server, which includes only components that are essential to a server.</span></span> <span data-ttu-id="b0553-375">預取現已在最新版本的 Windows Server 中提供,它可以優化單個網站的啟動。</span><span class="sxs-lookup"><span data-stu-id="b0553-375">Prefetching is now available in the latest version of Windows Server, where it can optimize the launch of individual websites.</span></span>

<span data-ttu-id="b0553-376">對於 Windows 伺服器,預設情況下未啟用預取器。</span><span class="sxs-lookup"><span data-stu-id="b0553-376">For Windows Server, the prefetcher is not enabled by default.</span></span> <span data-ttu-id="b0553-377">要啟用與設定高密度 Web 託管的預取器,請在命令列上執行以下命令集:</span><span class="sxs-lookup"><span data-stu-id="b0553-377">To enable and configure the prefetcher for high-density web hosting, run the following set of commands at the command line:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

<span data-ttu-id="b0553-378">然後,要將預取器與ASP.NET應用程式整合,請向 Web.config 檔案新增以下內容:</span><span class="sxs-lookup"><span data-stu-id="b0553-378">Then, to integrate the prefetcher with ASP.NET applications, add the following to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="b0553-379">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="b0553-379">ASP.NET Web Forms</span></span>

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a><span data-ttu-id="b0553-380">強型別資料控制項</span><span class="sxs-lookup"><span data-stu-id="b0553-380">Strongly Typed Data Controls</span></span>

<span data-ttu-id="b0553-381">在 ASP.NET 4.5 中,Web 窗體包括一些用於處理數據的改進。</span><span class="sxs-lookup"><span data-stu-id="b0553-381">In ASP.NET 4.5, Web Forms includes some improvements for working with data.</span></span> <span data-ttu-id="b0553-382">第一個改進是強類型數據控制。</span><span class="sxs-lookup"><span data-stu-id="b0553-382">The first improvement is strongly typed data controls.</span></span> <span data-ttu-id="b0553-383">對於早期版本的 ASP.NET 中的 Web 窗體控制項,使用*Eval*和資料繫式顯示資料繫結度值:</span><span class="sxs-lookup"><span data-stu-id="b0553-383">For Web Forms controls in previous versions of ASP.NET, you display a data-bound value using *Eval* and a data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

<span data-ttu-id="b0553-384">對雙向資料繫結,請使用*連結 :*</span><span class="sxs-lookup"><span data-stu-id="b0553-384">For two-way data binding, you use *Bind*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

<span data-ttu-id="b0553-385">在運行時,這些調用使用反射讀取指定成員的值,然後在標記中顯示結果。</span><span class="sxs-lookup"><span data-stu-id="b0553-385">At run time, these calls use reflection to read the value of the specified member and then display the result in the markup.</span></span> <span data-ttu-id="b0553-386">此方法使數據與任意、未成形的數據綁定變得容易。</span><span class="sxs-lookup"><span data-stu-id="b0553-386">This approach makes it easy to data bind against arbitrary, unshaped data.</span></span>

<span data-ttu-id="b0553-387">但是,像這樣的數據綁定表達式不支援諸如成員名稱的 IntelliSense、導航(如轉到定義)或對這些名稱的編譯時間檢查等功能。</span><span class="sxs-lookup"><span data-stu-id="b0553-387">However, data-binding expressions like this don't support features like IntelliSense for member names, navigation (like Go To Definition), or compile-time checking for these names.</span></span>

<span data-ttu-id="b0553-388">為了解決此問題,ASP.NET 4.5 添加了聲明控制件綁定到的數據的數據類型的能力。</span><span class="sxs-lookup"><span data-stu-id="b0553-388">To address this issue, ASP.NET 4.5 adds the ability to declare the data type of the data that a control is bound to.</span></span> <span data-ttu-id="b0553-389">使用新的*ItemType*屬性執行此操作。</span><span class="sxs-lookup"><span data-stu-id="b0553-389">You do this using the new *ItemType* property.</span></span> <span data-ttu-id="b0553-390">設定此屬性時,資料繫式的作用區中有兩個新的類型變數 *:Item*和*BindItem*。</span><span class="sxs-lookup"><span data-stu-id="b0553-390">When you set this property, two new typed variables are available in the scope of data-binding expressions: *Item* and *BindItem*.</span></span> <span data-ttu-id="b0553-391">由於變數是強類型,因此您可以獲得 Visual Studio 開發體驗的全部優勢。</span><span class="sxs-lookup"><span data-stu-id="b0553-391">Because the variables are strongly typed, you get the full benefits of the Visual Studio development experience.</span></span>

<span data-ttu-id="b0553-392">對於雙向資料繫式,請使用*BindItem*變數:</span><span class="sxs-lookup"><span data-stu-id="b0553-392">For two-way data-binding expressions, use the *BindItem* variable:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

<span data-ttu-id="b0553-393">ASP.NET Web 窗體框架中支援數據綁定的大多數控制項都已更新以支援*ItemType*屬性。</span><span class="sxs-lookup"><span data-stu-id="b0553-393">Most controls in the ASP.NET Web Forms framework that support data binding have been updated to support the *ItemType* property.</span></span>

<a id="_Toc318097387"></a>
### <a name="model-binding"></a><span data-ttu-id="b0553-394">模型繫結</span><span class="sxs-lookup"><span data-stu-id="b0553-394">Model Binding</span></span>

<span data-ttu-id="b0553-395">模型綁定擴展了ASP.NET Web 窗體控件中的數據綁定,以便使用以代碼為中心的數據訪問。</span><span class="sxs-lookup"><span data-stu-id="b0553-395">Model binding extends data binding in ASP.NET Web Forms controls to work with code-focused data access.</span></span> <span data-ttu-id="b0553-396">它包含*了 ObjectDataSource*控制項和模型綁定中的概念ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="b0553-396">It incorporates concepts from the *ObjectDataSource* control and from model binding in ASP.NET MVC.</span></span>

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a><span data-ttu-id="b0553-397">選擇資料</span><span class="sxs-lookup"><span data-stu-id="b0553-397">Selecting data</span></span>

<span data-ttu-id="b0553-398">要將數據控制項配置為使用模型綁定來選擇資料,請將控制項的*SelectMethod*屬性設定為頁面代碼中的方法的名稱。</span><span class="sxs-lookup"><span data-stu-id="b0553-398">To configure a data control to use model binding to select data, you set the control's *SelectMethod* property to the name of a method in the page's code.</span></span> <span data-ttu-id="b0553-399">數據控件在頁面生命週期中的適當時間調用該方法,並自動綁定返回的數據。</span><span class="sxs-lookup"><span data-stu-id="b0553-399">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="b0553-400">無需顯式調用*DataBind*方法。</span><span class="sxs-lookup"><span data-stu-id="b0553-400">There's no need to explicitly call the *DataBind* method.</span></span>

<span data-ttu-id="b0553-401">在下面的範例中 *,GridView*控制項組設定為使用名為*GetCategories*的方法 :</span><span class="sxs-lookup"><span data-stu-id="b0553-401">In the following example, the *GridView* control is configured to use a method named *GetCategories*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

<span data-ttu-id="b0553-402">在頁面的代碼中創建*GetCategories*方法。</span><span class="sxs-lookup"><span data-stu-id="b0553-402">You create the *GetCategories* method in the page's code.</span></span> <span data-ttu-id="b0553-403">對於簡單的選擇操作,該方法不需要任何參數,並且應返回*IE50 或* *IQuery 物件*。</span><span class="sxs-lookup"><span data-stu-id="b0553-403">For a simple select operation, the method needs no parameters and should return an *IEnumerable* or *IQueryable* object.</span></span> <span data-ttu-id="b0553-404">如果設置了新的*ItemType*屬性(啟用強類型數據綁定表達式,如前面在[強類型數據控件](#_Toc318097386)中所述),則應返回這些介面的泛型版本 - *&lt;&gt;IE5500t*或*IQuery&lt;&gt;T,T\*\*參數匹配* *ItemType*屬性的類型(例如 *,IQuery&lt;類別&gt;*)。</span><span class="sxs-lookup"><span data-stu-id="b0553-404">If the new *ItemType* property is set (which enables strongly typed data-binding expressions, as explained under [Strongly Typed Data Controls](#_Toc318097386) earlier), the generic versions of these interfaces should be returned — *IEnumerable&lt;T&gt;* or *IQueryable&lt;T&gt;*, with the *T* parameter matching the type of the *ItemType* property (for example, *IQueryable&lt;Category&gt;*).</span></span>

<span data-ttu-id="b0553-405">下面的範例顯示了*GetCategories*方法的代碼。</span><span class="sxs-lookup"><span data-stu-id="b0553-405">The following example shows the code for a *GetCategories* method.</span></span> <span data-ttu-id="b0553-406">本示例使用實體框架代碼第一模型與北風示例資料庫。</span><span class="sxs-lookup"><span data-stu-id="b0553-406">This example uses the Entity Framework Code First model with the Northwind sample database.</span></span> <span data-ttu-id="b0553-407">代碼確保查詢通過 *「包括」* 方法傳回每個類別的相關產品的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b0553-407">The code makes sure that the query returns details of the related products for each category by way of the *Include* method.</span></span> <span data-ttu-id="b0553-408">(這可確保標記中的*樣本欄位*元素顯示每個類別中的產品計數,而無需[n+1 選擇](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)</span><span class="sxs-lookup"><span data-stu-id="b0553-408">(This ensures that the *TemplateField* element in the markup displays the count of products in each category without requiring an [n+1 select](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

<span data-ttu-id="b0553-409">當頁面執行時 *,GridView*控制檔會自動呼叫*GetCategories*方法,並使用設定的欄位呈現傳回的資料:</span><span class="sxs-lookup"><span data-stu-id="b0553-409">When the page runs, the *GridView* control calls the *GetCategories* method automatically and renders the returned data using the configured fields:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

<span data-ttu-id="b0553-410">由於選擇方法返回*IQuery 物件*,因此*GridView*控件可以在執行查詢之前進一步操作查詢。</span><span class="sxs-lookup"><span data-stu-id="b0553-410">Because the select method returns an *IQueryable* object, the *GridView* control can further manipulate the query before executing it.</span></span> <span data-ttu-id="b0553-411">例如 *,GridView*控件可以在執行返回*的 IQuery 物件*之前將用於排序和分頁的查詢表達式添加到返回的 IQuery 物件,以便這些操作由基礎 LINQ 提供程式執行。</span><span class="sxs-lookup"><span data-stu-id="b0553-411">For example, the *GridView* control can add query expressions for sorting and paging to the returned *IQueryable* object before it is executed, so that those operations are performed by the underlying LINQ provider.</span></span> <span data-ttu-id="b0553-412">在這種情況下,實體框架將確保在資料庫中執行這些操作。</span><span class="sxs-lookup"><span data-stu-id="b0553-412">In this case, Entity Framework will ensure those operations are performed in the database.</span></span>

<span data-ttu-id="b0553-413">下面的範例顯示已修改的*GridView*控制項以允許排序和分頁:</span><span class="sxs-lookup"><span data-stu-id="b0553-413">The following example shows the *GridView* control modified to allow sorting and paging:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

<span data-ttu-id="b0553-414">現在,當頁面運行時,控制項可以確保只顯示當前資料頁,並且數據按所選列排序:</span><span class="sxs-lookup"><span data-stu-id="b0553-414">Now when the page runs, the control can make sure that only the current page of data is displayed and that it's ordered by the selected column:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

<span data-ttu-id="b0553-415">要篩選返回的數據,必須將參數添加到選擇方法。</span><span class="sxs-lookup"><span data-stu-id="b0553-415">To filter the returned data, parameters have to be added to the select method.</span></span> <span data-ttu-id="b0553-416">這些參數將在執行時由模型綁定填充,您可以在返回數據之前使用它們來更改查詢。</span><span class="sxs-lookup"><span data-stu-id="b0553-416">These parameters will be populated by the model binding at run time, and you can use them to alter the query before returning the data.</span></span>

<span data-ttu-id="b0553-417">例如,假設您要通過在查詢字串中輸入關鍵字來允許使用者篩選產品。</span><span class="sxs-lookup"><span data-stu-id="b0553-417">For example, assume that you want to let users filter products by entering a keyword in the query string.</span></span> <span data-ttu-id="b0553-418">您可以將參數加入方法並更新代碼以使用參數值:</span><span class="sxs-lookup"><span data-stu-id="b0553-418">You can add a parameter to the method and update the code to use the parameter value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

<span data-ttu-id="b0553-419">如果為*關鍵字*提供了值,然後返回查詢結果,則此代碼包括*Where*表達式。</span><span class="sxs-lookup"><span data-stu-id="b0553-419">This code includes a *Where* expression if a value is provided for *keyword* and then returns the query results.</span></span>

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a><span data-ttu-id="b0553-420">價值提供者</span><span class="sxs-lookup"><span data-stu-id="b0553-420">Value providers</span></span>

<span data-ttu-id="b0553-421">前面的範例沒有具體說明*關鍵字*參數的值來自何處。</span><span class="sxs-lookup"><span data-stu-id="b0553-421">The previous example was not specific about where the value for the *keyword* parameter was coming from.</span></span> <span data-ttu-id="b0553-422">要指示此資訊,可以使用參數屬性。</span><span class="sxs-lookup"><span data-stu-id="b0553-422">To indicate this information, you can use a parameter attribute.</span></span> <span data-ttu-id="b0553-423">在此範例中,可以使用*System.Web.Model 綁定*命名空間中的*QueryStringattribute*類:</span><span class="sxs-lookup"><span data-stu-id="b0553-423">For this example, you can use the *QueryStringAttribute* class that's in the *System.Web.ModelBinding* namespace:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

<span data-ttu-id="b0553-424">這指示模型綁定嘗試在運行時將值從查詢字串綁定到*關鍵字*參數。</span><span class="sxs-lookup"><span data-stu-id="b0553-424">This instructs model binding to try to bind a value from the query string to the *keyword* parameter at run time.</span></span> <span data-ttu-id="b0553-425">(這可能涉及執行類型轉換,儘管在這種情況下不執行。如果無法提供值且類型不可為空,則引發異常。</span><span class="sxs-lookup"><span data-stu-id="b0553-425">(This might involve performing type conversion, although it doesn't in this case.) If a value cannot be provided and the type is non-nullable, an exception is thrown.</span></span>

<span data-ttu-id="b0553-426">這些方法的值源稱為值提供程式,指示要使用的值提供程式的參數屬性稱為值提供程式屬性。</span><span class="sxs-lookup"><span data-stu-id="b0553-426">The sources of values for these methods are referred to as value providers, and the parameter attributes that indicate which value provider to use are referred to as value provider attributes.</span></span> <span data-ttu-id="b0553-427">Web 表單組會包括 Web 窗體應用程式中所有典型使用者輸入來源的值提供程式和相應屬性,例如查詢字串、Cookie、窗體值、控制件、檢視狀態、工作階段狀態和設定檔屬性。</span><span class="sxs-lookup"><span data-stu-id="b0553-427">Web Forms will include value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="b0553-428">您還可以編寫自定義值提供程式。</span><span class="sxs-lookup"><span data-stu-id="b0553-428">You can also write custom value providers.</span></span>

<span data-ttu-id="b0553-429">預設情況下,參數名稱用作在值提供程式集合中查找值的鍵。</span><span class="sxs-lookup"><span data-stu-id="b0553-429">By default, the parameter name is used as the key to find a value in the value provider collection.</span></span> <span data-ttu-id="b0553-430">在此示例中,代碼將查找名為關鍵字的查詢字串值(例如,\*/default.aspx?關鍵字_chef)。</span><span class="sxs-lookup"><span data-stu-id="b0553-430">In the example, the code will look for a query-string value named keyword (for example, ~/default.aspx?keyword=chef).</span></span> <span data-ttu-id="b0553-431">可以通過將自定義鍵作為參數傳遞給參數屬性來指定它。</span><span class="sxs-lookup"><span data-stu-id="b0553-431">You can specify a custom key by passing it as an argument to the parameter attribute.</span></span> <span data-ttu-id="b0553-432">例如,要使用名為 q 的查詢字串變數的值,可以執行此操作:</span><span class="sxs-lookup"><span data-stu-id="b0553-432">For example, to use the value of the query-string variable named q, you could do this:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

<span data-ttu-id="b0553-433">如果此方法位於頁面的代碼中,使用者可以透過使用查詢字串傳遞關鍵字來篩選結果:</span><span class="sxs-lookup"><span data-stu-id="b0553-433">If this method is in the page's code, users can filter the results by passing a keyword using the query string:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

<span data-ttu-id="b0553-434">模型繫結完成許多工作,否則您必須手動編寫代碼:讀取值、檢查空值、嘗試將其轉換為適當的類型、檢查轉換是否成功,最後使用查詢中的值。</span><span class="sxs-lookup"><span data-stu-id="b0553-434">Model binding accomplishes many tasks that you would otherwise have to code by hand: reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="b0553-435">模型綁定導致的代碼少得多,並且能夠在整個應用程式中重用該功能。</span><span class="sxs-lookup"><span data-stu-id="b0553-435">Model binding results in far less code and in the ability to reuse the functionality throughout your application.</span></span>

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a><span data-ttu-id="b0553-436">依控制項的值篩選</span><span class="sxs-lookup"><span data-stu-id="b0553-436">Filtering by values from a control</span></span>

<span data-ttu-id="b0553-437">假設您要擴展示例,以便使用者從下拉清單中選擇篩選器值。</span><span class="sxs-lookup"><span data-stu-id="b0553-437">Suppose you want to extend the example to let the user choose a filter value from a drop-down list.</span></span> <span data-ttu-id="b0553-438">將以下下拉清單加入到標記中,並將其設定為使用*SelectMethod*屬性從其他方法取得其資料:</span><span class="sxs-lookup"><span data-stu-id="b0553-438">Add the following drop-down list to the markup and configure it to get its data from another method using the *SelectMethod* property:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

<span data-ttu-id="b0553-439">通常,您還會向*GridView*控制件添加*EmptyDataTemplate*元素,以便在找不到符合的產品時,控制項將顯示一條訊息:</span><span class="sxs-lookup"><span data-stu-id="b0553-439">Typically you would also add an *EmptyDataTemplate* element to the *GridView* control so that the control will display a message if no matching products are found:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

<span data-ttu-id="b0553-440">在頁面代碼中,為下拉清單添加新的 select 方法:</span><span class="sxs-lookup"><span data-stu-id="b0553-440">In the page code, add the new select method for the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

<span data-ttu-id="b0553-441">最後,更新*GetProducts*選擇方法,從下拉清單中獲取包含所選類別 ID 的新參數:</span><span class="sxs-lookup"><span data-stu-id="b0553-441">Finally, update the *GetProducts* select method to take a new parameter that contains the ID of the selected category from the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

<span data-ttu-id="b0553-442">現在,當頁面運行時,用戶可以從下拉清單中選擇一個類別,並且*GridView*控件將自動重新綁定以顯示篩選的資料。</span><span class="sxs-lookup"><span data-stu-id="b0553-442">Now when the page runs, users can select a category from the drop-down list, and the *GridView* control is automatically re-bound to show the filtered data.</span></span> <span data-ttu-id="b0553-443">這是可能的,因為模型綁定跟蹤選定方法的參數值,並檢測任何參數值在回退後是否已更改。</span><span class="sxs-lookup"><span data-stu-id="b0553-443">This is possible because model binding tracks the values of parameters for select methods and detects whether any parameter value has changed after a postback.</span></span> <span data-ttu-id="b0553-444">如果是這樣,模型綁定強制關聯的數據控件重新綁定到數據。</span><span class="sxs-lookup"><span data-stu-id="b0553-444">If so, model binding forces the associated data control to re-bind to the data.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a><span data-ttu-id="b0553-445">HTML 編碼資料繫結表示式</span><span class="sxs-lookup"><span data-stu-id="b0553-445">HTML Encoded Data-Binding Expressions</span></span>

<span data-ttu-id="b0553-446">現在,您可以對資料綁定表達式的結果進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="b0553-446">You can now HTML-encode the result of data-binding expressions.</span></span> <span data-ttu-id="b0553-447">新增冒號(:)標記資料繫結表示式的&lt;%# 前置字尾的尾尾:</span><span class="sxs-lookup"><span data-stu-id="b0553-447">Add a colon (:) to the end of the &lt;%# prefix that marks the data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a><span data-ttu-id="b0553-448">不顯眼的驗證</span><span class="sxs-lookup"><span data-stu-id="b0553-448">Unobtrusive Validation</span></span>

<span data-ttu-id="b0553-449">現在,您可以將內建驗證器控制項配置為對用戶端驗證邏輯使用不顯眼的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="b0553-449">You can now configure the built-in validator controls to use unobtrusive JavaScript for client-side validation logic.</span></span> <span data-ttu-id="b0553-450">這大大減少了頁面標記中內聯呈現的 JavaScript 量,並減小了整個頁面大小。</span><span class="sxs-lookup"><span data-stu-id="b0553-450">This significantly reduces the amount of JavaScript rendered inline in the page markup and reduces the overall page size.</span></span> <span data-ttu-id="b0553-451">您可以透過以下任何方式為驗證器控制項設定不顯眼的 JavaScript:</span><span class="sxs-lookup"><span data-stu-id="b0553-451">You can configure unobtrusive JavaScript for validator controls in any of these ways:</span></span>

- <span data-ttu-id="b0553-452">以從 Web.config 檔案*&lt;中&gt;的應用程式設定*元素新增以下設定,從而全域:</span><span class="sxs-lookup"><span data-stu-id="b0553-452">Globally by adding the following setting to the *&lt;appSettings&gt;* element in the Web.config file:</span></span> 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- <span data-ttu-id="b0553-453">通過將靜態*System.Web.UI.驗證設置.無顯眼驗證模式*屬性設置為 *"無顯眼驗證模式.WebForms"(* 通常在 Global.asax 檔中*的應用程式\_啟動*方法中),在全球範圍內。</span><span class="sxs-lookup"><span data-stu-id="b0553-453">Globally by setting the static *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* property to *UnobtrusiveValidationMode.WebForms* (typically in the *Application\_Start* method in the Global.asax file).</span></span>
- <span data-ttu-id="b0553-454">使用頁面類別的新 *「不顯眼驗證模式」* 屬性設定為 *「不顯眼驗證模式.WebForms」 ,* 單獨為*頁面*。</span><span class="sxs-lookup"><span data-stu-id="b0553-454">Individually for a page by setting the new *UnobtrusiveValidationMode* property of the *Page* class to *UnobtrusiveValidationMode.WebForms*.</span></span>

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a><span data-ttu-id="b0553-455">HTML5 更新</span><span class="sxs-lookup"><span data-stu-id="b0553-455">HTML5 Updates</span></span>

<span data-ttu-id="b0553-456">為了利用 HTML5 的新功能,對 Web 窗體伺服器控制件進行了一些改進:</span><span class="sxs-lookup"><span data-stu-id="b0553-456">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>

- <span data-ttu-id="b0553-457">*TextBox*控制項的*TextMode*屬性已更新以支援新的 HTML5 輸入類型,如*電子郵件*、*日期時間*等。</span><span class="sxs-lookup"><span data-stu-id="b0553-457">The *TextMode* property of the *TextBox* control has been updated to support the new HTML5 input types like *email*, *datetime*, and so on.</span></span>
- <span data-ttu-id="b0553-458">*FileUpload*控制項現在支援從支援此 HTML5 功能的瀏覽器上載多個檔。</span><span class="sxs-lookup"><span data-stu-id="b0553-458">The *FileUpload* control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
- <span data-ttu-id="b0553-459">驗證器控制項支援驗證 HTML5 輸入元素。</span><span class="sxs-lookup"><span data-stu-id="b0553-459">Validator controls now support validating HTML5 input elements.</span></span>
- <span data-ttu-id="b0553-460">具有表示 URL 屬性的新 HTML5 元素現在支援 runat_"server"。</span><span class="sxs-lookup"><span data-stu-id="b0553-460">New HTML5 elements that have attributes that represent a URL now support runat="server".</span></span> <span data-ttu-id="b0553-461">因此,您可以在 URL 路徑中使用 ASP.NET 約定,例如 \* 運算符來表示&lt;應用程式根(例如, 視頻 runat_" 伺服器 「 src_&gt;」 my Video.wmv"</span><span class="sxs-lookup"><span data-stu-id="b0553-461">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat="server" src="~/myVideo.wmv" /&gt;).</span></span>
- <span data-ttu-id="b0553-462">*UpdatePanel*控制件已修復,以支援過帳 HTML5 輸入欄位。</span><span class="sxs-lookup"><span data-stu-id="b0553-462">The *UpdatePanel* control has been fixed to support posting HTML5 input fields.</span></span>

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a><span data-ttu-id="b0553-463">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="b0553-463">ASP.NET MVC 4</span></span>

<span data-ttu-id="b0553-464">ASP.NET MVC 4 測試版現在包含在 Visual Studio 11 測試版中。</span><span class="sxs-lookup"><span data-stu-id="b0553-464">ASP.NET MVC 4 Beta is now included with Visual Studio 11 Beta.</span></span> <span data-ttu-id="b0553-465">ASP.NET MVC 是利用模型檢視控制器 (MVC) 模式開發高度可測試和可維護的 Web 應用程式的框架。</span><span class="sxs-lookup"><span data-stu-id="b0553-465">ASP.NET MVC is a framework for developing highly testable and maintainable Web applications by leveraging the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="b0553-466">ASP.NET MVC 4 使建置行動 Web 應用程式變得容易,並且包括 ASP.NET Web API,這有助於建構可覆寫任何設備的 HTTP 服務。</span><span class="sxs-lookup"><span data-stu-id="b0553-466">ASP.NET MVC 4 makes it easy to build applications for the mobile Web and includes ASP.NET Web API, which helps you build HTTP services that can reach any device.</span></span> <span data-ttu-id="b0553-467">有關詳細資訊,請參閱 ASP.NET [MVC 4 發行說明](mvc4-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="b0553-467">For more information, see the [ASP.NET MVC 4 Release Notes](mvc4-release-notes.md).</span></span>

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a><span data-ttu-id="b0553-468">ASP.NET Web Pages 2</span><span class="sxs-lookup"><span data-stu-id="b0553-468">ASP.NET Web Pages 2</span></span>

<span data-ttu-id="b0553-469">新功能包括以下內容:</span><span class="sxs-lookup"><span data-stu-id="b0553-469">New features include the following:</span></span>

- <span data-ttu-id="b0553-470">新建和更新的網站範本。</span><span class="sxs-lookup"><span data-stu-id="b0553-470">New and updated site templates.</span></span>
- <span data-ttu-id="b0553-471">使用*驗證*幫助程式添加伺服器端和客戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="b0553-471">Adding server-side and client-side validation using the *Validation* helper.</span></span>
- <span data-ttu-id="b0553-472">使用資產管理註冊腳本的功能。</span><span class="sxs-lookup"><span data-stu-id="b0553-472">The ability to register scripts using an assets manager.</span></span>
- <span data-ttu-id="b0553-473">使用 OAuth 和 OpenID 啟用來自 Facebook 和其他網站的登錄。</span><span class="sxs-lookup"><span data-stu-id="b0553-473">Enabling logins from Facebook and other sites using OAuth and OpenID.</span></span>
- <span data-ttu-id="b0553-474">使用地圖說明器新增*地圖*。</span><span class="sxs-lookup"><span data-stu-id="b0553-474">Adding maps using the *Maps* helper.</span></span>
- <span data-ttu-id="b0553-475">並排運行網頁應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0553-475">Running Web Pages applications side-by-side.</span></span>
- <span data-ttu-id="b0553-476">移動設備的呈現頁面。</span><span class="sxs-lookup"><span data-stu-id="b0553-476">Rendering pages for mobile devices.</span></span>

<span data-ttu-id="b0553-477">有關這些功能和整頁代碼範例的詳細資訊,請參閱[網頁 2 Beta 中的頂部功能](https://go.microsoft.com/fwlink/?LinkID=227824)。</span><span class="sxs-lookup"><span data-stu-id="b0553-477">For more information about these features and full-page code examples, see [The Top Features in Web Pages 2 Beta](https://go.microsoft.com/fwlink/?LinkID=227824).</span></span>

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a><span data-ttu-id="b0553-478">視覺化 Web 開發人員 11 測試版</span><span class="sxs-lookup"><span data-stu-id="b0553-478">Visual Web Developer 11 Beta</span></span>

<span data-ttu-id="b0553-479">本節提供有關可視化 Web 開發人員 11 Beta 和可視化工作室 2012 版本候選版中 Web 開發改進的資訊。</span><span class="sxs-lookup"><span data-stu-id="b0553-479">This section provides information about improvements for web development in Visual Web Developer 11 Beta and Visual Studio 2012 Release Candidate.</span></span>

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a><span data-ttu-id="b0553-480">Visual Studio 2010 和 Visual Studio 2012 版本候選版本之間的項目共享(專案相容性)</span><span class="sxs-lookup"><span data-stu-id="b0553-480">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>

<span data-ttu-id="b0553-481">在 Visual Studio 2012 發佈候選版之前,在較新版本的 Visual Studio 中打開現有項目啟動了轉換嚮導。</span><span class="sxs-lookup"><span data-stu-id="b0553-481">Until Visual Studio 2012 Release Candidate, opening an existing project in a newer version of Visual Studio launched the Conversion Wizard.</span></span> <span data-ttu-id="b0553-482">這迫使專案的內容(資產)和解決方案升級到不向後相容的新格式。</span><span class="sxs-lookup"><span data-stu-id="b0553-482">This forced an upgrade of the content (assets) of a project and solution to new formats that were not backward compatible.</span></span> <span data-ttu-id="b0553-483">因此,轉換後,您無法在舊版本的 Visual Studio 中打開專案。</span><span class="sxs-lookup"><span data-stu-id="b0553-483">Therefore, after the conversion you could not open the project in the older version of Visual Studio.</span></span>

<span data-ttu-id="b0553-484">許多客戶告訴我們,這不是正確的方法。</span><span class="sxs-lookup"><span data-stu-id="b0553-484">Many customers have told us that this was not the right approach.</span></span> <span data-ttu-id="b0553-485">在 Visual Studio 11 Beta 中,我們現在支援與 Visual Studio 2010 SP1 共用專案和解決方案。</span><span class="sxs-lookup"><span data-stu-id="b0553-485">In Visual Studio 11 Beta, we now support sharing projects and solutions with Visual Studio 2010 SP1.</span></span> <span data-ttu-id="b0553-486">這意味著,如果您在 Visual Studio 2012 版本候選版中打開 2010 年專案,您仍然可以在 Visual Studio 2010 SP1 中打開該專案。</span><span class="sxs-lookup"><span data-stu-id="b0553-486">This means that if you open a 2010 project in Visual Studio 2012 Release Candidate, you will still be able to open the project in Visual Studio 2010 SP1.</span></span>

> [!NOTE]
> <span data-ttu-id="b0553-487">幾種類型的專案不能在 Visual Studio 2010 SP1 和 Visual Studio 2012 版本候選版之間共用。</span><span class="sxs-lookup"><span data-stu-id="b0553-487">A few types of projects cannot be shared between Visual Studio 2010 SP1 and Visual Studio 2012 Release Candidate.</span></span> <span data-ttu-id="b0553-488">其中包括一些較舊的專案(如ASP.NET MVC 2 專案)或用於特殊目的的專案(如安裝程式專案)。</span><span class="sxs-lookup"><span data-stu-id="b0553-488">These include some older projects (such as ASP.NET MVC 2 projects) or projects for special purposes (such as Setup projects).</span></span>

<span data-ttu-id="b0553-489">首次在 Visual Studio 11 Beta 開啟 Visual Studio 2010 SP1 Web 專案時,以下屬性將新增到專案檔中:</span><span class="sxs-lookup"><span data-stu-id="b0553-489">When you open a Visual Studio 2010 SP1 Web project for the first time in Visual Studio 11 Beta, the following properties are added to the project file:</span></span>

- <span data-ttu-id="b0553-490">檔案升級標誌</span><span class="sxs-lookup"><span data-stu-id="b0553-490">FileUpgradeFlags</span></span>
- <span data-ttu-id="b0553-491">升級備份位置</span><span class="sxs-lookup"><span data-stu-id="b0553-491">UpgradeBackupLocation</span></span>
- <span data-ttu-id="b0553-492">舊工具版本</span><span class="sxs-lookup"><span data-stu-id="b0553-492">OldToolsVersion</span></span>
- <span data-ttu-id="b0553-493">VisualStudioVersion</span><span class="sxs-lookup"><span data-stu-id="b0553-493">VisualStudioVersion</span></span>
- <span data-ttu-id="b0553-494">VSToolsPath</span><span class="sxs-lookup"><span data-stu-id="b0553-494">VSToolsPath</span></span>

<span data-ttu-id="b0553-495">檔升級標誌、升級備份位置和舊工具版本由升級專案檔的過程使用。</span><span class="sxs-lookup"><span data-stu-id="b0553-495">FileUpgradeFlags, UpgradeBackupLocation, and OldToolsVersion are used by the process that upgrades the project file.</span></span> <span data-ttu-id="b0553-496">它們對在 Visual Studio 2010 中使用該專案沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="b0553-496">They have no impact on working with the project in Visual Studio 2010.</span></span>

<span data-ttu-id="b0553-497">VisualStudioVersion 是 MSBuild 4.5 使用的新屬性,用於指示當前專案的 Visual Studio 版本。</span><span class="sxs-lookup"><span data-stu-id="b0553-497">VisualStudioVersion is a new property used by MSBuild 4.5 that indicates the version of Visual Studio for the current project.</span></span> <span data-ttu-id="b0553-498">由於此屬性在 MSBuild 4.0 中不存在(Visual Studio 2010 SP1 使用的 MSBuild 版本),因此我們將預設值注入到專案檔中。</span><span class="sxs-lookup"><span data-stu-id="b0553-498">Because this property didn't exist in MSBuild 4.0 (the version of MSBuild that Visual Studio 2010 SP1 uses), we inject a default value into the project file.</span></span>

<span data-ttu-id="b0553-499">VSToolsPath 屬性用於確定要從 MSBuild 擴展器Path32 設置表示的路徑導入的正確 .target 檔。</span><span class="sxs-lookup"><span data-stu-id="b0553-499">The VSToolsPath property is used to determine the correct .targets file to import from the path represented by the MSBuildExtensionsPath32 setting.</span></span>

<span data-ttu-id="b0553-500">還有一些與導入元素相關的更改。</span><span class="sxs-lookup"><span data-stu-id="b0553-500">There are also some changes related to Import elements.</span></span> <span data-ttu-id="b0553-501">為了支援兩個版本的 Visual Studio 之間的相容性,需要進行這些更改。</span><span class="sxs-lookup"><span data-stu-id="b0553-501">These changes are required in order to support compatibility between both versions of Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="b0553-502">如果 Visual Studio 2010 SP1 和 Visual Studio 11 Beta 在兩台\_不同電腦上共用專案,並且該專案在應用 數據資料夾中包含本地資料庫,則必須確保資料庫使用的 SQL Server 版本安裝在兩台電腦上。</span><span class="sxs-lookup"><span data-stu-id="b0553-502">If a project is being shared between Visual Studio 2010 SP1 and Visual Studio 11 Beta on two different computers, and if the project includes a local database in the App\_Data folder, you must make sure that the version of SQL Server used by the database is installed on both computers.</span></span>

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a><span data-ttu-id="b0553-503">ASP.NET 4.5 網站樣本中的設定變更</span><span class="sxs-lookup"><span data-stu-id="b0553-503">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>

<span data-ttu-id="b0553-504">使用 Visual Studio 2012 版本候選版中的網站樣本建立的網站的預設*Web.config*檔進行了以下變更:</span><span class="sxs-lookup"><span data-stu-id="b0553-504">The following changes have been made to the default *Web.config* file for site that are created using website templates in Visual Studio 2012 Release Candidate:</span></span>

- <span data-ttu-id="b0553-505">在元素`<httpRuntime>`中,`encoderType`屬性現在預設設定為使用添加到ASP.NET的 AntiXSS 類型。</span><span class="sxs-lookup"><span data-stu-id="b0553-505">In the `<httpRuntime>` element, the `encoderType` attribute is now set by default to use the AntiXSS types that were added to ASP.NET.</span></span> <span data-ttu-id="b0553-506">有關詳細資訊,請參閱[AntiXSS 函式庫](#_Toc318097382)。</span><span class="sxs-lookup"><span data-stu-id="b0553-506">For details, see [AntiXSS Library](#_Toc318097382).</span></span>
- <span data-ttu-id="b0553-507">此外,在`<httpRuntime>`元素中,`requestValidationMode`屬性設置為"4.5"。</span><span class="sxs-lookup"><span data-stu-id="b0553-507">Also in the `<httpRuntime>` element, the `requestValidationMode` attribute is set to "4.5".</span></span> <span data-ttu-id="b0553-508">這意味著默認情況下,請求驗證配置為使用延遲("延遲")驗證。</span><span class="sxs-lookup"><span data-stu-id="b0553-508">This means that by default, request validation is configured to use deferred ("lazy") validation.</span></span> <span data-ttu-id="b0553-509">有關詳細資訊,請參閱[新ASP.NET請求驗證功能](#_Toc318097379)。</span><span class="sxs-lookup"><span data-stu-id="b0553-509">For details, see [New ASP.NET Request Validation Features](#_Toc318097379).</span></span>
- <span data-ttu-id="b0553-510">節`<modules>`元素`<system.webServer>`不包含屬性`runAllManagedModulesForAllRequests`。</span><span class="sxs-lookup"><span data-stu-id="b0553-510">The `<modules>` element of the `<system.webServer>` section does not contain a `runAllManagedModulesForAllRequests` attribute.</span></span> <span data-ttu-id="b0553-511">(其預設值為 false。這意味著,如果您使用的 IIS 7 版本尚未更新到 SP1,則新網站中的路由可能有問題。</span><span class="sxs-lookup"><span data-stu-id="b0553-511">(Its default value is false.) This means that if you are using a version of IIS 7 that has not been updated to SP1, you might have issues with routing in a new site.</span></span> <span data-ttu-id="b0553-512">有關詳細資訊,請參閱[IIS 7 中的本機支援,瞭解 ASP.NET 路由](#Native_Support_In_IIS7_For_ASPNET_Routine)。</span><span class="sxs-lookup"><span data-stu-id="b0553-512">For more information, see [Native Support in IIS 7 for ASP.NET Routing](#Native_Support_In_IIS7_For_ASPNET_Routine).</span></span>

<span data-ttu-id="b0553-513">這些更改不會影響現有應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0553-513">These changes do not affect existing applications.</span></span> <span data-ttu-id="b0553-514">但是,它們可能表示現有網站與您使用新範本為 ASP.NET 4.5 創建的新網站的行為差異。</span><span class="sxs-lookup"><span data-stu-id="b0553-514">However, they might represent a difference in behavior between existing websites and new websites that you create for ASP.NET 4.5 using the new templates.</span></span>

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a><span data-ttu-id="b0553-515">IIS 7 中用於ASP.NET路由的本機支援</span><span class="sxs-lookup"><span data-stu-id="b0553-515">Native Support in IIS 7 for ASP.NET Routing</span></span>

<span data-ttu-id="b0553-516">這不是對ASP.NET的更改,而是新網站項目的範本更改,如果您正在使用未應用SP1更新的IIS7版本,可能會影響您。</span><span class="sxs-lookup"><span data-stu-id="b0553-516">This is not a change to ASP.NET as such, but a change in templates for new website projects that can affect you if you are working a version of IIS 7 that has not had the SP1 update applied.</span></span>

<span data-ttu-id="b0553-517">在ASP.NET中,您可以將以下設定設定新增到應用程式中,以支援路由:</span><span class="sxs-lookup"><span data-stu-id="b0553-517">In ASP.NET, you can add the following configuration setting to applications in order to support routing:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

<span data-ttu-id="b0553-518">當**RunAll管理ModuleAll 請求**為`http://mysite/myapp/home`true 時, 即使 URL 上沒有 *.aspx、.mvc*或類似擴展,也可以 *.mvc*將類似 URL 轉到 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="b0553-518">When **runAllManagedModulesForAllRequests** is true, a URL like `http://mysite/myapp/home` goes to ASP.NET, even though there is no *.aspx*, *.mvc*, or similar extension on the URL.</span></span>

<span data-ttu-id="b0553-519">對 IIS 7 所做的更新使**runAll管理模組所有請求**設置變得不必要,並支援本機路由ASP.NET路由。</span><span class="sxs-lookup"><span data-stu-id="b0553-519">An update that was made to IIS 7 makes the **runAllManagedModulesForAllRequests** setting unnecessary and supports ASP.NET routing natively.</span></span> <span data-ttu-id="b0553-520">(有關更新的資訊,請參閱 Microsoft 支援文章[一個可用更新,使某些 IIS 7.0 或 IIS 7.5 處理程式能夠處理 URL 未以句點結尾的請求](https://support.microsoft.com/kb/980368)。</span><span class="sxs-lookup"><span data-stu-id="b0553-520">(For information about the update, see the Microsoft Support article [An update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).)</span></span>

<span data-ttu-id="b0553-521">如果您的網站在IIS 7上運行,並且IIS已更新,則無需將**執行All管理模組全部請求**設置為 true。</span><span class="sxs-lookup"><span data-stu-id="b0553-521">If your website is running on IIS 7 and if IIS has been updated, you do not need to set **runAllManagedModulesForAllRequests** to true.</span></span> <span data-ttu-id="b0553-522">事實上,不建議將其設置為 true,因為它會增加不必要的處理開銷。</span><span class="sxs-lookup"><span data-stu-id="b0553-522">In fact, setting it to true is not recommended, because it adds unnecessary processing overhead to request.</span></span> <span data-ttu-id="b0553-523">當此設置為 true 時,所有請求(包括 *.htm、.jpg*和其他靜態檔的請求)也會通過請求管道 *.jpg*ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="b0553-523">When this setting is true, all requests, including those for *.htm*, *.jpg*, and other static files, also go through the ASP.NET request pipeline.</span></span>

<span data-ttu-id="b0553-524">如果使用 Visual Studio 2012 RC 中提供的範本建立新 ASP.NET 4.5 網站,則網站的配置不包括**RunAll 管理模組全部請求**設置。</span><span class="sxs-lookup"><span data-stu-id="b0553-524">If you create a new ASP.NET 4.5 website using the templates that are provided in Visual Studio 2012 RC, the configuration for the website does not include the **runAllManagedModulesForAllRequests** setting.</span></span> <span data-ttu-id="b0553-525">這意味著默認情況下,該設置為 false。</span><span class="sxs-lookup"><span data-stu-id="b0553-525">This means that by default the setting is false.</span></span>

<span data-ttu-id="b0553-526">如果隨後在 Windows 7 上運行網站而不安裝 SP1,則 IIS 7 將不包含所需的更新。</span><span class="sxs-lookup"><span data-stu-id="b0553-526">If you then run the website on Windows 7 without SP1 installed, IIS 7 will not include the required update.</span></span> <span data-ttu-id="b0553-527">因此,路由將不起作用,您將看到錯誤。</span><span class="sxs-lookup"><span data-stu-id="b0553-527">As a consequence, routing will not work and you will see errors.</span></span> <span data-ttu-id="b0553-528">如果路由不起作用,可以執行以下任一操作:</span><span class="sxs-lookup"><span data-stu-id="b0553-528">If you have a problem where routing does not work, you can do either the following:</span></span>

- <span data-ttu-id="b0553-529">將 Windows 7 更新為 SP1,這將將更新添加到 IIS 7。</span><span class="sxs-lookup"><span data-stu-id="b0553-529">Update Windows 7 to SP1, which will add the update to IIS 7.</span></span>
- <span data-ttu-id="b0553-530">安裝前面列出的 Microsoft 支援文章中所述的更新。</span><span class="sxs-lookup"><span data-stu-id="b0553-530">Install the update that's described in the Microsoft Support article listed previously.</span></span>
- <span data-ttu-id="b0553-531">將**執行All管理模組所有請求**設置為 true,在該網站的 Web.config 檔中。</span><span class="sxs-lookup"><span data-stu-id="b0553-531">Set **runAllManagedModulesForAllRequests** to true in that website's Web.config file.</span></span> <span data-ttu-id="b0553-532">請注意,這將為請求增加一些開銷。</span><span class="sxs-lookup"><span data-stu-id="b0553-532">Note that this will add some overhead to requests.</span></span>

<a id="_Toc318097397"></a>
### <a name="html-editor"></a><span data-ttu-id="b0553-533">HTML 編輯器</span><span class="sxs-lookup"><span data-stu-id="b0553-533">HTML Editor</span></span>

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a><span data-ttu-id="b0553-534">智慧任務</span><span class="sxs-lookup"><span data-stu-id="b0553-534">Smart Tasks</span></span>

<span data-ttu-id="b0553-535">在"設計"檢視中,伺服器控制項的複雜屬性通常具有關聯的對話框和嚮導,以便輕鬆設置它們。</span><span class="sxs-lookup"><span data-stu-id="b0553-535">In Design view, complex properties of server controls often have associated dialog boxes and wizards to make it easy to set them.</span></span> <span data-ttu-id="b0553-536">例如,可以使用特殊的對話框向*中繼器*控制項添加資料源或向*GridView*控制件添加列。</span><span class="sxs-lookup"><span data-stu-id="b0553-536">For example, you can use a special dialog box to add a data source to a *Repeater* control or add columns to a *GridView* control.</span></span>

<span data-ttu-id="b0553-537">但是,針對複雜屬性的這種類型的 UI 説明在源視圖中不可用。</span><span class="sxs-lookup"><span data-stu-id="b0553-537">However, this type of UI help for complex properties has not been available in Source view.</span></span> <span data-ttu-id="b0553-538">因此,Visual Studio 11 引入了源視圖的智慧任務。</span><span class="sxs-lookup"><span data-stu-id="b0553-538">Therefore, Visual Studio 11 introduces Smart Tasks for Source view.</span></span> <span data-ttu-id="b0553-539">智慧任務是 C# 和 Visual Basic 編輯器中常用功能的上下文感知快捷方式。</span><span class="sxs-lookup"><span data-stu-id="b0553-539">Smart Tasks are context-aware shortcuts for commonly used features in the C# and Visual Basic editors.</span></span>

<span data-ttu-id="b0553-540">對於ASP.NET Web 表單控制項,當插入點位於元素內部時,智慧任務在伺服器標記上顯示為一個小字形:</span><span class="sxs-lookup"><span data-stu-id="b0553-540">For ASP.NET Web Forms controls, Smart Tasks appear on server tags as a small glyph when the insertion point is inside the element:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

<span data-ttu-id="b0553-541">按下字形或按 CTRL+時,智慧任務將展開。</span><span class="sxs-lookup"><span data-stu-id="b0553-541">The Smart Task expands when you click the glyph or press CTRL+.</span></span> <span data-ttu-id="b0553-542">(點),就像代碼編輯器一樣。</span><span class="sxs-lookup"><span data-stu-id="b0553-542">(dot), just as in the code editors.</span></span> <span data-ttu-id="b0553-543">然後,它顯示類似於"設計"視圖中的智慧任務的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="b0553-543">It then displays shortcuts that are similar to the Smart Tasks in Design view.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

<span data-ttu-id="b0553-544">例如,上圖中的智慧任務顯示了 GridView 任務選項。</span><span class="sxs-lookup"><span data-stu-id="b0553-544">For example, the Smart Task in the previous illustration shows the GridView Tasks options.</span></span> <span data-ttu-id="b0553-545">如果選擇「編輯列」,將顯示以下對話框:</span><span class="sxs-lookup"><span data-stu-id="b0553-545">If you choose Edit Columns, the following dialog box is displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

<span data-ttu-id="b0553-546">填寫對話框將設置可在「設計」檢視中設置的相同屬性。</span><span class="sxs-lookup"><span data-stu-id="b0553-546">Filling in the dialog box sets the same properties you can set in Design view.</span></span> <span data-ttu-id="b0553-547">按下「確定」時,控制項的標記將使用新設定更新:</span><span class="sxs-lookup"><span data-stu-id="b0553-547">When you click OK, the markup for the control is updated with the new settings:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a><span data-ttu-id="b0553-548">WAI-ARIA 支援</span><span class="sxs-lookup"><span data-stu-id="b0553-548">WAI-ARIA support</span></span>

<span data-ttu-id="b0553-549">編寫可訪問的網站變得越來越重要。</span><span class="sxs-lookup"><span data-stu-id="b0553-549">Writing accessible websites is becoming increasingly important.</span></span> <span data-ttu-id="b0553-550">[WAI-ARIA 輔助功能標準](http://www.w3.org/WAI/intro/aria)定義了開發人員應如何編寫可訪問的網站。</span><span class="sxs-lookup"><span data-stu-id="b0553-550">The [WAI-ARIA accessibility standard](http://www.w3.org/WAI/intro/aria) defines how developers should write accessible websites.</span></span> <span data-ttu-id="b0553-551">此標準現在完全支援在視覺工作室。</span><span class="sxs-lookup"><span data-stu-id="b0553-551">This standard is now fully supported in Visual Studio.</span></span>

<span data-ttu-id="b0553-552">例如,*角色*屬性現在具有完整的 IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="b0553-552">For example, the *role* attribute now has full IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

<span data-ttu-id="b0553-553">WAI-ARIA 標準還引入了以*aria-* 預先碼的屬性,這些屬性允許您向 HTML5 文件添加語義。</span><span class="sxs-lookup"><span data-stu-id="b0553-553">The WAI-ARIA standard also introduces attributes that are prefixed with *aria-* that let you add semantics to an HTML5 document.</span></span> <span data-ttu-id="b0553-554">Visual Studio 還完全支援這些*aria 屬性*:</span><span class="sxs-lookup"><span data-stu-id="b0553-554">Visual Studio also fully supports these *aria-* attributes:</span></span>

<span data-ttu-id="b0553-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="b0553-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span></span>

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a><span data-ttu-id="b0553-556">新的 HTML5 碼段</span><span class="sxs-lookup"><span data-stu-id="b0553-556">New HTML5 snippets</span></span>

<span data-ttu-id="b0553-557">為了使編寫常用的 HTML5 標籤更快、更容易,Visual Studio 包含許多代碼段。</span><span class="sxs-lookup"><span data-stu-id="b0553-557">To make it faster and easier to write commonly used HTML5 markup, Visual Studio includes a number of snippets.</span></span> <span data-ttu-id="b0553-558">例如視訊片段:</span><span class="sxs-lookup"><span data-stu-id="b0553-558">An example is the video snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

<span data-ttu-id="b0553-559">要呼叫代碼段,請在 IntelliSense 中選擇元素時按 Tab 兩次:</span><span class="sxs-lookup"><span data-stu-id="b0553-559">To invoke the snippet, press Tab twice when the element is selected in IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

<span data-ttu-id="b0553-560">這將生成可以自定義的代碼段。</span><span class="sxs-lookup"><span data-stu-id="b0553-560">This produces a snippet that you can customize.</span></span>

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a><span data-ttu-id="b0553-561">擷取使用者控制項</span><span class="sxs-lookup"><span data-stu-id="b0553-561">Extract to user control</span></span>

<span data-ttu-id="b0553-562">在大型網頁中,最好將單個片段移動到使用者控件中。</span><span class="sxs-lookup"><span data-stu-id="b0553-562">In large web pages, it can be a good idea to move individual pieces into user controls.</span></span> <span data-ttu-id="b0553-563">這種重構形式有助於提高頁面的可讀性,並可以簡化頁面結構。</span><span class="sxs-lookup"><span data-stu-id="b0553-563">This form of refactoring can help increase the readability of the page and can simplify the page structure.</span></span>

<span data-ttu-id="b0553-564">為了簡化此功能,當您在「源」檢視中編輯「Web 窗體」頁時,您現在可以選擇頁面中的文字,右鍵按一下它,然後選擇「提取到使用者控制」:</span><span class="sxs-lookup"><span data-stu-id="b0553-564">To make this easier, when you edit Web Forms pages in Source view, you can now select text in a page, right-click it, and then choose Extract to User Control:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a><span data-ttu-id="b0553-565">屬性中片段的 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="b0553-565">IntelliSense for code nuggets in attributes</span></span>

<span data-ttu-id="b0553-566">Visual Studio 始終為任何頁面或控制項中的伺服器端代碼塊提供 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="b0553-566">Visual Studio has always provided IntelliSense for server-side code nuggets in any page or control.</span></span> <span data-ttu-id="b0553-567">現在,Visual Studio 還包括用於 HTML 屬性中的代碼塊的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="b0553-567">Now Visual Studio includes IntelliSense for code nuggets in HTML attributes as well.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

<span data-ttu-id="b0553-568">這樣可以更輕鬆地建立資料繫式:</span><span class="sxs-lookup"><span data-stu-id="b0553-568">This makes it easier to create data-binding expressions:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a><span data-ttu-id="b0553-569">重新命名開啟或關閉標籤時自動重新命名符合標記</span><span class="sxs-lookup"><span data-stu-id="b0553-569">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>

<span data-ttu-id="b0553-570">如果重新命名 HTML 元素(例如,將*div*標記更改為*標頭*標記),相應的打開或關閉標記也會即時更改。</span><span class="sxs-lookup"><span data-stu-id="b0553-570">If you rename an HTML element (for example, you change a *div* tag to be a *header* tag), the corresponding opening or closing tag also changes in real time.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

<span data-ttu-id="b0553-571">這有助於避免忘記更改結束標記或更改錯誤標記的錯誤。</span><span class="sxs-lookup"><span data-stu-id="b0553-571">This helps avoid the error where you forget to change a closing tag or change the wrong one.</span></span>

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a><span data-ttu-id="b0553-572">事件處理程式產生</span><span class="sxs-lookup"><span data-stu-id="b0553-572">Event handler generation</span></span>

<span data-ttu-id="b0553-573">Visual Studio 現在包括在「源」檢視中的功能,以説明您編寫事件處理程式並手動綁定它們。</span><span class="sxs-lookup"><span data-stu-id="b0553-573">Visual Studio now includes features in Source view to help you write event handlers and bind them manually.</span></span> <span data-ttu-id="b0553-574">如果要在原始檢視中編輯事件名稱,IntelliSense 將顯示&lt;「建立新事件&gt;」,這將在具有正確簽名的頁面代碼中建立事件處理程式:</span><span class="sxs-lookup"><span data-stu-id="b0553-574">If you are editing an event name in Source view, IntelliSense displays &lt;Create New Event&gt;, which will create an event handler in the page's code that has the right signature:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

<span data-ttu-id="b0553-575">預設情況下,事件處理程式將使用控制項的 ID 來表示事件處理方法的名稱:</span><span class="sxs-lookup"><span data-stu-id="b0553-575">By default, the event handler will use the control's ID for the name of the event-handling method:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

<span data-ttu-id="b0553-576">生成的事件處理程式將如下所示(在本例中,在 C#中):</span><span class="sxs-lookup"><span data-stu-id="b0553-576">The resulting event handler will look like this (in this case, in C#):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a><span data-ttu-id="b0553-577">智慧縮排</span><span class="sxs-lookup"><span data-stu-id="b0553-577">Smart indent</span></span>

<span data-ttu-id="b0553-578">當您在空的 HTML 元素內按 Enter 時,編輯器將插入點放在正確的位置:</span><span class="sxs-lookup"><span data-stu-id="b0553-578">When you press Enter while inside an empty HTML element, the editor will put the insertion point in the right place:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

<span data-ttu-id="b0553-579">如果在此位置按 Enter,則關閉標記將向下移動並縮進以匹配打開標記。</span><span class="sxs-lookup"><span data-stu-id="b0553-579">If you press Enter in this location, the closing tag is moved down and indented to match the opening tag.</span></span> <span data-ttu-id="b0553-580">插入點也縮進:</span><span class="sxs-lookup"><span data-stu-id="b0553-580">The insertion point is also indented:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="b0553-581">自動減少敘述完成</span><span class="sxs-lookup"><span data-stu-id="b0553-581">Auto-reduce statement completion</span></span>

<span data-ttu-id="b0553-582">Visual Studio 中的 IntelliSense 清單現在根據您鍵入的內容進行篩選,以便僅顯示相關選項:</span><span class="sxs-lookup"><span data-stu-id="b0553-582">The IntelliSense list in Visual Studio now filters based on what you type so that it displays only relevant options:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

<span data-ttu-id="b0553-583">IntelliSense 還會根據 IntelliSense 清單中單一單字的標題大小寫進行篩選。</span><span class="sxs-lookup"><span data-stu-id="b0553-583">IntelliSense also filters based on the title case of the individual words in the IntelliSense list.</span></span> <span data-ttu-id="b0553-584">例如,如果您鍵入「dl」,則將顯示 dl 和 asp:DataList:</span><span class="sxs-lookup"><span data-stu-id="b0553-584">For example, if you type "dl", both dl and asp:DataList are displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

<span data-ttu-id="b0553-585">此功能使獲取已知元素的語句完成速度更快。</span><span class="sxs-lookup"><span data-stu-id="b0553-585">This feature makes it faster to get statement completion for known elements.</span></span>

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a><span data-ttu-id="b0553-586">JavaScript 編輯器</span><span class="sxs-lookup"><span data-stu-id="b0553-586">JavaScript Editor</span></span>

<span data-ttu-id="b0553-587">Visual Studio 2012 版本候選版中的 JAvaScript 編輯器是全新的,它極大地改善了在可視化工作室中使用 JAVAScript 的體驗。</span><span class="sxs-lookup"><span data-stu-id="b0553-587">The JavaScript editor in Visual Studio 2012 Release Candidate is completely new and it greatly improves the experience of working with JavaScript in Visual Studio.</span></span>

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a><span data-ttu-id="b0553-588">程式碼大綱</span><span class="sxs-lookup"><span data-stu-id="b0553-588">Code outlining</span></span>

<span data-ttu-id="b0553-589">現在會自動為所有函數創建大綱區域,從而可以摺疊與當前焦點無關的檔部分。</span><span class="sxs-lookup"><span data-stu-id="b0553-589">Outlining regions are now automatically created for all functions, allowing you to collapse parts of the file that aren't pertinent to your current focus.</span></span>

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a><span data-ttu-id="b0553-590">括號對稱</span><span class="sxs-lookup"><span data-stu-id="b0553-590">Brace matching</span></span>

<span data-ttu-id="b0553-591">將插入點放在開括弧或關閉大括弧上時,編輯器將突出顯示匹配的支撐。</span><span class="sxs-lookup"><span data-stu-id="b0553-591">When you put the insertion point on an opening or closing brace, the editor highlights the matching one.</span></span>

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a><span data-ttu-id="b0553-592">移至定義</span><span class="sxs-lookup"><span data-stu-id="b0553-592">Go to Definition</span></span>

<span data-ttu-id="b0553-593">"轉到定義"命令允許您跳轉到函數或變數的源。</span><span class="sxs-lookup"><span data-stu-id="b0553-593">The Go to Definition command lets you jump to the source for a function or variable.</span></span>

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a><span data-ttu-id="b0553-594">ECMAScript5 支援</span><span class="sxs-lookup"><span data-stu-id="b0553-594">ECMAScript5 support</span></span>

<span data-ttu-id="b0553-595">編輯器支援 ECMAScript5 中的新語法和 API,ECMAScript5 是描述 JavaScript 語言的標準的最新版本。</span><span class="sxs-lookup"><span data-stu-id="b0553-595">The editor supports the new syntax and APIs in ECMAScript5, the latest version of the standard that describes the JavaScript language.</span></span>

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a><span data-ttu-id="b0553-596">DOM 感知</span><span class="sxs-lookup"><span data-stu-id="b0553-596">DOM IntelliSense</span></span>

<span data-ttu-id="b0553-597">DOM API 的智慧感知得到了改進,支援許多新的 HTML5 API,包括*查詢選擇器*、DOM 儲存、跨文件訊息傳遞和*畫佈*。</span><span class="sxs-lookup"><span data-stu-id="b0553-597">IntelliSense for DOM APIs has been improved, with support for many new HTML5 APIs including *querySelector*, DOM Storage, cross-document messaging, and *canvas*.</span></span> <span data-ttu-id="b0553-598">DOM IntelliSense 現在由單個簡單的 JavaScript 檔案驅動,而不是由本機類型庫定義驅動。</span><span class="sxs-lookup"><span data-stu-id="b0553-598">DOM IntelliSense is now driven by a single simple JavaScript file, rather than by a native type library definition.</span></span> <span data-ttu-id="b0553-599">這使得擴展或更換變得容易。</span><span class="sxs-lookup"><span data-stu-id="b0553-599">This makes it easy to extend or replace.</span></span>

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a><span data-ttu-id="b0553-600">VSDOC 簽署重載</span><span class="sxs-lookup"><span data-stu-id="b0553-600">VSDOC signature overloads</span></span>

<span data-ttu-id="b0553-601">現在可以使用新的*&lt;&gt;簽名*元素聲明詳細的 IntelliSense 註解,以便單獨重載 JavaScript 函數,如以下範例所示:</span><span class="sxs-lookup"><span data-stu-id="b0553-601">Detailed IntelliSense comments can now be declared for separate overloads of JavaScript functions by using the new *&lt;signature&gt;* element, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a><span data-ttu-id="b0553-602">隱含參考</span><span class="sxs-lookup"><span data-stu-id="b0553-602">Implicit references</span></span>

<span data-ttu-id="b0553-603">現在,您可以將 JavaScript 檔添加到一個中心清單中,該清單將隱式包含在任何給定的 JavaScript 檔或阻止引用的檔案清單中,這意味著您將獲得 IntelliSense 的內容。</span><span class="sxs-lookup"><span data-stu-id="b0553-603">You can now add JavaScript files to a central list that will be implicitly included in the list of files that any given JavaScript file or block references, meaning you'll get IntelliSense for its contents.</span></span> <span data-ttu-id="b0553-604">例如,您可以將 jQuery 檔添加到檔案的中心清單中,並且無論是否已顯式引用它(使用&lt;// /&gt;引用 /), 您都將在任何 JavaScript 檔案塊中獲取 jQuery 函數的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="b0553-604">For example, you can add jQuery files to the central list of files, and you'll get IntelliSense for jQuery functions in any JavaScript block of file, whether you've referenced it explicitly (using /// &lt;reference /&gt;) or not.</span></span>

<a id="_Toc318097415"></a>
### <a name="css-editor"></a><span data-ttu-id="b0553-605">CSS 編輯器</span><span class="sxs-lookup"><span data-stu-id="b0553-605">CSS Editor</span></span>

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="b0553-606">自動減少敘述完成</span><span class="sxs-lookup"><span data-stu-id="b0553-606">Auto-reduce statement completion</span></span>

<span data-ttu-id="b0553-607">CSS 的 IntelliSense 清單現在根據選取架構支援的 CSS 屬性和值進行篩選。</span><span class="sxs-lookup"><span data-stu-id="b0553-607">The IntelliSense list for CSS now filters based on the CSS properties and values supported by the selected schema.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

<span data-ttu-id="b0553-608">IntelliSense 還支援標題案例搜尋:</span><span class="sxs-lookup"><span data-stu-id="b0553-608">IntelliSense also supports title case searches:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a><span data-ttu-id="b0553-609">階層式縮排</span><span class="sxs-lookup"><span data-stu-id="b0553-609">Hierarchical indentation</span></span>

<span data-ttu-id="b0553-610">CSS 編輯器使用縮進來顯示分層規則,這為您提供了級聯規則邏輯組織方式的概述。</span><span class="sxs-lookup"><span data-stu-id="b0553-610">The CSS editor uses indentation to display hierarchical rules, which gives you an overview of how the cascading rules are logically organized.</span></span> <span data-ttu-id="b0553-611">在下面的範例中,選擇器#list是列表的級聯子級,因此縮進。</span><span class="sxs-lookup"><span data-stu-id="b0553-611">In the following example, the #list a selector is a cascading child of list and is therefore indented.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

<span data-ttu-id="b0553-612">下面的範例顯示了更複雜的繼承:</span><span class="sxs-lookup"><span data-stu-id="b0553-612">The following example shows more complex inheritance:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

<span data-ttu-id="b0553-613">規則的縮進由其父規則決定。</span><span class="sxs-lookup"><span data-stu-id="b0553-613">The indentation of a rule is determined by its parent rules.</span></span> <span data-ttu-id="b0553-614">預設情況下啟用分層縮進,但您可以關閉「選項」對話框(選單欄中的工具、選項):</span><span class="sxs-lookup"><span data-stu-id="b0553-614">Hierarchical indentation is enabled by default, but you can disable it the Options dialog box (Tools, Options from the menu bar):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a><span data-ttu-id="b0553-615">CSS 駭客支援</span><span class="sxs-lookup"><span data-stu-id="b0553-615">CSS hacks support</span></span>

<span data-ttu-id="b0553-616">對數百個真實 CSS 檔的分析表明,CSS 駭客非常常見,現在 Visual Studio 支援使用最廣泛的駭客。</span><span class="sxs-lookup"><span data-stu-id="b0553-616">Analysis of hundreds of real-world CSS files shows that CSS hacks are very common, and now Visual Studio supports the most widely used ones.</span></span> <span data-ttu-id="b0553-617">這種支援包括IntelliSense和驗證的明星\*( )\_和下 劃線 ( ) 屬性駭客:</span><span class="sxs-lookup"><span data-stu-id="b0553-617">This support includes IntelliSense and validation of the star (\*) and underscore (\_) property hacks:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

<span data-ttu-id="b0553-618">還支援典型的選擇器駭客,以便即使應用分層縮進,也能保持分層縮進。</span><span class="sxs-lookup"><span data-stu-id="b0553-618">Typical selector hacks are also supported so that hierarchical indentation is maintained even when they are applied.</span></span> <span data-ttu-id="b0553-619">典型的選擇器駭客用於目標網際網路瀏覽器7是準備一個選擇器與*\*:第一個孩子 + html*。</span><span class="sxs-lookup"><span data-stu-id="b0553-619">A typical selector hack used to target Internet Explorer 7 is to prepend a selector with *\*:first-child + html*.</span></span> <span data-ttu-id="b0553-620">使用該規則將保持分層縮排:</span><span class="sxs-lookup"><span data-stu-id="b0553-620">Using that rule will maintain the hierarchical indentation:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a><span data-ttu-id="b0553-621">供應商指定的架構(-moz-, -webkit)</span><span class="sxs-lookup"><span data-stu-id="b0553-621">Vendor specific schemas (-moz-, -webkit)</span></span>

<span data-ttu-id="b0553-622">CSS3 引入了許多由不同瀏覽器在不同時間實現的屬性。</span><span class="sxs-lookup"><span data-stu-id="b0553-622">CSS3 introduces many properties that have been implemented by different browsers at different times.</span></span> <span data-ttu-id="b0553-623">這以前迫使開發人員使用特定於供應商的語法為特定瀏覽器編寫代碼。</span><span class="sxs-lookup"><span data-stu-id="b0553-623">This previously forced developers to code for specific browsers by using vendor-specific syntax.</span></span> <span data-ttu-id="b0553-624">這些特定於瀏覽器的屬性現在包含在 IntelliSense 中。</span><span class="sxs-lookup"><span data-stu-id="b0553-624">These browser-specific properties are now included in IntelliSense.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a><span data-ttu-id="b0553-625">評論和非評論支援</span><span class="sxs-lookup"><span data-stu-id="b0553-625">Commenting and uncommenting support</span></span>

<span data-ttu-id="b0553-626">現在,您可以使用代碼編輯器中使用的快捷方式(Ctrl_K、C註釋和 Ctrl_K,您取消註釋)對 CSS 規則進行註釋和取消註解。</span><span class="sxs-lookup"><span data-stu-id="b0553-626">You can now comment and uncomment CSS rules using the same shortcuts that you use in the code editor (Ctrl+K,C to comment and Ctrl+K,U to uncomment).</span></span>

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a><span data-ttu-id="b0553-627">Color picker</span><span class="sxs-lookup"><span data-stu-id="b0553-627">Color picker</span></span>

<span data-ttu-id="b0553-628">在早期版本的 Visual Studio 中,與顏色相關的屬性的 IntelliSense 由命名顏色值的下拉列表組成。</span><span class="sxs-lookup"><span data-stu-id="b0553-628">In previous versions of Visual Studio, IntelliSense for color-related attributes consisted of a drop-down list of named color values.</span></span> <span data-ttu-id="b0553-629">該清單已被全功能顏色選取器替換。</span><span class="sxs-lookup"><span data-stu-id="b0553-629">That list has been replaced by a full-featured color picker.</span></span>

<span data-ttu-id="b0553-630">輸入顏色值時,顏色選取器將自動顯示,並顯示以前使用的顏色清單,後跟預設調色板。</span><span class="sxs-lookup"><span data-stu-id="b0553-630">When you enter a color value, the color picker is displayed automatically and presents a list of previously used colors followed by a default color palette.</span></span> <span data-ttu-id="b0553-631">您可以使用滑鼠或鍵盤選擇顏色。</span><span class="sxs-lookup"><span data-stu-id="b0553-631">You can select a color using the mouse or the keyboard.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

<span data-ttu-id="b0553-632">該清單可以展開為完整的顏色選取器。</span><span class="sxs-lookup"><span data-stu-id="b0553-632">The list can be expanded into a complete color picker.</span></span> <span data-ttu-id="b0553-633">選取器允許您在移動不協調性滑動時自動將任何顏色轉換為 RGBA 來控制 Alpha 通道:</span><span class="sxs-lookup"><span data-stu-id="b0553-633">The picker lets you control the alpha channel by automatically converting any color into RGBA when you move the opacity slider:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a><span data-ttu-id="b0553-634">程式碼片段</span><span class="sxs-lookup"><span data-stu-id="b0553-634">Snippets</span></span>

<span data-ttu-id="b0553-635">CSS 編輯器中的代碼段使創建跨瀏覽器樣式變得更加簡單和快速。</span><span class="sxs-lookup"><span data-stu-id="b0553-635">Snippets in the CSS editor make it easier and faster to create cross-browser styles.</span></span> <span data-ttu-id="b0553-636">許多需要特定於瀏覽器設置的 CSS3 屬性現已滾入代碼段。</span><span class="sxs-lookup"><span data-stu-id="b0553-636">Many CSS3 properties that require browser-specific settings have now been rolled into snippets.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

<span data-ttu-id="b0553-637">CSS 程式碼段透過鍵入在符號 (#) 中顯示 IntelliSense 清單來支援進階方案(如 CSS3 媒體查詢)。</span><span class="sxs-lookup"><span data-stu-id="b0553-637">CSS snippets support advanced scenarios (like CSS3 media queries) by typing the at-symbol (@), which shows the IntelliSense list.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

<span data-ttu-id="b0553-638">當您選擇@media值並按選項卡時,CSS 編輯器將插入以下代碼段:</span><span class="sxs-lookup"><span data-stu-id="b0553-638">When you select @media value and press Tab, the CSS editor inserts the following snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

<span data-ttu-id="b0553-639">與代碼代碼段一樣,您可以創建自己的 CSS 代碼段。</span><span class="sxs-lookup"><span data-stu-id="b0553-639">As with snippets for code, you can create your own CSS snippets.</span></span>

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a><span data-ttu-id="b0553-640">自訂區域</span><span class="sxs-lookup"><span data-stu-id="b0553-640">Custom regions</span></span>

<span data-ttu-id="b0553-641">命名代碼區域(已在代碼編輯器中提供)現在可用於 CSS 編輯。</span><span class="sxs-lookup"><span data-stu-id="b0553-641">Named code regions, which are already available in the code editor, are now available for CSS editing.</span></span> <span data-ttu-id="b0553-642">這使您可以輕鬆對相關的樣式塊進行分組。</span><span class="sxs-lookup"><span data-stu-id="b0553-642">This lets you easily group related style blocks.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

<span data-ttu-id="b0553-643">當區域折疊時,將顯示區域的名稱:</span><span class="sxs-lookup"><span data-stu-id="b0553-643">When a region is collapsed it displays the name of the region:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a><span data-ttu-id="b0553-644">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="b0553-644">Page Inspector</span></span>

<span data-ttu-id="b0553-645">頁面檢查器是一種工具,用於在 Visual Studio IDE 中呈現網頁(HTML、Web 窗體、ASP.NET MVC 或網頁),並允許您檢查原始碼和生成的輸出。</span><span class="sxs-lookup"><span data-stu-id="b0553-645">Page Inspector is a tool that renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) in the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="b0553-646">對於ASP.NET頁,頁面檢查器允許您確定哪些伺服器端代碼已生成呈現到瀏覽器的 HTML 標記。</span><span class="sxs-lookup"><span data-stu-id="b0553-646">For ASP.NET pages, Page Inspector lets you determine which server-side code has produced the HTML markup that is rendered to the browser.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

<span data-ttu-id="b0553-647">有關頁面檢查器的詳細資訊,請參閱以下教程:</span><span class="sxs-lookup"><span data-stu-id="b0553-647">For more information about Page Inspector, please see the following tutorials:</span></span>

- <span data-ttu-id="b0553-648">在[mVC 中使用 ASP.NET](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)網頁檢查器</span><span class="sxs-lookup"><span data-stu-id="b0553-648">Using Page Inspector in [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span></span>
- <span data-ttu-id="b0553-649">在[ASP.NET Web 窗體](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)中使用網頁檢查器</span><span class="sxs-lookup"><span data-stu-id="b0553-649">Using Page Inspector in [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span></span>

<a id="_Toc318097425"></a>
### <a name="publishing"></a><span data-ttu-id="b0553-650">發佈</span><span class="sxs-lookup"><span data-stu-id="b0553-650">Publishing</span></span>

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a><span data-ttu-id="b0553-651">發佈設定檔</span><span class="sxs-lookup"><span data-stu-id="b0553-651">Publish profiles</span></span>

<span data-ttu-id="b0553-652">在 Visual Studio 2010 中,Web 應用程式專案的發佈資訊不存儲在版本控制中,並且不設計為與他人共用。</span><span class="sxs-lookup"><span data-stu-id="b0553-652">In Visual Studio 2010, publishing information for Web application projects is not stored in version control and is not designed for sharing with others.</span></span> <span data-ttu-id="b0553-653">在 Visual Studio 2012 版本候選版中,發佈配置檔的格式已更改。</span><span class="sxs-lookup"><span data-stu-id="b0553-653">In Visual Studio 2012 Release Candidate, the format of the publish profile has been changed.</span></span> <span data-ttu-id="b0553-654">它已成為團隊工件,現在很容易從基於 MSBuild 的生成中利用。</span><span class="sxs-lookup"><span data-stu-id="b0553-654">It has been made a team artifact, and it is now easy to leverage from builds based on MSBuild.</span></span> <span data-ttu-id="b0553-655">生成配置資訊位於"發佈"對話框中,以便在發佈之前輕鬆切換生成配置。</span><span class="sxs-lookup"><span data-stu-id="b0553-655">Build configuration information is in the Publish dialog box so that you can easily switch build configurations before publishing.</span></span>

<span data-ttu-id="b0553-656">發佈設定檔儲存在「發布設定檔」資料夾中。</span><span class="sxs-lookup"><span data-stu-id="b0553-656">Publish profiles are stored in the PublishProfiles folder.</span></span> <span data-ttu-id="b0553-657">資料夾的位置取決於您使用的程式設計語言:</span><span class="sxs-lookup"><span data-stu-id="b0553-657">The location of the folder depends on what programming language you are using:</span></span>

- <span data-ttu-id="b0553-658">C#:屬性\發行設定檔</span><span class="sxs-lookup"><span data-stu-id="b0553-658">C#: Properties\PublishProfiles</span></span>
- <span data-ttu-id="b0553-659">視覺化基礎知識:我的項目\發行設定檔</span><span class="sxs-lookup"><span data-stu-id="b0553-659">Visual Basic: My Project\PublishProfiles</span></span>

<span data-ttu-id="b0553-660">每個配置檔都是一個 MSBuild 檔。</span><span class="sxs-lookup"><span data-stu-id="b0553-660">Each profile is an MSBuild file.</span></span> <span data-ttu-id="b0553-661">在發佈期間,此檔將導入到專案的 MSBuild 檔中。</span><span class="sxs-lookup"><span data-stu-id="b0553-661">During publishing, this file is imported into the project's MSBuild file.</span></span> <span data-ttu-id="b0553-662">在 Visual Studio 2010 中,如果要對發佈或包過程進行更改,則必須將自定義項放在名為**ProjectName**.wpp.target 的檔中。</span><span class="sxs-lookup"><span data-stu-id="b0553-662">In Visual Studio 2010, if you want to make changes to the publish or package process, you have to put your customizations in a file named **ProjectName**.wpp.targets.</span></span> <span data-ttu-id="b0553-663">這仍然受支援,但現在可以將自定義項放在發佈配置檔本身中。</span><span class="sxs-lookup"><span data-stu-id="b0553-663">This is still supported, but you can now put your customizations in the publish profile itself.</span></span> <span data-ttu-id="b0553-664">這樣,自定義將僅用於該配置檔。</span><span class="sxs-lookup"><span data-stu-id="b0553-664">That way, the customizations will be used only for that profile.</span></span>

<span data-ttu-id="b0553-665">您現在還可以利用 MSBuild 的發佈配置檔。</span><span class="sxs-lookup"><span data-stu-id="b0553-665">You can now also leverage publish profiles from MSBuild.</span></span> <span data-ttu-id="b0553-666">為此,在產生專案時使用以下命令:</span><span class="sxs-lookup"><span data-stu-id="b0553-666">To do so, use the following command when you build the project:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

<span data-ttu-id="b0553-667">project.csproj 值是專案的路徑,而配置檔名稱是要發布的設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="b0553-667">The project.csproj value is the path of the project, and ProfileName is the name of the profile to publish.</span></span> <span data-ttu-id="b0553-668">或者,您可以傳入發佈配置檔的完整路徑,而不是傳遞*PublishProfile*屬性的設定檔名稱。</span><span class="sxs-lookup"><span data-stu-id="b0553-668">Alternatively, instead of passing the profile name for the *PublishProfile* property, you can pass in the full path to the publish profile.</span></span>

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a><span data-ttu-id="b0553-669">ASP.NET 預寫和合併</span><span class="sxs-lookup"><span data-stu-id="b0553-669">ASP.NET precompilation and merge</span></span>

<span data-ttu-id="b0553-670">對於 Web 應用程式專案,Visual Studio 2012 發佈候選版在「包/發佈 Web 屬性」頁上添加了一個選項,允許您在發佈或打包專案時預編譯和合併網站的內容。</span><span class="sxs-lookup"><span data-stu-id="b0553-670">For Web application projects, Visual Studio 2012 Release Candidate adds an option on the Package/Publish Web properties page that lets you precompile and merge your site's content when you publish or package the project.</span></span> <span data-ttu-id="b0553-671">要查看這些選項,請右鍵單擊解決方案資源管理器中的項目,選擇"屬性",然後選擇"包/發佈 Web 屬性頁"。</span><span class="sxs-lookup"><span data-stu-id="b0553-671">To see these options, right-click the project in Solution Explorer, choose Properties, and then choose the Package/Publish Web property page.</span></span> <span data-ttu-id="b0553-672">下圖顯示了發佈選項之前預編譯此應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0553-672">The following illustration shows the Precompile this application before publishing option.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

<span data-ttu-id="b0553-673">選擇此選項後,每當發佈或打包 Web 應用程式時,Visual Studio 都會預編譯應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0553-673">When this option is selected, Visual Studio precompiles the application whenever you publish or package the web application.</span></span> <span data-ttu-id="b0553-674">如果要控制網站的預編譯方式或程式集的合併方式,請單擊「高級」按鈕以配置這些選項。</span><span class="sxs-lookup"><span data-stu-id="b0553-674">If you want to control how the site is precompiled or how assemblies are merged, click the Advanced button to configure those options.</span></span>

<a id="_Toc318097428"></a>
### <a name="iis-express"></a><span data-ttu-id="b0553-675">IIS Express</span><span class="sxs-lookup"><span data-stu-id="b0553-675">IIS Express</span></span>

<span data-ttu-id="b0553-676">用於在 Visual Studio 中測試 Web 專案的預設 Web 伺服器現在是 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="b0553-676">The default web server for testing web projects in Visual Studio is now IIS Express.</span></span> <span data-ttu-id="b0553-677">可視化工作室開發伺服器仍然是開發過程中本地 Web 伺服器的選項,但 IIS Express 現在是推薦的伺服器。</span><span class="sxs-lookup"><span data-stu-id="b0553-677">The Visual Studio Development Server is still an option for local web server during development, but IIS Express is now the recommended server.</span></span> <span data-ttu-id="b0553-678">在 Visual Studio 11 Beta 中使用 IIS Express 的經驗與在 Visual Studio 2010 SP1 中使用它非常相似。</span><span class="sxs-lookup"><span data-stu-id="b0553-678">The experience of using IIS Express in Visual Studio 11 Beta is very similar to using it in Visual Studio 2010 SP1.</span></span>

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a><span data-ttu-id="b0553-679">免責聲明</span><span class="sxs-lookup"><span data-stu-id="b0553-679">Disclaimer</span></span>

<span data-ttu-id="b0553-680">這是一份初稿，內容在本文所述的軟體於正式商業發行前都可能有所更動。</span><span class="sxs-lookup"><span data-stu-id="b0553-680">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="b0553-681">本文件所含的資訊代表 Microsoft Corporation 在發行日當下對問題的看法。</span><span class="sxs-lookup"><span data-stu-id="b0553-681">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="b0553-682">由於 Microsoft 必須因應不斷變化的市場狀況，因此不應將此解讀為 Microsoft 方面所作出的承諾，且 Microsoft 也無法保證在發行日之後所提出任何資訊的正確性。</span><span class="sxs-lookup"><span data-stu-id="b0553-682">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="b0553-683">本技術白皮書僅供參考。</span><span class="sxs-lookup"><span data-stu-id="b0553-683">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="b0553-684">MICROSOFT 對本文件中的資訊不提供任何明示、暗示或法定擔保。</span><span class="sxs-lookup"><span data-stu-id="b0553-684">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="b0553-685">遵守所有適用之著作權法係使用者的責任。</span><span class="sxs-lookup"><span data-stu-id="b0553-685">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="b0553-686">在不限制任何依著作權本得享有之權利，未經 Microsoft Corporation 書面許可， 貴用戶不得為任何目的使用任何形式或方法 (電子形式、機械形式、影印、記錄或其他方式) 複製或傳送本文件的任何部份，也不得將本文件的任何部份儲存或放入檢索系統 (a retrieval system)。</span><span class="sxs-lookup"><span data-stu-id="b0553-686">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="b0553-687">在本文件所提述之內容中，可能包括 Microsoft 的專利、申請專利案件、商標、著作權，或其他智慧財產權等。</span><span class="sxs-lookup"><span data-stu-id="b0553-687">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="b0553-688">除非於 Microsoft 提出的任何書面授權條約中明確規定者外，提供本文件並不表示賦予台端上述專利、商標、著作權或其他智慧財產權等之任何授權。</span><span class="sxs-lookup"><span data-stu-id="b0553-688">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="b0553-689">除非另有說明,否則此處描述的示例公司、組織、產品、域名、電子郵件地址、徽標、人員、地點和事件均屬虛構,且無意或不應推斷與任何真實的公司、組織、產品、功能變數名稱、電子郵寄地址、徽標、人員、地點或事件有任何關聯。</span><span class="sxs-lookup"><span data-stu-id="b0553-689">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="b0553-690">(C) 2012 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="b0553-690">© 2012 Microsoft Corporation.</span></span> <span data-ttu-id="b0553-691">著作權所有，並保留一切權利。</span><span class="sxs-lookup"><span data-stu-id="b0553-691">All rights reserved.</span></span>

<span data-ttu-id="b0553-692">Microsoft 和 Windows 是 Microsoft Corporation 在美國及/或其他國家/地區的註冊商標或商標。</span><span class="sxs-lookup"><span data-stu-id="b0553-692">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="b0553-693">本文件中所提實際公司和產品，可能為各所有人所有之商標。</span><span class="sxs-lookup"><span data-stu-id="b0553-693">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
