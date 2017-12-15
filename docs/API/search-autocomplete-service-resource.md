---
title: "记忆式键入功能、 NuGet API |Microsoft 文档"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: ead5cf7a-e51e-4cbb-8798-58226f4c853f
description: "搜索记忆式键入功能服务支持交互式发现的包 Id 和版本。"
keywords: "NuGet 记忆式键入功能 API、 NuGet 搜索包 ID、 子字符串包 ID"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 313ceb630947b46c34b98e14044ecf121b725087
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="autocomplete"></a><span data-ttu-id="34190-104">自动完成</span><span class="sxs-lookup"><span data-stu-id="34190-104">Autocomplete</span></span>

<span data-ttu-id="34190-105">它是可以生成使用 V3 API 的包 ID 和版本记忆式键入功能体验。</span><span class="sxs-lookup"><span data-stu-id="34190-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="34190-106">用于进行自动完成查询的资源是`SearchAutocompleteService`资源位于[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="34190-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="34190-107">版本管理</span><span class="sxs-lookup"><span data-stu-id="34190-107">Versioning</span></span>

<span data-ttu-id="34190-108">以下`@type`将使用值：</span><span class="sxs-lookup"><span data-stu-id="34190-108">The following `@type` values are used:</span></span>

<span data-ttu-id="34190-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="34190-109">@type value</span></span>                          | <span data-ttu-id="34190-110">说明</span><span class="sxs-lookup"><span data-stu-id="34190-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="34190-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="34190-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="34190-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="34190-112">The initial release</span></span>
<span data-ttu-id="34190-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="34190-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="34190-114">别名`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="34190-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="34190-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="34190-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="34190-116">别名`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="34190-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="34190-117">基 URL</span><span class="sxs-lookup"><span data-stu-id="34190-117">Base URL</span></span>

<span data-ttu-id="34190-118">以下 Api 的基 URL 是值`@id`与前面提到的资源之一相关联的属性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="34190-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="34190-119">在以下文档中，将占位符基本 URL`{@id}`将使用。</span><span class="sxs-lookup"><span data-stu-id="34190-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="34190-120">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="34190-120">HTTP Methods</span></span>

<span data-ttu-id="34190-121">HTTP 方法位于注册资源支持的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="34190-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="34190-122">搜索包 Id</span><span class="sxs-lookup"><span data-stu-id="34190-122">Search for package IDs</span></span>

<span data-ttu-id="34190-123">第一个自动完成 API 支持搜索包 ID 字符串的一部分。</span><span class="sxs-lookup"><span data-stu-id="34190-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="34190-124">当你想要提供用户界面集成在一起的 NuGet 包源中的包 typeahead 功能时，这非常有利。</span><span class="sxs-lookup"><span data-stu-id="34190-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="34190-125">仅未列出的版本的包将不会出现在结果中。</span><span class="sxs-lookup"><span data-stu-id="34190-125">A package with only unlisted versions will not appear in the results.</span></span>

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="34190-126">请求参数</span><span class="sxs-lookup"><span data-stu-id="34190-126">Request parameters</span></span>

<span data-ttu-id="34190-127">名称</span><span class="sxs-lookup"><span data-stu-id="34190-127">Name</span></span>        | <span data-ttu-id="34190-128">内</span><span class="sxs-lookup"><span data-stu-id="34190-128">In</span></span>     | <span data-ttu-id="34190-129">类型</span><span class="sxs-lookup"><span data-stu-id="34190-129">Type</span></span>    | <span data-ttu-id="34190-130">必需</span><span class="sxs-lookup"><span data-stu-id="34190-130">Required</span></span> | <span data-ttu-id="34190-131">说明</span><span class="sxs-lookup"><span data-stu-id="34190-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="34190-132">q</span><span class="sxs-lookup"><span data-stu-id="34190-132">q</span></span>           | <span data-ttu-id="34190-133">URL</span><span class="sxs-lookup"><span data-stu-id="34190-133">URL</span></span>    | <span data-ttu-id="34190-134">string</span><span class="sxs-lookup"><span data-stu-id="34190-134">string</span></span>  | <span data-ttu-id="34190-135">no</span><span class="sxs-lookup"><span data-stu-id="34190-135">no</span></span>       | <span data-ttu-id="34190-136">要针对包 Id 进行比较的字符串</span><span class="sxs-lookup"><span data-stu-id="34190-136">The string to compare against package IDs</span></span>
<span data-ttu-id="34190-137">skip</span><span class="sxs-lookup"><span data-stu-id="34190-137">skip</span></span>        | <span data-ttu-id="34190-138">URL</span><span class="sxs-lookup"><span data-stu-id="34190-138">URL</span></span>    | <span data-ttu-id="34190-139">整数</span><span class="sxs-lookup"><span data-stu-id="34190-139">integer</span></span> | <span data-ttu-id="34190-140">no</span><span class="sxs-lookup"><span data-stu-id="34190-140">no</span></span>       | <span data-ttu-id="34190-141">要分页的跳过的结果数</span><span class="sxs-lookup"><span data-stu-id="34190-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="34190-142">take</span><span class="sxs-lookup"><span data-stu-id="34190-142">take</span></span>        | <span data-ttu-id="34190-143">URL</span><span class="sxs-lookup"><span data-stu-id="34190-143">URL</span></span>    | <span data-ttu-id="34190-144">整数</span><span class="sxs-lookup"><span data-stu-id="34190-144">integer</span></span> | <span data-ttu-id="34190-145">no</span><span class="sxs-lookup"><span data-stu-id="34190-145">no</span></span>       | <span data-ttu-id="34190-146">要为分页返回的结果数</span><span class="sxs-lookup"><span data-stu-id="34190-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="34190-147">预发行版</span><span class="sxs-lookup"><span data-stu-id="34190-147">prerelease</span></span>  | <span data-ttu-id="34190-148">URL</span><span class="sxs-lookup"><span data-stu-id="34190-148">URL</span></span>    | <span data-ttu-id="34190-149">boolean</span><span class="sxs-lookup"><span data-stu-id="34190-149">boolean</span></span> | <span data-ttu-id="34190-150">no</span><span class="sxs-lookup"><span data-stu-id="34190-150">no</span></span>       | <span data-ttu-id="34190-151">`true`或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="34190-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="34190-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="34190-152">semVerLevel</span></span> | <span data-ttu-id="34190-153">URL</span><span class="sxs-lookup"><span data-stu-id="34190-153">URL</span></span>    | <span data-ttu-id="34190-154">string</span><span class="sxs-lookup"><span data-stu-id="34190-154">string</span></span>  | <span data-ttu-id="34190-155">no</span><span class="sxs-lookup"><span data-stu-id="34190-155">no</span></span>       | <span data-ttu-id="34190-156">SemVer 1.0.0 版本字符串</span><span class="sxs-lookup"><span data-stu-id="34190-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="34190-157">自动完成查询`q`分析由服务器实现定义的方式。</span><span class="sxs-lookup"><span data-stu-id="34190-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="34190-158">nuget.org 支持查询个前缀的包 ID 令牌，它们是由拆分生成的 ID 的段原始由 camel 大小写和符号字符。</span><span class="sxs-lookup"><span data-stu-id="34190-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="34190-159">`skip`参数默认值为 0。</span><span class="sxs-lookup"><span data-stu-id="34190-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="34190-160">`take`参数应大于零的整数。</span><span class="sxs-lookup"><span data-stu-id="34190-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="34190-161">服务器实现可能会对施加的最大值。</span><span class="sxs-lookup"><span data-stu-id="34190-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="34190-162">如果`prerelease`未提供排除预发行包。</span><span class="sxs-lookup"><span data-stu-id="34190-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="34190-163">`semVerLevel`查询参数用来选择[SemVer 2.0.0 包](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。</span><span class="sxs-lookup"><span data-stu-id="34190-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="34190-164">如果排除此查询参数，将返回与 SemVer 1.0.0 兼容版本的唯一包 Id (与[标准的 NuGet 版本控制](../reference/package-versioning.md)需要注意的问题，如使用 4 的整数部分的版本字符串)。</span><span class="sxs-lookup"><span data-stu-id="34190-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="34190-165">如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 兼容包将返回。</span><span class="sxs-lookup"><span data-stu-id="34190-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="34190-166">请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="34190-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="34190-167">响应</span><span class="sxs-lookup"><span data-stu-id="34190-167">Response</span></span>

<span data-ttu-id="34190-168">响应是包含最多的 JSON 文档`take`记忆式键入功能结果。</span><span class="sxs-lookup"><span data-stu-id="34190-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="34190-169">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="34190-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="34190-170">名称</span><span class="sxs-lookup"><span data-stu-id="34190-170">Name</span></span>      | <span data-ttu-id="34190-171">类型</span><span class="sxs-lookup"><span data-stu-id="34190-171">Type</span></span>             | <span data-ttu-id="34190-172">必需</span><span class="sxs-lookup"><span data-stu-id="34190-172">Required</span></span> | <span data-ttu-id="34190-173">说明</span><span class="sxs-lookup"><span data-stu-id="34190-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="34190-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="34190-174">totalHits</span></span> | <span data-ttu-id="34190-175">整数</span><span class="sxs-lookup"><span data-stu-id="34190-175">integer</span></span>          | <span data-ttu-id="34190-176">是</span><span class="sxs-lookup"><span data-stu-id="34190-176">yes</span></span>      | <span data-ttu-id="34190-177">匹配项，而不考虑的总数目`skip`和`take`</span><span class="sxs-lookup"><span data-stu-id="34190-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="34190-178">数据</span><span class="sxs-lookup"><span data-stu-id="34190-178">data</span></span>      | <span data-ttu-id="34190-179">字符串数组</span><span class="sxs-lookup"><span data-stu-id="34190-179">array of strings</span></span> | <span data-ttu-id="34190-180">是</span><span class="sxs-lookup"><span data-stu-id="34190-180">yes</span></span>      | <span data-ttu-id="34190-181">由请求的包 Id 匹配</span><span class="sxs-lookup"><span data-stu-id="34190-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="34190-182">示例请求</span><span class="sxs-lookup"><span data-stu-id="34190-182">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="34190-183">示例响应</span><span class="sxs-lookup"><span data-stu-id="34190-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="34190-184">枚举包版本</span><span class="sxs-lookup"><span data-stu-id="34190-184">Enumerate package versions</span></span>

<span data-ttu-id="34190-185">客户端后，发现了包 ID 使用以前的 API，可以使用记忆式键入 API 提供的包 id 枚举包版本</span><span class="sxs-lookup"><span data-stu-id="34190-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="34190-186">未列出的包版本将不会出现在结果中。</span><span class="sxs-lookup"><span data-stu-id="34190-186">A package version that is unlisted will not appear in the results.</span></span>

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="34190-187">请求参数</span><span class="sxs-lookup"><span data-stu-id="34190-187">Request parameters</span></span>

<span data-ttu-id="34190-188">名称</span><span class="sxs-lookup"><span data-stu-id="34190-188">Name</span></span>        | <span data-ttu-id="34190-189">内</span><span class="sxs-lookup"><span data-stu-id="34190-189">In</span></span>     | <span data-ttu-id="34190-190">类型</span><span class="sxs-lookup"><span data-stu-id="34190-190">Type</span></span>    | <span data-ttu-id="34190-191">必需</span><span class="sxs-lookup"><span data-stu-id="34190-191">Required</span></span> | <span data-ttu-id="34190-192">说明</span><span class="sxs-lookup"><span data-stu-id="34190-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="34190-193">id</span><span class="sxs-lookup"><span data-stu-id="34190-193">id</span></span>          | <span data-ttu-id="34190-194">URL</span><span class="sxs-lookup"><span data-stu-id="34190-194">URL</span></span>    | <span data-ttu-id="34190-195">string</span><span class="sxs-lookup"><span data-stu-id="34190-195">string</span></span>  | <span data-ttu-id="34190-196">是</span><span class="sxs-lookup"><span data-stu-id="34190-196">yes</span></span>      | <span data-ttu-id="34190-197">要提取的版本的包 ID</span><span class="sxs-lookup"><span data-stu-id="34190-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="34190-198">预发行版</span><span class="sxs-lookup"><span data-stu-id="34190-198">prerelease</span></span>  | <span data-ttu-id="34190-199">URL</span><span class="sxs-lookup"><span data-stu-id="34190-199">URL</span></span>    | <span data-ttu-id="34190-200">boolean</span><span class="sxs-lookup"><span data-stu-id="34190-200">boolean</span></span> | <span data-ttu-id="34190-201">no</span><span class="sxs-lookup"><span data-stu-id="34190-201">no</span></span>       | <span data-ttu-id="34190-202">`true`或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="34190-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="34190-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="34190-203">semVerLevel</span></span> | <span data-ttu-id="34190-204">URL</span><span class="sxs-lookup"><span data-stu-id="34190-204">URL</span></span>    | <span data-ttu-id="34190-205">string</span><span class="sxs-lookup"><span data-stu-id="34190-205">string</span></span>  | <span data-ttu-id="34190-206">no</span><span class="sxs-lookup"><span data-stu-id="34190-206">no</span></span>       | <span data-ttu-id="34190-207">SemVer 2.0.0 的版本字符串</span><span class="sxs-lookup"><span data-stu-id="34190-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="34190-208">如果`prerelease`未提供排除预发行包。</span><span class="sxs-lookup"><span data-stu-id="34190-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="34190-209">`semVerLevel`查询参数用于选择加入到 SemVer 2.0.0 包。</span><span class="sxs-lookup"><span data-stu-id="34190-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="34190-210">如果排除此查询参数，将返回仅 SemVer 1.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="34190-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="34190-211">如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 版本将返回。</span><span class="sxs-lookup"><span data-stu-id="34190-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="34190-212">请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="34190-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="34190-213">响应</span><span class="sxs-lookup"><span data-stu-id="34190-213">Response</span></span>

<span data-ttu-id="34190-214">响应是包含所有包版本的提供的包 ID，筛选由给定的查询参数的 JSON 文档。</span><span class="sxs-lookup"><span data-stu-id="34190-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="34190-215">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="34190-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="34190-216">名称</span><span class="sxs-lookup"><span data-stu-id="34190-216">Name</span></span>      | <span data-ttu-id="34190-217">类型</span><span class="sxs-lookup"><span data-stu-id="34190-217">Type</span></span>             | <span data-ttu-id="34190-218">必需</span><span class="sxs-lookup"><span data-stu-id="34190-218">Required</span></span> | <span data-ttu-id="34190-219">说明</span><span class="sxs-lookup"><span data-stu-id="34190-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="34190-220">数据</span><span class="sxs-lookup"><span data-stu-id="34190-220">data</span></span>      | <span data-ttu-id="34190-221">字符串数组</span><span class="sxs-lookup"><span data-stu-id="34190-221">array of strings</span></span> | <span data-ttu-id="34190-222">是</span><span class="sxs-lookup"><span data-stu-id="34190-222">yes</span></span>      | <span data-ttu-id="34190-223">由请求匹配的程序包版本</span><span class="sxs-lookup"><span data-stu-id="34190-223">The package versions matched by the request</span></span>

<span data-ttu-id="34190-224">中的包版本`data`数组可能包含 SemVer 2.0.0 生成元数据 (例如`1.0.0+metadata`) 如果`semVerLevel=2.0.0`查询字符串中提供。</span><span class="sxs-lookup"><span data-stu-id="34190-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="34190-225">示例请求</span><span class="sxs-lookup"><span data-stu-id="34190-225">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="34190-226">示例响应</span><span class="sxs-lookup"><span data-stu-id="34190-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
