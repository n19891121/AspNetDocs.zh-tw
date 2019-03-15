---
title: 在 ASP.NET Core 中使用 Grunt
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2016
uid: client-side/using-grunt
ms.openlocfilehash: 21fa565c930563bbc819c2a02ea71655193513d0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049795"
---
# <a name="use-grunt-in-aspnet-core"></a><span data-ttu-id="06ed2-102">在 ASP.NET Core 中使用 Grunt</span><span class="sxs-lookup"><span data-stu-id="06ed2-102">Use Grunt in ASP.NET Core</span></span>

<span data-ttu-id="06ed2-103">作者：[Noel Rice](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/)</span><span class="sxs-lookup"><span data-stu-id="06ed2-103">By [Noel Rice](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/)</span></span>

<span data-ttu-id="06ed2-104">Grunt 是一個 JavaScript 工作執行器，它會會自動化指令碼縮製、TypeScript 編譯、程式碼品質 "lint" 工具、CSS 前置處理器，以及支援用戶端開發所需的任何重複性工作。</span><span class="sxs-lookup"><span data-stu-id="06ed2-104">Grunt is a JavaScript task runner that automates script minification, TypeScript compilation, code quality "lint" tools, CSS pre-processors, and just about any repetitive chore that needs doing to support client development.</span></span> <span data-ttu-id="06ed2-105">Grunt 在 Visual Studio 中受到完整的支援，雖然 ASP.NET 專案範本預設使用 Gulp (請參閱[使用 Gulp](using-gulp.md))。</span><span class="sxs-lookup"><span data-stu-id="06ed2-105">Grunt is fully supported in Visual Studio, though the ASP.NET project templates use Gulp by default (see [Use Gulp](using-gulp.md)).</span></span>

<span data-ttu-id="06ed2-106">這個範例會使用空的 ASP.NET Core 專案做為起點，展示如何從頭開始自動化用戶端建置程序。</span><span class="sxs-lookup"><span data-stu-id="06ed2-106">This example uses an empty ASP.NET Core project as its starting point, to show how to automate the client build process from scratch.</span></span>

<span data-ttu-id="06ed2-107">完成的範例會清除目標部署目錄、 組合 JavaScript 檔案、 檢查程式碼品質、 壓縮 JavaScript 文件內容和部署到您的網頁應用程式根目錄。</span><span class="sxs-lookup"><span data-stu-id="06ed2-107">The finished example cleans the target deployment directory, combines JavaScript files, checks code quality, condenses JavaScript file content and deploys to the root of your web application.</span></span> <span data-ttu-id="06ed2-108">我們將使用下列套件：</span><span class="sxs-lookup"><span data-stu-id="06ed2-108">We will use the following packages:</span></span>

* <span data-ttu-id="06ed2-109">**grunt**:Grunt 工作執行器套件。</span><span class="sxs-lookup"><span data-stu-id="06ed2-109">**grunt**: The Grunt task runner package.</span></span>

* <span data-ttu-id="06ed2-110">**grunt contrib 清除**:移除檔案或目錄的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="06ed2-110">**grunt-contrib-clean**: A plugin that removes files or directories.</span></span>

* <span data-ttu-id="06ed2-111">**grunt-contrib-jshint**:檢閱 JavaScript 程式碼品質的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="06ed2-111">**grunt-contrib-jshint**: A plugin that reviews JavaScript code quality.</span></span>

* <span data-ttu-id="06ed2-112">**grunt-contrib-concat**:外掛程式聯結成單一檔案的檔案。</span><span class="sxs-lookup"><span data-stu-id="06ed2-112">**grunt-contrib-concat**: A plugin that joins files into a single file.</span></span>

* <span data-ttu-id="06ed2-113">**grunt contrib uglify**:縮短 JavaScript，以減少大小的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="06ed2-113">**grunt-contrib-uglify**: A plugin that minifies JavaScript to reduce size.</span></span>

* <span data-ttu-id="06ed2-114">**grunt-contrib-watch**:監看檔案 」 活動的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="06ed2-114">**grunt-contrib-watch**: A plugin that watches file activity.</span></span>

## <a name="preparing-the-application"></a><span data-ttu-id="06ed2-115">準備應用程式</span><span class="sxs-lookup"><span data-stu-id="06ed2-115">Preparing the application</span></span>

<span data-ttu-id="06ed2-116">若要開始，設定新的空白 web 應用程式並新增 TypeScript 範例檔案。</span><span class="sxs-lookup"><span data-stu-id="06ed2-116">To begin, set up a new empty web application and add TypeScript example files.</span></span> <span data-ttu-id="06ed2-117">TypeScript 檔案會自動編譯成 JavaScript 使用 Visual Studio 的預設設定，因此我們處理使用 Grunt 的原始資料。</span><span class="sxs-lookup"><span data-stu-id="06ed2-117">TypeScript files are automatically compiled into JavaScript using default Visual Studio settings and will be our raw material to process using Grunt.</span></span>

1.  <span data-ttu-id="06ed2-118">在 Visual Studio 中，建立新`ASP.NET Web Application`。</span><span class="sxs-lookup"><span data-stu-id="06ed2-118">In Visual Studio, create a new `ASP.NET Web Application`.</span></span>

2.  <span data-ttu-id="06ed2-119">在 [新增 ASP.NET 專案] 對話方塊中，選取 [ASP.NET Core] **空白**範本，然後按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="06ed2-119">In the **New ASP.NET Project** dialog, select the ASP.NET Core **Empty** template and click the OK button.</span></span>

3.  <span data-ttu-id="06ed2-120">在 [方案總管] 中檢閱專案結構。</span><span class="sxs-lookup"><span data-stu-id="06ed2-120">In the Solution Explorer, review the project structure.</span></span> <span data-ttu-id="06ed2-121">`\src`資料夾包含空`wwwroot`和`Dependencies`節點。</span><span class="sxs-lookup"><span data-stu-id="06ed2-121">The `\src` folder includes empty `wwwroot` and `Dependencies` nodes.</span></span>

    ![空的 web 方案](using-grunt/_static/grunt-solution-explorer.png)

4.  <span data-ttu-id="06ed2-123">加入新的資料夾，名為`TypeScript`到您的專案目錄。</span><span class="sxs-lookup"><span data-stu-id="06ed2-123">Add a new folder named `TypeScript` to your project directory.</span></span>

5.  <span data-ttu-id="06ed2-124">之前新增任何檔案，請確定 Visual Studio 有選項 '編譯儲存' 檢查的 TypeScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="06ed2-124">Before adding any files, make sure that Visual Studio has the option 'compile on save' for TypeScript files checked.</span></span> <span data-ttu-id="06ed2-125">瀏覽至**工具** > **選項** > **文字編輯器** > **Typescript**  > **專案**:</span><span class="sxs-lookup"><span data-stu-id="06ed2-125">Navigate to **Tools** > **Options** > **Text Editor** > **Typescript** > **Project**:</span></span>

    ![設定自動 compliation 的 TypeScript 檔案的選項](using-grunt/_static/typescript-options.png)

6.  <span data-ttu-id="06ed2-127">以滑鼠右鍵按一下 `TypeScript` 目錄，然後從快顯功能表選取 [新增 > 新增項目]。</span><span class="sxs-lookup"><span data-stu-id="06ed2-127">Right-click the `TypeScript` directory and select **Add > New Item** from the context menu.</span></span> <span data-ttu-id="06ed2-128">選取 **JavaScript 檔案**項目，並將檔案命名為 *Tastes.ts* (請注意 \*.ts 副檔名)。</span><span class="sxs-lookup"><span data-stu-id="06ed2-128">Select the **JavaScript file** item and name the file *Tastes.ts* (note the \*.ts extension).</span></span> <span data-ttu-id="06ed2-129">將下面 TypeScript 程式碼行複製到檔案中 (當您儲存時，新 *Tastes.js* 檔案將會隨 JavaScript 原始程式碼出現)。</span><span class="sxs-lookup"><span data-stu-id="06ed2-129">Copy the line of TypeScript code below into the file (when you save, a new *Tastes.js* file will appear with the JavaScript source).</span></span>
    
    ```typescript
    enum Tastes { Sweet, Sour, Salty, Bitter }
    ```

7.  <span data-ttu-id="06ed2-130">第二個將檔案加入至**TypeScript** directory 並將它命名`Food.ts`。</span><span class="sxs-lookup"><span data-stu-id="06ed2-130">Add a second file to the **TypeScript** directory and name it `Food.ts`.</span></span> <span data-ttu-id="06ed2-131">將下列程式碼複製到檔案。</span><span class="sxs-lookup"><span data-stu-id="06ed2-131">Copy the code below into the file.</span></span>

    ```typescript
    class Food {
      constructor(name: string, calories: number) {
        this._name = name;
        this._calories = calories;
      }
    
      private _name: string;
      get Name() {
        return this._name;
      }
    
      private _calories: number;
      get Calories() {
        return this._calories;
      }
    
      private _taste: Tastes;
      get Taste(): Tastes { return this._taste }
      set Taste(value: Tastes) {
        this._taste = value;
      }
    }
    ```

## <a name="configuring-npm"></a><span data-ttu-id="06ed2-132">設定 NPM</span><span class="sxs-lookup"><span data-stu-id="06ed2-132">Configuring NPM</span></span>

<span data-ttu-id="06ed2-133">接著，設定 NPM 以便下載 grunt 與 grunt-tasks。</span><span class="sxs-lookup"><span data-stu-id="06ed2-133">Next, configure NPM to download grunt and grunt-tasks.</span></span>

1. <span data-ttu-id="06ed2-134">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後從快顯功能表選取 [新增 > 新增項目]。</span><span class="sxs-lookup"><span data-stu-id="06ed2-134">In the Solution Explorer, right-click the project and select **Add > New Item** from the context menu.</span></span> <span data-ttu-id="06ed2-135">選取 **NPM 設定檔**項目，保留預設名稱  *package.json*，然後按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="06ed2-135">Select the **NPM configuration file** item, leave the default name, *package.json*, and click the **Add** button.</span></span>

2. <span data-ttu-id="06ed2-136">在  *package.json*檔案，內部`devDependencies`物件大括號中，輸入 「 grunt"。</span><span class="sxs-lookup"><span data-stu-id="06ed2-136">In the *package.json* file, inside the `devDependencies` object braces, enter "grunt".</span></span> <span data-ttu-id="06ed2-137">選取`grunt`從 Intellisense 清單，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="06ed2-137">Select `grunt` from the Intellisense list and press the Enter key.</span></span> <span data-ttu-id="06ed2-138">Visual Studio 會加上引號 grunt 封裝名稱，並加入冒號。</span><span class="sxs-lookup"><span data-stu-id="06ed2-138">Visual Studio will quote the grunt package name, and add a colon.</span></span> <span data-ttu-id="06ed2-139">冒號右邊，請從頂端的 [Intellisense] 清單中選取封裝的最新穩定版本 (按`Ctrl-Space`Intellisense 不會出現)。</span><span class="sxs-lookup"><span data-stu-id="06ed2-139">To the right of the colon, select the latest stable version of the package from the top of the Intellisense list (press `Ctrl-Space` if Intellisense doesn't appear).</span></span>

    ![grun Intellisense](using-grunt/_static/devdependencies-grunt.png)
    
    > [!NOTE]
    > <span data-ttu-id="06ed2-141">使用 NPM[語意版本設定](http://semver.org/)組織相依性。</span><span class="sxs-lookup"><span data-stu-id="06ed2-141">NPM uses [semantic versioning](http://semver.org/) to organize dependencies.</span></span> <span data-ttu-id="06ed2-142">語意版本設定，也就是 SemVer 識別套件的編號配置<major>。<minor>。<patch>.Intellisense 會顯示只有幾個常見的選擇，以簡化語意版本設定。</span><span class="sxs-lookup"><span data-stu-id="06ed2-142">Semantic versioning, also known as SemVer, identifies packages with the numbering scheme <major>.<minor>.<patch>. Intellisense simplifies semantic versioning by showing only a few common choices.</span></span> <span data-ttu-id="06ed2-143">在 [Intellisense] 清單 (在上述範例中的 0.4.5) 頂端的項目會被視為封裝的最新穩定版本。</span><span class="sxs-lookup"><span data-stu-id="06ed2-143">The top item in the Intellisense list (0.4.5 in the example above) is considered the latest stable version of the package.</span></span> <span data-ttu-id="06ed2-144">插入號 (^) 符號符合最新的主要版本和波狀符號 （~） 比對的最新的次要版本。</span><span class="sxs-lookup"><span data-stu-id="06ed2-144">The caret (^) symbol matches the most recent major version and the tilde (~) matches the most recent minor version.</span></span> <span data-ttu-id="06ed2-145">請參閱[NPM semver 版本剖析器參考](https://www.npmjs.com/package/semver)做為 SemVer 提供的完整表現度的指南。</span><span class="sxs-lookup"><span data-stu-id="06ed2-145">See the [NPM semver version parser reference](https://www.npmjs.com/package/semver) as a guide to the full expressivity that SemVer provides.</span></span>

3. <span data-ttu-id="06ed2-146">如下列範例所示，新增更多的相依性以針對 *clean*、*jshint*、*concat*、*uglify* 與 *watch* 載入 grunt-contrib-\* 套件。</span><span class="sxs-lookup"><span data-stu-id="06ed2-146">Add more dependencies to load grunt-contrib-\* packages for *clean*, *jshint*, *concat*, *uglify*, and *watch* as shown in the example below.</span></span> <span data-ttu-id="06ed2-147">版本不需要與範例相符。</span><span class="sxs-lookup"><span data-stu-id="06ed2-147">The versions don't need to match the example.</span></span>

    ```json
    "devDependencies": {
      "grunt": "0.4.5",
      "grunt-contrib-clean": "0.6.0",
      "grunt-contrib-jshint": "0.11.0",
      "grunt-contrib-concat": "0.5.1",
      "grunt-contrib-uglify": "0.8.0",
      "grunt-contrib-watch": "0.6.1"
    }
    ```

4. <span data-ttu-id="06ed2-148">儲存*package.json*檔案。</span><span class="sxs-lookup"><span data-stu-id="06ed2-148">Save the *package.json* file.</span></span>

<span data-ttu-id="06ed2-149">每個 devDependencies 項目的封裝會下載，以及每個封裝所需的任何檔案。</span><span class="sxs-lookup"><span data-stu-id="06ed2-149">The packages for each devDependencies item will download, along with any files that each package requires.</span></span> <span data-ttu-id="06ed2-150">您可以找到套件檔案中的`node_modules`目錄啟用**顯示所有檔案**方案總管 中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="06ed2-150">You can find the package files in the `node_modules` directory by enabling the **Show All Files** button in the Solution Explorer.</span></span>

![grunt node_modules](using-grunt/_static/node-modules.png)

> [!NOTE]
> <span data-ttu-id="06ed2-152">如果需要您可以手動還原相依性，在 [方案總管] 上按一下滑鼠右鍵`Dependencies\NPM`，然後選取**還原套件**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="06ed2-152">If you need to, you can manually restore dependencies in Solution Explorer by right-clicking on `Dependencies\NPM` and selecting the **Restore Packages** menu option.</span></span>

![還原套件](using-grunt/_static/restore-packages.png)

## <a name="configuring-grunt"></a><span data-ttu-id="06ed2-154">設定 Grunt</span><span class="sxs-lookup"><span data-stu-id="06ed2-154">Configuring Grunt</span></span>

<span data-ttu-id="06ed2-155">Grunt 已設定使用名為資訊清單*Gruntfile.js* ，定義、 載入和註冊可以手動執行或執行 Visual Studio 中的事件中的 自動根據設定的工作。</span><span class="sxs-lookup"><span data-stu-id="06ed2-155">Grunt is configured using a manifest named *Gruntfile.js* that defines, loads and registers tasks that can be run manually or configured to run automatically based on events in Visual Studio.</span></span>

1. <span data-ttu-id="06ed2-156">以滑鼠右鍵按一下專案，然後選取 [新增 > 新增項目]。</span><span class="sxs-lookup"><span data-stu-id="06ed2-156">Right-click the project and select **Add > New Item**.</span></span> <span data-ttu-id="06ed2-157">選取 **Grunt 設定檔**選項，保留預設名稱 *Gruntfile.js*，然後按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="06ed2-157">Select the **Grunt Configuration file** option, leave the default name, *Gruntfile.js*, and click the **Add** button.</span></span>

   <span data-ttu-id="06ed2-158">初始程式碼包含模組定義和`grunt.initConfig()`方法。</span><span class="sxs-lookup"><span data-stu-id="06ed2-158">The initial code includes a module definition and the `grunt.initConfig()` method.</span></span> <span data-ttu-id="06ed2-159">`initConfig()`用來設定每一個封裝的選項和模組的其餘部分將會載入並註冊工作。</span><span class="sxs-lookup"><span data-stu-id="06ed2-159">The `initConfig()` is used to set options for each package, and the remainder of the module will load and register tasks.</span></span>
    
   ```javascript
   module.exports = function (grunt) {
     grunt.initConfig({
     });
   };
   ```

2. <span data-ttu-id="06ed2-160">在 `initConfig()` 方法內，加入 `clean` 工作的選項，如下面的 *Gruntfile.js* 範例所示。</span><span class="sxs-lookup"><span data-stu-id="06ed2-160">Inside the `initConfig()` method, add options for the `clean` task as shown in the example *Gruntfile.js* below.</span></span> <span data-ttu-id="06ed2-161">清除工作會接受目錄字串的陣列。</span><span class="sxs-lookup"><span data-stu-id="06ed2-161">The clean task accepts an array of directory strings.</span></span> <span data-ttu-id="06ed2-162">此工作會從 wwwroot/lib 移除檔案，並移除整個 /temp 目錄。</span><span class="sxs-lookup"><span data-stu-id="06ed2-162">This task removes files from wwwroot/lib and removes the entire /temp directory.</span></span>

    ```javascript
    module.exports = function (grunt) {
      grunt.initConfig({
        clean: ["wwwroot/lib/*", "temp/"],
      });
    };
    ```

3. <span data-ttu-id="06ed2-163">在 initConfig() 方法下方，加入對 `grunt.loadNpmTasks()` 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="06ed2-163">Below the initConfig() method, add a call to `grunt.loadNpmTasks()`.</span></span> <span data-ttu-id="06ed2-164">這將使工作可以從 Visual Studio 執行。</span><span class="sxs-lookup"><span data-stu-id="06ed2-164">This will make the task runnable from Visual Studio.</span></span>

    ```javascript
    grunt.loadNpmTasks("grunt-contrib-clean");
    ```

4. <span data-ttu-id="06ed2-165">儲存*Gruntfile.js*。</span><span class="sxs-lookup"><span data-stu-id="06ed2-165">Save *Gruntfile.js*.</span></span> <span data-ttu-id="06ed2-166">檔案看起來應該像下列螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="06ed2-166">The file should look something like the screenshot below.</span></span>

    ![初始的 gruntfile](using-grunt/_static/gruntfile-js-initial.png)

5. <span data-ttu-id="06ed2-168">以滑鼠右鍵按一下*Gruntfile.js* ，然後選取**Task Runner Explorer**從內容功能表。</span><span class="sxs-lookup"><span data-stu-id="06ed2-168">Right-click *Gruntfile.js* and select **Task Runner Explorer** from the context menu.</span></span> <span data-ttu-id="06ed2-169">Task Runner explorer 視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="06ed2-169">The Task Runner Explorer window will open.</span></span>

    ![工作執行器總管功能表](using-grunt/_static/task-runner-explorer-menu.png)

6. <span data-ttu-id="06ed2-171">確認`clean`會顯示在下方**工作**Task Runner explorer 中。</span><span class="sxs-lookup"><span data-stu-id="06ed2-171">Verify that `clean` shows under **Tasks** in the Task Runner Explorer.</span></span>

    ![工作執行器總管工作清單](using-grunt/_static/task-runner-explorer-tasks.png)

7. <span data-ttu-id="06ed2-173">以滑鼠右鍵按一下 「 清除 」 工作，然後選取**執行**從內容功能表。</span><span class="sxs-lookup"><span data-stu-id="06ed2-173">Right-click the clean task and select **Run** from the context menu.</span></span> <span data-ttu-id="06ed2-174">命令視窗會顯示作業進度。</span><span class="sxs-lookup"><span data-stu-id="06ed2-174">A command window displays progress of the task.</span></span>

    ![工作執行器總管 中執行清理工作](using-grunt/_static/task-runner-explorer-run-clean.png)
    
    > [!NOTE]
    > <span data-ttu-id="06ed2-176">沒有任何檔案或目錄將尚未清除。</span><span class="sxs-lookup"><span data-stu-id="06ed2-176">There are no files or directories to clean yet.</span></span> <span data-ttu-id="06ed2-177">如有需要，您可以在 方案總管 中手動建立它們，然後再執行測試的 「 清除 」 工作。</span><span class="sxs-lookup"><span data-stu-id="06ed2-177">If you like, you can manually create them in the Solution Explorer and then run the clean task as a test.</span></span>
    
8. <span data-ttu-id="06ed2-178">在 initConfig() 方法中，新增項目`concat`使用下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="06ed2-178">In the initConfig() method, add an entry for `concat` using the code below.</span></span>

    <span data-ttu-id="06ed2-179">`src`屬性陣列會列出檔案，若要結合，它們應該要結合的順序。</span><span class="sxs-lookup"><span data-stu-id="06ed2-179">The `src` property array lists files to combine, in the order that they should be combined.</span></span> <span data-ttu-id="06ed2-180">`dest`屬性指派給所產生的合併檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="06ed2-180">The `dest` property assigns the path to the combined file that's produced.</span></span>

    ```javascript
    concat: {
      all: {
        src: ['TypeScript/Tastes.js', 'TypeScript/Food.js'],
        dest: 'temp/combined.js'
      }
    },
    ```
    
    > [!NOTE]
    > <span data-ttu-id="06ed2-181">`all`上述程式碼中的屬性為目標的名稱。</span><span class="sxs-lookup"><span data-stu-id="06ed2-181">The `all` property in the code above is the name of a target.</span></span> <span data-ttu-id="06ed2-182">目標用於某些 Grunt 工作，以允許多個組建環境。</span><span class="sxs-lookup"><span data-stu-id="06ed2-182">Targets are used in some Grunt tasks to allow multiple build environments.</span></span> <span data-ttu-id="06ed2-183">您可以檢視使用 Intellisense 的內建的目標，或指派自己。</span><span class="sxs-lookup"><span data-stu-id="06ed2-183">You can view the built-in targets using Intellisense or assign your own.</span></span>
    
9. <span data-ttu-id="06ed2-184">使用下列程式碼新增`jshint`工作。</span><span class="sxs-lookup"><span data-stu-id="06ed2-184">Add the `jshint` task using the code below.</span></span>

    <span data-ttu-id="06ed2-185">對暫存目錄中找到的每個 JavaScript 檔案執行 jshint 程式碼品質公用程式。</span><span class="sxs-lookup"><span data-stu-id="06ed2-185">The jshint code-quality utility is run against every JavaScript file found in the temp directory.</span></span>
    
    ```javascript
    jshint: {
      files: ['temp/*.js'],
      options: {
        '-W069': false,
      }
    },
    ```

    > [!NOTE]
    > <span data-ttu-id="06ed2-186">選項 "-W069" 錯誤是由 jshint 在 JavaScript 使用括號語法來指派屬性而非點標記法 (亦即 `Tastes["Sweet"]`，而非 `Tastes.Sweet`) 時所產生。</span><span class="sxs-lookup"><span data-stu-id="06ed2-186">The option "-W069" is an error produced by jshint when JavaScript uses bracket syntax to assign a property instead of dot notation, i.e. `Tastes["Sweet"]` instead of `Tastes.Sweet`.</span></span> <span data-ttu-id="06ed2-187">此選項會關閉警告，以允許處理序的剩餘部分。</span><span class="sxs-lookup"><span data-stu-id="06ed2-187">The option turns off the warning to allow the rest of the process to continue.</span></span>

10. <span data-ttu-id="06ed2-188">使用下列程式碼新增`uglify`工作。</span><span class="sxs-lookup"><span data-stu-id="06ed2-188">Add the `uglify` task using the code below.</span></span>

    <span data-ttu-id="06ed2-189">工作縮短*combined.js*檔案找到暫存目錄中，並會將結果檔案建立標準的命名慣例的 wwwroot/lib *\<檔案名稱\>。 min.js*.</span><span class="sxs-lookup"><span data-stu-id="06ed2-189">The task minifies the *combined.js* file found in the temp directory and creates the result file in wwwroot/lib following the standard naming convention *\<file name\>.min.js*.</span></span>
    
    ```javascript
    uglify: {
     all: {
       src: ['temp/combined.js'],
       dest: 'wwwroot/lib/combined.min.js'
     }
    },
    ```

11. <span data-ttu-id="06ed2-190">在載入 grunt contrib 清除呼叫 grunt.loadNpmTasks()，包括 jshint，concat 的相同呼叫和 uglify 使用下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="06ed2-190">Under the call grunt.loadNpmTasks() that loads grunt-contrib-clean, include the same call for jshint, concat and uglify using the code below.</span></span>
    
    ```javascript
    grunt.loadNpmTasks('grunt-contrib-jshint');
    grunt.loadNpmTasks('grunt-contrib-concat');
    grunt.loadNpmTasks('grunt-contrib-uglify');
    ```

12. <span data-ttu-id="06ed2-191">儲存*Gruntfile.js*。</span><span class="sxs-lookup"><span data-stu-id="06ed2-191">Save *Gruntfile.js*.</span></span> <span data-ttu-id="06ed2-192">檔案看起來應該像下面範例。</span><span class="sxs-lookup"><span data-stu-id="06ed2-192">The file should look something like the example below.</span></span>

    ![完整的 grunt 檔案範例](using-grunt/_static/gruntfile-js-complete.png)

13. <span data-ttu-id="06ed2-194">請注意，包含工作執行器總管工作清單`clean`， `concat`，`jshint`和`uglify`工作。</span><span class="sxs-lookup"><span data-stu-id="06ed2-194">Notice that the Task Runner Explorer Tasks list includes `clean`, `concat`, `jshint` and `uglify` tasks.</span></span> <span data-ttu-id="06ed2-195">順序執行每項工作，並觀察 [方案總管] 中的結果。</span><span class="sxs-lookup"><span data-stu-id="06ed2-195">Run each task in order and observe the results in Solution Explorer.</span></span> <span data-ttu-id="06ed2-196">每個工作應該執行無誤。</span><span class="sxs-lookup"><span data-stu-id="06ed2-196">Each task should run without errors.</span></span>
    
    ![執行每項工作的工作執行器總管](using-grunt/_static/task-runner-explorer-run-each-task.png)
    
    <span data-ttu-id="06ed2-198">Concat 工作建立新*combined.js*檔案，並將它放入暫存目錄。</span><span class="sxs-lookup"><span data-stu-id="06ed2-198">The concat task creates a new *combined.js* file and places it into the temp directory.</span></span> <span data-ttu-id="06ed2-199">Jshint 工作只會執行，並不會產生輸出。</span><span class="sxs-lookup"><span data-stu-id="06ed2-199">The jshint task simply runs and doesn't produce output.</span></span> <span data-ttu-id="06ed2-200">Uglify 工作建立新*combined.min.js*檔案，並將它放入 wwwroot/lib。</span><span class="sxs-lookup"><span data-stu-id="06ed2-200">The uglify task creates a new *combined.min.js* file and places it into wwwroot/lib.</span></span> <span data-ttu-id="06ed2-201">完成時，方案應該看起來像下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="06ed2-201">On completion, the solution should look something like the screenshot below:</span></span>
    
    ![方案總管 中的所有工作](using-grunt/_static/solution-explorer-after-all-tasks.png)
    
    > [!NOTE]
    > <span data-ttu-id="06ed2-203">如需有關每個套件的選項的詳細資訊，請瀏覽[ https://www.npmjs.com/ ](https://www.npmjs.com/)和查閱的主頁面上的 [搜尋] 方塊中的封裝名稱。</span><span class="sxs-lookup"><span data-stu-id="06ed2-203">For more information on the options for each package, visit [https://www.npmjs.com/](https://www.npmjs.com/) and lookup the package name in the search box on the main page.</span></span> <span data-ttu-id="06ed2-204">例如，您可以查閱 grunt contrib 清除封裝，以取得說明的所有參數的文件連結。</span><span class="sxs-lookup"><span data-stu-id="06ed2-204">For example, you can look up the grunt-contrib-clean package to get a documentation link that explains all of its parameters.</span></span>

### <a name="all-together-now"></a><span data-ttu-id="06ed2-205">整合所有工作</span><span class="sxs-lookup"><span data-stu-id="06ed2-205">All together now</span></span>

<span data-ttu-id="06ed2-206">使用 Grunt`registerTask()`方法，以特定順序執行一系列的工作。</span><span class="sxs-lookup"><span data-stu-id="06ed2-206">Use the Grunt `registerTask()` method to run a series of tasks in a particular sequence.</span></span> <span data-ttu-id="06ed2-207">例如，若要執行上述步驟中全新的順序]-> [範例 concat]-> [jshint]-> [uglify、 將下列程式碼新增至模組。</span><span class="sxs-lookup"><span data-stu-id="06ed2-207">For example, to run the example steps above in the order clean -> concat -> jshint -> uglify, add the code below to the module.</span></span> <span data-ttu-id="06ed2-208">程式碼應該將外部 initConfig loadNpmTasks() 呼叫相同的層級。</span><span class="sxs-lookup"><span data-stu-id="06ed2-208">The code should be added to the same level as the loadNpmTasks() calls, outside initConfig.</span></span>

```javascript
grunt.registerTask("all", ['clean', 'concat', 'jshint', 'uglify']);
```

<span data-ttu-id="06ed2-209">在 [別名工作] 下的 [Task Runner explorer] 中出現新的工作。</span><span class="sxs-lookup"><span data-stu-id="06ed2-209">The new task shows up in Task Runner Explorer under Alias Tasks.</span></span> <span data-ttu-id="06ed2-210">您可以以滑鼠右鍵按一下，並執行它，就像其他工作一樣。</span><span class="sxs-lookup"><span data-stu-id="06ed2-210">You can right-click and run it just as you would other tasks.</span></span> <span data-ttu-id="06ed2-211">`all`工作會執行`clean`， `concat`，`jshint`和`uglify`，順序。</span><span class="sxs-lookup"><span data-stu-id="06ed2-211">The `all` task will run `clean`, `concat`, `jshint` and `uglify`, in order.</span></span>

![別名 grunt 工作](using-grunt/_static/alias-tasks.png)

## <a name="watching-for-changes"></a><span data-ttu-id="06ed2-213">監看變更</span><span class="sxs-lookup"><span data-stu-id="06ed2-213">Watching for changes</span></span>

<span data-ttu-id="06ed2-214">A`watch`工作會監看檔案和目錄上的。</span><span class="sxs-lookup"><span data-stu-id="06ed2-214">A `watch` task keeps an eye on files and directories.</span></span> <span data-ttu-id="06ed2-215">監看式自動觸發的工作，偵測到變更時。</span><span class="sxs-lookup"><span data-stu-id="06ed2-215">The watch triggers tasks automatically if it detects changes.</span></span> <span data-ttu-id="06ed2-216">將以下的程式碼新增至監看變更 initConfig \*TypeScript 目錄中的.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="06ed2-216">Add the code below to initConfig to watch for changes to \*.js files in the TypeScript directory.</span></span> <span data-ttu-id="06ed2-217">如果 JavaScript 檔案變更時，`watch`將會執行`all`工作。</span><span class="sxs-lookup"><span data-stu-id="06ed2-217">If a JavaScript file is changed, `watch` will run the `all` task.</span></span>

```javascript
watch: {
  files: ["TypeScript/*.js"],
  tasks: ["all"]
}
```

<span data-ttu-id="06ed2-218">將呼叫加入`loadNpmTasks()`以顯示`watch`Task Runner explorer 中的工作。</span><span class="sxs-lookup"><span data-stu-id="06ed2-218">Add a call to `loadNpmTasks()` to show the `watch` task in Task Runner Explorer.</span></span>

```javascript
grunt.loadNpmTasks('grunt-contrib-watch');
```

<span data-ttu-id="06ed2-219">以滑鼠右鍵按一下 Task Runner explorer 中的監看式項工作，並從操作功能表中選取 執行。</span><span class="sxs-lookup"><span data-stu-id="06ed2-219">Right-click the watch task in Task Runner Explorer and select Run from the context menu.</span></span> <span data-ttu-id="06ed2-220">顯示 監看式工作執行的命令視窗會顯示 等候訊息。</span><span class="sxs-lookup"><span data-stu-id="06ed2-220">The command window that shows the watch task running will display a "Waiting…" message.</span></span> <span data-ttu-id="06ed2-221">開啟 TypeScript 檔案的其中一個，加上空格，並儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="06ed2-221">Open one of the TypeScript files, add a space, and then save the file.</span></span> <span data-ttu-id="06ed2-222">這會觸發監看式工作，並觸發其他工作順序執行。</span><span class="sxs-lookup"><span data-stu-id="06ed2-222">This will trigger the watch task and trigger the other tasks to run in order.</span></span> <span data-ttu-id="06ed2-223">以下螢幕擷取畫面顯示執行範例。</span><span class="sxs-lookup"><span data-stu-id="06ed2-223">The screenshot below shows a sample run.</span></span>

![執行工作輸出](using-grunt/_static/watch-running.png)

## <a name="binding-to-visual-studio-events"></a><span data-ttu-id="06ed2-225">繫結至 Visual Studio 事件</span><span class="sxs-lookup"><span data-stu-id="06ed2-225">Binding to Visual Studio events</span></span>

<span data-ttu-id="06ed2-226">除非您想要以手動方式啟動您的工作，每次您在 Visual Studio 中工作時，您可以繫結到工作**再建置**，**之後建置**，**清除**，和**專案開啟**事件。</span><span class="sxs-lookup"><span data-stu-id="06ed2-226">Unless you want to manually start your tasks every time you work in Visual Studio, you can bind tasks to **Before Build**, **After Build**, **Clean**, and **Project Open** events.</span></span>

<span data-ttu-id="06ed2-227">讓我們繫結`watch`使其執行每次 Visual Studio 隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="06ed2-227">Let’s bind `watch` so that it runs every time Visual Studio opens.</span></span> <span data-ttu-id="06ed2-228">在 Task Runner explorer 中，以滑鼠右鍵按一下 監看式工作，然後選取**繫結 > 專案開啟**從內容功能表。</span><span class="sxs-lookup"><span data-stu-id="06ed2-228">In Task Runner Explorer, right-click the watch task and select **Bindings > Project Open** from the context menu.</span></span>

![繫結至專案開啟的工作](using-grunt/_static/bindings-project-open.png)

<span data-ttu-id="06ed2-230">卸載並重新載入專案。</span><span class="sxs-lookup"><span data-stu-id="06ed2-230">Unload and reload the project.</span></span> <span data-ttu-id="06ed2-231">當專案重新載入時，監看式工作就會開始自動執行。</span><span class="sxs-lookup"><span data-stu-id="06ed2-231">When the project loads again, the watch task will start running automatically.</span></span>

## <a name="summary"></a><span data-ttu-id="06ed2-232">總結</span><span class="sxs-lookup"><span data-stu-id="06ed2-232">Summary</span></span>

<span data-ttu-id="06ed2-233">Grunt 是功能強大的工作執行器，可用來將大部分的用戶端組建工作自動化。</span><span class="sxs-lookup"><span data-stu-id="06ed2-233">Grunt is a powerful task runner that can be used to automate most client-build tasks.</span></span> <span data-ttu-id="06ed2-234">Grunt 運用 NPM 提供其套件和工具與 Visual Studio 整合的功能。</span><span class="sxs-lookup"><span data-stu-id="06ed2-234">Grunt leverages NPM to deliver its packages, and features tooling integration with Visual Studio.</span></span> <span data-ttu-id="06ed2-235">Visual Studio 的 Task Runner explorer 會偵測到組態檔的變更，並提供方便的介面，以執行工作、 檢視執行中的工作，並將工作繫結至 Visual Studio 事件。</span><span class="sxs-lookup"><span data-stu-id="06ed2-235">Visual Studio's Task Runner Explorer detects changes to configuration files and provides a convenient interface to run tasks, view running tasks, and bind tasks to Visual Studio events.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="06ed2-236">其他資源</span><span class="sxs-lookup"><span data-stu-id="06ed2-236">Additional resources</span></span>

   * [<span data-ttu-id="06ed2-237">使用 Gulp</span><span class="sxs-lookup"><span data-stu-id="06ed2-237">Use Gulp</span></span>](using-gulp.md)
