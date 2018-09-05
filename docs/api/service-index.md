---
title: 服务索引，NuGet API
description: 服务索引是 NuGet HTTP API 的入口点，并枚举服务器的功能。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 478b74f98caafdc7c6b69423b9f9d72890c8d7cb
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545252"
---
# <a name="service-index"></a><span data-ttu-id="05edb-103">服务索引</span><span class="sxs-lookup"><span data-stu-id="05edb-103">Service index</span></span>

<span data-ttu-id="05edb-104">服务索引是一个 JSON 文档是 NuGet 包源的入口点，并允许客户端实现，若要了解包源的功能。</span><span class="sxs-lookup"><span data-stu-id="05edb-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="05edb-105">服务索引是一个具有两个必需属性的 JSON 对象： `version` （服务索引的架构版本） 和`resources`（终结点或功能的包源）。</span><span class="sxs-lookup"><span data-stu-id="05edb-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="05edb-106">nuget.org 的服务索引位于`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="05edb-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="05edb-107">版本管理</span><span class="sxs-lookup"><span data-stu-id="05edb-107">Versioning</span></span>

<span data-ttu-id="05edb-108">`version`值是 SemVer 2.0.0 版本解析，因此字符串指示服务索引的架构版本。</span><span class="sxs-lookup"><span data-stu-id="05edb-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="05edb-109">API 要求的版本字符串有主版本号的`3`。</span><span class="sxs-lookup"><span data-stu-id="05edb-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="05edb-110">服务索引架构做出非重大更改后，会增加版本字符串的次要版本。</span><span class="sxs-lookup"><span data-stu-id="05edb-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="05edb-111">服务索引的每个资源是版本控制独立于服务索引的架构版本。</span><span class="sxs-lookup"><span data-stu-id="05edb-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="05edb-112">当前架构版本是`3.0.0`。</span><span class="sxs-lookup"><span data-stu-id="05edb-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="05edb-113">`3.0.0`版本在功能上等效于较旧`3.0.0-beta.1`版本但只是首选，因为它更清楚地传达稳定、 定义架构。</span><span class="sxs-lookup"><span data-stu-id="05edb-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="05edb-114">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="05edb-114">HTTP methods</span></span>

<span data-ttu-id="05edb-115">服务索引是使用 HTTP 方法可以访问`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="05edb-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="05edb-116">资源</span><span class="sxs-lookup"><span data-stu-id="05edb-116">Resources</span></span>

<span data-ttu-id="05edb-117">`resources`属性包含此包源支持的资源数组。</span><span class="sxs-lookup"><span data-stu-id="05edb-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="05edb-118">资源</span><span class="sxs-lookup"><span data-stu-id="05edb-118">Resource</span></span>

<span data-ttu-id="05edb-119">资源是中的对象`resources`数组。</span><span class="sxs-lookup"><span data-stu-id="05edb-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="05edb-120">它表示包源的版本控制功能。</span><span class="sxs-lookup"><span data-stu-id="05edb-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="05edb-121">每个资源有以下属性：</span><span class="sxs-lookup"><span data-stu-id="05edb-121">A resource has the following properties:</span></span>

<span data-ttu-id="05edb-122">name</span><span class="sxs-lookup"><span data-stu-id="05edb-122">Name</span></span>          | <span data-ttu-id="05edb-123">类型</span><span class="sxs-lookup"><span data-stu-id="05edb-123">Type</span></span>   | <span data-ttu-id="05edb-124">必需</span><span class="sxs-lookup"><span data-stu-id="05edb-124">Required</span></span> | <span data-ttu-id="05edb-125">说明</span><span class="sxs-lookup"><span data-stu-id="05edb-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="05edb-126">字符串</span><span class="sxs-lookup"><span data-stu-id="05edb-126">string</span></span> | <span data-ttu-id="05edb-127">是</span><span class="sxs-lookup"><span data-stu-id="05edb-127">yes</span></span>      | <span data-ttu-id="05edb-128">资源的 URL</span><span class="sxs-lookup"><span data-stu-id="05edb-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="05edb-129">字符串</span><span class="sxs-lookup"><span data-stu-id="05edb-129">string</span></span> | <span data-ttu-id="05edb-130">是</span><span class="sxs-lookup"><span data-stu-id="05edb-130">yes</span></span>      | <span data-ttu-id="05edb-131">一个字符串常数，表示资源类型</span><span class="sxs-lookup"><span data-stu-id="05edb-131">A string constant representing the resource type</span></span>
<span data-ttu-id="05edb-132">注释</span><span class="sxs-lookup"><span data-stu-id="05edb-132">comment</span></span>       | <span data-ttu-id="05edb-133">字符串</span><span class="sxs-lookup"><span data-stu-id="05edb-133">string</span></span> | <span data-ttu-id="05edb-134">否</span><span class="sxs-lookup"><span data-stu-id="05edb-134">no</span></span>       | <span data-ttu-id="05edb-135">资源的人工可读说明</span><span class="sxs-lookup"><span data-stu-id="05edb-135">A human readable description of the resource</span></span>

<span data-ttu-id="05edb-136">`@id`是 URL 必须是绝对路径，并且必须具有 HTTP 或 HTTPS 架构。</span><span class="sxs-lookup"><span data-stu-id="05edb-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="05edb-137">`@type`用于标识要与资源交互时使用的特定协议。</span><span class="sxs-lookup"><span data-stu-id="05edb-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="05edb-138">资源类型是不透明的字符串，但通常采用格式：</span><span class="sxs-lookup"><span data-stu-id="05edb-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="05edb-139">客户端应进行硬编码`@type`他们了解并查找包源的服务索引中的值。</span><span class="sxs-lookup"><span data-stu-id="05edb-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="05edb-140">确切`@type`枚举中列出的单个资源引用文档上目前所用的值[API 概述](overview.md#resources-and-schema)。</span><span class="sxs-lookup"><span data-stu-id="05edb-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="05edb-141">本文档中，为不同的资源有关的文档将实质上是按分组`{RESOURCE_NAME}`它类似于按方案进行分组的服务索引中找到。</span><span class="sxs-lookup"><span data-stu-id="05edb-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="05edb-142">没有任何要求每个资源具有一个唯一`@id`或`@type`。</span><span class="sxs-lookup"><span data-stu-id="05edb-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="05edb-143">负责要确定哪些资源通过另一个首选的客户端实现。</span><span class="sxs-lookup"><span data-stu-id="05edb-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="05edb-144">一个可能的实现是相同或兼容的资源`@type`可以以轮循机制方式发生连接故障或服务器错误时使用。</span><span class="sxs-lookup"><span data-stu-id="05edb-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="05edb-145">示例请求</span><span class="sxs-lookup"><span data-stu-id="05edb-145">Sample request</span></span>

<span data-ttu-id="05edb-146">获取 https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="05edb-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="05edb-147">示例响应</span><span class="sxs-lookup"><span data-stu-id="05edb-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
