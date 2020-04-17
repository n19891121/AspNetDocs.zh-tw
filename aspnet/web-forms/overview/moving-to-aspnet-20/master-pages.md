---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 母版頁 |微軟文件
author: rick-anderson
description: 成功網站的關鍵元件之一是外觀一致。 在ASP.NET 1.x 中,開發人員使用使用者控制件來複製通用頁面 elem...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: b493feb21d2e3d6429f0a23df5aab66e0c4c5b07
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543180"
---
# <a name="master-pages"></a><span data-ttu-id="52dec-104">主版頁面</span><span class="sxs-lookup"><span data-stu-id="52dec-104">Master Pages</span></span>

<span data-ttu-id="52dec-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="52dec-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="52dec-106">成功網站的關鍵元件之一是外觀一致。</span><span class="sxs-lookup"><span data-stu-id="52dec-106">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="52dec-107">在ASP.NET 1.x 中,開發人員使用使用者控制件跨Web應用程式複製公共頁面元素。</span><span class="sxs-lookup"><span data-stu-id="52dec-107">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="52dec-108">雖然這當然是一個可行的解決方案,但使用使用者控件確實有一些缺點。</span><span class="sxs-lookup"><span data-stu-id="52dec-108">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="52dec-109">例如,更改使用者控制項的位置需要更改到網站中的多個頁面。</span><span class="sxs-lookup"><span data-stu-id="52dec-109">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="52dec-110">在頁面上插入后,使用者控件也不會在"設計"視圖中呈現。</span><span class="sxs-lookup"><span data-stu-id="52dec-110">User controls are also not rendered in Design view after being inserted on a page.</span></span>

<span data-ttu-id="52dec-111">成功網站的關鍵元件之一是外觀一致。</span><span class="sxs-lookup"><span data-stu-id="52dec-111">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="52dec-112">在ASP.NET 1.x 中,開發人員使用使用者控制件跨Web應用程式複製公共頁面元素。</span><span class="sxs-lookup"><span data-stu-id="52dec-112">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="52dec-113">雖然這當然是一個可行的解決方案,但使用使用者控件確實有一些缺點。</span><span class="sxs-lookup"><span data-stu-id="52dec-113">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="52dec-114">例如,更改使用者控制項的位置需要更改到網站中的多個頁面。</span><span class="sxs-lookup"><span data-stu-id="52dec-114">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="52dec-115">在頁面上插入后,使用者控件也不會在"設計"視圖中呈現。</span><span class="sxs-lookup"><span data-stu-id="52dec-115">User controls are also not rendered in Design view after being inserted on a page.</span></span>

<span data-ttu-id="52dec-116">ASP.NET 2.0 引入母版頁作為保持一致外觀和感覺的一種方式,正如您很快就會看到的那樣,母版頁代表了對使用者控制方法的重大改進。</span><span class="sxs-lookup"><span data-stu-id="52dec-116">ASP.NET 2.0 introduces Master pages as a way of maintaining a consistent look and feel, and as you'll soon see, Master pages represent a significant improvement over the user control method.</span></span>

## <a name="why-master-pages"></a><span data-ttu-id="52dec-117">為什麼選擇母版頁?</span><span class="sxs-lookup"><span data-stu-id="52dec-117">Why Master Pages?</span></span>

<span data-ttu-id="52dec-118">您可能想知道為什麼 ASP.NET 2.0 需要母版頁。</span><span class="sxs-lookup"><span data-stu-id="52dec-118">You may be wondering why master pages were needed in ASP.NET 2.0.</span></span> <span data-ttu-id="52dec-119">畢竟,網站開發人員已經在ASP.NET 1.x 中使用使用者控制式件在頁面之間共用內容區域。</span><span class="sxs-lookup"><span data-stu-id="52dec-119">After all, Web site developers are already using user controls in ASP.NET 1.x to share content areas between pages.</span></span> <span data-ttu-id="52dec-120">實際上,使用者控件是創建公共佈局的不太理想的解決方案的原因有很多。</span><span class="sxs-lookup"><span data-stu-id="52dec-120">There are actually several reasons why user controls are a less-than-optimal solution for creating a common layout.</span></span>

<span data-ttu-id="52dec-121">使用者控件實際上不定義頁面佈局。</span><span class="sxs-lookup"><span data-stu-id="52dec-121">User controls don't actually define page layout.</span></span> <span data-ttu-id="52dec-122">相反,它們定義頁面的一部分的佈局和功能。</span><span class="sxs-lookup"><span data-stu-id="52dec-122">Instead, they define the layout and functionality for a portion of a page.</span></span> <span data-ttu-id="52dec-123">這兩者之間的區別很重要,因為它使用戶控制解決方案的可管理性變得更加困難。</span><span class="sxs-lookup"><span data-stu-id="52dec-123">The distinction between these two is important because it makes manageability of a user control solution much more difficult.</span></span> <span data-ttu-id="52dec-124">例如,如果要更改頁面上的使用者控制項的位置,必須編輯顯示使用者控制件的實際頁面。</span><span class="sxs-lookup"><span data-stu-id="52dec-124">For example, when you want to change the position of a user control on your page, you must edit the actual page on which the user control appears.</span></span> <span data-ttu-id="52dec-125">如果你只有幾頁,這很好,但在大型網站,它迅速成為一個網站管理噩夢!</span><span class="sxs-lookup"><span data-stu-id="52dec-125">Thats fine if you have only a few pages, but in large sites, it quickly becomes a site management nightmare!</span></span>

<span data-ttu-id="52dec-126">使用使用者控制定義公共佈局的另一個缺點是ASP.NET本身的體系結構。</span><span class="sxs-lookup"><span data-stu-id="52dec-126">Another drawback of using user controls for defining a common layout is rooted in the architecture of ASP.NET itself.</span></span> <span data-ttu-id="52dec-127">如果更改了使用者控件的任何公共成員,則需要重新編譯使用使用者控制件的所有頁面。</span><span class="sxs-lookup"><span data-stu-id="52dec-127">If any public member of a user control is changed, it requires you to recompile all of the pages that use the user control.</span></span> <span data-ttu-id="52dec-128">反過來,ASP.NET將在首次訪問頁面時重新 JIT。</span><span class="sxs-lookup"><span data-stu-id="52dec-128">In turn, ASP.NET will then re-JIT your pages when they are first accessed.</span></span> <span data-ttu-id="52dec-129">這再次產生了一個不可擴展的體系結構和大型網站的網站管理問題。</span><span class="sxs-lookup"><span data-stu-id="52dec-129">This, once again, produces a non-scalable architecture and a site management problem for larger sites.</span></span>

<span data-ttu-id="52dec-130">ASP.NET 2.0 中的母版頁很好地解決了這兩個問題(以及更多問題)。</span><span class="sxs-lookup"><span data-stu-id="52dec-130">Both of these problems (and many more) are nicely addressed by master pages in ASP.NET 2.0.</span></span>

## <a name="how-master-pages-work"></a><span data-ttu-id="52dec-131">母版頁的工作原理</span><span class="sxs-lookup"><span data-stu-id="52dec-131">How Master Pages Work</span></span>

<span data-ttu-id="52dec-132">母版頁類似於其他頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="52dec-132">A master page is analogous to a template for other pages.</span></span> <span data-ttu-id="52dec-133">應在其他頁面(即功能表、邊框等)之間共用的頁面元素將添加到母版頁中。</span><span class="sxs-lookup"><span data-stu-id="52dec-133">Page elements that should be shared among other pages (i.e. menus, borders, etc.) are added to the master page.</span></span> <span data-ttu-id="52dec-134">將新頁面添加到網站時,可以將它們與母版頁相關聯。</span><span class="sxs-lookup"><span data-stu-id="52dec-134">When new pages are added to the site, you can associate them with a master page.</span></span> <span data-ttu-id="52dec-135">與母版頁關聯的頁面稱為**內容頁**。</span><span class="sxs-lookup"><span data-stu-id="52dec-135">A page that is associated with a master page is called a **content page**.</span></span> <span data-ttu-id="52dec-136">默認情況下,內容頁從母版頁中呈現外觀。</span><span class="sxs-lookup"><span data-stu-id="52dec-136">By default, a content page takes on the appearance from the master page.</span></span> <span data-ttu-id="52dec-137">但是,在創建母版頁時,可以定義內容頁可以替換為其自己的內容的部分內容。</span><span class="sxs-lookup"><span data-stu-id="52dec-137">However, when you create a master page, you can define portions of the page that the content page can replace with its own content.</span></span> <span data-ttu-id="52dec-138">這些部分使用ASP.NET 2.0 中引入的新控制件進行定義;**ContentPlaceHolder 控制項**。</span><span class="sxs-lookup"><span data-stu-id="52dec-138">These portions are defined using a new control introduced in ASP.NET 2.0; the **ContentPlaceHolder** control.</span></span>

<span data-ttu-id="52dec-139">母版頁可以包含任意數量的 Content PlaceHolder 控件(或根本沒有。在內容頁上,"ContentPlace Holder"控件中的內容將顯示在**內容**控件中,這是 ASP.NET 2.0 中的另一個新控制項。</span><span class="sxs-lookup"><span data-stu-id="52dec-139">A master page can contain any number of ContentPlaceHolder controls (or none at all.) On the content page, the content from the ContentPlaceHolder controls appears inside of **Content** controls, another new control in ASP.NET 2.0.</span></span> <span data-ttu-id="52dec-140">預設情況下,內容頁 內容控制項為空,以便您可以提供自己的內容。</span><span class="sxs-lookup"><span data-stu-id="52dec-140">By default, the content pages Content controls are empty so that you can provide your own content.</span></span> <span data-ttu-id="52dec-141">如果要使用內容控制件內母版頁中的內容,可以執行此操作,正如您將在此模組的後面部分看到的。</span><span class="sxs-lookup"><span data-stu-id="52dec-141">If you want to use the content from the master page inside of the Content controls, you can do so as you will see later in this module.</span></span> <span data-ttu-id="52dec-142">內容控件通過內容控制件的「內容霍爾德ID」屬性映射到 ContentPlaceHolderId 控制件。</span><span class="sxs-lookup"><span data-stu-id="52dec-142">The Content control is mapped to the ContentPlaceHolder control via the ContentPlaceHolderID attribute of the Content control.</span></span> <span data-ttu-id="52dec-143">下面的代碼將內容控件映射到主頁上稱為 mainBody 的 Content Place Holder 控件。</span><span class="sxs-lookup"><span data-stu-id="52dec-143">The code below maps a Content control to a ContentPlaceHolder control called mainBody on a master page.</span></span>

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> <span data-ttu-id="52dec-144">您經常會聽到人們將母版頁描述為其他頁面的基類。</span><span class="sxs-lookup"><span data-stu-id="52dec-144">You will often hear people describe master pages as being a base class for other pages.</span></span> <span data-ttu-id="52dec-145">這實際上不是真的。</span><span class="sxs-lookup"><span data-stu-id="52dec-145">Thats actually not true.</span></span> <span data-ttu-id="52dec-146">母版頁和內容頁之間的關係不是繼承關係。</span><span class="sxs-lookup"><span data-stu-id="52dec-146">The relationship between master pages and content pages is not one of inheritance.</span></span>

<span data-ttu-id="52dec-147">**圖 1**顯示了母版頁和關聯的內容頁,因為它們出現在 Visual Studio 2005 中。</span><span class="sxs-lookup"><span data-stu-id="52dec-147">**Figure 1** shows a master page and an associated content page as they appear in Visual Studio 2005.</span></span> <span data-ttu-id="52dec-148">您可以在母版頁中查看 ContentPlaceHolder 控件,並在內容頁中看到相應的內容控制件。</span><span class="sxs-lookup"><span data-stu-id="52dec-148">You can see the ContentPlaceHolder control in the master page and the corresponding Content control in the content page.</span></span> <span data-ttu-id="52dec-149">請注意,內容霍爾德持有人外部的母版頁內容可見,但在內容頁中顯示為灰色。</span><span class="sxs-lookup"><span data-stu-id="52dec-149">Notice that the master pages content that is outside of the ContentPlaceHolder is visible but grayed out in the content page.</span></span> <span data-ttu-id="52dec-150">只有 ContentPlaceHolder 中的內容可以由內容頁取代。</span><span class="sxs-lookup"><span data-stu-id="52dec-150">Only the content inside of the ContentPlaceHolder can be supplanted by the content page.</span></span> <span data-ttu-id="52dec-151">來自母版頁的所有其他內容是不可改變的。</span><span class="sxs-lookup"><span data-stu-id="52dec-151">All other content that comes from the master page is immutable.</span></span>

![母版頁及其關聯內容頁](master-pages/_static/image1.jpg)

<span data-ttu-id="52dec-153">**圖 1**: 母版頁及其關聯內容頁</span><span class="sxs-lookup"><span data-stu-id="52dec-153">**Figure 1**: A master page and its associated content page</span></span>

## <a name="creating-a-master-page"></a><span data-ttu-id="52dec-154">建立母版頁</span><span class="sxs-lookup"><span data-stu-id="52dec-154">Creating a Master Page</span></span>

<span data-ttu-id="52dec-155">要創建新的母版頁,</span><span class="sxs-lookup"><span data-stu-id="52dec-155">To create a new master page:</span></span>

1. <span data-ttu-id="52dec-156">打開 Visual Studio 2005 並創建新網站。</span><span class="sxs-lookup"><span data-stu-id="52dec-156">Open Visual Studio 2005 and create a new Web site.</span></span>
2. <span data-ttu-id="52dec-157">按下"檔,新建,檔"。</span><span class="sxs-lookup"><span data-stu-id="52dec-157">Click File, New, File.</span></span>
3. <span data-ttu-id="52dec-158">從"添加新項目"對話框中選擇主檔,如圖**2**所示。</span><span class="sxs-lookup"><span data-stu-id="52dec-158">Choose Master File from the Add New Item dialog as shown in **figure 2**.</span></span>
4. <span data-ttu-id="52dec-159">按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="52dec-159">Click Add.</span></span>

![建立新母版頁](master-pages/_static/image2.jpg)

<span data-ttu-id="52dec-161">**圖 2**: 建立新母版頁</span><span class="sxs-lookup"><span data-stu-id="52dec-161">**Figure 2**: Creating a New Master Page</span></span>

<span data-ttu-id="52dec-162">請注意,母版頁的檔案副檔名是 *.master*。</span><span class="sxs-lookup"><span data-stu-id="52dec-162">Notice that the file extension for a master page is *.master*.</span></span> <span data-ttu-id="52dec-163">這是母版頁與普通頁面不同的方式之一。</span><span class="sxs-lookup"><span data-stu-id="52dec-163">This is one of the ways that a master page differs from an ordinary page.</span></span> <span data-ttu-id="52dec-164">另一個主要區別是,母版頁代替指令@Page,包含一@Master個 指令。</span><span class="sxs-lookup"><span data-stu-id="52dec-164">The other primary difference is that in lieu of a @Page directive, the master page contains a @Master directive.</span></span> <span data-ttu-id="52dec-165">切換到您剛剛建立的母版頁的源檢視並查看代碼。</span><span class="sxs-lookup"><span data-stu-id="52dec-165">Switch to Source View for the master page you've just created and review the code.</span></span>

<span data-ttu-id="52dec-166">默認情況下,新的母版頁將有一個 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="52dec-166">A new master page will have one ContentPlaceHolder control by default.</span></span> <span data-ttu-id="52dec-167">在大多數情況下,首先創建公共頁面元素,然後插入需要自定義內容的 ContentPlace Holder 控件更有意義。</span><span class="sxs-lookup"><span data-stu-id="52dec-167">In most cases, it makes more sense to create the common page elements first and then insert ContentPlaceHolder controls where custom content is desired.</span></span> <span data-ttu-id="52dec-168">在這些情況下,開發人員將希望刪除預設的 ContentPlaceHolder 控件,並在頁面開發時插入新的控制項。</span><span class="sxs-lookup"><span data-stu-id="52dec-168">In those cases, developers will want to delete the default ContentPlaceHolder control and insert new ones as the page is developed.</span></span> <span data-ttu-id="52dec-169">ContentPlaceHolder 控件雖然確實顯示大小調整句柄,但它們不會調整大小。</span><span class="sxs-lookup"><span data-stu-id="52dec-169">ContentPlaceHolder controls are not resizable despite the fact that they do display sizing handles.</span></span> <span data-ttu-id="52dec-170">ContentPlaceHolder 控件的大小會自動基於它包含的內容,但有一個例外;如果將 ContentPlaceHolder 控制元件放置在塊元素(如表單元格)內,則該控制項將根據元素的大小進行大小調整。</span><span class="sxs-lookup"><span data-stu-id="52dec-170">The ContentPlaceHolder control sizes automatically based upon the content that it contains with one exception; if you place a ContentPlaceHolder control inside of a block element such as a table cell, it will size according to the size of the element.</span></span>

## <a name="lab-1-working-with-master-pages"></a><span data-ttu-id="52dec-171">實驗室 1 使用母版頁</span><span class="sxs-lookup"><span data-stu-id="52dec-171">Lab 1 Working with Master Pages</span></span>

<span data-ttu-id="52dec-172">在本實驗中,您將創建一個新的母版頁,並定義三個 ContentPlaceHolder 控制件。</span><span class="sxs-lookup"><span data-stu-id="52dec-172">In this lab, you will create a new master page and define three ContentPlaceHolder controls.</span></span> <span data-ttu-id="52dec-173">然後,您將創建新的內容頁,並至少從其中一個 ContentPlace Holder 控制中替換內容。</span><span class="sxs-lookup"><span data-stu-id="52dec-173">You will then create a new Content page and replace the content from at least one of the ContentPlaceHolder controls.</span></span>

1. <span data-ttu-id="52dec-174">創建母版頁並插入內容霍爾德控制項。</span><span class="sxs-lookup"><span data-stu-id="52dec-174">Create a master page and insert ContentPlaceHolder controls.</span></span> 

    1. <span data-ttu-id="52dec-175">如上文所述,創建新的母版頁。</span><span class="sxs-lookup"><span data-stu-id="52dec-175">Create a new master page as described above.</span></span>
    2. <span data-ttu-id="52dec-176">移除預設的「內容放置」 控制器。</span><span class="sxs-lookup"><span data-stu-id="52dec-176">Delete the default ContentPlaceHolder control.</span></span>
    3. <span data-ttu-id="52dec-177">通過按一下控制的上邊框,然後點擊鍵盤上的 DEL 鍵將其刪除,選擇 ContentPlaceHolder 控制件。</span><span class="sxs-lookup"><span data-stu-id="52dec-177">Select the ContentPlaceHolder control by clicking the shaded top border of the control and then delete it by hitting the DEL key on your keyboard.</span></span>
    4. <span data-ttu-id="52dec-178">使用*標題和側*範本插入新錶,如圖 3 所示。</span><span class="sxs-lookup"><span data-stu-id="52dec-178">Insert a new table using the *Header and side* template as shown in figure 3.</span></span> <span data-ttu-id="52dec-179">將寬度和高度更改為 90%,以便整個表在設計器中可見。</span><span class="sxs-lookup"><span data-stu-id="52dec-179">Change the width and height to 90% each so that the entire table is visible in the designer.</span></span>

![](master-pages/_static/image3.jpg)

<span data-ttu-id="52dec-180">**圖 3**</span><span class="sxs-lookup"><span data-stu-id="52dec-180">**Figure 3**</span></span>

1. <span data-ttu-id="52dec-181">將游標放入表的每個儲存格中,並將*valign*屬性設定為*頂端*。</span><span class="sxs-lookup"><span data-stu-id="52dec-181">Place the cursor into each cell of the table and set the *valign* property to *top*.</span></span>
2. <span data-ttu-id="52dec-182">在工具箱中,在表的頂部單元格(標題單元格)中插入 ContentPlaceHolder 控制件。</span><span class="sxs-lookup"><span data-stu-id="52dec-182">From the Toolbox, insert a ContentPlaceHolder control in the top cell of the table (the header cell.)</span></span>
3. <span data-ttu-id="52dec-183">插入此 ContentPlaceHolder 控件時,您會注意到行高度將佔用幾乎整個頁面,如圖 4 所示。</span><span class="sxs-lookup"><span data-stu-id="52dec-183">When you insert this ContentPlaceHolder control, you will notice that the row height will take up almost the entire page as shown in figure 4.</span></span> <span data-ttu-id="52dec-184">在這一點上不要擔心。</span><span class="sxs-lookup"><span data-stu-id="52dec-184">Don't be concerned about that at this point.</span></span>

![空白空間與內容霍爾德位於同一單元格中](master-pages/_static/image1.gif)

<span data-ttu-id="52dec-186">**圖 4**: 空白空間與內容霍爾德位於同一儲存格中</span><span class="sxs-lookup"><span data-stu-id="52dec-186">**Figure 4**: The empty space is in the same cell as the ContentPlaceHolder</span></span>

1. <span data-ttu-id="52dec-187">將 Content PlaceHolder 控件放在其他兩個單元格中。</span><span class="sxs-lookup"><span data-stu-id="52dec-187">Place a ContentPlaceHolder control in the other two cells.</span></span> <span data-ttu-id="52dec-188">插入其他 ContentPlaceHolder 控制程式後,表單元格的大小應如您所料。</span><span class="sxs-lookup"><span data-stu-id="52dec-188">Once the other ContentPlaceHolder controls have been inserted, the size of the table cells should be as you would expect.</span></span> <span data-ttu-id="52dec-189">該頁現在應類似於**圖 5**所示的頁面。</span><span class="sxs-lookup"><span data-stu-id="52dec-189">The page should now look like the page shown in **figure 5**.</span></span>

![包含所有內容位置擁有者控制件的主控形狀。](master-pages/_static/image2.gif)

<span data-ttu-id="52dec-192">**圖 5**: 包含所有內容霍爾德控制項的主控形狀。</span><span class="sxs-lookup"><span data-stu-id="52dec-192">**Figure 5**: The Master with all ContentPlaceHolder controls.</span></span> <span data-ttu-id="52dec-193">請注意,頭單元格的單元格高度現在正是它應該的</span><span class="sxs-lookup"><span data-stu-id="52dec-193">Notice that the cell height for the header cell is now what it should be</span></span>

1. <span data-ttu-id="52dec-194">在三個 ContentPlaceHolder 控制件中的每個控制項中輸入您選擇的文字。</span><span class="sxs-lookup"><span data-stu-id="52dec-194">Enter some text of your choice into each of the three ContentPlaceHolder controls.</span></span>
2. <span data-ttu-id="52dec-195">將母版頁另存為練習1.master。</span><span class="sxs-lookup"><span data-stu-id="52dec-195">Save the master page as exercise1.master.</span></span>
3. <span data-ttu-id="52dec-196">創建新的 Web 窗體並將其與練習 1.master 頁相關聯。</span><span class="sxs-lookup"><span data-stu-id="52dec-196">Create a new Web Form and associate it with the exercise1.master master page.</span></span>
4. <span data-ttu-id="52dec-197">選擇檔,新建,檔在可視化工作室2005年。</span><span class="sxs-lookup"><span data-stu-id="52dec-197">Select File, New, File in Visual Studio 2005.</span></span>
5. <span data-ttu-id="52dec-198">在「添加新項目」對話框中選擇 **「Web 窗體**」 。。</span><span class="sxs-lookup"><span data-stu-id="52dec-198">Select **Web Form** in the Add New Item dialog.</span></span>
6. <span data-ttu-id="52dec-199">確保選中"選擇母版頁"複選框,如圖 6 所示。</span><span class="sxs-lookup"><span data-stu-id="52dec-199">Make sure that the Select master page checkbox is checked as shown in figure 6.</span></span>

![新增的內容頁](master-pages/_static/image3.gif)

<span data-ttu-id="52dec-201">**圖 6**: 新增新的內容頁</span><span class="sxs-lookup"><span data-stu-id="52dec-201">**Figure 6**: Adding a new Content Page</span></span>

1. <span data-ttu-id="52dec-202">按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="52dec-202">Click Add.</span></span>
2. <span data-ttu-id="52dec-203">在「選擇母版頁對話框中選擇練習1.master,如圖 7 所示。</span><span class="sxs-lookup"><span data-stu-id="52dec-203">Select exercise1.master in the Select a master page dialog as shown in figure 7.</span></span>
3. <span data-ttu-id="52dec-204">按一下「確定」以添加新內容頁。</span><span class="sxs-lookup"><span data-stu-id="52dec-204">Click OK to add the new content page.</span></span>

<span data-ttu-id="52dec-205">新內容頁顯示在 Visual Studio 中,母版頁上每個 Content PlaceHolder 控制件都有一個內容控制件。</span><span class="sxs-lookup"><span data-stu-id="52dec-205">The new content page appears in Visual Studio with one Content control for each ContentPlaceHolder control on the master page.</span></span> <span data-ttu-id="52dec-206">預設情況下,內容控制項為空,以便您可以添加自己的內容。</span><span class="sxs-lookup"><span data-stu-id="52dec-206">By default, the Content controls are empty so that you can add your own content.</span></span> <span data-ttu-id="52dec-207">如果您希望他們使用母版頁上的 ContentPlaceHolder 控件中的內容,只需單擊智慧標記符號(控件右上角的小黑箭頭),然後從智慧標記中選擇 *「默認到母版內容*」,如圖**8**所示。</span><span class="sxs-lookup"><span data-stu-id="52dec-207">If you'd like for them to use the content from the ContentPlaceHolder control on the master page, simply click on the smart tag symbol (the small black arrow in the upper-right corner of the control) and choose *Default to Masters Content* from the smart tag as shown in **figure 8**.</span></span> <span data-ttu-id="52dec-208">執行此操作時,功能表項將更改為 *「創建自訂內容*」 。</span><span class="sxs-lookup"><span data-stu-id="52dec-208">When you do so, the menu item changes to *Create Custom Content*.</span></span> <span data-ttu-id="52dec-209">此時按這裏選它會從母版頁中刪除內容,允許您為該特定內容控制項定義自訂內容。</span><span class="sxs-lookup"><span data-stu-id="52dec-209">Clicking it at that point removes the content from the master page allowing you to define custom content for that particular Content control.</span></span>

![將內容控制檔設定為預設為母版頁內容](master-pages/_static/image4.gif)

<span data-ttu-id="52dec-211">**圖 7**: 將內容控制檔設定為預設為母版頁內容</span><span class="sxs-lookup"><span data-stu-id="52dec-211">**Figure 7**: Setting a Content Control to Default to the Master Pages Content</span></span>

## <a name="connecting-master-page-and-content-pages"></a><span data-ttu-id="52dec-212">連接母版頁與內容頁</span><span class="sxs-lookup"><span data-stu-id="52dec-212">Connecting Master Page and Content Pages</span></span>

<span data-ttu-id="52dec-213">母版頁和內容頁之間的關聯可以通過以下四種不同方式之一進行配置:</span><span class="sxs-lookup"><span data-stu-id="52dec-213">The association between a master page and a content page can be configured in one of four different ways:</span></span>

- <span data-ttu-id="52dec-214">指令的@Page<strong>母版頁面檔案</strong>屬性</span><span class="sxs-lookup"><span data-stu-id="52dec-214">The <strong>MasterPageFile</strong> attribute of the @Page directive</span></span>
- <span data-ttu-id="52dec-215">在代碼中設置**Page.MasterPageFile**屬性。</span><span class="sxs-lookup"><span data-stu-id="52dec-215">Setting the **Page.MasterPageFile** property in code.</span></span>
- <span data-ttu-id="52dec-216">應用程式設定檔中的**&lt;頁面&gt;** 元素(應用程式根資料夾中的 Web.config)</span><span class="sxs-lookup"><span data-stu-id="52dec-216">The **&lt;pages&gt;** element in the applications configuration file (web.config in the root folder of the application)</span></span>
- <span data-ttu-id="52dec-217">子資料夾設定檔中的**&lt;頁面&gt;** 元素(子資料夾中的 Web.config)</span><span class="sxs-lookup"><span data-stu-id="52dec-217">The **&lt;pages&gt;** element in a subfolders configuration file (web.config in a subfolder)</span></span>

## <a name="masterpagefile-attribute"></a><span data-ttu-id="52dec-218">母版檔案屬性</span><span class="sxs-lookup"><span data-stu-id="52dec-218">MasterPageFile Attribute</span></span>

<span data-ttu-id="52dec-219">MasterPageFile 屬性使將母版頁應用於特定ASP.NET頁面變得容易。</span><span class="sxs-lookup"><span data-stu-id="52dec-219">The MasterPageFile attribute makes it easy to apply a master page to a particular ASP.NET page.</span></span> <span data-ttu-id="52dec-220">當您選中 **「選擇母版頁**」複選框時,它也是用於應用母版頁的方法,就像練習 1 中所做的那樣。</span><span class="sxs-lookup"><span data-stu-id="52dec-220">It is also the method used to apply the master page when you check the **Select Master Page** checkbox as you did in Exercise 1.</span></span>

## <a name="setting-pagemasterpagefile-in-code"></a><span data-ttu-id="52dec-221">設定頁面.MasterPage檔案代碼</span><span class="sxs-lookup"><span data-stu-id="52dec-221">Setting Page.MasterPageFile in Code</span></span>

<span data-ttu-id="52dec-222">通過在代碼中設置 MasterPageFile 屬性,可以在運行時將特定的母版頁應用於您的內容。</span><span class="sxs-lookup"><span data-stu-id="52dec-222">By setting the MasterPageFile property in code, you can apply a particular master page to your content at runtime.</span></span> <span data-ttu-id="52dec-223">在可能需要根據使用者角色或其他一些條件應用特定母版頁的情況下,這非常有用。</span><span class="sxs-lookup"><span data-stu-id="52dec-223">This is useful in cases where you may need to apply a specific master page based upon a users role or some other criteria.</span></span> <span data-ttu-id="52dec-224">必須在 PreInit 方法中設置 MasterPageFile 屬性。</span><span class="sxs-lookup"><span data-stu-id="52dec-224">The MasterPageFile property must be set in the PreInit method.</span></span> <span data-ttu-id="52dec-225">如果在 PreInit 方法之後設置,將引發無效操作異常。</span><span class="sxs-lookup"><span data-stu-id="52dec-225">If it is set after the PreInit method, an InvalidOperationException will be thrown.</span></span> <span data-ttu-id="52dec-226">正在設置此屬性的頁面還必須具有「內容」控件作為該頁的頂級控制項。</span><span class="sxs-lookup"><span data-stu-id="52dec-226">The page on which this property is being set must also have a Content control as the top-level control for the page.</span></span> <span data-ttu-id="52dec-227">否則,在設置 MasterPageFile 屬性時,將引發 HTTPException。</span><span class="sxs-lookup"><span data-stu-id="52dec-227">Otherwise an HttpException will be thrown when the MasterPageFile property is set.</span></span>

## <a name="using-the-ltpagesgt-element"></a><span data-ttu-id="52dec-228">使用&lt;頁面&gt;元素</span><span class="sxs-lookup"><span data-stu-id="52dec-228">Using the &lt;pages&gt; Element</span></span>

<span data-ttu-id="52dec-229">您可以通過在 Web.config&lt;&gt;檔的頁面 元素中設定 masterPageFile 屬性來設定頁面的母版頁。</span><span class="sxs-lookup"><span data-stu-id="52dec-229">You can configure a master page for your pages by setting the masterPageFile attribute in the &lt;pages&gt; element of the web.config file.</span></span> <span data-ttu-id="52dec-230">使用此方法時,請記住,應用程式結構中較低的 Web.config 檔可以覆蓋此設置。</span><span class="sxs-lookup"><span data-stu-id="52dec-230">When using this method, keep in mind that web.config files lower in the application structure can override this setting.</span></span> <span data-ttu-id="52dec-231">@Page指令中的任何 MasterPageFile 屬性集也將覆蓋此設定。</span><span class="sxs-lookup"><span data-stu-id="52dec-231">Any MasterPageFile attribute set in a @Page directive will also override this setting.</span></span> <span data-ttu-id="52dec-232">使用&lt;頁面&gt;元素可以創建可在特定資料夾或檔中在必要時重寫*的主版*頁變得簡單。</span><span class="sxs-lookup"><span data-stu-id="52dec-232">Using the &lt;pages&gt; element makes it simple to create a *master* master page that can be overridden if necessary in particular folders or files.</span></span>

## <a name="properties-in-master-pages"></a><span data-ttu-id="52dec-233">母版頁中的屬性</span><span class="sxs-lookup"><span data-stu-id="52dec-233">Properties in Master Pages</span></span>

<span data-ttu-id="52dec-234">母版頁只需在母版頁中公開這些屬性,即可公開屬性。</span><span class="sxs-lookup"><span data-stu-id="52dec-234">A master page can expose properties by simply making those properties public within the master page.</span></span> <span data-ttu-id="52dec-235">例如,以下代碼定義名為「某些屬性」的屬性:</span><span class="sxs-lookup"><span data-stu-id="52dec-235">For example, the following code defines a property called SomeProperty:</span></span>

[!code-csharp[Main](master-pages/samples/sample2.cs)]

<span data-ttu-id="52dec-236">要從「內容」頁存取「某些屬性」屬性,您需要使用「主」屬性,如下所示:</span><span class="sxs-lookup"><span data-stu-id="52dec-236">To access the SomeProperty property from the Content page, you will need to use the Master property like so:</span></span>

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a><span data-ttu-id="52dec-237">巢狀母版頁</span><span class="sxs-lookup"><span data-stu-id="52dec-237">Nesting Master Pages</span></span>

<span data-ttu-id="52dec-238">母版頁是確保大型 Web 應用程式的共同外觀的完美解決方案。</span><span class="sxs-lookup"><span data-stu-id="52dec-238">Master pages are the perfect solution for ensuring a common look and feel across a large Web application.</span></span> <span data-ttu-id="52dec-239">但是,大型網站的某些部分共用公共介面,而其他部分共用不同的介面的情況並不少見。</span><span class="sxs-lookup"><span data-stu-id="52dec-239">However, it's not uncommon to have certain parts of a large site share a common interface while other parts share a different interface.</span></span> <span data-ttu-id="52dec-240">為了滿足這一需求,多個母版頁是完美的解決方案。</span><span class="sxs-lookup"><span data-stu-id="52dec-240">To address that need, multiple master pages are the perfect solution.</span></span> <span data-ttu-id="52dec-241">但是,這仍然不能解決大型應用程式可能具有某些元件(例如功能表)這一事實,這些元件僅在網站的某些部分之間共用的所有頁面和其他元件之間共用。</span><span class="sxs-lookup"><span data-stu-id="52dec-241">However, that still doesn't address the fact that a large application may have certain components (such as a menu, for example) that are shared among all pages and other components that are shared only among certain sections of the site.</span></span> <span data-ttu-id="52dec-242">對於這種情況,嵌套母版頁很好地滿足了需求。</span><span class="sxs-lookup"><span data-stu-id="52dec-242">For that type of situation, nested master pages fill the need nicely.</span></span> <span data-ttu-id="52dec-243">正如您所看到的,普通母版頁由母版頁和內容頁組成。</span><span class="sxs-lookup"><span data-stu-id="52dec-243">As you've seen, a normal master page consists of a master page and a content page.</span></span> <span data-ttu-id="52dec-244">在嵌套母版頁的情況下,有兩個母版頁;父主控形狀和子母版。</span><span class="sxs-lookup"><span data-stu-id="52dec-244">In a nested master page situation, there are two master pages; a parent master and a child master.</span></span> <span data-ttu-id="52dec-245">子母版頁也是內容頁,其母版頁是父母版頁。</span><span class="sxs-lookup"><span data-stu-id="52dec-245">The child master page is also a content page and its master is the parent master page.</span></span>

<span data-ttu-id="52dec-246">下面是典型母版頁的代碼:</span><span class="sxs-lookup"><span data-stu-id="52dec-246">Here is the code for a typical master page:</span></span>

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

<span data-ttu-id="52dec-247">在嵌套主方案中,這將是父主控形狀。</span><span class="sxs-lookup"><span data-stu-id="52dec-247">In a nested master scenario, this would be the parent master.</span></span> <span data-ttu-id="52dec-248">另一個母版頁將使用此頁作為其母版頁,該代碼如下所示:</span><span class="sxs-lookup"><span data-stu-id="52dec-248">Another master page would use this page as its master page, and that code would look like this:</span></span>

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

<span data-ttu-id="52dec-249">請注意,在這種情況下,子母版也是父主控形狀的內容頁。</span><span class="sxs-lookup"><span data-stu-id="52dec-249">Note that in this scenario, the child master is also a content page for the parent master.</span></span> <span data-ttu-id="52dec-250">所有子主控內容都顯示在內容控件中,該控件從父級的 ContentPlaceHolder 控件中獲取其內容。</span><span class="sxs-lookup"><span data-stu-id="52dec-250">All of the child master's content appears inside of a Content control that gets its content from the parent's ContentPlaceHolder control.</span></span>

> [!NOTE]
> <span data-ttu-id="52dec-251">設計器支援不適用於嵌套母版頁。</span><span class="sxs-lookup"><span data-stu-id="52dec-251">Designer support is not available for nested master pages.</span></span> <span data-ttu-id="52dec-252">使用嵌套母版進行開發時,需要使用源視圖。</span><span class="sxs-lookup"><span data-stu-id="52dec-252">When you are developing using nested masters, you will need to use source view.</span></span>

<span data-ttu-id="52dec-253">此視頻顯示了使用嵌套母版頁的演練。</span><span class="sxs-lookup"><span data-stu-id="52dec-253">This video shows a walkthrough of using nested master pages.</span></span>

![](master-pages/_static/image1.png)

[<span data-ttu-id="52dec-254">開啟全螢幕視訊</span><span class="sxs-lookup"><span data-stu-id="52dec-254">Open Full-Screen Video</span></span>](master-pages/_static/nested1.wmv)

![選擇母版頁](master-pages/_static/image4.jpg)

<span data-ttu-id="52dec-256">**圖 8**: 選擇母版頁</span><span class="sxs-lookup"><span data-stu-id="52dec-256">**Figure 8**: Selecting a Master Page</span></span>
