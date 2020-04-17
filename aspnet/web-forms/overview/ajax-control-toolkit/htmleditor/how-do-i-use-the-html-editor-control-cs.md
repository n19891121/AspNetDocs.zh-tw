---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
title: 如何使用 HTML 編輯器控制項? (C#) |微軟文件
author: rick-anderson
description: HTMLEditor 是 ASP.NET AJAX 控制件,允許您透過工具列中的按鈕輕鬆建立和編輯 HTML 內容。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: f47e6224-c2e5-4472-b069-b6c7b6115200
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
msc.type: authoredcontent
ms.openlocfilehash: eb3a87f914c24ada52ebb5a315a7e242e96158f7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543115"
---
# <a name="how-do-i-use-the-html-editor-control-c"></a><span data-ttu-id="145c5-104">如何使用 HTML 編輯器控制項?</span><span class="sxs-lookup"><span data-stu-id="145c5-104">How do I use the HTML Editor Control?</span></span> <span data-ttu-id="145c5-105">(C#)</span><span class="sxs-lookup"><span data-stu-id="145c5-105">(C#)</span></span>

<span data-ttu-id="145c5-106">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="145c5-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="145c5-107">HTMLEditor 是 ASP.NET AJAX 控制件,允許您透過工具列中的按鈕輕鬆建立和編輯 HTML 內容。</span><span class="sxs-lookup"><span data-stu-id="145c5-107">HTMLEditor is an ASP.NET AJAX Control that allows you to easily create and edit HTML content via buttons in a toolbar.</span></span>

<span data-ttu-id="145c5-108">本教學的目標是為您提供 AJAX 控制工具套件中包含的 HTML 編輯器控制項的概述。</span><span class="sxs-lookup"><span data-stu-id="145c5-108">The goal of this tutorial is to provide you with an overview of the HTML Editor control included with the AJAX Control Toolkit.</span></span> <span data-ttu-id="145c5-109">HTML 編輯器包括用於更改字型大小、選擇字型、更改背景顏色、修改前景顏色、添加連結、添加圖像、更改文本對齊以及執行剪切、複製和粘貼操作的選項(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="145c5-109">The HTML Editor includes options for changing font size, selecting a font, changing background color, modifying the foreground color, adding links, adding images, changing text alignment, and performing cut, copy, and paste operations (see Figure 1).</span></span>

<span data-ttu-id="145c5-110">[![HTML 編輯器](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="145c5-110">[![The HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="145c5-111">**圖 01**: HTML 編輯器([按下以檢視全尺寸影像](how-do-i-use-the-html-editor-control-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="145c5-111">**Figure 01**: The HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image2.png))</span></span>

<span data-ttu-id="145c5-112">HTML 編輯器允許您使用設計模式輸入內容,也可以直接輸入 HTML。</span><span class="sxs-lookup"><span data-stu-id="145c5-112">The HTML editor enables you to enter content using a design mode or you can enter HTML directly.</span></span> <span data-ttu-id="145c5-113">此外,您還可以提供預覽 HTML 內容的選項(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="145c5-113">You also are provided with the option to preview your HTML content (see Figure 2).</span></span>

<span data-ttu-id="145c5-114">[![設計、HTML 和預覽按鈕](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="145c5-114">[![Design, HTML, and Preview buttons](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)</span></span>

<span data-ttu-id="145c5-115">**圖 02**:設計、HTML 和預覽按鈕([按下以檢視全尺寸影像](how-do-i-use-the-html-editor-control-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="145c5-115">**Figure 02**: Design, HTML, and Preview buttons([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image4.png))</span></span>

<span data-ttu-id="145c5-116">在本教學中,您將瞭解如何顯示 HTML 編輯器、如何自訂 HTML 編輯器中顯示的工具列按鈕以及如何避免跨網站腳稿攻擊。</span><span class="sxs-lookup"><span data-stu-id="145c5-116">In this tutorial, you learn how to display the HTML Editor, how to customize the toolbar buttons that appear in the HTML Editor, and how to avoid Cross-Site Scripting Attacks.</span></span>

## <a name="displaying-the-html-editor"></a><span data-ttu-id="145c5-117">顯示 HTML 編輯器</span><span class="sxs-lookup"><span data-stu-id="145c5-117">Displaying the HTML Editor</span></span>

<span data-ttu-id="145c5-118">在ASP.NET頁中使用 HTML 編輯器之前,必須先向該頁添加文本管理器控制項。</span><span class="sxs-lookup"><span data-stu-id="145c5-118">Before you can use the HTML Editor in an ASP.NET page, you must first add a ScriptManager control to the page.</span></span> <span data-ttu-id="145c5-119">文稿管理器控制件位於可視化工作室/可視化 Web 開發人員快速工具箱中的 AJAX 擴充選項卡下方。</span><span class="sxs-lookup"><span data-stu-id="145c5-119">The ScriptManager control is located beneath the AJAX Extensions tab in the Visual Studio/Visual Web Developer Express toolbox.</span></span>

<span data-ttu-id="145c5-120">您應該在頁面的任何其他控制項之前將腳本管理器控制件放在頁面頂部。</span><span class="sxs-lookup"><span data-stu-id="145c5-120">You should place the ScriptManager control at the top of the page before any other controls on the page.</span></span> <span data-ttu-id="145c5-121">例如,您可以將它放在打開的伺服器端&lt;窗&gt;體 標記的下方。</span><span class="sxs-lookup"><span data-stu-id="145c5-121">For example, you can place it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="145c5-122">HTML 編輯器控制件與 AJAX 控制件工具套件控制件的其餘部分一起位於工具箱中。</span><span class="sxs-lookup"><span data-stu-id="145c5-122">The HTML Editor control is located in the toolbox with the rest of the AJAX Control Toolkit controls.</span></span> <span data-ttu-id="145c5-123">它被命名為編輯器控制件(參見圖 3)。</span><span class="sxs-lookup"><span data-stu-id="145c5-123">It is named the Editor control (see Figure 3).</span></span>

<span data-ttu-id="145c5-124">[![HTML 編輯器控制項](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="145c5-124">[![The HTML Editor control](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)</span></span>

<span data-ttu-id="145c5-125">**圖 03**: HTML 編輯器控制件([按下以檢視全尺寸影像](how-do-i-use-the-html-editor-control-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="145c5-125">**Figure 03**: The HTML Editor control([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image6.png))</span></span>

<span data-ttu-id="145c5-126">將 HTML 編輯器拖到頁面上後,可以在屬性表中設置其屬性。</span><span class="sxs-lookup"><span data-stu-id="145c5-126">After you drag the HTML Editor onto a page, you can set its properties in the property sheet.</span></span> <span data-ttu-id="145c5-127">例如,您通常要設置"寬度"和"高度"屬性。</span><span class="sxs-lookup"><span data-stu-id="145c5-127">For example, you normally want to set the Width and Height properties.</span></span> <span data-ttu-id="145c5-128">清單 1 包含包含 HTML 編輯器的 ASP.NET 頁的來源。</span><span class="sxs-lookup"><span data-stu-id="145c5-128">Listing 1 contains the source for an ASP.NET page that contains an HTML editor.</span></span>

<span data-ttu-id="145c5-129">**清單 1 - 簡單編輯器.aspx**</span><span class="sxs-lookup"><span data-stu-id="145c5-129">**Listing 1 - SimpleEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

<span data-ttu-id="145c5-130">清單1中的頁面包含 HTML 編輯器控制件、按鈕控制項和文字控制元件。</span><span class="sxs-lookup"><span data-stu-id="145c5-130">The page in Listing 1 contains an HTML Editor control, a Button control, and a Literal control.</span></span> <span data-ttu-id="145c5-131">按下這個按鈕時,HTML 編輯器的內容將顯示在「文字」控制件中(參見圖 4)。</span><span class="sxs-lookup"><span data-stu-id="145c5-131">When you click the button, the contents of the HTML Editor appear in the Literal control (see Figure 4).</span></span>

<span data-ttu-id="145c5-132">[![使用 HTML 編輯器提交表單](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="145c5-132">[![Submitting a form with an HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)</span></span>

<span data-ttu-id="145c5-133">**圖 04**: 提交含有 HTML 編輯器的表單([按下以檢視全尺寸影像](how-do-i-use-the-html-editor-control-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="145c5-133">**Figure 04**: Submitting a form with an HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image8.png))</span></span>

<span data-ttu-id="145c5-134">HTML 編輯器內容屬性用於檢索輸入到 HTML 編輯器中的 HTML 內容。</span><span class="sxs-lookup"><span data-stu-id="145c5-134">The HTML Editor Content property is used to retrieve the HTML content entered into the HTML Editor.</span></span> <span data-ttu-id="145c5-135">請注意,此 HTML 內容可能包含 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="145c5-135">Be aware that this HTML content can contain JavaScript.</span></span> <span data-ttu-id="145c5-136">在下一節中,我們將討論如何防止 JAVAScript 注入攻擊。</span><span class="sxs-lookup"><span data-stu-id="145c5-136">In the next section, we discuss how you can prevent JavaScript Injection Attacks.</span></span>

## <a name="customizing-the-html-editor-toolbar"></a><span data-ttu-id="145c5-137">自訂 HTML 編輯器工具列</span><span class="sxs-lookup"><span data-stu-id="145c5-137">Customizing the HTML Editor Toolbar</span></span>

<span data-ttu-id="145c5-138">您可以準確自定義編輯器中顯示的按鈕。</span><span class="sxs-lookup"><span data-stu-id="145c5-138">You can customize exactly which buttons appear in the editor.</span></span> <span data-ttu-id="145c5-139">例如,您可能希望刪除 HTML 選項卡,以防止使用者將 HTML 編輯器切換到 HTML 模式。</span><span class="sxs-lookup"><span data-stu-id="145c5-139">For example, you might want to remove the HTML tab to prevent users from switching the HTML Editor into HTML mode.</span></span> <span data-ttu-id="145c5-140">或者,您可能希望刪除字體大小下拉清單,以防止使用者在論壇消息帖子中創建過大的文本(參見圖 5)。</span><span class="sxs-lookup"><span data-stu-id="145c5-140">Or, you might want to remove the font size dropdown list to prevent users from creating overly large text in a forum message post (see Figure 5).</span></span>

<span data-ttu-id="145c5-141">[![自訂 HTML 編輯器](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="145c5-141">[![A customized HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)</span></span>

<span data-ttu-id="145c5-142">**圖 05**: 自訂 HTML 編輯器([按下以檢視全尺寸影像](how-do-i-use-the-html-editor-control-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="145c5-142">**Figure 05**: A customized HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image10.png))</span></span>

<span data-ttu-id="145c5-143">通過從基本編輯器類派生新的 HTML 編輯器來自定義工具列按鈕。</span><span class="sxs-lookup"><span data-stu-id="145c5-143">You customize the toolbar buttons by deriving a new HTML Editor from the base Editor class.</span></span> <span data-ttu-id="145c5-144">例如,清單 2 中的自定義編輯器僅包含粗體和斜體工具列按鈕。</span><span class="sxs-lookup"><span data-stu-id="145c5-144">For example, the custom editor in Listing 2 only contains toolbar buttons for bold and italic.</span></span> <span data-ttu-id="145c5-145">所有其他工具列按鈕已被刪除。</span><span class="sxs-lookup"><span data-stu-id="145c5-145">All other toolbar buttons have been removed.</span></span> <span data-ttu-id="145c5-146">此外,HTML 選項卡已從編輯器的底部刪除(但"設計和預覽"選項卡仍然存在)。</span><span class="sxs-lookup"><span data-stu-id="145c5-146">Furthermore, the HTML tab has been removed from the bottom of the editor (but the Design and Preview tabs are still there).</span></span>

<span data-ttu-id="145c5-147">**清單2\_- 應用程式代碼_自訂編輯器.cs**</span><span class="sxs-lookup"><span data-stu-id="145c5-147">**Listing 2 - App\_Code\CustomEditor.cs**</span></span>

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

<span data-ttu-id="145c5-148">您必須將清單 2 中的類新增\_到應用程式碼資料夾,以便自動編譯該類。</span><span class="sxs-lookup"><span data-stu-id="145c5-148">You must add the class in Listing 2 to your App\_Code folder so that the class will be compiled automatically.</span></span> <span data-ttu-id="145c5-149">如果網站中\_不存在應用代碼資料夾,則只需添加該資料夾即可。</span><span class="sxs-lookup"><span data-stu-id="145c5-149">If the App\_Code folder does not exist in your website then you can simply add the folder.</span></span>

<span data-ttu-id="145c5-150">創建自訂編輯器後,可以將其添加到ASP.NET頁,其方式與添加普通 HTML 編輯器的方式相同(請參閱清單 3)。</span><span class="sxs-lookup"><span data-stu-id="145c5-150">After you create a custom editor, you can add it to an ASP.NET page in the same way as you add the normal HTML Editor (see Listing 3).</span></span>

<span data-ttu-id="145c5-151">**清單3 - 顯示自訂編輯器.aspx**</span><span class="sxs-lookup"><span data-stu-id="145c5-151">**Listing 3 - ShowCustomEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a><span data-ttu-id="145c5-152">避免跨網站文稿 (XSS) 攻擊</span><span class="sxs-lookup"><span data-stu-id="145c5-152">Avoiding Cross-Site Scripting (XSS) Attacks</span></span>

<span data-ttu-id="145c5-153">每當您接受使用者的輸入,並在網站上重新顯示該輸入時,您都有可能將網站打開以進行跨網站腳本 (XSS) 攻擊。</span><span class="sxs-lookup"><span data-stu-id="145c5-153">Whenever you accept input from a user, and redisplay that input on your website, you potentially open your website to Cross-Site Scripting (XSS) Attacks.</span></span> <span data-ttu-id="145c5-154">理論上,惡意駭客可以提交 JAVAScript 代碼,這些代碼在重新顯示輸入時將執行。</span><span class="sxs-lookup"><span data-stu-id="145c5-154">In theory, a malicious hacker could submit JavaScript code that gets executed when the input is redisplayed.</span></span> <span data-ttu-id="145c5-155">JavaScript 可用於竊取使用者密碼或其他敏感資訊。</span><span class="sxs-lookup"><span data-stu-id="145c5-155">The JavaScript could be used to steal user passwords or other sensitive information.</span></span>

<span data-ttu-id="145c5-156">通常,在網頁中顯示之前,可以通過 HTML 編碼從使用者檢索的任何輸入來擊敗 XSS 攻擊。</span><span class="sxs-lookup"><span data-stu-id="145c5-156">Normally, you can defeat XSS attacks by HTML encoding whatever input you retrieve from a user before displaying it in a web page.</span></span> <span data-ttu-id="145c5-157">但是,HTML 編碼 HTML 編輯器的輸出不僅&lt;會編&gt;碼 文本標記,還會對所有 HTML 標記進行編碼。</span><span class="sxs-lookup"><span data-stu-id="145c5-157">However, HTML encoding the output of the HTML Editor would not only encode &lt;script&gt; tags, it would also encode all HTML tags.</span></span> <span data-ttu-id="145c5-158">換句話說,您將丟失所有格式,如字型類型、字體大小和背景顏色。</span><span class="sxs-lookup"><span data-stu-id="145c5-158">In other words, you would lose all of the formatting such as the font type, font size, and background color.</span></span>

<span data-ttu-id="145c5-159">如果要從使用者收集敏感資訊(如密碼、信用卡號碼和社會保險號),則不應顯示使用 HTML 編輯器從使用者檢索的未編碼內容。</span><span class="sxs-lookup"><span data-stu-id="145c5-159">If you are collecting sensitive information from your users -- such as passwords, credit-card numbers, and social security numbers - then you should not display un-encoded content that you retrieve from a user with the HTML Editor.</span></span> <span data-ttu-id="145c5-160">僅當您未重新播放 HTML 內容或受信任方向您的網站提交 HTML 內容的情況時,才應使用 HTML 編輯器。</span><span class="sxs-lookup"><span data-stu-id="145c5-160">You should use the HTML Editor only in situations in which you are not redisplaying the HTML content, or the HTML content is being submitted to your website by a trusted party.</span></span>

<span data-ttu-id="145c5-161">例如,假設您正在創建一個博客應用程式。</span><span class="sxs-lookup"><span data-stu-id="145c5-161">Imagine, for example, that you are creating a blog application.</span></span> <span data-ttu-id="145c5-162">在這種情況下,在撰寫部落格文章時使用 HTML 編輯器是有意義的。</span><span class="sxs-lookup"><span data-stu-id="145c5-162">In this situation, it makes sense to use the HTML Editor when composing blog posts.</span></span> <span data-ttu-id="145c5-163">您是唯一提交博客文章的人,而且,大概,您可以相信自己不會提交惡意的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="145c5-163">You are the only one who submits a blog post and, presumably, you can trust yourself not to submit malicious JavaScript.</span></span> <span data-ttu-id="145c5-164">但是,在允許匿名使用者發表評論時,使用 HTML 編輯器是沒有意義的。</span><span class="sxs-lookup"><span data-stu-id="145c5-164">However, it does not make sense to use the HTML Editor when allowing anonymous users to post comments.</span></span> <span data-ttu-id="145c5-165">在使用者提交敏感資訊(如密碼)時,應特別小心。</span><span class="sxs-lookup"><span data-stu-id="145c5-165">You should be especially careful in situations in which users submit sensitive information such as passwords.</span></span> <span data-ttu-id="145c5-166">惡意使用者可能會發佈包含用於竊取密碼的 JavaScript 的註釋。</span><span class="sxs-lookup"><span data-stu-id="145c5-166">Potentially, a malicious user could post a comment that contains the right JavaScript for stealing a password.</span></span>

## <a name="summary"></a><span data-ttu-id="145c5-167">總結</span><span class="sxs-lookup"><span data-stu-id="145c5-167">Summary</span></span>

<span data-ttu-id="145c5-168">在本教學中,您得到了 AJAX 控制工具套件中包含的 HTML 編輯器控制項的簡要概述。</span><span class="sxs-lookup"><span data-stu-id="145c5-168">In this tutorial, you were provided with a brief overview of the HTML Editor control included in the AJAX Control Toolkit.</span></span> <span data-ttu-id="145c5-169">您學習了如何使用 HTML 編輯器從使用者那裡接受豐富內容並將內容提交到伺服器。</span><span class="sxs-lookup"><span data-stu-id="145c5-169">You learned how to use the HTML Editor to accept rich content from a user and submit the content to the server.</span></span> <span data-ttu-id="145c5-170">我們還討論了如何自定義 HTML 編輯器顯示的工具列按鈕。</span><span class="sxs-lookup"><span data-stu-id="145c5-170">We also discussed how you can customize the toolbar buttons that are displayed by the HTML Editor.</span></span> <span data-ttu-id="145c5-171">最後,您學習了在使用 HTML 編輯器接受潛在的惡意輸入時,如何避免跨網站腳本攻擊。</span><span class="sxs-lookup"><span data-stu-id="145c5-171">Finally, you learned how to avoid Cross-Site Scripting Attacks when using the HTML Editor to accept potentially malicious input.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="145c5-172">下一步</span><span class="sxs-lookup"><span data-stu-id="145c5-172">Next</span></span>](how-do-i-use-the-html-editor-control-vb.md)
