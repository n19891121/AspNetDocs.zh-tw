---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
title: 建立模型類別使用 LINQ to SQL (C#) |Microsoft Docs
author: microsoft
description: 本教學課程的目標是說明建立 ASP.NET MVC 應用程式的模型類別的一種方法。 在本教學課程中，您會學習如何建置模型 c...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f84b4a16-e8bb-49e8-87a0-1832879a3501
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
msc.type: authoredcontent
ms.openlocfilehash: d1895b03a2aa877bfd279995dc5647c5efefade6
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59414201"
---
# <a name="creating-model-classes-with-linq-to-sql-c"></a><span data-ttu-id="f3fd5-104">使用 LINQ to SQL 建立模型類別 (C#)</span><span class="sxs-lookup"><span data-stu-id="f3fd5-104">Creating Model Classes with LINQ to SQL (C#)</span></span>

<span data-ttu-id="f3fd5-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f3fd5-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="f3fd5-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="f3fd5-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_CS.pdf)

> <span data-ttu-id="f3fd5-107">本教學課程的目標是說明建立 ASP.NET MVC 應用程式的模型類別的一種方法。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-107">The goal of this tutorial is to explain one method of creating model classes for an ASP.NET MVC application.</span></span> <span data-ttu-id="f3fd5-108">在本教學課程中，您已了解如何建置模型類別，並藉由利用 Microsoft LINQ to SQL 中執行資料庫存取權。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-108">In this tutorial, you learn how to build model classes and perform database access by taking advantage of Microsoft LINQ to SQL.</span></span>


<span data-ttu-id="f3fd5-109">本教學課程的目標是說明建立 ASP.NET MVC 應用程式的模型類別的一種方法。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-109">The goal of this tutorial is to explain one method of creating model classes for an ASP.NET MVC application.</span></span> <span data-ttu-id="f3fd5-110">在本教學課程，了解如何建置模型類別，並藉由利用 Microsoft LINQ to SQL 中執行資料庫存取權</span><span class="sxs-lookup"><span data-stu-id="f3fd5-110">In this tutorial, you learn how to build model classes and perform database access by taking advantage of Microsoft LINQ to SQL</span></span>

<span data-ttu-id="f3fd5-111">在本教學課程中，我們會建置基本的影片資料庫應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-111">In this tutorial, we build a basic Movie database application.</span></span> <span data-ttu-id="f3fd5-112">我們先以最快、 最簡單的方式可能建立影片資料庫應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-112">We start by creating the Movie database application in the fastest and easiest way possible.</span></span> <span data-ttu-id="f3fd5-113">我們會執行所有存取我們的資料直接從我們的控制器動作。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-113">We perform all of our data access directly from our controller actions.</span></span>

<span data-ttu-id="f3fd5-114">接下來，您會了解如何使用儲存機制模式。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-114">Next, you learn how to use the Repository pattern.</span></span> <span data-ttu-id="f3fd5-115">使用儲存機制模式需要多一點的工作。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-115">Using the Repository pattern requires a little more work.</span></span> <span data-ttu-id="f3fd5-116">不過，採用此模式的優點是它可讓您建置可適用於應用程式變更，而且可以輕鬆地測試。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-116">However, the advantage of adopting this pattern is that it enables you to build applications that are adaptable to change and can be easily tested.</span></span>

## <a name="what-is-a-model-class"></a><span data-ttu-id="f3fd5-117">模型類別為何？</span><span class="sxs-lookup"><span data-stu-id="f3fd5-117">What is a Model Class?</span></span>

<span data-ttu-id="f3fd5-118">MVC 模型包含的所有未包含在 MVC 檢視或 MVC 控制器中的應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-118">An MVC model contains all of the application logic that is not contained in an MVC view or MVC controller.</span></span> <span data-ttu-id="f3fd5-119">特別是，MVC 模型包含的所有應用程式的商務和資料存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-119">In particular, an MVC model contains all of your application business and data access logic.</span></span>

<span data-ttu-id="f3fd5-120">您可以使用各種不同的技術來實作資料存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-120">You can use a variety of different technologies to implement your data access logic.</span></span> <span data-ttu-id="f3fd5-121">例如，您可以建置使用 Microsoft Entity Framework、 NHibernate、 Subsonic 或 ADO.NET 類別的資料存取類別。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-121">For example, you can build your data access classes using the Microsoft Entity Framework, NHibernate, Subsonic, or ADO.NET classes.</span></span>

<span data-ttu-id="f3fd5-122">在本教學課程中，我可以使用 LINQ to SQL 查詢和更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-122">In this tutorial, I use LINQ to SQL to query and update the database.</span></span> <span data-ttu-id="f3fd5-123">LINQ to SQL 會提供您與 Microsoft SQL Server 資料庫互動的非常簡單的方法。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-123">LINQ to SQL provides you with a very easy method of interacting with a Microsoft SQL Server database.</span></span> <span data-ttu-id="f3fd5-124">不過，務必了解，ASP.NET MVC 架構未繫結至 LINQ to SQL 以任何方式。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-124">However, it is important to understand that the ASP.NET MVC framework is not tied to LINQ to SQL in any way.</span></span> <span data-ttu-id="f3fd5-125">ASP.NET MVC 是與任何資料存取技術相容。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-125">ASP.NET MVC is compatible with any data access technology.</span></span>

## <a name="create-a-movie-database"></a><span data-ttu-id="f3fd5-126">建立影片資料庫</span><span class="sxs-lookup"><span data-stu-id="f3fd5-126">Create a Movie Database</span></span>

<span data-ttu-id="f3fd5-127">在本教學課程中，以說明如何建立模型類別，我們建置一個簡單的電影資料庫應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-127">In this tutorial -- in order to illustrate how you can build model classes -- we build a simple Movie database application.</span></span> <span data-ttu-id="f3fd5-128">第一個步驟是建立新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-128">The first step is to create a new database.</span></span> <span data-ttu-id="f3fd5-129">以滑鼠右鍵按一下 [應用程式\_Data 資料夾中的方案總管] 視窗，然後選取功能表選項**新增]、 [新項目**。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-129">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span> <span data-ttu-id="f3fd5-130">選取  **SQL Server 資料庫**範本，將它命名 MoviesDB.mdf，然後按一下**新增**按鈕 （請參閱 圖 1）。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-130">Select the **SQL Server Database** template, give it the name MoviesDB.mdf, and click the **Add** button (see Figure 1).</span></span>


[![A<span data-ttu-id="f3fd5-131">dding 新的 SQL Server 資料庫]</span><span class="sxs-lookup"><span data-stu-id="f3fd5-131">dding a new SQL Server Database]</span></span>(creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)

<span data-ttu-id="f3fd5-132">**圖 01**:加入新的 SQL Server 資料庫 ([按一下以檢視完整大小的影像](creating-model-classes-with-linq-to-sql-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f3fd5-132">**Figure 01**: Adding a new SQL Server Database ([Click to view full-size image](creating-model-classes-with-linq-to-sql-cs/_static/image3.png))</span></span>


<span data-ttu-id="f3fd5-133">建立新的資料庫之後，您可以按兩下 MoviesDB.mdf 檔案的應用程式中開啟資料庫\_Data 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-133">After you create the new database, you can open the database by double-clicking the MoviesDB.mdf file in the App\_Data folder.</span></span> <span data-ttu-id="f3fd5-134">按兩下 MoviesDB.mdf 檔案隨即開啟 伺服器總管 視窗 （請參閱 圖 2）。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-134">Double-clicking the MoviesDB.mdf file opens the Server Explorer window (see Figure 2).</span></span>

<span data-ttu-id="f3fd5-135">使用 Visual Web Developer 時，[伺服器總管] 視窗會呼叫 [資料庫總管] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-135">The Server Explorer window is called the Database Explorer window when using Visual Web Developer.</span></span>


[![U<span data-ttu-id="f3fd5-136">發揚光大伺服器總管] 視窗]</span><span class="sxs-lookup"><span data-stu-id="f3fd5-136">sing the Server Explorer window]</span></span>(creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)

<span data-ttu-id="f3fd5-137">**圖 02**:使用 [伺服器總管] 視窗 ([按一下以檢視完整大小的影像](creating-model-classes-with-linq-to-sql-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="f3fd5-137">**Figure 02**: Using the Server Explorer window ([Click to view full-size image](creating-model-classes-with-linq-to-sql-cs/_static/image6.png))</span></span>


<span data-ttu-id="f3fd5-138">我們需要將一個資料表加入至資料庫，表示我們的影片。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-138">We need to add one table to our database that represents our movies.</span></span> <span data-ttu-id="f3fd5-139">以滑鼠右鍵按一下 [資料表] 資料夾，然後選取功能表選項**加入新的資料表**。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-139">Right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="f3fd5-140">選取此功能表選項會開啟 資料表設計工具 （請參閱 圖 3）。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-140">Selecting this menu option opens the Table Designer (see Figure 3).</span></span>


[![U<span data-ttu-id="f3fd5-141">發揚光大伺服器總管] 視窗]</span><span class="sxs-lookup"><span data-stu-id="f3fd5-141">sing the Server Explorer window]</span></span>(creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)

<span data-ttu-id="f3fd5-142">**圖 03**:資料表設計工具 ([按一下以檢視完整大小的影像](creating-model-classes-with-linq-to-sql-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="f3fd5-142">**Figure 03**: The Table Designer ([Click to view full-size image](creating-model-classes-with-linq-to-sql-cs/_static/image9.png))</span></span>


<span data-ttu-id="f3fd5-143">我們需要將下列資料行加入至資料庫資料表：</span><span class="sxs-lookup"><span data-stu-id="f3fd5-143">We need to add the following columns to our database table:</span></span>

| **<span data-ttu-id="f3fd5-144">資料行名稱</span><span class="sxs-lookup"><span data-stu-id="f3fd5-144">Column Name</span></span>** | **<span data-ttu-id="f3fd5-145">資料類型</span><span class="sxs-lookup"><span data-stu-id="f3fd5-145">Data Type</span></span>** | **<span data-ttu-id="f3fd5-146">允許 Null</span><span class="sxs-lookup"><span data-stu-id="f3fd5-146">Allow Nulls</span></span>** |
| --- | --- | --- |
| <span data-ttu-id="f3fd5-147">ID</span><span class="sxs-lookup"><span data-stu-id="f3fd5-147">Id</span></span> | <span data-ttu-id="f3fd5-148">Int</span><span class="sxs-lookup"><span data-stu-id="f3fd5-148">Int</span></span> | <span data-ttu-id="f3fd5-149">False</span><span class="sxs-lookup"><span data-stu-id="f3fd5-149">False</span></span> |
| <span data-ttu-id="f3fd5-150">標題</span><span class="sxs-lookup"><span data-stu-id="f3fd5-150">Title</span></span> | <span data-ttu-id="f3fd5-151">Nvarchar(200)</span><span class="sxs-lookup"><span data-stu-id="f3fd5-151">Nvarchar(200)</span></span> | <span data-ttu-id="f3fd5-152">False</span><span class="sxs-lookup"><span data-stu-id="f3fd5-152">False</span></span> |
| <span data-ttu-id="f3fd5-153">總監</span><span class="sxs-lookup"><span data-stu-id="f3fd5-153">Director</span></span> | <span data-ttu-id="f3fd5-154">Nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="f3fd5-154">Nvarchar(50)</span></span> | <span data-ttu-id="f3fd5-155">False</span><span class="sxs-lookup"><span data-stu-id="f3fd5-155">False</span></span> |

<span data-ttu-id="f3fd5-156">您需要執行兩個特殊的動作識別碼資料行。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-156">You need to do two special things to the Id column.</span></span> <span data-ttu-id="f3fd5-157">首先，您需要將識別碼資料行標示為主要的索引鍵資料行中，資料表設計工具中選取資料行，然後按一下 機碼的圖示。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-157">First, you need to mark the Id column as a primary key column by selecting the column in the Table Designer and clicking the icon of a key.</span></span> <span data-ttu-id="f3fd5-158">LINQ to SQL 會要求您指定您主要的索引鍵資料行，當執行插入或更新對資料庫。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-158">LINQ to SQL requires you to specify your primary key columns when performing inserts or updates against the database.</span></span>

<span data-ttu-id="f3fd5-159">接下來，您需要將識別碼資料行標示為識別欄位中，是將值指派給**是識別**屬性 （請參閱 [圖 3]）。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-159">Next, you need to mark the Id column as an Identity column by assigning the value Yes to the **Is Identity** property (see Figure 3).</span></span> <span data-ttu-id="f3fd5-160">識別資料行是會自動指派給新的數字每當您將新的資料列加入資料表的資料行。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-160">An Identity column is a column that is assigned a new number automatically whenever you add a new row of data to a table.</span></span>

## <a name="create-linq-to-sql-classes"></a><span data-ttu-id="f3fd5-161">建立 LINQ to SQL 類別</span><span class="sxs-lookup"><span data-stu-id="f3fd5-161">Create LINQ to SQL Classes</span></span>

<span data-ttu-id="f3fd5-162">我們 MVC 的模型會包含 LINQ to SQL 類別代表 tblMovie 資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-162">Our MVC model will contain LINQ to SQL classes that represent the tblMovie database table.</span></span> <span data-ttu-id="f3fd5-163">若要建立這些 LINQ to SQL 類別最簡單方式是以滑鼠右鍵按一下 模型 資料夾中，選取**新增、 新項目**、 選取 LINQ to SQL 類別範本，將類別命名 Movie.dbml，然後按一下**新增**按鈕 （請參閱 圖 4）。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-163">The easiest way to create these LINQ to SQL classes is to right-click the Models folder, select **Add, New Item**, select the LINQ to SQL Classes template, give the classes the name Movie.dbml, and click the **Add** button (see Figure 4).</span></span>


[![C<span data-ttu-id="f3fd5-164">reating LINQ to SQL 類別]</span><span class="sxs-lookup"><span data-stu-id="f3fd5-164">reating LINQ to SQL classes]</span></span>(creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)

<span data-ttu-id="f3fd5-165">**圖 04**:建立 LINQ to SQL 類別 ([按一下以檢視完整大小的影像](creating-model-classes-with-linq-to-sql-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="f3fd5-165">**Figure 04**: Creating LINQ to SQL classes ([Click to view full-size image](creating-model-classes-with-linq-to-sql-cs/_static/image12.png))</span></span>


<span data-ttu-id="f3fd5-166">立即建立影片的 LINQ to SQL 類別之後，會顯示物件關聯式設計工具。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-166">Immediately after you create the Movie LINQ to SQL Classes, the Object Relational Designer appears.</span></span> <span data-ttu-id="f3fd5-167">您可以將資料庫資料表從 [伺服器總管] 視窗拖曳至物件關聯式設計工具建立 LINQ to SQL 類別代表特定的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-167">You can drag database tables from the Server Explorer window onto the Object Relational Designer to create LINQ to SQL Classes that represent particular database tables.</span></span> <span data-ttu-id="f3fd5-168">我們需要加入 tblMovie 資料庫資料表拖曳至物件關聯式設計工具 （請參閱 [圖 5]）。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-168">We need to add the tblMovie database table onto the Object Relational Designer (see Figure 5).</span></span>


[![U<span data-ttu-id="f3fd5-169">發揚光大物件關聯式設計工具]</span><span class="sxs-lookup"><span data-stu-id="f3fd5-169">sing the Object Relational Designer]</span></span>(creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)

<span data-ttu-id="f3fd5-170">**圖 05**:使用物件關聯式設計工具 ([按一下以檢視完整大小的影像](creating-model-classes-with-linq-to-sql-cs/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="f3fd5-170">**Figure 05**: Using the Object Relational Designer  ([Click to view full-size image](creating-model-classes-with-linq-to-sql-cs/_static/image15.png))</span></span>


<span data-ttu-id="f3fd5-171">根據預設，物件關聯式設計工具會建立具有相同名稱做為資料庫資料表拖曳至設計工具的類別。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-171">By default, the Object Relational Designer creates a class with the very same name as the database table that you drag onto the Designer.</span></span> <span data-ttu-id="f3fd5-172">不過，我們不想要呼叫我們的類別`tblMovie`。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-172">However, we don't want to call our class `tblMovie`.</span></span> <span data-ttu-id="f3fd5-173">因此，按一下 類別設計工具中的名稱，並將變更影片的類別名稱。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-173">Therefore, click the name of the class in the Designer and change the name of the class to Movie.</span></span>

<span data-ttu-id="f3fd5-174">最後，請記得按一下 **儲存**按鈕 （磁片的圖片） 來儲存 LINQ to SQL 類別。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-174">Finally, remember to click the **Save** button (the picture of the floppy) to save the LINQ to SQL Classes.</span></span> <span data-ttu-id="f3fd5-175">否則，LINQ to SQL 類別不會產生由物件關聯式設計工具。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-175">Otherwise, the LINQ to SQL Classes won't be generated by the Object Relational Designer.</span></span>

## <a name="using-linq-to-sql-in-a-controller-action"></a><span data-ttu-id="f3fd5-176">使用 LINQ to SQL 中的控制器動作</span><span class="sxs-lookup"><span data-stu-id="f3fd5-176">Using LINQ to SQL in a Controller Action</span></span>

<span data-ttu-id="f3fd5-177">現在，我們有我們的 LINQ to SQL 類別時，我們可以使用這些類別來擷取資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-177">Now that we have our LINQ to SQL classes, we can use these classes to retrieve data from the database.</span></span> <span data-ttu-id="f3fd5-178">在本節中，您將了解如何使用 LINQ to SQL 類別，直接在控制器動作。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-178">In this section, you learn how to use LINQ to SQL classes directly within a controller action.</span></span> <span data-ttu-id="f3fd5-179">我們會在 MVC 檢視中顯示 tblMovies 資料庫資料表中的電影的清單。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-179">We'll display the list of movies from the tblMovies database table in an MVC view.</span></span>

<span data-ttu-id="f3fd5-180">首先，我們需要修改 HomeController 類別。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-180">First, we need to modify the HomeController class.</span></span> <span data-ttu-id="f3fd5-181">這個類別可在您的應用程式的 [控制器] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-181">This class can be found in the Controllers folder of your application.</span></span> <span data-ttu-id="f3fd5-182">修改類別，使它看起來像 列表 1 中的類別。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-182">Modify the class so it looks like the class in Listing 1.</span></span>

**<span data-ttu-id="f3fd5-183">列表 1 –</span><span class="sxs-lookup"><span data-stu-id="f3fd5-183">Listing 1 –</span></span> `Controllers\HomeController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample1.cs)]

<span data-ttu-id="f3fd5-184">`Index()`列表 1 中的動作是使用 LINQ to SQL DataContext 類別 ( `MovieDataContext`) 來代表`MoviesDB`資料庫。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-184">The `Index()` action in Listing 1 uses a LINQ to SQL DataContext class (the `MovieDataContext`) to represent the `MoviesDB` database.</span></span> <span data-ttu-id="f3fd5-185">`MoveDataContext`由 Visual Studio 物件關聯式設計工具產生的類別。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-185">The `MoveDataContext` class was generated by the Visual Studio Object Relational Designer.</span></span>

<span data-ttu-id="f3fd5-186">LINQ 查詢會擷取所有從電影 DataContext 對執行`tblMovies`資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-186">A LINQ query is performed against the DataContext to retrieve all of the movies from the `tblMovies` database table.</span></span> <span data-ttu-id="f3fd5-187">電影清單指派給本機變數，名為`movies`。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-187">The list of movies is assigned to a local variable named `movies`.</span></span> <span data-ttu-id="f3fd5-188">最後的電影清單會傳遞至檢視檢視資料。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-188">Finally, the list of movies is passed to the view through view data.</span></span>

<span data-ttu-id="f3fd5-189">若要顯示電影，我們接下來要修改索引檢視表。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-189">In order to show the movies, we next need to modify the Index view.</span></span> <span data-ttu-id="f3fd5-190">您可以找到 [索引] 檢視中的`Views\Home\`資料夾。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-190">You can find the Index view in the `Views\Home\` folder.</span></span> <span data-ttu-id="f3fd5-191">更新 索引 檢視，使它看起來像 列表 2 中的檢視。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-191">Update the Index view so that it looks like the view in Listing 2.</span></span>

**<span data-ttu-id="f3fd5-192">列表 2 –</span><span class="sxs-lookup"><span data-stu-id="f3fd5-192">Listing 2 –</span></span> `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample2.aspx)]

<span data-ttu-id="f3fd5-193">請注意，修改過的 [索引] 檢視包含`<%@ import namespace %>`頂端的檢視指示詞。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-193">Notice that the modified Index view includes an `<%@ import namespace %>` directive at the top of the view.</span></span> <span data-ttu-id="f3fd5-194">這個指示詞會匯入`MvcApplication1.Models namespace`。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-194">This directive imports the `MvcApplication1.Models namespace`.</span></span> <span data-ttu-id="f3fd5-195">我們需要此命名空間，才能使用`model`類別 – 特別是，`Movie`類別-在檢視中的。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-195">We need this namespace in order to work with the `model` classes – in particular, the `Movie` class -- in the view.</span></span>

<span data-ttu-id="f3fd5-196">列表 2 中的檢視包含`foreach`逐一查看所有項目所代表的迴圈`ViewData.Model`屬性。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-196">The view in Listing 2 contains a `foreach` loop that iterates through all of the items represented by the `ViewData.Model` property.</span></span> <span data-ttu-id="f3fd5-197">值`Title`屬性會顯示每個`movie`。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-197">The value of the `Title` property is displayed for each `movie`.</span></span>

<span data-ttu-id="f3fd5-198">請注意，值`ViewData.Model`屬性會轉換成`IEnumerable`。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-198">Notice that the value of the `ViewData.Model` property is cast to an `IEnumerable`.</span></span> <span data-ttu-id="f3fd5-199">這是必要的內容執行迴圈`ViewData.Model`。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-199">This is necessary in order to loop through the contents of `ViewData.Model`.</span></span> <span data-ttu-id="f3fd5-200">此處的另一個選項是建立強型別`view`。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-200">Another option here is to create a strongly-typed `view`.</span></span> <span data-ttu-id="f3fd5-201">當您建立強型別`view`，您將轉型`ViewData.Model`中檢視的程式碼後置類別的特定類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-201">When you create a strongly-typed `view`, you cast the `ViewData.Model` property to a particular type in a view's code-behind class.</span></span>

<span data-ttu-id="f3fd5-202">如果您執行應用程式之後修改`HomeController`類別及索引檢視，然後就會出現空白頁面。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-202">If you run the application after modifying the `HomeController` class and the Index view then you will get a blank page.</span></span> <span data-ttu-id="f3fd5-203">您將取得空白的頁面，因為在沒有影片記錄`tblMovies`資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-203">You'll get a blank page because there are no movie records in the `tblMovies` database table.</span></span>

<span data-ttu-id="f3fd5-204">若要新增記錄`tblMovies`資料庫資料表，以滑鼠右鍵按一下`tblMovies`資料庫 （在 Visual Web Developer 的 [資料庫總管] 視窗） 上的 [伺服器總管] 視窗中的資料表，然後選取 [顯示資料表資料] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-204">In order to add records to the `tblMovies` database table, right-click the `tblMovies` database table in the Server Explorer window (Database Explorer window in Visual Web Developer) and select the menu option Show Table Data.</span></span> <span data-ttu-id="f3fd5-205">您可以插入`movie`方格隨即出現 （請參閱 圖 6） 的記錄。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-205">You can insert `movie` records by using the grid that appears (see Figure 6).</span></span>


[![I<span data-ttu-id="f3fd5-206">nserting 影片]</span><span class="sxs-lookup"><span data-stu-id="f3fd5-206">nserting movies]</span></span>(creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)

<span data-ttu-id="f3fd5-207">**圖 06**:插入電影 ([按一下以檢視完整大小的影像](creating-model-classes-with-linq-to-sql-cs/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="f3fd5-207">**Figure 06**: Inserting movies([Click to view full-size image](creating-model-classes-with-linq-to-sql-cs/_static/image18.png))</span></span>


<span data-ttu-id="f3fd5-208">您將加入到某些資料庫記錄之後`tblMovies`資料表，並執行應用程式，您會看到 [圖 7] 中的頁面。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-208">After you add some database records to the `tblMovies` table, and you run the application, you'll see the page in Figure 7.</span></span> <span data-ttu-id="f3fd5-209">所有的電影資料庫記錄會顯示在項目符號清單。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-209">All of the movie database records are displayed in a bulleted list.</span></span>


[![D<span data-ttu-id="f3fd5-210">具備索引檢視的 isplaying 影片]</span><span class="sxs-lookup"><span data-stu-id="f3fd5-210">isplaying movies with the Index view]</span></span>(creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)

<span data-ttu-id="f3fd5-211">**圖 07**:顯示與索引檢視的影片 ([按一下以檢視完整大小的影像](creating-model-classes-with-linq-to-sql-cs/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="f3fd5-211">**Figure 07**: Displaying movies with the Index view([Click to view full-size image](creating-model-classes-with-linq-to-sql-cs/_static/image21.png))</span></span>


## <a name="using-the-repository-pattern"></a><span data-ttu-id="f3fd5-212">使用儲存機制模式</span><span class="sxs-lookup"><span data-stu-id="f3fd5-212">Using the Repository Pattern</span></span>

<span data-ttu-id="f3fd5-213">在上一節中，我們會使用 LINQ to SQL 類別，直接在控制器動作。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-213">In the previous section, we used LINQ to SQL classes directly within a controller action.</span></span> <span data-ttu-id="f3fd5-214">我們使用了`MovieDataContext`直接從類別`Index()`控制器動作。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-214">We used the `MovieDataContext` class directly from the `Index()` controller action.</span></span> <span data-ttu-id="f3fd5-215">沒有任何問題，在簡單的應用程式的情況下這項操作。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-215">There is nothing wrong with doing this in the case of a simple application.</span></span> <span data-ttu-id="f3fd5-216">不過，在控制器類別中的直接使用 LINQ to SQL 工作會產生問題，當您要建置更複雜的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-216">However, working directly with LINQ to SQL in a controller class creates problems when you need to build a more complex application.</span></span>

<span data-ttu-id="f3fd5-217">使用 LINQ to SQL 中的控制器類別使您更難以在未來切換資料存取技術。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-217">Using LINQ to SQL within a controller class makes it difficult to switch data access technologies in the future.</span></span> <span data-ttu-id="f3fd5-218">例如，您可能會決定切換到使用做為您的資料存取技術的 Microsoft Entity Framework 使用 Microsoft LINQ to SQL。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-218">For example, you might decide to switch from using Microsoft LINQ to SQL to using the Microsoft Entity Framework as your data access technology.</span></span> <span data-ttu-id="f3fd5-219">在此情況下，您必須重寫每個控制站可存取您的應用程式內的資料庫。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-219">In that case, you would need to rewrite every controller that accesses the database within your application.</span></span>

<span data-ttu-id="f3fd5-220">使用 LINQ to SQL 中的控制器類別也很難建置您的應用程式的單元測試。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-220">Using LINQ to SQL within a controller class also makes it difficult to build unit tests for your application.</span></span> <span data-ttu-id="f3fd5-221">一般來說，您不想要執行單元測試時，與資料庫互動。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-221">Normally, you do not want to interact with a database when performing unit tests.</span></span> <span data-ttu-id="f3fd5-222">您想要使用您的單元測試來測試您的應用程式邏輯而非您資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-222">You want to use your unit tests to test your application logic and not your database server.</span></span>

<span data-ttu-id="f3fd5-223">若要建立 MVC 應用程式中，這是更適用於未來的變更可以更輕鬆地測試，您應該考慮使用儲存機制模式。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-223">In order to build an MVC application that is more adaptable to future change and that can be more easily tested, you should consider using the Repository pattern.</span></span> <span data-ttu-id="f3fd5-224">當您使用儲存機制模式時，您會建立個別的存放庫類別，其中包含所有的資料庫存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-224">When you use the Repository pattern, you create a separate repository class that contains all of your database access logic.</span></span>

<span data-ttu-id="f3fd5-225">當您建立儲存機制類別時，您會建立表示所有儲存機制類別所使用的方法的介面。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-225">When you create the repository class, you create an interface that represents all of the methods used by the repository class.</span></span> <span data-ttu-id="f3fd5-226">在您的控制器，您撰寫您的程式碼的介面，而不是存放庫。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-226">Within your controllers, you write your code against the interface instead of the repository.</span></span> <span data-ttu-id="f3fd5-227">如此一來，您可以實作存放庫在未來使用不同的資料存取技術。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-227">That way, you can implement the repository using different data access technologies in the future.</span></span>

<span data-ttu-id="f3fd5-228">列表 3 中的介面稱為`IMovieRepository`，而它代表單一方法，名為`ListAll()`。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-228">The interface in Listing 3 is named `IMovieRepository` and it represents a single method named `ListAll()`.</span></span>

**<span data-ttu-id="f3fd5-229">列表 3 –</span><span class="sxs-lookup"><span data-stu-id="f3fd5-229">Listing 3 –</span></span> `Models\IMovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample3.cs)]

<span data-ttu-id="f3fd5-230">在 列表 4 中的儲存機制類別會實作`IMovieRepository`介面。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-230">The repository class in Listing 4 implements the `IMovieRepository` interface.</span></span> <span data-ttu-id="f3fd5-231">請注意，它包含一個名為方法`ListAll()`，其對應於所需的方法`IMovieRepository`介面。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-231">Notice that it contains a method named `ListAll()` that corresponds to the method required by the `IMovieRepository` interface.</span></span>

**<span data-ttu-id="f3fd5-232">列表 4 –</span><span class="sxs-lookup"><span data-stu-id="f3fd5-232">Listing 4 –</span></span> `Models\MovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample4.cs)]

<span data-ttu-id="f3fd5-233">最後，`MoviesController`表 5 中的類別會使用儲存機制模式。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-233">Finally, the `MoviesController` class in Listing 5 uses the Repository pattern.</span></span> <span data-ttu-id="f3fd5-234">它不會再使用 LINQ to SQL 類別直接。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-234">It no longer uses LINQ to SQL classes directly.</span></span>

**<span data-ttu-id="f3fd5-235">列表 5 –</span><span class="sxs-lookup"><span data-stu-id="f3fd5-235">Listing 5 –</span></span> `Controllers\MoviesController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample5.cs)]

<span data-ttu-id="f3fd5-236">請注意，`MoviesController`表 5 中的類別有兩個建構函式。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-236">Notice that the `MoviesController` class in Listing 5 has two constructors.</span></span> <span data-ttu-id="f3fd5-237">您的應用程式執行時，會呼叫第一個建構函式的無參數建構函式。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-237">The first constructor, the parameterless constructor, is called when your application is running.</span></span> <span data-ttu-id="f3fd5-238">這個建構函式建立的執行個體`MovieRepository`類別，並將它傳遞給第二個建構函式。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-238">This constructor creates an instance of the `MovieRepository` class and passes it to the second constructor.</span></span>

<span data-ttu-id="f3fd5-239">第二個建構函式具有單一參數：`IMovieRepository`參數。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-239">The second constructor has a single parameter: an `IMovieRepository` parameter.</span></span> <span data-ttu-id="f3fd5-240">這個建構函式只會將參數的值指派給名為的類別層級欄位`_repository`。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-240">This constructor simply assigns the value of the parameter to a class-level field named `_repository`.</span></span>

<span data-ttu-id="f3fd5-241">`MoviesController`類別就利用一種軟體設計模式，稱為相依性插入模式。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-241">The `MoviesController` class is taking advantage of a software design pattern called the Dependency Injection pattern.</span></span> <span data-ttu-id="f3fd5-242">特別是，它使用所謂的建構函式相依性插入。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-242">In particular, it is using something called Constructor Dependency Injection.</span></span> <span data-ttu-id="f3fd5-243">您可以深入了解此模式，請閱讀下列文章 Martin fowler:</span><span class="sxs-lookup"><span data-stu-id="f3fd5-243">You can read more about this pattern by reading the following article by Martin Fowler:</span></span>

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

<span data-ttu-id="f3fd5-244">請注意，所有的指令碼`MoviesController`（除了第一個建構函式） 的類別互動`IMovieRepository`介面，而不是實際`MovieRepository`類別。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-244">Notice that all of the code in the `MoviesController` class (with the exception of the first constructor) interacts with the `IMovieRepository` interface instead of the actual `MovieRepository` class.</span></span> <span data-ttu-id="f3fd5-245">程式碼互動的抽象的介面，而不是介面的具象實作。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-245">The code interacts with an abstract interface instead of a concrete implementation of the interface.</span></span>

<span data-ttu-id="f3fd5-246">如果您想要修改應用程式所使用的資料存取技術，則您可以直接實作`IMovieRepository`使用替代的資料庫存取技術的類別與介面。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-246">If you want to modify the data access technology used by the application then you can simply implement the `IMovieRepository` interface with a class that uses the alternative database access technology.</span></span> <span data-ttu-id="f3fd5-247">例如，您可以建立`EntityFrameworkMovieRepository`類別或`SubSonicMovieRepository`類別。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-247">For example, you could create an `EntityFrameworkMovieRepository` class or a `SubSonicMovieRepository` class.</span></span> <span data-ttu-id="f3fd5-248">因為控制器類別撰寫的介面，您可以將傳遞的新實作`IMovieRepository`至控制器類別和類別會繼續運作。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-248">Because the controller class is programmed against the interface, you can pass a new implementation of `IMovieRepository` to the controller class and the class would continue to work.</span></span>

<span data-ttu-id="f3fd5-249">此外，如果您想要測試`MoviesController`類別，則您可以傳遞到假的電影儲存機制類別`HomeController`。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-249">Furthermore, if you want to test the `MoviesController` class, then you can pass a fake movie repository class to the `HomeController`.</span></span> <span data-ttu-id="f3fd5-250">您可以實作`IMovieRepository`類別的類別，並不會實際存取資料庫，但包含所有的必要方法`IMovieRepository`介面。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-250">You can implement the `IMovieRepository` class with a class that does not actually access the database but contains all of the required methods of the `IMovieRepository` interface.</span></span> <span data-ttu-id="f3fd5-251">如此一來，您可以單元測試`MoviesController`類別，而不實際存取實際的資料庫。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-251">That way, you can unit test the `MoviesController` class without actually accessing a real database.</span></span>

## <a name="summary"></a><span data-ttu-id="f3fd5-252">總結</span><span class="sxs-lookup"><span data-stu-id="f3fd5-252">Summary</span></span>

<span data-ttu-id="f3fd5-253">本教學課程的目標是要示範如何建立 MVC 模型類別，藉由利用 Microsoft LINQ to SQL。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-253">The goal of this tutorial was to demonstrate how you can create MVC model classes by taking advantage of Microsoft LINQ to SQL.</span></span> <span data-ttu-id="f3fd5-254">我們會檢查 ASP.NET MVC 應用程式中顯示資料庫資料的兩種策略。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-254">We examined two strategies for displaying database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="f3fd5-255">首先，我們會建立 LINQ to SQL 類別，並使用直接在控制器動作的類別。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-255">First, we created LINQ to SQL classes and used the classes directly within a controller action.</span></span> <span data-ttu-id="f3fd5-256">使用 LINQ to SQL 類別的控制器內，可讓您快速並輕鬆地顯示在 MVC 應用程式中的 資料庫資料。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-256">Using LINQ to SQL classes within a controller enables you to quickly and easily display database data in an MVC application.</span></span>

<span data-ttu-id="f3fd5-257">接下來，我們探討了稍微困難，但一定更良性，顯示資料庫資料路徑。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-257">Next, we explored a slightly more difficult, but definitely more virtuous, path for displaying database data.</span></span> <span data-ttu-id="f3fd5-258">我們花了儲存機制模式的優點和所有我們資料庫存取邏輯放在個別的存放庫類別。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-258">We took advantage of the Repository pattern and placed all of our database access logic in a separate repository class.</span></span> <span data-ttu-id="f3fd5-259">在我們的控制器中，我們會撰寫所有我們的程式碼，根據介面而不是具象類別。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-259">In our controller, we wrote all of our code against an interface instead of a concrete class.</span></span> <span data-ttu-id="f3fd5-260">儲存機制模式的優點是，它可讓我們將在未來輕鬆變更資料庫存取技術，而且它可讓我們輕鬆地測試我們的控制器類別。</span><span class="sxs-lookup"><span data-stu-id="f3fd5-260">The advantage of the Repository pattern is that it enables us to easily change database access technologies in the future and it enables us to easily test our controller classes.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f3fd5-261">[上一頁](creating-model-classes-with-the-entity-framework-cs.md)
> [下一頁](displaying-a-table-of-database-data-cs.md)</span><span class="sxs-lookup"><span data-stu-id="f3fd5-261">[Previous](creating-model-classes-with-the-entity-framework-cs.md)
[Next](displaying-a-table-of-database-data-cs.md)</span></span>
