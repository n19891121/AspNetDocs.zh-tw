---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
title: 使用實體框架 (VB) 建立模型類別 ( / )微軟文件
author: rick-anderson
description: 在本教學中,您將瞭解如何將ASP.NETMVC與Microsoft實體框架一起使用。 您將瞭解如何使用實體精靈建立ADO.NET實體 Da...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: ff8322c9-12f3-4e24-aba6-a38046b9bb0d
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
msc.type: authoredcontent
ms.openlocfilehash: cdba91969a6ed9c02965999bbc48d5c5cdea140d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542647"
---
# <a name="creating-model-classes-with-the-entity-framework-vb"></a><span data-ttu-id="60a79-104">使用 Entity Framework 建立模型類別 (VB)</span><span class="sxs-lookup"><span data-stu-id="60a79-104">Creating Model Classes with the Entity Framework (VB)</span></span>

<span data-ttu-id="60a79-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="60a79-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="60a79-106">在本教學中,您將瞭解如何將ASP.NETMVC與Microsoft實體框架一起使用。</span><span class="sxs-lookup"><span data-stu-id="60a79-106">In this tutorial, you learn how to use ASP.NET MVC with the Microsoft Entity Framework.</span></span> <span data-ttu-id="60a79-107">您將瞭解如何使用實體嚮導創建ADO.NET實體資料模型。</span><span class="sxs-lookup"><span data-stu-id="60a79-107">You learn how to use the Entity Wizard to create an ADO.NET Entity Data Model.</span></span> <span data-ttu-id="60a79-108">在本教學中,我們將建構一個 Web 應用程式,說明如何使用實體框架選擇、插入、更新和刪除資料庫資料。</span><span class="sxs-lookup"><span data-stu-id="60a79-108">Over the course of this tutorial, we build a web application that illustrates how to select, insert, update, and delete database data by using the Entity Framework.</span></span>

<span data-ttu-id="60a79-109">本教學的目的是說明如何在建構ASP.NET MVC 應用程式時使用Microsoft實體架構創建資料存取類。</span><span class="sxs-lookup"><span data-stu-id="60a79-109">The goal of this tutorial is to explain how you can create data access classes using the Microsoft Entity Framework when building an ASP.NET MVC application.</span></span> <span data-ttu-id="60a79-110">本教程假定之前對 Microsoft 實體框架沒有瞭解。</span><span class="sxs-lookup"><span data-stu-id="60a79-110">This tutorial assumes no previous knowledge of the Microsoft Entity Framework.</span></span> <span data-ttu-id="60a79-111">在本教學結束時,您將瞭解如何使用實體框架來選擇、插入、更新和刪除資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="60a79-111">By the end of this tutorial, you'll understand how to use the Entity Framework to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="60a79-112">Microsoft 實體框架是一個對象關係映射 (O/RM) 工具,使您能夠從資料庫自動生成數據存取層。</span><span class="sxs-lookup"><span data-stu-id="60a79-112">The Microsoft Entity Framework is an Object Relational Mapping (O/RM) tool that enables you to generate a data access layer from a database automatically.</span></span> <span data-ttu-id="60a79-113">實體框架使您能夠避免手動構建數據訪問類的繁瑣工作。</span><span class="sxs-lookup"><span data-stu-id="60a79-113">The Entity Framework enables you to avoid the tedious work of building your data access classes by hand.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="60a79-114">ASP.NET MVC 和 Microsoft 實體框架之間沒有基本聯繫。</span><span class="sxs-lookup"><span data-stu-id="60a79-114">There is no essential connection between ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="60a79-115">實體框架有幾個替代方法可用於mVCASP.NET。</span><span class="sxs-lookup"><span data-stu-id="60a79-115">There are several alternatives to the Entity Framework that you can use with ASP.NET MVC.</span></span> <span data-ttu-id="60a79-116">例如,您可以使用其他 O/RM 工具(如 Microsoft LINQ 到 SQL、NHibernate 或 SubSonic)構建 MVC 模型類。</span><span class="sxs-lookup"><span data-stu-id="60a79-116">For example, you can build your MVC Model classes using other O/RM tools such as Microsoft LINQ to SQL, NHibernate, or SubSonic.</span></span>

<span data-ttu-id="60a79-117">為了說明如何使用微軟實體框架進行ASP.NET MVC,我們將構建一個簡單的示例應用程式。</span><span class="sxs-lookup"><span data-stu-id="60a79-117">In order to illustrate how you can use the Microsoft Entity Framework with ASP.NET MVC, we'll build a simple sample application.</span></span> <span data-ttu-id="60a79-118">我們將創建一個影片資料庫應用程式,使您能夠顯示和編輯影片資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="60a79-118">We'll create a Movie Database application that enables you to display and edit movie database records.</span></span>

<span data-ttu-id="60a79-119">本教程假定您擁有 Visual Studio 2008 或帶 Service Pack 1 的可視化 Web 開發人員 2008。</span><span class="sxs-lookup"><span data-stu-id="60a79-119">This tutorial assumes that you have Visual Studio 2008 or Visual Web Developer 2008 with Service Pack 1.</span></span> <span data-ttu-id="60a79-120">您需要服務包 1 才能使用實體框架。</span><span class="sxs-lookup"><span data-stu-id="60a79-120">You need Service Pack 1 in order to use the Entity Framework.</span></span> <span data-ttu-id="60a79-121">您可以透過以下位址下載 Visual Studio 2008 服務套件 1 或帶服務套件 1 的視覺化 Web 開發人員:</span><span class="sxs-lookup"><span data-stu-id="60a79-121">You can download Visual Studio 2008 Service Pack 1 or Visual Web Developer with Service Pack 1 from the following address:</span></span>

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

## <a name="creating-the-movie-sample-database"></a><span data-ttu-id="60a79-122">建立影片範例資料庫</span><span class="sxs-lookup"><span data-stu-id="60a79-122">Creating the Movie Sample Database</span></span>

<span data-ttu-id="60a79-123">影片資料庫應用程式使用名為「Movie」的資料庫表,其中包含以下列:</span><span class="sxs-lookup"><span data-stu-id="60a79-123">The Movie Database application uses a database table named Movies that contains the following columns:</span></span>

| <span data-ttu-id="60a79-124">資料行名稱</span><span class="sxs-lookup"><span data-stu-id="60a79-124">Column Name</span></span> | <span data-ttu-id="60a79-125">資料類型</span><span class="sxs-lookup"><span data-stu-id="60a79-125">Data Type</span></span> | <span data-ttu-id="60a79-126">允許 Nulls?</span><span class="sxs-lookup"><span data-stu-id="60a79-126">Allow Nulls?</span></span> | <span data-ttu-id="60a79-127">是主鍵嗎?</span><span class="sxs-lookup"><span data-stu-id="60a79-127">Is Primary Key?</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="60a79-128">Id</span><span class="sxs-lookup"><span data-stu-id="60a79-128">Id</span></span> | <span data-ttu-id="60a79-129">int</span><span class="sxs-lookup"><span data-stu-id="60a79-129">int</span></span> | <span data-ttu-id="60a79-130">False</span><span class="sxs-lookup"><span data-stu-id="60a79-130">False</span></span> | <span data-ttu-id="60a79-131">True</span><span class="sxs-lookup"><span data-stu-id="60a79-131">True</span></span> |
| <span data-ttu-id="60a79-132">Title</span><span class="sxs-lookup"><span data-stu-id="60a79-132">Title</span></span> | <span data-ttu-id="60a79-133">恩瓦爾查爾 (100)</span><span class="sxs-lookup"><span data-stu-id="60a79-133">nvarchar(100)</span></span> | <span data-ttu-id="60a79-134">False</span><span class="sxs-lookup"><span data-stu-id="60a79-134">False</span></span> | <span data-ttu-id="60a79-135">False</span><span class="sxs-lookup"><span data-stu-id="60a79-135">False</span></span> |
| <span data-ttu-id="60a79-136">導演</span><span class="sxs-lookup"><span data-stu-id="60a79-136">Director</span></span> | <span data-ttu-id="60a79-137">恩瓦爾查爾 (100)</span><span class="sxs-lookup"><span data-stu-id="60a79-137">nvarchar(100)</span></span> | <span data-ttu-id="60a79-138">False</span><span class="sxs-lookup"><span data-stu-id="60a79-138">False</span></span> | <span data-ttu-id="60a79-139">False</span><span class="sxs-lookup"><span data-stu-id="60a79-139">False</span></span> |

<span data-ttu-id="60a79-140">您可以按照以下步驟將此表加入ASP.NET MVC 專案中:</span><span class="sxs-lookup"><span data-stu-id="60a79-140">You can add this table to an ASP.NET MVC project by following these steps:</span></span>

1. <span data-ttu-id="60a79-141">右鍵按一下「\_解決方案資源管理器」視窗中的應用數據資料夾,然後選擇選單選項 **「添加,新建專案」。。**</span><span class="sxs-lookup"><span data-stu-id="60a79-141">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item.**</span></span>
2. <span data-ttu-id="60a79-142">在 **「新增新項目」** 對話方塊中,選擇**SQL Server 資料庫**,為資料庫指定名稱 MoviesDB.mdf,然後按下「**添加**」按鈕。</span><span class="sxs-lookup"><span data-stu-id="60a79-142">From the **Add New Item** dialog box, select **SQL Server Database**, give the database the name MoviesDB.mdf, and click the **Add** button.</span></span>
3. <span data-ttu-id="60a79-143">按兩下 MoviesDB.mdf 檔以打開伺服器資源管理器/資料庫資源管理器視窗。</span><span class="sxs-lookup"><span data-stu-id="60a79-143">Double-click the MoviesDB.mdf file to open the Server Explorer/Database Explorer window.</span></span>
4. <span data-ttu-id="60a79-144">展開 MoviesDB.mdf 資料庫連接,右鍵單擊「表」資料夾,然後選擇功能表選項 **「添加新錶**」。</span><span class="sxs-lookup"><span data-stu-id="60a79-144">Expand the MoviesDB.mdf database connection, right-click the Tables folder, and select the menu option **Add New Table**.</span></span>
5. <span data-ttu-id="60a79-145">在表設計器中,添加 Id、標題和控制器列。</span><span class="sxs-lookup"><span data-stu-id="60a79-145">In the Table Designer, add the Id, Title, and Director columns.</span></span>
6. <span data-ttu-id="60a79-146">按下 **「儲存**」按鈕(它有軟盤的圖示)以儲存新錶的名稱「電影」。。</span><span class="sxs-lookup"><span data-stu-id="60a79-146">Click the **Save** button (it has the icon of the floppy) to save the new table with the name Movies.</span></span>

<span data-ttu-id="60a79-147">創建"影片"資料庫表後,應向該表添加一些範例資料。</span><span class="sxs-lookup"><span data-stu-id="60a79-147">After you create the Movies database table, you should add some sample data to the table.</span></span> <span data-ttu-id="60a79-148">右鍵按一下「影片」表併選擇功能表選項 **「顯示表數據**」。</span><span class="sxs-lookup"><span data-stu-id="60a79-148">Right-click the Movies table and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="60a79-149">您可以將假影片數據輸入顯示的網格中。</span><span class="sxs-lookup"><span data-stu-id="60a79-149">You can enter fake movie data into the grid that appears.</span></span>

## <a name="creating-the-adonet-entity-data-model"></a><span data-ttu-id="60a79-150">建立ADO.NET實體資料模型</span><span class="sxs-lookup"><span data-stu-id="60a79-150">Creating the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="60a79-151">為了使用實體框架,您需要創建實體數據模型。</span><span class="sxs-lookup"><span data-stu-id="60a79-151">In order to use the Entity Framework, you need to create an Entity Data Model.</span></span> <span data-ttu-id="60a79-152">您可以使用視覺化工作室*實體資料模型精靈*從資料庫自動生成實體資料模型。</span><span class="sxs-lookup"><span data-stu-id="60a79-152">You can take advantage of the Visual Studio *Entity Data Model Wizard* to generate an Entity Data Model from a database automatically.</span></span>

<span data-ttu-id="60a79-153">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="60a79-153">Follow these steps:</span></span>

1. <span data-ttu-id="60a79-154">右鍵按一下「解決方案資源管理器」視窗中的「模型」資料夾,然後選擇選單選項 **「添加,新專案**」。</span><span class="sxs-lookup"><span data-stu-id="60a79-154">Right-click the Models folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="60a79-155">在「**添加新專案」** 對話方塊中,選擇「資料」類別(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="60a79-155">In the **Add New Item** dialog, select the Data category (see Figure 1).</span></span>
3. <span data-ttu-id="60a79-156">選擇**ADO.NET 實體資料模型**樣本,為實體數據模型指定名稱「電影 DBModel.edmx」,然後按下 **「添加**」按鈕。</span><span class="sxs-lookup"><span data-stu-id="60a79-156">Select the **ADO.NET Entity Data Model** template, give the Entity Data Model the name MoviesDBModel.edmx, and click the **Add** button.</span></span> <span data-ttu-id="60a79-157">按下 **「添加**」按鈕將啟動「數據模型精靈」。</span><span class="sxs-lookup"><span data-stu-id="60a79-157">Clicking the **Add** button launches the Data Model Wizard.</span></span>
4. <span data-ttu-id="60a79-158">在 **「選擇模型內容」** 步驟中,選擇「**從資料庫產生**」選項,然後單擊 **「下一步**」按鈕(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="60a79-158">In the **Choose Model Contents** step, choose the **Generate from a database** option and click the **Next** button (see Figure 2).</span></span>
5. <span data-ttu-id="60a79-159">在 **「選擇數據連接**」步驟中,選擇 MoviesDB.mdf 資料庫連接,輸入實體連接設置名稱「電影 DB 實體」,然後單擊 **「下一步**」按鈕(參見圖 3)。</span><span class="sxs-lookup"><span data-stu-id="60a79-159">In the **Choose Your Data Connection** step, select the MoviesDB.mdf database connection, enter the entities connection settings name MoviesDBEntities, and click the **Next** button (see Figure 3).</span></span>
6. <span data-ttu-id="60a79-160">在 **「選擇資料庫物件**」步驟中,選擇「影片資料庫」表並單擊 **「完成」** 按鈕(參見圖 4)。</span><span class="sxs-lookup"><span data-stu-id="60a79-160">In the **Choose Your Database Objects** step, select the Movie database table and click the **Finish** button (see Figure 4).</span></span>

<span data-ttu-id="60a79-161">完成這些步驟後,將打開ADO.NET實體數據模型設計器(實體設計器)。</span><span class="sxs-lookup"><span data-stu-id="60a79-161">After you complete these steps, the ADO.NET Entity Data Model Designer (Entity Designer) opens.</span></span>

<span data-ttu-id="60a79-162">**圖 1 = 建立新的實體資料模型**</span><span class="sxs-lookup"><span data-stu-id="60a79-162">**Figure 1 – Creating a new Entity Data Model**</span></span>

![clip_image002](creating-model-classes-with-the-entity-framework-vb/_static/image1.jpg)

<span data-ttu-id="60a79-164">**圖 2 = 選擇模型內容步驟**</span><span class="sxs-lookup"><span data-stu-id="60a79-164">**Figure 2 – Choose Model Contents Step**</span></span>

![clip_image004](creating-model-classes-with-the-entity-framework-vb/_static/image2.jpg)

<span data-ttu-id="60a79-166">**圖 3 = 選擇資料連線**</span><span class="sxs-lookup"><span data-stu-id="60a79-166">**Figure 3 – Choose Your Data Connection**</span></span>

![clip_image006](creating-model-classes-with-the-entity-framework-vb/_static/image3.jpg)

<span data-ttu-id="60a79-168">**圖 4 = 選擇資料庫物件**</span><span class="sxs-lookup"><span data-stu-id="60a79-168">**Figure 4 – Choose Your Database Objects**</span></span>

![clip_image008](creating-model-classes-with-the-entity-framework-vb/_static/image4.jpg)

## <a name="modifying-the-adonet-entity-data-model"></a><span data-ttu-id="60a79-170">變更ADO.NET實體資料模型</span><span class="sxs-lookup"><span data-stu-id="60a79-170">Modifying the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="60a79-171">創建實體數據模型后,可以使用實體設計器修改模型(參見圖 5)。</span><span class="sxs-lookup"><span data-stu-id="60a79-171">After you create an Entity Data Model, you can modify the model by taking advantage of the Entity Designer (see Figure 5).</span></span> <span data-ttu-id="60a79-172">您可以隨時透過雙擊解決方案資源管理器視窗中的「模型」資料夾中的「電影 DBModel.edmx 檔案」來打開實體設計器。</span><span class="sxs-lookup"><span data-stu-id="60a79-172">You can open the Entity Designer at any time by double-clicking the MoviesDBModel.edmx file contained in the Models folder within the Solution Explorer window.</span></span>

<span data-ttu-id="60a79-173">**圖 5 = ADO.NET 實體資料模型設計器**</span><span class="sxs-lookup"><span data-stu-id="60a79-173">**Figure 5 – The ADO.NET Entity Data Model Designer**</span></span>

![clip_image010](creating-model-classes-with-the-entity-framework-vb/_static/image5.jpg)

<span data-ttu-id="60a79-175">例如,可以使用實體設計器更改實體模型數據嚮導生成的類的名稱。</span><span class="sxs-lookup"><span data-stu-id="60a79-175">For example, you can use the Entity Designer to change the names of the classes that the Entity Model Data Wizard generates.</span></span> <span data-ttu-id="60a79-176">嚮導創建了名為"電影"的新數據存取類。</span><span class="sxs-lookup"><span data-stu-id="60a79-176">The Wizard created a new data access class named Movies.</span></span> <span data-ttu-id="60a79-177">換句話說,嚮導為類指定與資料庫表相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="60a79-177">In other words, the Wizard gave the class the very same name as the database table.</span></span> <span data-ttu-id="60a79-178">由於我們將使用此類來表示特定的「影片」實例,因此應將類從「影片」重新命名為「影片」。</span><span class="sxs-lookup"><span data-stu-id="60a79-178">Because we will use this class to represent a particular Movie instance, we should rename the class from Movies to Movie.</span></span>

<span data-ttu-id="60a79-179">如果要重命名實體類,可以按兩下實體設計器中的類名稱並輸入新名稱(參見圖 6)。</span><span class="sxs-lookup"><span data-stu-id="60a79-179">If you want to rename an entity class, you can double-click on the class name in the Entity Designer and enter a new name (see Figure 6).</span></span> <span data-ttu-id="60a79-180">或者,您可以在實體設計器中選擇實體后,在"屬性"視窗中更改實體的名稱。</span><span class="sxs-lookup"><span data-stu-id="60a79-180">Alternatively, you can change the name of an entity in the Properties window after selecting an entity in the Entity Designer.</span></span>

<span data-ttu-id="60a79-181">**圖 6 = 變更實體名稱**</span><span class="sxs-lookup"><span data-stu-id="60a79-181">**Figure 6 – Changing an entity name**</span></span>

![clip_image012](creating-model-classes-with-the-entity-framework-vb/_static/image6.jpg)

<span data-ttu-id="60a79-183">請記住,通過按一下「儲存」按鈕(軟盤的圖示)進行修改後保存實體數據模型。</span><span class="sxs-lookup"><span data-stu-id="60a79-183">Remember to save your Entity Data Model after making a modification by clicking the Save button (the icon of the floppy disk).</span></span> <span data-ttu-id="60a79-184">在後台,實體設計器生成一組 Visual Basic .NET 類。</span><span class="sxs-lookup"><span data-stu-id="60a79-184">Behind the scenes, the Entity Designer generates a set of Visual Basic .NET classes.</span></span> <span data-ttu-id="60a79-185">您可以通過從解決方案資源管理器視窗中打開 MoviesDBModel.Designer.vb 檔來查看這些類。</span><span class="sxs-lookup"><span data-stu-id="60a79-185">You can view these classes by opening the MoviesDBModel.Designer.vb file from the Solution Explorer window.</span></span>

<span data-ttu-id="60a79-186">不要修改 Designer.vb 檔中的代碼,因為下次使用實體設計器時,您的更改將被覆蓋。</span><span class="sxs-lookup"><span data-stu-id="60a79-186">Don't modify the code in the Designer.vb file since your changes will be overwritten the next time you use the Entity Designer.</span></span> <span data-ttu-id="60a79-187">如果要擴展在 Designer.vb 檔中定義的實體類別的功能,則可以在單獨的檔案中建立*部分類別*。</span><span class="sxs-lookup"><span data-stu-id="60a79-187">If you want to extend the functionality of the entity classes defined in the Designer.vb file then you can create *partial classes* in separate files.</span></span>

#### <a name="selecting-database-records-with-the-entity-framework"></a><span data-ttu-id="60a79-188">使用實體框架選擇資料庫記錄</span><span class="sxs-lookup"><span data-stu-id="60a79-188">Selecting Database Records with the Entity Framework</span></span>

<span data-ttu-id="60a79-189">讓我們通過創建顯示影片記錄列表的頁面開始構建影片資料庫應用程式。</span><span class="sxs-lookup"><span data-stu-id="60a79-189">Let's start building our Movie Database application by creating a page that displays a list of movie records.</span></span> <span data-ttu-id="60a79-190">清單 1 中的主控制器公開名為 Index() 的操作。</span><span class="sxs-lookup"><span data-stu-id="60a79-190">The Home controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="60a79-191">索引() 操作利用實體框架從影片資料庫表中返回所有影片記錄。</span><span class="sxs-lookup"><span data-stu-id="60a79-191">The Index() action returns all of the movie records from the Movie database table by taking advantage of the Entity Framework.</span></span>

<span data-ttu-id="60a79-192">**清單1 = 控制器\主控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="60a79-192">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample1.vb)]

<span data-ttu-id="60a79-193">請注意,清單 1 中的控制器包括一個構造函數。</span><span class="sxs-lookup"><span data-stu-id="60a79-193">Notice that the controller in Listing 1 includes a constructor.</span></span> <span data-ttu-id="60a79-194">建構函數初始化名為\_db 的類級欄位。</span><span class="sxs-lookup"><span data-stu-id="60a79-194">The constructor initializes a class-level field named \_db.</span></span> <span data-ttu-id="60a79-195">db\_欄位表示由Microsoft實體架構生成的資料庫實體。</span><span class="sxs-lookup"><span data-stu-id="60a79-195">The \_db field represents the database entities generated by the Microsoft Entity Framework.</span></span> <span data-ttu-id="60a79-196">db\_欄位是實體設計器生成的 MoviesDBEntity 類的實例。</span><span class="sxs-lookup"><span data-stu-id="60a79-196">The \_db field is an instance of the MoviesDBEntities class that was generated by the Entity Designer.</span></span>

<span data-ttu-id="60a79-197">db\_欄位在 Index() 操作中使用,以從「影片」資料庫表中檢索記錄。</span><span class="sxs-lookup"><span data-stu-id="60a79-197">The \_db field is used within the Index() action to retrieve the records from the Movies database table.</span></span> <span data-ttu-id="60a79-198">表達式\_db。MovieSet 表示「影片」資料庫表中的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="60a79-198">The expression \_db.MovieSet represents all of the records from the Movies database table.</span></span> <span data-ttu-id="60a79-199">ToList() 方法用於將影片集轉換為影片物件的通用集合:清單(影片)。</span><span class="sxs-lookup"><span data-stu-id="60a79-199">The ToList() method is used to convert the set of movies into a generic collection of Movie objects: List( Of Movie).</span></span>

<span data-ttu-id="60a79-200">影片記錄在 LINQ 到實體的幫助下檢索。</span><span class="sxs-lookup"><span data-stu-id="60a79-200">The movie records are retrieved with the help of LINQ to Entities.</span></span> <span data-ttu-id="60a79-201">清單 1 中的 Index() 操作使用 LINQ*方法語法*來檢索資料庫記錄集。</span><span class="sxs-lookup"><span data-stu-id="60a79-201">The Index() action in Listing 1 uses LINQ *method syntax* to retrieve the set of database records.</span></span> <span data-ttu-id="60a79-202">如果您願意,可以使用 LINQ*查詢文法*。</span><span class="sxs-lookup"><span data-stu-id="60a79-202">If you prefer, you can use LINQ *query syntax* instead.</span></span> <span data-ttu-id="60a79-203">以下兩個語句執行相同的操作:</span><span class="sxs-lookup"><span data-stu-id="60a79-203">The following two statements do the very same thing:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample2.vb)]

<span data-ttu-id="60a79-204">使用您認為最直觀的 LINQ 語法(方法語法或查詢語法)。</span><span class="sxs-lookup"><span data-stu-id="60a79-204">Use whichever LINQ syntax – method syntax or query syntax – that you find most intuitive.</span></span> <span data-ttu-id="60a79-205">這兩種方法在性能上沒有差別 ,唯一的區別是風格。</span><span class="sxs-lookup"><span data-stu-id="60a79-205">There is no difference in performance between the two approaches – the only difference is style.</span></span>

<span data-ttu-id="60a79-206">清單 2 中的檢視用於顯示影片記錄。</span><span class="sxs-lookup"><span data-stu-id="60a79-206">The view in Listing 2 is used to display the movie records.</span></span>

<span data-ttu-id="60a79-207">**清單 2 = 檢視\home_Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="60a79-207">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample3.aspx)]

<span data-ttu-id="60a79-208">清單 2 中的檢視包含一個 **「每個」** 迴圈,該迴圈遍歷每個影片記錄並顯示影片記錄的標題和導演屬性的值。</span><span class="sxs-lookup"><span data-stu-id="60a79-208">The view in Listing 2 contains a **For Each** loop that iterates through each movie record and displays the values of the movie record's Title and Director properties.</span></span> <span data-ttu-id="60a79-209">請注意,每個記錄旁邊都會顯示"編輯"和"刪除"連結。</span><span class="sxs-lookup"><span data-stu-id="60a79-209">Notice that an Edit and Delete link is displayed next to each record.</span></span> <span data-ttu-id="60a79-210">此外,檢視底部還顯示「添加影片」連結(參見圖 7)。</span><span class="sxs-lookup"><span data-stu-id="60a79-210">Furthermore, an Add Movie link appears at the bottom of the view (see Figure 7).</span></span>

<span data-ttu-id="60a79-211">**圖 7 = 索引檢視**</span><span class="sxs-lookup"><span data-stu-id="60a79-211">**Figure 7 – The Index view**</span></span>

![clip_image014](creating-model-classes-with-the-entity-framework-vb/_static/image7.jpg)

<span data-ttu-id="60a79-213">索引檢視是*鍵入的檢視*。</span><span class="sxs-lookup"><span data-stu-id="60a79-213">The Index view is a *typed view*.</span></span> <span data-ttu-id="60a79-214">索引檢視具有&lt;%@ Page&gt; % 指令,該指令包含繼承屬性。</span><span class="sxs-lookup"><span data-stu-id="60a79-214">The Index view has a &lt;%@ Page %&gt; directive that includes an Inherits attribute.</span></span> <span data-ttu-id="60a79-215">繼承屬性將 ViewData.Model 屬性強制轉換為影片物件的強類型泛型清單集合 - 清單(影片)。</span><span class="sxs-lookup"><span data-stu-id="60a79-215">The Inherits attribute casts the ViewData.Model property to a strongly typed generic List collection of Movie objects – a List(Of Movie).</span></span>

## <a name="inserting-database-records-with-the-entity-framework"></a><span data-ttu-id="60a79-216">將資料庫記錄插入實體框架</span><span class="sxs-lookup"><span data-stu-id="60a79-216">Inserting Database Records with the Entity Framework</span></span>

<span data-ttu-id="60a79-217">您可以使用實體框架輕鬆將新記錄插入到資料庫表中。</span><span class="sxs-lookup"><span data-stu-id="60a79-217">You can use the Entity Framework to make it easy to insert new records into a database table.</span></span> <span data-ttu-id="60a79-218">清單3包含添加到主控制器類的兩個新操作,可用於將新記錄插入到 Movie 資料庫表中。</span><span class="sxs-lookup"><span data-stu-id="60a79-218">Listing 3 contains two new actions added to the Home controller class that you can use to insert new records into the Movie database table.</span></span>

<span data-ttu-id="60a79-219">**清單3 = 控制器\主控制器.vb(新增方法)**</span><span class="sxs-lookup"><span data-stu-id="60a79-219">**Listing 3 – Controllers\HomeController.vb (Add methods)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample4.vb)]

<span data-ttu-id="60a79-220">第一個 Add() 操作僅返回檢視。</span><span class="sxs-lookup"><span data-stu-id="60a79-220">The first Add() action simply returns a view.</span></span> <span data-ttu-id="60a79-221">該檢視包含用於添加新影片資料庫記錄的窗體(參見圖 8)。</span><span class="sxs-lookup"><span data-stu-id="60a79-221">The view contains a form for adding a new movie database record (see Figure 8).</span></span> <span data-ttu-id="60a79-222">提交表單時,將調用第二個 Add() 操作。</span><span class="sxs-lookup"><span data-stu-id="60a79-222">When you submit the form, the second Add() action is invoked.</span></span>

<span data-ttu-id="60a79-223">請注意,第二個 Add() 操作用 AcceptVerbs 屬性進行修飾。</span><span class="sxs-lookup"><span data-stu-id="60a79-223">Notice that the second Add() action is decorated with the AcceptVerbs attribute.</span></span> <span data-ttu-id="60a79-224">僅當執行 HTTP POST 操作時,才能呼叫此操作。</span><span class="sxs-lookup"><span data-stu-id="60a79-224">This action can be invoked only when performing an HTTP POST operation.</span></span> <span data-ttu-id="60a79-225">換句話說,此操作只能在發佈 HTML 窗體時調用。</span><span class="sxs-lookup"><span data-stu-id="60a79-225">In other words, this action can only be invoked when posting an HTML form.</span></span>

<span data-ttu-id="60a79-226">第二個 Add() 操作在 ASP.NET MVC TryUpdateModel() 方法的幫助下創建實體框架影片類的新實例。</span><span class="sxs-lookup"><span data-stu-id="60a79-226">The second Add() action creates a new instance of the Entity Framework Movie class with the help of the ASP.NET MVC TryUpdateModel() method.</span></span> <span data-ttu-id="60a79-227">TryUpdateModel() 方法獲取傳遞給 Add() 方法的窗體集合中的欄位,並將這些 HTML 表單欄位的值分配給 Movie 類。</span><span class="sxs-lookup"><span data-stu-id="60a79-227">The TryUpdateModel() method takes the fields in the FormCollection passed to the Add() method and assigns the values of these HTML form fields to the Movie class.</span></span>

<span data-ttu-id="60a79-228">使用實體框架時,在使用 TryUpdateModel 或 UpdateModel 方法更新實體類的屬性時,必須提供屬性的「白名單」。</span><span class="sxs-lookup"><span data-stu-id="60a79-228">When using the Entity Framework, you must supply a "white list" of properties when using the TryUpdateModel or UpdateModel methods to update the properties of an entity class.</span></span>

<span data-ttu-id="60a79-229">接下來,Add() 操作執行一些簡單的表單驗證。</span><span class="sxs-lookup"><span data-stu-id="60a79-229">Next, the Add() action performs some simple form validation.</span></span> <span data-ttu-id="60a79-230">該操作驗證"標題"和"控制器"屬性是否具有值。</span><span class="sxs-lookup"><span data-stu-id="60a79-230">The action verifies that both the Title and Director properties have values.</span></span> <span data-ttu-id="60a79-231">如果存在驗證錯誤,則會向 ModelState 添加驗證錯誤消息。</span><span class="sxs-lookup"><span data-stu-id="60a79-231">If there is a validation error, then a validation error message is added to ModelState.</span></span>

<span data-ttu-id="60a79-232">如果沒有驗證錯誤,則在實體框架的説明下,將新的影片記錄添加到「電影」資料庫表。</span><span class="sxs-lookup"><span data-stu-id="60a79-232">If there are no validation errors then a new movie record is added to the Movies database table with the help of the Entity Framework.</span></span> <span data-ttu-id="60a79-233">新記錄將新增到資料庫中,並帶有以下兩行代碼:</span><span class="sxs-lookup"><span data-stu-id="60a79-233">The new record is added to the database with the following two lines of code:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample5.vb)]

<span data-ttu-id="60a79-234">第一行代碼將新的影片實體添加到實體框架正在跟蹤的影片集中。</span><span class="sxs-lookup"><span data-stu-id="60a79-234">The first line of code adds the new Movie entity to the set of movies being tracked by the Entity Framework.</span></span> <span data-ttu-id="60a79-235">第二行代碼將保存對被跟蹤回基礎資料庫的"電影"所做的任何更改。</span><span class="sxs-lookup"><span data-stu-id="60a79-235">The second line of code saves whatever changes have been made to the Movies being tracked back to the underlying database.</span></span>

<span data-ttu-id="60a79-236">**圖 8 = 新增檢視**</span><span class="sxs-lookup"><span data-stu-id="60a79-236">**Figure 8 – The Add view**</span></span>

![clip_image016](creating-model-classes-with-the-entity-framework-vb/_static/image8.jpg)

## <a name="updating-database-records-with-the-entity-framework"></a><span data-ttu-id="60a79-238">使用實體框架更新資料庫記錄</span><span class="sxs-lookup"><span data-stu-id="60a79-238">Updating Database Records with the Entity Framework</span></span>

<span data-ttu-id="60a79-239">您可以採用幾乎相同的方法,使用實體框架編輯資料庫記錄,就像我們剛才採用的方法插入新的資料庫記錄一樣。</span><span class="sxs-lookup"><span data-stu-id="60a79-239">You can follow almost the same approach to edit a database record with the Entity Framework as the approach that we just followed to insert a new database record.</span></span> <span data-ttu-id="60a79-240">清單4包含兩個名為 Edit() 的新控制器操作。</span><span class="sxs-lookup"><span data-stu-id="60a79-240">Listing 4 contains two new controller actions named Edit().</span></span> <span data-ttu-id="60a79-241">第一個 Edit() 操作傳回用於編輯影片記錄的 HTML 窗體。</span><span class="sxs-lookup"><span data-stu-id="60a79-241">The first Edit() action returns an HTML form for editing a movie record.</span></span> <span data-ttu-id="60a79-242">第二個 Edit() 操作嘗試更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="60a79-242">The second Edit() action attempts to update the database.</span></span>

<span data-ttu-id="60a79-243">**清單4 = 控制器\主控制器.vb(編輯方法)**</span><span class="sxs-lookup"><span data-stu-id="60a79-243">**Listing 4 – Controllers\HomeController.vb (Edit methods)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample6.vb)]

<span data-ttu-id="60a79-244">第二個 Edit() 操作首先從與正在編輯的影片的 ID 匹配的資料庫檢索影片記錄。</span><span class="sxs-lookup"><span data-stu-id="60a79-244">The second Edit() action starts by retrieving the Movie record from the database that matches the Id of the movie being edited.</span></span> <span data-ttu-id="60a79-245">以下 LINQ 到實體語片取得與特定 Id 符合的第一個資料庫紀錄:</span><span class="sxs-lookup"><span data-stu-id="60a79-245">The following LINQ to Entities statement grabs the first database record that matches a particular Id:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample7.vb)]

<span data-ttu-id="60a79-246">接下來,TryUpdateModel() 方法用於將 HTML 表單欄位的值分配給影片實體的屬性。</span><span class="sxs-lookup"><span data-stu-id="60a79-246">Next, the TryUpdateModel() method is used to assign the values of the HTML form fields to the properties of the movie entity.</span></span> <span data-ttu-id="60a79-247">請注意,提供了一個白名單,以指定要更新的確切屬性。</span><span class="sxs-lookup"><span data-stu-id="60a79-247">Notice that a white list is supplied to specify the exact properties to update.</span></span>

<span data-ttu-id="60a79-248">接下來,執行一些簡單的驗證,以驗證影片標題和導演屬性是否具有值。</span><span class="sxs-lookup"><span data-stu-id="60a79-248">Next, some simple validation is performed to verify that both the Movie Title and Director properties have values.</span></span> <span data-ttu-id="60a79-249">如果任一屬性缺少值,則驗證錯誤消息將添加到 ModelState 和 ModelState。IsValid 返回該值為 false。</span><span class="sxs-lookup"><span data-stu-id="60a79-249">If either property is missing a value, then a validation error message is added to ModelState and ModelState.IsValid returns the value false.</span></span>

<span data-ttu-id="60a79-250">最後,如果沒有驗證錯誤,則通過調用 SaveChanges() 方法,將更新基礎「電影」資料庫表與任何更改。</span><span class="sxs-lookup"><span data-stu-id="60a79-250">Finally, if there are no validation errors, then the underlying Movies database table is updated with any changes by calling the SaveChanges() method.</span></span>

<span data-ttu-id="60a79-251">編輯資料庫記錄時,需要將正在編輯的記錄的 Id 傳遞給執行資料庫更新的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="60a79-251">When editing database records, you need to pass the Id of the record being edited to the controller action that performs the database update.</span></span> <span data-ttu-id="60a79-252">否則,控制器操作將不知道要在基礎資料庫中更新哪個記錄。</span><span class="sxs-lookup"><span data-stu-id="60a79-252">Otherwise, the controller action will not know which record to update in the underlying database.</span></span> <span data-ttu-id="60a79-253">清單 5 中包含的「編輯」檢視包含隱藏表單欄位,該欄位表示要編輯的資料庫記錄的識別碼。</span><span class="sxs-lookup"><span data-stu-id="60a79-253">The Edit view, contained in Listing 5, includes a hidden form field that represents the Id of the database record being edited.</span></span>

<span data-ttu-id="60a79-254">**清單5 = 檢視\home_編輯.aspx**</span><span class="sxs-lookup"><span data-stu-id="60a79-254">**Listing 5 – Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a><span data-ttu-id="60a79-255">使用實體框架移除資料庫記錄</span><span class="sxs-lookup"><span data-stu-id="60a79-255">Deleting Database Records with the Entity Framework</span></span>

<span data-ttu-id="60a79-256">本教學中需要處理的最終資料庫操作是刪除資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="60a79-256">The final database operation, which we need to tackle in this tutorial, is deleting database records.</span></span> <span data-ttu-id="60a79-257">您可以使用清單 6 中的控制器操作刪除特定的資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="60a79-257">You can use the controller action in Listing 6 to delete a particular database record.</span></span>

<span data-ttu-id="60a79-258">**清單6 -- [控制器]主控制器.vb(刪除操作)**</span><span class="sxs-lookup"><span data-stu-id="60a79-258">**Listing 6 -- \Controllers\HomeController.vb (Delete action)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample9.vb)]

<span data-ttu-id="60a79-259">Delete() 操作首先檢索與傳遞給該操作的 ID 匹配的 Movie 實體。</span><span class="sxs-lookup"><span data-stu-id="60a79-259">The Delete() action first retrieves the Movie entity that matches the Id passed to the action.</span></span> <span data-ttu-id="60a79-260">接下來,通過調用 DeleteObject() 方法後跟 SaveChanges() 方法從資料庫中刪除影片。</span><span class="sxs-lookup"><span data-stu-id="60a79-260">Next, the movie is deleted from the database by calling the DeleteObject() method followed by the SaveChanges() method.</span></span> <span data-ttu-id="60a79-261">最後,使用者被重定向回索引視圖。</span><span class="sxs-lookup"><span data-stu-id="60a79-261">Finally, the user is redirected back to the Index view.</span></span>

## <a name="summary"></a><span data-ttu-id="60a79-262">總結</span><span class="sxs-lookup"><span data-stu-id="60a79-262">Summary</span></span>

<span data-ttu-id="60a79-263">本教學的目的是展示如何利用ASP.NET MVC 和Microsoft 實體架構建構資料庫驅動的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="60a79-263">The purpose of this tutorial was to demonstrate how you can build database-driven web applications by taking advantage of ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="60a79-264">您學習了如何建構應用程式,讓您能夠選擇、插入、更新和刪除資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="60a79-264">You learned how to build an application that enables you to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="60a79-265">首先,我們討論了如何使用實體數據模型嚮導從 Visual Studio 中生成實體數據模型。</span><span class="sxs-lookup"><span data-stu-id="60a79-265">First, we discussed how you can use the Entity Data Model Wizard to generate an Entity Data Model from within Visual Studio.</span></span> <span data-ttu-id="60a79-266">接下來,您將學習如何使用 LINQ 到實體從資料庫表中檢索一組資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="60a79-266">Next, you learn how to use LINQ to Entities to retrieve a set of database records from a database table.</span></span> <span data-ttu-id="60a79-267">最後,我們使用實體框架插入、更新和刪除資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="60a79-267">Finally, we used the Entity Framework to insert, update, and delete database records.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="60a79-268">[前一個](validation-with-the-data-annotation-validators-cs.md)
> [下一個](creating-model-classes-with-linq-to-sql-vb.md)</span><span class="sxs-lookup"><span data-stu-id="60a79-268">[Previous](validation-with-the-data-annotation-validators-cs.md)
[Next](creating-model-classes-with-linq-to-sql-vb.md)</span></span>
