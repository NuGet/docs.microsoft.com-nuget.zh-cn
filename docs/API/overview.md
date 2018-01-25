---
title: "概述、 NuGet API |Microsoft 文档"
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
description: "NuGet API 是一组可用于下载包，提取元数据，发布新的包等的 HTTP 终结点。"
keywords: "NuGet V3 API、 NuGet V2 API、 NuGet JSON、 NuGet 注册 API，NuGet API 平面容器、 NuGet nupkg API、 NuGet 元数据 API、 NuGet 搜索 API、 NuGet 推送 API，NuGe 发布 API，NuGet 删除 API，NuGet 不列出 API，NuGet 协议"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c28b0912be6dbccab06078100cb71821c3658e08
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-api"></a><span data-ttu-id="89e1b-104">NuGet API</span><span class="sxs-lookup"><span data-stu-id="89e1b-104">NuGet API</span></span>

<span data-ttu-id="89e1b-105">NuGet API 是一套用于下载包、 提取元数据、 发布新的程序包和执行大多数官方 NuGet 客户端中提供其他操作的 HTTP 终结点。</span><span class="sxs-lookup"><span data-stu-id="89e1b-105">The NuGet API is a set of HTTP endpoints that can be used to download packages, fetch metadata, publish new packages, and perform most other operations available in the official NuGet clients.</span></span>

<span data-ttu-id="89e1b-106">在 Visual Studio、 nuget.exe 和.NET CLI NuGet 客户端使用此 API 执行 NuGet 操作如[ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore)，在 Visual Studio UI 中，搜索和[ `nuget.exe push` ](../tools/cli-ref-push.md)。</span><span class="sxs-lookup"><span data-stu-id="89e1b-106">This API is used by the NuGet client in Visual Studio, nuget.exe, and the .NET CLI to perform NuGet operations such as [`dotnet restore`](/dotnet/articles/core/preview3/tools/dotnet-restore), search in the Visual Studio UI, and [`nuget.exe push`](../tools/cli-ref-push.md).</span></span>

<span data-ttu-id="89e1b-107">请注意，在某些情况下，nuget.org 具有由其他包源中不强制执行的附加要求。</span><span class="sxs-lookup"><span data-stu-id="89e1b-107">Note in some cases, nuget.org has additional requirements that are not enforced by other package sources.</span></span> <span data-ttu-id="89e1b-108">这些差异记录通过[nuget.org 协议](nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="89e1b-108">These differences are documented by the [nuget.org Protocols](nuget-protocols.md).</span></span>

## <a name="service-index"></a><span data-ttu-id="89e1b-109">服务索引</span><span class="sxs-lookup"><span data-stu-id="89e1b-109">Service index</span></span>

<span data-ttu-id="89e1b-110">API 的入口点是一个已知位置中的 JSON 文档。</span><span class="sxs-lookup"><span data-stu-id="89e1b-110">The entry point for the API is a JSON document in a well known location.</span></span> <span data-ttu-id="89e1b-111">此文档被称为**服务索引**。</span><span class="sxs-lookup"><span data-stu-id="89e1b-111">This document is called the **service index**.</span></span>
<span data-ttu-id="89e1b-112">Nuget.org 的服务索引的位置是`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="89e1b-112">The location of the service index for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

<span data-ttu-id="89e1b-113">此 JSON 文档包含的列表*资源*其提供不同的功能和满足不同用例。</span><span class="sxs-lookup"><span data-stu-id="89e1b-113">This JSON document contains a list of *resources* which provide different functionality and fulfill different use cases.</span></span>

<span data-ttu-id="89e1b-114">支持 API 的客户端应接受一个或多个这些服务索引 URL 作为连接到相应的程序包源的方法。</span><span class="sxs-lookup"><span data-stu-id="89e1b-114">Clients that support the API should accept one or more of these service index URL as the means of connecting to the respective package sources.</span></span>

<span data-ttu-id="89e1b-115">服务索引有关的详细信息，请参阅[其 API 参考](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="89e1b-115">For more information about the service index, see [its API reference](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="89e1b-116">版本管理</span><span class="sxs-lookup"><span data-stu-id="89e1b-116">Versioning</span></span>

<span data-ttu-id="89e1b-117">API 是 NuGet 的 HTTP 协议版本 3。</span><span class="sxs-lookup"><span data-stu-id="89e1b-117">The API is version 3 of NuGet's HTTP protocol.</span></span> <span data-ttu-id="89e1b-118">此协议有时称为"V3 API。"</span><span class="sxs-lookup"><span data-stu-id="89e1b-118">This protocol is sometimes referred to as "the V3 API."</span></span> <span data-ttu-id="89e1b-119">这些引用文档将引用到此版本的协议，只需作为"API。"</span><span class="sxs-lookup"><span data-stu-id="89e1b-119">These reference documents will refer to this version of the protocol simply as "the API."</span></span>

<span data-ttu-id="89e1b-120">服务索引架构版本将由`version`服务索引中的属性。</span><span class="sxs-lookup"><span data-stu-id="89e1b-120">The service index schema version is indicated by the `version` property in the service index.</span></span> <span data-ttu-id="89e1b-121">API 规定的版本字符串有的一个主要版本号`3`。</span><span class="sxs-lookup"><span data-stu-id="89e1b-121">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="89e1b-122">对服务索引架构进行非重大更改时，将增加的版本字符串的次要版本。</span><span class="sxs-lookup"><span data-stu-id="89e1b-122">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="89e1b-123">旧版客户端 (如 nuget.exe 2.x) 不支持 V3 API，并仅支持较旧的 V2 API 未在此处介绍。</span><span class="sxs-lookup"><span data-stu-id="89e1b-123">Older clients (such as nuget.exe 2.x) do not support the V3 API and only support the older V2 API, which is not documented here.</span></span>

<span data-ttu-id="89e1b-124">因为它是 V2 API 的后继版本这是由官方 NuGet 客户端 2.x 版本实现的基于 OData 的协议，因此命名 NuGet V3 API。</span><span class="sxs-lookup"><span data-stu-id="89e1b-124">The NuGet V3 API is named as such because it's the successor of the V2 API, which was the OData-based protocol implemented by the 2.x version of the official NuGet client.</span></span> <span data-ttu-id="89e1b-125">V3 API 首先受正式 NuGet 客户端的 3.0 版本和仍的最新主要协议版本支持通过 NuGet 客户端，4.0，在。</span><span class="sxs-lookup"><span data-stu-id="89e1b-125">The V3 API was first supported by the 3.0 version of the official NuGet client and is still the latest major protocol version supported by the NuGet client, 4.0 and on.</span></span> 

<span data-ttu-id="89e1b-126">第一次发布以来，对 API 进行了非重大协议更改。</span><span class="sxs-lookup"><span data-stu-id="89e1b-126">Non-breaking protocol changes have been made to the API since it was first release.</span></span>

## <a name="resources-and-schema"></a><span data-ttu-id="89e1b-127">资源和架构</span><span class="sxs-lookup"><span data-stu-id="89e1b-127">Resources and schema</span></span>

<span data-ttu-id="89e1b-128">**服务索引**介绍各种资源。</span><span class="sxs-lookup"><span data-stu-id="89e1b-128">The **service index** describes a variety of resources.</span></span> <span data-ttu-id="89e1b-129">当前的受支持的资源集如下所示：</span><span class="sxs-lookup"><span data-stu-id="89e1b-129">The current set of supported resources are as follows:</span></span>

<span data-ttu-id="89e1b-130">资源名称</span><span class="sxs-lookup"><span data-stu-id="89e1b-130">Resource name</span></span>                                                          | <span data-ttu-id="89e1b-131">必需</span><span class="sxs-lookup"><span data-stu-id="89e1b-131">Required</span></span> | <span data-ttu-id="89e1b-132">描述</span><span class="sxs-lookup"><span data-stu-id="89e1b-132">Description</span></span>
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | <span data-ttu-id="89e1b-133">是</span><span class="sxs-lookup"><span data-stu-id="89e1b-133">yes</span></span>      | <span data-ttu-id="89e1b-134">推送和删除 （或不列出） 包。</span><span class="sxs-lookup"><span data-stu-id="89e1b-134">Push and delete (or unlist) packages.</span></span>
[`SearchQueryService`](search-query-service-resource.md)               | <span data-ttu-id="89e1b-135">是</span><span class="sxs-lookup"><span data-stu-id="89e1b-135">yes</span></span>      | <span data-ttu-id="89e1b-136">筛选器和搜索的关键字的包。</span><span class="sxs-lookup"><span data-stu-id="89e1b-136">Filter and search for packages by keyword.</span></span>
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | <span data-ttu-id="89e1b-137">是</span><span class="sxs-lookup"><span data-stu-id="89e1b-137">yes</span></span>      | <span data-ttu-id="89e1b-138">获取包元数据。</span><span class="sxs-lookup"><span data-stu-id="89e1b-138">Get package metadata.</span></span>
[`PackageBaseAddress`](package-base-address-resource.md)               | <span data-ttu-id="89e1b-139">是</span><span class="sxs-lookup"><span data-stu-id="89e1b-139">yes</span></span>      | <span data-ttu-id="89e1b-140">获取包的内容 (.nupkg)。</span><span class="sxs-lookup"><span data-stu-id="89e1b-140">Get package content (.nupkg).</span></span>
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | <span data-ttu-id="89e1b-141">否</span><span class="sxs-lookup"><span data-stu-id="89e1b-141">no</span></span>       | <span data-ttu-id="89e1b-142">按子字符串中发现的包 Id 和版本。</span><span class="sxs-lookup"><span data-stu-id="89e1b-142">Discover package IDs and versions by substring.</span></span>
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | <span data-ttu-id="89e1b-143">否</span><span class="sxs-lookup"><span data-stu-id="89e1b-143">no</span></span>       | <span data-ttu-id="89e1b-144">构造访问"报告滥用行为"网页的 URL。</span><span class="sxs-lookup"><span data-stu-id="89e1b-144">Construct a URL to access a "report abuse" web page.</span></span>
[`Catalog`](catalog-resource.md)                                       | <span data-ttu-id="89e1b-145">否</span><span class="sxs-lookup"><span data-stu-id="89e1b-145">no</span></span>       | <span data-ttu-id="89e1b-146">所有包事件的完整记录。</span><span class="sxs-lookup"><span data-stu-id="89e1b-146">Full record of all package events.</span></span>

<span data-ttu-id="89e1b-147">一般情况下，使用 JSON API 资源返回的所有非二进制数据进行序列化。</span><span class="sxs-lookup"><span data-stu-id="89e1b-147">In general, all non-binary data returned by a API resource are serialized using JSON.</span></span> <span data-ttu-id="89e1b-148">为该资源，分别定义了返回服务索引中每个资源的响应架构。</span><span class="sxs-lookup"><span data-stu-id="89e1b-148">The response schema returned by each resource in the service index is defined individually for that resource.</span></span> <span data-ttu-id="89e1b-149">有关每个资源的详细信息，请参阅上面列出的主题。</span><span class="sxs-lookup"><span data-stu-id="89e1b-149">For more information about each resource, see the topics listed above.</span></span>

> [!Note]
> <span data-ttu-id="89e1b-150">当源不实现`SearchAutocompleteService`应正常禁用任何自动完成行为。</span><span class="sxs-lookup"><span data-stu-id="89e1b-150">When a source does not implement `SearchAutocompleteService` any autocomplete behavior should be disabled gracefully.</span></span> <span data-ttu-id="89e1b-151">当`ReportAbuseUriTemplate`未实现，则正式的 NuGet 客户端回退到 nuget.org 的报告滥用行为 URL (通过跟踪[NuGet/主页 #4924](https://github.com/NuGet/Home/issues/4924))。</span><span class="sxs-lookup"><span data-stu-id="89e1b-151">When `ReportAbuseUriTemplate` is not implemented, the official NuGet client falls back to nuget.org's report abuse URL (tracked by [NuGet/Home#4924](https://github.com/NuGet/Home/issues/4924)).</span></span> <span data-ttu-id="89e1b-152">其他客户端可以选择只是不向用户显示报表滥用行为 URL。</span><span class="sxs-lookup"><span data-stu-id="89e1b-152">Other clients may opt to simply not show a report abuse URL to the user.</span></span>

## <a name="timestamps"></a><span data-ttu-id="89e1b-153">时间戳</span><span class="sxs-lookup"><span data-stu-id="89e1b-153">Timestamps</span></span>

<span data-ttu-id="89e1b-154">API 返回的所有时间戳是 UTC，或使用否则指定[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)表示形式。</span><span class="sxs-lookup"><span data-stu-id="89e1b-154">All timestamps returned by the API are UTC or are otherwise specified using [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) representation.</span></span> 

## <a name="http-methods"></a><span data-ttu-id="89e1b-155">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="89e1b-155">HTTP methods</span></span>

<span data-ttu-id="89e1b-156">谓词</span><span class="sxs-lookup"><span data-stu-id="89e1b-156">Verb</span></span>   | <span data-ttu-id="89e1b-157">使用</span><span class="sxs-lookup"><span data-stu-id="89e1b-157">Use</span></span>
------ | -----------
<span data-ttu-id="89e1b-158">GET</span><span class="sxs-lookup"><span data-stu-id="89e1b-158">GET</span></span>    | <span data-ttu-id="89e1b-159">执行只读操作，通常检索数据。</span><span class="sxs-lookup"><span data-stu-id="89e1b-159">Performs a read-only operation, typically retrieving data.</span></span>
<span data-ttu-id="89e1b-160">HEAD</span><span class="sxs-lookup"><span data-stu-id="89e1b-160">HEAD</span></span>   | <span data-ttu-id="89e1b-161">提取相应的响应标头`GET`请求。</span><span class="sxs-lookup"><span data-stu-id="89e1b-161">Fetches the response headers for the corresponding `GET` request.</span></span>
<span data-ttu-id="89e1b-162">PUT</span><span class="sxs-lookup"><span data-stu-id="89e1b-162">PUT</span></span>    | <span data-ttu-id="89e1b-163">创建的资源不存在，或如果文件确实存在，更新它。</span><span class="sxs-lookup"><span data-stu-id="89e1b-163">Creates a resource that doesn't exist or, if it does exist, updates it.</span></span> <span data-ttu-id="89e1b-164">某些资源可能不支持更新。</span><span class="sxs-lookup"><span data-stu-id="89e1b-164">Some resources may not support update.</span></span>
<span data-ttu-id="89e1b-165">DELETE</span><span class="sxs-lookup"><span data-stu-id="89e1b-165">DELETE</span></span> | <span data-ttu-id="89e1b-166">删除或 unlists 资源。</span><span class="sxs-lookup"><span data-stu-id="89e1b-166">Deletes or unlists a resource.</span></span>

## <a name="http-status-codes"></a><span data-ttu-id="89e1b-167">HTTP 状态代码</span><span class="sxs-lookup"><span data-stu-id="89e1b-167">HTTP status codes</span></span>

<span data-ttu-id="89e1b-168">代码</span><span class="sxs-lookup"><span data-stu-id="89e1b-168">Code</span></span> | <span data-ttu-id="89e1b-169">描述</span><span class="sxs-lookup"><span data-stu-id="89e1b-169">Description</span></span>
---- | -----
<span data-ttu-id="89e1b-170">200</span><span class="sxs-lookup"><span data-stu-id="89e1b-170">200</span></span>  | <span data-ttu-id="89e1b-171">如果成功，并且没有响应正文。</span><span class="sxs-lookup"><span data-stu-id="89e1b-171">Success, and there is a response body.</span></span>
<span data-ttu-id="89e1b-172">201</span><span class="sxs-lookup"><span data-stu-id="89e1b-172">201</span></span>  | <span data-ttu-id="89e1b-173">已创建成功后和资源。</span><span class="sxs-lookup"><span data-stu-id="89e1b-173">Success, and the resource was created.</span></span>
<span data-ttu-id="89e1b-174">202</span><span class="sxs-lookup"><span data-stu-id="89e1b-174">202</span></span>  | <span data-ttu-id="89e1b-175">成功后，请求已被接受，但某些工作仍可能不完整和已完成以异步方式。</span><span class="sxs-lookup"><span data-stu-id="89e1b-175">Success, the request has been accepted but some work may still be incomplete and completed asynchronously.</span></span>
<span data-ttu-id="89e1b-176">204</span><span class="sxs-lookup"><span data-stu-id="89e1b-176">204</span></span>  | <span data-ttu-id="89e1b-177">如果成功，但没有任何响应正文。</span><span class="sxs-lookup"><span data-stu-id="89e1b-177">Success, but there is no response body.</span></span>
<span data-ttu-id="89e1b-178">301</span><span class="sxs-lookup"><span data-stu-id="89e1b-178">301</span></span>  | <span data-ttu-id="89e1b-179">永久重定向。</span><span class="sxs-lookup"><span data-stu-id="89e1b-179">A permanent redirect.</span></span>
<span data-ttu-id="89e1b-180">302</span><span class="sxs-lookup"><span data-stu-id="89e1b-180">302</span></span>  | <span data-ttu-id="89e1b-181">临时重定向。</span><span class="sxs-lookup"><span data-stu-id="89e1b-181">A temporary redirect.</span></span>
<span data-ttu-id="89e1b-182">400</span><span class="sxs-lookup"><span data-stu-id="89e1b-182">400</span></span>  | <span data-ttu-id="89e1b-183">在 URL 中或在请求正文中的参数不是有效的。</span><span class="sxs-lookup"><span data-stu-id="89e1b-183">The parameters in the URL or in the request body aren't valid.</span></span>
<span data-ttu-id="89e1b-184">401</span><span class="sxs-lookup"><span data-stu-id="89e1b-184">401</span></span>  | <span data-ttu-id="89e1b-185">提供的凭据均无效。</span><span class="sxs-lookup"><span data-stu-id="89e1b-185">The provided credentials are invalid.</span></span>
<span data-ttu-id="89e1b-186">403</span><span class="sxs-lookup"><span data-stu-id="89e1b-186">403</span></span>  | <span data-ttu-id="89e1b-187">给定提供的凭据不允许操作。</span><span class="sxs-lookup"><span data-stu-id="89e1b-187">The action is not allowed given the provided credentials.</span></span>
<span data-ttu-id="89e1b-188">404</span><span class="sxs-lookup"><span data-stu-id="89e1b-188">404</span></span>  | <span data-ttu-id="89e1b-189">请求的资源不存在。</span><span class="sxs-lookup"><span data-stu-id="89e1b-189">The requested resource doesn't exist.</span></span>
<span data-ttu-id="89e1b-190">409</span><span class="sxs-lookup"><span data-stu-id="89e1b-190">409</span></span>  | <span data-ttu-id="89e1b-191">与现有资源的请求冲突。</span><span class="sxs-lookup"><span data-stu-id="89e1b-191">The request conflicts with an existing resource.</span></span>
<span data-ttu-id="89e1b-192">500</span><span class="sxs-lookup"><span data-stu-id="89e1b-192">500</span></span>  | <span data-ttu-id="89e1b-193">服务遇到意外的错误。</span><span class="sxs-lookup"><span data-stu-id="89e1b-193">The service has encountered an unexpected error.</span></span>
<span data-ttu-id="89e1b-194">503</span><span class="sxs-lookup"><span data-stu-id="89e1b-194">503</span></span>  | <span data-ttu-id="89e1b-195">该服务是暂时不可用。</span><span class="sxs-lookup"><span data-stu-id="89e1b-195">The service is temporarily unavailable.</span></span>

<span data-ttu-id="89e1b-196">任何`GET`向 API 终结点发出的请求可能返回的 HTTP 重定向 （301 或 302）。</span><span class="sxs-lookup"><span data-stu-id="89e1b-196">Any `GET` request made to a API endpoint may return an HTTP redirect (301 or 302).</span></span> <span data-ttu-id="89e1b-197">客户端应通过观察正常处理此类重定向`Location`标头和正在发送后续`GET`。</span><span class="sxs-lookup"><span data-stu-id="89e1b-197">Clients should gracefully handle such redirects by observing the `Location` header and issueing a subsequent `GET`.</span></span> <span data-ttu-id="89e1b-198">有关特定终结点的文档将不显式调出可能使用重定向的位置。</span><span class="sxs-lookup"><span data-stu-id="89e1b-198">Documentation concerning specific endpoints will not explicitly call out where redirects may be used.</span></span>

<span data-ttu-id="89e1b-199">对于 500 级别状态代码，客户端可以实现合理的重试机制。</span><span class="sxs-lookup"><span data-stu-id="89e1b-199">In the case of a 500-level status code, the client can implement a reasonable retry mechanism.</span></span> <span data-ttu-id="89e1b-200">官方 NuGet 客户端重试三次时遇到任何 500 级别状态代码或 TCP/DNS 错误。</span><span class="sxs-lookup"><span data-stu-id="89e1b-200">The official NuGet client retries three times when encountering any 500-level status code or TCP/DNS error.</span></span>

## <a name="http-request-headers"></a><span data-ttu-id="89e1b-201">HTTP 请求标头</span><span class="sxs-lookup"><span data-stu-id="89e1b-201">HTTP request headers</span></span>

<span data-ttu-id="89e1b-202">name</span><span class="sxs-lookup"><span data-stu-id="89e1b-202">Name</span></span>                     | <span data-ttu-id="89e1b-203">描述</span><span class="sxs-lookup"><span data-stu-id="89e1b-203">Description</span></span>
------------------------ | -----------
<span data-ttu-id="89e1b-204">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="89e1b-204">X-NuGet-ApiKey</span></span>           | <span data-ttu-id="89e1b-205">所需的推送和删除，请参阅[`PackagePublish`资源](package-publish-resource.md)</span><span class="sxs-lookup"><span data-stu-id="89e1b-205">Required for push and delete, see [`PackagePublish` resource](package-publish-resource.md)</span></span>
<span data-ttu-id="89e1b-206">X-NuGet-Client-Version</span><span class="sxs-lookup"><span data-stu-id="89e1b-206">X-NuGet-Client-Version</span></span>   | <span data-ttu-id="89e1b-207">**弃用**和替换为`X-NuGet-Protocol-Version`</span><span class="sxs-lookup"><span data-stu-id="89e1b-207">**Deprecated** and replaced by `X-NuGet-Protocol-Version`</span></span>
<span data-ttu-id="89e1b-208">X-NuGet-Protocol-Version</span><span class="sxs-lookup"><span data-stu-id="89e1b-208">X-NuGet-Protocol-Version</span></span> | <span data-ttu-id="89e1b-209">在某些情况下，仅在 nuget.org 上的需要，请参阅[nuget.org 协议](NuGet-Protocols.md)</span><span class="sxs-lookup"><span data-stu-id="89e1b-209">Required in certain cases only on nuget.org, see [nuget.org protocols](NuGet-Protocols.md)</span></span>

## <a name="authentication"></a><span data-ttu-id="89e1b-210">身份验证</span><span class="sxs-lookup"><span data-stu-id="89e1b-210">Authentication</span></span>

<span data-ttu-id="89e1b-211">身份验证都留给要定义的包源实现。</span><span class="sxs-lookup"><span data-stu-id="89e1b-211">Authentication is left up to the package source implementation to define.</span></span> <span data-ttu-id="89e1b-212">Nuget.org，仅为`PackagePublish`资源需要身份验证通过特殊的 API 密钥标头。</span><span class="sxs-lookup"><span data-stu-id="89e1b-212">For nuget.org, only the `PackagePublish` resource requires authentication via a special API key header.</span></span> <span data-ttu-id="89e1b-213">请参阅[`PackagePublish`资源](package-publish-resource.md)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="89e1b-213">See [`PackagePublish` resource](package-publish-resource.md) for details.</span></span>
