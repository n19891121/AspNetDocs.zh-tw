---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: 建立自訂 AJAX 控制工具套件控制延伸器 (VB) |微軟文件
author: rick-anderson
description: 自訂擴充程式使您能夠自訂和擴展ASP.NET控件的功能,而無需創建新類。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: adce8e23ccf0a3364ee85534e98f8ea67ae4718d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543674"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a><span data-ttu-id="3202c-103">建立自訂的 AJAX Control Toolkit 控制項擴充項 (VB)</span><span class="sxs-lookup"><span data-stu-id="3202c-103">Creating a Custom AJAX Control Toolkit Control Extender (VB)</span></span>

<span data-ttu-id="3202c-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3202c-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="3202c-105">自訂擴充程式使您能夠自訂和擴展ASP.NET控件的功能,而無需創建新類。</span><span class="sxs-lookup"><span data-stu-id="3202c-105">Custom Extenders enable you to customize and extend the capabilities of ASP.NET controls without having to create new classes.</span></span>

<span data-ttu-id="3202c-106">在本教學中,您將瞭解如何創建自定義 AJAX 控制件工具套件控制元件延伸器。</span><span class="sxs-lookup"><span data-stu-id="3202c-106">In this tutorial, you learn how to create a custom AJAX Control Toolkit control extender.</span></span> <span data-ttu-id="3202c-107">我們創建一個簡單但有用的新擴展器,當您在 TextBox 中鍵入文本時,將按鈕的狀態從禁用更改為啟用。</span><span class="sxs-lookup"><span data-stu-id="3202c-107">We create a simple, but useful, new extender that changes the state of a Button from disabled to enabled when you type text into a TextBox.</span></span> <span data-ttu-id="3202c-108">閱讀本教程後,您將能夠使用自己的控制元件擴展器擴展ASP.NET AJAX 工具組。</span><span class="sxs-lookup"><span data-stu-id="3202c-108">After reading this tutorial, you will be able to extend the ASP.NET AJAX Toolkit with your own control extenders.</span></span>

<span data-ttu-id="3202c-109">您可以使用視覺化工作室或可視化 Web 開發人員建立自訂控制元件擴展器(請確保您具有最新版本的視覺化 Web 開發人員)。</span><span class="sxs-lookup"><span data-stu-id="3202c-109">You can create custom control extenders using either Visual Studio or Visual Web Developer (make sure that you have the latest version of Visual Web Developer).</span></span>

## <a name="overview-of-the-disabledbutton-extender"></a><span data-ttu-id="3202c-110">關閉按鈕延伸器概述</span><span class="sxs-lookup"><span data-stu-id="3202c-110">Overview of the DisabledButton Extender</span></span>

<span data-ttu-id="3202c-111">我們的新控制擴展器被命名為禁用按鈕擴展器。</span><span class="sxs-lookup"><span data-stu-id="3202c-111">Our new control extender is named the DisabledButton extender.</span></span> <span data-ttu-id="3202c-112">新增延伸器將有三個屬性:</span><span class="sxs-lookup"><span data-stu-id="3202c-112">This extender will have three properties:</span></span>

- <span data-ttu-id="3202c-113">目標控制ID - 控制元件擴展的文字框。</span><span class="sxs-lookup"><span data-stu-id="3202c-113">TargetControlID - The TextBox that the control extends.</span></span>
- <span data-ttu-id="3202c-114">目標ButtonIID - 已關閉或啟用的按鈕。</span><span class="sxs-lookup"><span data-stu-id="3202c-114">TargetButtonIID - The Button that is disabled or enabled.</span></span>
- <span data-ttu-id="3202c-115">關閉文字 - 最初顯示在按鈕中的文字。</span><span class="sxs-lookup"><span data-stu-id="3202c-115">DisabledText - The text that is initially displayed in the Button.</span></span> <span data-ttu-id="3202c-116">開始鍵入時,按鈕將顯示按鈕文本屬性的值。</span><span class="sxs-lookup"><span data-stu-id="3202c-116">When you start typing, the Button displays the value of the Button Text property.</span></span>

<span data-ttu-id="3202c-117">將「禁用按鈕擴展器」掛到文字框和按鈕控制件。</span><span class="sxs-lookup"><span data-stu-id="3202c-117">You hook the DisabledButton extender to a TextBox and Button control.</span></span> <span data-ttu-id="3202c-118">鍵入任何文字之前,將禁用「按鈕」,文本框和按鈕如下所示:</span><span class="sxs-lookup"><span data-stu-id="3202c-118">Before you type any text, the Button is disabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

<span data-ttu-id="3202c-119">([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="3202c-119">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))</span></span>

<span data-ttu-id="3202c-120">開始鍵入文字後,將啟用「按鈕」,文字框和按鈕如下所示:</span><span class="sxs-lookup"><span data-stu-id="3202c-120">After you start typing text, the Button is enabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

<span data-ttu-id="3202c-121">([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="3202c-121">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))</span></span>

<span data-ttu-id="3202c-122">要建立我們的控制器擴充器,我們需要建立以下三個檔案:</span><span class="sxs-lookup"><span data-stu-id="3202c-122">To create our control extender, we need to create the following three files:</span></span>

- <span data-ttu-id="3202c-123">關閉ButtonExtender.vb - 此檔案是伺服器端控制類,將管理建立擴充器,並允許您在設計時設定屬性。</span><span class="sxs-lookup"><span data-stu-id="3202c-123">DisabledButtonExtender.vb - This file is the server-side control class that will manage creating your extender and allow you to set the properties at design-time.</span></span> <span data-ttu-id="3202c-124">它還定義可以在擴展器上設置的屬性。</span><span class="sxs-lookup"><span data-stu-id="3202c-124">It also defines the properties that can be set on your extender.</span></span> <span data-ttu-id="3202c-125">這些屬性可透過代碼和設計時間存取,並匹配在禁用ButtonBehavior.js檔中定義的屬性。</span><span class="sxs-lookup"><span data-stu-id="3202c-125">These properties are accessible via code and at design time and match properties defined in the DisableButtonBehavior.js file.</span></span>
- <span data-ttu-id="3202c-126">關閉ButtonBehavior.js -- 此檔案是您將添加所有用戶端文本邏輯的位置。</span><span class="sxs-lookup"><span data-stu-id="3202c-126">DisabledButtonBehavior.js -- This file is where you will add all of your client script logic.</span></span>
- <span data-ttu-id="3202c-127">禁用ButtonDesigner.vb - 此類啟用設計時功能。</span><span class="sxs-lookup"><span data-stu-id="3202c-127">DisabledButtonDesigner.vb - This class enables design-time functionality.</span></span> <span data-ttu-id="3202c-128">如果希望控件擴展器與可視化工作室/可視化 Web 開發人員設計器正確工作,則需要此類。</span><span class="sxs-lookup"><span data-stu-id="3202c-128">You need this class if you want the control extender to work correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="3202c-129">因此,控制項裝置擴展器由伺服器端控制、用戶端行為和伺服器端設計器類組成。</span><span class="sxs-lookup"><span data-stu-id="3202c-129">So a control extender consists of a server-side control, a client-side behavior, and a server-side designer class.</span></span> <span data-ttu-id="3202c-130">您將在以下部分瞭解如何建立所有三個這些檔。</span><span class="sxs-lookup"><span data-stu-id="3202c-130">You learn how to create all three of these files in the following sections.</span></span>

## <a name="creating-the-custom-extender-website-and-project"></a><span data-ttu-id="3202c-131">建立自訂延伸器網站和專案</span><span class="sxs-lookup"><span data-stu-id="3202c-131">Creating the Custom Extender Website and Project</span></span>

<span data-ttu-id="3202c-132">第一步是在可視化工作室/可視化 Web 開發人員中創建類庫專案和網站。</span><span class="sxs-lookup"><span data-stu-id="3202c-132">The first step is to create a class library project and website in Visual Studio/Visual Web Developer.</span></span> <span data-ttu-id="3202c-133">我們將在類庫項目中創建自定義擴展器,並在網站中測試自定義擴展器。</span><span class="sxs-lookup"><span data-stu-id="3202c-133">We�ll create the custom extender in the class library project and test the custom extender in the website.</span></span>

<span data-ttu-id="3202c-134">讓我們從網站開始。</span><span class="sxs-lookup"><span data-stu-id="3202c-134">Let�s start with the website.</span></span> <span data-ttu-id="3202c-135">依以下步驟建立網站:</span><span class="sxs-lookup"><span data-stu-id="3202c-135">Follow these steps to create the website:</span></span>

1. <span data-ttu-id="3202c-136">選擇選單選項 **「檔案,新建網站**」。</span><span class="sxs-lookup"><span data-stu-id="3202c-136">Select the menu option **File, New Web Site**.</span></span>
2. <span data-ttu-id="3202c-137">選擇**ASP.NET 網站**樣本。</span><span class="sxs-lookup"><span data-stu-id="3202c-137">Select the **ASP.NET Web Site** template.</span></span>
3. <span data-ttu-id="3202c-138">命名新的*網站網站1。*</span><span class="sxs-lookup"><span data-stu-id="3202c-138">Name the new website *Website1*.</span></span>
4. <span data-ttu-id="3202c-139">按一下 [確定]\*\*\*\* 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3202c-139">Click the **OK** button.</span></span>

<span data-ttu-id="3202c-140">接下來,我們需要創建包含控制項擴展器代碼的類庫專案:</span><span class="sxs-lookup"><span data-stu-id="3202c-140">Next, we need to create the class library project that will contain the code for the control extender:</span></span>

1. <span data-ttu-id="3202c-141">選擇選單選項 **「檔、添加、新專案**」。</span><span class="sxs-lookup"><span data-stu-id="3202c-141">Select the menu option **File, Add, New Project**.</span></span>
2. <span data-ttu-id="3202c-142">選擇**類庫**範本。</span><span class="sxs-lookup"><span data-stu-id="3202c-142">Select the **Class Library** template.</span></span>
3. <span data-ttu-id="3202c-143">使用名稱 **「自訂擴充器**」為新類庫命名。</span><span class="sxs-lookup"><span data-stu-id="3202c-143">Name the new class library with the name **CustomExtenders**.</span></span>
4. <span data-ttu-id="3202c-144">按一下 [確定]\*\*\*\* 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3202c-144">Click the **OK** button.</span></span>

<span data-ttu-id="3202c-145">完成這些步驟後,解決方案資源管理器視窗應類似於圖 1。</span><span class="sxs-lookup"><span data-stu-id="3202c-145">After you complete these steps, your Solution Explorer window should look like Figure 1.</span></span>

<span data-ttu-id="3202c-146">[![網站和類別庫專案的解決方案](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="3202c-146">[![Solution with website and class library project](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="3202c-147">**圖01:** 包含網站和類別庫專案的解決方案([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="3202c-147">**Figure 01**: Solution with website and class library project([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))</span></span>

<span data-ttu-id="3202c-148">接下來,您需要向類庫專案添加所有必要的程式集引用:</span><span class="sxs-lookup"><span data-stu-id="3202c-148">Next, you need to add all of the necessary assembly references to the class library project:</span></span>

1. <span data-ttu-id="3202c-149">右鍵按下「自訂擴展器」專案並選擇功能表選項 **「新增參考**」 。</span><span class="sxs-lookup"><span data-stu-id="3202c-149">Right-click the CustomExtenders project and select the menu option **Add Reference**.</span></span>
2. <span data-ttu-id="3202c-150">選取 [.NET] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3202c-150">Select the .NET tab.</span></span>
3. <span data-ttu-id="3202c-151">加入下列組件的參考：</span><span class="sxs-lookup"><span data-stu-id="3202c-151">Add references to the following assemblies:</span></span>

    1. <span data-ttu-id="3202c-152">System.Web.dll</span><span class="sxs-lookup"><span data-stu-id="3202c-152">System.Web.dll</span></span>
    2. <span data-ttu-id="3202c-153">System.Web.Extensions.dll</span><span class="sxs-lookup"><span data-stu-id="3202c-153">System.Web.Extensions.dll</span></span>
    3. <span data-ttu-id="3202c-154">System.Design.dll</span><span class="sxs-lookup"><span data-stu-id="3202c-154">System.Design.dll</span></span>
    4. <span data-ttu-id="3202c-155">系統.Web.延伸.設計.dll</span><span class="sxs-lookup"><span data-stu-id="3202c-155">System.Web.Extensions.Design.dll</span></span>
4. <span data-ttu-id="3202c-156">選取 [瀏覽] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3202c-156">Select the Browse tab.</span></span>
5. <span data-ttu-id="3202c-157">添加對 AjaxControlToolkit.dll 程式集的引用。</span><span class="sxs-lookup"><span data-stu-id="3202c-157">Add a reference to the AjaxControlToolkit.dll assembly.</span></span> <span data-ttu-id="3202c-158">此程式集位於下載 AJAX 控制工具套件的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="3202c-158">This assembly is located in the folder where you downloaded the AJAX Control Toolkit.</span></span>

<span data-ttu-id="3202c-159">通過右鍵單擊項目、選擇"屬性"並按下"引用"選項卡,可以驗證是否添加了所有正確的引用(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="3202c-159">You can verify that you have added all of the right references by right-clicking your project, selecting Properties, and clicking the References tab (see Figure 2).</span></span>

<span data-ttu-id="3202c-160">[![具有所需參考的參考資料夾](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="3202c-160">[![References folder with required references](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)</span></span>

<span data-ttu-id="3202c-161">**圖 02**:參考需要參考的資料夾([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="3202c-161">**Figure 02**: References folder with required references([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png))</span></span>

## <a name="creating-the-custom-control-extender"></a><span data-ttu-id="3202c-162">建立自訂控制器</span><span class="sxs-lookup"><span data-stu-id="3202c-162">Creating the Custom Control Extender</span></span>

<span data-ttu-id="3202c-163">現在,我們已經有了類庫,我們可以開始構建擴展器控件。</span><span class="sxs-lookup"><span data-stu-id="3202c-163">Now that we have our class library, we can start building our extender control.</span></span> <span data-ttu-id="3202c-164">讓我們從自定義擴展器控件類的裸骨開始(參見清單 1)。</span><span class="sxs-lookup"><span data-stu-id="3202c-164">Let�s start with the bare bones of a custom extender control class (see Listing 1).</span></span>

<span data-ttu-id="3202c-165">**清單1 - 我的自訂延伸器.vb**</span><span class="sxs-lookup"><span data-stu-id="3202c-165">**Listing 1 - MyCustomExtender.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

<span data-ttu-id="3202c-166">關於清單1中的控件擴展器類,您注意到幾件事。</span><span class="sxs-lookup"><span data-stu-id="3202c-166">There are several things that you notice about the control extender class in Listing 1.</span></span> <span data-ttu-id="3202c-167">首先,請注意,類從基擴展器控制庫類繼承。</span><span class="sxs-lookup"><span data-stu-id="3202c-167">First, notice that the class inherits from the base ExtenderControlBase class.</span></span> <span data-ttu-id="3202c-168">所有 AJAX 控制工具套件擴展器控制項都源自此基類。</span><span class="sxs-lookup"><span data-stu-id="3202c-168">All AJAX Control Toolkit extender controls derive from this base class.</span></span> <span data-ttu-id="3202c-169">例如,基類包括作為每個控制元件擴展器的必需屬性的 TargetID 屬性。</span><span class="sxs-lookup"><span data-stu-id="3202c-169">For example, the base class includes the TargetID property that is a required property of every control extender.</span></span>

<span data-ttu-id="3202c-170">接下來,請注意,該類包含以下與用戶端腳本相關的兩個屬性:</span><span class="sxs-lookup"><span data-stu-id="3202c-170">Next, notice that the class includes the following two attributes related to client script:</span></span>

- <span data-ttu-id="3202c-171">Web 資源 - 使檔案作為嵌入資源包含在程式集中。</span><span class="sxs-lookup"><span data-stu-id="3202c-171">WebResource - Causes a file to be included as an embedded resource in an assembly.</span></span>
- <span data-ttu-id="3202c-172">用戶端文稿資源 - 導致從程式集檢索腳本資源。</span><span class="sxs-lookup"><span data-stu-id="3202c-172">ClientScriptResource - Causes a script resource to be retrieved from an assembly.</span></span>

<span data-ttu-id="3202c-173">WebResource 屬性用於在編譯自定義擴展器時將 MyControlBehavior.js JavaScript 檔嵌入到程式集中。</span><span class="sxs-lookup"><span data-stu-id="3202c-173">The WebResource attribute is used to embed the MyControlBehavior.js JavaScript file into the assembly when the custom extender is compiled.</span></span> <span data-ttu-id="3202c-174">當在網頁中使用自定義擴展器時,用戶端腳本資源屬性用於從程式集中檢索 MyControlBehavior.js 文稿。</span><span class="sxs-lookup"><span data-stu-id="3202c-174">The ClientScriptResource attribute is used to retrieve the MyControlBehavior.js script from the assembly when the custom extender is used in a web page.</span></span>

<span data-ttu-id="3202c-175">為了使 Web 資源和用戶端文本資源屬性正常工作,必須將 JavaScript 檔案編譯為嵌入式資源。</span><span class="sxs-lookup"><span data-stu-id="3202c-175">In order for the WebResource and ClientScriptResource attributes to work, you must compile the JavaScript file as an embedded resource.</span></span> <span data-ttu-id="3202c-176">在解決方案資源管理器視窗中選擇檔,打開屬性表,並將值 *「嵌入資源」* 分配給 **「生成操作」** 屬性。</span><span class="sxs-lookup"><span data-stu-id="3202c-176">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property.</span></span>

<span data-ttu-id="3202c-177">請注意,控制器還包括一個 TargetControlType 屬性。</span><span class="sxs-lookup"><span data-stu-id="3202c-177">Notice that the control extender also includes a TargetControlType attribute.</span></span> <span data-ttu-id="3202c-178">此屬性用於指定由控制器擴展器擴展的控制項類型。</span><span class="sxs-lookup"><span data-stu-id="3202c-178">This attribute is used to specify the type of control that is extended by the control extender.</span></span> <span data-ttu-id="3202c-179">在清單 1 中,控制器用於擴展 TextBox。</span><span class="sxs-lookup"><span data-stu-id="3202c-179">In the case of Listing 1, the control extender is used to extend a TextBox.</span></span>

<span data-ttu-id="3202c-180">最後,請注意,自定義擴展器包含名為 MyProperty 的屬性。</span><span class="sxs-lookup"><span data-stu-id="3202c-180">Finally, notice that the custom extender includes a property named MyProperty.</span></span> <span data-ttu-id="3202c-181">屬性使用擴展器控制屬性屬性進行標記。</span><span class="sxs-lookup"><span data-stu-id="3202c-181">The property is marked with the ExtenderControlProperty attribute.</span></span> <span data-ttu-id="3202c-182">GetPropertyValue() 和 SetPropertyValue() 方法用於將屬性值從伺服器端控制元件擴展器傳遞到客戶端行為。</span><span class="sxs-lookup"><span data-stu-id="3202c-182">The GetPropertyValue() and SetPropertyValue() methods are used to pass the property value from the server-side control extender to the client-side behavior.</span></span>

<span data-ttu-id="3202c-183">讓我們繼續實現我們的禁用按鈕擴展器的代碼。</span><span class="sxs-lookup"><span data-stu-id="3202c-183">Let�s go ahead and implement the code for our DisabledButton extender.</span></span> <span data-ttu-id="3202c-184">此擴展器的代碼可在清單 2 中找到。</span><span class="sxs-lookup"><span data-stu-id="3202c-184">The code for this extender can be found in Listing 2.</span></span>

<span data-ttu-id="3202c-185">**清單2 - 關閉按鈕延伸器.vb**</span><span class="sxs-lookup"><span data-stu-id="3202c-185">**Listing 2 - DisabledButtonExtender.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

<span data-ttu-id="3202c-186">清單2中的"禁用按鈕擴展器"具有兩個屬性,分別命名為TargetButtonID和"禁用文本"。</span><span class="sxs-lookup"><span data-stu-id="3202c-186">The DisabledButton extender in Listing 2 has two properties named TargetButtonID and DisabledText.</span></span> <span data-ttu-id="3202c-187">應用於 TargetButtonID 屬性的 IDReference 屬性可防止您將 Button 控制項 ID 以外的任何內容分配給此屬性。</span><span class="sxs-lookup"><span data-stu-id="3202c-187">The IDReferenceProperty applied to the TargetButtonID property prevents you from assigning anything other than the ID of a Button control to this property.</span></span>

<span data-ttu-id="3202c-188">WebResource 和 ClientScriptResource 屬性將位於名為"禁用ButtonBehavior.js"的檔案中的客戶端行為與此擴展器相關聯。</span><span class="sxs-lookup"><span data-stu-id="3202c-188">The WebResource and ClientScriptResource attributes associate a client-side behavior located in a file named DisabledButtonBehavior.js with this extender.</span></span> <span data-ttu-id="3202c-189">我們將在下一節中討論此 JavaScript 檔。</span><span class="sxs-lookup"><span data-stu-id="3202c-189">We discuss this JavaScript file in the next section.</span></span>

## <a name="creating-the-custom-extender-behavior"></a><span data-ttu-id="3202c-190">建立自訂延伸程式行為</span><span class="sxs-lookup"><span data-stu-id="3202c-190">Creating the Custom Extender Behavior</span></span>

<span data-ttu-id="3202c-191">控件擴展器的用戶端元件稱為行為。</span><span class="sxs-lookup"><span data-stu-id="3202c-191">The client-side component of a control extender is called a behavior.</span></span> <span data-ttu-id="3202c-192">關閉和啟用按鈕的實際邏輯包含在"禁用按鈕"行為中。</span><span class="sxs-lookup"><span data-stu-id="3202c-192">The actual logic for disabling and enabling the Button is contained in the DisabledButton behavior.</span></span> <span data-ttu-id="3202c-193">該行為的 JavaScript 代碼包含在清單 3 中。</span><span class="sxs-lookup"><span data-stu-id="3202c-193">The JavaScript code for the behavior is included in Listing 3.</span></span>

<span data-ttu-id="3202c-194">**清單 3 - 停用Button.js**</span><span class="sxs-lookup"><span data-stu-id="3202c-194">**Listing 3 - DisabledButton.js**</span></span>

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

<span data-ttu-id="3202c-195">清單3中的 JavaScript 檔包含名為"禁用Button行為"的用戶端類。</span><span class="sxs-lookup"><span data-stu-id="3202c-195">The JavaScript file in Listing 3 contains a client-side class named DisabledButtonBehavior.</span></span> <span data-ttu-id="3202c-196">此類,與其伺服器端孿生一樣,包括名為 TargetButtonID 和禁用文本的兩個屬性,您\_可以使用 GetTargetButtonID/設置\_TargetButtonID\_進行訪問,並獲得\_禁用文本/集 禁用文本。</span><span class="sxs-lookup"><span data-stu-id="3202c-196">This class, like its server-side twin, includes two properties named TargetButtonID and DisabledText which you can access using get\_TargetButtonID/set\_TargetButtonID and get\_DisabledText/set\_DisabledText.</span></span>

<span data-ttu-id="3202c-197">初始化() 方法將鍵up事件處理程式與行為的目標元素關聯。</span><span class="sxs-lookup"><span data-stu-id="3202c-197">The initialize() method associates a keyup event handler with the target element for the behavior.</span></span> <span data-ttu-id="3202c-198">每次在與此行為關聯的 TextBox 中鍵入字母時,鍵 up 處理程序都會執行。</span><span class="sxs-lookup"><span data-stu-id="3202c-198">Each time you type a letter into the TextBox associated with this behavior, the keyup handler executes.</span></span> <span data-ttu-id="3202c-199">鍵up 處理程式啟用或禁用按鈕,具體取決於與該行為關聯的 TextBox 是否包含任何文本。</span><span class="sxs-lookup"><span data-stu-id="3202c-199">The keyup handler either enables or disables the Button depending on whether the TextBox associated with the behavior contains any text.</span></span>

<span data-ttu-id="3202c-200">請記住,您必須將清單 3 中的 JavaScript 檔編譯為嵌入式資源。</span><span class="sxs-lookup"><span data-stu-id="3202c-200">Remember that you must compile the JavaScript file in Listing 3 as an embedded resource.</span></span> <span data-ttu-id="3202c-201">在解決方案資源管理器視窗中選擇檔,打開屬性表,並將值 *「嵌入資源」* 分配給**生成操作**屬性(參見圖 3)。</span><span class="sxs-lookup"><span data-stu-id="3202c-201">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property (see Figure 3).</span></span> <span data-ttu-id="3202c-202">此選項在可視化工作室和可視化 Web 開發人員中都可用。</span><span class="sxs-lookup"><span data-stu-id="3202c-202">This option is available in both Visual Studio and Visual Web Developer.</span></span>

<span data-ttu-id="3202c-203">[![將 JavaScript 檔案加入為嵌入式資源](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="3202c-203">[![Adding a JavaScript file as an embedded resource](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)</span></span>

<span data-ttu-id="3202c-204">**圖 03**: 將 JavaScript 檔案加入為嵌入式資源([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="3202c-204">**Figure 03**: Adding a JavaScript file as an embedded resource([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))</span></span>

## <a name="creating-the-custom-extender-designer"></a><span data-ttu-id="3202c-205">建立自訂延伸程式設計器</span><span class="sxs-lookup"><span data-stu-id="3202c-205">Creating the Custom Extender Designer</span></span>

<span data-ttu-id="3202c-206">我們需要創建最後一個類來完成擴展器。</span><span class="sxs-lookup"><span data-stu-id="3202c-206">There is one last class that we need to create to complete our extender.</span></span> <span data-ttu-id="3202c-207">我們需要在清單4中創建設計器類。</span><span class="sxs-lookup"><span data-stu-id="3202c-207">We need to create the designer class in Listing 4.</span></span> <span data-ttu-id="3202c-208">此類是使擴展器在可視化工作室/可視化 Web 開發人員設計器中正確運行所必需的。</span><span class="sxs-lookup"><span data-stu-id="3202c-208">This class is required to make the extender behave correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="3202c-209">**清單4 - 關閉按鈕設計器.vb**</span><span class="sxs-lookup"><span data-stu-id="3202c-209">**Listing 4 - DisabledButtonDesigner.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

<span data-ttu-id="3202c-210">將清單 4 中的設計器與「已禁用Button擴展器」與「設計器」屬性相關聯。您需要將 Designer 屬性應用於禁用Button擴展器類,如下所示:</span><span class="sxs-lookup"><span data-stu-id="3202c-210">You associate the designer in Listing 4 with the DisabledButton extender with the Designer attribute.You need to apply the Designer attribute to the DisabledButtonExtender class like this:</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a><span data-ttu-id="3202c-211">使用自訂延伸器</span><span class="sxs-lookup"><span data-stu-id="3202c-211">Using the Custom Extender</span></span>

<span data-ttu-id="3202c-212">現在,我們已經完成了創建禁用按鈕控件擴展器,是時候在我們的ASP.NET網站使用它了。</span><span class="sxs-lookup"><span data-stu-id="3202c-212">Now that we have finished creating the DisabledButton control extender, it is time to use it in our ASP.NET website.</span></span> <span data-ttu-id="3202c-213">首先,我們需要將自定義擴展器添加到工具箱中。</span><span class="sxs-lookup"><span data-stu-id="3202c-213">First, we need to add the custom extender to the toolbox.</span></span> <span data-ttu-id="3202c-214">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3202c-214">Follow these steps:</span></span>

1. <span data-ttu-id="3202c-215">通過按兩下解決方案資源管理器視窗中的頁面打開ASP.NET頁。</span><span class="sxs-lookup"><span data-stu-id="3202c-215">Open an ASP.NET page by double-clicking the page in the Solution Explorer window.</span></span>
2. <span data-ttu-id="3202c-216">右鍵按一下工具箱並選擇選單選項 **「選擇專案**」。</span><span class="sxs-lookup"><span data-stu-id="3202c-216">Right-click the toolbox and select the menu option **Choose Items**.</span></span>
3. <span data-ttu-id="3202c-217">在「選擇工具箱項目」對話框中,流覽到「自訂擴展器.dll」程式集。</span><span class="sxs-lookup"><span data-stu-id="3202c-217">In the Choose Toolbox Items dialog, browse to the CustomExtenders.dll assembly.</span></span>
4. <span data-ttu-id="3202c-218">按下「**確定」** 按鈕關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3202c-218">Click the **OK** button to close the dialog.</span></span>

<span data-ttu-id="3202c-219">完成這些步驟後,禁用 Button 控件擴展器應顯示在工具箱中(參見圖 4)。</span><span class="sxs-lookup"><span data-stu-id="3202c-219">After you complete these steps, the DisabledButton control extender should appear in the toolbox (see Figure 4).</span></span>

<span data-ttu-id="3202c-220">[![工具箱中的關閉按鈕](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="3202c-220">[![DisabledButton in the toolbox](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)</span></span>

<span data-ttu-id="3202c-221">**圖 04**: 工具殼中的關閉按鈕([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="3202c-221">**Figure 04**: DisabledButton in the toolbox([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png))</span></span>

<span data-ttu-id="3202c-222">接下來,我們需要創建一個新的ASP.NET頁。</span><span class="sxs-lookup"><span data-stu-id="3202c-222">Next, we need to create a new ASP.NET page.</span></span> <span data-ttu-id="3202c-223">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3202c-223">Follow these steps:</span></span>

1. <span data-ttu-id="3202c-224">創建新ASP.NET頁面名為"顯示禁用按鈕.aspx"。</span><span class="sxs-lookup"><span data-stu-id="3202c-224">Create a new ASP.NET page named ShowDisabledButton.aspx.</span></span>
2. <span data-ttu-id="3202c-225">將腳本管理器拖到頁面上。</span><span class="sxs-lookup"><span data-stu-id="3202c-225">Drag a ScriptManager onto the page.</span></span>
3. <span data-ttu-id="3202c-226">將文字框控件拖到頁面上。</span><span class="sxs-lookup"><span data-stu-id="3202c-226">Drag a TextBox control onto the page.</span></span>
4. <span data-ttu-id="3202c-227">將「按鈕」控制器拖到頁面上。</span><span class="sxs-lookup"><span data-stu-id="3202c-227">Drag a Button control onto the page.</span></span>
5. <span data-ttu-id="3202c-228">在"屬性"視窗中,將按鈕ID屬性更改為值<em>btnSave,</em>將文本屬性更改為*\*值"儲存*"。</span><span class="sxs-lookup"><span data-stu-id="3202c-228">In the Properties window, change the Button ID property to the value <em>btnSave</em> and the Text property to the value *Save\**.</span></span>

<span data-ttu-id="3202c-229">我們創建了一個包含標準ASP.NET文本框和按鈕控制項的頁面。</span><span class="sxs-lookup"><span data-stu-id="3202c-229">We created a page with a standard ASP.NET TextBox and Button control.</span></span>

<span data-ttu-id="3202c-230">接下來,我們需要使用關閉按鈕延伸器延伸 TextBox 控制件:</span><span class="sxs-lookup"><span data-stu-id="3202c-230">Next, we need to extend the TextBox control with the DisabledButton extender:</span></span>

1. <span data-ttu-id="3202c-231">選擇 **「新增延伸器**」工作選項以開啟延伸程式精靈對話框(參見圖 5)。</span><span class="sxs-lookup"><span data-stu-id="3202c-231">Select the **Add Extender** task option to open the Extender Wizard dialog (see Figure 5).</span></span> <span data-ttu-id="3202c-232">請注意,該對話框包括我們的自定義禁用按鈕擴展器。</span><span class="sxs-lookup"><span data-stu-id="3202c-232">Notice that the dialog includes our custom DisabledButton extender.</span></span>
2. <span data-ttu-id="3202c-233">選擇"停用按鈕擴展器",然後按下 **「確定**」按鈕。</span><span class="sxs-lookup"><span data-stu-id="3202c-233">Select the DisabledButton extender and click the **OK** button.</span></span>

<span data-ttu-id="3202c-234">[![擴充器精靈對話框](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="3202c-234">[![The Extender Wizard dialog](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)</span></span>

<span data-ttu-id="3202c-235">**圖 05**: 擴充器精靈對話框([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="3202c-235">**Figure 05**: The Extender Wizard dialog([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))</span></span>

<span data-ttu-id="3202c-236">最後,我們可以設置禁用按鈕擴展器的屬性。</span><span class="sxs-lookup"><span data-stu-id="3202c-236">Finally, we can set the properties of the DisabledButton extender.</span></span> <span data-ttu-id="3202c-237">您可以透過修改 TextBox 控制檔屬性來變更關閉Button延伸器的屬性:</span><span class="sxs-lookup"><span data-stu-id="3202c-237">You can modify the properties of the DisabledButton extender by modifying the properties of the TextBox control:</span></span>

1. <span data-ttu-id="3202c-238">選擇設計器中的文字框。</span><span class="sxs-lookup"><span data-stu-id="3202c-238">Select the TextBox in the Designer.</span></span>
2. <span data-ttu-id="3202c-239">在"屬性"視窗中,展開擴展器節點(參見圖 6)。</span><span class="sxs-lookup"><span data-stu-id="3202c-239">In the Properties window, expand the Extenders node (see Figure 6).</span></span>
3. <span data-ttu-id="3202c-240">將「*儲存到*關閉文字」 屬性的值和值*btnSave*分配給 TargetButtonID 屬性。</span><span class="sxs-lookup"><span data-stu-id="3202c-240">Assign the value *Save* to the DisabledText property and the value *btnSave* to the TargetButtonID property.</span></span>

<span data-ttu-id="3202c-241">[![設定延伸器屬性](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="3202c-241">[![Setting extender properties](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)</span></span>

<span data-ttu-id="3202c-242">**圖 06**:設定延伸器屬性([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="3202c-242">**Figure 06**: Setting extender properties([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))</span></span>

<span data-ttu-id="3202c-243">當您運行頁面(通過點擊 F5)時,按鈕控制項最初被禁用。</span><span class="sxs-lookup"><span data-stu-id="3202c-243">When you run the page (by hitting F5), the Button control is initially disabled.</span></span> <span data-ttu-id="3202c-244">一旦您開始將文字輸入到 TextBox 中,按鈕控制件即啟用(參見圖 7)。</span><span class="sxs-lookup"><span data-stu-id="3202c-244">As soon as you start entering text into the TextBox, the Button control is enabled (see Figure 7).</span></span>

<span data-ttu-id="3202c-245">[![關閉按鈕延伸器正在操作中](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="3202c-245">[![The DisabledButton extender in action](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)</span></span>

<span data-ttu-id="3202c-246">**圖 07**: 關閉按鈕延伸器在操作中([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="3202c-246">**Figure 07**: The DisabledButton extender in action([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))</span></span>

## <a name="summary"></a><span data-ttu-id="3202c-247">總結</span><span class="sxs-lookup"><span data-stu-id="3202c-247">Summary</span></span>

<span data-ttu-id="3202c-248">本教學的目的是說明如何使用自定義擴展器控制項擴展 AJAX 控制項工具組。</span><span class="sxs-lookup"><span data-stu-id="3202c-248">The goal of this tutorial was to explain how you can extend the AJAX Control Toolkit with custom extender controls.</span></span> <span data-ttu-id="3202c-249">在本教學中,我們創建了一個簡單的禁用按鈕控制元件擴展器。</span><span class="sxs-lookup"><span data-stu-id="3202c-249">In this tutorial, we created a simple DisabledButton control extender.</span></span> <span data-ttu-id="3202c-250">我們通過創建禁用Button擴展器類、禁用Button行為 JavaScript 行為和禁用ButtonDesigner類實現了此擴展程式。</span><span class="sxs-lookup"><span data-stu-id="3202c-250">We implemented this extender by creating a DisabledButtonExtender class, a DisabledButtonBehavior JavaScript behavior, and a DisabledButtonDesigner class.</span></span> <span data-ttu-id="3202c-251">每當創建自定義控制器時,都會遵循一組類似的步驟。</span><span class="sxs-lookup"><span data-stu-id="3202c-251">You follow a similar set of steps whenever you create a custom control extender.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3202c-252">上一步</span><span class="sxs-lookup"><span data-stu-id="3202c-252">Previous</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
