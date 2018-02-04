---
title: "包内容，NuGet API |Microsoft 文档"
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
description: "包基址是一个简单接口提取包本身。"
keywords: "NuGet 平面容器、 NuGet 包基址、 NuGet nupkg API，NuGet API 包版本中，NuGet API 未列出的包、 NuGet API 下载 nuspec"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c2e631dc0bba95ac849430d77142f27ef591f741
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="package-content"></a><span data-ttu-id="2fb99-104">包内容</span><span class="sxs-lookup"><span data-stu-id="2fb99-104">Package Content</span></span>

<span data-ttu-id="2fb99-105">就可以生成一个 URL，以提取任意包的内容 （.nupkg 文件） 使用 V3 API。</span><span class="sxs-lookup"><span data-stu-id="2fb99-105">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="2fb99-106">用于提取包内容的资源是`PackageBaseAddress`资源位于[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="2fb99-106">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="2fb99-107">此资源还使发现的所有版本的包，列出或未列出。</span><span class="sxs-lookup"><span data-stu-id="2fb99-107">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="2fb99-108">此资源通常称为为任一的"包基址"或"平面容器"。</span><span class="sxs-lookup"><span data-stu-id="2fb99-108">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="2fb99-109">版本管理</span><span class="sxs-lookup"><span data-stu-id="2fb99-109">Versioning</span></span>

<span data-ttu-id="2fb99-110">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="2fb99-110">The following `@type` value is used:</span></span>

<span data-ttu-id="2fb99-111">@type 值</span><span class="sxs-lookup"><span data-stu-id="2fb99-111">@type value</span></span>              | <span data-ttu-id="2fb99-112">说明</span><span class="sxs-lookup"><span data-stu-id="2fb99-112">Notes</span></span>
------------------------ | -----
<span data-ttu-id="2fb99-113">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="2fb99-113">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="2fb99-114">初始版本</span><span class="sxs-lookup"><span data-stu-id="2fb99-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="2fb99-115">基 URL</span><span class="sxs-lookup"><span data-stu-id="2fb99-115">Base URL</span></span>

<span data-ttu-id="2fb99-116">以下 Api 的基 URL 是值`@id`与前面提到的资源关联的属性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="2fb99-116">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="2fb99-117">在以下文档中，将占位符基本 URL`{@id}`将使用。</span><span class="sxs-lookup"><span data-stu-id="2fb99-117">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2fb99-118">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="2fb99-118">HTTP methods</span></span>

<span data-ttu-id="2fb99-119">HTTP 方法位于注册资源支持的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="2fb99-119">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="2fb99-120">枚举包版本</span><span class="sxs-lookup"><span data-stu-id="2fb99-120">Enumerate package versions</span></span>

<span data-ttu-id="2fb99-121">如果客户端知道包 ID，并想要发现的包版本包源具有可用，客户端可以构造一个可预测的 URL，以枚举所有包版本。</span><span class="sxs-lookup"><span data-stu-id="2fb99-121">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="2fb99-122">此列表是要作为"目录列表"下面所述的内容包 api。</span><span class="sxs-lookup"><span data-stu-id="2fb99-122">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="2fb99-123">此列表包含两个列和未列出的包版本。</span><span class="sxs-lookup"><span data-stu-id="2fb99-123">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="2fb99-124">请求参数</span><span class="sxs-lookup"><span data-stu-id="2fb99-124">Request parameters</span></span>

<span data-ttu-id="2fb99-125">name</span><span class="sxs-lookup"><span data-stu-id="2fb99-125">Name</span></span>     | <span data-ttu-id="2fb99-126">内</span><span class="sxs-lookup"><span data-stu-id="2fb99-126">In</span></span>     | <span data-ttu-id="2fb99-127">类型</span><span class="sxs-lookup"><span data-stu-id="2fb99-127">Type</span></span>    | <span data-ttu-id="2fb99-128">必需</span><span class="sxs-lookup"><span data-stu-id="2fb99-128">Required</span></span> | <span data-ttu-id="2fb99-129">说明</span><span class="sxs-lookup"><span data-stu-id="2fb99-129">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="2fb99-130">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="2fb99-130">LOWER_ID</span></span> | <span data-ttu-id="2fb99-131">URL</span><span class="sxs-lookup"><span data-stu-id="2fb99-131">URL</span></span>    | <span data-ttu-id="2fb99-132">字符串</span><span class="sxs-lookup"><span data-stu-id="2fb99-132">string</span></span>  | <span data-ttu-id="2fb99-133">是</span><span class="sxs-lookup"><span data-stu-id="2fb99-133">yes</span></span>      | <span data-ttu-id="2fb99-134">包 ID 小写</span><span class="sxs-lookup"><span data-stu-id="2fb99-134">The package ID, lowercase</span></span>

<span data-ttu-id="2fb99-135">`LOWER_ID`值是小写使用由实现的规则的所需的包 ID。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="2fb99-135">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="2fb99-136">响应</span><span class="sxs-lookup"><span data-stu-id="2fb99-136">Response</span></span>

<span data-ttu-id="2fb99-137">如果包源具有未提供的包 ID 的版本，则返回状态代码 404。</span><span class="sxs-lookup"><span data-stu-id="2fb99-137">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="2fb99-138">如果包源具有一个或多个版本，则返回状态代码 200。</span><span class="sxs-lookup"><span data-stu-id="2fb99-138">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="2fb99-139">响应正文是具有以下属性的 JSON 对象：</span><span class="sxs-lookup"><span data-stu-id="2fb99-139">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="2fb99-140">name</span><span class="sxs-lookup"><span data-stu-id="2fb99-140">Name</span></span>     | <span data-ttu-id="2fb99-141">类型</span><span class="sxs-lookup"><span data-stu-id="2fb99-141">Type</span></span>             | <span data-ttu-id="2fb99-142">必需</span><span class="sxs-lookup"><span data-stu-id="2fb99-142">Required</span></span> | <span data-ttu-id="2fb99-143">说明</span><span class="sxs-lookup"><span data-stu-id="2fb99-143">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="2fb99-144">版本</span><span class="sxs-lookup"><span data-stu-id="2fb99-144">versions</span></span> | <span data-ttu-id="2fb99-145">字符串数组</span><span class="sxs-lookup"><span data-stu-id="2fb99-145">array of strings</span></span> | <span data-ttu-id="2fb99-146">是</span><span class="sxs-lookup"><span data-stu-id="2fb99-146">yes</span></span>      | <span data-ttu-id="2fb99-147">包 Id 可用</span><span class="sxs-lookup"><span data-stu-id="2fb99-147">The package IDs available</span></span>

<span data-ttu-id="2fb99-148">中的字符串`versions`所有小写数组，[规范化 NuGet 版本字符串](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="2fb99-148">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="2fb99-149">版本字符串不包含任何 SemVer 2.0.0 生成元数据。</span><span class="sxs-lookup"><span data-stu-id="2fb99-149">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="2fb99-150">目的是，在此数组中找到的版本字符串可用于按原义`LOWER_VERSION`以下终结点中找到的令牌。</span><span class="sxs-lookup"><span data-stu-id="2fb99-150">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="2fb99-151">示例请求</span><span class="sxs-lookup"><span data-stu-id="2fb99-151">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="2fb99-152">示例响应</span><span class="sxs-lookup"><span data-stu-id="2fb99-152">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="2fb99-153">下载包内容 (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="2fb99-153">Download package content (.nupkg)</span></span>

<span data-ttu-id="2fb99-154">如果客户端知道包 ID 和版本，并且想要下载包内容，只需构造以下 URL:</span><span class="sxs-lookup"><span data-stu-id="2fb99-154">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="2fb99-155">请求参数</span><span class="sxs-lookup"><span data-stu-id="2fb99-155">Request parameters</span></span>

<span data-ttu-id="2fb99-156">name</span><span class="sxs-lookup"><span data-stu-id="2fb99-156">Name</span></span>          | <span data-ttu-id="2fb99-157">内</span><span class="sxs-lookup"><span data-stu-id="2fb99-157">In</span></span>     | <span data-ttu-id="2fb99-158">类型</span><span class="sxs-lookup"><span data-stu-id="2fb99-158">Type</span></span>   | <span data-ttu-id="2fb99-159">必需</span><span class="sxs-lookup"><span data-stu-id="2fb99-159">Required</span></span> | <span data-ttu-id="2fb99-160">说明</span><span class="sxs-lookup"><span data-stu-id="2fb99-160">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2fb99-161">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="2fb99-161">LOWER_ID</span></span>      | <span data-ttu-id="2fb99-162">URL</span><span class="sxs-lookup"><span data-stu-id="2fb99-162">URL</span></span>    | <span data-ttu-id="2fb99-163">字符串</span><span class="sxs-lookup"><span data-stu-id="2fb99-163">string</span></span> | <span data-ttu-id="2fb99-164">是</span><span class="sxs-lookup"><span data-stu-id="2fb99-164">yes</span></span>      | <span data-ttu-id="2fb99-165">包 ID 小写</span><span class="sxs-lookup"><span data-stu-id="2fb99-165">The package ID, lowercase</span></span>
<span data-ttu-id="2fb99-166">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="2fb99-166">LOWER_VERSION</span></span> | <span data-ttu-id="2fb99-167">URL</span><span class="sxs-lookup"><span data-stu-id="2fb99-167">URL</span></span>    | <span data-ttu-id="2fb99-168">字符串</span><span class="sxs-lookup"><span data-stu-id="2fb99-168">string</span></span> | <span data-ttu-id="2fb99-169">是</span><span class="sxs-lookup"><span data-stu-id="2fb99-169">yes</span></span>      | <span data-ttu-id="2fb99-170">包版本、 规范化和小写</span><span class="sxs-lookup"><span data-stu-id="2fb99-170">The package version, normalized and lowercased</span></span>

<span data-ttu-id="2fb99-171">同时`LOWER_ID`和`LOWER_VERSION`小写使用由实现的规则。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="2fb99-171">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="2fb99-172">`LOWER_VERSION`所需的包版本进行了规范化使用 NuGet 的版本[规范化规则](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="2fb99-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="2fb99-173">这意味着必须在此情况下排除 SemVer 2.0.0 规范允许该生成元数据。</span><span class="sxs-lookup"><span data-stu-id="2fb99-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="2fb99-174">响应正文</span><span class="sxs-lookup"><span data-stu-id="2fb99-174">Response body</span></span>

<span data-ttu-id="2fb99-175">如果包存在对包源，则返回状态代码 200。</span><span class="sxs-lookup"><span data-stu-id="2fb99-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="2fb99-176">响应正文将包内容本身。</span><span class="sxs-lookup"><span data-stu-id="2fb99-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="2fb99-177">如果包不存在对包源，则返回状态代码 404。</span><span class="sxs-lookup"><span data-stu-id="2fb99-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="2fb99-178">示例请求</span><span class="sxs-lookup"><span data-stu-id="2fb99-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="2fb99-179">示例响应</span><span class="sxs-lookup"><span data-stu-id="2fb99-179">Sample response</span></span>

<span data-ttu-id="2fb99-180">Newtonsoft.Json 9.0.1.nupkg 二进制流。</span><span class="sxs-lookup"><span data-stu-id="2fb99-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="2fb99-181">下载包清单 (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="2fb99-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="2fb99-182">如果客户端知道包 ID 和版本，并且想要下载包清单，只需构造以下 URL:</span><span class="sxs-lookup"><span data-stu-id="2fb99-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="2fb99-183">请求参数</span><span class="sxs-lookup"><span data-stu-id="2fb99-183">Request parameters</span></span>

<span data-ttu-id="2fb99-184">name</span><span class="sxs-lookup"><span data-stu-id="2fb99-184">Name</span></span>          | <span data-ttu-id="2fb99-185">内</span><span class="sxs-lookup"><span data-stu-id="2fb99-185">In</span></span>     | <span data-ttu-id="2fb99-186">类型</span><span class="sxs-lookup"><span data-stu-id="2fb99-186">Type</span></span>    | <span data-ttu-id="2fb99-187">必需</span><span class="sxs-lookup"><span data-stu-id="2fb99-187">Required</span></span> | <span data-ttu-id="2fb99-188">说明</span><span class="sxs-lookup"><span data-stu-id="2fb99-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="2fb99-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="2fb99-189">LOWER_ID</span></span>      | <span data-ttu-id="2fb99-190">URL</span><span class="sxs-lookup"><span data-stu-id="2fb99-190">URL</span></span>    | <span data-ttu-id="2fb99-191">字符串</span><span class="sxs-lookup"><span data-stu-id="2fb99-191">string</span></span>  | <span data-ttu-id="2fb99-192">是</span><span class="sxs-lookup"><span data-stu-id="2fb99-192">yes</span></span>      | <span data-ttu-id="2fb99-193">包 ID 小写</span><span class="sxs-lookup"><span data-stu-id="2fb99-193">The package ID, lowercase</span></span>
<span data-ttu-id="2fb99-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="2fb99-194">LOWER_VERSION</span></span> | <span data-ttu-id="2fb99-195">URL</span><span class="sxs-lookup"><span data-stu-id="2fb99-195">URL</span></span>    | <span data-ttu-id="2fb99-196">整数</span><span class="sxs-lookup"><span data-stu-id="2fb99-196">integer</span></span> | <span data-ttu-id="2fb99-197">是</span><span class="sxs-lookup"><span data-stu-id="2fb99-197">yes</span></span>      | <span data-ttu-id="2fb99-198">包版本、 规范化和小写</span><span class="sxs-lookup"><span data-stu-id="2fb99-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="2fb99-199">同时`LOWER_ID`和`LOWER_VERSION`小写使用由实现的规则。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="2fb99-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="2fb99-200">`LOWER_VERSION`所需的包版本进行了规范化使用 NuGet 的版本[规范化规则](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="2fb99-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="2fb99-201">这意味着必须在此情况下排除 SemVer 2.0.0 规范允许该生成元数据。</span><span class="sxs-lookup"><span data-stu-id="2fb99-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="2fb99-202">响应正文</span><span class="sxs-lookup"><span data-stu-id="2fb99-202">Response body</span></span>

<span data-ttu-id="2fb99-203">如果包存在对包源，则返回状态代码 200。</span><span class="sxs-lookup"><span data-stu-id="2fb99-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="2fb99-204">响应正文将包清单，这是包含在相应的.nupkg.nuspec。</span><span class="sxs-lookup"><span data-stu-id="2fb99-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="2fb99-205">.Nuspec 是一个 XML 文档。</span><span class="sxs-lookup"><span data-stu-id="2fb99-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="2fb99-206">如果包不存在对包源，则返回状态代码 404。</span><span class="sxs-lookup"><span data-stu-id="2fb99-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="2fb99-207">示例请求</span><span class="sxs-lookup"><span data-stu-id="2fb99-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="2fb99-208">示例响应</span><span class="sxs-lookup"><span data-stu-id="2fb99-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
