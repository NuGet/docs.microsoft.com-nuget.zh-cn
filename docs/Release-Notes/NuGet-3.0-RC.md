---
title: "NuGet 3.0 RC 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.0 RC 的发行说明。"
keywords: "NuGet 3.0 RC 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4693fd8884283e01d3c0a8ad74e0692c1ca00659
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="a31b6-104">NuGet 3.0 RC 发行说明</span><span class="sxs-lookup"><span data-stu-id="a31b6-104">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="a31b6-105">[NuGet 3.0 Beta 发行说明](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 发行说明](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="a31b6-105">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="a31b6-106">随 Visual Studio 2015 RC 版本于 2015 年 4 月 29 日发布 NuGet 3.0 RC。</span><span class="sxs-lookup"><span data-stu-id="a31b6-106">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="a31b6-107">此版本有大量的重要的 bug 修复、 性能改进和更新以支持新的框架。</span><span class="sxs-lookup"><span data-stu-id="a31b6-107">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="a31b6-108">它才可用于 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="a31b6-108">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="a31b6-109">一贯的关注性能</span><span class="sxs-lookup"><span data-stu-id="a31b6-109">Continued Focus on Performance</span></span>

<span data-ttu-id="a31b6-110">稳定性和性能的 NuGet 查询仍是我们关注的热门话题。</span><span class="sxs-lookup"><span data-stu-id="a31b6-110">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="a31b6-111">此版本中，你将会看到在 NuGet UI 和网站的非常快速搜索操作。</span><span class="sxs-lookup"><span data-stu-id="a31b6-111">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="a31b6-112">我们正在监视的服务以及如何使用服务，以便我们可以继续优化这些操作。</span><span class="sxs-lookup"><span data-stu-id="a31b6-112">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="a31b6-113">解决的重要问题</span><span class="sxs-lookup"><span data-stu-id="a31b6-113">Significant Issues Resolved</span></span>

<span data-ttu-id="a31b6-114">为了保持稳定，NuGet 客户端，我们解决许多问题作为此版本的一部分。</span><span class="sxs-lookup"><span data-stu-id="a31b6-114">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="a31b6-115">下面是只需要的一些更重要的问题已解决的简短列表：</span><span class="sxs-lookup"><span data-stu-id="a31b6-115">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="a31b6-116">作为 ASP.NET 5 K framework 的重命名的一部分，已更新了框架名字对象来处理 dnx 和 dnxcore[链接](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="a31b6-116">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="a31b6-117">从 Visual Studio UI 中的链接添加帮助文档[链接](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="a31b6-117">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="a31b6-118">更好地处理中的复杂引用`.nuspec`与以逗号分隔 framework 引用[链接](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="a31b6-118">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="a31b6-119">修复了对日语区域性的支持[链接](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="a31b6-119">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="a31b6-120">更新的客户端，以允许 ASP.NET 5 项目以使用新的 v3 终结点[链接](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="a31b6-120">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="a31b6-121">更新为更好的句柄与源代码管理的包文件夹[链接](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="a31b6-121">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="a31b6-122">固定附属包支持[链接](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="a31b6-122">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="a31b6-123">更正的特定于框架的内容文件的支持[链接](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="a31b6-123">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="a31b6-124">GitHub 状态检查</span><span class="sxs-lookup"><span data-stu-id="a31b6-124">GitHub presence overhaul</span></span>

<span data-ttu-id="a31b6-125">我们已对一些更改我们[源在 GitHub 上的代码存储库](http://github.com/nuget/home)。</span><span class="sxs-lookup"><span data-stu-id="a31b6-125">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="a31b6-126">如果你有任何问题，NuGet Visual Studio 客户端、 Powershell 命令或命令行可执行你可以记录这些问题和上监视其进度我们[GitHub 主页存储库问题列表](http://github.com/nuget/home/issues)。</span><span class="sxs-lookup"><span data-stu-id="a31b6-126">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="a31b6-127">我们在跟踪中的库的问题我们[GitHub NuGetGallery 存储库](http://github.com/nuget/NuGetGallery/issues)。</span><span class="sxs-lookup"><span data-stu-id="a31b6-127">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="a31b6-128">请继续关注</span><span class="sxs-lookup"><span data-stu-id="a31b6-128">Stay Tuned</span></span>

<span data-ttu-id="a31b6-129">请留意[我们的博客](http://blog.nuget.org)了解详细的进度和公告 NuGet 3.0 ！</span><span class="sxs-lookup"><span data-stu-id="a31b6-129">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>