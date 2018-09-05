---
title: NuGet 3.4.2 发行说明
description: NuGet 3.4.2 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549146"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="3037e-103">NuGet 3.4.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="3037e-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="3037e-104">[NuGet 3.4.1 发行说明](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 发行说明](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="3037e-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="3037e-105">NuGet 3.4.2 已于 2016 年 4 月 8，若要解决几个在 3.4 和 3.4.1 中发现的问题，发布版本。</span><span class="sxs-lookup"><span data-stu-id="3037e-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="3037e-106">nuget.exe 3.4.2 RC 现已推出</span><span class="sxs-lookup"><span data-stu-id="3037e-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="3037e-107">您可以下载 release candidate 的 nuget.exe 3.4.2[此处](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="3037e-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="3037e-108">更新和改进</span><span class="sxs-lookup"><span data-stu-id="3037e-108">Updates and Improvements</span></span>

* <span data-ttu-id="3037e-109">我们显著改进性能的特定方案中，其中有深入的依赖项关系图的包上的更新需要花费很长时间，挂起 Visual Studio 中的更新。</span><span class="sxs-lookup"><span data-stu-id="3037e-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="3037e-110">nuget 还原，而无需网络流量是 2.5 倍 – Visual Studio 中更快 3 倍。</span><span class="sxs-lookup"><span data-stu-id="3037e-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="3037e-111">除了此更改后，我们已解决了问题，我们已达到网络，两次时 VS UI 中提取更新计数。</span><span class="sxs-lookup"><span data-stu-id="3037e-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="3037e-112">这是部分负责方面具有丰富经验 3.4/3.4.1 某些超时问题客户。</span><span class="sxs-lookup"><span data-stu-id="3037e-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="3037e-113">添加了的对 no_proxy 设置</span><span class="sxs-lookup"><span data-stu-id="3037e-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="3037e-114">修补程序</span><span class="sxs-lookup"><span data-stu-id="3037e-114">Fixes</span></span>

* <span data-ttu-id="3037e-115">修复了其中 nuget.org 源中缺少 NuGet 设置或配置更新到 3.4.1 后。</span><span class="sxs-lookup"><span data-stu-id="3037e-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="3037e-116">修复了在何处对 FindPackagesById 3.4.1 中的大小写更改断开 Artifactory。</span><span class="sxs-lookup"><span data-stu-id="3037e-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="3037e-117">更正了 FIPS 使用 nuget.exe 的 NuGet 还原导致失败的问题。</span><span class="sxs-lookup"><span data-stu-id="3037e-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="3037e-118">浏览具有无效的图标 URL 源时，修复了故障。</span><span class="sxs-lookup"><span data-stu-id="3037e-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="3037e-119">修复了与合并版本和所有源中的条目的问题。</span><span class="sxs-lookup"><span data-stu-id="3037e-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="3037e-120">上面 3.4.2 中的已知问题 Windows x86 命令行 (版本 RC)</span><span class="sxs-lookup"><span data-stu-id="3037e-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="3037e-121">将早期的下一步一周前我们碰到 RTM 修复这些问题。</span><span class="sxs-lookup"><span data-stu-id="3037e-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="3037e-122">如果解决方案文件放置在与项目文件的较低的文件夹层次结构中，对解决方案运行 nuget 还原将失败。</span><span class="sxs-lookup"><span data-stu-id="3037e-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="3037e-123">使用 V2 源的包上运行 nuget delete 命令将失败。</span><span class="sxs-lookup"><span data-stu-id="3037e-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="3037e-124">改为使用 V3 源。</span><span class="sxs-lookup"><span data-stu-id="3037e-124">Use V3 feed instead.</span></span>


<span data-ttu-id="3037e-125">有关此版本中的修补程序和改进的完整列表，请参阅问题列表[此处](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)。</span><span class="sxs-lookup"><span data-stu-id="3037e-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>