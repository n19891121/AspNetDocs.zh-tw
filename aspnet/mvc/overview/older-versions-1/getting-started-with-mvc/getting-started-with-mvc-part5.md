---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: 從控制器存取模型的資料 |Microsoft Docs
author: shanselman
description: 這是初學者教學課程中，將會介紹 ASP.NET MVC 的基本概念。 建立簡單的 web 應用程式，從資料庫讀取與寫入。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: e0b540c030bf600def9b9efad4c73f055a343851
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59402826"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="33f6c-104">從控制器存取模型資料</span><span class="sxs-lookup"><span data-stu-id="33f6c-104">Accessing your Model's Data from a Controller</span></span>

<span data-ttu-id="33f6c-105">藉由[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="33f6c-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="33f6c-106">這是初學者教學課程中，將會介紹 ASP.NET MVC 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="33f6c-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="33f6c-107">您將建立簡單 web 應用程式，從資料庫讀取與寫入。</span><span class="sxs-lookup"><span data-stu-id="33f6c-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="33f6c-108">請瀏覽[ASP.NET MVC 學習中心](../../../index.md)來尋找其他 ASP.NET MVC 教學課程和範例。</span><span class="sxs-lookup"><span data-stu-id="33f6c-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="33f6c-109">這一節我們要建立新的 MoviesController 類別，並撰寫一些程式碼會擷取電影資料，並顯示回瀏覽器使用檢視範本。</span><span class="sxs-lookup"><span data-stu-id="33f6c-109">In this section we are going to create a new MoviesController class, and write some code that retrieves our Movie data and displays it back to the browser using a View template.</span></span>

<span data-ttu-id="33f6c-110">以滑鼠右鍵按一下 [控制器] 資料夾，並讓新 MoviesController。</span><span class="sxs-lookup"><span data-stu-id="33f6c-110">Right click on the Controllers folder and make a new MoviesController.</span></span>

<span data-ttu-id="33f6c-111">[![新增控制器](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="33f6c-111">[![Add Controller](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span></span>

<span data-ttu-id="33f6c-112">這會建立新的 「 MoviesController.cs"檔案，我們的專案中我們 \Controllers 資料夾下。</span><span class="sxs-lookup"><span data-stu-id="33f6c-112">This will create a new "MoviesController.cs" file underneath our \Controllers folder within our project.</span></span> <span data-ttu-id="33f6c-113">讓我們更新 MovieController 從我們的新填入資料庫中擷取的電影清單。</span><span class="sxs-lookup"><span data-stu-id="33f6c-113">Let's update the MovieController to retrieve the list of movies from our newly populated database.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

<span data-ttu-id="33f6c-114">因此，我們只會擷取 1984 年的夏季之後發行的影片，我們要執行 LINQ 查詢。</span><span class="sxs-lookup"><span data-stu-id="33f6c-114">We are performing a LINQ query so that we only retrieve movies released after the summer of 1984.</span></span> <span data-ttu-id="33f6c-115">我們將需要呈現的電影傳回這份清單，因此在方法中以滑鼠右鍵按一下並選取新增的檢視，來建立它的檢視範本。</span><span class="sxs-lookup"><span data-stu-id="33f6c-115">We'll need a View template to render this list of movies back, so right-click in the method and select Add View to create it.</span></span>

<span data-ttu-id="33f6c-116">[新增檢視] 對話方塊中我們將指出，我們會將清單傳遞&lt;Movies.Models.Movie&gt;檢視範本。</span><span class="sxs-lookup"><span data-stu-id="33f6c-116">Within the Add View dialog we'll indicate that we are passing a List&lt;Movies.Models.Movie&gt; to our View template.</span></span> <span data-ttu-id="33f6c-117">不同於前一次，我們使用 [新增檢視] 對話方塊，並選擇建立 「 空白 」 範本時，我們會指出這次我們要 Visual Studio 自動"scaffold 」 檢視範本的某些預設的內容。</span><span class="sxs-lookup"><span data-stu-id="33f6c-117">Unlike the previous times we used the Add View dialog and chose to create an "Empty" template, this time we'll indicate that we want Visual Studio to automatically "scaffold" a view template for us with some default content.</span></span> <span data-ttu-id="33f6c-118">將執行此作業，選取 「 清單 」 中的項目 」 檢視內容下拉式功能表。</span><span class="sxs-lookup"><span data-stu-id="33f6c-118">We'll do this by selecting the "List" item within the "View content dropdown menu.</span></span>

<span data-ttu-id="33f6c-119">請記住，如果您已建立新的類別，您必須編譯您的應用程式，它才會顯示在 [新增檢視] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="33f6c-119">Remember, when you have a created a new class you'll need to compile your application for it to show up in the Add View Dialog.</span></span>

![新增檢視](getting-started-with-mvc-part5/_static/image3.png)

<span data-ttu-id="33f6c-121">按一下 [新增]，系統會自動產生的程式碼以檢視我們會顯示我們的電影清單。</span><span class="sxs-lookup"><span data-stu-id="33f6c-121">Click add and the system will automatically generate the code for a View for us that displays our list of movies.</span></span> <span data-ttu-id="33f6c-122">這是要變更的好時機&lt;h2&gt;像我們稍早使用 Hello World 的檢視，標題為類似 「 我的電影清單 」。</span><span class="sxs-lookup"><span data-stu-id="33f6c-122">This is a good time to change the &lt;h2&gt; heading to something like "My Movie List" like we did earlier with the Hello World view.</span></span>

<span data-ttu-id="33f6c-123">[![影片-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="33f6c-123">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span></span>

<span data-ttu-id="33f6c-124">執行您的應用程式，並請 /Movies 瀏覽的網址列中。</span><span class="sxs-lookup"><span data-stu-id="33f6c-124">Run your application and visit /Movies in the address bar.</span></span> <span data-ttu-id="33f6c-125">現在我們使用控制器內的基本查詢從資料庫擷取資料，並回到知道電影的檢視中的資料。</span><span class="sxs-lookup"><span data-stu-id="33f6c-125">Now we've retrieved data from the database using a basic query inside the Controller and returned the data to a View that knows about Movies.</span></span> <span data-ttu-id="33f6c-126">該檢視會透過的電影清單，然後為我們建立資料的資料表。</span><span class="sxs-lookup"><span data-stu-id="33f6c-126">That View then spins through the list of Movies and creates a table of data for us.</span></span>

<span data-ttu-id="33f6c-127">[![電影清單-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="33f6c-127">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span></span>

<span data-ttu-id="33f6c-128">我們將不會實作編輯、 詳細資料和刪除功能，與此應用程式-因此我們不需要預設 scaffold 樣板為我們建立的連結。</span><span class="sxs-lookup"><span data-stu-id="33f6c-128">We won't be implementing Edit, Details and Delete functionality with this application - so we don't need the default links that the scaffold template created for us.</span></span> <span data-ttu-id="33f6c-129">開啟 /Movies/Index.aspx 檔案，並將它們移除。</span><span class="sxs-lookup"><span data-stu-id="33f6c-129">Open up the /Movies/Index.aspx file and remove them.</span></span>

<span data-ttu-id="33f6c-130">以下是我們已更新的檢視範本外觀應該為何我們進行這些變更後的原始程式碼：</span><span class="sxs-lookup"><span data-stu-id="33f6c-130">Here is the source code for what our updated View template should look like once we make these changes:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

<span data-ttu-id="33f6c-131">我們會將其刪除此範例中，它會建立我們就不需要的連結。</span><span class="sxs-lookup"><span data-stu-id="33f6c-131">It's creating links that we won't need, so we'll delete them for this example.</span></span> <span data-ttu-id="33f6c-132">不過，因為這是下一步，我們會保留我們新建立的連結 ！</span><span class="sxs-lookup"><span data-stu-id="33f6c-132">We will keep our Create New link though, as that's next!</span></span> <span data-ttu-id="33f6c-133">以下是我們的應用程式與已移除該資料行的外觀。</span><span class="sxs-lookup"><span data-stu-id="33f6c-133">Here's what our app looks like with that column removed.</span></span>

<span data-ttu-id="33f6c-134">[![電影清單-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="33f6c-134">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span></span>

<span data-ttu-id="33f6c-135">我們現在有簡單的電影資料清單。</span><span class="sxs-lookup"><span data-stu-id="33f6c-135">We now have a simple listing of our movie data.</span></span> <span data-ttu-id="33f6c-136">不過，如果我們按一下 [新建] 連結時，我們將會收到錯誤，因為它不連結 ！</span><span class="sxs-lookup"><span data-stu-id="33f6c-136">However, if we click the "Create New" link, we'll get an error as it's not hooked up!</span></span> <span data-ttu-id="33f6c-137">讓我們實作建立動作方法，並讓使用者在資料庫中，輸入新的電影。</span><span class="sxs-lookup"><span data-stu-id="33f6c-137">Let's implement a Create Action method and enable a user to enter new movies in our database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="33f6c-138">[上一頁](getting-started-with-mvc-part4.md)
> [下一頁](getting-started-with-mvc-part6.md)</span><span class="sxs-lookup"><span data-stu-id="33f6c-138">[Previous](getting-started-with-mvc-part4.md)
[Next](getting-started-with-mvc-part6.md)</span></span>
