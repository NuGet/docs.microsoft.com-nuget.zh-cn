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
description: "搜索记忆式键入功能服务支持交互式发现的包 Id 和版本。"
keywords: "NuGet 记忆式键入功能 API、 NuGet 搜索包 ID、 子字符串包 ID"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="autocomplete"></a><span data-ttu-id="7b661-104">自动完成</span><span class="sxs-lookup"><span data-stu-id="7b661-104">Autocomplete</span></span>

<span data-ttu-id="7b661-105">它是可以生成使用 V3 API 的包 ID 和版本记忆式键入功能体验。</span><span class="sxs-lookup"><span data-stu-id="7b661-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="7b661-106">用于进行自动完成查询的资源是`SearchAutocompleteService`资源位于[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="7b661-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="7b661-107">版本管理</span><span class="sxs-lookup"><span data-stu-id="7b661-107">Versioning</span></span>

<span data-ttu-id="7b661-108">以下`@type`将使用值：</span><span class="sxs-lookup"><span data-stu-id="7b661-108">The following `@type` values are used:</span></span>

<span data-ttu-id="7b661-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="7b661-109">@type value</span></span>                          | <span data-ttu-id="7b661-110">说明</span><span class="sxs-lookup"><span data-stu-id="7b661-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="7b661-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="7b661-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="7b661-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="7b661-112">The initial release</span></span>
<span data-ttu-id="7b661-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="7b661-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="7b661-114">别名`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="7b661-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="7b661-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="7b661-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="7b661-116">别名`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="7b661-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="7b661-117">基 URL</span><span class="sxs-lookup"><span data-stu-id="7b661-117">Base URL</span></span>

<span data-ttu-id="7b661-118">以下 Api 的基 URL 是值`@id`与前面提到的资源之一相关联的属性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="7b661-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="7b661-119">在以下文档中，将占位符基本 URL`{@id}`将使用。</span><span class="sxs-lookup"><span data-stu-id="7b661-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="7b661-120">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="7b661-120">HTTP Methods</span></span>

<span data-ttu-id="7b661-121">HTTP 方法位于注册资源支持的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="7b661-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="7b661-122">搜索包 Id</span><span class="sxs-lookup"><span data-stu-id="7b661-122">Search for package IDs</span></span>

<span data-ttu-id="7b661-123">第一个自动完成 API 支持搜索包 ID 字符串的一部分。</span><span class="sxs-lookup"><span data-stu-id="7b661-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="7b661-124">当你想要提供用户界面集成在一起的 NuGet 包源中的包 typeahead 功能时，这非常有利。</span><span class="sxs-lookup"><span data-stu-id="7b661-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="7b661-125">仅未列出的版本的包将不会出现在结果中。</span><span class="sxs-lookup"><span data-stu-id="7b661-125">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="7b661-126">请求参数</span><span class="sxs-lookup"><span data-stu-id="7b661-126">Request parameters</span></span>

<span data-ttu-id="7b661-127">name</span><span class="sxs-lookup"><span data-stu-id="7b661-127">Name</span></span>        | <span data-ttu-id="7b661-128">内</span><span class="sxs-lookup"><span data-stu-id="7b661-128">In</span></span>     | <span data-ttu-id="7b661-129">类型</span><span class="sxs-lookup"><span data-stu-id="7b661-129">Type</span></span>    | <span data-ttu-id="7b661-130">必需</span><span class="sxs-lookup"><span data-stu-id="7b661-130">Required</span></span> | <span data-ttu-id="7b661-131">说明</span><span class="sxs-lookup"><span data-stu-id="7b661-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="7b661-132">q</span><span class="sxs-lookup"><span data-stu-id="7b661-132">q</span></span>           | <span data-ttu-id="7b661-133">URL</span><span class="sxs-lookup"><span data-stu-id="7b661-133">URL</span></span>    | <span data-ttu-id="7b661-134">字符串</span><span class="sxs-lookup"><span data-stu-id="7b661-134">string</span></span>  | <span data-ttu-id="7b661-135">否</span><span class="sxs-lookup"><span data-stu-id="7b661-135">no</span></span>       | <span data-ttu-id="7b661-136">要针对包 Id 进行比较的字符串</span><span class="sxs-lookup"><span data-stu-id="7b661-136">The string to compare against package IDs</span></span>
<span data-ttu-id="7b661-137">skip</span><span class="sxs-lookup"><span data-stu-id="7b661-137">skip</span></span>        | <span data-ttu-id="7b661-138">URL</span><span class="sxs-lookup"><span data-stu-id="7b661-138">URL</span></span>    | <span data-ttu-id="7b661-139">整数</span><span class="sxs-lookup"><span data-stu-id="7b661-139">integer</span></span> | <span data-ttu-id="7b661-140">否</span><span class="sxs-lookup"><span data-stu-id="7b661-140">no</span></span>       | <span data-ttu-id="7b661-141">要分页的跳过的结果数</span><span class="sxs-lookup"><span data-stu-id="7b661-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="7b661-142">take</span><span class="sxs-lookup"><span data-stu-id="7b661-142">take</span></span>        | <span data-ttu-id="7b661-143">URL</span><span class="sxs-lookup"><span data-stu-id="7b661-143">URL</span></span>    | <span data-ttu-id="7b661-144">整数</span><span class="sxs-lookup"><span data-stu-id="7b661-144">integer</span></span> | <span data-ttu-id="7b661-145">否</span><span class="sxs-lookup"><span data-stu-id="7b661-145">no</span></span>       | <span data-ttu-id="7b661-146">要为分页返回的结果数</span><span class="sxs-lookup"><span data-stu-id="7b661-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="7b661-147">预发行版</span><span class="sxs-lookup"><span data-stu-id="7b661-147">prerelease</span></span>  | <span data-ttu-id="7b661-148">URL</span><span class="sxs-lookup"><span data-stu-id="7b661-148">URL</span></span>    | <span data-ttu-id="7b661-149">boolean</span><span class="sxs-lookup"><span data-stu-id="7b661-149">boolean</span></span> | <span data-ttu-id="7b661-150">否</span><span class="sxs-lookup"><span data-stu-id="7b661-150">no</span></span>       | <span data-ttu-id="7b661-151">`true`或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="7b661-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="7b661-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="7b661-152">semVerLevel</span></span> | <span data-ttu-id="7b661-153">URL</span><span class="sxs-lookup"><span data-stu-id="7b661-153">URL</span></span>    | <span data-ttu-id="7b661-154">字符串</span><span class="sxs-lookup"><span data-stu-id="7b661-154">string</span></span>  | <span data-ttu-id="7b661-155">否</span><span class="sxs-lookup"><span data-stu-id="7b661-155">no</span></span>       | <span data-ttu-id="7b661-156">SemVer 1.0.0 版本字符串</span><span class="sxs-lookup"><span data-stu-id="7b661-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="7b661-157">自动完成查询`q`分析由服务器实现定义的方式。</span><span class="sxs-lookup"><span data-stu-id="7b661-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="7b661-158">nuget.org 支持查询个前缀的包 ID 令牌，它们是由拆分生成的 ID 的段原始由 camel 大小写和符号字符。</span><span class="sxs-lookup"><span data-stu-id="7b661-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="7b661-159">`skip`参数默认值为 0。</span><span class="sxs-lookup"><span data-stu-id="7b661-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="7b661-160">`take`参数应大于零的整数。</span><span class="sxs-lookup"><span data-stu-id="7b661-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="7b661-161">服务器实现可能会对施加的最大值。</span><span class="sxs-lookup"><span data-stu-id="7b661-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="7b661-162">如果`prerelease`未提供排除预发行包。</span><span class="sxs-lookup"><span data-stu-id="7b661-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="7b661-163">`semVerLevel`查询参数用来选择[SemVer 2.0.0 包](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。</span><span class="sxs-lookup"><span data-stu-id="7b661-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="7b661-164">如果排除此查询参数，将返回与 SemVer 1.0.0 兼容版本的唯一包 Id (与[标准的 NuGet 版本控制](../reference/package-versioning.md)需要注意的问题，如使用 4 的整数部分的版本字符串)。</span><span class="sxs-lookup"><span data-stu-id="7b661-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="7b661-165">如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 兼容包将返回。</span><span class="sxs-lookup"><span data-stu-id="7b661-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="7b661-166">请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="7b661-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="7b661-167">响应</span><span class="sxs-lookup"><span data-stu-id="7b661-167">Response</span></span>

<span data-ttu-id="7b661-168">响应是包含最多的 JSON 文档`take`记忆式键入功能结果。</span><span class="sxs-lookup"><span data-stu-id="7b661-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="7b661-169">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="7b661-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="7b661-170">name</span><span class="sxs-lookup"><span data-stu-id="7b661-170">Name</span></span>      | <span data-ttu-id="7b661-171">类型</span><span class="sxs-lookup"><span data-stu-id="7b661-171">Type</span></span>             | <span data-ttu-id="7b661-172">必需</span><span class="sxs-lookup"><span data-stu-id="7b661-172">Required</span></span> | <span data-ttu-id="7b661-173">说明</span><span class="sxs-lookup"><span data-stu-id="7b661-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="7b661-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="7b661-174">totalHits</span></span> | <span data-ttu-id="7b661-175">整数</span><span class="sxs-lookup"><span data-stu-id="7b661-175">integer</span></span>          | <span data-ttu-id="7b661-176">是</span><span class="sxs-lookup"><span data-stu-id="7b661-176">yes</span></span>      | <span data-ttu-id="7b661-177">匹配项，而不考虑的总数目`skip`和`take`</span><span class="sxs-lookup"><span data-stu-id="7b661-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="7b661-178">数据</span><span class="sxs-lookup"><span data-stu-id="7b661-178">data</span></span>      | <span data-ttu-id="7b661-179">字符串数组</span><span class="sxs-lookup"><span data-stu-id="7b661-179">array of strings</span></span> | <span data-ttu-id="7b661-180">是</span><span class="sxs-lookup"><span data-stu-id="7b661-180">yes</span></span>      | <span data-ttu-id="7b661-181">由请求的包 Id 匹配</span><span class="sxs-lookup"><span data-stu-id="7b661-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="7b661-182">示例请求</span><span class="sxs-lookup"><span data-stu-id="7b661-182">Sample request</span></span>

<span data-ttu-id="7b661-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="7b661-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="7b661-184">示例响应</span><span class="sxs-lookup"><span data-stu-id="7b661-184">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="7b661-185">枚举包版本</span><span class="sxs-lookup"><span data-stu-id="7b661-185">Enumerate package versions</span></span>

<span data-ttu-id="7b661-186">客户端后，发现了包 ID 使用以前的 API，可以使用记忆式键入 API 提供的包 id 枚举包版本</span><span class="sxs-lookup"><span data-stu-id="7b661-186">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="7b661-187">未列出的包版本将不会出现在结果中。</span><span class="sxs-lookup"><span data-stu-id="7b661-187">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="7b661-188">请求参数</span><span class="sxs-lookup"><span data-stu-id="7b661-188">Request parameters</span></span>

<span data-ttu-id="7b661-189">name</span><span class="sxs-lookup"><span data-stu-id="7b661-189">Name</span></span>        | <span data-ttu-id="7b661-190">内</span><span class="sxs-lookup"><span data-stu-id="7b661-190">In</span></span>     | <span data-ttu-id="7b661-191">类型</span><span class="sxs-lookup"><span data-stu-id="7b661-191">Type</span></span>    | <span data-ttu-id="7b661-192">必需</span><span class="sxs-lookup"><span data-stu-id="7b661-192">Required</span></span> | <span data-ttu-id="7b661-193">说明</span><span class="sxs-lookup"><span data-stu-id="7b661-193">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="7b661-194">id</span><span class="sxs-lookup"><span data-stu-id="7b661-194">id</span></span>          | <span data-ttu-id="7b661-195">URL</span><span class="sxs-lookup"><span data-stu-id="7b661-195">URL</span></span>    | <span data-ttu-id="7b661-196">字符串</span><span class="sxs-lookup"><span data-stu-id="7b661-196">string</span></span>  | <span data-ttu-id="7b661-197">是</span><span class="sxs-lookup"><span data-stu-id="7b661-197">yes</span></span>      | <span data-ttu-id="7b661-198">要提取的版本的包 ID</span><span class="sxs-lookup"><span data-stu-id="7b661-198">The package ID to fetch versions for</span></span>
<span data-ttu-id="7b661-199">预发行版</span><span class="sxs-lookup"><span data-stu-id="7b661-199">prerelease</span></span>  | <span data-ttu-id="7b661-200">URL</span><span class="sxs-lookup"><span data-stu-id="7b661-200">URL</span></span>    | <span data-ttu-id="7b661-201">boolean</span><span class="sxs-lookup"><span data-stu-id="7b661-201">boolean</span></span> | <span data-ttu-id="7b661-202">否</span><span class="sxs-lookup"><span data-stu-id="7b661-202">no</span></span>       | <span data-ttu-id="7b661-203">`true`或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="7b661-203">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="7b661-204">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="7b661-204">semVerLevel</span></span> | <span data-ttu-id="7b661-205">URL</span><span class="sxs-lookup"><span data-stu-id="7b661-205">URL</span></span>    | <span data-ttu-id="7b661-206">字符串</span><span class="sxs-lookup"><span data-stu-id="7b661-206">string</span></span>  | <span data-ttu-id="7b661-207">否</span><span class="sxs-lookup"><span data-stu-id="7b661-207">no</span></span>       | <span data-ttu-id="7b661-208">SemVer 2.0.0 的版本字符串</span><span class="sxs-lookup"><span data-stu-id="7b661-208">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="7b661-209">如果`prerelease`未提供排除预发行包。</span><span class="sxs-lookup"><span data-stu-id="7b661-209">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="7b661-210">`semVerLevel`查询参数用于选择加入到 SemVer 2.0.0 包。</span><span class="sxs-lookup"><span data-stu-id="7b661-210">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="7b661-211">如果排除此查询参数，将返回仅 SemVer 1.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="7b661-211">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="7b661-212">如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 版本将返回。</span><span class="sxs-lookup"><span data-stu-id="7b661-212">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="7b661-213">请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="7b661-213">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="7b661-214">响应</span><span class="sxs-lookup"><span data-stu-id="7b661-214">Response</span></span>

<span data-ttu-id="7b661-215">响应是包含所有包版本的提供的包 ID，筛选由给定的查询参数的 JSON 文档。</span><span class="sxs-lookup"><span data-stu-id="7b661-215">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="7b661-216">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="7b661-216">The root JSON object has the following property:</span></span>

<span data-ttu-id="7b661-217">name</span><span class="sxs-lookup"><span data-stu-id="7b661-217">Name</span></span>      | <span data-ttu-id="7b661-218">类型</span><span class="sxs-lookup"><span data-stu-id="7b661-218">Type</span></span>             | <span data-ttu-id="7b661-219">必需</span><span class="sxs-lookup"><span data-stu-id="7b661-219">Required</span></span> | <span data-ttu-id="7b661-220">说明</span><span class="sxs-lookup"><span data-stu-id="7b661-220">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="7b661-221">数据</span><span class="sxs-lookup"><span data-stu-id="7b661-221">data</span></span>      | <span data-ttu-id="7b661-222">字符串数组</span><span class="sxs-lookup"><span data-stu-id="7b661-222">array of strings</span></span> | <span data-ttu-id="7b661-223">是</span><span class="sxs-lookup"><span data-stu-id="7b661-223">yes</span></span>      | <span data-ttu-id="7b661-224">由请求匹配的程序包版本</span><span class="sxs-lookup"><span data-stu-id="7b661-224">The package versions matched by the request</span></span>

<span data-ttu-id="7b661-225">中的包版本`data`数组可能包含 SemVer 2.0.0 生成元数据 (例如`1.0.0+metadata`) 如果`semVerLevel=2.0.0`查询字符串中提供。</span><span class="sxs-lookup"><span data-stu-id="7b661-225">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="7b661-226">示例请求</span><span class="sxs-lookup"><span data-stu-id="7b661-226">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="7b661-227">示例响应</span><span class="sxs-lookup"><span data-stu-id="7b661-227">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
