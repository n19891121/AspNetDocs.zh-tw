---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: 建置真實世界的雲端應用程式與 Azure |Microsoft Docs
author: MikeWasson
description: 本電子書會引導您透過模式為基礎的方法，用以建置真實世界的雲端解決方案。 這些模式可套用至開發程序也為...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: bf9cf1f5be22a5b97ec964277c11ae21066676f0
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59412407"
---
# <a name="building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="f3d87-104">使用 Azure 建置真實世界的雲端應用程式</span><span class="sxs-lookup"><span data-stu-id="f3d87-104">Building Real-World Cloud Apps with Azure</span></span>

<span data-ttu-id="f3d87-105">藉由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f3d87-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="f3d87-106">[下載修正此問題的專案](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="f3d87-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="f3d87-107">本電子書會引導您透過模式為基礎的方法，用以建置真實世界的雲端解決方案。</span><span class="sxs-lookup"><span data-stu-id="f3d87-107">This e-book walks you through a patterns-based approach to building real-world cloud solutions.</span></span> <span data-ttu-id="f3d87-108">這些模式可套用至開發程序、 架構及程式碼實作。</span><span class="sxs-lookup"><span data-stu-id="f3d87-108">The patterns apply to the development process as well as to architecture and coding practices.</span></span>
> 
> <span data-ttu-id="f3d87-109">內容以 Scott Guthrie 所開發，由傳遞他在挪威開發人員 Conference (NDC) 在 2013 年 6 月中的簡報為依據 ([第 1 部分](http://vimeo.com/68215538)，[第 2 部分](http://vimeo.com/68215602))，而是在中的 Microsoft Tech Ed 澳洲2013 年 9 月日 ([第 1 部分](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)，[第 2 部分](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325))。</span><span class="sxs-lookup"><span data-stu-id="f3d87-109">The content is based on a presentation developed by Scott Guthrie and delivered by him at the Norwegian Developers Conference (NDC) in June of 2013 ([part 1](http://vimeo.com/68215538), [part 2](http://vimeo.com/68215602)), and at Microsoft Tech Ed Australia in September, 2013 ([part 1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324), [part 2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)).</span></span> <span data-ttu-id="f3d87-110">[許多其他](more-patterns-and-guidance.md#acknowledgments)隨後更新和內容從視訊轉換成書面形式。</span><span class="sxs-lookup"><span data-stu-id="f3d87-110">[Many others](more-patterns-and-guidance.md#acknowledgments) updated and augmented the content while transitioning it from video to written form.</span></span>


## <a name="intended-audience"></a><span data-ttu-id="f3d87-111">適用對象</span><span class="sxs-lookup"><span data-stu-id="f3d87-111">Intended Audience</span></span>

<span data-ttu-id="f3d87-112">Building real-world 定域機組，考慮移轉至雲端，或不熟悉雲端開發的開發人員會發現這裡的最重要的概念和做法，他們需要知道的簡要概觀。</span><span class="sxs-lookup"><span data-stu-id="f3d87-112">Developers who are curious about developing for the cloud, considering a move to the cloud, or are new to cloud development will find here a concise overview of the most important concepts and practices they need to know.</span></span> <span data-ttu-id="f3d87-113">搭配具體範例，以及更深入的資訊的其他資源的每個章節連結，來說明概念。</span><span class="sxs-lookup"><span data-stu-id="f3d87-113">The concepts are illustrated with concrete examples, and each chapter links to other resources for more in-depth information.</span></span> <span data-ttu-id="f3d87-114">範例和其他資源連結是以 Microsoft 架構和服務，但說明的原則套用至其他 web 開發架構和雲端環境。</span><span class="sxs-lookup"><span data-stu-id="f3d87-114">The examples and the links to additional resources are for Microsoft frameworks and services, but the principles illustrated apply to other web development frameworks and cloud environments as well.</span></span>

<span data-ttu-id="f3d87-115">已針對雲端開發人員可能會發現這裡的概念將協助使其更大的成就。</span><span class="sxs-lookup"><span data-stu-id="f3d87-115">Developers who are already developing for the cloud may find ideas here that will help make them more successful.</span></span> <span data-ttu-id="f3d87-116">數列中的每一章可以獨立地讀取，因此您可以挑選並選擇您感興趣的主題。</span><span class="sxs-lookup"><span data-stu-id="f3d87-116">Each chapter in the series can be read independently, so you can pick and choose topics that you're interested in.</span></span>

<span data-ttu-id="f3d87-117">觀賞 Scott Guthrie 的任何人*建置真實世界雲端應用程式與 Azure*展示層和更多詳細資料和更新的資訊會發現以下的想。</span><span class="sxs-lookup"><span data-stu-id="f3d87-117">Anyone who watched Scott Guthrie's *Building Real World Cloud Apps with Azure* presentation and wants more details and updated information will find that here.</span></span>

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a><span data-ttu-id="f3d87-118">雲端開發模式</span><span class="sxs-lookup"><span data-stu-id="f3d87-118">Cloud development patterns</span></span>

<span data-ttu-id="f3d87-119">本電子書會說明十三個建議的雲端開發模式。</span><span class="sxs-lookup"><span data-stu-id="f3d87-119">This e-book explains thirteen recommended patterns for cloud development.</span></span> <span data-ttu-id="f3d87-120">「 模式 」 來這裡廣泛表示建議的方法做事： 如何以開發、 設計和撰寫程式碼的雲端應用程式的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="f3d87-120">"Pattern" is used here in a broad sense to mean a recommended way to do things: how best to go about developing, designing, and coding cloud apps.</span></span> <span data-ttu-id="f3d87-121">這些是可協助您 「 成功的 pit 分為 「 如果您遵循這些索引鍵模式。</span><span class="sxs-lookup"><span data-stu-id="f3d87-121">These are key patterns which will help you "fall into the pit of success" if you follow them.</span></span>

- <span data-ttu-id="f3d87-122">[一切自動化](automate-everything.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-122">[Automate everything](automate-everything.md).</span></span>

    - <span data-ttu-id="f3d87-123">您可以使用 指令碼效率最大化，然後重複處理序中的錯誤降至最低。</span><span class="sxs-lookup"><span data-stu-id="f3d87-123">Use scripts to maximize efficiency and minimize errors in repetitive processes.</span></span>
    - <span data-ttu-id="f3d87-124">示範：Azure 管理指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3d87-124">Demo: Azure management scripts.</span></span>
- <span data-ttu-id="f3d87-125">[原始檔控制](source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-125">[Source control](source-control.md).</span></span> 

    - <span data-ttu-id="f3d87-126">設定原始檔控制中的分支結構，以加速 DevOps 工作流程。</span><span class="sxs-lookup"><span data-stu-id="f3d87-126">Set up branching structure in source control to facilitate DevOps workflow.</span></span>
    - <span data-ttu-id="f3d87-127">示範： 將指令碼新增至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="f3d87-127">Demo: add scripts to source control.</span></span>
    - <span data-ttu-id="f3d87-128">示範： 保留出原始檔控制的敏感性資料。</span><span class="sxs-lookup"><span data-stu-id="f3d87-128">Demo: keep sensitive data out of source control.</span></span>
    - <span data-ttu-id="f3d87-129">示範： 在 Visual Studio 中使用 Git。</span><span class="sxs-lookup"><span data-stu-id="f3d87-129">Demo: use Git in Visual Studio.</span></span>
- <span data-ttu-id="f3d87-130">[持續整合與傳遞](continuous-integration-and-continuous-delivery.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-130">[Continuous integration and delivery](continuous-integration-and-continuous-delivery.md).</span></span> 

    - <span data-ttu-id="f3d87-131">自動化組建和與每個原始檔控制簽入的部署。</span><span class="sxs-lookup"><span data-stu-id="f3d87-131">Automate build and deployment with each source control check-in.</span></span>
- <span data-ttu-id="f3d87-132">[Web 開發最佳作法](web-development-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-132">[Web development best practices](web-development-best-practices.md).</span></span> 

    - <span data-ttu-id="f3d87-133">讓 web 層保持無狀態。</span><span class="sxs-lookup"><span data-stu-id="f3d87-133">Keep web tier stateless.</span></span>
    - <span data-ttu-id="f3d87-134">示範： 縮放比例和自動調整 Azure App Service 中的 Web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="f3d87-134">Demo: scaling and auto-scaling in Web Apps in Azure App Service.</span></span>
    - <span data-ttu-id="f3d87-135">避免工作階段狀態。</span><span class="sxs-lookup"><span data-stu-id="f3d87-135">Avoid session state.</span></span>
    - <span data-ttu-id="f3d87-136">無法使用 CDN 時，則您可以使用後援 CDN。</span><span class="sxs-lookup"><span data-stu-id="f3d87-136">Use a CDN with a fallback when the CDN is unavailable.</span></span>
    - <span data-ttu-id="f3d87-137">使用非同步程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="f3d87-137">Use asynchronous programming model.</span></span>
    - <span data-ttu-id="f3d87-138">示範： 在 ASP.NET MVC 和 Entity Framework 中的非同步。</span><span class="sxs-lookup"><span data-stu-id="f3d87-138">Demo: async in ASP.NET MVC and Entity Framework.</span></span>
- <span data-ttu-id="f3d87-139">[單一登入](single-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-139">[Single sign-on](single-sign-on.md).</span></span> 

    - <span data-ttu-id="f3d87-140">Azure Active Directory 簡介。</span><span class="sxs-lookup"><span data-stu-id="f3d87-140">Introduction to Azure Active Directory.</span></span>
    - <span data-ttu-id="f3d87-141">示範： 建立使用 Azure Active Directory 的 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3d87-141">Demo: create an ASP.NET app that uses Azure Active Directory.</span></span>
- <span data-ttu-id="f3d87-142">[資料儲存體選項](data-storage-options.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-142">[Data storage options](data-storage-options.md).</span></span> 

    - <span data-ttu-id="f3d87-143">類型的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="f3d87-143">Types of data stores.</span></span>
    - <span data-ttu-id="f3d87-144">如何選擇正確的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="f3d87-144">How to choose the right data store.</span></span>
    - <span data-ttu-id="f3d87-145">示範：Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="f3d87-145">Demo: Azure SQL Database.</span></span>
- <span data-ttu-id="f3d87-146">[資料分割策略](data-partitioning-strategies.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-146">[Data partitioning strategies](data-partitioning-strategies.md).</span></span> 

    - <span data-ttu-id="f3d87-147">垂直、 水平分割資料或兩者皆可讓您調整規模的關聯式資料庫。</span><span class="sxs-lookup"><span data-stu-id="f3d87-147">Partition data vertically, horizontally, or both to facilitate scaling a relational database.</span></span>
- <span data-ttu-id="f3d87-148">[非結構化的 blob 儲存體](unstructured-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-148">[Unstructured blob storage](unstructured-blob-storage.md).</span></span> 

    - <span data-ttu-id="f3d87-149">使用 blob 服務，在雲端中儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="f3d87-149">Store files in the cloud by using the blob service.</span></span>
    - <span data-ttu-id="f3d87-150">示範： 修正其應用程式中使用 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="f3d87-150">Demo: using blob storage in the Fix It app.</span></span>
- <span data-ttu-id="f3d87-151">[設計存留失敗](design-to-survive-failures.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-151">[Design to survive failures](design-to-survive-failures.md).</span></span> 

    - <span data-ttu-id="f3d87-152">類型的失敗。</span><span class="sxs-lookup"><span data-stu-id="f3d87-152">Types of failures.</span></span>
    - <span data-ttu-id="f3d87-153">失敗的範圍。</span><span class="sxs-lookup"><span data-stu-id="f3d87-153">Failure Scope.</span></span>
    - <span data-ttu-id="f3d87-154">了解 Sla。</span><span class="sxs-lookup"><span data-stu-id="f3d87-154">Understanding SLAs.</span></span>
- <span data-ttu-id="f3d87-155">[監視和遙測](monitoring-and-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-155">[Monitoring and telemetry](monitoring-and-telemetry.md).</span></span> 

    - <span data-ttu-id="f3d87-156">為什麼您應該同時購買的遙測的應用程式並撰寫您自己的程式碼，來檢測您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3d87-156">Why you should both buy a telemetry app and write your own code to instrument your app.</span></span>
    - <span data-ttu-id="f3d87-157">示範：適用於 Azure 的 new Relic</span><span class="sxs-lookup"><span data-stu-id="f3d87-157">Demo: New Relic for Azure</span></span>
    - <span data-ttu-id="f3d87-158">示範： 修正其應用程式中的記錄程式碼。</span><span class="sxs-lookup"><span data-stu-id="f3d87-158">Demo: logging code in the Fix It app.</span></span>
    - <span data-ttu-id="f3d87-159">示範： 修正其應用程式中的相依性插入。</span><span class="sxs-lookup"><span data-stu-id="f3d87-159">Demo: dependency injection in the Fix It app.</span></span>
    - <span data-ttu-id="f3d87-160">示範： 在 Azure 中的內建的記錄支援。</span><span class="sxs-lookup"><span data-stu-id="f3d87-160">Demo: built-in logging support in Azure.</span></span>
- <span data-ttu-id="f3d87-161">[暫時性錯誤處理](transient-fault-handling.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-161">[Transient fault handling](transient-fault-handling.md).</span></span> 

    - <span data-ttu-id="f3d87-162">使用智慧型的重試/撤退邏輯來減少暫時性失敗的影響。</span><span class="sxs-lookup"><span data-stu-id="f3d87-162">Use smart retry/back-off logic to mitigate the effect of transient failures.</span></span>
    - <span data-ttu-id="f3d87-163">示範： 重試/退避法在 Entity Framework 6。</span><span class="sxs-lookup"><span data-stu-id="f3d87-163">Demo: retry/back-off in Entity Framework 6.</span></span>
- <span data-ttu-id="f3d87-164">[分散式快取](distributed-caching.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-164">[Distributed caching](distributed-caching.md).</span></span> 

    - <span data-ttu-id="f3d87-165">改善延展性，並使用分散式快取來降低資料庫的交易成本。</span><span class="sxs-lookup"><span data-stu-id="f3d87-165">Improve scalability and reduce database transaction costs by using distributed caching.</span></span>
- <span data-ttu-id="f3d87-166">[以佇列為主的工作模式](queue-centric-work-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-166">[Queue-centric work pattern](queue-centric-work-pattern.md).</span></span> 

    - <span data-ttu-id="f3d87-167">啟用高可用性和鬆散結合 web 和背景工作層，藉以改善延展性。</span><span class="sxs-lookup"><span data-stu-id="f3d87-167">Enable high availability and improve scalability by loosely coupling web and worker tiers.</span></span>
    - <span data-ttu-id="f3d87-168">示範：修正其應用程式中的 azure 儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="f3d87-168">Demo: Azure storage queues in the Fix It app.</span></span>
- <span data-ttu-id="f3d87-169">[更多雲端應用程式模式和指導方針](more-patterns-and-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-169">[More cloud app patterns and guidance](more-patterns-and-guidance.md).</span></span>
- [<span data-ttu-id="f3d87-170">附錄：Fix It 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="f3d87-170">Appendix: The Fix It Sample Application</span></span>](the-fix-it-sample-application.md)

    - <span data-ttu-id="f3d87-171">已知問題</span><span class="sxs-lookup"><span data-stu-id="f3d87-171">Known Issues</span></span>
    - <span data-ttu-id="f3d87-172">最佳作法</span><span class="sxs-lookup"><span data-stu-id="f3d87-172">Best Practices</span></span>
    - <span data-ttu-id="f3d87-173">如何下載、 建置、 執行和部署。</span><span class="sxs-lookup"><span data-stu-id="f3d87-173">How to download, build, run, and deploy.</span></span>

<span data-ttu-id="f3d87-174">這些模式可套用到所有的雲端環境，但我們將使用 Microsoft 技術和服務，例如 Visual Studio、 Team Foundation Service、 ASP.NET 和 Azure 為基礎的範例說明它們。</span><span class="sxs-lookup"><span data-stu-id="f3d87-174">These patterns apply to all cloud environments, but we'll illustrate them by using examples based on Microsoft technologies and services, such as Visual Studio, Team Foundation Service, ASP.NET, and Azure.</span></span>

<span data-ttu-id="f3d87-175">本章的其餘部分會介紹它修正範例應用程式和 Web 應用程式在 Azure App Service 中執行它修正應用程式的雲端環境中。</span><span class="sxs-lookup"><span data-stu-id="f3d87-175">This remainder of this chapter introduces the Fix It sample application and the Web Apps in Azure App Service cloud environment that the Fix It app runs in.</span></span>

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a><span data-ttu-id="f3d87-176">範例應用程式修正程式</span><span class="sxs-lookup"><span data-stu-id="f3d87-176">The Fix it sample application</span></span>

<span data-ttu-id="f3d87-177">大部分的螢幕擷取畫面和本電子書中所顯示的程式碼範例根據它修正應用程式原本由[Scott Guthrie](https://weblogs.asp.net/scottgu/)示範建議的雲端應用程式開發模式和作法。</span><span class="sxs-lookup"><span data-stu-id="f3d87-177">Most of the screen shots and code examples shown in this e-book are based on the Fix It app originally developed by [Scott Guthrie](https://weblogs.asp.net/scottgu/) to demonstrate recommended cloud app development patterns and practices.</span></span>

![修正此問題的應用程式首頁](introduction/_static/image1.png)

<span data-ttu-id="f3d87-179">範例應用程式是票證系統的簡單工作項目。</span><span class="sxs-lookup"><span data-stu-id="f3d87-179">The sample app is a simple work item ticketing system.</span></span> <span data-ttu-id="f3d87-180">當您需要修正的項目時，您會建立票證，並指派它某人，或其他人可以登入，並查看 指派票證給它們，並標示為已完成的工作完成時的票證。</span><span class="sxs-lookup"><span data-stu-id="f3d87-180">When you need something fixed, you create a ticket and assign it to someone, and others can log in and see the tickets assigned to them and mark tickets as completed when the work is done.</span></span>

<span data-ttu-id="f3d87-181">它是標準的 Visual Studio web 專案。</span><span class="sxs-lookup"><span data-stu-id="f3d87-181">It's a standard Visual Studio web project.</span></span> <span data-ttu-id="f3d87-182">它建置在 ASP.NET MVC，並使用 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f3d87-182">It is built on ASP.NET MVC and uses a SQL Server database.</span></span> <span data-ttu-id="f3d87-183">它可以在 IIS Express 在本機執行，而且可以部署至 Azure 網站在雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="f3d87-183">It can run locally in IIS Express and can be deployed to a Azure Web Site to run in the cloud.</span></span> <span data-ttu-id="f3d87-184">您可以記錄中使用表單驗證和本機資料庫，或使用 Google 等社交提供者。</span><span class="sxs-lookup"><span data-stu-id="f3d87-184">You can log in using forms authentication and a local database or by using a social provider such as Google.</span></span> <span data-ttu-id="f3d87-185">（稍後我們將也說明如何以 Active Directory 組織帳戶登入。）</span><span class="sxs-lookup"><span data-stu-id="f3d87-185">(Later we'll also show how to log in with an Active Directory organizational account.)</span></span>

![登入頁面](introduction/_static/image2.png)

<span data-ttu-id="f3d87-187">一旦您登中建立票證、 將它指派給某個成員，以及上傳您想要修正的圖片。</span><span class="sxs-lookup"><span data-stu-id="f3d87-187">Once you're logged in you can create a ticket, assign it to someone, and upload a picture of what you want to get fixed.</span></span>

![建立修正它的工作](introduction/_static/image3.png)

![修正此問題建立工作](introduction/_static/image4.png)

<span data-ttu-id="f3d87-190">您可以追蹤您所建立的工作項目的進度，查看指派給您，檢視票證詳細資料，與標記的項目，為已完成的票證。</span><span class="sxs-lookup"><span data-stu-id="f3d87-190">You can track the progress of work items you created, see tickets assigned to you, view ticket details, and mark items as completed.</span></span>

<span data-ttu-id="f3d87-191">這是非常簡單的應用程式，從功能觀點來看，但您會看到如何建置可調整為數百萬位使用者，使其將會復原資料庫失敗與連接終止數目之類的事項。</span><span class="sxs-lookup"><span data-stu-id="f3d87-191">This is a very simple app from a feature perspective, but you'll see how to build it so that it can scale to millions of users and will be resilient to things like database failures and connection terminations.</span></span> <span data-ttu-id="f3d87-192">您也將了解如何建立自動化且靈活的開發工作流程，可讓您輕鬆入門，並讓應用程式更好且更有效率且快速地反覆開發週期。</span><span class="sxs-lookup"><span data-stu-id="f3d87-192">You'll also see how to create an automated and agile development workflow, which enables you to start simple and make the app better and better by iterating the development cycle efficiently and quickly.</span></span>

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a><span data-ttu-id="f3d87-193">在 Azure App Service 中的 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="f3d87-193">Web Apps in Azure App Service</span></span>

<span data-ttu-id="f3d87-194">修正其應用程式所使用的雲端環境是 azure 的一種我們呼叫網站服務。</span><span class="sxs-lookup"><span data-stu-id="f3d87-194">The cloud environment used for the Fix It application is a service of Azure that we call Web Sites.</span></span> <span data-ttu-id="f3d87-195">這項服務是方法，您可以裝載您自己在 Azure 中的 web 應用程式，而不需要建立 Vm，並進行更新、 安裝和設定 IIS 等。我們在我們的 Vm 上裝載您的網站，並自動提供備份和復原和其他服務，供您。</span><span class="sxs-lookup"><span data-stu-id="f3d87-195">This service is a way that you can host your own web app in Azure without having to create VMs and keep them updated, install and configure IIS, etc. We host your site on our VMs and automatically provide backup and recovery and other services for you.</span></span> <span data-ttu-id="f3d87-196">Web Sites 服務適用於 ASP.NET、 Node.js、 PHP 和 Python。</span><span class="sxs-lookup"><span data-stu-id="f3d87-196">The Web Sites service works with ASP.NET, Node.js, PHP, and Python.</span></span> <span data-ttu-id="f3d87-197">它可讓您非常快速地使用 Visual Studio、 Web Deploy、 FTP、 Git 或 TFS 部署。</span><span class="sxs-lookup"><span data-stu-id="f3d87-197">It enables you to deploy very quickly using Visual Studio, Web Deploy, FTP, Git, or TFS.</span></span> <span data-ttu-id="f3d87-198">這通常是在幾秒內開始部署的時間與您的更新功能在網際網路上的時間之間。</span><span class="sxs-lookup"><span data-stu-id="f3d87-198">It's usually just a few seconds between the time you start a deployment and the time your update is available over the Internet.</span></span> <span data-ttu-id="f3d87-199">若要開始，所有免費且在流量增長時，您可以相應增加。</span><span class="sxs-lookup"><span data-stu-id="f3d87-199">It's all free to get started, and you can scale up as your traffic grows.</span></span>

<span data-ttu-id="f3d87-200">在幕後，Azure App Service 中的 Web 應用程式會提供許多架構的元件和功能，您必須自行建置，如果您要裝載您的 Vm 上使用 IIS 的網站。</span><span class="sxs-lookup"><span data-stu-id="f3d87-200">Behind the scenes, Web Apps in Azure App Service provides a lot of architectural components and features that you'd have to build yourself if you were going to host a web site using IIS on your own VMs.</span></span> <span data-ttu-id="f3d87-201">一個元件是部署結束點，會自動設定 IIS，並且為您想要執行您的網站的多個 Vm 上安裝您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3d87-201">One component is a deployment end point that automatically configures IIS and installs your application on as many VMs as you want to run your site on.</span></span>

![部署服務](introduction/_static/image5.png)

<span data-ttu-id="f3d87-203">當使用者叫用 web 站台時，它們不會直接達到 IIS Vm 時，會經歷[Application Request Routing (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing)負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="f3d87-203">When a user hits the web site, they don't hit the IIS VMs directly, they go through [Application Request Routing (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing) load balancers.</span></span> <span data-ttu-id="f3d87-204">您可以使用這些項目與您自己的伺服器，但此處的優點是，它們為您自動設定。</span><span class="sxs-lookup"><span data-stu-id="f3d87-204">You can use these with your own servers, but the advantage here is that they're set up for you automatically.</span></span> <span data-ttu-id="f3d87-205">使用智慧型的啟發學習法會將帳戶因素，例如工作階段親和性，在 IIS 中的佇列深度，以及 CPU 使用量，每個電腦，以將流量導向至虛擬機器裝載您的網站。</span><span class="sxs-lookup"><span data-stu-id="f3d87-205">They use a smart heuristic that takes into account factors such as session affinity, queue depth in IIS, and CPU usage on each machine to direct traffic to the VMs that host your web site.</span></span>

![ARR 負載平衡器](introduction/_static/image6.png)

<span data-ttu-id="f3d87-207">如果機器已關閉時，Azure 自動提取從循環，會啟動新的 VM 執行個體，而且會開始將流量導向至新的執行個體--所有與您的應用程式不需要停機。</span><span class="sxs-lookup"><span data-stu-id="f3d87-207">If a machine goes down, Azure automatically pulls it from the rotation, spins up a new VM instance, and starts directing traffic to the new instance -- all with no down time for your application.</span></span>

![從機器失敗的自動復原](introduction/_static/image7.png)

<span data-ttu-id="f3d87-209">這會自動發生。</span><span class="sxs-lookup"><span data-stu-id="f3d87-209">All of this takes place automatically.</span></span> <span data-ttu-id="f3d87-210">您要做的就是建立網站及部署您的應用程式，使用 Windows PowerShell、 Visual Studio 中或 Azure 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="f3d87-210">All you need to do is create a web site and deploy your application to it, using Windows PowerShell, Visual Studio, or the Azure management portal.</span></span>

<span data-ttu-id="f3d87-211">如需快速且輕鬆地逐步教學課程示範如何在 Visual Studio 中建立 web 應用程式，並將它部署至 Azure 網站，請參閱 <<c0> [ 開始使用 Azure 和 ASP.NET](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-211">For a quick and easy step-by-step tutorial that shows how to create a web application in Visual Studio and deploy it to a Azure Web Site, see [Get started with Azure and ASP.NET](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<a id="summary"></a>
## <a name="summary"></a><span data-ttu-id="f3d87-212">總結</span><span class="sxs-lookup"><span data-stu-id="f3d87-212">Summary</span></span>

<span data-ttu-id="f3d87-213">本簡介提供一份活頁簿將會涵蓋的主題、 螢幕擷取畫面的範例應用程式，並在 Azure App Service 雲端環境中的 Web 應用程式的簡短概觀。</span><span class="sxs-lookup"><span data-stu-id="f3d87-213">This introduction has provided a list of topics the book will cover, screenshots of the sample application, and a brief overview of the Web Apps in Azure App Service cloud environment.</span></span> <span data-ttu-id="f3d87-214">其中一個最大的開發應用程式中，和適用於雲端的優點是，就可以輕鬆地自動化重複性的開發工作，例如建立測試環境，並將您的程式碼部署到它。</span><span class="sxs-lookup"><span data-stu-id="f3d87-214">One of the great advantages of developing apps in and for the cloud is that it's easy to automate repetitive development tasks such as creating a test environment and deploying your code to it.</span></span> <span data-ttu-id="f3d87-215">如何執行這個動作的主旨[下一步 一章](automate-everything.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-215">How to do that is the subject of the [next chapter](automate-everything.md).</span></span>

## <a name="resources"></a><span data-ttu-id="f3d87-216">資源</span><span class="sxs-lookup"><span data-stu-id="f3d87-216">Resources</span></span>

<span data-ttu-id="f3d87-217">如需有關本章節涵蓋之主題的詳細資訊，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="f3d87-217">For more information about the topics covered in this chapter, see the following resources.</span></span>

<span data-ttu-id="f3d87-218">文件：</span><span class="sxs-lookup"><span data-stu-id="f3d87-218">Documentation:</span></span>

- <span data-ttu-id="f3d87-219">[Web 應用程式在 Azure App Service 中的](https://azure.microsoft.com/services/app-service/web/)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-219">[Web Apps in Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="f3d87-220">如需 Web 應用程式的 Azure 文件的入口網站頁面。</span><span class="sxs-lookup"><span data-stu-id="f3d87-220">Portal page for Azure documentation about Web Apps.</span></span>
- [<span data-ttu-id="f3d87-221">Web Apps、 雲端服務和 Vm:使用時機？</span><span class="sxs-lookup"><span data-stu-id="f3d87-221">Web Apps, Cloud Services, and VMs: When to use which?</span></span>](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) <span data-ttu-id="f3d87-222">在這一章中所示的 WAWS 只是三種方式，您可以在 Azure 中執行 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3d87-222">WAWS as shown in this chapter is just one of three ways you can run web apps in Azure.</span></span> <span data-ttu-id="f3d87-223">本文說明的三種方式之間的差異，並提供有關如何選擇哪一種適合您案例的指引。</span><span class="sxs-lookup"><span data-stu-id="f3d87-223">This article explains the differences between the three ways and gives guidance on how to choose which one is right for your scenario.</span></span> <span data-ttu-id="f3d87-224">Web Sites 中，例如雲端服務是一項 Azure PaaS 功能。</span><span class="sxs-lookup"><span data-stu-id="f3d87-224">Like Web Sites, Cloud Services is a PaaS feature of Azure.</span></span> <span data-ttu-id="f3d87-225">Vm 是 IaaS 功能。</span><span class="sxs-lookup"><span data-stu-id="f3d87-225">VMs are an IaaS feature.</span></span> <span data-ttu-id="f3d87-226">如需 PaaS 與 IaaS 的說明，請參閱 <<c0> [ 資料選項](data-storage-options.md#paasiaas)一章。</span><span class="sxs-lookup"><span data-stu-id="f3d87-226">For an explanation of PaaS versus IaaS, see the [Data Options](data-storage-options.md#paasiaas) chapter.</span></span>

<span data-ttu-id="f3d87-227">影片：</span><span class="sxs-lookup"><span data-stu-id="f3d87-227">Videos:</span></span>

- [<span data-ttu-id="f3d87-228">Scott Guthrie 開始步驟 0-什麼是 Azure 雲端作業系統？</span><span class="sxs-lookup"><span data-stu-id="f3d87-228">Scott Guthrie starts at Step 0 - What is the Azure Cloud OS?</span></span>](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- <span data-ttu-id="f3d87-229">[Web Sites 的架構-Stefan schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-229">[Web Sites Architecture - with Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/).</span></span>
- <span data-ttu-id="f3d87-230">[Azure Web Sites 內部運作 Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski)。</span><span class="sxs-lookup"><span data-stu-id="f3d87-230">[Azure Web Sites Internals with Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f3d87-231">下一步</span><span class="sxs-lookup"><span data-stu-id="f3d87-231">Next</span></span>](automate-everything.md)
