---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: 新增模型和控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59405075"
---
# <a name="add-models-and-controllers"></a>新增模型與控制器

藉由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://github.com/MikeWasson/BookService)

在本節中，您將定義的資料庫實體的模型類別。 然後您會加入這些實體執行 CRUD 作業的 Web API 控制器。

## <a name="add-model-classes"></a>新增模型類別

在本教學課程中，我們將使用 Entity Framework (EF) 的 「 程式碼優先 」 方法來建立資料庫。 使用 Code First，您撰寫 C# 類別對應到資料庫資料表，和 EF 會建立資料庫。 (如需詳細資訊，請參閱 < [Entity Framework 開發方式](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf)。)

我們首先定義為 Poco （單純 CLR 物件） 的網域物件。 我們將建立下列 Poco:

- 作者
- 活頁簿

在 [方案總管] 中，以滑鼠右鍵按一下 [模型] 資料夾。 選取 **新增**，然後選取**類別**。 將類別命名為 `Author` 。

![](part-2/_static/image1.png)

所有 Author.cs 的未定案程式碼取代下列程式碼。

[!code-csharp[Main](part-2/samples/sample1.cs)]

新增另一個類別，名為`Book`，為下列程式碼。

[!code-csharp[Main](part-2/samples/sample2.cs)]

Entity Framework 會使用這些模型來建立資料庫資料表。 針對每個模型，`Id`屬性就會成為資料庫資料表的主索引鍵資料行。

在活頁簿類別中，`AuthorId`定義外部索引鍵`Author`資料表。 （為了簡單起見，我假設每個活頁簿有單一的作者。）Book 類別也包含對相關的導覽屬性`Author`。 您可以使用導覽屬性存取相關`Author`在程式碼中。 我加入更多導覽屬性，在第 4 部分[處理實體關聯性](part-4.md)。

## <a name="add-web-api-controllers"></a>新增 Web API 控制器

在本節中，我們將新增 Web API 控制器支援 CRUD 作業 （建立、 讀取、 更新和刪除）。 控制器會使用 Entity Framework 與資料庫層級進行通訊。

首先，您可以刪除 Controllers/ValuesController.cs 的檔案。 此檔案包含的範例 Web API 控制器，但您不在本教學課程中需要它。

![](part-2/_static/image2.png)

接下來，建置專案。 Web API scaffolding 會使用反映來尋找模型類別，因此它需要編譯的組件。

在 [方案總管] 中，以滑鼠右鍵按一下 [控制器] 資料夾。 選取 **新增**，然後選取**控制站**。

![](part-2/_static/image3.png)

在 **新增 Scaffold**對話方塊中，選取"Web API 2 控制器會執行動作，使用 Entity Framework 」。 按一下 [加入] 。

![](part-2/_static/image4.png)

在 [**新增控制器**] 對話方塊中，執行下列動作：

1. 在 **模型類別**下拉式清單中，選取`Author`類別。 （如果您沒有看到它列在下拉式清單中，請確定您建置專案。）
2. 請檢查 [使用非同步控制器動作]。
3. 將控制器名稱，作為&quot;AuthorsController&quot;。
4. 按一下加號 （+） 按鈕旁**資料內容類別**。

![](part-2/_static/image5.png)

在 [**新的資料內容**] 對話方塊中，保留預設名稱，然後按一下**新增**。

![](part-2/_static/image6.png)

按一下 **新增**才能完成**新增控制器**對話方塊。 對話方塊會將兩個類別新增至您的專案：

- `AuthorsController` 定義 Web API 控制器。 控制器會實作 REST API 用戶端用來執行的作者清單上的 CRUD 作業。
- `BookServiceContext` 在執行階段，其中包含填入物件，包含來自資料庫、 變更追蹤和資料保存到資料庫管理實體的物件。 它繼承自`DbContext`。

![](part-2/_static/image7.png)

到目前為止，再次建置專案。 現在，移到相同的步驟來新增此 API 控制器會針對`Book`實體。 這次請選取`Book`模型類別，然後選取現有`BookServiceContext`資料內容類別的類別。 （不建立新的資料內容）。按一下 **新增**加入控制器。

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> [上一頁](part-1.md)
> [下一頁](part-3.md)
