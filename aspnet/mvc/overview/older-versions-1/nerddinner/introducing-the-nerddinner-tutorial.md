---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: 簡介 NerdDinner 教學課程 |Microsoft Docs
author: shanselman
description: 若要了解新架構的最佳方式是建置與它的一些項目。 本教學課程逐步解說如何建置使用 ASP.NET 的小，但完整的應用程式...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: ebd49295ea165ba4ef1a25398cff7dddcfa54f11
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59392192"
---
# <a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="ce7c4-104">NerdDinner 教學課程簡介</span><span class="sxs-lookup"><span data-stu-id="ce7c4-104">Introducing the NerdDinner Tutorial</span></span>

<span data-ttu-id="ce7c4-105">藉由[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="ce7c4-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

[<span data-ttu-id="ce7c4-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="ce7c4-106">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="ce7c4-107">若要了解新架構的最佳方式是建置與它的一些項目。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="ce7c4-108">本教學課程會逐步解說如何建置一個小型的但在完成時，使用 ASP.NET MVC 1，應用程式，並介紹一些其背後的核心概念。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="ce7c4-109">如果您使用 ASP.NET MVC 3，我們建議您遵循[取得開始使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或是[MVC Music 市集](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-tutorial"></a><span data-ttu-id="ce7c4-110">NerdDinner 教學課程</span><span class="sxs-lookup"><span data-stu-id="ce7c4-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="ce7c4-111">若要了解新架構的最佳方式是建置與它的一些項目。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="ce7c4-112">本教學課程會逐步解說如何建置一個小型的但在完成時，使用 ASP.NET MVC 應用程式，並介紹一些其背後的核心概念。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="ce7c4-113">我們將建置的應用程式稱為 「 NerdDinner"。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="ce7c4-114">NerdDinner 提供簡單的方法讓人們尋找和組織 dinners 線上：</span><span class="sxs-lookup"><span data-stu-id="ce7c4-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="ce7c4-115">NerdDinner 可讓已註冊的使用者，來建立、 編輯和刪除 dinners。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="ce7c4-116">它會強制整個應用程式執行一組一致的驗證和商務規則：</span><span class="sxs-lookup"><span data-stu-id="ce7c4-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="ce7c4-117">訪客可以使用 AJAX 為基礎的地圖，來搜尋即將推出的 dinners 持有接近它們：</span><span class="sxs-lookup"><span data-stu-id="ce7c4-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="ce7c4-118">按一下 dinner 會移至詳細資料頁面讓他們從中學習更多關於此：</span><span class="sxs-lookup"><span data-stu-id="ce7c4-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="ce7c4-119">如果他們有興趣參加的 dinner 他們可以登入或註冊網站：</span><span class="sxs-lookup"><span data-stu-id="ce7c4-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="ce7c4-120">它們可以然後按一下 參加的 AJAX 為基礎的 RSVP 連結：</span><span class="sxs-lookup"><span data-stu-id="ce7c4-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="ce7c4-121">實作 NerdDinner</span><span class="sxs-lookup"><span data-stu-id="ce7c4-121">Implementing NerdDinner</span></span>

<span data-ttu-id="ce7c4-122">我們將從我們的 NerdDinner 應用程式使用 [檔案]-&gt;新專案在 Visual Studio 中的命令來建立全新的 ASP.NET MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="ce7c4-123">我們接著會以累加方式新增功能和功能。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="ce7c4-124">在過程中，我們將討論：</span><span class="sxs-lookup"><span data-stu-id="ce7c4-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="ce7c4-125">如何建立新的 ASP.NET MVC 專案</span><span class="sxs-lookup"><span data-stu-id="ce7c4-125">How to create a new ASP.NET MVC Project</span></span>](create-a-new-aspnet-mvc-project.md)
2. [<span data-ttu-id="ce7c4-126">如何建立資料庫</span><span class="sxs-lookup"><span data-stu-id="ce7c4-126">How to create a database</span></span>](create-a-database.md)
3. [<span data-ttu-id="ce7c4-127">如何建立使用商務規則驗證模型</span><span class="sxs-lookup"><span data-stu-id="ce7c4-127">How to build a model with business rule validations</span></span>](build-a-model-with-business-rule-validations.md)
4. [<span data-ttu-id="ce7c4-128">如何使用控制器和檢視來實作清單/詳細資料 UI</span><span class="sxs-lookup"><span data-stu-id="ce7c4-128">How to use controllers and views to implement a listing/details UI</span></span>](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [<span data-ttu-id="ce7c4-129">如何提供 CRUD （建立、 讀取、 更新、 刪除） 資料表單項目支援</span><span class="sxs-lookup"><span data-stu-id="ce7c4-129">How to provide CRUD (create, read, update, delete) data form entry support</span></span>](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [<span data-ttu-id="ce7c4-130">如何使用 ViewData 和實作 ViewModel 類別</span><span class="sxs-lookup"><span data-stu-id="ce7c4-130">How to use ViewData and implement ViewModel classes</span></span>](use-viewdata-and-implement-viewmodel-classes.md)
7. [<span data-ttu-id="ce7c4-131">如何重新使用使用主版頁面及部分的 UI</span><span class="sxs-lookup"><span data-stu-id="ce7c4-131">How to re-use UI using master pages and partials</span></span>](re-use-ui-using-master-pages-and-partials.md)
8. [<span data-ttu-id="ce7c4-132">如何實作有效率的資料分頁</span><span class="sxs-lookup"><span data-stu-id="ce7c4-132">How to implement efficient data paging</span></span>](implement-efficient-data-paging.md)
9. [<span data-ttu-id="ce7c4-133">如何保護應用程式使用驗證和授權</span><span class="sxs-lookup"><span data-stu-id="ce7c4-133">How to secure applications using authentication and authorization</span></span>](secure-applications-using-authentication-and-authorization.md)
10. [<span data-ttu-id="ce7c4-134">如何使用 AJAX 傳送動態更新</span><span class="sxs-lookup"><span data-stu-id="ce7c4-134">How to use AJAX to deliver dynamic updates</span></span>](use-ajax-to-deliver-dynamic-updates.md)
11. [<span data-ttu-id="ce7c4-135">如何使用 AJAX 實作對應實例</span><span class="sxs-lookup"><span data-stu-id="ce7c4-135">How to use AJAX to implement mapping scenarios</span></span>](use-ajax-to-implement-mapping-scenarios.md)
12. [<span data-ttu-id="ce7c4-136">如何啟用自動化的單元測試</span><span class="sxs-lookup"><span data-stu-id="ce7c4-136">How to enable automated unit testing</span></span>](enable-automated-unit-testing.md)

<span data-ttu-id="ce7c4-137">您可以建置自己的 NerdDinner 從頭開始，藉由完成每個步驟中我們在這一章中的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="ce7c4-138">或者，您可以下載原始碼的完整的版本：[在 GitHub 上的 NerdDinner](https://github.com/AspNetMVPSamples/NerdDinner)。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="ce7c4-139">您可以選擇性地也[下載免費的 PDF 版本，本教學課程的](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)如果您想要讀取的離線教學課程。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="ce7c4-140">您可以使用 Visual Studio 2008 或免費 Visual Web Developer 2008 Express 建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="ce7c4-141">您可以使用 SQL Server 或免費的 SQL Server Express 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="ce7c4-142">您可以安裝 ASP.NET MVC、 Visual Web Developer 2008 Express，和 SQL Server Express （所有免費） 使用的 V2 [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span><span class="sxs-lookup"><span data-stu-id="ce7c4-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="ce7c4-143">現在讓我們開始...</span><span class="sxs-lookup"><span data-stu-id="ce7c4-143">Now let's get started....</span></span>

<span data-ttu-id="ce7c4-144">既然我們已涵蓋 NerdDinner 的功能，讓我們彙總我們套筒，並撰寫一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="ce7c4-145">首先我們使用檔案-&gt;建立 NerdDinner 應用程式的 Visual Studio 中的新專案。</span><span class="sxs-lookup"><span data-stu-id="ce7c4-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ce7c4-146">下一步</span><span class="sxs-lookup"><span data-stu-id="ce7c4-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)
