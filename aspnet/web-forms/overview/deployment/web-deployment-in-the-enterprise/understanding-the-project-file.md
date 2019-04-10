---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
title: 了解專案檔 |Microsoft Docs
author: jrjlee
description: Microsoft Build Engine (MSBuild) 專案檔之間的組建和部署程序的核心。 本主題開頭的 MSBuild 概觀為...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 07978d9d-341c-4524-bcba-62976f390f77
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
msc.type: authoredcontent
ms.openlocfilehash: d774a8e13e108d1be4c39e1e909d3d9683968a0d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59404919"
---
# <a name="understanding-the-project-file"></a><span data-ttu-id="2f0a2-104">了解專案檔</span><span class="sxs-lookup"><span data-stu-id="2f0a2-104">Understanding the Project File</span></span>

<span data-ttu-id="2f0a2-105">藉由[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="2f0a2-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="2f0a2-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="2f0a2-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="2f0a2-107">Microsoft Build Engine (MSBuild) 專案檔之間的組建和部署程序的核心。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-107">Microsoft Build Engine (MSBuild) project files lie at the heart of the build and deployment process.</span></span> <span data-ttu-id="2f0a2-108">本主題開頭的 MSBuild 和專案檔案的概念性概觀。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-108">This topic starts with a conceptual overview of MSBuild and the project file.</span></span> <span data-ttu-id="2f0a2-109">它會描述當您使用專案檔和它的運作方式說明如何使用專案檔，以及在部署真實世界應用程式的範例將會遇到的重要元件。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-109">It describes the key components you'll come across when you work with project files, and it works through an example of how you can use project files to deploy real-world applications.</span></span>
> 
> <span data-ttu-id="2f0a2-110">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="2f0a2-110">What you'll learn:</span></span>
> 
> - <span data-ttu-id="2f0a2-111">如何 MSBuild 會使用 MSBuild 專案檔來建置專案。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-111">How MSBuild uses MSBuild project files to build projects.</span></span>
> - <span data-ttu-id="2f0a2-112">如何 MSBuild 整合與部署技術，例如 Internet Information Services (IIS) Web Deployment Tool (Web Deploy)。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-112">How MSBuild integrates with deployment technologies, like the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span>
> - <span data-ttu-id="2f0a2-113">如何了解專案檔的重要元件。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-113">How to understand the key components of a project file.</span></span>
> - <span data-ttu-id="2f0a2-114">您如何也可以使用專案檔建置及部署複雜的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-114">How you can use project files to build and deploy complex applications.</span></span>


## <a name="msbuild-and-the-project-file"></a><span data-ttu-id="2f0a2-115">MSBuild 和專案檔</span><span class="sxs-lookup"><span data-stu-id="2f0a2-115">MSBuild and the Project File</span></span>

<span data-ttu-id="2f0a2-116">當您建立並在 Visual Studio 中建置解決方案時，Visual Studio 會使用 MSBuild 來建置您的方案中的每個專案。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-116">When you create and build solutions in Visual Studio, Visual Studio uses MSBuild to build each project in your solution.</span></span> <span data-ttu-id="2f0a2-117">每個 Visual Studio 專案包含 MSBuild 專案檔，以反映的專案類型的副檔名&#x2014;，例如 C# 專案 (.csproj)、 Visual Basic.NET 專案 (.vbproj) 或資料庫專案 (.dbproj)。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-117">Every Visual Studio project includes an MSBuild project file, with a file extension that reflects the type of project&#x2014;for example, a C# project (.csproj), a Visual Basic.NET project (.vbproj), or a database project (.dbproj).</span></span> <span data-ttu-id="2f0a2-118">若要建置專案時，MSBuild 必須處理與專案相關聯的專案檔。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-118">In order to build a project, MSBuild must process the project file associated with the project.</span></span> <span data-ttu-id="2f0a2-119">專案檔是 XML 文件，其中包含所有資訊和指示 MSBuild 需要以建置專案，若要加入，平台需求、 版本設定資訊、 web 伺服器或資料庫伺服器設定，內容和必須執行的工作。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-119">The project file is an XML document that contains all the information and instructions that MSBuild needs in order to build your project, like the content to include, the platform requirements, versioning information, web server or database server settings, and the tasks that must be performed.</span></span>

<span data-ttu-id="2f0a2-120">MSBuild 專案檔根據[MSBuild XML 結構描述](https://msdn.microsoft.com/library/5dy88c2e.aspx)，並因此建置程序是完全開放且透明。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-120">MSBuild project files are based on the [MSBuild XML schema](https://msdn.microsoft.com/library/5dy88c2e.aspx), and as a result the build process is entirely open and transparent.</span></span> <span data-ttu-id="2f0a2-121">此外，您不需要安裝 Visual Studio 才能使用 MSBuild 引擎&#x2014;MSBuild.exe 的可執行檔是.NET framework 的一部分，而且您就可以從命令提示字元執行它。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-121">In addition, you don't need to install Visual Studio in order to use the MSBuild engine&#x2014;the MSBuild.exe executable is part of the .NET Framework, and you can run it from a command prompt.</span></span> <span data-ttu-id="2f0a2-122">身為開發人員，您可以製作您自己的 MSBuild 專案檔，使用 MSBuild XML 結構描述強加精密且更精細控制如何建置及部署您的專案。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-122">As a developer, you can craft your own MSBuild project files, using the MSBuild XML schema, to impose sophisticated and fine-grained control over how your projects are built and deployed.</span></span> <span data-ttu-id="2f0a2-123">這些自訂的專案檔在 Visual Studio 會自動產生的專案檔案完全相同的方式。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-123">These custom project files work in exactly the same way as the project files that Visual Studio generates automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="2f0a2-124">您也可以使用與 Team Build 的服務在 Team Foundation Server (TFS) 中的 MSBuild 專案檔。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-124">You can also use MSBuild project files with the Team Build service in Team Foundation Server (TFS).</span></span> <span data-ttu-id="2f0a2-125">例如，您可以使用持續整合 (CI) 案例中的專案檔案來自動化部署到測試環境，當新的程式碼簽入。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-125">For example, you can use project files in continuous integration (CI) scenarios to automate deployment to a test environment when new code is checked in.</span></span> <span data-ttu-id="2f0a2-126">如需詳細資訊，請參閱 <<c0> [ 自動化 Web 部署設定 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-126">For more information, see [Configuring Team Foundation Server for Automated Web Deployment](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span></span>


### <a name="project-file-naming-conventions"></a><span data-ttu-id="2f0a2-127">專案檔命名慣例</span><span class="sxs-lookup"><span data-stu-id="2f0a2-127">Project File Naming Conventions</span></span>

<span data-ttu-id="2f0a2-128">當您建立您自己的專案檔時，您可以使用任何您喜歡的副檔名。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-128">When you create your own project files, you can use any file extension you like.</span></span> <span data-ttu-id="2f0a2-129">不過，若要簡化您的解決方案供其他人了解，您應該使用這些常見的慣例：</span><span class="sxs-lookup"><span data-stu-id="2f0a2-129">However, to make your solutions easier for others to understand, you should use these common conventions:</span></span>

- <span data-ttu-id="2f0a2-130">當您建立專案檔來建置專案時，請使用.proj 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-130">Use the .proj extension when you create a project file that builds projects.</span></span>
- <span data-ttu-id="2f0a2-131">當您建立可重複使用的專案檔匯入至其他專案檔案時，請使用.targets 副檔名。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-131">Use the .targets extension when you create a reusable project file to import into other project files.</span></span> <span data-ttu-id="2f0a2-132">副檔名為.targets 檔案通常不建立任何項目本身，它們只包含您可以匯入至.proj 檔案的指示。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-132">Files with a .targets extension typically don't build anything themselves, they simply contain instructions that you can import into your .proj files.</span></span>

### <a name="integration-with-deployment-technologies"></a><span data-ttu-id="2f0a2-133">與部署技術的整合</span><span class="sxs-lookup"><span data-stu-id="2f0a2-133">Integration with Deployment Technologies</span></span>

<span data-ttu-id="2f0a2-134">如果您先前曾經使用 web 應用程式專案，在 Visual Studio 2010 中，例如 ASP.NET web 應用程式和 ASP.NET MVC web 應用程式，就會知道這些專案包含封裝和部署至目標環境的 web 應用程式的內建支援。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-134">If you've worked with web application projects in Visual Studio 2010, like ASP.NET web applications and ASP.NET MVC web applications, you'll know that these projects include built-in support for packaging and deploying the web application to a target environment.</span></span> <span data-ttu-id="2f0a2-135">**屬性**頁面包含這些專案**封裝/發行 Web**和**封裝/發行 SQL**索引標籤可供您設定如何組成您封裝及部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-135">The **Properties** pages for these projects include **Package/Publish Web** and **Package/Publish SQL** tabs that you can use to configure how the components of your application are packaged and deployed.</span></span> <span data-ttu-id="2f0a2-136">這會顯示**封裝/發行 Web**  索引標籤：</span><span class="sxs-lookup"><span data-stu-id="2f0a2-136">This shows the **Package/Publish Web** tab:</span></span>

![](understanding-the-project-file/_static/image1.png)

<span data-ttu-id="2f0a2-137">這些功能的基礎技術稱為做為 Web 發行管線 (WPP)。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-137">The underlying technology behind these capabilities is known as the Web Publishing Pipeline (WPP).</span></span> <span data-ttu-id="2f0a2-138">WPP 基本上會將 MSBuild 與[Web Deploy](https://go.microsoft.com/?linkid=9805122)一起，以提供完整的建置、 封裝及部署程序，為 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-138">The WPP essentially brings MSBuild and [Web Deploy](https://go.microsoft.com/?linkid=9805122) together to provide a complete build, package, and deployment process for your web applications.</span></span>

<span data-ttu-id="2f0a2-139">好消息是，您可以利用 WPP 提供當您建立 web 專案的自訂專案檔案的整合點。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-139">The good news is that you can take advantage of the integration points that the WPP provides when you create custom project files for web projects.</span></span> <span data-ttu-id="2f0a2-140">您可以在專案檔案中，可讓您建置專案、 建立 web 部署套件，並透過單一的專案檔和 MSBuild 的單一呼叫，在遠端伺服器上安裝這些套件包含部署指示。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-140">You can include deployment instructions in your project file, which allows you to build your projects, create web deployment packages, and install these packages on remote servers through a single project file and a single call to MSBuild.</span></span> <span data-ttu-id="2f0a2-141">您也可以呼叫任何其他可執行檔做為建置流程的一部分。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-141">You can also call any other executables as part of your build process.</span></span> <span data-ttu-id="2f0a2-142">例如，您可以執行 VSDBCMD.exe 命令列工具，從部署資料庫結構描述檔案。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-142">For example, you can run the VSDBCMD.exe command-line tool to deploy a database from a schema file.</span></span> <span data-ttu-id="2f0a2-143">在本主題的過程中，您會看到如何使用這些功能，以符合您企業的部署案例的需求的利用。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-143">Over the course of this topic, you'll see how you can take advantage of these capabilities to meet the requirements of your enterprise deployment scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="2f0a2-144">如需有關 web 應用程式部署程序的運作方式的詳細資訊，請參閱 < [ASP.NET Web 應用程式專案部署概觀](https://msdn.microsoft.com/library/dd394698.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-144">For more information on how the web application deployment process works, see [ASP.NET Web Application Project Deployment Overview](https://msdn.microsoft.com/library/dd394698.aspx).</span></span>


## <a name="the-anatomy-of-a-project-file"></a><span data-ttu-id="2f0a2-145">專案檔的結構</span><span class="sxs-lookup"><span data-stu-id="2f0a2-145">The Anatomy of a Project File</span></span>

<span data-ttu-id="2f0a2-146">您查看更詳細地建置處理序之前，倒是值得花一些時間才能熟悉 MSBuild 專案檔的基本結構。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-146">Before you look at the build process in more detail, it's worth taking a few moments to familiarize yourself with the basic structure of an MSBuild project file.</span></span> <span data-ttu-id="2f0a2-147">本節概述時檢閱、 編輯或建立的專案檔，將會遇到的常見項目。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-147">This section provides an overview of the more common elements that you'll encounter when you review, edit, or create a project file.</span></span> <span data-ttu-id="2f0a2-148">特別是，您將了解：</span><span class="sxs-lookup"><span data-stu-id="2f0a2-148">In particular, you'll learn:</span></span>

- <span data-ttu-id="2f0a2-149">如何使用*屬性*管理建置程序的變數。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-149">How to use *properties* to manage variables for the build process.</span></span>
- <span data-ttu-id="2f0a2-150">如何使用*項目*找出建置處理序的輸入，例如程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-150">How to use *items* to identify the inputs to the build process, like code files.</span></span>
- <span data-ttu-id="2f0a2-151">如何使用*目標*並*工作*以提供執行指示 msbuild，使用*屬性*和*項目*中其他地方定義專案檔中。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-151">How to use *targets* and *tasks* to provide execution instructions to MSBuild, using *properties* and *items* defined elsewhere in the project file.</span></span>

<span data-ttu-id="2f0a2-152">這會顯示在 MSBuild 專案檔中的索引鍵項目之間的關聯性：</span><span class="sxs-lookup"><span data-stu-id="2f0a2-152">This shows the relationship between the key elements in an MSBuild project file:</span></span>

![](understanding-the-project-file/_static/image2.png)

### <a name="the-project-element"></a><span data-ttu-id="2f0a2-153">專案項目</span><span class="sxs-lookup"><span data-stu-id="2f0a2-153">The Project Element</span></span>

<span data-ttu-id="2f0a2-154">[專案](https://msdn.microsoft.com/library/bcxfsh87.aspx)項目是每個專案檔的根項目。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-154">The [Project](https://msdn.microsoft.com/library/bcxfsh87.aspx) element is the root element of every project file.</span></span> <span data-ttu-id="2f0a2-155">除了找出專案檔的 XML 結構描述**專案**元素可以包含屬性，以指定進入點，供建置程序。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-155">In addition to identifying the XML schema for the project file, the **Project** element can include attributes to specify the entry points for the build process.</span></span> <span data-ttu-id="2f0a2-156">例如，在[連絡管理員範例解決方案](the-contact-manager-solution.md)，則*Publish.proj*檔案會指定開始組建時，應該先呼叫名為目標**FullPublish**。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-156">For example, in the [Contact Manager sample solution](the-contact-manager-solution.md), the *Publish.proj* file specifies that the build should start by calling the target named **FullPublish**.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample1.xml)]


### <a name="properties-and-conditions"></a><span data-ttu-id="2f0a2-157">屬性和條件</span><span class="sxs-lookup"><span data-stu-id="2f0a2-157">Properties and Conditions</span></span>

<span data-ttu-id="2f0a2-158">通常需要提供許多不同的功能，才能成功建置及部署您的專案資訊的專案檔。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-158">A project file typically needs to provide lots of different pieces of information in order to successfully build and deploy your projects.</span></span> <span data-ttu-id="2f0a2-159">這項資訊可能包括伺服器名稱、 連接字串、 認證、 組建組態、 來源和目的地檔案路徑，以及任何其他您想要包含支援自訂的資訊。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-159">These pieces of information could include server names, connection strings, credentials, build configurations, source and destination file paths, and any other information you want to include to support customization.</span></span> <span data-ttu-id="2f0a2-160">在專案檔中，屬性必須定義內[PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx)項目。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-160">In a project file, properties must be defined within a [PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx) element.</span></span> <span data-ttu-id="2f0a2-161">MSBuild 屬性是由索引鍵-值配對所組成。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-161">MSBuild properties consist of key-value pairs.</span></span> <span data-ttu-id="2f0a2-162">內**PropertyGroup**項目，項目名稱會定義屬性索引鍵和項目的內容定義的屬性值。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-162">Within the **PropertyGroup** element, the element name defines the property key and the content of the element defines the property value.</span></span> <span data-ttu-id="2f0a2-163">例如，您可以在其中定義具名的屬性**ServerName**並**ConnectionString**儲存靜態的伺服器名稱和連接字串。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-163">For example, you could define properties named **ServerName** and **ConnectionString** to store a static server name and connection string.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample2.xml)]


<span data-ttu-id="2f0a2-164">若要擷取的屬性值，您可以使用格式 \*\*$(***PropertyName***) \* \* *。*</span><span class="sxs-lookup"><span data-stu-id="2f0a2-164">To retrieve a property value, you use the format \**$(***PropertyName***)\*\*\*.*</span></span> <span data-ttu-id="2f0a2-165">例如，若要擷取的值**ServerName**屬性，您會輸入：</span><span class="sxs-lookup"><span data-stu-id="2f0a2-165">For example, to retrieve the value of the **ServerName** property, you would type:</span></span>


[!code-powershell[Main](understanding-the-project-file/samples/sample3.ps1)]


> [!NOTE]
> <span data-ttu-id="2f0a2-166">您會看到如何的範例，以及何時使用本主題稍後的屬性值。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-166">You'll see examples of how and when to use property values later in this topic.</span></span>


<span data-ttu-id="2f0a2-167">在專案檔中內嵌為靜態屬性的資訊不一定理想的方式，來管理建置程序。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-167">Embedding information as static properties in a project file is not always the ideal approach to managing the build process.</span></span> <span data-ttu-id="2f0a2-168">在許多案例中，您會想要從其他來源取得資訊，或讓使用者提供的資訊，從命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-168">In a lot of scenarios, you'll want to obtain the information from other sources or empower the user to provide the information from the command prompt.</span></span> <span data-ttu-id="2f0a2-169">MSBuild 可讓您指定做為命令列參數的任何屬性值。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-169">MSBuild allows you to specify any property value as a command-line parameter.</span></span> <span data-ttu-id="2f0a2-170">例如，使用者無法提供值給**ServerName**當他或她 MSBuild.exe 從命令列執行。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-170">For example, the user could provide a value for **ServerName** when he or she runs MSBuild.exe from the command line.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample4.cmd)]


> [!NOTE]
> <span data-ttu-id="2f0a2-171">如需有關引數和參數可以搭配 MSBuild.exe 使用的詳細資訊，請參閱 < [MSBuild 命令列參考](https://msdn.microsoft.com/library/ms164311.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-171">For more information on the arguments and switches you can use with MSBuild.exe, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>


<span data-ttu-id="2f0a2-172">您可以使用相同的屬性語法以取得環境變數和內建的專案屬性的值。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-172">You can use the same property syntax to obtain the values of environment variables and built-in project properties.</span></span> <span data-ttu-id="2f0a2-173">針對您所定義的許多常用的屬性，您可以在您的專案檔中使用它們，包含相關的參數名稱。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-173">Lots of commonly used properties are defined for you, and you can use them in your project files by including the relevant parameter name.</span></span> <span data-ttu-id="2f0a2-174">例如，若要擷取目前的專案平台&#x2014;，例如**x86**或**AnyCpu**&#x2014;您可以包含 **$ （platform)** 中的屬性參考您的專案檔。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-174">For example, to retrieve the current project platform&#x2014;for example, **x86** or **AnyCpu**&#x2014;you can include the **$(Platform)** property reference in your project file.</span></span> <span data-ttu-id="2f0a2-175">如需詳細資訊，請參閱 <<c0> [ 建置命令和屬性的巨集](https://msdn.microsoft.com/library/c02as0cs.aspx)，[通用的 MSBuild 專案屬性](https://msdn.microsoft.com/library/bb629394.aspx)，並[保留的屬性](https://msdn.microsoft.com/library/ms164309.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-175">For more information, see [Macros for Build Commands and Properties](https://msdn.microsoft.com/library/c02as0cs.aspx), [Common MSBuild Project Properties](https://msdn.microsoft.com/library/bb629394.aspx), and [Reserved Properties](https://msdn.microsoft.com/library/ms164309.aspx).</span></span>

<span data-ttu-id="2f0a2-176">屬性通常用於搭配*條件*。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-176">Properties are often used in conjunction with *conditions*.</span></span> <span data-ttu-id="2f0a2-177">大部分的 MSBuild 項目支援**條件**屬性，可讓您指定的 MSBuild 應該評估之項目的準則。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-177">Most MSBuild elements support the **Condition** attribute, which lets you specify the criteria upon which MSBuild should evaluate the element.</span></span> <span data-ttu-id="2f0a2-178">例如，請考慮此屬性定義：</span><span class="sxs-lookup"><span data-stu-id="2f0a2-178">For example, consider this property definition:</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample5.xml)]


<span data-ttu-id="2f0a2-179">當 MSBuild 處理此屬性定義時，它會先檢查以查看是否 **$(OutputRoot)** 屬性的值為止。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-179">When MSBuild processes this property definition, it first checks to see whether an **$(OutputRoot)** property value is available.</span></span> <span data-ttu-id="2f0a2-180">如果屬性值為空白&#x2014;亦即，使用者未提供值給此屬性&#x2014;條件評估為 **，則為 true**屬性值設定為與 **...\Publish\Out**。如果使用者已經提供值，這個屬性，條件評估為**false**並不會使用靜態屬性值。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-180">If the property value is blank&#x2014;in other words, the user hasn't provided a value for this property&#x2014;the condition evaluates to **true** and the property value is set to **..\Publish\Out**. If the user has provided a value for this property, the condition evaluates to **false** and the static property value is not used.</span></span>

<span data-ttu-id="2f0a2-181">如需有關您可以在其中指定條件的不同方式的詳細資訊，請參閱[MSBuild 條件](https://msdn.microsoft.com/library/7szfhaft.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-181">For more information on the different ways in which you can specify conditions, see [MSBuild Conditions](https://msdn.microsoft.com/library/7szfhaft.aspx).</span></span>

### <a name="items-and-item-groups"></a><span data-ttu-id="2f0a2-182">項目和項目群組</span><span class="sxs-lookup"><span data-stu-id="2f0a2-182">Items and Item Groups</span></span>

<span data-ttu-id="2f0a2-183">其中一個重要角色的專案檔是定義建置程序的輸入。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-183">One of the important roles of the project file is to define the inputs to the build process.</span></span> <span data-ttu-id="2f0a2-184">通常，這些輸入是檔案&#x2014;程式碼檔案、 組態檔、 指令檔和任何其他您需要處理，或做為複製的檔案在建置程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-184">Typically, these inputs are files&#x2014;code files, configuration files, command files, and any other files that you need to process or copy as part of the build process.</span></span> <span data-ttu-id="2f0a2-185">在 MSBuild 專案結構描述中，以表示這些輸入[項目](https://msdn.microsoft.com/library/ms164283.aspx)項目。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-185">In the MSBuild project schema, these inputs are represented by [Item](https://msdn.microsoft.com/library/ms164283.aspx) elements.</span></span> <span data-ttu-id="2f0a2-186">在專案檔中，必須定義項目內[ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx)項目。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-186">In a project file, items must be defined within an [ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx) element.</span></span> <span data-ttu-id="2f0a2-187">就如同**屬性**項目，您可以命名**項目**項目您隨心所欲。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-187">Just like **Property** elements, you can name an **Item** element however you like.</span></span> <span data-ttu-id="2f0a2-188">不過，您必須指定**Include**來識別的檔案或萬用字元項目所代表的屬性。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-188">However, you must specify an **Include** attribute to identify the file or wildcard that the item represents.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample6.xml)]


<span data-ttu-id="2f0a2-189">藉由指定多個**項目**具有相同名稱的項目，您要有效地建立資源的具名的清單。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-189">By specifying multiple **Item** elements with the same name, you're effectively creating a named list of resources.</span></span> <span data-ttu-id="2f0a2-190">若要查看此動作的好方法是查看其中一個 Visual Studio 會建立專案檔。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-190">A good way to see this in action is to take a look inside one of the project files that Visual Studio creates.</span></span> <span data-ttu-id="2f0a2-191">例如， *ContactManager.Mvc.csproj*範例方案中的檔案包含大量的項目群組，每個都有數個相同的已命名**項目**項目。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-191">For example, the *ContactManager.Mvc.csproj* file in the sample solution includes a lot of item groups, each with several identically named **Item** elements.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample7.xml)]


<span data-ttu-id="2f0a2-192">如此一來，專案檔會指示 MSBuild 建構需要相同的方式處理的檔案清單&#x2014;**參考**清單包含組件，必須先成功的組建，準備好**編譯**清單包含必須編譯的程式碼檔案和**內容**清單包含必須複製不變的資源。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-192">In this way, the project file is instructing MSBuild to construct lists of files that need to be processed in the same way&#x2014;the **Reference** list includes assemblies that must be in place for a successful build, the **Compile** list includes code files that must be compiled, and the **Content** list includes resources that must be copied unaltered.</span></span> <span data-ttu-id="2f0a2-193">我們將探討如何建置程序的參考位置，並使用本主題稍後的這些項目。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-193">We'll look at how the build process references and uses these items later in this topic.</span></span>

<span data-ttu-id="2f0a2-194">也可以包含項目的項目[ItemMetadata](https://msdn.microsoft.com/library/ms164284.aspx)子項目。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-194">Item elements can also include [ItemMetadata](https://msdn.microsoft.com/library/ms164284.aspx) child elements.</span></span> <span data-ttu-id="2f0a2-195">這些是使用者定義的索引鍵 / 值組，而且基本上代表該項目的特定屬性。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-195">These are user-defined key-value pairs and essentially represent properties that are specific to that item.</span></span> <span data-ttu-id="2f0a2-196">比方說，許多**編譯**專案檔中的項目包含**DependentUpon**子項目。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-196">For example, a lot of the **Compile** item elements in the project file include **DependentUpon** child elements.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample8.xml)]


> [!NOTE]
> <span data-ttu-id="2f0a2-197">除了使用者建立的項目中繼資料，所有的項目指派建立各種常見的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-197">In addition to user-created item metadata, all items are assigned various common metadata on creation.</span></span> <span data-ttu-id="2f0a2-198">如需詳細資訊，請參閱[已知的項目中繼資料](https://msdn.microsoft.com/library/ms164313.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-198">For more information, see [Well-known Item Metadata](https://msdn.microsoft.com/library/ms164313.aspx).</span></span>


<span data-ttu-id="2f0a2-199">您可以建立**ItemGroup**根層級中的項目**專案**項目或在特定**目標**項目。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-199">You can create **ItemGroup** elements within the root-level **Project** element or within specific **Target** elements.</span></span> <span data-ttu-id="2f0a2-200">**ItemGroup**項目也支援**條件**屬性，可讓您調整建置程序，根據條件，例如專案組態或平台所需的輸入。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-200">**ItemGroup** elements also support **Condition** attributes, which lets you tailor the inputs to the build process according to conditions like the project configuration or platform.</span></span>

### <a name="targets-and-tasks"></a><span data-ttu-id="2f0a2-201">目標和工作</span><span class="sxs-lookup"><span data-stu-id="2f0a2-201">Targets and Tasks</span></span>

<span data-ttu-id="2f0a2-202">在 MSBuild 結構描述[任務](https://msdn.microsoft.com/library/77f2hx1s.aspx)項目代表的個別組建指令 （或工作）。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-202">In the MSBuild schema, a [Task](https://msdn.microsoft.com/library/77f2hx1s.aspx) element represents an individual build instruction (or task).</span></span> <span data-ttu-id="2f0a2-203">MSBuild 包含許多預先定義的工作。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-203">MSBuild includes a multitude of predefined tasks.</span></span> <span data-ttu-id="2f0a2-204">例如: </span><span class="sxs-lookup"><span data-stu-id="2f0a2-204">For example:</span></span>

- <span data-ttu-id="2f0a2-205">**複製**工作將檔案複製到新位置。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-205">The **Copy** task copies files to a new location.</span></span>
- <span data-ttu-id="2f0a2-206">**Csc**工作叫用 Visual C# 編譯器。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-206">The **Csc** task invokes the Visual C# compiler.</span></span>
- <span data-ttu-id="2f0a2-207">**Vbc**工作叫用 Visual Basic 編譯器。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-207">The **Vbc** task invokes the Visual Basic compiler.</span></span>
- <span data-ttu-id="2f0a2-208">**Exec**工作會執行指定的程式。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-208">The **Exec** task runs a specified program.</span></span>
- <span data-ttu-id="2f0a2-209">**訊息**工作會將訊息寫入至記錄器。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-209">The **Message** task writes a message to a logger.</span></span>

> [!NOTE]
> <span data-ttu-id="2f0a2-210">立即可用的工作的完整詳細資訊，請參閱[MSBuild 工作參考](https://msdn.microsoft.com/library/7z253716.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-210">For full details of the tasks that are available out of the box, see [MSBuild Task Reference](https://msdn.microsoft.com/library/7z253716.aspx).</span></span> <span data-ttu-id="2f0a2-211">如需有關工作，包括如何建立您自己自訂的工作，請參閱[MSBuild 工作](https://msdn.microsoft.com/library/ms171466.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-211">For more information on tasks, including how to create your own custom tasks, see [MSBuild Tasks](https://msdn.microsoft.com/library/ms171466.aspx).</span></span>


<span data-ttu-id="2f0a2-212">工作必須一律包含在[目標](https://msdn.microsoft.com/library/t50z2hka.aspx)項目。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-212">Tasks must always be contained within [Target](https://msdn.microsoft.com/library/t50z2hka.aspx) elements.</span></span> <span data-ttu-id="2f0a2-213">A**目標**項目是一組循序執行的一或多個工作和專案檔案可以包含多個目標。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-213">A **Target** element is a set of one or more tasks that are executed sequentially, and a project file can contain multiple targets.</span></span> <span data-ttu-id="2f0a2-214">當您想要執行工作或一組工作時，您就會叫用包含它們的目標。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-214">When you want to run a task, or a set of tasks, you invoke the target that contains them.</span></span> <span data-ttu-id="2f0a2-215">例如，假設您有一個簡單的專案檔，會記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-215">For example, suppose you have a simple project file that logs a message.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample9.xml)]


<span data-ttu-id="2f0a2-216">您可以使用連線，叫用命令列中，從目標 **/t**參數來指定目標。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-216">You can invoke the target from the command line, by using the **/t** switch to specify the target.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample10.cmd)]


<span data-ttu-id="2f0a2-217">或者，您可以在其中加入**DefaultTargets**屬性設定為**專案**項目，來指定您想要叫用的目標。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-217">Alternatively, you can add a **DefaultTargets** attribute to the **Project** element, to specify the targets that you want to invoke.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample11.xml)]


<span data-ttu-id="2f0a2-218">在此情況下，您不需要指定從命令列目標。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-218">In this case, you don't need to specify the target from the command line.</span></span> <span data-ttu-id="2f0a2-219">您只可以指定專案檔，並叫用 MSBuild **FullPublish**為您的目標。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-219">You can simply specify the project file, and MSBuild will invoke the **FullPublish** target for you.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample12.cmd)]


<span data-ttu-id="2f0a2-220">目標和工作可以包含**條件**屬性。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-220">Both targets and tasks can include **Condition** attributes.</span></span> <span data-ttu-id="2f0a2-221">因此，您可以選擇略過整個目標或個別的工作如果符合特定條件。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-221">As such, you can choose to omit entire targets or individual tasks if certain conditions are met.</span></span>

<span data-ttu-id="2f0a2-222">一般而言，當您建立有用的工作和目標，您必須參考的屬性和您已在專案檔中其他地方定義的項目：</span><span class="sxs-lookup"><span data-stu-id="2f0a2-222">Generally speaking, when you create useful tasks and targets, you'll need to refer to the properties and items that you've defined elsewhere in the project file:</span></span>

- <span data-ttu-id="2f0a2-223">若要使用的屬性值，請輸入 **$(***PropertyName***)**，其中*PropertyName*名稱**屬性**項目或名稱參數。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-223">To use a property value, type **$(***PropertyName***)**, where *PropertyName* is the name of the **Property** element or the name of the parameter.</span></span>
- <span data-ttu-id="2f0a2-224">若要使用的項目，輸入 **@(***ItemName***)**，其中*ItemName*名稱**項目**項目。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-224">To use an item, type **@(***ItemName***)**, where *ItemName* is the name of the **Item** element.</span></span>

> [!NOTE]
> <span data-ttu-id="2f0a2-225">請記住，是否您建立多個項目具有相同名稱時，您要建置清單。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-225">Remember that if you create multiple items with the same name, you're building a list.</span></span> <span data-ttu-id="2f0a2-226">相反地，如果您建立多個屬性具有相同名稱時，您所提供的最後一個屬性值會覆寫任何先前的屬性具有相同名稱&#x2014;屬性只能包含單一值。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-226">In contrast, if you create multiple properties with the same name, the last property value you provide will overwrite any previous properties with the same name&#x2014;a property can only contain a single value.</span></span>


<span data-ttu-id="2f0a2-227">例如，在*Publish.proj*檔案中的範例解決方案，看看**BuildProjects**目標。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-227">For example, in the *Publish.proj* file in the sample solution, take a look at the **BuildProjects** target.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample13.xml)]


<span data-ttu-id="2f0a2-228">在此範例中，您可以觀察下列重點：</span><span class="sxs-lookup"><span data-stu-id="2f0a2-228">In this sample, you can observe these key points:</span></span>

- <span data-ttu-id="2f0a2-229">如果**BuildingInTeamBuild**參數指定，且其值為 **，則為 true**，則這個目標內的工作將會執行。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-229">If the **BuildingInTeamBuild** parameter is specified and has a value of **true**, none of the tasks within this target will be executed.</span></span>
- <span data-ttu-id="2f0a2-230">目標包含的單一執行個體[MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx)工作。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-230">The target contains a single instance of the [MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx) task.</span></span> <span data-ttu-id="2f0a2-231">此工作可讓您建立其他的 MSBuild 專案。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-231">This task lets you build other MSBuild projects.</span></span>
- <span data-ttu-id="2f0a2-232">**ProjectsToBuild**項目傳遞給工作。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-232">The **ProjectsToBuild** item is passed to the task.</span></span> <span data-ttu-id="2f0a2-233">此項目可能代表專案或方案檔，所有已定義的一份**ProjectsToBuild**項目中的項目群組的項目。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-233">This item could represent a list of project or solution files, all defined by **ProjectsToBuild** item elements within an item group.</span></span> <span data-ttu-id="2f0a2-234">在此情況下， **ProjectsToBuild**項目是指單一方案檔。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-234">In this case, the **ProjectsToBuild** item refers to a single solution file.</span></span>

    [!code-xml[Main](understanding-the-project-file/samples/sample14.xml)]
- <span data-ttu-id="2f0a2-235">屬性值傳遞給**MSBuild**工作包含名為的參數**OutputRoot**並**Configuration**。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-235">The property values passed to the **MSBuild** task include parameters named **OutputRoot** and **Configuration**.</span></span> <span data-ttu-id="2f0a2-236">如果它們不是，這些都會設為參數值，如果提供或靜態屬性值。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-236">These are set to parameter values if they are provided, or static property values if they are not.</span></span>

    [!code-xml[Main](understanding-the-project-file/samples/sample15.xml)]

<span data-ttu-id="2f0a2-237">您也可以看到**MSBuild**工作會叫用名為的目標**建置**。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-237">You can also see that the **MSBuild** task invokes a target named **Build**.</span></span> <span data-ttu-id="2f0a2-238">這是很廣泛地在 Visual Studio 專案檔，並且可用於您在自訂專案檔案中，例如的數個內建目標之一**建置**，**清除**，**重建**，並**發行**。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-238">This is one of several built-in targets that are widely used in Visual Studio project files and are available to you in your custom project files, like **Build**, **Clean**, **Rebuild**, and **Publish**.</span></span> <span data-ttu-id="2f0a2-239">您將了解更多關於使用目標和工作，以控制建置程序，以及關於**MSBuild**工作特別的是，本主題稍後的。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-239">You'll learn more about using targets and tasks to control the build process, and about the **MSBuild** task in particular, later in this topic.</span></span>

> [!NOTE]
> <span data-ttu-id="2f0a2-240">如需有關目標的詳細資訊，請參閱[MSBuild 目標](https://msdn.microsoft.com/library/ms171462.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-240">For more information on targets, see [MSBuild Targets](https://msdn.microsoft.com/library/ms171462.aspx).</span></span>


## <a name="splitting-project-files-to-support-multiple-environments"></a><span data-ttu-id="2f0a2-241">分割的專案檔，以支援多個環境</span><span class="sxs-lookup"><span data-stu-id="2f0a2-241">Splitting Project Files to Support Multiple Environments</span></span>

<span data-ttu-id="2f0a2-242">假設您想要能夠將方案部署到多個環境，例如測試伺服器、 暫存的平台，以及實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-242">Suppose you want to be able to deploy a solution to multiple environments, like test servers, staging platforms, and production environments.</span></span> <span data-ttu-id="2f0a2-243">設定這些環境之間可能大幅不同&#x2014;只是根據伺服器名稱、 連接字串，並依此類推，但也可能根據認證、 安全性設定，以及許多其他因素。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-243">The configuration may vary substantially between these environments&#x2014;not just in terms of server names, connection strings, and so on, but also potentially in terms of credentials, security settings, and lots of other factors.</span></span> <span data-ttu-id="2f0a2-244">如果您需要定期執行這項操作，不過它不是編輯專案檔中的多個屬性，每次切換的目標環境很有利。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-244">If you need to do this regularly, it's not really expedient to edit multiple properties in your project file every time you switch the target environment.</span></span> <span data-ttu-id="2f0a2-245">也不是理想的解決方案需要永無止盡的清單，提供給建置程序的屬性值。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-245">Nor is it an ideal solution to require an endless list of property values to be provided to the build process.</span></span>

<span data-ttu-id="2f0a2-246">所幸還有另一個方法。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-246">Fortunately there is an alternative.</span></span> <span data-ttu-id="2f0a2-247">MSBuild 可讓您將您的組建組態分割到多個專案檔。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-247">MSBuild lets you split your build configuration across multiple project files.</span></span> <span data-ttu-id="2f0a2-248">若要查看其運作方式，在範例解決方案中，請注意，有兩個自訂的專案檔：</span><span class="sxs-lookup"><span data-stu-id="2f0a2-248">To see how this works, in the sample solution, notice that there are two custom project files:</span></span>

- <span data-ttu-id="2f0a2-249">*Publish.proj*，其中包含屬性，項目，以及目標，通用於所有環境。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-249">*Publish.proj*, which contains properties, items, and targets that are common to all environments.</span></span>
- <span data-ttu-id="2f0a2-250">*Env Dev.proj*，其中包含開發人員環境特有的屬性。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-250">*Env-Dev.proj*, which contains properties that are specific to a developer environment.</span></span>

<span data-ttu-id="2f0a2-251">現在，請注意*Publish.proj*檔案包含[匯入](https://msdn.microsoft.com/library/92x05xfs.aspx)元素，緊接在開頭**專案**標記。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-251">Now notice that the *Publish.proj* file includes an [Import](https://msdn.microsoft.com/library/92x05xfs.aspx) element, immediately beneath the opening **Project** tag.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample16.xml)]


<span data-ttu-id="2f0a2-252">**匯入**元素用來匯入到目前的 MSBuild 專案檔案的另一個 MSBuild 專案檔的內容。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-252">The **Import** element is used to import the contents of another MSBuild project file into the current MSBuild project file.</span></span> <span data-ttu-id="2f0a2-253">在此情況下， **TargetEnvPropsFile**參數會提供您想要匯入的專案檔的檔名。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-253">In this case, the **TargetEnvPropsFile** parameter provides the filename of the project file you want to import.</span></span> <span data-ttu-id="2f0a2-254">當您執行 MSBuild 時，您便可以提供這個參數的值。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-254">You can provide a value for this parameter when you run MSBuild.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample17.cmd)]


<span data-ttu-id="2f0a2-255">這會有效地將兩個檔案的內容合併到單一專案檔案。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-255">This effectively merges the contents of the two files into a single project file.</span></span> <span data-ttu-id="2f0a2-256">您可以使用這個方法，建立包含您的通用的組建組態的專案檔案和包含環境特定屬性的多個增補的專案檔。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-256">Using this approach, you can create one project file containing your universal build configuration and multiple supplementary project files containing environment-specific properties.</span></span> <span data-ttu-id="2f0a2-257">如此一來，只要使用不同的參數值執行的命令可讓您將方案部署至不同的環境。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-257">As a result, simply running a command with a different parameter value lets you deploy your solution to a different environment.</span></span>

![](understanding-the-project-file/_static/image3.png)

<span data-ttu-id="2f0a2-258">分割您的專案檔案，以這種方式是最好的作法是遵循。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-258">Splitting your project files in this way is a good practice to follow.</span></span> <span data-ttu-id="2f0a2-259">它可讓開發人員，同時避免重複的通用的建置屬性，跨多個專案檔中執行單一命令，將部署到多個環境。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-259">It allows developers to deploy to multiple environments by running a single command, while avoiding the duplication of universal build properties across multiple project files.</span></span>

> [!NOTE]
> <span data-ttu-id="2f0a2-260">如需如何自訂您自己的伺服器環境的特定環境的專案檔的指引，請參閱 <<c0> [ 設定目標環境的部署屬性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-260">For guidance on how to customize the environment-specific project files for your own server environments, see [Configuring Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>


## <a name="conclusion"></a><span data-ttu-id="2f0a2-261">結論</span><span class="sxs-lookup"><span data-stu-id="2f0a2-261">Conclusion</span></span>

<span data-ttu-id="2f0a2-262">本主題提供 MSBuild 專案檔的一般簡介，並說明如何建立您自己的自訂專案檔，來控制建置程序。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-262">This topic provided a general introduction to MSBuild project files and explained how you can create your own custom project files to control the build process.</span></span> <span data-ttu-id="2f0a2-263">它也導入的概念將專案檔案分割成通用的組建指示和環境特定建置屬性，讓您輕鬆建置及將專案部署到多個目的地。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-263">It also introduced the concept of splitting project files into universal build instructions and environment-specific build properties, to make it easy to build and deploy projects to multiple destinations.</span></span>

<span data-ttu-id="2f0a2-264">下一個主題中，[了解建置程序](understanding-the-build-process.md)，提供更多深入了解如何使用專案檔，以控制組建和部署，以及在逐步引導您透過實際的複雜度層級部署的解決方案。</span><span class="sxs-lookup"><span data-stu-id="2f0a2-264">The next topic, [Understanding the Build Process](understanding-the-build-process.md), provides more insight into how you can use project files to control build and deployment by walking you through the deployment of a solution with a realistic level of complexity.</span></span>

## <a name="further-reading"></a><span data-ttu-id="2f0a2-265">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="2f0a2-265">Further Reading</span></span>

<span data-ttu-id="2f0a2-266">專案檔和 WPP 更深入的簡介，請參閱[內 Microsoft Build Engine:使用 MSBuild 和 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi 和 William bartholomew< /，ISBN:978-0-7356-4524-0.</span><span class="sxs-lookup"><span data-stu-id="2f0a2-266">For a more in-depth introduction to project files and the WPP, see [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://amzn.com/0735645248) by Sayed Ibrahim Hashimi and William Bartholomew, ISBN: 978-0-7356-4524-0.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2f0a2-267">[上一頁](setting-up-the-contact-manager-solution.md)
> [下一頁](understanding-the-build-process.md)</span><span class="sxs-lookup"><span data-stu-id="2f0a2-267">[Previous](setting-up-the-contact-manager-solution.md)
[Next](understanding-the-build-process.md)</span></span>
