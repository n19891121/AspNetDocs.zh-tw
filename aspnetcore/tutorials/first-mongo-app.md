---
title: 使用 ASP.NET Core 與 MongoDB 建置 Web API
author: prkhandelwal
description: 此教學課程示範如何使用 MongoDB NoSQL 資料庫建置 ASP.NET Core Web API。
ms.author: scaddie
ms.custom: mvc, seodec18
ms.date: 01/31/2019
uid: tutorials/first-mongo-app
ms.openlocfilehash: 5e146261fdc8354fc9f4295a8af317e5cc36332f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57032965"
---
# <a name="create-a-web-api-with-aspnet-core-and-mongodb"></a><span data-ttu-id="51ba9-103">使用 ASP.NET Core 與 MongoDB 建立 Web API</span><span class="sxs-lookup"><span data-stu-id="51ba9-103">Create a web API with ASP.NET Core and MongoDB</span></span>

<span data-ttu-id="51ba9-104">作者：[Pratik Khandelwal](https://twitter.com/K2Prk) 與 [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="51ba9-104">By [Pratik Khandelwal](https://twitter.com/K2Prk) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="51ba9-105">此教學課程會建立 Web API，此 API 會在 [MongoDB](https://www.mongodb.com/what-is-mongodb) NoSQL 資料庫上執行建立、讀取、更新及刪除 (CRUD) 作業。</span><span class="sxs-lookup"><span data-stu-id="51ba9-105">This tutorial creates a web API that performs Create, Read, Update, and Delete (CRUD) operations on a [MongoDB](https://www.mongodb.com/what-is-mongodb) NoSQL database.</span></span>

<span data-ttu-id="51ba9-106">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="51ba9-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="51ba9-107">設定 MongoDB</span><span class="sxs-lookup"><span data-stu-id="51ba9-107">Configure MongoDB</span></span>
> * <span data-ttu-id="51ba9-108">建立 MongoDB 資料庫</span><span class="sxs-lookup"><span data-stu-id="51ba9-108">Create a MongoDB database</span></span>
> * <span data-ttu-id="51ba9-109">定義 MongoDB 集合與結構描述</span><span class="sxs-lookup"><span data-stu-id="51ba9-109">Define a MongoDB collection and schema</span></span>
> * <span data-ttu-id="51ba9-110">從 Web API 執行 MongoDB CRUD 作業</span><span class="sxs-lookup"><span data-stu-id="51ba9-110">Perform MongoDB CRUD operations from a web API</span></span>

<span data-ttu-id="51ba9-111">[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/first-mongo-app/sample) \(英文\) ([如何下載](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="51ba9-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/first-mongo-app/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51ba9-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="51ba9-112">Prerequisites</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="51ba9-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51ba9-113">Visual Studio</span></span>](#tab/visual-studio)

* [<span data-ttu-id="51ba9-114">.NET Core SDK 2.2 或更新版本</span><span class="sxs-lookup"><span data-stu-id="51ba9-114">.NET Core SDK 2.2 or later</span></span>](https://www.microsoft.com/net/download/all)
* <span data-ttu-id="51ba9-115">[Visual Studio 2017 15.9 版或更新版本](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)，包含 **ASP.NET 與網頁程式開發**工作負載</span><span class="sxs-lookup"><span data-stu-id="51ba9-115">[Visual Studio 2017 version 15.9 or later](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) with the **ASP.NET and web development** workload</span></span>
* [<span data-ttu-id="51ba9-116">MongoDB</span><span class="sxs-lookup"><span data-stu-id="51ba9-116">MongoDB</span></span>](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="51ba9-117">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="51ba9-117">Visual Studio Code</span></span>](#tab/visual-studio-code)

* [<span data-ttu-id="51ba9-118">.NET Core SDK 2.2 或更新版本</span><span class="sxs-lookup"><span data-stu-id="51ba9-118">.NET Core SDK 2.2 or later</span></span>](https://www.microsoft.com/net/download/all)
* [<span data-ttu-id="51ba9-119">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="51ba9-119">Visual Studio Code</span></span>](https://code.visualstudio.com/download)
* [<span data-ttu-id="51ba9-120">C# for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="51ba9-120">C# for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
* [<span data-ttu-id="51ba9-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="51ba9-121">MongoDB</span></span>](https://docs.mongodb.com/manual/administration/install-community/)

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="51ba9-122">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="51ba9-122">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* [<span data-ttu-id="51ba9-123">.NET Core SDK 2.2 或更新版本</span><span class="sxs-lookup"><span data-stu-id="51ba9-123">.NET Core SDK 2.2 or later</span></span>](https://www.microsoft.com/net/download/all)
* [<span data-ttu-id="51ba9-124">Visual Studio for Mac 7.7 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="51ba9-124">Visual Studio for Mac version 7.7 or later</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="51ba9-125">MongoDB</span><span class="sxs-lookup"><span data-stu-id="51ba9-125">MongoDB</span></span>](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)

---

## <a name="configure-mongodb"></a><span data-ttu-id="51ba9-126">設定 MongoDB</span><span class="sxs-lookup"><span data-stu-id="51ba9-126">Configure MongoDB</span></span>

<span data-ttu-id="51ba9-127">若使用 Windows，MongoDB 預設會安裝在 *C:\\Program Files\\MongoDB*。</span><span class="sxs-lookup"><span data-stu-id="51ba9-127">If using Windows, MongoDB is installed at *C:\\Program Files\\MongoDB* by default.</span></span> <span data-ttu-id="51ba9-128">將 *C:\\Program Files\\MongoDB\\Server\\\<版本號碼>\\bin* 新增到 `Path` 環境變數。</span><span class="sxs-lookup"><span data-stu-id="51ba9-128">Add *C:\\Program Files\\MongoDB\\Server\\\<version_number>\\bin* to the `Path` environment variable.</span></span> <span data-ttu-id="51ba9-129">此變更會啟用從您開發機器上的任意位置存取 MongoDB 的功能。</span><span class="sxs-lookup"><span data-stu-id="51ba9-129">This change enables MongoDB access from anywhere on your development machine.</span></span>

<span data-ttu-id="51ba9-130">在下列步驟中使用 mongo 殼層來建立資料庫、建立集合及存放文件。</span><span class="sxs-lookup"><span data-stu-id="51ba9-130">Use the mongo Shell in the following steps to create a database, make collections, and store documents.</span></span> <span data-ttu-id="51ba9-131">如需有關 mongo 殼層命令的詳細資訊，請參閱[使用 mongo 殼層](https://docs.mongodb.com/manual/mongo/#working-with-the-mongo-shell)。</span><span class="sxs-lookup"><span data-stu-id="51ba9-131">For more information on mongo Shell commands, see [Working with the mongo Shell](https://docs.mongodb.com/manual/mongo/#working-with-the-mongo-shell).</span></span>

1. <span data-ttu-id="51ba9-132">選擇您開發機器上的目錄來存放資料。</span><span class="sxs-lookup"><span data-stu-id="51ba9-132">Choose a directory on your development machine for storing the data.</span></span> <span data-ttu-id="51ba9-133">例如， Windows 上的 *C:\\BooksData*。</span><span class="sxs-lookup"><span data-stu-id="51ba9-133">For example, *C:\\BooksData* on Windows.</span></span> <span data-ttu-id="51ba9-134">若該目錄不存在，請建立它。</span><span class="sxs-lookup"><span data-stu-id="51ba9-134">Create the directory if it doesn't exist.</span></span> <span data-ttu-id="51ba9-135">mongo 殼層不會建立新目錄。</span><span class="sxs-lookup"><span data-stu-id="51ba9-135">The mongo Shell doesn't create new directories.</span></span>
1. <span data-ttu-id="51ba9-136">開啟命令殼層。</span><span class="sxs-lookup"><span data-stu-id="51ba9-136">Open a command shell.</span></span> <span data-ttu-id="51ba9-137">執行下列命令以連線到預設連接埠 27017 上的 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="51ba9-137">Run the following command to connect to MongoDB on default port 27017.</span></span> <span data-ttu-id="51ba9-138">請記得將 `<data_directory_path>` 取代為您在上一個步驟中選擇的目錄。</span><span class="sxs-lookup"><span data-stu-id="51ba9-138">Remember to replace `<data_directory_path>` with the directory you chose in the previous step.</span></span>

    ```console
    mongod --dbpath <data_directory_path>
    ```

1. <span data-ttu-id="51ba9-139">開啟另一個命令殼層執行個體。</span><span class="sxs-lookup"><span data-stu-id="51ba9-139">Open another command shell instance.</span></span> <span data-ttu-id="51ba9-140">執行下列命令以連線到預設測試資料庫：</span><span class="sxs-lookup"><span data-stu-id="51ba9-140">Connect to the default test database by running the following command:</span></span>

    ```console
    mongo
    ```

1. <span data-ttu-id="51ba9-141">在命令殼層中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="51ba9-141">Run the following in a command shell:</span></span>

    ```console
    use BookstoreDb
    ```

    <span data-ttu-id="51ba9-142">若它不存在，會建立名為 *BookstoreDb* 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="51ba9-142">If it doesn't already exist, a database named *BookstoreDb* is created.</span></span> <span data-ttu-id="51ba9-143">若該資料庫存在，會開啟其連線進行交易。</span><span class="sxs-lookup"><span data-stu-id="51ba9-143">If the database does exist, its connection is opened for transactions.</span></span>

1. <span data-ttu-id="51ba9-144">使用下列命令建立 `Books` 集合：</span><span class="sxs-lookup"><span data-stu-id="51ba9-144">Create a `Books` collection using following command:</span></span>

    ```console
    db.createCollection('Books')
    ```

    <span data-ttu-id="51ba9-145">會顯示下列結果：</span><span class="sxs-lookup"><span data-stu-id="51ba9-145">The following result is displayed:</span></span>

    ```console
    { "ok" : 1 }
    ```

1. <span data-ttu-id="51ba9-146">使用下列命令為 `Books` 集合定義結構描述並插入兩份文件：</span><span class="sxs-lookup"><span data-stu-id="51ba9-146">Define a schema for the `Books` collection and insert two documents using the following command:</span></span>

    ```console
    db.Books.insertMany([{'Name':'Design Patterns','Price':54.93,'Category':'Computers','Author':'Ralph Johnson'}, {'Name':'Clean Code','Price':43.15,'Category':'Computers','Author':'Robert C. Martin'}])
    ```

    <span data-ttu-id="51ba9-147">會顯示下列結果：</span><span class="sxs-lookup"><span data-stu-id="51ba9-147">The following result is displayed:</span></span>

    ```console
    {
      "acknowledged" : true,
      "insertedIds" : [
        ObjectId("5bfd996f7b8e48dc15ff215d"),
        ObjectId("5bfd996f7b8e48dc15ff215e")
      ]
    }
    ```

1. <span data-ttu-id="51ba9-148">使用下列命令檢視資料庫中的文件：</span><span class="sxs-lookup"><span data-stu-id="51ba9-148">View the documents in the database using the following command:</span></span>

    ```console
    db.Books.find({}).pretty()
    ```

    <span data-ttu-id="51ba9-149">會顯示下列結果：</span><span class="sxs-lookup"><span data-stu-id="51ba9-149">The following result is displayed:</span></span>

    ```console
    {
      "_id" : ObjectId("5bfd996f7b8e48dc15ff215d"),
      "Name" : "Design Patterns",
      "Price" : 54.93,
      "Category" : "Computers",
      "Author" : "Ralph Johnson"
    }
    {
      "_id" : ObjectId("5bfd996f7b8e48dc15ff215e"),
      "Name" : "Clean Code",
      "Price" : 43.15,
      "Category" : "Computers",
      "Author" : "Robert C. Martin"
    }
    ```

    <span data-ttu-id="51ba9-150">結構描述會為每份文件新增自動彙總的 `_id` 屬性 (類型 `ObjectId`)。</span><span class="sxs-lookup"><span data-stu-id="51ba9-150">The schema adds an autogenerated `_id` property of type `ObjectId` for each document.</span></span>

<span data-ttu-id="51ba9-151">資料庫已就緒。</span><span class="sxs-lookup"><span data-stu-id="51ba9-151">The database is ready.</span></span> <span data-ttu-id="51ba9-152">您可以開始建立 ASP.NET Core Web API。</span><span class="sxs-lookup"><span data-stu-id="51ba9-152">You can start creating the ASP.NET Core web API.</span></span>

## <a name="create-the-aspnet-core-web-api-project"></a><span data-ttu-id="51ba9-153">建立 ASP.NET Core Web API 專案</span><span class="sxs-lookup"><span data-stu-id="51ba9-153">Create the ASP.NET Core web API project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="51ba9-154">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51ba9-154">Visual Studio</span></span>](#tab/visual-studio)

1. <span data-ttu-id="51ba9-155">移至 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="51ba9-155">Go to **File** > **New** > **Project**.</span></span>
1. <span data-ttu-id="51ba9-156">選取 [ASP.NET Core Web 應用程式]、將專案命名為 *BooksApi*，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="51ba9-156">Select **ASP.NET Core Web Application**, name the project *BooksApi*, and click **OK**.</span></span>
1. <span data-ttu-id="51ba9-157">選取 [.NET Core] 目標架構與 [ASP.NET Core 2.1]。</span><span class="sxs-lookup"><span data-stu-id="51ba9-157">Select the **.NET Core** target framework and **ASP.NET Core 2.1**.</span></span> <span data-ttu-id="51ba9-158">選取 [API] 專案範本，然後按一下 [確定]：</span><span class="sxs-lookup"><span data-stu-id="51ba9-158">Select the **API** project template, and click **OK**:</span></span>
1. <span data-ttu-id="51ba9-159">造訪 [NuGet 資源庫：MongoDB.Driver](https://www.nuget.org/packages/MongoDB.Driver/) 來判斷 MongoDB 的最新穩定 .NET 驅動程式版本。</span><span class="sxs-lookup"><span data-stu-id="51ba9-159">Visit the [NuGet Gallery: MongoDB.Driver](https://www.nuget.org/packages/MongoDB.Driver/) to determine the latest stable version of the .NET driver for MongoDB.</span></span> <span data-ttu-id="51ba9-160">在 [套件管理員主控台] 視窗中，瀏覽到專案根目錄。</span><span class="sxs-lookup"><span data-stu-id="51ba9-160">In the **Package Manager Console** window, navigate to the project root.</span></span> <span data-ttu-id="51ba9-161">執行下列命令以安裝適用於 MongoDB 的 .NET 驅動程式：</span><span class="sxs-lookup"><span data-stu-id="51ba9-161">Run the following command to install the .NET driver for MongoDB:</span></span>

    ```powershell
    Install-Package MongoDB.Driver -Version {VERSION}
    ```

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="51ba9-162">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="51ba9-162">Visual Studio Code</span></span>](#tab/visual-studio-code)

1. <span data-ttu-id="51ba9-163">在命令殼層中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="51ba9-163">Run the following commands in a command shell:</span></span>

    ```console
    dotnet new webapi -o BooksApi
    code BooksApi
    ```

    <span data-ttu-id="51ba9-164">會產生以 .NET Core 為目標的新 ASP.NET Core Web API 專案，並在 Visual Studio Code 中開啟。</span><span class="sxs-lookup"><span data-stu-id="51ba9-164">A new ASP.NET Core web API project targeting .NET Core is generated and opened in Visual Studio Code.</span></span>

1. <span data-ttu-id="51ba9-165">當 ['BooksApi' 中缺少要建置及偵錯的必要資產。是否要新增它們?] 通知出現時，請按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="51ba9-165">Click **Yes** when the *Required assets to build and debug are missing from 'BooksApi'. Add them?* notification appears.</span></span>
1. <span data-ttu-id="51ba9-166">造訪 [NuGet 資源庫：MongoDB.Driver](https://www.nuget.org/packages/MongoDB.Driver/) 來判斷 MongoDB 的最新穩定 .NET 驅動程式版本。</span><span class="sxs-lookup"><span data-stu-id="51ba9-166">Visit the [NuGet Gallery: MongoDB.Driver](https://www.nuget.org/packages/MongoDB.Driver/) to determine the latest stable version of the .NET driver for MongoDB.</span></span> <span data-ttu-id="51ba9-167">開啟 [整合式終端機] 並瀏覽到專案根目錄。</span><span class="sxs-lookup"><span data-stu-id="51ba9-167">Open **Integrated Terminal** and navigate to the project root.</span></span> <span data-ttu-id="51ba9-168">執行下列命令以安裝適用於 MongoDB 的 .NET 驅動程式：</span><span class="sxs-lookup"><span data-stu-id="51ba9-168">Run the following command to install the .NET driver for MongoDB:</span></span>

    ```console
    dotnet add BooksApi.csproj package MongoDB.Driver -v {VERSION}
    ```

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="51ba9-169">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="51ba9-169">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

1. <span data-ttu-id="51ba9-170">移至 [檔案] > [新增解決方案] > [.NET Core] > [應用程式]。</span><span class="sxs-lookup"><span data-stu-id="51ba9-170">Go to **File** > **New Solution** > **.NET Core** > **App**.</span></span>
1. <span data-ttu-id="51ba9-171">選取 **ASP.NET Core Web API** C# 專案範本，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="51ba9-171">Select the **ASP.NET Core Web API** C# project template, and click **Next**.</span></span>
1. <span data-ttu-id="51ba9-172">從 [目標 Framework] 下拉式清單選取 [.NET Core 2.2]，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="51ba9-172">Select **.NET Core 2.2** from the **Target Framework** drop-down list, and click **Next**.</span></span>
1. <span data-ttu-id="51ba9-173">在 [專案名稱] 中輸入 *BooksApi*，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="51ba9-173">Enter *BooksApi* for the **Project Name**, and click **Create**.</span></span>
1. <span data-ttu-id="51ba9-174">在 [方案] 台中，以滑鼠右鍵按一下專案的 [相依性] 節點並選取 [新增封裝]。</span><span class="sxs-lookup"><span data-stu-id="51ba9-174">In the **Solution** pad, right-click the project's **Dependencies** node and select **Add Packages**.</span></span>
1. <span data-ttu-id="51ba9-175">在搜尋方塊中輸入 *MongoDB.Driver*、選取 *MongoDB.Driver* 套件，然後按一下 [新增封裝]。</span><span class="sxs-lookup"><span data-stu-id="51ba9-175">Enter *MongoDB.Driver* in the search box, select the *MongoDB.Driver* package, and click **Add Package**.</span></span>
1. <span data-ttu-id="51ba9-176">按一下 [授權接受] 對話方塊中的 [接受] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51ba9-176">Click the **Accept** button in the **License Acceptance** dialog.</span></span>

---

## <a name="add-a-model"></a><span data-ttu-id="51ba9-177">新增模型</span><span class="sxs-lookup"><span data-stu-id="51ba9-177">Add a model</span></span>

1. <span data-ttu-id="51ba9-178">新增 *Models* 目錄到專案根目錄。</span><span class="sxs-lookup"><span data-stu-id="51ba9-178">Add a *Models* directory to the project root.</span></span>
1. <span data-ttu-id="51ba9-179">新增具有下列程式碼的 `Book` 類別到 *Models* 目錄：</span><span class="sxs-lookup"><span data-stu-id="51ba9-179">Add a `Book` class to the *Models* directory with the following code:</span></span>

    [!code-csharp[](first-mongo-app/sample/BooksApi/Models/Book.cs)]

<span data-ttu-id="51ba9-180">在上面的類別中，需要 `Id` 屬性：</span><span class="sxs-lookup"><span data-stu-id="51ba9-180">In the preceding class, the `Id` property:</span></span>

* <span data-ttu-id="51ba9-181">才能將通用語言執行平台 (CLR) 物件對應到 MongoDB 集合。</span><span class="sxs-lookup"><span data-stu-id="51ba9-181">Is required for mapping the Common Language Runtime (CLR) object to the MongoDB collection.</span></span>
* <span data-ttu-id="51ba9-182">使用 `[BsonId]` 加上附註以指定此屬性做為文件的主要機碼。</span><span class="sxs-lookup"><span data-stu-id="51ba9-182">Is annotated with `[BsonId]` to designate this property as the document's primary key.</span></span>
* <span data-ttu-id="51ba9-183">使用 `[BsonRepresentation(BsonType.ObjectId)]` 加上附註以允許將參數傳遞為類型 `string` 而非 `ObjectId`。</span><span class="sxs-lookup"><span data-stu-id="51ba9-183">Is annotated with `[BsonRepresentation(BsonType.ObjectId)]` to allow passing the parameter as type `string` instead of `ObjectId`.</span></span> <span data-ttu-id="51ba9-184">Mongo 會處理從 `string` 轉換到 `ObjectId` 的作業。</span><span class="sxs-lookup"><span data-stu-id="51ba9-184">Mongo handles the conversion from `string` to `ObjectId`.</span></span>

<span data-ttu-id="51ba9-185">該類別中的其他屬性是使用 `[BsonElement]` 屬性加上註解。</span><span class="sxs-lookup"><span data-stu-id="51ba9-185">Other properties in the class are annotated with the `[BsonElement]` attribute.</span></span> <span data-ttu-id="51ba9-186">屬性的值代表 MongoDB 集合中的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="51ba9-186">The attribute's value represents the property name in the MongoDB collection.</span></span>

## <a name="add-a-crud-operations-class"></a><span data-ttu-id="51ba9-187">新增 CRUD 作業類別</span><span class="sxs-lookup"><span data-stu-id="51ba9-187">Add a CRUD operations class</span></span>

1. <span data-ttu-id="51ba9-188">新增 *Services* 目錄到專案根目錄。</span><span class="sxs-lookup"><span data-stu-id="51ba9-188">Add a *Services* directory to the project root.</span></span>
1. <span data-ttu-id="51ba9-189">新增具有下列程式碼的 `BookService` 類別到 *Services* 目錄：</span><span class="sxs-lookup"><span data-stu-id="51ba9-189">Add a `BookService` class to the *Services* directory with the following code:</span></span>

    [!code-csharp[](first-mongo-app/sample/BooksApi/Services/BookService.cs?name=snippet_BookServiceClass)]

1. <span data-ttu-id="51ba9-190">新增 MongoDB 連接字串到 *appsettings.json*：</span><span class="sxs-lookup"><span data-stu-id="51ba9-190">Add the MongoDB connection string to *appsettings.json*:</span></span>

    [!code-csharp[](first-mongo-app/sample/BooksApi/appsettings.json?highlight=2-4)]

    <span data-ttu-id="51ba9-191">上面的 `BookstoreDb` 屬性是在 `BookService` 類別建構函式中存取的。</span><span class="sxs-lookup"><span data-stu-id="51ba9-191">The preceding `BookstoreDb` property is accessed in the `BookService` class constructor.</span></span>

1. <span data-ttu-id="51ba9-192">在 `Startup.ConfigureServices` 中，向相依性插入系統註冊 `BookService` 類別：</span><span class="sxs-lookup"><span data-stu-id="51ba9-192">In `Startup.ConfigureServices`, register the `BookService` class with the Dependency Injection system:</span></span>

    [!code-csharp[](first-mongo-app/sample/BooksApi/Startup.cs?name=snippet_ConfigureServices&highlight=3)]

    <span data-ttu-id="51ba9-193">必須完成上面的服務註冊，才能在取用資源的類別中支援建構函式插入。</span><span class="sxs-lookup"><span data-stu-id="51ba9-193">The preceding service registration is necessary to support constructor injection in consuming classes.</span></span>

<span data-ttu-id="51ba9-194">`BookService` 類別使用下列 `MongoDB.Driver` 成員來對資料庫執行 CRUD 作業：</span><span class="sxs-lookup"><span data-stu-id="51ba9-194">The `BookService` class uses the following `MongoDB.Driver` members to perform CRUD operations against the database:</span></span>

* <span data-ttu-id="51ba9-195">`MongoClient` &ndash; 讀取用於執行資料庫作業的伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="51ba9-195">`MongoClient` &ndash; Reads the server instance for performing database operations.</span></span> <span data-ttu-id="51ba9-196">此類別的建構函式是使用 MongoDB 連接字串提供：</span><span class="sxs-lookup"><span data-stu-id="51ba9-196">The constructor of this class is provided the MongoDB connection string:</span></span>

    [!code-csharp[](first-mongo-app/sample/BooksApi/Services/BookService.cs?name=snippet_BookServiceConstructor&highlight=3)]

* <span data-ttu-id="51ba9-197">`IMongoDatabase` &ndash; 代表用於執行作業的 Mongo 資料庫。</span><span class="sxs-lookup"><span data-stu-id="51ba9-197">`IMongoDatabase` &ndash; Represents the Mongo database for performing operations.</span></span> <span data-ttu-id="51ba9-198">此教學課程使用介面上的一般 `GetCollection<T>(collection)` 方法來存取特定集合中的資料。</span><span class="sxs-lookup"><span data-stu-id="51ba9-198">This tutorial uses the generic `GetCollection<T>(collection)` method on the interface to gain access to data in a specific collection.</span></span> <span data-ttu-id="51ba9-199">呼叫此方法之後，CRUD 作業可針對集合執行。</span><span class="sxs-lookup"><span data-stu-id="51ba9-199">CRUD operations can be performed against the collection after this method is called.</span></span> <span data-ttu-id="51ba9-200">在 `GetCollection<T>(collection)` 方法呼叫中：</span><span class="sxs-lookup"><span data-stu-id="51ba9-200">In the `GetCollection<T>(collection)` method call:</span></span>
  * <span data-ttu-id="51ba9-201">`collection` 代表集合名稱。</span><span class="sxs-lookup"><span data-stu-id="51ba9-201">`collection` represents the collection name.</span></span>
  * <span data-ttu-id="51ba9-202">`T` 代表儲存在集合中的 CLR 物件類型。</span><span class="sxs-lookup"><span data-stu-id="51ba9-202">`T` represents the CLR object type stored in the collection.</span></span>

<span data-ttu-id="51ba9-203">`GetCollection<T>(collection)` 會傳回代表集合的 `MongoCollection` 物件。</span><span class="sxs-lookup"><span data-stu-id="51ba9-203">`GetCollection<T>(collection)` returns a `MongoCollection` object representing the collection.</span></span> <span data-ttu-id="51ba9-204">在此教學課程中，會在集合上叫用下列方法：</span><span class="sxs-lookup"><span data-stu-id="51ba9-204">In this tutorial, the following methods are invoked on the collection:</span></span>

* <span data-ttu-id="51ba9-205">`Find<T>` &ndash; 傳回集合中符合所提供搜尋條件的所有文件。</span><span class="sxs-lookup"><span data-stu-id="51ba9-205">`Find<T>` &ndash; Returns all documents in the collection matching the provided search criteria.</span></span>
* <span data-ttu-id="51ba9-206">`InsertOne` &ndash; 插入提供的物件做為集合中的新文件。</span><span class="sxs-lookup"><span data-stu-id="51ba9-206">`InsertOne` &ndash; Inserts the provided object as a new document in the collection.</span></span>
* <span data-ttu-id="51ba9-207">`ReplaceOne` &ndash; 使用提供的物件取代符合所提供搜尋條件的單一文件。</span><span class="sxs-lookup"><span data-stu-id="51ba9-207">`ReplaceOne` &ndash; Replaces the single document matching the provided search criteria with the provided object.</span></span>
* <span data-ttu-id="51ba9-208">`DeleteOne` &ndash; 刪除符合所提供搜尋條件的單一文件。</span><span class="sxs-lookup"><span data-stu-id="51ba9-208">`DeleteOne` &ndash; Deletes a single document matching the provided search criteria.</span></span>

## <a name="add-a-controller"></a><span data-ttu-id="51ba9-209">新增控制器</span><span class="sxs-lookup"><span data-stu-id="51ba9-209">Add a controller</span></span>

1. <span data-ttu-id="51ba9-210">新增具有下列程式碼的 `BooksController` 類別到 *Controllers* 目錄：</span><span class="sxs-lookup"><span data-stu-id="51ba9-210">Add a `BooksController` class to the *Controllers* directory with the following code:</span></span>

    [!code-csharp[](first-mongo-app/sample/BooksApi/Controllers/BooksController.cs)]

    <span data-ttu-id="51ba9-211">上述 Web API 控制器會：</span><span class="sxs-lookup"><span data-stu-id="51ba9-211">The preceding web API controller:</span></span>

    * <span data-ttu-id="51ba9-212">使用 `BookService` 類別來執行 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="51ba9-212">Uses the `BookService` class to perform CRUD operations.</span></span>
    * <span data-ttu-id="51ba9-213">包含動作方法以支援 GET、POST、PUT 與 DELETE HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="51ba9-213">Contains action methods to support GET, POST, PUT, and DELETE HTTP requests.</span></span>
1. <span data-ttu-id="51ba9-214">建置和執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="51ba9-214">Build and run the app.</span></span>
1. <span data-ttu-id="51ba9-215">在您的瀏覽器中瀏覽到 `http://localhost:<port>/api/books`。</span><span class="sxs-lookup"><span data-stu-id="51ba9-215">Navigate to `http://localhost:<port>/api/books` in your browser.</span></span> <span data-ttu-id="51ba9-216">會顯示下列 JSON 回應：</span><span class="sxs-lookup"><span data-stu-id="51ba9-216">The following JSON response is displayed:</span></span>

    ```json
    [
      {
        "id":"5bfd996f7b8e48dc15ff215d",
        "bookName":"Design Patterns",
        "price":54.93,
        "category":"Computers",
        "author":"Ralph Johnson"
      },
      {
        "id":"5bfd996f7b8e48dc15ff215e",
        "bookName":"Clean Code",
        "price":43.15,
        "category":"Computers",
        "author":"Robert C. Martin"
      }
    ]
    ```

## <a name="next-steps"></a><span data-ttu-id="51ba9-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51ba9-217">Next steps</span></span>

<span data-ttu-id="51ba9-218">如需有關建置 ASP.NET Core Web API 的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="51ba9-218">For more information on building ASP.NET Core web APIs, see the following resources:</span></span>

* <xref:web-api/index>
* <xref:web-api/action-return-types>
