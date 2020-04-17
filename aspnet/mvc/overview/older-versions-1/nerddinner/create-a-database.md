---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 建立資料庫 | Microsoft 文件
author: rick-anderson
description: 步驟 2 顯示了創建資料庫的步驟,這些資料庫包含我們 NerdDinner 應用程式的所有晚餐和 RSVP 數據。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541607"
---
# <a name="create-a-database"></a><span data-ttu-id="37cc8-103">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="37cc8-103">Create a Database</span></span>

<span data-ttu-id="37cc8-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="37cc8-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="37cc8-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="37cc8-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="37cc8-106">這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第2步,它介紹了如何使用 ASP.NETmVC 1構建小型但完整的Web應用程式。</span><span class="sxs-lookup"><span data-stu-id="37cc8-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="37cc8-107">步驟 2 顯示了創建資料庫的步驟,這些資料庫包含我們 NerdDinner 應用程式的所有晚餐和 RSVP 數據。</span><span class="sxs-lookup"><span data-stu-id="37cc8-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="37cc8-108">如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。</span><span class="sxs-lookup"><span data-stu-id="37cc8-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="37cc8-109">神經晚餐步驟 2:創建資料庫</span><span class="sxs-lookup"><span data-stu-id="37cc8-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="37cc8-110">我們將使用資料庫來儲存我們NerdDinner應用程式的所有晚餐和RSVP數據。</span><span class="sxs-lookup"><span data-stu-id="37cc8-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="37cc8-111">以下步驟顯示了使用免費 SQL Server Express 版本創建資料庫(您可以使用[Microsoft Web 平臺安裝程式](https://www.microsoft.com/web/downloads/platform.aspx)的 V2 輕鬆安裝)。</span><span class="sxs-lookup"><span data-stu-id="37cc8-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="37cc8-112">我們將編寫的所有代碼都適用於 SQL Server Express 和完整 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="37cc8-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="37cc8-113">建立新的 SQL Server Express 資料庫</span><span class="sxs-lookup"><span data-stu-id="37cc8-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="37cc8-114">我們將從右鍵單擊 Web 專案開始,然後選擇 **「新增新&gt;專案」** 選單命令:</span><span class="sxs-lookup"><span data-stu-id="37cc8-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="37cc8-115">這將彈出可視化工作室的「添加新項目」對話框。</span><span class="sxs-lookup"><span data-stu-id="37cc8-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="37cc8-116">我們將按「資料」類別進行篩選,然後選擇「SQL 伺服器資料庫」項範本:</span><span class="sxs-lookup"><span data-stu-id="37cc8-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="37cc8-117">我們將命名要創建的 SQL Server Express 資料庫「NerdDinner.mdf」,然後點擊確定。</span><span class="sxs-lookup"><span data-stu-id="37cc8-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="37cc8-118">然後,Visual Studio 會詢問我們是否要將此檔添加到\_我們的 @App 資料目錄(該目錄已設置包含讀取和寫入安全 ACL):</span><span class="sxs-lookup"><span data-stu-id="37cc8-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="37cc8-119">我們將按下「是」,我們將創建新資料庫並將其添加到解決方案資源管理器中:</span><span class="sxs-lookup"><span data-stu-id="37cc8-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="37cc8-120">在資料庫建立表格</span><span class="sxs-lookup"><span data-stu-id="37cc8-120">Creating Tables within our Database</span></span>

<span data-ttu-id="37cc8-121">我們現在有一個新的空資料庫。</span><span class="sxs-lookup"><span data-stu-id="37cc8-121">We now have a new empty database.</span></span> <span data-ttu-id="37cc8-122">讓我們向它添加一些表。</span><span class="sxs-lookup"><span data-stu-id="37cc8-122">Let's add some tables to it.</span></span>

<span data-ttu-id="37cc8-123">為此,我們將導航到 Visual Studio 中的「伺服器資源管理器」選項卡視窗,這使我們能夠管理資料庫和伺服器。</span><span class="sxs-lookup"><span data-stu-id="37cc8-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="37cc8-124">儲存在應用程式的\_@App 資料資料夾中的 SQL Server Express 資料庫將自動顯示在伺服器資源管理器中。</span><span class="sxs-lookup"><span data-stu-id="37cc8-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="37cc8-125">我們可以選擇使用「伺服器資源管理員」視窗頂部的「連接到資料庫」圖示,將其他 SQL Server 資料庫(本地資料庫和遠端資料庫)新增到清單中:</span><span class="sxs-lookup"><span data-stu-id="37cc8-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="37cc8-126">我們將向NerdDinner資料庫添加兩個錶 - 一個用於存儲我們的晚餐,另一個用於跟蹤 RSVP 接受的接收。</span><span class="sxs-lookup"><span data-stu-id="37cc8-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="37cc8-127">我們可以通過右鍵按一下資料庫中的「表」資料夾並選擇「新增新表」選單命令來建立新錶:</span><span class="sxs-lookup"><span data-stu-id="37cc8-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="37cc8-128">這將打開一個表設計器,允許我們配置表的架構。</span><span class="sxs-lookup"><span data-stu-id="37cc8-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="37cc8-129">對於我們的「Dinners」表,我們將添加 10 列數據:</span><span class="sxs-lookup"><span data-stu-id="37cc8-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="37cc8-130">我們希望「DinnerID」列是表的唯一主鍵。</span><span class="sxs-lookup"><span data-stu-id="37cc8-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="37cc8-131">我們可以通過右鍵單擊「DinnerID」列並選擇「設定主鍵」功能表項來配置此項:</span><span class="sxs-lookup"><span data-stu-id="37cc8-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="37cc8-132">除了使 DinnerID 成為主鍵外,我們還希望將其配置為「標識」列,該列的值隨著新數據行添加到表中而自動遞增(這意味著第一個插入的 Dinner 行的 DinnerID 為 1,第二個插入的行的 DinnerID 為 2,等等)。</span><span class="sxs-lookup"><span data-stu-id="37cc8-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="37cc8-133">為此,我們可以選擇"DinnerID"列,然後使用"列屬性"編輯器將列上的"(即標識)"屬性設置為"是"。</span><span class="sxs-lookup"><span data-stu-id="37cc8-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="37cc8-134">我們將使用標準標識預設值(從 1 開始,在每個新的 Dinner 行上增加 1):</span><span class="sxs-lookup"><span data-stu-id="37cc8-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="37cc8-135">然後,我們將通過鍵入 Ctrl-S 或使用 **「&gt;檔儲存」** 選單命令來保存我們的表。</span><span class="sxs-lookup"><span data-stu-id="37cc8-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="37cc8-136">這將提示我們命名表。</span><span class="sxs-lookup"><span data-stu-id="37cc8-136">This will prompt us to name the table.</span></span> <span data-ttu-id="37cc8-137">我們將將其命名為「晚餐」:</span><span class="sxs-lookup"><span data-stu-id="37cc8-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="37cc8-138">然後,我們新的 Dinners 表將顯示到伺服器資源管理器中的資料庫中。</span><span class="sxs-lookup"><span data-stu-id="37cc8-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="37cc8-139">然後,我們將重複上述步驟,並創建一個"RSVP"表。</span><span class="sxs-lookup"><span data-stu-id="37cc8-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="37cc8-140">此表包含 3 列。</span><span class="sxs-lookup"><span data-stu-id="37cc8-140">This table with have 3 columns.</span></span> <span data-ttu-id="37cc8-141">我們將將 RsvpID 列設定為主鍵,並使其成為識別列:</span><span class="sxs-lookup"><span data-stu-id="37cc8-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="37cc8-142">我們將保存它,並給它的名字"RSVP"。</span><span class="sxs-lookup"><span data-stu-id="37cc8-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="37cc8-143">設定表之間的外鍵關係</span><span class="sxs-lookup"><span data-stu-id="37cc8-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="37cc8-144">現在,我們的資料庫中有兩個表。</span><span class="sxs-lookup"><span data-stu-id="37cc8-144">We now have two tables within our database.</span></span> <span data-ttu-id="37cc8-145">我們最後一個架構設計步驟是在這兩個表之間建立「一對多」關係,以便我們可以將每個 Dinner 行與應用於它的零個或多個 RSVP 行相關聯。</span><span class="sxs-lookup"><span data-stu-id="37cc8-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="37cc8-146">為此,我們將配置 RSVP 表的「DinnerID」列,以便與「Dinners」表中的「DinnerID」列具有外鍵關係。</span><span class="sxs-lookup"><span data-stu-id="37cc8-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="37cc8-147">為此,我們將在伺服器資源管理器中按兩下表設計器中打開 RSVP 表。</span><span class="sxs-lookup"><span data-stu-id="37cc8-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="37cc8-148">然後,我們將選擇其中的"DinnerID"列,右鍵單擊,然後選擇"關係..."內容選單指令:</span><span class="sxs-lookup"><span data-stu-id="37cc8-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="37cc8-149">這將彈出一個對話框,我們可以用它來設置表之間的關係:</span><span class="sxs-lookup"><span data-stu-id="37cc8-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="37cc8-150">我們將按下「添加」按鈕以向對話框添加新關係。</span><span class="sxs-lookup"><span data-stu-id="37cc8-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="37cc8-151">添加關係後,我們將將屬性網格中的"表和列規範"樹視圖節點擴展到對話框的右側,然後單擊"..."按鈕右方:</span><span class="sxs-lookup"><span data-stu-id="37cc8-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="37cc8-152">單擊"..."按鈕將彈出另一個對話框,允許我們指定關係中涉及哪些表和列,並允許我們命名關係。</span><span class="sxs-lookup"><span data-stu-id="37cc8-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="37cc8-153">我們將主鍵表更改為「Dinners」,並選擇「晚餐」表中的「DinnerID」列作為主鍵。</span><span class="sxs-lookup"><span data-stu-id="37cc8-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="37cc8-154">我們的 RSVP 表將是外鍵表和 RSVP。DinnerID 列將作為外鍵關聯:</span><span class="sxs-lookup"><span data-stu-id="37cc8-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="37cc8-155">現在,RSVP 表中的每一行都將與"晚餐"表中的一行相關聯。</span><span class="sxs-lookup"><span data-stu-id="37cc8-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="37cc8-156">SQL Server 將為我們保持參考完整性 , 並且阻止我們添加新的 RSVP 行,如果它不指向有效的 Dinner 行。</span><span class="sxs-lookup"><span data-stu-id="37cc8-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="37cc8-157">如果仍有 RSVP 行引用它,它也會阻止我們刪除 Dinner 行。</span><span class="sxs-lookup"><span data-stu-id="37cc8-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="37cc8-158">新增資料到我們的表格</span><span class="sxs-lookup"><span data-stu-id="37cc8-158">Adding Data to our Tables</span></span>

<span data-ttu-id="37cc8-159">最後,讓我們向「晚餐」表添加一些示例數據。</span><span class="sxs-lookup"><span data-stu-id="37cc8-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="37cc8-160">我們可以在伺服器資源管理器中右鍵按一下資料並選擇「顯示表資料」命令,將資料新增到表中:</span><span class="sxs-lookup"><span data-stu-id="37cc8-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="37cc8-161">我們將添加幾行 Dinner 數據,稍後在開始實現應用程式時可以使用這些數據:</span><span class="sxs-lookup"><span data-stu-id="37cc8-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="37cc8-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37cc8-162">Next Step</span></span>

<span data-ttu-id="37cc8-163">我們已經完成了資料庫的創建。</span><span class="sxs-lookup"><span data-stu-id="37cc8-163">We've finished creating our database.</span></span> <span data-ttu-id="37cc8-164">現在,讓我們創建模型類,可用於查詢和更新它。</span><span class="sxs-lookup"><span data-stu-id="37cc8-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="37cc8-165">[前一個](create-a-new-aspnet-mvc-project.md)
> [下一個](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="37cc8-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
