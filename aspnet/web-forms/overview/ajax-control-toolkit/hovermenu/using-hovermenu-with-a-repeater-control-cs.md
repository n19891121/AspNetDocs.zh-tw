---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: 使用 HoverMenu 與重複項控制項 (C#) |Microsoft Docs
author: wenz
description: 在 AJAX Control Toolkit HoverMenu 控制項提供簡單的快顯效果：當滑鼠指標停留在項目，快顯視窗會出現在 specifi...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 7f64e90eb2f8f87e2f382cb7897793e7071d305d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59384496"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a><span data-ttu-id="f6877-103">使用 HoverMenu 與重複項控制項 (C#)</span><span class="sxs-lookup"><span data-stu-id="f6877-103">Using HoverMenu with a Repeater Control (C#)</span></span>

<span data-ttu-id="f6877-104">藉由[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f6877-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f6877-105">[下載程式碼](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip)或[下載 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f6877-105">[Download Code](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span></span>

> <span data-ttu-id="f6877-106">在 AJAX Control Toolkit HoverMenu 控制項提供簡單的快顯效果：當滑鼠指標停留在項目上方時，則會在指定的位置出現快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="f6877-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="f6877-107">它也可使用這個控制項內的重複項。</span><span class="sxs-lookup"><span data-stu-id="f6877-107">It is also possible to use this control within a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="f6877-108">總覽</span><span class="sxs-lookup"><span data-stu-id="f6877-108">Overview</span></span>

<span data-ttu-id="f6877-109">`HoverMenu` AJAX Control Toolkit 中的控制項提供簡單的快顯效果：當滑鼠指標停留在項目上方時，則會在指定的位置出現快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="f6877-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="f6877-110">它也可使用這個控制項內的重複項。</span><span class="sxs-lookup"><span data-stu-id="f6877-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="f6877-111">步驟</span><span class="sxs-lookup"><span data-stu-id="f6877-111">Steps</span></span>

<span data-ttu-id="f6877-112">首先，資料來源是必要的。</span><span class="sxs-lookup"><span data-stu-id="f6877-112">First of all, a data source is required.</span></span> <span data-ttu-id="f6877-113">此範例使用 AdventureWorks 資料庫和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="f6877-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="f6877-114">資料庫 （包括 express edition） 的 Visual Studio 安裝的選擇性部分作業，因此也會提供個別下載底下[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。</span><span class="sxs-lookup"><span data-stu-id="f6877-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="f6877-115">AdventureWorks 資料庫是 SQL Server 2005 範例和範例資料庫的一部分 (下載網址[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。</span><span class="sxs-lookup"><span data-stu-id="f6877-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="f6877-116">若要設定資料庫的最簡單方式是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))，並將附加`AdventureWorks.mdf`資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="f6877-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="f6877-117">此範例中，我們假設 SQL Server 2005 Express Edition 的執行個體，會呼叫`SQLEXPRESS`位於與網頁伺服器; 相同的電腦上，這也是預設設定。</span><span class="sxs-lookup"><span data-stu-id="f6877-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="f6877-118">如果您的設定不同，您必須調整資料庫的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="f6877-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="f6877-119">若要啟動的 ASP.NET AJAX Control Toolkit 中，功能`ScriptManager`控制項必須放置在任何位置上 (但在`<form>`項目):</span><span class="sxs-lookup"><span data-stu-id="f6877-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="f6877-120">然後，新增至頁面的資料來源。</span><span class="sxs-lookup"><span data-stu-id="f6877-120">Then, add a data source to the page.</span></span> <span data-ttu-id="f6877-121">若要使用的資料數量有限，我們只選取前五個項目在 Vendor 資料表的 AdventureWorks 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="f6877-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="f6877-122">如果您使用 Visual Studio 助理員來建立資料來源，請記住目前的版本中的錯誤不前置的資料表名稱 (`Vendor`) 與`Purchasing`。</span><span class="sxs-lookup"><span data-stu-id="f6877-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="f6877-123">下列標記會顯示正確的語法：</span><span class="sxs-lookup"><span data-stu-id="f6877-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="f6877-124">接下來，新增一個面板作為強制回應快顯視窗：</span><span class="sxs-lookup"><span data-stu-id="f6877-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="f6877-125">現在，`HoverMenuExtender`派上用場。</span><span class="sxs-lookup"><span data-stu-id="f6877-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="f6877-126">擴充項，讓資料來源中的每個項目取得自己的快顯視窗，必須將 repeater 內`<ItemTemplate>`一節。</span><span class="sxs-lookup"><span data-stu-id="f6877-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="f6877-127">標記如下：</span><span class="sxs-lookup"><span data-stu-id="f6877-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="f6877-128">現在的右邊資料來源中的每個項目顯示快顯視窗 (`PopupPosition`屬性) 的 50 毫秒的延遲之後 (`PopDelay`屬性)。</span><span class="sxs-lookup"><span data-stu-id="f6877-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>


[![T<span data-ttu-id="f6877-129">他暫留功能表顯示中繼器中每個項目旁邊]</span><span class="sxs-lookup"><span data-stu-id="f6877-129">he hover menu appears next to each item in the repeater]</span></span>(using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)

<span data-ttu-id="f6877-130">中繼器中每個項目旁邊會出現的停留功能表 ([按一下以檢視完整大小的影像](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f6877-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f6877-131">下一步</span><span class="sxs-lookup"><span data-stu-id="f6877-131">Next</span></span>](using-hovermenu-with-a-repeater-control-vb.md)
