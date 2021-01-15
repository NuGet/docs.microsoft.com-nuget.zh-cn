---
title: NuGet 客户端 SDK
description: 此 API 已发展，但尚未记录在 Dave Glick 的博客上。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 0eca8478b4d6509dbc1407560d2c86069c7575dd
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235732"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="f619a-103">NuGet 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="f619a-103">NuGet Client SDK</span></span>

<span data-ttu-id="f619a-104">*Nuget 客户端 SDK* 引用一组 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="f619a-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="f619a-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -用于与基于 HTTP 和文件的 NuGet 源交互</span><span class="sxs-lookup"><span data-stu-id="f619a-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="f619a-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -用于与 NuGet 包交互。</span><span class="sxs-lookup"><span data-stu-id="f619a-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="f619a-107">`NuGet.Protocol` 依赖于此包</span><span class="sxs-lookup"><span data-stu-id="f619a-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="f619a-108">你可以在 [NuGet/nuget。客户端](https://github.com/NuGet/NuGet.Client) GitHub 存储库中找到这些包的源代码。</span><span class="sxs-lookup"><span data-stu-id="f619a-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="f619a-109">可以在 GitHub 上的 [nuget.exe](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) 项目中找到这些示例的源代码。</span><span class="sxs-lookup"><span data-stu-id="f619a-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="f619a-110">有关 NuGet 服务器协议的文档，请参阅 [Nuget 服务器 API](~/api/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f619a-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="f619a-111">NuGet。协议</span><span class="sxs-lookup"><span data-stu-id="f619a-111">NuGet.Protocol</span></span>

<span data-ttu-id="f619a-112">安装 `NuGet.Protocol` 包以与 HTTP 和基于文件夹的 NuGet 包源交互：</span><span class="sxs-lookup"><span data-stu-id="f619a-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

### <a name="list-package-versions"></a><span data-ttu-id="f619a-113">列出包版本</span><span class="sxs-lookup"><span data-stu-id="f619a-113">List package versions</span></span>

<span data-ttu-id="f619a-114">使用 [NuGet V3 包内容 API](../api/package-base-address-resource.md#enumerate-package-versions)查找 Newtonsoft.Js的所有版本：</span><span class="sxs-lookup"><span data-stu-id="f619a-114">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="f619a-115">下载包</span><span class="sxs-lookup"><span data-stu-id="f619a-115">Download a package</span></span>

<span data-ttu-id="f619a-116">使用 [NuGet V3 包内容 API](../api/package-base-address-resource.md)在12.0.1 上下载 Newtonsoft.Js：</span><span class="sxs-lookup"><span data-stu-id="f619a-116">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="f619a-117">获取包元数据</span><span class="sxs-lookup"><span data-stu-id="f619a-117">Get package metadata</span></span>

<span data-ttu-id="f619a-118">使用 [NuGet V3 包元数据 API](../api/registration-base-url-resource.md)获取 "Newtonsoft.Json" 包的元数据：</span><span class="sxs-lookup"><span data-stu-id="f619a-118">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="f619a-119">搜索包</span><span class="sxs-lookup"><span data-stu-id="f619a-119">Search packages</span></span>

<span data-ttu-id="f619a-120">使用 [NuGet V3 搜索 API](../api/search-query-service-resource.md)搜索 "json" 包：</span><span class="sxs-lookup"><span data-stu-id="f619a-120">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="f619a-121">推送包</span><span class="sxs-lookup"><span data-stu-id="f619a-121">Push a package</span></span>

<span data-ttu-id="f619a-122">使用 [NuGet V3 推送和删除 API](../api/package-publish-resource.md)推送包：</span><span class="sxs-lookup"><span data-stu-id="f619a-122">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="f619a-123">删除包</span><span class="sxs-lookup"><span data-stu-id="f619a-123">Delete a package</span></span>

<span data-ttu-id="f619a-124">使用 [NuGet V3 推送和删除 API](../api/package-publish-resource.md)删除包：</span><span class="sxs-lookup"><span data-stu-id="f619a-124">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="f619a-125">NuGet 服务器可以自由地将包删除请求解释为 "硬删除"、"软删除" 或 "取消列出"。</span><span class="sxs-lookup"><span data-stu-id="f619a-125">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="f619a-126">例如，nuget.org 将包删除请求解释为 "取消列出"。</span><span class="sxs-lookup"><span data-stu-id="f619a-126">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="f619a-127">有关这种做法的详细信息，请参阅 [删除包](../nuget-org/policies/deleting-packages.md) 策略。</span><span class="sxs-lookup"><span data-stu-id="f619a-127">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="f619a-128">使用经过身份验证的源</span><span class="sxs-lookup"><span data-stu-id="f619a-128">Work with authenticated feeds</span></span>

<span data-ttu-id="f619a-129">用于 [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) 处理已验证的源。</span><span class="sxs-lookup"><span data-stu-id="f619a-129">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="f619a-130">NuGet。打包</span><span class="sxs-lookup"><span data-stu-id="f619a-130">NuGet.Packaging</span></span>

<span data-ttu-id="f619a-131">安装 `NuGet.Packaging` 包以与 `.nupkg` `.nuspec` 流中的文件进行交互：</span><span class="sxs-lookup"><span data-stu-id="f619a-131">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="f619a-132">创建包</span><span class="sxs-lookup"><span data-stu-id="f619a-132">Create a package</span></span>

<span data-ttu-id="f619a-133">使用创建包、设置元数据并添加依赖项 [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) 。</span><span class="sxs-lookup"><span data-stu-id="f619a-133">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f619a-134">强烈建议使用官方 NuGet 工具创建 NuGet 包，而 **不** 是使用此低级别 API。</span><span class="sxs-lookup"><span data-stu-id="f619a-134">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="f619a-135">很多特性对于格式正确的包都很重要，最新版本的工具有助于合并这些最佳做法。</span><span class="sxs-lookup"><span data-stu-id="f619a-135">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="f619a-136">有关创建 NuGet 包的详细信息，请参阅 [包创建工作流](../create-packages/overview-and-workflow.md) 概述和官方包工具文档 (例如， [使用 dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)) 。</span><span class="sxs-lookup"><span data-stu-id="f619a-136">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="f619a-137">读取包</span><span class="sxs-lookup"><span data-stu-id="f619a-137">Read a package</span></span>

<span data-ttu-id="f619a-138">使用从文件流中读取包 [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) 。</span><span class="sxs-lookup"><span data-stu-id="f619a-138">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="f619a-139">第三方文档</span><span class="sxs-lookup"><span data-stu-id="f619a-139">Third-party documentation</span></span>

<span data-ttu-id="f619a-140">可以在以下博客系列中的 Dave Glick （已发布2016：</span><span class="sxs-lookup"><span data-stu-id="f619a-140">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="f619a-141">浏览 NuGet v3 库，第1部分：简介和概念</span><span class="sxs-lookup"><span data-stu-id="f619a-141">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="f619a-142">浏览 NuGet v3 库，第2部分：搜索包</span><span class="sxs-lookup"><span data-stu-id="f619a-142">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="f619a-143">浏览 NuGet v3 库，第3部分：安装包</span><span class="sxs-lookup"><span data-stu-id="f619a-143">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="f619a-144">**3.4.3** 版本的 NuGet 客户端 SDK 包发布后，不久就会编写这些博客文章。</span><span class="sxs-lookup"><span data-stu-id="f619a-144">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="f619a-145">较新版本的包可能与博客文章中的信息不兼容。</span><span class="sxs-lookup"><span data-stu-id="f619a-145">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="f619a-146">圣马丁 Björkström 对 Dave Glick 的博客系列进行了跟进博客文章，其中介绍了使用 NuGet 客户端 SDK 安装 NuGet 包的不同方法：</span><span class="sxs-lookup"><span data-stu-id="f619a-146">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="f619a-147">重新进行 NuGet v3 库</span><span class="sxs-lookup"><span data-stu-id="f619a-147">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
