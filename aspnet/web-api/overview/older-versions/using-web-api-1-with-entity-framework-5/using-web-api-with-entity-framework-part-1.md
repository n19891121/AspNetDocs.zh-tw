---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: 第 1 部份：概觀與建立專案 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: d5a72dbfe1530e457ec16df5c7d50b03b5f63502
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59384210"
---
# <a name="part-1-overview-and-creating-the-project"></a><span data-ttu-id="c08ed-102">第 1 部份：概觀與建立專案</span><span class="sxs-lookup"><span data-stu-id="c08ed-102">Part 1: Overview and Creating the Project</span></span>

<span data-ttu-id="c08ed-103">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c08ed-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c08ed-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="c08ed-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

<span data-ttu-id="c08ed-105">Entity Framework 是物件/關聯式對應架構。</span><span class="sxs-lookup"><span data-stu-id="c08ed-105">Entity Framework is an object/relational mapping framework.</span></span> <span data-ttu-id="c08ed-106">它會在您的程式碼中的網域物件對應到關聯式資料庫中的實體。</span><span class="sxs-lookup"><span data-stu-id="c08ed-106">It maps the domain objects in your code to entities in a relational database.</span></span> <span data-ttu-id="c08ed-107">大部分的情況下，您不必擔心資料庫層級，因為 Entity Framework 會為您處理它。</span><span class="sxs-lookup"><span data-stu-id="c08ed-107">For the most part, you do not have to worry about the database layer, because Entity Framework takes care of it for you.</span></span> <span data-ttu-id="c08ed-108">您的程式碼會操作物件，並變更已保存至資料庫。</span><span class="sxs-lookup"><span data-stu-id="c08ed-108">Your code manipulates the objects, and changes are persisted to a database.</span></span>

## <a name="about-the-tutorial"></a><span data-ttu-id="c08ed-109">針對本教學課程</span><span class="sxs-lookup"><span data-stu-id="c08ed-109">About the Tutorial</span></span>

<span data-ttu-id="c08ed-110">在本教學課程中，您將建立一個簡單的市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="c08ed-110">In this tutorial, you will create a simple store application.</span></span> <span data-ttu-id="c08ed-111">有兩個應用程式的主要部分。</span><span class="sxs-lookup"><span data-stu-id="c08ed-111">There are two main parts to the application.</span></span> <span data-ttu-id="c08ed-112">一般使用者可以檢視產品，並建立訂單：</span><span class="sxs-lookup"><span data-stu-id="c08ed-112">Normal users can view products and create orders:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

<span data-ttu-id="c08ed-113">系統管理員可以建立、 刪除或編輯產品：</span><span class="sxs-lookup"><span data-stu-id="c08ed-113">Administrators can create, delete, or edit products:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="c08ed-114">您將學習到的技能</span><span class="sxs-lookup"><span data-stu-id="c08ed-114">Skills You'll Learn</span></span>

<span data-ttu-id="c08ed-115">以下是您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="c08ed-115">Here's what you'll learn:</span></span>

- <span data-ttu-id="c08ed-116">如何使用 Entity Framework 搭配 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="c08ed-116">How to use Entity Framework with ASP.NET Web API.</span></span>
- <span data-ttu-id="c08ed-117">如何使用 knockout.js 建立動態的用戶端 UI。</span><span class="sxs-lookup"><span data-stu-id="c08ed-117">How to use knockout.js to create a dynamic client UI.</span></span>
- <span data-ttu-id="c08ed-118">如何使用 Web API 中的表單驗證，來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="c08ed-118">How to use forms authentication with Web API to authenticate users.</span></span>

<span data-ttu-id="c08ed-119">雖然本教學課程都各自獨立的您可能想要先閱讀下列教學課程：</span><span class="sxs-lookup"><span data-stu-id="c08ed-119">Although this tutorial is self-contained, you might want to read the following tutorials first:</span></span>

- [<span data-ttu-id="c08ed-120">第一個 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="c08ed-120">Your First ASP.NET Web API</span></span>](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [<span data-ttu-id="c08ed-121">建立 Web API 支援 CRUD 作業</span><span class="sxs-lookup"><span data-stu-id="c08ed-121">Creating a Web API that Supports CRUD Operations</span></span>](../creating-a-web-api-that-supports-crud-operations.md)

<span data-ttu-id="c08ed-122">一些知識[ASP.NET MVC](../../../../mvc/index.md)也很有用。</span><span class="sxs-lookup"><span data-stu-id="c08ed-122">Some knowledge of [ASP.NET MVC](../../../../mvc/index.md) is also helpful.</span></span>

## <a name="overview"></a><span data-ttu-id="c08ed-123">總覽</span><span class="sxs-lookup"><span data-stu-id="c08ed-123">Overview</span></span>

<span data-ttu-id="c08ed-124">概括而言，以下是應用程式的架構：</span><span class="sxs-lookup"><span data-stu-id="c08ed-124">At a high level, here is the architecture of the application:</span></span>

- <span data-ttu-id="c08ed-125">ASP.NET MVC 會為用戶端產生的 HTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="c08ed-125">ASP.NET MVC generates the HTML pages for the client.</span></span>
- <span data-ttu-id="c08ed-126">ASP.NET Web API 會公開資料 （「 產品 」 和 「 訂單 」） 上的 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="c08ed-126">ASP.NET Web API exposes CRUD operations on the data (products and orders).</span></span>
- <span data-ttu-id="c08ed-127">Entity Framework 會轉譯成資料庫實體的 Web API 所使用的 C# 模型。</span><span class="sxs-lookup"><span data-stu-id="c08ed-127">Entity Framework translates the C# models used by Web API into database entities.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

<span data-ttu-id="c08ed-128">下圖顯示如何在應用程式的各種層級表示網域物件：資料庫層級、 物件模型，而最後電傳格式，這會將資料以用戶端透過 HTTP 傳輸。</span><span class="sxs-lookup"><span data-stu-id="c08ed-128">The following diagram shows how the domain objects are represented at various layers of the application: The database layer, the object model, and finally the wire format, which is used to transmit data to the client via HTTP.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="c08ed-129">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="c08ed-129">Create the Visual Studio Project</span></span>

<span data-ttu-id="c08ed-130">您可以建立使用 Visual Web Developer Express 或 Visual Studio 的完整版本的教學課程專案。</span><span class="sxs-lookup"><span data-stu-id="c08ed-130">You can create the tutorial project using either Visual Web Developer Express or the full version of Visual Studio.</span></span>

<span data-ttu-id="c08ed-131">從**開始**頁面上，按一下**新的專案**。</span><span class="sxs-lookup"><span data-stu-id="c08ed-131">From the **Start** page, click **New Project**.</span></span>

<span data-ttu-id="c08ed-132">在 **範本**窗格中，選取**已安裝的範本**展開**Visual C#** 節點。</span><span class="sxs-lookup"><span data-stu-id="c08ed-132">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="c08ed-133">底下**Visual C#**，選取**Web**。</span><span class="sxs-lookup"><span data-stu-id="c08ed-133">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="c08ed-134">在專案範本清單中，選取**ASP.NET MVC 4 Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c08ed-134">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="c08ed-135">將專案命名為"ProductStore 」，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="c08ed-135">Name the project "ProductStore" and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

<span data-ttu-id="c08ed-136">在 **新的 ASP.NET MVC 4 專案**對話方塊中，選取**網際網路應用程式**，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="c08ed-136">In the **New ASP.NET MVC 4 Project** dialog, select **Internet Application** and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

<span data-ttu-id="c08ed-137">「 網際網路應用程式 」 範本會建立支援表單驗證的 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c08ed-137">The "Internet Application" template creates an ASP.NET MVC application that supports forms authentication.</span></span> <span data-ttu-id="c08ed-138">如果您執行應用程式現在，它已經具有一些功能：</span><span class="sxs-lookup"><span data-stu-id="c08ed-138">If you run the application now, it already has some features:</span></span>

- <span data-ttu-id="c08ed-139">新的使用者可以按一下右上角的 [註冊] 連結進行註冊。</span><span class="sxs-lookup"><span data-stu-id="c08ed-139">New users can register by clicking the "Register" link in the upper right corner.</span></span>
- <span data-ttu-id="c08ed-140">已註冊的使用者可以登入，按一下 「 登入 」 的連結。</span><span class="sxs-lookup"><span data-stu-id="c08ed-140">Registered users can log in by clicking the "Log in" link.</span></span>

<span data-ttu-id="c08ed-141">成員資格資訊會保存在資料庫中自動建立。</span><span class="sxs-lookup"><span data-stu-id="c08ed-141">Membership information is persisted in a database that gets created automatically.</span></span> <span data-ttu-id="c08ed-142">如需在 ASP.NET MVC 中的表單驗證的詳細資訊，請參閱[逐步解說：在 ASP.NET MVC 中使用表單驗證](https://msdn.microsoft.com/library/ff398049(VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="c08ed-142">For more information about forms authentication in ASP.NET MVC, see [Walkthrough: Using Forms Authentication in ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span></span>

## <a name="update-the-css-file"></a><span data-ttu-id="c08ed-143">更新 CSS 檔案</span><span class="sxs-lookup"><span data-stu-id="c08ed-143">Update the CSS File</span></span>

<span data-ttu-id="c08ed-144">是表面，在此步驟中，但它會讓轉譯先前的螢幕擷取畫面如下的頁面。</span><span class="sxs-lookup"><span data-stu-id="c08ed-144">This step is cosmetic, but it will make the pages render like the earlier screen shots.</span></span>

<span data-ttu-id="c08ed-145">在方案總管 中，展開 Content 資料夾，然後開啟名為 Site.css 檔案。</span><span class="sxs-lookup"><span data-stu-id="c08ed-145">In Solution Explorer, expand the Content folder and open the file named Site.css.</span></span> <span data-ttu-id="c08ed-146">新增下列 CSS 樣式：</span><span class="sxs-lookup"><span data-stu-id="c08ed-146">Add the following CSS styles:</span></span>

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [<span data-ttu-id="c08ed-147">下一步</span><span class="sxs-lookup"><span data-stu-id="c08ed-147">Next</span></span>](using-web-api-with-entity-framework-part-2.md)
