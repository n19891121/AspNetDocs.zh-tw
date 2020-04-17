---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: 顯示資料庫資料表 (C#) |微軟文件
author: rick-anderson
description: 在本教程中,我將演示顯示一組資料庫記錄的兩種方法。 我在 HTML ta...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 3fca8ac9e9b4e549ca76ffa282cc03aa4cc50e88
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542050"
---
# <a name="displaying-a-table-of-database-data-c"></a><span data-ttu-id="86fa3-104">顯示資料庫資料的資料表 (C#)</span><span class="sxs-lookup"><span data-stu-id="86fa3-104">Displaying a Table of Database Data (C#)</span></span>

<span data-ttu-id="86fa3-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="86fa3-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="86fa3-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="86fa3-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> <span data-ttu-id="86fa3-107">在本教程中,我將演示顯示一組資料庫記錄的兩種方法。</span><span class="sxs-lookup"><span data-stu-id="86fa3-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="86fa3-108">我在 HTML 表中顯示了兩種格式化一組資料庫記錄的方法。</span><span class="sxs-lookup"><span data-stu-id="86fa3-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="86fa3-109">首先,我將演示如何直接在視圖中設置資料庫記錄的格式。</span><span class="sxs-lookup"><span data-stu-id="86fa3-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="86fa3-110">接下來,我將演示如何在格式化資料庫記錄時利用部分。</span><span class="sxs-lookup"><span data-stu-id="86fa3-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>

<span data-ttu-id="86fa3-111">本教學的目的是解釋如何在 mVC 應用程式中顯示 ASP.NET 資料庫數據的 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="86fa3-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="86fa3-112">首先,您將瞭解如何使用 Visual Studio 中包含的基架工具生成自動顯示一組記錄的檢視。</span><span class="sxs-lookup"><span data-stu-id="86fa3-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="86fa3-113">接下來,您將學習如何在格式化資料庫記錄時使用部分範本。</span><span class="sxs-lookup"><span data-stu-id="86fa3-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="86fa3-114">建立模型類</span><span class="sxs-lookup"><span data-stu-id="86fa3-114">Create the Model Classes</span></span>

<span data-ttu-id="86fa3-115">我們將從「電影」資料庫表中顯示記錄集。</span><span class="sxs-lookup"><span data-stu-id="86fa3-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="86fa3-116">「影片」資料庫表包含以下欄:</span><span class="sxs-lookup"><span data-stu-id="86fa3-116">The Movies database table contains the following columns:</span></span>

<a id="0.3_table01"></a>

| <span data-ttu-id="86fa3-117">**資料行名稱**</span><span class="sxs-lookup"><span data-stu-id="86fa3-117">**Column Name**</span></span> | <span data-ttu-id="86fa3-118">**資料類型**</span><span class="sxs-lookup"><span data-stu-id="86fa3-118">**Data Type**</span></span> | <span data-ttu-id="86fa3-119">**允許 Null**</span><span class="sxs-lookup"><span data-stu-id="86fa3-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="86fa3-120">Id</span><span class="sxs-lookup"><span data-stu-id="86fa3-120">Id</span></span> | <span data-ttu-id="86fa3-121">Int</span><span class="sxs-lookup"><span data-stu-id="86fa3-121">Int</span></span> | <span data-ttu-id="86fa3-122">False</span><span class="sxs-lookup"><span data-stu-id="86fa3-122">False</span></span> |
| <span data-ttu-id="86fa3-123">Title</span><span class="sxs-lookup"><span data-stu-id="86fa3-123">Title</span></span> | <span data-ttu-id="86fa3-124">恩瓦爾查爾 (200)</span><span class="sxs-lookup"><span data-stu-id="86fa3-124">Nvarchar(200)</span></span> | <span data-ttu-id="86fa3-125">False</span><span class="sxs-lookup"><span data-stu-id="86fa3-125">False</span></span> |
| <span data-ttu-id="86fa3-126">導演</span><span class="sxs-lookup"><span data-stu-id="86fa3-126">Director</span></span> | <span data-ttu-id="86fa3-127">恩瓦爾查爾 (50)</span><span class="sxs-lookup"><span data-stu-id="86fa3-127">NVarchar(50)</span></span> | <span data-ttu-id="86fa3-128">False</span><span class="sxs-lookup"><span data-stu-id="86fa3-128">False</span></span> |
| <span data-ttu-id="86fa3-129">發佈日期</span><span class="sxs-lookup"><span data-stu-id="86fa3-129">DateReleased</span></span> | <span data-ttu-id="86fa3-130">Datetime</span><span class="sxs-lookup"><span data-stu-id="86fa3-130">DateTime</span></span> | <span data-ttu-id="86fa3-131">False</span><span class="sxs-lookup"><span data-stu-id="86fa3-131">False</span></span> |

<span data-ttu-id="86fa3-132">為了在ASP.NET MVC 應用程式中表示"電影"表,我們需要創建一個模型類。</span><span class="sxs-lookup"><span data-stu-id="86fa3-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="86fa3-133">在本教學中,我們使用Microsoft實體框架創建模型類。</span><span class="sxs-lookup"><span data-stu-id="86fa3-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="86fa3-134">在本教學中,我們使用Microsoft實體框架。</span><span class="sxs-lookup"><span data-stu-id="86fa3-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="86fa3-135">但是,請務必瞭解,您可以使用各種不同的技術與資料庫進行交互,從ASP.NET MVC 應用程式(包括 LINQ 到 SQL、NHibernate 或ADO.NET)。</span><span class="sxs-lookup"><span data-stu-id="86fa3-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>

<span data-ttu-id="86fa3-136">依以下步驟啟動實體資料模型精靈:</span><span class="sxs-lookup"><span data-stu-id="86fa3-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="86fa3-137">右鍵按一下「解決方案資源管理器」視窗中的「模型」資料夾,然後選擇選單選項 **「添加、新建專案**」。</span><span class="sxs-lookup"><span data-stu-id="86fa3-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="86fa3-138">選擇 **「資料**」類別並選擇**ADO.NET 實體資料模型**樣本。</span><span class="sxs-lookup"><span data-stu-id="86fa3-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="86fa3-139">為資料模型指定名稱 *「MoviesDBModel.edmx」,* 然後單擊 **「添加**」按鈕。</span><span class="sxs-lookup"><span data-stu-id="86fa3-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="86fa3-140">按下「添加」按鈕後,將顯示實體數據模型嚮導(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="86fa3-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="86fa3-141">按照以下步驟完成精靈:</span><span class="sxs-lookup"><span data-stu-id="86fa3-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="86fa3-142">在 **「選擇模型內容」** 步驟中,選擇「**從資料庫產生**」選項。</span><span class="sxs-lookup"><span data-stu-id="86fa3-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="86fa3-143">在 **「選擇數據連接**」步驟中,使用*MoviesDB.mdf*數據連接和名稱 *「電影 DB 實體*」來設置連接設置。</span><span class="sxs-lookup"><span data-stu-id="86fa3-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="86fa3-144">按 **[下一步]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="86fa3-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="86fa3-145">在 **「選擇資料庫物件**」步驟中,展開「表」節點,選擇「影片」表。</span><span class="sxs-lookup"><span data-stu-id="86fa3-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="86fa3-146">輸入命名空間*模型*,然後按下 **「完成」** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="86fa3-146">Enter the namespace *Models* and click the **Finish** button.</span></span>

<span data-ttu-id="86fa3-147">[![將 LINQ 建立 SQL 類別](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="86fa3-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span></span>

<span data-ttu-id="86fa3-148">**圖 01**: 建立 LINQ 到 SQL 類別 ([按下以檢視全尺寸影像](displaying-a-table-of-database-data-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="86fa3-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image2.png))</span></span>

<span data-ttu-id="86fa3-149">完成實體數據模型嚮導後,將打開實體數據模型設計器。</span><span class="sxs-lookup"><span data-stu-id="86fa3-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="86fa3-150">設計器應顯示影片實體(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="86fa3-150">The Designer should display the Movies entity (see Figure 2).</span></span>

<span data-ttu-id="86fa3-151">[![實體資料模型設計器](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="86fa3-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span></span>

<span data-ttu-id="86fa3-152">**圖 02**: 實體資料模型設計器 ([按下以檢視全尺寸影像](displaying-a-table-of-database-data-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="86fa3-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image4.png))</span></span>

<span data-ttu-id="86fa3-153">在繼續之前,我們需要作出一個改變。</span><span class="sxs-lookup"><span data-stu-id="86fa3-153">We need to make one change before we continue.</span></span> <span data-ttu-id="86fa3-154">實體數據嚮導生成一個名為 *「電影」* 的模型類,該類表示"影片"資料庫表。</span><span class="sxs-lookup"><span data-stu-id="86fa3-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="86fa3-155">由於我們將使用「電影」類來表示特定影片,因此我們需要將類的名稱修改為 *「電影*」而不是 *「電影*」(單數而不是複數)。</span><span class="sxs-lookup"><span data-stu-id="86fa3-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="86fa3-156">按兩下設計器表面上的類的名稱,並將類的名稱從「影片」更改為「影片」。。</span><span class="sxs-lookup"><span data-stu-id="86fa3-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="86fa3-157">進行此更改後,按下 **「保存**」按鈕(軟盤的圖示)以生成 Movie 類。</span><span class="sxs-lookup"><span data-stu-id="86fa3-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="86fa3-158">建立影片控制器</span><span class="sxs-lookup"><span data-stu-id="86fa3-158">Create the Movies Controller</span></span>

<span data-ttu-id="86fa3-159">現在,我們有一種方法來表示我們的資料庫記錄,我們可以創建一個控制器,返回電影的集合。</span><span class="sxs-lookup"><span data-stu-id="86fa3-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="86fa3-160">在可視化工作室解決方案資源管理器視窗中,右鍵單擊"控制器"資料夾並選擇功能表選項 **'添加控制器**"(參見圖 3)。</span><span class="sxs-lookup"><span data-stu-id="86fa3-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>

<span data-ttu-id="86fa3-161">[![新增控制器選單](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="86fa3-161">[![The Add Controller Menu](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span></span>

<span data-ttu-id="86fa3-162">**圖 03**: 新增控制器選單 ([按下以檢視全尺寸影像](displaying-a-table-of-database-data-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="86fa3-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image6.png))</span></span>

<span data-ttu-id="86fa3-163">出現 **「添加控制器」** 對話方塊時,輸入控制器名稱「電影控制器」(參見圖 4)。</span><span class="sxs-lookup"><span data-stu-id="86fa3-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="86fa3-164">按下「**新增**」按鈕以新增新控制器。</span><span class="sxs-lookup"><span data-stu-id="86fa3-164">Click the **Add** button to add the new controller.</span></span>

<span data-ttu-id="86fa3-165">[![新增控制器對話框](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="86fa3-165">[![The Add Controller dialog](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span></span>

<span data-ttu-id="86fa3-166">**圖 04**: 新增控制器對話框([按下以檢視全尺寸影像](displaying-a-table-of-database-data-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="86fa3-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image8.png))</span></span>

<span data-ttu-id="86fa3-167">我們需要修改由 Movie 控制器公開的 Index() 操作,以便它返回資料庫記錄集。</span><span class="sxs-lookup"><span data-stu-id="86fa3-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="86fa3-168">修改控制器,使其看起來像清單 1 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="86fa3-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="86fa3-169">**清單1 = 控制器\電影控制器.cs**</span><span class="sxs-lookup"><span data-stu-id="86fa3-169">**Listing 1 – Controllers\MovieController.cs**</span></span>

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

<span data-ttu-id="86fa3-170">在清單 1 中,電影 DB 實體類用於表示 MoviesDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="86fa3-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="86fa3-171">要使用此類,您需要導入 MvcApplication1.模型命名空間,如下所示:</span><span class="sxs-lookup"><span data-stu-id="86fa3-171">To use this class, you need to import the MvcApplication1.Models namespace like this:</span></span>

<span data-ttu-id="86fa3-172">使用 Mvc 應用程式 1.模型;</span><span class="sxs-lookup"><span data-stu-id="86fa3-172">using MvcApplication1.Models;</span></span>

<span data-ttu-id="86fa3-173">表達式*實體。MovieSet.ToList()* 從「影片」資料庫表中返回所有影片集。</span><span class="sxs-lookup"><span data-stu-id="86fa3-173">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="86fa3-174">建立檢視</span><span class="sxs-lookup"><span data-stu-id="86fa3-174">Create the View</span></span>

<span data-ttu-id="86fa3-175">在 HTML 表中顯示一組資料庫記錄的最簡單方法是利用 Visual Studio 提供的基架。</span><span class="sxs-lookup"><span data-stu-id="86fa3-175">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="86fa3-176">通過選擇功能表選項 **「生成」、「生成解決方案**」來構建應用程式。</span><span class="sxs-lookup"><span data-stu-id="86fa3-176">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="86fa3-177">在打開 **「添加檢視**」對話方塊之前,必須生成應用程式,否則數據類不會顯示在對話框中。</span><span class="sxs-lookup"><span data-stu-id="86fa3-177">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="86fa3-178">右鍵按一下索引() 操作並選擇功能表選項 **「添加檢視**」(參見圖 5)。</span><span class="sxs-lookup"><span data-stu-id="86fa3-178">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>

<span data-ttu-id="86fa3-179">[![新增檢視](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="86fa3-179">[![Adding a view](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span></span>

<span data-ttu-id="86fa3-180">**圖 05**: 新增檢視 ([按下以檢視全尺寸影像](displaying-a-table-of-database-data-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="86fa3-180">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image10.png))</span></span>

<span data-ttu-id="86fa3-181">在 **'新增檢視'** 對話框中, 選擇標籤為「**建立強類型檢視」 選單的欄位**。</span><span class="sxs-lookup"><span data-stu-id="86fa3-181">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="86fa3-182">選擇「影片」類別作為**檢視資料類別**。</span><span class="sxs-lookup"><span data-stu-id="86fa3-182">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="86fa3-183">選擇 *「清單*」作為**檢視內容**(參見圖 6)。</span><span class="sxs-lookup"><span data-stu-id="86fa3-183">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="86fa3-184">選擇這些選項將生成顯示影片清單的強類型視圖。</span><span class="sxs-lookup"><span data-stu-id="86fa3-184">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>

<span data-ttu-id="86fa3-185">[!['新增檢視"對話框](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="86fa3-185">[![The Add View dialog](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span></span>

<span data-ttu-id="86fa3-186">**圖 06**: 新增檢視對話框([按下以檢視全尺寸影像](displaying-a-table-of-database-data-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="86fa3-186">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image12.png))</span></span>

<span data-ttu-id="86fa3-187">按下「**添加**」按鈕後,將自動生成清單 2 中的檢視。</span><span class="sxs-lookup"><span data-stu-id="86fa3-187">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="86fa3-188">此檢視包含遍遍遍電影集合並顯示影片的每個屬性所需的代碼。</span><span class="sxs-lookup"><span data-stu-id="86fa3-188">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="86fa3-189">**清單 2 = 檢視\影片_索引.aspx**</span><span class="sxs-lookup"><span data-stu-id="86fa3-189">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

<span data-ttu-id="86fa3-190">您可以通過選擇功能表選項 **「除錯」、「開始除錯**」(或點擊 F5 鍵)來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="86fa3-190">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="86fa3-191">運行應用程式將啟動 Internet 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="86fa3-191">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="86fa3-192">如果您導航到 /Movie URL,您將看到圖 7 中的頁面。</span><span class="sxs-lookup"><span data-stu-id="86fa3-192">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>

<span data-ttu-id="86fa3-193">[![電影表](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="86fa3-193">[![A table of movies](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span></span>

<span data-ttu-id="86fa3-194">**圖 07**: 電影表([按下以檢視全尺寸影像](displaying-a-table-of-database-data-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="86fa3-194">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image14.png))</span></span>

<span data-ttu-id="86fa3-195">如果您不喜歡圖 7 中資料庫記錄網格的外觀,則只需修改 Index 視圖即可。</span><span class="sxs-lookup"><span data-stu-id="86fa3-195">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="86fa3-196">例如,您可以通過修改索引檢視將*日期釋放*標頭更改為*發佈日期釋放*日期。</span><span class="sxs-lookup"><span data-stu-id="86fa3-196">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="86fa3-197">建立產生部分的樣本</span><span class="sxs-lookup"><span data-stu-id="86fa3-197">Create a Template with a Partial</span></span>

<span data-ttu-id="86fa3-198">當視圖變得過於複雜時,最好開始將視圖分解為部分視圖。</span><span class="sxs-lookup"><span data-stu-id="86fa3-198">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="86fa3-199">使用部分使您的檢視更易於理解和維護。</span><span class="sxs-lookup"><span data-stu-id="86fa3-199">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="86fa3-200">我們將創建一個部分,我們可以用作範本來格式化每個影片資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="86fa3-200">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="86fa3-201">依以下步驟建立部分:</span><span class="sxs-lookup"><span data-stu-id="86fa3-201">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="86fa3-202">右鍵按兩下「檢視」+影片資料夾,然後選擇功能表選項 **「添加檢視**」。</span><span class="sxs-lookup"><span data-stu-id="86fa3-202">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="86fa3-203">選中標記為「*創建部分檢視 (.ascx)」的*複選框。</span><span class="sxs-lookup"><span data-stu-id="86fa3-203">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="86fa3-204">命名部分*影片樣本*。</span><span class="sxs-lookup"><span data-stu-id="86fa3-204">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="86fa3-205">選中標記為「**創建強類型檢視」的**複選框。</span><span class="sxs-lookup"><span data-stu-id="86fa3-205">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="86fa3-206">選擇「影片」 作為*檢視資料類別*。</span><span class="sxs-lookup"><span data-stu-id="86fa3-206">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="86fa3-207">選擇「空」作為*檢視內容*。</span><span class="sxs-lookup"><span data-stu-id="86fa3-207">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="86fa3-208">按下「**新增**」按鈕將部分新增到專案中。</span><span class="sxs-lookup"><span data-stu-id="86fa3-208">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="86fa3-209">完成這些步驟后,將「電影範本」部分修改為類似於清單 3。</span><span class="sxs-lookup"><span data-stu-id="86fa3-209">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="86fa3-210">**清單3 = 檢視\電影_電影範本.ascx**</span><span class="sxs-lookup"><span data-stu-id="86fa3-210">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

<span data-ttu-id="86fa3-211">清單3中的部分包含一行記錄的範本。</span><span class="sxs-lookup"><span data-stu-id="86fa3-211">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="86fa3-212">清單4中修改後的索引視圖使用影片範本部分。</span><span class="sxs-lookup"><span data-stu-id="86fa3-212">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="86fa3-213">**清單4 = 檢視\影片_索引.aspx**</span><span class="sxs-lookup"><span data-stu-id="86fa3-213">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

<span data-ttu-id="86fa3-214">清單 4 中的檢視包含一個迴圈,該迴圈遍歷所有影片。</span><span class="sxs-lookup"><span data-stu-id="86fa3-214">The view in Listing 4 contains a foreach loop that iterates through all of the movies.</span></span> <span data-ttu-id="86fa3-215">對於每個影片,影片範本部分用於格式化影片。</span><span class="sxs-lookup"><span data-stu-id="86fa3-215">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="86fa3-216">通過調用 Render 部分() 説明器方法來呈現影片範本。</span><span class="sxs-lookup"><span data-stu-id="86fa3-216">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="86fa3-217">修改後的 Index 檢視呈現的資料庫記錄的 HTML 表與同一個表。</span><span class="sxs-lookup"><span data-stu-id="86fa3-217">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="86fa3-218">但是,視圖已大大簡化。</span><span class="sxs-lookup"><span data-stu-id="86fa3-218">However, the view has been greatly simplified.</span></span>

<span data-ttu-id="86fa3-219">Render部分() 方法不同於大多數其他幫助器方法,因為它不返回字串。</span><span class="sxs-lookup"><span data-stu-id="86fa3-219">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="86fa3-220">因此,必須使用&lt;% Html.render 部分();%&gt;&lt;而不是 %= Html.render 部份();%&gt;.</span><span class="sxs-lookup"><span data-stu-id="86fa3-220">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial(); %&gt; instead of &lt;%= Html.RenderPartial(); %&gt;.</span></span>

## <a name="summary"></a><span data-ttu-id="86fa3-221">總結</span><span class="sxs-lookup"><span data-stu-id="86fa3-221">Summary</span></span>

<span data-ttu-id="86fa3-222">本教學的目的是解釋如何在 HTML 表中顯示一組資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="86fa3-222">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="86fa3-223">首先,您學習了如何通過利用 Microsoft 實體框架從控制器操作返回一組資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="86fa3-223">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="86fa3-224">接下來,您學習了如何使用 Visual Studio 基架生成自動顯示專案集合的視圖。</span><span class="sxs-lookup"><span data-stu-id="86fa3-224">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="86fa3-225">最後,您學習了如何通過利用部分視圖來簡化視圖。</span><span class="sxs-lookup"><span data-stu-id="86fa3-225">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="86fa3-226">您學習了如何使用部分作為範本,以便可以格式化每個資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="86fa3-226">You learned how to use a partial as a template so that you can format each database record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="86fa3-227">[前一個](creating-model-classes-with-linq-to-sql-cs.md)
> [下一個](performing-simple-validation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="86fa3-227">[Previous](creating-model-classes-with-linq-to-sql-cs.md)
[Next](performing-simple-validation-cs.md)</span></span>
