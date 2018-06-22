---
title: 查询所有发布到 nuget.org 的包
description: 使用 NuGet API 可以查询所有发布到 nuget.org 的包并随着时间推移保持最新状态。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 4190cfb500127f117ea1067f0679e5c248bffb3d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821364"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="0dee4-103">查询所有发布到 nuget.org 的包</span><span class="sxs-lookup"><span data-stu-id="0dee4-103">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="0dee4-104">旧版 OData V2 API 上一个常见查询模式为枚举所有发布到 nuget.org 的包，按照包发布的时间排序。</span><span class="sxs-lookup"><span data-stu-id="0dee4-104">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="0dee4-105">需要这类针对 nuget.org 的查询的情况多种多样：</span><span class="sxs-lookup"><span data-stu-id="0dee4-105">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="0dee4-106">完全复制 nuget.org</span><span class="sxs-lookup"><span data-stu-id="0dee4-106">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="0dee4-107">检测包发布新版本的时间</span><span class="sxs-lookup"><span data-stu-id="0dee4-107">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="0dee4-108">查找依赖包的包</span><span class="sxs-lookup"><span data-stu-id="0dee4-108">Finding packages that depend on your package</span></span>

<span data-ttu-id="0dee4-109">执行此操作的老式方法通常依靠按照时间戳对 OData 包实体进行排序并且用 `skip` 和 `top`（页大小）参数跨大型结果集进行分页。</span><span class="sxs-lookup"><span data-stu-id="0dee4-109">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="0dee4-110">遗憾的是，这种方法有一些缺点：</span><span class="sxs-lookup"><span data-stu-id="0dee4-110">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="0dee4-111">可能会丢失包，因为查询的对象为常常更改顺序的数据</span><span class="sxs-lookup"><span data-stu-id="0dee4-111">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="0dee4-112">查询响应时间长，因为查询未优化（最优化的查询支持官方 NuGet 客户端的主流场景）</span><span class="sxs-lookup"><span data-stu-id="0dee4-112">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="0dee4-113">使用弃用和未记录的 API，意味着将来不保证支持此类查询</span><span class="sxs-lookup"><span data-stu-id="0dee4-113">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="0dee4-114">不能按照发生的确切顺序重播历史记录</span><span class="sxs-lookup"><span data-stu-id="0dee4-114">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="0dee4-115">因此，可以遵循以下指南以更加可靠新颖的方法解决上述情况。</span><span class="sxs-lookup"><span data-stu-id="0dee4-115">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="0dee4-116">概述</span><span class="sxs-lookup"><span data-stu-id="0dee4-116">Overview</span></span>

<span data-ttu-id="0dee4-117">本指南的中心是 [NuGet API](../../api/overview.md) 中称为“目录”的资源。</span><span class="sxs-lookup"><span data-stu-id="0dee4-117">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="0dee4-118">目录是仅限追加的 API，它允许调用方查看在 nuget.org 中添加、修改和删除的包的完整历史记录。如果对发布到 nuget.org 的所有包甚至是包的子集感兴趣，则最好用目录来跟进了解当前可用的包集。</span><span class="sxs-lookup"><span data-stu-id="0dee4-118">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="0dee4-119">本指南旨在提供高级演练，如果你对目录的详情细节感兴趣，请参阅它的 [API 引用文档](../../api/catalog-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="0dee4-119">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="0dee4-120">以下步骤可以选择任意的编程语言来执行。</span><span class="sxs-lookup"><span data-stu-id="0dee4-120">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="0dee4-121">如果需要完整的运行示例，请查看下面提及的 [C# 示例](#c-sample-code)。</span><span class="sxs-lookup"><span data-stu-id="0dee4-121">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="0dee4-122">反之，按照以下指南生成可靠的目录阅读器。</span><span class="sxs-lookup"><span data-stu-id="0dee4-122">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="0dee4-123">初始化游标</span><span class="sxs-lookup"><span data-stu-id="0dee4-123">Initialize a cursor</span></span>

<span data-ttu-id="0dee4-124">生成可靠目录阅读器的第一步是实现游标。</span><span class="sxs-lookup"><span data-stu-id="0dee4-124">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="0dee4-125">有关目录游标设计的完整详细信息，请参阅[目录引用文档](../../api/catalog-resource.md#cursor)。</span><span class="sxs-lookup"><span data-stu-id="0dee4-125">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="0dee4-126">简而言之，游标是时间中的某一点，你在目录中处理事件直到该点。</span><span class="sxs-lookup"><span data-stu-id="0dee4-126">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="0dee4-127">目录中的事件表示包发布和其他包更改。</span><span class="sxs-lookup"><span data-stu-id="0dee4-127">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="0dee4-128">如果你关注（从一开始）发布到 NuGet 的所有包，那么将游标初始化为“最小值”时间戳（例如 .NET 中的 `DateTime.MinValue`）。</span><span class="sxs-lookup"><span data-stu-id="0dee4-128">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="0dee4-129">如果仅关注现在开始发布的包，则使用当前时间戳作为初始游标值。</span><span class="sxs-lookup"><span data-stu-id="0dee4-129">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="0dee4-130">对于本指南，我们要将游标初始化为一小时前的时间戳。</span><span class="sxs-lookup"><span data-stu-id="0dee4-130">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="0dee4-131">现在，只需在内存中保存时间戳。</span><span class="sxs-lookup"><span data-stu-id="0dee4-131">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="0dee4-132">确定目录索引 URL</span><span class="sxs-lookup"><span data-stu-id="0dee4-132">Determine catalog index URL</span></span>

<span data-ttu-id="0dee4-133">NuGet API 中每个资源（终结点）的位置应使用[服务索引](../../api/service-index.md)发现。</span><span class="sxs-lookup"><span data-stu-id="0dee4-133">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="0dee4-134">因为本指南重点介绍 nuget.org，所以我们使用 nuget.org 的服务索引。</span><span class="sxs-lookup"><span data-stu-id="0dee4-134">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="0dee4-135">服务文档是包含 nuget.org 上所有资源的 JSON 文档。查找具有 `Catalog/3.0.0` 的 `@type` 属性值的资源。</span><span class="sxs-lookup"><span data-stu-id="0dee4-135">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="0dee4-136">相关联的 `@id` 属性值是到目录索引本身的 URL。</span><span class="sxs-lookup"><span data-stu-id="0dee4-136">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="0dee4-137">查找新的目录叶</span><span class="sxs-lookup"><span data-stu-id="0dee4-137">Find new catalog leaves</span></span>

<span data-ttu-id="0dee4-138">使用前面步骤中找到的 `@id` 属性值下载目录索引：</span><span class="sxs-lookup"><span data-stu-id="0dee4-138">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="0dee4-139">反序列化[目录索引](../../api/catalog-resource.md#catalog-index)。</span><span class="sxs-lookup"><span data-stu-id="0dee4-139">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="0dee4-140">筛选出 `commitTimeStamp` 小于或等于当前游标值的所有[目录页对象](../../api/catalog-resource.md#catalog-page-object-in-the-index)。</span><span class="sxs-lookup"><span data-stu-id="0dee4-140">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="0dee4-141">对于每个剩余的目录页，使用 `@id` 属性下载完整文档。</span><span class="sxs-lookup"><span data-stu-id="0dee4-141">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="0dee4-142">反序列化[目录页](../../api/catalog-resource.md#catalog-page)。</span><span class="sxs-lookup"><span data-stu-id="0dee4-142">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="0dee4-143">筛选出 `commitTimeStamp` 小于或等于当前游标值的所有[目录叶对象](../../api/catalog-resource.md#catalog-item-object-in-a-page)。</span><span class="sxs-lookup"><span data-stu-id="0dee4-143">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="0dee4-144">在下载没有筛选出的所有目录页之后，你会具有目录叶对象集，用于表示在游标时间戳和现在时间之间已发布的、未列出、已列出或删除的包。</span><span class="sxs-lookup"><span data-stu-id="0dee4-144">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="0dee4-145">处理目录叶</span><span class="sxs-lookup"><span data-stu-id="0dee4-145">Process catalog leaves</span></span>

<span data-ttu-id="0dee4-146">此时，可以对目录项执行任何自定义处理。</span><span class="sxs-lookup"><span data-stu-id="0dee4-146">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="0dee4-147">如果只需要包的 ID 和版本，则可以在页中找到的目录项对象上检查 `nuget:id` 和 `nuget:version` 属性。</span><span class="sxs-lookup"><span data-stu-id="0dee4-147">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="0dee4-148">请务必查看 `@type` 属性，了解目录项是否涉及现有包或者删除包。</span><span class="sxs-lookup"><span data-stu-id="0dee4-148">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="0dee4-149">如果对有关包的元数据感兴趣（例如描述、依赖项、.nupkg 大小等），则可以使用 `@id` 属性提取[目录叶文档](../../api/catalog-resource.md#catalog-leaf)。</span><span class="sxs-lookup"><span data-stu-id="0dee4-149">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="0dee4-150">本文档不仅有[包元数据资源](../../api/registration-base-url-resource.md)中包含的所有元数据，而且还有更多内容！</span><span class="sxs-lookup"><span data-stu-id="0dee4-150">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="0dee4-151">通过该步骤可以实现自定义逻辑。</span><span class="sxs-lookup"><span data-stu-id="0dee4-151">This step is where you implement your custom logic.</span></span> <span data-ttu-id="0dee4-152">无论要使用目录叶来做什么，本指南中的其他步骤也以大致相同的方法实现。</span><span class="sxs-lookup"><span data-stu-id="0dee4-152">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="0dee4-153">下载 .nupkg</span><span class="sxs-lookup"><span data-stu-id="0dee4-153">Downloading the .nupkg</span></span>

<span data-ttu-id="0dee4-154">如果对下载目录中找到的包的 .nupkg 感兴趣，那么可以使用[包内容资源](../../api/package-base-address-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="0dee4-154">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="0dee4-155">但请注意，在目录中找到包和包在包内容资源中可用之间有短暂的延迟。</span><span class="sxs-lookup"><span data-stu-id="0dee4-155">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="0dee4-156">所以，如果在尝试下载目录中找到的包的 .nupkg 时遇到 `404 Not Found`，只需稍后进行重试。</span><span class="sxs-lookup"><span data-stu-id="0dee4-156">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="0dee4-157">由 GitHub 问题 [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455) 跟踪此延迟的修复。</span><span class="sxs-lookup"><span data-stu-id="0dee4-157">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="0dee4-158">向前移动游标</span><span class="sxs-lookup"><span data-stu-id="0dee4-158">Move the cursor forward</span></span>

<span data-ttu-id="0dee4-159">成功处理目录项后，需要确定要保存的新游标值。</span><span class="sxs-lookup"><span data-stu-id="0dee4-159">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="0dee4-160">为了执行此操作，请找到处理的所有目录项的最大（按最新时间顺序） `commitTimeStamp`。</span><span class="sxs-lookup"><span data-stu-id="0dee4-160">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="0dee4-161">这是新的游标值。</span><span class="sxs-lookup"><span data-stu-id="0dee4-161">This is your new cursor value.</span></span> <span data-ttu-id="0dee4-162">将其保存到某些永久存储中，例如数据库、文件系统或 blob 存储。</span><span class="sxs-lookup"><span data-stu-id="0dee4-162">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="0dee4-163">当需要获取更多目录项时，只需通过从此永久存储中初始化游标值从[第一步](#initialize-a-cursor)开始。</span><span class="sxs-lookup"><span data-stu-id="0dee4-163">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="0dee4-164">如果应用程序引发异常或错误，请勿向前移动游标。</span><span class="sxs-lookup"><span data-stu-id="0dee4-164">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="0dee4-165">向前移动游标意味着不再需要处理游标前的目录项。</span><span class="sxs-lookup"><span data-stu-id="0dee4-165">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="0dee4-166">如果某些原因导致处理目录叶的方式有错误，只需及时向后移动游标并允许代码重新处理旧的目录项。</span><span class="sxs-lookup"><span data-stu-id="0dee4-166">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="0dee4-167">C# 示例代码</span><span class="sxs-lookup"><span data-stu-id="0dee4-167">C# sample code</span></span>

<span data-ttu-id="0dee4-168">因为目录是可以通过 HTTP 获得的 JSON 文档集，所以可以使用有 HTTP 客户端和 JSON 反序列化程序的任意编程语言与之交互。</span><span class="sxs-lookup"><span data-stu-id="0dee4-168">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="0dee4-169">C# 示例可在 [NuGet/示例存储库](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample)中获得。</span><span class="sxs-lookup"><span data-stu-id="0dee4-169">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="0dee4-170">目录 SDK</span><span class="sxs-lookup"><span data-stu-id="0dee4-170">Catalog SDK</span></span>

<span data-ttu-id="0dee4-171">使用目录最简单的方法是使用预发布 .NET 目录 SDK 包：[NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog)。</span><span class="sxs-lookup"><span data-stu-id="0dee4-171">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span> <span data-ttu-id="0dee4-172">此包可在 `nuget-build` MyGet 源`https://dotnet.myget.org/F/nuget-build/api/v3/index.json`上获得，可以使用 NuGet 包源 URL 找到该源。</span><span class="sxs-lookup"><span data-stu-id="0dee4-172">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="0dee4-173">可以将此包安装到与 `netstandard1.3` 或更高版本（例如 .NET Framework 4.6）兼容的项目。</span><span class="sxs-lookup"><span data-stu-id="0dee4-173">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="0dee4-174">使用此包的示例可在 [NuGet.Protocol.Catalog.Sample 项目](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample)中的 GitHub 上获得。</span><span class="sxs-lookup"><span data-stu-id="0dee4-174">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="0dee4-175">示例输出</span><span class="sxs-lookup"><span data-stu-id="0dee4-175">Sample output</span></span>

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a><span data-ttu-id="0dee4-176">最小示例</span><span class="sxs-lookup"><span data-stu-id="0dee4-176">Minimal sample</span></span>

<span data-ttu-id="0dee4-177">有关详细说明与目录交互的较少依赖项的示例，请参阅 [CatalogReaderExample 示例项目](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample)。</span><span class="sxs-lookup"><span data-stu-id="0dee4-177">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="0dee4-178">项目面向 `netcoreapp2.0` 并依赖 [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0)（适用于解析服务索引）和 [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1)（适用于 JSON 序列化）。</span><span class="sxs-lookup"><span data-stu-id="0dee4-178">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="0dee4-179">代码的主要逻辑在 [Program.cs 文件](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs)中可见。</span><span class="sxs-lookup"><span data-stu-id="0dee4-179">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="0dee4-180">示例输出</span><span class="sxs-lookup"><span data-stu-id="0dee4-180">Sample output</span></span>

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
