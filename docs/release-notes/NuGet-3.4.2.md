---
title: NuGet 3.4.2 发行说明
description: NuGet 3.4.2 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780251"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="d20ac-103">NuGet 3.4.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="d20ac-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="d20ac-104">[NuGet 3.4.1 发行说明](../release-notes/nuget-3.4.1.md)  | [NuGet 3.4.3 发行说明](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="d20ac-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="d20ac-105">NuGet 3.4.2 于2016年4月8日发布，以解决3.4 和3.4.1 版本中标识的多个问题。</span><span class="sxs-lookup"><span data-stu-id="d20ac-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="d20ac-106">nuget.exe 3.4.2 RC 现已推出</span><span class="sxs-lookup"><span data-stu-id="d20ac-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="d20ac-107">可在 [此处](https://dist.nuget.org/index.html)下载 nuget.exe 3.4.2 的候选发布版本。</span><span class="sxs-lookup"><span data-stu-id="d20ac-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="d20ac-108">更新和改进</span><span class="sxs-lookup"><span data-stu-id="d20ac-108">Updates and Improvements</span></span>

* <span data-ttu-id="d20ac-109">在特定方案中，我们大大提高了更新的性能，在此方案中，具有深层依赖项关系图的包上的更新花了很长时间并挂起了 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d20ac-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="d20ac-110">不带网络流量的 nuget 还原在 Visual Studio 中速度为 2.5 x –3倍。</span><span class="sxs-lookup"><span data-stu-id="d20ac-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="d20ac-111">除了此更改之外，我们还修复了一个问题，即在 VS UI 中提取更新计数时，我们将网络命中了两次。</span><span class="sxs-lookup"><span data-stu-id="d20ac-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="d20ac-112">这部分负责在 3.4/3.4.1 中遇到的客户遇到一些超时问题。</span><span class="sxs-lookup"><span data-stu-id="d20ac-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="d20ac-113">添加了 no_proxy 设置支持</span><span class="sxs-lookup"><span data-stu-id="d20ac-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="d20ac-114">修复项</span><span class="sxs-lookup"><span data-stu-id="d20ac-114">Fixes</span></span>

* <span data-ttu-id="d20ac-115">修复了更新到3.4.1 后，NuGet 设置或配置中缺少 nuget.org 源的问题。</span><span class="sxs-lookup"><span data-stu-id="d20ac-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="d20ac-116">修复了3.4.1 中断 Artifactory 时，大小写更改为 FindPackagesById 的问题。</span><span class="sxs-lookup"><span data-stu-id="d20ac-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="d20ac-117">更正了导致 NuGet 还原失败的 FIPS 的问题，nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="d20ac-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="d20ac-118">修复了浏览具有无效图标 URL 的源时出现的故障。</span><span class="sxs-lookup"><span data-stu-id="d20ac-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="d20ac-119">修复了合并版本和条目来自 "所有源" 的问题。</span><span class="sxs-lookup"><span data-stu-id="d20ac-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="d20ac-120">3.4.2 Windows x86 命令行 (RC 中的已知问题) </span><span class="sxs-lookup"><span data-stu-id="d20ac-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="d20ac-121">这些问题将在第一周的第一周提前修复，然后再进行 RTM。</span><span class="sxs-lookup"><span data-stu-id="d20ac-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="d20ac-122">如果解决方案文件位于低于项目文件的文件夹层次结构中，则在解决方案上运行 nuget 还原将会失败。</span><span class="sxs-lookup"><span data-stu-id="d20ac-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="d20ac-123">使用 V2 馈送对包运行 nuget delete 命令将失败。</span><span class="sxs-lookup"><span data-stu-id="d20ac-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="d20ac-124">请改用 V3 馈送。</span><span class="sxs-lookup"><span data-stu-id="d20ac-124">Use V3 feed instead.</span></span>


<span data-ttu-id="d20ac-125">有关此版本中的修复和改进的完整列表，请查看 [此处](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)的问题列表。</span><span class="sxs-lookup"><span data-stu-id="d20ac-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>