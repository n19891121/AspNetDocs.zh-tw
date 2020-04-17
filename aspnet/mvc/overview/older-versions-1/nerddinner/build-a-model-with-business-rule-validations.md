---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 使用業務規則驗證建構模型 |微軟文件
author: rick-anderson
description: 步驟 3 演示如何創建模型,可用於查詢和更新 NerdDinner 應用程式的資料庫。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 1a316e9051cf56cd4f1546336b334ace991c05b3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541633"
---
# <a name="build-a-model-with-business-rule-validations"></a><span data-ttu-id="8cf2e-103">使用商務規則驗證建置模型</span><span class="sxs-lookup"><span data-stu-id="8cf2e-103">Build a Model with Business Rule Validations</span></span>

<span data-ttu-id="8cf2e-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8cf2e-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="8cf2e-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="8cf2e-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="8cf2e-106">這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第3步,該教程示範如何使用 ASP.NETmVC 1構建小型但完整的Web應用程式。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-106">This is step 3 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="8cf2e-107">步驟 3 演示如何創建模型,可用於查詢和更新 NerdDinner 應用程式的資料庫。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-107">Step 3 shows how to create a model that we can use to both query and update the database for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="8cf2e-108">如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-3-building-the-model"></a><span data-ttu-id="8cf2e-109">神經晚餐步驟 3: 構建模型</span><span class="sxs-lookup"><span data-stu-id="8cf2e-109">NerdDinner Step 3: Building the Model</span></span>

<span data-ttu-id="8cf2e-110">在模型檢視控制器框架中,術語"模型"是指表示應用程序數據的物件,以及與其集成驗證和業務規則的相應域邏輯。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-110">In a model-view-controller framework the term "model" refers to the objects that represent the data of the application, as well as the corresponding domain logic that integrates validation and business rules with it.</span></span> <span data-ttu-id="8cf2e-111">該模型在許多方面是基於 MVC 的應用程式的「心臟」,稍後我們將看到從根本上推動它的行為。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-111">The model is in many ways the "heart" of an MVC-based application, and as we'll see later fundamentally drives the behavior of it.</span></span>

<span data-ttu-id="8cf2e-112">ASP.NET MVC 框架支援使用任何資料存取技術,開發人員可以從各種豐富的 .NET 資料選項中進行選擇以實施其模型,包括:LINQ 到實體、LINQ 到 SQL、NHibernate、LLBLGen Pro、SubSonic、WilsonORM,或者只是原始ADO.NET數據閱讀器或數據集集。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-112">The ASP.NET MVC framework supports using any data access technology, and developers can choose from a variety of rich .NET data options to implement their models including: LINQ to Entities, LINQ to SQL, NHibernate, LLBLGen Pro, SubSonic, WilsonORM, or just raw ADO.NET DataReaders or DataSets.</span></span>

<span data-ttu-id="8cf2e-113">對於我們的NerdDinner應用程式,我們將使用LINQ到SQL來創建一個與資料庫設計相當一致的簡單模型,並添加一些自定義驗證邏輯和業務規則。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-113">For our NerdDinner application we are going to use LINQ to SQL to create a simple model that corresponds fairly closely to our database design, and adds some custom validation logic and business rules.</span></span> <span data-ttu-id="8cf2e-114">然後,我們將實現一個存儲庫類,該類可説明從應用程式的其餘部分提取數據持久性實現,並使我們能夠輕鬆地對其進行單元測試。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-114">We will then implement a repository class that helps abstract away the data persistence implementation from the rest of the application, and enables us to easily unit test it.</span></span>

### <a name="linq-to-sql"></a><span data-ttu-id="8cf2e-115">LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="8cf2e-115">LINQ to SQL</span></span>

<span data-ttu-id="8cf2e-116">LINQ 到 SQL 是作為 .NET 3.5 的一部分而附帶的 ORM(對象關係映射器)。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-116">LINQ to SQL is an ORM (object relational mapper) that ships as part of .NET 3.5.</span></span>

<span data-ttu-id="8cf2e-117">LINQ 到 SQL 提供了一種將資料庫表映射到 .NET 類的簡單方法,我們可以針對它編寫代碼。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-117">LINQ to SQL provides an easy way to map database tables to .NET classes we can code against.</span></span> <span data-ttu-id="8cf2e-118">對於我們的NerdDinner應用程式,我們將用它來將資料庫中的晚餐和RSVP表映射到晚餐和RSVP類。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-118">For our NerdDinner application we'll use it to map the Dinners and RSVP tables within our database to Dinner and RSVP classes.</span></span> <span data-ttu-id="8cf2e-119">晚餐和 RSVP 表的列將對應於「晚餐」和「RSVP」類的屬性。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-119">The columns of the Dinners and RSVP tables will correspond to properties on the Dinner and RSVP classes.</span></span> <span data-ttu-id="8cf2e-120">每個 Dinner 和 RSVP 物件將表示資料庫中的 Dinner 或 RSVP 表中的單獨行。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-120">Each Dinner and RSVP object will represent a separate row within the Dinners or RSVP tables in the database.</span></span>

<span data-ttu-id="8cf2e-121">LINQ 到 SQL 允許我們避免手動構造 SQL 語句來檢索和更新具有資料庫數據的 Dinner 和 RSVP 物件。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-121">LINQ to SQL allows us to avoid having to manually construct SQL statements to retrieve and update Dinner and RSVP objects with database data.</span></span> <span data-ttu-id="8cf2e-122">相反,我們將定義 Dinner 和 RSVP 類、它們如何映射到/從資料庫映射以及它們之間的關係。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-122">Instead, we'll define the Dinner and RSVP classes, how they map to/from the database, and the relationships between them.</span></span> <span data-ttu-id="8cf2e-123">然後,LINQ到 SQL 將負責生成適當的 SQL 執行邏輯,以便在運行時交互使用它們時使用。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-123">LINQ to SQL will then takes care of generating the appropriate SQL execution logic to use at runtime when we interact and use them.</span></span>

<span data-ttu-id="8cf2e-124">我們可以在VB和C#中使用LINQ語言支援來編寫表達性查詢,從資料庫中檢索Dinner和RSVP物件。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-124">We can use the LINQ language support within VB and C# to write expressive queries that retrieve Dinner and RSVP objects from the database.</span></span> <span data-ttu-id="8cf2e-125">這最大限度地減少了我們需要編寫的數據代碼量,並允許我們構建真正乾淨的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-125">This minimizes the amount of data code we need to write, and allows us to build really clean applications.</span></span>

### <a name="adding-linq-to-sql-classes-to-our-project"></a><span data-ttu-id="8cf2e-126">將 LINQ 新增到 SQL 類別到我們的項目</span><span class="sxs-lookup"><span data-stu-id="8cf2e-126">Adding LINQ to SQL Classes to our project</span></span>

<span data-ttu-id="8cf2e-127">我們將從右鍵單擊專案中的「模型」資料夾開始,然後選擇 **「新增&gt;新 專案**」選單命令:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-127">We'll begin by right-clicking on the "Models" folder within our project, and select the **Add-&gt;New Item** menu command:</span></span>

![](build-a-model-with-business-rule-validations/_static/image1.png)

<span data-ttu-id="8cf2e-128">這將彈出「添加新項目」對話框。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-128">This will bring up the "Add New Item" dialog.</span></span> <span data-ttu-id="8cf2e-129">我們將按「資料」類別進行篩選,並在其中選擇「LINQ 到 SQL 類」樣本:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-129">We'll filter by the "Data" category and select the "LINQ to SQL Classes" template within it:</span></span>

![](build-a-model-with-business-rule-validations/_static/image2.png)

<span data-ttu-id="8cf2e-130">我們將為專案命名為「NerdDinner」,然後單擊「添加」按鈕。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-130">We'll name the item "NerdDinner" and click the "Add" button.</span></span> <span data-ttu-id="8cf2e-131">Visual Studio 將在我們的 #Model 目錄下添加 NerdDinner.dbml 檔案,然後打開 LINQ 到 SQL 物件關係設計器:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-131">Visual Studio will add a NerdDinner.dbml file under our \Models directory, and then open the LINQ to SQL object relational designer:</span></span>

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a><span data-ttu-id="8cf2e-132">使用 LINQ 建立 SQL 的資料模型類別</span><span class="sxs-lookup"><span data-stu-id="8cf2e-132">Creating Data Model Classes with LINQ to SQL</span></span>

<span data-ttu-id="8cf2e-133">LINQ 到 SQL 使我們能夠從現有資料庫架構快速創建數據模型類。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-133">LINQ to SQL enables us to quickly create data model classes from existing database schema.</span></span> <span data-ttu-id="8cf2e-134">為此,我們將在伺服器資源管理器中打開NerdDinner資料庫,並選擇要在其中建模的表:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-134">To-do this we'll open the NerdDinner database in the Server Explorer, and select the Tables we want to model in it:</span></span>

![](build-a-model-with-business-rule-validations/_static/image4.png)

<span data-ttu-id="8cf2e-135">然後,我們可以將表拖到 LINQ 到 SQL 設計器表面。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-135">We can then drag the tables onto the LINQ to SQL designer surface.</span></span> <span data-ttu-id="8cf2e-136">當我們執行此操作 LINQ 到 SQL 時,將使用表格架構(具有映射到資料庫表列的類屬性)自動建立 Dinner 和 RSVP 類別:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-136">When we do this LINQ to SQL will automatically create Dinner and RSVP classes using the schema of the tables (with class properties that map to the database table columns):</span></span>

![](build-a-model-with-business-rule-validations/_static/image5.png)

<span data-ttu-id="8cf2e-137">默認情況下,LINQ到 SQL 設計器在基於資料庫架構創建類時自動「複數」表和列名稱。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-137">By default the LINQ to SQL designer automatically "pluralizes" table and column names when it creates classes based on a database schema.</span></span> <span data-ttu-id="8cf2e-138">例如:我們上面示例中的「Dinners」表產生了一個「Dinner」類。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-138">For example: the "Dinners" table in our example above resulted in a "Dinner" class.</span></span> <span data-ttu-id="8cf2e-139">此類命名有助於使我們的模型與 .NET 命名約定保持一致,我通常發現讓設計器修復這一點很方便(尤其是在添加大量表時)。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-139">This class naming helps make our models consistent with .NET naming conventions, and I usually find that having the designer fix this up convenient (especially when adding lots of tables).</span></span> <span data-ttu-id="8cf2e-140">但是,如果您不喜歡設計器生成的類或屬性的名稱,則始終可以重寫它並將其更改為所需的任何名稱。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-140">If you don't like the name of a class or property that the designer generates, though, you can always override it and change it to any name you want.</span></span> <span data-ttu-id="8cf2e-141">可以通過在設計器內編輯實體/屬性名稱,或通過屬性網格對其進行修改來執行此操作。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-141">You can do this either by editing the entity/property name in-line within the designer or by modifying it via the property grid.</span></span>

<span data-ttu-id="8cf2e-142">默認情況下,LINQ 到 SQL 設計器還會檢查表的主鍵/外鍵關係,並基於這些關係自動在它創建的不同模型類之間創建預設的「關係關聯」。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-142">By default the LINQ to SQL designer also inspects the primary key/foreign key relationships of the tables, and based on them automatically creates default "relationship associations" between the different model classes it creates.</span></span> <span data-ttu-id="8cf2e-143">例如,當我們將 Dinner 和 RSVP 表拖到 LINQ 到 SQL 設計器時,根據 RSVP 表對 Dinners 表具有外鍵(由設計器中的箭頭指示)推斷兩者之間存在一對多關係關聯:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-143">For example, when we dragged the Dinners and RSVP tables onto the LINQ to SQL designer a one-to-many relationship association between the two was inferred based on the fact that the RSVP table had a foreign-key to the Dinners table (this is indicated by the arrow in the designer):</span></span>

![](build-a-model-with-business-rule-validations/_static/image6.png)

<span data-ttu-id="8cf2e-144">上述關聯將導致 LINQ 到 SQL 向 RSVP 類添加強類型「Dinner」屬性,開發人員可以使用該屬性訪問與給定 RSVP 關聯的 Dinner。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-144">The above association will cause LINQ to SQL to add a strongly typed "Dinner" property to the RSVP class that developers can use to access the Dinner associated with a given RSVP.</span></span> <span data-ttu-id="8cf2e-145">它還會導致 Dinner 類具有" RSVP"集合屬性,使開發人員能夠檢索和更新與特定 Dinner 關聯的 RSVP 物件。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-145">It will also cause the Dinner class to have a "RSVPs" collection property that enables developers to retrieve and update RSVP objects associated with a particular Dinner.</span></span>

<span data-ttu-id="8cf2e-146">下面您可以看到 Visual Studio 中一個智慧感知示例,當我們創建新的 RSVP 物件並將其添加到 Dinner 的 RSVP 集合中時。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-146">Below you can see an example of intellisense within Visual Studio when we create a new RSVP object and add it to a Dinner's RSVPs collection.</span></span> <span data-ttu-id="8cf2e-147">請注意 LINQ 到 SQL 如何在 Dinner 物件上自動新增「RSV」集合:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-147">Notice how LINQ to SQL automatically added a "RSVPs" collection on the Dinner object:</span></span>

![](build-a-model-with-business-rule-validations/_static/image7.png)

<span data-ttu-id="8cf2e-148">通過將 RSVP 物件添加到 Dinner 的 RSVP 集合中,我們告訴 LINQ 到 SQL 來關聯資料庫中的 Dinner 和 RSVP 行之間的外鍵關係:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-148">By adding the RSVP object to the Dinner's RSVPs collection we are telling LINQ to SQL to associate a foreign-key relationship between the Dinner and the RSVP row in our database:</span></span>

![](build-a-model-with-business-rule-validations/_static/image8.png)

<span data-ttu-id="8cf2e-149">如果您不喜歡設計器建模或命名表關聯的方式,則可以重寫它。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-149">If you don't like how the designer has modeled or named a table association, you can override it.</span></span> <span data-ttu-id="8cf2e-150">只需單擊設計器中的關聯箭頭,並通過屬性網格訪問其屬性以重命名、刪除或修改它。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-150">Just click on the association arrow within the designer and access its properties via the property grid to rename, delete or modify it.</span></span> <span data-ttu-id="8cf2e-151">但是,對於我們的NerdDinner應用程式,默認關聯規則非常適合我們構建的數據模型類,我們可以只使用默認行為。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-151">For our NerdDinner application, though, the default association rules work well for the data model classes we are building and we can just use the default behavior.</span></span>

### <a name="nerddinnerdatacontext-class"></a><span data-ttu-id="8cf2e-152">內德晚餐資料上下文類</span><span class="sxs-lookup"><span data-stu-id="8cf2e-152">NerdDinnerDataContext Class</span></span>

<span data-ttu-id="8cf2e-153">Visual Studio 將自動建立 .NET 類,這些類表示使用 LINQ 到 SQL 設計器定義的模型和資料庫關係。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-153">Visual Studio will automatically create .NET classes that represent the models and database relationships defined using the LINQ to SQL designer.</span></span> <span data-ttu-id="8cf2e-154">還將為添加到解決方案的每個 LINQ 到 SQL 設計器檔生成 LINQ 到 SQL DataContext 類。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-154">A LINQ to SQL DataContext class is also generated for each LINQ to SQL designer file added to the solution.</span></span> <span data-ttu-id="8cf2e-155">由於我們將 LINQ 命名為 SQL 類項「NerdDinner」,因此創建的數據上下文類將稱為「NerdDinnerDataContext」。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-155">Because we named our LINQ to SQL class item "NerdDinner", the DataContext class created will be called "NerdDinnerDataContext".</span></span> <span data-ttu-id="8cf2e-156">此NerdDinnerDataContext類是我們與資料庫互動的主要方式。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-156">This NerdDinnerDataContext class is the primary way we will interact with the database.</span></span>

<span data-ttu-id="8cf2e-157">我們的NerdDinnerDataContext類公開了兩個屬性 - 'Dinners" 和"RSVPs" - 它們表示我們在資料庫中建模的兩個表。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-157">Our NerdDinnerDataContext class exposes two properties - "Dinners" and "RSVPs" - that represent the two tables we modeled within the database.</span></span> <span data-ttu-id="8cf2e-158">我們可以使用 C# 針對這些屬性編寫 LINQ 查詢,以便從資料庫中查詢和檢索 Dinner 和 RSVP 物件。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-158">We can use C# to write LINQ queries against those properties to query and retrieve Dinner and RSVP objects from the database.</span></span>

<span data-ttu-id="8cf2e-159">以下代碼演示如何實例化NerdDinnerDataContext物件,並針對該物件執行LINQ查詢,以獲取將來發生的一系列Dinner。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-159">The following code demonstrates how to instantiate a NerdDinnerDataContext object and perform a LINQ query against it to obtain a sequence of Dinners that occur in the future.</span></span> <span data-ttu-id="8cf2e-160">Visual Studio 在編寫 LINQ 查詢時提供完整的無意義,從它返回的對像是強類型,並且還支援智慧感知:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-160">Visual Studio provides full intellisense when writing the LINQ query, and the objects returned from it are strongly-typed and also support intellisense:</span></span>

![](build-a-model-with-business-rule-validations/_static/image9.png)

<span data-ttu-id="8cf2e-161">除了允許我們查詢晚餐和RSVP物件外,NerdDinnerDataContext 還會自動跟蹤我們隨後對我們通過它檢索的晚餐和 RSVP 物件所做的任何更改。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-161">In addition to allowing us to query for Dinner and RSVP objects, a NerdDinnerDataContext also automatically tracks any changes we subsequently make to the Dinner and RSVP objects we retrieve through it.</span></span> <span data-ttu-id="8cf2e-162">我們可以使用此功能輕鬆地將更改保存回資料庫 - 而無需編寫任何顯式 SQL 更新代碼。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-162">We can use this functionality to easily save the changes back to the database - without having to write any explicit SQL update code.</span></span>

<span data-ttu-id="8cf2e-163">例如,下面的程式碼展示如何使用 LINQ 查詢從資料庫中檢索單個 Dinner 物件,更新兩個 Dinner 屬性,然後將更改儲存回資料庫:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-163">For example, the code below demonstrates how to use a LINQ query to retrieve a single Dinner object from the database, update two of the Dinner properties, and then save the changes back to the database:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

<span data-ttu-id="8cf2e-164">上面代碼中的NerdDinnerDataContext物件自動追蹤我們對從該物件檢索到的Dinner物件所做的屬性更改。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-164">The NerdDinnerDataContext object in the code above automatically tracked the property changes made to the Dinner object we retrieved from it.</span></span> <span data-ttu-id="8cf2e-165">當我們調用"提交更改()"方法時,它將對資料庫執行適當的 SQL"UPDATE"語句,以保留更新的值。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-165">When we called the "SubmitChanges()" method, it will execute an appropriate SQL "UPDATE" statement to the database to persist the updated values back.</span></span>

### <a name="creating-a-dinnerrepository-class"></a><span data-ttu-id="8cf2e-166">建立晚餐儲存庫類別</span><span class="sxs-lookup"><span data-stu-id="8cf2e-166">Creating a DinnerRepository Class</span></span>

<span data-ttu-id="8cf2e-167">對於小型應用程式,有時讓控制器直接針對 LINQ 到 SQL DataContext 類工作,並將 LINQ 查詢嵌入到控制器中,這有時很好。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-167">For small applications it is sometimes fine to have Controllers work directly against a LINQ to SQL DataContext class, and embed LINQ queries within the Controllers.</span></span> <span data-ttu-id="8cf2e-168">但是,隨著應用程式變得越來越大,此方法在維護和測試方面變得繁瑣起來。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-168">As applications get larger, though, this approach becomes cumbersome to maintain and test.</span></span> <span data-ttu-id="8cf2e-169">它還可能導致我們在多個位置複製相同的 LINQ 查詢。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-169">It can also lead to us duplicating the same LINQ queries in multiple places.</span></span>

<span data-ttu-id="8cf2e-170">使應用程式更易於維護和測試的一種方法是使用"存儲庫"模式。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-170">One approach that can make applications easier to maintain and test is to use a "repository" pattern.</span></span> <span data-ttu-id="8cf2e-171">存儲庫類有助於封裝數據查詢和持久性邏輯,並從應用程式抽象數據持久性的實現詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-171">A repository class helps encapsulate data querying and persistence logic, and abstracts away the implementation details of the data persistence from the application.</span></span> <span data-ttu-id="8cf2e-172">除了使應用程式代碼更簡潔之外,使用存儲庫模式還可以使將來更輕鬆地更改數據存儲實現,並且它可以説明簡化應用程式單元測試,而無需真正的資料庫。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-172">In addition to making application code cleaner, using a repository pattern can make it easier to change data storage implementations in the future, and it can help facilitate unit testing an application without requiring a real database.</span></span>

<span data-ttu-id="8cf2e-173">對於我們的NerdDinner應用程式,我們將定義一個帶有以下簽名的 DinnerRepository 類:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-173">For our NerdDinner application we'll define a DinnerRepository class with the below signature:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

<span data-ttu-id="8cf2e-174">*注意:在本章的後面部分,我們將從此類中提取 IDinnerRepository 介面,並在我們的控制器上啟用依賴項注入。不過,首先,我們將開始簡單,只是直接與 DinnerRepository 類一起工作。*</span><span class="sxs-lookup"><span data-stu-id="8cf2e-174">*Note: Later in this chapter we'll extract an IDinnerRepository interface from this class and enable dependency injection with it on our Controllers. To begin with, though, we are going to start simple and just work directly with the DinnerRepository class.*</span></span>

<span data-ttu-id="8cf2e-175">要實現此類,我們將右鍵單擊我們的"模型"資料夾,然後選擇 **「添加&gt;新專案**」功能表命令。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-175">To implement this class we'll right-click on our "Models" folder and choose the **Add-&gt;New Item** menu command.</span></span> <span data-ttu-id="8cf2e-176">在「添加新項目」對話框中,我們將選擇「類」樣本並將檔案命名為「DinnerRepository.cs」:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-176">Within the "Add New Item" dialog we'll select the "Class" template and name the file "DinnerRepository.cs":</span></span>

![](build-a-model-with-business-rule-validations/_static/image10.png)

<span data-ttu-id="8cf2e-177">然後,我們可以使用以下代碼實現我們的 DinnerRepository 類:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-177">We can then implement our DinnerRepository class using the code below:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a><span data-ttu-id="8cf2e-178">使用 DinnerRepository 類別索、更新、插入和刪除</span><span class="sxs-lookup"><span data-stu-id="8cf2e-178">Retrieving, Updating, Inserting and Deleting using the DinnerRepository class</span></span>

<span data-ttu-id="8cf2e-179">現在,我們已經創建了 DinnerRepository 類,讓我們看一些代碼示例,這些示例演示了我們可以執行的常見任務:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-179">Now that we've created our DinnerRepository class, let's look at a few code examples that demonstrate common tasks we can do with it:</span></span>

#### <a name="querying-examples"></a><span data-ttu-id="8cf2e-180">查詢範例</span><span class="sxs-lookup"><span data-stu-id="8cf2e-180">Querying Examples</span></span>

<span data-ttu-id="8cf2e-181">以下代碼使用 DinnerID 值檢索單個晚餐:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-181">The code below retrieves a single Dinner using the DinnerID value:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

<span data-ttu-id="8cf2e-182">下面的代碼檢索所有即將舉辦的晚餐,並在它們上迴圈:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-182">The code below retrieves all upcoming dinners and loops over them:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a><span data-ttu-id="8cf2e-183">插入並更新範例</span><span class="sxs-lookup"><span data-stu-id="8cf2e-183">Insert and Update Examples</span></span>

<span data-ttu-id="8cf2e-184">下面的代碼演示了添加兩個新晚餐。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-184">The code below demonstrates adding two new dinners.</span></span> <span data-ttu-id="8cf2e-185">在調用"Save()"方法之前,不會將存儲庫的添加/修改提交到資料庫。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-185">Additions/modifications to the repository aren't committed to the database until the "Save()" method is called on it.</span></span> <span data-ttu-id="8cf2e-186">LINQ 到 SQL 會自動包裝資料庫事務中的所有變更 , 因此,當我們的儲存庫保存時,要麼發生所有更改,要麼這些更改都不會發生:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-186">LINQ to SQL automatically wraps all changes in a database transaction – so either all changes happen or none of them do when our repository saves:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

<span data-ttu-id="8cf2e-187">下面的代碼檢索現有的 Dinner 物件,並修改其上的兩個屬性。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-187">The code below retrieves an existing Dinner object, and modifies two properties on it.</span></span> <span data-ttu-id="8cf2e-188">當我們的儲存庫上調用「Save())」方法時,更改將提交回資料庫:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-188">The changes are committed back to the database when the "Save()" method is called on our repository:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

<span data-ttu-id="8cf2e-189">下面的代碼檢索晚餐,然後向其中添加 RSVP。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-189">The code below retrieves a dinner and then adds an RSVP to it.</span></span> <span data-ttu-id="8cf2e-190">它使用 LINQ 到 SQL 為我們創建的 Dinner 物件上的 RSVP 集合來這樣做(因為資料庫中兩者之間存在主鍵/外鍵關係)。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-190">It does this using the RSVPs collection on the Dinner object that LINQ to SQL created for us (because there is a primary-key/foreign-key relationship between the two in the database).</span></span> <span data-ttu-id="8cf2e-191">當在儲存庫上調用「Save())」方法時,此更改將作為新的 RSVP 表行保留回資料庫:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-191">This change is persisted back to the database as a new RSVP table row when the "Save()" method is called on the repository:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a><span data-ttu-id="8cf2e-192">刪除範例</span><span class="sxs-lookup"><span data-stu-id="8cf2e-192">Delete Example</span></span>

<span data-ttu-id="8cf2e-193">下面的代碼檢索現有的 Dinner 物件,然後將其標記為要刪除。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-193">The code below retrieves an existing Dinner object, and then marks it to be deleted.</span></span> <span data-ttu-id="8cf2e-194">在儲存函式庫上調用「Save())」方法時,它將將刪除提交回資料庫:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-194">When the "Save()" method is called on the repository it will commit the delete back to the database:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a><span data-ttu-id="8cf2e-195">將驗證和業務規則邏輯與模型類別</span><span class="sxs-lookup"><span data-stu-id="8cf2e-195">Integrating Validation and Business Rule Logic with Model Classes</span></span>

<span data-ttu-id="8cf2e-196">集成驗證和業務規則邏輯是任何處理數據的應用程序的關鍵部分。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-196">Integrating validation and business rule logic is a key part of any application that works with data.</span></span>

#### <a name="schema-validation"></a><span data-ttu-id="8cf2e-197">結構描述驗證</span><span class="sxs-lookup"><span data-stu-id="8cf2e-197">Schema Validation</span></span>

<span data-ttu-id="8cf2e-198">使用 LINQ 到 SQL 設計器定義模型類時,數據模型類中屬性的數據類型對應於資料庫表的數據類型。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-198">When model classes are defined using the LINQ to SQL designer, the datatypes of the properties in the data model classes correspond to the datatypes of the database table.</span></span> <span data-ttu-id="8cf2e-199">例如:如果 Dinners 表中的「EventDate」列是「日期時間」,則 LINQ 創建的 SQL 資料模型類的類型為「DateTime」(這是內置的 .NET 數據類型)。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-199">For example: if the "EventDate" column in the Dinners table is a "datetime", the data model class created by LINQ to SQL will be of type "DateTime" (which is a built-in .NET datatype).</span></span> <span data-ttu-id="8cf2e-200">這意味著,如果您嘗試從代碼為其分配整數或布爾,則收到編譯錯誤,如果嘗試在運行時隱式將無效字串類型轉換為該字串類型,則會自動引發錯誤。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-200">This means you will get compile errors if you attempt to assign an integer or boolean to it from code, and it will raise an error automatically if you attempt to implicitly convert a non-valid string type to it at runtime.</span></span>

<span data-ttu-id="8cf2e-201">LINQ 到 SQL 還會在使用字串時自動處理轉義 SQL 值,這有助於在使用字串時防止 SQL 注入攻擊。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-201">LINQ to SQL will also automatically handles escaping SQL values for you when using strings - which helps protect you against SQL injection attacks when using it.</span></span>

#### <a name="validation-and-business-rule-logic"></a><span data-ttu-id="8cf2e-202">驗證與業務規則邏輯</span><span class="sxs-lookup"><span data-stu-id="8cf2e-202">Validation and Business Rule Logic</span></span>

<span data-ttu-id="8cf2e-203">架構驗證作為第一步非常有用,但很少足夠。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-203">Schema validation is useful as a first step, but is rarely sufficient.</span></span> <span data-ttu-id="8cf2e-204">大多數實際方案都需要能夠指定更豐富的驗證邏輯,該驗證邏輯可以跨越多個屬性,執行代碼,並且通常瞭解模型的狀態(例如:它是在創建/更新/刪除,還是處於特定於域的狀態(如"存檔")。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-204">Most real-world scenarios require the ability to specify richer validation logic that can span multiple properties, execute code, and often have awareness of a model's state (for example: is it being created /updated/deleted, or within a domain-specific state like "archived").</span></span> <span data-ttu-id="8cf2e-205">有多種不同的模式和框架可用於定義驗證規則並將其應用於模型類,並且有幾個基於 .NET 的框架可用於幫助實現此。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-205">There are a variety of different patterns and frameworks that can be used to define and apply validation rules to model classes, and there are several .NET based frameworks out there that can be used to help with this.</span></span> <span data-ttu-id="8cf2e-206">您可以在mVC應用程式中使用幾乎任何ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-206">You can use pretty much any of them within ASP.NET MVC applications.</span></span>

<span data-ttu-id="8cf2e-207">為了我們的NerdDinner應用程式,我們將使用相對簡單和直接的模式,在其中我們公開IsValid屬性和GetRule侵犯() 方法在我們的Dinner模型物件上。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-207">For the purposes of our NerdDinner application, we'll use a relatively simple and straight-forward pattern where we expose an IsValid property and a GetRuleViolations() method on our Dinner model object.</span></span> <span data-ttu-id="8cf2e-208">IsValid 屬性將返回真或假,具體取決於驗證和業務規則是否都有效。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-208">The IsValid property will return true or false depending on whether the validation and business rules are all valid.</span></span> <span data-ttu-id="8cf2e-209">GetRule違反() 方法將返回任何規則錯誤的清單。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-209">The GetRuleViolations() method will return a list of any rule errors.</span></span>

<span data-ttu-id="8cf2e-210">我們將通過在我們的專案中添加「部分類」來實現「有效」和 GetRule 違反()) 我們的晚餐模型。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-210">We'll implement IsValid and GetRuleViolations() for our Dinner model by adding a "partial class" to our project.</span></span> <span data-ttu-id="8cf2e-211">部分類可用於向 VS 設計器維護的類(如 LINQ 生成的到 SQL 設計器生成的 Dinner 類)添加方法/ 屬性/ 事件,並説明避免工具混亂我們的代碼。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-211">Partial classes can be used to add methods/properties/events to classes maintained by a VS designer (like the Dinner class generated by the LINQ to SQL designer) and help avoid the tool from messing with our code.</span></span> <span data-ttu-id="8cf2e-212">我們可以通過右鍵單擊 #Model 資料夾,將新的部分類添加到專案中,然後選擇"添加新專案"功能表命令。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-212">We can add a new partial class to our project by right-clicking on the \Models folder, and then select the "Add New Item" menu command.</span></span> <span data-ttu-id="8cf2e-213">然後,我們可以在"添加新項目"對話框中選擇"類"範本,並將其命名為Dinner.cs。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-213">We can then choose the "Class" template within the "Add New Item" dialog and name it Dinner.cs.</span></span>

![](build-a-model-with-business-rule-validations/_static/image11.png)

<span data-ttu-id="8cf2e-214">按下「添加」按鈕會將Dinner.cs檔添加到我們的專案中,並在IDE中打開該檔。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-214">Clicking the "Add" button will add a Dinner.cs file to our project and open it within the IDE.</span></span> <span data-ttu-id="8cf2e-215">然後,我們可以使用以下代碼實現基本的規則/驗證實施框架:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-215">We can then implement a basic rule/validation enforcement framework using the below code:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

<span data-ttu-id="8cf2e-216">有關上述代碼的一些說明:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-216">A few notes about the above code:</span></span>

- <span data-ttu-id="8cf2e-217">Dinner 類以"部分"關鍵字為開頭 - 這意味著其中包含的代碼將與 LINQ 生成/維護的類組合到 SQL 設計器並編譯為單個類。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-217">The Dinner class is prefaced with a "partial" keyword – which means the code contained within it will be combined with the class generated/maintained by the LINQ to SQL designer and compiled into a single class.</span></span>
- <span data-ttu-id="8cf2e-218">RuleRuleRule 類是一個説明類,我們將添加到專案中,允許我們提供有關規則違反的更多詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-218">The RuleViolation class is a helper class we'll add to the project that allows us to provide more details about a rule violation.</span></span>
- <span data-ttu-id="8cf2e-219">晚餐.GetRule違反()方法會導致評估我們的驗證和業務規則(我們將很快實施它們)。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-219">The Dinner.GetRuleViolations() method causes our validation and business rules to be evaluated (we'll implement them shortly).</span></span> <span data-ttu-id="8cf2e-220">然後,它返回一系列規則衝突物件,這些物件提供有關任何規則錯誤的更多詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-220">It then returns back a sequence of RuleViolation objects that provide more details about any rule errors.</span></span>
- <span data-ttu-id="8cf2e-221">Dinner.IsValid 屬性提供了一個方便的幫助程式屬性,用於指示 Dinner 物件是否具有任何活動的規則衝突。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-221">The Dinner.IsValid property provides a convenient helper property that indicates whether the Dinner object has any active RuleViolations.</span></span> <span data-ttu-id="8cf2e-222">開發人員可以隨時使用 Dinner 物件主動檢查它(並且不會引發異常)。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-222">It can be proactively checked by a developer using the Dinner object at anytime (and does not raise an exception).</span></span>
- <span data-ttu-id="8cf2e-223">Dinner.OnValidate() 部分方法是 LINQ 到 SQL 提供的一個掛鉤,它允許我們在即將在資料庫中持久化 Dinner 物件的任何時間收到通知。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-223">The Dinner.OnValidate() partial method is a hook that LINQ to SQL provides that allows us to be notified anytime the Dinner object is about to be persisted within the database.</span></span> <span data-ttu-id="8cf2e-224">上述 OnValidate() 實現可確保在保存之前沒有規則違反規則。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-224">Our OnValidate() implementation above ensures that the Dinner has no RuleViolations before it is saved.</span></span> <span data-ttu-id="8cf2e-225">如果處於無效狀態,它將引發異常,這將導致 LINQ 到 SQL 中止事務。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-225">If it is in an invalid state it raises an exception, which will cause LINQ to SQL to abort the transaction.</span></span>

<span data-ttu-id="8cf2e-226">此方法提供了一個簡單的框架,我們可以將驗證和業務規則集成到其中。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-226">This approach provides a simple framework that we can integrate validation and business rules into.</span></span> <span data-ttu-id="8cf2e-227">現在,讓我們將以下規則添加到我們的 GetRule 違反() 方法:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-227">For now let's add the below rules to our GetRuleViolations() method:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

<span data-ttu-id="8cf2e-228">我們使用 C# 的「收益回報」功能來返回任何規則違反規則的序列。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-228">We are using the "yield return" feature of C# to return a sequence of any RuleViolations.</span></span> <span data-ttu-id="8cf2e-229">上面的前六個規則檢查只是強制說,我們 Dinner 上的字串屬性不能為空或為空。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-229">The first six rule checks above simply enforce that string properties on our Dinner cannot be null or empty.</span></span> <span data-ttu-id="8cf2e-230">最後一條規則更有趣一點,並調用 PhoneValidator.IsValidNumber() 説明器方法,我們可以添加到我們的專案中,以驗證 ContactPhone 號碼格式是否與 Dinner 的國家/ 地區匹配。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-230">The last rule is a little more interesting, and calls a PhoneValidator.IsValidNumber() helper method that we can add to our project to verify that the ContactPhone number format matches the Dinner's country.</span></span>

<span data-ttu-id="8cf2e-231">我們可以使用 。NET 的正則表達式支持實現此電話驗證支援。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-231">We can use .NET's regular expression support to implement this phone validation support.</span></span> <span data-ttu-id="8cf2e-232">下面是一個簡單的電話驗證器實現,我們可以添加到我們的專案,使我們能夠添加特定於國家/地區的 Regex 模式檢查:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-232">Below is a simple PhoneValidator implementation that we can add to our project that enables us to add country-specific Regex pattern checks:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a><span data-ttu-id="8cf2e-233">處理驗證與業務邏輯衝突</span><span class="sxs-lookup"><span data-stu-id="8cf2e-233">Handling Validation and Business Logic Violations</span></span>

<span data-ttu-id="8cf2e-234">現在,我們已經添加了上述驗證和業務規則代碼,每當我們嘗試創建或更新 Dinner 時,都將評估和強制執行驗證邏輯規則。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-234">Now that we've added the above validation and business rule code, any time we try to create or update a Dinner, our validation logic rules will be evaluated and enforced.</span></span>

<span data-ttu-id="8cf2e-235">開發人員可以編寫如下代碼,以主動確定 Dinner 物件是否有效,並檢索其中所有衝突的清單,而不會引發任何異常:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-235">Developers can write code like below to proactively determine if a Dinner object is valid, and retrieve a list of all violations in it without raising any exceptions:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

<span data-ttu-id="8cf2e-236">如果我們嘗試將 Dinner 保存為無效狀態,則當我們在 Dinner 儲存庫上調用 Save() 方法時,將引發異常。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-236">If we attempt to save a Dinner in an invalid state, an exception will be raised when we call the Save() method on the DinnerRepository.</span></span> <span data-ttu-id="8cf2e-237">這是因為 LINQ 到 SQL 在保存晚餐更改之前自動調用我們的 Dinner.OnValidate() 部分方法,並且我們在晚餐中添加了代碼。OnValidate() 如果晚餐中存在任何違反規則的行為,則引發異常。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-237">This occurs because LINQ to SQL automatically calls our Dinner.OnValidate() partial method before it saves the Dinner's changes, and we added code to Dinner.OnValidate() to raise an exception if any rule violations exist in the Dinner.</span></span> <span data-ttu-id="8cf2e-238">我們可以捕獲此異常並被動檢索要修復的違規清單:</span><span class="sxs-lookup"><span data-stu-id="8cf2e-238">We can catch this exception and reactively retrieve a list of the violations to fix:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

<span data-ttu-id="8cf2e-239">由於驗證和業務規則在我們的模型層中實現,而不是 UI 層內,因此它們將在應用程式中的所有方案中應用和使用。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-239">Because our validation and business rules are implemented within our model layer, and not within the UI layer, they will be applied and used across all scenarios within our application.</span></span> <span data-ttu-id="8cf2e-240">我們以後可以更改或添加業務規則,並讓所有與我們的 Dinner 物件一起使用的代碼都遵守它們。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-240">We can later change or add business rules and have all code that works with our Dinner objects honor them.</span></span>

<span data-ttu-id="8cf2e-241">在一個位置靈活地更改業務規則,而不使這些更改波及整個應用程式和 UI 邏輯,是編寫良好的應用程式的標誌,也是 MVC 框架有助於鼓勵的好處。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-241">Having the flexibility to change business rules in one place, without having these changes ripple throughout the application and UI logic, is a sign of a well-written application, and a benefit that an MVC framework helps encourage.</span></span>

### <a name="next-step"></a><span data-ttu-id="8cf2e-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8cf2e-242">Next Step</span></span>

<span data-ttu-id="8cf2e-243">現在,我們有一個模型,我們可以用於查詢和更新我們的資料庫。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-243">We've now got a model that we can use to both query and update our database.</span></span>

<span data-ttu-id="8cf2e-244">現在,讓我們向專案添加一些控制器和視圖,可用於構建圍繞它的 HTML UI 體驗。</span><span class="sxs-lookup"><span data-stu-id="8cf2e-244">Let's now add some controllers and views to the project that we can use to build an HTML UI experience around it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8cf2e-245">[前一個](create-a-database.md)
> [下一個](use-controllers-and-views-to-implement-a-listingdetails-ui.md)</span><span class="sxs-lookup"><span data-stu-id="8cf2e-245">[Previous](create-a-database.md)
[Next](use-controllers-and-views-to-implement-a-listingdetails-ui.md)</span></span>
