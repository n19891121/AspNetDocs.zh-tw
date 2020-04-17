---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: 資料來源控制 |微軟文件
author: rick-anderson
description: ASP.NET 1.x 中的 DataGrid 控制件標誌著 Web 應用程式中數據存取的重大改進。 然而,它並不像它本來可以的那麼使用者友好。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: 2b4302b509af57dc5d9db9de9ee824df767d0737
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540216"
---
# <a name="data-source-controls"></a><span data-ttu-id="8d6ab-104">資料來源控制項</span><span class="sxs-lookup"><span data-stu-id="8d6ab-104">Data Source Controls</span></span>

<span data-ttu-id="8d6ab-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8d6ab-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="8d6ab-106">ASP.NET 1.x 中的 DataGrid 控制件標誌著 Web 應用程式中數據存取的重大改進。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-106">The DataGrid control in ASP.NET 1.x marked a great improvement in data access in Web applications.</span></span> <span data-ttu-id="8d6ab-107">然而,它並不像它本來可以對使用者友好。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-107">However, it wasn't as user-friendly as it could have been.</span></span> <span data-ttu-id="8d6ab-108">它仍然需要大量的代碼才能從中獲得許多有用的功能。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-108">It still required a considerable amount of code to obtain much useful functionality from it.</span></span> <span data-ttu-id="8d6ab-109">這就是 1.x 中所有數據訪問努力中的模型。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-109">Such is the model in all data access endeavors in 1.x.</span></span>

<span data-ttu-id="8d6ab-110">ASP.NET 1.x 中的 DataGrid 控制件標誌著 Web 應用程式中數據存取的重大改進。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-110">The DataGrid control in ASP.NET 1.x marked a great improvement in data access in Web applications.</span></span> <span data-ttu-id="8d6ab-111">然而,它並不像它本來可以對使用者友好。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-111">However, it wasn't as user-friendly as it could have been.</span></span> <span data-ttu-id="8d6ab-112">它仍然需要大量的代碼才能從中獲得許多有用的功能。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-112">It still required a considerable amount of code to obtain much useful functionality from it.</span></span> <span data-ttu-id="8d6ab-113">這就是 1.x 中所有數據訪問努力中的模型。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-113">Such is the model in all data access endeavors in 1.x.</span></span>

<span data-ttu-id="8d6ab-114">ASP.NET 2.0 部分使用數據源控件解決了這個問題。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-114">ASP.NET 2.0 addresses this with in part with data source controls.</span></span> <span data-ttu-id="8d6ab-115">ASP.NET 2.0 中的數據來源控制項為開發人員提供了用於檢索資料、顯示數據和編輯數據的聲明性模型。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-115">The data source controls in ASP.NET 2.0 provide developers with a declarative model for retrieving data, displaying data, and editing data.</span></span> <span data-ttu-id="8d6ab-116">數據源控件的目的是向數據綁定控件提供數據一致的表示形式,而不管數據源如何。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-116">The purpose of data source controls is to provide a consistent representation of data to data-bound controls regardless of the source of those data.</span></span> <span data-ttu-id="8d6ab-117">ASP.NET 2.0 中資料源控制項的核心是 DataSourceControl 抽象類。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-117">At the heart of the data source controls in ASP.NET 2.0 is the DataSourceControl abstract class.</span></span> <span data-ttu-id="8d6ab-118">DataSourceControl 類提供了 IDataSource 介面和 IListSource 介面的基本實現,後者允許您將資料來源控制項指定為數據綁定控制項的 DataSource(透過稍後討論的新 DataSourceId 屬性),並將其中的數據公開為清單。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-118">The DataSourceControl class provides a base implementation of the IDataSource interface and the IListSource interface, the latter of which allows you to assign the data source control as the DataSource of a data-bound control (via the new DataSourceId property discussed later) and expose the data therein as a list.</span></span> <span data-ttu-id="8d6ab-119">數據源控制項每個資料清單都公開為 DataSourceView 物件。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-119">Each list of data from a data source control is exposed as a DataSourceView object.</span></span> <span data-ttu-id="8d6ab-120">IDataSource 介面提供了對 DataSourceView 實例的訪問。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-120">Access to the DataSourceView instances is provided by the IDataSource interface.</span></span> <span data-ttu-id="8d6ab-121">例如,GetViewNames 方法傳回 ICollection,允許您枚舉與特定資料來源控制項關聯的 DataSourceViews,GetView 方法允許您按名稱存取特定的 DataSourceView 實例。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-121">For example, the GetViewNames method returns an ICollection that allows you to enumerate the DataSourceViews associated with a particular data source control, and the GetView method allows you to access a particular DataSourceView instance by name.</span></span>

<span data-ttu-id="8d6ab-122">數據源控件沒有用戶介面。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-122">Data source controls have no user-interface.</span></span> <span data-ttu-id="8d6ab-123">它們作為伺服器控制項實現,以便它們可以支援聲明性語法,以便根據需要存取頁面狀態。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-123">They are implemented as server controls so that they can support declarative syntax and so that they have access to page state if desired.</span></span> <span data-ttu-id="8d6ab-124">數據來源控制項不向客戶端呈現任何 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-124">Data source controls do not render any HTML markup to the client.</span></span>

> [!NOTE]
> <span data-ttu-id="8d6ab-125">稍後您將看到,使用數據源控件還可以獲得緩存好處。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-125">As you'll see later, there are also caching benefits obtained by using data source controls.</span></span>

## <a name="storing-connection-strings"></a><span data-ttu-id="8d6ab-126">儲存連線字串</span><span class="sxs-lookup"><span data-stu-id="8d6ab-126">Storing Connection Strings</span></span>

<span data-ttu-id="8d6ab-127">在研究如何配置數據源控件之前,我們應該在有關連接字串ASP.NET 2.0 中介紹新功能。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-127">Before we get into looking at how to configure data source controls, we should cover a new capability in ASP.NET 2.0 concerning connection strings.</span></span> <span data-ttu-id="8d6ab-128">ASP.NET 2.0 在設定檔中引入了一個新部分,允許您輕鬆儲存可在運行時動態讀取的連接字串。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-128">ASP.NET 2.0 introduces a new section in the configuration file that allows you to easily store connection strings that can be read dynamically at runtime.</span></span> <span data-ttu-id="8d6ab-129">連接&lt;字串&gt;部份便於儲存連接字串。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-129">The &lt;connectionStrings&gt; section makes it easy to store connection strings.</span></span>

<span data-ttu-id="8d6ab-130">下面的代碼段添加了一個新的連接字串。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-130">The snippet below adds a new connection string.</span></span>

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> <span data-ttu-id="8d6ab-131">&lt;與&gt;appSettings 部分一&lt;樣, 連接&gt;字串 部分顯示在&lt;配置檔中的 system.web&gt;部分之外。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-131">Just as with the &lt;appSettings&gt; section, the &lt;connectionStrings&gt; section appears outside of the &lt;system.web&gt; section in the configuration file.</span></span>

<span data-ttu-id="8d6ab-132">要使用此連接字串,可以在設定伺服器控制項的 ConnectString 屬性時使用以下語法。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-132">To use this connection string, you can use the following syntax when setting the ConnectionString attribute of a server control.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

<span data-ttu-id="8d6ab-133">還可以&lt;加密&gt;連接 字串部分,以便不公開敏感資訊。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-133">The &lt;connectionStrings&gt; section can also be encrypted so that sensitive information is not exposed.</span></span> <span data-ttu-id="8d6ab-134">這一能力將在後面的模組中介紹。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-134">That ability will be covered in a later module.</span></span>

## <a name="caching-data-sources"></a><span data-ttu-id="8d6ab-135">快取資料來源</span><span class="sxs-lookup"><span data-stu-id="8d6ab-135">Caching Data Sources</span></span>

<span data-ttu-id="8d6ab-136">每個 DataSourceControl 提供四個屬性來配置緩存;啟用快取、快取持續時間、緩存過期策略和快取金鑰依賴性。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-136">Each DataSourceControl provides four properties for configuring caching; EnableCaching, CacheDuration, CacheExpirationPolicy, and CacheKeyDependency.</span></span>

## <a name="enablecaching"></a><span data-ttu-id="8d6ab-137">開啟快取</span><span class="sxs-lookup"><span data-stu-id="8d6ab-137">EnableCaching</span></span>

<span data-ttu-id="8d6ab-138">啟用快取是一個布林屬性,用於確定是否為資料源控制項啟用緩存。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-138">EnableCaching is a Boolean property that determines whether or not caching is enabled for the data source control.</span></span>

## <a name="cacheduration-property"></a><span data-ttu-id="8d6ab-139">快取持續時間屬性</span><span class="sxs-lookup"><span data-stu-id="8d6ab-139">CacheDuration Property</span></span>

<span data-ttu-id="8d6ab-140">"快取時間"屬性設定快取保持有效的秒數。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-140">The CacheDuration property sets the number of seconds that the cache remains valid.</span></span> <span data-ttu-id="8d6ab-141">將此屬性設置為**0**會導致緩存保持有效,直到顯式失效。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-141">Setting this property to **0** causes the cache to remain valid until explicitly invalidated.</span></span>

## <a name="cacheexpirationpolicy-property"></a><span data-ttu-id="8d6ab-142">快取過期政策屬性</span><span class="sxs-lookup"><span data-stu-id="8d6ab-142">CacheExpirationPolicy Property</span></span>

<span data-ttu-id="8d6ab-143">快取過期政策屬性可以設定為**絕對**或**滑動**。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-143">The CacheExpirationPolicy property can be set to either **Absolute** or **Sliding**.</span></span> <span data-ttu-id="8d6ab-144">將其設置為「絕對」意味著緩存數據的最大時間是 CacheDuration 屬性指定的秒數。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-144">Setting it to Absolute means that the maximum amount of time that the data will be cached is the number of seconds specified by the CacheDuration property.</span></span> <span data-ttu-id="8d6ab-145">通過將它設置為「滑動」,執行每個操作時將重置過期時間。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-145">By setting it to Sliding, the expiration time is reset when each operation is performed.</span></span>

## <a name="cachekeydependency-property"></a><span data-ttu-id="8d6ab-146">快取金鑰相依屬性</span><span class="sxs-lookup"><span data-stu-id="8d6ab-146">CacheKeyDependency Property</span></span>

<span data-ttu-id="8d6ab-147">如果為 CacheKey 依賴項屬性指定了字串值,ASP.NET將基於該字串設置新的緩存依賴項。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-147">If a string value is specified for the CacheKeyDependency property, ASP.NET will set up a new cache dependency based on that string.</span></span> <span data-ttu-id="8d6ab-148">這允許您透過簡單地更改或刪除 CacheKey 依賴項來顯式使緩存無效。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-148">This allows you to explicitly invalidate the cache by simply changing or removing the CacheKeyDependency.</span></span>

<span data-ttu-id="8d6ab-149">**重要提示**:如果啟用了類比,並且對資料源和/或數據內容的訪問基於用戶端標識,則建議通過設置啟用緩存設置為 False 來禁用緩存。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-149">**Important**: If impersonation is enabled and access to the data source and/or content of data are based upon client identity, it is recommended that caching be disabled by setting EnableCaching to False.</span></span> <span data-ttu-id="8d6ab-150">如果在此方案中啟用了緩存,並且最初請求數據的使用者以外的使用者發出請求,則不會強制執行對數據源的授權。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-150">If caching is enabled in this scenario and a user other than the user who originally requested the data issues a request, authorization to the data source is not enforced.</span></span> <span data-ttu-id="8d6ab-151">數據將僅從緩存中提供。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-151">The data will simply be served from cache.</span></span>

## <a name="the-sqldatasource-control"></a><span data-ttu-id="8d6ab-152">SqlDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="8d6ab-152">The SqlDataSource Control</span></span>

<span data-ttu-id="8d6ab-153">SqlDataSource 控制件允許開發人員存取儲存在支援ADO.NET的任何關係資料庫中的數據。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-153">The SqlDataSource control allows a developer to access data stored in any relational database that supports ADO.NET.</span></span> <span data-ttu-id="8d6ab-154">它可以使用 System.Data.SqlClient 提供程式訪問 SQL Server 資料庫、System.Data.OleDb 提供程式、系統.Data.Odbc 提供程式或 System.Data.OracleClient 提供程式來造訪 Oracle。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-154">It can use the System.Data.SqlClient provider to access a SQL Server database, the System.Data.OleDb provider, the System.Data.Odbc provider, or the System.Data.OracleClient provider to access Oracle.</span></span> <span data-ttu-id="8d6ab-155">因此,SqlDataSource 當然不僅用於訪問 SQL Server 資料庫中的數據。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-155">Therefore, the SqlDataSource is certainly not only used for accessing data in a SQL Server database.</span></span>

<span data-ttu-id="8d6ab-156">為了使用 SqlDataSource,您只需為 ConnectString 屬性提供一個值,並指定 SQL 命令或儲存過程。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-156">In order to use the SqlDataSource, you simply provide a value for the ConnectionString property and specify a SQL command or stored procedure.</span></span> <span data-ttu-id="8d6ab-157">SqlDataSource 控制項負責使用底層ADO.NET體系結構。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-157">The SqlDataSource control takes care of working with the underlying ADO.NET architecture.</span></span> <span data-ttu-id="8d6ab-158">它打開連接,查詢數據源或執行存儲過程,返回數據,然後為您關閉連接。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-158">It opens the connection, queries the data source or executes the stored procedure, returns the data, and then closes the connection for you.</span></span>

> [!NOTE]
> <span data-ttu-id="8d6ab-159">由於 DataSourceControl 類會自動為您關閉連接,因此它應該減少因資料庫連接洩漏而生成的客戶呼叫數。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-159">Because the DataSourceControl class automatically closes the connection for you, it should reduce the number of customer calls generated by leaking database connections.</span></span>

<span data-ttu-id="8d6ab-160">下面的代碼段使用儲存在配置檔中的連接字串將下拉清單控件綁定到 SqlDataSource 控制項,如上所示。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-160">The code snippet below binds a DropDownList control to a SqlDataSource control using the connection string that is stored in the configuration file as shown above.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

<span data-ttu-id="8d6ab-161">如上所述,SqlDataSource 的 DataSourceMode 屬性指定數據源的模式。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-161">As illustrated above, the DataSourceMode property of the SqlDataSource specifies the mode for the data source.</span></span> <span data-ttu-id="8d6ab-162">在上面的範例中,資料來源模式設置為資料閱讀器。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-162">In the example above, the DataSourceMode is set to DataReader.</span></span> <span data-ttu-id="8d6ab-163">在這種情況下,SqlDataSource 將使用僅行和唯讀游標返回 IDataReader 物件。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-163">In that case, the SqlDataSource will return an IDataReader object using a forward-only and read-only cursor.</span></span> <span data-ttu-id="8d6ab-164">返回的指定類型的物件由所使用的提供程式控制。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-164">The specified type of object that is returned is controlled by the provider that is used.</span></span> <span data-ttu-id="8d6ab-165">在這種情況下,我使用的是 Web.config&lt;檔的 connectStrings&gt;部分中指定的 System.Data.SqlClient 提供程式。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-165">In this case, I'm using the System.Data.SqlClient provider as specified in the &lt;connectionStrings&gt; section of the web.config file.</span></span> <span data-ttu-id="8d6ab-166">因此,返回的對象將採用 SqlDataReader 類型。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-166">Therefore, the object that is returned will be of type SqlDataReader.</span></span> <span data-ttu-id="8d6ab-167">通過指定 DataSet 的 DataSourceMode 值,資料可以儲存在伺服器上的 DataSet 中。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-167">By specifying a DataSourceMode value of DataSet, the data can be stored in a DataSet on the server.</span></span> <span data-ttu-id="8d6ab-168">此模式允許您添加排序、分頁等功能。如果我將 SqlDataSource 數據綁定到 GridView 控件,我會選擇 DataSet 模式。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-168">This mode allows you to add features such as sorting, paging, etc. If I had been data-binding the SqlDataSource to a GridView control, I would have chosen the DataSet mode.</span></span> <span data-ttu-id="8d6ab-169">但是,在下拉清單的情況下,數據閱讀器模式是正確的選擇。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-169">However, in the case of a DropDownList, the DataReader mode is the correct choice.</span></span>

> [!NOTE]
> <span data-ttu-id="8d6ab-170">緩存 SqlDataSource 或 AccessDataSource 時,必須將 DataSourceMode 屬性設置為 DataSet。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-170">When caching a SqlDataSource or an AccessDataSource, the DataSourceMode property must be set to DataSet.</span></span> <span data-ttu-id="8d6ab-171">如果使用 DataReader 的 DataSource 模式啟用快取,則會出現異常。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-171">An exception will occur if you enable caching with a DataSourceMode of DataReader.</span></span>

## <a name="sqldatasource-properties"></a><span data-ttu-id="8d6ab-172">SqlDataSource 屬性</span><span class="sxs-lookup"><span data-stu-id="8d6ab-172">SqlDataSource Properties</span></span>

<span data-ttu-id="8d6ab-173">以下是 SqlDataSource 控制件的一些屬性。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-173">The following are some of the properties of the SqlDataSource control.</span></span>

### <a name="cancelselectonnullparameter"></a><span data-ttu-id="8d6ab-174">取消選取的參數</span><span class="sxs-lookup"><span data-stu-id="8d6ab-174">CancelSelectOnNullParameter</span></span>

<span data-ttu-id="8d6ab-175">布爾值,用於指定如果其中一個參數為空,是否取消選擇命令。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-175">A Boolean value that specifies whether a select command is canceled if one of the parameters is null.</span></span> <span data-ttu-id="8d6ab-176">預設為 true。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-176">True by default.</span></span>

### <a name="conflictdetection"></a><span data-ttu-id="8d6ab-177">衝突偵測</span><span class="sxs-lookup"><span data-stu-id="8d6ab-177">ConflictDetection</span></span>

<span data-ttu-id="8d6ab-178">在多個使用者可能同時更新數據源的情況下,衝突檢測屬性確定 SqlDataSource 控制件的行為。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-178">In a situation where multiple users may be updating a data source at the same time, the ConflictDetection property determines the behavior of the SqlDataSource control.</span></span> <span data-ttu-id="8d6ab-179">此屬性計算為衝突選項枚舉的值之一。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-179">This property evaluates to one of the values of the ConflictOptions enumeration.</span></span> <span data-ttu-id="8d6ab-180">這些值是**比較所有值**與**覆寫變更**。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-180">Those values are **CompareAllValues** and **OverwriteChanges**.</span></span> <span data-ttu-id="8d6ab-181">如果設置為"覆蓋更改",則最後一個將數據寫入數據源的人員將覆蓋任何以前的更改。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-181">If set to OverwriteChanges, the last person to write data to the data source overwrites any previous changes.</span></span> <span data-ttu-id="8d6ab-182">但是,如果衝突檢測屬性設置為比較 AllValue,則為 SelectCommand 返回的列創建參數,並創建參數以在每個列中保存原始值,從而允許 SqlDataSource 確定自執行 SelectCommand 以來值是否已更改。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-182">However, if the ConflictDetection property is set to CompareAllValues, parameters get created for the columns returned by the SelectCommand and parameters are also created to hold the original values in each of those columns allowing the SqlDataSource to determine whether or not the values have changed since the SelectCommand was executed.</span></span>

### <a name="deletecommand"></a><span data-ttu-id="8d6ab-183">移除命令</span><span class="sxs-lookup"><span data-stu-id="8d6ab-183">DeleteCommand</span></span>

<span data-ttu-id="8d6ab-184">設定或取得從資料庫中刪除行時使用的 SQL 字串。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-184">Sets or gets the SQL string used when deleting rows from the database.</span></span> <span data-ttu-id="8d6ab-185">這可以是 SQL 查詢或儲存過程名稱。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-185">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="deletecommandtype"></a><span data-ttu-id="8d6ab-186">刪除指令型態</span><span class="sxs-lookup"><span data-stu-id="8d6ab-186">DeleteCommandType</span></span>

<span data-ttu-id="8d6ab-187">設置或獲取刪除命令的類型,SQL 查詢(文本)或存儲過程(存儲過程)。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-187">Sets or gets the type of delete command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="deleteparameters"></a><span data-ttu-id="8d6ab-188">刪除參數</span><span class="sxs-lookup"><span data-stu-id="8d6ab-188">DeleteParameters</span></span>

<span data-ttu-id="8d6ab-189">返回與 SqlDataSource 控制件關聯的 SqlDataSourceView 物件的 DeleteCommand 使用的參數。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-189">Returns the parameters that are used by the DeleteCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

### <a name="oldvaluesparameterformatstring"></a><span data-ttu-id="8d6ab-190">舊值參數格式字串</span><span class="sxs-lookup"><span data-stu-id="8d6ab-190">OldValuesParameterFormatString</span></span>

<span data-ttu-id="8d6ab-191">此屬性用於指定原始值參數的格式,在衝突檢測屬性設置為比較AllValue的情況下。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-191">This property is used to specify the format of the original value parameters in cases where the ConflictDetection property is set to CompareAllValues.</span></span> <span data-ttu-id="8d6ab-192">預設值表示{0}原始值參數的名稱與原始參數相同。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-192">The default is {0} which means that original value parameters will take the same name as the original parameter.</span></span> <span data-ttu-id="8d6ab-193">換句話說,如果欄位名稱稱為 EmployID,則原始值參數將@EmployeeID為 。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-193">In other words, if the field name is EmployeeID, the original value parameter would be @EmployeeID.</span></span>

### <a name="selectcommand"></a><span data-ttu-id="8d6ab-194">SelectCommand</span><span class="sxs-lookup"><span data-stu-id="8d6ab-194">SelectCommand</span></span>

<span data-ttu-id="8d6ab-195">設置或獲取用於從資料庫中檢索數據的 SQL 字串。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-195">Sets or gets the SQL string that is used to retrieve data from the database.</span></span> <span data-ttu-id="8d6ab-196">這可以是 SQL 查詢或儲存過程名稱。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-196">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="selectcommandtype"></a><span data-ttu-id="8d6ab-197">選擇指令型態</span><span class="sxs-lookup"><span data-stu-id="8d6ab-197">SelectCommandType</span></span>

<span data-ttu-id="8d6ab-198">設置或獲取選擇命令的類型,SQL 查詢(文本)或存儲過程(存儲過程)。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-198">Sets or gets the type of select command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="selectparameters"></a><span data-ttu-id="8d6ab-199">選擇參數</span><span class="sxs-lookup"><span data-stu-id="8d6ab-199">SelectParameters</span></span>

<span data-ttu-id="8d6ab-200">返回與 SqlDataSource 控制件關聯的 SqlDataSource 物件的 SelectCommand 使用的參數。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-200">Returns the parameters that are used by the SelectCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

### <a name="sortparametername"></a><span data-ttu-id="8d6ab-201">排序參數名稱</span><span class="sxs-lookup"><span data-stu-id="8d6ab-201">SortParameterName</span></span>

<span data-ttu-id="8d6ab-202">獲取或設置在排序數據來源控制元件檢索的資料時使用的儲存過程參數的名稱。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-202">Gets or sets the name of a stored procedure parameter that is used when sorting data retrieved by the data source control.</span></span> <span data-ttu-id="8d6ab-203">僅當 SelectCommandType 設定為儲存過程時才有效。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-203">Valid only when SelectCommandType is set to StoredProcedure.</span></span>

### <a name="sqlcachedependency"></a><span data-ttu-id="8d6ab-204">SqlCache 相依性</span><span class="sxs-lookup"><span data-stu-id="8d6ab-204">SqlCacheDependency</span></span>

<span data-ttu-id="8d6ab-205">指定 SQL Server 快取相依項中使用的資料庫和表的分號分隔字串。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-205">A semi-colon delimited string specifying the databases and tables used in a SQL Server cache dependency.</span></span> <span data-ttu-id="8d6ab-206">(SQL 緩存依賴項將在後面的模組中討論。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-206">(SQL cache dependencies will be discussed in a later module.)</span></span>

### <a name="updatecommand"></a><span data-ttu-id="8d6ab-207">更新命令</span><span class="sxs-lookup"><span data-stu-id="8d6ab-207">UpdateCommand</span></span>

<span data-ttu-id="8d6ab-208">設定或獲取更新資料庫中的數據時使用的 SQL 字串。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-208">Sets or gets the SQL string that is used when updating data in the database.</span></span> <span data-ttu-id="8d6ab-209">這可以是 SQL 查詢或儲存過程名稱。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-209">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="updatecommandtype"></a><span data-ttu-id="8d6ab-210">更新指令型態</span><span class="sxs-lookup"><span data-stu-id="8d6ab-210">UpdateCommandType</span></span>

<span data-ttu-id="8d6ab-211">設置或獲取更新命令的類型,SQL 查詢(文本)或存儲過程(存儲過程)。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-211">Sets or gets the type of update command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="updateparameters"></a><span data-ttu-id="8d6ab-212">更新參數</span><span class="sxs-lookup"><span data-stu-id="8d6ab-212">UpdateParameters</span></span>

<span data-ttu-id="8d6ab-213">返回與 SqlDataSource 控制件關聯的 SqlDataSourceView 物件的 UpdateCommand 使用的參數。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-213">Returns the parameters that are used by the UpdateCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

## <a name="the-accessdatasource-control"></a><span data-ttu-id="8d6ab-214">存取資料來源控制項</span><span class="sxs-lookup"><span data-stu-id="8d6ab-214">The AccessDataSource Control</span></span>

<span data-ttu-id="8d6ab-215">AccessDataSource 控制件派生自 SqlDataSource 類,用於將資料綁定到 Microsoft Access 資料庫。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-215">The AccessDataSource control derives from the SqlDataSource class and is used to data-bind to a Microsoft Access database.</span></span> <span data-ttu-id="8d6ab-216">AccessDataSource 控制項的 ConnectString 屬性是唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-216">The ConnectionString property for the AccessDataSource control is a read-only property.</span></span> <span data-ttu-id="8d6ab-217">DataFile 屬性使用"連接字串"屬性,而不是使用 ConnectString 屬性來指向訪問資料庫,如下所示。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-217">Instead of using the ConnectionString property, the DataFile property is used to point to the Access Database as shown below.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

<span data-ttu-id="8d6ab-218">AccessDataSource 將始終將基本 SqlDataSource 的提供程式名稱設置為系統.Data.OleDb,並使用 Microsoft.Jet.OLEDB.4.0 OLE DB 提供程式連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-218">The AccessDataSource will always set the ProviderName of the base SqlDataSource to System.Data.OleDb and connects to the database using the Microsoft.Jet.OLEDB.4.0 OLE DB provider.</span></span> <span data-ttu-id="8d6ab-219">不能使用 AccessDataSource 控制件連接到受密碼保護的訪問資料庫。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-219">You cannot use the AccessDataSource control to connect to a password-protected Access database.</span></span> <span data-ttu-id="8d6ab-220">如果必須連接到受密碼保護的資料庫,則應使用 SqlDataSource 控制項。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-220">If you have to connect to a password protected database, you should use the SqlDataSource control.</span></span>

> [!NOTE]
> <span data-ttu-id="8d6ab-221">存儲在網站中的訪問資料庫應放在應用\_數據目錄中。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-221">Access databases stored within the Web site should be placed in the App\_Data directory.</span></span> <span data-ttu-id="8d6ab-222">ASP.NET不允許瀏覽此目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-222">ASP.NET does not allow files in this directory to be browsed.</span></span> <span data-ttu-id="8d6ab-223">使用 Access 資料庫時,您需要\_向應用 資料目錄授予進程帳戶"讀取和寫入"許可權。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-223">You will need to grant the process account Read and Write permissions to the App\_Data directory when using Access databases.</span></span>

## <a name="the-xmldatasource-control"></a><span data-ttu-id="8d6ab-224">XmlDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="8d6ab-224">The XmlDataSource Control</span></span>

<span data-ttu-id="8d6ab-225">XmlDataSource 用於將資料綁定 XML 資料到資料綁定控制項。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-225">The XmlDataSource is used to data-bind XML data to data-bound controls.</span></span> <span data-ttu-id="8d6ab-226">您可以使用 DataFile 屬性結合 XML 檔,也可以使用 Data 屬性結合 XML 字串。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-226">You can bind to an XML file using the DataFile property or you can bind to an XML string using the Data property.</span></span> <span data-ttu-id="8d6ab-227">XmlDataSource 將 XML 屬性公開為可綁定欄位。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-227">The XmlDataSource exposes XML attributes as bindable fields.</span></span> <span data-ttu-id="8d6ab-228">如果需要綁定到未表示為屬性的值,則需要使用 XSL 轉換。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-228">In cases where you need to bind to values that are not represented as attributes, you will need to use an XSL transform.</span></span> <span data-ttu-id="8d6ab-229">您還可以使用 XPath 表示式來篩選 XML 資料。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-229">You can also use XPath expressions to filter XML data.</span></span>

<span data-ttu-id="8d6ab-230">請考慮以下 XML 檔:</span><span class="sxs-lookup"><span data-stu-id="8d6ab-230">Consider the following XML file:</span></span>

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

<span data-ttu-id="8d6ab-231">請注意,XmlDataSource 使用*人員/人員*的 XPath&lt;&gt;屬性來僅對人員 節點進行篩選。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-231">Notice that the XmlDataSource uses an XPath property of *People/Person* in order to filter on just the &lt;Person&gt; nodes.</span></span> <span data-ttu-id="8d6ab-232">然後,使用DataTextField屬性將數據綁定到姓氏屬性。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-232">The DropDownList then data-binds to the LastName attribute using the DataTextField property.</span></span>

<span data-ttu-id="8d6ab-233">雖然 XmlDataSource 控制件主要用於將數據綁定到唯讀的 XML 資料,但可以編輯 XML 資料檔。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-233">While the XmlDataSource control is primarily used to data-bind to read-only XML data, it is possible to edit the XML data file.</span></span> <span data-ttu-id="8d6ab-234">請注意,在這種情況下,自動插入、更新和刪除 XML 檔中的資訊不會像在其他數據源控制件中那樣自動發生。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-234">Note that in such cases, automatic insertion, updating, and deletion of information in the XML file does not happen automatically as it does with other data source controls.</span></span> <span data-ttu-id="8d6ab-235">相反,您必須編寫代碼才能使用 XmlDataSource 控制件的以下方法手動編輯數據。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-235">Instead, you will have to write code to manually edit the data using the following methods of the XmlDataSource control.</span></span>

### <a name="getxmldocument"></a><span data-ttu-id="8d6ab-236">取得Xml文件</span><span class="sxs-lookup"><span data-stu-id="8d6ab-236">GetXmlDocument</span></span>

<span data-ttu-id="8d6ab-237">檢索包含 XmlDataSource 檢索的 XML 代碼的 XmlDocument 物件。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-237">Retrieves an XmlDocument object containing the XML code retrieved by the XmlDataSource.</span></span>

### <a name="save"></a><span data-ttu-id="8d6ab-238">儲存</span><span class="sxs-lookup"><span data-stu-id="8d6ab-238">Save</span></span>

<span data-ttu-id="8d6ab-239">將記憶體中的 XmlDocument 儲存回資料來源。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-239">Saves the in-memory XmlDocument back to the data source.</span></span>

<span data-ttu-id="8d6ab-240">請務必瞭解,僅滿足以下兩個條件時,Save 方法才能工作:</span><span class="sxs-lookup"><span data-stu-id="8d6ab-240">It's important to realize that the Save method will only work when the following two conditions are met:</span></span>

1. <span data-ttu-id="8d6ab-241">XmlDataSource 正在使用 DataFile 屬性綁定到 XML 檔案,而不是資料屬性以綁定到記憶體中的 XML 資料。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-241">The XmlDataSource is using the DataFile property to bind to an XML file instead of the Data property to bind to in-memory XML data.</span></span>
2. <span data-ttu-id="8d6ab-242">不會透過『轉換』或「轉換檔」屬性指定轉換。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-242">No transformation is specified via the Transform or TransformFile property.</span></span>

<span data-ttu-id="8d6ab-243">另請注意,當多個用戶同時調用 Save 方法時,可能會產生意外的結果。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-243">Note also that the Save method can yield unexpected results when called by multiple users concurrently.</span></span>

## <a name="the-objectdatasource-control"></a><span data-ttu-id="8d6ab-244">物件資料來源控制項</span><span class="sxs-lookup"><span data-stu-id="8d6ab-244">The ObjectDataSource Control</span></span>

<span data-ttu-id="8d6ab-245">對於數據源控件直接與數據存儲通信的兩層應用程式而言,我們覆蓋的數據源控件是絕佳的選擇。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-245">The data source controls that we have covered up to this point are excellent choices for two-tier applications where the data source control communicates directly to the data store.</span></span> <span data-ttu-id="8d6ab-246">但是,許多實際應用程式是多層應用程式,其中數據源控件可能需要與業務物件通信,而業務物件又與數據層通信。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-246">However, many real-world applications are multi-tier applications where a data source control might need to communicate to a business object which, in turn, communicates with the data layer.</span></span> <span data-ttu-id="8d6ab-247">在這些情況下,ObjectDataSource 很好地填充了帳單。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-247">In these situations, the ObjectDataSource fills the bill nicely.</span></span> <span data-ttu-id="8d6ab-248">ObjectDataSource 與源物件結合使用。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-248">The ObjectDataSource works in conjunction with a source object.</span></span> <span data-ttu-id="8d6ab-249">如果物件具有實例方法而不是靜態方法(在 Visual Basic 中共用),則 ObjectDataSource 控制件將創建源物件的實例,調用指定的方法,並釋放物件實例。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-249">The ObjectDataSource control will create an instance of the source object, call the specified method, and dispose of the object instance all within the scope of a single request, if your object has instance methods instead of static methods (Shared in Visual Basic).</span></span> <span data-ttu-id="8d6ab-250">因此,對象必須是無狀態的。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-250">Therefore, your object must be stateless.</span></span> <span data-ttu-id="8d6ab-251">也就是說,對象應在單個請求的範圍內獲取和釋放所有必需的資源。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-251">That is, your object should acquire and release all required resources within the span of a single request.</span></span> <span data-ttu-id="8d6ab-252">您可以通過處理 ObjectDataSource 控制件的物件創建事件來控制來源物件的建立方式。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-252">You can control how the source object is created by handling the ObjectCreating event of the ObjectDataSource control.</span></span> <span data-ttu-id="8d6ab-253">您可以建立源物件的實例,然後將 ObjectDataSourceEventArgs 類的 ObjectInstance 屬性設置為該實例。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-253">You can create an instance of the source object, and then set the ObjectInstance property of the ObjectDataSourceEventArgs class to that instance.</span></span> <span data-ttu-id="8d6ab-254">ObjectDataSource 控制項使用在物件建立事件中建立的實體,而不是自行建立實例。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-254">The ObjectDataSource control will use the instance that is created in the ObjectCreating event instead of creating an instance on its own.</span></span>

<span data-ttu-id="8d6ab-255">如果 ObjectDataSource 控制件的源物件公開可呼叫以檢索和修改資料的公共靜態方法(在 Visual Basic 中共用),則 ObjectDataSource 控制件將直接呼叫這些方法。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-255">If the source object for an ObjectDataSource control exposes public static methods (Shared in Visual Basic) that can be called to retrieve and modify data, an ObjectDataSource control will call those methods directly.</span></span> <span data-ttu-id="8d6ab-256">如果 ObjectDataSource 控制項必須建立源物件的實例才能進行方法呼叫,則該物件必須包括一個不採用任何參數的公共構造函數。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-256">If an ObjectDataSource control must create an instance of the source object in order to make method calls, the object must include a public constructor that takes no parameters.</span></span> <span data-ttu-id="8d6ab-257">當 ObjectDataSource 控制件建立源物件的新實例時,它將調用此建構函數。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-257">The ObjectDataSource control will call this constructor when it creates a new instance of the source object.</span></span>

<span data-ttu-id="8d6ab-258">如果源物件不包含沒有參數的公共構造函數,則可以創建源物件的實例,該實例將由 ObjectDataSource 控制件在 ObjectCreate 事件中使用。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-258">If the source object does not contain a public constructor without parameters, you can create an instance of the source object that will be used by the ObjectDataSource control in the ObjectCreating event.</span></span>

## <a name="specifying-object-methods"></a><span data-ttu-id="8d6ab-259">指定物件方法</span><span class="sxs-lookup"><span data-stu-id="8d6ab-259">Specifying Object Methods</span></span>

<span data-ttu-id="8d6ab-260">ObjectDataSource 控制項的來源物件可以包含任何任何數量的用於選擇、插入、更新或刪除資料的方法。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-260">The source object for an ObjectDataSource control can contain any number of methods that are used to select, insert, update, or delete data.</span></span> <span data-ttu-id="8d6ab-261">這些方法由基於方法名稱的 ObjectDataSource 控制件呼叫,使用 ObjectDataSource 控制項的 SelectMethod、插入方法、更新方法或 DeleteMethod 屬性識別。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-261">These methods are called by the ObjectDataSource control based on the name of the method, as identified by using either the SelectMethod, InsertMethod, UpdateMethod, or DeleteMethod property of the ObjectDataSource control.</span></span> <span data-ttu-id="8d6ab-262">源物件還可以包括可選的 SelectCount 方法,該方法由使用 SelectCountMethod 屬性的 ObjectDataSource 控制件標識,該方法返回數據源中物件總數的計數。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-262">The source object can also include an optional SelectCount method, which is identified by the ObjectDataSource control using the SelectCountMethod property, that returns the count of the total number of objects at the data source.</span></span> <span data-ttu-id="8d6ab-263">在調用 Select 方法以檢索資料來源中用於分頁時的記錄總數後,ObjectDataSource 控制件將調用 SelectCount 方法。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-263">The ObjectDataSource control will call the SelectCount method after a Select method has been called to retrieve the total number of records at the data source for use when paging.</span></span>

## <a name="lab-using-data-source-controls"></a><span data-ttu-id="8d6ab-264">使用資料來源控制項的實驗室</span><span class="sxs-lookup"><span data-stu-id="8d6ab-264">Lab Using Data Source Controls</span></span>

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a><span data-ttu-id="8d6ab-265">練習 1 - 使用 SqlDataSource 控制項顯示資料</span><span class="sxs-lookup"><span data-stu-id="8d6ab-265">Exercise 1 - Displaying Data with the SqlDataSource Control</span></span>

<span data-ttu-id="8d6ab-266">以下練習使用 SqlDataSource 控制件連接到北風資料庫。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-266">The following exercise uses the SqlDataSource control to connect to the Northwind database.</span></span> <span data-ttu-id="8d6ab-267">它假定您可以訪問 SQL Server 2000 實例上的北風資料庫。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-267">It assumes that you have access to the Northwind database on a SQL Server 2000 instance.</span></span>

1. <span data-ttu-id="8d6ab-268">建立新的 ASP.NET 網站。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-268">Create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="8d6ab-269">添加新的 Web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-269">Add a new web.config file.</span></span>

    1. <span data-ttu-id="8d6ab-270">右鍵單擊解決方案資源管理器中的專案,然後單擊"添加新專案"。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-270">Right-click on the project in Solution Explorer and click Add New Item.</span></span>
    2. <span data-ttu-id="8d6ab-271">從樣本清單中選擇 Web 設定檔,然後單擊" 添加"</span><span class="sxs-lookup"><span data-stu-id="8d6ab-271">Choose Web Configuration File from the list of templates and click Add.</span></span>
3. <span data-ttu-id="8d6ab-272">編輯&lt;連接字串&gt;部份,如下所示:</span><span class="sxs-lookup"><span data-stu-id="8d6ab-272">Edit the &lt;connectionStrings&gt; section as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. <span data-ttu-id="8d6ab-273">切換到代碼檢視,並將連接String 屬性和 SelectCommand 屬性&lt;新增到 asp:SqlDataSource&gt;控制件,如下所示:</span><span class="sxs-lookup"><span data-stu-id="8d6ab-273">Switch to Code view and add a ConnectionString attribute and a SelectCommand attribute to the &lt;asp:SqlDataSource&gt; control as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. <span data-ttu-id="8d6ab-274">從"設計"視圖中,添加新的 GridView 控件。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-274">From Design view, add a new GridView control.</span></span>
6. <span data-ttu-id="8d6ab-275">從 GridView 工作選單中的「選擇資料源」下拉清單,選擇 SqlDataSource1。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-275">From the Choose Data Source dropdown in the GridView Tasks menu, choose SqlDataSource1.</span></span>
7. <span data-ttu-id="8d6ab-276">右鍵按一下 Default.aspx,然後從菜單中選擇「在瀏覽器中查看」。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-276">Right-click on Default.aspx and choose View in Browser from the menu.</span></span> <span data-ttu-id="8d6ab-277">當提示保存時,單擊"是"。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-277">Click Yes when prompted to save.</span></span>
8. <span data-ttu-id="8d6ab-278">GridView 顯示"產品"表中的數據。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-278">The GridView displays the data from the Products table.</span></span>

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a><span data-ttu-id="8d6ab-279">練習 2 - 使用 SqlDataSource 控制件編輯資料</span><span class="sxs-lookup"><span data-stu-id="8d6ab-279">Exercise 2 - Editing Data with the SqlDataSource Control</span></span>

<span data-ttu-id="8d6ab-280">下面的練習演示如何使用聲明性語法對下拉清單控件進行數據綁定,並允許您編輯下拉清單控件中顯示的數據。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-280">The following exercise demonstrates how to data bind a DropDownList control using the declarative syntax and allows you to edit the data presented in the DropDownList control.</span></span>

1. <span data-ttu-id="8d6ab-281">在"設計"檢視中,從 Default.aspx 中刪除 GridView 控件。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-281">In Design view, delete the GridView control from Default.aspx.</span></span> 

    <span data-ttu-id="8d6ab-282">**重要提示**:將 SqlDataSource 控制件保留在頁面上。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-282">**Important**: Leave the SqlDataSource control on the page.</span></span>
2. <span data-ttu-id="8d6ab-283">將下拉清單控制件添加到 Default.aspx。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-283">Add a DropDownList control to Default.aspx.</span></span>
3. <span data-ttu-id="8d6ab-284">切換到源視圖。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-284">Switch to Source view.</span></span>
4. <span data-ttu-id="8d6ab-285">將 DataSourceId、資料文字欄位和 DataValueField&lt;屬性加入 asp:下拉&gt;清單控制項,如下所示:</span><span class="sxs-lookup"><span data-stu-id="8d6ab-285">Add a DataSourceId, DataTextField, and DataValueField attribute to the &lt;asp:DropDownList&gt; control as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. <span data-ttu-id="8d6ab-286">保存預設.aspx 並在瀏覽器中查看它。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-286">Save Default.aspx and view it in the browser.</span></span> <span data-ttu-id="8d6ab-287">請注意,下拉清單包含來自北風資料庫的所有產品。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-287">Note that the DropDownList contains all of the products from the Northwind database.</span></span>
6. <span data-ttu-id="8d6ab-288">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-288">Close the browser.</span></span>
7. <span data-ttu-id="8d6ab-289">在 Default.aspx 的來源檢視中,在下拉清單控制元件下方添加新的 TextBox 控制件。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-289">In Source view of Default.aspx, add a new TextBox control below the DropDownList control.</span></span> <span data-ttu-id="8d6ab-290">將 TextBox 的 ID 屬性更改為 txtProduct 名稱。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-290">Change the ID property of the TextBox to txtProductName.</span></span>
8. <span data-ttu-id="8d6ab-291">在「文字框」控件下,添加新的「按鈕」控制件。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-291">Under the TextBox control, add a new Button control.</span></span> <span data-ttu-id="8d6ab-292">將按鈕的 ID 屬性更改為 btnUpdate,將文本屬性更改為 **「更新產品名稱**」 。。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-292">Change the ID property of the Button to btnUpdate and the Text property to **Update Product Name**.</span></span>
9. <span data-ttu-id="8d6ab-293">在 Default.aspx 的源檢視中,向 SqlDataSource 標籤新增 UpdateCommand 屬性和兩個新的 Update 參數,如下所示:</span><span class="sxs-lookup"><span data-stu-id="8d6ab-293">In Source view of Default.aspx, add an UpdateCommand property and two new UpdateParameters to the SqlDataSource tag as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > <span data-ttu-id="8d6ab-294">請注意,此代碼中添加了兩個更新參數(產品名稱和產品ID)。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-294">Note that there are two update parameters (ProductName and ProductID) added in this code.</span></span> <span data-ttu-id="8d6ab-295">這些參數映射到 txtProduct 名稱文字框的文本屬性和 ddlProducts 下拉清單的「選定值」屬性。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-295">These parameters are mapped to the Text property of the txtProductName TextBox and the SelectedValue property of the ddlProducts DropDownList.</span></span>
10. <span data-ttu-id="8d6ab-296">切換到"設計"檢視並按兩下"按鈕"控制項以添加事件處理程式。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-296">Switch to Design view and double-click on the Button control to add an event handler.</span></span>
11. <span data-ttu-id="8d6ab-297">將以下代碼加入 btnUpdate\_按一個程式碼:</span><span class="sxs-lookup"><span data-stu-id="8d6ab-297">Add the following code to the btnUpdate\_Click code:</span></span> 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. <span data-ttu-id="8d6ab-298">右鍵按一下 Default.aspx 並選擇在瀏覽器中查看它。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-298">Right-click on Default.aspx and choose to view it in the browser.</span></span> <span data-ttu-id="8d6ab-299">當提示保存所有更改時,按一下「是」。。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-299">Click Yes when prompted to save all changes.</span></span>
13. <span data-ttu-id="8d6ab-300">ASP.NET 2.0 部分類允許在運行時進行編譯。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-300">ASP.NET 2.0 partial classes allow for compilation at runtime.</span></span> <span data-ttu-id="8d6ab-301">無需構建應用程式,以便看到代碼更改生效。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-301">It is not necessary to build an application in order to see code changes take effect.</span></span>
14. <span data-ttu-id="8d6ab-302">從下拉清單中選擇產品。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-302">Select a product from the DropDownList.</span></span>
15. <span data-ttu-id="8d6ab-303">在 TextBox 中輸入所選產品的新名稱,然後單擊"更新"按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-303">Enter a new name for the selected product in the TextBox and then click the Update button.</span></span>
16. <span data-ttu-id="8d6ab-304">產品名稱在資料庫中更新。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-304">The product name is updated in the database.</span></span>

## <a name="exercise-3-using-the-objectdatasource-control"></a><span data-ttu-id="8d6ab-305">練習 3 使用物件資料來源控制項</span><span class="sxs-lookup"><span data-stu-id="8d6ab-305">Exercise 3 Using the ObjectDataSource Control</span></span>

<span data-ttu-id="8d6ab-306">本練習將演示如何使用ObjectDataSource控制件和來源物件與Northwind資料庫進行互動。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-306">This exercise will demonstrate how to use the ObjectDataSource control and a source object to interact with the Northwind database.</span></span>

1. <span data-ttu-id="8d6ab-307">右鍵單擊解決方案資源管理器中的專案,然後單擊"添加新專案"。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-307">Right-click on the project in Solution Explorer and click on Add New Item.</span></span>
2. <span data-ttu-id="8d6ab-308">在範本清單中選擇"Web 窗體"。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-308">Select Web Form in the templates list.</span></span> <span data-ttu-id="8d6ab-309">將名稱更改為物件.aspx,然後單擊"添加"。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-309">Change the name to object.aspx and click Add.</span></span>
3. <span data-ttu-id="8d6ab-310">右鍵單擊解決方案資源管理器中的專案,然後單擊"添加新專案"。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-310">Right-click on the project in Solution Explorer and click on Add New Item.</span></span>
4. <span data-ttu-id="8d6ab-311">在樣本清單中選擇類。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-311">Select Class in the templates list.</span></span> <span data-ttu-id="8d6ab-312">將類的名稱更改為NorthwindData.cs,然後單擊"添加"。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-312">Change the name of the class to NorthwindData.cs and click Add.</span></span>
5. <span data-ttu-id="8d6ab-313">當提示將類添加到應用\_代碼資料夾時,按一下"是"</span><span class="sxs-lookup"><span data-stu-id="8d6ab-313">Click Yes when prompted to add the class to the App\_Code folder.</span></span>
6. <span data-ttu-id="8d6ab-314">將以下代碼加入NorthwindData.cs檔:</span><span class="sxs-lookup"><span data-stu-id="8d6ab-314">Add the following code to the NorthwindData.cs file:</span></span> 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. <span data-ttu-id="8d6ab-315">將以下代碼加入物件的「原始程式」檢視.</span><span class="sxs-lookup"><span data-stu-id="8d6ab-315">Add the following code to the Source view of object.aspx:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. <span data-ttu-id="8d6ab-316">保存所有文件和流覽物件.aspx。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-316">Save all files and browse object.aspx.</span></span>
9. <span data-ttu-id="8d6ab-317">通過詳細資訊、編輯員工、添加員工和刪除員工與介面進行互動。</span><span class="sxs-lookup"><span data-stu-id="8d6ab-317">Interact with the interface by viewing details, editing employees, adding employees, and deleting employees.</span></span>
