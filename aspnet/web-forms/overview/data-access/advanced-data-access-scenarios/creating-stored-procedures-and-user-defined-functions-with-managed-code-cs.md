---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
title: '使用 Managed 程式碼建立預存程式和使用者定義函數 (c # ) |Microsoft Docs'
author: rick-anderson
description: Microsoft SQL Server 2005 與 .NET Common Language Runtime 整合，可讓開發人員透過 managed 程式碼建立資料庫物件。 本教學課程 .。。
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 213eea41-1ab4-4371-8b24-1a1a66c515de
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
msc.type: authoredcontent
ms.openlocfilehash: c1882d019d9dfde2dc4f960cae65aa8268c97a51
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045295"
---
# <a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-c"></a>使用受控碼建立預存程序和使用者定義函式 (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_CS.zip) 或 [下載 PDF](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/datatutorial75cs1.pdf)

> Microsoft SQL Server 2005 與 .NET Common Language Runtime 整合，可讓開發人員透過 managed 程式碼建立資料庫物件。 本教學課程示範如何使用您的 Visual Basic 或 c # 程式碼，建立 managed 預存程式和受控使用者定義函數。 我們也會看到這些版本的 Visual Studio 如何讓您對這類 managed 資料庫物件進行 debug。

## <a name="introduction"></a>簡介

像是 Microsoft s SQL Server 2005 的資料庫會使用 [ (結構化查詢語言 (SQL) transact-sql) ](http://en.wikipedia.org/wiki/Transact-SQL) 來插入、修改及取出資料。 大部分的資料庫系統都包含用來分組一連串 SQL 語句的結構，這些語句接著可以用單一、可重複使用的單位來執行。 預存程式就是其中一個範例。 另一種是 *使用者定義* 的函式 (udf) ，這是我們將在步驟9中更詳細地檢查的結構。

SQL 的核心是設計用來處理資料集。 `SELECT`、 `UPDATE` 和 `DELETE` 語句本身就會套用至對應資料表中的所有記錄，而且只會受到其 `WHERE` 子句的限制。 但有許多語言功能是設計來一次處理一筆記錄，以及處理純量資料。 [ `CURSOR` 允許一](http://www.sqlteam.com/item.asp?ItemID=553)組記錄一次迴圈一個記錄。 字串操作函式（例如、和）使用純量 `LEFT` `CHARINDEX` `PATINDEX` 資料。 SQL 也包含和之類的控制流程語句 `IF` `WHILE` 。

在 Microsoft SQL Server 2005 之前，預存程式和 Udf 只能定義為 T-sql 語句的集合。 不過，SQL Server 2005 的設計目的是要提供與 [Common Language Runtime (CLR) ](https://msdn.microsoft.com/netframework/aa497266.aspx)（所有 .net 元件所使用的執行時間）的整合。 因此，可以使用 managed 程式碼來建立 SQL Server 2005 資料庫中的預存程式和 Udf。 也就是說，您可以建立預存程式或 UDF 作為 c # 類別中的方法。 這可讓這些預存程式和 Udf 利用 .NET Framework 中的功能，以及從您自己的自訂類別。

在本教學課程中，我們將探討如何建立 managed 預存程式和使用者定義的函式，以及如何將其整合到 Northwind 資料庫中。 現在就開始吧！

> [!NOTE]
> 受管理的資料庫物件在 SQL 對應專案方面提供一些優點。 語言豐富且熟悉，以及重複使用現有程式碼和邏輯的能力，是主要優點。 但是，當您使用的資料集不牽涉到許多程式邏輯時，管理資料庫物件的效率可能較低。 如需更全面討論使用 managed 程式碼與 T-sql 的優點，請參閱 [使用 managed 程式碼來建立資料庫物件的優點](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx)。

## <a name="step-1-moving-the-northwind-database-out-ofapp_data"></a>步驟1：將 Northwind 資料庫移出`App_Data`

至此，我們到目前為止的所有教學課程都已在 web 應用程式的資料夾中使用 Microsoft SQL Server 2005 Express Edition 資料庫檔案 `App_Data` 。 將資料庫放入 `App_Data` 簡化的散發和執行這些教學課程，因為所有檔案都位於一個目錄中，而且不需要額外的設定步驟來測試教學課程。

不過，在本教學課程中，我們會將 Northwind 資料庫移出 `App_Data` ，並明確地向 SQL Server 2005 Express Edition 資料庫實例註冊。 雖然我們可以使用資料夾中的資料庫來執行此教學課程的步驟，但有 `App_Data` 幾個步驟會藉由明確地向 SQL Server 2005 Express Edition 資料庫實例註冊資料庫，使得更簡單的步驟。

本教學課程的下載會有兩個資料庫檔案 `NORTHWND.MDF` ，並 `NORTHWND_log.LDF` 放在名為的資料夾中 `DataFiles` 。 如果您遵循自己的教學課程執行，請關閉 Visual Studio，並將 `NORTHWND.MDF` 和檔案 `NORTHWND_log.LDF` 從網站 s `App_Data` 資料夾移至網站以外的資料夾。 一旦將資料庫檔案移至另一個資料夾，就必須向 SQL Server 2005 Express Edition 資料庫實例註冊 Northwind 資料庫。 這可以從 SQL Server Management Studio 完成。 如果您的電腦上已安裝非 Express Edition 的 SQL Server 2005，則可能已安裝 Management Studio。 如果您的電腦上只有 SQL Server 2005 Express Edition，請花一點時間下載並安裝 [Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)。

啟動 SQL Server Management Studio。 如 [圖 1] 所示，Management Studio 開始詢問要連接的伺服器。 在 [伺服器名稱] 中輸入 localhost\SQLExpress，在 [驗證] 下拉式清單中選擇 [Windows 驗證]，然後按一下 [連線]。

![連接到適當的資料庫實例](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image1.png)

**圖 1**：連接到適當的資料庫實例

連接之後，物件總管視窗將會列出 SQL Server 2005 Express Edition 資料庫實例的相關資訊，包括其資料庫、安全性資訊、管理選項等等。

我們需要將 Northwind 資料庫附加 `DataFiles` (或您可能已將其移) 至 SQL Server 2005 Express Edition 資料庫實例的任何位置。 以滑鼠右鍵按一下 [資料庫] 資料夾，然後從內容功能表中選擇 [附加] 選項。 這會顯示 [附加資料庫] 對話方塊。 按一下 [加入] 按鈕，向下切入至適當的檔案 `NORTHWND.MDF` ，然後按一下 [確定]。 此時您的畫面看起來應該類似 [圖 2]。

[![連接到適當的資料庫實例](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image2.png)

**圖 2**：連接到適當的資料庫實例 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image4.png)) 

> [!NOTE]
> 透過 Management Studio 連接到 SQL Server 2005 Express Edition 實例時，[附加資料庫] 對話方塊不會讓您向下切入到使用者設定檔目錄，例如我的檔。 因此，請務必將 `NORTHWND.MDF` 和檔案放 `NORTHWND_log.LDF` 在非使用者設定檔目錄中。

按一下 [確定] 按鈕以附加資料庫。 [附加資料庫] 對話方塊會關閉，而物件總管現在應該會列出剛剛附加的資料庫。 Northwind 資料庫很可能會有類似的名稱 `9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF` 。 以滑鼠右鍵按一下資料庫，然後選擇 [重新命名]，將資料庫重新命名為 Northwind。

![將資料庫重新命名為 Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image5.png)

**圖 3**：將資料庫重新命名為 Northwind

## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>步驟2：在 Visual Studio 中建立新的方案和 SQL Server 專案

為了在 SQL Server 2005 中建立 managed 預存程式或 Udf，我們會將預存程式和 UDF 邏輯撰寫為類別中的 c # 程式碼。 撰寫程式碼之後，我們必須將此類別編譯成 (檔案的元件 `.dll`) 、向 SQL Server 資料庫註冊元件，然後在資料庫中建立指向元件中對應方法的預存程式或 UDF 物件。 您可以手動執行這些步驟。 我們可以在任何文字編輯器中建立程式碼、使用 c # 編譯器 () 從命令列進行編譯、 [`csc.exe`](https://msdn.microsoft.com/library/ms379563(vs.80).aspx) 使用 [`CREATE ASSEMBLY`](https://msdn.microsoft.com/library/ms189524.aspx) 命令或從 Management Studio 向資料庫註冊，以及透過類似的方式新增預存程式或 UDF 物件。 幸好 Visual Studio 的 Professional 和 Team 系統版本包含了可將這些工作自動化的 SQL Server 專案類型。 在本教學課程中，我們將逐步解說如何使用 SQL Server 專案類型來建立 managed 預存程式和 UDF。

> [!NOTE]
> 如果您使用的是 Visual Web Developer 或 Standard edition 的 Visual Studio，就必須改用手動方法。 步驟13提供手動執行這些步驟的詳細指示。 在閱讀步驟13之前，建議您先閱讀步驟2到12，因為這些步驟包括重要 SQL Server 設定指示，無論您使用的是哪一個版本的 Visual Studio 都必須套用這些指示。

從開啟 Visual Studio 開始。 在 [檔案] 功能表中，選擇 [新增專案] 以顯示 [新增專案] 對話方塊 (參閱 [圖 4]) 。 向下切入至資料庫專案類型，然後從右側所列的範本中，選擇建立新的 SQL Server 專案。 我選擇將此專案命名為 `ManagedDatabaseConstructs` ，並將其放在名為的方案內 `Tutorial75` 。

[![建立新的 SQL Server 專案](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image6.png)

**圖 4**：建立新的 SQL Server 專案 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image8.png)) 

按一下 [新增專案] 對話方塊中的 [確定] 按鈕，以建立方案和 SQL Server 專案。

SQL Server 專案系結至特定的資料庫。 因此，在建立新的 SQL Server 專案之後，系統會立即要求您指定此資訊。 [圖 5] 顯示新的 [資料庫參考] 對話方塊，該對話方塊已填妥以指向我們在步驟1中的 SQL Server 2005 Express Edition 資料庫實例中註冊的 Northwind 資料庫。

![建立 SQL Server 專案與 Northwind 資料庫的關聯](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image9.png)

**圖 5**：建立 SQL Server 專案與 Northwind 資料庫的關聯

為了將我們將在此專案中建立的 managed 預存程式和 Udf 進行 debug 錯，我們必須啟用連接的 SQL/CLR 偵錯工具支援。 當 SQL Server 專案與新的資料庫建立關聯時， (與我們在 [圖 5] 中所做的) 一樣，Visual Studio 會詢問我們是否要在連接上啟用 SQL/CLR 調試，請參閱 [圖 6] (。 按一下 [是]。

![啟用 SQL/CLR 調試](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image10.png)

**圖 6**：啟用 SQL/CLR 調試

此時，新的 SQL Server 專案已加入至方案中。 它包含名為的資料夾，其中包含名為的檔案 `Test Scripts` `Test.sql` ，可用來偵測在專案中建立的 managed 資料庫物件。 我們將在步驟12中探討如何進行調試。

我們現在可以在這個專案中加入新的 managed 預存程式和 Udf，但是在我們開始之前，先將現有的 web 應用程式包含在解決方案中。 從 [檔案] 功能表選取 [加入] 選項，然後選擇 [現有的網站]。 流覽至適當的網站資料夾，然後按一下 [確定]。 如圖7所示，這會更新方案，以包含兩個專案：網站和 `ManagedDatabaseConstructs` SQL Server 專案。

![方案總管現在包含兩個專案](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image11.png)

**圖 7**：方案總管現在包含兩個專案

`NORTHWNDConnectionString`中的值 `Web.config` 目前會參考 `NORTHWND.MDF` `App_Data` 資料夾中的檔案。 由於我們已從移除此資料庫， `App_Data` 並在 SQL Server 2005 Express Edition 資料庫實例中明確地將它註冊，因此我們必須先更新 `NORTHWNDConnectionString` 該值。 開啟 `Web.config` 網站中的檔案並變更值， `NORTHWNDConnectionString` 使連接字串讀取： `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True` 。 在這項變更之後， `<connectionStrings>` 中的區段 `Web.config` 看起來應該會如下所示：

[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample1.xml)]

> [!NOTE]
> 如 [先前的教學](debugging-stored-procedures-cs.md)課程中所述，從用戶端應用程式（例如 ASP.NET 網站）進行 SQL Server 物件的偵錯工具時，我們需要停用連接共用。 上方顯示的連接字串會停用連接共用 ( `Pooling=false` ) 。 如果您不打算從 ASP.NET 網站調試 managed 預存程式和 Udf，請啟用連接共用。

## <a name="step-3-creating-a-managed-stored-procedure"></a>步驟3：建立 Managed 預存程式

若要將 managed 預存程式加入至 Northwind 資料庫，我們必須先在 SQL Server 專案中建立預存程式做為方法。 在 [方案總管中，以滑鼠右鍵按一下 `ManagedDatabaseConstructs` 專案名稱，然後選擇 [加入新專案]。 這會顯示 [加入新專案] 對話方塊，其中會列出可加入至專案的 managed 資料庫物件類型。 如圖8所示，這包括預存程式和使用者定義函式，還有其他功能。

首先，讓我們加入一個預存程式，只傳回已停止的所有產品。 將新的預存程式檔案命名為 `GetDiscontinuedProducts.cs` 。

[![加入名為 GetDiscontinuedProducts.cs 的新預存程式](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image12.png)

**圖 8**：新增新的預存程式 `GetDiscontinuedProducts.cs` ，名為 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image14.png)) 

這會建立具有下列內容的新 c # 類別檔案：

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample2.cs)]

請注意，預存程式會實作為 `static` 名為之類別檔案內的方法 `partial` `StoredProcedures` 。 此外，此 `GetDiscontinuedProducts` 方法會使用將 `SqlProcedure attribute` 方法標示為預存程式的來裝飾。

下列程式碼會建立 `SqlCommand` 物件，並將其設定 `CommandText` 為 `SELECT` 查詢，該查詢會 `Products` 針對其欄位等於1的產品，從資料表傳回所有資料行 `Discontinued` 。 然後，它會執行命令，並將結果傳回用戶端應用程式。 將此程式碼加入至 `GetDiscontinuedProducts` 方法。

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample3.cs)]

所有的 managed 資料庫物件都具有物件的存取權，該[ `SqlContext` 物件](https://msdn.microsoft.com/library/ms131108.aspx)代表呼叫者的內容。 `SqlContext`可透過其[ `Pipe` 屬性](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx)提供[ `SqlPipe` 物件](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx)的存取權。 此 `SqlPipe` 物件可用來 ferry SQL Server 資料庫與呼叫應用程式之間的資訊。 顧名思義， [ `ExecuteAndSend` 方法](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx)會執行傳入的 `SqlCommand` 物件，並將結果傳回用戶端應用程式。

> [!NOTE]
> 受管理的資料庫物件最適合使用程式邏輯的預存程式和 Udf，而不是以集合為基礎的邏輯。 程式邏輯牽涉到以逐資料列或使用純量資料的方式來處理資料集。 `GetDiscontinuedProducts`不過，我們剛剛建立的方法不包含程式邏輯。 因此，最好是以 T-sql 預存程式的形式來執行。 它會實作為 managed 預存程式，以示範建立和部署 managed 預存程式所需的步驟。

## <a name="step-4-deploying-the-managed-stored-procedure"></a>步驟4：部署 Managed 預存程式

完成此程式碼之後，我們就可以將它部署到 Northwind 資料庫。 部署 SQL Server 專案時，會將程式碼編譯為元件、向資料庫註冊元件，並在資料庫中建立對應的物件，並將它們連結至元件中的適當方法。 在步驟13中，部署選項所執行的一組確切工作會更精確。 `ManagedDatabaseConstructs`在方案總管中，以滑鼠右鍵按一下專案名稱，然後選擇 [部署] 選項。 不過，部署會失敗並出現下列錯誤：「外部」附近的語法不正確。 您可能要將目前資料庫的相容性層級設成高一點的值，以啟用這項功能。 請參閱預存程式的說明 `sp_dbcmptlevel` 。

當您嘗試向 Northwind 資料庫註冊元件時，就會發生這個錯誤訊息。 為了向 SQL Server 2005 資料庫註冊元件，資料庫的相容性層級必須設定為90。 根據預設，新的 SQL Server 2005 資料庫的相容性層級是90。 不過，使用 Microsoft SQL Server 2000 建立的資料庫預設相容性層級是80。 由於 Northwind 資料庫一開始是 Microsoft SQL Server 2000 資料庫，因此它的相容性層級目前設定為80，因此需要增加至90才能註冊受管理的資料庫物件。

若要更新資料庫的相容性層級，請在 Management Studio 中開啟新的查詢視窗，然後輸入：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample4.sql)]

按一下工具列中的 [執行] 圖示，以執行上述查詢。

[![更新 Northwind 資料庫的相容性層級](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image15.png)

**圖 9**：更新 Northwind 資料庫的相容性層級 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image17.png)) 

更新相容性層級之後，重新部署 SQL Server 專案。 這次部署應該會完成，而不會發生錯誤。

返回 [SQL Server Management Studio]，以滑鼠右鍵按一下物件總管中的 Northwind 資料庫，然後選擇 [重新整理]。 接下來，向下切入到 [可程式性] 資料夾，然後展開 [元件] 資料夾。 如圖10所示，Northwind 資料庫現在包含專案所產生的元件 `ManagedDatabaseConstructs` 。

![ManagedDatabaseConstructs 元件現在已向 Northwind 資料庫註冊](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image18.png)

**圖 10**： `ManagedDatabaseConstructs` 元件現在已向 Northwind 資料庫註冊

也請展開 [預存程式] 資料夾。 您會看到一個名為的預存程式 `GetDiscontinuedProducts` 。 這個預存程式是由部署程式所建立，並指向 `GetDiscontinuedProducts` 元件中的方法 `ManagedDatabaseConstructs` 。 `GetDiscontinuedProducts`執行預存程式時，它會接著執行 `GetDiscontinuedProducts` 方法。 因為這是 managed 預存程式，所以無法透過 Management Studio 進行編輯 (因此，預存程式名稱旁邊的鎖定圖示) 。

![GetDiscontinuedProducts 預存程式會列在 [預存程式] 資料夾中。](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image19.png)

**圖 11**： `GetDiscontinuedProducts` 預存程式列在 [預存程式] 資料夾中

在呼叫 managed 預存程式之前，我們必須先克服另外一項障礙：資料庫設定為防止執行 managed 程式碼。 開啟新的查詢視窗並執行預存程式，即可確認此情況 `GetDiscontinuedProducts` 。 您將會收到下列錯誤訊息：已停用 .NET Framework 中的使用者程式碼執行。 啟用 [clr 已啟用] 設定選項。

若要檢查 Northwind 資料庫的設定資訊，請 `exec sp_configure` 在查詢視窗中輸入並執行命令。 這會顯示 [clr 已啟用] 設定目前設定為0。

[![啟用 clr 的設定目前設定為0](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image20.png)

**圖 12**：啟用 Clr 的設定目前設定為 0 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image22.png)) 

請注意，[圖 12] 中的每個設定都有四個列出的值：最小值和最大值，以及設定和執行的值。 若要更新 clr 已啟用設定的設定值，請執行下列命令：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample5.sql)]

如果您重新執行，就 `exec sp_configure` 會看到上述語句將 clr enabled 設定的設定值更新為1，但回合值仍設為0。 為了讓此設定變更生效，我們需要執行[ `RECONFIGURE` 命令](https://msdn.microsoft.com/library/ms176069.aspx)，這會將執行值設定為目前的設定值。 只要 `RECONFIGURE` 在查詢視窗中輸入，然後按一下工具列中的 [執行] 圖示。 如果您現在執行， `exec sp_configure` 您應該會看到已啟用 clr 的設定和執行值的值為1。

啟用 clr 的設定完成之後，就可以開始執行 managed `GetDiscontinuedProducts` 預存程式。 在查詢視窗中，輸入並執行命令 `exec` `GetDiscontinuedProducts` 。 叫用預存程式會導致方法中的對應 managed 程式碼 `GetDiscontinuedProducts` 執行。 這段程式碼 `SELECT` 會發出查詢來傳回所有已停止的產品，並將此資料傳回給呼叫應用程式，這在此實例中 SQL Server Management Studio。 Management Studio 會接收這些結果，並將它們顯示在 [結果] 視窗中。

[![GetDiscontinuedProducts 預存程式會傳回所有已停止的產品](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image23.png)

**圖 13**：預存程式會傳回 `GetDiscontinuedProducts` 所有已停止的產品 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image25.png)) 

## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>步驟5：建立接受輸入參數的 Managed 預存程式

我們在這些教學課程中建立的許多查詢和預存程式都有使用 *參數*。 例如，在建立具 [類型資料集 tableadapter 教學課程的新預存程式](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 中，我們建立了一個名為的預存程式，該預存程式 `GetProductsByCategoryID` 接受名為的輸入參數 `@CategoryID` 。 然後，預存程式會傳回其 `CategoryID` 欄位符合所提供參數值的所有產品 `@CategoryID` 。

若要建立可接受輸入參數的 managed 預存程式，只需在方法的定義中指定這些參數。 為了說明這一點，讓我們將另一個 managed 預存程式新增至 `ManagedDatabaseConstructs` 名為的專案 `GetProductsWithPriceLessThan` 。 此 managed 預存程式會接受指定價格的輸入參數，並傳回其 `UnitPrice` 欄位小於參數 s 值的所有產品。

若要將新的預存程式加入至專案，請以滑鼠右鍵按一下 `ManagedDatabaseConstructs` 專案名稱，然後加入宣告新的預存程式。 將檔案命名為 `GetProductsWithPriceLessThan.cs`。 如我們在步驟3中所見，這將會建立一個新的 c # 類別檔案，其中包含一個名為的方法， `GetProductsWithPriceLessThan` 放在 `partial` 類別中 `StoredProcedures` 。

更新 `GetProductsWithPriceLessThan` 方法的定義，使其接受 [`SqlMoney`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.aspx) 名為的輸入參數 `price` ，並撰寫程式碼以執行並傳回查詢結果：

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample6.cs)]

`GetProductsWithPriceLessThan`方法的定義和程式碼與 `GetDiscontinuedProducts` 在步驟3中建立之方法的定義和程式碼十分類似。 唯一的差異在於此 `GetProductsWithPriceLessThan` 方法會接受 () 的輸入參數 `price` 、 `SqlCommand` s 查詢包含 () 的參數 `@MaxPrice` ，而且會將參數加入至 `SqlCommand` s 集合， `Parameters` 並指派變數的值 `price` 。

新增此程式碼之後，請重新部署 SQL Server 專案。 接下來，返回 SQL Server Management Studio 並重新整理 [預存程式] 資料夾。 您應該會看到新的專案 `GetProductsWithPriceLessThan` 。 從查詢視窗中，輸入並執行命令 `exec GetProductsWithPriceLessThan 25` ，這會列出所有小於 $25 的產品，如圖14所示。

[![顯示 $25 下的產品](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image26.png)

**圖 14**： $25 下的產品會顯示 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image28.png)) 

## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>步驟6：從資料存取層呼叫 Managed 預存程式

至此，我們已將 `GetDiscontinuedProducts` 和 `GetProductsWithPriceLessThan` managed 預存程式新增至 `ManagedDatabaseConstructs` 專案，並已向 Northwind SQL Server 資料庫註冊它們。 我們也從 SQL Server Management Studio 叫用這些 managed 預存程式 (請參閱圖 s 13 和 14) 。 不過，為了讓我們的 ASP.NET 應用程式使用這些 managed 預存程式，我們需要將它們新增至架構中的資料存取和商務邏輯層。 在這個步驟中，我們會在具型別資料集的中加入兩個新方法 `ProductsTableAdapter` `NorthwindWithSprocs` ，這一開始是在為具型別 [資料集 Tableadapter 教學課程建立新的預存程式](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 中建立的。 在步驟7中，我們會將對應的方法新增至 BLL。

`NorthwindWithSprocs`在 Visual Studio 中開啟具類型的資料集，並從將新方法加入至 `ProductsTableAdapter` 名為的開始 `GetDiscontinuedProducts` 。 若要將新的方法加入至 TableAdapter，請在設計工具中以滑鼠右鍵按一下 TableAdapter s 名稱，然後從內容功能表中選擇 [加入查詢] 選項。

> [!NOTE]
> 由於我們已將 Northwind 資料庫從 `App_Data` 資料夾移至 SQL Server 2005 Express Edition 資料庫實例，因此 Web.config 中對應的連接字串必須更新以反映這項變更。 在步驟2中，我們討論了更新 `NORTHWNDConnectionString` 中的值 `Web.config` 。 如果您忘記進行此更新，則會看到錯誤訊息無法加入查詢。 `NORTHWNDConnectionString` `Web.config` 嘗試將新方法加入 TableAdapter 時，找不到對話方塊中物件的連接。 若要解決此錯誤，請按一下 [確定]，然後依 `Web.config` 步驟2所述，移至並更新 `NORTHWNDConnectionString` 值。 然後，嘗試將方法重新新增至 TableAdapter。 這次它應該可以正常運作，而不會發生錯誤。

新增方法會啟動 [TableAdapter 查詢設定向導]，在過去的教學課程中，我們已使用許多次。 第一個步驟會要求我們指定 TableAdapter 應如何存取資料庫：透過臨機操作 SQL 語句，或透過新的或現有的預存程式。 由於我們已經使用資料庫建立並註冊 `GetDiscontinuedProducts` managed 預存程式，因此請選擇 [使用現有的預存程式] 選項，然後按 [下一步]。

[![選擇 [使用現有的預存程式] 選項](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image29.png)

**圖 15**：選擇 [使用現有的預存程式] 選項 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image31.png)) 

下一個畫面會提示我們輸入方法將叫用的預存程式。 `GetDiscontinuedProducts`從下拉式清單中選擇 managed 預存程式，然後按 [下一步]。

[![選取 GetDiscontinuedProducts 受控預存程式](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image32.png)

**圖 16**：選取 `GetDiscontinuedProducts` Managed 預存程式 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image34.png)) 

然後，系統會要求您指定預存程式是要傳回資料列、單一值或 nothing。 由於會傳回一 `GetDiscontinuedProducts` 組已停止的產品資料列，請選擇 ( 表格式資料 ) 的第一個選項，然後按 [下一步]。

[![選取表格式資料選項](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image35.png)

**圖 17**：選取表格式資料選項 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image37.png)) 

最後的 wizard 畫面可讓我們指定所使用的資料存取模式，以及所產生方法的名稱。 將兩個核取方塊保持選取狀態，並將方法命名為 `FillByDiscontinued` 和 `GetDiscontinuedProducts` 。 按一下 [完成] 以完成精靈。

[![將方法命名為 FillByDiscontinued 和 GetDiscontinuedProducts](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image38.png)

**圖 18**：命名方法 `FillByDiscontinued` 並 `GetDiscontinuedProducts` ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image40.png)) 

重複這些步驟， `FillByPriceLessThan` `GetProductsWithPriceLessThan` 在中 `ProductsTableAdapter` 針對 `GetProductsWithPriceLessThan` managed 預存程式建立名為和的方法。

[圖 19] 顯示將的方法加入至的 `ProductsTableAdapter` `GetDiscontinuedProducts` 和 `GetProductsWithPriceLessThan` managed 預存程式之後，資料集設計工具的螢幕擷取畫面。

[![此 ProductsTableAdapter 包含在此步驟中新增的方法](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image41.png)

**圖 19**： `ProductsTableAdapter` 包含這個步驟新增的方法 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image43.png)) 

## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>步驟7：將對應的方法加入至商務邏輯層

既然我們已更新資料存取層，以包含呼叫步驟4和5中所加入之 managed 預存程式的方法，我們必須將對應的方法加入至商務邏輯層。 將下列兩個方法新增至 `ProductsBLLWithSprocs` 類別：

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample7.cs)]

這兩種方法只會呼叫對應的 DAL 方法，並傳回 `ProductsDataTable` 實例。 `DataObjectMethodAttribute`每個方法上方的標記都會讓這些方法包含在 ObjectDataSource 的 [設定資料來源] wizard 的 [選取] 索引標籤中的下拉式清單中。

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>步驟8：從展示層叫用 Managed 預存程式

利用增強的商務邏輯和資料存取層來支援呼叫 `GetDiscontinuedProducts` 和 `GetProductsWithPriceLessThan` managed 預存程式，現在我們可以透過 ASP.NET 網頁顯示這些預存程式的結果。

開啟 `ManagedFunctionsAndSprocs.aspx` 資料夾中的頁面， `AdvancedDAL` 然後從 [工具箱] 將 GridView 拖曳至設計工具。 將 GridView 的 `ID` 屬性設定為 `DiscontinuedProducts` ，並從其智慧標籤將其系結至名為的新 ObjectDataSource `DiscontinuedProductsDataSource` 。 設定 ObjectDataSource 從類別 s 方法提取其資料 `ProductsBLLWithSprocs` `GetDiscontinuedProducts` 。

[![設定 ObjectDataSource 以使用 ProductsBLLWithSprocs 類別](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image44.png)

**圖 20**：設定 ObjectDataSource 以使用 `ProductsBLLWithSprocs` 類別 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image46.png)) 

[![從選取索引標籤的下拉式清單中選擇 [GetDiscontinuedProducts] 方法](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image47.png)

**圖 21**： `GetDiscontinuedProducts` 在 [選取] 索引標籤的下拉式清單中選擇方法 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image49.png)) 

因為這個方格將用來只顯示產品資訊，所以請將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [無] () 然後按一下 [完成]。

完成嚮導之後，Visual Studio 會自動為中的每個資料欄位新增 BoundField 或 CheckBoxField `ProductsDataTable` 。 請花一些時間來移除除了和以外的所有 `ProductName` 欄位 `Discontinued` ，此時您的 GridView 和 ObjectDataSource 宣告式標記看起來應該會如下所示：

[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample8.aspx)]

花點時間透過瀏覽器來觀看此頁面。 造訪頁面時，ObjectDataSource 會呼叫 `ProductsBLLWithSprocs` 類別 s `GetDiscontinuedProducts` 方法。 如我們在步驟7中所見，這個方法會向下呼叫 DAL s `ProductsDataTable` 類別的 `GetDiscontinuedProducts` 方法，此方法會叫用 `GetDiscontinuedProducts` 預存程式。 這個預存程式是 managed 預存程式，會執行我們在步驟3中建立的程式碼，以傳回已停止的產品。

Managed 預存程式所傳回的結果會由 DAL 封裝到中 `ProductsDataTable` ，然後傳回給 BLL，然後將它們傳回至展示層，並將其系結至 GridView 並顯示。 如預期般，方格會列出已停止的產品。

[![已停止的產品會列出](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image50.png)

**圖 22**：已停止的產品會列出 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image52.png)) 

為了進一步練習，請在頁面中新增 TextBox 和另一個 GridView。 讓這個 GridView 藉由呼叫類別 s 方法來顯示小於輸入文字方塊的產品 `ProductsBLLWithSprocs` `GetProductsWithPriceLessThan` 。

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>步驟9：建立和呼叫 T-sql Udf

使用者定義函式（或 Udf）是指在程式設計語言中密切模仿函式之語義的資料庫物件。 如同 c # 中的函式，Udf 可以包含可變數目的輸入參數，並傳回特定類型的值。 UDF 可以傳回純量資料，也就是字串、整數，依此類推或表格式資料。 讓我們快速查看兩種類型的 Udf，從會傳回純量資料類型的 UDF 開始。

下列 UDF 會計算特定產品的清查預估值。 它會採用三個輸入參數（ `UnitPrice` 特定產品的、 `UnitsInStock` 和值），並傳回類型的 `Discontinued` 值 `money` 。 它會藉由將乘以來計算清查的估計值 `UnitPrice` `UnitsInStock` 。 針對已停止的專案，此值會減半。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample9.sql)]

一旦將此 UDF 新增至資料庫之後，就可以藉由展開 [可程式性] 資料夾、函式和純量值函式，在 Management Studio 中找到它。 它可用於 `SELECT` 查詢中，如下所示：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample10.sql)]

我已將 `udf_ComputeInventoryValue` UDF 新增至 Northwind 資料庫;[圖 23] 顯示 `SELECT` 透過 Management Studio 查看上述查詢的輸出。 另請注意，UDF 會列在物件總管的 [純量值函式] 資料夾底下。

[![列出每個產品的清查值](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image53.png)

**圖 23**：每個產品的清查值都列出 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image55.png)) 

Udf 也可以傳回表格式資料。 例如，我們可以建立 UDF 來傳回屬於特定類別的產品：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample11.sql)]

`udf_GetProductsByCategoryID`UDF 接受 `@CategoryID` 輸入參數，並傳回指定之查詢的結果 `SELECT` 。 一旦建立之後，就可以在 `FROM` 查詢的 (或) 子句中參考此 UDF `JOIN` `SELECT` 。 下列範例會傳回 `ProductID` `ProductName` `CategoryID` 每個飲料的、和值。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample12.sql)]

我已將 `udf_GetProductsByCategoryID` UDF 新增至 Northwind 資料庫;圖24顯示 `SELECT` 透過 Management Studio 查看上述查詢的輸出。 傳回表格式資料的 Udf 可以在物件總管的資料表值函數資料夾中找到。

[![每個飲料都會列出 ProductID、ProductName 和類別名稱](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image56.png)

**圖 24**： `ProductID` `ProductName` `CategoryID` 每個飲料都會列出、和， ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image58.png)) 

> [!NOTE]
> 如需有關建立和使用 Udf 的詳細資訊，請參閱 [使用者定義函數的簡介](http://www.sqlteam.com/item.asp?ItemID=1955)。 另外也請查看 [使用者定義函數的優點和缺點](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)。

## <a name="step-10-creating-a-managed-udf"></a>步驟10：建立受控 UDF

`udf_ComputeInventoryValue` `udf_GetProductsByCategoryID` 在上述範例中建立的和 Udf 為 t-sql 資料庫物件。 SQL Server 2005 也支援受控 Udf，可新增至 `ManagedDatabaseConstructs` 專案，就像步驟3和5中的 managed 預存程式一樣。 在這個步驟中，讓我們 `udf_ComputeInventoryValue` 在 managed 程式碼中執行 UDF。

若要將 managed UDF 新增至 `ManagedDatabaseConstructs` 專案，請在方案總管中的專案名稱上按一下滑鼠右鍵，然後加入宣告新專案。 從 [加入新專案] 對話方塊中選取 [使用者定義] 範本，並將新的 UDF 檔案命名為 `udf_ComputeInventoryValue_Managed.cs` 。

[![將新的受控 UDF 新增至 ManagedDatabaseConstructs 專案](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image59.png)

**圖 25**：在專案中加入新的受控 UDF `ManagedDatabaseConstructs` ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image61.png)) 

使用者定義函式範本會建立名為的 `partial` 類別， `UserDefinedFunctions` 其名稱與類別檔案的名稱相同 (`udf_ComputeInventoryValue_Managed` ，在此例中) 。 這個方法會使用屬性裝飾，而此[ `SqlFunction` 屬性](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx)會將方法標示為受管理的 UDF。

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample13.cs)]

`udf_ComputeInventoryValue`方法目前會傳回[ `SqlString` 物件](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx)，但不接受任何輸入參數。 我們需要更新方法定義，讓它接受三個輸入參數- `UnitPrice` 、 `UnitsInStock` 和-， `Discontinued` 並傳回 `SqlMoney` 物件。 計算清查值的邏輯與 T-sql UDF 中的邏輯相同 `udf_ComputeInventoryValue` 。

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample14.cs)]

請注意，UDF 方法的輸入參數是其對應的 SQL 類型： `SqlMoney` 適用于的 `UnitPrice` 欄位、 [`SqlInt16`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx) for 的 `UnitsInStock` 和 [`SqlBoolean`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx) `Discontinued` 。 這些資料類型會反映資料表中定義的類型 `Products` ：資料 `UnitPrice` 行的類型為 `money` 、類型的資料 `UnitsInStock` 行 `smallint` ，以及類型的資料 `Discontinued` 行 `bit` 。

程式碼一開始會先建立 `SqlMoney` 名為 `inventoryValue` 的實例，並將值指派為0。 `Products`資料表允許 `NULL` 和資料行中的資料庫 `UnitsInPrice` 值 `UnitsInStock` 。 因此，我們需要先檢查這些值是否包含 `NULL` s，我們會透過 `SqlMoney` 物件的[ `IsNull` 屬性](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx)來進行。 如果 `UnitPrice` 和都 `UnitsInStock` 包含非 `NULL` 值，則我們 `inventoryValue` 會計算為兩者的乘積。 然後，如果 `Discontinued` 是 true，則會可以藉減半值。

> [!NOTE]
> `SqlMoney`物件只允許將兩個 `SqlMoney` 實例相乘。 它不允許將 `SqlMoney` 實例乘以常值浮點數。 因此，若要可以藉減半， `inventoryValue` 我們會將它乘以值為0.5 的新 `SqlMoney` 實例。

## <a name="step-11-deploying-the-managed-udf"></a>步驟11：部署受控 UDF

現在已建立受控 UDF，我們已準備好將其部署至 Northwind 資料庫。 如我們在步驟4中所見，以滑鼠右鍵按一下方案總管中的專案名稱，然後從內容功能表中選擇 [部署] 選項，即可部署 SQL Server 專案中的 managed 物件。

部署專案之後，請返回 SQL Server Management Studio 並重新整理純量值函式資料夾。 您現在應該會看到兩個專案：

- `dbo.udf_ComputeInventoryValue` -在步驟9中建立的 T-sql UDF，以及
- `dbo.udf ComputeInventoryValue_Managed` -剛部署的步驟10中建立的受控 UDF。

若要測試此受控 UDF，請從 Management Studio 中執行下列查詢：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample15.sql)]

此命令會使用 managed `udf ComputeInventoryValue_Managed` UDF 而非 T-sql `udf_ComputeInventoryValue` UDF，但輸出會相同。 返回 [圖 23] 以查看 UDF 輸出的螢幕擷取畫面。

## <a name="step-12-debugging-the-managed-database-objects"></a>步驟12：調試 Managed 資料庫物件

在 [偵錯工具的偵錯工具](debugging-stored-procedures-cs.md) 教學課程中，我們討論了三個透過 Visual Studio 來進行 SQL Server 的偵錯工具選項：直接資料庫的偵錯工具、應用程式的偵錯工具，以及 SQL Server 專案的偵錯工具 受管理的資料庫物件無法透過直接資料庫的偵錯工具進行調試，但可以從用戶端應用程式和 SQL Server 專案直接進行調試。 不過，若要讓偵錯工具正常運作，SQL Server 2005 資料庫必須允許 SQL/CLR 的偵錯工具。 回想一下，當我們第一次建立 `ManagedDatabaseConstructs` 專案時 Visual Studio 會詢問我們是否要啟用 SQL/CLR 偵錯工具 (請參閱步驟 2) 的圖6。 您可以用滑鼠右鍵按一下伺服器總管視窗中的資料庫，以修改此設定。

![確定資料庫允許 SQL/CLR 偵錯工具](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image62.png)

**圖 26**：確定資料庫允許 SQL/CLR 偵錯工具

假設我們想要對 `GetProductsWithPriceLessThan` managed 預存程式進行 debug。 我們首先會在方法的程式碼內設定中斷點 `GetProductsWithPriceLessThan` 。

[![在 GetProductsWithPriceLessThan 方法中設定中斷點](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image63.png)

**圖 27**：在方法中設定中斷點 `GetProductsWithPriceLessThan` ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image65.png)) 

讓我們先從 SQL Server 專案中查看 managed 資料庫物件的調試。 由於我們的解決方案包含兩個專案（ `ManagedDatabaseConstructs` SQL Server 專案與我們的網站），因此，若要從 SQL Server 專案進行調試，我們必須指示 Visual Studio `ManagedDatabaseConstructs` 在開始進行調試時啟動 SQL Server 專案。 以滑鼠右鍵按一下 `ManagedDatabaseConstructs` 方案總管中的專案，然後從內容功能表中選擇 [設定為啟始專案] 選項。

`ManagedDatabaseConstructs`從偵錯工具啟動專案時，它會執行檔案中的 SQL 語句 `Test.sql` ，該檔案位於 `Test Scripts` 資料夾中。 例如，若要測試 `GetProductsWithPriceLessThan` managed 預存程式，請使用下列語句取代現有的檔案 `Test.sql` 內容，這會叫用 `GetProductsWithPriceLessThan` 傳入14.95 值的 managed 預存程式 `@CategoryID` ：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample16.sql)]

當您輸入上述腳本之後 `Test.sql` ，請前往 [偵錯工具] 功能表並選擇 [開始偵錯工具]，或按下工具列中的 F5 或綠色播放圖示來開始偵錯工具。 這將會在方案中建立專案、將 managed 資料庫物件部署至 Northwind 資料庫，然後執行 `Test.sql` 腳本。 此時，將會叫用中斷點，而我們可以逐步執行 `GetProductsWithPriceLessThan` 方法，檢查輸入參數的值等等。

[![遇到 GetProductsWithPriceLessThan 方法中的中斷點](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image66.png)

**圖 28**：點擊方法中的中斷點 `GetProductsWithPriceLessThan` ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image68.png)) 

為了讓 SQL database 物件可以透過用戶端應用程式進行調試，必須將資料庫設定為支援應用程式的偵錯工具。 以滑鼠右鍵按一下伺服器總管中的資料庫，並確定已核取 [應用程式偵錯工具] 選項。 此外，我們還需要將 ASP.NET 應用程式設定為與 SQL 偵錯工具整合，並停用連接共用。 這些步驟已在 [調試預存程式](debugging-stored-procedures-cs.md) 教學課程的步驟2中詳細討論。

設定 ASP.NET 應用程式和資料庫之後，請將 ASP.NET 網站設定為啟始專案，並開始進行偵錯工具。 如果您造訪的頁面會呼叫其中一個具有中斷點的 managed 物件，應用程式將會停止，並將控制權轉換到偵錯工具，您可以在這裡逐步執行程式碼，如圖28所示。

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>步驟13：手動編譯和部署 Managed 資料庫物件

SQL Server 專案可讓您輕鬆地建立、編譯和部署 managed 資料庫物件。 可惜的是，SQL Server 專案只在 Visual Studio 的 Professional 和 Team Systems 版本中提供。 如果您使用的是 Visual Web Developer 或 Standard Edition 的 Visual Studio，而且想要使用受管理的資料庫物件，您必須手動建立並部署它們。 這包含四個步驟：

1. 建立檔案，其中包含 managed 資料庫物件的原始程式碼。
2. 將物件編譯成元件，
3. 向 SQL Server 2005 資料庫註冊元件，並
4. 在 SQL Server 中建立資料庫物件，以指向元件中的適當方法。

為了說明這些工作，讓我們建立一個新的 managed 預存程式，以傳回其 `UnitPrice` 大於指定值的產品。 在您的電腦上建立名為的新檔案 `GetProductsWithPriceGreaterThan.cs` ，並在檔案中輸入下列程式碼 (您可以使用 Visual Studio、記事本或任何文字編輯器來完成這項) ：

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample17.cs)]

這段程式碼與 `GetProductsWithPriceLessThan` 在步驟5中建立的方法幾乎完全相同。 唯一的差異在於查詢中所使用的方法名稱、 `WHERE` 子句和參數名稱。 回到 `GetProductsWithPriceLessThan` 方法， `WHERE` 子句 read： `WHERE UnitPrice < @MaxPrice` 。 在這裡， `GetProductsWithPriceGreaterThan` 我們會使用： `WHERE UnitPrice > @MinPrice` 。

我們現在需要將此類別編譯為元件。 從命令列，流覽至您儲存檔案的目錄， `GetProductsWithPriceGreaterThan.cs` 並使用 c # 編譯器 (`csc.exe`) 將類別檔案編譯成元件：

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample18.cmd)]

如果 `csc.exe` 不在系統中的資料夾包含 `PATH` ，您將必須完整參考其路徑， `%WINDOWS%\Microsoft.NET\Framework\version\` 如下所示：

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample19.cmd)]

[![將 GetProductsWithPriceGreaterThan.cs 編譯成元件](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image69.png)

**圖 29**：編譯 `GetProductsWithPriceGreaterThan.cs` 成元件 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image71.png)) 

旗標會 `/t` 指定應該將 c # 類別檔案編譯成 DLL (而不是可執行檔) 。 旗標會 `/out` 指定產生的元件名稱。

> [!NOTE]
> `GetProductsWithPriceGreaterThan.cs`您也可以使用[Visual c # Express edition](https://msdn.microsoft.com/vstudio/express/visualcsharp/)或在 Visual Studio Standard Edition 中建立個別的類別庫專案，而不是從命令列編譯類別檔案。 S Jacob Lauritsen 已提供這類 Visual c # Express Edition 專案，其中包含 `GetProductsWithPriceGreaterThan` 預存程式的程式碼，以及在步驟3、5和10中建立的兩個 managed 預存程式和 UDF。 S $ s 專案也包含加入對應的資料庫物件所需的 T-sql 命令。

將程式碼編譯為元件之後，我們就可以在 SQL Server 2005 資料庫內註冊元件。 您可以透過 T-sql、使用命令或 SQL Server Management Studio 來執行此作業 `CREATE ASSEMBLY` 。 讓我們將焦點放在使用 Management Studio。

從 Management Studio 中，展開 Northwind 資料庫中的 [可程式性] 資料夾。 其中一個子資料夾是元件。 若要以手動方式將新元件加入至資料庫，請以滑鼠右鍵按一下 [元件] 資料夾，然後從內容功能表選擇 [新增元件]。 這會顯示 [新增元件] 對話方塊 (請參閱圖 30) 。 按一下 [流覽] 按鈕，選取 `ManuallyCreatedDBObjects.dll` 我們剛剛編譯的元件，然後按一下 [確定]，將元件加入至資料庫。 您 `ManuallyCreatedDBObjects.dll` 在物件總管中看不到元件。

[![將 ManuallyCreatedDBObjects.dll 元件新增至資料庫](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image72.png)

**圖 30**：將 `ManuallyCreatedDBObjects.dll` 元件新增至資料庫 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image74.png)) 

![ManuallyCreatedDBObjects.dll 列在物件總管](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image75.png)

**圖 31**： `ManuallyCreatedDBObjects.dll` 列示于物件總管

雖然我們已將元件新增至 Northwind 資料庫，但我們尚未將預存程式與 `GetProductsWithPriceGreaterThan` 元件中的方法產生關聯。 若要完成此動作，請開啟新的查詢視窗，然後執行下列腳本：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample20.sql)]

這會在名為的 Northwind 資料庫中建立新的預存程式 `GetProductsWithPriceGreaterThan` ，並將它與類別中的 managed 方法 (（位於 `GetProductsWithPriceGreaterThan` `StoredProcedures` 元件) 中）相關聯 `ManuallyCreatedDBObjects` 。

執行上述腳本之後，請重新整理物件總管中的 [預存程式] 資料夾。 您應該會看到新的預存程式專案，其 `GetProductsWithPriceGreaterThan` 旁邊有鎖定圖示。 若要測試此預存程式，請在查詢視窗中輸入並執行下列腳本：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample21.sql)]

如圖32所示，上述命令會顯示大於 $24.95 之產品的資訊 `UnitPrice` 。

[![ManuallyCreatedDBObjects.dll 列在物件總管](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image76.png)

**圖 32**： `ManuallyCreatedDBObjects.dll` 物件總管 ([按一下以查看完整大小的影像](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image78.png)) 

## <a name="summary"></a>摘要

Microsoft SQL Server 2005 提供與 Common Language Runtime (CLR) 的整合，可讓您使用 managed 程式碼來建立資料庫物件。 之前，這些資料庫物件只能使用 T-sql 建立，但現在我們可以使用 c # 之類的 .NET 程式設計語言來建立這些物件。 在本教學課程中，我們建立了兩個 managed 預存程式和一個受管理的使用者定義函數。

Visual Studio 的 SQL Server 專案類型有助於建立、編譯和部署 managed 資料庫物件。 此外，它還提供豐富的調試支援。 不過，SQL Server 的專案類型只適用于 Visual Studio 的 Professional 和 Team Systems 版。 若使用 Visual Web Developer 或 Standard Edition 的 Visual Studio，就必須手動執行建立、編譯和部署步驟，如我們在步驟13中所見。

快樂程式設計！

## <a name="further-reading"></a>深入閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [使用者定義函數的優點和缺點](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [在 Managed 程式碼中建立 SQL Server 2005 物件](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [使用 SQL Server 2005 中的 Managed 程式碼建立觸發程式](http://www.15seconds.com/issue/041006.htm)
- [如何：建立和執行 CLR SQL Server 預存程式](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [如何：建立和執行 CLR SQL Server 使用者定義函數](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [如何：編輯 `Test.sql` 腳本以執行 SQL 物件](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [使用者定義函數簡介](http://www.sqlteam.com/item.asp?ItemID=1955)
- [Managed 程式碼和 SQL Server 2005 (影片) ](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Transact-SQL 參考](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [逐步解說：在 Managed 程式碼中建立預存程式](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者是七個 ASP/ASP. NET 書籍和創辦人 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)，自1998起一直都在使用 Microsoft Web 技術。 Scott 以獨立顧問、訓練員和作者的形式運作。 他的最新書籍是 [*在24小時內 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 您可以在此聯繫[ mitchell@4GuysFromRolla.com 。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog （可在中找到） [http://ScottOnWriting.NET](http://ScottOnWriting.NET) 。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列是由許多有用的審核者所審核。 本教學課程的潛在客戶審核者為 < ren Jacob Lauritsen。 除了複習本文之外，也建立了本文中的 Visual c # Express Edition 專案，以手動編譯 managed 資料庫物件。 有興趣複習我即將推出的 MSDN 文章嗎？ 如果是的話，請在這裡放置一行[ mitchell@4GuysFromRolla.com 。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一個](debugging-stored-procedures-cs.md) 
> [下一步](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
