---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: 伺服器控制 |微軟文件
author: rick-anderson
description: ASP.NET 2.0 在許多方面增強了伺服器控件。 在本模組中,我們將介紹ASP.NET 2.0 和 Visual Studio 200 的方式的一些體系結構更改。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: 7109f10e87abfadf1e7e08795cf9d3d6bf5df122
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543739"
---
# <a name="server-controls"></a><span data-ttu-id="57426-104">伺服器控制項</span><span class="sxs-lookup"><span data-stu-id="57426-104">Server Controls</span></span>

<span data-ttu-id="57426-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="57426-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="57426-106">ASP.NET 2.0 在許多方面增強了伺服器控件。</span><span class="sxs-lookup"><span data-stu-id="57426-106">ASP.NET 2.0 enhances server controls in many ways.</span></span> <span data-ttu-id="57426-107">在本模組中,我們將介紹ASP.NET 2.0 和Visual Studio 2005處理伺服器控制項的方式的一些體系結構更改。</span><span class="sxs-lookup"><span data-stu-id="57426-107">In this module, we'll cover some of the architectural changes to the way ASP.NET 2.0 and Visual Studio 2005 deals with server controls.</span></span>

<span data-ttu-id="57426-108">ASP.NET 2.0 在許多方面增強了伺服器控件。</span><span class="sxs-lookup"><span data-stu-id="57426-108">ASP.NET 2.0 enhances server controls in many ways.</span></span> <span data-ttu-id="57426-109">在本模組中,我們將介紹ASP.NET 2.0 和Visual Studio 2005處理伺服器控制項的方式的一些體系結構更改。</span><span class="sxs-lookup"><span data-stu-id="57426-109">In this module, we'll cover some of the architectural changes to the way ASP.NET 2.0 and Visual Studio 2005 deals with server controls.</span></span>

## <a name="view-state"></a><span data-ttu-id="57426-110">檢視狀態</span><span class="sxs-lookup"><span data-stu-id="57426-110">View state</span></span>

<span data-ttu-id="57426-111">ASP.NET 2.0 中視圖狀態的主要變化是大小顯著減小。</span><span class="sxs-lookup"><span data-stu-id="57426-111">The primary change in view state in ASP.NET 2.0 is a dramatic reduction in size.</span></span> <span data-ttu-id="57426-112">考慮一個只有"日曆"控制件的頁面。</span><span class="sxs-lookup"><span data-stu-id="57426-112">Consider a page with only a Calendar control on it.</span></span> <span data-ttu-id="57426-113">下面是ASP.NET 1.1 中的視圖狀態。</span><span class="sxs-lookup"><span data-stu-id="57426-113">Here is the view state in ASP.NET 1.1.</span></span>

[!code-css[Main](server-controls/samples/sample1.css)]

<span data-ttu-id="57426-114">現在,下面是ASP.NET 2.0中相同頁面上的視圖狀態。</span><span class="sxs-lookup"><span data-stu-id="57426-114">Now here's the view state on an identical page in ASP.NET 2.0.</span></span>

[!code-css[Main](server-controls/samples/sample2.css)]

<span data-ttu-id="57426-115">這是一個相當重大的變化,考慮到視圖狀態在線上來回移動,此更改可以顯著提高開發人員的性能。</span><span class="sxs-lookup"><span data-stu-id="57426-115">That's a pretty significant change, and considering that view state is carried back and forth over the wire, this change can give developers a significant performance increase.</span></span> <span data-ttu-id="57426-116">視圖狀態大小的減小主要是由於我們在內部處理它的方式。</span><span class="sxs-lookup"><span data-stu-id="57426-116">The reduction in size of view state is largely due to the way that we handle it internally.</span></span> <span data-ttu-id="57426-117">請記住,檢視狀態是 Base64 編碼字串。</span><span class="sxs-lookup"><span data-stu-id="57426-117">Remember that view state is a Base64 encoded string.</span></span> <span data-ttu-id="57426-118">為了更好地瞭解 ASP.NET 2.0 中視圖狀態的變化,讓我們從上面的示例中查看解碼的值。</span><span class="sxs-lookup"><span data-stu-id="57426-118">To better understand the change in view state in ASP.NET 2.0, let's have a look at the decoded values from the examples above.</span></span>

<span data-ttu-id="57426-119">下面是已解碼的 1.1 檢視狀態:</span><span class="sxs-lookup"><span data-stu-id="57426-119">Here is the 1.1 view state decoded:</span></span>

[!code-css[Main](server-controls/samples/sample3.css)]

<span data-ttu-id="57426-120">這可能看起來有點胡言亂語,但這裡有一個模式。</span><span class="sxs-lookup"><span data-stu-id="57426-120">This may look a bit like gibberish, but there is a pattern here.</span></span> <span data-ttu-id="57426-121">在ASP.NET 1.x 中,我們使用單個字元&lt;&gt;來標識 數據類型並使用字元分隔值。</span><span class="sxs-lookup"><span data-stu-id="57426-121">In ASP.NET 1.x, we used single characters to identify data-types and delimited values using the &lt;&gt; characters.</span></span> <span data-ttu-id="57426-122">上面的檢視狀態示例中的「t」表示三重。</span><span class="sxs-lookup"><span data-stu-id="57426-122">The "t" in the view state sample above represents a Triplet.</span></span> <span data-ttu-id="57426-123">三重清單包含一對陣列清單("l"表示陣列清單)。其中一個陣列清單包含一個 Int32 ("i"),其值為 1,另一個包含另一個 Triplet。</span><span class="sxs-lookup"><span data-stu-id="57426-123">The Triplet contains a pair of ArrayLists (the "l" represents an ArrayList.) One of those ArrayLists contains an Int32 ("i") with a value of 1 and the other contains another Triplet.</span></span> <span data-ttu-id="57426-124">三重包含一對陣列清單等。需要記住的重要的事情是,我們使用包含對的三腳架,我們通過字母識別數據類型,並使用和&lt;&gt;字元作為分隔符。</span><span class="sxs-lookup"><span data-stu-id="57426-124">The Triplet contains a pair of ArrayLists, etc. The important thing to remember is that we use Triplets that contain pairs, we identify the data-types via a letter, and we use the &lt; and &gt; characters as delimiters.</span></span>

<span data-ttu-id="57426-125">在ASP.NET 2.0 中,解碼的視圖狀態看起來有點不同。</span><span class="sxs-lookup"><span data-stu-id="57426-125">In ASP.NET 2.0, the decoded view state looks a bit different.</span></span>

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

<span data-ttu-id="57426-126">您應該注意到解碼視圖狀態的外觀發生巨大變化。</span><span class="sxs-lookup"><span data-stu-id="57426-126">You should notice a huge change in the appearance of the decoded view state.</span></span> <span data-ttu-id="57426-127">此更改具有多個體系結構基礎。</span><span class="sxs-lookup"><span data-stu-id="57426-127">This change has several architectural underpinnings.</span></span> <span data-ttu-id="57426-128">ASP.NET 1.x 中的檢視狀態使用 LosFormatter 對資料進行序列化。</span><span class="sxs-lookup"><span data-stu-id="57426-128">View state in ASP.NET 1.x used the LosFormatter to serialize data.</span></span> <span data-ttu-id="57426-129">在 2.0 中,我們使用新的 Object StateFormatter 類。</span><span class="sxs-lookup"><span data-stu-id="57426-129">In 2.0, we use the new ObjectStateFormatter class.</span></span> <span data-ttu-id="57426-130">此類是專門為幫助檢視狀態和控制狀態的序列化和反序列化而設計的。</span><span class="sxs-lookup"><span data-stu-id="57426-130">This class was specifically designed to aid in the serialization and deserialization of view state and control state.</span></span> <span data-ttu-id="57426-131">(下一節將介紹控制狀態。通過改變序列化和反序列化的方法,可以帶來許多好處。</span><span class="sxs-lookup"><span data-stu-id="57426-131">(Control state will be covered in the next section.) There are many benefits gained by changing the method by which serialization and deserialization take place.</span></span> <span data-ttu-id="57426-132">其中最戲劇性的是,與使用文本Writer的LosFormatter不同,ObjectStateFormatter使用二進制寫入器。</span><span class="sxs-lookup"><span data-stu-id="57426-132">One of the most dramatic is the fact that unlike the LosFormatter which uses a TextWriter, the ObjectStateFormatter uses a BinaryWriter.</span></span> <span data-ttu-id="57426-133">這允許ASP.NET 2.0 儲存一系列位元組而不是位元串的視圖狀態。</span><span class="sxs-lookup"><span data-stu-id="57426-133">This allows ASP.NET 2.0 to store view state a series of bytes instead of strings.</span></span> <span data-ttu-id="57426-134">以整數為例。</span><span class="sxs-lookup"><span data-stu-id="57426-134">Take, for example, an integer.</span></span> <span data-ttu-id="57426-135">在ASP.NET 1.1 中,整數需要4個字節的視圖狀態。</span><span class="sxs-lookup"><span data-stu-id="57426-135">In ASP.NET 1.1, an integer required 4 bytes of view state.</span></span> <span data-ttu-id="57426-136">在ASP.NET 2.0 中,相同的整數只需要1個字節。</span><span class="sxs-lookup"><span data-stu-id="57426-136">In ASP.NET 2.0, that same integer only requires 1 byte.</span></span> <span data-ttu-id="57426-137">進行了其他增強,以減少存儲的視圖狀態量。</span><span class="sxs-lookup"><span data-stu-id="57426-137">Other enhancements were made to decrease the amount of view state that is stored.</span></span> <span data-ttu-id="57426-138">例如,DateTime 值現在使用TickCount而不是字串進行存儲。</span><span class="sxs-lookup"><span data-stu-id="57426-138">DateTime values, for example, are now stored using a TickCount instead of a string.</span></span>

<span data-ttu-id="57426-139">似乎所有這一切還不夠,特別注意的是,在 1.x 中,視圖狀態的最大消費者之一是 DataGrid 和類似的控制項。</span><span class="sxs-lookup"><span data-stu-id="57426-139">As if all of that weren't enough, special attention was paid to the fact that one of the greatest consumers of view state in 1.x was the DataGrid and similar controls.</span></span> <span data-ttu-id="57426-140">控件(如檢視狀態所在的 DataGrid)的一個主要缺點是,它通常包含大量重複的資訊。</span><span class="sxs-lookup"><span data-stu-id="57426-140">A major drawback of controls such as the DataGrid where view state is concerned is that it often contains large amounts of repeated information.</span></span> <span data-ttu-id="57426-141">在ASP.NET 1.x 中,重複的資訊只是一遍又一遍地存儲,導致視圖狀態膨脹。</span><span class="sxs-lookup"><span data-stu-id="57426-141">In ASP.NET 1.x, that repeated information was simply stored over and over again resulting in a bloated view state.</span></span> <span data-ttu-id="57426-142">在 ASP.NET 2.0 中,我們使用新的 IndexedString 類來存儲此類數據。</span><span class="sxs-lookup"><span data-stu-id="57426-142">In ASP.NET 2.0, we use the new IndexedString class to store such data.</span></span> <span data-ttu-id="57426-143">如果字串重複,我們只需將索引String 和索引的令牌存儲在索引String 對象的運行表中。</span><span class="sxs-lookup"><span data-stu-id="57426-143">If a string repeats, we just store the token for the IndexedString and the index within a running table of IndexedString objects.</span></span>

## <a name="control-state"></a><span data-ttu-id="57426-144">控制狀態</span><span class="sxs-lookup"><span data-stu-id="57426-144">Control State</span></span>

<span data-ttu-id="57426-145">開發人員對檢視狀態的主要抱怨之一是它添加到 HTTP 負載的大小。</span><span class="sxs-lookup"><span data-stu-id="57426-145">One of the major gripes that developers had with view state was the size that it added to the HTTP payload.</span></span> <span data-ttu-id="57426-146">如前所述,視圖狀態的最大消費者之一是DataGrid控件。</span><span class="sxs-lookup"><span data-stu-id="57426-146">As previously mentioned, one of the greatest consumers of view state is the DataGrid control.</span></span> <span data-ttu-id="57426-147">為了避免 DataGrid 生成的大量檢視狀態,許多開發人員只是禁用該控制件的視圖狀態。</span><span class="sxs-lookup"><span data-stu-id="57426-147">To avoid the huge amounts of view state generated by a DataGrid, many developers simply disabled view state for that control.</span></span> <span data-ttu-id="57426-148">不幸的是,這個解決方案並不總是一個好的。</span><span class="sxs-lookup"><span data-stu-id="57426-148">Unfortunately, that solution wasn't always a good one.</span></span> <span data-ttu-id="57426-149">ASP.NET 1.x 中的檢視狀態不僅包含控件正確功能所需的數據。</span><span class="sxs-lookup"><span data-stu-id="57426-149">View state in ASP.NET 1.x contains not only data necessary for the correct functionality of the control.</span></span> <span data-ttu-id="57426-150">它還包含有關控制者的 UI 的狀態的資訊。</span><span class="sxs-lookup"><span data-stu-id="57426-150">It also contains information concerning the state of the control's UI.</span></span> <span data-ttu-id="57426-151">這意味著,如果要允許在 DataGrid 上進行分頁,則必須啟用檢視狀態,即使您不需要檢視狀態包含的所有 UI 資訊也是如此。</span><span class="sxs-lookup"><span data-stu-id="57426-151">This means that if you want to allow for pagination on a DataGrid, you must enable view state even if you don't need all of the UI information that view state contains.</span></span> <span data-ttu-id="57426-152">這是一個全有或全無的情況。</span><span class="sxs-lookup"><span data-stu-id="57426-152">It's an all-or-nothing scenario.</span></span>

<span data-ttu-id="57426-153">在ASP.NET 2.0中,控制狀態通過引入控制狀態很好地解決了該問題。</span><span class="sxs-lookup"><span data-stu-id="57426-153">In ASP.NET 2.0, control state solves that problem nicely via the introduction of control state.</span></span> <span data-ttu-id="57426-154">控件狀態包含控制式正確功能絕對必要的資料。</span><span class="sxs-lookup"><span data-stu-id="57426-154">Control state contains the data that is absolutely necessary for the proper functionality of a control.</span></span> <span data-ttu-id="57426-155">與視圖狀態不同,無法禁用控件狀態。</span><span class="sxs-lookup"><span data-stu-id="57426-155">Unlike view state, control state cannot be disabled.</span></span> <span data-ttu-id="57426-156">因此,必須嚴格控制存儲在受控狀態的數據。</span><span class="sxs-lookup"><span data-stu-id="57426-156">Therefore, it is important that the data being stored in control state is carefully controlled.</span></span>

> [!NOTE]
> <span data-ttu-id="57426-157">控制項狀態與\_\_「檢視狀態隱藏窗體」欄位中的檢視狀態一起保留。</span><span class="sxs-lookup"><span data-stu-id="57426-157">Control state is persisted along with the view state in the \_\_VIEWSTATE hidden form field.</span></span>

<span data-ttu-id="57426-158">此視頻是視圖狀態和控制狀態的演練。</span><span class="sxs-lookup"><span data-stu-id="57426-158">This video is a walkthrough of view state and control state.</span></span>

![](server-controls/_static/image1.png)

[<span data-ttu-id="57426-159">開啟全螢幕視訊</span><span class="sxs-lookup"><span data-stu-id="57426-159">Open Full-Screen Video</span></span>](server-controls/_static/state1.wmv)

<span data-ttu-id="57426-160">為了使伺服器控制件讀取和寫入以控制狀態,必須執行三個步驟。</span><span class="sxs-lookup"><span data-stu-id="57426-160">In order for a server control to read and write to control state, you must take three steps.</span></span>

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a><span data-ttu-id="57426-161">第一步:呼叫寄存器需求控制狀態方法</span><span class="sxs-lookup"><span data-stu-id="57426-161">Step 1: Call the RegisterRequiresControlState Method</span></span>

<span data-ttu-id="57426-162">註冊需求控制狀態方法ASP.NET通知控件需要保持控制狀態。</span><span class="sxs-lookup"><span data-stu-id="57426-162">The RegisterRequiresControlState method informs ASP.NET that a control needs to persist control state.</span></span> <span data-ttu-id="57426-163">它採用類型控制(即正在註冊的控制項)的一個參數。</span><span class="sxs-lookup"><span data-stu-id="57426-163">It takes one argument of type Control which is the control that is being registered.</span></span>

<span data-ttu-id="57426-164">請務必注意,註冊不會從請求持續到請求。</span><span class="sxs-lookup"><span data-stu-id="57426-164">It is important to note that registration does not persist from request to request.</span></span> <span data-ttu-id="57426-165">因此,如果控件要保留控制狀態,則必須在每個請求上調用此方法。</span><span class="sxs-lookup"><span data-stu-id="57426-165">Therefore, this method must be called on every request if a control is to persist control state.</span></span> <span data-ttu-id="57426-166">建議在 OnInit 中調用該方法。</span><span class="sxs-lookup"><span data-stu-id="57426-166">It is recommended that the method be called in OnInit.</span></span>

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a><span data-ttu-id="57426-167">第二步:重寫儲存控制狀態</span><span class="sxs-lookup"><span data-stu-id="57426-167">Step 2: Override SaveControlState</span></span>

<span data-ttu-id="57426-168">自上次回帖以來,SaveControlState 方法保存控制件的控制狀態更改。</span><span class="sxs-lookup"><span data-stu-id="57426-168">The SaveControlState method saves control state changes for a control since the last post back.</span></span> <span data-ttu-id="57426-169">它返回表示控件狀態的物件。</span><span class="sxs-lookup"><span data-stu-id="57426-169">It returns an object representing the control's state.</span></span>

## <a name="step-3-override-loadcontrolstate"></a><span data-ttu-id="57426-170">步驟 3:覆蓋負載控制狀態</span><span class="sxs-lookup"><span data-stu-id="57426-170">Step 3: Override LoadControlState</span></span>

<span data-ttu-id="57426-171">LoadControlState 方法將保存的狀態載入到控制項中。</span><span class="sxs-lookup"><span data-stu-id="57426-171">The LoadControlState method loads saved state into a control.</span></span> <span data-ttu-id="57426-172">該方法採用一種類型 Object 的參數,該參數保存控制項的保存狀態。</span><span class="sxs-lookup"><span data-stu-id="57426-172">The method takes one argument of type Object which holds the saved state for the control.</span></span>

## <a name="full-xhtml-compliance"></a><span data-ttu-id="57426-173">完全 XHTML 合規性</span><span class="sxs-lookup"><span data-stu-id="57426-173">Full XHTML Compliance</span></span>

<span data-ttu-id="57426-174">任何 Web 開發人員都知道標準在 Web 應用程式中的重要性。</span><span class="sxs-lookup"><span data-stu-id="57426-174">Any Web developer knows the importance of standards in Web applications.</span></span> <span data-ttu-id="57426-175">為了維護基於標準的開發環境,ASP.NET 2.0 完全符合 XHTML 標準。</span><span class="sxs-lookup"><span data-stu-id="57426-175">In order to maintain a standards-based development environment, ASP.NET 2.0 is fully XHTML compliant.</span></span> <span data-ttu-id="57426-176">因此,所有標記都根據支援 HTML 4.0 或更高程度的瀏覽器中的 XHTML 標準進行呈現。</span><span class="sxs-lookup"><span data-stu-id="57426-176">Therefore, all tags are rendered according to XHTML standards in browsers that support HTML 4.0 or greater.</span></span>

<span data-ttu-id="57426-177">ASP.NET 1.1 中的 DOCTYPE 定義如下:</span><span class="sxs-lookup"><span data-stu-id="57426-177">The DOCTYPE definition in ASP.NET 1.1 was as follows:</span></span>

[!code-html[Main](server-controls/samples/sample6.html)]

<span data-ttu-id="57426-178">在 ASP.NET 2.0 中,預設的 DOCTYPE 定義如下所示:</span><span class="sxs-lookup"><span data-stu-id="57426-178">In ASP.NET 2.0, the default DOCTYPE definition is as follows:</span></span>

[!code-html[Main](server-controls/samples/sample7.html)]

<span data-ttu-id="57426-179">如果選擇,您可以通過設定檔中的 xhtml 一致性節點更改預設 XHTML 合規性。</span><span class="sxs-lookup"><span data-stu-id="57426-179">If you choose, you can alter the default XHTML compliance via the xhtmlConformance node in the configuration file.</span></span> <span data-ttu-id="57426-180">例如,Web.config 檔中的以下節點將 XHTML 符合性更改為 XHTML 1.0 嚴格:</span><span class="sxs-lookup"><span data-stu-id="57426-180">For example, the following node in the web.config file will change XHTML compliance to XHTML 1.0 Strict:</span></span>

[!code-xml[Main](server-controls/samples/sample8.xml)]

<span data-ttu-id="57426-181">如果選擇,還可以配置ASP.NET以使用 ASP.NET 1.x 中使用的舊配置,如下所示:</span><span class="sxs-lookup"><span data-stu-id="57426-181">If you choose, you can also configure ASP.NET to use the legacy configuration used in ASP.NET 1.x as follows:</span></span>

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a><span data-ttu-id="57426-182">使用配接器進行自我調整</span><span class="sxs-lookup"><span data-stu-id="57426-182">Adaptive Rendering Using Adapters</span></span>

<span data-ttu-id="57426-183">在 ASP.NET 1.x 中&lt;,配置檔&gt;包含填充 HttpBrowser 功能物件的瀏覽器 Cap 節。</span><span class="sxs-lookup"><span data-stu-id="57426-183">In ASP.NET 1.x, the configuration file contained a &lt;browserCaps&gt; section that populated a HttpBrowserCapabilities object.</span></span> <span data-ttu-id="57426-184">此物件允許開發人員確定正在發出特定請求的設備並適當地呈現代碼。</span><span class="sxs-lookup"><span data-stu-id="57426-184">This object allowed a developer to determine what device is making a particular request and render code appropriately.</span></span> <span data-ttu-id="57426-185">在 ASP.NET 2.0 中,模型已改進,現在使用新的 ControlAdapter 類。</span><span class="sxs-lookup"><span data-stu-id="57426-185">In ASP.NET 2.0, the model has improved and now uses the new ControlAdapter class.</span></span> <span data-ttu-id="57426-186">ControlAdapter 類覆蓋控制件生命週期中的事件,並控制基於使用者代理功能的控制件的呈現。</span><span class="sxs-lookup"><span data-stu-id="57426-186">The ControlAdapter class overrides events in the control's lifecycle and controls the rendering of controls based upon the user agent's capabilities.</span></span> <span data-ttu-id="57426-187">特定使用者代理的功能由存儲在 c:_windows_microsoft.net_framework_v2.0 中的瀏覽器定義檔(具有 .browser 檔副檔名的檔案)定義。\* \*[CONFIG]瀏覽器\* \*</span><span class="sxs-lookup"><span data-stu-id="57426-187">The capabilities of a specific user agent are defined by a browser definition file (a file with a .browser file extension) stored in the c:\windows\microsoft.net\framework\v2.0.\*\*\*\*\CONFIG\Browsers folder.</span></span>

> [!NOTE]
> <span data-ttu-id="57426-188">ControlAdapter 類是一個抽象類。</span><span class="sxs-lookup"><span data-stu-id="57426-188">The ControlAdapter class is an abstract class.</span></span>

<span data-ttu-id="57426-189">與 1.x&lt;中的&gt;瀏覽器 Cap 節類似,瀏覽器定義檔案使用正則運算式來分析使用者代理字串以識別請求的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="57426-189">Much like the &lt;browserCaps&gt; section in 1.x, the browser definition file uses a Regular Expression to parse the user agent string in order to identify the requesting browser.</span></span> <span data-ttu-id="57426-190">它們定義該使用者代理的特定功能。</span><span class="sxs-lookup"><span data-stu-id="57426-190">It them defines particular capabilities for that user agent.</span></span> <span data-ttu-id="57426-191">控件適配器通過渲染方法呈現控件。</span><span class="sxs-lookup"><span data-stu-id="57426-191">The ControlAdapter renders the control via the Render method.</span></span> <span data-ttu-id="57426-192">因此,如果重寫 Render 方法,則不應在基類上調用 Render。</span><span class="sxs-lookup"><span data-stu-id="57426-192">Therefore, if you override the Render method, you should not call Render on the base class.</span></span> <span data-ttu-id="57426-193">這樣做可能會導致渲染發生兩次,一次用於適配器,一次用於控件本身。</span><span class="sxs-lookup"><span data-stu-id="57426-193">Doing so may cause rendering to occur twice, once for the adapter and once for the control itself.</span></span>

## <a name="developing-a-custom-adapter"></a><span data-ttu-id="57426-194">開發自訂介面卡</span><span class="sxs-lookup"><span data-stu-id="57426-194">Developing a Custom Adapter</span></span>

<span data-ttu-id="57426-195">您可以通過從 ControlAdapter 繼承來開發自己的自訂適配器。</span><span class="sxs-lookup"><span data-stu-id="57426-195">You can develop your own custom adapter by inheriting from ControlAdapter.</span></span> <span data-ttu-id="57426-196">此外,在頁面需要適配器的情況下,可以從抽象類 PageAdapter 繼承。</span><span class="sxs-lookup"><span data-stu-id="57426-196">Additionally, you can inherit from the abstract class PageAdapter in cases where an adapter is needed for a page.</span></span> <span data-ttu-id="57426-197">控制項映射到自訂配接器是透過瀏覽器定義檔中的&lt;控制項配接器&gt;元素完成的。</span><span class="sxs-lookup"><span data-stu-id="57426-197">Mapping of controls to your custom adapter is accomplished via the &lt;controlAdapters&gt; element in the browser definition file.</span></span> <span data-ttu-id="57426-198">例如,瀏覽器定義檔案中的以下 XML 將選單控制元件映射到 MenuAdapter 類別:</span><span class="sxs-lookup"><span data-stu-id="57426-198">For example, the following XML from a browser definition file maps the Menu control to the MenuAdapter class:</span></span>

[!code-html[Main](server-controls/samples/sample10.html)]

<span data-ttu-id="57426-199">使用此模型,控件開發人員很容易定位特定設備或瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="57426-199">Using this model, it becomes quite easy for a control developer to target a particular device or browser.</span></span> <span data-ttu-id="57426-200">對於開發人員來說,完全控制每個設備上的頁面呈現方式也非常簡單。</span><span class="sxs-lookup"><span data-stu-id="57426-200">It's also quite simple for a developer to have complete control over how pages render on every device.</span></span>

## <a name="per-device-rendering"></a><span data-ttu-id="57426-201">每裝置渲染</span><span class="sxs-lookup"><span data-stu-id="57426-201">Per-Device Rendering</span></span>

<span data-ttu-id="57426-202">ASP.NET 2.0 中的伺服器控制項屬性可以使用特定於瀏覽器的前置碼按裝置指定。</span><span class="sxs-lookup"><span data-stu-id="57426-202">Server control properties in ASP.NET 2.0 can be specified per-device using a browser-specific prefix.</span></span> <span data-ttu-id="57426-203">例如,下面的代碼將更改標籤的文本,具體取決於用於瀏覽頁面的設備。</span><span class="sxs-lookup"><span data-stu-id="57426-203">For example, the code below will change the Text of a label depending upon which device is being used to browse the page.</span></span>

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

<span data-ttu-id="57426-204">當包含此標籤的頁面從 Internet Explorer 瀏覽時,標籤將顯示文本,上面寫著"您正在從 Internet 資源管理器流覽」。。</span><span class="sxs-lookup"><span data-stu-id="57426-204">When the page containing this label is browsed from Internet Explorer, the label will display text saying "You are browsing from Internet Explorer."</span></span> <span data-ttu-id="57426-205">當從 Firefox 瀏覽頁面時,標籤將顯示文本「您正在從 Firefox 瀏覽」。</span><span class="sxs-lookup"><span data-stu-id="57426-205">When the page is browsed from Firefox, the label will display the text "You are browsing from Firefox."</span></span> <span data-ttu-id="57426-206">從任何其他設備瀏覽頁面時,將顯示「您正在從未知設備瀏覽」。</span><span class="sxs-lookup"><span data-stu-id="57426-206">When the page is browsed from any other device, it will display "You are browsing from an unknown device."</span></span> <span data-ttu-id="57426-207">可以使用此特殊語法指定任何屬性。</span><span class="sxs-lookup"><span data-stu-id="57426-207">Any property can be specified using this special syntax.</span></span>

## <a name="setting-focus"></a><span data-ttu-id="57426-208">設定焦點</span><span class="sxs-lookup"><span data-stu-id="57426-208">Setting Focus</span></span>

<span data-ttu-id="57426-209">ASP.NET 1.x 開發人員經常詢問如何將初始焦點放在特定控制項。</span><span class="sxs-lookup"><span data-stu-id="57426-209">ASP.NET 1.x developers frequently asked about how to set initial focus on a particular control.</span></span> <span data-ttu-id="57426-210">例如,在登錄頁上,讓使用者 ID 文本框在頁面首次載入時獲取焦點非常有用。</span><span class="sxs-lookup"><span data-stu-id="57426-210">For example, on a login page, it's useful to have the User ID textbox get the focus when the page first loads.</span></span> <span data-ttu-id="57426-211">在ASP.NET 1.x 中,執行此操作需要編寫一些用戶端腳本。</span><span class="sxs-lookup"><span data-stu-id="57426-211">In ASP.NET 1.x, doing this required writing some client-side script.</span></span> <span data-ttu-id="57426-212">儘管此類腳本是一項瑣碎的任務,但由於 SetFocus 方法,ASP.NET 2.0 中不再需要它。</span><span class="sxs-lookup"><span data-stu-id="57426-212">Even though such a script is a trivial task, it's no longer necessary in ASP.NET 2.0 thanks to the SetFocus method.</span></span> <span data-ttu-id="57426-213">SetFocus 方法採用一個參數,指示應接收焦點的控制項。</span><span class="sxs-lookup"><span data-stu-id="57426-213">The SetFocus method takes one argument indicating the control that should receive focus.</span></span> <span data-ttu-id="57426-214">此參數可以是控制項的客戶端 ID 作為字串,也可以是 Server 控制件的名稱作為控制項物件。</span><span class="sxs-lookup"><span data-stu-id="57426-214">This argument can either be the client ID of the control as a string or the name of the Server control as a Control object.</span></span> <span data-ttu-id="57426-215">例如,要將初始焦點設定為頁面首次載入時稱為 txtUserID 的 TextBox 控制項\_,請向頁面載入新增以下代碼:</span><span class="sxs-lookup"><span data-stu-id="57426-215">For example, to set the initial focus to a TextBox control called txtUserID when the page first loads, add the following code to Page\_Load:</span></span>

[!code-csharp[Main](server-controls/samples/sample12.cs)]

<span data-ttu-id="57426-216">- 或</span><span class="sxs-lookup"><span data-stu-id="57426-216">-- or</span></span>

[!code-csharp[Main](server-controls/samples/sample13.cs)]

<span data-ttu-id="57426-217">ASP.NET 2.0 使用 Webresource.axd 處理程式(前面討論)來呈現設置焦點的用戶端函數。</span><span class="sxs-lookup"><span data-stu-id="57426-217">ASP.NET 2.0 uses the Webresource.axd handler (discussed previously) to render a client-side function that sets the focus.</span></span> <span data-ttu-id="57426-218">用戶端函數的名稱是 WebForm\_自動焦點,如下所示:</span><span class="sxs-lookup"><span data-stu-id="57426-218">The name of the client-side function is WebForm\_AutoFocus as shown here:</span></span>

[!code-html[Main](server-controls/samples/sample14.html)]

<span data-ttu-id="57426-219">或者,可以使用控制項的 Focus 方法將初始焦點設定為該控制項。</span><span class="sxs-lookup"><span data-stu-id="57426-219">Alternatively, you can use the Focus method for a control to set the initial focus to that control.</span></span> <span data-ttu-id="57426-220">Focus 方法派生自 Control 類,可用於所有ASP.NET 2.0 控件。</span><span class="sxs-lookup"><span data-stu-id="57426-220">The Focus method derives from the Control class and is available to all ASP.NET 2.0 controls.</span></span> <span data-ttu-id="57426-221">當發生驗證錯誤時,還可以將焦點設置為特定控制項。</span><span class="sxs-lookup"><span data-stu-id="57426-221">It is also possible to set focus to a particular control when a validation error occurs.</span></span> <span data-ttu-id="57426-222">稍後將介紹這一點。</span><span class="sxs-lookup"><span data-stu-id="57426-222">That will be covered in a later module.</span></span>

## <a name="new-server-controls-in-aspnet-20"></a><span data-ttu-id="57426-223">ASP.NET 2.0 中的新伺服器控制項</span><span class="sxs-lookup"><span data-stu-id="57426-223">New Server Controls in ASP.NET 2.0</span></span>

<span data-ttu-id="57426-224">以下是 ASP.NET 2.0 中的新伺服器控制件。</span><span class="sxs-lookup"><span data-stu-id="57426-224">The following are new server controls in ASP.NET 2.0.</span></span> <span data-ttu-id="57426-225">我們將在後面的模組中更詳細地介紹其中一些內容。</span><span class="sxs-lookup"><span data-stu-id="57426-225">We will go into more detail on some of them in later modules.</span></span>

## <a name="imagemap-control"></a><span data-ttu-id="57426-226">影像對應控制項</span><span class="sxs-lookup"><span data-stu-id="57426-226">ImageMap Control</span></span>

<span data-ttu-id="57426-227">ImageMap 控制項允許您向影像添加熱點,該影像可以啟動帖子或導航到 URL。</span><span class="sxs-lookup"><span data-stu-id="57426-227">The ImageMap control allows you to add hotspots to an image that can initiate a post back or navigate to a URL.</span></span> <span data-ttu-id="57426-228">有三種類型的熱點可用;圓熱點、矩形熱點和多邊形熱點。</span><span class="sxs-lookup"><span data-stu-id="57426-228">There are three types of hotspots available; CircleHotSpot, RectangleHotSpot, and PolygonHotSpot.</span></span> <span data-ttu-id="57426-229">熱點透過 Visual Studio 中的集合編輯器添加,或在代碼中以程式設計方式添加。</span><span class="sxs-lookup"><span data-stu-id="57426-229">Hotspots are added via a collection editor in Visual Studio or programmatically in code.</span></span> <span data-ttu-id="57426-230">沒有可用於在圖像上繪製熱點的用戶介面。</span><span class="sxs-lookup"><span data-stu-id="57426-230">There is no user-interface available for drawing hotspots on an image.</span></span> <span data-ttu-id="57426-231">必須聲明性地指定熱點的座標、大小或半徑。</span><span class="sxs-lookup"><span data-stu-id="57426-231">The coordinates and size or radius of the hotspot must be specified declaratively.</span></span> <span data-ttu-id="57426-232">設計器中也沒有熱點的可視表示形式。</span><span class="sxs-lookup"><span data-stu-id="57426-232">There is also no visual representation of a hotspot in the designer.</span></span> <span data-ttu-id="57426-233">如果熱點配置為導航到 URL,則 URL 將通過熱點的 NavigateUrl 屬性指定。</span><span class="sxs-lookup"><span data-stu-id="57426-233">If a hotspot is configured to navigate to a URL, the URL is specified via the NavigateUrl property of the hotspot.</span></span> <span data-ttu-id="57426-234">在後回熱點的情況下,PostBackValue 屬性允許您傳遞後回的字串,該字串可以在伺服器端代碼中檢索。</span><span class="sxs-lookup"><span data-stu-id="57426-234">In the case of a post back hotspot, the PostBackValue property allows you to pass a string in the post back that can be retrieved in server-side code.</span></span>

![視覺化工作室中的熱點集合編輯器](server-controls/_static/image1.jpg)

<span data-ttu-id="57426-236">**圖 1**: 視覺化工作室中的熱點集合編輯器</span><span class="sxs-lookup"><span data-stu-id="57426-236">**Figure 1**: HotSpot Collection Editor in Visual Studio</span></span>

## <a name="bulletedlist-control"></a><span data-ttu-id="57426-237">項目符號清單控制</span><span class="sxs-lookup"><span data-stu-id="57426-237">BulletedList Control</span></span>

<span data-ttu-id="57426-238">項目符號清單「控制件是一個項目符號清單,可以輕鬆綁定數據。</span><span class="sxs-lookup"><span data-stu-id="57426-238">The BulletedList control is a bulleted list that can easily be data bound.</span></span> <span data-ttu-id="57426-239">清單可以通過「項目符號樣式」屬性排序(編號)或無序排序。</span><span class="sxs-lookup"><span data-stu-id="57426-239">The list can be ordered (numbered) or unordered via the BulletStyle property.</span></span> <span data-ttu-id="57426-240">清單中的每個項都由 ListItem 物件表示。</span><span class="sxs-lookup"><span data-stu-id="57426-240">Each item in the list is represented by a ListItem object.</span></span>

![視覺化工作室中的項目符號清單控制](server-controls/_static/image1.gif)

<span data-ttu-id="57426-242">**圖 2**: 視覺化工作室中的項目清單控制</span><span class="sxs-lookup"><span data-stu-id="57426-242">**Figure 2**: BulletedList Control in Visual Studio</span></span>

## <a name="hiddenfield-control"></a><span data-ttu-id="57426-243">隱藏欄位控制</span><span class="sxs-lookup"><span data-stu-id="57426-243">HiddenField Control</span></span>

<span data-ttu-id="57426-244">HiddenField 控制件向頁面添加隱藏表單欄位,其值在伺服器端代碼中可用。</span><span class="sxs-lookup"><span data-stu-id="57426-244">The HiddenField control adds a hidden form field to your page, the value of which is available in server-side code.</span></span> <span data-ttu-id="57426-245">隱藏窗體欄位的值通常預計在後背之間保持不變。</span><span class="sxs-lookup"><span data-stu-id="57426-245">The value of a hidden form field is generally expected to remain unchanged between post backs.</span></span> <span data-ttu-id="57426-246">但是,惡意使用者可能會在回發佈之前更改該值。</span><span class="sxs-lookup"><span data-stu-id="57426-246">However, it is possible for a malicious user to change the value prior to post back.</span></span> <span data-ttu-id="57426-247">如果發生這種情況,"隱藏欄位"控制件將引發"值更改"事件。</span><span class="sxs-lookup"><span data-stu-id="57426-247">If this happens, the HiddenField control will raise the ValueChanged event.</span></span> <span data-ttu-id="57426-248">如果在 HiddenField 控制件中具有敏感資訊,並且希望確保資訊保持不變,則應在代碼中處理 Value"更改"事件。</span><span class="sxs-lookup"><span data-stu-id="57426-248">If you have sensitive information in the HiddenField control and you want to ensure that it remains unchanged, you should handle the ValueChanged event in your code.</span></span>

## <a name="fileupload-control"></a><span data-ttu-id="57426-249">檔案上傳控制</span><span class="sxs-lookup"><span data-stu-id="57426-249">FileUpload Control</span></span>

<span data-ttu-id="57426-250">ASP.NET 2.0 中的 FileUpload 控制件使得可以通過 ASP.NET 頁面將檔上傳到 Web 伺服器成為可能。</span><span class="sxs-lookup"><span data-stu-id="57426-250">The FileUpload control in ASP.NET 2.0 makes it possible to upload files to a Web server via an ASP.NET page.</span></span> <span data-ttu-id="57426-251">此控制項與 ASP.NET 1.x HtmlInputFile 類非常相似,但有一些例外。</span><span class="sxs-lookup"><span data-stu-id="57426-251">This control is quite similar to the ASP.NET 1.x HtmlInputFile class with a few exceptions.</span></span> <span data-ttu-id="57426-252">在 ASP.NET 1.x 中,建議將「已發布檔」屬性檢查為 null,以確定您是否具有良好的檔。</span><span class="sxs-lookup"><span data-stu-id="57426-252">In ASP.NET 1.x, it was recommended that the PostedFile property be checked for null in order to determine if you had a good file.</span></span> <span data-ttu-id="57426-253">ASP.NET 2.0 中的 FileUpload 控件添加了一個新的 HasFile 屬性,您可以將其用於同一目的,並且效率更高一些。</span><span class="sxs-lookup"><span data-stu-id="57426-253">The FileUpload control in ASP.NET 2.0 adds a new HasFile property that you can use for the same purpose and it's a bit more efficient.</span></span>

<span data-ttu-id="57426-254">已發布檔屬性仍可用於訪問 HttpPostedFile 物件,但 HttpPostedFile 的某些功能現在可透過 FileUpload 控制檔在本質上可用。</span><span class="sxs-lookup"><span data-stu-id="57426-254">The PostedFile property is still available for access to an HttpPostedFile object, but some of the functionality of the HttpPostedFile is now available intrinsically with the FileUpload control.</span></span> <span data-ttu-id="57426-255">例如,要將上載的檔保存在 ASP.NET 1.x 中,請調用 HttpPostedFile 物件上的 SaveAs 方法。</span><span class="sxs-lookup"><span data-stu-id="57426-255">For example, to save an uploaded file in ASP.NET 1.x, you call the SaveAs method on the HttpPostedFile object.</span></span> <span data-ttu-id="57426-256">使用 ASP.NET 2.0 中的 FileUpload 控制項,您將在 FileUpload 控制項本身上調用 SaveAs 方法。</span><span class="sxs-lookup"><span data-stu-id="57426-256">Using the FileUpload control in ASP.NET 2.0, you would call the SaveAs method on the FileUpload control itself.</span></span>

<span data-ttu-id="57426-257">2.0 行為(可能是最重要的更改)的另一個重要變化是,在保存整個上載的檔之前,不再需要將整個上載的檔載入到記憶體中。</span><span class="sxs-lookup"><span data-stu-id="57426-257">Another significant change in the 2.0 behavior (and likely the most significant change) is that it is no longer necessary to load an entire uploaded file into memory before saving it.</span></span> <span data-ttu-id="57426-258">在 1.x 中,上傳的任何檔在寫入磁碟之前都完全保存到記憶體中。</span><span class="sxs-lookup"><span data-stu-id="57426-258">In 1.x, any file that was uploaded is saved entirely into memory prior to being written to disk.</span></span> <span data-ttu-id="57426-259">此體系結構可防止上載大型檔。</span><span class="sxs-lookup"><span data-stu-id="57426-259">This architecture prevents the upload of large files.</span></span>

<span data-ttu-id="57426-260">在 ASP.NET 2.0 中,HTTPRuntime 元素的請求長度磁碟閾值屬性允許您設定在寫入磁碟之前在記憶體中存儲緩衝區中的數量。</span><span class="sxs-lookup"><span data-stu-id="57426-260">In ASP.NET 2.0, the requestLengthDiskThreshold attribute of the httpRuntime element allows you to configure how many Kilobytes are held in a buffer in memory prior to being written to disk.</span></span>

<span data-ttu-id="57426-261">**重要提示**:MSDN 文件(和其他地方的文檔)指定此值以位元組為單位(不是千位元組),預設值為 256。</span><span class="sxs-lookup"><span data-stu-id="57426-261">**IMPORTANT**: MSDN documentation (and documentation elsewhere) specifies that this value is in bytes (not Kilobytes) and that the default is 256.</span></span> <span data-ttu-id="57426-262">該值實際上以千位元組為單位指定,預設值為 80。</span><span class="sxs-lookup"><span data-stu-id="57426-262">The value is actually specified in Kilobytes and the default value is 80.</span></span> <span data-ttu-id="57426-263">通過預設值 80K,我們確保緩衝區不會最終位於大型物件堆上。</span><span class="sxs-lookup"><span data-stu-id="57426-263">By having a default value of 80K, we ensure that the buffer does not end up on the large object heap.</span></span>

## <a name="wizard-control"></a><span data-ttu-id="57426-264">向導控制</span><span class="sxs-lookup"><span data-stu-id="57426-264">Wizard Control</span></span>

<span data-ttu-id="57426-265">遇到ASP.NET開發人員在嘗試使用面板在一系列「頁面」中收集資訊或從一個頁面傳輸到一個頁面時遇到這樣的常見情況。</span><span class="sxs-lookup"><span data-stu-id="57426-265">It is fairly common to encounter ASP.NET developers struggling with attempting to gather information in a series of "pages" using panels or by transferring from page to page.</span></span> <span data-ttu-id="57426-266">很多時候,這種努力是令人沮喪的,而且非常耗時。</span><span class="sxs-lookup"><span data-stu-id="57426-266">More often than not, the endeavor is a frustrating one and is time consuming.</span></span> <span data-ttu-id="57426-267">新的嚮導控件通過在使用者熟悉的嚮導介面中允許線性和非線性步驟來解決問題。</span><span class="sxs-lookup"><span data-stu-id="57426-267">The new Wizard control solves the problems by allowing for linear and non-linear steps in a wizard interface that users are familiar with.</span></span> <span data-ttu-id="57426-268">嚮導控制項以一系列步驟顯示輸入窗體。</span><span class="sxs-lookup"><span data-stu-id="57426-268">The Wizard control presents input forms in a series of steps.</span></span> <span data-ttu-id="57426-269">每個步驟都是控件的 StepType 屬性指定的特定類型。</span><span class="sxs-lookup"><span data-stu-id="57426-269">Each step is of a particular type specified by the StepType property of the control.</span></span> <span data-ttu-id="57426-270">可用的步驟類型如下:</span><span class="sxs-lookup"><span data-stu-id="57426-270">The available step types are as follows:</span></span>

| <span data-ttu-id="57426-271">**步長類型**</span><span class="sxs-lookup"><span data-stu-id="57426-271">**Step Type**</span></span> | <span data-ttu-id="57426-272">**說明**</span><span class="sxs-lookup"><span data-stu-id="57426-272">**Explanation**</span></span> |
| --- | --- |
| <span data-ttu-id="57426-273">Auto</span><span class="sxs-lookup"><span data-stu-id="57426-273">Auto</span></span> | <span data-ttu-id="57426-274">嚮導根據步驟層次結構中的位置自動確定步驟的類型。</span><span class="sxs-lookup"><span data-stu-id="57426-274">The wizard automatically determines the type of step based upon its position within the step hierarchy.</span></span> |
| <span data-ttu-id="57426-275">Start</span><span class="sxs-lookup"><span data-stu-id="57426-275">Start</span></span> | <span data-ttu-id="57426-276">第一步,通常用於提出介紹性陳述。</span><span class="sxs-lookup"><span data-stu-id="57426-276">The first step, often used to present an introductory statement.</span></span> |
| <span data-ttu-id="57426-277">步驟</span><span class="sxs-lookup"><span data-stu-id="57426-277">Step</span></span> | <span data-ttu-id="57426-278">正常步驟。</span><span class="sxs-lookup"><span data-stu-id="57426-278">A normal step.</span></span> |
| <span data-ttu-id="57426-279">[完成]</span><span class="sxs-lookup"><span data-stu-id="57426-279">Finish</span></span> | <span data-ttu-id="57426-280">最後一步,通常用於顯示一個按鈕來完成嚮導。</span><span class="sxs-lookup"><span data-stu-id="57426-280">The final step, usually used to present a button to finish the wizard.</span></span> |
| <span data-ttu-id="57426-281">[完成]</span><span class="sxs-lookup"><span data-stu-id="57426-281">Complete</span></span> | <span data-ttu-id="57426-282">顯示傳達成功或失敗的資訊。</span><span class="sxs-lookup"><span data-stu-id="57426-282">Presents a message communicating success or failure.</span></span> |

> [!NOTE]
> <span data-ttu-id="57426-283">嚮導控制件使用ASP.NET控制狀態追蹤其狀態。</span><span class="sxs-lookup"><span data-stu-id="57426-283">The Wizard control keeps track of its state using ASP.NET control state.</span></span> <span data-ttu-id="57426-284">因此,啟用檢視狀態屬性可以設置為 false,而不會造成任何損害。</span><span class="sxs-lookup"><span data-stu-id="57426-284">Therefore, the EnableViewState property can be set to false without any detriment.</span></span>

<span data-ttu-id="57426-285">此視頻是嚮導控件的演練。</span><span class="sxs-lookup"><span data-stu-id="57426-285">This video is a walkthrough of the Wizard control.</span></span>

![](server-controls/_static/image2.png)

[<span data-ttu-id="57426-286">開啟全螢幕視訊</span><span class="sxs-lookup"><span data-stu-id="57426-286">Open Full-Screen Video</span></span>](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a><span data-ttu-id="57426-287">本地化控制</span><span class="sxs-lookup"><span data-stu-id="57426-287">Localize Control</span></span>

<span data-ttu-id="57426-288">當地語系化控制項類似於文字控制項。</span><span class="sxs-lookup"><span data-stu-id="57426-288">The Localize control is similar to a Literal control.</span></span> <span data-ttu-id="57426-289">但是,當地語系化控制項具有一個**Mode**屬性,用於控制如何向其添加標記。</span><span class="sxs-lookup"><span data-stu-id="57426-289">However, the Localize control has a **Mode** property that controls how markup that is added to it is rendered.</span></span> <span data-ttu-id="57426-290">Mode 屬性支援以下值:</span><span class="sxs-lookup"><span data-stu-id="57426-290">The Mode property supports the following values:</span></span>

| <span data-ttu-id="57426-291">**Mode**</span><span class="sxs-lookup"><span data-stu-id="57426-291">**Mode**</span></span> | <span data-ttu-id="57426-292">**說明**</span><span class="sxs-lookup"><span data-stu-id="57426-292">**Explanation**</span></span> |
| --- | --- |
| <span data-ttu-id="57426-293">轉換</span><span class="sxs-lookup"><span data-stu-id="57426-293">Transform</span></span> | <span data-ttu-id="57426-294">標記根據發出請求的瀏覽器的協議進行轉換。</span><span class="sxs-lookup"><span data-stu-id="57426-294">Markup is transformed according to the protocol of the browser making the request.</span></span> |
| <span data-ttu-id="57426-295">直通</span><span class="sxs-lookup"><span data-stu-id="57426-295">PassThrough</span></span> | <span data-ttu-id="57426-296">標記將呈現為"正樣"。</span><span class="sxs-lookup"><span data-stu-id="57426-296">Markup is rendered as-is.</span></span> |
| <span data-ttu-id="57426-297">編碼</span><span class="sxs-lookup"><span data-stu-id="57426-297">Encode</span></span> | <span data-ttu-id="57426-298">新增到控制項的標記使用 HtmlEncode 進行編碼。</span><span class="sxs-lookup"><span data-stu-id="57426-298">Markup that is added to the control is encoded using HtmlEncode.</span></span> |

## <a name="multiview-and-view-controls"></a><span data-ttu-id="57426-299">多檢視及檢視控制項</span><span class="sxs-lookup"><span data-stu-id="57426-299">MultiView and View Controls</span></span>

<span data-ttu-id="57426-300">MultiView 控件充當檢視控制件的容器,檢視控制項充當其他控制項的容器(與面板控制項類似)。</span><span class="sxs-lookup"><span data-stu-id="57426-300">The MultiView control acts as a container for View controls, and the View control acts as a container (much like a Panel control) for other controls.</span></span> <span data-ttu-id="57426-301">MultiView 控制件中的每個檢視都由單個檢視控制項表示。</span><span class="sxs-lookup"><span data-stu-id="57426-301">Each view in a MultiView control is represented by a single View control.</span></span> <span data-ttu-id="57426-302">MultiView 中的第一個檢視控件是視圖 0,第二個視圖 1 等。您可以通過指定 MultiView 控制件的 ActiveViewIndex 來切換檢視。</span><span class="sxs-lookup"><span data-stu-id="57426-302">The first View control in the MultiView is view 0, the second is view 1, etc. You can switch views by specifying the ActiveViewIndex of the MultiView control.</span></span>

## <a name="substitution-control"></a><span data-ttu-id="57426-303">替代控制</span><span class="sxs-lookup"><span data-stu-id="57426-303">Substitution Control</span></span>

<span data-ttu-id="57426-304">替換控制項與ASP.NET快取一起使用。</span><span class="sxs-lookup"><span data-stu-id="57426-304">The Substitution control is used in conjunction with ASP.NET caching.</span></span> <span data-ttu-id="57426-305">如果要利用緩存,但具有必須在每個請求上更新頁面的某些部分(換句話說,免除緩存的頁面部分),則替換元件提供了一個很好的解決方案。</span><span class="sxs-lookup"><span data-stu-id="57426-305">In cases where you want to take advantage of caching, but you have portions of a page that must be updated on each request (in other words, portions of a page that are exempt from caching), the Substitution component provides a great solution.</span></span> <span data-ttu-id="57426-306">控件實際上不會自行呈現任何輸出。</span><span class="sxs-lookup"><span data-stu-id="57426-306">The control doesn't actually render any output on its own.</span></span> <span data-ttu-id="57426-307">相反,它綁定到伺服器端代碼中的方法。</span><span class="sxs-lookup"><span data-stu-id="57426-307">Instead, it is bound to a method in server-side code.</span></span> <span data-ttu-id="57426-308">請求頁面時,將調用該方法,並呈現返回的標記來代替替換控制項。</span><span class="sxs-lookup"><span data-stu-id="57426-308">When the page is requested, the method is called and the returned markup is rendered in place of the substitution control.</span></span>

<span data-ttu-id="57426-309">透過**MethodName**屬性指定替換控制項的結合的方法。</span><span class="sxs-lookup"><span data-stu-id="57426-309">The method to which the Substitution control is bound is specified via the **MethodName** property.</span></span> <span data-ttu-id="57426-310">該方法必須滿足以下條件:</span><span class="sxs-lookup"><span data-stu-id="57426-310">That method must meet the following criteria:</span></span>

- <span data-ttu-id="57426-311">它必須是靜態(在VB中共用)方法。</span><span class="sxs-lookup"><span data-stu-id="57426-311">It must be a static (shared in VB) method.</span></span>
- <span data-ttu-id="57426-312">它接受 HTTPContext 類型的一個參數。</span><span class="sxs-lookup"><span data-stu-id="57426-312">It accepts one parameter of type HttpContext.</span></span>
- <span data-ttu-id="57426-313">它返回一個字串,表示應替換頁面上的控件的標記。</span><span class="sxs-lookup"><span data-stu-id="57426-313">It returns a string representing the markup that should replace the control on the page.</span></span>

<span data-ttu-id="57426-314">替換控制項無法修改頁面上的任何其他控制項,但它確實可以透過其參數存取目前 HTTPContext。</span><span class="sxs-lookup"><span data-stu-id="57426-314">The Substitution control does not have the ability to modify any other control on the page, but it does have access to the current HttpContext via its parameter.</span></span>

## <a name="gridview-control"></a><span data-ttu-id="57426-315">格線檢視控制</span><span class="sxs-lookup"><span data-stu-id="57426-315">GridView Control</span></span>

<span data-ttu-id="57426-316">GridView 控件是 DataGrid 控制件的替換。</span><span class="sxs-lookup"><span data-stu-id="57426-316">The GridView control is the replacement for the DataGrid control.</span></span> <span data-ttu-id="57426-317">此控件將在後面的模組中更詳細地介紹。</span><span class="sxs-lookup"><span data-stu-id="57426-317">This control will be covered in more detail in a later module.</span></span>

## <a name="detailsview-control"></a><span data-ttu-id="57426-318">詳細資訊檢視控制項</span><span class="sxs-lookup"><span data-stu-id="57426-318">DetailsView Control</span></span>

<span data-ttu-id="57426-319">"詳細資訊檢視"控制件允許您從資料源顯示單個記錄,並對其進行編輯或刪除。</span><span class="sxs-lookup"><span data-stu-id="57426-319">The DetailsView control allows you to display a single record from a data source and to edit or delete it.</span></span> <span data-ttu-id="57426-320">在後面的模組中更詳細地介紹它。</span><span class="sxs-lookup"><span data-stu-id="57426-320">It is covered in more detail in a later module.</span></span>

## <a name="formview-control"></a><span data-ttu-id="57426-321">表單檢視控制項</span><span class="sxs-lookup"><span data-stu-id="57426-321">FormView Control</span></span>

<span data-ttu-id="57426-322">FormView 控制項用於在可配置的界面中顯示來自資料源的單個記錄。</span><span class="sxs-lookup"><span data-stu-id="57426-322">The FormView control is used to display a single record from a datasource in a configurable interface.</span></span> <span data-ttu-id="57426-323">在後面的模組中更詳細地介紹它。</span><span class="sxs-lookup"><span data-stu-id="57426-323">It is covered in more detail in a later module.</span></span>

## <a name="accessdatasource-control"></a><span data-ttu-id="57426-324">存取資料來源控制</span><span class="sxs-lookup"><span data-stu-id="57426-324">AccessDataSource Control</span></span>

<span data-ttu-id="57426-325">AccessDataSource 控制項用於資料綁定 Access 資料庫。</span><span class="sxs-lookup"><span data-stu-id="57426-325">The AccessDataSource control is used to data bind an Access database.</span></span> <span data-ttu-id="57426-326">在後面的模組中更詳細地介紹它。</span><span class="sxs-lookup"><span data-stu-id="57426-326">It is covered in more detail in a later module.</span></span>

## <a name="objectdatasource-control"></a><span data-ttu-id="57426-327">物件資料來源控制</span><span class="sxs-lookup"><span data-stu-id="57426-327">ObjectDataSource Control</span></span>

<span data-ttu-id="57426-328">ObjectDataSource 控制項用於支援三層體系結構,以便控制項可以將資料綁定到中介層業務物件,而不是控制項直接綁定到資料源的雙層模型。</span><span class="sxs-lookup"><span data-stu-id="57426-328">The ObjectDataSource control is used to support a three-tier architecture so that controls can be data-bound to a middle-tier business object as opposed to a two-tiered model where controls are bound directly to the data source.</span></span> <span data-ttu-id="57426-329">稍後將在後面的模組中更詳細地討論它。</span><span class="sxs-lookup"><span data-stu-id="57426-329">It will be discussed in more detail in a later module.</span></span>

## <a name="xmldatasource-control"></a><span data-ttu-id="57426-330">XmlDataSource 控制</span><span class="sxs-lookup"><span data-stu-id="57426-330">XmlDataSource Control</span></span>

<span data-ttu-id="57426-331">XmlDataSource 控制項用於結合XML資料來源的資料。</span><span class="sxs-lookup"><span data-stu-id="57426-331">The XmlDataSource control is used to data bind to an XML data source.</span></span> <span data-ttu-id="57426-332">在後面的模組中更詳細地介紹它。</span><span class="sxs-lookup"><span data-stu-id="57426-332">It is covered in more detail in a later module.</span></span>

## <a name="sitemapdatasource-control"></a><span data-ttu-id="57426-333">站台對應資料來源控制</span><span class="sxs-lookup"><span data-stu-id="57426-333">SiteMapDataSource Control</span></span>

<span data-ttu-id="57426-334">SiteMapDataSource 控制件基於網站地圖為網站導航控制件提供數據綁定。</span><span class="sxs-lookup"><span data-stu-id="57426-334">The SiteMapDataSource control provides data binding for site navigation controls based on a site map.</span></span> <span data-ttu-id="57426-335">稍後將在後面的模組中更詳細地討論它。</span><span class="sxs-lookup"><span data-stu-id="57426-335">It will be discussed in more detail in a later module.</span></span>

## <a name="sitemappath-control"></a><span data-ttu-id="57426-336">站台地圖路徑控制</span><span class="sxs-lookup"><span data-stu-id="57426-336">SiteMapPath Control</span></span>

<span data-ttu-id="57426-337">SiteMapPath 控制項顯示一系列導航連結,通常稱為痕跡。</span><span class="sxs-lookup"><span data-stu-id="57426-337">The SiteMapPath control displays a series of navigation links commonly referred to as breadcrumbs.</span></span> <span data-ttu-id="57426-338">在後面的模組中更詳細地介紹它。</span><span class="sxs-lookup"><span data-stu-id="57426-338">It is covered in more detail in a later module.</span></span>

## <a name="menu-control"></a><span data-ttu-id="57426-339">功能表控制項</span><span class="sxs-lookup"><span data-stu-id="57426-339">Menu Control</span></span>

<span data-ttu-id="57426-340">"選單"控制項使用 DHTML 顯示動態功能表。</span><span class="sxs-lookup"><span data-stu-id="57426-340">The Menu control displays dynamic menus using DHTML.</span></span> <span data-ttu-id="57426-341">在後面的模組中更詳細地介紹它。</span><span class="sxs-lookup"><span data-stu-id="57426-341">It is covered in more detail in a later module.</span></span>

## <a name="treeview-control"></a><span data-ttu-id="57426-342">TreeView 控制項</span><span class="sxs-lookup"><span data-stu-id="57426-342">TreeView Control</span></span>

<span data-ttu-id="57426-343">TreeView 控件用於顯示數據的分層樹視圖。</span><span class="sxs-lookup"><span data-stu-id="57426-343">The TreeView control is used to display a hierarchical tree view of data.</span></span> <span data-ttu-id="57426-344">在後面的模組中更詳細地介紹它。</span><span class="sxs-lookup"><span data-stu-id="57426-344">It is covered in more detail in a later module.</span></span>

## <a name="login-control"></a><span data-ttu-id="57426-345">登入控制</span><span class="sxs-lookup"><span data-stu-id="57426-345">Login Control</span></span>

<span data-ttu-id="57426-346">登錄控件提供了登錄到網站的機制。</span><span class="sxs-lookup"><span data-stu-id="57426-346">The Login control provides for a mechanism to log into a Web site.</span></span> <span data-ttu-id="57426-347">在後面的模組中更詳細地介紹它。</span><span class="sxs-lookup"><span data-stu-id="57426-347">It is covered in more detail in a later module.</span></span>

## <a name="loginview-control"></a><span data-ttu-id="57426-348">LoginView 控制項</span><span class="sxs-lookup"><span data-stu-id="57426-348">LoginView Control</span></span>

<span data-ttu-id="57426-349">登錄視圖控制件允許根據使用者的登錄狀態顯示不同的範本。</span><span class="sxs-lookup"><span data-stu-id="57426-349">The LoginView control allows for the display of different templates based upon a user's login status.</span></span> <span data-ttu-id="57426-350">在後面的模組中更詳細地介紹它。</span><span class="sxs-lookup"><span data-stu-id="57426-350">It is covered in more detail in a later module.</span></span>

## <a name="passwordrecovery-control"></a><span data-ttu-id="57426-351">密碼修復控制</span><span class="sxs-lookup"><span data-stu-id="57426-351">PasswordRecovery Control</span></span>

<span data-ttu-id="57426-352">密碼恢復控制項用於檢索ASP.NET應用程式的使用者忘記的密碼。</span><span class="sxs-lookup"><span data-stu-id="57426-352">The PasswordRecovery control is used to retrieve forgotten passwords by users of an ASP.NET application.</span></span> <span data-ttu-id="57426-353">在後面的模組中更詳細地介紹它。</span><span class="sxs-lookup"><span data-stu-id="57426-353">It is covered in more detail in a later module.</span></span>

## <a name="loginstatus"></a><span data-ttu-id="57426-354">LoginStatus</span><span class="sxs-lookup"><span data-stu-id="57426-354">LoginStatus</span></span>

<span data-ttu-id="57426-355">登錄狀態控制項顯示使用者的登錄狀態。</span><span class="sxs-lookup"><span data-stu-id="57426-355">The LoginStatus control displays a user's login status.</span></span> <span data-ttu-id="57426-356">在後面的模組中更詳細地介紹它。</span><span class="sxs-lookup"><span data-stu-id="57426-356">It is covered in more detail in a later module.</span></span>

## <a name="loginname"></a><span data-ttu-id="57426-357">LoginName</span><span class="sxs-lookup"><span data-stu-id="57426-357">LoginName</span></span>

<span data-ttu-id="57426-358">登錄名稱控制件在登入ASP.NET應用程式後顯示使用者的使用者名。</span><span class="sxs-lookup"><span data-stu-id="57426-358">The LoginName control displays a user's username after being logged into an ASP.NET application.</span></span> <span data-ttu-id="57426-359">在後面的模組中更詳細地介紹它。</span><span class="sxs-lookup"><span data-stu-id="57426-359">It is covered in more detail in a later module.</span></span>

## <a name="createuserwizard"></a><span data-ttu-id="57426-360">建立使用者精靈</span><span class="sxs-lookup"><span data-stu-id="57426-360">CreateUserWizard</span></span>

<span data-ttu-id="57426-361">CreateUserWizard 是一個可配置的嚮導,它使用戶能夠創建ASP.NET成員資格帳戶,供ASP.NET應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="57426-361">The CreateUserWizard is a configurable wizard which gives users the ability to create an ASP.NET Membership account for use in an ASP.NET application.</span></span> <span data-ttu-id="57426-362">在後面的模組中更詳細地介紹它。</span><span class="sxs-lookup"><span data-stu-id="57426-362">It is covered in more detail in a later module.</span></span>

## <a name="changepassword"></a><span data-ttu-id="57426-363">ChangePassword</span><span class="sxs-lookup"><span data-stu-id="57426-363">ChangePassword</span></span>

<span data-ttu-id="57426-364">更改密碼控制項允許使用者更改其ASP.NET應用程式的密碼。</span><span class="sxs-lookup"><span data-stu-id="57426-364">The ChangePassword control allows users to change their password for an ASP.NET application.</span></span> <span data-ttu-id="57426-365">在後面的模組中更詳細地介紹它。</span><span class="sxs-lookup"><span data-stu-id="57426-365">It is covered in more detail in a later module.</span></span>

## <a name="various-webparts"></a><span data-ttu-id="57426-366">各種 Web 組件</span><span class="sxs-lookup"><span data-stu-id="57426-366">Various WebParts</span></span>

<span data-ttu-id="57426-367">ASP.NET 2.0 船舶與各種 Web 部件。</span><span class="sxs-lookup"><span data-stu-id="57426-367">ASP.NET 2.0 ships with various Web Parts.</span></span> <span data-ttu-id="57426-368">這些將在後面的模組中詳細介紹。</span><span class="sxs-lookup"><span data-stu-id="57426-368">These will be covered in detail in a later module.</span></span>
