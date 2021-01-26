---
title: 推送符号包，NuGet API |Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 发布服务允许客户端发布新的符号包。
keywords: NuGet API 推送符号包
ms.reviewer: karann
ms.openlocfilehash: 91bb4c9ca77fd7f1ff35831e02eb4f9d65d641c5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773895"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="c57bf-104">推送符号包</span><span class="sxs-lookup"><span data-stu-id="c57bf-104">Push Symbol Packages</span></span>

<span data-ttu-id="c57bf-105">可以使用 NuGet V3 API ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 推送符号包。</span><span class="sxs-lookup"><span data-stu-id="c57bf-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="c57bf-106">这些操作基于 `SymbolPackagePublish` 在 [服务索引](service-index.md)中找到的资源。</span><span class="sxs-lookup"><span data-stu-id="c57bf-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="c57bf-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="c57bf-107">Versioning</span></span>

<span data-ttu-id="c57bf-108">使用以下 `@type` 值：</span><span class="sxs-lookup"><span data-stu-id="c57bf-108">The following `@type` value is used:</span></span>

<span data-ttu-id="c57bf-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="c57bf-109">@type value</span></span>                 | <span data-ttu-id="c57bf-110">说明</span><span class="sxs-lookup"><span data-stu-id="c57bf-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="c57bf-111">SymbolPackagePublish/4.9。0</span><span class="sxs-lookup"><span data-stu-id="c57bf-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="c57bf-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="c57bf-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="c57bf-113">基 URL</span><span class="sxs-lookup"><span data-stu-id="c57bf-113">Base URL</span></span>

<span data-ttu-id="c57bf-114">以下 Api 的基 URL 是 `@id` `SymbolPackagePublish/4.9.0` 包源的 [服务索引](service-index.md)中资源的属性的值。</span><span class="sxs-lookup"><span data-stu-id="c57bf-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="c57bf-115">对于以下文档，使用 nuget 的 URL。</span><span class="sxs-lookup"><span data-stu-id="c57bf-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="c57bf-116">请考虑 `https://www.nuget.org/api/v2/symbolpackage` `@id` 在服务索引中找到的值的占位符。</span><span class="sxs-lookup"><span data-stu-id="c57bf-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c57bf-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="c57bf-117">HTTP methods</span></span>

<span data-ttu-id="c57bf-118">`PUT`此资源支持 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="c57bf-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="c57bf-119">推送符号包</span><span class="sxs-lookup"><span data-stu-id="c57bf-119">Push a symbol package</span></span>

<span data-ttu-id="c57bf-120">nuget.org 支持使用以下 API 将新的符号包格式推送 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 。</span><span class="sxs-lookup"><span data-stu-id="c57bf-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

```
PUT https://www.nuget.org/api/v2/symbolpackage
```

<span data-ttu-id="c57bf-121">可以多次提交具有相同 ID 和版本的符号包。</span><span class="sxs-lookup"><span data-stu-id="c57bf-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="c57bf-122">在以下情况下，将拒绝符号包。</span><span class="sxs-lookup"><span data-stu-id="c57bf-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="c57bf-123">ID 和版本相同的包不存在。</span><span class="sxs-lookup"><span data-stu-id="c57bf-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="c57bf-124">已推送具有相同 ID 和版本的符号包，但尚未发布。</span><span class="sxs-lookup"><span data-stu-id="c57bf-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="c57bf-125"> ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 的符号包无效 (参见 [符号包约束](../create-packages/Symbol-Packages-snupkg.md)) 。</span><span class="sxs-lookup"><span data-stu-id="c57bf-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="c57bf-126">请求参数</span><span class="sxs-lookup"><span data-stu-id="c57bf-126">Request parameters</span></span>

<span data-ttu-id="c57bf-127">名称</span><span class="sxs-lookup"><span data-stu-id="c57bf-127">Name</span></span>           | <span data-ttu-id="c57bf-128">In</span><span class="sxs-lookup"><span data-stu-id="c57bf-128">In</span></span>     | <span data-ttu-id="c57bf-129">类型</span><span class="sxs-lookup"><span data-stu-id="c57bf-129">Type</span></span>   | <span data-ttu-id="c57bf-130">必须</span><span class="sxs-lookup"><span data-stu-id="c57bf-130">Required</span></span> | <span data-ttu-id="c57bf-131">注释</span><span class="sxs-lookup"><span data-stu-id="c57bf-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="c57bf-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="c57bf-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="c57bf-133">标头</span><span class="sxs-lookup"><span data-stu-id="c57bf-133">Header</span></span> | <span data-ttu-id="c57bf-134">string</span><span class="sxs-lookup"><span data-stu-id="c57bf-134">string</span></span> | <span data-ttu-id="c57bf-135">是</span><span class="sxs-lookup"><span data-stu-id="c57bf-135">yes</span></span>      | <span data-ttu-id="c57bf-136">例如： `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="c57bf-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="c57bf-137">API 密钥是用户从包源中获得的不透明字符串，配置到客户端。</span><span class="sxs-lookup"><span data-stu-id="c57bf-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="c57bf-138">不会强制执行任何特定的字符串格式，但 API 密钥的长度不应超过 HTTP 标头值的合理大小。</span><span class="sxs-lookup"><span data-stu-id="c57bf-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="c57bf-139">请求正文</span><span class="sxs-lookup"><span data-stu-id="c57bf-139">Request body</span></span>

<span data-ttu-id="c57bf-140">符号推送的请求正文与包推送请求的请求正文相同 (请参阅 [包推送和删除](package-publish-resource.md)) 。</span><span class="sxs-lookup"><span data-stu-id="c57bf-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="c57bf-141">响应</span><span class="sxs-lookup"><span data-stu-id="c57bf-141">Response</span></span>

<span data-ttu-id="c57bf-142">状态代码</span><span class="sxs-lookup"><span data-stu-id="c57bf-142">Status Code</span></span> | <span data-ttu-id="c57bf-143">含义</span><span class="sxs-lookup"><span data-stu-id="c57bf-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="c57bf-144">201</span><span class="sxs-lookup"><span data-stu-id="c57bf-144">201</span></span>         | <span data-ttu-id="c57bf-145">已成功推送符号包。</span><span class="sxs-lookup"><span data-stu-id="c57bf-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="c57bf-146">400</span><span class="sxs-lookup"><span data-stu-id="c57bf-146">400</span></span>         | <span data-ttu-id="c57bf-147">提供的符号包无效。</span><span class="sxs-lookup"><span data-stu-id="c57bf-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="c57bf-148">401</span><span class="sxs-lookup"><span data-stu-id="c57bf-148">401</span></span>         | <span data-ttu-id="c57bf-149">用户无权执行此操作。</span><span class="sxs-lookup"><span data-stu-id="c57bf-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="c57bf-150">404</span><span class="sxs-lookup"><span data-stu-id="c57bf-150">404</span></span>         | <span data-ttu-id="c57bf-151">具有提供的 ID 和版本的对应包不存在。</span><span class="sxs-lookup"><span data-stu-id="c57bf-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="c57bf-152">409</span><span class="sxs-lookup"><span data-stu-id="c57bf-152">409</span></span>         | <span data-ttu-id="c57bf-153">已推送具有提供的 ID 和版本的符号包，但它尚不可用。</span><span class="sxs-lookup"><span data-stu-id="c57bf-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="c57bf-154">413</span><span class="sxs-lookup"><span data-stu-id="c57bf-154">413</span></span>         | <span data-ttu-id="c57bf-155">包太大。</span><span class="sxs-lookup"><span data-stu-id="c57bf-155">The package is too large.</span></span>

