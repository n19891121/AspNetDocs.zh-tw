---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: 使用檢視母版頁 (C#) 建立頁面佈局 |微軟文件
author: rick-anderson
description: 在本教學中,您將瞭解如何利用檢視母版頁為應用程式中的多個頁面創建通用頁面佈局。 您可以使用...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: d313e017d7061ae03e8dea79e611d0cf3838297d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542517"
---
# <a name="creating-page-layouts-with-view-master-pages-c"></a><span data-ttu-id="65a8f-104">使用檢視主版頁面建立頁面配置 (C#)</span><span class="sxs-lookup"><span data-stu-id="65a8f-104">Creating Page Layouts with View Master Pages (C#)</span></span>

<span data-ttu-id="65a8f-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="65a8f-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="65a8f-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="65a8f-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> <span data-ttu-id="65a8f-107">在本教學中,您將瞭解如何利用檢視母版頁為應用程式中的多個頁面創建通用頁面佈局。</span><span class="sxs-lookup"><span data-stu-id="65a8f-107">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="65a8f-108">例如,可以使用檢視母版頁定義兩列頁面佈局,並為 Web 應用程式中的所有頁面使用兩列佈局。</span><span class="sxs-lookup"><span data-stu-id="65a8f-108">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

## <a name="creating-page-layouts-with-view-master-pages"></a><span data-ttu-id="65a8f-109">使用檢視母版頁建立頁面配置</span><span class="sxs-lookup"><span data-stu-id="65a8f-109">Creating Page Layouts with View Master Pages</span></span>

<span data-ttu-id="65a8f-110">在本教學中,您將瞭解如何利用檢視母版頁為應用程式中的多個頁面創建通用頁面佈局。</span><span class="sxs-lookup"><span data-stu-id="65a8f-110">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="65a8f-111">例如,可以使用檢視母版頁定義兩列頁面佈局,並為 Web 應用程式中的所有頁面使用兩列佈局。</span><span class="sxs-lookup"><span data-stu-id="65a8f-111">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

<span data-ttu-id="65a8f-112">您還可以利用查看母版頁在應用程式中多個頁面之間共用常見內容。</span><span class="sxs-lookup"><span data-stu-id="65a8f-112">You also can take advantage of view master pages to share common content across multiple pages in your application.</span></span> <span data-ttu-id="65a8f-113">例如,您可以將網站徽標、導航鏈接和橫幅廣告放在視圖母版頁中。</span><span class="sxs-lookup"><span data-stu-id="65a8f-113">For example, you can place your website logo, navigation links, and banner advertisements in a view master page.</span></span> <span data-ttu-id="65a8f-114">這樣,應用程式中的每個頁面都會自動顯示此內容。</span><span class="sxs-lookup"><span data-stu-id="65a8f-114">That way, every page in your application would display this content automatically.</span></span>

<span data-ttu-id="65a8f-115">在本教學中,您將瞭解如何創建新的檢視母版頁,並根據母版頁創建新的檢視內容頁。</span><span class="sxs-lookup"><span data-stu-id="65a8f-115">In this tutorial, you learn how to create a new view master page and create a new view content page based on the master page.</span></span>

### <a name="creating-a-view-master-page"></a><span data-ttu-id="65a8f-116">建立檢視母版頁</span><span class="sxs-lookup"><span data-stu-id="65a8f-116">Creating a View Master Page</span></span>

<span data-ttu-id="65a8f-117">讓我們首先創建定義兩列佈局的檢視母版頁。</span><span class="sxs-lookup"><span data-stu-id="65a8f-117">Let's start by creating a view master page that defines a two-column layout.</span></span> <span data-ttu-id="65a8f-118">通過右鍵按下「檢視+共用」資料夾、選擇功能表選項 **「新增、新建專案**」以及選擇**MVC 檢視母版頁**樣本(參見圖 1),將新的檢視母版頁添加到 MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="65a8f-118">You add a new view master page to an MVC project by right-clicking the Views\Shared folder, selecting the menu option **Add, New Item**, and selecting the **MVC View Master Page** template (see Figure 1).</span></span>

<span data-ttu-id="65a8f-119">[![新增檢視母版頁](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="65a8f-119">[![Adding a view master page](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span></span>

<span data-ttu-id="65a8f-120">**圖 01**: 新增檢視母版頁 ([按下以檢視全尺寸影像](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="65a8f-120">**Figure 01**: Adding a view master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span></span>

<span data-ttu-id="65a8f-121">您可以在應用程式中創建多個檢視母版頁。</span><span class="sxs-lookup"><span data-stu-id="65a8f-121">You can create more than one view master page in an application.</span></span> <span data-ttu-id="65a8f-122">每個檢視母版頁可以定義不同的頁面佈局。</span><span class="sxs-lookup"><span data-stu-id="65a8f-122">Each view master page can define a different page layout.</span></span> <span data-ttu-id="65a8f-123">例如,您可能希望某些頁面具有兩列佈局和其他頁面具有三列佈局。</span><span class="sxs-lookup"><span data-stu-id="65a8f-123">For example, you might want certain pages to have a two-column layout and other pages to have a three-column layout.</span></span>

<span data-ttu-id="65a8f-124">檢視母版頁看起來非常類似於標準ASP.NET MVC 檢視。</span><span class="sxs-lookup"><span data-stu-id="65a8f-124">A view master page looks very much like a standard ASP.NET MVC view.</span></span> <span data-ttu-id="65a8f-125">但是,與普通視圖不同,視圖母版頁包含一個或多個`<asp:ContentPlaceHolder>`標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-125">However, unlike a normal view, a view master page contains one or more `<asp:ContentPlaceHolder>` tags.</span></span> <span data-ttu-id="65a8f-126">這些`<contentplaceholder>`標記用於標記可在單個內容頁中重寫的母版頁區域。</span><span class="sxs-lookup"><span data-stu-id="65a8f-126">The `<contentplaceholder>` tags are used to mark the areas of the master page that can be overridden in an individual content page.</span></span>

<span data-ttu-id="65a8f-127">例如,清單 1 中的檢視母版頁定義兩列佈局。</span><span class="sxs-lookup"><span data-stu-id="65a8f-127">For example, the view master page in Listing 1 defines a two-column layout.</span></span> <span data-ttu-id="65a8f-128">它包含兩`<contentplaceholder>`個標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-128">It contains two `<contentplaceholder>` tags.</span></span> <span data-ttu-id="65a8f-129">每`<ContentPlaceHolder>`列一列。</span><span class="sxs-lookup"><span data-stu-id="65a8f-129">One `<ContentPlaceHolder>` for each column.</span></span>

<span data-ttu-id="65a8f-130">**清單1 |`Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="65a8f-130">**Listing 1 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

<span data-ttu-id="65a8f-131">清單1中的檢視母版頁的正文包含兩`<div>`個對應於兩列的標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-131">The body of the view master page in Listing 1 contains two `<div>` tags that correspond to the two columns.</span></span> <span data-ttu-id="65a8f-132">"級聯樣式表"列類應用於這兩個`<div>`標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-132">The Cascading Style Sheet column class is applied to both `<div>` tags.</span></span> <span data-ttu-id="65a8f-133">此類在母版頁頂部聲明的樣式表中定義。</span><span class="sxs-lookup"><span data-stu-id="65a8f-133">This class is defined in the style sheet declared at the top of the master page.</span></span> <span data-ttu-id="65a8f-134">您可以通過切換到"設計"視圖來預覽視圖母版頁的呈現方式。</span><span class="sxs-lookup"><span data-stu-id="65a8f-134">You can preview how the view master page will be rendered by switching to Design view.</span></span> <span data-ttu-id="65a8f-135">按一下原始碼編輯器左下角的「設計」選項卡(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="65a8f-135">Click the Design tab at the bottom-left of the source code editor (see Figure 2).</span></span>

<span data-ttu-id="65a8f-136">[![在設計器中預覽母版頁](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="65a8f-136">[![Previewing a master page in the designer](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span></span>

<span data-ttu-id="65a8f-137">**圖 02**: 預覽設計器中的母版頁 ([按下以檢視全尺寸影像](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="65a8f-137">**Figure 02**: Previewing a master page in the designer ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span></span>

### <a name="creating-a-view-content-page"></a><span data-ttu-id="65a8f-138">建立檢視內容頁面</span><span class="sxs-lookup"><span data-stu-id="65a8f-138">Creating a View Content Page</span></span>

<span data-ttu-id="65a8f-139">創建檢視母版頁後,可以基於檢視母版頁創建一個或多個視圖內容頁。</span><span class="sxs-lookup"><span data-stu-id="65a8f-139">After you create a view master page, you can create one or more view content pages based on the view master page.</span></span> <span data-ttu-id="65a8f-140">例如,您可以通過右鍵單擊「檢視+主頁」資料夾、選擇 **「新增、新建專案」、** 選擇**MVC 查看內容頁**樣本、輸入名稱 Index.aspx 以及單擊 **「新增**」按鈕(參見圖 3)為主控制器建立索引視圖內容頁。</span><span class="sxs-lookup"><span data-stu-id="65a8f-140">For example, you can create an Index view content page for the Home controller by right-clicking the Views\Home folder, selecting **Add, New Item**, selecting the **MVC View Content Page** template, entering the name Index.aspx, and clicking the **Add** button (see Figure 3).</span></span>

<span data-ttu-id="65a8f-141">[![新增檢視內容頁](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="65a8f-141">[![Adding a view content page](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span></span>

<span data-ttu-id="65a8f-142">**圖 03**: 新增檢視內容頁 ([按下以檢視全尺寸影像](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="65a8f-142">**Figure 03**: Adding a view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span></span>

<span data-ttu-id="65a8f-143">按下「添加」按鈕後,將出現一個新對話框,使您能夠選擇視圖母版頁以與檢視內容頁關聯(參見圖 4)。</span><span class="sxs-lookup"><span data-stu-id="65a8f-143">After you click the Add button, a new dialog appears that enables you to select a view master page to associate with the view content page (see Figure 4).</span></span> <span data-ttu-id="65a8f-144">您可以導航到我們在上一節中創建的 Site.master 檢視母版頁。</span><span class="sxs-lookup"><span data-stu-id="65a8f-144">You can navigate to the Site.master view master page that we created in the previous section.</span></span>

<span data-ttu-id="65a8f-145">[![選擇母版頁](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="65a8f-145">[![Selecting a master page](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span></span>

<span data-ttu-id="65a8f-146">**圖 04**: 選擇母版頁 ([按下以檢視全尺寸影像](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="65a8f-146">**Figure 04**: Selecting a master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span></span>

<span data-ttu-id="65a8f-147">基於 Site.master 母版頁建立新的檢視內容頁後,您將在清單 2 中獲取該檔。</span><span class="sxs-lookup"><span data-stu-id="65a8f-147">After you create a new view content page based on the Site.master master page, you get the file in Listing 2.</span></span>

<span data-ttu-id="65a8f-148">**清單2 |`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="65a8f-148">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

<span data-ttu-id="65a8f-149">請注意,此檢視包含一個`<asp:Content>`對應於視圖母版頁中每個`<asp:ContentPlaceHolder>`標記的標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-149">Notice that this view contains a `<asp:Content>` tag that corresponds to each of the `<asp:ContentPlaceHolder>` tags in the view master page.</span></span> <span data-ttu-id="65a8f-150">每個`<asp:Content>`標記都包含 ContentPlace HolderID`<asp:ContentPlaceHolder>`屬性, 該屬性指向它覆蓋的特定。</span><span class="sxs-lookup"><span data-stu-id="65a8f-150">Each `<asp:Content>` tag includes a ContentPlaceHolderID attribute that points to the particular `<asp:ContentPlaceHolder>` that it overrides.</span></span>

<span data-ttu-id="65a8f-151">此外,請注意,清單 2 中的內容檢視頁不包含任何正常的打開和關閉 HTML 標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-151">Notice, furthermore, that the content view page in Listing 2 does not contain any of the normal opening and closing HTML tags.</span></span> <span data-ttu-id="65a8f-152">例如,它不包含打開和關閉`<html>`或`<head>`標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-152">For example, it does not contain the opening and closing `<html>` or `<head>` tags.</span></span> <span data-ttu-id="65a8f-153">所有正常的打開和關閉標記都包含在檢視母版頁中。</span><span class="sxs-lookup"><span data-stu-id="65a8f-153">All of the normal opening and closing tags are contained in the view master page.</span></span>

<span data-ttu-id="65a8f-154">要在檢視內容頁中顯示的任何內容都必須放置在`<asp:Content>`標記中。</span><span class="sxs-lookup"><span data-stu-id="65a8f-154">Any content that you want to display in a view content page must be placed within a `<asp:Content>` tag.</span></span> <span data-ttu-id="65a8f-155">如果將這些標記之外放置任何 HTML 或其他內容,則當您嘗試查看頁面時,將出現錯誤。</span><span class="sxs-lookup"><span data-stu-id="65a8f-155">If you place any HTML or other content outside of these tags, then you will get an error when you attempt to view the page.</span></span>

<span data-ttu-id="65a8f-156">您無需覆蓋內容檢視頁中母`<asp:ContentPlaceHolder>`版頁中的每個標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-156">You don't need to override every `<asp:ContentPlaceHolder>` tag from a master page in a content view page.</span></span> <span data-ttu-id="65a8f-157">僅當要將`<asp:ContentPlaceHolder>`標記替換為特定內容時,才需要覆蓋標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-157">You only need to override a `<asp:ContentPlaceHolder>` tag when you want to replace the tag with particular content.</span></span>

<span data-ttu-id="65a8f-158">例如,清單 3 中修改的索引檢視僅包含`<asp:Content>`兩 個標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-158">For example, the modified Index view in Listing 3 contains only two `<asp:Content>` tags.</span></span> <span data-ttu-id="65a8f-159">每個`<asp:Content>`標記都包含一些文本。</span><span class="sxs-lookup"><span data-stu-id="65a8f-159">Each of the `<asp:Content>` tags includes some text.</span></span>

<span data-ttu-id="65a8f-160">**清單3 |`Views\Home\Index.aspx (modified)`**</span><span class="sxs-lookup"><span data-stu-id="65a8f-160">**Listing 3 – `Views\Home\Index.aspx (modified)`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

<span data-ttu-id="65a8f-161">當請求清單 3 中的檢視時,它將呈現圖 5 中的頁面。</span><span class="sxs-lookup"><span data-stu-id="65a8f-161">When the view in Listing 3 is requested, it renders the page in Figure 5.</span></span> <span data-ttu-id="65a8f-162">請注意,視圖呈現具有兩列的頁面。</span><span class="sxs-lookup"><span data-stu-id="65a8f-162">Notice that the view renders a page with two columns.</span></span> <span data-ttu-id="65a8f-163">此外,請注意,檢視內容頁中的內容將與檢視母版頁中的內容合併</span><span class="sxs-lookup"><span data-stu-id="65a8f-163">Notice, furthermore, that the content from the view content page is merged with the content from the view master page</span></span>

<span data-ttu-id="65a8f-164">[![索引檢視內容頁](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="65a8f-164">[![The Index view content page](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span></span>

<span data-ttu-id="65a8f-165">**圖 05**: 索引檢視內容頁 ([按下以檢視全尺寸影像](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="65a8f-165">**Figure 05**: The Index view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span></span>

### <a name="modifying-view-master-page-content"></a><span data-ttu-id="65a8f-166">變更檢視母版頁內容</span><span class="sxs-lookup"><span data-stu-id="65a8f-166">Modifying View Master Page Content</span></span>

<span data-ttu-id="65a8f-167">在使用檢視母版頁時,您幾乎立即遇到的一個問題是,當請求不同的檢視內容頁時,會修改視圖母版頁內容。</span><span class="sxs-lookup"><span data-stu-id="65a8f-167">One issue that you encounter almost immediately when working with view master pages is the problem of modifying view master page content when different view content pages are requested.</span></span> <span data-ttu-id="65a8f-168">例如,您希望 Web 應用程式中的每個頁面都有唯一的標題。</span><span class="sxs-lookup"><span data-stu-id="65a8f-168">For example, you want each page in your web application to have a unique title.</span></span> <span data-ttu-id="65a8f-169">但是,標題在視圖母版頁中聲明,而不是在視圖內容頁中聲明。</span><span class="sxs-lookup"><span data-stu-id="65a8f-169">However, the title is declared in the view master page and not in the view content page.</span></span> <span data-ttu-id="65a8f-170">那麼,如何為每個檢視內容頁面自定義頁面標題?</span><span class="sxs-lookup"><span data-stu-id="65a8f-170">So, how do you customize the page title for each view content page?</span></span>

<span data-ttu-id="65a8f-171">有兩種方法可以修改檢視內容頁顯示的標題。</span><span class="sxs-lookup"><span data-stu-id="65a8f-171">There are two ways that you can modify the title displayed by a view content page.</span></span> <span data-ttu-id="65a8f-172">首先,您可以將頁面標題分配給檢視內容頁頂部聲明的`<%@ page %>`指令的標題屬性。</span><span class="sxs-lookup"><span data-stu-id="65a8f-172">First, you can assign a page title to the title attribute of the `<%@ page %>` directive declared at the top of a view content page.</span></span> <span data-ttu-id="65a8f-173">例如,如果要將頁面標題「超級大網站」分配給索引檢視,則可以在 Index 視圖的頂部包括以下指令:</span><span class="sxs-lookup"><span data-stu-id="65a8f-173">For example, if you want to assign the page title "Super Great Website" to the Index view, then you can include the following directive at the top of the Index view:</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

<span data-ttu-id="65a8f-174">當「索引」檢視呈現給瀏覽器時,所需的標題將顯示在瀏覽器標題列中:</span><span class="sxs-lookup"><span data-stu-id="65a8f-174">When the Index view is rendered to the browser, the desired title appears in the browser title bar:</span></span>

<span data-ttu-id="65a8f-175">[![瀏覽器標題列](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="65a8f-175">[![Browser title bar](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span></span>

<span data-ttu-id="65a8f-176">主視圖頁必須滿足一個重要要求,以便標題屬性正常工作。</span><span class="sxs-lookup"><span data-stu-id="65a8f-176">There is one important requirement that a master view page must satisfy in order for the title attribute to work.</span></span> <span data-ttu-id="65a8f-177">視圖母版頁必須包含`<head runat="server">`標記,而不是其標題的`<head>`正常 標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-177">The view master page must contain a `<head runat="server">` tag instead of a normal `<head>` tag for its header.</span></span> <span data-ttu-id="65a8f-178">如果`<head>`標記不包含 runat_"server"屬性,則標題將不會顯示。</span><span class="sxs-lookup"><span data-stu-id="65a8f-178">If the `<head>` tag does not include the runat="server" attribute then the title won't appear.</span></span> <span data-ttu-id="65a8f-179">默認檢視母版頁包括所需的`<head runat="server">`標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-179">The default view master page includes the required `<head runat="server">` tag.</span></span>

<span data-ttu-id="65a8f-180">從單個檢視內容頁修改母版頁內容的另一種方法是包裝要在`<asp:ContentPlaceHolder>`標記中修改的區域。</span><span class="sxs-lookup"><span data-stu-id="65a8f-180">An alternative approach to modifying master page content from an individual view content page is to wrap the region that you want to modify in a `<asp:ContentPlaceHolder>` tag.</span></span> <span data-ttu-id="65a8f-181">例如,假設您不僅希望更改標題,還要更改由母版視圖頁呈現的元標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-181">For example, imagine that you want to change not only the title, but also the meta tags, rendered by a master view page.</span></span> <span data-ttu-id="65a8f-182">清單4中的主視圖頁在其`<asp:ContentPlaceHolder>``<head>`標記中包含一個標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-182">The master view page in Listing 4 contains a `<asp:ContentPlaceHolder>` tag within its `<head>` tag.</span></span>

<span data-ttu-id="65a8f-183">**清單4 |`Views\Shared\Site2.master`**</span><span class="sxs-lookup"><span data-stu-id="65a8f-183">**Listing 4 – `Views\Shared\Site2.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

<span data-ttu-id="65a8f-184">請注意,`<asp:ContentPlaceHolder>`清單 4 中的標記包括預設內容:默認標題和預設元標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-184">Notice that the `<asp:ContentPlaceHolder>` tag in Listing 4 includes default content: a default title and default meta tags.</span></span> <span data-ttu-id="65a8f-185">如果不在單個檢視內容頁中`<asp:ContentPlaceHolder>`覆蓋此標記,則將顯示默認內容。</span><span class="sxs-lookup"><span data-stu-id="65a8f-185">If you don't override this `<asp:ContentPlaceHolder>` tag in an individual view content page, then the default content will be displayed.</span></span>

<span data-ttu-id="65a8f-186">清單5中的內容檢視頁將覆蓋`<asp:ContentPlaceHolder>`標記,以便顯示自定義標題和自定義元標記。</span><span class="sxs-lookup"><span data-stu-id="65a8f-186">The content view page in Listing 5 overrides the `<asp:ContentPlaceHolder>` tag in order to display a custom title and custom meta tags.</span></span>

<span data-ttu-id="65a8f-187">**清單5 |`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="65a8f-187">**Listing 5 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a><span data-ttu-id="65a8f-188">總結</span><span class="sxs-lookup"><span data-stu-id="65a8f-188">Summary</span></span>

<span data-ttu-id="65a8f-189">本教程為您提供查看母版頁和查看內容頁的基本介紹。</span><span class="sxs-lookup"><span data-stu-id="65a8f-189">This tutorial provided you with a basic introduction to view master pages and view content pages.</span></span> <span data-ttu-id="65a8f-190">您學習了如何創建新的檢視母版頁,並基於它們創建檢視內容頁。</span><span class="sxs-lookup"><span data-stu-id="65a8f-190">You learned how to create new view master pages and create view content pages based on them.</span></span> <span data-ttu-id="65a8f-191">我們還研究了如何從特定視圖內容頁修改視圖母版頁的內容。</span><span class="sxs-lookup"><span data-stu-id="65a8f-191">We also examined how you can modify the content of a view master page from a particular view content page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="65a8f-192">[前一個](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [下一個](passing-data-to-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="65a8f-192">[Previous](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
[Next](passing-data-to-view-master-pages-cs.md)</span></span>
