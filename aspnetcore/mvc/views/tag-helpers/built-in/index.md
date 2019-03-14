---
title: ASP.NET Core 內建的標記協助程式
author: pkellner
description: 了解 ASP.NET Core 內建標籤協助程式如何提升您的產能。
ms.author: riande
ms.custom: mvc
ms.date: 10/10/2018
uid: mvc/views/tag-helpers/builtin-th/Index
---

# <a name="aspnet-core-built-in-tag-helpers"></a><span data-ttu-id="c86f9-103">ASP.NET Core 內建的標記協助程式</span><span class="sxs-lookup"><span data-stu-id="c86f9-103">ASP.NET Core built-in Tag Helpers</span></span>

<span data-ttu-id="c86f9-104">由 [Peter Kellner](http://peterkellner.net) 提供</span><span class="sxs-lookup"><span data-stu-id="c86f9-104">By [Peter Kellner](http://peterkellner.net)</span></span>

<span data-ttu-id="c86f9-105">如需標籤協助程式的概觀，請參閱 <xref:mvc/views/tag-helpers/intro>。</span><span class="sxs-lookup"><span data-stu-id="c86f9-105">For an overview of Tag Helpers, see <xref:mvc/views/tag-helpers/intro>.</span></span>

> [!NOTE]
> <span data-ttu-id="c86f9-106">有一些內建標籤協助程式未在本文件中加以描述。</span><span class="sxs-lookup"><span data-stu-id="c86f9-106">There are built-in Tag Helpers which aren't described in the documentation.</span></span> <span data-ttu-id="c86f9-107">這些標籤協助程式供 [Razor](xref:mvc/views/razor) 檢視引擎在內部使用。</span><span class="sxs-lookup"><span data-stu-id="c86f9-107">These Tag Helpers are used internally by the [Razor](xref:mvc/views/razor) view engine.</span></span> <span data-ttu-id="c86f9-108">這包括 `~` (波狀符號) 字元的標籤協助程式，其可將範圍擴展到網站的根路徑。</span><span class="sxs-lookup"><span data-stu-id="c86f9-108">This includes a Tag Helper for the `~` (tilde) character, which expands to the root path of the website.</span></span>

## <a name="built-in-aspnet-core-tag-helpers"></a><span data-ttu-id="c86f9-109">內建的 ASP.NET Core 標記協助程式</span><span class="sxs-lookup"><span data-stu-id="c86f9-109">Built-in ASP.NET Core Tag Helpers</span></span>

<span data-ttu-id="c86f9-110">**[錨點標記協助程式](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="c86f9-110">**[Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span></span>

<span data-ttu-id="c86f9-111">**[快取標記協助程式](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="c86f9-111">**[Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span></span>

<span data-ttu-id="c86f9-112">**[分散式快取標記協助程式](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="c86f9-112">**[Distributed Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span></span>

<span data-ttu-id="c86f9-113">**[環境標記協助程式](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="c86f9-113">**[Environment Tag Helper](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span></span>

[comment]: **[FormActionTagHelper](xref:mvc/views/tag-helpers/builtin-th/form-action-tag-helper)**

<span data-ttu-id="c86f9-114">**[表單標記協助程式](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="c86f9-114">**[Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span></span>

<span data-ttu-id="c86f9-115">**[影像標記協助程式](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="c86f9-115">**[Image Tag Helper](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span></span>

<span data-ttu-id="c86f9-116">**[輸入標記協助程式](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="c86f9-116">**[Input Tag Helper](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span></span>

<span data-ttu-id="c86f9-117">**[標籤標記協助程式](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="c86f9-117">**[Label Tag Helper](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span></span>

[comment]: **[LinkTagHelper](xref:mvc/views/tag-helpers/builtin-th/link-tag-helper)**

[comment]: **[OptionTagHelper](xref:mvc/views/tag-helpers/builtin-th/option-tag-helper)**

[comment]: **[ScriptTagHelper](xref:mvc/views/tag-helpers/builtin-th/script-tag-helper)**

<span data-ttu-id="c86f9-118">**[部分標記協助程式](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="c86f9-118">**[Partial Tag Helper](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)**</span></span>

<span data-ttu-id="c86f9-119">**[選取標記協助程式](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="c86f9-119">**[Select Tag Helper](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span></span>

<span data-ttu-id="c86f9-120">**[Textarea 標記協助程式](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="c86f9-120">**[Textarea Tag Helper](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span></span>

<span data-ttu-id="c86f9-121">**[驗證訊息標記協助程式](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="c86f9-121">**[Validation Message Tag Helper](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span></span>

<span data-ttu-id="c86f9-122">**[驗證摘要標記協助程式](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="c86f9-122">**[Validation Summary Tag Helper](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c86f9-123">其他資源</span><span class="sxs-lookup"><span data-stu-id="c86f9-123">Additional resources</span></span>

* <xref:mvc/views/tag-helpers/intro>
* <xref:mvc/views/tag-helpers/th-components>
