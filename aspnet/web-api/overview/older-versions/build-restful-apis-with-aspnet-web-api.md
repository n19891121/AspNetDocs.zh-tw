---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: 建置 RESTful Api，使用 ASP.NET Web API-ASP.NET 4.x
author: rick-anderson
description: 實習實驗室：使用 Web API 中 ASP.NET 4.x 建置簡單的 REST API 連絡人管理員應用程式。
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3ba7f2d186e6f0837a32f69f964cec19fe625953
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59391477"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a><span data-ttu-id="48484-103">建置使用 ASP.NET Web API 的 RESTful Api</span><span class="sxs-lookup"><span data-stu-id="48484-103">Build RESTful APIs with ASP.NET Web API</span></span>

<span data-ttu-id="48484-104">藉由[Web Camp 小組](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="48484-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="48484-105">實習實驗室：使用 Web API 中 ASP.NET 4.x 建置簡單的 REST API 連絡人管理員應用程式。</span><span class="sxs-lookup"><span data-stu-id="48484-105">Hands on lab: Use Web API in ASP.NET 4.x to build a simple REST API for a contact manager application.</span></span> <span data-ttu-id="48484-106">您也將建置的用戶端取用 API。</span><span class="sxs-lookup"><span data-stu-id="48484-106">You will also build a client to consume the API.</span></span>

<span data-ttu-id="48484-107">近年來，它具有一目了然，HTTP 不只是提供 HTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="48484-107">In recent years, it has become clear that HTTP is not just for serving up HTML pages.</span></span> <span data-ttu-id="48484-108">它也是強大的平台，建置 Web Api，使用少數幾個動詞 （GET、 POST 等） 再加上幾個簡單的概念，例如*Uri*並*標頭*。</span><span class="sxs-lookup"><span data-stu-id="48484-108">It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as *URIs* and *headers*.</span></span> <span data-ttu-id="48484-109">ASP.NET Web API 是一組簡化 HTTP 程式設計的元件。</span><span class="sxs-lookup"><span data-stu-id="48484-109">ASP.NET Web API is a set of components that simplify HTTP programming.</span></span> <span data-ttu-id="48484-110">由於它建置在 ASP.NET MVC 執行階段上，Web API 會自動處理 HTTP 傳輸低階詳細資料。</span><span class="sxs-lookup"><span data-stu-id="48484-110">Because it is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP.</span></span> <span data-ttu-id="48484-111">在此同時，Web API，自然地公開 HTTP 程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="48484-111">At the same time, Web API naturally exposes the HTTP programming model.</span></span> <span data-ttu-id="48484-112">事實上，Web API 的其中一個目標是要*不*摘除 HTTP 的事實。</span><span class="sxs-lookup"><span data-stu-id="48484-112">In fact, one goal of Web API is to *not* abstract away the reality of HTTP.</span></span> <span data-ttu-id="48484-113">如此一來，Web API 是彈性且容易擴充。</span><span class="sxs-lookup"><span data-stu-id="48484-113">As a result, Web API is both flexible and easy to extend.</span></span>  <span data-ttu-id="48484-114">事實證明的 REST 架構樣式會運用 HTTP-的有效方法，但是它當然不是 HTTP 的唯一有效方法。</span><span class="sxs-lookup"><span data-stu-id="48484-114">The REST architectural style has proven to be an effective way to leverage HTTP - although it is certainly not the only valid approach to HTTP.</span></span> <span data-ttu-id="48484-115">連絡人的管理員會公開清單、 加入和移除連絡人，以及其他符合 rest 限制。</span><span class="sxs-lookup"><span data-stu-id="48484-115">The contact manager will expose the RESTful for listing, adding and removing contacts, among others.</span></span> 

<span data-ttu-id="48484-116">這個實驗室需要基本 HTTP，其餘部分，了解，並假設您有基本的 HTML、 JavaScript 和 jQuery 的實用知識。</span><span class="sxs-lookup"><span data-stu-id="48484-116">This lab requires a basic understanding of HTTP, REST, and assumes you have a basic working knowledge of HTML, JavaScript, and jQuery.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="48484-117">ASP.NET 網站有一個專門用來在 ASP.NET Web API 架構的區域[ https://asp.net/web-api ](https://asp.net/web-api)。</span><span class="sxs-lookup"><span data-stu-id="48484-117">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [https://asp.net/web-api](https://asp.net/web-api).</span></span> <span data-ttu-id="48484-118">此站台將持續提供最新的資訊、 範例和新聞與 Web API，因此請經常如果您想要更深入地鑽研建立給幾乎任何裝置或開發架構，可用的自訂 Web Api 的圖案。</span><span class="sxs-lookup"><span data-stu-id="48484-118">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>
> > 
> > <span data-ttu-id="48484-119">ASP.NET Web API，類似於 ASP.NET MVC 4 中，有很大的彈性方面開來，讓您可以使用數個可用的相依性插入架構相當簡單的控制站的服務層。</span><span class="sxs-lookup"><span data-stu-id="48484-119">ASP.NET Web API, similar to ASP.NET MVC 4, has great flexibility in terms of separating the service layer from the controllers allowing you to use several of the available Dependency Injection frameworks fairly easy.</span></span> <span data-ttu-id="48484-120">示範如何使用 Ninject 相依性插入，您可以下載從 ASP.NET Web API 專案中的 MSDN 中沒有良好的樣本[此處](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)。</span><span class="sxs-lookup"><span data-stu-id="48484-120">There is a good sample in MSDN that shows how to use Ninject for dependency injection in an ASP.NET Web API project that you can download it from [here](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span></span>
> 
> 
> <span data-ttu-id="48484-121">所有的範例程式碼和程式碼片段會包含在 Web 研討會訓練套件，可在[ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="48484-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>


<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="48484-122">目標</span><span class="sxs-lookup"><span data-stu-id="48484-122">Objectives</span></span>

<span data-ttu-id="48484-123">在這個實際操作實驗室中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="48484-123">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="48484-124">實作 RESTful Web API</span><span class="sxs-lookup"><span data-stu-id="48484-124">Implement a RESTful Web API</span></span>
- <span data-ttu-id="48484-125">從 HTML 用戶端呼叫 API</span><span class="sxs-lookup"><span data-stu-id="48484-125">Call the API from an HTML client</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="48484-126">必要條件</span><span class="sxs-lookup"><span data-stu-id="48484-126">Prerequisites</span></span>

<span data-ttu-id="48484-127">需要下列項目才能完成這個實際操作實驗室：</span><span class="sxs-lookup"><span data-stu-id="48484-127">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="48484-128">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更好 (讀取[附錄 B](#AppendixB)如需有關如何安裝它)。</span><span class="sxs-lookup"><span data-stu-id="48484-128">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="48484-129">安裝程式</span><span class="sxs-lookup"><span data-stu-id="48484-129">Setup</span></span>

<span data-ttu-id="48484-130">**安裝程式碼片段**</span><span class="sxs-lookup"><span data-stu-id="48484-130">**Installing Code Snippets**</span></span>

<span data-ttu-id="48484-131">為了方便起見，大部分的程式碼，您將沿著這個實驗室管理可從 Visual Studio 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="48484-131">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="48484-132">若要安裝執行的程式碼片段 **.\Source\Setup\CodeSnippets.vsi**檔案。</span><span class="sxs-lookup"><span data-stu-id="48484-132">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="48484-133">如果您不熟悉 Visual Studio 程式碼片段，而且想要了解如何使用它們，您可以從這份文件參考附錄&quot;[附錄 a:使用程式碼片段](#AppendixA)&quot;。</span><span class="sxs-lookup"><span data-stu-id="48484-133">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="48484-134">練習</span><span class="sxs-lookup"><span data-stu-id="48484-134">Exercises</span></span>

<span data-ttu-id="48484-135">這個實際操作實驗室還包含下列練習：</span><span class="sxs-lookup"><span data-stu-id="48484-135">This hands-on lab includes the following exercise:</span></span>

1. [<span data-ttu-id="48484-136">練習 1:建立唯讀的 Web API</span><span class="sxs-lookup"><span data-stu-id="48484-136">Exercise 1: Create a Read-Only Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="48484-137">練習 2:建立讀取/寫入 Web API</span><span class="sxs-lookup"><span data-stu-id="48484-137">Exercise 2: Create a Read/Write Web API</span></span>](#Exercise2)
3. [<span data-ttu-id="48484-138">練習 3:使用 HTML 用戶端從 Web API</span><span class="sxs-lookup"><span data-stu-id="48484-138">Exercise 3: Consume the Web API from an HTML Client</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="48484-139">每個練習會伴隨**結束**包含完成練習之後，您應該取得所產生的方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="48484-139">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="48484-140">如果您需要的所有練習所使用的其他說明，您可以使用此解決方案作為指南。</span><span class="sxs-lookup"><span data-stu-id="48484-140">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="48484-141">估計的時間才能完成這個實驗室：**60 分鐘**。</span><span class="sxs-lookup"><span data-stu-id="48484-141">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a><span data-ttu-id="48484-142">練習 1:建立唯讀的 Web API</span><span class="sxs-lookup"><span data-stu-id="48484-142">Exercise 1: Create a Read-Only Web API</span></span>

<span data-ttu-id="48484-143">在此練習中，您將連絡人的 manager 實作的唯寫的 GET 方法。</span><span class="sxs-lookup"><span data-stu-id="48484-143">In this exercise, you will implement the read-only GET methods for the contact manager.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a><span data-ttu-id="48484-144">工作 1-建立 API 專案</span><span class="sxs-lookup"><span data-stu-id="48484-144">Task 1 - Creating the API Project</span></span>

<span data-ttu-id="48484-145">在這個工作中，您將使用新的 ASP.NET web 專案範本建立 Web API 的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="48484-145">In this task, you will use the new ASP.NET web project templates to create a Web API web application.</span></span>

1. <span data-ttu-id="48484-146">執行**Visual Studio 2012 Express for Web**，以前往**開始**然後輸入**VS Express for Web**然後按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="48484-146">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="48484-147">從**檔案**功能表上，選取**新的專案**。</span><span class="sxs-lookup"><span data-stu-id="48484-147">From the **File** menu, select **New Project**.</span></span> <span data-ttu-id="48484-148">選取**Visual C# |Web**專案類型從 專案類型樹狀檢視中，然後選取**ASP.NET MVC 4 Web 應用程式**專案類型。</span><span class="sxs-lookup"><span data-stu-id="48484-148">Select the **Visual C# | Web** project type from the project type tree view, then select the **ASP.NET MVC 4 Web Application** project type.</span></span> <span data-ttu-id="48484-149">將此專案的**名稱**要*ContactManager*和**方案名稱**至*開始*，然後按一下 **確定**.</span><span class="sxs-lookup"><span data-stu-id="48484-149">Set the project's **Name** to *ContactManager* and the **Solution name** to *Begin*, then click **OK**.</span></span>

    <span data-ttu-id="48484-150">![建立新的 ASP.NET MVC 4.0 Web 應用程式專案](build-restful-apis-with-aspnet-web-api/_static/image1.png "建立新的 ASP.NET MVC 4.0 Web 應用程式專案")</span><span class="sxs-lookup"><span data-stu-id="48484-150">![Creating a new ASP.NET MVC 4.0 Web Application Project](build-restful-apis-with-aspnet-web-api/_static/image1.png "Creating a new ASP.NET MVC 4.0 Web Application Project")</span></span>

    <span data-ttu-id="48484-151">*建立新的 ASP.NET MVC 4.0 Web 應用程式專案*</span><span class="sxs-lookup"><span data-stu-id="48484-151">*Creating a new ASP.NET MVC 4.0 Web Application Project*</span></span>
3. <span data-ttu-id="48484-152">在 ASP.NET MVC 4 專案的 [類型] 對話方塊中，選取**Web API**專案類型。</span><span class="sxs-lookup"><span data-stu-id="48484-152">In the ASP.NET MVC 4 project type dialog, select the **Web API** project type.</span></span> <span data-ttu-id="48484-153">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="48484-153">Click **OK**.</span></span>

    <span data-ttu-id="48484-154">![指定的 Web API 專案型別](build-restful-apis-with-aspnet-web-api/_static/image2.png "指定 Web API 專案類型")</span><span class="sxs-lookup"><span data-stu-id="48484-154">![Specifying the Web API project type](build-restful-apis-with-aspnet-web-api/_static/image2.png "Specifying the Web API project type")</span></span>

    <span data-ttu-id="48484-155">*指定 Web API 專案類型*</span><span class="sxs-lookup"><span data-stu-id="48484-155">*Specifying the Web API project type*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a><span data-ttu-id="48484-156">工作 2-建立連絡人管理員 API 控制器</span><span class="sxs-lookup"><span data-stu-id="48484-156">Task 2 - Creating the Contact Manager API Controllers</span></span>

<span data-ttu-id="48484-157">在這個工作中，您將建立的 API 方法所在的控制器類別。</span><span class="sxs-lookup"><span data-stu-id="48484-157">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="48484-158">刪除名為的檔案**ValuesController.cs**內**控制站**從專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="48484-158">Delete the file named **ValuesController.cs** within **Controllers** folder from the project.</span></span>
2. <span data-ttu-id="48484-159">以滑鼠右鍵按一下**控制器**資料夾中的專案，然後選取**新增 |控制器**從內容功能表。</span><span class="sxs-lookup"><span data-stu-id="48484-159">Right-click the **Controllers** folder in the project and select **Add | Controller** from the context menu.</span></span>

    <span data-ttu-id="48484-160">![將新的控制站新增至專案](build-restful-apis-with-aspnet-web-api/_static/image3.png "專案中加入新的控制站")</span><span class="sxs-lookup"><span data-stu-id="48484-160">![Adding a new controller to the project](build-restful-apis-with-aspnet-web-api/_static/image3.png "Adding a new controller to the project")</span></span>

    <span data-ttu-id="48484-161">*將新的控制站新增至專案*</span><span class="sxs-lookup"><span data-stu-id="48484-161">*Adding a new controller to the project*</span></span>
3. <span data-ttu-id="48484-162">在 **新增控制器**出現對話方塊中，選取**空白 API 控制器**從 範本 功能表。</span><span class="sxs-lookup"><span data-stu-id="48484-162">In the **Add Controller** dialog that appears, select **Empty API Controller** from the Template menu.</span></span> <span data-ttu-id="48484-163">將類別命名為控制器**ContactController**。</span><span class="sxs-lookup"><span data-stu-id="48484-163">Name the controller class **ContactController**.</span></span> <span data-ttu-id="48484-164">然後，按一下 **新增。**</span><span class="sxs-lookup"><span data-stu-id="48484-164">Then, click **Add.**</span></span>

    <span data-ttu-id="48484-165">![使用 [新增控制器] 對話方塊來建立新的 Web API 控制器](build-restful-apis-with-aspnet-web-api/_static/image4.png "使用 [新增控制器] 對話方塊來建立新的 Web API 控制器")</span><span class="sxs-lookup"><span data-stu-id="48484-165">![Using the Add Controller dialog to create a new Web API controller](build-restful-apis-with-aspnet-web-api/_static/image4.png "Using the Add Controller dialog to create a new Web API controller")</span></span>

    <span data-ttu-id="48484-166">*使用 [新增控制器] 對話方塊來建立新的 Web API 控制器*</span><span class="sxs-lookup"><span data-stu-id="48484-166">*Using the Add Controller dialog to create a new Web API controller*</span></span>
4. <span data-ttu-id="48484-167">將下列程式碼加入**ContactController**。</span><span class="sxs-lookup"><span data-stu-id="48484-167">Add the following code to the **ContactController**.</span></span>

    <span data-ttu-id="48484-168">(程式碼片段- *Web API 實驗室-Ex01-Get API 方法*)</span><span class="sxs-lookup"><span data-stu-id="48484-168">(Code Snippet - *Web API Lab - Ex01 - Get API Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. <span data-ttu-id="48484-169">按下**F5**偵錯應用程式。</span><span class="sxs-lookup"><span data-stu-id="48484-169">Press **F5** to debug the application.</span></span> <span data-ttu-id="48484-170">預設的首頁上，為 Web API 專案應該會出現。</span><span class="sxs-lookup"><span data-stu-id="48484-170">The default home page for a Web API project should appear.</span></span>

    <span data-ttu-id="48484-171">![ASP.NET Web API 應用程式的預設首頁](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API 應用程式的預設首頁")</span><span class="sxs-lookup"><span data-stu-id="48484-171">![The default home page of an ASP.NET Web API application](build-restful-apis-with-aspnet-web-api/_static/image5.png "The default home page of an ASP.NET Web API application")</span></span>

    <span data-ttu-id="48484-172">*ASP.NET Web API 應用程式的預設首頁*</span><span class="sxs-lookup"><span data-stu-id="48484-172">*The default home page of an ASP.NET Web API application*</span></span>
6. <span data-ttu-id="48484-173">在 [Internet Explorer] 視窗中，按下**F12**鍵以開啟**開發人員工具**視窗。</span><span class="sxs-lookup"><span data-stu-id="48484-173">In the Internet Explorer window, press the **F12** key to open the **Developer Tools** window.</span></span> <span data-ttu-id="48484-174">按一下 **網路**索引標籤，然後再按一下**開始擷取**按鈕，開始擷取網路流量到視窗。</span><span class="sxs-lookup"><span data-stu-id="48484-174">Click the **Network** tab, and then click the **Start Capturing** button to begin capturing network traffic into the window.</span></span>

    <span data-ttu-id="48484-175">![開啟 [網路] 索引標籤，然後啟動網路擷取](build-restful-apis-with-aspnet-web-api/_static/image6.png "開啟 [網路] 索引標籤，然後啟動網路擷取")</span><span class="sxs-lookup"><span data-stu-id="48484-175">![Opening the network tab and initiating network capture](build-restful-apis-with-aspnet-web-api/_static/image6.png "Opening the network tab and initiating network capture")</span></span>

    <span data-ttu-id="48484-176">*開啟 [網路] 索引標籤，然後啟動網路擷取*</span><span class="sxs-lookup"><span data-stu-id="48484-176">*Opening the network tab and initiating network capture*</span></span>
7. <span data-ttu-id="48484-177">附加與瀏覽器的網址列中的 URL **/api/contact** ，然後按 enter。</span><span class="sxs-lookup"><span data-stu-id="48484-177">Append the URL in the browser's address bar with **/api/contact** and press enter.</span></span> <span data-ttu-id="48484-178">傳輸的詳細資料會出現在網路的 [擷取] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="48484-178">The transmission details will appear in the network capture window.</span></span> <span data-ttu-id="48484-179">請注意，回應的 MIME 類型，則**application/json**。</span><span class="sxs-lookup"><span data-stu-id="48484-179">Note that the response's MIME type is **application/json**.</span></span> <span data-ttu-id="48484-180">這示範了如何的預設輸出格式為 JSON。</span><span class="sxs-lookup"><span data-stu-id="48484-180">This demonstrates how the default output format is JSON.</span></span>

    <span data-ttu-id="48484-181">![在 [網路] 檢視中檢視 Web API 要求的輸出](build-restful-apis-with-aspnet-web-api/_static/image7.png "檢視在 [網路] 檢視中的 Web API 要求的輸出")</span><span class="sxs-lookup"><span data-stu-id="48484-181">![Viewing the output of the Web API request in the Network view](build-restful-apis-with-aspnet-web-api/_static/image7.png "Viewing the output of the Web API request in the Network view")</span></span>

    <span data-ttu-id="48484-182">*在 [網路] 檢視中檢視 Web API 要求的輸出*</span><span class="sxs-lookup"><span data-stu-id="48484-182">*Viewing the output of the Web API request in the Network view*</span></span>

    > [!NOTE]
    > <span data-ttu-id="48484-183">此時 Internet Explorer 10 的預設行為將會詢問使用者想要儲存或開啟 Web API 呼叫所產生的資料流。</span><span class="sxs-lookup"><span data-stu-id="48484-183">Internet Explorer 10's default behavior at this point will be to ask if the user would like to save or open the stream resulting from the Web API call.</span></span> <span data-ttu-id="48484-184">輸出會包含 Web API URL 呼叫的 JSON 結果的文字檔。</span><span class="sxs-lookup"><span data-stu-id="48484-184">The output will be a text file containing the JSON result of the Web API URL call.</span></span> <span data-ttu-id="48484-185">不要取消對話方塊，才能夠觀賞回應的內容，透過開發人員工具視窗。</span><span class="sxs-lookup"><span data-stu-id="48484-185">Do not cancel the dialog in order to be able to watch the response's content through Developers Tool window.</span></span>
8. <span data-ttu-id="48484-186">按一下 **前往 詳細檢視**以查看有關此 API 呼叫的回應詳細資料 按鈕。</span><span class="sxs-lookup"><span data-stu-id="48484-186">Click the **Go to detailed view** button to see more details about the response of this API call.</span></span>

    <span data-ttu-id="48484-187">![切換至 詳細檢視](build-restful-apis-with-aspnet-web-api/_static/image8.png "切換至 詳細資料檢視")</span><span class="sxs-lookup"><span data-stu-id="48484-187">![Switch to Detailed View](build-restful-apis-with-aspnet-web-api/_static/image8.png "Switch to Details View")</span></span>

    <span data-ttu-id="48484-188">*切換至 詳細檢視*</span><span class="sxs-lookup"><span data-stu-id="48484-188">*Switch to Detailed View*</span></span>
9. <span data-ttu-id="48484-189">按一下 [**回應主體**若要檢視實際的 JSON 回應文字] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="48484-189">Click the **Response body** tab to view the actual JSON response text.</span></span>

    <span data-ttu-id="48484-190">![檢視 JSON 輸出網路監視器中的文字](build-restful-apis-with-aspnet-web-api/_static/image9.png "檢視 JSON 輸出網路監視器中的文字")</span><span class="sxs-lookup"><span data-stu-id="48484-190">![Viewing the JSON output text in the network monitor](build-restful-apis-with-aspnet-web-api/_static/image9.png "Viewing the JSON output text in the network monitor")</span></span>

    <span data-ttu-id="48484-191">*在 網路監視器中檢視 JSON 輸出文字*</span><span class="sxs-lookup"><span data-stu-id="48484-191">*Viewing the JSON output text in the network monitor*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a><span data-ttu-id="48484-192">工作 3-建立連絡人的模型，以及增強的連絡人的控制站</span><span class="sxs-lookup"><span data-stu-id="48484-192">Task 3 - Creating the Contact Models and Augment the Contact Controller</span></span>

<span data-ttu-id="48484-193">在這個工作中，您將建立的 API 方法所在的控制器類別。</span><span class="sxs-lookup"><span data-stu-id="48484-193">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="48484-194">以滑鼠右鍵按一下**模型**資料夾，然後選取**新增 |類別...** 從內容功能表。</span><span class="sxs-lookup"><span data-stu-id="48484-194">Right-click the **Models** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="48484-195">![將新模型加入至 web 應用程式](build-restful-apis-with-aspnet-web-api/_static/image10.png "將新模型加入至 web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="48484-195">![Adding a new model to the web application](build-restful-apis-with-aspnet-web-api/_static/image10.png "Adding a new model to the web application")</span></span>

    <span data-ttu-id="48484-196">*將新模型加入至 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="48484-196">*Adding a new model to the web application*</span></span>
2. <span data-ttu-id="48484-197">在 [**加入新項目**] 對話方塊中，將新檔案命名**Contact.cs**按一下**新增。**</span><span class="sxs-lookup"><span data-stu-id="48484-197">In the **Add New Item** dialog, name the new file **Contact.cs** and click **Add.**</span></span>

    <span data-ttu-id="48484-198">![建立新的連絡人類別檔案](build-restful-apis-with-aspnet-web-api/_static/image11.png "建立新的連絡人類別檔案")</span><span class="sxs-lookup"><span data-stu-id="48484-198">![Creating the new Contact class file](build-restful-apis-with-aspnet-web-api/_static/image11.png "Creating the new Contact class file")</span></span>

    <span data-ttu-id="48484-199">*建立新的連絡人類別檔案*</span><span class="sxs-lookup"><span data-stu-id="48484-199">*Creating the new Contact class file*</span></span>
3. <span data-ttu-id="48484-200">將下列反白顯示的程式碼，加入**連絡人**類別。</span><span class="sxs-lookup"><span data-stu-id="48484-200">Add the following highlighted code to the **Contact** class.</span></span>

    <span data-ttu-id="48484-201">(程式碼片段- *Web API 實驗室-Ex01-連絡類別*)</span><span class="sxs-lookup"><span data-stu-id="48484-201">(Code Snippet - *Web API Lab - Ex01 - Contact Class*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. <span data-ttu-id="48484-202">在  **ContactController**類別中，選取 word**字串**方法定義中**取得**方法，並輸入文字*連絡人*。</span><span class="sxs-lookup"><span data-stu-id="48484-202">In the **ContactController** class, select the word **string** in method definition of the **Get** method, and type the word *Contact*.</span></span> <span data-ttu-id="48484-203">一旦這個字型別中，指標就會出現在單字開頭**連絡人**。</span><span class="sxs-lookup"><span data-stu-id="48484-203">Once the word is typed in, an indicator will appear at the beginning of the word **Contact**.</span></span> <span data-ttu-id="48484-204">請按住**Ctrl**鍵並按下句號 （.） 索引鍵或按一下圖示以開啟 設定在程式碼編輯器中，會自動填入的 協助 對話方塊中使用滑鼠**使用**模型指示詞命名空間。</span><span class="sxs-lookup"><span data-stu-id="48484-204">Either hold down the **Ctrl** key and press the period (.) key or click the icon using your mouse to open up the assistance dialog in the code editor, to automatically fill in the **using** directive for the Models namespace.</span></span>

    ![為命名空間宣告中使用 Intellisense 協助](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    <span data-ttu-id="48484-206">*為命名空間宣告中使用 Intellisense 協助*</span><span class="sxs-lookup"><span data-stu-id="48484-206">*Using Intellisense assistance for namespace declarations*</span></span>
5. <span data-ttu-id="48484-207">修改程式碼**取得**方法，讓它傳回連絡人模型執行個體陣列。</span><span class="sxs-lookup"><span data-stu-id="48484-207">Modify the code for the **Get** method so that it returns an array of Contact model instances.</span></span>

    <span data-ttu-id="48484-208">(程式碼片段-*傳回的連絡人清單 Web API 實驗室-Ex01-*)</span><span class="sxs-lookup"><span data-stu-id="48484-208">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. <span data-ttu-id="48484-209">按下**F5**偵錯 web 應用程式，在瀏覽器中的。</span><span class="sxs-lookup"><span data-stu-id="48484-209">Press **F5** to debug the web application in the browser.</span></span> <span data-ttu-id="48484-210">若要檢視對 API 的回應輸出的變更，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="48484-210">To view the changes made to the response output of the API, perform the following steps.</span></span>

   1. <span data-ttu-id="48484-211">瀏覽器開啟後，請按下**F12**如果開發人員工具還不開啟。</span><span class="sxs-lookup"><span data-stu-id="48484-211">Once the browser opens, press **F12** if the developer tools are not open yet.</span></span>
   2. <span data-ttu-id="48484-212">按一下 [**網路**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="48484-212">Click the **Network** tab.</span></span>
   3. <span data-ttu-id="48484-213">按下**開始擷取** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="48484-213">Press the **Start Capturing** button.</span></span>
   4. <span data-ttu-id="48484-214">新增 URL 尾碼 **/api/contact** url 網址列，然後按下**Enter**索引鍵。</span><span class="sxs-lookup"><span data-stu-id="48484-214">Add the URL suffix **/api/contact** to the URL in the address bar and press the **Enter** key.</span></span>
   5. <span data-ttu-id="48484-215">按下**前往 [詳細檢視**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="48484-215">Press the **Go to detailed view** button.</span></span>
   6. <span data-ttu-id="48484-216">選取 [**回應主體**] 索引標籤。您應該會看到 JSON 字串，代表序列化的形式的連絡執行個體陣列。</span><span class="sxs-lookup"><span data-stu-id="48484-216">Select the **Response body** tab. You should see a JSON string representing the serialized form of an array of Contact instances.</span></span>

      <span data-ttu-id="48484-217">![JSON 序列化的複雜的 Web API 方法呼叫的輸出](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON 序列化的複雜的 Web API 方法呼叫的輸出")</span><span class="sxs-lookup"><span data-stu-id="48484-217">![JSON serialized output of a complex Web API method call](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON serialized output of a complex Web API method call")</span></span>

      <span data-ttu-id="48484-218">*複雜的 Web API 方法呼叫的序列化的 JSON 輸出*</span><span class="sxs-lookup"><span data-stu-id="48484-218">*JSON serialized output of a complex Web API method call*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a><span data-ttu-id="48484-219">工作 4-解壓縮到服務層的功能</span><span class="sxs-lookup"><span data-stu-id="48484-219">Task 4 - Extracting Functionality into a Service Layer</span></span>

<span data-ttu-id="48484-220">這項工作中將示範如何擷取到的服務層，讓您輕鬆將其服務的功能分開控制站的圖層，藉此讓人重複使用之服務的實際執行工作的開發人員的功能。</span><span class="sxs-lookup"><span data-stu-id="48484-220">This task will demonstrate how to extract functionality into a Service layer to make it easy for developers to separate their service functionality from the controller layer, thereby allowing reusability of the services that actually do the work.</span></span>

1. <span data-ttu-id="48484-221">在方案根目錄中建立新的資料夾並將它命名**Services**。</span><span class="sxs-lookup"><span data-stu-id="48484-221">Create a new folder in the solution root and name it **Services**.</span></span> <span data-ttu-id="48484-222">若要這樣做，請以滑鼠右鍵按一下**ContactManager**專案，然後選取**新增** | **新資料夾**，其命名*服務*。</span><span class="sxs-lookup"><span data-stu-id="48484-222">To do this, right-click **ContactManager** project, select **Add** | **New Folder**, name it *Services*.</span></span>

    <span data-ttu-id="48484-223">![建立服務 資料夾](build-restful-apis-with-aspnet-web-api/_static/image14.png "建立服務資料夾")</span><span class="sxs-lookup"><span data-stu-id="48484-223">![Creating Services folder](build-restful-apis-with-aspnet-web-api/_static/image14.png "Creating Services folder")</span></span>

    <span data-ttu-id="48484-224">*建立服務 資料夾*</span><span class="sxs-lookup"><span data-stu-id="48484-224">*Creating Services folder*</span></span>
2. <span data-ttu-id="48484-225">以滑鼠右鍵按一下**Services**資料夾，然後選取**新增 |類別...** 從內容功能表。</span><span class="sxs-lookup"><span data-stu-id="48484-225">Right-click the **Services** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="48484-226">![將新類別新增至 [服務] 資料夾](build-restful-apis-with-aspnet-web-api/_static/image15.png "將新類別新增至 [服務] 資料夾")</span><span class="sxs-lookup"><span data-stu-id="48484-226">![Adding a new class to the Services folder](build-restful-apis-with-aspnet-web-api/_static/image15.png "Adding a new class to the Services folder")</span></span>

    <span data-ttu-id="48484-227">*將新類別新增至 [服務] 資料夾*</span><span class="sxs-lookup"><span data-stu-id="48484-227">*Adding a new class to the Services folder*</span></span>
3. <span data-ttu-id="48484-228">當**加入新項目**對話方塊隨即出現，新類別命名**ContactRepository**然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="48484-228">When the **Add New Item** dialog appears, name the new class **ContactRepository** and click **Add**.</span></span>

    <span data-ttu-id="48484-229">![建立類別檔案，以包含連絡人儲存機制的服務層的程式碼](build-restful-apis-with-aspnet-web-api/_static/image16.png "建立類別檔案，以包含連絡人儲存機制的服務層的程式碼")</span><span class="sxs-lookup"><span data-stu-id="48484-229">![Creating a class file to contain the code for the Contact Repository service layer](build-restful-apis-with-aspnet-web-api/_static/image16.png "Creating a class file to contain the code for the Contact Repository service layer")</span></span>

    <span data-ttu-id="48484-230">*建立類別檔案，以包含連絡人儲存機制的服務層的程式碼*</span><span class="sxs-lookup"><span data-stu-id="48484-230">*Creating a class file to contain the code for the Contact Repository service layer*</span></span>
4. <span data-ttu-id="48484-231">新增 using 指示詞**ContactRepository.cs**檔案，以包含模型命名空間。</span><span class="sxs-lookup"><span data-stu-id="48484-231">Add a using directive to the **ContactRepository.cs** file to include the models namespace.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. <span data-ttu-id="48484-232">將下列反白顯示的程式碼，加入**ContactRepository.cs**檔案以實作 GetAllContacts 方法。</span><span class="sxs-lookup"><span data-stu-id="48484-232">Add the following highlighted code to the **ContactRepository.cs** file to implement GetAllContacts method.</span></span>

    <span data-ttu-id="48484-233">(程式碼片段- *Web API 實驗室-Ex01-連絡人儲存機制*)</span><span class="sxs-lookup"><span data-stu-id="48484-233">(Code Snippet - *Web API Lab - Ex01 - Contact Repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. <span data-ttu-id="48484-234">開啟**ContactController.cs**檔案如果它尚未開啟。</span><span class="sxs-lookup"><span data-stu-id="48484-234">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="48484-235">新增下列 using 陳述式之檔案的命名空間宣告一節。</span><span class="sxs-lookup"><span data-stu-id="48484-235">Add the following using statement to the namespace declaration section of the file.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. <span data-ttu-id="48484-236">將下列反白顯示的程式碼，加入**ContactController.cs**新增私用欄位來代表儲存機制的執行個體，以便成員可以建立的類別的其餘部分使用的服務實作的類別。</span><span class="sxs-lookup"><span data-stu-id="48484-236">Add the following highlighted code to the **ContactController.cs** class to add a private field to represent the instance of the repository, so that the rest of the class members can make use of the service implementation.</span></span>

    <span data-ttu-id="48484-237">(程式碼片段-*的 Web API 實驗室-Ex01-連絡人控制器*)</span><span class="sxs-lookup"><span data-stu-id="48484-237">(Code Snippet - *Web API Lab - Ex01 - Contact Controller*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. <span data-ttu-id="48484-238">變更**取得**方法，讓它可讓使用連絡人儲存機制的服務。</span><span class="sxs-lookup"><span data-stu-id="48484-238">Change the **Get** method so that it makes use of the contact repository service.</span></span>

    <span data-ttu-id="48484-239">(程式碼片段-*透過儲存機制中傳回的連絡人清單 Web API 實驗室-Ex01-*)</span><span class="sxs-lookup"><span data-stu-id="48484-239">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts via the repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. <span data-ttu-id="48484-240">將中斷點放**ContactController**的**取得**方法定義。</span><span class="sxs-lookup"><span data-stu-id="48484-240">Put a breakpoint on the **ContactController**'s **Get** method definition.</span></span>

   <span data-ttu-id="48484-241">![將中斷點新增至連絡人控制器](build-restful-apis-with-aspnet-web-api/_static/image17.png "將中斷點新增至連絡人控制器")</span><span class="sxs-lookup"><span data-stu-id="48484-241">![Adding breakpoints to the contact controller](build-restful-apis-with-aspnet-web-api/_static/image17.png "Adding breakpoints to the contact controller")</span></span>

   <span data-ttu-id="48484-242">*將中斷點新增至連絡人控制器*</span><span class="sxs-lookup"><span data-stu-id="48484-242">*Adding breakpoints to the contact controller*</span></span>
11. <span data-ttu-id="48484-243">按 **F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="48484-243">Press **F5** to run the application.</span></span>
12. <span data-ttu-id="48484-244">當瀏覽器會開啟時，請按**F12**以開啟 開發人員工具。</span><span class="sxs-lookup"><span data-stu-id="48484-244">When the browser opens, press **F12** to open the developer tools.</span></span>
13. <span data-ttu-id="48484-245">按一下 [**網路**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="48484-245">Click the **Network** tab.</span></span>
14. <span data-ttu-id="48484-246">按一下 [**開始擷取**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="48484-246">Click the **Start Capturing** button.</span></span>
15. <span data-ttu-id="48484-247">附加後置詞的 [網址] 列中的 URL **/api/contact**然後按**Enter**載入 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="48484-247">Append the URL in the address bar with the suffix **/api/contact** and press **Enter** to load the API controller.</span></span>
16. <span data-ttu-id="48484-248">Visual Studio 2012 應該一次中斷**取得**方法開始執行。</span><span class="sxs-lookup"><span data-stu-id="48484-248">Visual Studio 2012 should break once **Get** method begins execution.</span></span>

   <span data-ttu-id="48484-249">![在 Get 方法中的重大](build-restful-apis-with-aspnet-web-api/_static/image18.png "中斷在 Get 方法")</span><span class="sxs-lookup"><span data-stu-id="48484-249">![Breaking within the Get method](build-restful-apis-with-aspnet-web-api/_static/image18.png "Breaking within the Get method")</span></span>

   <span data-ttu-id="48484-250">*在 Get 方法中的重大*</span><span class="sxs-lookup"><span data-stu-id="48484-250">*Breaking within the Get method*</span></span>
17. <span data-ttu-id="48484-251">按 **F5** 繼續。</span><span class="sxs-lookup"><span data-stu-id="48484-251">Press **F5** to continue.</span></span>
18. <span data-ttu-id="48484-252">回到 Internet Explorer 如果它尚未在成為焦點。</span><span class="sxs-lookup"><span data-stu-id="48484-252">Go back to Internet Explorer if it is not already in focus.</span></span> <span data-ttu-id="48484-253">請注意網路的 [擷取] 視窗。</span><span class="sxs-lookup"><span data-stu-id="48484-253">Note the network capture window.</span></span>

    <span data-ttu-id="48484-254">![網路在 Internet Explorer 中顯示的 Web API 呼叫結果的檢視](build-restful-apis-with-aspnet-web-api/_static/image19.png "網路在 Internet Explorer 中顯示的 Web API 呼叫結果的檢視")</span><span class="sxs-lookup"><span data-stu-id="48484-254">![Network view in Internet Explorer showing results of the Web API call](build-restful-apis-with-aspnet-web-api/_static/image19.png "Network view in Internet Explorer showing results of the Web API call")</span></span>

    <span data-ttu-id="48484-255">*在 Internet Explorer 中顯示的 Web API 呼叫結果的 [網路] 檢視*</span><span class="sxs-lookup"><span data-stu-id="48484-255">*Network view in Internet Explorer showing results of the Web API call*</span></span>
19. <span data-ttu-id="48484-256">按一下 **前往 詳細檢視** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="48484-256">Click the **Go to detailed view** button.</span></span>
20. <span data-ttu-id="48484-257">按一下 [**回應主體**] 索引標籤。請注意 JSON 輸出的 API，以及它如何表示兩個服務層所擷取的連絡人。</span><span class="sxs-lookup"><span data-stu-id="48484-257">Click the **Response body** tab. Note the JSON output of the API call, and how it represents the two contacts retrieved by the service layer.</span></span>

    <span data-ttu-id="48484-258">![開發人員工具 視窗中檢視 Web API 的 JSON 輸出](build-restful-apis-with-aspnet-web-api/_static/image20.png "開發人員工具 視窗中檢視 Web API 的 JSON 輸出")</span><span class="sxs-lookup"><span data-stu-id="48484-258">![Viewing the JSON output from the Web API in the developer tools window](build-restful-apis-with-aspnet-web-api/_static/image20.png "Viewing the JSON output from the Web API in the developer tools window")</span></span>

    <span data-ttu-id="48484-259">*開發人員工具 視窗中檢視 Web API 的 JSON 輸出*</span><span class="sxs-lookup"><span data-stu-id="48484-259">*Viewing the JSON output from the Web API in the developer tools window*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a><span data-ttu-id="48484-260">練習 2:建立讀取/寫入 Web API</span><span class="sxs-lookup"><span data-stu-id="48484-260">Exercise 2: Create a Read/Write Web API</span></span>

<span data-ttu-id="48484-261">在此練習中，您會將實作 POST 和 PUT 方法的連絡人管理員 」 來啟用資料編輯功能。</span><span class="sxs-lookup"><span data-stu-id="48484-261">In this exercise, you will implement POST and PUT methods for the contact manager to enable it with data-editing features.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a><span data-ttu-id="48484-262">工作 1-開啟 Web API 專案</span><span class="sxs-lookup"><span data-stu-id="48484-262">Task 1 - Opening the Web API Project</span></span>

<span data-ttu-id="48484-263">在這個工作中，您會準備增強，因此可以接受使用者輸入，在練習 1 中建立的 Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="48484-263">In this task, you will prepare to enhance the Web API project created in Exercise 1 so that it can accept user input.</span></span>

1. <span data-ttu-id="48484-264">執行**Visual Studio 2012 Express for Web**，以前往**開始**然後輸入**VS Express for Web**然後按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="48484-264">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="48484-265">開啟**開始**解決方案位於**來源/Ex02-ReadWriteWebAPI/開始/** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="48484-265">Open the **Begin** solution located at **Source/Ex02-ReadWriteWebAPI/Begin/** folder.</span></span> <span data-ttu-id="48484-266">否則，您可能會繼續使用**結束**方案取得完成前一個練習。</span><span class="sxs-lookup"><span data-stu-id="48484-266">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="48484-267">如果您開啟提供**開始**解決方案中，您必須下載某些缺少的 NuGet 封裝才能繼續。</span><span class="sxs-lookup"><span data-stu-id="48484-267">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="48484-268">若要這樣做，請按一下**專案**功能表，然後選取**管理 NuGet 套件**。</span><span class="sxs-lookup"><span data-stu-id="48484-268">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="48484-269">在 [**管理 NuGet 套件**] 對話方塊中，按一下**還原**才能下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="48484-269">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="48484-270">最後，按一下 建置方案**建置** | **建置方案**。</span><span class="sxs-lookup"><span data-stu-id="48484-270">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="48484-271">使用 NuGet 的優點之一是，您不需要寄送您的專案中的所有程式庫專案縮小。</span><span class="sxs-lookup"><span data-stu-id="48484-271">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="48484-272">NuGet Power tools，藉由指定封裝版本在 Packages.config 檔案中，您將能夠下載所有必要的程式庫第一次執行專案。</span><span class="sxs-lookup"><span data-stu-id="48484-272">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="48484-273">這就是為什麼您必須在您開啟現有的方案從這個實驗室之後，執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="48484-273">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="48484-274">開啟**Services/ContactRepository.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="48484-274">Open the **Services/ContactRepository.cs** file.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a><span data-ttu-id="48484-275">工作 2-加入連絡人儲存機制實作的資料持續性功能</span><span class="sxs-lookup"><span data-stu-id="48484-275">Task 2 - Adding Data-Persistence Features to the Contact Repository Implementation</span></span>

<span data-ttu-id="48484-276">在這個工作中，您將會擴大 ContactRepository 的類別，使其可以保存，並接受使用者輸入和新的連絡人執行個體，在練習 1 中建立的 Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="48484-276">In this task, you will augment the ContactRepository class of the Web API project created in Exercise 1 so that it can persist and accept user input and new Contact instances.</span></span>

1. <span data-ttu-id="48484-277">新增下列常數**ContactRepository**類別來代表 web 伺服器快取項目索引鍵名稱的稍後在本練習中的名稱。</span><span class="sxs-lookup"><span data-stu-id="48484-277">Add the following constant to the **ContactRepository** class to represent the name of the web server cache item key name later in this exercise.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. <span data-ttu-id="48484-278">新增的建構函式**ContactRepository**包含下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="48484-278">Add a constructor to the **ContactRepository** containing the following code.</span></span>

    <span data-ttu-id="48484-279">(程式碼片段- *Web API 實驗室-Ex02-連絡人儲存機制的建構函式*)</span><span class="sxs-lookup"><span data-stu-id="48484-279">(Code Snippet - *Web API Lab - Ex02 - Contact Repository Constructor*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. <span data-ttu-id="48484-280">修改程式碼**GetAllContacts**方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="48484-280">Modify the code for the **GetAllContacts** method as demonstrated below.</span></span>

    <span data-ttu-id="48484-281">(程式碼片段- *Web API 實驗室-Ex02-取得所有連絡人*)</span><span class="sxs-lookup"><span data-stu-id="48484-281">(Code Snippet - *Web API Lab - Ex02 - Get All Contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="48484-282">這個範例是供示範之用，並將 web 伺服器的快取做為儲存媒體，以便值將同時適用於多個用戶端，而不是使用工作階段儲存機制或要求儲存體的存留期。</span><span class="sxs-lookup"><span data-stu-id="48484-282">This example is for demonstration purposes and will use the web server's cache as a storage medium, so that the values will be available to multiple clients simultaneously, rather than use a Session storage mechanism or a Request storage lifetime.</span></span> <span data-ttu-id="48484-283">可以使用 Entity Framework、 XML 儲存體或任何其他各種取代 web 伺服器快取。</span><span class="sxs-lookup"><span data-stu-id="48484-283">One could use Entity Framework, XML storage, or any other variety in place of the web server cache.</span></span>
4. <span data-ttu-id="48484-284">實作一個名為的新方法**SaveContact**要**ContactRepository**類別來儲存連絡人的工作。</span><span class="sxs-lookup"><span data-stu-id="48484-284">Implement a new method named **SaveContact** to the **ContactRepository** class to do the work of saving a contact.</span></span> <span data-ttu-id="48484-285">**SaveContact**方法應該採用單一**連絡人**參數和傳回布林值，指出成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="48484-285">The **SaveContact** method should take a single **Contact** parameter and return a Boolean value indicating success or failure.</span></span>

    <span data-ttu-id="48484-286">(程式碼片段- *Web API 的實驗室-Ex02-實作 SaveContact 方法*)</span><span class="sxs-lookup"><span data-stu-id="48484-286">(Code Snippet - *Web API Lab - Ex02 - Implementing the SaveContact Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a><span data-ttu-id="48484-287">練習 3:使用 HTML 用戶端從 Web API</span><span class="sxs-lookup"><span data-stu-id="48484-287">Exercise 3: Consume the Web API from an HTML Client</span></span>

<span data-ttu-id="48484-288">在此練習中，您將建立 HTML 用戶端呼叫 Web API。</span><span class="sxs-lookup"><span data-stu-id="48484-288">In this exercise, you will create an HTML client to call the Web API.</span></span> <span data-ttu-id="48484-289">此用戶端會使用 JavaScript 的 Web api 方便資料交換，並將結果顯示在網頁瀏覽器使用 HTML 標記。</span><span class="sxs-lookup"><span data-stu-id="48484-289">This client will facilitate data exchange with the Web API using JavaScript and will display the results in a web browser using HTML markup.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a><span data-ttu-id="48484-290">工作 1-修改 [索引] 檢視，以提供 GUI 顯示連絡人</span><span class="sxs-lookup"><span data-stu-id="48484-290">Task 1 - Modifying the Index View to Provide a GUI for Displaying Contacts</span></span>

<span data-ttu-id="48484-291">在這個工作中，您將修改以支援的需求在 HTML 瀏覽器中顯示現有的連絡人清單 web 應用程式的預設索引檢視。</span><span class="sxs-lookup"><span data-stu-id="48484-291">In this task, you will modify the default Index view of the web application to support the requirement of displaying the list of existing contacts in an HTML browser.</span></span>

1. <span data-ttu-id="48484-292">開啟**Visual Studio 2012 Express for Web**如果它尚未開啟。</span><span class="sxs-lookup"><span data-stu-id="48484-292">Open **Visual Studio 2012 Express for Web** if it is not already open.</span></span>
2. <span data-ttu-id="48484-293">開啟**開始**解決方案位於**來源/Ex03-ConsumingWebAPI/開始/** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="48484-293">Open the **Begin** solution located at **Source/Ex03-ConsumingWebAPI/Begin/** folder.</span></span> <span data-ttu-id="48484-294">否則，您可能會繼續使用**結束**方案取得完成前一個練習。</span><span class="sxs-lookup"><span data-stu-id="48484-294">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="48484-295">如果您開啟提供**開始**解決方案中，您必須下載某些缺少的 NuGet 封裝才能繼續。</span><span class="sxs-lookup"><span data-stu-id="48484-295">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="48484-296">若要這樣做，請按一下**專案**功能表，然後選取**管理 NuGet 套件**。</span><span class="sxs-lookup"><span data-stu-id="48484-296">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="48484-297">在 [**管理 NuGet 套件**] 對話方塊中，按一下**還原**才能下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="48484-297">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="48484-298">最後，按一下 建置方案**建置** | **建置方案**。</span><span class="sxs-lookup"><span data-stu-id="48484-298">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="48484-299">使用 NuGet 的優點之一是，您不需要寄送您的專案中的所有程式庫專案縮小。</span><span class="sxs-lookup"><span data-stu-id="48484-299">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="48484-300">NuGet Power tools，藉由指定封裝版本在 Packages.config 檔案中，您將能夠下載所有必要的程式庫第一次執行專案。</span><span class="sxs-lookup"><span data-stu-id="48484-300">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="48484-301">這就是為什麼您必須在您開啟現有的方案從這個實驗室之後，執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="48484-301">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="48484-302">開啟**Index.cshtml**位於檔案**Views/Home**資料夾。</span><span class="sxs-lookup"><span data-stu-id="48484-302">Open the **Index.cshtml** file located at **Views/Home** folder.</span></span>
4. <span data-ttu-id="48484-303">Div 項目內的 HTML 程式碼取代識別碼**主體**使它看起來像下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="48484-303">Replace the HTML code within the div element with id **body** so that it looks like the following code.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. <span data-ttu-id="48484-304">要執行 Web API 的 HTTP 要求之檔案的底部新增下列 Javascript 程式碼。</span><span class="sxs-lookup"><span data-stu-id="48484-304">Add the following Javascript code at the bottom of the file to perform the HTTP request to the Web API.</span></span>

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. <span data-ttu-id="48484-305">開啟**ContactController.cs**檔案如果它尚未開啟。</span><span class="sxs-lookup"><span data-stu-id="48484-305">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="48484-306">將中斷點放在**取得**方法**ContactController**類別。</span><span class="sxs-lookup"><span data-stu-id="48484-306">Place a breakpoint on the **Get** method of the **ContactController** class.</span></span>

    <span data-ttu-id="48484-307">![在 API 控制器的 Get 方法中放置中斷點](build-restful-apis-with-aspnet-web-api/_static/image21.png "將中斷點放上 API 控制器的 Get 方法")</span><span class="sxs-lookup"><span data-stu-id="48484-307">![Placing a breakpoint on the Get method of the API controller](build-restful-apis-with-aspnet-web-api/_static/image21.png "Placing a breakpoint on the Get method of the API controller")</span></span>

    <span data-ttu-id="48484-308">*將中斷點放上 API 控制器的 Get 方法*</span><span class="sxs-lookup"><span data-stu-id="48484-308">*Placing a breakpoint on the Get method of the API controller*</span></span>
8. <span data-ttu-id="48484-309">按 **F5** 執行專案。</span><span class="sxs-lookup"><span data-stu-id="48484-309">Press **F5** to run the project.</span></span> <span data-ttu-id="48484-310">HTML 文件時，會載入瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="48484-310">The browser will load the HTML document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="48484-311">請確定您正在瀏覽至您的應用程式的根目錄 URL。</span><span class="sxs-lookup"><span data-stu-id="48484-311">Ensure that you are browsing to the root URL of your application.</span></span>
9. <span data-ttu-id="48484-312">一旦頁面載入和執行的 JavaScript，會叫用中斷點，並執行程式碼，將會暫停在控制器中。</span><span class="sxs-lookup"><span data-stu-id="48484-312">Once the page loads and the JavaScript executes, the breakpoint will be hit and the code execution will pause in the controller.</span></span>

    <span data-ttu-id="48484-313">![使用 VS Express for Web 的 Web API 呼叫偵錯](build-restful-apis-with-aspnet-web-api/_static/image22.png "偵錯使用 VS Express for Web 的 Web API 呼叫")</span><span class="sxs-lookup"><span data-stu-id="48484-313">![Debugging into the Web API calls using VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Debugging into the Web API calls using VS Express for Web")</span></span>

    <span data-ttu-id="48484-314">*偵錯使用 Visual Studio 2012 Express for Web 的 Web API 呼叫*</span><span class="sxs-lookup"><span data-stu-id="48484-314">*Debugging into the Web API call using Visual Studio 2012 Express for Web*</span></span>
10. <span data-ttu-id="48484-315">移除中斷點，然後按**F5**或偵錯工具列**繼續**按鈕以繼續載入瀏覽器中的檢視。</span><span class="sxs-lookup"><span data-stu-id="48484-315">Remove the breakpoint and press **F5** or the debugging toolbar's **Continue** button to continue loading the view in the browser.</span></span> <span data-ttu-id="48484-316">Web API 呼叫完成之後應該會看到呼叫瀏覽器中的 顯示為清單項目從 Web API 傳回的連絡人。</span><span class="sxs-lookup"><span data-stu-id="48484-316">Once the Web API call completes you should see the contacts returned from the Web API call displayed as list items in the browser.</span></span>

    <span data-ttu-id="48484-317">![在瀏覽器中顯示為清單項目 API 呼叫的結果](build-restful-apis-with-aspnet-web-api/_static/image23.png "瀏覽器中顯示為清單項目 API 呼叫的結果")</span><span class="sxs-lookup"><span data-stu-id="48484-317">![Results of the API call displayed in the browser as list items](build-restful-apis-with-aspnet-web-api/_static/image23.png "Results of the API call displayed in the browser as list items")</span></span>

    <span data-ttu-id="48484-318">*在瀏覽器中顯示為清單項目 API 呼叫的結果*</span><span class="sxs-lookup"><span data-stu-id="48484-318">*Results of the API call displayed in the browser as list items*</span></span>
11. <span data-ttu-id="48484-319">停止偵錯。</span><span class="sxs-lookup"><span data-stu-id="48484-319">Stop debugging.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a><span data-ttu-id="48484-320">工作 2-修改 [索引] 檢視，以提供 GUI 建立連絡人</span><span class="sxs-lookup"><span data-stu-id="48484-320">Task 2 - Modifying the Index View to Provide a GUI for Creating Contacts</span></span>

<span data-ttu-id="48484-321">在這個工作中，您將繼續修改索引檢視的 MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="48484-321">In this task, you will continue to modify the Index view of the MVC application.</span></span> <span data-ttu-id="48484-322">表單會新增至 HTML 頁面，將會擷取使用者輸入，並將它傳送給 Web API 來建立新的連絡人，並將建立新的 Web API 控制器方法，以收集從 GUI 的日期。</span><span class="sxs-lookup"><span data-stu-id="48484-322">A form will be added to the HTML page that will capture user input and send it to the Web API to create a new Contact, and a new Web API controller method will be created to collect date from the GUI.</span></span>

1. <span data-ttu-id="48484-323">開啟**ContactController.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="48484-323">Open the **ContactController.cs** file.</span></span>
2. <span data-ttu-id="48484-324">新增至名為控制器類別的新方法**Post**如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="48484-324">Add a new method to the controller class named **Post** as shown in the following code.</span></span>

    <span data-ttu-id="48484-325">(程式碼片段- *Web API 實驗室-Ex03-Post 方法*)</span><span class="sxs-lookup"><span data-stu-id="48484-325">(Code Snippet - *Web API Lab - Ex03 - Post Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. <span data-ttu-id="48484-326">開啟**Index.cshtml**檔案在 Visual Studio 中，如果它尚未開啟。</span><span class="sxs-lookup"><span data-stu-id="48484-326">Open the **Index.cshtml** file in Visual Studio if it is not already open.</span></span>
4. <span data-ttu-id="48484-327">將下列 HTML 程式碼加入檔案之後您加入在先前的工作的未排序清單。</span><span class="sxs-lookup"><span data-stu-id="48484-327">Add the HTML code below to the file just after the unordered list you added in the previous task.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. <span data-ttu-id="48484-328">在底部的 文件的指令碼項目，新增下列醒目提示的程式碼，來處理按鈕 click 事件，將資料張貼至 Web API 使用 HTTP POST 呼叫。</span><span class="sxs-lookup"><span data-stu-id="48484-328">Within the script element at the bottom of the document, add the following highlighted code to handle button-click events, which will post the data to the Web API using an HTTP POST call.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. <span data-ttu-id="48484-329">在  **ContactController.cs**，將中斷點放上**Post**方法。</span><span class="sxs-lookup"><span data-stu-id="48484-329">In **ContactController.cs**, place a breakpoint on the **Post** method.</span></span>
7. <span data-ttu-id="48484-330">按下**F5**瀏覽器中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="48484-330">Press **F5** to run the application in the browser.</span></span>
8. <span data-ttu-id="48484-331">一旦頁面載入瀏覽器中，輸入新的連絡人名稱和識別碼，然後按一下**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="48484-331">Once the page is loaded in the browser, type in a new contact name and Id and click the **Save** button.</span></span>

    <span data-ttu-id="48484-332">![用戶端 HTML 文件載入瀏覽器](build-restful-apis-with-aspnet-web-api/_static/image24.png "瀏覽器中載入用戶端 HTML 文件")</span><span class="sxs-lookup"><span data-stu-id="48484-332">![The client HTML document loaded in the browser](build-restful-apis-with-aspnet-web-api/_static/image24.png "The client HTML document loaded in the browser")</span></span>

    <span data-ttu-id="48484-333">*用戶端 HTML 文件載入瀏覽器*</span><span class="sxs-lookup"><span data-stu-id="48484-333">*The client HTML document loaded in the browser*</span></span>
9. <span data-ttu-id="48484-334">當偵錯工具視窗會在中斷**Post**方法，可看一下屬性**連絡**參數。</span><span class="sxs-lookup"><span data-stu-id="48484-334">When the debugger window breaks in the **Post** method, take a look at the properties of the **contact** parameter.</span></span> <span data-ttu-id="48484-335">值應該符合您在表單中輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="48484-335">The values should match the data you entered in the form.</span></span>

    <span data-ttu-id="48484-336">![從用戶端傳送至 Web API 的連絡人物件](build-restful-apis-with-aspnet-web-api/_static/image25.png "從用戶端傳送至 Web API 的連絡人物件")</span><span class="sxs-lookup"><span data-stu-id="48484-336">![The Contact object being sent to the Web API from the client](build-restful-apis-with-aspnet-web-api/_static/image25.png "The Contact object being sent to the Web API from the client")</span></span>

    <span data-ttu-id="48484-337">*從用戶端傳送至 Web API 的連絡人物件*</span><span class="sxs-lookup"><span data-stu-id="48484-337">*The Contact object being sent to the Web API from the client*</span></span>
10. <span data-ttu-id="48484-338">逐步執行直到偵錯工具中的方法**回應**在建立變數。</span><span class="sxs-lookup"><span data-stu-id="48484-338">Step through the method in the debugger until the **response** variable has been created.</span></span> <span data-ttu-id="48484-339">中的檢查時**區域變數**偵錯工具 視窗中的，您會看到已設定的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="48484-339">Upon inspection in the **Locals** window in the debugger, you'll see that all the properties have been set.</span></span>

   <span data-ttu-id="48484-340">![在 偵錯工具中建立的回應](build-restful-apis-with-aspnet-web-api/_static/image26.png "偵錯工具中建立的回應")</span><span class="sxs-lookup"><span data-stu-id="48484-340">![The response following creation in the debugger](build-restful-apis-with-aspnet-web-api/_static/image26.png "The response following creation in the debugger")</span></span>

   <span data-ttu-id="48484-341">*在偵錯工具中建立的回應*</span><span class="sxs-lookup"><span data-stu-id="48484-341">*The response following creation in the debugger*</span></span>
11. <span data-ttu-id="48484-342">如果您按下**F5**或按**繼續**在偵錯工具將完成的要求。</span><span class="sxs-lookup"><span data-stu-id="48484-342">If you press **F5** or click **Continue** in the debugger the request will complete.</span></span> <span data-ttu-id="48484-343">所儲存的連絡人清單一旦您切換回瀏覽器，已加入新的連絡人**ContactRepository**實作。</span><span class="sxs-lookup"><span data-stu-id="48484-343">Once you switch back to the browser, the new contact has been added to the list of contacts stored by the **ContactRepository** implementation.</span></span>

   <span data-ttu-id="48484-344">![瀏覽器會反映成功建立新的連絡人執行個體](build-restful-apis-with-aspnet-web-api/_static/image27.png "瀏覽器會反映成功建立新的連絡人執行個體")</span><span class="sxs-lookup"><span data-stu-id="48484-344">![The browser reflects successful creation of the new contact instance](build-restful-apis-with-aspnet-web-api/_static/image27.png "The browser reflects successful creation of the new contact instance")</span></span>

   <span data-ttu-id="48484-345">*瀏覽器會反映成功建立新的連絡人執行個體*</span><span class="sxs-lookup"><span data-stu-id="48484-345">*The browser reflects successful creation of the new contact instance*</span></span>

> [!NOTE]
> <span data-ttu-id="48484-346">此外，您可以在其中部署此應用程式至 Azure 的下列[附錄 c:發行 ASP.NET MVC 4 應用程式使用 Web Deploy](#AppendixC)。</span><span class="sxs-lookup"><span data-stu-id="48484-346">Additionally, you can deploy this application to Azure following [Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixC).</span></span>


---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="48484-347">總結</span><span class="sxs-lookup"><span data-stu-id="48484-347">Summary</span></span>

<span data-ttu-id="48484-348">這個實驗室已引進新的 ASP.NET Web API 架構，並使用架構的 RESTful Web Api 的實作。</span><span class="sxs-lookup"><span data-stu-id="48484-348">This lab has introduced you to the new ASP.NET Web API framework and to the implementation of RESTful Web APIs using the framework.</span></span> <span data-ttu-id="48484-349">從這裡開始，您可以建立新的存放庫，可協助資料持續性使用任意數目的機制，並連接該服務而不是提供做為範例，在這個實驗室中其中一個。</span><span class="sxs-lookup"><span data-stu-id="48484-349">From here, you could create a new repository that facilitates data persistence using any number of mechanisms and wire that service up rather than the simple one provided as an example in this lab.</span></span> <span data-ttu-id="48484-350">Web API 支援一些其他功能，例如啟用支援 HTTP 和 JSON 或 XML 的任何語言撰寫的非 HTML 用戶端傳來的通訊。</span><span class="sxs-lookup"><span data-stu-id="48484-350">Web API supports a number of additional features, such as enabling communication from non-HTML clients written in any language that supports HTTP and JSON or XML.</span></span> <span data-ttu-id="48484-351">裝載 Web API，典型的 web 應用程式之外的能力也是可行的以及已建立您自己的序列化格式的能力。</span><span class="sxs-lookup"><span data-stu-id="48484-351">The ability to host a Web API outside of a typical web application is also possible, as well as is the ability to create your own serialization formats.</span></span>

<span data-ttu-id="48484-352">ASP.NET 網站有一個專門用來在 ASP.NET Web API 架構的區域[ [ https://asp.net/web-api ](https://asp.net/web-api) ](https://asp.net/web-api)。</span><span class="sxs-lookup"><span data-stu-id="48484-352">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="48484-353">此站台將持續提供最新的資訊、 範例和新聞與 Web API，因此請經常如果您想要更深入地鑽研建立給幾乎任何裝置或開發架構，可用的自訂 Web Api 的圖案。</span><span class="sxs-lookup"><span data-stu-id="48484-353">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="48484-354">附錄 a:使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="48484-354">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="48484-355">使用程式碼片段，您會有您需要在隨手可得的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="48484-355">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="48484-356">實驗室課程文件會告訴您完全時您可以使用它們，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="48484-356">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="48484-357">![若要將程式碼插入您的專案使用 Visual Studio 程式碼片段](build-restful-apis-with-aspnet-web-api/_static/image28.png "程式碼插入您的專案使用 Visual Studio 程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="48484-357">![Using Visual Studio code snippets to insert code into your project](build-restful-apis-with-aspnet-web-api/_static/image28.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="48484-358">*若要將程式碼插入您的專案使用 Visual Studio 程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="48484-358">*Using Visual Studio code snippets to insert code into your project*</span></span>

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a><span data-ttu-id="48484-359">若要新增的程式碼片段，使用鍵盤 （僅限 C#)</span><span class="sxs-lookup"><span data-stu-id="48484-359">To add a code snippet using the keyboard (C# only)</span></span>

1. <span data-ttu-id="48484-360">將游標放在您想要插入的程式碼。</span><span class="sxs-lookup"><span data-stu-id="48484-360">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="48484-361">開始輸入程式碼片段名稱 （不含空格或連字號）。</span><span class="sxs-lookup"><span data-stu-id="48484-361">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="48484-362">觀看為 IntelliSense 會顯示相符的程式碼片段的名稱。</span><span class="sxs-lookup"><span data-stu-id="48484-362">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="48484-363">選取正確的程式碼片段 （或直到選取整個程式碼片段名稱時，保留 輸入）。</span><span class="sxs-lookup"><span data-stu-id="48484-363">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="48484-364">按下 Tab 鍵兩次的游標位置插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="48484-364">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

    <span data-ttu-id="48484-365">![開始鍵入程式碼片段名稱](build-restful-apis-with-aspnet-web-api/_static/image29.png "開始輸入程式碼片段名稱")</span><span class="sxs-lookup"><span data-stu-id="48484-365">![Start typing the snippet name](build-restful-apis-with-aspnet-web-api/_static/image29.png "Start typing the snippet name")</span></span>

    <span data-ttu-id="48484-366">*開始鍵入程式碼片段名稱*</span><span class="sxs-lookup"><span data-stu-id="48484-366">*Start typing the snippet name*</span></span>

    <span data-ttu-id="48484-367">![按 Tab 鍵以選取反白顯示的程式碼片段](build-restful-apis-with-aspnet-web-api/_static/image30.png "按 Tab 鍵以選取反白顯示的程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="48484-367">![Press Tab to select the highlighted snippet](build-restful-apis-with-aspnet-web-api/_static/image30.png "Press Tab to select the highlighted snippet")</span></span>

    <span data-ttu-id="48484-368">*按 Tab 鍵以選取反白顯示的程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="48484-368">*Press Tab to select the highlighted snippet*</span></span>

    <span data-ttu-id="48484-369">![再次按 Tab 鍵和程式碼片段會依序展開](build-restful-apis-with-aspnet-web-api/_static/image31.png "再次按 Tab 鍵和程式碼片段會展開")</span><span class="sxs-lookup"><span data-stu-id="48484-369">![Press Tab again and the snippet will expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "Press Tab again and the snippet will expand")</span></span>

    <span data-ttu-id="48484-370">*再次按 Tab 鍵和程式碼片段會展開*</span><span class="sxs-lookup"><span data-stu-id="48484-370">*Press Tab again and the snippet will expand*</span></span>

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a><span data-ttu-id="48484-371">若要新增的程式碼片段，使用滑鼠 （C#、 Visual Basic 和 XML）</span><span class="sxs-lookup"><span data-stu-id="48484-371">To add a code snippet using the mouse (C#, Visual Basic and XML)</span></span>

1. <span data-ttu-id="48484-372">以滑鼠右鍵按一下您要插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="48484-372">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="48484-373">選取 **插入程式碼片段**後面**My Code Snippets**。</span><span class="sxs-lookup"><span data-stu-id="48484-373">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="48484-374">選擇相關的程式片段，從清單中，對它按一下。</span><span class="sxs-lookup"><span data-stu-id="48484-374">Pick the relevant snippet from the list, by clicking on it.</span></span>

    <span data-ttu-id="48484-375">![以滑鼠右鍵按一下您要插入程式碼片段，然後選取 插入程式碼片段](build-restful-apis-with-aspnet-web-api/_static/image32.png "以滑鼠右鍵按一下您要插入程式碼片段，然後選取 插入程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="48484-375">![Right-click where you want to insert the code snippet and select Insert Snippet](build-restful-apis-with-aspnet-web-api/_static/image32.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

    <span data-ttu-id="48484-376">*以滑鼠右鍵按一下您要插入程式碼片段，然後選取 插入程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="48484-376">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

    <span data-ttu-id="48484-377">![對它按一下挑選清單中，相關程式碼片段](build-restful-apis-with-aspnet-web-api/_static/image33.png "對它按一下挑選清單中，相關程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="48484-377">![Pick the relevant snippet from the list, by clicking on it](build-restful-apis-with-aspnet-web-api/_static/image33.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

    <span data-ttu-id="48484-378">*對它按一下挑選清單中，相關程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="48484-378">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="48484-379">附錄 b:安裝 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="48484-379">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="48484-380">您可以安裝**Microsoft Visual Studio Express 2012 for Web**或另一個&quot;Express&quot;使用版本 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="48484-380">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="48484-381">下列指示會引導您完成安裝所需的步驟*Visual studio Express 2012 for Web*使用*Microsoft Web Platform Installer*。</span><span class="sxs-lookup"><span data-stu-id="48484-381">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="48484-382">移至[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="48484-382">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="48484-383">或者，如果您已安裝 Web Platform Installer，您可以開啟它，並搜尋產品&quot; <em>Visual Studio Express 2012 for Web 含 Azure SDK</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="48484-383">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="48484-384">按一下 **立即安裝**。</span><span class="sxs-lookup"><span data-stu-id="48484-384">Click on **Install Now**.</span></span> <span data-ttu-id="48484-385">如果您不需要**Web Platform Installer**您將會重新導向至下載並安裝第一次。</span><span class="sxs-lookup"><span data-stu-id="48484-385">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="48484-386">一次**Web Platform Installer**已開啟，按一下**安裝**，啟動安裝程式。</span><span class="sxs-lookup"><span data-stu-id="48484-386">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="48484-387">![安裝 Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "安裝 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="48484-387">![Install Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="48484-388">*安裝 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="48484-388">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="48484-389">閱讀所有產品的授權和詞彙，然後按一下**我接受**以繼續。</span><span class="sxs-lookup"><span data-stu-id="48484-389">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受授權條款](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    <span data-ttu-id="48484-391">*接受授權條款*</span><span class="sxs-lookup"><span data-stu-id="48484-391">*Accepting the license terms*</span></span>
5. <span data-ttu-id="48484-392">等候完成的下載與安裝程序。</span><span class="sxs-lookup"><span data-stu-id="48484-392">Wait until the downloading and installation process completes.</span></span>

    ![安裝進度](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    <span data-ttu-id="48484-394">*安裝進度*</span><span class="sxs-lookup"><span data-stu-id="48484-394">*Installation progress*</span></span>
6. <span data-ttu-id="48484-395">安裝完成時，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="48484-395">When the installation completes, click **Finish**.</span></span>

    ![安裝已完成](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    <span data-ttu-id="48484-397">*安裝已完成*</span><span class="sxs-lookup"><span data-stu-id="48484-397">*Installation completed*</span></span>
7. <span data-ttu-id="48484-398">按一下 **結束**關閉 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="48484-398">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="48484-399">若要開啟 Visual Studio Express for Web，請前往**開始**畫面，即可開始撰寫&quot; **VS Express**&quot;，然後按一下**VS Express for Web**圖格。</span><span class="sxs-lookup"><span data-stu-id="48484-399">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 圖格](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    <span data-ttu-id="48484-401">*VS Express for Web 圖格*</span><span class="sxs-lookup"><span data-stu-id="48484-401">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="48484-402">附錄 c:發行 ASP.NET MVC 4 應用程式使用 Web Deploy</span><span class="sxs-lookup"><span data-stu-id="48484-402">Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="48484-403">本附錄將說明如何從 Azure 入口網站中建立新的網站和發行您取得所遵循的實驗室中，利用 Web Deploy 發行所提供的功能由 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="48484-403">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="48484-404">工作 1： 從 Azure 入口網站中建立新的網站</span><span class="sxs-lookup"><span data-stu-id="48484-404">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="48484-405">移至[Azure 管理入口網站](https://manage.windowsazure.com/)並使用您的訂用帳戶相關聯的 Microsoft 認證登入。</span><span class="sxs-lookup"><span data-stu-id="48484-405">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="48484-406">使用 Azure，您可以免費託管 10 個 ASP.NET 網站，並再隨著流量成長而調整。</span><span class="sxs-lookup"><span data-stu-id="48484-406">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="48484-407">您可以註冊申請[此處](https://aka.ms/aspnet-hol-azure)。</span><span class="sxs-lookup"><span data-stu-id="48484-407">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="48484-408">![登入 Windows Azure 入口網站](build-restful-apis-with-aspnet-web-api/_static/image39.png "登入 Windows Azure 入口網站")</span><span class="sxs-lookup"><span data-stu-id="48484-408">![Log on to Windows Azure portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="48484-409">*登入入口網站*</span><span class="sxs-lookup"><span data-stu-id="48484-409">*Log on to Portal*</span></span>
2. <span data-ttu-id="48484-410">按一下 **新增**命令列上。</span><span class="sxs-lookup"><span data-stu-id="48484-410">Click **New** on the command bar.</span></span>

    <span data-ttu-id="48484-411">![建立新的 Web 站台](build-restful-apis-with-aspnet-web-api/_static/image40.png "建立新的網站")</span><span class="sxs-lookup"><span data-stu-id="48484-411">![Creating a new Web Site](build-restful-apis-with-aspnet-web-api/_static/image40.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="48484-412">*建立新的網站*</span><span class="sxs-lookup"><span data-stu-id="48484-412">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="48484-413">按一下 **計算** | **網站**。</span><span class="sxs-lookup"><span data-stu-id="48484-413">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="48484-414">然後選取**快速建立**選項。</span><span class="sxs-lookup"><span data-stu-id="48484-414">Then select **Quick Create** option.</span></span> <span data-ttu-id="48484-415">新的網站提供可用的 URL，然後按**建立網站**。</span><span class="sxs-lookup"><span data-stu-id="48484-415">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="48484-416">Azure 是您可以控制和管理雲端中執行的 web 應用程式的主應用程式。</span><span class="sxs-lookup"><span data-stu-id="48484-416">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="48484-417">[快速建立] 選項可讓您從 azure 入口網站外部的已完成的 web 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="48484-417">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="48484-418">它不包含設定資料庫的步驟。</span><span class="sxs-lookup"><span data-stu-id="48484-418">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="48484-419">![建立新的網站上，使用 快速建立](build-restful-apis-with-aspnet-web-api/_static/image41.png "建立新的網站上，使用 快速建立")</span><span class="sxs-lookup"><span data-stu-id="48484-419">![Creating a new Web Site using Quick Create](build-restful-apis-with-aspnet-web-api/_static/image41.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="48484-420">*建立新的網站上，使用 快速建立*</span><span class="sxs-lookup"><span data-stu-id="48484-420">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="48484-421">等到新**網站**建立。</span><span class="sxs-lookup"><span data-stu-id="48484-421">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="48484-422">建立網站後按一下底下的連結**URL**資料行。</span><span class="sxs-lookup"><span data-stu-id="48484-422">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="48484-423">檢查新的網站運作。</span><span class="sxs-lookup"><span data-stu-id="48484-423">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="48484-424">![瀏覽至新的 web 站台](build-restful-apis-with-aspnet-web-api/_static/image42.png "瀏覽至新的網站")</span><span class="sxs-lookup"><span data-stu-id="48484-424">![Browsing to the new web site](build-restful-apis-with-aspnet-web-api/_static/image42.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="48484-425">*瀏覽至新的網站*</span><span class="sxs-lookup"><span data-stu-id="48484-425">*Browsing to the new web site*</span></span>

    <span data-ttu-id="48484-426">![執行的 web 站台](build-restful-apis-with-aspnet-web-api/_static/image43.png "執行的網站")</span><span class="sxs-lookup"><span data-stu-id="48484-426">![Web site running](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web site running")</span></span>

    <span data-ttu-id="48484-427">*執行的網站*</span><span class="sxs-lookup"><span data-stu-id="48484-427">*Web site running*</span></span>
6. <span data-ttu-id="48484-428">返回入口網站並按一下底下的網站名稱**名稱**資料行來顯示 [管理] 頁面。</span><span class="sxs-lookup"><span data-stu-id="48484-428">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="48484-429">![開啟 網站管理頁面](build-restful-apis-with-aspnet-web-api/_static/image44.png "開啟的網站管理頁面")</span><span class="sxs-lookup"><span data-stu-id="48484-429">![Opening the web site management pages](build-restful-apis-with-aspnet-web-api/_static/image44.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="48484-430">*開啟 網站管理頁面*</span><span class="sxs-lookup"><span data-stu-id="48484-430">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="48484-431">在 **儀表板**頁面的 **快速概覽**區段中，按一下**下載發行設定檔**連結。</span><span class="sxs-lookup"><span data-stu-id="48484-431">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="48484-432">*發行設定檔*包含所有發行至 Azure，以針對每個已啟用的發行方法的 web 應用程式所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="48484-432">The *publish profile* contains all of the information required to publish a web application to a Azure for each enabled publication method.</span></span> <span data-ttu-id="48484-433">發行設定檔包含 Url、 使用者認證和連接到並對每個發行集的方法已啟用的端點進行驗證所需的資料庫字串。</span><span class="sxs-lookup"><span data-stu-id="48484-433">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="48484-434">**Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**並**Microsoft Visual Studio 2012**支援讀取發行設定檔，以自動化的這些程式的組態正在發行至 Azure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="48484-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="48484-435">![正在下載網站發行設定檔](build-restful-apis-with-aspnet-web-api/_static/image45.png "下載網站發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="48484-435">![Downloading the web site publish profile](build-restful-apis-with-aspnet-web-api/_static/image45.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="48484-436">*正在下載網站發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="48484-436">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="48484-437">下載發行設定檔至已知位置。</span><span class="sxs-lookup"><span data-stu-id="48484-437">Download the publish profile file to a known location.</span></span> <span data-ttu-id="48484-438">進一步在這個練習中，您會看到如何使用此檔案來發佈 Azure web 應用程式從 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="48484-438">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="48484-439">![儲存發行設定檔](build-restful-apis-with-aspnet-web-api/_static/image46.png "儲存發佈設定檔")</span><span class="sxs-lookup"><span data-stu-id="48484-439">![Saving the publish profile file](build-restful-apis-with-aspnet-web-api/_static/image46.png "Saving the publish profile")</span></span>

    <span data-ttu-id="48484-440">*儲存發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="48484-440">*Saving the publish profile file*</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="48484-441">工作 2-設定資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="48484-441">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="48484-442">如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="48484-442">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="48484-443">如果您想要部署簡單的應用程式不會使用 SQL Server，您可能會略過這項工作。</span><span class="sxs-lookup"><span data-stu-id="48484-443">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="48484-444">您將需要 SQL Database 伺服器來儲存應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="48484-444">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="48484-445">您可以從您的訂用帳戶，在 Azure 管理入口網站中檢視 SQL Database 伺服器**Sql Database** | **伺服器** | **伺服器的儀表板**.</span><span class="sxs-lookup"><span data-stu-id="48484-445">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="48484-446">如果您沒有建立伺服器，您可以建立一個使用**新增**命令列上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="48484-446">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="48484-447">請記下的**伺服器名稱和 URL、 系統管理員身分登入名稱和密碼**，如同您會在下一個工作中使用它們。</span><span class="sxs-lookup"><span data-stu-id="48484-447">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="48484-448">並未建立資料庫，因為它會建立在稍後的階段。</span><span class="sxs-lookup"><span data-stu-id="48484-448">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="48484-449">![SQL Database 伺服器儀表板](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database 伺服器儀表板")</span><span class="sxs-lookup"><span data-stu-id="48484-449">![SQL Database Server Dashboard](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="48484-450">*SQL Database 伺服器儀表板*</span><span class="sxs-lookup"><span data-stu-id="48484-450">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="48484-451">下一個工作在您將測試資料庫連接，從 Visual Studio 中，因此您需要在伺服器的清單包含您的本機 IP 位址**允許的 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="48484-451">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="48484-452">若要這樣做，請按一下**設定**，選取的 IP 位址**目前的用戶端 IP 位址**並將它貼上**起始 IP 位址**並**結束 IP 位址**文字方塊中，然後按一下 [ ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="48484-452">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) button.</span></span>

    ![新增用戶端 IP 位址](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    <span data-ttu-id="48484-454">*新增用戶端 IP 位址*</span><span class="sxs-lookup"><span data-stu-id="48484-454">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="48484-455">一次**用戶端 IP 位址**新增至允許的 IP 位址清單中，按一下**儲存**來確認變更。</span><span class="sxs-lookup"><span data-stu-id="48484-455">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![確認變更](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    <span data-ttu-id="48484-457">*確認變更*</span><span class="sxs-lookup"><span data-stu-id="48484-457">*Confirm Changes*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="48484-458">工作 3-發行 ASP.NET MVC 4 應用程式使用 Web Deploy</span><span class="sxs-lookup"><span data-stu-id="48484-458">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="48484-459">返回至 ASP.NET MVC 4 的方案。</span><span class="sxs-lookup"><span data-stu-id="48484-459">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="48484-460">在 **方案總管**，以滑鼠右鍵按一下網站專案，然後選取**發佈**。</span><span class="sxs-lookup"><span data-stu-id="48484-460">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="48484-461">![發行應用程式](build-restful-apis-with-aspnet-web-api/_static/image51.png "發行應用程式")</span><span class="sxs-lookup"><span data-stu-id="48484-461">![Publishing the Application](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publishing the Application")</span></span>

    <span data-ttu-id="48484-462">*發行網站*</span><span class="sxs-lookup"><span data-stu-id="48484-462">*Publishing the web site*</span></span>
2. <span data-ttu-id="48484-463">匯入發行設定檔儲存在第一項工作。</span><span class="sxs-lookup"><span data-stu-id="48484-463">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="48484-464">![匯入發行設定檔](build-restful-apis-with-aspnet-web-api/_static/image52.png "匯入發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="48484-464">![Importing the publish profile](build-restful-apis-with-aspnet-web-api/_static/image52.png "Importing the publish profile")</span></span>

    <span data-ttu-id="48484-465">*匯入發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="48484-465">*Importing publish profile*</span></span>
3. <span data-ttu-id="48484-466">按一下 **驗證連線**。</span><span class="sxs-lookup"><span data-stu-id="48484-466">Click **Validate Connection**.</span></span> <span data-ttu-id="48484-467">驗證完成後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="48484-467">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="48484-468">一旦您看到 [驗證連線] 按鈕旁邊會出現綠色核取記號完成驗證。</span><span class="sxs-lookup"><span data-stu-id="48484-468">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="48484-469">![驗證連接](build-restful-apis-with-aspnet-web-api/_static/image53.png "驗證連線")</span><span class="sxs-lookup"><span data-stu-id="48484-469">![Validating connection](build-restful-apis-with-aspnet-web-api/_static/image53.png "Validating connection")</span></span>

    <span data-ttu-id="48484-470">*驗證連接*</span><span class="sxs-lookup"><span data-stu-id="48484-470">*Validating connection*</span></span>
4. <span data-ttu-id="48484-471">在 **設定**頁面的 **資料庫**區段中，按一下您的資料庫連接文字方塊旁邊的按鈕 (也就是**DefaultConnection**)。</span><span class="sxs-lookup"><span data-stu-id="48484-471">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="48484-472">![Web 部署組態](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web 部署設定")</span><span class="sxs-lookup"><span data-stu-id="48484-472">![Web deploy configuration](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy configuration")</span></span>

    <span data-ttu-id="48484-473">*Web 部署設定*</span><span class="sxs-lookup"><span data-stu-id="48484-473">*Web deploy configuration*</span></span>
5. <span data-ttu-id="48484-474">設定資料庫連線，如下所示：</span><span class="sxs-lookup"><span data-stu-id="48484-474">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="48484-475">在 **伺服器名稱**輸入您使用 SQL Database 伺服器的 URL *tcp:* 前置詞。</span><span class="sxs-lookup"><span data-stu-id="48484-475">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="48484-476">在 **使用者名**輸入您的伺服器系統管理員身分登入名稱。</span><span class="sxs-lookup"><span data-stu-id="48484-476">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="48484-477">在 **密碼**輸入您的伺服器系統管理員身分登入密碼。</span><span class="sxs-lookup"><span data-stu-id="48484-477">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="48484-478">輸入新的資料庫名稱，例如：*MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="48484-478">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="48484-479">![設定目的地連接字串](build-restful-apis-with-aspnet-web-api/_static/image55.png "設定目的地連接字串")</span><span class="sxs-lookup"><span data-stu-id="48484-479">![Configuring destination connection string](build-restful-apis-with-aspnet-web-api/_static/image55.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="48484-480">*設定目的地連接字串*</span><span class="sxs-lookup"><span data-stu-id="48484-480">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="48484-481">然後按一下 [確定]。 </span><span class="sxs-lookup"><span data-stu-id="48484-481">Then click **OK**.</span></span> <span data-ttu-id="48484-482">當系統提示您建立資料庫時，按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="48484-482">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="48484-483">![建立資料庫](build-restful-apis-with-aspnet-web-api/_static/image56.png "建立的資料庫字串")</span><span class="sxs-lookup"><span data-stu-id="48484-483">![Creating the database](build-restful-apis-with-aspnet-web-api/_static/image56.png "Creating the database string")</span></span>

    <span data-ttu-id="48484-484">*建立資料庫*</span><span class="sxs-lookup"><span data-stu-id="48484-484">*Creating the database*</span></span>
7. <span data-ttu-id="48484-485">您將用來連接至 Windows Azure 中的 SQL 資料庫的連接字串會顯示在文字方塊中的預設連線。</span><span class="sxs-lookup"><span data-stu-id="48484-485">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="48484-486">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="48484-486">Then click **Next**.</span></span>

    <span data-ttu-id="48484-487">![連接字串指向 SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "連接字串指向 SQL Database")</span><span class="sxs-lookup"><span data-stu-id="48484-487">![Connection string pointing to SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="48484-488">*連接字串指向 SQL Database*</span><span class="sxs-lookup"><span data-stu-id="48484-488">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="48484-489">在  **Preview**頁面上，按一下**發佈**。</span><span class="sxs-lookup"><span data-stu-id="48484-489">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="48484-490">![Web 應用程式發行](build-restful-apis-with-aspnet-web-api/_static/image58.png "發行 web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="48484-490">![Publishing the web application](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publishing the web application")</span></span>

    <span data-ttu-id="48484-491">*發行 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="48484-491">*Publishing the web application*</span></span>
9. <span data-ttu-id="48484-492">當發行程序完成時，預設瀏覽器會開啟已發行的網站。</span><span class="sxs-lookup"><span data-stu-id="48484-492">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="48484-493">![應用程式發行至 Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "應用程式發行至 Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="48484-493">![Application published to Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="48484-494">*應用程式發佈至 Azure*</span><span class="sxs-lookup"><span data-stu-id="48484-494">*Application published to Azure*</span></span>
