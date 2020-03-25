---
title: NuGet 5.5 发行说明
description: NuGet 5.5 的发行说明，包括新功能、bug 修复和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0e8ab66c937058e84420bc3e3a5031cbc133aad7
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2020
ms.locfileid: "80148281"
---
# <a name="nuget-55-release-notes"></a><span data-ttu-id="21e3d-103">NuGet 5.5 发行说明</span><span class="sxs-lookup"><span data-stu-id="21e3d-103">NuGet 5.5 Release Notes</span></span>

<span data-ttu-id="21e3d-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="21e3d-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="21e3d-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="21e3d-105">NuGet version</span></span> | <span data-ttu-id="21e3d-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="21e3d-106">Available in Visual Studio version</span></span>| <span data-ttu-id="21e3d-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="21e3d-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="21e3d-108">**5.5.0**</span><span class="sxs-lookup"><span data-stu-id="21e3d-108">**5.5.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="21e3d-109">Visual Studio 2019 版本16。5</span><span class="sxs-lookup"><span data-stu-id="21e3d-109">Visual Studio 2019 version 16.5</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="21e3d-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="21e3d-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="21e3d-111"><sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装</span><span class="sxs-lookup"><span data-stu-id="21e3d-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-55"></a><span data-ttu-id="21e3d-112">摘要：5.5 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="21e3d-112">Summary: What's New in 5.5</span></span>

* <span data-ttu-id="21e3d-113">改进了 Visual Studio 中 NuGet 包管理器 UI 的辅助功能和屏幕阅读器体验</span><span class="sxs-lookup"><span data-stu-id="21e3d-113">Improved accessibility and screen reader experience for the NuGet package manager UI in Visual Studio</span></span>
    * <span data-ttu-id="21e3d-114">屏幕阅读器体验中的辅助功能问题，缺少已安装文本框等的 altText 和可访问的名称， [#9059](https://github.com/NuGet/Home/issues/9059)</span><span class="sxs-lookup"><span data-stu-id="21e3d-114">Accessibility issues in Screen Reader experiences, missing altText and accessible name for Installed textbox, etc., - [#9059](https://github.com/NuGet/Home/issues/9059)</span></span>
    * <span data-ttu-id="21e3d-115">包中的屏幕阅读器体验中的辅助功能问题列表- [#9077](https://github.com/NuGet/Home/issues/9077)</span><span class="sxs-lookup"><span data-stu-id="21e3d-115">Accessibility issues in Screen Reader experiences in Packages List - [#9077](https://github.com/NuGet/Home/issues/9077)</span></span>
    * <span data-ttu-id="21e3d-116">屏幕阅读器体验中与 "浏览"、"安装" 和 "更新" 选项卡相关的辅助功能问题- [#9078](https://github.com/NuGet/Home/issues/9078)</span><span class="sxs-lookup"><span data-stu-id="21e3d-116">Accessibility issues in Screen Reader experiences related to "browse","install","update" Tabs - [#9078](https://github.com/NuGet/Home/issues/9078)</span></span>
    * <span data-ttu-id="21e3d-117">讲述人不会公告 "空白"、"无 Dependencies" "、" "nuget"、"MIT" 链接标签[#9157](https://github.com/NuGet/Home/issues/9157)</span><span class="sxs-lookup"><span data-stu-id="21e3d-117">Narrator does not announce "Blank","No Dependencies","nuget.org","MIT" link label [#9157](https://github.com/NuGet/Home/issues/9157)</span></span>

* <span data-ttu-id="21e3d-118">支持在 Visual Studio 包管理器 UI 中为本地源上承载的包提供自包含的图标- [#8189](https://github.com/NuGet/Home/issues/8189)</span><span class="sxs-lookup"><span data-stu-id="21e3d-118">Support for surfacing self-contained icons in Visual Studio package manager UI for packages hosted on local feeds - [#8189](https://github.com/NuGet/Home/issues/8189)</span></span>

* <span data-ttu-id="21e3d-119">使用 `RestoreUseStaticGraphEvaluation` 提高了无操作还原性能，从而可通过调用 MSBuild 静态图形 Api 来加快评估- [8791](https://github.com/NuGet/Home/issues/8791)</span><span class="sxs-lookup"><span data-stu-id="21e3d-119">Significantly improved no-op restore performance using `RestoreUseStaticGraphEvaluation` which speeds up evaluations by calling MSBuild Static Graph APIs - [8791](https://github.com/NuGet/Home/issues/8791)</span></span>

* <span data-ttu-id="21e3d-120">通过跨平台身份验证插件改进 dotnet 的可靠性</span><span class="sxs-lookup"><span data-stu-id="21e3d-120">Improved dotnet.exe reliability with cross-platform authentication plugins</span></span>
    * <span data-ttu-id="21e3d-121">dotnet restore 失败，TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)</span><span class="sxs-lookup"><span data-stu-id="21e3d-121">dotnet restore failing with TaskCanceledException - [#7842](https://github.com/NuGet/Home/issues/7842)</span></span>
    * <span data-ttu-id="21e3d-122">插件： "已取消任务"-由于此原因，ADO 身份验证存在问题。</span><span class="sxs-lookup"><span data-stu-id="21e3d-122">Plugin:  "A task was cancelled" - problem with ADO authentication due to this.</span></span><span data-ttu-id="21e3d-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span><span class="sxs-lookup"><span data-stu-id="21e3d-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span></span>

* <span data-ttu-id="21e3d-124">添加 `dotnet nuget <add|remove|update|disable|enable|list> source` 命令- [#4126](https://github.com/NuGet/Home/issues/4126)</span><span class="sxs-lookup"><span data-stu-id="21e3d-124">add `dotnet nuget <add|remove|update|disable|enable|list> source` command - [#4126](https://github.com/NuGet/Home/issues/4126)</span></span>

* <span data-ttu-id="21e3d-125">使用 dotnet nuget 推送[#8778](https://github.com/NuGet/Home/issues/8778)的 `--skip-duplicate` 的支持</span><span class="sxs-lookup"><span data-stu-id="21e3d-125">Suport for `--skip-duplicate`  using dotnet nuget push - [#8778](https://github.com/NuGet/Home/issues/8778)</span></span>

* <span data-ttu-id="21e3d-126">支持 `packages.config` 与 msbuild/restore- [#8506](https://github.com/NuGet/Home/issues/8506)</span><span class="sxs-lookup"><span data-stu-id="21e3d-126">Support `packages.config` with msbuild /restore - [#8506](https://github.com/NuGet/Home/issues/8506)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="21e3d-127">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="21e3d-127">Issues fixed in this release</span></span>

<span data-ttu-id="21e3d-128">**Bug**</span><span class="sxs-lookup"><span data-stu-id="21e3d-128">**Bugs**</span></span>

* <span data-ttu-id="21e3d-129">通过 V3 Api 改编自我更新程序- [#4197](https://github.com/NuGet/Home/issues/4197)</span><span class="sxs-lookup"><span data-stu-id="21e3d-129">Rework Self-Updater with V3 Apis - [#4197](https://github.com/NuGet/Home/issues/4197)</span></span>

* <span data-ttu-id="21e3d-130">如果包依赖项版本设置为 "\*"，则包依赖项版本错误- [#6697](https://github.com/NuGet/Home/issues/6697)</span><span class="sxs-lookup"><span data-stu-id="21e3d-130">Wrong package dependency version If package dependency version is set to '\*' - [#6697](https://github.com/NuGet/Home/issues/6697)</span></span>

* <span data-ttu-id="21e3d-131">ErrorUnsafePackageEntry 错误消息不指向问题的根源- [#7505](https://github.com/NuGet/Home/issues/7505)</span><span class="sxs-lookup"><span data-stu-id="21e3d-131">ErrorUnsafePackageEntry error message is not pointing to source of problem - [#7505](https://github.com/NuGet/Home/issues/7505)</span></span>

* <span data-ttu-id="21e3d-132">锁定文件不采用 "\*" 方案- [#8073](https://github.com/NuGet/Home/issues/8073)</span><span class="sxs-lookup"><span data-stu-id="21e3d-132">Lock file is not honored in "\*" scenarios  - [#8073](https://github.com/NuGet/Home/issues/8073)</span></span>

* <span data-ttu-id="21e3d-133">在 PackageReference 中使用 \* 时，Nuget.exe 不会解析为包的最新版本（MSBuild/Dotnet/VS restore do）- [#8432](https://github.com/NuGet/Home/issues/8432)</span><span class="sxs-lookup"><span data-stu-id="21e3d-133">NuGet.exe does not resolve to the latest version of a package when using \* in PackageReference (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)</span></span>

* <span data-ttu-id="21e3d-134">具有多个目标 WPF 项目的 dotnet 列表包- [#8463](https://github.com/NuGet/Home/issues/8463)</span><span class="sxs-lookup"><span data-stu-id="21e3d-134">dotnet list package with multi targeting WPF project - [#8463](https://github.com/NuGet/Home/issues/8463)</span></span>

* <span data-ttu-id="21e3d-135">改善 ConcurrencyUtilities （降低 CPU 使用率）- [#8653](https://github.com/NuGet/Home/issues/8653)</span><span class="sxs-lookup"><span data-stu-id="21e3d-135">Improve ConcurrencyUtilities (reduce CPU usage) - [#8653](https://github.com/NuGet/Home/issues/8653)</span></span>

* <span data-ttu-id="21e3d-136">不应在预览还原中编写已卸载项目方案的 DG 规范- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="21e3d-136">DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="21e3d-137">Visual Studio NuGet 包（RestoreManagerPackage）需要自动加载解决方案生成事件- [#8796](https://github.com/NuGet/Home/issues/8796)</span><span class="sxs-lookup"><span data-stu-id="21e3d-137">The Visual Studio NuGet packages (RestoreManagerPackage) needs to auto load on solution build events - [#8796](https://github.com/NuGet/Home/issues/8796)</span></span>

* <span data-ttu-id="21e3d-138">.Vssettings 初始化中的死锁- [#8842](https://github.com/NuGet/Home/issues/8842)</span><span class="sxs-lookup"><span data-stu-id="21e3d-138">Deadlock in VSSettings init - [#8842](https://github.com/NuGet/Home/issues/8842)</span></span>

* <span data-ttu-id="21e3d-139">如果项目位于解决方案文件夹中，则不会从 NuGet 包填充 VisualStudio 工具箱- [#8868](https://github.com/NuGet/Home/issues/8868)</span><span class="sxs-lookup"><span data-stu-id="21e3d-139">VisualStudio ToolBox is not populated from a NuGet package if a project is placed in a solution folder - [#8868](https://github.com/NuGet/Home/issues/8868)</span></span>

* <span data-ttu-id="21e3d-140">VS：由于争用条件，解决方案还原永久失败- [#8881](https://github.com/NuGet/Home/issues/8881)</span><span class="sxs-lookup"><span data-stu-id="21e3d-140">VS:  solution restore perpetually fails due to race condition - [#8881](https://github.com/NuGet/Home/issues/8881)</span></span>

* <span data-ttu-id="21e3d-141">"正在安装" 选项卡上的 "正在加载 ..." 和 "搜索</span><span class="sxs-lookup"><span data-stu-id="21e3d-141">Constant "loading.." on installed tab, and "searching</span></span> <term><span data-ttu-id="21e3d-142">... "更新选项卡- [#8890](https://github.com/NuGet/Home/issues/8890)</span><span class="sxs-lookup"><span data-stu-id="21e3d-142">.." on updates tab - [#8890](https://github.com/NuGet/Home/issues/8890)</span></span>

* <span data-ttu-id="21e3d-143">缓存过期后，VS PM UI 中缺少嵌入的图标- [#9069](https://github.com/NuGet/Home/issues/9069)</span><span class="sxs-lookup"><span data-stu-id="21e3d-143">Missing Embedded Icons in VS PM UI after cache expires - [#9069](https://github.com/NuGet/Home/issues/9069)</span></span>

* <span data-ttu-id="21e3d-144">FireAndForget PM UI 启动- [#9112](https://github.com/NuGet/Home/issues/9112)</span><span class="sxs-lookup"><span data-stu-id="21e3d-144">FireAndForget PM UI startup - [#9112](https://github.com/NuGet/Home/issues/9112)</span></span>

* <span data-ttu-id="21e3d-145">Restore： IncludeExcludeFiles （...）实现不正确- [#9167](https://github.com/NuGet/Home/issues/9167)</span><span class="sxs-lookup"><span data-stu-id="21e3d-145">Restore: IncludeExcludeFiles.Equals(...) implementation is incorrect - [#9167](https://github.com/NuGet/Home/issues/9167)</span></span>

* <span data-ttu-id="21e3d-146">Restore： PackageSpec （）创建不相等的克隆[#9211](https://github.com/NuGet/Home/issues/9211)</span><span class="sxs-lookup"><span data-stu-id="21e3d-146">Restore: PackageSpec.Clone() creates unequal clone - [#9211](https://github.com/NuGet/Home/issues/9211)</span></span>

* <span data-ttu-id="21e3d-147">未选中错误列表 "如果生成完成但有错误，则显示错误列表" 的错误列表- [#8190](https://github.com/NuGet/Home/issues/8190)</span><span class="sxs-lookup"><span data-stu-id="21e3d-147">Error list shown although "Always show Error List if build finishes with errors" is not checked - [#8190](https://github.com/NuGet/Home/issues/8190)</span></span>

* <span data-ttu-id="21e3d-148">静态图形还原不应传递空的 SolutionPath [#9061](https://github.com/NuGet/Home/issues/9061)</span><span class="sxs-lookup"><span data-stu-id="21e3d-148">Static Graph restore should not pass empty SolutionPath - [#9061](https://github.com/NuGet/Home/issues/9061)</span></span>

* <span data-ttu-id="21e3d-149">还原：计算每个项目4次的结束时间- [#9042](https://github.com/NuGet/Home/issues/9042)</span><span class="sxs-lookup"><span data-stu-id="21e3d-149">Restore: closure computed for each project 4 times - [#9042](https://github.com/NuGet/Home/issues/9042)</span></span>

* <span data-ttu-id="21e3d-150">Restore： DependencyGraphSpec （...）不需要 JObject- [#9040](https://github.com/NuGet/Home/issues/9040)</span><span class="sxs-lookup"><span data-stu-id="21e3d-150">Restore: DependencyGraphSpec.Load(...) does not need JObject - [#9040](https://github.com/NuGet/Home/issues/9040)</span></span>

* <span data-ttu-id="21e3d-151">还原：在大型对象堆（LOH）上创建的大型字符串- [#9031](https://github.com/NuGet/Home/issues/9031)</span><span class="sxs-lookup"><span data-stu-id="21e3d-151">Restore: large strings created on large object heap (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)</span></span>

* <span data-ttu-id="21e3d-152">新 mono 上的自定义 nuget.exe 可能因 MSBuild SDK 解析程序而中断- [8848](https://github.com/NuGet/Home/issues/8848)</span><span class="sxs-lookup"><span data-stu-id="21e3d-152">Custom nuget.exe on newer mono might break due to the MSBuild SDK Resolver - [8848](https://github.com/NuGet/Home/issues/8848)</span></span>

* <span data-ttu-id="21e3d-153">dgspec "由其他进程使用" 时还原失败- [8692](https://github.com/NuGet/Home/issues/8692)</span><span class="sxs-lookup"><span data-stu-id="21e3d-153">restore fails when nuget.dgspec.json is "used by another process" - [8692](https://github.com/NuGet/Home/issues/8692)</span></span>

<span data-ttu-id="21e3d-154">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="21e3d-154">**DCRs**</span></span>

* <span data-ttu-id="21e3d-155">_GetRestoreProjectStyle 中的逻辑应在任务[#8804](https://github.com/NuGet/Home/issues/8804)</span><span class="sxs-lookup"><span data-stu-id="21e3d-155">Logic in _GetRestoreProjectStyle should be in a task - [#8804](https://github.com/NuGet/Home/issues/8804)</span></span>

* <span data-ttu-id="21e3d-156">默认情况下，在 "已安装" 选项卡上添加弃用信息- [#8541](https://github.com/NuGet/Home/issues/8541)</span><span class="sxs-lookup"><span data-stu-id="21e3d-156">Add deprecation information by default on the installed tab - [#8541](https://github.com/NuGet/Home/issues/8541)</span></span>

<span data-ttu-id="21e3d-157">**[此版本中已修复的所有问题的列表-5。5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span><span class="sxs-lookup"><span data-stu-id="21e3d-157">**[List of all issues fixed in this release - 5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span></span>
