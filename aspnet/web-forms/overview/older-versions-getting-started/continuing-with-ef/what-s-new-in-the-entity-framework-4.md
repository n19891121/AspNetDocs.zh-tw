---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
title: 什麼是 Entity Framework 4.0 的新功能 |Microsoft Docs
author: tdykstra
description: 本教學課程系列由開始使用 Entity Framework 4.0 的教學課程系列的 Contoso 大學 web 應用程式為基礎。 我...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 393df4a8-b1db-44c4-9db7-2b533ca887d0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
msc.type: authoredcontent
ms.openlocfilehash: 0bc24a59e09728a5ecb6e18378c4cde0c8e046f2
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59387447"
---
# <a name="whats-new-in-the-entity-framework-40"></a><span data-ttu-id="28d04-104">Entity Framework 4.0 的新功能</span><span class="sxs-lookup"><span data-stu-id="28d04-104">What's New in the Entity Framework 4.0</span></span>

<span data-ttu-id="28d04-105">藉由[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="28d04-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="28d04-106">本教學課程系列是根據所建立的 Contoso 大學 web 應用程式[Getting Started with Entity Framework](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)教學課程系列。</span><span class="sxs-lookup"><span data-stu-id="28d04-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) tutorial series.</span></span> <span data-ttu-id="28d04-107">如果您未完成先前的教學課程，為本教學課程的起始點即可[下載應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)您會建立。</span><span class="sxs-lookup"><span data-stu-id="28d04-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="28d04-108">您也可以[下載應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)，它由完整的教學課程系列。</span><span class="sxs-lookup"><span data-stu-id="28d04-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="28d04-109">如果您有疑問的教學課程，您可以張貼他們[ASP.NET Entity Framework 論壇](https://forums.asp.net/1227.aspx)。</span><span class="sxs-lookup"><span data-stu-id="28d04-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>


<span data-ttu-id="28d04-110">在上一個教學課程，您會看到一些方法來將使用 Entity Framework 的 web 應用程式的效能最大化。</span><span class="sxs-lookup"><span data-stu-id="28d04-110">In the previous tutorial you saw some methods for maximizing the performance of a web application that uses the Entity Framework.</span></span> <span data-ttu-id="28d04-111">本教學課程中檢閱的一些最重要的新功能的 Entity Framework 版本 4 中，它會連結到資源提供所有新功能的更完整介紹。</span><span class="sxs-lookup"><span data-stu-id="28d04-111">This tutorial reviews some of the most important new features in version 4 of the Entity Framework, and it links to resources that provide a more complete introduction to all of the new features.</span></span> <span data-ttu-id="28d04-112">在本教學課程中反白顯示的功能包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="28d04-112">The features highlighted in this tutorial include the following:</span></span>

- <span data-ttu-id="28d04-113">外部索引鍵的關聯。</span><span class="sxs-lookup"><span data-stu-id="28d04-113">Foreign-key associations.</span></span>
- <span data-ttu-id="28d04-114">執行使用者定義的 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="28d04-114">Executing user-defined SQL commands.</span></span>
- <span data-ttu-id="28d04-115">模型優先開發。</span><span class="sxs-lookup"><span data-stu-id="28d04-115">Model-first development.</span></span>
- <span data-ttu-id="28d04-116">POCO 支援。</span><span class="sxs-lookup"><span data-stu-id="28d04-116">POCO support.</span></span>

<span data-ttu-id="28d04-117">此外，本教學課程將簡短介紹*code first 開發*，即將在下一個版本的 Entity Framework 的功能。</span><span class="sxs-lookup"><span data-stu-id="28d04-117">In addition, the tutorial will briefly introduce *code-first development*, a feature that's coming in the next release of the Entity Framework.</span></span>

<span data-ttu-id="28d04-118">若要開始本教學課程，請啟動 Visual Studio，並開啟您已在上一個教學課程中使用的 Contoso 大學 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="28d04-118">To start the tutorial, start Visual Studio and open the Contoso University web application that you were working with in the previous tutorial.</span></span>

## <a name="foreign-key-associations"></a><span data-ttu-id="28d04-119">外部索引鍵的關聯</span><span class="sxs-lookup"><span data-stu-id="28d04-119">Foreign-Key Associations</span></span>

<span data-ttu-id="28d04-120">Entity Framework 3.5 版包含導覽屬性，但其未包含資料模型中的外部索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="28d04-120">Version 3.5 of the Entity Framework included navigation properties, but it didn't include foreign-key properties in the data model.</span></span> <span data-ttu-id="28d04-121">例如，`CourseID`並`StudentID`的資料行`StudentGrade`資料表也會一併省略從`StudentGrade`實體。</span><span class="sxs-lookup"><span data-stu-id="28d04-121">For example, the `CourseID` and `StudentID` columns of the `StudentGrade` table would be omitted from the `StudentGrade` entity.</span></span>

[![I<span data-ttu-id="28d04-122">mage01]</span><span class="sxs-lookup"><span data-stu-id="28d04-122">mage01]</span></span>(what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)

<span data-ttu-id="28d04-123">這種方法的原因是，嚴格來說，外部索引鍵是實體的實作詳細資料，並不屬於概念資料模型中。</span><span class="sxs-lookup"><span data-stu-id="28d04-123">The reason for this approach was that, strictly speaking, foreign keys are a physical implementation detail and don't belong in a conceptual data model.</span></span> <span data-ttu-id="28d04-124">不過，實際上，通常很容易使用的程式碼中的實體，當您直接存取的外部索引鍵。</span><span class="sxs-lookup"><span data-stu-id="28d04-124">However, as a practical matter, it's often easier to work with entities in code when you have direct access to the foreign keys.</span></span>

<span data-ttu-id="28d04-125">如需資料模型中如何外部索引鍵的範例可以簡化程式碼，請考慮如何您原本的程式碼*DepartmentsAdd.aspx*未加上的頁面。</span><span class="sxs-lookup"><span data-stu-id="28d04-125">For an example of how foreign keys in the data model can simplify your code, consider how you would have had to code the *DepartmentsAdd.aspx* page without them.</span></span> <span data-ttu-id="28d04-126">在 `Department`實體`Administrator`屬性會對應至外部索引鍵`PersonID`中`Person`實體。</span><span class="sxs-lookup"><span data-stu-id="28d04-126">In the `Department` entity, the `Administrator` property is a foreign key that corresponds to `PersonID` in the `Person` entity.</span></span> <span data-ttu-id="28d04-127">若要建立新的部門和其系統管理員之間的關聯，您只需要設定的值`Administrator`屬性中的`ItemInserting`的資料繫結控制項的事件處理常式：</span><span class="sxs-lookup"><span data-stu-id="28d04-127">In order to establish the association between a new department and its administrator, all you had to do was set the value for the `Administrator` property in the `ItemInserting` event handler of the databound control:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample1.cs)]

<span data-ttu-id="28d04-128">沒有資料模型中的外部索引鍵，您會處理`Inserting`事件的資料來源控制項，而不是`ItemInserting`事件的資料繫結控制項，以取得實體本身的參考，才能將該實體加入至實體集。</span><span class="sxs-lookup"><span data-stu-id="28d04-128">Without foreign keys in the data model, you'd handle the `Inserting` event of the data source control instead of the `ItemInserting` event of the databound control, in order to get a reference to the entity itself before the entity is added to the entity set.</span></span> <span data-ttu-id="28d04-129">當您擁有該參考時，您會建立關聯的使用中的下列範例的程式碼：</span><span class="sxs-lookup"><span data-stu-id="28d04-129">When you have that reference, you establish the association using code like that in the following examples:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample2.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample3.cs)]

<span data-ttu-id="28d04-130">如您在 Entity Framework 小組中所見[外部索引鍵關聯上的部落格文章](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx)，其他地方的程式碼複雜度差別更大的情況下。</span><span class="sxs-lookup"><span data-stu-id="28d04-130">As you can see in the Entity Framework team's [blog post on Foreign Key associations](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx), there are other cases where the difference in code complexity is much greater.</span></span> <span data-ttu-id="28d04-131">為想要即時為了更簡單的程式碼的概念資料模型中的實作詳細資料的任何人的需求，Entity Framework 現在可以讓您選擇的資料模型中包括外部索引鍵。</span><span class="sxs-lookup"><span data-stu-id="28d04-131">To meet the needs of those who prefer to live with implementation details in the conceptual data model for the sake of simpler code, the Entity Framework now gives you the option of including foreign keys in the data model.</span></span>

<span data-ttu-id="28d04-132">在 Entity Framework 詞彙中，您的資料模型中包含外部索引鍵，如果您使用*外部索引鍵關聯*，而且如果您排除您使用的外部索引鍵*獨立關聯*。</span><span class="sxs-lookup"><span data-stu-id="28d04-132">In Entity Framework terminology, if you include foreign keys in the data model you're using *foreign key associations*, and if you exclude foreign keys you're using *independent associations*.</span></span>

## <a name="executing-user-defined-sql-commands"></a><span data-ttu-id="28d04-133">執行使用者定義的 SQL 命令</span><span class="sxs-lookup"><span data-stu-id="28d04-133">Executing User-Defined SQL Commands</span></span>

<span data-ttu-id="28d04-134">在舊版的 Entity Framework 中，有無簡單的方式，立即建立您自己的 SQL 命令，並執行它們。</span><span class="sxs-lookup"><span data-stu-id="28d04-134">In earlier versions of the Entity Framework, there was no easy way to create your own SQL commands on the fly and run them.</span></span> <span data-ttu-id="28d04-135">Entity Framework 動態產生的 SQL 命令，或是您必須建立預存程序，並為函式將它匯入。</span><span class="sxs-lookup"><span data-stu-id="28d04-135">Either the Entity Framework dynamically generated SQL commands for you, or you had to create a stored procedure and import it as a function.</span></span> <span data-ttu-id="28d04-136">第 4 版新增`ExecuteStoreQuery`並`ExecuteStoreCommand`方法`ObjectContext`類別可讓您更輕鬆地傳遞直接與資料庫的任何查詢。</span><span class="sxs-lookup"><span data-stu-id="28d04-136">Version 4 adds `ExecuteStoreQuery` and `ExecuteStoreCommand` methods the `ObjectContext` class that make it easier for you to pass any query directly to the database.</span></span>

<span data-ttu-id="28d04-137">假設 Contoso 大學的系統管理員想要能夠在資料庫中執行大量變更，而不需要經歷建立預存程序，並在匯入資料模型的程序。</span><span class="sxs-lookup"><span data-stu-id="28d04-137">Suppose Contoso University administrators want to be able to perform bulk changes in the database without having to go through the process of creating a stored procedure and importing it into the data model.</span></span> <span data-ttu-id="28d04-138">第一個要求是，讓他們變更的資料庫中的所有課程的學分數頁面。</span><span class="sxs-lookup"><span data-stu-id="28d04-138">Their first request is for a page that lets them change the number of credits for all courses in the database.</span></span> <span data-ttu-id="28d04-139">在網頁上，他們想要可以輸入要用來將值相乘的數字每隔`Course`資料列的`Credits`資料行。</span><span class="sxs-lookup"><span data-stu-id="28d04-139">On the web page, they want to be able to enter a number to use to multiply the value of every `Course` row's `Credits` column.</span></span>

<span data-ttu-id="28d04-140">建立新的頁面會*Site.Master*主版頁面，然後將它命名*UpdateCredits.aspx*。</span><span class="sxs-lookup"><span data-stu-id="28d04-140">Create a new page that uses the *Site.Master* master page and name it *UpdateCredits.aspx*.</span></span> <span data-ttu-id="28d04-141">然後新增下列標記，即可`Content`控制項，名為`Content2`:</span><span class="sxs-lookup"><span data-stu-id="28d04-141">Then add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample4.aspx)]

<span data-ttu-id="28d04-142">此標記會建立`TextBox`使用者可以在其中輸入乘數的值，控制`Button`才能執行此命令中，按一下 控制和`Label`控制項，指出受影響的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="28d04-142">This markup creates a `TextBox` control in which the user can enter the multiplier value, a `Button` control to click in order to execute the command, and a `Label` control for indicating the number of rows affected.</span></span>

<span data-ttu-id="28d04-143">開啟*UpdateCredits.aspx.cs*，並新增下列`using`陳述式和按鈕的處理常式`Click`事件：</span><span class="sxs-lookup"><span data-stu-id="28d04-143">Open *UpdateCredits.aspx.cs*, and add the following `using` statement and a handler for the button's `Click` event:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample5.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample6.cs)]

<span data-ttu-id="28d04-144">此程式碼執行的 SQL`Update`命令使用的值，在文字方塊中，並使用標籤來顯示受影響的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="28d04-144">This code executes the SQL `Update` command using the value in the text box and uses the label to display the number of rows affected.</span></span> <span data-ttu-id="28d04-145">執行此頁面之前，先執行*Courses.aspx*頁面，即可取得 「 過去 」 圖片的一些資料。</span><span class="sxs-lookup"><span data-stu-id="28d04-145">Before you run the page, run the *Courses.aspx* page to get a "before" picture of some data.</span></span>

[![I<span data-ttu-id="28d04-146">mage02]</span><span class="sxs-lookup"><span data-stu-id="28d04-146">mage02]</span></span>(what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)

<span data-ttu-id="28d04-147">執行*UpdateCredits.aspx*乘數，請輸入"10"，然後按一下  **Execute**。</span><span class="sxs-lookup"><span data-stu-id="28d04-147">Run *UpdateCredits.aspx*, enter "10" as the multiplier, and then click **Execute**.</span></span>

[![I<span data-ttu-id="28d04-148">mage03]</span><span class="sxs-lookup"><span data-stu-id="28d04-148">mage03]</span></span>(what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)

<span data-ttu-id="28d04-149">執行*Courses.aspx*頁面以查看變更的資料。</span><span class="sxs-lookup"><span data-stu-id="28d04-149">Run the *Courses.aspx* page again to see the changed data.</span></span>

[![I<span data-ttu-id="28d04-150">mage04]</span><span class="sxs-lookup"><span data-stu-id="28d04-150">mage04]</span></span>(what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)

<span data-ttu-id="28d04-151">(如果您想要設定的學分數設回其原始值，在*UpdateCredits.aspx.cs*變更`Credits * {0}`到`Credits / {0}`並重新執行 頁面上，輸入 10 做為除數。)</span><span class="sxs-lookup"><span data-stu-id="28d04-151">(If you want to set the number of credits back to their original values, in *UpdateCredits.aspx.cs* change `Credits * {0}` to `Credits / {0}` and re-run the page, entering 10 as the divisor.)</span></span>

<span data-ttu-id="28d04-152">如需有關如何執行您在程式碼中定義的查詢的詳細資訊，請參閱[How to:直接針對資料來源執行命令](https://msdn.microsoft.com/library/ee358769.aspx)。</span><span class="sxs-lookup"><span data-stu-id="28d04-152">For more information about executing queries that you define in code, see [How to: Directly Execute Commands Against the Data Source](https://msdn.microsoft.com/library/ee358769.aspx).</span></span>

## <a name="model-first-development"></a><span data-ttu-id="28d04-153">模型優先開發</span><span class="sxs-lookup"><span data-stu-id="28d04-153">Model-First Development</span></span>

<span data-ttu-id="28d04-154">這些逐步解說中您會先建立資料庫，並產生資料庫結構為基礎的資料模型。</span><span class="sxs-lookup"><span data-stu-id="28d04-154">In these walkthroughs you created the database first and then generated the data model based on the database structure.</span></span> <span data-ttu-id="28d04-155">在 Entity Framework 4 中，您可以改為使用資料模型開始，並產生資料模型結構為基礎的資料庫。</span><span class="sxs-lookup"><span data-stu-id="28d04-155">In the Entity Framework 4 you can start with the data model instead and generate the database based on the data model structure.</span></span> <span data-ttu-id="28d04-156">如果您要建立的資料庫不存在的應用程式，模型優先方法可讓您建立實體和關聯性在概念上對應用程式，同時不擔心實際的實作詳細資料意義.</span><span class="sxs-lookup"><span data-stu-id="28d04-156">If you're creating an application for which the database doesn't already exist, the model-first approach enables you to create entities and relationships that make sense conceptually for the application, while not worrying about physical implementation details.</span></span> <span data-ttu-id="28d04-157">（如此只能透過初始的開發階段，不過。</span><span class="sxs-lookup"><span data-stu-id="28d04-157">(This remains true only through the initial stages of development, however.</span></span> <span data-ttu-id="28d04-158">最終將會建立資料庫，而且都會在實際執行資料，並徹底重建模型將不再實用;此時，您會回到資料庫優先方法。）</span><span class="sxs-lookup"><span data-stu-id="28d04-158">Eventually the database will be created and will have production data in it, and recreating it from the model will no longer be practical; at that point you'll be back to the database-first approach.)</span></span>

<span data-ttu-id="28d04-159">在本節的教學課程中，您將建立簡單的資料模型，並從它產生資料庫。</span><span class="sxs-lookup"><span data-stu-id="28d04-159">In this section of the tutorial, you'll create a simple data model and generate the database from it.</span></span>

<span data-ttu-id="28d04-160">在 **方案總管**，以滑鼠右鍵按一下*DAL*資料夾，然後選取**加入新項目**。</span><span class="sxs-lookup"><span data-stu-id="28d04-160">In **Solution Explorer**, right-click the *DAL* folder and select **Add New Item**.</span></span> <span data-ttu-id="28d04-161">在 **加入新項目**對話方塊的 **已安裝的範本**選取**資料**，然後選取**ADO.NET 實體資料模型**範本.</span><span class="sxs-lookup"><span data-stu-id="28d04-161">In the **Add New Item** dialog box, under **Installed Templates** select **Data** and then select the **ADO.NET Entity Data Model** template.</span></span> <span data-ttu-id="28d04-162">將新檔案命名*AlumniAssociationModel.edmx*然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="28d04-162">Name the new file *AlumniAssociationModel.edmx* and click **Add**.</span></span>

[![I<span data-ttu-id="28d04-163">mage06]</span><span class="sxs-lookup"><span data-stu-id="28d04-163">mage06]</span></span>(what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)

<span data-ttu-id="28d04-164">這會啟動 Entity Data Model 精靈。</span><span class="sxs-lookup"><span data-stu-id="28d04-164">This launches the Entity Data Model Wizard.</span></span> <span data-ttu-id="28d04-165">在 **選擇模型內容**步驟中，選取**空的模型**，然後按一下 **完成**。</span><span class="sxs-lookup"><span data-stu-id="28d04-165">In the **Choose Model Contents** step, select **Empty Model** and then click **Finish**.</span></span>

[![I<span data-ttu-id="28d04-166">mage07]</span><span class="sxs-lookup"><span data-stu-id="28d04-166">mage07]</span></span>(what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)

<span data-ttu-id="28d04-167">**Entity Data Model Designer**的空白設計介面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="28d04-167">The **Entity Data Model Designer** opens with a blank design surface.</span></span> <span data-ttu-id="28d04-168">拖曳**實體**項目從**工具箱**拖曳至設計介面。</span><span class="sxs-lookup"><span data-stu-id="28d04-168">Drag an **Entity** item from the **Toolbox** onto the design surface.</span></span>

[![I<span data-ttu-id="28d04-169">mage08]</span><span class="sxs-lookup"><span data-stu-id="28d04-169">mage08]</span></span>(what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)

<span data-ttu-id="28d04-170">變更實體名稱，從`Entity1`要`Alumnus`，變更`Id`屬性名稱，以`AlumnusId`，並加入新的純量屬性，名為`Name`。</span><span class="sxs-lookup"><span data-stu-id="28d04-170">Change the entity name from `Entity1` to `Alumnus`, change the `Id` property name to `AlumnusId`, and add a new scalar property named `Name`.</span></span> <span data-ttu-id="28d04-171">若要新增新的屬性可以按 Enter 鍵之後變更的名稱`Id`資料行，或以滑鼠右鍵按一下實體，然後選取**加入純量屬性**。</span><span class="sxs-lookup"><span data-stu-id="28d04-171">To add new properties you can press Enter after changing the name of the `Id` column, or right-click the entity and select **Add Scalar Property**.</span></span> <span data-ttu-id="28d04-172">新屬性的預設類型是`String`，即適合使用這個簡單的示範，但當然您可以在此變更中的資料類型等**屬性**視窗。</span><span class="sxs-lookup"><span data-stu-id="28d04-172">The default type for new properties is `String`, which is fine for this simple demonstration, but of course you can change things like data type in the **Properties** window.</span></span>

<span data-ttu-id="28d04-173">相同的方式來建立另一個實體並將它命名`Donation`。</span><span class="sxs-lookup"><span data-stu-id="28d04-173">Create another entity the same way and name it `Donation`.</span></span> <span data-ttu-id="28d04-174">變更`Id`屬性，以`DonationId`，並新增一個名為的純量屬性`DateAndAmount`。</span><span class="sxs-lookup"><span data-stu-id="28d04-174">Change the `Id` property to `DonationId` and add a scalar property named `DateAndAmount`.</span></span>

[![I<span data-ttu-id="28d04-175">mage09]</span><span class="sxs-lookup"><span data-stu-id="28d04-175">mage09]</span></span>(what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)

<span data-ttu-id="28d04-176">若要新增這兩個實體之間的關聯，以滑鼠右鍵按一下`Alumnus`實體中，選取**新增**，然後選取**關聯**。</span><span class="sxs-lookup"><span data-stu-id="28d04-176">To add an association between these two entities, right-click the `Alumnus` entity, select **Add**, and then select **Association**.</span></span>

[![I<span data-ttu-id="28d04-177">mage10]</span><span class="sxs-lookup"><span data-stu-id="28d04-177">mage10]</span></span>(what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)

<span data-ttu-id="28d04-178">中的預設值**新增關聯** 對話方塊中，是您想要一個對多、 包含導覽屬性 (包括外部索引鍵），因此只要按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="28d04-178">The default values in the **Add Association** dialog box are what you want (one-to-many, include navigation properties, include foreign keys), so just click **OK**.</span></span>

[![I<span data-ttu-id="28d04-179">mage11]</span><span class="sxs-lookup"><span data-stu-id="28d04-179">mage11]</span></span>(what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)

<span data-ttu-id="28d04-180">設計工具加入的關聯線和外部索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="28d04-180">The designer adds an association line and a foreign-key property.</span></span>

[![I<span data-ttu-id="28d04-181">mage12]</span><span class="sxs-lookup"><span data-stu-id="28d04-181">mage12]</span></span>(what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)

<span data-ttu-id="28d04-182">現在您已準備好要建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="28d04-182">Now you're ready to create the database.</span></span> <span data-ttu-id="28d04-183">以滑鼠右鍵按一下設計介面，然後選取**從模型產生資料庫**。</span><span class="sxs-lookup"><span data-stu-id="28d04-183">Right-click the design surface and select **Generate Database from Model**.</span></span>

[![I<span data-ttu-id="28d04-184">mage13]</span><span class="sxs-lookup"><span data-stu-id="28d04-184">mage13]</span></span>(what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)

<span data-ttu-id="28d04-185">這會啟動 [產生資料庫精靈]。</span><span class="sxs-lookup"><span data-stu-id="28d04-185">This launches the Generate Database Wizard.</span></span> <span data-ttu-id="28d04-186">（如果您看到警告，指出未對應的實體，您可以忽略這些目前。）</span><span class="sxs-lookup"><span data-stu-id="28d04-186">(If you see warnings that indicate that the entities aren't mapped, you can ignore those for the time being.)</span></span>

<span data-ttu-id="28d04-187">在 **選擇資料連接**步驟中，按一下**新的連接**。</span><span class="sxs-lookup"><span data-stu-id="28d04-187">In the **Choose Your Data Connection** step, click **New Connection**.</span></span>

[![I<span data-ttu-id="28d04-188">mage14]</span><span class="sxs-lookup"><span data-stu-id="28d04-188">mage14]</span></span>(what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)

<span data-ttu-id="28d04-189">在 **連接屬性**對話方塊中，選取 本機的 SQL Server Express 執行個體，為資料庫命名`AlumniAssociation`。</span><span class="sxs-lookup"><span data-stu-id="28d04-189">In the **Connection Properties** dialog box, select the local SQL Server Express instance and name the database `AlumniAssociation`.</span></span>

[![I<span data-ttu-id="28d04-190">mage15]</span><span class="sxs-lookup"><span data-stu-id="28d04-190">mage15]</span></span>(what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)

<span data-ttu-id="28d04-191">按一下 **是**當系統詢問您要建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="28d04-191">Click **Yes** when you're asked if you want to create the database.</span></span> <span data-ttu-id="28d04-192">當**選擇資料連接**步驟會再次顯示，請按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="28d04-192">When the **Choose Your Data Connection** step is displayed again, click **Next**.</span></span>

<span data-ttu-id="28d04-193">在 **摘要和設定**步驟中，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="28d04-193">In the **Summary and Settings** step, click **Finish**.</span></span>

[![I<span data-ttu-id="28d04-194">mage18]</span><span class="sxs-lookup"><span data-stu-id="28d04-194">mage18]</span></span>(what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)

<span data-ttu-id="28d04-195">A *.sql*使用資料定義語言 (DDL) 命令來建立檔案，但尚未執行的命令。</span><span class="sxs-lookup"><span data-stu-id="28d04-195">A *.sql* file with the data definition language (DDL) commands is created, but the commands haven't been run yet.</span></span>

[![I<span data-ttu-id="28d04-196">mage20]</span><span class="sxs-lookup"><span data-stu-id="28d04-196">mage20]</span></span>(what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)

<span data-ttu-id="28d04-197">使用一種工具，例如**SQL Server Management Studio**來執行指令碼，並且在建立資料表，您可能會在建立時完成`School`資料庫的[快速入門教學課程系列的第一個教學課程](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="28d04-197">Use a tool such as **SQL Server Management Studio** to run the script and create the tables, as you might have done when you created the `School` database for [the first tutorial in the Getting Started tutorial series](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md).</span></span> <span data-ttu-id="28d04-198">（除非您已下載的資料庫。）</span><span class="sxs-lookup"><span data-stu-id="28d04-198">(Unless you downloaded the database.)</span></span>

<span data-ttu-id="28d04-199">您現在可以使用`AlumniAssociation`資料模型，在您的 web pages 您所使用的相同方式`School`模型。</span><span class="sxs-lookup"><span data-stu-id="28d04-199">You can now use the `AlumniAssociation` data model in your web pages the same way you've been using the `School` model.</span></span> <span data-ttu-id="28d04-200">若要這麼做時，將一些資料加入資料表並建立網頁，顯示的資料。</span><span class="sxs-lookup"><span data-stu-id="28d04-200">To try this out, add some data to the tables and create a web page that displays the data.</span></span>

<span data-ttu-id="28d04-201">使用**伺服器總管**，將下列資料列加入`Alumnus`和`Donation`資料表。</span><span class="sxs-lookup"><span data-stu-id="28d04-201">Using **Server Explorer**, add the following rows to the `Alumnus` and `Donation` tables.</span></span>

[![I<span data-ttu-id="28d04-202">mage21]</span><span class="sxs-lookup"><span data-stu-id="28d04-202">mage21]</span></span>(what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)

<span data-ttu-id="28d04-203">建立名為的新網頁*Alumni.aspx*使用*Site.Master*主版頁面。</span><span class="sxs-lookup"><span data-stu-id="28d04-203">Create a new web page named *Alumni.aspx* that uses the *Site.Master* master page.</span></span> <span data-ttu-id="28d04-204">新增下列標記，即可`Content`控制項，名為`Content2`:</span><span class="sxs-lookup"><span data-stu-id="28d04-204">Add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample7.aspx)]

<span data-ttu-id="28d04-205">此標記會建立巢狀`GridView`控制外部顯示校友名稱以及內部顯示捐贈日期與數量。</span><span class="sxs-lookup"><span data-stu-id="28d04-205">This markup creates nested `GridView` controls, the outer one to display alumni names and the inner one to display donation dates and amounts.</span></span>

<span data-ttu-id="28d04-206">開啟*Alumni.aspx.cs*。</span><span class="sxs-lookup"><span data-stu-id="28d04-206">Open *Alumni.aspx.cs*.</span></span> <span data-ttu-id="28d04-207">新增`using`陳述式的資料存取層和外部的處理常式`GridView`控制項的`RowDataBound`事件：</span><span class="sxs-lookup"><span data-stu-id="28d04-207">Add a `using` statement for the data access layer and a handler for the outer `GridView` control's `RowDataBound` event:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample8.cs)]

<span data-ttu-id="28d04-208">此程式碼將內部`GridView`使用控制`Donations`導覽屬性的目前資料列`Alumnus`實體。</span><span class="sxs-lookup"><span data-stu-id="28d04-208">This code databinds the inner `GridView` control using the `Donations` navigation property of the current row's `Alumnus` entity.</span></span>

<span data-ttu-id="28d04-209">執行網頁。</span><span class="sxs-lookup"><span data-stu-id="28d04-209">Run the page.</span></span>

[![I<span data-ttu-id="28d04-210">mage22]</span><span class="sxs-lookup"><span data-stu-id="28d04-210">mage22]</span></span>(what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)

<span data-ttu-id="28d04-211">(注意：此頁面會包含在可下載的專案中，但若要讓它正常運作，您必須在本機 SQL Server Express 執行個體; 中建立資料庫資料庫未隨附 *.mdf*中的檔案*應用程式\_資料*資料夾。)</span><span class="sxs-lookup"><span data-stu-id="28d04-211">(Note: This page is included in the downloadable project, but to make it work you must create the database in your local SQL Server Express instance; the database isn't included as an *.mdf* file in the *App\_Data* folder.)</span></span>

<span data-ttu-id="28d04-212">如需使用 Entity Framework 的 「 模型優先 」 功能的詳細資訊，請參閱 < [Entity Framework 4 中的模型優先](https://msdn.microsoft.com/data/ff830362.aspx)。</span><span class="sxs-lookup"><span data-stu-id="28d04-212">For more information about using the model-first feature of the Entity Framework, see [Model-First in the Entity Framework 4](https://msdn.microsoft.com/data/ff830362.aspx).</span></span>

## <a name="poco-support"></a><span data-ttu-id="28d04-213">POCO 支援</span><span class="sxs-lookup"><span data-stu-id="28d04-213">POCO Support</span></span>

<span data-ttu-id="28d04-214">當您使用網域導向設計方法時，您會設計資料類別，代表資料和商務領域相關的行為。</span><span class="sxs-lookup"><span data-stu-id="28d04-214">When you use domain-driven design methodology, you design data classes that represent data and behavior that's relevant to the business domain.</span></span> <span data-ttu-id="28d04-215">這些類別都應該獨立於用來儲存任何特定技術 （保留） 的資料;也就是說，它們應該*持續*。</span><span class="sxs-lookup"><span data-stu-id="28d04-215">These classes should be independent of any specific technology used to store (persist) the data; in other words, they should be *persistence ignorant*.</span></span> <span data-ttu-id="28d04-216">持續性無知也方便類別進行單元測試因為單元測試專案可以使用任何持續性技術是最方便進行測試。</span><span class="sxs-lookup"><span data-stu-id="28d04-216">Persistence ignorance can also make a class easier to unit test because the unit test project can use whatever persistence technology is most convenient for testing.</span></span> <span data-ttu-id="28d04-217">較早版本的 Entity Framework 會提供有限的非持續性支援，因為實體類別必須繼承自`EntityObject`類別，並因此包含大量的實體架構特有功能。</span><span class="sxs-lookup"><span data-stu-id="28d04-217">Earlier versions of the Entity Framework offered limited support for persistence ignorance because entity classes had to inherit from the `EntityObject` class and thus included a great deal of Entity Framework-specific functionality.</span></span>

<span data-ttu-id="28d04-218">Entity Framework 4 引進了使用實體類別不繼承自`EntityObject`類別，並因此會保存非持續性。</span><span class="sxs-lookup"><span data-stu-id="28d04-218">The Entity Framework 4 introduces the ability to use entity classes that don't inherit from the `EntityObject` class and therefore are persistence ignorant.</span></span> <span data-ttu-id="28d04-219">在 Entity Framework 內容中，通常稱為類別如下*純舊 CLR 物件*（POCO 或 Poco）。</span><span class="sxs-lookup"><span data-stu-id="28d04-219">In the context of the Entity Framework, classes like this are typically called *plain-old CLR objects* (POCO, or POCOs).</span></span> <span data-ttu-id="28d04-220">您可以手動撰寫的 POCO 類別，或您可以自動產生根據現有的資料模型使用 Entity Framework 所提供的文字範本轉換工具組 (T4) 範本。</span><span class="sxs-lookup"><span data-stu-id="28d04-220">You can write POCO classes manually, or you can automatically generate them based on an existing data model using Text Template Transformation Toolkit (T4) templates provided by the Entity Framework.</span></span>

<span data-ttu-id="28d04-221">如需使用 Poco Entity Framework 中的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="28d04-221">For more information about using POCOs in the Entity Framework, see the following resources:</span></span>

- <span data-ttu-id="28d04-222">[處理 POCO 實體](https://msdn.microsoft.com/library/dd456853.aspx)。</span><span class="sxs-lookup"><span data-stu-id="28d04-222">[Working with POCO Entities](https://msdn.microsoft.com/library/dd456853.aspx).</span></span> <span data-ttu-id="28d04-223">這是 Poco，有更多詳細資訊的其他文件的連結與概觀的 MSDN 文件。</span><span class="sxs-lookup"><span data-stu-id="28d04-223">This is an MSDN document that's an overview of POCOs, with links to other documents that have more detailed information.</span></span>
- <span data-ttu-id="28d04-224">[逐步解說：Entity Framework 的 POCO 範本](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx)這是 Entity Framework 的開發小組，其他有關 Poco 的部落格文章的連結的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="28d04-224">[Walkthrough: POCO Template for the Entity Framework](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx) This is a blog post from the Entity Framework development team, with links to other blog posts about POCOs.</span></span>

## <a name="code-first-development"></a><span data-ttu-id="28d04-225">Code First 開發</span><span class="sxs-lookup"><span data-stu-id="28d04-225">Code-First Development</span></span>

<span data-ttu-id="28d04-226">POCO 支援 Entity Framework 4 中的仍需要您建立資料模型，並連結至資料模型的實體類別。</span><span class="sxs-lookup"><span data-stu-id="28d04-226">POCO support in the Entity Framework 4 still requires that you create a data model and link your entity classes to the data model.</span></span> <span data-ttu-id="28d04-227">Entity Framework 的下一個版本將包含稱為*code first 開發*。</span><span class="sxs-lookup"><span data-stu-id="28d04-227">The next release of the Entity Framework will include a feature called *code-first development*.</span></span> <span data-ttu-id="28d04-228">這項功能可讓您使用 Entity Framework 搭配您自己的 POCO 類別而不需要來使用資料模型設計工具或資料模型的 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="28d04-228">This feature enables you to use the Entity Framework with your own POCO classes without needing to use either the data model designer or a data model XML file.</span></span> <span data-ttu-id="28d04-229">(因此，此選項也已呼叫*僅適用程式碼*;*code first*並*僅限程式碼的*都會指向相同的 Entity Framework 功能。)</span><span class="sxs-lookup"><span data-stu-id="28d04-229">(Therefore, this option has also been called *code-only*; *code-first* and *code-only* both refer to the same Entity Framework feature.)</span></span>

<span data-ttu-id="28d04-230">如需使用程式開發的程式碼優先方法的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="28d04-230">For more information about using the code-first approach to development, see the following resources:</span></span>

- <span data-ttu-id="28d04-231">[Code First 和 Entity Framework 4 的開發](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="28d04-231">[Code-First Development with Entity Framework 4](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx).</span></span> <span data-ttu-id="28d04-232">這是由 Scott Guthrie 介紹 code first 開發部落格文章。</span><span class="sxs-lookup"><span data-stu-id="28d04-232">This is a blog post by Scott Guthrie introducing code-first development.</span></span>
- [<span data-ttu-id="28d04-233">Entity Framework 開發小組部落格-張貼標記的 CodeOnly</span><span class="sxs-lookup"><span data-stu-id="28d04-233">Entity Framework Development Team Blog - posts tagged CodeOnly</span></span>](https://blogs.msdn.com/b/efdesign/archive/tags/codeonly/)
- [<span data-ttu-id="28d04-234">Entity Framework 開發小組部落格-張貼標記 Code First</span><span class="sxs-lookup"><span data-stu-id="28d04-234">Entity Framework Development Team Blog - posts tagged Code First</span></span>](https://blogs.msdn.com/b/efdesign/archive/tags/code+first/)
- [<span data-ttu-id="28d04-235">MVC Music Store 教學課程-第 4 部分：模型和資料存取</span><span class="sxs-lookup"><span data-stu-id="28d04-235">MVC Music Store tutorial - Part 4: Models and Data Access</span></span>](../../../../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4.md)
- [<span data-ttu-id="28d04-236">開始使用 MVC 3-第 4 部分：Entity Framework Code First 開發</span><span class="sxs-lookup"><span data-stu-id="28d04-236">Getting Started with MVC 3 - Part 4: Entity Framework Code-First Development</span></span>](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model.md)

<span data-ttu-id="28d04-237">此外，新的 MVC 程式碼-第一個教學課程可建立類似於的 Contoso 大學應用程式的應用程式預計在 2011 年春季發行 [https://asp.net/entity-framework/tutorials](../../../../entity-framework.md)</span><span class="sxs-lookup"><span data-stu-id="28d04-237">In addition, a new MVC Code-First tutorial that builds an application similar to the Contoso University application is projected to be published in the spring of 2011 at [https://asp.net/entity-framework/tutorials](../../../../entity-framework.md)</span></span>

## <a name="more-information"></a><span data-ttu-id="28d04-238">更多資訊</span><span class="sxs-lookup"><span data-stu-id="28d04-238">More Information</span></span>

<span data-ttu-id="28d04-239">這樣就完成的新功能的 Entity Framework 和此繼續透過 Entity Framework 的教學課程系列的概觀。</span><span class="sxs-lookup"><span data-stu-id="28d04-239">This completes the overview to what's new in the Entity Framework and this Continuing with the Entity Framework tutorial series.</span></span> <span data-ttu-id="28d04-240">如需 Entity Framework 4 中這裡未涵蓋的新功能的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="28d04-240">For more information about new features in the Entity Framework 4 that aren't covered here, see the following resources:</span></span>

- <span data-ttu-id="28d04-241">[What's New in ADO.NET](https://msdn.microsoft.com/library/ex6y04yf.aspx) MSDN 主題中的 Entity framework 第 4 版的新功能。</span><span class="sxs-lookup"><span data-stu-id="28d04-241">[What's New in ADO.NET](https://msdn.microsoft.com/library/ex6y04yf.aspx) MSDN topic on new features in version 4 of the Entity Framework.</span></span>
- <span data-ttu-id="28d04-242">[發表最新的 Entity Framework 4](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx)第 4 版的新功能的 Entity Framework 開發小組的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="28d04-242">[Announcing the release of Entity Framework 4](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx) The Entity Framework development team's blog post about new features in version 4.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="28d04-243">上一步</span><span class="sxs-lookup"><span data-stu-id="28d04-243">Previous</span></span>](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
