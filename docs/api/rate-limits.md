---
title: 速率限制，NuGet API
description: NuGet Api 将强制实施速率限制以防止滥用行为。
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: c5d3cf68ac6a96a6c14eb5e652bcf72698b6a8e8
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
ms.locfileid: "34225939"
---
# <a name="rate-limits"></a>速率限制

NuGet.org API 强制实施速率限制以防止滥用行为。 超过速率限制的请求将返回以下错误： 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

下表列出 NuGet.org API 速率限制。

## <a name="package-search"></a>包搜索

> [!Note]
> 我们建议使用 NuGet.org 的[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)搜索高性能且不具有任何将限制当前。 V1 和 V2 搜索 Api，followins 限制适用：


| API | 限制类型 | 限制值 | API 用例 |
|:---|:---|:---|:---|
**获取** `/api/v1/Packages` | IP | 1000 / 分钟 | 查询通过 v1 OData 的 NuGet 包元数据`Packages`集合 |
**获取** `/api/v1/Search()` | IP | 3000 / 分钟 | 搜索通过 v1 搜索终结点的 NuGet 包 | 
**获取** `/api/v2/Packages` | IP | 20000 / 分钟 | 查询通过 v2 OData 的 NuGet 包元数据`Packages`集合 | 
**获取** `/api/v2/Packages/$count` | IP | 100 / 分钟 | 查询通过 v2 OData 的 NuGet 包计数`Packages`集合 | 

## <a name="package-push-and-unlist"></a>包推送和不列出

| API | 限制类型 | 限制值 | API 用例 | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API 密钥 | 250 / 小时 | 上载新 NuGet 包 （版本） 通过 v2 推送终结点 
**删除** `/api/v2/package/{id}/{version}` | API 密钥 | 250 / 小时 | 不列出通过 v2 终结点的 NuGet 包 （版本） 
