---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 第 2 部分：資料存取層 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列會詳細說明所有建置 Tailspin Spyworks 範例應用程式所採取的步驟。 第 2 部分涵蓋新增資料存取層。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 3fbc6fe4d94534a038a81532b3cd8ca30ddf9b11
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59378382"
---
# <a name="part-2-data-access-layer"></a><span data-ttu-id="b8b56-104">第 2 部分：資料存取層</span><span class="sxs-lookup"><span data-stu-id="b8b56-104">Part 2: Data Access Layer</span></span>

<span data-ttu-id="b8b56-105">藉由[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="b8b56-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="b8b56-106">Tailspin Spyworks 示範建立功能強大、 可擴充的應用程式，適用於.NET 平台是如何富含簡單。</span><span class="sxs-lookup"><span data-stu-id="b8b56-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="b8b56-107">它會展示如何在 ASP.NET 4 中使用最棒的新功能，建置線上商店，包括購物、 簽出，以及系統管理。</span><span class="sxs-lookup"><span data-stu-id="b8b56-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="b8b56-108">本教學課程系列會詳細說明所有建置 Tailspin Spyworks 範例應用程式所採取的步驟。</span><span class="sxs-lookup"><span data-stu-id="b8b56-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="b8b56-109">第 2 部分涵蓋新增資料存取層。</span><span class="sxs-lookup"><span data-stu-id="b8b56-109">Part 2 covers adding the data access layer.</span></span>


## <a id="_Toc260221668"></a>  <span data-ttu-id="b8b56-110">新增資料存取層</span><span class="sxs-lookup"><span data-stu-id="b8b56-110">Adding the Data Access Layer</span></span>

<span data-ttu-id="b8b56-111">我們的電子商務應用程式將取決於兩個資料庫。</span><span class="sxs-lookup"><span data-stu-id="b8b56-111">Our ecommerce application will depend on two databases.</span></span>

<span data-ttu-id="b8b56-112">客戶資訊中，我們將使用標準 ASP.NET 成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="b8b56-112">For customer information we'll use the standard ASP.NET Membership database.</span></span> <span data-ttu-id="b8b56-113">我們的購物車 」 和 「 產品類別目錄中，我們將實作的 SQL Express 資料庫執行，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b8b56-113">For our shopping cart and product catalog we'll implement a SQL Express database as follows.</span></span>

![](tailspin-spyworks-part-2/_static/image1.jpg)

<span data-ttu-id="b8b56-114">在應用程式的應用程式中建立資料庫 (Commerce.mdf)\_我們可以繼續建立我們使用.NET Entity Framework 的資料存取層的 [Data] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="b8b56-114">Having created the database (Commerce.mdf) in the application's App\_Data folder we can proceed to create our Data Access Layer using the .NET Entity Framework.</span></span>

<span data-ttu-id="b8b56-115">我們將建立名為 「 資料\_存取 」 和它們在該資料夾上按一下滑鼠右鍵，然後選取 新增新的項目 」。</span><span class="sxs-lookup"><span data-stu-id="b8b56-115">We'll create a folder named "Data\_Access" and them right click on that folder and select "Add New Item".</span></span>

<span data-ttu-id="b8b56-116">在 「 已安裝的範本 」 項目，然後選取 「 ADO.NET 實體資料模型 」 輸入 EDM\_Commerce.edmx 做為名稱，然後按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b8b56-116">In the "Installed Templates" item and then select "ADO.NET Entity Data Model" enter EDM\_Commerce.edmx as the name and click the "Add" button.</span></span>

![](tailspin-spyworks-part-2/_static/image2.jpg)

<span data-ttu-id="b8b56-117">選擇 [從資料庫產生]。</span><span class="sxs-lookup"><span data-stu-id="b8b56-117">Choose "Generate from Database".</span></span>

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

<span data-ttu-id="b8b56-118">儲存並建置。</span><span class="sxs-lookup"><span data-stu-id="b8b56-118">Save and build.</span></span>

<span data-ttu-id="b8b56-119">現在，我們已經準備好加入我們的第一項功能 – 產品類別目錄 功能表。</span><span class="sxs-lookup"><span data-stu-id="b8b56-119">Now we are ready to add our first feature – a product category menu.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b8b56-120">[上一頁](tailspin-spyworks-part-1.md)
> [下一頁](tailspin-spyworks-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="b8b56-120">[Previous](tailspin-spyworks-part-1.md)
[Next](tailspin-spyworks-part-3.md)</span></span>
