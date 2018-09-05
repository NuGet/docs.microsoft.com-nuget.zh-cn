---
title: NuGet 3.2.1 发行说明
description: NuGet 3.2.1 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548185"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="f5aaf-103">NuGet 3.2.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="f5aaf-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="f5aaf-104">[NuGet 3.2 发行说明](../release-notes/nuget-3.2.md) | [NuGet 3.3 发行说明](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="f5aaf-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="f5aaf-105">有关命令行中的 NuGet 3.2.1 已于 2015 年 10 月 12 日发布了几个优化和 3.2 版本的修补程序，可从[dist.nuget.org](http://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="f5aaf-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="f5aaf-106">改进</span><span class="sxs-lookup"><span data-stu-id="f5aaf-106">Improvements</span></span>

* <span data-ttu-id="f5aaf-107">NuGet 现在使用配置文件时使用的原始大小写`NuGet.Config`。</span><span class="sxs-lookup"><span data-stu-id="f5aaf-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="f5aaf-108">这一点在区分大小写的操作系统上[1427年](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="f5aaf-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="f5aaf-109">NuGet 还原现在将忽略 dnx 项目 (`*.xproj`) 应具有处理`dnu` [1227年](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="f5aaf-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="f5aaf-110">使用时，优化网络利用率`index.json`并将其打包注册数据[1426年](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="f5aaf-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="f5aaf-111">处理，与 v2 服务更加稳定可靠的改进的资源下载[1448年](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="f5aaf-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="f5aaf-112">修补程序</span><span class="sxs-lookup"><span data-stu-id="f5aaf-112">Fixes</span></span>

* <span data-ttu-id="f5aaf-113">NuGet 更新是否能够正确更新`.csproj` / `.vcxproj`引用[1483年](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="f5aaf-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="f5aaf-114">现在阻止本地.nuget 文件夹时 SpecialFolders.UserProfile 找不到创建[1531年](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="f5aaf-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="f5aaf-115">改进了在下载过程中损坏的包在本地缓存中的处理[1405年](https://github.com/NuGet/Home/issues/1405) [1157年](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="f5aaf-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="f5aaf-116">可以在 NuGet GitHub 中找到的命令行和 Visual Studio 扩展已解决的问题的完整列表[3.2.1 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="f5aaf-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="f5aaf-117">已知问题</span><span class="sxs-lookup"><span data-stu-id="f5aaf-117">Known Issues</span></span>

<span data-ttu-id="f5aaf-118">我们继续来跟踪我们的 GitHub 问题中，可以在中找到的问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="f5aaf-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>