---
title: 速率限制，NuGet API
description: NuGet Api 将强制实施速率限制来防止滥用。
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548672"
---
# <a name="rate-limits"></a><span data-ttu-id="48972-103">速率限制</span><span class="sxs-lookup"><span data-stu-id="48972-103">Rate Limits</span></span>

<span data-ttu-id="48972-104">NuGet.org API 强制实施速率限制以防止滥用。</span><span class="sxs-lookup"><span data-stu-id="48972-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="48972-105">超出速率限制的请求返回以下错误：</span><span class="sxs-lookup"><span data-stu-id="48972-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="48972-106">除了请求限制使用速率限制，某些 Api 还强制实施配额。</span><span class="sxs-lookup"><span data-stu-id="48972-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="48972-107">超出配额的请求返回以下错误：</span><span class="sxs-lookup"><span data-stu-id="48972-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="48972-108">下表列出 NuGet.org api 速率限制。</span><span class="sxs-lookup"><span data-stu-id="48972-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="48972-109">包搜索</span><span class="sxs-lookup"><span data-stu-id="48972-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="48972-110">我们建议使用 NuGet.org 的[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)是高性能且不安装任何搜索将限制当前。</span><span class="sxs-lookup"><span data-stu-id="48972-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="48972-111">有关 V1 和 V2 搜索 Api、 followins 限制适用：</span><span class="sxs-lookup"><span data-stu-id="48972-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="48972-112">API</span><span class="sxs-lookup"><span data-stu-id="48972-112">API</span></span> | <span data-ttu-id="48972-113">限制类型</span><span class="sxs-lookup"><span data-stu-id="48972-113">Limit Type</span></span> | <span data-ttu-id="48972-114">限制值</span><span class="sxs-lookup"><span data-stu-id="48972-114">Limit Value</span></span> | <span data-ttu-id="48972-115">API 用例</span><span class="sxs-lookup"><span data-stu-id="48972-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="48972-116">**获取** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="48972-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="48972-117">IP</span><span class="sxs-lookup"><span data-stu-id="48972-117">IP</span></span> | <span data-ttu-id="48972-118">1000 / 分钟</span><span class="sxs-lookup"><span data-stu-id="48972-118">1000 / minute</span></span> | <span data-ttu-id="48972-119">查询通过 v1 OData 的 NuGet 包元数据`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="48972-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="48972-120">**获取** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="48972-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="48972-121">IP</span><span class="sxs-lookup"><span data-stu-id="48972-121">IP</span></span> | <span data-ttu-id="48972-122">3000 / 分钟</span><span class="sxs-lookup"><span data-stu-id="48972-122">3000 / minute</span></span> | <span data-ttu-id="48972-123">搜索通过 v1 搜索终结点的 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="48972-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="48972-124">**获取** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="48972-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="48972-125">IP</span><span class="sxs-lookup"><span data-stu-id="48972-125">IP</span></span> | <span data-ttu-id="48972-126">20000 / 分钟</span><span class="sxs-lookup"><span data-stu-id="48972-126">20000 / minute</span></span> | <span data-ttu-id="48972-127">查询通过 v2 OData 的 NuGet 包元数据`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="48972-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="48972-128">**获取** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="48972-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="48972-129">IP</span><span class="sxs-lookup"><span data-stu-id="48972-129">IP</span></span> | <span data-ttu-id="48972-130">100 / 分钟</span><span class="sxs-lookup"><span data-stu-id="48972-130">100 / minute</span></span> | <span data-ttu-id="48972-131">查询通过 v2 OData 的 NuGet 包计数`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="48972-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="48972-132">包推送和取消列出</span><span class="sxs-lookup"><span data-stu-id="48972-132">Package Push and Unlist</span></span>

| <span data-ttu-id="48972-133">API</span><span class="sxs-lookup"><span data-stu-id="48972-133">API</span></span> | <span data-ttu-id="48972-134">限制类型</span><span class="sxs-lookup"><span data-stu-id="48972-134">Limit Type</span></span> | <span data-ttu-id="48972-135">限制值</span><span class="sxs-lookup"><span data-stu-id="48972-135">Limit Value</span></span> | <span data-ttu-id="48972-136">API 用例</span><span class="sxs-lookup"><span data-stu-id="48972-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="48972-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="48972-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="48972-138">API 密钥</span><span class="sxs-lookup"><span data-stu-id="48972-138">API Key</span></span> | <span data-ttu-id="48972-139">250 / 小时</span><span class="sxs-lookup"><span data-stu-id="48972-139">250 / hour</span></span> | <span data-ttu-id="48972-140">上传通过 v2 推送终结点的新 NuGet 包 （版本）</span><span class="sxs-lookup"><span data-stu-id="48972-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="48972-141">**删除** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="48972-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="48972-142">API 密钥</span><span class="sxs-lookup"><span data-stu-id="48972-142">API Key</span></span> | <span data-ttu-id="48972-143">250 / 小时</span><span class="sxs-lookup"><span data-stu-id="48972-143">250 / hour</span></span> | <span data-ttu-id="48972-144">取消列出通过 v2 终结点的 NuGet 包 （版本）</span><span class="sxs-lookup"><span data-stu-id="48972-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
