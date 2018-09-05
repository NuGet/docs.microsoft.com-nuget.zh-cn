---
title: 记忆式键入功能，NuGet API
description: 该搜索自动完成服务支持交互式搜索的包 Id 和版本。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 01f919dc3bbfb6752c8f8e055a3cd473ad194e75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549078"
---
# <a name="autocomplete"></a><span data-ttu-id="6fae9-103">自动完成</span><span class="sxs-lookup"><span data-stu-id="6fae9-103">Autocomplete</span></span>

<span data-ttu-id="6fae9-104">它是可以构建使用 V3 API 的包 ID 和版本自动完成体验。</span><span class="sxs-lookup"><span data-stu-id="6fae9-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="6fae9-105">在进行自动完成查询使用的资源是`SearchAutocompleteService`资源中找到[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="6fae9-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="6fae9-106">版本管理</span><span class="sxs-lookup"><span data-stu-id="6fae9-106">Versioning</span></span>

<span data-ttu-id="6fae9-107">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="6fae9-107">The following `@type` values are used:</span></span>

<span data-ttu-id="6fae9-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="6fae9-108">@type value</span></span>                          | <span data-ttu-id="6fae9-109">说明</span><span class="sxs-lookup"><span data-stu-id="6fae9-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="6fae9-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="6fae9-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="6fae9-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="6fae9-111">The initial release</span></span>
<span data-ttu-id="6fae9-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="6fae9-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="6fae9-113">别名 `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="6fae9-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="6fae9-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="6fae9-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="6fae9-115">别名 `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="6fae9-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="6fae9-116">基 URL</span><span class="sxs-lookup"><span data-stu-id="6fae9-116">Base URL</span></span>

<span data-ttu-id="6fae9-117">以下 Api 的基 URL 是的值`@id`属性与前面提到的资源之一相关联`@type`值。</span><span class="sxs-lookup"><span data-stu-id="6fae9-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="6fae9-118">在以下文档中，占位符基 URL`{@id}`将使用。</span><span class="sxs-lookup"><span data-stu-id="6fae9-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="6fae9-119">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="6fae9-119">HTTP Methods</span></span>

<span data-ttu-id="6fae9-120">中的注册资源支持的 HTTP 方法找到的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="6fae9-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="6fae9-121">搜索包 Id</span><span class="sxs-lookup"><span data-stu-id="6fae9-121">Search for package IDs</span></span>

<span data-ttu-id="6fae9-122">第一个自动完成 API 支持搜索包 ID 字符串的一部分。</span><span class="sxs-lookup"><span data-stu-id="6fae9-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="6fae9-123">当您想要提供用户界面集成在一起的 NuGet 包源中的包 typeahead 功能时，这非常有利。</span><span class="sxs-lookup"><span data-stu-id="6fae9-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="6fae9-124">仅未列出的版本的包不会出现在结果中。</span><span class="sxs-lookup"><span data-stu-id="6fae9-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="6fae9-125">请求参数</span><span class="sxs-lookup"><span data-stu-id="6fae9-125">Request parameters</span></span>

<span data-ttu-id="6fae9-126">name</span><span class="sxs-lookup"><span data-stu-id="6fae9-126">Name</span></span>        | <span data-ttu-id="6fae9-127">内</span><span class="sxs-lookup"><span data-stu-id="6fae9-127">In</span></span>     | <span data-ttu-id="6fae9-128">类型</span><span class="sxs-lookup"><span data-stu-id="6fae9-128">Type</span></span>    | <span data-ttu-id="6fae9-129">必需</span><span class="sxs-lookup"><span data-stu-id="6fae9-129">Required</span></span> | <span data-ttu-id="6fae9-130">说明</span><span class="sxs-lookup"><span data-stu-id="6fae9-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="6fae9-131">q</span><span class="sxs-lookup"><span data-stu-id="6fae9-131">q</span></span>           | <span data-ttu-id="6fae9-132">URL</span><span class="sxs-lookup"><span data-stu-id="6fae9-132">URL</span></span>    | <span data-ttu-id="6fae9-133">字符串</span><span class="sxs-lookup"><span data-stu-id="6fae9-133">string</span></span>  | <span data-ttu-id="6fae9-134">否</span><span class="sxs-lookup"><span data-stu-id="6fae9-134">no</span></span>       | <span data-ttu-id="6fae9-135">要与包 Id 进行比较的字符串</span><span class="sxs-lookup"><span data-stu-id="6fae9-135">The string to compare against package IDs</span></span>
<span data-ttu-id="6fae9-136">skip</span><span class="sxs-lookup"><span data-stu-id="6fae9-136">skip</span></span>        | <span data-ttu-id="6fae9-137">URL</span><span class="sxs-lookup"><span data-stu-id="6fae9-137">URL</span></span>    | <span data-ttu-id="6fae9-138">整数</span><span class="sxs-lookup"><span data-stu-id="6fae9-138">integer</span></span> | <span data-ttu-id="6fae9-139">否</span><span class="sxs-lookup"><span data-stu-id="6fae9-139">no</span></span>       | <span data-ttu-id="6fae9-140">要分页的跳过的结果数</span><span class="sxs-lookup"><span data-stu-id="6fae9-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="6fae9-141">Take</span><span class="sxs-lookup"><span data-stu-id="6fae9-141">take</span></span>        | <span data-ttu-id="6fae9-142">URL</span><span class="sxs-lookup"><span data-stu-id="6fae9-142">URL</span></span>    | <span data-ttu-id="6fae9-143">整数</span><span class="sxs-lookup"><span data-stu-id="6fae9-143">integer</span></span> | <span data-ttu-id="6fae9-144">否</span><span class="sxs-lookup"><span data-stu-id="6fae9-144">no</span></span>       | <span data-ttu-id="6fae9-145">要为分页返回的结果数</span><span class="sxs-lookup"><span data-stu-id="6fae9-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="6fae9-146">预发行版</span><span class="sxs-lookup"><span data-stu-id="6fae9-146">prerelease</span></span>  | <span data-ttu-id="6fae9-147">URL</span><span class="sxs-lookup"><span data-stu-id="6fae9-147">URL</span></span>    | <span data-ttu-id="6fae9-148">boolean</span><span class="sxs-lookup"><span data-stu-id="6fae9-148">boolean</span></span> | <span data-ttu-id="6fae9-149">否</span><span class="sxs-lookup"><span data-stu-id="6fae9-149">no</span></span>       | <span data-ttu-id="6fae9-150">`true` 或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="6fae9-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="6fae9-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="6fae9-151">semVerLevel</span></span> | <span data-ttu-id="6fae9-152">URL</span><span class="sxs-lookup"><span data-stu-id="6fae9-152">URL</span></span>    | <span data-ttu-id="6fae9-153">字符串</span><span class="sxs-lookup"><span data-stu-id="6fae9-153">string</span></span>  | <span data-ttu-id="6fae9-154">否</span><span class="sxs-lookup"><span data-stu-id="6fae9-154">no</span></span>       | <span data-ttu-id="6fae9-155">SemVer 1.0.0 版本字符串</span><span class="sxs-lookup"><span data-stu-id="6fae9-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="6fae9-156">记忆式键入功能查询`q`分析由服务器实现定义的方式。</span><span class="sxs-lookup"><span data-stu-id="6fae9-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="6fae9-157">nuget.org 支持查询是由拆分生成的 ID 的片段的包 ID 令牌的前缀为原始由驼峰式大小写和符号字符。</span><span class="sxs-lookup"><span data-stu-id="6fae9-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="6fae9-158">`skip`参数默认值为 0。</span><span class="sxs-lookup"><span data-stu-id="6fae9-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="6fae9-159">`take`参数应为大于零的整数。</span><span class="sxs-lookup"><span data-stu-id="6fae9-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="6fae9-160">服务器实现可能会施加最大值。</span><span class="sxs-lookup"><span data-stu-id="6fae9-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="6fae9-161">如果`prerelease`未提供排除预发行包。</span><span class="sxs-lookup"><span data-stu-id="6fae9-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="6fae9-162">`semVerLevel`查询参数用来选择中加入[SemVer 2.0.0 包](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。</span><span class="sxs-lookup"><span data-stu-id="6fae9-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="6fae9-163">如果排除此查询参数，将返回与 SemVer 1.0.0 兼容版本的唯一程序包 Id (与[standard 的 NuGet 版本控制](../reference/package-versioning.md)需要注意的问题，例如使用 4 个整数部分的版本字符串)。</span><span class="sxs-lookup"><span data-stu-id="6fae9-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="6fae9-164">如果`semVerLevel=2.0.0`提供，将返回 SemVer 1.0.0 和 SemVer 2.0.0 兼容包。</span><span class="sxs-lookup"><span data-stu-id="6fae9-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="6fae9-165">请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="6fae9-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="6fae9-166">响应</span><span class="sxs-lookup"><span data-stu-id="6fae9-166">Response</span></span>

<span data-ttu-id="6fae9-167">响应是 JSON 文档，其中最多包含`take`记忆式键入功能结果。</span><span class="sxs-lookup"><span data-stu-id="6fae9-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="6fae9-168">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="6fae9-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="6fae9-169">name</span><span class="sxs-lookup"><span data-stu-id="6fae9-169">Name</span></span>      | <span data-ttu-id="6fae9-170">类型</span><span class="sxs-lookup"><span data-stu-id="6fae9-170">Type</span></span>             | <span data-ttu-id="6fae9-171">必需</span><span class="sxs-lookup"><span data-stu-id="6fae9-171">Required</span></span> | <span data-ttu-id="6fae9-172">说明</span><span class="sxs-lookup"><span data-stu-id="6fae9-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="6fae9-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="6fae9-173">totalHits</span></span> | <span data-ttu-id="6fae9-174">整数</span><span class="sxs-lookup"><span data-stu-id="6fae9-174">integer</span></span>          | <span data-ttu-id="6fae9-175">是</span><span class="sxs-lookup"><span data-stu-id="6fae9-175">yes</span></span>      | <span data-ttu-id="6fae9-176">匹配项，而不考虑总数`skip`和 `take`</span><span class="sxs-lookup"><span data-stu-id="6fae9-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="6fae9-177">数据</span><span class="sxs-lookup"><span data-stu-id="6fae9-177">data</span></span>      | <span data-ttu-id="6fae9-178">字符串数组</span><span class="sxs-lookup"><span data-stu-id="6fae9-178">array of strings</span></span> | <span data-ttu-id="6fae9-179">是</span><span class="sxs-lookup"><span data-stu-id="6fae9-179">yes</span></span>      | <span data-ttu-id="6fae9-180">包 Id 匹配的请求</span><span class="sxs-lookup"><span data-stu-id="6fae9-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="6fae9-181">示例请求</span><span class="sxs-lookup"><span data-stu-id="6fae9-181">Sample request</span></span>

<span data-ttu-id="6fae9-182">获取 https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="6fae9-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="6fae9-183">示例响应</span><span class="sxs-lookup"><span data-stu-id="6fae9-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="6fae9-184">枚举的包版本</span><span class="sxs-lookup"><span data-stu-id="6fae9-184">Enumerate package versions</span></span>

<span data-ttu-id="6fae9-185">客户端的包 ID 发现后使用以前的 API，可以使用记忆式键入功能 API 枚举的包版本的提供的包 id。</span><span class="sxs-lookup"><span data-stu-id="6fae9-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="6fae9-186">未列出的包版本不会出现在结果中。</span><span class="sxs-lookup"><span data-stu-id="6fae9-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="6fae9-187">请求参数</span><span class="sxs-lookup"><span data-stu-id="6fae9-187">Request parameters</span></span>

<span data-ttu-id="6fae9-188">name</span><span class="sxs-lookup"><span data-stu-id="6fae9-188">Name</span></span>        | <span data-ttu-id="6fae9-189">内</span><span class="sxs-lookup"><span data-stu-id="6fae9-189">In</span></span>     | <span data-ttu-id="6fae9-190">类型</span><span class="sxs-lookup"><span data-stu-id="6fae9-190">Type</span></span>    | <span data-ttu-id="6fae9-191">必需</span><span class="sxs-lookup"><span data-stu-id="6fae9-191">Required</span></span> | <span data-ttu-id="6fae9-192">说明</span><span class="sxs-lookup"><span data-stu-id="6fae9-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="6fae9-193">id</span><span class="sxs-lookup"><span data-stu-id="6fae9-193">id</span></span>          | <span data-ttu-id="6fae9-194">URL</span><span class="sxs-lookup"><span data-stu-id="6fae9-194">URL</span></span>    | <span data-ttu-id="6fae9-195">字符串</span><span class="sxs-lookup"><span data-stu-id="6fae9-195">string</span></span>  | <span data-ttu-id="6fae9-196">是</span><span class="sxs-lookup"><span data-stu-id="6fae9-196">yes</span></span>      | <span data-ttu-id="6fae9-197">要提取的版本的程序包 ID</span><span class="sxs-lookup"><span data-stu-id="6fae9-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="6fae9-198">预发行版</span><span class="sxs-lookup"><span data-stu-id="6fae9-198">prerelease</span></span>  | <span data-ttu-id="6fae9-199">URL</span><span class="sxs-lookup"><span data-stu-id="6fae9-199">URL</span></span>    | <span data-ttu-id="6fae9-200">boolean</span><span class="sxs-lookup"><span data-stu-id="6fae9-200">boolean</span></span> | <span data-ttu-id="6fae9-201">否</span><span class="sxs-lookup"><span data-stu-id="6fae9-201">no</span></span>       | <span data-ttu-id="6fae9-202">`true` 或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="6fae9-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="6fae9-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="6fae9-203">semVerLevel</span></span> | <span data-ttu-id="6fae9-204">URL</span><span class="sxs-lookup"><span data-stu-id="6fae9-204">URL</span></span>    | <span data-ttu-id="6fae9-205">字符串</span><span class="sxs-lookup"><span data-stu-id="6fae9-205">string</span></span>  | <span data-ttu-id="6fae9-206">否</span><span class="sxs-lookup"><span data-stu-id="6fae9-206">no</span></span>       | <span data-ttu-id="6fae9-207">SemVer 2.0.0 版本字符串</span><span class="sxs-lookup"><span data-stu-id="6fae9-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="6fae9-208">如果`prerelease`未提供排除预发行包。</span><span class="sxs-lookup"><span data-stu-id="6fae9-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="6fae9-209">`semVerLevel`查询参数用来参加 SemVer 2.0.0 包。</span><span class="sxs-lookup"><span data-stu-id="6fae9-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="6fae9-210">如果排除此查询参数，将返回仅 SemVer 1.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="6fae9-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="6fae9-211">如果`semVerLevel=2.0.0`提供，将返回 SemVer 1.0.0 和 SemVer 2.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="6fae9-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="6fae9-212">请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="6fae9-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="6fae9-213">响应</span><span class="sxs-lookup"><span data-stu-id="6fae9-213">Response</span></span>

<span data-ttu-id="6fae9-214">响应是 JSON 文档，其中包含按给定的查询参数进行筛选提供的包 ID 的所有包版本。</span><span class="sxs-lookup"><span data-stu-id="6fae9-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="6fae9-215">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="6fae9-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="6fae9-216">name</span><span class="sxs-lookup"><span data-stu-id="6fae9-216">Name</span></span>      | <span data-ttu-id="6fae9-217">类型</span><span class="sxs-lookup"><span data-stu-id="6fae9-217">Type</span></span>             | <span data-ttu-id="6fae9-218">必需</span><span class="sxs-lookup"><span data-stu-id="6fae9-218">Required</span></span> | <span data-ttu-id="6fae9-219">说明</span><span class="sxs-lookup"><span data-stu-id="6fae9-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="6fae9-220">数据</span><span class="sxs-lookup"><span data-stu-id="6fae9-220">data</span></span>      | <span data-ttu-id="6fae9-221">字符串数组</span><span class="sxs-lookup"><span data-stu-id="6fae9-221">array of strings</span></span> | <span data-ttu-id="6fae9-222">是</span><span class="sxs-lookup"><span data-stu-id="6fae9-222">yes</span></span>      | <span data-ttu-id="6fae9-223">由请求匹配的包版本</span><span class="sxs-lookup"><span data-stu-id="6fae9-223">The package versions matched by the request</span></span>

<span data-ttu-id="6fae9-224">中的包版本`data`数组可能包含 SemVer 2.0.0 生成元数据 (例如`1.0.0+metadata`) 如果`semVerLevel=2.0.0`查询字符串中提供。</span><span class="sxs-lookup"><span data-stu-id="6fae9-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="6fae9-225">示例请求</span><span class="sxs-lookup"><span data-stu-id="6fae9-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="6fae9-226">示例响应</span><span class="sxs-lookup"><span data-stu-id="6fae9-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
