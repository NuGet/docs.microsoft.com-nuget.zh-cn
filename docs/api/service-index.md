---
title: 服务索引，NuGet API
description: 服务索引是 NuGet HTTP API 的入口点，可枚举服务器的功能。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775361"
---
# <a name="service-index"></a><span data-ttu-id="da433-103">服务索引</span><span class="sxs-lookup"><span data-stu-id="da433-103">Service index</span></span>

<span data-ttu-id="da433-104">服务索引是一个 JSON 文档，它是 NuGet 包源的入口点，并允许客户端实现发现包源的功能。</span><span class="sxs-lookup"><span data-stu-id="da433-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="da433-105">服务索引是一个具有两个必需属性的 JSON 对象： `version` (服务索引的架构版本) 并 `resources`  (包源) 的终结点或功能。</span><span class="sxs-lookup"><span data-stu-id="da433-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="da433-106">nuget.exe 的服务索引位于 `https://api.nuget.org/v3/index.json` 。</span><span class="sxs-lookup"><span data-stu-id="da433-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="da433-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="da433-107">Versioning</span></span>

<span data-ttu-id="da433-108">`version`该值是一个 SemVer 2.0.0 不可解析版本字符串，它指示服务索引的架构版本。</span><span class="sxs-lookup"><span data-stu-id="da433-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="da433-109">API 规定版本字符串具有的主要版本号 `3` 。</span><span class="sxs-lookup"><span data-stu-id="da433-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="da433-110">由于对服务索引架构进行了非重大更改，将增加版本字符串的次要版本。</span><span class="sxs-lookup"><span data-stu-id="da433-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="da433-111">服务索引中的每个资源独立于服务索引架构版本进行了版本控制。</span><span class="sxs-lookup"><span data-stu-id="da433-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="da433-112">当前架构版本为 `3.0.0` 。</span><span class="sxs-lookup"><span data-stu-id="da433-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="da433-113">`3.0.0`版本在功能上等同于旧 `3.0.0-beta.1` 版本，但应首选此版本，因为它更清晰地传达稳定定义的架构。</span><span class="sxs-lookup"><span data-stu-id="da433-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="da433-114">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="da433-114">HTTP methods</span></span>

<span data-ttu-id="da433-115">可以使用 HTTP 方法和访问服务索引 `GET` `HEAD` 。</span><span class="sxs-lookup"><span data-stu-id="da433-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="da433-116">资源</span><span class="sxs-lookup"><span data-stu-id="da433-116">Resources</span></span>

<span data-ttu-id="da433-117">`resources`属性包含此包源支持的资源的数组。</span><span class="sxs-lookup"><span data-stu-id="da433-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="da433-118">资源</span><span class="sxs-lookup"><span data-stu-id="da433-118">Resource</span></span>

<span data-ttu-id="da433-119">资源是数组中的对象 `resources` 。</span><span class="sxs-lookup"><span data-stu-id="da433-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="da433-120">它表示包源的版本控制功能。</span><span class="sxs-lookup"><span data-stu-id="da433-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="da433-121">资源具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="da433-121">A resource has the following properties:</span></span>

<span data-ttu-id="da433-122">名称</span><span class="sxs-lookup"><span data-stu-id="da433-122">Name</span></span>          | <span data-ttu-id="da433-123">类型</span><span class="sxs-lookup"><span data-stu-id="da433-123">Type</span></span>   | <span data-ttu-id="da433-124">必须</span><span class="sxs-lookup"><span data-stu-id="da433-124">Required</span></span> | <span data-ttu-id="da433-125">注释</span><span class="sxs-lookup"><span data-stu-id="da433-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="da433-126">string</span><span class="sxs-lookup"><span data-stu-id="da433-126">string</span></span> | <span data-ttu-id="da433-127">是</span><span class="sxs-lookup"><span data-stu-id="da433-127">yes</span></span>      | <span data-ttu-id="da433-128">资源的 URL</span><span class="sxs-lookup"><span data-stu-id="da433-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="da433-129">string</span><span class="sxs-lookup"><span data-stu-id="da433-129">string</span></span> | <span data-ttu-id="da433-130">是</span><span class="sxs-lookup"><span data-stu-id="da433-130">yes</span></span>      | <span data-ttu-id="da433-131">表示资源类型的字符串常数</span><span class="sxs-lookup"><span data-stu-id="da433-131">A string constant representing the resource type</span></span>
<span data-ttu-id="da433-132">comment</span><span class="sxs-lookup"><span data-stu-id="da433-132">comment</span></span>       | <span data-ttu-id="da433-133">string</span><span class="sxs-lookup"><span data-stu-id="da433-133">string</span></span> | <span data-ttu-id="da433-134">否</span><span class="sxs-lookup"><span data-stu-id="da433-134">no</span></span>       | <span data-ttu-id="da433-135">用户可读的资源说明</span><span class="sxs-lookup"><span data-stu-id="da433-135">A human readable description of the resource</span></span>

<span data-ttu-id="da433-136">`@id`是一个必须为绝对的 URL，并且必须具有 HTTP 或 HTTPS 架构。</span><span class="sxs-lookup"><span data-stu-id="da433-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="da433-137">`@type`用于标识与资源交互时要使用的特定协议。</span><span class="sxs-lookup"><span data-stu-id="da433-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="da433-138">资源的类型是不透明的字符串，但通常采用以下格式：</span><span class="sxs-lookup"><span data-stu-id="da433-138">The type of the resource is an opaque string but generally has the format:</span></span>

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

<span data-ttu-id="da433-139">客户端应对它们理解的值进行硬编码 `@type` ，并在包源的服务索引中查找这些值。</span><span class="sxs-lookup"><span data-stu-id="da433-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="da433-140">`@type`当前使用的确切值基于[API 概述](overview.md#resources-and-schema)中列出的各个资源引用文档进行枚举。</span><span class="sxs-lookup"><span data-stu-id="da433-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="da433-141">对于本文档，有关不同资源的文档实质上是按 `{RESOURCE_NAME}` 服务索引中找到的，这类似于按方案分组。</span><span class="sxs-lookup"><span data-stu-id="da433-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="da433-142">不要求每个资源都具有唯一的 `@id` 或 `@type` 。</span><span class="sxs-lookup"><span data-stu-id="da433-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="da433-143">由客户端实现确定要优先于另一种资源。</span><span class="sxs-lookup"><span data-stu-id="da433-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="da433-144">一个可能的实现是在 `@type` 出现连接故障或服务器错误的情况下，可以使用相同或兼容的资源。</span><span class="sxs-lookup"><span data-stu-id="da433-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="da433-145">示例请求</span><span class="sxs-lookup"><span data-stu-id="da433-145">Sample request</span></span>

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a><span data-ttu-id="da433-146">示例响应</span><span class="sxs-lookup"><span data-stu-id="da433-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
