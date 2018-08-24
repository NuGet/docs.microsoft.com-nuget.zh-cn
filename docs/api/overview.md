---
title: NuGet API 的概述
description: NuGet API 是一组 HTTP 终结点，可用于下载包，提取元数据，将发布新的包，等等。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0cb40a640a0bab63a63b3b690a34f1f8cbf7fcb8
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793320"
---
# <a name="nuget-api"></a><span data-ttu-id="4e113-103">NuGet API</span><span class="sxs-lookup"><span data-stu-id="4e113-103">NuGet API</span></span>

<span data-ttu-id="4e113-104">NuGet API 是一组可用于下载包、 提取元数据、 将发布新的包，并执行大多数官方 NuGet 客户端中提供其他操作的 HTTP 终结点。</span><span class="sxs-lookup"><span data-stu-id="4e113-104">The NuGet API is a set of HTTP endpoints that can be used to download packages, fetch metadata, publish new packages, and perform most other operations available in the official NuGet clients.</span></span>

<span data-ttu-id="4e113-105">在 Visual Studio、 nuget.exe 和.NET CLI 中的 NuGet 客户端使用此 API 来执行 NuGet 操作，如[ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore)，在 Visual Studio UI 中，搜索并[ `nuget.exe push` ](../tools/cli-ref-push.md)。</span><span class="sxs-lookup"><span data-stu-id="4e113-105">This API is used by the NuGet client in Visual Studio, nuget.exe, and the .NET CLI to perform NuGet operations such as [`dotnet restore`](/dotnet/articles/core/preview3/tools/dotnet-restore), search in the Visual Studio UI, and [`nuget.exe push`](../tools/cli-ref-push.md).</span></span>

<span data-ttu-id="4e113-106">请注意，在某些情况下，nuget.org 具有由其他包源中不强制执行的附加要求。</span><span class="sxs-lookup"><span data-stu-id="4e113-106">Note in some cases, nuget.org has additional requirements that are not enforced by other package sources.</span></span> <span data-ttu-id="4e113-107">这些差异记录通过[nuget.org 协议](nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="4e113-107">These differences are documented by the [nuget.org Protocols](nuget-protocols.md).</span></span>

<span data-ttu-id="4e113-108">简单枚举和可用 nuget.exe 版本的下载，请参阅[tools.json](tools-json.md)终结点。</span><span class="sxs-lookup"><span data-stu-id="4e113-108">For a simple enumeration and download of available nuget.exe versions, see the [tools.json](tools-json.md) endpoint.</span></span>

## <a name="service-index"></a><span data-ttu-id="4e113-109">服务索引</span><span class="sxs-lookup"><span data-stu-id="4e113-109">Service index</span></span>

<span data-ttu-id="4e113-110">适用于 API 的入口点是一个已知位置中的 JSON 文档。</span><span class="sxs-lookup"><span data-stu-id="4e113-110">The entry point for the API is a JSON document in a well known location.</span></span> <span data-ttu-id="4e113-111">本文档名为**服务索引**。</span><span class="sxs-lookup"><span data-stu-id="4e113-111">This document is called the **service index**.</span></span> <span data-ttu-id="4e113-112">Nuget.org 的服务索引的位置是`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="4e113-112">The location of the service index for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

<span data-ttu-id="4e113-113">此 JSON 文档包含一系列*资源*它提供不同的功能并满足不同的用例。</span><span class="sxs-lookup"><span data-stu-id="4e113-113">This JSON document contains a list of *resources* which provide different functionality and fulfill different use cases.</span></span>

<span data-ttu-id="4e113-114">支持 API 的客户端应接受一个或多个这些服务索引 URL 作为连接到相应的程序包源的方式。</span><span class="sxs-lookup"><span data-stu-id="4e113-114">Clients that support the API should accept one or more of these service index URL as the means of connecting to the respective package sources.</span></span>

<span data-ttu-id="4e113-115">有关服务索引的详细信息，请参阅[其 API 参考](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="4e113-115">For more information about the service index, see [its API reference](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="4e113-116">版本管理</span><span class="sxs-lookup"><span data-stu-id="4e113-116">Versioning</span></span>

<span data-ttu-id="4e113-117">该 API 是 NuGet 的 HTTP 协议版本 3。</span><span class="sxs-lookup"><span data-stu-id="4e113-117">The API is version 3 of NuGet's HTTP protocol.</span></span> <span data-ttu-id="4e113-118">此协议有时称为"V3 API。"</span><span class="sxs-lookup"><span data-stu-id="4e113-118">This protocol is sometimes referred to as "the V3 API."</span></span> <span data-ttu-id="4e113-119">这些引用文档将引用到此版本的协议，简称为"API。"</span><span class="sxs-lookup"><span data-stu-id="4e113-119">These reference documents will refer to this version of the protocol simply as "the API."</span></span>

<span data-ttu-id="4e113-120">指示服务索引的架构版本`version`服务索引中的属性。</span><span class="sxs-lookup"><span data-stu-id="4e113-120">The service index schema version is indicated by the `version` property in the service index.</span></span> <span data-ttu-id="4e113-121">API 要求的版本字符串有主版本号的`3`。</span><span class="sxs-lookup"><span data-stu-id="4e113-121">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="4e113-122">服务索引架构做出非重大更改后，会增加版本字符串的次要版本。</span><span class="sxs-lookup"><span data-stu-id="4e113-122">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="4e113-123">较旧的客户端 (如 nuget.exe 2.x) 不支持 V3 API，并仅支持较旧的 V2 API，本文未提供。</span><span class="sxs-lookup"><span data-stu-id="4e113-123">Older clients (such as nuget.exe 2.x) do not support the V3 API and only support the older V2 API, which is not documented here.</span></span>

<span data-ttu-id="4e113-124">因为它是后一 V2 API，这是由 2.x 版的官方 NuGet 客户端实现的基于 OData 的协议，这种情况下命名 NuGet V3 API。</span><span class="sxs-lookup"><span data-stu-id="4e113-124">The NuGet V3 API is named as such because it's the successor of the V2 API, which was the OData-based protocol implemented by the 2.x version of the official NuGet client.</span></span> <span data-ttu-id="4e113-125">V3 API 首先受官方 NuGet 客户端的 3.0 版本和仍的主要协议最新版本支持通过 NuGet 客户端，4.0 和上。</span><span class="sxs-lookup"><span data-stu-id="4e113-125">The V3 API was first supported by the 3.0 version of the official NuGet client and is still the latest major protocol version supported by the NuGet client, 4.0 and on.</span></span> 

<span data-ttu-id="4e113-126">第一次发布以来，对 API 进行了非重大协议更改。</span><span class="sxs-lookup"><span data-stu-id="4e113-126">Non-breaking protocol changes have been made to the API since it was first release.</span></span>

## <a name="resources-and-schema"></a><span data-ttu-id="4e113-127">资源和架构</span><span class="sxs-lookup"><span data-stu-id="4e113-127">Resources and schema</span></span>

<span data-ttu-id="4e113-128">**服务索引**介绍了各种资源。</span><span class="sxs-lookup"><span data-stu-id="4e113-128">The **service index** describes a variety of resources.</span></span> <span data-ttu-id="4e113-129">当前的受支持的资源集如下所示：</span><span class="sxs-lookup"><span data-stu-id="4e113-129">The current set of supported resources are as follows:</span></span>

<span data-ttu-id="4e113-130">资源名称</span><span class="sxs-lookup"><span data-stu-id="4e113-130">Resource name</span></span>                                                          | <span data-ttu-id="4e113-131">必需</span><span class="sxs-lookup"><span data-stu-id="4e113-131">Required</span></span> | <span data-ttu-id="4e113-132">描述</span><span class="sxs-lookup"><span data-stu-id="4e113-132">Description</span></span>
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | <span data-ttu-id="4e113-133">是</span><span class="sxs-lookup"><span data-stu-id="4e113-133">yes</span></span>      | <span data-ttu-id="4e113-134">推送和删除 （或取消列出） 包。</span><span class="sxs-lookup"><span data-stu-id="4e113-134">Push and delete (or unlist) packages.</span></span>
[`SearchQueryService`](search-query-service-resource.md)               | <span data-ttu-id="4e113-135">是</span><span class="sxs-lookup"><span data-stu-id="4e113-135">yes</span></span>      | <span data-ttu-id="4e113-136">筛选器和搜索的关键字的包。</span><span class="sxs-lookup"><span data-stu-id="4e113-136">Filter and search for packages by keyword.</span></span>
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | <span data-ttu-id="4e113-137">是</span><span class="sxs-lookup"><span data-stu-id="4e113-137">yes</span></span>      | <span data-ttu-id="4e113-138">获取包元数据。</span><span class="sxs-lookup"><span data-stu-id="4e113-138">Get package metadata.</span></span>
[`PackageBaseAddress`](package-base-address-resource.md)               | <span data-ttu-id="4e113-139">是</span><span class="sxs-lookup"><span data-stu-id="4e113-139">yes</span></span>      | <span data-ttu-id="4e113-140">获取包的内容 (.nupkg)。</span><span class="sxs-lookup"><span data-stu-id="4e113-140">Get package content (.nupkg).</span></span>
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | <span data-ttu-id="4e113-141">否</span><span class="sxs-lookup"><span data-stu-id="4e113-141">no</span></span>       | <span data-ttu-id="4e113-142">发现的子字符串的包 Id 和版本。</span><span class="sxs-lookup"><span data-stu-id="4e113-142">Discover package IDs and versions by substring.</span></span>
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | <span data-ttu-id="4e113-143">否</span><span class="sxs-lookup"><span data-stu-id="4e113-143">no</span></span>       | <span data-ttu-id="4e113-144">构造一个 URL 以访问"报告滥用行为"网页。</span><span class="sxs-lookup"><span data-stu-id="4e113-144">Construct a URL to access a "report abuse" web page.</span></span>
[`RepositorySignatures`](repository-signatures-resource.md)            | <span data-ttu-id="4e113-145">否</span><span class="sxs-lookup"><span data-stu-id="4e113-145">no</span></span>       | <span data-ttu-id="4e113-146">获取用于存储库签名的证书。</span><span class="sxs-lookup"><span data-stu-id="4e113-146">Get certificates used for repository signing.</span></span>
[`Catalog`](catalog-resource.md)                                       | <span data-ttu-id="4e113-147">否</span><span class="sxs-lookup"><span data-stu-id="4e113-147">no</span></span>       | <span data-ttu-id="4e113-148">包的所有事件的完整记录。</span><span class="sxs-lookup"><span data-stu-id="4e113-148">Full record of all package events.</span></span>

<span data-ttu-id="4e113-149">一般情况下，使用 JSON API 资源返回的所有非二进制数据进行序列化。</span><span class="sxs-lookup"><span data-stu-id="4e113-149">In general, all non-binary data returned by a API resource are serialized using JSON.</span></span> <span data-ttu-id="4e113-150">该资源的单独定义的服务索引的每个资源返回的响应架构。</span><span class="sxs-lookup"><span data-stu-id="4e113-150">The response schema returned by each resource in the service index is defined individually for that resource.</span></span> <span data-ttu-id="4e113-151">有关每个资源的详细信息，请参阅上面列出的主题。</span><span class="sxs-lookup"><span data-stu-id="4e113-151">For more information about each resource, see the topics listed above.</span></span>

> [!Note]
> <span data-ttu-id="4e113-152">当源不实现`SearchAutocompleteService`应适当地禁用任何自动完成行为。</span><span class="sxs-lookup"><span data-stu-id="4e113-152">When a source does not implement `SearchAutocompleteService` any autocomplete behavior should be disabled gracefully.</span></span> <span data-ttu-id="4e113-153">当`ReportAbuseUriTemplate`未实现，正式的 NuGet 客户端回退到 nuget.org 的报告滥用 URL (通过跟踪[NuGet/Home #4924](https://github.com/NuGet/Home/issues/4924))。</span><span class="sxs-lookup"><span data-stu-id="4e113-153">When `ReportAbuseUriTemplate` is not implemented, the official NuGet client falls back to nuget.org's report abuse URL (tracked by [NuGet/Home#4924](https://github.com/NuGet/Home/issues/4924)).</span></span> <span data-ttu-id="4e113-154">其他客户端可以选择只是不向用户显示报告滥用 URL。</span><span class="sxs-lookup"><span data-stu-id="4e113-154">Other clients may opt to simply not show a report abuse URL to the user.</span></span>

## <a name="timestamps"></a><span data-ttu-id="4e113-155">时间戳</span><span class="sxs-lookup"><span data-stu-id="4e113-155">Timestamps</span></span>

<span data-ttu-id="4e113-156">API 返回的所有时间戳采用 UTC，或使用否则指定[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)表示形式。</span><span class="sxs-lookup"><span data-stu-id="4e113-156">All timestamps returned by the API are UTC or are otherwise specified using [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) representation.</span></span> 

## <a name="http-methods"></a><span data-ttu-id="4e113-157">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="4e113-157">HTTP methods</span></span>

<span data-ttu-id="4e113-158">谓词</span><span class="sxs-lookup"><span data-stu-id="4e113-158">Verb</span></span>   | <span data-ttu-id="4e113-159">使用</span><span class="sxs-lookup"><span data-stu-id="4e113-159">Use</span></span>
------ | -----------
<span data-ttu-id="4e113-160">GET</span><span class="sxs-lookup"><span data-stu-id="4e113-160">GET</span></span>    | <span data-ttu-id="4e113-161">执行只读操作，通常检索数据。</span><span class="sxs-lookup"><span data-stu-id="4e113-161">Performs a read-only operation, typically retrieving data.</span></span>
<span data-ttu-id="4e113-162">HEAD</span><span class="sxs-lookup"><span data-stu-id="4e113-162">HEAD</span></span>   | <span data-ttu-id="4e113-163">提取相应的响应标头`GET`请求。</span><span class="sxs-lookup"><span data-stu-id="4e113-163">Fetches the response headers for the corresponding `GET` request.</span></span>
<span data-ttu-id="4e113-164">PUT</span><span class="sxs-lookup"><span data-stu-id="4e113-164">PUT</span></span>    | <span data-ttu-id="4e113-165">创建一个资源不存在，或如果文件确实存在，对其进行更新。</span><span class="sxs-lookup"><span data-stu-id="4e113-165">Creates a resource that doesn't exist or, if it does exist, updates it.</span></span> <span data-ttu-id="4e113-166">某些资源可能不支持更新。</span><span class="sxs-lookup"><span data-stu-id="4e113-166">Some resources may not support update.</span></span>
<span data-ttu-id="4e113-167">DELETE</span><span class="sxs-lookup"><span data-stu-id="4e113-167">DELETE</span></span> | <span data-ttu-id="4e113-168">删除或取消列出资源。</span><span class="sxs-lookup"><span data-stu-id="4e113-168">Deletes or unlists a resource.</span></span>

## <a name="http-status-codes"></a><span data-ttu-id="4e113-169">HTTP 状态代码</span><span class="sxs-lookup"><span data-stu-id="4e113-169">HTTP status codes</span></span>

<span data-ttu-id="4e113-170">代码</span><span class="sxs-lookup"><span data-stu-id="4e113-170">Code</span></span> | <span data-ttu-id="4e113-171">描述</span><span class="sxs-lookup"><span data-stu-id="4e113-171">Description</span></span>
---- | -----
<span data-ttu-id="4e113-172">200</span><span class="sxs-lookup"><span data-stu-id="4e113-172">200</span></span>  | <span data-ttu-id="4e113-173">如果成功，并且没有响应正文。</span><span class="sxs-lookup"><span data-stu-id="4e113-173">Success, and there is a response body.</span></span>
<span data-ttu-id="4e113-174">201</span><span class="sxs-lookup"><span data-stu-id="4e113-174">201</span></span>  | <span data-ttu-id="4e113-175">已创建成功后和资源。</span><span class="sxs-lookup"><span data-stu-id="4e113-175">Success, and the resource was created.</span></span>
<span data-ttu-id="4e113-176">202</span><span class="sxs-lookup"><span data-stu-id="4e113-176">202</span></span>  | <span data-ttu-id="4e113-177">如果成功，该请求已被接受，但一些工作仍可能是不完整且已完成以异步方式。</span><span class="sxs-lookup"><span data-stu-id="4e113-177">Success, the request has been accepted but some work may still be incomplete and completed asynchronously.</span></span>
<span data-ttu-id="4e113-178">204</span><span class="sxs-lookup"><span data-stu-id="4e113-178">204</span></span>  | <span data-ttu-id="4e113-179">如果成功，但没有任何响应正文。</span><span class="sxs-lookup"><span data-stu-id="4e113-179">Success, but there is no response body.</span></span>
<span data-ttu-id="4e113-180">301</span><span class="sxs-lookup"><span data-stu-id="4e113-180">301</span></span>  | <span data-ttu-id="4e113-181">永久重定向。</span><span class="sxs-lookup"><span data-stu-id="4e113-181">A permanent redirect.</span></span>
<span data-ttu-id="4e113-182">302</span><span class="sxs-lookup"><span data-stu-id="4e113-182">302</span></span>  | <span data-ttu-id="4e113-183">临时重定向。</span><span class="sxs-lookup"><span data-stu-id="4e113-183">A temporary redirect.</span></span>
<span data-ttu-id="4e113-184">400</span><span class="sxs-lookup"><span data-stu-id="4e113-184">400</span></span>  | <span data-ttu-id="4e113-185">在 URL 中或在请求正文中的参数不是有效的。</span><span class="sxs-lookup"><span data-stu-id="4e113-185">The parameters in the URL or in the request body aren't valid.</span></span>
<span data-ttu-id="4e113-186">401</span><span class="sxs-lookup"><span data-stu-id="4e113-186">401</span></span>  | <span data-ttu-id="4e113-187">所提供的凭据均无效。</span><span class="sxs-lookup"><span data-stu-id="4e113-187">The provided credentials are invalid.</span></span>
<span data-ttu-id="4e113-188">403</span><span class="sxs-lookup"><span data-stu-id="4e113-188">403</span></span>  | <span data-ttu-id="4e113-189">给定所提供的凭据不允许操作。</span><span class="sxs-lookup"><span data-stu-id="4e113-189">The action is not allowed given the provided credentials.</span></span>
<span data-ttu-id="4e113-190">404</span><span class="sxs-lookup"><span data-stu-id="4e113-190">404</span></span>  | <span data-ttu-id="4e113-191">请求的资源不存在。</span><span class="sxs-lookup"><span data-stu-id="4e113-191">The requested resource doesn't exist.</span></span>
<span data-ttu-id="4e113-192">409</span><span class="sxs-lookup"><span data-stu-id="4e113-192">409</span></span>  | <span data-ttu-id="4e113-193">请求与现有资源冲突。</span><span class="sxs-lookup"><span data-stu-id="4e113-193">The request conflicts with an existing resource.</span></span>
<span data-ttu-id="4e113-194">500</span><span class="sxs-lookup"><span data-stu-id="4e113-194">500</span></span>  | <span data-ttu-id="4e113-195">服务遇到意外的错误。</span><span class="sxs-lookup"><span data-stu-id="4e113-195">The service has encountered an unexpected error.</span></span>
<span data-ttu-id="4e113-196">503</span><span class="sxs-lookup"><span data-stu-id="4e113-196">503</span></span>  | <span data-ttu-id="4e113-197">此服务暂时不可用。</span><span class="sxs-lookup"><span data-stu-id="4e113-197">The service is temporarily unavailable.</span></span>

<span data-ttu-id="4e113-198">任何`GET`对 API 终结点发出的请求可能返回的 HTTP 重定向 （301 或 302）。</span><span class="sxs-lookup"><span data-stu-id="4e113-198">Any `GET` request made to a API endpoint may return an HTTP redirect (301 or 302).</span></span> <span data-ttu-id="4e113-199">客户端应适当地处理这种重定向通过观察`Location`标头和发出的后续`GET`。</span><span class="sxs-lookup"><span data-stu-id="4e113-199">Clients should gracefully handle such redirects by observing the `Location` header and issuing a subsequent `GET`.</span></span> <span data-ttu-id="4e113-200">有关特定终结点的文档将不显式调用重定向可能会派上用场。</span><span class="sxs-lookup"><span data-stu-id="4e113-200">Documentation concerning specific endpoints will not explicitly call out where redirects may be used.</span></span>

<span data-ttu-id="4e113-201">对于一个 500 级状态代码和客户端可以实现合理的重试机制。</span><span class="sxs-lookup"><span data-stu-id="4e113-201">In the case of a 500-level status code, the client can implement a reasonable retry mechanism.</span></span> <span data-ttu-id="4e113-202">官方 NuGet 客户端时，重试三次遇到任何 500 级状态代码或 TCP/DNS 错误。</span><span class="sxs-lookup"><span data-stu-id="4e113-202">The official NuGet client retries three times when encountering any 500-level status code or TCP/DNS error.</span></span>

## <a name="http-request-headers"></a><span data-ttu-id="4e113-203">HTTP 请求标头</span><span class="sxs-lookup"><span data-stu-id="4e113-203">HTTP request headers</span></span>

<span data-ttu-id="4e113-204">name</span><span class="sxs-lookup"><span data-stu-id="4e113-204">Name</span></span>                     | <span data-ttu-id="4e113-205">描述</span><span class="sxs-lookup"><span data-stu-id="4e113-205">Description</span></span>
------------------------ | -----------
<span data-ttu-id="4e113-206">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="4e113-206">X-NuGet-ApiKey</span></span>           | <span data-ttu-id="4e113-207">所需的推送和删除，请参阅[`PackagePublish`资源](package-publish-resource.md)</span><span class="sxs-lookup"><span data-stu-id="4e113-207">Required for push and delete, see [`PackagePublish` resource](package-publish-resource.md)</span></span>
<span data-ttu-id="4e113-208">X-NuGet-Client-Version</span><span class="sxs-lookup"><span data-stu-id="4e113-208">X-NuGet-Client-Version</span></span>   | <span data-ttu-id="4e113-209">**不推荐使用**并替换为 `X-NuGet-Protocol-Version`</span><span class="sxs-lookup"><span data-stu-id="4e113-209">**Deprecated** and replaced by `X-NuGet-Protocol-Version`</span></span>
<span data-ttu-id="4e113-210">X-NuGet-Protocol-Version</span><span class="sxs-lookup"><span data-stu-id="4e113-210">X-NuGet-Protocol-Version</span></span> | <span data-ttu-id="4e113-211">在某些情况下，仅在 nuget.org 上必需的请参阅[nuget.org 协议](NuGet-Protocols.md)</span><span class="sxs-lookup"><span data-stu-id="4e113-211">Required in certain cases only on nuget.org, see [nuget.org protocols](NuGet-Protocols.md)</span></span>
<span data-ttu-id="4e113-212">X-NuGet-Session-Id</span><span class="sxs-lookup"><span data-stu-id="4e113-212">X-NuGet-Session-Id</span></span>       | <span data-ttu-id="4e113-213">*可选*。</span><span class="sxs-lookup"><span data-stu-id="4e113-213">*Optional*.</span></span> <span data-ttu-id="4e113-214">NuGet 客户端 v4.7 + 标识属于同一个 NuGet 客户端会话的 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="4e113-214">NuGet clients v4.7+ identify HTTP requests that are part of the same NuGet client session.</span></span> <span data-ttu-id="4e113-215">有关`PackageReference`存在还原操作是单个会话 id，对于其他方案，如自动完成，和`packages.config`还原可能有几个不同的会话 id 的由于代码构造的方式。</span><span class="sxs-lookup"><span data-stu-id="4e113-215">For `PackageReference` restore operations there is a single session id, for other scenarios such as auto complete, and `packages.config` restore there may be several different session id's due to how the code is factored.</span></span>

## <a name="authentication"></a><span data-ttu-id="4e113-216">身份验证</span><span class="sxs-lookup"><span data-stu-id="4e113-216">Authentication</span></span>

<span data-ttu-id="4e113-217">身份验证应由要定义的包源实现。</span><span class="sxs-lookup"><span data-stu-id="4e113-217">Authentication is left up to the package source implementation to define.</span></span> <span data-ttu-id="4e113-218">对于 nuget.org，仅`PackagePublish`资源需要通过特殊的 API 密钥标头的身份验证。</span><span class="sxs-lookup"><span data-stu-id="4e113-218">For nuget.org, only the `PackagePublish` resource requires authentication via a special API key header.</span></span> <span data-ttu-id="4e113-219">请参阅[`PackagePublish`资源](package-publish-resource.md)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="4e113-219">See [`PackagePublish` resource](package-publish-resource.md) for details.</span></span>
