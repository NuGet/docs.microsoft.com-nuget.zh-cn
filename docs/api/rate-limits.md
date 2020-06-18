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
**GET** `/api/v1/Packages` | IP | 1000/分钟 | 通过 v1 OData 集合查询 NuGet 包元数据 `Packages` |
**GET** `/api/v1/Search()` | IP | 3000/分钟 | 通过 v1 搜索终结点搜索 NuGet 包 | 
**GET** `/api/v2/Packages` | IP | 20000/分钟 | 通过 v2 OData 集合查询 NuGet 包元数据 `Packages` | 
**GET** `/api/v2/Packages/$count` | IP | 100/分钟 | 通过 v2 OData 集合查询 NuGet 包计数 `Packages` | 

## <a name="package-push-and-unlist"></a>包推送和取消列出

| API | 限制类型 | 限制值 | API 用例 | 
|:---|:---|:---|:--- |
**PUT**`/api/v2/package` | API 密钥 | 350/小时 | 通过 v2 推送终结点上传新的 NuGet 包（版本） 
**删除**`/api/v2/package/{id}/{version}` | API 密钥 | 250/小时 | 通过 v2 终结点取消列出 NuGet 包（版本） 

## <a name="nugetorg-website-page-views"></a>nuget.org 网站页面视图

如果以编程方式访问 nuget.org 网页，请考虑调查我们记录的[V3 api](overview.md)。 通过这些终结点，可以更简单地访问包元数据和内容。 V3 API 具有更好的可用性，性能高于访问 NuGet 库网页（专为 web 浏览器交互）。

| API | 限制类型 | 限制值 | API 用例 | 
|:---|:---|:---|:--- |
**GET** `/package/{id}/{version}` | IP | 50/分钟 | 显示包（版本）详细信息页。 
