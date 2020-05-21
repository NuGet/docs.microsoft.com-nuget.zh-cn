---
title: NuGet 5.6 发行说明
description: NuGet 5.6 的发行说明，包括新功能、bug 修复和 Dcr。
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727805"
---
# <a name="nuget-56-release-notes"></a><span data-ttu-id="67517-103">NuGet 5.6 发行说明</span><span class="sxs-lookup"><span data-stu-id="67517-103">NuGet 5.6 Release Notes</span></span>

<span data-ttu-id="67517-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="67517-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="67517-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="67517-105">NuGet version</span></span> | <span data-ttu-id="67517-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="67517-106">Available in Visual Studio version</span></span>| <span data-ttu-id="67517-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="67517-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="67517-108">**5.6.0**</span><span class="sxs-lookup"><span data-stu-id="67517-108">**5.6.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="67517-109">Visual Studio 2019 版本 16.6</span><span class="sxs-lookup"><span data-stu-id="67517-109">Visual Studio 2019 version 16.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="67517-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="67517-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="67517-111"><sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装</span><span class="sxs-lookup"><span data-stu-id="67517-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-56"></a><span data-ttu-id="67517-112">摘要：5.6 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="67517-112">Summary: What's New in 5.6</span></span>

* <span data-ttu-id="67517-113">支持浮动版本的预发布包。</span><span class="sxs-lookup"><span data-stu-id="67517-113">Support prerelease packages with floating versions.</span></span> <span data-ttu-id="67517-114">`Version="*-*"`、 `Version="1.*-*"` 和类似浮动到最新版本，包括预发行版本（在指定范围内）- [#912](https://github.com/NuGet/Home/issues/912)</span><span class="sxs-lookup"><span data-stu-id="67517-114">`Version="*-*"`, `Version="1.*-*"`, and similar float to latest versions, including prerelease versions, within specified range  - [#912](https://github.com/NuGet/Home/issues/912)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="67517-115">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="67517-115">Issues fixed in this release</span></span>

<span data-ttu-id="67517-116">**漏洞**</span><span class="sxs-lookup"><span data-stu-id="67517-116">**Bugs:**</span></span>

* <span data-ttu-id="67517-117">`nuget push *.nupkg`当 snupkg 不存在时失败- [#8148](https://github.com/NuGet/Home/issues/8148)</span><span class="sxs-lookup"><span data-stu-id="67517-117">`nuget push *.nupkg` fails when snupkg does not exist - [#8148](https://github.com/NuGet/Home/issues/8148)</span></span>

* <span data-ttu-id="67517-118">Pack 和多个其他代码路径，依赖于区域设置。</span><span class="sxs-lookup"><span data-stu-id="67517-118">Pack, and several other code paths, fail dependent on locale.</span></span> <span data-ttu-id="67517-119">使用 System.text.regularexpressions.regexoptions. Regexoptions.cultureinvariant- [#8246](https://github.com/NuGet/Home/issues/8246)</span><span class="sxs-lookup"><span data-stu-id="67517-119">Use RegexOptions.CultureInvariant - [#8246](https://github.com/NuGet/Home/issues/8246)</span></span>

* <span data-ttu-id="67517-120">Perf：不应在预览还原中编写已卸载项目方案的 DG 规范- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="67517-120">Perf: DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="67517-121">还原：通过缓存解决方案依赖项关系图规范提高性能[#9201](https://github.com/NuGet/Home/issues/9201)</span><span class="sxs-lookup"><span data-stu-id="67517-121">Restore: Improve performance by caching solution dependency graph spec - [#9201](https://github.com/NuGet/Home/issues/9201)</span></span>

* <span data-ttu-id="67517-122">使用 PM 控制台安装包后，PM UI 不适用于 SDK 样式项目- [#9203](https://github.com/NuGet/Home/issues/9203)</span><span class="sxs-lookup"><span data-stu-id="67517-122">PM UI doesn't work for SDK style projects after installing a package with PM Console - [#9203](https://github.com/NuGet/Home/issues/9203)</span></span>

* <span data-ttu-id="67517-123">嵌入的图标无法在具有本地包源的 PM UI 中显示-具体取决于/vs \- [#9225](https://github.com/NuGet/Home/issues/9225)</span><span class="sxs-lookup"><span data-stu-id="67517-123">Embedded icon can’t be shown in PM UI with local package feed - depending on / vs \ - [#9225](https://github.com/NuGet/Home/issues/9225)</span></span>

* <span data-ttu-id="67517-124">如果 NuGetVersion 无法[#9255](https://github.com/NuGet/Home/issues/9255)解析，则 TryParseStrict （）应返回 false</span><span class="sxs-lookup"><span data-stu-id="67517-124">NuGetVersion.TryParseStrict() should return false if it fails to parse - [#9255](https://github.com/NuGet/Home/issues/9255)</span></span>

* <span data-ttu-id="67517-125">`nuget.exe push`有关的帮助 `-source` ，应建议使用源名称，而不是源 URL- [#9265](https://github.com/NuGet/Home/issues/9265)</span><span class="sxs-lookup"><span data-stu-id="67517-125">`nuget.exe push` help for `-source`, should suggest usage of source name, not source URL - [#9265](https://github.com/NuGet/Home/issues/9265)</span></span>

* <span data-ttu-id="67517-126">`dotnet nuget add package SourceUri`创建错误的默认包源名称- [#9277](https://github.com/NuGet/Home/issues/9277)</span><span class="sxs-lookup"><span data-stu-id="67517-126">`dotnet nuget add package SourceUri`  creates bad default package source name - [#9277](https://github.com/NuGet/Home/issues/9277)</span></span>

* <span data-ttu-id="67517-127">屏幕阅读器未公布 "搜索 ..."切换选项卡时的消息- [#9307](https://github.com/NuGet/Home/issues/9307)</span><span class="sxs-lookup"><span data-stu-id="67517-127">Screen reader doesn't announce "Searching..." message when switching tabs - [#9307](https://github.com/NuGet/Home/issues/9307)</span></span>

* <span data-ttu-id="67517-128">辅助功能：聚焦框的颜色不适用于深色主题中的 UI 选项卡- [#9336](https://github.com/NuGet/Home/issues/9336)</span><span class="sxs-lookup"><span data-stu-id="67517-128">Accessibility: Focus-rectangle color is not accessible PM UI tabs in dark theme - [#9336](https://github.com/NuGet/Home/issues/9336)</span></span>

* <span data-ttu-id="67517-129">由于 MSBuild 14 或更低，无法还原 nuget.exe 5.5- [#9458](https://github.com/NuGet/Home/issues/9458)</span><span class="sxs-lookup"><span data-stu-id="67517-129">nuget.exe 5.5 fails to restore with MSBuild 14 or below - [#9458](https://github.com/NuGet/Home/issues/9458)</span></span>

* <span data-ttu-id="67517-130">请勿记录还原消息中的毫秒时间- [#8977](https://github.com/NuGet/Home/issues/8977)</span><span class="sxs-lookup"><span data-stu-id="67517-130">Don't log millisecond times in restore messages - [#8977](https://github.com/NuGet/Home/issues/8977)</span></span>

* <span data-ttu-id="67517-131">使 IOutputConsole 异步[#9268](https://github.com/NuGet/Home/issues/9268)</span><span class="sxs-lookup"><span data-stu-id="67517-131">Make IOutputConsole async - [#9268](https://github.com/NuGet/Home/issues/9268)</span></span>

* <span data-ttu-id="67517-132">MSBuild 版本选取在某些非英语区域性上的运行效果很差- [#9322](https://github.com/NuGet/Home/issues/9322)</span><span class="sxs-lookup"><span data-stu-id="67517-132">MSBuild version picking works poorly on some non-english cultures - [#9322](https://github.com/NuGet/Home/issues/9322)</span></span>

* <span data-ttu-id="67517-133">#9337 上缺少格式默认值 `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)</span><span class="sxs-lookup"><span data-stu-id="67517-133">Missing format default on `dotnet nuget list source` - [#9337](https://github.com/NuGet/Home/issues/9337)</span></span>

* <span data-ttu-id="67517-134">Perf： RestoreOperationLogger 具有不必要的线程关联性[#9288](https://github.com/NuGet/Home/issues/9288)</span><span class="sxs-lookup"><span data-stu-id="67517-134">Perf: RestoreOperationLogger has unnecessary thread affinity - [#9288](https://github.com/NuGet/Home/issues/9288)</span></span>

* <span data-ttu-id="67517-135">命令文档的自动创建 `dotnet nuget` - [#9146](https://github.com/NuGet/Home/issues/9146)</span><span class="sxs-lookup"><span data-stu-id="67517-135">Automated creation of docs for `dotnet nuget` commands - [#9146](https://github.com/NuGet/Home/issues/9146)</span></span>

* <span data-ttu-id="67517-136">默认详细级别不应报告每个项目的 noop 还原[#8792](https://github.com/NuGet/Home/issues/8792)</span><span class="sxs-lookup"><span data-stu-id="67517-136">Default verbosity should not report each project's noop restore - [#8792](https://github.com/NuGet/Home/issues/8792)</span></span>

* <span data-ttu-id="67517-137">`-DependencyVersion`的支持参数 `NuGet.exe update` ，类似于安装命令- [#7694](https://github.com/NuGet/Home/issues/7694)</span><span class="sxs-lookup"><span data-stu-id="67517-137">Support `-DependencyVersion` parameter for `NuGet.exe update`, similar to install command - [#7694](https://github.com/NuGet/Home/issues/7694)</span></span>


<span data-ttu-id="67517-138">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="67517-138">**DCRs:**</span></span>

* <span data-ttu-id="67517-139">添加对 net 5.0 目标框架的初始支持- [#9584](https://github.com/NuGet/Home/issues/9584)</span><span class="sxs-lookup"><span data-stu-id="67517-139">Add initial support for net5.0 target framework - [#9584](https://github.com/NuGet/Home/issues/9584)</span></span>

* <span data-ttu-id="67517-140">在 PM UI 的 "更新" 选项卡中按 ID 对包排序- [#9278](https://github.com/NuGet/Home/issues/9278)</span><span class="sxs-lookup"><span data-stu-id="67517-140">Sort packages by ID in the Updates tab of the PM UI - [#9278](https://github.com/NuGet/Home/issues/9278)</span></span>


<span data-ttu-id="67517-141">**[此版本中已修复的所有问题的列表-5。6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span><span class="sxs-lookup"><span data-stu-id="67517-141">**[List of all issues fixed in this release - 5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span></span>
