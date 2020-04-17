---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: 使用 CAPTCHA 防止機器人使用您的ASP.NET網络剃刀)網站 |微軟文件
author: rick-anderson
description: 本文介紹如何使用 ReCaptcha(安全措施)來防止自動程式 (bot) 在 ASP.NET 網頁 (Razor) 中執行任務...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 65f414ae3fed5e2fa28b1e57f5327c6411a43d55
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543752"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="3e917-103">使用 CAPTCHA 防止機器人使用ASP.NET網路剃刀)網站</span><span class="sxs-lookup"><span data-stu-id="3e917-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="3e917-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3e917-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="3e917-105">本文介紹如何使用 ReCaptcha(安全措施)來防止自動程式 (bot) 在ASP.NET網頁 (Razor) 網站中執行任務。</span><span class="sxs-lookup"><span data-stu-id="3e917-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="3e917-106">**您將學到什麼：**</span><span class="sxs-lookup"><span data-stu-id="3e917-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="3e917-107">如何向您的網站添加 CAPTCHA 測試。</span><span class="sxs-lookup"><span data-stu-id="3e917-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="3e917-108">以下是本文介紹的ASP.NET功能:</span><span class="sxs-lookup"><span data-stu-id="3e917-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="3e917-109">幫手`ReCaptcha`</span><span class="sxs-lookup"><span data-stu-id="3e917-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="3e917-110">本文中的資訊適用於ASP.NET網頁 1.0 和網頁 2。</span><span class="sxs-lookup"><span data-stu-id="3e917-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="3e917-111">關於 CAPTCHAs</span><span class="sxs-lookup"><span data-stu-id="3e917-111">About CAPTCHAs</span></span>

<span data-ttu-id="3e917-112">任何時候,當你讓人們在您的網站註冊,甚至只是輸入一個名字和URL(如博客評論),你可能會得到大量的假名。</span><span class="sxs-lookup"><span data-stu-id="3e917-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="3e917-113">這些通常由自動程式(機器人)留下,這些程式(機器人)試圖在他們能找到的每個網站中保留 URL。</span><span class="sxs-lookup"><span data-stu-id="3e917-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="3e917-114">(一個常見的動機是發佈要銷售的產品的 URL。</span><span class="sxs-lookup"><span data-stu-id="3e917-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="3e917-115">通過使用*CAPTCHA*驗證使用者註冊或以其他方式輸入其名稱和網站時,可以幫助確保使用者是真實使用者而不是電腦程式。</span><span class="sxs-lookup"><span data-stu-id="3e917-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="3e917-116">CAPTCHA 代表完全自動化的公共圖靈測試,告訴計算機和人類分開。</span><span class="sxs-lookup"><span data-stu-id="3e917-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="3e917-117">CAPTCHA 是一種*質詢-回應*測試,要求使用者執行一些使用者容易做的事情,但自動化程式卻很難做到。</span><span class="sxs-lookup"><span data-stu-id="3e917-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="3e917-118">CAPTCHA的最常見類型是看到一些扭曲的字母並被要求鍵入它們。</span><span class="sxs-lookup"><span data-stu-id="3e917-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="3e917-119">(失真應該使機器人很難破譯這些字母。</span><span class="sxs-lookup"><span data-stu-id="3e917-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="3e917-120">新增重新卡普查測試</span><span class="sxs-lookup"><span data-stu-id="3e917-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="3e917-121">在ASP.NET頁中`ReCaptcha`,可以使用説明程序呈現基於ReCaptcha服務[http://recaptcha.net](http://recaptcha.net)(的CAPTCHA測試)。</span><span class="sxs-lookup"><span data-stu-id="3e917-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="3e917-122">`ReCaptcha`説明程序顯示兩個扭曲的單詞的圖像,使用者在驗證頁面之前必須正確輸入這些單詞。</span><span class="sxs-lookup"><span data-stu-id="3e917-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="3e917-123">用戶回應由ReCaptcha.Net服務驗證。</span><span class="sxs-lookup"><span data-stu-id="3e917-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="3e917-124">在ReCaptcha.Net註冊您的網站。[http://recaptcha.net](http://recaptcha.net)</span><span class="sxs-lookup"><span data-stu-id="3e917-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="3e917-125">完成註冊后,您將獲得公鑰和私鑰。</span><span class="sxs-lookup"><span data-stu-id="3e917-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="3e917-126">將ASP.NET Web 幫助器庫添加到您的網站,如[在ASP.NET網頁網站中安裝説明程式](https://go.microsoft.com/fwlink/?LinkId=252372)(如果您尚未)中所述。</span><span class="sxs-lookup"><span data-stu-id="3e917-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="3e917-127">如果您還沒有*\_AppStart.cshtml*檔,則在網站的根資料夾中創建名為*\_AppStart.cshtml*的檔。</span><span class="sxs-lookup"><span data-stu-id="3e917-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="3e917-128">`Recaptcha`*在\_AppStart.cshtml*檔加入以下說明程式設定:</span><span class="sxs-lookup"><span data-stu-id="3e917-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="3e917-129">使用您自己的`PublicKey``PrivateKey`公共和私密金鑰設定和屬性。</span><span class="sxs-lookup"><span data-stu-id="3e917-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="3e917-130">保存*\_AppStart.cshtml*檔並關閉它。</span><span class="sxs-lookup"><span data-stu-id="3e917-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="3e917-131">在網站的根資料夾中,創建名為*Recaptcha.cshtml*的新頁面。</span><span class="sxs-lookup"><span data-stu-id="3e917-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="3e917-132">將現有內容取代為以下內容:</span><span class="sxs-lookup"><span data-stu-id="3e917-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="3e917-133">在瀏覽器中運行*Recaptcha.cshtml*頁面。</span><span class="sxs-lookup"><span data-stu-id="3e917-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="3e917-134">如果`PrivateKey`該值有效,則頁面將顯示 ReCaptcha 控件和一個按鈕。</span><span class="sxs-lookup"><span data-stu-id="3e917-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="3e917-135">如果未在*\_AppStart.html*中全域設置金鑰,則頁面將顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e917-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="3e917-136">輸入測試的單詞。</span><span class="sxs-lookup"><span data-stu-id="3e917-136">Enter the words for the test.</span></span> <span data-ttu-id="3e917-137">如果通過 ReCaptcha 測試,則會看到一條達到該效果的消息。</span><span class="sxs-lookup"><span data-stu-id="3e917-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="3e917-138">否則,您將看到一條錯誤消息,並重新顯示 ReCaptcha 控件。</span><span class="sxs-lookup"><span data-stu-id="3e917-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="3e917-139">如果您的電腦位於使用代理伺服器的域中,則可能需要配置*Web.config*`defaultproxy`檔案的元素。</span><span class="sxs-lookup"><span data-stu-id="3e917-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="3e917-140">下面的範例顯示了一個*Web.config*檔`defaultproxy`,該檔配置了元素以使 ReCaptcha 服務正常工作。</span><span class="sxs-lookup"><span data-stu-id="3e917-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="3e917-141">其他資源</span><span class="sxs-lookup"><span data-stu-id="3e917-141">Additional Resources</span></span>

- [<span data-ttu-id="3e917-142">為ASP.NET網頁網站自訂網站範圍行為</span><span class="sxs-lookup"><span data-stu-id="3e917-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="3e917-143">雷卡普查網站</span><span class="sxs-lookup"><span data-stu-id="3e917-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
