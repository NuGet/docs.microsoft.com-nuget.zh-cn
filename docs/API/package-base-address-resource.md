---
title: 包的内容，NuGet API
description: 包基址是一个简单接口提取包本身。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="package-content"></a><span data-ttu-id="8603a-103">包内容</span><span class="sxs-lookup"><span data-stu-id="8603a-103">Package Content</span></span>

<span data-ttu-id="8603a-104">就可以生成一个 URL，以提取任意包的内容 （.nupkg 文件） 使用 V3 API。</span><span class="sxs-lookup"><span data-stu-id="8603a-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="8603a-105">用于提取包内容的资源是`PackageBaseAddress`资源位于[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="8603a-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="8603a-106">此资源还使发现的所有版本的包，列出或未列出。</span><span class="sxs-lookup"><span data-stu-id="8603a-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="8603a-107">此资源通常称为为任一的"包基址"或"平面容器"。</span><span class="sxs-lookup"><span data-stu-id="8603a-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="8603a-108">版本管理</span><span class="sxs-lookup"><span data-stu-id="8603a-108">Versioning</span></span>

<span data-ttu-id="8603a-109">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="8603a-109">The following `@type` value is used:</span></span>

<span data-ttu-id="8603a-110">@type 值</span><span class="sxs-lookup"><span data-stu-id="8603a-110">@type value</span></span>              | <span data-ttu-id="8603a-111">说明</span><span class="sxs-lookup"><span data-stu-id="8603a-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="8603a-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="8603a-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="8603a-113">初始版本</span><span class="sxs-lookup"><span data-stu-id="8603a-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="8603a-114">基 URL</span><span class="sxs-lookup"><span data-stu-id="8603a-114">Base URL</span></span>

<span data-ttu-id="8603a-115">以下 Api 的基 URL 是值`@id`与前面提到的资源关联的属性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="8603a-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="8603a-116">在以下文档中，将占位符基本 URL`{@id}`将使用。</span><span class="sxs-lookup"><span data-stu-id="8603a-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="8603a-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="8603a-117">HTTP methods</span></span>

<span data-ttu-id="8603a-118">HTTP 方法位于注册资源支持的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="8603a-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="8603a-119">枚举包版本</span><span class="sxs-lookup"><span data-stu-id="8603a-119">Enumerate package versions</span></span>

<span data-ttu-id="8603a-120">如果客户端知道包 ID，并想要发现的包版本包源具有可用，客户端可以构造一个可预测的 URL，以枚举所有包版本。</span><span class="sxs-lookup"><span data-stu-id="8603a-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="8603a-121">此列表是要作为"目录列表"下面所述的内容包 api。</span><span class="sxs-lookup"><span data-stu-id="8603a-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="8603a-122">此列表包含两个列和未列出的包版本。</span><span class="sxs-lookup"><span data-stu-id="8603a-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="8603a-123">请求参数</span><span class="sxs-lookup"><span data-stu-id="8603a-123">Request parameters</span></span>

<span data-ttu-id="8603a-124">名称</span><span class="sxs-lookup"><span data-stu-id="8603a-124">Name</span></span>     | <span data-ttu-id="8603a-125">内</span><span class="sxs-lookup"><span data-stu-id="8603a-125">In</span></span>     | <span data-ttu-id="8603a-126">类型</span><span class="sxs-lookup"><span data-stu-id="8603a-126">Type</span></span>    | <span data-ttu-id="8603a-127">必需</span><span class="sxs-lookup"><span data-stu-id="8603a-127">Required</span></span> | <span data-ttu-id="8603a-128">说明</span><span class="sxs-lookup"><span data-stu-id="8603a-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="8603a-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="8603a-129">LOWER_ID</span></span> | <span data-ttu-id="8603a-130">URL</span><span class="sxs-lookup"><span data-stu-id="8603a-130">URL</span></span>    | <span data-ttu-id="8603a-131">字符串</span><span class="sxs-lookup"><span data-stu-id="8603a-131">string</span></span>  | <span data-ttu-id="8603a-132">是</span><span class="sxs-lookup"><span data-stu-id="8603a-132">yes</span></span>      | <span data-ttu-id="8603a-133">包 ID 小写</span><span class="sxs-lookup"><span data-stu-id="8603a-133">The package ID, lowercase</span></span>

<span data-ttu-id="8603a-134">`LOWER_ID`值是小写使用由实现的规则的所需的包 ID。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="8603a-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="8603a-135">响应</span><span class="sxs-lookup"><span data-stu-id="8603a-135">Response</span></span>

<span data-ttu-id="8603a-136">如果包源具有未提供的包 ID 的版本，则返回状态代码 404。</span><span class="sxs-lookup"><span data-stu-id="8603a-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="8603a-137">如果包源具有一个或多个版本，则返回状态代码 200。</span><span class="sxs-lookup"><span data-stu-id="8603a-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="8603a-138">响应正文是具有以下属性的 JSON 对象：</span><span class="sxs-lookup"><span data-stu-id="8603a-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="8603a-139">名称</span><span class="sxs-lookup"><span data-stu-id="8603a-139">Name</span></span>     | <span data-ttu-id="8603a-140">类型</span><span class="sxs-lookup"><span data-stu-id="8603a-140">Type</span></span>             | <span data-ttu-id="8603a-141">必需</span><span class="sxs-lookup"><span data-stu-id="8603a-141">Required</span></span> | <span data-ttu-id="8603a-142">说明</span><span class="sxs-lookup"><span data-stu-id="8603a-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="8603a-143">版本</span><span class="sxs-lookup"><span data-stu-id="8603a-143">versions</span></span> | <span data-ttu-id="8603a-144">字符串数组</span><span class="sxs-lookup"><span data-stu-id="8603a-144">array of strings</span></span> | <span data-ttu-id="8603a-145">是</span><span class="sxs-lookup"><span data-stu-id="8603a-145">yes</span></span>      | <span data-ttu-id="8603a-146">包 Id 可用</span><span class="sxs-lookup"><span data-stu-id="8603a-146">The package IDs available</span></span>

<span data-ttu-id="8603a-147">中的字符串`versions`所有小写数组，[规范化 NuGet 版本字符串](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="8603a-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="8603a-148">版本字符串不包含任何 SemVer 2.0.0 生成元数据。</span><span class="sxs-lookup"><span data-stu-id="8603a-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="8603a-149">目的是，在此数组中找到的版本字符串可用于按原义`LOWER_VERSION`以下终结点中找到的令牌。</span><span class="sxs-lookup"><span data-stu-id="8603a-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="8603a-150">示例请求</span><span class="sxs-lookup"><span data-stu-id="8603a-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="8603a-151">示例响应</span><span class="sxs-lookup"><span data-stu-id="8603a-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="8603a-152">下载包内容 (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="8603a-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="8603a-153">如果客户端知道包 ID 和版本，并且想要下载包内容，只需构造以下 URL:</span><span class="sxs-lookup"><span data-stu-id="8603a-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="8603a-154">请求参数</span><span class="sxs-lookup"><span data-stu-id="8603a-154">Request parameters</span></span>

<span data-ttu-id="8603a-155">名称</span><span class="sxs-lookup"><span data-stu-id="8603a-155">Name</span></span>          | <span data-ttu-id="8603a-156">内</span><span class="sxs-lookup"><span data-stu-id="8603a-156">In</span></span>     | <span data-ttu-id="8603a-157">类型</span><span class="sxs-lookup"><span data-stu-id="8603a-157">Type</span></span>   | <span data-ttu-id="8603a-158">必需</span><span class="sxs-lookup"><span data-stu-id="8603a-158">Required</span></span> | <span data-ttu-id="8603a-159">说明</span><span class="sxs-lookup"><span data-stu-id="8603a-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="8603a-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="8603a-160">LOWER_ID</span></span>      | <span data-ttu-id="8603a-161">URL</span><span class="sxs-lookup"><span data-stu-id="8603a-161">URL</span></span>    | <span data-ttu-id="8603a-162">字符串</span><span class="sxs-lookup"><span data-stu-id="8603a-162">string</span></span> | <span data-ttu-id="8603a-163">是</span><span class="sxs-lookup"><span data-stu-id="8603a-163">yes</span></span>      | <span data-ttu-id="8603a-164">包 ID 小写</span><span class="sxs-lookup"><span data-stu-id="8603a-164">The package ID, lowercase</span></span>
<span data-ttu-id="8603a-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="8603a-165">LOWER_VERSION</span></span> | <span data-ttu-id="8603a-166">URL</span><span class="sxs-lookup"><span data-stu-id="8603a-166">URL</span></span>    | <span data-ttu-id="8603a-167">字符串</span><span class="sxs-lookup"><span data-stu-id="8603a-167">string</span></span> | <span data-ttu-id="8603a-168">是</span><span class="sxs-lookup"><span data-stu-id="8603a-168">yes</span></span>      | <span data-ttu-id="8603a-169">包版本、 规范化和小写</span><span class="sxs-lookup"><span data-stu-id="8603a-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="8603a-170">同时`LOWER_ID`和`LOWER_VERSION`小写使用由实现的规则。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="8603a-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="8603a-171">`LOWER_VERSION`所需的包版本进行了规范化使用 NuGet 的版本[规范化规则](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="8603a-171">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="8603a-172">这意味着必须在此情况下排除 SemVer 2.0.0 规范允许该生成元数据。</span><span class="sxs-lookup"><span data-stu-id="8603a-172">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="8603a-173">响应正文</span><span class="sxs-lookup"><span data-stu-id="8603a-173">Response body</span></span>

<span data-ttu-id="8603a-174">如果包存在对包源，则返回状态代码 200。</span><span class="sxs-lookup"><span data-stu-id="8603a-174">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="8603a-175">响应正文将包内容本身。</span><span class="sxs-lookup"><span data-stu-id="8603a-175">The response body will be the package content itself.</span></span>

<span data-ttu-id="8603a-176">如果包不存在对包源，则返回状态代码 404。</span><span class="sxs-lookup"><span data-stu-id="8603a-176">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="8603a-177">示例请求</span><span class="sxs-lookup"><span data-stu-id="8603a-177">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="8603a-178">示例响应</span><span class="sxs-lookup"><span data-stu-id="8603a-178">Sample response</span></span>

<span data-ttu-id="8603a-179">Newtonsoft.Json 9.0.1.nupkg 二进制流。</span><span class="sxs-lookup"><span data-stu-id="8603a-179">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="8603a-180">下载包清单 (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="8603a-180">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="8603a-181">如果客户端知道包 ID 和版本，并且想要下载包清单，只需构造以下 URL:</span><span class="sxs-lookup"><span data-stu-id="8603a-181">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="8603a-182">请求参数</span><span class="sxs-lookup"><span data-stu-id="8603a-182">Request parameters</span></span>

<span data-ttu-id="8603a-183">名称</span><span class="sxs-lookup"><span data-stu-id="8603a-183">Name</span></span>          | <span data-ttu-id="8603a-184">内</span><span class="sxs-lookup"><span data-stu-id="8603a-184">In</span></span>     | <span data-ttu-id="8603a-185">类型</span><span class="sxs-lookup"><span data-stu-id="8603a-185">Type</span></span>    | <span data-ttu-id="8603a-186">必需</span><span class="sxs-lookup"><span data-stu-id="8603a-186">Required</span></span> | <span data-ttu-id="8603a-187">说明</span><span class="sxs-lookup"><span data-stu-id="8603a-187">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="8603a-188">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="8603a-188">LOWER_ID</span></span>      | <span data-ttu-id="8603a-189">URL</span><span class="sxs-lookup"><span data-stu-id="8603a-189">URL</span></span>    | <span data-ttu-id="8603a-190">字符串</span><span class="sxs-lookup"><span data-stu-id="8603a-190">string</span></span>  | <span data-ttu-id="8603a-191">是</span><span class="sxs-lookup"><span data-stu-id="8603a-191">yes</span></span>      | <span data-ttu-id="8603a-192">包 ID 小写</span><span class="sxs-lookup"><span data-stu-id="8603a-192">The package ID, lowercase</span></span>
<span data-ttu-id="8603a-193">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="8603a-193">LOWER_VERSION</span></span> | <span data-ttu-id="8603a-194">URL</span><span class="sxs-lookup"><span data-stu-id="8603a-194">URL</span></span>    | <span data-ttu-id="8603a-195">整数</span><span class="sxs-lookup"><span data-stu-id="8603a-195">integer</span></span> | <span data-ttu-id="8603a-196">是</span><span class="sxs-lookup"><span data-stu-id="8603a-196">yes</span></span>      | <span data-ttu-id="8603a-197">包版本、 规范化和小写</span><span class="sxs-lookup"><span data-stu-id="8603a-197">The package version, normalized and lowercased</span></span>

<span data-ttu-id="8603a-198">同时`LOWER_ID`和`LOWER_VERSION`小写使用由实现的规则。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="8603a-198">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="8603a-199">`LOWER_VERSION`所需的包版本进行了规范化使用 NuGet 的版本[规范化规则](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="8603a-199">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="8603a-200">这意味着必须在此情况下排除 SemVer 2.0.0 规范允许该生成元数据。</span><span class="sxs-lookup"><span data-stu-id="8603a-200">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="8603a-201">响应正文</span><span class="sxs-lookup"><span data-stu-id="8603a-201">Response body</span></span>

<span data-ttu-id="8603a-202">如果包存在对包源，则返回状态代码 200。</span><span class="sxs-lookup"><span data-stu-id="8603a-202">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="8603a-203">响应正文将包清单，这是包含在相应的.nupkg.nuspec。</span><span class="sxs-lookup"><span data-stu-id="8603a-203">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="8603a-204">.Nuspec 是一个 XML 文档。</span><span class="sxs-lookup"><span data-stu-id="8603a-204">The .nuspec is an XML document.</span></span>

<span data-ttu-id="8603a-205">如果包不存在对包源，则返回状态代码 404。</span><span class="sxs-lookup"><span data-stu-id="8603a-205">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="8603a-206">示例请求</span><span class="sxs-lookup"><span data-stu-id="8603a-206">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="8603a-207">示例响应</span><span class="sxs-lookup"><span data-stu-id="8603a-207">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
