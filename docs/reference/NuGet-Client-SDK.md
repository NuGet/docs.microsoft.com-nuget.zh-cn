---
title: NuGet 客户端 SDK
description: 该 API 是不断变化且不尚有记录，但示例 Dave Glick 博客上可用。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 8f96bf289e8121fd25262fb95c2f36dfc89045c5
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911031"
---
# <a name="nuget-client-sdk"></a>NuGet 客户端 SDK

> [!Note]
> 无法与相混淆[NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)

*NuGet 客户端 SDK*表示一组.NET 库围绕[NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands)， [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging)，和[NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol). 这些包替换较早[NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)库。

我们正在努力具有稳定的表面区域，我们很快就可以记录。

## <a name="source-code"></a>源代码

在项目中 GitHub 上已发布的源代码[NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client)。

## <a name="third-party-documentation"></a>第三方文档

以下博客系列由 Dave Glick，发布 2016年中，可以找到示例和文档的某些 API:

- [探索 NuGet v3 库，第 1 部分：简介和概念](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [探索 NuGet v3 库，第 2 部分：搜索包](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [探索 NuGet v3 库，第 3 部分：安装包](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> 这些博客文章编写后不久**3.4.3** NuGet 客户端 SDK 包已发布的版本。
> 包的较新版本可能与博客文章中的信息不兼容。

Martin Björkström 未到 Dave Glick 博客系列的后续博客文章，他介绍了不同的方法上使用 NuGet 客户端 SDK 安装 NuGet 包：

- [再探 NuGet v3 库](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
