---
title: 自动完成, NuGet API
description: 搜索自动完成服务支持对包 Id 和版本进行交互式发现。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488295"
---
# <a name="autocomplete"></a><span data-ttu-id="538c7-103">自动完成</span><span class="sxs-lookup"><span data-stu-id="538c7-103">Autocomplete</span></span>

<span data-ttu-id="538c7-104">可以使用 V3 API 构建包 ID 和版本自动完成体验。</span><span class="sxs-lookup"><span data-stu-id="538c7-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="538c7-105">用于使自动完成查询的资源是在`SearchAutocompleteService` [服务索引](service-index.md)中找到的资源。</span><span class="sxs-lookup"><span data-stu-id="538c7-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="538c7-106">版本管理</span><span class="sxs-lookup"><span data-stu-id="538c7-106">Versioning</span></span>

<span data-ttu-id="538c7-107">使用以下`@type`值:</span><span class="sxs-lookup"><span data-stu-id="538c7-107">The following `@type` values are used:</span></span>

<span data-ttu-id="538c7-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="538c7-108">@type value</span></span>                          | <span data-ttu-id="538c7-109">说明</span><span class="sxs-lookup"><span data-stu-id="538c7-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="538c7-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="538c7-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="538c7-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="538c7-111">The initial release</span></span>
<span data-ttu-id="538c7-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="538c7-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="538c7-113">别名`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="538c7-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="538c7-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="538c7-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="538c7-115">别名`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="538c7-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="538c7-116">基 URL</span><span class="sxs-lookup"><span data-stu-id="538c7-116">Base URL</span></span>

<span data-ttu-id="538c7-117">以下 api 的基 URL 是与上述某个资源`@id` `@type`值关联的属性的值。</span><span class="sxs-lookup"><span data-stu-id="538c7-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="538c7-118">在下面的文档中, 将使用占位符`{@id}`基 URL。</span><span class="sxs-lookup"><span data-stu-id="538c7-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="538c7-119">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="538c7-119">HTTP Methods</span></span>

<span data-ttu-id="538c7-120">注册资源中找到的所有 url 都支持 HTTP 方法`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="538c7-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="538c7-121">搜索包 Id</span><span class="sxs-lookup"><span data-stu-id="538c7-121">Search for package IDs</span></span>

<span data-ttu-id="538c7-122">第一个自动完成 API 支持搜索包 ID 字符串的一部分。</span><span class="sxs-lookup"><span data-stu-id="538c7-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="538c7-123">如果要在与 NuGet 包源集成的用户界面中提供包 typeahead 功能, 这非常有用。</span><span class="sxs-lookup"><span data-stu-id="538c7-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="538c7-124">只有未列出的版本的包将不会出现在结果中。</span><span class="sxs-lookup"><span data-stu-id="538c7-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="538c7-125">请求参数</span><span class="sxs-lookup"><span data-stu-id="538c7-125">Request parameters</span></span>

<span data-ttu-id="538c7-126">name</span><span class="sxs-lookup"><span data-stu-id="538c7-126">Name</span></span>        | <span data-ttu-id="538c7-127">内</span><span class="sxs-lookup"><span data-stu-id="538c7-127">In</span></span>     | <span data-ttu-id="538c7-128">类型</span><span class="sxs-lookup"><span data-stu-id="538c7-128">Type</span></span>    | <span data-ttu-id="538c7-129">必需</span><span class="sxs-lookup"><span data-stu-id="538c7-129">Required</span></span> | <span data-ttu-id="538c7-130">说明</span><span class="sxs-lookup"><span data-stu-id="538c7-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="538c7-131">q</span><span class="sxs-lookup"><span data-stu-id="538c7-131">q</span></span>           | <span data-ttu-id="538c7-132">URL</span><span class="sxs-lookup"><span data-stu-id="538c7-132">URL</span></span>    | <span data-ttu-id="538c7-133">string</span><span class="sxs-lookup"><span data-stu-id="538c7-133">string</span></span>  | <span data-ttu-id="538c7-134">否</span><span class="sxs-lookup"><span data-stu-id="538c7-134">no</span></span>       | <span data-ttu-id="538c7-135">要与包 Id 进行比较的字符串</span><span class="sxs-lookup"><span data-stu-id="538c7-135">The string to compare against package IDs</span></span>
<span data-ttu-id="538c7-136">skip</span><span class="sxs-lookup"><span data-stu-id="538c7-136">skip</span></span>        | <span data-ttu-id="538c7-137">URL</span><span class="sxs-lookup"><span data-stu-id="538c7-137">URL</span></span>    | <span data-ttu-id="538c7-138">integer</span><span class="sxs-lookup"><span data-stu-id="538c7-138">integer</span></span> | <span data-ttu-id="538c7-139">否</span><span class="sxs-lookup"><span data-stu-id="538c7-139">no</span></span>       | <span data-ttu-id="538c7-140">要跳过的结果数, 用于分页</span><span class="sxs-lookup"><span data-stu-id="538c7-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="538c7-141">长</span><span class="sxs-lookup"><span data-stu-id="538c7-141">take</span></span>        | <span data-ttu-id="538c7-142">URL</span><span class="sxs-lookup"><span data-stu-id="538c7-142">URL</span></span>    | <span data-ttu-id="538c7-143">integer</span><span class="sxs-lookup"><span data-stu-id="538c7-143">integer</span></span> | <span data-ttu-id="538c7-144">否</span><span class="sxs-lookup"><span data-stu-id="538c7-144">no</span></span>       | <span data-ttu-id="538c7-145">要返回的结果数, 用于分页</span><span class="sxs-lookup"><span data-stu-id="538c7-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="538c7-146">早期</span><span class="sxs-lookup"><span data-stu-id="538c7-146">prerelease</span></span>  | <span data-ttu-id="538c7-147">URL</span><span class="sxs-lookup"><span data-stu-id="538c7-147">URL</span></span>    | <span data-ttu-id="538c7-148">boolean</span><span class="sxs-lookup"><span data-stu-id="538c7-148">boolean</span></span> | <span data-ttu-id="538c7-149">否</span><span class="sxs-lookup"><span data-stu-id="538c7-149">no</span></span>       | <span data-ttu-id="538c7-150">`true`或`false`确定是否包括[预发布包](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="538c7-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="538c7-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="538c7-151">semVerLevel</span></span> | <span data-ttu-id="538c7-152">URL</span><span class="sxs-lookup"><span data-stu-id="538c7-152">URL</span></span>    | <span data-ttu-id="538c7-153">string</span><span class="sxs-lookup"><span data-stu-id="538c7-153">string</span></span>  | <span data-ttu-id="538c7-154">否</span><span class="sxs-lookup"><span data-stu-id="538c7-154">no</span></span>       | <span data-ttu-id="538c7-155">SemVer 1.0.0 版本字符串</span><span class="sxs-lookup"><span data-stu-id="538c7-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="538c7-156">自动完成查询`q`按服务器实现所定义的方式进行分析。</span><span class="sxs-lookup"><span data-stu-id="538c7-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="538c7-157">nuget.org 支持查询包 ID 令牌的前缀, 该前缀是由拆分以大小写字符和符号字符为原始而生成的 ID 的组成部分。</span><span class="sxs-lookup"><span data-stu-id="538c7-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="538c7-158">`skip`参数默认为0。</span><span class="sxs-lookup"><span data-stu-id="538c7-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="538c7-159">`take`参数应为大于零的整数。</span><span class="sxs-lookup"><span data-stu-id="538c7-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="538c7-160">服务器实现可能会施加最大值。</span><span class="sxs-lookup"><span data-stu-id="538c7-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="538c7-161">如果`prerelease`未提供, 则将排除预发布包。</span><span class="sxs-lookup"><span data-stu-id="538c7-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="538c7-162">Query 参数用于选择[SemVer 2.0.0 包。](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages) `semVerLevel`</span><span class="sxs-lookup"><span data-stu-id="538c7-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="538c7-163">如果排除此查询参数, 则将仅返回带有 SemVer 1.0.0 兼容版本的包 Id (带有[标准的 NuGet 版本控制](../concepts/package-versioning.md)注意事项, 如具有4个整数部分的版本字符串)。</span><span class="sxs-lookup"><span data-stu-id="538c7-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="538c7-164">如果`semVerLevel=2.0.0`提供了, 则将返回 SemVer 1.0.0 和 SemVer 2.0.0 兼容包。</span><span class="sxs-lookup"><span data-stu-id="538c7-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="538c7-165">有关详细信息, 请参阅[SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。</span><span class="sxs-lookup"><span data-stu-id="538c7-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="538c7-166">响应</span><span class="sxs-lookup"><span data-stu-id="538c7-166">Response</span></span>

<span data-ttu-id="538c7-167">响应是最多`take`包含自动完成结果的 JSON 文档。</span><span class="sxs-lookup"><span data-stu-id="538c7-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="538c7-168">根 JSON 对象具有以下属性:</span><span class="sxs-lookup"><span data-stu-id="538c7-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="538c7-169">name</span><span class="sxs-lookup"><span data-stu-id="538c7-169">Name</span></span>      | <span data-ttu-id="538c7-170">类型</span><span class="sxs-lookup"><span data-stu-id="538c7-170">Type</span></span>             | <span data-ttu-id="538c7-171">必填</span><span class="sxs-lookup"><span data-stu-id="538c7-171">Required</span></span> | <span data-ttu-id="538c7-172">说明</span><span class="sxs-lookup"><span data-stu-id="538c7-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="538c7-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="538c7-173">totalHits</span></span> | <span data-ttu-id="538c7-174">integer</span><span class="sxs-lookup"><span data-stu-id="538c7-174">integer</span></span>          | <span data-ttu-id="538c7-175">是</span><span class="sxs-lookup"><span data-stu-id="538c7-175">yes</span></span>      | <span data-ttu-id="538c7-176">匹配项的总数, `skip`忽略和`take`</span><span class="sxs-lookup"><span data-stu-id="538c7-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="538c7-177">数据</span><span class="sxs-lookup"><span data-stu-id="538c7-177">data</span></span>      | <span data-ttu-id="538c7-178">字符串数组</span><span class="sxs-lookup"><span data-stu-id="538c7-178">array of strings</span></span> | <span data-ttu-id="538c7-179">是</span><span class="sxs-lookup"><span data-stu-id="538c7-179">yes</span></span>      | <span data-ttu-id="538c7-180">请求匹配的包 Id</span><span class="sxs-lookup"><span data-stu-id="538c7-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="538c7-181">示例请求</span><span class="sxs-lookup"><span data-stu-id="538c7-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="538c7-182">示例响应</span><span class="sxs-lookup"><span data-stu-id="538c7-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="538c7-183">枚举包版本</span><span class="sxs-lookup"><span data-stu-id="538c7-183">Enumerate package versions</span></span>

<span data-ttu-id="538c7-184">使用以前的 API 发现包 ID 后, 客户端可以使用自动完成 API 来枚举提供的包 ID 的包版本。</span><span class="sxs-lookup"><span data-stu-id="538c7-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="538c7-185">未列出的包版本将不会出现在结果中。</span><span class="sxs-lookup"><span data-stu-id="538c7-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="538c7-186">请求参数</span><span class="sxs-lookup"><span data-stu-id="538c7-186">Request parameters</span></span>

<span data-ttu-id="538c7-187">name</span><span class="sxs-lookup"><span data-stu-id="538c7-187">Name</span></span>        | <span data-ttu-id="538c7-188">内</span><span class="sxs-lookup"><span data-stu-id="538c7-188">In</span></span>     | <span data-ttu-id="538c7-189">类型</span><span class="sxs-lookup"><span data-stu-id="538c7-189">Type</span></span>    | <span data-ttu-id="538c7-190">必需</span><span class="sxs-lookup"><span data-stu-id="538c7-190">Required</span></span> | <span data-ttu-id="538c7-191">说明</span><span class="sxs-lookup"><span data-stu-id="538c7-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="538c7-192">id</span><span class="sxs-lookup"><span data-stu-id="538c7-192">id</span></span>          | <span data-ttu-id="538c7-193">URL</span><span class="sxs-lookup"><span data-stu-id="538c7-193">URL</span></span>    | <span data-ttu-id="538c7-194">string</span><span class="sxs-lookup"><span data-stu-id="538c7-194">string</span></span>  | <span data-ttu-id="538c7-195">是</span><span class="sxs-lookup"><span data-stu-id="538c7-195">yes</span></span>      | <span data-ttu-id="538c7-196">要提取其版本的包 ID</span><span class="sxs-lookup"><span data-stu-id="538c7-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="538c7-197">早期</span><span class="sxs-lookup"><span data-stu-id="538c7-197">prerelease</span></span>  | <span data-ttu-id="538c7-198">URL</span><span class="sxs-lookup"><span data-stu-id="538c7-198">URL</span></span>    | <span data-ttu-id="538c7-199">boolean</span><span class="sxs-lookup"><span data-stu-id="538c7-199">boolean</span></span> | <span data-ttu-id="538c7-200">否</span><span class="sxs-lookup"><span data-stu-id="538c7-200">no</span></span>       | <span data-ttu-id="538c7-201">`true`或`false`确定是否包括[预发布包](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="538c7-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="538c7-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="538c7-202">semVerLevel</span></span> | <span data-ttu-id="538c7-203">URL</span><span class="sxs-lookup"><span data-stu-id="538c7-203">URL</span></span>    | <span data-ttu-id="538c7-204">string</span><span class="sxs-lookup"><span data-stu-id="538c7-204">string</span></span>  | <span data-ttu-id="538c7-205">否</span><span class="sxs-lookup"><span data-stu-id="538c7-205">no</span></span>       | <span data-ttu-id="538c7-206">SemVer 2.0.0 版本字符串</span><span class="sxs-lookup"><span data-stu-id="538c7-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="538c7-207">如果`prerelease`未提供, 则将排除预发布包。</span><span class="sxs-lookup"><span data-stu-id="538c7-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="538c7-208">`semVerLevel` Query 参数用于选择 SemVer 2.0.0 包。</span><span class="sxs-lookup"><span data-stu-id="538c7-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="538c7-209">如果排除此查询参数, 则仅返回 SemVer 1.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="538c7-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="538c7-210">如果`semVerLevel=2.0.0`提供了, 则将返回 SemVer 1.0.0 和 SemVer 2.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="538c7-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="538c7-211">有关详细信息, 请参阅[SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。</span><span class="sxs-lookup"><span data-stu-id="538c7-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="538c7-212">响应</span><span class="sxs-lookup"><span data-stu-id="538c7-212">Response</span></span>

<span data-ttu-id="538c7-213">响应是一个 JSON 文档, 其中包含所提供的包 ID 的所有包版本, 并按给定的查询参数进行筛选。</span><span class="sxs-lookup"><span data-stu-id="538c7-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="538c7-214">根 JSON 对象具有以下属性:</span><span class="sxs-lookup"><span data-stu-id="538c7-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="538c7-215">name</span><span class="sxs-lookup"><span data-stu-id="538c7-215">Name</span></span>      | <span data-ttu-id="538c7-216">类型</span><span class="sxs-lookup"><span data-stu-id="538c7-216">Type</span></span>             | <span data-ttu-id="538c7-217">必需</span><span class="sxs-lookup"><span data-stu-id="538c7-217">Required</span></span> | <span data-ttu-id="538c7-218">说明</span><span class="sxs-lookup"><span data-stu-id="538c7-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="538c7-219">数据</span><span class="sxs-lookup"><span data-stu-id="538c7-219">data</span></span>      | <span data-ttu-id="538c7-220">字符串数组</span><span class="sxs-lookup"><span data-stu-id="538c7-220">array of strings</span></span> | <span data-ttu-id="538c7-221">是</span><span class="sxs-lookup"><span data-stu-id="538c7-221">yes</span></span>      | <span data-ttu-id="538c7-222">与请求匹配的包版本</span><span class="sxs-lookup"><span data-stu-id="538c7-222">The package versions matched by the request</span></span>

<span data-ttu-id="538c7-223">如果`1.0.0+metadata` `data` 查询字符串中提供了,则数组中的包版本可能包含SemVer2.0.0生成元数据(例如)。`semVerLevel=2.0.0`</span><span class="sxs-lookup"><span data-stu-id="538c7-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="538c7-224">示例请求</span><span class="sxs-lookup"><span data-stu-id="538c7-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="538c7-225">示例响应</span><span class="sxs-lookup"><span data-stu-id="538c7-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
