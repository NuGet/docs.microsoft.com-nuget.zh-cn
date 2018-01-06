---
title: "目录、 NuGet V3 API |Microsoft 文档"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/30/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cfd338b5-6253-48c0-88ba-17c6b98fc935
description: "目录是创建和删除在 nuget.org 上的所有包的索引。"
keywords: "NuGet V3 API 目录，nuget.org 事务日志复制 NuGet.org、 克隆 NuGet.org，NuGet.org 的仅限追加的记录"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 4c98b7cbd92575f6905e98a5bca5602a4d8ac0dd
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="catalog"></a><span data-ttu-id="106bf-104">Catalog</span><span class="sxs-lookup"><span data-stu-id="106bf-104">Catalog</span></span>

<span data-ttu-id="106bf-105">**目录**是记录上的包源，如创建和删除的所有包操作的资源。</span><span class="sxs-lookup"><span data-stu-id="106bf-105">The **catalog** is a resource that records all package operations on a package source, such as creations and deletions.</span></span> <span data-ttu-id="106bf-106">目录资源具有`Catalog`键入[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="106bf-106">The catalog resource has the `Catalog` type in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="106bf-107">由于官方 NuGet 客户端不使用该目录，并非所有包源都实现目录。</span><span class="sxs-lookup"><span data-stu-id="106bf-107">Because the catalog is not used by the official NuGet client, not all package sources implement the catalog.</span></span>

> [!Note]
> <span data-ttu-id="106bf-108">目前，nuget.org 目录不是在中国提供的。</span><span class="sxs-lookup"><span data-stu-id="106bf-108">Currently, the nuget.org catalog is not available in China.</span></span> <span data-ttu-id="106bf-109">有关更多详细信息，请参阅[NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949)。</span><span class="sxs-lookup"><span data-stu-id="106bf-109">For more details, see [NuGet/NuGetGallery#4949](https://github.com/NuGet/NuGetGallery/issues/4949).</span></span>

## <a name="versioning"></a><span data-ttu-id="106bf-110">版本管理</span><span class="sxs-lookup"><span data-stu-id="106bf-110">Versioning</span></span>

<span data-ttu-id="106bf-111">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="106bf-111">The following `@type` value is used:</span></span>

<span data-ttu-id="106bf-112">@type 值</span><span class="sxs-lookup"><span data-stu-id="106bf-112">@type value</span></span>   | <span data-ttu-id="106bf-113">说明</span><span class="sxs-lookup"><span data-stu-id="106bf-113">Notes</span></span>
------------- | -----
<span data-ttu-id="106bf-114">Catalog/3.0.0</span><span class="sxs-lookup"><span data-stu-id="106bf-114">Catalog/3.0.0</span></span> | <span data-ttu-id="106bf-115">初始版本</span><span class="sxs-lookup"><span data-stu-id="106bf-115">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="106bf-116">基 URL</span><span class="sxs-lookup"><span data-stu-id="106bf-116">Base URL</span></span>

<span data-ttu-id="106bf-117">以下 Api 的入口点 URL 是值的`@id`与前面提到的资源关联的属性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="106bf-117">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` values.</span></span> <span data-ttu-id="106bf-118">本主题使用的占位符 URL `{@id}`。</span><span class="sxs-lookup"><span data-stu-id="106bf-118">This topic uses the placeholder URL `{@id}`.</span></span>

## <a name="http-methods"></a><span data-ttu-id="106bf-119">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="106bf-119">HTTP methods</span></span>

<span data-ttu-id="106bf-120">只有的 HTTP 方法位于目录资源支持的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="106bf-120">All URLs found in the catalog resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="catalog-index"></a><span data-ttu-id="106bf-121">目录索引</span><span class="sxs-lookup"><span data-stu-id="106bf-121">Catalog index</span></span>

<span data-ttu-id="106bf-122">目录索引是拥有的目录项，排序 cronologically 列表的已知位置中的文档。</span><span class="sxs-lookup"><span data-stu-id="106bf-122">The catalog index is a document in a well-known location that has a list of catalog items, ordered cronologically.</span></span> <span data-ttu-id="106bf-123">它是目录资源的入口点。</span><span class="sxs-lookup"><span data-stu-id="106bf-123">It is the entry point of the catalog resource.</span></span>

<span data-ttu-id="106bf-124">索引组成目录页。</span><span class="sxs-lookup"><span data-stu-id="106bf-124">The index is comprised of catalog pages.</span></span> <span data-ttu-id="106bf-125">每个目录页包含目录项。</span><span class="sxs-lookup"><span data-stu-id="106bf-125">Each catalog page contains catalog items.</span></span> <span data-ttu-id="106bf-126">每个目录项表示时间有关的某个点单个包的事件。</span><span class="sxs-lookup"><span data-stu-id="106bf-126">Each catalog item represents an event concerning a single package at a point in time.</span></span> <span data-ttu-id="106bf-127">目录项可以表示已创建，未列出的、 重新列，或已删除程序包源中的包。</span><span class="sxs-lookup"><span data-stu-id="106bf-127">A catalog item can represent a package that was created, unlisted, relisted, or deleted from the package source.</span></span> <span data-ttu-id="106bf-128">通过处理按时间顺序的目录项，客户端可以生成 V3 包源上存在的每个包的最新视图。</span><span class="sxs-lookup"><span data-stu-id="106bf-128">By processing the catalog items in chronological order, the client can build an up-to-date view of every package that exists on the V3 package source.</span></span>

<span data-ttu-id="106bf-129">简单地说，目录的 blob 具有以下层次结构：</span><span class="sxs-lookup"><span data-stu-id="106bf-129">In short, catalog blobs have the following hierarchical structure:</span></span>

- <span data-ttu-id="106bf-130">**索引**: 目录的入口点。</span><span class="sxs-lookup"><span data-stu-id="106bf-130">**Index**: the entry point for the catalog.</span></span>
- <span data-ttu-id="106bf-131">**页**： 目录项的分组。</span><span class="sxs-lookup"><span data-stu-id="106bf-131">**Page**: a grouping of catalog items.</span></span>
- <span data-ttu-id="106bf-132">**叶**： 表示一个目录项，它是单个包的状态的快照的文档。</span><span class="sxs-lookup"><span data-stu-id="106bf-132">**Leaf**: a document representing a catalog item, which is a snapshot of a single package's state.</span></span>

<span data-ttu-id="106bf-133">每个目录对象具有一个名为属性`commitTimeStamp`表示项添加到目录时。</span><span class="sxs-lookup"><span data-stu-id="106bf-133">Each catalog object has a property called the `commitTimeStamp` representing when the item was added to the catalog.</span></span> <span data-ttu-id="106bf-134">目录项添加到名为提交的批次中的目录页中。</span><span class="sxs-lookup"><span data-stu-id="106bf-134">Catalog items are added to a catalog page in batches called commits.</span></span> <span data-ttu-id="106bf-135">中的相同的提交的所有目录项都具有相同的提交时间戳 (`commitTimeStamp`) 并提交 ID (`commitId`)。</span><span class="sxs-lookup"><span data-stu-id="106bf-135">All catalog items in the same commit have the same commit timestamp (`commitTimeStamp`) and commit ID (`commitId`).</span></span> <span data-ttu-id="106bf-136">目录项放置在同一个提交表示时间上的包源绕相同点发生的事件。</span><span class="sxs-lookup"><span data-stu-id="106bf-136">Catalog items placed in the same commit represent events that happened around the same point in time on the package source.</span></span> <span data-ttu-id="106bf-137">目录提交内没有排序。</span><span class="sxs-lookup"><span data-stu-id="106bf-137">There is no ordering within a catalog commit.</span></span>

<span data-ttu-id="106bf-138">因为每个包 ID 和版本是唯一的将永远不会有多个目录项目中提交。</span><span class="sxs-lookup"><span data-stu-id="106bf-138">Because each package ID and version is unique, there will never be more than one catalog item in a commit.</span></span> <span data-ttu-id="106bf-139">这可确保，在单个包的目录项可以始终是明确相对于排序的提交时间戳。</span><span class="sxs-lookup"><span data-stu-id="106bf-139">This ensures that catalog items for a single package can always be unambiguously ordered with respect to commit timestamp.</span></span>

<span data-ttu-id="106bf-140">永远不会将多个提交给每个目录`commitTimeStamp`。</span><span class="sxs-lookup"><span data-stu-id="106bf-140">There is never be more than one commit to the catalog per `commitTimeStamp`.</span></span> <span data-ttu-id="106bf-141">换而言之，`commitId`是冗余的`commitTimeStamp`。</span><span class="sxs-lookup"><span data-stu-id="106bf-141">In other words, the `commitId` is redundant with the `commitTimeStamp`.</span></span>

<span data-ttu-id="106bf-142">与此相反[package 元数据资源](registration-base-url-resource.md)，哪些索引按包 ID，该目录是索引 （和可查询） 只能由时间。</span><span class="sxs-lookup"><span data-stu-id="106bf-142">In contrast to the [package metadata resource](registration-base-url-resource.md), which is indexed by package ID, the catalog is indexed (and queryable) only by time.</span></span>

<span data-ttu-id="106bf-143">目录项始终添加到单调递增，按时间顺序排列的顺序目录中。</span><span class="sxs-lookup"><span data-stu-id="106bf-143">Catalog items are always added to the catalog in a monotonically increasing, chronological order.</span></span> <span data-ttu-id="106bf-144">这意味着，如果在时间 X 添加目录提交，则没有目录提交将不断添加带有时间小于或等于为 X。</span><span class="sxs-lookup"><span data-stu-id="106bf-144">This means that if a catalog commit is added at time X then no catalog commit will ever be added with a time less than or equal to X.</span></span>

<span data-ttu-id="106bf-145">以下请求获取目录索引。</span><span class="sxs-lookup"><span data-stu-id="106bf-145">The following request fetches the catalog index.</span></span>

```
GET {@id}
```

<span data-ttu-id="106bf-146">目录索引是包含具有以下属性的对象的 JSON 文档：</span><span class="sxs-lookup"><span data-stu-id="106bf-146">The catalog index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="106bf-147">name</span><span class="sxs-lookup"><span data-stu-id="106bf-147">Name</span></span>            | <span data-ttu-id="106bf-148">类型</span><span class="sxs-lookup"><span data-stu-id="106bf-148">Type</span></span>             | <span data-ttu-id="106bf-149">必需</span><span class="sxs-lookup"><span data-stu-id="106bf-149">Required</span></span> | <span data-ttu-id="106bf-150">说明</span><span class="sxs-lookup"><span data-stu-id="106bf-150">Notes</span></span>
--------------- | ---------------- | -------- | -----
<span data-ttu-id="106bf-151">commitId</span><span class="sxs-lookup"><span data-stu-id="106bf-151">commitId</span></span>        | <span data-ttu-id="106bf-152">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-152">string</span></span>           | <span data-ttu-id="106bf-153">是</span><span class="sxs-lookup"><span data-stu-id="106bf-153">yes</span></span>      | <span data-ttu-id="106bf-154">与最新提交关联的唯一 ID</span><span class="sxs-lookup"><span data-stu-id="106bf-154">A unique ID associated with the most recent commit</span></span>
<span data-ttu-id="106bf-155">commitTimeStamp</span><span class="sxs-lookup"><span data-stu-id="106bf-155">commitTimeStamp</span></span> | <span data-ttu-id="106bf-156">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-156">string</span></span>           | <span data-ttu-id="106bf-157">是</span><span class="sxs-lookup"><span data-stu-id="106bf-157">yes</span></span>      | <span data-ttu-id="106bf-158">最新的提交时间戳</span><span class="sxs-lookup"><span data-stu-id="106bf-158">A timestamp of the most recent commit</span></span>
<span data-ttu-id="106bf-159">count</span><span class="sxs-lookup"><span data-stu-id="106bf-159">count</span></span>           | <span data-ttu-id="106bf-160">整数</span><span class="sxs-lookup"><span data-stu-id="106bf-160">integer</span></span>          | <span data-ttu-id="106bf-161">是</span><span class="sxs-lookup"><span data-stu-id="106bf-161">yes</span></span>      | <span data-ttu-id="106bf-162">在索引中的页面数</span><span class="sxs-lookup"><span data-stu-id="106bf-162">The number of pages in the index</span></span>
<span data-ttu-id="106bf-163">项</span><span class="sxs-lookup"><span data-stu-id="106bf-163">items</span></span>           | <span data-ttu-id="106bf-164">对象的数组</span><span class="sxs-lookup"><span data-stu-id="106bf-164">array of objects</span></span> | <span data-ttu-id="106bf-165">是</span><span class="sxs-lookup"><span data-stu-id="106bf-165">yes</span></span>      | <span data-ttu-id="106bf-166">对象，表示页每个对象的数组</span><span class="sxs-lookup"><span data-stu-id="106bf-166">A array of objects, each object representing a page</span></span>

<span data-ttu-id="106bf-167">在每个元素`items`数组是具有一些有关每个页面的最小的详细信息的对象。</span><span class="sxs-lookup"><span data-stu-id="106bf-167">Each element in the `items` array is an object with some minimal details about each page.</span></span> <span data-ttu-id="106bf-168">这些页对象不包含目录叶 （项）。</span><span class="sxs-lookup"><span data-stu-id="106bf-168">These page objects do not contain the catalog leaves (items).</span></span> <span data-ttu-id="106bf-169">未定义此数组中元素的顺序。</span><span class="sxs-lookup"><span data-stu-id="106bf-169">The order of the elements in this array is not defined.</span></span> <span data-ttu-id="106bf-170">可以按内存使用中的客户端排序页其`commitTimeStamp`属性。</span><span class="sxs-lookup"><span data-stu-id="106bf-170">Pages can be ordered by the client in memory using their `commitTimeStamp` property.</span></span>

<span data-ttu-id="106bf-171">引入新的页，`count`将递增，并且新的对象将会显示在`items`数组。</span><span class="sxs-lookup"><span data-stu-id="106bf-171">As new pages are introduced, the `count` will be incremented and new objects will appear in the `items` array.</span></span>

<span data-ttu-id="106bf-172">将项目添加到目录，索引的`commitId`将更改和`commitTimeStamp`将增加。</span><span class="sxs-lookup"><span data-stu-id="106bf-172">As items are added to the catalog, the index's `commitId` will change and the `commitTimeStamp` will increase.</span></span> <span data-ttu-id="106bf-173">这两个属性均通过所有页实质上是摘要`commitId`和`commitTimeStamp`中值`items`数组。</span><span class="sxs-lookup"><span data-stu-id="106bf-173">These two properties are essentially a summary over all page `commitId` and `commitTimeStamp` values in the `items` array.</span></span>

### <a name="catalog-page-object-in-the-index"></a><span data-ttu-id="106bf-174">在索引中的目录 page 对象</span><span class="sxs-lookup"><span data-stu-id="106bf-174">Catalog page object in the index</span></span>

<span data-ttu-id="106bf-175">目录索引中找到的目录页对象`items`属性具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="106bf-175">The catalog page objects found in the catalog index's `items` property have the following properties:</span></span>

<span data-ttu-id="106bf-176">name</span><span class="sxs-lookup"><span data-stu-id="106bf-176">Name</span></span>            | <span data-ttu-id="106bf-177">类型</span><span class="sxs-lookup"><span data-stu-id="106bf-177">Type</span></span>    | <span data-ttu-id="106bf-178">必需</span><span class="sxs-lookup"><span data-stu-id="106bf-178">Required</span></span> | <span data-ttu-id="106bf-179">说明</span><span class="sxs-lookup"><span data-stu-id="106bf-179">Notes</span></span>
--------------- | ------- | -------- | -----
@id             | <span data-ttu-id="106bf-180">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-180">string</span></span>  | <span data-ttu-id="106bf-181">是</span><span class="sxs-lookup"><span data-stu-id="106bf-181">yes</span></span>      | <span data-ttu-id="106bf-182">到提取目录页 URL</span><span class="sxs-lookup"><span data-stu-id="106bf-182">The URL to fetch catalog page</span></span>
<span data-ttu-id="106bf-183">commitId</span><span class="sxs-lookup"><span data-stu-id="106bf-183">commitId</span></span>        | <span data-ttu-id="106bf-184">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-184">string</span></span>  | <span data-ttu-id="106bf-185">是</span><span class="sxs-lookup"><span data-stu-id="106bf-185">yes</span></span>      | <span data-ttu-id="106bf-186">在此页中的最新提交与关联的唯一 ID</span><span class="sxs-lookup"><span data-stu-id="106bf-186">A unique ID associated with the most recent commit in this page</span></span>
<span data-ttu-id="106bf-187">commitTimeStamp</span><span class="sxs-lookup"><span data-stu-id="106bf-187">commitTimeStamp</span></span> | <span data-ttu-id="106bf-188">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-188">string</span></span>  | <span data-ttu-id="106bf-189">是</span><span class="sxs-lookup"><span data-stu-id="106bf-189">yes</span></span>      | <span data-ttu-id="106bf-190">在此页中的最新提交的时间戳</span><span class="sxs-lookup"><span data-stu-id="106bf-190">A timestamp of the most recent commit in this page</span></span>
<span data-ttu-id="106bf-191">count</span><span class="sxs-lookup"><span data-stu-id="106bf-191">count</span></span>           | <span data-ttu-id="106bf-192">整数</span><span class="sxs-lookup"><span data-stu-id="106bf-192">integer</span></span> | <span data-ttu-id="106bf-193">是</span><span class="sxs-lookup"><span data-stu-id="106bf-193">yes</span></span>      | <span data-ttu-id="106bf-194">在目录页中的项的数目</span><span class="sxs-lookup"><span data-stu-id="106bf-194">The number of items in the catalog page</span></span>

<span data-ttu-id="106bf-195">与此相反[package 元数据资源](registration-base-url-resource.md)这在某些情况下，内联离开到索引，因此目录叶是永远不会内联到索引，始终必须通过使用页面的提取`@id`URL。</span><span class="sxs-lookup"><span data-stu-id="106bf-195">In contrast to the [package metadata resource](registration-base-url-resource.md) which in some cases inlines leaves into the index, catalog leaves are never inlined into the index and must always be fetched by using the page's `@id` URL.</span></span>

### <a name="sample-request"></a><span data-ttu-id="106bf-196">示例请求</span><span class="sxs-lookup"><span data-stu-id="106bf-196">Sample request</span></span>

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a><span data-ttu-id="106bf-197">示例响应</span><span class="sxs-lookup"><span data-stu-id="106bf-197">Sample response</span></span>

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a><span data-ttu-id="106bf-198">目录页</span><span class="sxs-lookup"><span data-stu-id="106bf-198">Catalog page</span></span>

<span data-ttu-id="106bf-199">目录页是目录项的集合。</span><span class="sxs-lookup"><span data-stu-id="106bf-199">The catalog page is a collection of catalog items.</span></span> <span data-ttu-id="106bf-200">这是提取使用之一的文档`@id`目录索引中找到的值。</span><span class="sxs-lookup"><span data-stu-id="106bf-200">It is a document fetched using one of the `@id` values found in the catalog index.</span></span> <span data-ttu-id="106bf-201">目录页的 URL 不应为可预测，并应使用只是目录索引发现。</span><span class="sxs-lookup"><span data-stu-id="106bf-201">The URL to a catalog page is not intended to be predictable and should be discovered using only the catalog index.</span></span>

<span data-ttu-id="106bf-202">中只能与最高的提交时间戳的目录索引页或到新页添加新的目录项。</span><span class="sxs-lookup"><span data-stu-id="106bf-202">New catalog items are added to the page in the catalog index only with the highest commit timestamp or to a new page.</span></span> <span data-ttu-id="106bf-203">一旦具有更高版本的提交时间戳的页添加到目录中，较早的页面永远不会添加或更改。</span><span class="sxs-lookup"><span data-stu-id="106bf-203">Once a page with a higher commit timestamp is added to the catalog, older pages are never added to or changed.</span></span>

<span data-ttu-id="106bf-204">编录页文档是具有以下属性的 JSON 对象：</span><span class="sxs-lookup"><span data-stu-id="106bf-204">The catalog page document is a JSON object with the following properties:</span></span>

<span data-ttu-id="106bf-205">name</span><span class="sxs-lookup"><span data-stu-id="106bf-205">Name</span></span>            | <span data-ttu-id="106bf-206">类型</span><span class="sxs-lookup"><span data-stu-id="106bf-206">Type</span></span>             | <span data-ttu-id="106bf-207">必需</span><span class="sxs-lookup"><span data-stu-id="106bf-207">Required</span></span> | <span data-ttu-id="106bf-208">说明</span><span class="sxs-lookup"><span data-stu-id="106bf-208">Notes</span></span>
--------------- | ---------------- | -------- | -----
<span data-ttu-id="106bf-209">commitId</span><span class="sxs-lookup"><span data-stu-id="106bf-209">commitId</span></span>        | <span data-ttu-id="106bf-210">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-210">string</span></span>           | <span data-ttu-id="106bf-211">是</span><span class="sxs-lookup"><span data-stu-id="106bf-211">yes</span></span>      | <span data-ttu-id="106bf-212">在此页中的最新提交与关联的唯一 ID</span><span class="sxs-lookup"><span data-stu-id="106bf-212">A unique ID associated with the most recent commit in this page</span></span>
<span data-ttu-id="106bf-213">commitTimeStamp</span><span class="sxs-lookup"><span data-stu-id="106bf-213">commitTimeStamp</span></span> | <span data-ttu-id="106bf-214">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-214">string</span></span>           | <span data-ttu-id="106bf-215">是</span><span class="sxs-lookup"><span data-stu-id="106bf-215">yes</span></span>      | <span data-ttu-id="106bf-216">在此页中的最新提交的时间戳</span><span class="sxs-lookup"><span data-stu-id="106bf-216">A timestamp of the most recent commit in this page</span></span>
<span data-ttu-id="106bf-217">count</span><span class="sxs-lookup"><span data-stu-id="106bf-217">count</span></span>           | <span data-ttu-id="106bf-218">整数</span><span class="sxs-lookup"><span data-stu-id="106bf-218">integer</span></span>          | <span data-ttu-id="106bf-219">是</span><span class="sxs-lookup"><span data-stu-id="106bf-219">yes</span></span>      | <span data-ttu-id="106bf-220">在页中的项的数目</span><span class="sxs-lookup"><span data-stu-id="106bf-220">The number of items in the page</span></span>
<span data-ttu-id="106bf-221">项</span><span class="sxs-lookup"><span data-stu-id="106bf-221">items</span></span>           | <span data-ttu-id="106bf-222">对象的数组</span><span class="sxs-lookup"><span data-stu-id="106bf-222">array of objects</span></span> | <span data-ttu-id="106bf-223">是</span><span class="sxs-lookup"><span data-stu-id="106bf-223">yes</span></span>      | <span data-ttu-id="106bf-224">此页中的目录项</span><span class="sxs-lookup"><span data-stu-id="106bf-224">The catalog items in this page</span></span>
<span data-ttu-id="106bf-225">父</span><span class="sxs-lookup"><span data-stu-id="106bf-225">parent</span></span>          | <span data-ttu-id="106bf-226">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-226">string</span></span>           | <span data-ttu-id="106bf-227">是</span><span class="sxs-lookup"><span data-stu-id="106bf-227">yes</span></span>      | <span data-ttu-id="106bf-228">指向目录索引的 URL</span><span class="sxs-lookup"><span data-stu-id="106bf-228">A URL to the catalog index</span></span>

<span data-ttu-id="106bf-229">在每个元素`items`数组是具有一些有关的目录项的最小的详细信息的对象。</span><span class="sxs-lookup"><span data-stu-id="106bf-229">Each element in the `items` array is an object with some minimal details about the catalog item.</span></span> <span data-ttu-id="106bf-230">这些项对象不包含的所有目录项的数据。</span><span class="sxs-lookup"><span data-stu-id="106bf-230">These item objects do not contain all of the catalog item's data.</span></span> <span data-ttu-id="106bf-231">在页中的项的顺序`items`未定义数组。</span><span class="sxs-lookup"><span data-stu-id="106bf-231">The order of the items in the page's `items` array is not defined.</span></span> <span data-ttu-id="106bf-232">项目可以使用的内存中的客户端经过排序其`commitTimeStamp`属性。</span><span class="sxs-lookup"><span data-stu-id="106bf-232">Items can be ordered by the client in memory using their `commitTimeStamp` property.</span></span>

<span data-ttu-id="106bf-233">在页中的目录项的数目由服务器实现定义。</span><span class="sxs-lookup"><span data-stu-id="106bf-233">The number of catalog items in a page is defined by server implementation.</span></span> <span data-ttu-id="106bf-234">对于 nuget.org，有最多 550 项在每个页中，尽管实际数的时间可能会更小，以某些页 dependong 上的点处的下一步提交批的大小。</span><span class="sxs-lookup"><span data-stu-id="106bf-234">For nuget.org, there are at most 550 items in each page, although the actual number may be smaller for some pages dependong on the size of the next commit batch at the point in time.</span></span>

<span data-ttu-id="106bf-235">引入新的项，`count`是递增和新的目录项对象会显示在`items`数组。</span><span class="sxs-lookup"><span data-stu-id="106bf-235">As new items are introduced, the `count` is incremented and new catalog item objects appear in the `items` array.</span></span>

<span data-ttu-id="106bf-236">将项目添加到页中，`commitId`更改和`commitTimeStamp`会增加。</span><span class="sxs-lookup"><span data-stu-id="106bf-236">As items are added to the page, the `commitId` changes and the `commitTimeStamp` increases.</span></span> <span data-ttu-id="106bf-237">这两个属性均通过所有实质上是摘要`commitId`和`commitTimeStamp`中值`items`数组。</span><span class="sxs-lookup"><span data-stu-id="106bf-237">These two properties are essentially a summary over all `commitId` and `commitTimeStamp` values in the `items` array.</span></span>

### <a name="catalog-item-object-in-a-page"></a><span data-ttu-id="106bf-238">目录在页中的项对象</span><span class="sxs-lookup"><span data-stu-id="106bf-238">Catalog item object in a page</span></span>

<span data-ttu-id="106bf-239">在目录页中找到的目录项对象`items`属性具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="106bf-239">The catalog item objects found in the catalog page's `items` property have the following properties:</span></span>

<span data-ttu-id="106bf-240">name</span><span class="sxs-lookup"><span data-stu-id="106bf-240">Name</span></span>            | <span data-ttu-id="106bf-241">类型</span><span class="sxs-lookup"><span data-stu-id="106bf-241">Type</span></span>    | <span data-ttu-id="106bf-242">必需</span><span class="sxs-lookup"><span data-stu-id="106bf-242">Required</span></span> | <span data-ttu-id="106bf-243">说明</span><span class="sxs-lookup"><span data-stu-id="106bf-243">Notes</span></span>
--------------- | ------- | -------- | -----
@id             | <span data-ttu-id="106bf-244">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-244">string</span></span>  | <span data-ttu-id="106bf-245">是</span><span class="sxs-lookup"><span data-stu-id="106bf-245">yes</span></span>      | <span data-ttu-id="106bf-246">要提取的目录项的 URL</span><span class="sxs-lookup"><span data-stu-id="106bf-246">The URL to fetch the catalog item</span></span>
@type           | <span data-ttu-id="106bf-247">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-247">string</span></span>  | <span data-ttu-id="106bf-248">是</span><span class="sxs-lookup"><span data-stu-id="106bf-248">yes</span></span>      | <span data-ttu-id="106bf-249">目录项的类型</span><span class="sxs-lookup"><span data-stu-id="106bf-249">The type of the catalog item</span></span>
<span data-ttu-id="106bf-250">commitId</span><span class="sxs-lookup"><span data-stu-id="106bf-250">commitId</span></span>        | <span data-ttu-id="106bf-251">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-251">string</span></span>  | <span data-ttu-id="106bf-252">是</span><span class="sxs-lookup"><span data-stu-id="106bf-252">yes</span></span>      | <span data-ttu-id="106bf-253">与此目录项关联的提交 ID</span><span class="sxs-lookup"><span data-stu-id="106bf-253">The commit ID associated with this catalog item</span></span>
<span data-ttu-id="106bf-254">commitTimeStamp</span><span class="sxs-lookup"><span data-stu-id="106bf-254">commitTimeStamp</span></span> | <span data-ttu-id="106bf-255">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-255">string</span></span>  | <span data-ttu-id="106bf-256">是</span><span class="sxs-lookup"><span data-stu-id="106bf-256">yes</span></span>      | <span data-ttu-id="106bf-257">此目录项的提交时间戳</span><span class="sxs-lookup"><span data-stu-id="106bf-257">The commit timestamp of this catalog item</span></span>
<span data-ttu-id="106bf-258">nuget:id</span><span class="sxs-lookup"><span data-stu-id="106bf-258">nuget:id</span></span>        | <span data-ttu-id="106bf-259">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-259">string</span></span>  | <span data-ttu-id="106bf-260">是</span><span class="sxs-lookup"><span data-stu-id="106bf-260">yes</span></span>      | <span data-ttu-id="106bf-261">与此叶包 ID</span><span class="sxs-lookup"><span data-stu-id="106bf-261">The package ID that this leaf is related to</span></span>
<span data-ttu-id="106bf-262">nuget:version</span><span class="sxs-lookup"><span data-stu-id="106bf-262">nuget:version</span></span>   | <span data-ttu-id="106bf-263">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-263">string</span></span>  | <span data-ttu-id="106bf-264">是</span><span class="sxs-lookup"><span data-stu-id="106bf-264">yes</span></span>      | <span data-ttu-id="106bf-265">与此叶包版本</span><span class="sxs-lookup"><span data-stu-id="106bf-265">The package version that this leaf is related to</span></span>

<span data-ttu-id="106bf-266">`@type`值将为以下两个值之一：</span><span class="sxs-lookup"><span data-stu-id="106bf-266">The `@type` value will be one of the following two values:</span></span>

1. <span data-ttu-id="106bf-267">`nuget:PackageDetails`： 这对应于`PackageDetails`目录叶文档中的类型。</span><span class="sxs-lookup"><span data-stu-id="106bf-267">`nuget:PackageDetails`: this corresponds to `PackageDetails` type in the catalog leaf document.</span></span>
1. <span data-ttu-id="106bf-268">`nuget:PackageDelete`： 这对应于`PackageDelete`目录叶文档中的类型。</span><span class="sxs-lookup"><span data-stu-id="106bf-268">`nuget:PackageDelete`: this corresponds to the `PackageDelete` type in the catalog leaf document.</span></span>

<span data-ttu-id="106bf-269">有关详细信息的链接，意味着每个类型，请参阅[对应项类型](#item-types)下面。</span><span class="sxs-lookup"><span data-stu-id="106bf-269">For more details about what each type means, see the [corresponding items type](#item-types) below.</span></span>

### <a name="sample-request"></a><span data-ttu-id="106bf-270">示例请求</span><span class="sxs-lookup"><span data-stu-id="106bf-270">Sample request</span></span>

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a><span data-ttu-id="106bf-271">示例响应</span><span class="sxs-lookup"><span data-stu-id="106bf-271">Sample response</span></span>

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a><span data-ttu-id="106bf-272">目录叶</span><span class="sxs-lookup"><span data-stu-id="106bf-272">Catalog leaf</span></span>

<span data-ttu-id="106bf-273">目录叶及时包含有关特定包 ID 和在某一时刻的版本的元数据。</span><span class="sxs-lookup"><span data-stu-id="106bf-273">The catalog leaf contains metadata about a specific package ID and version at some point in time.</span></span> <span data-ttu-id="106bf-274">这是提取使用的文档`@id`值在目录页中找到。</span><span class="sxs-lookup"><span data-stu-id="106bf-274">It is a document fetched using the `@id` value found in a catalog page.</span></span> <span data-ttu-id="106bf-275">目录叶的 URL 不应为 predictedable 和应使用仅目录页被发现。</span><span class="sxs-lookup"><span data-stu-id="106bf-275">The URL to a catalog leaf is not intended to be predictedable and should be discovered using only a catalog page.</span></span>

<span data-ttu-id="106bf-276">编录叶文档是具有以下属性的 JSON 对象：</span><span class="sxs-lookup"><span data-stu-id="106bf-276">The catalog leaf document is a JSON object with the following properties:</span></span>

<span data-ttu-id="106bf-277">name</span><span class="sxs-lookup"><span data-stu-id="106bf-277">Name</span></span>                    | <span data-ttu-id="106bf-278">类型</span><span class="sxs-lookup"><span data-stu-id="106bf-278">Type</span></span>                       | <span data-ttu-id="106bf-279">必需</span><span class="sxs-lookup"><span data-stu-id="106bf-279">Required</span></span> | <span data-ttu-id="106bf-280">说明</span><span class="sxs-lookup"><span data-stu-id="106bf-280">Notes</span></span>
----------------------- | -------------------------- | -------- | -----
@type                   | <span data-ttu-id="106bf-281">字符串或字符串数组</span><span class="sxs-lookup"><span data-stu-id="106bf-281">string or array of strings</span></span> | <span data-ttu-id="106bf-282">是</span><span class="sxs-lookup"><span data-stu-id="106bf-282">yes</span></span>      | <span data-ttu-id="106bf-283">目录项的类型</span><span class="sxs-lookup"><span data-stu-id="106bf-283">The type(s) of the catalog item</span></span>
<span data-ttu-id="106bf-284">目录： commitId</span><span class="sxs-lookup"><span data-stu-id="106bf-284">catalog:commitId</span></span>        | <span data-ttu-id="106bf-285">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-285">string</span></span>                     | <span data-ttu-id="106bf-286">是</span><span class="sxs-lookup"><span data-stu-id="106bf-286">yes</span></span>      | <span data-ttu-id="106bf-287">与此目录项关联的提交 ID</span><span class="sxs-lookup"><span data-stu-id="106bf-287">A commit ID associated with this catalog item</span></span>
<span data-ttu-id="106bf-288">目录： commitTimeStamp</span><span class="sxs-lookup"><span data-stu-id="106bf-288">catalog:commitTimeStamp</span></span> | <span data-ttu-id="106bf-289">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-289">string</span></span>                     | <span data-ttu-id="106bf-290">是</span><span class="sxs-lookup"><span data-stu-id="106bf-290">yes</span></span>      | <span data-ttu-id="106bf-291">此目录项的提交时间戳</span><span class="sxs-lookup"><span data-stu-id="106bf-291">The commit timestamp of this catalog item</span></span>
<span data-ttu-id="106bf-292">id</span><span class="sxs-lookup"><span data-stu-id="106bf-292">id</span></span>                      | <span data-ttu-id="106bf-293">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-293">string</span></span>                     | <span data-ttu-id="106bf-294">是</span><span class="sxs-lookup"><span data-stu-id="106bf-294">yes</span></span>      | <span data-ttu-id="106bf-295">目录项的包 ID</span><span class="sxs-lookup"><span data-stu-id="106bf-295">The package ID of the catalog item</span></span>
<span data-ttu-id="106bf-296">发布</span><span class="sxs-lookup"><span data-stu-id="106bf-296">published</span></span>               | <span data-ttu-id="106bf-297">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-297">string</span></span>                     | <span data-ttu-id="106bf-298">是</span><span class="sxs-lookup"><span data-stu-id="106bf-298">yes</span></span>      | <span data-ttu-id="106bf-299">包的目录项目发布的日期</span><span class="sxs-lookup"><span data-stu-id="106bf-299">The published date of the package catalog item</span></span>
<span data-ttu-id="106bf-300">version</span><span class="sxs-lookup"><span data-stu-id="106bf-300">version</span></span>                 | <span data-ttu-id="106bf-301">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-301">string</span></span>                     | <span data-ttu-id="106bf-302">是</span><span class="sxs-lookup"><span data-stu-id="106bf-302">yes</span></span>      | <span data-ttu-id="106bf-303">目录项的包版本</span><span class="sxs-lookup"><span data-stu-id="106bf-303">The package version of the catalog item</span></span>

### <a name="item-types"></a><span data-ttu-id="106bf-304">项类型</span><span class="sxs-lookup"><span data-stu-id="106bf-304">Item types</span></span>

<span data-ttu-id="106bf-305">`@type`属性是由字符串的数组。</span><span class="sxs-lookup"><span data-stu-id="106bf-305">The `@type` property is a string or array of strings.</span></span> <span data-ttu-id="106bf-306">为方便起见，如果`@type`值是一个字符串，它应视为一个大小的任何数组。</span><span class="sxs-lookup"><span data-stu-id="106bf-306">For convenience, if the `@type` value is a string, it should be treated as any array of size one.</span></span> <span data-ttu-id="106bf-307">并非所有可能值`@type`中进行了说明。</span><span class="sxs-lookup"><span data-stu-id="106bf-307">Not all possible values for `@type` are documented.</span></span> <span data-ttu-id="106bf-308">但是，每个目录项具有完全的两个以下的字符串类型值之一：</span><span class="sxs-lookup"><span data-stu-id="106bf-308">However, each catalog item has exactly one of the two following string type values:</span></span>

1. <span data-ttu-id="106bf-309">`PackageDetails`： 表示包元数据的快照</span><span class="sxs-lookup"><span data-stu-id="106bf-309">`PackageDetails`: represents a snapshot of package metadata</span></span>
1. <span data-ttu-id="106bf-310">`PackageDelete`： 表示已删除的包</span><span class="sxs-lookup"><span data-stu-id="106bf-310">`PackageDelete`: represents a package that was deleted</span></span>

### <a name="package-details-catalog-items"></a><span data-ttu-id="106bf-311">包的详细信息的目录项</span><span class="sxs-lookup"><span data-stu-id="106bf-311">Package details catalog items</span></span>

<span data-ttu-id="106bf-312">目录项类型的`PackageDetails`包含特定包 （ID 和版本组合） 的包元数据的快照。</span><span class="sxs-lookup"><span data-stu-id="106bf-312">Catalog items with the type `PackageDetails` contain a snapshot of package metadata for a specific package (ID and version combination).</span></span> <span data-ttu-id="106bf-313">如果包源遇到下列任一情况，则会生成对包的详细信息的目录项目：</span><span class="sxs-lookup"><span data-stu-id="106bf-313">A package details catalog item is produced when a package source encounters any of the following scenarios:</span></span>

1. <span data-ttu-id="106bf-314">包是**推送**。</span><span class="sxs-lookup"><span data-stu-id="106bf-314">A package is **pushed**.</span></span>
1. <span data-ttu-id="106bf-315">包是**列出**。</span><span class="sxs-lookup"><span data-stu-id="106bf-315">A package is **listed**.</span></span>
1. <span data-ttu-id="106bf-316">包是**未列出**。</span><span class="sxs-lookup"><span data-stu-id="106bf-316">A package is **unlisted**.</span></span>
1. <span data-ttu-id="106bf-317">包是**重排**。</span><span class="sxs-lookup"><span data-stu-id="106bf-317">A package is **reflowed**.</span></span>

<span data-ttu-id="106bf-318">包重排是实质上是生成到包本身不进行任何更改的现有包的假推送管理手势。</span><span class="sxs-lookup"><span data-stu-id="106bf-318">A package reflow is an administrative gesture that essentially generates a fake push of an existing package with no changes to the package itself.</span></span> <span data-ttu-id="106bf-319">在 nuget.org，重排 bug 修复使用该目录的后台作业之一后使用。</span><span class="sxs-lookup"><span data-stu-id="106bf-319">On nuget.org, a reflow is used after fixing a bug in one of the background jobs which consume the catalog.</span></span>

<span data-ttu-id="106bf-320">客户端使用的目录项不应尝试来确定哪种方案生成的目录项。</span><span class="sxs-lookup"><span data-stu-id="106bf-320">Clients consuming the catalog items should not attempt to determine which of these scenarios produced the catalog item.</span></span> <span data-ttu-id="106bf-321">相反，客户端应只需使用更新任何维护的视图或索引中的目录项，包含的元数据。</span><span class="sxs-lookup"><span data-stu-id="106bf-321">Instead, the client should simply update any maintained view or index with the metadata contained in the catalog item.</span></span> <span data-ttu-id="106bf-322">此外，应适当处理重复或冗余目录项 （幂等方式）。</span><span class="sxs-lookup"><span data-stu-id="106bf-322">Furthermore, duplicate or redundant catalog items should be handled gracefully (idempotently).</span></span>

<span data-ttu-id="106bf-323">包详细信息目录项具有以下属性除了[包含在所有目录叶](#catalog-leaf)。</span><span class="sxs-lookup"><span data-stu-id="106bf-323">Package details catalog items have the following properties in addition to those [included on all catalog leaves](#catalog-leaf).</span></span>

<span data-ttu-id="106bf-324">name</span><span class="sxs-lookup"><span data-stu-id="106bf-324">Name</span></span>                    | <span data-ttu-id="106bf-325">类型</span><span class="sxs-lookup"><span data-stu-id="106bf-325">Type</span></span>                       | <span data-ttu-id="106bf-326">必需</span><span class="sxs-lookup"><span data-stu-id="106bf-326">Required</span></span> | <span data-ttu-id="106bf-327">说明</span><span class="sxs-lookup"><span data-stu-id="106bf-327">Notes</span></span>
----------------------- | -------------------------- | -------- | -----
<span data-ttu-id="106bf-328">作者</span><span class="sxs-lookup"><span data-stu-id="106bf-328">authors</span></span>                 | <span data-ttu-id="106bf-329">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-329">string</span></span>                     | <span data-ttu-id="106bf-330">否</span><span class="sxs-lookup"><span data-stu-id="106bf-330">no</span></span>       |
<span data-ttu-id="106bf-331">created</span><span class="sxs-lookup"><span data-stu-id="106bf-331">created</span></span>                 | <span data-ttu-id="106bf-332">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-332">string</span></span>                     | <span data-ttu-id="106bf-333">是</span><span class="sxs-lookup"><span data-stu-id="106bf-333">yes</span></span>      | <span data-ttu-id="106bf-334">首次创建包的时间戳</span><span class="sxs-lookup"><span data-stu-id="106bf-334">A timestamp of when the package was first created</span></span>
<span data-ttu-id="106bf-335">dependencyGroups</span><span class="sxs-lookup"><span data-stu-id="106bf-335">dependencyGroups</span></span>        | <span data-ttu-id="106bf-336">对象的数组</span><span class="sxs-lookup"><span data-stu-id="106bf-336">array of objects</span></span>           | <span data-ttu-id="106bf-337">否</span><span class="sxs-lookup"><span data-stu-id="106bf-337">no</span></span>       | <span data-ttu-id="106bf-338">相同的格式设置为[package 元数据资源](registration-base-url-resource.md#package-dependency-group)</span><span class="sxs-lookup"><span data-stu-id="106bf-338">Same format as the [package metadata resource](registration-base-url-resource.md#package-dependency-group)</span></span>
<span data-ttu-id="106bf-339">说明</span><span class="sxs-lookup"><span data-stu-id="106bf-339">description</span></span>             | <span data-ttu-id="106bf-340">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-340">string</span></span>                     | <span data-ttu-id="106bf-341">否</span><span class="sxs-lookup"><span data-stu-id="106bf-341">no</span></span>       |
<span data-ttu-id="106bf-342">iconUrl</span><span class="sxs-lookup"><span data-stu-id="106bf-342">iconUrl</span></span>                 | <span data-ttu-id="106bf-343">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-343">string</span></span>                     | <span data-ttu-id="106bf-344">否</span><span class="sxs-lookup"><span data-stu-id="106bf-344">no</span></span>       |
<span data-ttu-id="106bf-345">isPrerelease</span><span class="sxs-lookup"><span data-stu-id="106bf-345">isPrerelease</span></span>            | <span data-ttu-id="106bf-346">boolean</span><span class="sxs-lookup"><span data-stu-id="106bf-346">boolean</span></span>                    | <span data-ttu-id="106bf-347">是</span><span class="sxs-lookup"><span data-stu-id="106bf-347">yes</span></span>      | <span data-ttu-id="106bf-348">是否预发布的包版本</span><span class="sxs-lookup"><span data-stu-id="106bf-348">Whether or not the package version is prerelease</span></span>
<span data-ttu-id="106bf-349">语言</span><span class="sxs-lookup"><span data-stu-id="106bf-349">language</span></span>                | <span data-ttu-id="106bf-350">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-350">string</span></span>                     | <span data-ttu-id="106bf-351">否</span><span class="sxs-lookup"><span data-stu-id="106bf-351">no</span></span>       |
<span data-ttu-id="106bf-352">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="106bf-352">licenseUrl</span></span>              | <span data-ttu-id="106bf-353">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-353">string</span></span>                     | <span data-ttu-id="106bf-354">否</span><span class="sxs-lookup"><span data-stu-id="106bf-354">no</span></span>       |
<span data-ttu-id="106bf-355">列出</span><span class="sxs-lookup"><span data-stu-id="106bf-355">listed</span></span>                  | <span data-ttu-id="106bf-356">boolean</span><span class="sxs-lookup"><span data-stu-id="106bf-356">boolean</span></span>                    | <span data-ttu-id="106bf-357">否</span><span class="sxs-lookup"><span data-stu-id="106bf-357">no</span></span>       | <span data-ttu-id="106bf-358">该程序包是否将列</span><span class="sxs-lookup"><span data-stu-id="106bf-358">Whether or not the package is listed</span></span>
<span data-ttu-id="106bf-359">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="106bf-359">minClientVersion</span></span>        | <span data-ttu-id="106bf-360">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-360">string</span></span>                     | <span data-ttu-id="106bf-361">否</span><span class="sxs-lookup"><span data-stu-id="106bf-361">no</span></span>       |
<span data-ttu-id="106bf-362">packageHash</span><span class="sxs-lookup"><span data-stu-id="106bf-362">packageHash</span></span>             | <span data-ttu-id="106bf-363">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-363">string</span></span>                     | <span data-ttu-id="106bf-364">是</span><span class="sxs-lookup"><span data-stu-id="106bf-364">yes</span></span>      | <span data-ttu-id="106bf-365">使用编码的包的哈希[标准 base 64](https://tools.ietf.org/html/rfc4648#section-4)</span><span class="sxs-lookup"><span data-stu-id="106bf-365">The hash of the package, encoding using [standard base 64](https://tools.ietf.org/html/rfc4648#section-4)</span></span>
<span data-ttu-id="106bf-366">packageHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="106bf-366">packageHashAlgorithm</span></span>    | <span data-ttu-id="106bf-367">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-367">string</span></span>                     | <span data-ttu-id="106bf-368">是</span><span class="sxs-lookup"><span data-stu-id="106bf-368">yes</span></span>      |
<span data-ttu-id="106bf-369">packageSize</span><span class="sxs-lookup"><span data-stu-id="106bf-369">packageSize</span></span>             | <span data-ttu-id="106bf-370">整数</span><span class="sxs-lookup"><span data-stu-id="106bf-370">integer</span></span>                    | <span data-ttu-id="106bf-371">是</span><span class="sxs-lookup"><span data-stu-id="106bf-371">yes</span></span>      | <span data-ttu-id="106bf-372">包.nupkg 以字节为单位的大小</span><span class="sxs-lookup"><span data-stu-id="106bf-372">The size of the package .nupkg in bytes</span></span>
<span data-ttu-id="106bf-373">projectUrl</span><span class="sxs-lookup"><span data-stu-id="106bf-373">projectUrl</span></span>              | <span data-ttu-id="106bf-374">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-374">string</span></span>                     | <span data-ttu-id="106bf-375">否</span><span class="sxs-lookup"><span data-stu-id="106bf-375">no</span></span>       |
<span data-ttu-id="106bf-376">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="106bf-376">releaseNotes</span></span>            | <span data-ttu-id="106bf-377">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-377">string</span></span>                     | <span data-ttu-id="106bf-378">否</span><span class="sxs-lookup"><span data-stu-id="106bf-378">no</span></span>       |
<span data-ttu-id="106bf-379">requireLicenseAgreement</span><span class="sxs-lookup"><span data-stu-id="106bf-379">requireLicenseAgreement</span></span> | <span data-ttu-id="106bf-380">boolean</span><span class="sxs-lookup"><span data-stu-id="106bf-380">boolean</span></span>                    | <span data-ttu-id="106bf-381">否</span><span class="sxs-lookup"><span data-stu-id="106bf-381">no</span></span>       | <span data-ttu-id="106bf-382">假定`false`如果排除</span><span class="sxs-lookup"><span data-stu-id="106bf-382">Assume `false` if excluded</span></span>
<span data-ttu-id="106bf-383">摘要</span><span class="sxs-lookup"><span data-stu-id="106bf-383">summary</span></span>                 | <span data-ttu-id="106bf-384">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-384">string</span></span>                     | <span data-ttu-id="106bf-385">否</span><span class="sxs-lookup"><span data-stu-id="106bf-385">no</span></span>       |
<span data-ttu-id="106bf-386">标记</span><span class="sxs-lookup"><span data-stu-id="106bf-386">tags</span></span>                    | <span data-ttu-id="106bf-387">字符串数组</span><span class="sxs-lookup"><span data-stu-id="106bf-387">array of strings</span></span>           | <span data-ttu-id="106bf-388">否</span><span class="sxs-lookup"><span data-stu-id="106bf-388">no</span></span>       |
<span data-ttu-id="106bf-389">标题</span><span class="sxs-lookup"><span data-stu-id="106bf-389">title</span></span>                   | <span data-ttu-id="106bf-390">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-390">string</span></span>                     | <span data-ttu-id="106bf-391">否</span><span class="sxs-lookup"><span data-stu-id="106bf-391">no</span></span>       |
<span data-ttu-id="106bf-392">verbatimVersion</span><span class="sxs-lookup"><span data-stu-id="106bf-392">verbatimVersion</span></span>         | <span data-ttu-id="106bf-393">字符串</span><span class="sxs-lookup"><span data-stu-id="106bf-393">string</span></span>                     | <span data-ttu-id="106bf-394">否</span><span class="sxs-lookup"><span data-stu-id="106bf-394">no</span></span>       | <span data-ttu-id="106bf-395">因为它的版本字符串最初位于.nuspec</span><span class="sxs-lookup"><span data-stu-id="106bf-395">The version string as it's originally found in the .nuspec</span></span>

<span data-ttu-id="106bf-396">包`version`属性是完整的规范化的版本字符串。</span><span class="sxs-lookup"><span data-stu-id="106bf-396">The package `version` property is the full, normalized version string.</span></span> <span data-ttu-id="106bf-397">这意味着，SemVer 2.0.0 生成数据可以是包含此处。</span><span class="sxs-lookup"><span data-stu-id="106bf-397">This means that SemVer 2.0.0 build data can be included here.</span></span>

<span data-ttu-id="106bf-398">`created`时间戳是包源，这通常是目录项的提交时间戳之前短暂地先接收包的时间。</span><span class="sxs-lookup"><span data-stu-id="106bf-398">The `created` timestamp is when the package was first received by the package source, which is typically a short time before the catalog item's commit timestamp.</span></span>

<span data-ttu-id="106bf-399">`packageHashAlgorithm`是一个字符串由服务器实现 represeting 用于生成的哈希算法定义`packageHash`。</span><span class="sxs-lookup"><span data-stu-id="106bf-399">The `packageHashAlgorithm` is a string defined by the server implementation represeting the hashing algorithm used to produce the `packageHash`.</span></span> <span data-ttu-id="106bf-400">始终使用 nuget.org`packageHashAlgorithm`值`SHA512`。</span><span class="sxs-lookup"><span data-stu-id="106bf-400">nuget.org always used the `packageHashAlgorithm` value of `SHA512`.</span></span>

<span data-ttu-id="106bf-401">`published`时间戳是上次列出包的时间。</span><span class="sxs-lookup"><span data-stu-id="106bf-401">The `published` timestamp is the time when the package was last listed.</span></span>

> [!Note]
> <span data-ttu-id="106bf-402">在 nuget.org，`published`值设置为包时未列出的 1900 年。</span><span class="sxs-lookup"><span data-stu-id="106bf-402">On nuget.org, the `published` value is set to year 1900 when the package is unlisted.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="106bf-403">示例请求</span><span class="sxs-lookup"><span data-stu-id="106bf-403">Sample request</span></span>

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a><span data-ttu-id="106bf-404">示例响应</span><span class="sxs-lookup"><span data-stu-id="106bf-404">Sample response</span></span>

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a><span data-ttu-id="106bf-405">包删除目录项</span><span class="sxs-lookup"><span data-stu-id="106bf-405">Package delete catalog items</span></span>

<span data-ttu-id="106bf-406">目录项类型的`PackageDelete`包含指明向目录客户端包从包源已被删除并且不再可用于任何包的操作 （如还原） 的信息的最小集。</span><span class="sxs-lookup"><span data-stu-id="106bf-406">Catalog items with the type `PackageDelete` contain a minimal set of information indicating to catalog clients that a package has been deleted from the package source and is no longer available for any package operation (such as restore).</span></span>

> [!Note]
> <span data-ttu-id="106bf-407">它是要删除的包和更高版本重新发布使用的相同包 ID 和版本的可能。</span><span class="sxs-lookup"><span data-stu-id="106bf-407">It is possible for a package to be deleted and later republished using the same package ID and version.</span></span> <span data-ttu-id="106bf-408">在 nuget.org，这是极少数情况下，因为这将打断包 ID 和版本表示特定包内容的正式客户端的假设。</span><span class="sxs-lookup"><span data-stu-id="106bf-408">On nuget.org, this is a very rare case as it breaks the official client's assumption that a package ID and version imply a specific package content.</span></span> <span data-ttu-id="106bf-409">有关删除该包在 nuget.org 上的详细信息，请参阅[我们策略](../policies/deleting-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="106bf-409">For more information about package deletion on nuget.org, see [our policy](../policies/deleting-packages.md).</span></span>

<span data-ttu-id="106bf-410">包删除目录项不包含其他属性除了[包含在所有目录叶](#catalog-leaf)。</span><span class="sxs-lookup"><span data-stu-id="106bf-410">Package delete catalog items have no additional properties in addition to those [included on all catalog leaves](#catalog-leaf).</span></span>

<span data-ttu-id="106bf-411">`version`属性是在包.nuspec 中找到的原始版本字符串。</span><span class="sxs-lookup"><span data-stu-id="106bf-411">The `version` property is the original version string found in the package .nuspec.</span></span>

<span data-ttu-id="106bf-412">`published`属性是当删除包，这通常是为目录项的提交时间戳之前的短时间的时间。</span><span class="sxs-lookup"><span data-stu-id="106bf-412">The `published` property is the time when package was deleted, which is typically as short time before the catalog item's commit timestamp.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="106bf-413">示例请求</span><span class="sxs-lookup"><span data-stu-id="106bf-413">Sample request</span></span>

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a><span data-ttu-id="106bf-414">示例响应</span><span class="sxs-lookup"><span data-stu-id="106bf-414">Sample response</span></span>

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a><span data-ttu-id="106bf-415">Cursor</span><span class="sxs-lookup"><span data-stu-id="106bf-415">Cursor</span></span>

### <a name="overview"></a><span data-ttu-id="106bf-416">概述</span><span class="sxs-lookup"><span data-stu-id="106bf-416">Overview</span></span>

<span data-ttu-id="106bf-417">本部分介绍了一个客户端的概念，尽管不一定由该协议，规定应该是任何实际目录客户端实现的一部分。</span><span class="sxs-lookup"><span data-stu-id="106bf-417">This section describes a client concept that, although is not necessarily mandated by the protocol, should be part of any practical catalog client implementation.</span></span>

<span data-ttu-id="106bf-418">由于该目录是按时间编制索引的仅限附加的数据结构，应将存储客户端**光标**本地，最多的时间点客户端表示已处理的目录项。</span><span class="sxs-lookup"><span data-stu-id="106bf-418">Because the catalog is an append-only data structure indexed by time, the client should store a **cursor** locally, representing up to what point in time the client has processed catalog items.</span></span> <span data-ttu-id="106bf-419">请注意，应永远不会使用客户端的计算机时钟生成此光标值。</span><span class="sxs-lookup"><span data-stu-id="106bf-419">Note that this cursor value should never be generated using the client's machine clock.</span></span> <span data-ttu-id="106bf-420">相反，值应来自目录对象的`commitTimestamp`值。</span><span class="sxs-lookup"><span data-stu-id="106bf-420">Instead, the value should come from a catalog object's `commitTimestamp` value.</span></span>

<span data-ttu-id="106bf-421">每次客户端想要处理的包源上的新事件，它需要仅查询目录的所有目录项，提交时间戳大于其存储的光标。</span><span class="sxs-lookup"><span data-stu-id="106bf-421">Every time the client wants to process new events on the package source, it need only query the catalog for all catalog items with a commit timestamp greater than its stored cursor.</span></span> <span data-ttu-id="106bf-422">客户端已成功处理所有新的目录项后，它记录只作为其新光标值处理的目录项的最新的提交时间戳。</span><span class="sxs-lookup"><span data-stu-id="106bf-422">After the client successfully processes all new catalog items, it records the latest commit timestamp of catalog items just processed as its new cursor value.</span></span>

<span data-ttu-id="106bf-423">使用此方法，而客户端可以确保永远不会丢失在包源发生的任何包事件。</span><span class="sxs-lookup"><span data-stu-id="106bf-423">Using this approach, the client can be sure to never miss any package events that occurred on the package source.</span></span>
<span data-ttu-id="106bf-424">此外，客户端从来不必重新处理旧事件之前光标的记录的提交时间戳。</span><span class="sxs-lookup"><span data-stu-id="106bf-424">Additionally, the client never has to reprocess old events prior to the cursor's recorded commit timestamp.</span></span>

<span data-ttu-id="106bf-425">此游标的非常强大的概念适用于许多 nuget.org 后台作业，用于使 V3 用 API 自身保持最新。</span><span class="sxs-lookup"><span data-stu-id="106bf-425">This powerful concept of cursors is used for many of nuget.org background jobs and is used to keep the V3 API itself up-to-date.</span></span> 

### <a name="initial-value"></a><span data-ttu-id="106bf-426">初始值</span><span class="sxs-lookup"><span data-stu-id="106bf-426">Initial value</span></span>

<span data-ttu-id="106bf-427">当目录客户端第一次启动 （并因此不具有任何游标值） 时，它应使用默认光标的值。NET 的`System.DateTimeOffset.MinValue`或某些最小可表示的时间戳的类似此类的概念。</span><span class="sxs-lookup"><span data-stu-id="106bf-427">When the catalog client is starting for the very first time (and therefore has no cursor value), it should use a default cursor value of .NET's `System.DateTimeOffset.MinValue` or some such analogous notion of minimum representable timestamp.</span></span>

### <a name="iterating-over-catalog-items"></a><span data-ttu-id="106bf-428">循环访问目录项</span><span class="sxs-lookup"><span data-stu-id="106bf-428">Iterating over catalog items</span></span>

<span data-ttu-id="106bf-429">若要查询的下一步的一套要处理的目录项，客户端应：</span><span class="sxs-lookup"><span data-stu-id="106bf-429">To query for the next set of catalog items to process, the client should:</span></span>

1. <span data-ttu-id="106bf-430">从本地存储区中提取的记录的光标值。</span><span class="sxs-lookup"><span data-stu-id="106bf-430">Fetch the recorded cursor value from a local store.</span></span>
1. <span data-ttu-id="106bf-431">下载和反序列化的目录索引。</span><span class="sxs-lookup"><span data-stu-id="106bf-431">Download and deserialize the catalog index.</span></span>
1. <span data-ttu-id="106bf-432">查找所有目录提交时间戳的页*大于*光标。</span><span class="sxs-lookup"><span data-stu-id="106bf-432">Find all catalog pages with a commit timestamp *greater than* the cursor.</span></span>
1. <span data-ttu-id="106bf-433">声明要处理的目录项的空列表。</span><span class="sxs-lookup"><span data-stu-id="106bf-433">Declare an empty list of catalog items to process.</span></span>
1. <span data-ttu-id="106bf-434">为在步骤 3 中匹配每个目录页：</span><span class="sxs-lookup"><span data-stu-id="106bf-434">For each catalog page matched in step 3:</span></span>
   1. <span data-ttu-id="106bf-435">下载和反序列化目录页。</span><span class="sxs-lookup"><span data-stu-id="106bf-435">Download and deserialized the catalog page.</span></span>
   1. <span data-ttu-id="106bf-436">查找所有目录项提交时间戳*大于*光标。</span><span class="sxs-lookup"><span data-stu-id="106bf-436">Find all catalog items with a commit timestamp *greater than* the cursor.</span></span>
   1. <span data-ttu-id="106bf-437">将所有匹配的目录项添加到在步骤 4 中声明的列表。</span><span class="sxs-lookup"><span data-stu-id="106bf-437">Add all matching catalog items to the list declared in step 4.</span></span>
1. <span data-ttu-id="106bf-438">目录项列表进行排序的提交时间戳。</span><span class="sxs-lookup"><span data-stu-id="106bf-438">Sort the catalog item list by commit timestamp.</span></span>
1. <span data-ttu-id="106bf-439">处理序列中的每个目录项：</span><span class="sxs-lookup"><span data-stu-id="106bf-439">Process each catalog item in sequence:</span></span>
   1. <span data-ttu-id="106bf-440">下载和反序列化的目录项。</span><span class="sxs-lookup"><span data-stu-id="106bf-440">Download and deserialize the catalog item.</span></span>
   1. <span data-ttu-id="106bf-441">相应地作出反应到目录项的类型。</span><span class="sxs-lookup"><span data-stu-id="106bf-441">React appropriately to the catalog item's type.</span></span>
   1. <span data-ttu-id="106bf-442">处理客户端特定方式中的目录项文档。</span><span class="sxs-lookup"><span data-stu-id="106bf-442">Process the catalog item document in a client-specific fashion.</span></span>
1. <span data-ttu-id="106bf-443">记录作为新光标值的最后一个目录项的提交时间戳。</span><span class="sxs-lookup"><span data-stu-id="106bf-443">Record the last catalog item's commit timestamp as the new cursor value.</span></span>

<span data-ttu-id="106bf-444">使用此基本算法，客户端实现可以生成的所有包可用包源上的完整视图。</span><span class="sxs-lookup"><span data-stu-id="106bf-444">With this basic algorithm, the client implementation can build up a complete view of all packages available on the package source.</span></span> <span data-ttu-id="106bf-445">客户端只需执行此算法定期需要始终注意的包源的最新更改。</span><span class="sxs-lookup"><span data-stu-id="106bf-445">The client need only execute this algorithm periodically to always be aware of the latest changes to the package source.</span></span>

> [!Note]
> <span data-ttu-id="106bf-446">这是算法，该 nuget.org 用来保持[包元数据](registration-base-url-resource.md)，[包内容](package-base-address-resource.md)，[搜索](search-query-service-resource.md)和[记忆式键入功能](search-autocomplete-service-resource.md)最新的资源。</span><span class="sxs-lookup"><span data-stu-id="106bf-446">This is the algorithm that nuget.org uses to keep the [Package Metadata](registration-base-url-resource.md), [Package Content](package-base-address-resource.md), [Search](search-query-service-resource.md) and [Autocomplete](search-autocomplete-service-resource.md) resources up to date.</span></span>

### <a name="dependent-cursors"></a><span data-ttu-id="106bf-447">依赖的游标</span><span class="sxs-lookup"><span data-stu-id="106bf-447">Dependent cursors</span></span>

<span data-ttu-id="106bf-448">假设有两个目录客户端具有 inherant 依赖项，其中一个客户端的输出取决于另一个客户端的输出。</span><span class="sxs-lookup"><span data-stu-id="106bf-448">Suppose there are two catalog clients that have an inherant dependency where one client's output depends on another client's output.</span></span> 

#### <a name="example"></a><span data-ttu-id="106bf-449">示例</span><span class="sxs-lookup"><span data-stu-id="106bf-449">Example</span></span>

<span data-ttu-id="106bf-450">例如，在 nuget.org 上的新发布的包不应出现在搜索资源之前它将显示在包的元数据资源。</span><span class="sxs-lookup"><span data-stu-id="106bf-450">For example, on nuget.org a newly published package should not appear in the search resource before it appears in the package metadata resource.</span></span> <span data-ttu-id="106bf-451">这是因为执行官方 NuGet 客户端的"还原"操作使用包元数据资源。</span><span class="sxs-lookup"><span data-stu-id="106bf-451">This is because the "restore" operation performed by the official NuGet client uses the package metadata resource.</span></span> <span data-ttu-id="106bf-452">如果客户发现使用搜索服务包，它们应能够成功还原该包使用包元数据资源。</span><span class="sxs-lookup"><span data-stu-id="106bf-452">If a customer discovers a package using the search service, they should be able to successfully restore that package using the package metadata resource.</span></span> <span data-ttu-id="106bf-453">换而言之，搜索资源依赖于包元数据资源。</span><span class="sxs-lookup"><span data-stu-id="106bf-453">In other words, the search resource depends on the package metadata resource.</span></span> <span data-ttu-id="106bf-454">每个资源都有一个更新该资源的目录客户端后台作业。</span><span class="sxs-lookup"><span data-stu-id="106bf-454">Each resource has a catalog client background job updating that resource.</span></span> <span data-ttu-id="106bf-455">每个客户端具有其自己的光标。</span><span class="sxs-lookup"><span data-stu-id="106bf-455">Each client has its own cursor.</span></span>

<span data-ttu-id="106bf-456">由于这两个资源生成从目录中，更新搜索资源的目录客户端游标中移出*必须不超过*包元数据目录客户端的光标。</span><span class="sxs-lookup"><span data-stu-id="106bf-456">Since both resources are built off of the catalog, the cursor of the catalog client that updates the search resource *must not go beyond* the cursor of the package metadata catalog client.</span></span>

#### <a name="algorithm"></a><span data-ttu-id="106bf-457">算法</span><span class="sxs-lookup"><span data-stu-id="106bf-457">Algorithm</span></span>

<span data-ttu-id="106bf-458">若要实现此限制，简单，请修改上述要算法：</span><span class="sxs-lookup"><span data-stu-id="106bf-458">To implement this restriction, simple modify the algorithm above to be:</span></span>

1. <span data-ttu-id="106bf-459">从本地存储区中提取的记录的光标值。</span><span class="sxs-lookup"><span data-stu-id="106bf-459">Fetch the recorded cursor value from a local store.</span></span>
1. <span data-ttu-id="106bf-460">下载和反序列化的目录索引。</span><span class="sxs-lookup"><span data-stu-id="106bf-460">Download and deserialize the catalog index.</span></span>
1. <span data-ttu-id="106bf-461">查找所有目录提交时间戳的页*大于*光标**小于或等于的依赖关系的光标。**</span><span class="sxs-lookup"><span data-stu-id="106bf-461">Find all catalog pages with a commit timestamp *greater than* the cursor **less than or equal to the dependency's cursor.**</span></span>
1. <span data-ttu-id="106bf-462">声明要处理的目录项的空列表。</span><span class="sxs-lookup"><span data-stu-id="106bf-462">Declare an empty list of catalog items to process.</span></span>
1. <span data-ttu-id="106bf-463">为在步骤 3 中匹配每个目录页：</span><span class="sxs-lookup"><span data-stu-id="106bf-463">For each catalog page matched in step 3:</span></span>
   1. <span data-ttu-id="106bf-464">下载和反序列化目录页。</span><span class="sxs-lookup"><span data-stu-id="106bf-464">Download and deserialized the catalog page.</span></span>
   1. <span data-ttu-id="106bf-465">查找所有目录项提交时间戳*大于*光标**小于或等于的依赖关系的光标。**</span><span class="sxs-lookup"><span data-stu-id="106bf-465">Find all catalog items with a commit timestamp *greater than* the cursor **less than or equal to the dependency's cursor.**</span></span>
   1. <span data-ttu-id="106bf-466">将所有匹配的目录项添加到在步骤 4 中声明的列表。</span><span class="sxs-lookup"><span data-stu-id="106bf-466">Add all matching catalog items to the list declared in step 4.</span></span>
1. <span data-ttu-id="106bf-467">目录项列表进行排序的提交时间戳。</span><span class="sxs-lookup"><span data-stu-id="106bf-467">Sort the catalog item list by commit timestamp.</span></span>
1. <span data-ttu-id="106bf-468">处理序列中的每个目录项：</span><span class="sxs-lookup"><span data-stu-id="106bf-468">Process each catalog item in sequence:</span></span>
   1. <span data-ttu-id="106bf-469">下载和反序列化的目录项。</span><span class="sxs-lookup"><span data-stu-id="106bf-469">Download and deserialize the catalog item.</span></span>
   1. <span data-ttu-id="106bf-470">相应地作出反应到目录项的类型。</span><span class="sxs-lookup"><span data-stu-id="106bf-470">React appropriately to the catalog item's type.</span></span>
   1. <span data-ttu-id="106bf-471">处理客户端特定方式中的目录项文档。</span><span class="sxs-lookup"><span data-stu-id="106bf-471">Process the catalog item document in a client-specific fashion.</span></span>
1. <span data-ttu-id="106bf-472">记录作为新光标值的最后一个目录项的提交时间戳。</span><span class="sxs-lookup"><span data-stu-id="106bf-472">Record the last catalog item's commit timestamp as the new cursor value.</span></span>

<span data-ttu-id="106bf-473">使用此修改的算法，你可以构建系统依赖目录客户端的所有生成其自己的特定索引、 项目等。</span><span class="sxs-lookup"><span data-stu-id="106bf-473">Using this modified algorithm, you can build a system of dependent catalog clients all producing their own specific indexes, artifacts, etc.</span></span>
