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
# <a name="rate-limits"></a>速率限制

NuGet.org API 强制实施速率限制以防止滥用。 超出速率限制的请求会返回以下错误： 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

除了使用速率限制进行请求限制之外，某些 Api 还强制执行配额。 超过配额的请求会返回以下错误：

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

下表列出了 NuGet.org API 的速率限制。

## <a name="package-search"></a>包搜索

> [!Note]
> 建议使用 NuGet 的[V3 搜索 api](search-query-service-resource.md) ，因为它当前未进行速率限制。 对于 V1 和 V2 搜索 Api，以下限制适用：

| API | 限制类型 | 限制值 | API 用例 |
|:---|:---|:---|:---|
**获取**`/api/v1/Packages` | IP | 1000/分钟 | 通过 v1 OData 查询 NuGet 包元数据 `Packages` 收集 |
**获取**`/api/v1/Search()` | IP | 3000/分钟 | 通过 v1 搜索终结点搜索 NuGet 包 | 
**获取**`/api/v2/Packages` | IP | 20000/分钟 | 通过 v2 OData `Packages` 收集查询 NuGet 包元数据 | 
**获取**`/api/v2/Packages/$count` | IP | 100/分钟 | 通过 v2 OData 查询 NuGet 包计数 `Packages` 收集 | 

## <a name="package-push-and-unlist"></a>包推送和取消列出

| API | 限制类型 | 限制值 | API 用例 | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API 密钥 | 350/小时 | 通过 v2 推送终结点上传新的 NuGet 包（版本） 
**删除**`/api/v2/package/{id}/{version}` | API 密钥 | 250/小时 | 通过 v2 终结点取消列出 NuGet 包（版本） 
