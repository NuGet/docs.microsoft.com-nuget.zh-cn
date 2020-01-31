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
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813190"
---
# <a name="rate-limits"></a><span data-ttu-id="a243f-103">速率限制</span><span class="sxs-lookup"><span data-stu-id="a243f-103">Rate Limits</span></span>

<span data-ttu-id="a243f-104">NuGet.org API 强制实施速率限制以防止滥用。</span><span class="sxs-lookup"><span data-stu-id="a243f-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="a243f-105">超出速率限制的请求会返回以下错误：</span><span class="sxs-lookup"><span data-stu-id="a243f-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="a243f-106">除了使用速率限制进行请求限制之外，某些 Api 还强制执行配额。</span><span class="sxs-lookup"><span data-stu-id="a243f-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="a243f-107">超过配额的请求会返回以下错误：</span><span class="sxs-lookup"><span data-stu-id="a243f-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="a243f-108">下表列出了 NuGet.org API 的速率限制。</span><span class="sxs-lookup"><span data-stu-id="a243f-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="a243f-109">包搜索</span><span class="sxs-lookup"><span data-stu-id="a243f-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="a243f-110">建议使用 NuGet 的[V3 搜索 api](search-query-service-resource.md) ，因为它当前未进行速率限制。</span><span class="sxs-lookup"><span data-stu-id="a243f-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="a243f-111">对于 V1 和 V2 搜索 Api，以下限制适用：</span><span class="sxs-lookup"><span data-stu-id="a243f-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="a243f-112">API</span><span class="sxs-lookup"><span data-stu-id="a243f-112">API</span></span> | <span data-ttu-id="a243f-113">限制类型</span><span class="sxs-lookup"><span data-stu-id="a243f-113">Limit Type</span></span> | <span data-ttu-id="a243f-114">限制值</span><span class="sxs-lookup"><span data-stu-id="a243f-114">Limit Value</span></span> | <span data-ttu-id="a243f-115">API 用例</span><span class="sxs-lookup"><span data-stu-id="a243f-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="a243f-116">**获取**`/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="a243f-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="a243f-117">IP</span><span class="sxs-lookup"><span data-stu-id="a243f-117">IP</span></span> | <span data-ttu-id="a243f-118">1000/分钟</span><span class="sxs-lookup"><span data-stu-id="a243f-118">1000 / minute</span></span> | <span data-ttu-id="a243f-119">通过 v1 OData 查询 NuGet 包元数据 `Packages` 收集</span><span class="sxs-lookup"><span data-stu-id="a243f-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="a243f-120">**获取**`/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="a243f-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="a243f-121">IP</span><span class="sxs-lookup"><span data-stu-id="a243f-121">IP</span></span> | <span data-ttu-id="a243f-122">3000/分钟</span><span class="sxs-lookup"><span data-stu-id="a243f-122">3000 / minute</span></span> | <span data-ttu-id="a243f-123">通过 v1 搜索终结点搜索 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="a243f-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="a243f-124">**获取**`/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="a243f-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="a243f-125">IP</span><span class="sxs-lookup"><span data-stu-id="a243f-125">IP</span></span> | <span data-ttu-id="a243f-126">20000/分钟</span><span class="sxs-lookup"><span data-stu-id="a243f-126">20000 / minute</span></span> | <span data-ttu-id="a243f-127">通过 v2 OData `Packages` 收集查询 NuGet 包元数据</span><span class="sxs-lookup"><span data-stu-id="a243f-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="a243f-128">**获取**`/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="a243f-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="a243f-129">IP</span><span class="sxs-lookup"><span data-stu-id="a243f-129">IP</span></span> | <span data-ttu-id="a243f-130">100/分钟</span><span class="sxs-lookup"><span data-stu-id="a243f-130">100 / minute</span></span> | <span data-ttu-id="a243f-131">通过 v2 OData 查询 NuGet 包计数 `Packages` 收集</span><span class="sxs-lookup"><span data-stu-id="a243f-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="a243f-132">包推送和取消列出</span><span class="sxs-lookup"><span data-stu-id="a243f-132">Package Push and Unlist</span></span>

| <span data-ttu-id="a243f-133">API</span><span class="sxs-lookup"><span data-stu-id="a243f-133">API</span></span> | <span data-ttu-id="a243f-134">限制类型</span><span class="sxs-lookup"><span data-stu-id="a243f-134">Limit Type</span></span> | <span data-ttu-id="a243f-135">限制值</span><span class="sxs-lookup"><span data-stu-id="a243f-135">Limit Value</span></span> | <span data-ttu-id="a243f-136">API 用例</span><span class="sxs-lookup"><span data-stu-id="a243f-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="a243f-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="a243f-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="a243f-138">API 密钥</span><span class="sxs-lookup"><span data-stu-id="a243f-138">API Key</span></span> | <span data-ttu-id="a243f-139">350/小时</span><span class="sxs-lookup"><span data-stu-id="a243f-139">350 / hour</span></span> | <span data-ttu-id="a243f-140">通过 v2 推送终结点上传新的 NuGet 包（版本）</span><span class="sxs-lookup"><span data-stu-id="a243f-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="a243f-141">**删除**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="a243f-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="a243f-142">API 密钥</span><span class="sxs-lookup"><span data-stu-id="a243f-142">API Key</span></span> | <span data-ttu-id="a243f-143">250/小时</span><span class="sxs-lookup"><span data-stu-id="a243f-143">250 / hour</span></span> | <span data-ttu-id="a243f-144">通过 v2 终结点取消列出 NuGet 包（版本）</span><span class="sxs-lookup"><span data-stu-id="a243f-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
