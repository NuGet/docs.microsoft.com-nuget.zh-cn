---
title: 记忆式键入功能，NuGet API
description: 该搜索自动完成服务支持交互式搜索的包 Id 和版本。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911044"
---
# <a name="autocomplete"></a><span data-ttu-id="2a7a1-103">自动完成</span><span class="sxs-lookup"><span data-stu-id="2a7a1-103">Autocomplete</span></span>

<span data-ttu-id="2a7a1-104">它是可以构建使用 V3 API 的包 ID 和版本自动完成体验。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="2a7a1-105">在进行自动完成查询使用的资源是`SearchAutocompleteService`资源中找到[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="2a7a1-106">版本管理</span><span class="sxs-lookup"><span data-stu-id="2a7a1-106">Versioning</span></span>

<span data-ttu-id="2a7a1-107">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="2a7a1-107">The following `@type` values are used:</span></span>

<span data-ttu-id="2a7a1-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="2a7a1-108">@type value</span></span>                          | <span data-ttu-id="2a7a1-109">说明</span><span class="sxs-lookup"><span data-stu-id="2a7a1-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="2a7a1-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="2a7a1-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="2a7a1-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="2a7a1-111">The initial release</span></span>
<span data-ttu-id="2a7a1-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="2a7a1-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="2a7a1-113">别名</span><span class="sxs-lookup"><span data-stu-id="2a7a1-113">Alias of</span></span> `SearchAutocompleteService`
<span data-ttu-id="2a7a1-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="2a7a1-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="2a7a1-115">别名</span><span class="sxs-lookup"><span data-stu-id="2a7a1-115">Alias of</span></span> `SearchAutocompleteService`

## <a name="base-url"></a><span data-ttu-id="2a7a1-116">基 URL</span><span class="sxs-lookup"><span data-stu-id="2a7a1-116">Base URL</span></span>

<span data-ttu-id="2a7a1-117">以下 Api 的基 URL 是的值`@id`属性与前面提到的资源之一相关联`@type`值。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="2a7a1-118">在以下文档中，占位符基 URL`{@id}`将使用。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2a7a1-119">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="2a7a1-119">HTTP Methods</span></span>

<span data-ttu-id="2a7a1-120">中的注册资源支持的 HTTP 方法找到的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="2a7a1-121">搜索包 Id</span><span class="sxs-lookup"><span data-stu-id="2a7a1-121">Search for package IDs</span></span>

<span data-ttu-id="2a7a1-122">第一个自动完成 API 支持搜索包 ID 字符串的一部分。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="2a7a1-123">当您想要提供用户界面集成在一起的 NuGet 包源中的包 typeahead 功能时，这非常有利。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="2a7a1-124">仅未列出的版本的包不会出现在结果中。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="2a7a1-125">请求参数</span><span class="sxs-lookup"><span data-stu-id="2a7a1-125">Request parameters</span></span>

<span data-ttu-id="2a7a1-126">名称</span><span class="sxs-lookup"><span data-stu-id="2a7a1-126">Name</span></span>        | <span data-ttu-id="2a7a1-127">内</span><span class="sxs-lookup"><span data-stu-id="2a7a1-127">In</span></span>     | <span data-ttu-id="2a7a1-128">类型</span><span class="sxs-lookup"><span data-stu-id="2a7a1-128">Type</span></span>    | <span data-ttu-id="2a7a1-129">必需</span><span class="sxs-lookup"><span data-stu-id="2a7a1-129">Required</span></span> | <span data-ttu-id="2a7a1-130">说明</span><span class="sxs-lookup"><span data-stu-id="2a7a1-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="2a7a1-131">q</span><span class="sxs-lookup"><span data-stu-id="2a7a1-131">q</span></span>           | <span data-ttu-id="2a7a1-132">URL</span><span class="sxs-lookup"><span data-stu-id="2a7a1-132">URL</span></span>    | <span data-ttu-id="2a7a1-133">string</span><span class="sxs-lookup"><span data-stu-id="2a7a1-133">string</span></span>  | <span data-ttu-id="2a7a1-134">否</span><span class="sxs-lookup"><span data-stu-id="2a7a1-134">no</span></span>       | <span data-ttu-id="2a7a1-135">要与包 Id 进行比较的字符串</span><span class="sxs-lookup"><span data-stu-id="2a7a1-135">The string to compare against package IDs</span></span>
<span data-ttu-id="2a7a1-136">skip</span><span class="sxs-lookup"><span data-stu-id="2a7a1-136">skip</span></span>        | <span data-ttu-id="2a7a1-137">URL</span><span class="sxs-lookup"><span data-stu-id="2a7a1-137">URL</span></span>    | <span data-ttu-id="2a7a1-138">整数</span><span class="sxs-lookup"><span data-stu-id="2a7a1-138">integer</span></span> | <span data-ttu-id="2a7a1-139">否</span><span class="sxs-lookup"><span data-stu-id="2a7a1-139">no</span></span>       | <span data-ttu-id="2a7a1-140">要分页的跳过的结果数</span><span class="sxs-lookup"><span data-stu-id="2a7a1-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="2a7a1-141">Take</span><span class="sxs-lookup"><span data-stu-id="2a7a1-141">take</span></span>        | <span data-ttu-id="2a7a1-142">URL</span><span class="sxs-lookup"><span data-stu-id="2a7a1-142">URL</span></span>    | <span data-ttu-id="2a7a1-143">整数</span><span class="sxs-lookup"><span data-stu-id="2a7a1-143">integer</span></span> | <span data-ttu-id="2a7a1-144">否</span><span class="sxs-lookup"><span data-stu-id="2a7a1-144">no</span></span>       | <span data-ttu-id="2a7a1-145">要为分页返回的结果数</span><span class="sxs-lookup"><span data-stu-id="2a7a1-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="2a7a1-146">预发行版</span><span class="sxs-lookup"><span data-stu-id="2a7a1-146">prerelease</span></span>  | <span data-ttu-id="2a7a1-147">URL</span><span class="sxs-lookup"><span data-stu-id="2a7a1-147">URL</span></span>    | <span data-ttu-id="2a7a1-148">boolean</span><span class="sxs-lookup"><span data-stu-id="2a7a1-148">boolean</span></span> | <span data-ttu-id="2a7a1-149">否</span><span class="sxs-lookup"><span data-stu-id="2a7a1-149">no</span></span>       | `true` <span data-ttu-id="2a7a1-150">或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="2a7a1-150">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="2a7a1-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="2a7a1-151">semVerLevel</span></span> | <span data-ttu-id="2a7a1-152">URL</span><span class="sxs-lookup"><span data-stu-id="2a7a1-152">URL</span></span>    | <span data-ttu-id="2a7a1-153">string</span><span class="sxs-lookup"><span data-stu-id="2a7a1-153">string</span></span>  | <span data-ttu-id="2a7a1-154">否</span><span class="sxs-lookup"><span data-stu-id="2a7a1-154">no</span></span>       | <span data-ttu-id="2a7a1-155">SemVer 1.0.0 版本字符串</span><span class="sxs-lookup"><span data-stu-id="2a7a1-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="2a7a1-156">记忆式键入功能查询`q`分析由服务器实现定义的方式。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="2a7a1-157">nuget.org 支持查询是由拆分生成的 ID 的片段的包 ID 令牌的前缀为原始由驼峰式大小写和符号字符。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="2a7a1-158">`skip`参数默认值为 0。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="2a7a1-159">`take`参数应为大于零的整数。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="2a7a1-160">服务器实现可能会施加最大值。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="2a7a1-161">如果`prerelease`未提供排除预发行包。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="2a7a1-162">`semVerLevel`查询参数用来选择中加入[SemVer 2.0.0 包](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="2a7a1-163">如果排除此查询参数，将返回与 SemVer 1.0.0 兼容版本的唯一程序包 Id (与[standard 的 NuGet 版本控制](../reference/package-versioning.md)需要注意的问题，例如使用 4 个整数部分的版本字符串)。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="2a7a1-164">如果`semVerLevel=2.0.0`提供，将返回 SemVer 1.0.0 和 SemVer 2.0.0 兼容包。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="2a7a1-165">请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="2a7a1-166">响应</span><span class="sxs-lookup"><span data-stu-id="2a7a1-166">Response</span></span>

<span data-ttu-id="2a7a1-167">响应是 JSON 文档，其中最多包含`take`记忆式键入功能结果。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="2a7a1-168">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="2a7a1-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="2a7a1-169">名称</span><span class="sxs-lookup"><span data-stu-id="2a7a1-169">Name</span></span>      | <span data-ttu-id="2a7a1-170">类型</span><span class="sxs-lookup"><span data-stu-id="2a7a1-170">Type</span></span>             | <span data-ttu-id="2a7a1-171">必需</span><span class="sxs-lookup"><span data-stu-id="2a7a1-171">Required</span></span> | <span data-ttu-id="2a7a1-172">说明</span><span class="sxs-lookup"><span data-stu-id="2a7a1-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="2a7a1-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="2a7a1-173">totalHits</span></span> | <span data-ttu-id="2a7a1-174">整数</span><span class="sxs-lookup"><span data-stu-id="2a7a1-174">integer</span></span>          | <span data-ttu-id="2a7a1-175">是</span><span class="sxs-lookup"><span data-stu-id="2a7a1-175">yes</span></span>      | <span data-ttu-id="2a7a1-176">匹配项，而不考虑总数`skip`和</span><span class="sxs-lookup"><span data-stu-id="2a7a1-176">The total number of matches, disregarding `skip` and</span></span> `take`
<span data-ttu-id="2a7a1-177">数据</span><span class="sxs-lookup"><span data-stu-id="2a7a1-177">data</span></span>      | <span data-ttu-id="2a7a1-178">字符串数组</span><span class="sxs-lookup"><span data-stu-id="2a7a1-178">array of strings</span></span> | <span data-ttu-id="2a7a1-179">是</span><span class="sxs-lookup"><span data-stu-id="2a7a1-179">yes</span></span>      | <span data-ttu-id="2a7a1-180">包 Id 匹配的请求</span><span class="sxs-lookup"><span data-stu-id="2a7a1-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="2a7a1-181">示例请求</span><span class="sxs-lookup"><span data-stu-id="2a7a1-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="2a7a1-182">示例响应</span><span class="sxs-lookup"><span data-stu-id="2a7a1-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="2a7a1-183">枚举的包版本</span><span class="sxs-lookup"><span data-stu-id="2a7a1-183">Enumerate package versions</span></span>

<span data-ttu-id="2a7a1-184">客户端的包 ID 发现后使用以前的 API，可以使用记忆式键入功能 API 枚举的包版本的提供的包 id。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="2a7a1-185">未列出的包版本不会出现在结果中。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="2a7a1-186">请求参数</span><span class="sxs-lookup"><span data-stu-id="2a7a1-186">Request parameters</span></span>

<span data-ttu-id="2a7a1-187">名称</span><span class="sxs-lookup"><span data-stu-id="2a7a1-187">Name</span></span>        | <span data-ttu-id="2a7a1-188">内</span><span class="sxs-lookup"><span data-stu-id="2a7a1-188">In</span></span>     | <span data-ttu-id="2a7a1-189">类型</span><span class="sxs-lookup"><span data-stu-id="2a7a1-189">Type</span></span>    | <span data-ttu-id="2a7a1-190">必需</span><span class="sxs-lookup"><span data-stu-id="2a7a1-190">Required</span></span> | <span data-ttu-id="2a7a1-191">说明</span><span class="sxs-lookup"><span data-stu-id="2a7a1-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="2a7a1-192">id</span><span class="sxs-lookup"><span data-stu-id="2a7a1-192">id</span></span>          | <span data-ttu-id="2a7a1-193">URL</span><span class="sxs-lookup"><span data-stu-id="2a7a1-193">URL</span></span>    | <span data-ttu-id="2a7a1-194">string</span><span class="sxs-lookup"><span data-stu-id="2a7a1-194">string</span></span>  | <span data-ttu-id="2a7a1-195">是</span><span class="sxs-lookup"><span data-stu-id="2a7a1-195">yes</span></span>      | <span data-ttu-id="2a7a1-196">要提取的版本的程序包 ID</span><span class="sxs-lookup"><span data-stu-id="2a7a1-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="2a7a1-197">预发行版</span><span class="sxs-lookup"><span data-stu-id="2a7a1-197">prerelease</span></span>  | <span data-ttu-id="2a7a1-198">URL</span><span class="sxs-lookup"><span data-stu-id="2a7a1-198">URL</span></span>    | <span data-ttu-id="2a7a1-199">boolean</span><span class="sxs-lookup"><span data-stu-id="2a7a1-199">boolean</span></span> | <span data-ttu-id="2a7a1-200">否</span><span class="sxs-lookup"><span data-stu-id="2a7a1-200">no</span></span>       | `true` <span data-ttu-id="2a7a1-201">或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="2a7a1-201">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="2a7a1-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="2a7a1-202">semVerLevel</span></span> | <span data-ttu-id="2a7a1-203">URL</span><span class="sxs-lookup"><span data-stu-id="2a7a1-203">URL</span></span>    | <span data-ttu-id="2a7a1-204">string</span><span class="sxs-lookup"><span data-stu-id="2a7a1-204">string</span></span>  | <span data-ttu-id="2a7a1-205">否</span><span class="sxs-lookup"><span data-stu-id="2a7a1-205">no</span></span>       | <span data-ttu-id="2a7a1-206">SemVer 2.0.0 版本字符串</span><span class="sxs-lookup"><span data-stu-id="2a7a1-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="2a7a1-207">如果`prerelease`未提供排除预发行包。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="2a7a1-208">`semVerLevel`查询参数用来参加 SemVer 2.0.0 包。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="2a7a1-209">如果排除此查询参数，将返回仅 SemVer 1.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="2a7a1-210">如果`semVerLevel=2.0.0`提供，将返回 SemVer 1.0.0 和 SemVer 2.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="2a7a1-211">请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="2a7a1-212">响应</span><span class="sxs-lookup"><span data-stu-id="2a7a1-212">Response</span></span>

<span data-ttu-id="2a7a1-213">响应是 JSON 文档，其中包含按给定的查询参数进行筛选提供的包 ID 的所有包版本。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="2a7a1-214">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="2a7a1-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="2a7a1-215">名称</span><span class="sxs-lookup"><span data-stu-id="2a7a1-215">Name</span></span>      | <span data-ttu-id="2a7a1-216">类型</span><span class="sxs-lookup"><span data-stu-id="2a7a1-216">Type</span></span>             | <span data-ttu-id="2a7a1-217">必需</span><span class="sxs-lookup"><span data-stu-id="2a7a1-217">Required</span></span> | <span data-ttu-id="2a7a1-218">说明</span><span class="sxs-lookup"><span data-stu-id="2a7a1-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="2a7a1-219">数据</span><span class="sxs-lookup"><span data-stu-id="2a7a1-219">data</span></span>      | <span data-ttu-id="2a7a1-220">字符串数组</span><span class="sxs-lookup"><span data-stu-id="2a7a1-220">array of strings</span></span> | <span data-ttu-id="2a7a1-221">是</span><span class="sxs-lookup"><span data-stu-id="2a7a1-221">yes</span></span>      | <span data-ttu-id="2a7a1-222">由请求匹配的包版本</span><span class="sxs-lookup"><span data-stu-id="2a7a1-222">The package versions matched by the request</span></span>

<span data-ttu-id="2a7a1-223">中的包版本`data`数组可能包含 SemVer 2.0.0 生成元数据 (例如`1.0.0+metadata`) 如果`semVerLevel=2.0.0`查询字符串中提供。</span><span class="sxs-lookup"><span data-stu-id="2a7a1-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="2a7a1-224">示例请求</span><span class="sxs-lookup"><span data-stu-id="2a7a1-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="2a7a1-225">示例响应</span><span class="sxs-lookup"><span data-stu-id="2a7a1-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
