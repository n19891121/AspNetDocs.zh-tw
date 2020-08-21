---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: 動態與 強型別視圖 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 30b84c71c86e455f15a659abf566750f1c6eea90
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702942"
---
# <a name="dynamic-v-strongly-typed-views"></a>動態與 強型別檢視

依 [Rick Anderson](https://twitter.com/RickAndMSFT)

有三種方式可將資訊從控制器傳遞至 ASP.NET MVC 3 中的觀點：

1. 做為強型別模型物件。
2. 作為動態類型 (使用 @model 動態) 
3. 使用 ViewBag

我撰寫了簡單的 MVC 3 熱門 Blog 應用程式，以比較和對比動態和強型別的觀點。 控制器會從簡單的 blog 清單開始：

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

以滑鼠右鍵按一下 IndexNotStonglyTyped ( # A1 方法，並新增 Razor view。

[![8475. NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

請確定未核取 [ **建立強型** 別] 視圖框。 產生的視圖不包含太多：

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

由於我們使用的是動態的，而不是強型別視圖，因此 intellisense 不會協助我們。 完成的程式碼如下所示：

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6646. NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

現在我們要新增強型別視圖。 將下列程式碼新增至控制器：

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

請注意， (topBlogs) ;以非強型別視圖的形式呼叫。 以滑鼠右鍵按一下 *StonglyTypedIndex ( # B1 * 內，然後選取 [ **加入視圖**]。 這次請選取 [ **Blog** ] 模型類別，然後選取 [ **清單** ] 作為 Scaffold 範本。

[![5658. StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

在新的 view 範本中，我們會取得 intellisense 支援。

[![7002。 IntelliSense [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)
