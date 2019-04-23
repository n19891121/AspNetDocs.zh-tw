---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: 將新的項目加入至資料庫 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 692269a2c11e529af78f24feca74bba704b5b54b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59415150"
---
# <a name="add-a-new-item-to-the-database"></a><span data-ttu-id="34851-102">將新項目新增至資料庫</span><span class="sxs-lookup"><span data-stu-id="34851-102">Add a New Item to the Database</span></span>

<span data-ttu-id="34851-103">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="34851-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="34851-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="34851-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="34851-105">在本節中，您將加入可讓使用者建立新的書籍。</span><span class="sxs-lookup"><span data-stu-id="34851-105">In this section, you will add the ability for users to create a new book.</span></span> <span data-ttu-id="34851-106">在 app.js 中加入檢視模型中的下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="34851-106">In app.js, add the following code to the view model:</span></span>

[!code-javascript[Main](part-9/samples/sample1.js)]

<span data-ttu-id="34851-107">在 Index.cshtml 中，將下列標記：</span><span class="sxs-lookup"><span data-stu-id="34851-107">In Index.cshtml, replace the following markup:</span></span>

[!code-html[Main](part-9/samples/sample2.html)]

<span data-ttu-id="34851-108">成為：</span><span class="sxs-lookup"><span data-stu-id="34851-108">With:</span></span>

[!code-html[Main](part-9/samples/sample3.html)]

<span data-ttu-id="34851-109">此標記會建立的表單提交新的作者。</span><span class="sxs-lookup"><span data-stu-id="34851-109">This markup creates a form for submitting a new author.</span></span> <span data-ttu-id="34851-110">[作者] 下拉式清單的值是資料繫結至`authors`可觀察的檢視模型中。</span><span class="sxs-lookup"><span data-stu-id="34851-110">The values for the author drop-down list are data-bound to the `authors` observable in the view model.</span></span> <span data-ttu-id="34851-111">其他表單輸入的值是資料繫結至`newBook`檢視模型的屬性。</span><span class="sxs-lookup"><span data-stu-id="34851-111">For the other form inputs, the values are data-bound to the `newBook` property of the view model.</span></span>

<span data-ttu-id="34851-112">提交處理常式，在表單上的繫結至`addBook`函式：</span><span class="sxs-lookup"><span data-stu-id="34851-112">The submit handler on the form is bound to the `addBook` function:</span></span>

[!code-html[Main](part-9/samples/sample4.html)]

<span data-ttu-id="34851-113">`addBook`函式會讀取所需資料繫結表單的輸入建立的 JSON 物件的目前值。</span><span class="sxs-lookup"><span data-stu-id="34851-113">The `addBook` function reads the current values of the data-bound form inputs to create a JSON object.</span></span> <span data-ttu-id="34851-114">然後它會張貼的 JSON 物件`/api/books`。</span><span class="sxs-lookup"><span data-stu-id="34851-114">Then it POSTs the JSON object to `/api/books`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="34851-115">[上一頁](part-8.md)
> [下一頁](part-10.md)</span><span class="sxs-lookup"><span data-stu-id="34851-115">[Previous](part-8.md)
[Next](part-10.md)</span></span>
