---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: 使用模型系結和 web forms 來抓取和顯示資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結讓資料互動更為直接-.。。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: d5f1982196c5985b001ca42c2711174e036bb1ec
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240747"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a>使用模型系結和 web forms 來抓取和顯示資料

> 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結可讓資料互動比處理資料來源物件（例如 ObjectDataSource 或 SqlDataSource）更直接。 此系列從簡介材料開始，並在稍後的教學課程中移至更先進的概念。
> 
> 模型系結模式適用于任何資料存取技術。 在本教學課程中，您將使用 Entity Framework，但您可以使用最熟悉的資料存取技術。 從資料系結伺服器控制項（例如 GridView、ListView、DetailsView 或 FormView 控制項），您可以指定用來選取、更新、刪除及建立資料的方法名稱。 在本教學課程中，您將指定 SelectMethod 的值。 
> 
> 在該方法中，您會提供用來抓取資料的邏輯。 在下一個教學課程中，您將設定 UpdateMethod、DeleteMethod 和 InsertMethod 的值。
>
> 您可以[下載](https://go.microsoft.com/fwlink/?LinkId=286116)c # 或 Visual Basic 中的完整專案。 可下載的程式碼適用于 Visual Studio 2012 和更新版本。 它會使用 Visual Studio 2012 範本，這與本教學課程中所顯示的 Visual Studio 2017 範本稍有不同。
> 
> 在教學課程中，您會在 Visual Studio 中執行應用程式。 您也可以將應用程式部署至主機服務提供者，使其可透過網際網路使用。 Microsoft 提供免費的 web 主機服務，最多可達10個網站  
> [免費的 Azure 試用帳戶](https://azure.microsoft.com/free/dotnet/)。 如需如何將 Visual Studio Web 專案部署至 Azure App Service Web Apps 的詳細資訊，請參閱[使用 Visual Studio 系列的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。 該教學課程也會示範如何使用 Entity Framework Code First 移轉將您的 SQL Server 資料庫部署至 Azure SQL Database。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> - Microsoft Visual Studio 2017 或 Microsoft Visual Studio Community 2017
>   
> 本教學課程也適用于 Visual Studio 2012 和 Visual Studio 2013，但使用者介面和專案範本中有一些差異。

## <a name="what-youll-build"></a>您將建立的內容

在本教學課程中，您將會：

* 建立資料物件，以反映學生在課程中註冊的大學
* 從物件建立資料庫資料表
* 以測試資料填入資料庫
* 在 web 表單中顯示資料

## <a name="create-the-project"></a>建立專案

1. 在 Visual Studio 2017 中，建立名為**ContosoUniversityModelBinding**的**ASP.NET Web 應用程式（.NET Framework）** 專案。

   ![建立專案](retrieving-data/_static/image19.png)

2. 選取 [確定]。 選取範本的對話方塊隨即出現。

   ![選取 web 表單](retrieving-data/_static/image3.png)

3. 選取 [ **Web** form] 範本。 

4. 如有必要，請將驗證變更為**個別使用者帳戶**。 

5. 選取 [確定] 可建立專案。

## <a name="modify-site-appearance"></a>修改網站外觀

   進行一些變更，以自訂網站外觀。 
   
   1. 開啟網站. Master 檔案。
   
   2. 變更標題以顯示**Contoso 大學**，而不是**我的 ASP.NET 應用程式**。

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. 將標題文字從 [**應用程式名稱**] 變更為 [ **Contoso 大學**]。

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. 將導覽標頭連結變更為適當的網站。 
   
      移除 [**關於**] 和 [**連絡人**] 的連結，改為連結至您將建立的 [**學生**] 頁面。

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. 儲存網站。

## <a name="add-a-web-form-to-display-student-data"></a>新增 web 表單以顯示學生資料

   1. 在**方案總管**中，以滑鼠右鍵按一下您的專案，然後依序選取 [**加入**] 和 [**新增專案**]。 
   
   2. 在 [**加入新專案**] 對話方塊中，選取 [**含有主版頁面的 Web 表單**] 範本，並將其命名為 [student **. .aspx**]。

      ![建立頁面](retrieving-data/_static/image5.png)

   3. 選取 [新增]。
   
   4. 在 web 表單的主版頁面上，選取 [**網站. 主機**]。
   
   5. 選取 [確定]。

## <a name="add-the-data-model"></a>加入資料模型

在 [**模型**] 資料夾中，新增名為**UniversityModels.cs**的類別。

   1. 以滑鼠右鍵按一下 [**模型**]，然後依序選取 [**加入**] 和 [**新增專案**]。 [加入新項目] **** 對話方塊隨即出現。

   2. 從左側導覽功能表中，依序選取 [程式**代碼**] 和 [**類別**]。

      ![建立模型類別](retrieving-data/_static/image20.png)

   3. 將類別命名為**UniversityModels.cs** ，然後選取 [**新增**]。

      在此檔案中，定義 `SchoolContext` 、 `Student` 、 `Enrollment` 和 `Course` 類別，如下所示：

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      `SchoolContext`類別衍生自 `DbContext` ，其會管理資料庫連接和資料中的變更。

      在 `Student` 類別中，請注意套用至 `FirstName` 、 `LastName` 和屬性的屬性 `Year` 。 本教學課程會使用這些屬性來進行資料驗證。 為了簡化程式碼，只有這些屬性會以資料驗證屬性來標示。 在實際專案中，您會將驗證屬性套用至需要驗證的所有屬性。

   4. 儲存 UniversityModels.cs。

## <a name="set-up-the-database-based-on-classes"></a>根據類別設定資料庫

本教學課程使用[Code First 移轉](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/)來建立物件和資料庫資料表。 這些表格會儲存學生及其課程的相關資訊。

   1. 選取 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。

   2. 在 [**套件管理員主控台**] 中，執行下列命令：  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      如果命令順利完成，就會出現訊息，指出已啟用 [遷移]。

      ![啟用遷移](retrieving-data/_static/image8.png)

      請注意，已建立名為*Configuration.cs*的檔案。 `Configuration`類別具有 `Seed` 方法，可以預先填入含有測試資料的資料庫資料表。

## <a name="pre-populate-the-database"></a>預先填入資料庫

   1. 開啟 Configuration.cs。
   
   2. 將下列程式碼新增至 `Seed` 方法。 此外，加入 `using` 命名空間的語句 `ContosoUniversityModelBinding. Models` 。

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. 儲存 Configuration.cs。

   4. 在 [套件管理員主控台] 中，執行 [**新增-遷移初始**] 命令。

   5. 執行命令**update-database**。

      如果您在執行此命令時收到例外狀況， `StudentID` 和 `CourseID` 值可能與 `Seed` 方法值不同。 開啟這些資料庫資料表，並尋找和的現有值 `StudentID` `CourseID` 。 將這些值新增至程式碼以植入 `Enrollments` 資料表。

## <a name="add-a-gridview-control"></a>新增 GridView 控制項

填入資料庫資料之後，您就可以開始取出該資料並加以顯示。 

1. 開啟 [student]。

2. 找出 `MainContent` 預留位置。 在該預留位置內，新增包含此程式碼的**GridView**控制項。

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   注意事項：
   * 請注意 `SelectMethod` GridView 元素中屬性的設定值。 這個值會指定用來抓取 GridView 資料的方法，您可以在下一個步驟中建立此資料。 
   
   * `ItemType`屬性會設定為稍 `Student` 早建立的類別。 此設定可讓您參考標記中的類別屬性。 例如， `Student` 類別具有名為的集合 `Enrollments` 。 您可以使用 `Item.Enrollments` 來抓取該集合，然後使用[LINQ 語法](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq)來抓取每個學生的已註冊點數總和。
   
3. 儲存 student .aspx。

## <a name="add-code-to-retrieve-data"></a>加入程式碼以取出資料

   在 student 程式碼後置檔案中，新增針對值所指定的方法 `SelectMethod` 。 
   
   1. 開啟 Students.aspx.cs。
   
   2. `using`為 `ContosoUniversityModelBinding. Models` 和 `System.Data.Entity` 命名空間新增語句。

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. 新增您為指定的方法 `SelectMethod` ：

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      `Include`子句可改善查詢效能，但不是必要的。 如果沒有 `Include` 子句，就會使用消極式[*載入*](https://en.wikipedia.org/wiki/Lazy_loading)來抓取資料，這牽涉到每次取得相關資料時，將個別查詢傳送至資料庫。 使用 `Include` 子句時，會使用積極式*載入*來抓取資料，這表示單一資料庫查詢會抓取所有相關資料。 如果未使用相關資料，積極式載入會較不有效率，因為會抓取更多資料。 不過，在此情況下，積極式載入會提供最佳效能，因為會顯示每筆記錄的相關資料。

      如需載入相關資料時的效能考慮的詳細資訊，請參閱[ASP.NET MVC 應用程式一文中的使用 Entity Framework 讀取相關資料](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)一節中的「**延遲」、「積極」和「明確載入相關資料**」一節。

      根據預設，資料會依標示為索引鍵的屬性值進行排序。 您可以加入 `OrderBy` 子句來指定不同的排序值。 在此範例中，預設 `StudentID` 屬性用於排序。 在[排序、分頁及篩選資料](sorting-paging-and-filtering-data.md)一文中，使用者可以選取資料行進行排序。
 
   4. 儲存 Students.aspx.cs。

## <a name="run-your-application"></a>執行您的應用程式 

執行您的 web 應用程式（**F5**），然後流覽至 [**學生**] 頁面，其中會顯示下列內容：

   ![顯示資料](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a>自動產生模型系結方法

當您完成本教學課程系列時，您可以直接將教學課程中的程式碼複製到您的專案。 不過，這種方法的其中一個缺點是，您可能不會注意到 Visual Studio 所提供的功能會自動產生模型系結方法的程式碼。 當您處理自己的專案時，自動產生程式碼可以節省您的時間，並協助您瞭解如何執行作業。 本節說明自動程式碼產生功能。 此區段僅供參考，而且不包含您在專案中所需執行的任何程式碼。 

在 `SelectMethod` 標記程式碼中設定、、或屬性的值時 `UpdateMethod` `InsertMethod` `DeleteMethod` ，您可以選取 [**建立新方法**] 選項。

![建立方法](retrieving-data/_static/image18.png)

Visual Studio 不僅會在程式碼後置中建立具有適當簽章的方法，也會產生可執行作業的實做程式碼。 如果您在 `ItemType` 使用自動程式碼產生功能之前先設定屬性，則產生的程式碼會使用該類型進行作業。 例如，設定 `UpdateMethod` 屬性時，會自動產生下列程式碼：

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

同樣地，此程式碼不需要新增至您的專案。 在下一個教學課程中，您將會執行更新、刪除和加入新資料的方法。

## <a name="summary"></a>摘要

在本教學課程中，您已建立資料模型類別，並從這些類別產生資料庫。 您已使用測試資料填入資料庫資料表。 您已使用模型系結來抓取資料庫中的資料，然後在 GridView 中顯示資料。

在此系列的下一個[教學](updating-deleting-and-creating-data.md)課程中，您將會啟用更新、刪除和建立資料。

> [!div class="step-by-step"]
> [下一步](updating-deleting-and-creating-data.md)
