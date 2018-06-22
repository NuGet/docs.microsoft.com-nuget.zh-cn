---
title: 服务索引，NuGet API
description: 服务索引是 NuGet HTTP API 的入口点，并枚举服务器的功能。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 84e623e8480e4d17edad2ec3b2da6dcb6e53d21b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822089"
---
# <a name="service-index"></a><span data-ttu-id="fd78a-103">服务索引</span><span class="sxs-lookup"><span data-stu-id="fd78a-103">Service index</span></span>

<span data-ttu-id="fd78a-104">服务索引是一个 JSON 文档，是 NuGet 程序包源的入口点，并允许一个客户端实现，以发现包源的功能。</span><span class="sxs-lookup"><span data-stu-id="fd78a-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="fd78a-105">服务索引是具有两个必需属性的 JSON 对象： `version` （服务索引的架构版本） 和`resources`（终结点或功能的包源）。</span><span class="sxs-lookup"><span data-stu-id="fd78a-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="fd78a-106">nuget.org 的服务索引位于`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="fd78a-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="fd78a-107">版本管理</span><span class="sxs-lookup"><span data-stu-id="fd78a-107">Versioning</span></span>

<span data-ttu-id="fd78a-108">`version`值是 SemVer 2.0.0 解析，因此版本字符串，它指示服务索引的架构版本。</span><span class="sxs-lookup"><span data-stu-id="fd78a-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="fd78a-109">API 规定的版本字符串有的一个主要版本号`3`。</span><span class="sxs-lookup"><span data-stu-id="fd78a-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="fd78a-110">对服务索引架构进行非重大更改时，将增加的版本字符串的次要版本。</span><span class="sxs-lookup"><span data-stu-id="fd78a-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="fd78a-111">服务索引中的每个资源是版本控制独立于服务索引架构版本。</span><span class="sxs-lookup"><span data-stu-id="fd78a-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="fd78a-112">当前架构版本是`3.0.0`。</span><span class="sxs-lookup"><span data-stu-id="fd78a-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="fd78a-113">`3.0.0`版本在功能上等效于较旧`3.0.0-beta.1`版本但应为首选，因为它更清楚地了解通信稳定、 定义架构。</span><span class="sxs-lookup"><span data-stu-id="fd78a-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="fd78a-114">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="fd78a-114">HTTP methods</span></span>

<span data-ttu-id="fd78a-115">服务索引是使用 HTTP 方法可以访问`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="fd78a-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="fd78a-116">资源</span><span class="sxs-lookup"><span data-stu-id="fd78a-116">Resources</span></span>

<span data-ttu-id="fd78a-117">`resources`属性包含此包源所支持的资源的数组。</span><span class="sxs-lookup"><span data-stu-id="fd78a-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="fd78a-118">资源</span><span class="sxs-lookup"><span data-stu-id="fd78a-118">Resource</span></span>

<span data-ttu-id="fd78a-119">资源是中的对象`resources`数组。</span><span class="sxs-lookup"><span data-stu-id="fd78a-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="fd78a-120">它表示包源已进行版本管理功能。</span><span class="sxs-lookup"><span data-stu-id="fd78a-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="fd78a-121">资源具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="fd78a-121">A resource has the following properties:</span></span>

<span data-ttu-id="fd78a-122">名称</span><span class="sxs-lookup"><span data-stu-id="fd78a-122">Name</span></span>          | <span data-ttu-id="fd78a-123">类型</span><span class="sxs-lookup"><span data-stu-id="fd78a-123">Type</span></span>   | <span data-ttu-id="fd78a-124">必需</span><span class="sxs-lookup"><span data-stu-id="fd78a-124">Required</span></span> | <span data-ttu-id="fd78a-125">说明</span><span class="sxs-lookup"><span data-stu-id="fd78a-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="fd78a-126">字符串</span><span class="sxs-lookup"><span data-stu-id="fd78a-126">string</span></span> | <span data-ttu-id="fd78a-127">是</span><span class="sxs-lookup"><span data-stu-id="fd78a-127">yes</span></span>      | <span data-ttu-id="fd78a-128">资源的 URL</span><span class="sxs-lookup"><span data-stu-id="fd78a-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="fd78a-129">字符串</span><span class="sxs-lookup"><span data-stu-id="fd78a-129">string</span></span> | <span data-ttu-id="fd78a-130">是</span><span class="sxs-lookup"><span data-stu-id="fd78a-130">yes</span></span>      | <span data-ttu-id="fd78a-131">一个字符串常量，代表资源类型</span><span class="sxs-lookup"><span data-stu-id="fd78a-131">A string constant representing the resource type</span></span>
<span data-ttu-id="fd78a-132">注释</span><span class="sxs-lookup"><span data-stu-id="fd78a-132">comment</span></span>       | <span data-ttu-id="fd78a-133">字符串</span><span class="sxs-lookup"><span data-stu-id="fd78a-133">string</span></span> | <span data-ttu-id="fd78a-134">否</span><span class="sxs-lookup"><span data-stu-id="fd78a-134">no</span></span>       | <span data-ttu-id="fd78a-135">资源的人工可读说明</span><span class="sxs-lookup"><span data-stu-id="fd78a-135">A human readable description of the resource</span></span>

<span data-ttu-id="fd78a-136">`@id`是 URL 必须是绝对路径，必须具有 HTTP 或 HTTPS 的架构。</span><span class="sxs-lookup"><span data-stu-id="fd78a-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="fd78a-137">`@type`用于标识要使用与资源交互时的特定协议。</span><span class="sxs-lookup"><span data-stu-id="fd78a-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="fd78a-138">资源的类型是不透明的字符串，但通常采用格式：</span><span class="sxs-lookup"><span data-stu-id="fd78a-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="fd78a-139">客户端预期硬编码到`@type`它们了解并查找包源的服务索引中的值。</span><span class="sxs-lookup"><span data-stu-id="fd78a-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="fd78a-140">准确`@type`当今使用的值枚举中列出的单个资源引用文档[API 概述](overview.md#resources-and-schema)。</span><span class="sxs-lookup"><span data-stu-id="fd78a-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="fd78a-141">本文档中，为不同的资源有关的文档都实质上是将按`{RESOURCE_NAME}`类似于按方案分组服务索引中找到。</span><span class="sxs-lookup"><span data-stu-id="fd78a-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="fd78a-142">不存在的每个资源具有一个唯一的要求`@id`或`@type`。</span><span class="sxs-lookup"><span data-stu-id="fd78a-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="fd78a-143">负责要确定哪些资源较另一种首选的客户端实现。</span><span class="sxs-lookup"><span data-stu-id="fd78a-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="fd78a-144">一个可能的实现是相同或兼容的资源`@type`可在发生连接故障或服务器错误一种轮循机制的方式。</span><span class="sxs-lookup"><span data-stu-id="fd78a-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="fd78a-145">示例请求</span><span class="sxs-lookup"><span data-stu-id="fd78a-145">Sample request</span></span>

<span data-ttu-id="fd78a-146">获取 https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="fd78a-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="fd78a-147">示例响应</span><span class="sxs-lookup"><span data-stu-id="fd78a-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
