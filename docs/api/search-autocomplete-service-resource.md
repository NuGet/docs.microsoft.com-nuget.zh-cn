---
title: 自动完成，NuGet API
description: 搜索自动完成服务支持对包 Id 和版本进行交互式发现。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2893e13ff7b070844a2bdd5722da3aa1f123538d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773957"
---
# <a name="autocomplete"></a><span data-ttu-id="9f493-103">自动完成</span><span class="sxs-lookup"><span data-stu-id="9f493-103">Autocomplete</span></span>

<span data-ttu-id="9f493-104">可以使用 V3 API 构建包 ID 和版本自动完成体验。</span><span class="sxs-lookup"><span data-stu-id="9f493-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="9f493-105">用于使自动完成查询的资源是 `SearchAutocompleteService` 在 [服务索引](service-index.md)中找到的资源。</span><span class="sxs-lookup"><span data-stu-id="9f493-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="9f493-106">版本控制</span><span class="sxs-lookup"><span data-stu-id="9f493-106">Versioning</span></span>

<span data-ttu-id="9f493-107">使用以下 `@type` 值：</span><span class="sxs-lookup"><span data-stu-id="9f493-107">The following `@type` values are used:</span></span>

<span data-ttu-id="9f493-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="9f493-108">@type value</span></span>                          | <span data-ttu-id="9f493-109">说明</span><span class="sxs-lookup"><span data-stu-id="9f493-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="9f493-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="9f493-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="9f493-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="9f493-111">The initial release</span></span>
<span data-ttu-id="9f493-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="9f493-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="9f493-113">别名 `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="9f493-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="9f493-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="9f493-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="9f493-115">别名 `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="9f493-115">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="9f493-116">SearchAutocompleteService/3.5。0</span><span class="sxs-lookup"><span data-stu-id="9f493-116">SearchAutocompleteService/3.5.0</span></span>      | <span data-ttu-id="9f493-117">支持 `packageType` 查询参数</span><span class="sxs-lookup"><span data-stu-id="9f493-117">Includes support for `packageType` query parameter</span></span>

### <a name="searchautocompleteservice350"></a><span data-ttu-id="9f493-118">SearchAutocompleteService/3.5。0</span><span class="sxs-lookup"><span data-stu-id="9f493-118">SearchAutocompleteService/3.5.0</span></span>
<span data-ttu-id="9f493-119">此版本引入了对 `packageType` 查询参数的支持，允许按作者定义的包类型进行筛选。</span><span class="sxs-lookup"><span data-stu-id="9f493-119">This version introduces support for the `packageType` query parameter, allowing filtering by author defined package types.</span></span> <span data-ttu-id="9f493-120">它完全向后兼容的查询 `SearchAutocompleteService` 。</span><span class="sxs-lookup"><span data-stu-id="9f493-120">It is fully backwards compatible with queries to `SearchAutocompleteService`.</span></span>

## <a name="base-url"></a><span data-ttu-id="9f493-121">基 URL</span><span class="sxs-lookup"><span data-stu-id="9f493-121">Base URL</span></span>

<span data-ttu-id="9f493-122">以下 Api 的基 URL 是 `@id` 与上述某个资源值关联的属性的值 `@type` 。</span><span class="sxs-lookup"><span data-stu-id="9f493-122">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="9f493-123">在下面的文档中，将使用占位符基 URL `{@id}` 。</span><span class="sxs-lookup"><span data-stu-id="9f493-123">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="9f493-124">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="9f493-124">HTTP Methods</span></span>

<span data-ttu-id="9f493-125">注册资源中找到的所有 Url 都支持 HTTP 方法 `GET` 和 `HEAD` 。</span><span class="sxs-lookup"><span data-stu-id="9f493-125">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="9f493-126">搜索包 Id</span><span class="sxs-lookup"><span data-stu-id="9f493-126">Search for package IDs</span></span>

<span data-ttu-id="9f493-127">第一个自动完成 API 支持搜索包 ID 字符串的一部分。</span><span class="sxs-lookup"><span data-stu-id="9f493-127">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="9f493-128">如果要在与 NuGet 包源集成的用户界面中提供包 typeahead 功能，这非常有用。</span><span class="sxs-lookup"><span data-stu-id="9f493-128">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="9f493-129">只有未列出的版本的包将不会出现在结果中。</span><span class="sxs-lookup"><span data-stu-id="9f493-129">A package with only unlisted versions will not appear in the results.</span></span>

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a><span data-ttu-id="9f493-130">请求参数</span><span class="sxs-lookup"><span data-stu-id="9f493-130">Request parameters</span></span>

<span data-ttu-id="9f493-131">名称</span><span class="sxs-lookup"><span data-stu-id="9f493-131">Name</span></span>        | <span data-ttu-id="9f493-132">In</span><span class="sxs-lookup"><span data-stu-id="9f493-132">In</span></span>     | <span data-ttu-id="9f493-133">类型</span><span class="sxs-lookup"><span data-stu-id="9f493-133">Type</span></span>    | <span data-ttu-id="9f493-134">必须</span><span class="sxs-lookup"><span data-stu-id="9f493-134">Required</span></span> | <span data-ttu-id="9f493-135">注释</span><span class="sxs-lookup"><span data-stu-id="9f493-135">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="9f493-136">q</span><span class="sxs-lookup"><span data-stu-id="9f493-136">q</span></span>           | <span data-ttu-id="9f493-137">URL</span><span class="sxs-lookup"><span data-stu-id="9f493-137">URL</span></span>    | <span data-ttu-id="9f493-138">string</span><span class="sxs-lookup"><span data-stu-id="9f493-138">string</span></span>  | <span data-ttu-id="9f493-139">否</span><span class="sxs-lookup"><span data-stu-id="9f493-139">no</span></span>       | <span data-ttu-id="9f493-140">要与包 Id 进行比较的字符串</span><span class="sxs-lookup"><span data-stu-id="9f493-140">The string to compare against package IDs</span></span>
<span data-ttu-id="9f493-141">skip</span><span class="sxs-lookup"><span data-stu-id="9f493-141">skip</span></span>        | <span data-ttu-id="9f493-142">URL</span><span class="sxs-lookup"><span data-stu-id="9f493-142">URL</span></span>    | <span data-ttu-id="9f493-143">integer</span><span class="sxs-lookup"><span data-stu-id="9f493-143">integer</span></span> | <span data-ttu-id="9f493-144">否</span><span class="sxs-lookup"><span data-stu-id="9f493-144">no</span></span>       | <span data-ttu-id="9f493-145">要跳过的结果数，用于分页</span><span class="sxs-lookup"><span data-stu-id="9f493-145">The number of results to skip, for pagination</span></span>
<span data-ttu-id="9f493-146">take</span><span class="sxs-lookup"><span data-stu-id="9f493-146">take</span></span>        | <span data-ttu-id="9f493-147">URL</span><span class="sxs-lookup"><span data-stu-id="9f493-147">URL</span></span>    | <span data-ttu-id="9f493-148">integer</span><span class="sxs-lookup"><span data-stu-id="9f493-148">integer</span></span> | <span data-ttu-id="9f493-149">否</span><span class="sxs-lookup"><span data-stu-id="9f493-149">no</span></span>       | <span data-ttu-id="9f493-150">要返回的结果数，用于分页</span><span class="sxs-lookup"><span data-stu-id="9f493-150">The number of results to return, for pagination</span></span>
<span data-ttu-id="9f493-151">prerelease</span><span class="sxs-lookup"><span data-stu-id="9f493-151">prerelease</span></span>  | <span data-ttu-id="9f493-152">URL</span><span class="sxs-lookup"><span data-stu-id="9f493-152">URL</span></span>    | <span data-ttu-id="9f493-153">boolean</span><span class="sxs-lookup"><span data-stu-id="9f493-153">boolean</span></span> | <span data-ttu-id="9f493-154">否</span><span class="sxs-lookup"><span data-stu-id="9f493-154">no</span></span>       | <span data-ttu-id="9f493-155">`true` 或 `false` 确定是否包括 [预发布包](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="9f493-155">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="9f493-156">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="9f493-156">semVerLevel</span></span> | <span data-ttu-id="9f493-157">URL</span><span class="sxs-lookup"><span data-stu-id="9f493-157">URL</span></span>    | <span data-ttu-id="9f493-158">string</span><span class="sxs-lookup"><span data-stu-id="9f493-158">string</span></span>  | <span data-ttu-id="9f493-159">否</span><span class="sxs-lookup"><span data-stu-id="9f493-159">no</span></span>       | <span data-ttu-id="9f493-160">SemVer 1.0.0 版本字符串</span><span class="sxs-lookup"><span data-stu-id="9f493-160">A SemVer 1.0.0 version string</span></span> 
<span data-ttu-id="9f493-161">packageType</span><span class="sxs-lookup"><span data-stu-id="9f493-161">packageType</span></span> | <span data-ttu-id="9f493-162">URL</span><span class="sxs-lookup"><span data-stu-id="9f493-162">URL</span></span>    | <span data-ttu-id="9f493-163">string</span><span class="sxs-lookup"><span data-stu-id="9f493-163">string</span></span>  | <span data-ttu-id="9f493-164">否</span><span class="sxs-lookup"><span data-stu-id="9f493-164">no</span></span>       | <span data-ttu-id="9f493-165">用于筛选包的包类型 (添加到 `SearchAutocompleteService/3.5.0`) </span><span class="sxs-lookup"><span data-stu-id="9f493-165">The package type to use to filter packages (added in `SearchAutocompleteService/3.5.0`)</span></span>

<span data-ttu-id="9f493-166">自动完成查询按 `q` 服务器实现所定义的方式进行分析。</span><span class="sxs-lookup"><span data-stu-id="9f493-166">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="9f493-167">nuget.org 支持查询包 ID 令牌的前缀，该前缀是由拆分以大小写字符和符号字符为原始而生成的 ID 的组成部分。</span><span class="sxs-lookup"><span data-stu-id="9f493-167">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="9f493-168">`skip`参数默认为0。</span><span class="sxs-lookup"><span data-stu-id="9f493-168">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="9f493-169">`take`参数应为大于零的整数。</span><span class="sxs-lookup"><span data-stu-id="9f493-169">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="9f493-170">服务器实现可能会施加最大值。</span><span class="sxs-lookup"><span data-stu-id="9f493-170">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="9f493-171">如果 `prerelease` 未提供，则将排除预发布包。</span><span class="sxs-lookup"><span data-stu-id="9f493-171">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="9f493-172">`semVerLevel`Query 参数用于选择[SemVer 2.0.0 包](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。</span><span class="sxs-lookup"><span data-stu-id="9f493-172">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="9f493-173">如果排除此查询参数，则将仅返回 SemVer 1.0.0 兼容版本的包 Id (与 [标准 NuGet 版本控制](../concepts/package-versioning.md) 注意事项一起返回，如) 具有4个整数段的版本字符串。</span><span class="sxs-lookup"><span data-stu-id="9f493-173">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="9f493-174">如果 `semVerLevel=2.0.0` 提供了，则将返回 SemVer 1.0.0 和 SemVer 2.0.0 兼容包。</span><span class="sxs-lookup"><span data-stu-id="9f493-174">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="9f493-175">有关详细信息，请参阅 [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。</span><span class="sxs-lookup"><span data-stu-id="9f493-175">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

<span data-ttu-id="9f493-176">`packageType`参数用于进一步筛选自动完成结果，以使其仅包含至少一个与包类型名称匹配的包类型的包。</span><span class="sxs-lookup"><span data-stu-id="9f493-176">The `packageType` parameter is used to further filter the autocomplete results to only packages that have at least one package type matching the package type name.</span></span>
<span data-ttu-id="9f493-177">如果所提供的包类型不是 [包类型文档](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D)定义的有效包类型，将返回一个空结果。</span><span class="sxs-lookup"><span data-stu-id="9f493-177">If the provided package type is not a valid package type as defined by the [Package Type document](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), an empty result will returned.</span></span>
<span data-ttu-id="9f493-178">如果提供的包类型为空，则不会应用任何筛选器。</span><span class="sxs-lookup"><span data-stu-id="9f493-178">If the provided package type is empty, no filter will be applied.</span></span> <span data-ttu-id="9f493-179">换言之，不将值传递给参数的 `packageType` 行为与未传递参数的行为相同。</span><span class="sxs-lookup"><span data-stu-id="9f493-179">In other words, passing no value to the `packageType` parameter will behave as if the parameter was not passed.</span></span>

### <a name="response"></a><span data-ttu-id="9f493-180">响应</span><span class="sxs-lookup"><span data-stu-id="9f493-180">Response</span></span>

<span data-ttu-id="9f493-181">响应是最多包含 `take` 自动完成结果的 JSON 文档。</span><span class="sxs-lookup"><span data-stu-id="9f493-181">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="9f493-182">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="9f493-182">The root JSON object has the following properties:</span></span>

<span data-ttu-id="9f493-183">名称</span><span class="sxs-lookup"><span data-stu-id="9f493-183">Name</span></span>      | <span data-ttu-id="9f493-184">类型</span><span class="sxs-lookup"><span data-stu-id="9f493-184">Type</span></span>             | <span data-ttu-id="9f493-185">必须</span><span class="sxs-lookup"><span data-stu-id="9f493-185">Required</span></span> | <span data-ttu-id="9f493-186">注释</span><span class="sxs-lookup"><span data-stu-id="9f493-186">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="9f493-187">totalHits</span><span class="sxs-lookup"><span data-stu-id="9f493-187">totalHits</span></span> | <span data-ttu-id="9f493-188">integer</span><span class="sxs-lookup"><span data-stu-id="9f493-188">integer</span></span>          | <span data-ttu-id="9f493-189">是</span><span class="sxs-lookup"><span data-stu-id="9f493-189">yes</span></span>      | <span data-ttu-id="9f493-190">匹配项的总数，忽略 `skip` 和 `take`</span><span class="sxs-lookup"><span data-stu-id="9f493-190">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="9f493-191">data</span><span class="sxs-lookup"><span data-stu-id="9f493-191">data</span></span>      | <span data-ttu-id="9f493-192">字符串数组</span><span class="sxs-lookup"><span data-stu-id="9f493-192">array of strings</span></span> | <span data-ttu-id="9f493-193">是</span><span class="sxs-lookup"><span data-stu-id="9f493-193">yes</span></span>      | <span data-ttu-id="9f493-194">请求匹配的包 Id</span><span class="sxs-lookup"><span data-stu-id="9f493-194">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="9f493-195">示例请求</span><span class="sxs-lookup"><span data-stu-id="9f493-195">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="9f493-196">示例响应</span><span class="sxs-lookup"><span data-stu-id="9f493-196">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="9f493-197">枚举包版本</span><span class="sxs-lookup"><span data-stu-id="9f493-197">Enumerate package versions</span></span>

<span data-ttu-id="9f493-198">使用以前的 API 发现包 ID 后，客户端可以使用自动完成 API 来枚举提供的包 ID 的包版本。</span><span class="sxs-lookup"><span data-stu-id="9f493-198">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="9f493-199">未列出的包版本将不会出现在结果中。</span><span class="sxs-lookup"><span data-stu-id="9f493-199">A package version that is unlisted will not appear in the results.</span></span>

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="9f493-200">请求参数</span><span class="sxs-lookup"><span data-stu-id="9f493-200">Request parameters</span></span>

<span data-ttu-id="9f493-201">名称</span><span class="sxs-lookup"><span data-stu-id="9f493-201">Name</span></span>        | <span data-ttu-id="9f493-202">In</span><span class="sxs-lookup"><span data-stu-id="9f493-202">In</span></span>     | <span data-ttu-id="9f493-203">类型</span><span class="sxs-lookup"><span data-stu-id="9f493-203">Type</span></span>    | <span data-ttu-id="9f493-204">必须</span><span class="sxs-lookup"><span data-stu-id="9f493-204">Required</span></span> | <span data-ttu-id="9f493-205">注释</span><span class="sxs-lookup"><span data-stu-id="9f493-205">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="9f493-206">id</span><span class="sxs-lookup"><span data-stu-id="9f493-206">id</span></span>          | <span data-ttu-id="9f493-207">URL</span><span class="sxs-lookup"><span data-stu-id="9f493-207">URL</span></span>    | <span data-ttu-id="9f493-208">string</span><span class="sxs-lookup"><span data-stu-id="9f493-208">string</span></span>  | <span data-ttu-id="9f493-209">是</span><span class="sxs-lookup"><span data-stu-id="9f493-209">yes</span></span>      | <span data-ttu-id="9f493-210">要提取其版本的包 ID</span><span class="sxs-lookup"><span data-stu-id="9f493-210">The package ID to fetch versions for</span></span>
<span data-ttu-id="9f493-211">prerelease</span><span class="sxs-lookup"><span data-stu-id="9f493-211">prerelease</span></span>  | <span data-ttu-id="9f493-212">URL</span><span class="sxs-lookup"><span data-stu-id="9f493-212">URL</span></span>    | <span data-ttu-id="9f493-213">boolean</span><span class="sxs-lookup"><span data-stu-id="9f493-213">boolean</span></span> | <span data-ttu-id="9f493-214">否</span><span class="sxs-lookup"><span data-stu-id="9f493-214">no</span></span>       | <span data-ttu-id="9f493-215">`true` 或 `false` 确定是否包括 [预发布包](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="9f493-215">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="9f493-216">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="9f493-216">semVerLevel</span></span> | <span data-ttu-id="9f493-217">URL</span><span class="sxs-lookup"><span data-stu-id="9f493-217">URL</span></span>    | <span data-ttu-id="9f493-218">string</span><span class="sxs-lookup"><span data-stu-id="9f493-218">string</span></span>  | <span data-ttu-id="9f493-219">否</span><span class="sxs-lookup"><span data-stu-id="9f493-219">no</span></span>       | <span data-ttu-id="9f493-220">SemVer 2.0.0 版本字符串</span><span class="sxs-lookup"><span data-stu-id="9f493-220">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="9f493-221">如果 `prerelease` 未提供，则将排除预发布包。</span><span class="sxs-lookup"><span data-stu-id="9f493-221">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="9f493-222">`semVerLevel`Query 参数用于选择 SemVer 2.0.0 包。</span><span class="sxs-lookup"><span data-stu-id="9f493-222">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="9f493-223">如果排除此查询参数，则仅返回 SemVer 1.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="9f493-223">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="9f493-224">如果 `semVerLevel=2.0.0` 提供了，则将返回 SemVer 1.0.0 和 SemVer 2.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="9f493-224">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="9f493-225">有关详细信息，请参阅 [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。</span><span class="sxs-lookup"><span data-stu-id="9f493-225">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="9f493-226">响应</span><span class="sxs-lookup"><span data-stu-id="9f493-226">Response</span></span>

<span data-ttu-id="9f493-227">响应是一个 JSON 文档，其中包含所提供的包 ID 的所有包版本，并按给定的查询参数进行筛选。</span><span class="sxs-lookup"><span data-stu-id="9f493-227">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="9f493-228">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="9f493-228">The root JSON object has the following property:</span></span>

<span data-ttu-id="9f493-229">名称</span><span class="sxs-lookup"><span data-stu-id="9f493-229">Name</span></span>      | <span data-ttu-id="9f493-230">类型</span><span class="sxs-lookup"><span data-stu-id="9f493-230">Type</span></span>             | <span data-ttu-id="9f493-231">必须</span><span class="sxs-lookup"><span data-stu-id="9f493-231">Required</span></span> | <span data-ttu-id="9f493-232">注释</span><span class="sxs-lookup"><span data-stu-id="9f493-232">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="9f493-233">data</span><span class="sxs-lookup"><span data-stu-id="9f493-233">data</span></span>      | <span data-ttu-id="9f493-234">字符串数组</span><span class="sxs-lookup"><span data-stu-id="9f493-234">array of strings</span></span> | <span data-ttu-id="9f493-235">是</span><span class="sxs-lookup"><span data-stu-id="9f493-235">yes</span></span>      | <span data-ttu-id="9f493-236">与请求匹配的包版本</span><span class="sxs-lookup"><span data-stu-id="9f493-236">The package versions matched by the request</span></span>

<span data-ttu-id="9f493-237">数组中的包版本 `data` 可能包含 SemVer 2.0.0 build metadata (例如， `1.0.0+metadata` 如果 `semVerLevel=2.0.0` 查询字符串中提供了) ，则为。</span><span class="sxs-lookup"><span data-stu-id="9f493-237">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="9f493-238">示例请求</span><span class="sxs-lookup"><span data-stu-id="9f493-238">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="9f493-239">示例响应</span><span class="sxs-lookup"><span data-stu-id="9f493-239">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
