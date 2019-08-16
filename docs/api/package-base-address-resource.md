---
title: 包内容, NuGet API
description: 包基址是一个简单的接口, 用于提取包本身。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 5ec6c0e17a3e8b9a3f156a48685bcaafe42c744b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488222"
---
# <a name="package-content"></a><span data-ttu-id="d712e-103">包内容</span><span class="sxs-lookup"><span data-stu-id="d712e-103">Package Content</span></span>

<span data-ttu-id="d712e-104">可以使用 V3 API 生成 URL 来提取任意包的内容 (nupkg 文件)。</span><span class="sxs-lookup"><span data-stu-id="d712e-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="d712e-105">用于提取包内容的资源是在`PackageBaseAddress` [服务索引](service-index.md)中找到的资源。</span><span class="sxs-lookup"><span data-stu-id="d712e-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="d712e-106">此资源还允许发现包的所有版本、列出或未列出。</span><span class="sxs-lookup"><span data-stu-id="d712e-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="d712e-107">此资源通常称为 "包基址" 或 "平面容器"。</span><span class="sxs-lookup"><span data-stu-id="d712e-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="d712e-108">版本管理</span><span class="sxs-lookup"><span data-stu-id="d712e-108">Versioning</span></span>

<span data-ttu-id="d712e-109">使用以下`@type`值:</span><span class="sxs-lookup"><span data-stu-id="d712e-109">The following `@type` value is used:</span></span>

<span data-ttu-id="d712e-110">@type 值</span><span class="sxs-lookup"><span data-stu-id="d712e-110">@type value</span></span>              | <span data-ttu-id="d712e-111">说明</span><span class="sxs-lookup"><span data-stu-id="d712e-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="d712e-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="d712e-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="d712e-113">初始版本</span><span class="sxs-lookup"><span data-stu-id="d712e-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="d712e-114">基 URL</span><span class="sxs-lookup"><span data-stu-id="d712e-114">Base URL</span></span>

<span data-ttu-id="d712e-115">以下 api 的基 URL 是与上述资源`@id` `@type`值关联的属性的值。</span><span class="sxs-lookup"><span data-stu-id="d712e-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="d712e-116">在下面的文档中, 将使用占位符`{@id}`基 URL。</span><span class="sxs-lookup"><span data-stu-id="d712e-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d712e-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="d712e-117">HTTP methods</span></span>

<span data-ttu-id="d712e-118">注册资源中找到的所有 url 都支持 HTTP 方法`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="d712e-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="d712e-119">枚举包版本</span><span class="sxs-lookup"><span data-stu-id="d712e-119">Enumerate package versions</span></span>

<span data-ttu-id="d712e-120">如果客户端知道包 ID 并想要发现包源有哪些包版本可用, 则客户端可以构造可预测的 URL 来枚举所有包版本。</span><span class="sxs-lookup"><span data-stu-id="d712e-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="d712e-121">此列表应为下述包内容 API 的 "目录列表"。</span><span class="sxs-lookup"><span data-stu-id="d712e-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="d712e-122">此列表包含列出和未列出的包版本。</span><span class="sxs-lookup"><span data-stu-id="d712e-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="d712e-123">请求参数</span><span class="sxs-lookup"><span data-stu-id="d712e-123">Request parameters</span></span>

<span data-ttu-id="d712e-124">name</span><span class="sxs-lookup"><span data-stu-id="d712e-124">Name</span></span>     | <span data-ttu-id="d712e-125">内</span><span class="sxs-lookup"><span data-stu-id="d712e-125">In</span></span>     | <span data-ttu-id="d712e-126">类型</span><span class="sxs-lookup"><span data-stu-id="d712e-126">Type</span></span>    | <span data-ttu-id="d712e-127">必填</span><span class="sxs-lookup"><span data-stu-id="d712e-127">Required</span></span> | <span data-ttu-id="d712e-128">说明</span><span class="sxs-lookup"><span data-stu-id="d712e-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="d712e-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="d712e-129">LOWER_ID</span></span> | <span data-ttu-id="d712e-130">URL</span><span class="sxs-lookup"><span data-stu-id="d712e-130">URL</span></span>    | <span data-ttu-id="d712e-131">string</span><span class="sxs-lookup"><span data-stu-id="d712e-131">string</span></span>  | <span data-ttu-id="d712e-132">是</span><span class="sxs-lookup"><span data-stu-id="d712e-132">yes</span></span>      | <span data-ttu-id="d712e-133">包 ID, 小写</span><span class="sxs-lookup"><span data-stu-id="d712e-133">The package ID, lowercase</span></span>

<span data-ttu-id="d712e-134">`LOWER_ID`值是所需的包 ID lowercased, 它使用由实现的规则。NET 的[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="d712e-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="d712e-135">响应</span><span class="sxs-lookup"><span data-stu-id="d712e-135">Response</span></span>

<span data-ttu-id="d712e-136">如果包源没有提供的包 ID 版本, 则返回404状态代码。</span><span class="sxs-lookup"><span data-stu-id="d712e-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="d712e-137">如果包源有一个或多个版本, 则返回200状态代码。</span><span class="sxs-lookup"><span data-stu-id="d712e-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="d712e-138">响应正文是包含以下属性的 JSON 对象:</span><span class="sxs-lookup"><span data-stu-id="d712e-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="d712e-139">name</span><span class="sxs-lookup"><span data-stu-id="d712e-139">Name</span></span>     | <span data-ttu-id="d712e-140">类型</span><span class="sxs-lookup"><span data-stu-id="d712e-140">Type</span></span>             | <span data-ttu-id="d712e-141">必填</span><span class="sxs-lookup"><span data-stu-id="d712e-141">Required</span></span> | <span data-ttu-id="d712e-142">说明</span><span class="sxs-lookup"><span data-stu-id="d712e-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="d712e-143">版本</span><span class="sxs-lookup"><span data-stu-id="d712e-143">versions</span></span> | <span data-ttu-id="d712e-144">字符串数组</span><span class="sxs-lookup"><span data-stu-id="d712e-144">array of strings</span></span> | <span data-ttu-id="d712e-145">是</span><span class="sxs-lookup"><span data-stu-id="d712e-145">yes</span></span>      | <span data-ttu-id="d712e-146">可用的包 Id</span><span class="sxs-lookup"><span data-stu-id="d712e-146">The package IDs available</span></span>

<span data-ttu-id="d712e-147">`versions`数组中的字符串是所有 lowercased 的[规范化 NuGet 版本字符串](../concepts/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="d712e-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="d712e-148">版本字符串不包含任何 SemVer 2.0.0 生成元数据。</span><span class="sxs-lookup"><span data-stu-id="d712e-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="d712e-149">目的在于, 在此数组中找到的版本字符串可以逐字`LOWER_VERSION`用于以下终结点中的标记。</span><span class="sxs-lookup"><span data-stu-id="d712e-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d712e-150">示例请求</span><span class="sxs-lookup"><span data-stu-id="d712e-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="d712e-151">示例响应</span><span class="sxs-lookup"><span data-stu-id="d712e-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="d712e-152">下载包内容 (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="d712e-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="d712e-153">如果客户端知道包 ID 和版本并想要下载包内容, 则它们只需构造以下 URL:</span><span class="sxs-lookup"><span data-stu-id="d712e-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="d712e-154">请求参数</span><span class="sxs-lookup"><span data-stu-id="d712e-154">Request parameters</span></span>

<span data-ttu-id="d712e-155">name</span><span class="sxs-lookup"><span data-stu-id="d712e-155">Name</span></span>          | <span data-ttu-id="d712e-156">内</span><span class="sxs-lookup"><span data-stu-id="d712e-156">In</span></span>     | <span data-ttu-id="d712e-157">类型</span><span class="sxs-lookup"><span data-stu-id="d712e-157">Type</span></span>   | <span data-ttu-id="d712e-158">必需</span><span class="sxs-lookup"><span data-stu-id="d712e-158">Required</span></span> | <span data-ttu-id="d712e-159">说明</span><span class="sxs-lookup"><span data-stu-id="d712e-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d712e-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="d712e-160">LOWER_ID</span></span>      | <span data-ttu-id="d712e-161">URL</span><span class="sxs-lookup"><span data-stu-id="d712e-161">URL</span></span>    | <span data-ttu-id="d712e-162">string</span><span class="sxs-lookup"><span data-stu-id="d712e-162">string</span></span> | <span data-ttu-id="d712e-163">是</span><span class="sxs-lookup"><span data-stu-id="d712e-163">yes</span></span>      | <span data-ttu-id="d712e-164">包 ID, 小写</span><span class="sxs-lookup"><span data-stu-id="d712e-164">The package ID, lowercase</span></span>
<span data-ttu-id="d712e-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="d712e-165">LOWER_VERSION</span></span> | <span data-ttu-id="d712e-166">URL</span><span class="sxs-lookup"><span data-stu-id="d712e-166">URL</span></span>    | <span data-ttu-id="d712e-167">string</span><span class="sxs-lookup"><span data-stu-id="d712e-167">string</span></span> | <span data-ttu-id="d712e-168">是</span><span class="sxs-lookup"><span data-stu-id="d712e-168">yes</span></span>      | <span data-ttu-id="d712e-169">包版本 (正常化和 lowercased)</span><span class="sxs-lookup"><span data-stu-id="d712e-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="d712e-170">`LOWER_ID` 和`LOWER_VERSION`都是使用实现的规则 lowercased 的。网络[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="d712e-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="d712e-171">方法。</span><span class="sxs-lookup"><span data-stu-id="d712e-171">method.</span></span>

<span data-ttu-id="d712e-172">是使用 NuGet 的版本[规范化规则](../concepts/package-versioning.md#normalized-version-numbers)规范化的所需包版本。 `LOWER_VERSION`</span><span class="sxs-lookup"><span data-stu-id="d712e-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="d712e-173">这意味着, 在这种情况下必须排除 SemVer 2.0.0 规范允许的生成元数据。</span><span class="sxs-lookup"><span data-stu-id="d712e-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="d712e-174">响应正文</span><span class="sxs-lookup"><span data-stu-id="d712e-174">Response body</span></span>

<span data-ttu-id="d712e-175">如果包源上存在包, 则返回200状态代码。</span><span class="sxs-lookup"><span data-stu-id="d712e-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="d712e-176">响应正文将是包内容本身。</span><span class="sxs-lookup"><span data-stu-id="d712e-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="d712e-177">如果包源中不存在包, 则返回404状态代码。</span><span class="sxs-lookup"><span data-stu-id="d712e-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d712e-178">示例请求</span><span class="sxs-lookup"><span data-stu-id="d712e-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="d712e-179">示例响应</span><span class="sxs-lookup"><span data-stu-id="d712e-179">Sample response</span></span>

<span data-ttu-id="d712e-180">Newtonsoft.json 的 nupkg 的二进制流。</span><span class="sxs-lookup"><span data-stu-id="d712e-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="d712e-181">下载包清单 (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="d712e-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="d712e-182">如果客户端知道包 ID 和版本并想要下载包清单, 则它们只需构造以下 URL:</span><span class="sxs-lookup"><span data-stu-id="d712e-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="d712e-183">请求参数</span><span class="sxs-lookup"><span data-stu-id="d712e-183">Request parameters</span></span>

<span data-ttu-id="d712e-184">name</span><span class="sxs-lookup"><span data-stu-id="d712e-184">Name</span></span>          | <span data-ttu-id="d712e-185">内</span><span class="sxs-lookup"><span data-stu-id="d712e-185">In</span></span>     | <span data-ttu-id="d712e-186">类型</span><span class="sxs-lookup"><span data-stu-id="d712e-186">Type</span></span>   | <span data-ttu-id="d712e-187">必需</span><span class="sxs-lookup"><span data-stu-id="d712e-187">Required</span></span> | <span data-ttu-id="d712e-188">说明</span><span class="sxs-lookup"><span data-stu-id="d712e-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d712e-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="d712e-189">LOWER_ID</span></span>      | <span data-ttu-id="d712e-190">URL</span><span class="sxs-lookup"><span data-stu-id="d712e-190">URL</span></span>    | <span data-ttu-id="d712e-191">string</span><span class="sxs-lookup"><span data-stu-id="d712e-191">string</span></span> | <span data-ttu-id="d712e-192">是</span><span class="sxs-lookup"><span data-stu-id="d712e-192">yes</span></span>      | <span data-ttu-id="d712e-193">包 ID, 小写</span><span class="sxs-lookup"><span data-stu-id="d712e-193">The package ID, lowercase</span></span>
<span data-ttu-id="d712e-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="d712e-194">LOWER_VERSION</span></span> | <span data-ttu-id="d712e-195">URL</span><span class="sxs-lookup"><span data-stu-id="d712e-195">URL</span></span>    | <span data-ttu-id="d712e-196">string</span><span class="sxs-lookup"><span data-stu-id="d712e-196">string</span></span> | <span data-ttu-id="d712e-197">是</span><span class="sxs-lookup"><span data-stu-id="d712e-197">yes</span></span>      | <span data-ttu-id="d712e-198">包版本 (正常化和 lowercased)</span><span class="sxs-lookup"><span data-stu-id="d712e-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="d712e-199">`LOWER_ID` 和`LOWER_VERSION`都是使用实现的规则 lowercased 的。NET 的[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="d712e-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="d712e-200">是使用 NuGet 的版本[规范化规则](../concepts/package-versioning.md#normalized-version-numbers)规范化的所需包版本。 `LOWER_VERSION`</span><span class="sxs-lookup"><span data-stu-id="d712e-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="d712e-201">这意味着, 在这种情况下必须排除 SemVer 2.0.0 规范允许的生成元数据。</span><span class="sxs-lookup"><span data-stu-id="d712e-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="d712e-202">响应正文</span><span class="sxs-lookup"><span data-stu-id="d712e-202">Response body</span></span>

<span data-ttu-id="d712e-203">如果包源上存在包, 则返回200状态代码。</span><span class="sxs-lookup"><span data-stu-id="d712e-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="d712e-204">响应正文将为包清单, 即 nuspec 中包含的 nupkg。</span><span class="sxs-lookup"><span data-stu-id="d712e-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="d712e-205">Nuspec 是一个 XML 文档。</span><span class="sxs-lookup"><span data-stu-id="d712e-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="d712e-206">如果包源中不存在包, 则返回404状态代码。</span><span class="sxs-lookup"><span data-stu-id="d712e-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d712e-207">示例请求</span><span class="sxs-lookup"><span data-stu-id="d712e-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="d712e-208">示例响应</span><span class="sxs-lookup"><span data-stu-id="d712e-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
