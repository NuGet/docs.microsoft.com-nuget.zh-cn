---
title: 包内容，NuGet API
description: 包基址是一个简单的接口，用于提取包本身。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7aea28d6224a89149aa33be035c82a45db3058f0
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094124"
---
# <a name="package-content"></a><span data-ttu-id="2322b-103">包内容</span><span class="sxs-lookup"><span data-stu-id="2322b-103">Package Content</span></span>

<span data-ttu-id="2322b-104">可以使用 V3 API 生成 URL 来提取任意包的内容（nupkg 文件）。</span><span class="sxs-lookup"><span data-stu-id="2322b-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="2322b-105">用于提取包内容的资源是在`PackageBaseAddress` [服务索引](service-index.md)中找到的资源。</span><span class="sxs-lookup"><span data-stu-id="2322b-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="2322b-106">此资源还允许发现包的所有版本、列出或未列出。</span><span class="sxs-lookup"><span data-stu-id="2322b-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="2322b-107">此资源通常称为 "包基址" 或 "平面容器"。</span><span class="sxs-lookup"><span data-stu-id="2322b-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="2322b-108">版本管理</span><span class="sxs-lookup"><span data-stu-id="2322b-108">Versioning</span></span>

<span data-ttu-id="2322b-109">使用以下`@type`值：</span><span class="sxs-lookup"><span data-stu-id="2322b-109">The following `@type` value is used:</span></span>

<span data-ttu-id="2322b-110">@type 值</span><span class="sxs-lookup"><span data-stu-id="2322b-110">@type value</span></span>              | <span data-ttu-id="2322b-111">说明</span><span class="sxs-lookup"><span data-stu-id="2322b-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="2322b-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="2322b-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="2322b-113">初始版本</span><span class="sxs-lookup"><span data-stu-id="2322b-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="2322b-114">基 URL</span><span class="sxs-lookup"><span data-stu-id="2322b-114">Base URL</span></span>

<span data-ttu-id="2322b-115">以下 api 的基 URL 是与上述资源`@id` `@type`值关联的属性的值。</span><span class="sxs-lookup"><span data-stu-id="2322b-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="2322b-116">在下面的文档中，将使用占位符`{@id}`基 URL。</span><span class="sxs-lookup"><span data-stu-id="2322b-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2322b-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="2322b-117">HTTP methods</span></span>

<span data-ttu-id="2322b-118">注册资源中找到的所有 url 都支持 HTTP 方法`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="2322b-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="2322b-119">枚举包版本</span><span class="sxs-lookup"><span data-stu-id="2322b-119">Enumerate package versions</span></span>

<span data-ttu-id="2322b-120">如果客户端知道包 ID 并想要发现包源有哪些包版本可用，则客户端可以构造可预测的 URL 来枚举所有包版本。</span><span class="sxs-lookup"><span data-stu-id="2322b-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="2322b-121">此列表应为下述包内容 API 的 "目录列表"。</span><span class="sxs-lookup"><span data-stu-id="2322b-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="2322b-122">此列表包含列出和未列出的包版本。</span><span class="sxs-lookup"><span data-stu-id="2322b-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="2322b-123">请求参数</span><span class="sxs-lookup"><span data-stu-id="2322b-123">Request parameters</span></span>

<span data-ttu-id="2322b-124">name</span><span class="sxs-lookup"><span data-stu-id="2322b-124">Name</span></span>     | <span data-ttu-id="2322b-125">内</span><span class="sxs-lookup"><span data-stu-id="2322b-125">In</span></span>     | <span data-ttu-id="2322b-126">类型</span><span class="sxs-lookup"><span data-stu-id="2322b-126">Type</span></span>    | <span data-ttu-id="2322b-127">必填</span><span class="sxs-lookup"><span data-stu-id="2322b-127">Required</span></span> | <span data-ttu-id="2322b-128">说明</span><span class="sxs-lookup"><span data-stu-id="2322b-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="2322b-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="2322b-129">LOWER_ID</span></span> | <span data-ttu-id="2322b-130">URL</span><span class="sxs-lookup"><span data-stu-id="2322b-130">URL</span></span>    | <span data-ttu-id="2322b-131">string</span><span class="sxs-lookup"><span data-stu-id="2322b-131">string</span></span>  | <span data-ttu-id="2322b-132">是</span><span class="sxs-lookup"><span data-stu-id="2322b-132">yes</span></span>      | <span data-ttu-id="2322b-133">包 ID lowercased</span><span class="sxs-lookup"><span data-stu-id="2322b-133">The package ID, lowercased</span></span>

<span data-ttu-id="2322b-134">`LOWER_ID`值是所需的包 ID lowercased，它使用由实现的规则。NET 的[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="2322b-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="2322b-135">响应</span><span class="sxs-lookup"><span data-stu-id="2322b-135">Response</span></span>

<span data-ttu-id="2322b-136">如果包源没有提供的包 ID 版本，则返回404状态代码。</span><span class="sxs-lookup"><span data-stu-id="2322b-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="2322b-137">如果包源有一个或多个版本，则返回200状态代码。</span><span class="sxs-lookup"><span data-stu-id="2322b-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="2322b-138">响应正文是包含以下属性的 JSON 对象：</span><span class="sxs-lookup"><span data-stu-id="2322b-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="2322b-139">name</span><span class="sxs-lookup"><span data-stu-id="2322b-139">Name</span></span>     | <span data-ttu-id="2322b-140">类型</span><span class="sxs-lookup"><span data-stu-id="2322b-140">Type</span></span>             | <span data-ttu-id="2322b-141">必填</span><span class="sxs-lookup"><span data-stu-id="2322b-141">Required</span></span> | <span data-ttu-id="2322b-142">说明</span><span class="sxs-lookup"><span data-stu-id="2322b-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="2322b-143">版本</span><span class="sxs-lookup"><span data-stu-id="2322b-143">versions</span></span> | <span data-ttu-id="2322b-144">字符串数组</span><span class="sxs-lookup"><span data-stu-id="2322b-144">array of strings</span></span> | <span data-ttu-id="2322b-145">是</span><span class="sxs-lookup"><span data-stu-id="2322b-145">yes</span></span>      | <span data-ttu-id="2322b-146">可用版本</span><span class="sxs-lookup"><span data-stu-id="2322b-146">The versions available</span></span>

<span data-ttu-id="2322b-147">`versions`数组中的字符串是所有 lowercased 的[规范化 NuGet 版本字符串](../concepts/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="2322b-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="2322b-148">版本字符串不包含任何 SemVer 2.0.0 生成元数据。</span><span class="sxs-lookup"><span data-stu-id="2322b-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="2322b-149">目的在于，在此数组中找到的版本字符串可以逐字`LOWER_VERSION`用于以下终结点中的标记。</span><span class="sxs-lookup"><span data-stu-id="2322b-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="2322b-150">示例请求</span><span class="sxs-lookup"><span data-stu-id="2322b-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="2322b-151">示例响应</span><span class="sxs-lookup"><span data-stu-id="2322b-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="2322b-152">下载包内容（. nupkg）</span><span class="sxs-lookup"><span data-stu-id="2322b-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="2322b-153">如果客户端知道包 ID 和版本并想要下载包内容，则它们只需构造以下 URL：</span><span class="sxs-lookup"><span data-stu-id="2322b-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="2322b-154">请求参数</span><span class="sxs-lookup"><span data-stu-id="2322b-154">Request parameters</span></span>

<span data-ttu-id="2322b-155">name</span><span class="sxs-lookup"><span data-stu-id="2322b-155">Name</span></span>          | <span data-ttu-id="2322b-156">内</span><span class="sxs-lookup"><span data-stu-id="2322b-156">In</span></span>     | <span data-ttu-id="2322b-157">类型</span><span class="sxs-lookup"><span data-stu-id="2322b-157">Type</span></span>   | <span data-ttu-id="2322b-158">必填</span><span class="sxs-lookup"><span data-stu-id="2322b-158">Required</span></span> | <span data-ttu-id="2322b-159">说明</span><span class="sxs-lookup"><span data-stu-id="2322b-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2322b-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="2322b-160">LOWER_ID</span></span>      | <span data-ttu-id="2322b-161">URL</span><span class="sxs-lookup"><span data-stu-id="2322b-161">URL</span></span>    | <span data-ttu-id="2322b-162">string</span><span class="sxs-lookup"><span data-stu-id="2322b-162">string</span></span> | <span data-ttu-id="2322b-163">是</span><span class="sxs-lookup"><span data-stu-id="2322b-163">yes</span></span>      | <span data-ttu-id="2322b-164">包 ID，小写</span><span class="sxs-lookup"><span data-stu-id="2322b-164">The package ID, lowercase</span></span>
<span data-ttu-id="2322b-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="2322b-165">LOWER_VERSION</span></span> | <span data-ttu-id="2322b-166">URL</span><span class="sxs-lookup"><span data-stu-id="2322b-166">URL</span></span>    | <span data-ttu-id="2322b-167">string</span><span class="sxs-lookup"><span data-stu-id="2322b-167">string</span></span> | <span data-ttu-id="2322b-168">是</span><span class="sxs-lookup"><span data-stu-id="2322b-168">yes</span></span>      | <span data-ttu-id="2322b-169">包版本（正常化和 lowercased）</span><span class="sxs-lookup"><span data-stu-id="2322b-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="2322b-170">`LOWER_ID` 和`LOWER_VERSION`都是使用实现的规则 lowercased 的。网络[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="2322b-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="2322b-171">方法。</span><span class="sxs-lookup"><span data-stu-id="2322b-171">method.</span></span>

<span data-ttu-id="2322b-172">是使用 NuGet 的版本[规范化规则](../concepts/package-versioning.md#normalized-version-numbers)规范化的所需包版本。 `LOWER_VERSION`</span><span class="sxs-lookup"><span data-stu-id="2322b-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="2322b-173">这意味着，在这种情况下必须排除 SemVer 2.0.0 规范允许的生成元数据。</span><span class="sxs-lookup"><span data-stu-id="2322b-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="2322b-174">响应正文</span><span class="sxs-lookup"><span data-stu-id="2322b-174">Response body</span></span>

<span data-ttu-id="2322b-175">如果包源上存在包，则返回200状态代码。</span><span class="sxs-lookup"><span data-stu-id="2322b-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="2322b-176">响应正文将是包内容本身。</span><span class="sxs-lookup"><span data-stu-id="2322b-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="2322b-177">如果包源中不存在包，则返回404状态代码。</span><span class="sxs-lookup"><span data-stu-id="2322b-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="2322b-178">示例请求</span><span class="sxs-lookup"><span data-stu-id="2322b-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="2322b-179">示例响应</span><span class="sxs-lookup"><span data-stu-id="2322b-179">Sample response</span></span>

<span data-ttu-id="2322b-180">Newtonsoft.json 的 nupkg 的二进制流。</span><span class="sxs-lookup"><span data-stu-id="2322b-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="2322b-181">下载包清单（. nuspec）</span><span class="sxs-lookup"><span data-stu-id="2322b-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="2322b-182">如果客户端知道包 ID 和版本并想要下载包清单，则它们只需构造以下 URL：</span><span class="sxs-lookup"><span data-stu-id="2322b-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="2322b-183">请求参数</span><span class="sxs-lookup"><span data-stu-id="2322b-183">Request parameters</span></span>

<span data-ttu-id="2322b-184">name</span><span class="sxs-lookup"><span data-stu-id="2322b-184">Name</span></span>          | <span data-ttu-id="2322b-185">内</span><span class="sxs-lookup"><span data-stu-id="2322b-185">In</span></span>     | <span data-ttu-id="2322b-186">类型</span><span class="sxs-lookup"><span data-stu-id="2322b-186">Type</span></span>   | <span data-ttu-id="2322b-187">必需</span><span class="sxs-lookup"><span data-stu-id="2322b-187">Required</span></span> | <span data-ttu-id="2322b-188">说明</span><span class="sxs-lookup"><span data-stu-id="2322b-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2322b-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="2322b-189">LOWER_ID</span></span>      | <span data-ttu-id="2322b-190">URL</span><span class="sxs-lookup"><span data-stu-id="2322b-190">URL</span></span>    | <span data-ttu-id="2322b-191">string</span><span class="sxs-lookup"><span data-stu-id="2322b-191">string</span></span> | <span data-ttu-id="2322b-192">是</span><span class="sxs-lookup"><span data-stu-id="2322b-192">yes</span></span>      | <span data-ttu-id="2322b-193">包 ID，小写</span><span class="sxs-lookup"><span data-stu-id="2322b-193">The package ID, lowercase</span></span>
<span data-ttu-id="2322b-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="2322b-194">LOWER_VERSION</span></span> | <span data-ttu-id="2322b-195">URL</span><span class="sxs-lookup"><span data-stu-id="2322b-195">URL</span></span>    | <span data-ttu-id="2322b-196">string</span><span class="sxs-lookup"><span data-stu-id="2322b-196">string</span></span> | <span data-ttu-id="2322b-197">是</span><span class="sxs-lookup"><span data-stu-id="2322b-197">yes</span></span>      | <span data-ttu-id="2322b-198">包版本（正常化和 lowercased）</span><span class="sxs-lookup"><span data-stu-id="2322b-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="2322b-199">`LOWER_ID` 和`LOWER_VERSION`都是使用实现的规则 lowercased 的。NET 的[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="2322b-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="2322b-200">是使用 NuGet 的版本[规范化规则](../concepts/package-versioning.md#normalized-version-numbers)规范化的所需包版本。 `LOWER_VERSION`</span><span class="sxs-lookup"><span data-stu-id="2322b-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="2322b-201">这意味着，在这种情况下必须排除 SemVer 2.0.0 规范允许的生成元数据。</span><span class="sxs-lookup"><span data-stu-id="2322b-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="2322b-202">响应正文</span><span class="sxs-lookup"><span data-stu-id="2322b-202">Response body</span></span>

<span data-ttu-id="2322b-203">如果包源上存在包，则返回200状态代码。</span><span class="sxs-lookup"><span data-stu-id="2322b-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="2322b-204">响应正文将为包清单，即 nuspec 中包含的 nupkg。</span><span class="sxs-lookup"><span data-stu-id="2322b-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="2322b-205">Nuspec 是一个 XML 文档。</span><span class="sxs-lookup"><span data-stu-id="2322b-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="2322b-206">如果包源中不存在包，则返回404状态代码。</span><span class="sxs-lookup"><span data-stu-id="2322b-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="2322b-207">示例请求</span><span class="sxs-lookup"><span data-stu-id="2322b-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="2322b-208">示例响应</span><span class="sxs-lookup"><span data-stu-id="2322b-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
