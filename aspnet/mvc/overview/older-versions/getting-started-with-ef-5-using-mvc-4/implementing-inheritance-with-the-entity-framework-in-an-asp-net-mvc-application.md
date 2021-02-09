---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 使用 ASP.NET MVC 應用程式中的 Entity Framework 來執行繼承， (8/10) |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 來建立 ASP.NET MVC 4 應用程式 .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: de86dd0d1a8e1b68d14971d328fe88a7fdb3e9b1
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2021
ms.locfileid: "99984779"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a>使用 ASP.NET MVC 應用程式中的 Entity Framework 來執行繼承， (8/10) 

由 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。 如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> > [!NOTE] 
> > 
> > 如果您遇到無法解決的問題，請 [下載已完成的章節](building-the-ef5-mvc4-chapter-downloads.md) ，並嘗試重現您的問題。 您通常可以藉由比較程式碼與已完成的程式碼，找到問題的解決方案。 針對一些常見的錯誤和解決方法，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。

在上一個教學課程中，您已處理平行存取例外狀況。 本教學課程將示範如何在資料模型中實作繼承。

在物件導向程式設計中，您可以使用繼承來消除多餘的程式碼。 在本教學課程中，您將變更 `Instructor` 和 `Student` 類別，讓它們衍生自 `Person` 基底類別，而此基底類別包含講師和學生通用的屬性，例如 `LastName`。 您不會新增或變更任何網頁，但是您將變更一些程式碼，這些變更將會自動反映在資料庫中。

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>每個階層的資料表與每一類型的資料表繼承

在物件導向程式設計中，您可以使用繼承來更輕鬆地使用相關類別。 例如， `Instructor` `Student` 資料模型中的和類別 `School` 共用數個屬性，因此會產生多餘的程式碼：

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

假設您想要針對 `Instructor` 和 `Student` 實體所共用的屬性消除多餘的程式碼。 您可以建立 `Person` 只包含這些共用屬性的基類，然後讓 `Instructor` 和 `Student` 實體繼承自該基類，如下圖所示：

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

有幾種方式可以在資料庫中表示此繼承結構。 您可以有一個 `Person` 資料表，其中包含與學生和講師在單一資料表中的相關資訊。 某些資料行只能套用至講師 (`HireDate`) ，有些則只適用于學生 (`EnrollmentDate`) ， () `LastName` `FirstName` 。 一般而言，您會有 *鑒別* 子資料行，以指出每個資料列所代表的類型。 例如，鑑別子資料行的 "Instructor" 代表講師，而 "Student" 代表學生。

![每 hierarchy_example 一份資料表](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

從單一資料庫資料表產生實體繼承結構的這種模式稱為「 *每個* 階層的資料表」， (TPH) 繼承。

替代方法是讓資料庫看起來更像繼承結構。 例如，您可能只有資料表中的名稱欄位 `Person` ，而且具有不同 `Instructor` `Student` 的資料表和 [日期] 欄位。

![每 type_inheritance 一份資料表](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

為每個實體類別建立資料庫資料表的這種模式， (TPT) 繼承的 *每個類型* 都稱為 table。

因為 TPT 模式可能會導致複雜的聯結查詢，所以 TPH 繼承模式通常會在 Entity Framework 中提供比 TPT 繼承模式更好的效能。 本教學課程將示範如何實作 TPH 繼承。 您將執行下列步驟來執行此動作：

- 建立 `Person` 類別，並變更 `Instructor` `Student` 要衍生自的和類別 `Person` 。
- 將模型對資料庫對應程式碼加入至資料庫內容類別。
- 在 `InstructorID` `StudentID` 整個專案中變更和參考 `PersonID` 。

## <a name="creating-the-person-class"></a>建立 Person 類別

 注意：在您更新使用這些類別的控制器之前，您無法在建立下列類別之後編譯專案。 

在 [ *模型* ] 資料夾中，建立 *Person.cs* ，並以下列程式碼取代範本程式碼：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

在 *Instructor.cs* 中， `Instructor` 從類別衍生類別 `Person` ，並移除索引鍵和名稱欄位。 程式碼看起來應該如下列範例所示：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

對 *Student.cs* 進行類似的變更。 `Student`類別看起來會如下列範例所示：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a>將 Person 實體類型加入至模型

在 *SchoolCoNtext.cs* 中，新增 `DbSet` `Person` 實體類型的屬性：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

這就是 Entity Framework 為了設定單表繼承而必須執行的所有工作。 如您所見，重新建立資料庫時，它會有一個 `Person` 資料表來取代 `Student` 和 `Instructor` 資料表。

## <a name="changing-instructorid-and-studentid-to-personid"></a>將 InstructorID 和 StudentID 變更為 PersonID

在 *SchoolCoNtext.cs* 的 Instructor-Course 對應語句中，變更 `MapRightKey("InstructorID")` 為 `MapRightKey("PersonID")` ：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

這不是必要的變更;它只會變更多對多聯結資料表中 InstructorID 資料行的名稱。 如果您將名稱保留為 InstructorID，應用程式仍然可以正常運作。 以下是已完成的 *SchoolCoNtext.cs*：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

接下來，您必須 `InstructorID` 將 `PersonID` `StudentID` `PersonID` _Migrations * 資料夾中時間戳記的遷移檔案，在專案中變更為和。 若要這樣做，您只會找到並開啟需要變更的檔案，然後對開啟的檔案執行全域變更。 在 [ *遷移* ] 資料夾中，您應該變更的唯一檔案是 *Migrations\Configuration.cs.*

1. > [!IMPORTANT]
   > 從 Visual Studio 中關閉所有開啟的檔案開始。
2. 在 [**編輯**] 功能表中，按一下 [**尋找並取代--尋找所有** 檔案]，然後在專案中搜尋包含的所有檔案 `InstructorID` 。  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. 在 [**尋找結果**] 視窗中開啟每 ** 個檔案，在 [遷移] 資料夾中開啟 [ &lt; 時間戳記] &gt; _ \_ .cs * 的檔案，方法是按兩下每個檔案的一行。   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. 開啟 [檔案 **中取代** ] 對話方塊，並將 [ **查詢** ] 變更為 **所有開啟** 的檔。
5. 使用 [檔案 **中取代** ] 對話方塊，將全部變更 `InstructorID` 為 `PersonID.`  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. 尋找專案中包含的所有檔案 `StudentID` 。
7. 在 [**尋找結果**] 視窗中開啟每 ** 個檔案，在 [遷移] 資料夾中開啟 [ &lt; 時間戳記] &gt; _ \_ \* .cs * 的檔案，方法是按兩下每個檔案的一行。   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. 開啟 [檔案 **中取代** ] 對話方塊，並將 [ **查詢** ] 變更為 **所有開啟** 的檔。
9. 使用 [檔案 **中取代** ] 對話方塊，將全部變更 `StudentID` 為 `PersonID` 。   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. 建置專案。

 (請注意，這會示範 `classnameID` 命名主鍵的模式缺點。 如果您在沒有首碼類別名稱的情況下命名 primary key ID，現在就 *不* 需要重新命名。 ) 

## <a name="create-and-update-a-migrations-file"></a>建立和更新遷移檔案

在封裝管理員主控台中 (PMC) 上，輸入下列命令：

`Add-Migration Inheritance`

`Update-Database`在 PMC 中執行命令。 此命令將會在此時失敗，因為我們有遷移不知道如何處理的現有資料。 而您會收到下列錯誤：

*ALTER TABLE 語句與外鍵條件約束「FK dbo」衝突 \_ 。部門 \_ dbo。Person \_ PersonID」。衝突發生在資料庫 "ContosoUniversity" 中，資料表 "dbo。Person "，資料行 ' PersonID '。*

開啟 *\& [遷移 lt; timestamp &gt; \_ Inheritance.cs]* ，並 `Up` 以下列程式碼取代方法：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

再次執行 `update-database` 命令。

> [!NOTE]
> 您可以在遷移資料並進行架構變更時，收到其他錯誤。 如果您收到無法解決的遷移錯誤，可以藉由變更 *Web.config* 檔案中的連接字串或刪除資料庫，繼續進行本教學課程。 最簡單的方法是在 *Web.config* 檔案中重新命名資料庫。 例如，將資料庫名稱變更為 CU \_ 測試，如下列範例所示：
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> 有了新的資料庫，就不會有要遷移的資料，而且 `update-database` 命令更可能會在沒有錯誤的情況下完成。 如需有關如何刪除資料庫的指示，請參閱 [如何從 Visual Studio 2012 卸載資料庫](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。 如果您採用此方法來繼續進行本教學課程，請略過本教學課程結尾的部署步驟，因為部署的網站會在自動執行遷移時取得相同的錯誤。 如果您想要針對遷移錯誤進行疑難排解，最佳的資源是其中一個 Entity Framework 論壇或 StackOverflow.com。

## <a name="testing"></a>測試

執行網站並嘗試各種不同的頁面。 一切項目的運作與之前一樣。

在 **伺服器總管中，** 依序展開 [ **SchoolCoNtext** ] 和 [ **資料表]**，然後您會看到 **學生** 和 **講師** 資料表已被 **Person** 資料表取代。 展開 [ **Person** ] 資料表，您會看到它的所有資料行都是在 **學生** 和 **講師** 資料表中。

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

以滑鼠右鍵按一下 Person 資料表，然後按一下 [顯示資料表資料] 以查看鑑別子資料行。

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

下圖說明新 School 資料庫的結構：

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a>摘要

`Person`、和類別現在已針對每個階層的資料表繼承執行 `Student` `Instructor` 。 如需有關這個和其他繼承結構的詳細資訊，請參閱 Morteza Manavi 的 blog 上的 [繼承對應策略](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) 。 在下一個教學課程中，您將會看到一些方法來執行存放庫和工作單元模式。

您可以在 [ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

> [!div class="step-by-step"]
> [上一個](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 
> [下一步](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
