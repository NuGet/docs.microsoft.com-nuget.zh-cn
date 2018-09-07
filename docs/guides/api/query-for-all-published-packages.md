---
title: 查询所有发布到 nuget.org 的包
description: 使用 NuGet API 可以查询所有发布到 nuget.org 的包并随着时间推移保持最新状态。
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 0bd21c427b5b89ae9e5f1500d75e1bf63a96e828
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551073"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>查询所有发布到 nuget.org 的包

旧版 OData V2 API 上一个常见查询模式为枚举所有发布到 nuget.org 的包，按照包发布的时间排序。 需要这类针对 nuget.org 的查询的情况多种多样：

- 完全复制 nuget.org
- 检测包发布新版本的时间
- 查找依赖包的包

执行此操作的老式方法通常依靠按照时间戳对 OData 包实体进行排序并且用 `skip` 和 `top`（页大小）参数跨大型结果集进行分页。 遗憾的是，这种方法有一些缺点：

- 可能会丢失包，因为查询的对象为常常更改顺序的数据
- 查询响应时间长，因为查询未优化（最优化的查询支持官方 NuGet 客户端的主流场景）
- 使用弃用和未记录的 API，意味着将来不保证支持此类查询
- 不能按照发生的确切顺序重播历史记录

因此，可以遵循以下指南以更加可靠新颖的方法解决上述情况。

## <a name="overview"></a>概述

本指南的中心是 [NuGet API](../../api/overview.md) 中称为“目录”的资源。 目录是仅限追加的 API，它允许调用方查看在 nuget.org 中添加、修改和删除的包的完整历史记录。如果对发布到 nuget.org 的所有包甚至是包的子集感兴趣，则最好用目录来跟进了解当前可用的包集。

本指南旨在提供高级演练，如果你对目录的详情细节感兴趣，请参阅它的 [API 引用文档](../../api/catalog-resource.md)。

以下步骤可以选择任意的编程语言来执行。 如果需要完整的运行示例，请查看下面提及的 [C# 示例](#c-sample-code)。

反之，按照以下指南生成可靠的目录阅读器。

## <a name="initialize-a-cursor"></a>初始化游标

生成可靠目录阅读器的第一步是实现游标。 有关目录游标设计的完整详细信息，请参阅[目录引用文档](../../api/catalog-resource.md#cursor)。 简而言之，游标是时间中的某一点，你在目录中处理事件直到该点。 目录中的事件表示包发布和其他包更改。 如果你关注（从一开始）发布到 NuGet 的所有包，那么将游标初始化为“最小值”时间戳（例如 .NET 中的 `DateTime.MinValue`）。 如果仅关注现在开始发布的包，则使用当前时间戳作为初始游标值。

对于本指南，我们要将游标初始化为一小时前的时间戳。 现在，只需在内存中保存时间戳。

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>确定目录索引 URL

NuGet API 中每个资源（终结点）的位置应使用[服务索引](../../api/service-index.md)发现。 因为本指南重点介绍 nuget.org，所以我们使用 nuget.org 的服务索引。

    GET https://api.nuget.org/v3/index.json

服务文档是包含 nuget.org 上所有资源的 JSON 文档。查找具有 `Catalog/3.0.0` 的 `@type` 属性值的资源。 相关联的 `@id` 属性值是到目录索引本身的 URL。 

## <a name="find-new-catalog-leaves"></a>查找新的目录叶

使用前面步骤中找到的 `@id` 属性值下载目录索引：

    GET https://api.nuget.org/v3/catalog0/index.json

反序列化[目录索引](../../api/catalog-resource.md#catalog-index)。 筛选出 `commitTimeStamp` 小于或等于当前游标值的所有[目录页对象](../../api/catalog-resource.md#catalog-page-object-in-the-index)。

对于每个剩余的目录页，使用 `@id` 属性下载完整文档。

    GET https://api.nuget.org/v3/catalog0/page2926.json

反序列化[目录页](../../api/catalog-resource.md#catalog-page)。 筛选出 `commitTimeStamp` 小于或等于当前游标值的所有[目录叶对象](../../api/catalog-resource.md#catalog-item-object-in-a-page)。

在下载没有筛选出的所有目录页之后，你会具有目录叶对象集，用于表示在游标时间戳和现在时间之间已发布的、未列出、已列出或删除的包。

## <a name="process-catalog-leaves"></a>处理目录叶

此时，可以对目录项执行任何自定义处理。 如果只需要包的 ID 和版本，则可以在页中找到的目录项对象上检查 `nuget:id` 和 `nuget:version` 属性。 请务必查看 `@type` 属性，了解目录项是否涉及现有包或者删除包。

如果对有关包的元数据感兴趣（例如描述、依赖项、.nupkg 大小等），则可以使用 `@id` 属性提取[目录叶文档](../../api/catalog-resource.md#catalog-leaf)。

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

本文档不仅有[包元数据资源](../../api/registration-base-url-resource.md)中包含的所有元数据，而且还有更多内容！

通过该步骤可以实现自定义逻辑。 无论要使用目录叶来做什么，本指南中的其他步骤也以大致相同的方法实现。

### <a name="downloading-the-nupkg"></a>下载 .nupkg

如果对下载目录中找到的包的 .nupkg 感兴趣，那么可以使用[包内容资源](../../api/package-base-address-resource.md)。 但请注意，在目录中找到包和包在包内容资源中可用之间有短暂的延迟。 所以，如果在尝试下载目录中找到的包的 .nupkg 时遇到 `404 Not Found`，只需稍后进行重试。 由 GitHub 问题 [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455) 跟踪此延迟的修复。

## <a name="move-the-cursor-forward"></a>向前移动游标

成功处理目录项后，需要确定要保存的新游标值。 为了执行此操作，请找到处理的所有目录项的最大（按最新时间顺序） `commitTimeStamp`。 这是新的游标值。 将其保存到某些永久存储中，例如数据库、文件系统或 blob 存储。 当需要获取更多目录项时，只需通过从此永久存储中初始化游标值从[第一步](#initialize-a-cursor)开始。

如果应用程序引发异常或错误，请勿向前移动游标。 向前移动游标意味着不再需要处理游标前的目录项。

如果某些原因导致处理目录叶的方式有错误，只需及时向后移动游标并允许代码重新处理旧的目录项。

## <a name="c-sample-code"></a>C# 示例代码

因为目录是可以通过 HTTP 获得的 JSON 文档集，所以可以使用有 HTTP 客户端和 JSON 反序列化程序的任意编程语言与之交互。

C# 示例可在 [NuGet/示例存储库](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample)中获得。

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>目录 SDK

使用目录最简单的方法是使用预发布 .NET 目录 SDK 包：[NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog)。 此包可在 `nuget-build` MyGet 源`https://dotnet.myget.org/F/nuget-build/api/v3/index.json`上获得，可以使用 NuGet 包源 URL 找到该源。

可以将此包安装到与 `netstandard1.3` 或更高版本（例如 .NET Framework 4.6）兼容的项目。

使用此包的示例可在 [NuGet.Protocol.Catalog.Sample 项目](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample)中的 GitHub 上获得。

#### <a name="sample-output"></a>示例输出

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a>最小示例

有关详细说明与目录交互的较少依赖项的示例，请参阅 [CatalogReaderExample 示例项目](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample)。 项目面向 `netcoreapp2.0` 并依赖 [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0)（适用于解析服务索引）和 [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1)（适用于 JSON 序列化）。

代码的主要逻辑在 [Program.cs 文件](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs)中可见。

#### <a name="sample-output"></a>示例输出

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
