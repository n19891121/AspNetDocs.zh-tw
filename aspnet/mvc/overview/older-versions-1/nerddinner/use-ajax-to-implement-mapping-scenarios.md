---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: 使用 AJAX 實現映射機制 :微軟文件
author: rick-anderson
description: 步驟 11 展示如何將 AJAX 映射支援整合到我們的 NerdDinner 應用程式中,使正在建立、編輯或查看晚餐的使用者能夠查看 l...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: f2e2640eb421d5ee8006915f46cbe1090b8d21ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542582"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a><span data-ttu-id="737d3-103">使用 AJAX 實作對應實例</span><span class="sxs-lookup"><span data-stu-id="737d3-103">Use AJAX to Implement Mapping Scenarios</span></span>

<span data-ttu-id="737d3-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="737d3-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="737d3-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="737d3-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="737d3-106">這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第11步,該教學示範如何使用mVC 1構建小型但完整的Web應用程式ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="737d3-106">This is step 11 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="737d3-107">步驟 11 展示如何將 AJAX 映射支援整合到我們的 NerdDinner 應用程式中,使正在創建、編輯或查看晚餐的用戶能夠以圖形方式查看晚餐的位置。</span><span class="sxs-lookup"><span data-stu-id="737d3-107">Step 11 shows how to integrate AJAX mapping support into our NerdDinner application, enabling users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>
> 
> <span data-ttu-id="737d3-108">如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。</span><span class="sxs-lookup"><span data-stu-id="737d3-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a><span data-ttu-id="737d3-109">神經晚餐第11步:集成AJAX地圖</span><span class="sxs-lookup"><span data-stu-id="737d3-109">NerdDinner Step 11: Integrating an AJAX Map</span></span>

<span data-ttu-id="737d3-110">現在,我們將通過集成 AJAX 映射支援,使我們的應用程式在視覺上更加精彩。</span><span class="sxs-lookup"><span data-stu-id="737d3-110">We'll now make our application a little more visually exciting by integrating AJAX mapping support.</span></span> <span data-ttu-id="737d3-111">這將使創建、編輯或查看晚餐的用戶能夠以圖形方式查看晚餐的位置。</span><span class="sxs-lookup"><span data-stu-id="737d3-111">This will enable users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>

### <a name="creating-a-map-partial-view"></a><span data-ttu-id="737d3-112">建立地圖部分檢視</span><span class="sxs-lookup"><span data-stu-id="737d3-112">Creating a Map Partial View</span></span>

<span data-ttu-id="737d3-113">我們將在應用程式中的幾個位置使用映射功能。</span><span class="sxs-lookup"><span data-stu-id="737d3-113">We are going to use mapping functionality in several places within our application.</span></span> <span data-ttu-id="737d3-114">為了保持我們的代碼 DRY,我們將將通用映射功能封裝在單個部分範本中,我們可以在多個控制器操作和視圖中重複使用。</span><span class="sxs-lookup"><span data-stu-id="737d3-114">To keep our code DRY we'll encapsulate the common map functionality within a single partial template that we can re-use across multiple controller actions and views.</span></span> <span data-ttu-id="737d3-115">我們將此部分檢視命名為"map.ascx",並在[Views_Dinners] 目錄中創建它。</span><span class="sxs-lookup"><span data-stu-id="737d3-115">We'll name this partial view "map.ascx" and create it within the \Views\Dinners directory.</span></span>

<span data-ttu-id="737d3-116">我們可以通過右鍵單擊「視圖\Dinners」目錄並選擇「添加視圖&gt;」功能表命令來創建 map.ascx 部分內容。</span><span class="sxs-lookup"><span data-stu-id="737d3-116">We can create the map.ascx partial by right-clicking on the \Views\Dinners directory and choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="737d3-117">我們將檢視命名為「Map.ascx」,將其作為部分檢視選中,並指示我們將通過一個強類型「Dinner」模型類:</span><span class="sxs-lookup"><span data-stu-id="737d3-117">We'll name the view "Map.ascx", check it as a partial view, and indicate that we are going to pass it a strongly-typed "Dinner" model class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

<span data-ttu-id="737d3-118">當我們按下「添加」按鈕時,將創建部分範本。</span><span class="sxs-lookup"><span data-stu-id="737d3-118">When we click the "Add" button our partial template will be created.</span></span> <span data-ttu-id="737d3-119">然後,我們將更新 Map.ascx 檔,以包含以下內容:</span><span class="sxs-lookup"><span data-stu-id="737d3-119">We'll then update the Map.ascx file to have the following content:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

<span data-ttu-id="737d3-120">第一&lt;個&gt;腳本引用指向 Microsoft 虛擬地球 6.2 映射庫。</span><span class="sxs-lookup"><span data-stu-id="737d3-120">The first &lt;script&gt; reference points to the Microsoft Virtual Earth 6.2 mapping library.</span></span> <span data-ttu-id="737d3-121">第二&lt;&gt;個 文稿引用指向我們即將創建的 map.js 檔,該檔將封裝我們常見的 Javascript 映射邏輯。</span><span class="sxs-lookup"><span data-stu-id="737d3-121">The second &lt;script&gt; reference points to a map.js file that we will shortly create which will encapsulate our common Javascript mapping logic.</span></span> <span data-ttu-id="737d3-122">div &lt;id="theMap"&gt;元素是虛擬地球將用來承載地圖的 HTML 容器。</span><span class="sxs-lookup"><span data-stu-id="737d3-122">The &lt;div id="theMap"&gt; element is the HTML container that Virtual Earth will use to host the map.</span></span>

<span data-ttu-id="737d3-123">然後,我們有一個&lt;嵌入&gt;式 腳本塊,其中包含特定於此視圖的兩個 JavaScript 函數。</span><span class="sxs-lookup"><span data-stu-id="737d3-123">We then have an embedded &lt;script&gt; block that contains two JavaScript functions specific to this view.</span></span> <span data-ttu-id="737d3-124">第一個函數使用 jQuery 來連接在頁面準備好運行用戶端文本時執行的函數。</span><span class="sxs-lookup"><span data-stu-id="737d3-124">The first function uses jQuery to wire-up a function that executes when the page is ready to run client-side script.</span></span> <span data-ttu-id="737d3-125">它調用 LoadMap() 説明器函數,我們將在 Map.js 文本檔中定義該函數以載入虛擬地球地圖控制項。</span><span class="sxs-lookup"><span data-stu-id="737d3-125">It calls a LoadMap() helper function that we'll define within our Map.js script file to load the virtual earth map control.</span></span> <span data-ttu-id="737d3-126">第二個函數是回調事件處理程式,該處理程式向標識位置的地圖添加引腳。</span><span class="sxs-lookup"><span data-stu-id="737d3-126">The second function is a callback event handler that adds a pin to the map that identifies a location.</span></span>

<span data-ttu-id="737d3-127">請注意,如何在用戶端腳本塊中使用伺服器端&lt;%+%&gt;塊來嵌入要映射到 JAVAScript 的 Dinner 的緯度和經度。</span><span class="sxs-lookup"><span data-stu-id="737d3-127">Notice how we are using a server-side &lt;%= %&gt; block within the client-side script block to embed the latitude and longitude of the Dinner we want to map into the JavaScript.</span></span> <span data-ttu-id="737d3-128">這是一種有用的技術來輸出用戶端文本可以使用的動態值(無需單獨的 AJAX 調用伺服器即可檢索值 , 使其更快)。</span><span class="sxs-lookup"><span data-stu-id="737d3-128">This is a useful technique to output dynamic values that can be used by client-side script (without requiring a separate AJAX call back to the server to retrieve the values – which makes it faster).</span></span> <span data-ttu-id="737d3-129">&lt;當檢視在伺服器上&gt;呈現時,%= % 塊將執行 ,因此 HTML 的輸出將最終使用嵌入的 JavaScript 值(例如:var 緯度 = 47.64312;)。</span><span class="sxs-lookup"><span data-stu-id="737d3-129">The &lt;%= %&gt; blocks will execute when the view is rendering on the server – and so the output of the HTML will just end up with embedded JavaScript values (for example: var latitude = 47.64312;).</span></span>

### <a name="creating-a-mapjs-utility-library"></a><span data-ttu-id="737d3-130">建立 Map.js 公用程式庫</span><span class="sxs-lookup"><span data-stu-id="737d3-130">Creating a Map.js utility library</span></span>

<span data-ttu-id="737d3-131">現在,讓我們創建 Map.js 檔,可用於封裝地圖的 JavaScript 功能(並實現上面的 LoadMap 和 LoadPin 方法)。</span><span class="sxs-lookup"><span data-stu-id="737d3-131">Let's now create the Map.js file that we can use to encapsulate the JavaScript functionality for our map (and implement the LoadMap and LoadPin methods above).</span></span> <span data-ttu-id="737d3-132">我們可以通過右鍵單擊專案中的 #Scripts 目錄來執行此操作,然後選擇「&gt;添加新 專案」功能表命令,選擇 JScript 項,並將其命名為"Map.js"。</span><span class="sxs-lookup"><span data-stu-id="737d3-132">We can do this by right-clicking on the \Scripts directory within our project, and then choose the "Add-&gt;New Item" menu command, select the JScript item, and name it "Map.js".</span></span>

<span data-ttu-id="737d3-133">下面是我們將添加到 Map.js 檔的 JavaScript 代碼,該代碼將與虛擬地球互動以顯示我們的地圖,並為其添加位置圖釘以進行晚餐:</span><span class="sxs-lookup"><span data-stu-id="737d3-133">Below is the JavaScript code we'll add to the Map.js file that will interact with Virtual Earth to display our map and add locations pins to it for our dinners:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a><span data-ttu-id="737d3-134">將地圖與建立及編輯表單整合</span><span class="sxs-lookup"><span data-stu-id="737d3-134">Integrating the Map with Create and Edit Forms</span></span>

<span data-ttu-id="737d3-135">現在,我們將 Map 支援與現有的創建和編輯方案集成。</span><span class="sxs-lookup"><span data-stu-id="737d3-135">We'll now integrate the Map support with our existing Create and Edit scenarios.</span></span> <span data-ttu-id="737d3-136">好消息是,這是很容易做到的,並且不需要我們更改任何控制器代碼。</span><span class="sxs-lookup"><span data-stu-id="737d3-136">The good news is that this is pretty easy to-do, and doesn't require us to change any of our Controller code.</span></span> <span data-ttu-id="737d3-137">由於我們的「創建」和「編輯」視圖共用一個通用的「DinnerForm」部分視圖來實現晚餐表單 UI,因此我們可以在一個位置添加地圖,並同時使用我們的「創建」 和「編輯」 方案。</span><span class="sxs-lookup"><span data-stu-id="737d3-137">Because our Create and Edit views share a common "DinnerForm" partial view to implement the dinner form UI, we can add the map in one place and have both our Create and Edit scenarios use it.</span></span>

<span data-ttu-id="737d3-138">我們只需要打開 [Views_Dinners_DinnerForm.ascx 部分視圖]並更新它,以包括我們的新地圖部分。</span><span class="sxs-lookup"><span data-stu-id="737d3-138">All we need to-do is to open the \Views\Dinners\DinnerForm.ascx partial view and update it to include our new map partial.</span></span> <span data-ttu-id="737d3-139">下面是添加地圖後更新的 DinnerForm 的外觀(注意:為了簡潔起見,下面代碼段省略了 HTML 表單元素):</span><span class="sxs-lookup"><span data-stu-id="737d3-139">Below is what the updated DinnerForm will look like once the map is added (note: the HTML form elements are omitted from the code snippet below for brevity):</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

<span data-ttu-id="737d3-140">上面的 DinnerForm 部分將類型為「DinnerFormViewModel」的物件作為其模型類型(因為它既需要 Dinner 物件,也需要 SelectList 來填充國家/地區的下拉清單)。</span><span class="sxs-lookup"><span data-stu-id="737d3-140">The DinnerForm partial above takes an object of type "DinnerFormViewModel" as its model type (because it needs both a Dinner object, as well as a SelectList to populate the dropdownlist of countries).</span></span> <span data-ttu-id="737d3-141">我們的地圖部分只需要一個類型「Dinner」的物件作為其模型類型,因此當我們渲染地圖部分時,我們只傳遞給 DinnerFormViewModel 的 Dinner 子屬性:</span><span class="sxs-lookup"><span data-stu-id="737d3-141">Our Map partial just needs an object of type "Dinner" as its model type, and so when we render the map partial we are passing just the Dinner sub-property of DinnerFormViewModel to it:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

<span data-ttu-id="737d3-142">我們添加到部分使用的 JavaScript 函數使用 jQuery 將「模糊」事件附加到「位址」HTML 文本框。</span><span class="sxs-lookup"><span data-stu-id="737d3-142">The JavaScript function we've added to the partial uses jQuery to attach a "blur" event to the "Address" HTML textbox.</span></span> <span data-ttu-id="737d3-143">您可能聽說過當使用者按下或選項卡進入文本框時觸發的「焦點」 事件。</span><span class="sxs-lookup"><span data-stu-id="737d3-143">You've probably heard of "focus" events that fire when a user clicks or tabs into a textbox.</span></span> <span data-ttu-id="737d3-144">相反,當使用者退出文本框時,將觸發"模糊"事件。</span><span class="sxs-lookup"><span data-stu-id="737d3-144">The opposite is a "blur" event that fires when a user exits a textbox.</span></span> <span data-ttu-id="737d3-145">上述事件處理程式在發生此情況時清除緯度和經度文本框值,然後繪製地圖上的新位址位置。</span><span class="sxs-lookup"><span data-stu-id="737d3-145">The above event handler clears the latitude and longitude textbox values when this happens, and then plots the new address location on our map.</span></span> <span data-ttu-id="737d3-146">然後,我們在 map.js 檔中定義的回調事件處理程式將使用虛擬地球返回的值更新窗體上的經度和緯度文本框,具體取決於我們提供的位址。</span><span class="sxs-lookup"><span data-stu-id="737d3-146">A callback event handler that we defined within the map.js file will then update the longitude and latitude textboxes on our form using values returned by virtual earth based on the address we gave it.</span></span>

<span data-ttu-id="737d3-147">現在,當我們再次運行我們的應用程式,然後單擊「主機晚餐」選項卡,我們將看到默認地圖顯示連同我們的標準晚餐表單元素:</span><span class="sxs-lookup"><span data-stu-id="737d3-147">And now when we run our application again and click the "Host Dinner" tab we'll see a default map displayed along with our standard Dinner form elements:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

<span data-ttu-id="737d3-148">當我們鍵入位址,然後選項卡離開時,地圖將動態更新以顯示位置,並且事件處理程式將用位置值填充緯度/經度文本框:</span><span class="sxs-lookup"><span data-stu-id="737d3-148">When we type in an address, and then tab away, the map will dynamically update to display the location, and our event handler will populate the latitude/longitude textboxes with the location values:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

<span data-ttu-id="737d3-149">如果我們保存新晚餐,然後再次打開它進行編輯,我們會發現在頁面載入時顯示地圖位置:</span><span class="sxs-lookup"><span data-stu-id="737d3-149">If we save the new dinner and then open it again for editing, we'll find that the map location is displayed when the page loads:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

<span data-ttu-id="737d3-150">每次更改位址欄位時,地圖和緯度/經度座標都將更新。</span><span class="sxs-lookup"><span data-stu-id="737d3-150">Every time the address field is changed, the map and the latitude/longitude coordinates will update.</span></span>

<span data-ttu-id="737d3-151">現在,地圖顯示「晚餐」位置,我們還可以將「緯度和經度」窗體欄位從可見文本框更改為隱藏元素(因為每次輸入位址時,地圖都會自動更新它們)。</span><span class="sxs-lookup"><span data-stu-id="737d3-151">Now that the map displays the Dinner location, we can also change the Latitude and Longitude form fields from being visible textboxes to instead be hidden elements (since the map is automatically updating them each time an address is entered).</span></span> <span data-ttu-id="737d3-152">此,我們將從使用 Html.TextBox() HTML 說明程式切換到使用 Html.Hidden() 說明器方法:</span><span class="sxs-lookup"><span data-stu-id="737d3-152">To-do this we'll switch from using the Html.TextBox() HTML helper to using the Html.Hidden() helper method:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

<span data-ttu-id="737d3-153">現在,我們的表單更加方便使用者,避免顯示原始緯度/經度(同時仍將其與資料庫中的每個晚餐一起存儲):</span><span class="sxs-lookup"><span data-stu-id="737d3-153">And now our forms are a little more user-friendly and avoid displaying the raw latitude/longitude (while still storing them with each Dinner in the database):</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a><span data-ttu-id="737d3-154">將地圖與詳細資訊檢視整合</span><span class="sxs-lookup"><span data-stu-id="737d3-154">Integrating the Map with the Details View</span></span>

<span data-ttu-id="737d3-155">現在,我們已經將地圖與我們的創建和編輯方案集成,讓我們也將其與我們的詳細資訊方案集成。</span><span class="sxs-lookup"><span data-stu-id="737d3-155">Now that we have the map integrated with our Create and Edit scenarios, let's also integrate it with our Details scenario.</span></span> <span data-ttu-id="737d3-156">我們只需要調用&lt;% Html.Render 部分("地圖");"&gt;詳細資訊"視圖中的百分比。</span><span class="sxs-lookup"><span data-stu-id="737d3-156">All we need to-do is to call &lt;% Html.RenderPartial("map"); %&gt; within the Details view.</span></span>

<span data-ttu-id="737d3-157">下面是完整詳細資訊檢視的原始碼(具有地圖整合)的外觀:</span><span class="sxs-lookup"><span data-stu-id="737d3-157">Below is what the source code to the complete Details view (with map integration) looks like:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

<span data-ttu-id="737d3-158">現在,當用戶導航到 /Dinners/細節/[id] URL 時,他們將看到有關晚餐的詳細資訊、地圖上的晚餐位置(隨滑鼠懸停在地圖上的圖釘顯示晚餐的標題和位址),併為其提供指向 RSVP 的 AJAX 連結:</span><span class="sxs-lookup"><span data-stu-id="737d3-158">And now when a user navigates to a /Dinners/Details/[id] URL they'll see details about the dinner, the location of the dinner on the map (complete with a push-pin that when hovered over displays the title of the dinner and the address of it), and have an AJAX link to RSVP for it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a><span data-ttu-id="737d3-159">在資料庫與儲存庫中實現位置搜尋</span><span class="sxs-lookup"><span data-stu-id="737d3-159">Implementing Location Search in our Database and Repository</span></span>

<span data-ttu-id="737d3-160">為了完成我們的AJAX實現,讓我們向應用程式的主頁添加一個地圖,允許使用者以圖形方式搜索附近的晚餐。</span><span class="sxs-lookup"><span data-stu-id="737d3-160">To finish off our AJAX implementation, let's add a Map to the home page of the application that allows users to graphically search for dinners near them.</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

<span data-ttu-id="737d3-161">我們將首先在資料庫和數據存儲庫層中實施支援,以高效地執行基於位置的 Dinner 半徑搜索。</span><span class="sxs-lookup"><span data-stu-id="737d3-161">We'll begin by implementing support within our database and data repository layer to efficiently perform a location-based radius search for Dinners.</span></span> <span data-ttu-id="737d3-162">我們可以使用 SQL [2008 的新地理空間功能](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx)來實現這一點,或者我們可以使用 Gary Dryden 在本文中討論的 SQL 函數方法:Rob [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) Conery 會在這裡寫關於使用 LINQ 到 SQL 的文章:[http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span><span class="sxs-lookup"><span data-stu-id="737d3-162">We could use the new [geospatial features of SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) to implement this, or alternatively we can use a SQL function approach that Gary Dryden discussed in article here: [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) and Rob Conery blogged about using with LINQ to SQL here: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span></span>

<span data-ttu-id="737d3-163">為了實現此技術,我們將在 Visual Studio 中打開「伺服器資源管理器」,選擇NerdDinner資料庫,然後右鍵單擊其下的「函數」子節點,然後選擇創建新的「Scalar 值函數」:</span><span class="sxs-lookup"><span data-stu-id="737d3-163">To implement this technique, we will open the "Server Explorer" within Visual Studio, select the NerdDinner database, and then right-click on the "functions" sub-node under it and choose to create a new "Scalar-valued function":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

<span data-ttu-id="737d3-164">然後,我們將粘貼到以下距離之間函數中:</span><span class="sxs-lookup"><span data-stu-id="737d3-164">We'll then paste in the following DistanceBetween function:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

<span data-ttu-id="737d3-165">然後,我們將在 SQL Server 中創建一個新的表值函數,我們稱之為「最近的晚餐」:</span><span class="sxs-lookup"><span data-stu-id="737d3-165">We'll then create a new table-valued function in SQL Server that we'll call "NearestDinners":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

<span data-ttu-id="737d3-166">此「最近的晚餐」表函數使用距離之間的幫助器功能返回我們提供它的自由經 100 英里內的所有晚餐:</span><span class="sxs-lookup"><span data-stu-id="737d3-166">This "NearestDinners" table function uses the DistanceBetween helper function to return all Dinners within 100 miles of the latitude and longitude we supply it:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

<span data-ttu-id="737d3-167">要呼叫此函數,我們將首先透過按兩下我們的#Model目錄中的NerdDinner.dbml檔向SQL設計器打開LINQ:</span><span class="sxs-lookup"><span data-stu-id="737d3-167">To call this function, we'll first open up the LINQ to SQL designer by double-clicking on the NerdDinner.dbml file within our \Models directory:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

<span data-ttu-id="737d3-168">然後,我們將最近 Dinner 和距離之間的函數拖動到 LINQ 到 SQL 設計器,這將導致它們作為 LINQ 上的方法添加到 SQL NerdDinnerDataContext 類:</span><span class="sxs-lookup"><span data-stu-id="737d3-168">We'll then drag the NearestDinners and DistanceBetween functions onto the LINQ to SQL designer, which will cause them to be added as methods on our LINQ to SQL NerdDinnerDataContext class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

<span data-ttu-id="737d3-169">然後,我們可以在我們的 DinnerRepository 類中公開「FindByLocation」查詢方法,該方法使用「最近 Dinner」功能返回即將在指定位置 100 英里範圍內的晚餐:</span><span class="sxs-lookup"><span data-stu-id="737d3-169">We can then expose a "FindByLocation" query method on our DinnerRepository class that uses the NearestDinner function to return upcoming Dinners that are within 100 miles of the specified location:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a><span data-ttu-id="737d3-170">實現基於JSON的AJAX搜尋操作方法</span><span class="sxs-lookup"><span data-stu-id="737d3-170">Implementing a JSON-based AJAX Search Action Method</span></span>

<span data-ttu-id="737d3-171">現在,我們將實現一個控制器操作方法,該方法利用新的 FindByLocation() 儲存庫方法返回可用於填充地圖的 Dinner 數據清單。</span><span class="sxs-lookup"><span data-stu-id="737d3-171">We'll now implement a controller action method that takes advantage of the new FindByLocation() repository method to return back a list of Dinner data that can be used to populate a map.</span></span> <span data-ttu-id="737d3-172">我們將讓此操作方法以 JSON(JavaScript 物件表示法)格式返回 Dinner 數據,以便可以輕鬆地在用戶端上使用 JAvaScript 對其進行操作。</span><span class="sxs-lookup"><span data-stu-id="737d3-172">We'll have this action method return back the Dinner data in a JSON (JavaScript Object Notation) format so that it can be easily manipulated using JavaScript on the client.</span></span>

<span data-ttu-id="737d3-173">為了實現這一點,我們將通過右鍵單擊 \控制器目錄並選擇"添加控制&gt;器 "功能表命令創建新的"SearchController"類。</span><span class="sxs-lookup"><span data-stu-id="737d3-173">To implement this, we'll create a new "SearchController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span> <span data-ttu-id="737d3-174">然後,我們將在新的 SearchController 類中實現「搜索ByLocation」操作方法,如下所示:</span><span class="sxs-lookup"><span data-stu-id="737d3-174">We'll then implement a "SearchByLocation" action method within the new SearchController class like below:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

<span data-ttu-id="737d3-175">SearchController 的 SearchByLocation 操作方法在內部調用晚餐存儲庫上的 FindByLocation 方法,以獲取有關附近晚餐的清單。</span><span class="sxs-lookup"><span data-stu-id="737d3-175">The SearchController's SearchByLocation action method internally calls the FindByLocation method on DinnerRepository to get a list of nearby dinners.</span></span> <span data-ttu-id="737d3-176">但是,它不是將 Dinner 物件直接返回給用戶端,而是返回 JsonDinner 物件。</span><span class="sxs-lookup"><span data-stu-id="737d3-176">Rather than return the Dinner objects directly to the client, though, it instead returns JsonDinner objects.</span></span> <span data-ttu-id="737d3-177">JsonDinner 類公開了 Dinner 屬性的子集(例如:出於安全原因,它不披露有 RSVP d 的晚餐人員的姓名)。</span><span class="sxs-lookup"><span data-stu-id="737d3-177">The JsonDinner class exposes a subset of Dinner properties (for example: for security reasons it doesn't disclose the names of the people who have RSVP'd for a dinner).</span></span> <span data-ttu-id="737d3-178">它還包括一個在晚餐上不存在的 RSVPCount 屬性,該屬性通過計算與特定晚餐關聯的 RSVP 物件數進行動態計算。</span><span class="sxs-lookup"><span data-stu-id="737d3-178">It also includes an RSVPCount property that doesn't exist on Dinner– and which is dynamically calculated by counting the number of RSVP objects associated with a particular dinner.</span></span>

<span data-ttu-id="737d3-179">然後,我們使用 Controller 基類上的 Json() 説明器方法使用基於 JSON 的線格式返回晚餐序列。</span><span class="sxs-lookup"><span data-stu-id="737d3-179">We are then using the Json() helper method on the Controller base class to return the sequence of dinners using a JSON-based wire format.</span></span> <span data-ttu-id="737d3-180">JSON 是一種標準文本格式,用於表示簡單的數據結構。</span><span class="sxs-lookup"><span data-stu-id="737d3-180">JSON is a standard text format for representing simple data-structures.</span></span> <span data-ttu-id="737d3-181">下面是從操作方法返回時由 JSON 格式為兩個 JsonDinner 物件的清單的範例:</span><span class="sxs-lookup"><span data-stu-id="737d3-181">Below is an example of what a JSON-formatted list of two JsonDinner objects looks like when returned from our action method:</span></span>

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a><span data-ttu-id="737d3-182">使用 jQuery 呼叫基於 JSON 的 AJAX 方法</span><span class="sxs-lookup"><span data-stu-id="737d3-182">Calling the JSON-based AJAX method using jQuery</span></span>

<span data-ttu-id="737d3-183">現在,我們準備更新NerdDinner應用程式的主頁,以使用搜索控制器的搜索ByLocation操作方法。</span><span class="sxs-lookup"><span data-stu-id="737d3-183">We are now ready to update the home page of the NerdDinner application to use the SearchController's SearchByLocation action method.</span></span> <span data-ttu-id="737d3-184">為此,我們將打開 /Views/Home/Index.aspx 檢視範本並更新該範本,使其具有文本框、搜索按鈕、地圖和名為 dinnerList 的&lt;&gt;div 元素:</span><span class="sxs-lookup"><span data-stu-id="737d3-184">To-do this, we'll open the /Views/Home/Index.aspx view template and update it to have a textbox, search button, our map, and a &lt;div&gt; element named dinnerList:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

<span data-ttu-id="737d3-185">然後,我們可以向頁面添加兩個 JavaScript 函數:</span><span class="sxs-lookup"><span data-stu-id="737d3-185">We can then add two JavaScript functions to the page:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

<span data-ttu-id="737d3-186">當頁面首次載入時,第一個 JavaScript 函數載入地圖。</span><span class="sxs-lookup"><span data-stu-id="737d3-186">The first JavaScript function loads the map when the page first loads.</span></span> <span data-ttu-id="737d3-187">第二個 JavaScript 函數在搜索按鈕上連接了 JavaScript 單擊事件處理程式。</span><span class="sxs-lookup"><span data-stu-id="737d3-187">The second JavaScript function wires up a JavaScript click event handler on the search button.</span></span> <span data-ttu-id="737d3-188">按下按鈕後,它將調用 FindDinnersGivenLocation() JavaScript 函數,我們將該函數添加到我們的 Map.js 檔中:</span><span class="sxs-lookup"><span data-stu-id="737d3-188">When the button is pressed it calls the FindDinnersGivenLocation() JavaScript function which we'll add to our Map.js file:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

<span data-ttu-id="737d3-189">此查找晚餐給定位置() 函數調用映射。在虛擬地球控制上查找()以將其居於輸入的位置。</span><span class="sxs-lookup"><span data-stu-id="737d3-189">This FindDinnersGivenLocation() function calls map.Find() on the Virtual Earth Control to center it on the entered location.</span></span> <span data-ttu-id="737d3-190">當虛擬地球地圖服務返回時,地圖。Find() 方法調用回調UpdateMapDinners回調方法,我們將其作為最後參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="737d3-190">When the virtual earth map service returns, the map.Find() method invokes the callbackUpdateMapDinners callback method we passed it as the final argument.</span></span>

<span data-ttu-id="737d3-191">回調UpdateMapDinners()方法是完成實際工作的地方。</span><span class="sxs-lookup"><span data-stu-id="737d3-191">The callbackUpdateMapDinners() method is where the real work is done.</span></span> <span data-ttu-id="737d3-192">它使用 jQuery 的 $.post() 説明器方法對我們的 SearchController 的 SearchByLocation() 操作方法執行 AJAX 調用 - 傳遞新居中地圖的緯度和經度。</span><span class="sxs-lookup"><span data-stu-id="737d3-192">It uses jQuery's $.post() helper method to perform an AJAX call to our SearchController's SearchByLocation() action method – passing it the latitude and longitude of the newly centered map.</span></span> <span data-ttu-id="737d3-193">它定義了一個內聯函數,將在 $.post() 説明器方法完成時調用,並且從 SearchByLocation() 操作方法返回的 JSON 格式的晚餐結果將使用名為"dinners"的變數傳遞它。</span><span class="sxs-lookup"><span data-stu-id="737d3-193">It defines an inline function that will be called when the $.post() helper method completes, and the JSON-formatted dinner results returned from the SearchByLocation() action method will be passed it using a variable called "dinners".</span></span> <span data-ttu-id="737d3-194">然後,它在每個返回的晚餐上做一個foron,並使用晚餐的緯度和經度和其他屬性在地圖上添加新的圖釘。</span><span class="sxs-lookup"><span data-stu-id="737d3-194">It then does a foreach over each returned dinner, and uses the dinner's latitude and longitude and other properties to add a new pin on the map.</span></span> <span data-ttu-id="737d3-195">它還在地圖右側的 HTML 晚餐清單中添加了一個晚餐條目。</span><span class="sxs-lookup"><span data-stu-id="737d3-195">It also adds a dinner entry to the HTML list of dinners to the right of the map.</span></span> <span data-ttu-id="737d3-196">然後,它會為圖釘和 HTML 清單啟用懸停事件,以便在使用者懸停在它們上時顯示有關晚餐的詳細資訊:</span><span class="sxs-lookup"><span data-stu-id="737d3-196">It then wires-up a hover event for both the pushpins and the HTML list so that details about the dinner are displayed when a user hovers over them:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

<span data-ttu-id="737d3-197">現在,當我們運行應用程式並訪問主頁時,我們將顯示一張地圖。</span><span class="sxs-lookup"><span data-stu-id="737d3-197">And now when we run the application and visit the home-page we'll be presented with a map.</span></span> <span data-ttu-id="737d3-198">當我們輸入城市名稱時,地圖將顯示附近即將舉辦的晚宴:</span><span class="sxs-lookup"><span data-stu-id="737d3-198">When we enter the name of a city the map will display the upcoming dinners near it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

<span data-ttu-id="737d3-199">懸停在晚餐上將顯示有關它的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="737d3-199">Hovering over a dinner will display details about it.</span></span>

<span data-ttu-id="737d3-200">按下氣泡中的晚餐標題或在 HTML 清單中的右側將引導我們前往晚宴 - 然後,我們可以選擇 RSVP 進行以下操作:</span><span class="sxs-lookup"><span data-stu-id="737d3-200">Clicking the Dinner title either in the bubble or on the right-hand side in the HTML list will navigate us to the dinner – which we can then optionally RSVP for:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a><span data-ttu-id="737d3-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="737d3-201">Next Step</span></span>

<span data-ttu-id="737d3-202">現在,我們已經實現了NerdDinner應用程式的所有應用程式功能。</span><span class="sxs-lookup"><span data-stu-id="737d3-202">We've now implemented all the application functionality of our NerdDinner application.</span></span> <span data-ttu-id="737d3-203">現在,讓我們來看看如何實現自動單元測試。</span><span class="sxs-lookup"><span data-stu-id="737d3-203">Let's now look at how we can enable automated unit testing of it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="737d3-204">[前一個](use-ajax-to-deliver-dynamic-updates.md)
> [下一個](enable-automated-unit-testing.md)</span><span class="sxs-lookup"><span data-stu-id="737d3-204">[Previous](use-ajax-to-deliver-dynamic-updates.md)
[Next](enable-automated-unit-testing.md)</span></span>
