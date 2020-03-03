---
title: NuGet 客户端 SDK
description: 此 API 已发展，但尚未记录在 Dave Glick 的博客上。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231235"
---
# <a name="nuget-client-sdk"></a>NuGet 客户端 SDK

*Nuget 客户端 SDK*引用一组 NuGet 包：

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -用于与基于 HTTP 和文件的 NuGet 源交互
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -用于与 NuGet 包交互。 `NuGet.Protocol` 依赖于此包

你可以在[NuGet/nuget。客户端](https://github.com/NuGet/NuGet.Client)GitHub 存储库中找到这些包的源代码。

> [!Note]
> 有关 NuGet 服务器协议的文档，请参阅[Nuget 服务器 API](~/api/overview.md)。

## <a name="getting-started"></a>入门

### <a name="install-the-package"></a>安装包

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a>示例

你可以在 GitHub 上的[nuget.exe](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples)项目上找到这些示例。

### <a name="list-package-versions"></a>列出包版本

使用[NuGet V3 包内容 API](../api/package-base-address-resource.md#enumerate-package-versions)查找 newtonsoft.json 的所有版本：

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>下载包

使用[NuGet V3 包内容 API](../api/package-base-address-resource.md)下载 newtonsoft.json v 12.0.1：

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>获取包元数据

使用[NuGet V3 包元数据 API](../api/registration-base-url-resource.md)获取 "newtonsoft.json" 包的元数据：

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>搜索包

使用[NuGet V3 搜索 API](../api/search-query-service-resource.md)搜索 "json" 包：

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a>第三方文档

可以在以下博客系列中的 Dave Glick （已发布2016：

- [浏览 NuGet v3 库，第1部分：简介和概念](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [浏览 NuGet v3 库，第2部分：搜索包](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [浏览 NuGet v3 库，第3部分：安装包](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> **3.4.3**版本的 NuGet 客户端 SDK 包发布后，不久就会编写这些博客文章。
> 较新版本的包可能与博客文章中的信息不兼容。

圣马丁 Björkström 对 Dave Glick 的博客系列进行了跟进博客文章，其中介绍了使用 NuGet 客户端 SDK 安装 NuGet 包的不同方法：

- [重新进行 NuGet v3 库](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
