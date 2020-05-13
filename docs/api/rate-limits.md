---
title: 速率限制，NuGet API
description: NuGet Api 将具有强制速率限制，以防止滥用。
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367929"
---
# <a name="rate-limits"></a><span data-ttu-id="12731-103">速率限制</span><span class="sxs-lookup"><span data-stu-id="12731-103">Rate Limits</span></span>

<span data-ttu-id="12731-104">NuGet.org API 强制实施速率限制以防止滥用。</span><span class="sxs-lookup"><span data-stu-id="12731-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="12731-105">超出速率限制的请求会返回以下错误：</span><span class="sxs-lookup"><span data-stu-id="12731-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="12731-106">除了使用速率限制进行请求限制之外，某些 Api 还强制执行配额。</span><span class="sxs-lookup"><span data-stu-id="12731-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="12731-107">超过配额的请求会返回以下错误：</span><span class="sxs-lookup"><span data-stu-id="12731-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="12731-108">下表列出了 NuGet.org API 的速率限制。</span><span class="sxs-lookup"><span data-stu-id="12731-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="12731-109">包搜索</span><span class="sxs-lookup"><span data-stu-id="12731-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="12731-110">建议使用 NuGet 的[V3 搜索 api](search-query-service-resource.md) ，因为它当前未进行速率限制。</span><span class="sxs-lookup"><span data-stu-id="12731-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="12731-111">对于 V1 和 V2 搜索 Api，以下限制适用：</span><span class="sxs-lookup"><span data-stu-id="12731-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="12731-112">API</span><span class="sxs-lookup"><span data-stu-id="12731-112">API</span></span> | <span data-ttu-id="12731-113">限制类型</span><span class="sxs-lookup"><span data-stu-id="12731-113">Limit Type</span></span> | <span data-ttu-id="12731-114">限制值</span><span class="sxs-lookup"><span data-stu-id="12731-114">Limit Value</span></span> | <span data-ttu-id="12731-115">API 用例</span><span class="sxs-lookup"><span data-stu-id="12731-115">API Use Case</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="12731-116">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="12731-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="12731-117">IP</span><span class="sxs-lookup"><span data-stu-id="12731-117">IP</span></span> | <span data-ttu-id="12731-118">1000/分钟</span><span class="sxs-lookup"><span data-stu-id="12731-118">1000 / minute</span></span> | <span data-ttu-id="12731-119">通过 v1 OData 集合查询 NuGet 包元数据 `Packages`</span><span class="sxs-lookup"><span data-stu-id="12731-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="12731-120">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="12731-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="12731-121">IP</span><span class="sxs-lookup"><span data-stu-id="12731-121">IP</span></span> | <span data-ttu-id="12731-122">3000/分钟</span><span class="sxs-lookup"><span data-stu-id="12731-122">3000 / minute</span></span> | <span data-ttu-id="12731-123">通过 v1 搜索终结点搜索 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="12731-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="12731-124">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="12731-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="12731-125">IP</span><span class="sxs-lookup"><span data-stu-id="12731-125">IP</span></span> | <span data-ttu-id="12731-126">20000/分钟</span><span class="sxs-lookup"><span data-stu-id="12731-126">20000 / minute</span></span> | <span data-ttu-id="12731-127">通过 v2 OData 集合查询 NuGet 包元数据 `Packages`</span><span class="sxs-lookup"><span data-stu-id="12731-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="12731-128">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="12731-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="12731-129">IP</span><span class="sxs-lookup"><span data-stu-id="12731-129">IP</span></span> | <span data-ttu-id="12731-130">100/分钟</span><span class="sxs-lookup"><span data-stu-id="12731-130">100 / minute</span></span> | <span data-ttu-id="12731-131">通过 v2 OData 集合查询 NuGet 包计数 `Packages`</span><span class="sxs-lookup"><span data-stu-id="12731-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="12731-132">包推送和取消列出</span><span class="sxs-lookup"><span data-stu-id="12731-132">Package Push and Unlist</span></span>

| <span data-ttu-id="12731-133">API</span><span class="sxs-lookup"><span data-stu-id="12731-133">API</span></span> | <span data-ttu-id="12731-134">限制类型</span><span class="sxs-lookup"><span data-stu-id="12731-134">Limit Type</span></span> | <span data-ttu-id="12731-135">限制值</span><span class="sxs-lookup"><span data-stu-id="12731-135">Limit Value</span></span> | <span data-ttu-id="12731-136">API 用例</span><span class="sxs-lookup"><span data-stu-id="12731-136">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="12731-137">**PUT**`/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="12731-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="12731-138">API 密钥</span><span class="sxs-lookup"><span data-stu-id="12731-138">API Key</span></span> | <span data-ttu-id="12731-139">350/小时</span><span class="sxs-lookup"><span data-stu-id="12731-139">350 / hour</span></span> | <span data-ttu-id="12731-140">通过 v2 推送终结点上传新的 NuGet 包（版本）</span><span class="sxs-lookup"><span data-stu-id="12731-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="12731-141">**删除**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="12731-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="12731-142">API 密钥</span><span class="sxs-lookup"><span data-stu-id="12731-142">API Key</span></span> | <span data-ttu-id="12731-143">250/小时</span><span class="sxs-lookup"><span data-stu-id="12731-143">250 / hour</span></span> | <span data-ttu-id="12731-144">通过 v2 终结点取消列出 NuGet 包（版本）</span><span class="sxs-lookup"><span data-stu-id="12731-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 

## <a name="nugetorg-website-page-views"></a><span data-ttu-id="12731-145">nuget.org 网站页面视图</span><span class="sxs-lookup"><span data-stu-id="12731-145">nuget.org website page views</span></span>

<span data-ttu-id="12731-146">如果以编程方式访问 nuget.org 网页，请考虑调查我们记录的[V3 api](overview.md)。</span><span class="sxs-lookup"><span data-stu-id="12731-146">If you are accessing the nuget.org web pages programmatically, consider investigating our documented [V3 APIs](overview.md).</span></span> <span data-ttu-id="12731-147">通过这些终结点，可以更简单地访问包元数据和内容。</span><span class="sxs-lookup"><span data-stu-id="12731-147">These endpoints allow for simpler access to package metadata and content.</span></span> <span data-ttu-id="12731-148">V3 API 具有更好的可用性，性能高于访问 NuGet 库网页（专为 web 浏览器交互）。</span><span class="sxs-lookup"><span data-stu-id="12731-148">The V3 API has better availability and has higher performance than accessing the NuGet Gallery web pages, which are designed for web browser interaction.</span></span>

| <span data-ttu-id="12731-149">API</span><span class="sxs-lookup"><span data-stu-id="12731-149">API</span></span> | <span data-ttu-id="12731-150">限制类型</span><span class="sxs-lookup"><span data-stu-id="12731-150">Limit Type</span></span> | <span data-ttu-id="12731-151">限制值</span><span class="sxs-lookup"><span data-stu-id="12731-151">Limit Value</span></span> | <span data-ttu-id="12731-152">API 用例</span><span class="sxs-lookup"><span data-stu-id="12731-152">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="12731-153">**GET** `/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="12731-153">**GET** `/package/{id}/{version}`</span></span> | <span data-ttu-id="12731-154">IP</span><span class="sxs-lookup"><span data-stu-id="12731-154">IP</span></span> | <span data-ttu-id="12731-155">50/分钟</span><span class="sxs-lookup"><span data-stu-id="12731-155">50 / minute</span></span> | <span data-ttu-id="12731-156">显示包（版本）详细信息页。</span><span class="sxs-lookup"><span data-stu-id="12731-156">Display package (version) details page.</span></span> 
