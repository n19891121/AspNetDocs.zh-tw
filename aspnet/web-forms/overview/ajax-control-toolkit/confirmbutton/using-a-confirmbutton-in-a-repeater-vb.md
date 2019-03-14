---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
title: (Vb) 中使用 ConfirmButton |Microsoft Docs
author: wenz
description: 在 AJAX Control Toolkit ConfirmButton 擴充項會建立 是/當使用者按一下按鈕上的任何快顯 （包含 LinkButton 控制項）。 只有當是...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 18c31709-3f9d-4d93-8b01-f1356bf610b4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: 38ac40776c2fdd14af046b5e13df0701c71a4ad0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044315"
---
<a name="using-a-confirmbutton-in-a-repeater-vb"></a>在重複項中使用 ConfirmButton (VB)
====================
藉由[Christian Wenz](https://github.com/wenz)

[下載程式碼](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip)或[下載 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)

> 在 AJAX Control Toolkit ConfirmButton 擴充項會建立 是/當使用者按一下按鈕上的任何快顯 （包含 LinkButton 控制項）。 只是按一下時，如果按鈕的執行動作，否則已取消。 這也是可能的重複項中。


## <a name="overview"></a>總覽

在 AJAX Control Toolkit ConfirmButton 擴充項會建立 是/當使用者按一下按鈕上的任何快顯 （包含 LinkButton 控制項）。 只是按一下時，如果按鈕的執行動作，否則已取消。 這也是可能的重複項中。

## <a name="steps"></a>步驟

首先，資料來源是必要的。 此範例使用 AdventureWorks 資料庫和 Microsoft SQL Server 2005 Express Edition。 資料庫 （包括 express edition） 的 Visual Studio 安裝的選擇性部分作業，因此也會提供個別下載底下[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。 AdventureWorks 資料庫是 SQL Server 2005 範例和範例資料庫的一部分 (下載網址[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。 若要設定資料庫的最簡單方式是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))，並將附加`AdventureWorks.mdf`資料庫檔案。

此範例中，我們假設 SQL Server 2005 Express Edition 的執行個體，會呼叫`SQLEXPRESS`位於與網頁伺服器; 相同的電腦上，這也是預設設定。 如果您的設定不同，您必須調整資料庫的連接資訊。

若要啟動的 ASP.NET AJAX Control Toolkit 中，功能`ScriptManager`控制項必須放置在任何位置上 (但在`<form>`項目):

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample1.aspx)]

然後，資料來源是必要的。 為了簡單起見，會擷取僅 AdventureWorks 的供應商資料表的前五個項目。 請注意，當使用 Visual Studio 精靈來建立資料來源時，資料表名稱 (`Vendors`) 目前未正確前面會加上`Purchasing`。 下列標記正確：

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample2.aspx)]

此資料來源可用內設有重複項。 像往常一樣，`DataBinder.Eval()`方法會從資料來源擷取資料。 `ConfirmButtonExtender`控制項則必須放在`<ItemTemplate>`區段的重複項，使它顯示的資料來源中的每個項目。

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample3.aspx)]


[![從資料來源的每個項目旁邊的 [確認] 按鈕會出現](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)

從資料來源的每個項目旁邊的 [確認] 按鈕會出現 ([按一下以檢視完整大小的影像](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一步](using-a-confirmbutton-in-a-repeater-cs.md)
