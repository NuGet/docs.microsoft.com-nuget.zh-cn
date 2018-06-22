---
title: 记忆式键入功能，NuGet API
description: 搜索记忆式键入功能服务支持交互式发现的包 Id 和版本。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822131"
---
# <a name="autocomplete"></a><span data-ttu-id="4e861-103">自动完成</span><span class="sxs-lookup"><span data-stu-id="4e861-103">Autocomplete</span></span>

<span data-ttu-id="4e861-104">它是可以生成使用 V3 API 的包 ID 和版本记忆式键入功能体验。</span><span class="sxs-lookup"><span data-stu-id="4e861-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="4e861-105">用于进行自动完成查询的资源是`SearchAutocompleteService`资源位于[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="4e861-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="4e861-106">版本管理</span><span class="sxs-lookup"><span data-stu-id="4e861-106">Versioning</span></span>

<span data-ttu-id="4e861-107">以下`@type`将使用值：</span><span class="sxs-lookup"><span data-stu-id="4e861-107">The following `@type` values are used:</span></span>

<span data-ttu-id="4e861-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="4e861-108">@type value</span></span>                          | <span data-ttu-id="4e861-109">说明</span><span class="sxs-lookup"><span data-stu-id="4e861-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="4e861-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="4e861-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="4e861-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="4e861-111">The initial release</span></span>
<span data-ttu-id="4e861-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="4e861-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="4e861-113">别名 `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="4e861-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="4e861-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="4e861-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="4e861-115">别名 `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="4e861-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="4e861-116">基 URL</span><span class="sxs-lookup"><span data-stu-id="4e861-116">Base URL</span></span>

<span data-ttu-id="4e861-117">以下 Api 的基 URL 是值`@id`与前面提到的资源之一相关联的属性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="4e861-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="4e861-118">在以下文档中，将占位符基本 URL`{@id}`将使用。</span><span class="sxs-lookup"><span data-stu-id="4e861-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="4e861-119">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="4e861-119">HTTP Methods</span></span>

<span data-ttu-id="4e861-120">HTTP 方法位于注册资源支持的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="4e861-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="4e861-121">搜索包 Id</span><span class="sxs-lookup"><span data-stu-id="4e861-121">Search for package IDs</span></span>

<span data-ttu-id="4e861-122">第一个自动完成 API 支持搜索包 ID 字符串的一部分。</span><span class="sxs-lookup"><span data-stu-id="4e861-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="4e861-123">当你想要提供用户界面集成在一起的 NuGet 包源中的包 typeahead 功能时，这非常有利。</span><span class="sxs-lookup"><span data-stu-id="4e861-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="4e861-124">仅未列出的版本的包将不会出现在结果中。</span><span class="sxs-lookup"><span data-stu-id="4e861-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="4e861-125">请求参数</span><span class="sxs-lookup"><span data-stu-id="4e861-125">Request parameters</span></span>

<span data-ttu-id="4e861-126">名称</span><span class="sxs-lookup"><span data-stu-id="4e861-126">Name</span></span>        | <span data-ttu-id="4e861-127">内</span><span class="sxs-lookup"><span data-stu-id="4e861-127">In</span></span>     | <span data-ttu-id="4e861-128">类型</span><span class="sxs-lookup"><span data-stu-id="4e861-128">Type</span></span>    | <span data-ttu-id="4e861-129">必需</span><span class="sxs-lookup"><span data-stu-id="4e861-129">Required</span></span> | <span data-ttu-id="4e861-130">说明</span><span class="sxs-lookup"><span data-stu-id="4e861-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="4e861-131">q</span><span class="sxs-lookup"><span data-stu-id="4e861-131">q</span></span>           | <span data-ttu-id="4e861-132">URL</span><span class="sxs-lookup"><span data-stu-id="4e861-132">URL</span></span>    | <span data-ttu-id="4e861-133">字符串</span><span class="sxs-lookup"><span data-stu-id="4e861-133">string</span></span>  | <span data-ttu-id="4e861-134">否</span><span class="sxs-lookup"><span data-stu-id="4e861-134">no</span></span>       | <span data-ttu-id="4e861-135">要针对包 Id 进行比较的字符串</span><span class="sxs-lookup"><span data-stu-id="4e861-135">The string to compare against package IDs</span></span>
<span data-ttu-id="4e861-136">skip</span><span class="sxs-lookup"><span data-stu-id="4e861-136">skip</span></span>        | <span data-ttu-id="4e861-137">URL</span><span class="sxs-lookup"><span data-stu-id="4e861-137">URL</span></span>    | <span data-ttu-id="4e861-138">整数</span><span class="sxs-lookup"><span data-stu-id="4e861-138">integer</span></span> | <span data-ttu-id="4e861-139">否</span><span class="sxs-lookup"><span data-stu-id="4e861-139">no</span></span>       | <span data-ttu-id="4e861-140">要分页的跳过的结果数</span><span class="sxs-lookup"><span data-stu-id="4e861-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="4e861-141">take</span><span class="sxs-lookup"><span data-stu-id="4e861-141">take</span></span>        | <span data-ttu-id="4e861-142">URL</span><span class="sxs-lookup"><span data-stu-id="4e861-142">URL</span></span>    | <span data-ttu-id="4e861-143">整数</span><span class="sxs-lookup"><span data-stu-id="4e861-143">integer</span></span> | <span data-ttu-id="4e861-144">否</span><span class="sxs-lookup"><span data-stu-id="4e861-144">no</span></span>       | <span data-ttu-id="4e861-145">要为分页返回的结果数</span><span class="sxs-lookup"><span data-stu-id="4e861-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="4e861-146">预发行版</span><span class="sxs-lookup"><span data-stu-id="4e861-146">prerelease</span></span>  | <span data-ttu-id="4e861-147">URL</span><span class="sxs-lookup"><span data-stu-id="4e861-147">URL</span></span>    | <span data-ttu-id="4e861-148">boolean</span><span class="sxs-lookup"><span data-stu-id="4e861-148">boolean</span></span> | <span data-ttu-id="4e861-149">否</span><span class="sxs-lookup"><span data-stu-id="4e861-149">no</span></span>       | <span data-ttu-id="4e861-150">`true` 或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="4e861-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="4e861-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="4e861-151">semVerLevel</span></span> | <span data-ttu-id="4e861-152">URL</span><span class="sxs-lookup"><span data-stu-id="4e861-152">URL</span></span>    | <span data-ttu-id="4e861-153">字符串</span><span class="sxs-lookup"><span data-stu-id="4e861-153">string</span></span>  | <span data-ttu-id="4e861-154">否</span><span class="sxs-lookup"><span data-stu-id="4e861-154">no</span></span>       | <span data-ttu-id="4e861-155">SemVer 1.0.0 版本字符串</span><span class="sxs-lookup"><span data-stu-id="4e861-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="4e861-156">自动完成查询`q`分析由服务器实现定义的方式。</span><span class="sxs-lookup"><span data-stu-id="4e861-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="4e861-157">nuget.org 支持查询个前缀的包 ID 令牌，它们是由拆分生成的 ID 的段原始由 camel 大小写和符号字符。</span><span class="sxs-lookup"><span data-stu-id="4e861-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="4e861-158">`skip`参数默认值为 0。</span><span class="sxs-lookup"><span data-stu-id="4e861-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="4e861-159">`take`参数应大于零的整数。</span><span class="sxs-lookup"><span data-stu-id="4e861-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="4e861-160">服务器实现可能会对施加的最大值。</span><span class="sxs-lookup"><span data-stu-id="4e861-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="4e861-161">如果`prerelease`未提供排除预发行包。</span><span class="sxs-lookup"><span data-stu-id="4e861-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="4e861-162">`semVerLevel`查询参数用来选择[SemVer 2.0.0 包](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。</span><span class="sxs-lookup"><span data-stu-id="4e861-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="4e861-163">如果排除此查询参数，将返回与 SemVer 1.0.0 兼容版本的唯一包 Id (与[标准的 NuGet 版本控制](../reference/package-versioning.md)需要注意的问题，如使用 4 的整数部分的版本字符串)。</span><span class="sxs-lookup"><span data-stu-id="4e861-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="4e861-164">如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 兼容包将返回。</span><span class="sxs-lookup"><span data-stu-id="4e861-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="4e861-165">请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="4e861-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="4e861-166">响应</span><span class="sxs-lookup"><span data-stu-id="4e861-166">Response</span></span>

<span data-ttu-id="4e861-167">响应是包含最多的 JSON 文档`take`记忆式键入功能结果。</span><span class="sxs-lookup"><span data-stu-id="4e861-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="4e861-168">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="4e861-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="4e861-169">名称</span><span class="sxs-lookup"><span data-stu-id="4e861-169">Name</span></span>      | <span data-ttu-id="4e861-170">类型</span><span class="sxs-lookup"><span data-stu-id="4e861-170">Type</span></span>             | <span data-ttu-id="4e861-171">必需</span><span class="sxs-lookup"><span data-stu-id="4e861-171">Required</span></span> | <span data-ttu-id="4e861-172">说明</span><span class="sxs-lookup"><span data-stu-id="4e861-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="4e861-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="4e861-173">totalHits</span></span> | <span data-ttu-id="4e861-174">整数</span><span class="sxs-lookup"><span data-stu-id="4e861-174">integer</span></span>          | <span data-ttu-id="4e861-175">是</span><span class="sxs-lookup"><span data-stu-id="4e861-175">yes</span></span>      | <span data-ttu-id="4e861-176">匹配项，而不考虑的总数目`skip`和 `take`</span><span class="sxs-lookup"><span data-stu-id="4e861-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="4e861-177">数据</span><span class="sxs-lookup"><span data-stu-id="4e861-177">data</span></span>      | <span data-ttu-id="4e861-178">字符串数组</span><span class="sxs-lookup"><span data-stu-id="4e861-178">array of strings</span></span> | <span data-ttu-id="4e861-179">是</span><span class="sxs-lookup"><span data-stu-id="4e861-179">yes</span></span>      | <span data-ttu-id="4e861-180">由请求的包 Id 匹配</span><span class="sxs-lookup"><span data-stu-id="4e861-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="4e861-181">示例请求</span><span class="sxs-lookup"><span data-stu-id="4e861-181">Sample request</span></span>

<span data-ttu-id="4e861-182">获取 https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="4e861-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="4e861-183">示例响应</span><span class="sxs-lookup"><span data-stu-id="4e861-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="4e861-184">枚举包版本</span><span class="sxs-lookup"><span data-stu-id="4e861-184">Enumerate package versions</span></span>

<span data-ttu-id="4e861-185">客户端后，发现了包 ID 使用以前的 API，可以使用记忆式键入 API 提供的包 id 枚举包版本</span><span class="sxs-lookup"><span data-stu-id="4e861-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="4e861-186">未列出的包版本将不会出现在结果中。</span><span class="sxs-lookup"><span data-stu-id="4e861-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="4e861-187">请求参数</span><span class="sxs-lookup"><span data-stu-id="4e861-187">Request parameters</span></span>

<span data-ttu-id="4e861-188">名称</span><span class="sxs-lookup"><span data-stu-id="4e861-188">Name</span></span>        | <span data-ttu-id="4e861-189">内</span><span class="sxs-lookup"><span data-stu-id="4e861-189">In</span></span>     | <span data-ttu-id="4e861-190">类型</span><span class="sxs-lookup"><span data-stu-id="4e861-190">Type</span></span>    | <span data-ttu-id="4e861-191">必需</span><span class="sxs-lookup"><span data-stu-id="4e861-191">Required</span></span> | <span data-ttu-id="4e861-192">说明</span><span class="sxs-lookup"><span data-stu-id="4e861-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="4e861-193">id</span><span class="sxs-lookup"><span data-stu-id="4e861-193">id</span></span>          | <span data-ttu-id="4e861-194">URL</span><span class="sxs-lookup"><span data-stu-id="4e861-194">URL</span></span>    | <span data-ttu-id="4e861-195">字符串</span><span class="sxs-lookup"><span data-stu-id="4e861-195">string</span></span>  | <span data-ttu-id="4e861-196">是</span><span class="sxs-lookup"><span data-stu-id="4e861-196">yes</span></span>      | <span data-ttu-id="4e861-197">要提取的版本的包 ID</span><span class="sxs-lookup"><span data-stu-id="4e861-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="4e861-198">预发行版</span><span class="sxs-lookup"><span data-stu-id="4e861-198">prerelease</span></span>  | <span data-ttu-id="4e861-199">URL</span><span class="sxs-lookup"><span data-stu-id="4e861-199">URL</span></span>    | <span data-ttu-id="4e861-200">boolean</span><span class="sxs-lookup"><span data-stu-id="4e861-200">boolean</span></span> | <span data-ttu-id="4e861-201">否</span><span class="sxs-lookup"><span data-stu-id="4e861-201">no</span></span>       | <span data-ttu-id="4e861-202">`true` 或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="4e861-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="4e861-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="4e861-203">semVerLevel</span></span> | <span data-ttu-id="4e861-204">URL</span><span class="sxs-lookup"><span data-stu-id="4e861-204">URL</span></span>    | <span data-ttu-id="4e861-205">字符串</span><span class="sxs-lookup"><span data-stu-id="4e861-205">string</span></span>  | <span data-ttu-id="4e861-206">否</span><span class="sxs-lookup"><span data-stu-id="4e861-206">no</span></span>       | <span data-ttu-id="4e861-207">SemVer 2.0.0 的版本字符串</span><span class="sxs-lookup"><span data-stu-id="4e861-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="4e861-208">如果`prerelease`未提供排除预发行包。</span><span class="sxs-lookup"><span data-stu-id="4e861-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="4e861-209">`semVerLevel`查询参数用于选择加入到 SemVer 2.0.0 包。</span><span class="sxs-lookup"><span data-stu-id="4e861-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="4e861-210">如果排除此查询参数，将返回仅 SemVer 1.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="4e861-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="4e861-211">如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 版本将返回。</span><span class="sxs-lookup"><span data-stu-id="4e861-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="4e861-212">请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="4e861-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="4e861-213">响应</span><span class="sxs-lookup"><span data-stu-id="4e861-213">Response</span></span>

<span data-ttu-id="4e861-214">响应是包含所有包版本的提供的包 ID，筛选由给定的查询参数的 JSON 文档。</span><span class="sxs-lookup"><span data-stu-id="4e861-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="4e861-215">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="4e861-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="4e861-216">名称</span><span class="sxs-lookup"><span data-stu-id="4e861-216">Name</span></span>      | <span data-ttu-id="4e861-217">类型</span><span class="sxs-lookup"><span data-stu-id="4e861-217">Type</span></span>             | <span data-ttu-id="4e861-218">必需</span><span class="sxs-lookup"><span data-stu-id="4e861-218">Required</span></span> | <span data-ttu-id="4e861-219">说明</span><span class="sxs-lookup"><span data-stu-id="4e861-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="4e861-220">数据</span><span class="sxs-lookup"><span data-stu-id="4e861-220">data</span></span>      | <span data-ttu-id="4e861-221">字符串数组</span><span class="sxs-lookup"><span data-stu-id="4e861-221">array of strings</span></span> | <span data-ttu-id="4e861-222">是</span><span class="sxs-lookup"><span data-stu-id="4e861-222">yes</span></span>      | <span data-ttu-id="4e861-223">由请求匹配的程序包版本</span><span class="sxs-lookup"><span data-stu-id="4e861-223">The package versions matched by the request</span></span>

<span data-ttu-id="4e861-224">中的包版本`data`数组可能包含 SemVer 2.0.0 生成元数据 (例如`1.0.0+metadata`) 如果`semVerLevel=2.0.0`查询字符串中提供。</span><span class="sxs-lookup"><span data-stu-id="4e861-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="4e861-225">示例请求</span><span class="sxs-lookup"><span data-stu-id="4e861-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="4e861-226">示例响应</span><span class="sxs-lookup"><span data-stu-id="4e861-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
