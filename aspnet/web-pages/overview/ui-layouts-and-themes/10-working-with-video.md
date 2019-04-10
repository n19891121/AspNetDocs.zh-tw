---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: 顯示視訊在 ASP.NET Web Pages (Razor) 網站 |Microsoft Docs
author: Rick-Anderson
description: 本章說明如何顯示視訊 ASP.NET Web Pages 中使用 Razor 語法的頁面。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 204611513860e268001596b9c7ac9e9c023caa12
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59399849"
---
# <a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="9e4d2-103">在 ASP.NET Web Pages (Razor) 網站中顯示影片</span><span class="sxs-lookup"><span data-stu-id="9e4d2-103">Displaying Video in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="9e4d2-104">藉由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9e4d2-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9e4d2-105">這篇文章說明如何在 ASP.NET Web Pages (Razor) 網站中使用 （媒體） 的影片播放程式，讓使用者檢視儲存在站台的影片。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-105">This article explains how to use a video (media) player in an ASP.NET Web Pages (Razor) website to let users view videos that are stored on the site.</span></span> <span data-ttu-id="9e4d2-106">含有 Razor 語法的 ASP.NET Web Pages 可讓您進行此遊戲 Flash (*.swf*)，Media Player (*.wmv*)，和 Silverlight (*.xap*) 影片。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-106">ASP.NET Web Pages with Razor syntax lets you play Flash (*.swf*), Media Player (*.wmv*), and Silverlight (*.xap*) videos.</span></span>
> 
> <span data-ttu-id="9e4d2-107">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="9e4d2-108">如何選擇的視訊播放器。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-108">How to choose a video player.</span></span>
> - <span data-ttu-id="9e4d2-109">如何將影片新增至網頁。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-109">How to add video to a web page.</span></span>
> - <span data-ttu-id="9e4d2-110">如何設定視訊播放程式屬性。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-110">How to set video player attributes.</span></span>
> 
> <span data-ttu-id="9e4d2-111">這些是 ASP.NET Razor pages 文件中所引進的功能：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-111">These are the ASP.NET Razor pages features introduced in the article:</span></span>
> 
> - <span data-ttu-id="9e4d2-112">`Video`協助程式。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-112">The `Video` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9e4d2-113">在本教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="9e4d2-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="9e4d2-114">ASP.NET Web Pages (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="9e4d2-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="9e4d2-115">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="9e4d2-115">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="9e4d2-116">本教學課程也適用於 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-116">This tutorial also works with WebMatrix 3.</span></span>


## <a name="introduction"></a><span data-ttu-id="9e4d2-117">簡介</span><span class="sxs-lookup"><span data-stu-id="9e4d2-117">Introduction</span></span>

<span data-ttu-id="9e4d2-118">您可能想要顯示在您的網站上的影片。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-118">You might want to display a video on your site.</span></span> <span data-ttu-id="9e4d2-119">方法之一是連結到已經有段影片中的，例如 YouTube 的站台。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-119">One way to do that is to link to a site that already has the video, like YouTube.</span></span> <span data-ttu-id="9e4d2-120">如果您想要直接在自己的網頁中內嵌來自這些網站的影片，您可以通常是從網站取得 HTML 標記，並再將它複製到您的頁面。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-120">If you want to embed a video from these sites directly in your own pages, you can usually get HTML markup from the site and then copy it into your page.</span></span> <span data-ttu-id="9e4d2-121">例如，下列範例示範如何內嵌的 YouTube 影片：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-121">For example, the following example shows how to embed a YouTube video:</span></span>

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

<span data-ttu-id="9e4d2-122">如果您想要播放的視訊，會在您自己的網站 （不在公用的視訊分享網站） 上，您無法直接連結使用像這樣的內嵌的標記。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-122">If you want to play a video that's on your own website (not on a public video-sharing site), you can't directly link to it using embedded markup like this.</span></span> <span data-ttu-id="9e4d2-123">不過，使用從您的網站播放影片`Video`helper 會呈現的媒體播放程式，直接在網頁中。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-123">However, you can play videos from your site by using the `Video` helper, which renders a media player directly in a page.</span></span>

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a><span data-ttu-id="9e4d2-124">選擇的視訊播放器</span><span class="sxs-lookup"><span data-stu-id="9e4d2-124">Choosing a Video Player</span></span>

<span data-ttu-id="9e4d2-125">有許多格式的視訊檔案，以及每個格式通常需要不同的播放程式，然後設定播放程式的不同方法。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-125">There are lots of formats for video files, and each format typically requires a different player and a different way to configure the player.</span></span> <span data-ttu-id="9e4d2-126">在 ASP.NET Razor 頁面中，您可以播放視訊時在網頁中使用`Video`協助程式。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-126">In ASP.NET Razor pages, you can play a video in a web page using the `Video` helper.</span></span> <span data-ttu-id="9e4d2-127">`Video`協助程式簡化在網頁中內嵌影片，因為它會自動產生的程序`object`和`embed`通常用來將影片新增至頁面的 HTML 項目。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-127">The `Video` helper simplifies the process of embedding videos in a web page because it automatically generates the `object` and `embed` HTML elements that are normally used to add video to the page.</span></span>

<span data-ttu-id="9e4d2-128">`Video`協助程式支援下列的媒體播放程式：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-128">The `Video` helper supports the following media players:</span></span>

- <span data-ttu-id="9e4d2-129">Adobe Flash</span><span class="sxs-lookup"><span data-stu-id="9e4d2-129">Adobe Flash</span></span>
- <span data-ttu-id="9e4d2-130">Windows MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="9e4d2-130">Windows MediaPlayer</span></span>
- <span data-ttu-id="9e4d2-131">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="9e4d2-131">Microsoft Silverlight</span></span>

### <a name="the-flash-player"></a><span data-ttu-id="9e4d2-132">Flash Player</span><span class="sxs-lookup"><span data-stu-id="9e4d2-132">The Flash Player</span></span>

<span data-ttu-id="9e4d2-133">`Flash`的 player`Video`協助程式可讓您播放 Flash 視訊 (*.swf*檔案) 在網頁中。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-133">The `Flash` player of the `Video` helper let you play Flash videos (*.swf* files) in a web page.</span></span> <span data-ttu-id="9e4d2-134">至少，您必須提供視訊檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-134">At a minimum, you have to provide a path to the video file.</span></span> <span data-ttu-id="9e4d2-135">如果您指定只一個路徑，播放程式會使用目前版本的 Flash 所設定的預設值。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-135">If you specify nothing but the path, the player uses default values that are set by the current version of Flash.</span></span> <span data-ttu-id="9e4d2-136">典型的預設設定如下：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-136">Typical default settings are:</span></span>

- <span data-ttu-id="9e4d2-137">在視訊顯示時使用它的預設寬度和高度，而不需要的背景色彩。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-137">The video is displayed using its default width and height and without a background color.</span></span>
- <span data-ttu-id="9e4d2-138">在頁面載入時，會自動播放視訊。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-138">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="9e4d2-139">影片迴圈持續直到明確停止為止。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-139">The video loops continuously until it's explicitly stopped.</span></span>
- <span data-ttu-id="9e4d2-140">視訊是以顯示所有的影片中，而不是裁剪視訊以符合特定的大小調整。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-140">The video is scaled to show all of the video, rather than cropping the video to fit a specific size.</span></span>
- <span data-ttu-id="9e4d2-141">在視窗中播放視訊。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-141">The video plays in a window.</span></span>

### <a name="the-mediaplayer-player"></a><span data-ttu-id="9e4d2-142">MediaPlayer 播放程式</span><span class="sxs-lookup"><span data-stu-id="9e4d2-142">The MediaPlayer Player</span></span>

<span data-ttu-id="9e4d2-143">`MediaPlayer`的 player`Video`協助程式可讓您播放 Windows Media 視訊 (*.wmv*檔案)，Windows Media audio (*.wma*檔案)，和 MP3 (*.mp3*在網頁中檔案）。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-143">The `MediaPlayer` player of the `Video` helper lets you play Windows Media videos (*.wmv* files), Windows Media audio (*.wma* files), and MP3 (*.mp3* files) in a web page.</span></span> <span data-ttu-id="9e4d2-144">您必須包含播放; 的媒體檔案的路徑所有其他參數是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-144">You must include path of the media file to play; all other parameters are optional.</span></span> <span data-ttu-id="9e4d2-145">如果您僅指定路徑，播放程式會使用這類設定的 MediaPlayer，最新版的預設設定：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-145">If you specify only a path, the player uses default settings set by the current version of MediaPlayer, such as:</span></span>

- <span data-ttu-id="9e4d2-146">在視訊顯示時使用它的預設寬度和高度。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-146">The video is displayed using its default width and height.</span></span>
- <span data-ttu-id="9e4d2-147">在頁面載入時，會自動播放視訊。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-147">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="9e4d2-148">視訊播放一次 （它不會執行迴圈）。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-148">The video plays once (it doesn't loop).</span></span>
- <span data-ttu-id="9e4d2-149">播放程式顯示使用者介面中的一組完整的控制項。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-149">The player displays the full set of controls in the user interface.</span></span>
- <span data-ttu-id="9e4d2-150">在視窗中播放視訊。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-150">The video plays in a window.</span></span>

### <a name="the-silverlight-player"></a><span data-ttu-id="9e4d2-151">Silverlight 播放程式</span><span class="sxs-lookup"><span data-stu-id="9e4d2-151">The Silverlight Player</span></span>

<span data-ttu-id="9e4d2-152">`Silverlight`的 player`Video`協助程式可讓您播放 Windows Media Video (*.wmv*檔案)，Windows Media Audio (*.wma*檔案)，和 MP3 (*.mp3*檔案）。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-152">The `Silverlight` player of the `Video` helper lets you play Windows Media Video (*.wmv* files), Windows Media Audio (*.wma* files), and MP3 (*.mp3* files).</span></span> <span data-ttu-id="9e4d2-153">您必須設定 path 參數來指向 Silverlight 應用程式封裝 (*.xap*檔案)。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-153">You must set the path parameter to point to a Silverlight-based application package (*.xap* file).</span></span> <span data-ttu-id="9e4d2-154">您也必須設定寬度和高度的參數。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-154">You also must set the width and height parameters.</span></span> <span data-ttu-id="9e4d2-155">所有其他參數皆為選擇性使用。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-155">All other parameters are optional.</span></span> <span data-ttu-id="9e4d2-156">當您使用 Silverlight 播放程式的影片中，如果您設定必要的參數時，Silverlight 播放程式就會顯示沒有背景色彩的影片。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-156">When you use the Silverlight player for video, if you set only the required parameters, the Silverlight player displays the video without a background color.</span></span>

> [!NOTE]
> <span data-ttu-id="9e4d2-157">如果您還不知道 Silverlight: *.xap*檔案會壓縮的檔案，包含配置中的指示 *.xaml*的組件和選擇性資源的 managed 程式碼檔。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-157">In case you don't already know Silverlight: the *.xap* file is a compressed file that contains layout instructions in a *.xaml* file, managed code in assemblies, and optional resources.</span></span> <span data-ttu-id="9e4d2-158">您可以建立 *.xap*為 Silverlight 應用程式專案的 Visual Studio 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-158">You can create a *.xap* file in Visual Studio as a Silverlight application project.</span></span>


<span data-ttu-id="9e4d2-159">`Silverlight`視訊播放程式會使用您提供的播放程式的設定和中提供的設定都 *.xap*檔案。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-159">The `Silverlight` video player uses both the settings that you provide for the player and the settings that are provided in the *.xap* file.</span></span>

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a><span data-ttu-id="9e4d2-160">MIME 類型</span><span class="sxs-lookup"><span data-stu-id="9e4d2-160">MIME Types</span></span>
> 
> <span data-ttu-id="9e4d2-161">當瀏覽器下載檔案時，瀏覽器確保檔案類型符合指定所呈現的文件的 MIME 類型。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-161">When a browser downloads a file, the browser makes sure that the file type matches the MIME type that's specified for the document that's being rendered.</span></span> <span data-ttu-id="9e4d2-162">內容類型或媒體檔案類型的 MIME 類型。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-162">The MIME type is the content type or media type of a file.</span></span> <span data-ttu-id="9e4d2-163">`Video`協助程式會使用下列 MIME 類型：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-163">The `Video` helper uses the following MIME types:</span></span>
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`


<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a><span data-ttu-id="9e4d2-164">播放視訊 Flash (.swf)</span><span class="sxs-lookup"><span data-stu-id="9e4d2-164">Playing Flash (.swf) Videos</span></span>

<span data-ttu-id="9e4d2-165">此程序會示範如何名為 Flash 視訊*sample.swf*。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-165">This procedure shows you how to play a Flash video named *sample.swf*.</span></span> <span data-ttu-id="9e4d2-166">此程序假設您有一個名為資料夾*媒體*您的網站，而且該 *.swf*檔案位在該資料夾。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-166">The procedure assumes that you've got a folder named *Media* on your site and that the *.swf* file is in that folder.</span></span>

1. <span data-ttu-id="9e4d2-167">將 ASP.NET Web Helpers Library 新增至您的網站，如中所述[安裝 ASP.NET Web Pages 網站中的協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)，如果您還沒有新增它。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-167">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="9e4d2-168">在網站中，加入頁面並將它命名*FlashVideo.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-168">In the website, add a page and name it *FlashVideo.cshtml*.</span></span>
3. <span data-ttu-id="9e4d2-169">將下列標記加入頁面：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-169">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. <span data-ttu-id="9e4d2-170">執行網頁瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-170">Run the page in a browser.</span></span> <span data-ttu-id="9e4d2-171">(請確定中選取頁面**檔案**才能執行這個工作區。)頁面隨即顯示，並會自動播放視訊。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-171">(Make sure the page is selected in the **Files** workspace before you run it.) The page is displayed and the video plays automatically.</span></span> 

    <span data-ttu-id="9e4d2-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span><span class="sxs-lookup"><span data-stu-id="9e4d2-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span></span>

<span data-ttu-id="9e4d2-173">您可以設定`quality`Flash 影片的參數`low`， `autolow`， `autohigh`， `medium`， `high`，和`best`:</span><span class="sxs-lookup"><span data-stu-id="9e4d2-173">You can set the `quality` parameter for a Flash video to `low`, `autolow`, `autohigh`, `medium`, `high`, and `best`:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

<span data-ttu-id="9e4d2-174">您可以變更播放在特定大小，使用 Flash 視訊`scale`參數，您可以將下列設定：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-174">You can change the Flash video to play at a specific size using the `scale` parameter, which you can set to the following:</span></span>

- `showall`<span data-ttu-id="9e4d2-175">。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-175">.</span></span> <span data-ttu-id="9e4d2-176">這樣可讓整個視訊看到同時維持原始外觀比例。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-176">This makes the entire video visible while maintaining the original aspect ratio.</span></span> <span data-ttu-id="9e4d2-177">不過，您可能會得到每一端上的框線。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-177">However, you might end up with borders on each side.</span></span>
- `noorder`<span data-ttu-id="9e4d2-178">。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-178">.</span></span> <span data-ttu-id="9e4d2-179">這樣可以調整視訊同時維持原始外觀比例，但它可能會被裁剪。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-179">This scales the video while maintaining the original aspect ratio, but it might be cropped.</span></span>
- `exactfit`<span data-ttu-id="9e4d2-180">。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-180">.</span></span> <span data-ttu-id="9e4d2-181">這樣可讓整個視訊看到不含維持原始外觀比例，但允許進行扭曲。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-181">This makes the entire video visible without preserving the original aspect ratio, but distortion may occur.</span></span>

<span data-ttu-id="9e4d2-182">如果您未指定`scale`參數，整個視訊會顯示，而不需要任何裁剪會維持原始外觀比例。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-182">If you don't specify a `scale` parameter, the entire video will be visible and the original aspect ratio will be maintained without any cropping.</span></span> <span data-ttu-id="9e4d2-183">下列範例示範如何使用`scale`參數：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-183">The following example shows how to use the `scale` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

<span data-ttu-id="9e4d2-184">Flash player 支援的視訊模式設定，稱為`windowMode`。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-184">The Flash player supports a video mode setting named `windowMode`.</span></span> <span data-ttu-id="9e4d2-185">您可以設定為`window`， `opaque`，和`transparent`。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-185">You can set this to `window`, `opaque`, and `transparent`.</span></span> <span data-ttu-id="9e4d2-186">根據預設，`windowMode`設為`window`，其中顯示在不同的視窗，在網頁上的影片。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-186">By default, the `windowMode` is set to `window`, which displays the video in a separate window on the web page.</span></span> <span data-ttu-id="9e4d2-187">`opaque`設定會隱藏在網頁上的視訊背後的所有項目。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-187">The `opaque` setting hides everything behind the video on the web page.</span></span> <span data-ttu-id="9e4d2-188">`transparent`設定可讓影片中，透過顯示網頁的背景假設任何部分視訊透明的。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-188">The `transparent` setting lets the background of the web page show through the video, assuming any part of the video is transparent.</span></span>

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a><span data-ttu-id="9e4d2-189">播放 MediaPlayer (*.wmv*) 影片</span><span class="sxs-lookup"><span data-stu-id="9e4d2-189">Playing MediaPlayer (*.wmv*) Videos</span></span>

<span data-ttu-id="9e4d2-190">下列程序會示範如何播放名為視窗 Media video *sample.wmv*位於*媒體*資料夾。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-190">The following procedure shows you how to play a Window Media video named *sample.wmv* that's in the *Media* folder.</span></span>

1. <span data-ttu-id="9e4d2-191">將 ASP.NET Web Helpers Library 新增至您的網站，如中所述[安裝 ASP.NET Web Pages 網站中的協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)，如果您還沒有這麼做。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-191">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="9e4d2-192">建立名為的新頁面*MediaPlayerVideo.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-192">Create a new page named *MediaPlayerVideo.cshtml*.</span></span>
3. <span data-ttu-id="9e4d2-193">將下列標記加入頁面：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-193">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. <span data-ttu-id="9e4d2-194">執行網頁瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-194">Run the page in a browser.</span></span> <span data-ttu-id="9e4d2-195">載入影片，並會自動播放。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-195">The video loads and plays automatically.</span></span> 

    <span data-ttu-id="9e4d2-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span><span class="sxs-lookup"><span data-stu-id="9e4d2-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span></span>

<span data-ttu-id="9e4d2-197">您可以設定`playCount`設為整數，表示要自動播放影片多少次：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-197">You can set `playCount` to an integer that indicates how many times to play the video automatically:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

<span data-ttu-id="9e4d2-198">`uiMode`參數可讓您指定的使用者介面中顯示哪些控制項。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-198">The `uiMode` parameter lets you specify which controls show up in the user interface.</span></span> <span data-ttu-id="9e4d2-199">您可以設定`uiMode`要`invisible`， `none`， `mini`，或`full`。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-199">You can set `uiMode` to `invisible`, `none`, `mini`, or `full`.</span></span> <span data-ttu-id="9e4d2-200">如果您未指定`uiMode`參數，影片將會顯示狀態視窗中，搜尋列中，控制按鈕及音量控制項，加上 [視訊] 視窗。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-200">If you don't specify a `uiMode` parameter, the video will be displayed with the status window, seek bar, control buttons, and volume controls in addition to the video window.</span></span> <span data-ttu-id="9e4d2-201">如果您使用 media player 播放音訊檔案，也會顯示這些控制項。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-201">These controls will also be displayed if you use the player to play an audio file.</span></span> <span data-ttu-id="9e4d2-202">以下是如何使用的範例`uiMode`參數：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-202">Here's an example of how to use the `uiMode` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

<span data-ttu-id="9e4d2-203">根據預設，音訊是上播放視訊時。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-203">By default, audio is on when the video plays.</span></span> <span data-ttu-id="9e4d2-204">您可以藉由設定靜音音訊`mute`參數設為 true:</span><span class="sxs-lookup"><span data-stu-id="9e4d2-204">You can mute the audio by setting the `mute` parameter to true:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

<span data-ttu-id="9e4d2-205">您可以設定來控制 MediaPlayer 視訊的音訊層級`volume`參數的值介於 0 到 100 之間。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-205">You can control the audio level of the MediaPlayer video by setting the `volume` parameter to a value between 0 and 100.</span></span> <span data-ttu-id="9e4d2-206">預設值為 50。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-206">The default value is 50.</span></span> <span data-ttu-id="9e4d2-207">以下為範例：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-207">Here's an example:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a><span data-ttu-id="9e4d2-208">播放 Silverlight 影片</span><span class="sxs-lookup"><span data-stu-id="9e4d2-208">Playing Silverlight Videos</span></span>

<span data-ttu-id="9e4d2-209">此程序會示範如何播放包含 Silverlight 中的影片 *.xap*資料夾中名為頁面*媒體*。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-209">This procedure shows you how to play video contained in a Silverlight *.xap* page that's in a folder named *Media*.</span></span>

1. <span data-ttu-id="9e4d2-210">將 ASP.NET Web Helpers Library 新增至您的網站，如中所述[安裝 ASP.NET Web Pages 網站中的協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)，如果您還沒有這麼做。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-210">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already .</span></span>
2. <span data-ttu-id="9e4d2-211">建立名為的新頁面*SilverlightVideo.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-211">Create a new page named *SilverlightVideo.cshtml*.</span></span>
3. <span data-ttu-id="9e4d2-212">將下列標記加入頁面：</span><span class="sxs-lookup"><span data-stu-id="9e4d2-212">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. <span data-ttu-id="9e4d2-213">執行網頁瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="9e4d2-213">Run the page in a browser.</span></span> 

    <span data-ttu-id="9e4d2-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span><span class="sxs-lookup"><span data-stu-id="9e4d2-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="9e4d2-215">其他資源</span><span class="sxs-lookup"><span data-stu-id="9e4d2-215">Additional Resources</span></span>


[<span data-ttu-id="9e4d2-216">Silverlight 的概觀</span><span class="sxs-lookup"><span data-stu-id="9e4d2-216">Silverlight Overview</span></span>](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)

[<span data-ttu-id="9e4d2-217">Flash 物件和內嵌的標記屬性</span><span class="sxs-lookup"><span data-stu-id="9e4d2-217">Flash OBJECT and EMBED tag attributes</span></span>](http://kb2.adobe.com/cps/127/tn_12701.html)

[<span data-ttu-id="9e4d2-218">Windows Media Player 11 SDK PARAM 標記</span><span class="sxs-lookup"><span data-stu-id="9e4d2-218">Windows Media Player 11 SDK PARAM Tags</span></span>](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)
