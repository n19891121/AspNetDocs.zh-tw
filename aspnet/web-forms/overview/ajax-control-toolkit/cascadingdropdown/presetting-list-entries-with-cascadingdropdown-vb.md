---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
title: Cascadingdropdown 預設清單項目與 CascadingDropDown (VB) |Microsoft Docs
author: wenz
description: 在 AJAX Control Toolkit CascadingDropDown 控制擴充 DropDownList 控制項以讓一個 DropDownList 載入中的變更相關聯 anoth 中的值...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec61ced7-bbca-4bdd-aa3b-80878f295181
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 6e685d599e3dbc095631e3c28a603ac9c38f799c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59385887"
---
# <a name="presetting-list-entries-with-cascadingdropdown-vb"></a>使用 CascadingDropDown 預設清單項目 (VB)

藉由[Christian Wenz](https://github.com/wenz)

[下載程式碼](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip)或[下載 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)

> 在 AJAX Control Toolkit CascadingDropDown 控制擴充 DropDownList 控制項以讓一個 DropDownList 載入中的變更相關聯的另一個 DropDownList 中的值。 加上一些程式碼就可以，以動態方式載入資料之後，已預先選取的清單項目。


## <a name="overview"></a>總覽

在 AJAX Control Toolkit CascadingDropDown 控制擴充 DropDownList 控制項以讓一個 DropDownList 載入中的變更相關聯的另一個 DropDownList 中的值。 （比方說，一份清單會提供一份我們狀態，而且下一個清單則填入該狀態中主要城市）。加上一些程式碼就可以，以動態方式載入資料之後，已預先選取的清單項目。

## <a name="steps"></a>步驟

若要啟動的 ASP.NET AJAX Control Toolkit 中，功能`ScriptManager`控制項必須放置在任何位置上 (但在`<form>`項目):

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample1.aspx)]

DropDownList 控制項則需要：

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample2.aspx)]

此清單中，會加入 CascadingDropDown 擴充項，提供 web 服務 URL 和方法資訊：

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample3.aspx)]

CascadingDropDown extender 接著會以非同步方式呼叫 web 服務的下列方法簽章：

[!code-vb[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample4.vb)]

方法會傳回類型 CascadingDropDown 值的陣列。 類型的建構函式必須要有先清單項目的標題，然後此值 (HTML`value`屬性)。 如果第三個引數設定為 true，清單項目會自動選取瀏覽器中。

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample5.aspx)]

載入瀏覽器頁面，將會填滿下拉式清單中的，使用三個廠商，第二個要預先選取。


[![T他清單是填滿，並預先選取 [自動](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)

清單會填入，且會自動預先選取 ([按一下以檢視完整大小的影像](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一頁](using-cascadingdropdown-with-a-database-vb.md)
> [下一頁](using-auto-postback-with-cascadingdropdown-vb.md)
