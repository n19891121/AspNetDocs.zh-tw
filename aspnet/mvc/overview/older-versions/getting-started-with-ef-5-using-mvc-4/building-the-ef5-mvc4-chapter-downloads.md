---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: 建立 EF 5 MVC 4 的章節下載教學課程 |Microsoft Docs
author: Rick-Anderson
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 來建立 ASP.NET MVC 4 應用程式 .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 0e3db273d43fef6956c07a5340eb9aa1d1425d59
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2021
ms.locfileid: "99985124"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a><span data-ttu-id="5182d-103">建立 EF 5 MVC 4 教學課程的章節下載</span><span class="sxs-lookup"><span data-stu-id="5182d-103">Building the Chapter Downloads for the EF 5 MVC 4 Tutorials</span></span>

<span data-ttu-id="5182d-104">依 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="5182d-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="5182d-105">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5182d-105">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="5182d-106">如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="5182d-106">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

## <a name="building-the-chapter-downloads"></a><span data-ttu-id="5182d-107">建置章節下載</span><span class="sxs-lookup"><span data-stu-id="5182d-107">Building the Chapter Downloads</span></span>

1. <span data-ttu-id="5182d-108">下載並解壓縮專案範例壓縮檔案。</span><span class="sxs-lookup"><span data-stu-id="5182d-108">Download and unzip the  project sample zip file.</span></span> <span data-ttu-id="5182d-109">在解壓縮的下載封裝中，您會發現其他的 zip 檔案，每個章節都有一個壓縮檔。</span><span class="sxs-lookup"><span data-stu-id="5182d-109">In the unzipped download package, you will find additional zip files, one for the completion of each chapter.</span></span>
2. <span data-ttu-id="5182d-110">以滑鼠右鍵按一下所需的 zip 檔案，按一下 [ **屬性**]，然後按一下 [ **解除封鎖** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5182d-110">Right click on the desired zip file, click **Properties**, and click the **Unblock** button.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. <span data-ttu-id="5182d-111">將檔案解壓縮。</span><span class="sxs-lookup"><span data-stu-id="5182d-111">Unzip the file.</span></span>
4. <span data-ttu-id="5182d-112">按兩下 *CUx .sln* 檔案以啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="5182d-112">Double-click the *CUx.sln* file to launch Visual Studio.</span></span>
5. <span data-ttu-id="5182d-113">從 [ **工具** ] 功能表中，按一下 [ **NuGet 封裝管理員**]，然後 **封裝管理員主控台**。</span><span class="sxs-lookup"><span data-stu-id="5182d-113">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. <span data-ttu-id="5182d-114">在封裝管理員主控台 (PMC) 中，按一下 [ **還原**]。</span><span class="sxs-lookup"><span data-stu-id="5182d-114">In the Package Manager Console (PMC), click **Restore**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. <span data-ttu-id="5182d-115">結束 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="5182d-115">Exit Visual Studio.</span></span>
8. <span data-ttu-id="5182d-116">重新開機 Visual Studio，開啟您在上述步驟中關閉的方案檔。</span><span class="sxs-lookup"><span data-stu-id="5182d-116">Restart Visual Studio, opening the solution file you closed in the step above.</span></span>
9. <span data-ttu-id="5182d-117">在封裝管理員主控台中 (PMC) 上，輸入 `Update-Database` 下列命令：</span><span class="sxs-lookup"><span data-stu-id="5182d-117">In the Package Manager Console (PMC), enter the `Update-Database` command:</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > <span data-ttu-id="5182d-118">如果您收到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="5182d-118">If you get the following error:</span></span>  
    >   
    >  <span data-ttu-id="5182d-119">*「更新資料庫」一詞無法辨識為 Cmdlet、函式、指令檔或可操作程式的名稱。請檢查名稱的拼寫是否正確，如果包含路徑的話，請確認路徑是否正確，然後再試一次。*</span><span class="sxs-lookup"><span data-stu-id="5182d-119">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*</span></span>  
    > <span data-ttu-id="5182d-120">結束並重新啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="5182d-120">Exit and restart Visual Studio.</span></span>

    <span data-ttu-id="5182d-121">每個遷移都會執行，然後會執行種子方法。</span><span class="sxs-lookup"><span data-stu-id="5182d-121">Each migration will run, then the seed method will run.</span></span> <span data-ttu-id="5182d-122">您現在可以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5182d-122">You can now run the app.</span></span>

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> <span data-ttu-id="5182d-123">[[上一步]](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="5182d-123">[Previous](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span></span>
