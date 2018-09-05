---
title: 包的内容，NuGet API
description: 包基址是提取包本身的一个简单接口。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 740defc34077793b81fb35db73a2eee393ae3bac
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547149"
---
# <a name="package-content"></a><span data-ttu-id="92877-103">包内容</span><span class="sxs-lookup"><span data-stu-id="92877-103">Package Content</span></span>

<span data-ttu-id="92877-104">就可以生成用于提取任意包的内容 （.nupkg 文件） 使用 V3 API 的 URL。</span><span class="sxs-lookup"><span data-stu-id="92877-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="92877-105">用于提取包内容的资源是`PackageBaseAddress`资源中找到[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="92877-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="92877-106">此资源还允许包，列出的所有版本的发现或未列出。</span><span class="sxs-lookup"><span data-stu-id="92877-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="92877-107">此资源通常称为与任一"包基址"或"平面容器"。</span><span class="sxs-lookup"><span data-stu-id="92877-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="92877-108">版本管理</span><span class="sxs-lookup"><span data-stu-id="92877-108">Versioning</span></span>

<span data-ttu-id="92877-109">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="92877-109">The following `@type` value is used:</span></span>

<span data-ttu-id="92877-110">@type 值</span><span class="sxs-lookup"><span data-stu-id="92877-110">@type value</span></span>              | <span data-ttu-id="92877-111">说明</span><span class="sxs-lookup"><span data-stu-id="92877-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="92877-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="92877-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="92877-113">初始版本</span><span class="sxs-lookup"><span data-stu-id="92877-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="92877-114">基 URL</span><span class="sxs-lookup"><span data-stu-id="92877-114">Base URL</span></span>

<span data-ttu-id="92877-115">以下 Api 的基 URL 是的值`@id`属性与前面提到的资源相关联`@type`值。</span><span class="sxs-lookup"><span data-stu-id="92877-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="92877-116">在以下文档中，占位符基 URL`{@id}`将使用。</span><span class="sxs-lookup"><span data-stu-id="92877-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="92877-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="92877-117">HTTP methods</span></span>

<span data-ttu-id="92877-118">中的注册资源支持的 HTTP 方法找到的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="92877-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="92877-119">枚举的包版本</span><span class="sxs-lookup"><span data-stu-id="92877-119">Enumerate package versions</span></span>

<span data-ttu-id="92877-120">如果客户端知道包 ID，并想要发现的包版本包源具有可用，客户端可以构建一个可预测的 URL 来枚举所有包版本。</span><span class="sxs-lookup"><span data-stu-id="92877-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="92877-121">下面所述的内容包 API 的情况下，此列表应为"目录列表"。</span><span class="sxs-lookup"><span data-stu-id="92877-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="92877-122">此列表包含这两个列出和取消列出包版本。</span><span class="sxs-lookup"><span data-stu-id="92877-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="92877-123">请求参数</span><span class="sxs-lookup"><span data-stu-id="92877-123">Request parameters</span></span>

<span data-ttu-id="92877-124">name</span><span class="sxs-lookup"><span data-stu-id="92877-124">Name</span></span>     | <span data-ttu-id="92877-125">内</span><span class="sxs-lookup"><span data-stu-id="92877-125">In</span></span>     | <span data-ttu-id="92877-126">类型</span><span class="sxs-lookup"><span data-stu-id="92877-126">Type</span></span>    | <span data-ttu-id="92877-127">必需</span><span class="sxs-lookup"><span data-stu-id="92877-127">Required</span></span> | <span data-ttu-id="92877-128">说明</span><span class="sxs-lookup"><span data-stu-id="92877-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="92877-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="92877-129">LOWER_ID</span></span> | <span data-ttu-id="92877-130">URL</span><span class="sxs-lookup"><span data-stu-id="92877-130">URL</span></span>    | <span data-ttu-id="92877-131">字符串</span><span class="sxs-lookup"><span data-stu-id="92877-131">string</span></span>  | <span data-ttu-id="92877-132">是</span><span class="sxs-lookup"><span data-stu-id="92877-132">yes</span></span>      | <span data-ttu-id="92877-133">包 ID 小写</span><span class="sxs-lookup"><span data-stu-id="92877-133">The package ID, lowercase</span></span>

<span data-ttu-id="92877-134">`LOWER_ID`值是小写使用通过实施的规则的所需的包 ID。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="92877-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="92877-135">响应</span><span class="sxs-lookup"><span data-stu-id="92877-135">Response</span></span>

<span data-ttu-id="92877-136">如果包源不具有提供的包 ID 的任何版本，则返回 404 状态代码。</span><span class="sxs-lookup"><span data-stu-id="92877-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="92877-137">如果包源具有一个或多个版本，则返回 200 状态代码。</span><span class="sxs-lookup"><span data-stu-id="92877-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="92877-138">响应正文是使用下面的属性的 JSON 对象：</span><span class="sxs-lookup"><span data-stu-id="92877-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="92877-139">name</span><span class="sxs-lookup"><span data-stu-id="92877-139">Name</span></span>     | <span data-ttu-id="92877-140">类型</span><span class="sxs-lookup"><span data-stu-id="92877-140">Type</span></span>             | <span data-ttu-id="92877-141">必需</span><span class="sxs-lookup"><span data-stu-id="92877-141">Required</span></span> | <span data-ttu-id="92877-142">说明</span><span class="sxs-lookup"><span data-stu-id="92877-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="92877-143">版本</span><span class="sxs-lookup"><span data-stu-id="92877-143">versions</span></span> | <span data-ttu-id="92877-144">字符串数组</span><span class="sxs-lookup"><span data-stu-id="92877-144">array of strings</span></span> | <span data-ttu-id="92877-145">是</span><span class="sxs-lookup"><span data-stu-id="92877-145">yes</span></span>      | <span data-ttu-id="92877-146">包 Id 可用</span><span class="sxs-lookup"><span data-stu-id="92877-146">The package IDs available</span></span>

<span data-ttu-id="92877-147">中的字符串`versions`所有小写数组，[规范化 NuGet 版本字符串](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="92877-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="92877-148">版本字符串不包含任何 SemVer 2.0.0 生成元数据。</span><span class="sxs-lookup"><span data-stu-id="92877-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="92877-149">目的是，在此数组中找到的版本字符串可用于按原义`LOWER_VERSION`以下终结点中找到令牌。</span><span class="sxs-lookup"><span data-stu-id="92877-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="92877-150">示例请求</span><span class="sxs-lookup"><span data-stu-id="92877-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="92877-151">示例响应</span><span class="sxs-lookup"><span data-stu-id="92877-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="92877-152">下载包内容 (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="92877-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="92877-153">如果客户端知道包 ID 和版本，并且想要下载包内容，只需构造以下 URL:</span><span class="sxs-lookup"><span data-stu-id="92877-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="92877-154">请求参数</span><span class="sxs-lookup"><span data-stu-id="92877-154">Request parameters</span></span>

<span data-ttu-id="92877-155">name</span><span class="sxs-lookup"><span data-stu-id="92877-155">Name</span></span>          | <span data-ttu-id="92877-156">内</span><span class="sxs-lookup"><span data-stu-id="92877-156">In</span></span>     | <span data-ttu-id="92877-157">类型</span><span class="sxs-lookup"><span data-stu-id="92877-157">Type</span></span>   | <span data-ttu-id="92877-158">必需</span><span class="sxs-lookup"><span data-stu-id="92877-158">Required</span></span> | <span data-ttu-id="92877-159">说明</span><span class="sxs-lookup"><span data-stu-id="92877-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="92877-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="92877-160">LOWER_ID</span></span>      | <span data-ttu-id="92877-161">URL</span><span class="sxs-lookup"><span data-stu-id="92877-161">URL</span></span>    | <span data-ttu-id="92877-162">字符串</span><span class="sxs-lookup"><span data-stu-id="92877-162">string</span></span> | <span data-ttu-id="92877-163">是</span><span class="sxs-lookup"><span data-stu-id="92877-163">yes</span></span>      | <span data-ttu-id="92877-164">包 ID 小写</span><span class="sxs-lookup"><span data-stu-id="92877-164">The package ID, lowercase</span></span>
<span data-ttu-id="92877-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="92877-165">LOWER_VERSION</span></span> | <span data-ttu-id="92877-166">URL</span><span class="sxs-lookup"><span data-stu-id="92877-166">URL</span></span>    | <span data-ttu-id="92877-167">字符串</span><span class="sxs-lookup"><span data-stu-id="92877-167">string</span></span> | <span data-ttu-id="92877-168">是</span><span class="sxs-lookup"><span data-stu-id="92877-168">yes</span></span>      | <span data-ttu-id="92877-169">包版本中，规范化和小写</span><span class="sxs-lookup"><span data-stu-id="92877-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="92877-170">这两`LOWER_ID`和`LOWER_VERSION`小写使用通过实施的规则。NET 的 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="92877-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="92877-171">方法。</span><span class="sxs-lookup"><span data-stu-id="92877-171">method.</span></span>

<span data-ttu-id="92877-172">`LOWER_VERSION`所需的包版本规范化使用 NuGet 的版本[规范化规则](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="92877-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="92877-173">这意味着必须在这种情况下排除允许的 SemVer 2.0.0 规范的生成元数据。</span><span class="sxs-lookup"><span data-stu-id="92877-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="92877-174">响应正文</span><span class="sxs-lookup"><span data-stu-id="92877-174">Response body</span></span>

<span data-ttu-id="92877-175">如果包存在于包源，则返回 200 状态代码。</span><span class="sxs-lookup"><span data-stu-id="92877-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="92877-176">响应正文将为包内容本身。</span><span class="sxs-lookup"><span data-stu-id="92877-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="92877-177">如果包不存在对包源，则返回 404 状态代码。</span><span class="sxs-lookup"><span data-stu-id="92877-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="92877-178">示例请求</span><span class="sxs-lookup"><span data-stu-id="92877-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="92877-179">示例响应</span><span class="sxs-lookup"><span data-stu-id="92877-179">Sample response</span></span>

<span data-ttu-id="92877-180">Newtonsoft.Json 9.0.1.nupkg 二进制流。</span><span class="sxs-lookup"><span data-stu-id="92877-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="92877-181">下载包清单 (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="92877-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="92877-182">如果客户端知道包 ID 和版本，并且想要下载包清单，只需构造以下 URL:</span><span class="sxs-lookup"><span data-stu-id="92877-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="92877-183">请求参数</span><span class="sxs-lookup"><span data-stu-id="92877-183">Request parameters</span></span>

<span data-ttu-id="92877-184">name</span><span class="sxs-lookup"><span data-stu-id="92877-184">Name</span></span>          | <span data-ttu-id="92877-185">内</span><span class="sxs-lookup"><span data-stu-id="92877-185">In</span></span>     | <span data-ttu-id="92877-186">类型</span><span class="sxs-lookup"><span data-stu-id="92877-186">Type</span></span>    | <span data-ttu-id="92877-187">必需</span><span class="sxs-lookup"><span data-stu-id="92877-187">Required</span></span> | <span data-ttu-id="92877-188">说明</span><span class="sxs-lookup"><span data-stu-id="92877-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="92877-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="92877-189">LOWER_ID</span></span>      | <span data-ttu-id="92877-190">URL</span><span class="sxs-lookup"><span data-stu-id="92877-190">URL</span></span>    | <span data-ttu-id="92877-191">字符串</span><span class="sxs-lookup"><span data-stu-id="92877-191">string</span></span>  | <span data-ttu-id="92877-192">是</span><span class="sxs-lookup"><span data-stu-id="92877-192">yes</span></span>      | <span data-ttu-id="92877-193">包 ID 小写</span><span class="sxs-lookup"><span data-stu-id="92877-193">The package ID, lowercase</span></span>
<span data-ttu-id="92877-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="92877-194">LOWER_VERSION</span></span> | <span data-ttu-id="92877-195">URL</span><span class="sxs-lookup"><span data-stu-id="92877-195">URL</span></span>    | <span data-ttu-id="92877-196">整数</span><span class="sxs-lookup"><span data-stu-id="92877-196">integer</span></span> | <span data-ttu-id="92877-197">是</span><span class="sxs-lookup"><span data-stu-id="92877-197">yes</span></span>      | <span data-ttu-id="92877-198">包版本中，规范化和小写</span><span class="sxs-lookup"><span data-stu-id="92877-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="92877-199">这两`LOWER_ID`和`LOWER_VERSION`小写使用通过实施的规则。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="92877-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="92877-200">`LOWER_VERSION`所需的包版本规范化使用 NuGet 的版本[规范化规则](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="92877-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="92877-201">这意味着必须在这种情况下排除允许的 SemVer 2.0.0 规范的生成元数据。</span><span class="sxs-lookup"><span data-stu-id="92877-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="92877-202">响应正文</span><span class="sxs-lookup"><span data-stu-id="92877-202">Response body</span></span>

<span data-ttu-id="92877-203">如果包存在于包源，则返回 200 状态代码。</span><span class="sxs-lookup"><span data-stu-id="92877-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="92877-204">响应正文将为包清单，其中是包含在相应的.nupkg.nuspec。</span><span class="sxs-lookup"><span data-stu-id="92877-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="92877-205">.Nuspec 是一个 XML 文档。</span><span class="sxs-lookup"><span data-stu-id="92877-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="92877-206">如果包不存在对包源，则返回 404 状态代码。</span><span class="sxs-lookup"><span data-stu-id="92877-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="92877-207">示例请求</span><span class="sxs-lookup"><span data-stu-id="92877-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="92877-208">示例响应</span><span class="sxs-lookup"><span data-stu-id="92877-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
