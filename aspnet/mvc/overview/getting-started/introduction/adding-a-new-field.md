---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: 加入新欄位 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 7018de3eab9d7cced72c76d0b74a79f7c8154f9d
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045139"
---
# <a name="adding-a-new-field"></a>新增欄位

依 [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

在本節中，您將使用 Entity Framework Code First 移轉將某些變更遷移至模型類別，以便將變更套用到資料庫。

依預設，當您使用 Entity Framework Code First 來自動建立資料庫時（如同您稍早在本教學課程中所做的），Code First 會將資料表新增至資料庫，以協助追蹤資料庫的架構是否與其產生的模型類別同步。 如果未同步，Entity Framework 會擲回錯誤。 這可讓您更輕鬆地在開發期間追蹤問題，您可能只需要在執行時間) 隱匿錯誤，就能找到 (。

## <a name="setting-up-code-first-migrations-for-model-changes"></a>設定模型變更的 Code First 移轉

流覽至方案總管。 以滑鼠右鍵按一下 [ *電影 .mdf* ] 檔案，然後選取 [ **刪除** ] 以移除電影資料庫。 如果您沒有看到 [ *電影 .mdf* ] 檔案，請按一下紅色外框中顯示的 [ **顯示所有** 檔案] 圖示。

![](adding-a-new-field/_static/image1.png)

建置應用程式，確定沒有任何錯誤。

從 [ **工具** ] 功能表中，按一下 [ **NuGet 封裝管理員** 然後 **封裝管理員主控台**。

![新增套件手冊](adding-a-new-field/_static/image2.png)

在 [ **封裝管理員主控台** ] 視窗中，于 `PM>` 提示輸入

啟用-遷移-CoNtextTypeName MvcMovie。 MovieDBCoNtext

![](adding-a-new-field/_static/image3.png)

以上所示的**啟用遷移**命令 (，) 在新的 [*遷移*] 資料夾中建立*Configuration.cs*檔案。

![](adding-a-new-field/_static/image4.png)

Visual Studio 會開啟 *Configuration.cs* 檔案。 `Seed`以下列程式碼取代*Configuration.cs*檔中的方法：

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

將滑鼠停留在下的紅色波浪線上 `Movie` ，然後按一下 `Show Potential Fixes` ，再按一下 [ **使用** **MvcMovie];**

![](adding-a-new-field/_static/image5.png)

這麼做會新增下列 using 語句：

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> Code First 移轉會在 `Seed` 每次遷移 (之後呼叫方法，也就是在封裝管理員主控台) 中呼叫 **update-database** ，而這個方法會更新已插入的資料列，如果尚不存在，則會插入這些資料列。
> 
> 下列程式碼中的 [>addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 方法會執行 "upsert" 作業：
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> 由於 [種子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 方法會在每次遷移時執行，因此您不能只插入資料，因為您嘗試加入的資料列將會在第一次建立資料庫的遷移之後存在。 如果您嘗試插入已經存在的資料列，則 "[upsert](http://en.wikipedia.org/wiki/Upsert)" 作業會防止發生的錯誤，但它會覆寫您在測試應用程式時可能進行的資料變更。 使用某些資料表中的測試資料時，您可能不會想要這樣做：在某些情況下，當您在測試時變更資料時，您會希望變更在資料庫更新之後仍維持不變。 在此情況下，您會想要執行條件式插入作業：只有在資料列不存在時，才插入該資料列。   
> 
> 傳遞至 [>addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 方法的第一個參數會指定要用來檢查資料列是否已經存在的屬性。 針對您提供的測試電影資料， `Title` 此屬性可用於此用途，因為清單中的每個標題都是唯一的：
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> 這段程式碼假設標題是唯一的。 如果您手動新增重複的標題，您將會在下一次執行遷移時收到下列例外狀況。   
> 
> *序列包含一個以上的元素*  
> 
> 如需 [>addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 方法的詳細資訊，請參閱 [使用 EF 4.3 >addorupdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)。

**按 CTRL-SHIFT-B 以建立專案。** 如果您目前未建立，下列步驟將會失敗 (。 ) 

下一步是建立 `DbMigration` 初始遷移的類別。 這項遷移會建立新的資料庫，這就是您在上一個步驟中刪除了 *movie .mdf* 檔案的原因。

在 **封裝管理員主控台** ] 視窗中，輸入用 `add-migration Initial` 來建立初始遷移的命令。 名稱 "初始" 是任意的，用來命名建立的遷移檔。

![](adding-a-new-field/_static/image6.png)

Code First 移轉會在 (名稱為 *{DateStamp} \_ * ) 的 [*遷移*] 資料夾中建立另一個類別檔案，且此類別包含可建立資料庫架構的程式碼。 使用時間戳預先修正遷移檔案名，以協助進行排序。 檢查 *{DateStamp} \_ Initial.cs* 檔案，其中包含為 `Movies` Movie DB 建立資料表的指示。 當您在下列指示中更新資料庫時，此 *{DateStamp} \_ Initial.cs* 檔案將會執行並建立資料庫架構。 然後，會執行 **種子** 方法，以測試資料填入資料庫。

在 **封裝管理員主控台**中，輸入用 `update-database` 來建立資料庫的命令，並執行 `Seed` 方法。

![](adding-a-new-field/_static/image7.png)

如果您收到指出資料表已經存在且無法建立的錯誤，可能是因為您在刪除資料庫之後，以及在執行之前執行了應用程式 `update-database` 。 在這種情況下，請再次刪除 *電影 .mdf* 檔案，然後重試 `update-database` 命令。 如果您仍然收到錯誤，請刪除 [遷移] 資料夾和內容，然後從這個頁面頂端的指示開始 (這會刪除 [ *電影 .mdf* 檔案]，然後繼續進行 [啟用-遷移) ]。 如果您仍然收到錯誤，請開啟 SQL Server 物件總管，並從清單中移除資料庫。

執行應用程式，並流覽至 */Movies* URL。 植入資料隨即顯示。

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>將 Rating 屬性新增至電影模型

首先，將新的 `Rating` 屬性加入至現有的 `Movie` 類別。 開啟 *Models\Movie.cs* 檔案，並新增 `Rating` 如下所示的屬性：

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

完整 `Movie` 類別現在看起來會像下列程式碼：

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

 (Ctrl + Shift + B) 來建立應用程式。

因為您已將新欄位新增至 `Movie` 類別，所以也需要更新系結 *白名單* ，以便包含這個新屬性。 更新 `bind` `Create` 和 `Edit` 動作方法的屬性，以包含 `Rating` 屬性：

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

您也需要更新檢視範本，以便在瀏覽器檢視中顯示、建立和編輯新的 `Rating` 屬性。

開啟 *\Views\Movies\Index.cshtml* 檔案，並在 `<th>Rating</th>` [ **Price** ] 資料行之後加入資料行標題。 然後新增 `<td>` 接近範本結尾的資料行，以轉譯 `@item.Rating` 值。 以下是更新的 *Index. cshtml* view 範本看起來像這樣：

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

接下來，開啟 *\Views\Movies\Create.cshtml* 檔案，並以下列醒目提示的 `Rating` 標記新增欄位。 這會呈現一個文字方塊，讓您可以在新電影建立時指定評等。

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

您現在已更新應用程式程式碼，以支援新的 `Rating` 屬性。

執行應用程式，並流覽至 */Movies* URL。 但是當您這樣做時，您會看到下列其中一個錯誤：

![](adding-a-new-field/_static/image9.png)  
  
在建立資料庫之後，支援 ' MovieDBCoNtext ' 內容的模型已變更。 請考慮使用 Code First 移轉來更新資料庫 (https://go.microsoft.com/fwlink/?LinkId=238269) 。

![](adding-a-new-field/_static/image10.png)

您看到此錯誤 `Movie` 是因為應用程式中已更新的模型類別現在與 `Movie` 現有資料庫的資料表架構不同。 (資料庫資料表中沒有任何 `Rating` 資料行)。

有幾個方法可以解決這個錯誤：

1. 讓 Entity Framework 自動卸除資料庫，並重新依據新的模型類別結構描述來建立資料庫。 在開發週期早期，當您在測試資料庫上進行開發時，這個方法會很方便；其可讓您一併調整模型和資料庫結構描述，更加快速。 但缺點是您會遺失資料庫中現有的資料，因此您 *不* 會想要在實際執行的資料庫上使用此方法！ 使用初始設定式將測試資料自動植入資料庫，通常是開發應用程式的有效方式。 如需 Entity Framework 資料庫初始化運算式的詳細資訊，請參閱 [ASP.NET MVC/Entity Framework 教學](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)課程。
2. 您可明確修改現有資料庫的結構描述，使其符合模型類別。 這種方法的優點是可以保留您的資料。 您可以手動方式或藉由建立資料庫變更指令碼來進行這項變更。
3. 使用 Code First 移轉來更新資料庫結構描述。

在本教學課程中，我們將使用 Code First 移轉。

更新種子方法，讓它為新的資料行提供值。 開啟 Migrations\Configuration.cs 檔案，並將 [評等] 欄位新增至每個 Movie 物件。

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

建立解決方案，然後開啟 **封裝管理員主控台** 視窗，並輸入下列命令：

`add-migration Rating`

此 `add-migration` 命令會告知遷移架構使用目前的 MOVIE DB 架構來檢查目前的電影模型，並建立必要的程式碼來將資料庫移轉至新的模型。 名稱 *評* 等是任意的，用來命名遷移檔。 針對遷移步驟使用有意義的名稱是很有説明的。

當此命令完成時，Visual Studio 會開啟定義新衍生類別的類別檔案 `DbMigration` ，而且在方法中， `Up` 您可以看到建立新資料行的程式碼。

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

建立解決方案，然後 `update-database` 在 **封裝管理員主控台** 視窗中輸入命令。

下圖顯示 **封裝管理員主控台** 視窗中的輸出， (前面加 *分級* 的日期戳記將會不同。 ) 

![](adding-a-new-field/_static/image11.png)

重新執行應用程式，並流覽至/Movies URL。 您可以看到新的 [評等] 欄位。

![](adding-a-new-field/_static/image12.png)

按一下 [ **建立新** 的] 連結以新增電影。 請注意，您可以新增評等。

![7_CreateRioII](adding-a-new-field/_static/image13.png)

按一下 [建立]。 新的電影（包含評等）現在會顯示在電影清單中：

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

現在專案正在使用遷移，您不需要在加入新欄位時卸載資料庫，也不需要更新架構。 在下一節中，我們會進行更多的架構變更，並使用遷移來更新資料庫。

您也應該將 `Rating` 欄位加入至 [編輯]、[詳細資料] 和 [刪除] 視圖範本。

您可以再次在 **封裝管理員主控台** 視窗中輸入 "update-database" 命令，而不會執行任何遷移程式碼，因為架構符合模型。 不過，執行 "update-database" 將會 `Seed` 再次執行方法，如果您變更了任何種子資料，變更將會遺失，因為 `Seed` 方法會 upsert 資料。 您可以 `Seed` 在 Tom Dykstra 的熱門 [ASP.NET MVC/Entity Framework 教學](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)課程中閱讀更多有關此方法的資訊。

在本節中，您會瞭解如何修改模型物件，並讓資料庫與變更保持同步。 您也已瞭解使用範例資料來填入新建立資料庫的方法，讓您可以試用案例。 這只是 Code First 的快速簡介，請參閱為 [ASP.NET MVC 應用程式建立 Entity Framework 資料模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) ，以取得主體的完整教學課程。 接下來，讓我們來看看如何將更豐富的驗證邏輯加入至模型類別，並讓某些商務規則得以強制執行。

> [!div class="step-by-step"]
> [上一個](adding-search.md) 
> [下一步](adding-validation.md)
