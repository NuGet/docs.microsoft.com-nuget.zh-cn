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
# <a name="nuget-client-sdk"></a><span data-ttu-id="30034-103">NuGet 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="30034-103">NuGet Client SDK</span></span>

<span data-ttu-id="30034-104">*Nuget 客户端 SDK*引用一组 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="30034-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="30034-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -用于与基于 HTTP 和文件的 NuGet 源交互</span><span class="sxs-lookup"><span data-stu-id="30034-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="30034-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -用于与 NuGet 包交互。</span><span class="sxs-lookup"><span data-stu-id="30034-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="30034-107">`NuGet.Protocol` 依赖于此包</span><span class="sxs-lookup"><span data-stu-id="30034-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="30034-108">你可以在[NuGet/nuget。客户端](https://github.com/NuGet/NuGet.Client)GitHub 存储库中找到这些包的源代码。</span><span class="sxs-lookup"><span data-stu-id="30034-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="30034-109">有关 NuGet 服务器协议的文档，请参阅[Nuget 服务器 API](~/api/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="30034-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="30034-110">入门</span><span class="sxs-lookup"><span data-stu-id="30034-110">Getting started</span></span>

### <a name="install-the-package"></a><span data-ttu-id="30034-111">安装包</span><span class="sxs-lookup"><span data-stu-id="30034-111">Install the package</span></span>

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a><span data-ttu-id="30034-112">示例</span><span class="sxs-lookup"><span data-stu-id="30034-112">Examples</span></span>

<span data-ttu-id="30034-113">你可以在 GitHub 上的[nuget.exe](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples)项目上找到这些示例。</span><span class="sxs-lookup"><span data-stu-id="30034-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="30034-114">列出包版本</span><span class="sxs-lookup"><span data-stu-id="30034-114">List package versions</span></span>

<span data-ttu-id="30034-115">使用[NuGet V3 包内容 API](../api/package-base-address-resource.md#enumerate-package-versions)查找 newtonsoft.json 的所有版本：</span><span class="sxs-lookup"><span data-stu-id="30034-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="30034-116">下载包</span><span class="sxs-lookup"><span data-stu-id="30034-116">Download a package</span></span>

<span data-ttu-id="30034-117">使用[NuGet V3 包内容 API](../api/package-base-address-resource.md)下载 newtonsoft.json v 12.0.1：</span><span class="sxs-lookup"><span data-stu-id="30034-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="30034-118">获取包元数据</span><span class="sxs-lookup"><span data-stu-id="30034-118">Get package metadata</span></span>

<span data-ttu-id="30034-119">使用[NuGet V3 包元数据 API](../api/registration-base-url-resource.md)获取 "newtonsoft.json" 包的元数据：</span><span class="sxs-lookup"><span data-stu-id="30034-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="30034-120">搜索包</span><span class="sxs-lookup"><span data-stu-id="30034-120">Search packages</span></span>

<span data-ttu-id="30034-121">使用[NuGet V3 搜索 API](../api/search-query-service-resource.md)搜索 "json" 包：</span><span class="sxs-lookup"><span data-stu-id="30034-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a><span data-ttu-id="30034-122">第三方文档</span><span class="sxs-lookup"><span data-stu-id="30034-122">Third-party documentation</span></span>

<span data-ttu-id="30034-123">可以在以下博客系列中的 Dave Glick （已发布2016：</span><span class="sxs-lookup"><span data-stu-id="30034-123">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="30034-124">浏览 NuGet v3 库，第1部分：简介和概念</span><span class="sxs-lookup"><span data-stu-id="30034-124">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="30034-125">浏览 NuGet v3 库，第2部分：搜索包</span><span class="sxs-lookup"><span data-stu-id="30034-125">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="30034-126">浏览 NuGet v3 库，第3部分：安装包</span><span class="sxs-lookup"><span data-stu-id="30034-126">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="30034-127">**3.4.3**版本的 NuGet 客户端 SDK 包发布后，不久就会编写这些博客文章。</span><span class="sxs-lookup"><span data-stu-id="30034-127">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="30034-128">较新版本的包可能与博客文章中的信息不兼容。</span><span class="sxs-lookup"><span data-stu-id="30034-128">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="30034-129">圣马丁 Björkström 对 Dave Glick 的博客系列进行了跟进博客文章，其中介绍了使用 NuGet 客户端 SDK 安装 NuGet 包的不同方法：</span><span class="sxs-lookup"><span data-stu-id="30034-129">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="30034-130">重新进行 NuGet v3 库</span><span class="sxs-lookup"><span data-stu-id="30034-130">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
