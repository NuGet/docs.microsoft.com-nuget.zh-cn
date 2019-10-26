---
title: NuGet 客户端 SDK
description: 此 API 已发展，但尚未记录在 Dave Glick 的博客上。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924602"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="5b1cb-103">NuGet 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="5b1cb-103">NuGet Client SDK</span></span>

<span data-ttu-id="5b1cb-104">*Nuget 客户端 SDK*指的是一组以[nuget. 命令](https://www.nuget.org/packages/NuGet.Commands)、 [nuget](https://www.nuget.org/packages/NuGet.Packaging)和[nuget](https://www.nuget.org/packages/NuGet.Protocol)为中心的 nuget 包。</span><span class="sxs-lookup"><span data-stu-id="5b1cb-104">The *NuGet Client SDK* refers to a group of NuGet packages centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="5b1cb-105">这些包将替换前面的[NuGet](https://www.nuget.org/packages/NuGet.Core/)库。</span><span class="sxs-lookup"><span data-stu-id="5b1cb-105">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

> [!Note]
>  <span data-ttu-id="5b1cb-106">有关 NuGet 服务器协议的文档，请参阅[Nuget 服务器 API](~/api/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5b1cb-106">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="source-code"></a><span data-ttu-id="5b1cb-107">源代码</span><span class="sxs-lookup"><span data-stu-id="5b1cb-107">Source code</span></span>

<span data-ttu-id="5b1cb-108">源代码在 GitHub 上的项目[NuGet/nuget](https://github.com/NuGet/NuGet.Client)中发布。</span><span class="sxs-lookup"><span data-stu-id="5b1cb-108">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="5b1cb-109">第三方文档</span><span class="sxs-lookup"><span data-stu-id="5b1cb-109">Third-party documentation</span></span>

<span data-ttu-id="5b1cb-110">可以在以下博客系列中的 Dave Glick （已发布2016：</span><span class="sxs-lookup"><span data-stu-id="5b1cb-110">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="5b1cb-111">浏览 NuGet v3 库，第1部分：简介和概念</span><span class="sxs-lookup"><span data-stu-id="5b1cb-111">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="5b1cb-112">浏览 NuGet v3 库，第2部分：搜索包</span><span class="sxs-lookup"><span data-stu-id="5b1cb-112">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="5b1cb-113">浏览 NuGet v3 库，第3部分：安装包</span><span class="sxs-lookup"><span data-stu-id="5b1cb-113">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="5b1cb-114">**3.4.3**版本的 NuGet 客户端 SDK 包发布后，不久就会编写这些博客文章。</span><span class="sxs-lookup"><span data-stu-id="5b1cb-114">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="5b1cb-115">较新版本的包可能与博客文章中的信息不兼容。</span><span class="sxs-lookup"><span data-stu-id="5b1cb-115">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="5b1cb-116">圣马丁 Björkström 对 Dave Glick 的博客系列进行了跟进博客文章，其中介绍了使用 NuGet 客户端 SDK 安装 NuGet 包的不同方法：</span><span class="sxs-lookup"><span data-stu-id="5b1cb-116">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="5b1cb-117">重新进行 NuGet v3 库</span><span class="sxs-lookup"><span data-stu-id="5b1cb-117">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
