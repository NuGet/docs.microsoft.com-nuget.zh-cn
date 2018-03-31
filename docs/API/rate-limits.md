---
title: 速率限制 |Microsoft 文档
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet Api 将强制实施速率限制以防止滥用行为。
keywords: NuGet API，速率限制
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a><span data-ttu-id="39b1e-104">速率限制</span><span class="sxs-lookup"><span data-stu-id="39b1e-104">Rate Limits</span></span>

<span data-ttu-id="39b1e-105">NuGet.org API 强制实施速率限制以防止滥用行为。</span><span class="sxs-lookup"><span data-stu-id="39b1e-105">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="39b1e-106">超过速率限制的请求将返回以下错误：</span><span class="sxs-lookup"><span data-stu-id="39b1e-106">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="39b1e-107">下表列出 NuGet.org API 速率限制。</span><span class="sxs-lookup"><span data-stu-id="39b1e-107">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="39b1e-108">包搜索</span><span class="sxs-lookup"><span data-stu-id="39b1e-108">Package search</span></span>

> [!Note]
> <span data-ttu-id="39b1e-109">我们建议使用 NuGet.org 的[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)搜索高性能且不具有任何将限制当前。</span><span class="sxs-lookup"><span data-stu-id="39b1e-109">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="39b1e-110">V1 和 V2 搜索 Api，followins 限制适用：</span><span class="sxs-lookup"><span data-stu-id="39b1e-110">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="39b1e-111">API</span><span class="sxs-lookup"><span data-stu-id="39b1e-111">API</span></span> | <span data-ttu-id="39b1e-112">限制类型</span><span class="sxs-lookup"><span data-stu-id="39b1e-112">Limit Type</span></span> | <span data-ttu-id="39b1e-113">限制值</span><span class="sxs-lookup"><span data-stu-id="39b1e-113">Limit Value</span></span> | <span data-ttu-id="39b1e-114">API 用例</span><span class="sxs-lookup"><span data-stu-id="39b1e-114">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="39b1e-115">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="39b1e-115">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="39b1e-116">IP</span><span class="sxs-lookup"><span data-stu-id="39b1e-116">IP</span></span> | <span data-ttu-id="39b1e-117">1000 / 分钟</span><span class="sxs-lookup"><span data-stu-id="39b1e-117">1000 / minute</span></span> | <span data-ttu-id="39b1e-118">查询通过 v1 OData 的 NuGet 包元数据`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="39b1e-118">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="39b1e-119">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="39b1e-119">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="39b1e-120">IP</span><span class="sxs-lookup"><span data-stu-id="39b1e-120">IP</span></span> | <span data-ttu-id="39b1e-121">3000 / 分钟</span><span class="sxs-lookup"><span data-stu-id="39b1e-121">3000 / minute</span></span> | <span data-ttu-id="39b1e-122">搜索通过 v1 搜索终结点的 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="39b1e-122">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="39b1e-123">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="39b1e-123">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="39b1e-124">IP</span><span class="sxs-lookup"><span data-stu-id="39b1e-124">IP</span></span> | <span data-ttu-id="39b1e-125">20000 / 分钟</span><span class="sxs-lookup"><span data-stu-id="39b1e-125">20000 / minute</span></span> | <span data-ttu-id="39b1e-126">查询通过 v2 OData 的 NuGet 包元数据`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="39b1e-126">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="39b1e-127">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="39b1e-127">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="39b1e-128">IP</span><span class="sxs-lookup"><span data-stu-id="39b1e-128">IP</span></span> | <span data-ttu-id="39b1e-129">100 / 分钟</span><span class="sxs-lookup"><span data-stu-id="39b1e-129">100 / minute</span></span> | <span data-ttu-id="39b1e-130">查询通过 v2 OData 的 NuGet 包计数`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="39b1e-130">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="39b1e-131">包推送和不列出</span><span class="sxs-lookup"><span data-stu-id="39b1e-131">Package Push and Unlist</span></span>

| <span data-ttu-id="39b1e-132">API</span><span class="sxs-lookup"><span data-stu-id="39b1e-132">API</span></span> | <span data-ttu-id="39b1e-133">限制类型</span><span class="sxs-lookup"><span data-stu-id="39b1e-133">Limit Type</span></span> | <span data-ttu-id="39b1e-134">限制值</span><span class="sxs-lookup"><span data-stu-id="39b1e-134">Limit Value</span></span> | <span data-ttu-id="39b1e-135">APU 用例</span><span class="sxs-lookup"><span data-stu-id="39b1e-135">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="39b1e-136">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="39b1e-136">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="39b1e-137">API 密钥</span><span class="sxs-lookup"><span data-stu-id="39b1e-137">API Key</span></span> | <span data-ttu-id="39b1e-138">100 / 分钟</span><span class="sxs-lookup"><span data-stu-id="39b1e-138">100 / minute</span></span> | <span data-ttu-id="39b1e-139">上载新 NuGet 包 （版本） 通过 v2 推送终结点</span><span class="sxs-lookup"><span data-stu-id="39b1e-139">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="39b1e-140">**删除** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="39b1e-140">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="39b1e-141">API 密钥</span><span class="sxs-lookup"><span data-stu-id="39b1e-141">API Key</span></span> | <span data-ttu-id="39b1e-142">100 / 分钟</span><span class="sxs-lookup"><span data-stu-id="39b1e-142">100 / minute</span></span> | <span data-ttu-id="39b1e-143">不列出通过 v2 终结点的 NuGet 包 （版本）</span><span class="sxs-lookup"><span data-stu-id="39b1e-143">Unlist a NuGet package (version) via v2 endpoint</span></span> 
