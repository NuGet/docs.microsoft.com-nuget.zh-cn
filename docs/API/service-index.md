---
title: "服务索引、 NuGet API |Microsoft 文档"
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
description: "服务索引是 NuGet HTTP API 的入口点，并枚举服务器的功能。"
keywords: "NuGet API 入口点，NuGetA PI 终结点发现"
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 9d0bb421c163520df4a1f0e9f3f71aab823aace3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="service-index"></a><span data-ttu-id="ad7ea-104">服务索引</span><span class="sxs-lookup"><span data-stu-id="ad7ea-104">Service index</span></span>

<span data-ttu-id="ad7ea-105">服务索引是一个 JSON 文档，是 NuGet 程序包源的入口点，并允许一个客户端实现，以发现包源的功能。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="ad7ea-106">服务索引是具有两个必需属性的 JSON 对象： `version` （服务索引的架构版本） 和`resources`（终结点或功能的包源）。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="ad7ea-107">nuget.org 的服务索引位于`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="ad7ea-108">版本管理</span><span class="sxs-lookup"><span data-stu-id="ad7ea-108">Versioning</span></span>

<span data-ttu-id="ad7ea-109">`version`值是 SemVer 2.0.0 解析，因此版本字符串，它指示服务索引的架构版本。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span>
<span data-ttu-id="ad7ea-110">API 规定的版本字符串有的一个主要版本号`3`。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="ad7ea-111">对服务索引架构进行非重大更改时，将增加的版本字符串的次要版本。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="ad7ea-112">服务索引中的每个资源是版本控制独立于服务索引架构版本。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="ad7ea-113">当前架构版本是`3.0.0-beta.1`。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-113">The current schema version is `3.0.0-beta.1`.</span></span>

## <a name="http-methods"></a><span data-ttu-id="ad7ea-114">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="ad7ea-114">HTTP methods</span></span>

<span data-ttu-id="ad7ea-115">服务索引是使用 HTTP 方法可以访问`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="ad7ea-116">资源</span><span class="sxs-lookup"><span data-stu-id="ad7ea-116">Resources</span></span>

<span data-ttu-id="ad7ea-117">`resources`属性包含此包源所支持的资源的数组。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="ad7ea-118">资源</span><span class="sxs-lookup"><span data-stu-id="ad7ea-118">Resource</span></span>

<span data-ttu-id="ad7ea-119">资源是中的对象`resources`数组。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="ad7ea-120">它表示包源已进行版本管理功能。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="ad7ea-121">资源具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="ad7ea-121">A resource has the following properties:</span></span>

<span data-ttu-id="ad7ea-122">name</span><span class="sxs-lookup"><span data-stu-id="ad7ea-122">Name</span></span>          | <span data-ttu-id="ad7ea-123">类型</span><span class="sxs-lookup"><span data-stu-id="ad7ea-123">Type</span></span>   | <span data-ttu-id="ad7ea-124">必需</span><span class="sxs-lookup"><span data-stu-id="ad7ea-124">Required</span></span> | <span data-ttu-id="ad7ea-125">说明</span><span class="sxs-lookup"><span data-stu-id="ad7ea-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="ad7ea-126">字符串</span><span class="sxs-lookup"><span data-stu-id="ad7ea-126">string</span></span> | <span data-ttu-id="ad7ea-127">是</span><span class="sxs-lookup"><span data-stu-id="ad7ea-127">yes</span></span>      | <span data-ttu-id="ad7ea-128">资源的 URL</span><span class="sxs-lookup"><span data-stu-id="ad7ea-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="ad7ea-129">字符串</span><span class="sxs-lookup"><span data-stu-id="ad7ea-129">string</span></span> | <span data-ttu-id="ad7ea-130">是</span><span class="sxs-lookup"><span data-stu-id="ad7ea-130">yes</span></span>      | <span data-ttu-id="ad7ea-131">一个字符串常量，代表资源类型</span><span class="sxs-lookup"><span data-stu-id="ad7ea-131">A string constant representing the resource type</span></span>
<span data-ttu-id="ad7ea-132">注释</span><span class="sxs-lookup"><span data-stu-id="ad7ea-132">comment</span></span>       | <span data-ttu-id="ad7ea-133">字符串</span><span class="sxs-lookup"><span data-stu-id="ad7ea-133">string</span></span> | <span data-ttu-id="ad7ea-134">否</span><span class="sxs-lookup"><span data-stu-id="ad7ea-134">no</span></span>       | <span data-ttu-id="ad7ea-135">资源的人工可读说明</span><span class="sxs-lookup"><span data-stu-id="ad7ea-135">A human readable description of the resource</span></span>

<span data-ttu-id="ad7ea-136">`@id`是 URL 必须是绝对路径，必须具有 HTTP 或 HTTPS 的架构。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="ad7ea-137">`@type`用于标识要使用与资源交互时的特定协议。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="ad7ea-138">资源的类型是不透明的字符串，但通常采用格式：</span><span class="sxs-lookup"><span data-stu-id="ad7ea-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="ad7ea-139">客户端预期硬编码到`@type`它们了解并查找包源的服务索引中的值。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="ad7ea-140">准确`@type`当今使用的值枚举中列出的单个资源引用文档[API 概述](overview.md#resources-and-schema)。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="ad7ea-141">本文档中，为不同的资源有关的文档都实质上是将按`{RESOURCE_NAME}`类似于按方案分组服务索引中找到。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="ad7ea-142">不存在的每个资源具有一个唯一的要求`@id`或`@type`。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="ad7ea-143">负责要确定哪些资源较另一种首选的客户端实现。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="ad7ea-144">一个可能的实现是相同或兼容的资源`@type`可在发生连接故障或服务器错误一种轮循机制的方式。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="ad7ea-145">示例请求</span><span class="sxs-lookup"><span data-stu-id="ad7ea-145">Sample request</span></span>

<span data-ttu-id="ad7ea-146">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="ad7ea-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="ad7ea-147">示例响应</span><span class="sxs-lookup"><span data-stu-id="ad7ea-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
