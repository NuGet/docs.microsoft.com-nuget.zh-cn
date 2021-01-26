---
title: NuGet 3.2.1 发行说明
description: NuGet 3.2.1 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776519"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="69da0-103">NuGet 3.2.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="69da0-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="69da0-104">[NuGet 3.2 发行说明](../release-notes/nuget-3.2.md)  | [NuGet 3.3 发行说明](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="69da0-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="69da0-105">2015年10月12日发布了适用于命令行的 NuGet 3.2.1，其中包含3.2 版本的少数优化和修补程序，可从 [dist.nuget.org](http://dist.nuget.org/index.html)获取。</span><span class="sxs-lookup"><span data-stu-id="69da0-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="69da0-106">改进</span><span class="sxs-lookup"><span data-stu-id="69da0-106">Improvements</span></span>

* <span data-ttu-id="69da0-107">NuGet 现在使用具有原始大小写的配置文件 `NuGet.Config` 。</span><span class="sxs-lookup"><span data-stu-id="69da0-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="69da0-108">这对于区分大小写的操作系统[1427](https://github.com/NuGet/Home/issues/1427)非常重要</span><span class="sxs-lookup"><span data-stu-id="69da0-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="69da0-109">NuGet 还原现在将忽略 `*.xproj` 应该用1227处理 () 的 dnx 项目 `dnu` [](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="69da0-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="69da0-110">使用 `index.json` 和打包注册数据时的优化网络利用率 [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="69da0-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="69da0-111">通过 v2 services [1448](https://github.com/NuGet/Home/issues/1448)提高了资源下载处理的可靠性</span><span class="sxs-lookup"><span data-stu-id="69da0-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="69da0-112">修复项</span><span class="sxs-lookup"><span data-stu-id="69da0-112">Fixes</span></span>

* <span data-ttu-id="69da0-113">NuGet 更新正确更新 `.csproj` / `.vcxproj` 引用[1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="69da0-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="69da0-114">现在禁止在 SpecialFolders 无法找到时创建本地 nuget 文件夹 [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="69da0-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="69da0-115">改善了在下载[1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)期间损坏的本地缓存中的包处理</span><span class="sxs-lookup"><span data-stu-id="69da0-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="69da0-116">有关命令行和 Visual Studio 扩展的问题的完整列表，请参阅 NuGet GitHub [3.2.1 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="69da0-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="69da0-117">已知问题</span><span class="sxs-lookup"><span data-stu-id="69da0-117">Known Issues</span></span>

<span data-ttu-id="69da0-118">我们继续跟踪 GitHub 问题列表中的问题，可在以下位置找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="69da0-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>