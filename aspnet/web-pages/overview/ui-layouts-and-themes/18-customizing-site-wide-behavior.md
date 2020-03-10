---
uid: web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
title: 針對 ASP.NET Web Pages （Razor）網站自訂全網站行為 |Microsoft Docs
author: Rick-Anderson
description: 本章說明如何將設定設為整個網站或整個資料夾，而不只是頁面。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: e158bed7-226f-4275-b02e-7553bd58c669
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
msc.type: authoredcontent
ms.openlocfilehash: f05e05f725d9209bce283ce18659ae5efe4de2ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634621"
---
# <a name="customizing-site-wide-behavior-for-aspnet-web-pages-razor-sites"></a><span data-ttu-id="5d917-103">針對 ASP.NET Web Pages （Razor）網站自訂全網站行為</span><span class="sxs-lookup"><span data-stu-id="5d917-103">Customizing Site-Wide Behavior for ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="5d917-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5d917-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="5d917-105">本文說明如何在 ASP.NET Web Pages （Razor）網站中建立頁面的網站端設定。</span><span class="sxs-lookup"><span data-stu-id="5d917-105">This article explains how to make site-side settings for pages in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="5d917-106">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="5d917-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="5d917-107">如何執行程式碼，讓您設定網站中所有頁面的值（全域值或 helper 設定）。</span><span class="sxs-lookup"><span data-stu-id="5d917-107">How to run code that lets you set values (global values or helper settings) for all pages in a site.</span></span>
> - <span data-ttu-id="5d917-108">如何執行程式碼，讓您設定資料夾中所有頁面的值。</span><span class="sxs-lookup"><span data-stu-id="5d917-108">How to run code that lets you set values for all pages in a folder.</span></span>
> - <span data-ttu-id="5d917-109">如何在頁面載入之前和之後執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="5d917-109">How to run code before and after a page loads.</span></span>
> - <span data-ttu-id="5d917-110">如何將錯誤傳送至中央錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-110">How to send errors to a central error page.</span></span>
> - <span data-ttu-id="5d917-111">如何將驗證新增至資料夾中的所有頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-111">How to add authentication to all pages in a folder.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5d917-112">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="5d917-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="5d917-113">ASP.NET Web Pages （Razor）2</span><span class="sxs-lookup"><span data-stu-id="5d917-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="5d917-114">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="5d917-114">WebMatrix 3</span></span>
> - <span data-ttu-id="5d917-115">ASP.NET Web helper 程式庫（NuGet 套件）</span><span class="sxs-lookup"><span data-stu-id="5d917-115">ASP.NET Web Helpers Library (NuGet package)</span></span>
>   
> 
> <span data-ttu-id="5d917-116">本教學課程也適用于 ASP.NET Web Pages 3 和 Visual Studio 2013 （或 Visual Studio Express 2013 for Web），不同之處在于您無法使用 ASP.NET Web helper 程式庫。</span><span class="sxs-lookup"><span data-stu-id="5d917-116">This tutorial also works with ASP.NET Web Pages 3 and Visual Studio 2013 (or Visual Studio Express 2013 for Web), except you cannot use the ASP.NET Web Helpers Library.</span></span>

<a id="Adding_Website_Startup_Code"></a>
## <a name="adding-website-startup-code-for-aspnet-web-pages"></a><span data-ttu-id="5d917-117">新增 ASP.NET Web Pages 的網站啟動程式碼</span><span class="sxs-lookup"><span data-stu-id="5d917-117">Adding Website Startup Code for ASP.NET Web Pages</span></span>

<span data-ttu-id="5d917-118">針對您在 ASP.NET Web Pages 中撰寫的大部分程式碼，個別頁面可以包含該頁面所需的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="5d917-118">For much of the code that you write in ASP.NET Web Pages, an individual page can contain all the code that's required for that page.</span></span> <span data-ttu-id="5d917-119">例如，如果頁面傳送電子郵件訊息，則可以將該作業的所有程式碼放在單一頁面中。</span><span class="sxs-lookup"><span data-stu-id="5d917-119">For example, if a page sends an email message, it's possible to put all the code for that operation in a single page.</span></span> <span data-ttu-id="5d917-120">這可包含程式碼，以初始化傳送電子郵件（也就是 SMTP 伺服器）的設定，以及傳送電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="5d917-120">This can include the code to initialize the settings for sending email (that is, for the SMTP server) and for sending the email message.</span></span>

<span data-ttu-id="5d917-121">不過，在某些情況下，您可能會想要在網站上的任何頁面執行之前執行一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="5d917-121">However, in some situations, you might want to run some code before any page on the site runs.</span></span> <span data-ttu-id="5d917-122">這適用于設定可在網站任何地方使用的值（稱為「*全域值*」）。例如，某些協助程式會要求您提供電子郵件設定或帳戶金鑰之類的值。</span><span class="sxs-lookup"><span data-stu-id="5d917-122">This is useful for setting values that can be used anywhere in the site (referred to as *global values*.) For example, some helpers require you to provide values like email settings or account keys.</span></span> <span data-ttu-id="5d917-123">將這些設定保留在全域值中是很方便的。</span><span class="sxs-lookup"><span data-stu-id="5d917-123">It can be handy to keep these settings in global values.</span></span>

<span data-ttu-id="5d917-124">若要這麼做，您可以在網站的根目錄中建立名為 *\_AppStart*的頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-124">You can do this by creating a page named *\_AppStart.cshtml* in the root of the site.</span></span> <span data-ttu-id="5d917-125">如果此頁面存在，則會在第一次要求網站中的任何頁面時執行。</span><span class="sxs-lookup"><span data-stu-id="5d917-125">If this page exists, it runs the first time any page in the site is requested.</span></span> <span data-ttu-id="5d917-126">因此，它是執行程式碼以設定全域值的好地方。</span><span class="sxs-lookup"><span data-stu-id="5d917-126">Therefore, it's a good place to run code to set global values.</span></span> <span data-ttu-id="5d917-127">（因為 *\_AppStart*的底線前置詞，ASP.NET 不會將頁面傳送至瀏覽器，即使使用者直接要求也一樣）。</span><span class="sxs-lookup"><span data-stu-id="5d917-127">(Because *\_AppStart.cshtml* has an underscore prefix, ASP.NET won't send the page to a browser even if users request it directly.)</span></span>

<span data-ttu-id="5d917-128">下圖顯示 [ *\_AppStart* ] 頁面的運作方式。</span><span class="sxs-lookup"><span data-stu-id="5d917-128">The following diagram shows how the *\_AppStart.cshtml* page works.</span></span> <span data-ttu-id="5d917-129">當要求傳入頁面時，如果這是網站中任何頁面的第一個要求，ASP.NET 會先檢查是否有 *\_AppStart. cshtml*頁面存在。</span><span class="sxs-lookup"><span data-stu-id="5d917-129">When a request comes in for a page, and if this is the first request for any page in the site, ASP.NET first checks whether a *\_AppStart.cshtml* page exists.</span></span> <span data-ttu-id="5d917-130">若是如此， *\_AppStart*中的任何程式碼都會執行，然後再執行要求的頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-130">If so, any code in the *\_AppStart.cshtml* page runs, and then the requested page runs.</span></span>

![[影像]](18-customizing-site-wide-behavior/_static/image1.jpg)

## <a name="setting-global-values-for-your-website"></a><span data-ttu-id="5d917-132">為您的網站設定全域值</span><span class="sxs-lookup"><span data-stu-id="5d917-132">Setting Global Values for Your Website</span></span>

1. <span data-ttu-id="5d917-133">在 WebMatrix 網站的根資料夾中，建立名為 *\_AppStart*的檔案。</span><span class="sxs-lookup"><span data-stu-id="5d917-133">In the root folder of a WebMatrix website, create a file named *\_AppStart.cshtml*.</span></span> <span data-ttu-id="5d917-134">檔案必須位於網站的根目錄中。</span><span class="sxs-lookup"><span data-stu-id="5d917-134">The file must be in the root of the site.</span></span>
2. <span data-ttu-id="5d917-135">以下列內容取代現有的內容：</span><span class="sxs-lookup"><span data-stu-id="5d917-135">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample1.cshtml)]

    <span data-ttu-id="5d917-136">此程式碼會將值儲存在 `AppState` 字典中，這會自動提供給網站中的所有頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-136">This code stores a value in the `AppState` dictionary, which is automatically available to all pages in the site.</span></span> <span data-ttu-id="5d917-137">請注意， *\_AppStart*檔案中沒有任何標記。</span><span class="sxs-lookup"><span data-stu-id="5d917-137">Notice that the *\_AppStart.cshtml* file does not have any markup in it.</span></span> <span data-ttu-id="5d917-138">頁面將會執行程式碼，然後重新導向至原先要求的頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-138">The page will run the code and then redirect to the page that was originally requested.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5d917-139">當您將程式碼放在 *\_AppStart*檔時，請務必小心。</span><span class="sxs-lookup"><span data-stu-id="5d917-139">Be careful when you put code in the *\_AppStart.cshtml* file.</span></span> <span data-ttu-id="5d917-140">如果 *\_AppStart*檔的程式碼中發生任何錯誤，網站就不會啟動。</span><span class="sxs-lookup"><span data-stu-id="5d917-140">If any errors occur in code in the *\_AppStart.cshtml* file, the website won't start.</span></span>
3. <span data-ttu-id="5d917-141">在根資料夾中，建立名為*AppName. cshtml*的新頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-141">In the root folder, create a new page named *AppName.cshtml*.</span></span>
4. <span data-ttu-id="5d917-142">將預設標記和程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="5d917-142">Replace the default markup and code with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample2.html)]

    <span data-ttu-id="5d917-143">此程式碼會從您在 [ *\_AppStart* ] 頁面中設定的 `AppState` 物件中，提取值。</span><span class="sxs-lookup"><span data-stu-id="5d917-143">This code extracts the value from the `AppState` object that you set in the *\_AppStart.cshtml* page.</span></span>
5. <span data-ttu-id="5d917-144">在瀏覽器中執行*AppName. cshtml*頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-144">Run the *AppName.cshtml* page in a browser.</span></span> <span data-ttu-id="5d917-145">（在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）此頁面會顯示全域值。</span><span class="sxs-lookup"><span data-stu-id="5d917-145">(Make sure the page is selected in the **Files** workspace before you run it.) The page displays the global value.</span></span> 

    ![[影像]](18-customizing-site-wide-behavior/_static/image2.jpg)

<a id="Setting_Values_For_Helpers"></a>
## <a name="setting-values-for-helpers"></a><span data-ttu-id="5d917-147">設定 helper 的值</span><span class="sxs-lookup"><span data-stu-id="5d917-147">Setting Values for Helpers</span></span>

<span data-ttu-id="5d917-148">*\_AppStart*的好用，就是為您在網站中使用且必須初始化的 helper 設定值。</span><span class="sxs-lookup"><span data-stu-id="5d917-148">A good use for the *\_AppStart.cshtml* file is to set values for helpers that you use in your site and that have to be initialized.</span></span> <span data-ttu-id="5d917-149">一般範例包括 `WebMail` helper 的電子郵件設定，以及 `ReCaptcha` 協助程式的私用和公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d917-149">Typical examples are email settings for the `WebMail` helper and the private and public keys for the `ReCaptcha` helper.</span></span> <span data-ttu-id="5d917-150">在這種情況下，您可以在 *\_AppStart*中設定值一次，然後在您的網站中為所有頁面設定它們。</span><span class="sxs-lookup"><span data-stu-id="5d917-150">In cases like these, you can set the values once in the *\_AppStart.cshtml* and then they're already set for all the pages in your site.</span></span>

<span data-ttu-id="5d917-151">此程式說明如何全域設定 `WebMail` 設定。</span><span class="sxs-lookup"><span data-stu-id="5d917-151">This procedure shows you how to set `WebMail` settings globally.</span></span> <span data-ttu-id="5d917-152">（如需有關使用 `WebMail` 協助程式的詳細資訊，請參閱[將電子郵件新增至 ASP.NET Web Pages 網站](../getting-started/11-adding-email-to-your-web-site.md)）。</span><span class="sxs-lookup"><span data-stu-id="5d917-152">(For more information about using the `WebMail` helper, see [Adding Email to an ASP.NET Web Pages Site](../getting-started/11-adding-email-to-your-web-site.md).)</span></span>

1. <span data-ttu-id="5d917-153">如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未新增）。</span><span class="sxs-lookup"><span data-stu-id="5d917-153">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="5d917-154">如果您還沒有 *\_AppStart. cshtml*檔案，請在網站的根資料夾中建立名為 *\_AppStart*的檔案。</span><span class="sxs-lookup"><span data-stu-id="5d917-154">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
3. <span data-ttu-id="5d917-155">將下列 `WebMail` 設定新增至 *\_AppStart. cshtml*檔案：</span><span class="sxs-lookup"><span data-stu-id="5d917-155">Add the following `WebMail` settings to the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample3.cshtml?highlight=2-7)]

    <span data-ttu-id="5d917-156">修改程式碼中的下列電子郵件相關設定：</span><span class="sxs-lookup"><span data-stu-id="5d917-156">Modify the following email related settings in the code:</span></span>

   - <span data-ttu-id="5d917-157">將 `your-SMTP-host` 設定為您可以存取的 SMTP 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="5d917-157">Set `your-SMTP-host` to the name of the SMTP server that you have access to.</span></span>
   - <span data-ttu-id="5d917-158">將 `your-user-name-here` 設定為 SMTP 伺服器帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="5d917-158">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
   - <span data-ttu-id="5d917-159">將 `your-account-password` 設定為 SMTP 伺服器帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="5d917-159">Set `your-account-password` to the password for your SMTP server account.</span></span>
   - <span data-ttu-id="5d917-160">將 `your-email-address-here` 設定為您自己的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="5d917-160">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="5d917-161">這是傳送訊息的來源電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="5d917-161">This is the email address that the message is sent from.</span></span> <span data-ttu-id="5d917-162">（有些電子郵件提供者不會讓您指定不同的 `From` 位址，而且會使用您的使用者名稱作為 `From` 位址）。</span><span class="sxs-lookup"><span data-stu-id="5d917-162">(Some email providers don't let you specify a different `From` address and will use your user name as the `From` address.)</span></span>

     <span data-ttu-id="5d917-163">如需 SMTP 設定的詳細資訊，請參閱在[ASP.NET Web Pages （razor）疑難排解指南](https://go.microsoft.com/fwlink/?LinkId=253001)中[從 ASP.NET Web Pages （razor）網站傳送電子郵件](https://go.microsoft.com/fwlink/?LinkID=202899)和傳送電子郵件的[問題](https://go.microsoft.com/fwlink/?LinkId=253001#email)一文中的[設定電子郵件設定](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings)。</span><span class="sxs-lookup"><span data-stu-id="5d917-163">For more information about SMTP settings, see [Configuring Email Settings](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings) in the article [Sending Email from an ASP.NET Web Pages (Razor) Site](https://go.microsoft.com/fwlink/?LinkID=202899) and [Issues with Sending Email](https://go.microsoft.com/fwlink/?LinkId=253001#email) in the [ASP.NET Web Pages (Razor) Troubleshooting Guide](https://go.microsoft.com/fwlink/?LinkId=253001).</span></span>
4. <span data-ttu-id="5d917-164">儲存 *\_AppStart* ，並將它關閉。</span><span class="sxs-lookup"><span data-stu-id="5d917-164">Save the *\_AppStart.cshtml* file and close it.</span></span>
5. <span data-ttu-id="5d917-165">在網站的根資料夾中，建立名為*TestEmail*的新頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-165">In the root folder of a website, create new page named *TestEmail.cshtml*.</span></span>
6. <span data-ttu-id="5d917-166">以下列內容取代現有的內容：</span><span class="sxs-lookup"><span data-stu-id="5d917-166">Replace the existing content with the following:</span></span> 

     [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample4.cshtml)]
7. <span data-ttu-id="5d917-167">在瀏覽器中執行*TestEmail。*</span><span class="sxs-lookup"><span data-stu-id="5d917-167">Run the *TestEmail.cshtml* page in a browser.</span></span>
8. <span data-ttu-id="5d917-168">填寫欄位將電子郵件傳送給自己，然後按一下 [**傳送**]。</span><span class="sxs-lookup"><span data-stu-id="5d917-168">Fill in the fields to send yourself an email message and then click **Send**.</span></span>
9. <span data-ttu-id="5d917-169">請檢查您的電子郵件，以確定您已取得該訊息。</span><span class="sxs-lookup"><span data-stu-id="5d917-169">Check your email to make sure you've gotten the message.</span></span>

<span data-ttu-id="5d917-170">這個範例的重要部分是，您通常不會變更的設定（例如 SMTP 伺服器的名稱和電子郵件認證）會在 *\_AppStart. cshtml*檔案中設定。</span><span class="sxs-lookup"><span data-stu-id="5d917-170">The important part of this example is that the settings that you don't usually change — like the name of your SMTP server and your email credentials — are set in the *\_AppStart.cshtml* file.</span></span> <span data-ttu-id="5d917-171">如此一來，您就不需要在傳送電子郵件的每一頁中重新設定這些專案。</span><span class="sxs-lookup"><span data-stu-id="5d917-171">That way you don't need to set them again in each page where you send email.</span></span> <span data-ttu-id="5d917-172">（不過，如果基於某些原因而需要變更這些設定，您可以在頁面中個別加以設定）。在此頁面中，您只會設定通常會每次變更的值，例如收件者和電子郵件訊息的主體。</span><span class="sxs-lookup"><span data-stu-id="5d917-172">(Although if for some reason you need to change those settings, you can set them individually in a page.) In the page, you only set the values that typically change each time, like the recipient and the body of the email message.</span></span>

<a id="Running_Code_Before_and_After"></a>
## <a name="running-code-before-and-after-files-in-a-folder"></a><span data-ttu-id="5d917-173">在資料夾中的檔案前後執行程式碼</span><span class="sxs-lookup"><span data-stu-id="5d917-173">Running Code Before and After Files in a Folder</span></span>

<span data-ttu-id="5d917-174">就像您可以在網站執行的頁面之前，使用 *\_AppStart*來撰寫程式碼，您可以撰寫在執行特定資料夾中的任何頁面之前（和之後）執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="5d917-174">Just like you can use *\_AppStart.cshtml* to write code before pages in the site run, you can write code that runs before (and after) any page in a particular folder run.</span></span> <span data-ttu-id="5d917-175">這適用于針對資料夾中的所有頁面設定相同的版面配置頁，或在執行資料夾中的頁面之前，檢查使用者是否已登入的專案。</span><span class="sxs-lookup"><span data-stu-id="5d917-175">This is useful for things like setting the same layout page for all the pages in a folder, or for checking that a user is logged in before running a page in the folder.</span></span>

<span data-ttu-id="5d917-176">針對特定資料夾中的頁面，您可以在名為 *\_PageStart*的檔案中建立程式碼。</span><span class="sxs-lookup"><span data-stu-id="5d917-176">For pages in particular folders, you can create code in a file named *\_PageStart.cshtml*.</span></span> <span data-ttu-id="5d917-177">下圖顯示 [ *\_PageStart* ] 頁面的運作方式。</span><span class="sxs-lookup"><span data-stu-id="5d917-177">The following diagram shows how the *\_PageStart.cshtml* page works.</span></span> <span data-ttu-id="5d917-178">當頁面出現要求時，ASP.NET 會先檢查 *\_的 AppStart* ，然後執行該頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-178">When a request comes in for a page, ASP.NET first checks for a *\_AppStart.cshtml* page and runs that.</span></span> <span data-ttu-id="5d917-179">然後，ASP.NET 會檢查是否有 *\_PageStart* ，如果是，則會執行該頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-179">Then ASP.NET checks whether there's a *\_PageStart.cshtml* page, and if so, runs that.</span></span> <span data-ttu-id="5d917-180">然後，它會執行要求的頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-180">It then runs the requested page.</span></span>

<span data-ttu-id="5d917-181">在 *\_PageStart*  頁面中，您可以藉由包含 `RunPage` 方法，指定要在處理期間執行要求的頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-181">Inside the *\_PageStart.cshtml* page, you can specify where during processing you want the requested page to run by including a `RunPage` method.</span></span> <span data-ttu-id="5d917-182">這可讓您先執行程式碼，然後再執行要求的頁面，然後再進行一次。</span><span class="sxs-lookup"><span data-stu-id="5d917-182">This lets you run code before the requested page runs and then again after it.</span></span> <span data-ttu-id="5d917-183">如果您未包含 `RunPage`， *\_PageStart*中的所有程式碼都會執行，然後要求的網頁會自動執行。</span><span class="sxs-lookup"><span data-stu-id="5d917-183">If you don't include `RunPage`, all the code in *\_PageStart.cshtml* runs, and then the requested page runs automatically.</span></span>

![[影像]](18-customizing-site-wide-behavior/_static/image3.jpg)

<span data-ttu-id="5d917-185">ASP.NET 可讓您建立 *\_PageStart*的階層。</span><span class="sxs-lookup"><span data-stu-id="5d917-185">ASP.NET lets you create a hierarchy of *\_PageStart.cshtml* files.</span></span> <span data-ttu-id="5d917-186">您可以將 *\_PageStart*放在網站根目錄和任何子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="5d917-186">You can put a *\_PageStart.cshtml* file in the root of the site and in any subfolder.</span></span> <span data-ttu-id="5d917-187">當要求頁面時，\_在最上層的位置（最接近網站根目錄）執行的*PageStart*檔案，後面接著下一個子資料夾中的 *\_PageStart*檔，然後關閉子資料夾結構，直到要求到達包含所要求頁面的資料夾為止。</span><span class="sxs-lookup"><span data-stu-id="5d917-187">When a page is requested, the *\_PageStart.cshtml* file at the top-most level (nearest to the site root) runs, followed by the *\_PageStart.cshtml* file in the next subfolder, and so on down the subfolder structure until the request reaches the folder that contains the requested page.</span></span> <span data-ttu-id="5d917-188">當所有適用的 *\_PageStart*檔案都已執行之後，要求的頁面就會執行。</span><span class="sxs-lookup"><span data-stu-id="5d917-188">After all the applicable *\_PageStart.cshtml* files have run, the requested page runs.</span></span>

<span data-ttu-id="5d917-189">例如，您可能會有下列 *\_PageStart*的組合，以及*預設的 cshtml*檔案：</span><span class="sxs-lookup"><span data-stu-id="5d917-189">For example, you might have the following combination of *\_PageStart.cshtml* files and *Default.cshtml* file:</span></span>

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample5.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample6.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample7.cshtml)]

<span data-ttu-id="5d917-190">當您執行 */myfolder/default.cshtml*時，您會看到下列內容：</span><span class="sxs-lookup"><span data-stu-id="5d917-190">When you run */myfolder/default.cshtml*, you'll see the following:</span></span>

[!code-console[Main](18-customizing-site-wide-behavior/samples/sample8.cmd)]

## <a name="running-initialization-code-for-all-pages-in-a-folder"></a><span data-ttu-id="5d917-191">針對資料夾中的所有頁面執行初始化程式碼</span><span class="sxs-lookup"><span data-stu-id="5d917-191">Running Initialization Code for All Pages in a Folder</span></span>

<span data-ttu-id="5d917-192">*\_PageStart*的良好用法是針對單一資料夾中的所有檔案，初始化相同的版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="5d917-192">A good use for *\_PageStart.cshtml* files is to initialize the same layout page for all files in a single folder.</span></span>

1. <span data-ttu-id="5d917-193">在根資料夾中，建立名為*InitPages*的新資料夾。</span><span class="sxs-lookup"><span data-stu-id="5d917-193">In the root folder, create a new folder named *InitPages*.</span></span>
2. <span data-ttu-id="5d917-194">在網站的 [ *InitPages* ] 資料夾中，建立名為 *\_PageStart*的檔案，並將預設標記和程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="5d917-194">In the *InitPages* folder of your website, create a file named *\_PageStart.cshtml* and replace the default markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample9.cshtml)]
3. <span data-ttu-id="5d917-195">在網站的根目錄中，建立名為*Shared*的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5d917-195">In the root of the website, create a folder named *Shared*.</span></span>
4. <span data-ttu-id="5d917-196">在*共用*資料夾中，建立名為 *\_layout1.xml*的檔案，並將預設標記和程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="5d917-196">In the *Shared* folder, create a file named *\_Layout1.cshtml* and replace the default markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample10.cshtml)]
5. <span data-ttu-id="5d917-197">在*InitPages*資料夾中，建立名為*Content1*的檔案，並以下列內容取代現有的內容：</span><span class="sxs-lookup"><span data-stu-id="5d917-197">In the *InitPages* folder, create a file named *Content1.cshtml* and replace the existing content with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample11.html)]
6. <span data-ttu-id="5d917-198">在*InitPages*資料夾中，建立另一個名為*Content2*的檔案，並將預設標記取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="5d917-198">In the *InitPages* folder, create another file named *Content2.cshtml* and replace the default markup with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample12.html)]
7. <span data-ttu-id="5d917-199">在瀏覽器中執行*Content1。*</span><span class="sxs-lookup"><span data-stu-id="5d917-199">Run *Content1.cshtml* in a browser.</span></span> 

    ![[影像]](18-customizing-site-wide-behavior/_static/image4.jpg)

    <span data-ttu-id="5d917-201">當*Content1*在執行時，會 `Layout` 設定 *\_的 PageStart* ，同時將 `PageData["MyBackground"]` 設定為色彩。</span><span class="sxs-lookup"><span data-stu-id="5d917-201">When the *Content1.cshtml* page runs, the *\_PageStart.cshtml* file sets `Layout` and also sets `PageData["MyBackground"]` to a color.</span></span> <span data-ttu-id="5d917-202">在*Content1*中，會套用版面配置和色彩。</span><span class="sxs-lookup"><span data-stu-id="5d917-202">In *Content1.cshtml*, the layout and color are applied.</span></span>
8. <span data-ttu-id="5d917-203">在瀏覽器中顯示*Content2* 。</span><span class="sxs-lookup"><span data-stu-id="5d917-203">Display *Content2.cshtml* in a browser.</span></span> 

    <span data-ttu-id="5d917-204">版面配置相同，因為這兩個頁面都會使用與 *\_PageStart*中初始化的相同版面配置頁和色彩。</span><span class="sxs-lookup"><span data-stu-id="5d917-204">The layout is the same, because both pages use the same layout page and color as initialized in *\_PageStart.cshtml*.</span></span>

## <a name="using-_pagestartcshtml-to-handle-errors"></a><span data-ttu-id="5d917-205">使用 \_PageStart 來處理錯誤</span><span class="sxs-lookup"><span data-stu-id="5d917-205">Using \_PageStart.cshtml to Handle Errors</span></span>

<span data-ttu-id="5d917-206">*\_PageStart*的另一個好用方法，就是建立一個方式來處理資料夾中任何 *. cshtml*頁面可能發生的程式設計錯誤（例外狀況）。</span><span class="sxs-lookup"><span data-stu-id="5d917-206">Another good use for the *\_PageStart.cshtml* file is to create a way to handle programming errors (exceptions) that might occur in any *.cshtml* page in a folder.</span></span> <span data-ttu-id="5d917-207">這個範例會示範一種執行此動作的方式。</span><span class="sxs-lookup"><span data-stu-id="5d917-207">This example shows you one way to do this.</span></span>

1. <span data-ttu-id="5d917-208">在根資料夾中，建立名為*InitCatch*的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5d917-208">In the root folder, create a folder named *InitCatch*.</span></span>
2. <span data-ttu-id="5d917-209">在網站的*InitCatch*資料夾中，建立名為 *\_PageStart*的檔案，並將現有的標記和程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="5d917-209">In the *InitCatch* folder of your website, create a file named *\_PageStart.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample13.cshtml)]

    <span data-ttu-id="5d917-210">在此程式碼中，您會藉由呼叫 `try` 區塊內的 `RunPage` 方法，來嘗試明確執行要求的頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-210">In this code, you try running the requested page explicitly by calling the `RunPage` method inside a `try` block.</span></span> <span data-ttu-id="5d917-211">如果要求的頁面中發生任何程式設計錯誤，`catch` 區塊內的程式碼就會執行。</span><span class="sxs-lookup"><span data-stu-id="5d917-211">If any programming errors occur in the requested page, the code inside the `catch` block runs.</span></span> <span data-ttu-id="5d917-212">在此情況下，程式碼會重新導向至頁面（*錯誤. cshtml*），並將發生錯誤的檔案名傳遞為 URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="5d917-212">In this case, the code redirects to a page (*Error.cshtml*) and passes the name of the file that experienced the error as part of the URL.</span></span> <span data-ttu-id="5d917-213">（您很快就會建立此頁面）。</span><span class="sxs-lookup"><span data-stu-id="5d917-213">(You'll create the page shortly.)</span></span>
3. <span data-ttu-id="5d917-214">在您網站的*InitCatch*資料夾中，建立名為*Exception. cshtml*的檔案，並將現有的標記和程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="5d917-214">In the *InitCatch* folder of your website, create a file named *Exception.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample14.cshtml)]

    <span data-ttu-id="5d917-215">基於此範例的目的，您在此頁面中執行的動作，是藉由嘗試開啟不存在的資料庫檔案，而故意建立錯誤。</span><span class="sxs-lookup"><span data-stu-id="5d917-215">For purposes of this example, what you're doing in this page is deliberately creating an error by trying to open a database file that doesn't exist.</span></span>
4. <span data-ttu-id="5d917-216">在根資料夾中，建立名為*Error*的檔案，並將現有的標記和程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="5d917-216">In the root folder, create a file named *Error.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample15.html)]

    <span data-ttu-id="5d917-217">在此頁面中，運算式 `@Request["source"]` 會從 URL 取得值，並加以顯示。</span><span class="sxs-lookup"><span data-stu-id="5d917-217">In this page, the expression `@Request["source"]` gets the value out of the URL and displays it.</span></span>
5. <span data-ttu-id="5d917-218">在工具列中，按一下 [**儲存**]。</span><span class="sxs-lookup"><span data-stu-id="5d917-218">In the toolbar, click **Save**.</span></span>
6. <span data-ttu-id="5d917-219">在瀏覽器中執行*Exception. cshtml* 。</span><span class="sxs-lookup"><span data-stu-id="5d917-219">Run *Exception.cshtml* in a browser.</span></span> 

    ![[影像]](18-customizing-site-wide-behavior/_static/image5.jpg)

    <span data-ttu-id="5d917-221">因為在*Exception. cshtml*中發生錯誤， *\_PageStart*會重新導向至*錯誤的 cshtml*檔案，該檔案會顯示訊息。</span><span class="sxs-lookup"><span data-stu-id="5d917-221">Because an error occurs in *Exception.cshtml*, the *\_PageStart.cshtml* page redirects to the *Error.cshtml* file, which displays the message.</span></span>

    <span data-ttu-id="5d917-222">如需例外狀況的詳細資訊，請參閱[使用 Razor 語法進行 ASP.NET Web Pages 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkID=251587)。</span><span class="sxs-lookup"><span data-stu-id="5d917-222">For more information about exceptions, see [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=251587).</span></span>

<a id="Using__PageStart.cshtml_to_Restrict_Folder_Access"></a>
## <a name="using-_pagestartcshtml-to-restrict-folder-access"></a><span data-ttu-id="5d917-223">使用 \_PageStart 來限制資料夾存取</span><span class="sxs-lookup"><span data-stu-id="5d917-223">Using \_PageStart.cshtml to Restrict Folder Access</span></span>

<span data-ttu-id="5d917-224">您也可以使用 *\_PageStart*檔來限制資料夾中所有檔案的存取權。</span><span class="sxs-lookup"><span data-stu-id="5d917-224">You can also use the *\_PageStart.cshtml* file to restrict access to all the files in a folder.</span></span>

1. <span data-ttu-id="5d917-225">在 WebMatrix 中，使用 [**來自範本的網站**] 選項建立新的網站。</span><span class="sxs-lookup"><span data-stu-id="5d917-225">In WebMatrix, create a new website using the **Site From Template** option.</span></span>
2. <span data-ttu-id="5d917-226">從可用的範本中，選取 [**入門網站**]。</span><span class="sxs-lookup"><span data-stu-id="5d917-226">From the available templates, select **Starter Site**.</span></span>
3. <span data-ttu-id="5d917-227">在根資料夾中，建立名為*AuthenticatedContent*的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5d917-227">In the root folder, create a folder named *AuthenticatedContent*.</span></span>
4. <span data-ttu-id="5d917-228">在*AuthenticatedContent*資料夾中，建立名為 *\_PageStart*的檔案，並將現有的標記和程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="5d917-228">In the *AuthenticatedContent* folder, create a file named *\_PageStart.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample16.cshtml)]

    <span data-ttu-id="5d917-229">程式碼一開始會防止快取資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="5d917-229">The code starts by preventing all files in the folder from being cached.</span></span> <span data-ttu-id="5d917-230">（這是公用電腦等案例的必要項，您不想讓使用者的快取頁面供下一位使用者使用）。接下來，程式碼會判斷使用者是否已登入網站，然後才能查看資料夾中的任何頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-230">(This is required for scenarios like public computers, where you don't want one user's cached pages to be available to the next user.) Next, the code determines whether the user has signed in to the site before they can view any of the pages in the folder.</span></span> <span data-ttu-id="5d917-231">如果使用者未登入，則程式碼會重新導向至登入頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-231">If the user is not signed in, the code redirects to the login page.</span></span> <span data-ttu-id="5d917-232">如果您包含名為 `ReturnUrl`的查詢字串值，登入頁面可以將使用者傳回原先要求的頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-232">The login page can return the user to the page that was originally requested if you include a query string value named `ReturnUrl`.</span></span>
5. <span data-ttu-id="5d917-233">在*AuthenticatedContent*資料夾中建立名為*page. cshtml*的新頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-233">Create a new page in the *AuthenticatedContent* folder named *Page.cshtml*.</span></span>
6. <span data-ttu-id="5d917-234">將預設標記取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="5d917-234">Replace the default markup with the following:</span></span>  

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample17.cshtml)]
7. <span data-ttu-id="5d917-235">在瀏覽器中執行 *. cshtml* 。</span><span class="sxs-lookup"><span data-stu-id="5d917-235">Run *Page.cshtml* in a browser.</span></span> <span data-ttu-id="5d917-236">此程式碼會將您重新導向至登入頁面。</span><span class="sxs-lookup"><span data-stu-id="5d917-236">The code redirects you to a login page.</span></span> <span data-ttu-id="5d917-237">在登入之前，您必須先註冊。</span><span class="sxs-lookup"><span data-stu-id="5d917-237">You must register before logging in.</span></span> <span data-ttu-id="5d917-238">註冊並登入之後，您可以流覽至頁面並查看其內容。</span><span class="sxs-lookup"><span data-stu-id="5d917-238">After you've registered and logged in, you can navigate to the page and view its contents.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="5d917-239">其他資源</span><span class="sxs-lookup"><span data-stu-id="5d917-239">Additional Resources</span></span>

[<span data-ttu-id="5d917-240">使用 Razor 語法進行 ASP.NET Web Pages 程式設計的簡介</span><span class="sxs-lookup"><span data-stu-id="5d917-240">Introduction to ASP.NET Web Pages Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=251587)
