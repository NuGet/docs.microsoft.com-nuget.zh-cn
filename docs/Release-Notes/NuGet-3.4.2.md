---
title: "NuGet 上面 3.4.2 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "发行说明，了解 NuGet 上面 3.4.2 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。"
keywords: "NuGet 上面 3.4.2 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 892a965e67762af2ae42c2d6ee75d2838104d1c2
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="0fcb9-104">NuGet 上面 3.4.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="0fcb9-104">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="0fcb9-105">[NuGet 3.4.1 发行说明](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 发行说明](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="0fcb9-105">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="0fcb9-106">NuGet 上面 3.4.2 已于 2016 年 4 月 8，以解决在 3.4 和 3.4.1 中识别的几个问题发布版本。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-106">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="0fcb9-107">nuget.exe 上面 3.4.2 RC 现已推出</span><span class="sxs-lookup"><span data-stu-id="0fcb9-107">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="0fcb9-108">你可以下载 nuget.exe 上面 3.4.2 的候选发布版[此处](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-108">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="0fcb9-109">更新和改进</span><span class="sxs-lookup"><span data-stu-id="0fcb9-109">Updates and Improvements</span></span>

* <span data-ttu-id="0fcb9-110">我们显著改进性能的特定方案中，其中上有深入的依赖项关系图的包的更新所花很长时间，挂起 Visual Studio 中的更新。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-110">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="0fcb9-111">而不会网络流量的 nuget 还原是 2.5 x-Visual Studio 中更快的 3 x。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-111">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="0fcb9-112">除了此更改后，我们已解决问题，我们已达到网络，两次时提取更新计数的 VS UI。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-112">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="0fcb9-113">这是部分负责 3.4/3.4.1 方面具有丰富经验某些超时问题客户。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-113">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="0fcb9-114">添加了对 no_proxy 设置支持</span><span class="sxs-lookup"><span data-stu-id="0fcb9-114">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="0fcb9-115">修补程序</span><span class="sxs-lookup"><span data-stu-id="0fcb9-115">Fixes</span></span>

* <span data-ttu-id="0fcb9-116">修复了问题 nuget.org 源所在 NuGet 的设置或配置中缺少更新到 3.4.1 后。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-116">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="0fcb9-117">修复了问题中 3.4.1 FindPackagesById 大小写更改将 Artifactory 处中断。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-117">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="0fcb9-118">更正 FIPS NuGet 还原与 nuget.exe 导致失败的问题。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-118">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="0fcb9-119">浏览具有无效的图标 URL 源时，请修复崩溃。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-119">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="0fcb9-120">修复了与合并版本和从 '所有资源' 的项的问题。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-120">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="0fcb9-121">上面 3.4.2 中的已知问题 Windows x86 命令行 (版本 RC)</span><span class="sxs-lookup"><span data-stu-id="0fcb9-121">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="0fcb9-122">将早期下周我们命中 RTM 之前修复这些问题。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-122">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="0fcb9-123">如果解决方案文件放置在与项目文件的较低的文件夹层次结构，正在运行的解决方案的 nuget 还原将失败。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-123">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="0fcb9-124">在包使用 V2 源上运行 nuget delete 命令将失败。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-124">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="0fcb9-125">请改用 V3 源。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-125">Use V3 feed instead.</span></span>


<span data-ttu-id="0fcb9-126">有关此版本中的修补程序和改进的完整列表，请参阅的问题列表[此处](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)。</span><span class="sxs-lookup"><span data-stu-id="0fcb9-126">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>