---
title: "NuGet 3.2.1 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: d27c3bb9-8db1-439a-a134-54e20b7a7766
description: "发行说明，了解 NuGet 3.2.1 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。"
keywords: "NuGet 3.2.1 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2001d9518a34bbd5f2879de6123ec13abf4ae08
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="e6de6-104">NuGet 3.2.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="e6de6-104">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="e6de6-105">[NuGet 3.2 发行说明](../release-notes/nuget-3.2.md) | [NuGet 3.3 发行说明](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="e6de6-105">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="e6de6-106">NuGet 3.2.1 为命令行发布于 2015 年 10 月 12 日有少量的优化和 3.2 版本的修补程序，并且可从[dist.nuget.org](http://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="e6de6-106">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="e6de6-107">改进</span><span class="sxs-lookup"><span data-stu-id="e6de6-107">Improvements</span></span>

* <span data-ttu-id="e6de6-108">NuGet 现在使用配置文件的原始大小写与`NuGet.Config`。</span><span class="sxs-lookup"><span data-stu-id="e6de6-108">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="e6de6-109">这是区分大小写的操作系统上重要[1427年](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="e6de6-109">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="e6de6-110">NuGet 还原现在将忽略 dnx 项目 (`*.xproj`) 应处理与`dnu` [1227年](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="e6de6-110">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="e6de6-111">使用时优化网络利用率`index.json`和包注册数据[1426年](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="e6de6-111">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="e6de6-112">处理，与 v2 服务更加稳定可靠的改进的资源下载[1448年](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="e6de6-112">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="e6de6-113">修补程序</span><span class="sxs-lookup"><span data-stu-id="e6de6-113">Fixes</span></span>

* <span data-ttu-id="e6de6-114">NuGet 更新是否能够正确更新`.csproj` / `.vcxproj`引用[1483年](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="e6de6-114">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="e6de6-115">现在防止本地.nuget 文件夹时 SpecialFolders.UserProfile 找不到创建[1531年](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="e6de6-115">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="e6de6-116">改进的在本地缓存中下载过程中损坏的包的处理[1405年](https://github.com/NuGet/Home/issues/1405) [1157年](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="e6de6-116">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="e6de6-117">处理命令行和 Visual Studio 扩展可以在 NuGet GitHub 中找到有关问题的完整列表[3.2.1 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="e6de6-117">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="e6de6-118">已知问题</span><span class="sxs-lookup"><span data-stu-id="e6de6-118">Known Issues</span></span>

<span data-ttu-id="e6de6-119">我们继续在我们的 GitHub 问题列表，可在上跟踪问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="e6de6-119">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>