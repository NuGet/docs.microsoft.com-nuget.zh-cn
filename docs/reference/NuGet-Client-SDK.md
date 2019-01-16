---
title: NuGet 客户端 SDK
description: 该 API 是不断变化且不尚有记录，但示例 Dave Glick 博客上可用。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 97ed3ec7d41d2847c0521af69373a1871eb585dd
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324677"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="4135e-103">NuGet 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="4135e-103">NuGet Client SDK</span></span>

> [!Note]
> <span data-ttu-id="4135e-104">无法与相混淆[NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span><span class="sxs-lookup"><span data-stu-id="4135e-104">Not to be confused with the [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span></span>

<span data-ttu-id="4135e-105">*NuGet 客户端 SDK*表示一组.NET 库围绕[NuGet.Client](https://www.nuget.org/packages/NuGet.Client)， [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging)，和[NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="4135e-105">The *NuGet Client SDK* refers to a group of .NET libraries centered around [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="4135e-106">这些包替换较早[NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)库。</span><span class="sxs-lookup"><span data-stu-id="4135e-106">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

<span data-ttu-id="4135e-107">我们正在努力具有稳定的表面区域，我们很快就可以记录。</span><span class="sxs-lookup"><span data-stu-id="4135e-107">We are working on having a stable surface area that we can document soon.</span></span>

## <a name="source-code"></a><span data-ttu-id="4135e-108">源代码</span><span class="sxs-lookup"><span data-stu-id="4135e-108">Source code</span></span>

<span data-ttu-id="4135e-109">在项目中 GitHub 上已发布的源代码[NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client)。</span><span class="sxs-lookup"><span data-stu-id="4135e-109">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="4135e-110">第三方文档</span><span class="sxs-lookup"><span data-stu-id="4135e-110">Third-party documentation</span></span>

<span data-ttu-id="4135e-111">以下博客系列由 Dave Glick，发布 2016年中，可以找到示例和文档的某些 API:</span><span class="sxs-lookup"><span data-stu-id="4135e-111">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="4135e-112">探索 NuGet v3 库，第 1 部分：简介和概念</span><span class="sxs-lookup"><span data-stu-id="4135e-112">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="4135e-113">探索 NuGet v3 库，第 2 部分：搜索包</span><span class="sxs-lookup"><span data-stu-id="4135e-113">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="4135e-114">探索 NuGet v3 库，第 3 部分：安装包</span><span class="sxs-lookup"><span data-stu-id="4135e-114">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="4135e-115">这些博客文章编写后不久**3.4.3** NuGet 客户端 SDK 包已发布的版本。</span><span class="sxs-lookup"><span data-stu-id="4135e-115">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="4135e-116">包的较新版本可能与博客文章中的信息不兼容。</span><span class="sxs-lookup"><span data-stu-id="4135e-116">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="4135e-117">Martin Björkström 未到 Dave Glick 博客系列的后续博客文章，他介绍了不同的方法上使用 NuGet 客户端 SDK 安装 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="4135e-117">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="4135e-118">再探 NuGet v3 库</span><span class="sxs-lookup"><span data-stu-id="4135e-118">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
