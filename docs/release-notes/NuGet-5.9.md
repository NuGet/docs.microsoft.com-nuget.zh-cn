---
title: NuGet 5.9 发行说明
description: NuGet 5.9 的发行说明，包括新功能、bug 修复和 Dcr。
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 24933ebb51851da2583b03e7fd3e55fade5e8a18
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859523"
---
# <a name="nuget-59-release-notes"></a><span data-ttu-id="68505-103">NuGet 5.9 发行说明</span><span class="sxs-lookup"><span data-stu-id="68505-103">NuGet 5.9 Release Notes</span></span>

<span data-ttu-id="68505-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="68505-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="68505-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="68505-105">NuGet version</span></span> | <span data-ttu-id="68505-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="68505-106">Available in Visual Studio version</span></span> | <span data-ttu-id="68505-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="68505-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="68505-108">**5.9**</span><span class="sxs-lookup"><span data-stu-id="68505-108">**5.9**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="68505-109">Visual Studio 2019 版本16。9</span><span class="sxs-lookup"><span data-stu-id="68505-109">Visual Studio 2019 version 16.9</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="68505-110">[5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="68505-110">[5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="68505-111"><sup>1</sup> 与带有 .net Core 工作负载的 Visual Studio 2019 一起安装</span><span class="sxs-lookup"><span data-stu-id="68505-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="68505-112">Visual Studio 16.9、MSBuild 16.9 和 .NET 5.0.3 + 要求 NuGet.exe 5.9 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="68505-112">Visual Studio 16.9, MSBuild 16.9, and .NET 5.0.3+ requires NuGet.exe 5.9 or later.</span></span>

## <a name="summary-whats-new-in-59"></a><span data-ttu-id="68505-113">摘要：5.9 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="68505-113">Summary: What's New in 5.9</span></span>

* <span data-ttu-id="68505-114">为包依赖项添加 "更新" 上下文菜单项，这些依赖项用于启动带有预选包的包管理器 UI 以更新- [#10378](https://github.com/NuGet/Home/issues/10378)</span><span class="sxs-lookup"><span data-stu-id="68505-114">Add "Update" context menu item for package dependencies that launches Package Manager UI with preselected packages to update - [#10378](https://github.com/NuGet/Home/issues/10378)</span></span>

    ![右键单击 "更新" 包体验](media/releasenotes-59-update.png)

* <span data-ttu-id="68505-116">在解决方案级包管理器 UI 中显示 "项目" 列表的 "版本" 列中 (包括浮动版本或版本范围请求) 请求的版本- [#9827](https://github.com/NuGet/Home/issues/9827)</span><span class="sxs-lookup"><span data-stu-id="68505-116">Show the requested version (including floating version or version range request) in the "Version" column of the project list in the solution level Package Manager UI - [#9827](https://github.com/NuGet/Home/issues/9827)</span></span>

    ![解决方案级包管理器 UI 中的请求版本](media/releasenotes-59-requested-version.png)

* <span data-ttu-id="68505-118">包管理器 UI "浏览" 选项卡中的 IntelliCode 包建议，作为 A/B 测试 [#10053](https://github.com/NuGet/Home/issues/10053)</span><span class="sxs-lookup"><span data-stu-id="68505-118">IntelliCode package suggestions in the Package Manager UI Browse tab released as an A/B test - [#10053](https://github.com/NuGet/Home/issues/10053)</span></span>

* <span data-ttu-id="68505-119">扩展 `.nupkg.metadata` 文件以包含安装源- [#10354](https://github.com/NuGet/Home/issues/10354)</span><span class="sxs-lookup"><span data-stu-id="68505-119">Extend the `.nupkg.metadata` file to include the installation source - [#10354](https://github.com/NuGet/Home/issues/10354)</span></span>

* <span data-ttu-id="68505-120">引入一个新的 msbuild 属性，以便在包任务期间排除特定 Tfm 的生成输出- [#10396](https://github.com/NuGet/Home/issues/10396)</span><span class="sxs-lookup"><span data-stu-id="68505-120">Introduce a new msbuild property to exclude build output for specific TFMs during pack task - [#10396](https://github.com/NuGet/Home/issues/10396)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="68505-121">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="68505-121">Issues fixed in this release</span></span>

<span data-ttu-id="68505-122">**Dcr (设计更改请求) ：**</span><span class="sxs-lookup"><span data-stu-id="68505-122">**DCRs(Design Change Request):**</span></span>

* <span data-ttu-id="68505-123">当安装了最新的包版本时，关闭图标图标是不是直观的。</span><span class="sxs-lookup"><span data-stu-id="68505-123">The down icon icon when the latest package version is installed is not intuitive.</span></span> <span data-ttu-id="68505-124">旧的绿色勾选标记为完美 [#9789](https://github.com/NuGet/Home/issues/9789)</span><span class="sxs-lookup"><span data-stu-id="68505-124">The old green tick was perfect - [#9789](https://github.com/NuGet/Home/issues/9789)</span></span>

* <span data-ttu-id="68505-125">Nuget 调试详细级别应指出包来自何处- [#3055](https://github.com/NuGet/Home/issues/3055)</span><span class="sxs-lookup"><span data-stu-id="68505-125">Nuget Debug verbosity should say where a package came from - [#3055](https://github.com/NuGet/Home/issues/3055)</span></span>

* <span data-ttu-id="68505-126">NuGet 包应不正确地省略句点 in 版本号- [#9215](https://github.com/NuGet/Home/issues/9215)</span><span class="sxs-lookup"><span data-stu-id="68505-126">NuGet pack should catch incorrect omitting of the dot in version numbers - [#9215](https://github.com/NuGet/Home/issues/9215)</span></span>

* <span data-ttu-id="68505-127">[CPVM]禁用集中传递依赖项的固定- [#10132](https://github.com/NuGet/Home/issues/10132)</span><span class="sxs-lookup"><span data-stu-id="68505-127">[CPVM] Disable pinning of the central transitive dependencies  - [#10132](https://github.com/NuGet/Home/issues/10132)</span></span>

* <span data-ttu-id="68505-128">net5 TFM：缺少 TPV 时产生错误 [#9441](https://github.com/NuGet/Home/issues/9441)</span><span class="sxs-lookup"><span data-stu-id="68505-128">net5 TFM: produce error when missing TPV - [#9441](https://github.com/NuGet/Home/issues/9441)</span></span>

* <span data-ttu-id="68505-129">在提取) 期间 (还原日志记录期间记录包- [#10384](https://github.com/NuGet/Home/issues/10384)</span><span class="sxs-lookup"><span data-stu-id="68505-129">Log package contenthash during restore logging (during extraction) - [#10384](https://github.com/NuGet/Home/issues/10384)</span></span>

* <span data-ttu-id="68505-130">为旧 PR 项目实现一种预先注册机制，在解决方案打开时调用 restore [#9986](https://github.com/NuGet/Home/issues/9986)</span><span class="sxs-lookup"><span data-stu-id="68505-130">Implement a pre-registration mechanism for legacy PR projects that call restore at solution open - [#9986](https://github.com/NuGet/Home/issues/9986)</span></span>

* <span data-ttu-id="68505-131">当在包管理器中选择多个源时，NuGet 包推荐器应该工作- [#10433](https://github.com/NuGet/Home/issues/10433)</span><span class="sxs-lookup"><span data-stu-id="68505-131">NuGet package recommender should work when more than one source is selected in package manager - [#10433](https://github.com/NuGet/Home/issues/10433)</span></span>

* <span data-ttu-id="68505-132">如果按正常的详细级别还原，请记录正在从中还原包的源 [#10461](https://github.com/NuGet/Home/issues/10461)</span><span class="sxs-lookup"><span data-stu-id="68505-132">When restoring at normal verbosity, log which source a package is being restored from - [#10461](https://github.com/NuGet/Home/issues/10461)</span></span>

<span data-ttu-id="68505-133">**漏洞**</span><span class="sxs-lookup"><span data-stu-id="68505-133">**Bugs:**</span></span>

* <span data-ttu-id="68505-134">INuGetPackageFileService-为 Codespaces 连接的和独立的[#10151](https://github.com/NuGet/Home/issues/10151)提取映像和嵌入式许可证</span><span class="sxs-lookup"><span data-stu-id="68505-134">INuGetPackageFileService - Fetch Images and embedded licenses for Codespaces-connected and standalone - [#10151](https://github.com/NuGet/Home/issues/10151)</span></span>

* <span data-ttu-id="68505-135">VS OE： IProjectMetadataContextInfo 缺少格式化程序- [#10079](https://github.com/NuGet/Home/issues/10079)</span><span class="sxs-lookup"><span data-stu-id="68505-135">VS OE:  IProjectMetadataContextInfo missing formatter - [#10079](https://github.com/NuGet/Home/issues/10079)</span></span>

* <span data-ttu-id="68505-136">[CPVM]减少写入到 centralTransitiveDependencyGroups 的信息- [#10002](https://github.com/NuGet/Home/issues/10002)</span><span class="sxs-lookup"><span data-stu-id="68505-136">[CPVM-Perf] Reduce the information written to centralTransitiveDependencyGroups - [#10002](https://github.com/NuGet/Home/issues/10002)</span></span>

* <span data-ttu-id="68505-137">由于未加载项目而引发的还原操作会报告为 `NoOp` 遥测- [#9985](https://github.com/NuGet/Home/issues/9985)</span><span class="sxs-lookup"><span data-stu-id="68505-137">Restore operations that throw due to a project not being loaded are reported as `NoOp` in telemetry - [#9985](https://github.com/NuGet/Home/issues/9985)</span></span>

* <span data-ttu-id="68505-138">具有特定颜色托盘的图标导致 PM UI 崩溃与 [#10037](https://github.com/NuGet/Home/issues/10037)</span><span class="sxs-lookup"><span data-stu-id="68505-138">Icons with certain color pallets causes PM UI to crash VS - [#10037](https://github.com/NuGet/Home/issues/10037)</span></span>

* <span data-ttu-id="68505-139">[CPVM]添加 CPVM 信息时减少 PackageSpec 克隆- [#10003](https://github.com/NuGet/Home/issues/10003)</span><span class="sxs-lookup"><span data-stu-id="68505-139">[CPVM-Perf] Reduce the PackageSpec clone when adding the CPVM information  - [#10003](https://github.com/NuGet/Home/issues/10003)</span></span>

* <span data-ttu-id="68505-140">PM UI-asyncify 图标加载- [#10009](https://github.com/NuGet/Home/issues/10009)</span><span class="sxs-lookup"><span data-stu-id="68505-140">PM UI - asyncify icon loading - [#10009](https://github.com/NuGet/Home/issues/10009)</span></span>

* <span data-ttu-id="68505-141">在 PM UI 中加载图标 Url 时的 UI 延迟- [#8505](https://github.com/NuGet/Home/issues/8505)</span><span class="sxs-lookup"><span data-stu-id="68505-141">UI delay when loading icon URLs in PM UI - [#8505](https://github.com/NuGet/Home/issues/8505)</span></span>

* <span data-ttu-id="68505-142">BitmapSource 和 WPF UI 线程中的线程关联- [#9161](https://github.com/NuGet/Home/issues/9161)</span><span class="sxs-lookup"><span data-stu-id="68505-142">Thread affinity in BitmapSource and WPF UI threads - [#9161](https://github.com/NuGet/Home/issues/9161)</span></span>

* <span data-ttu-id="68505-143">Packastool 带有 targetframework 别名[#10097](https://github.com/NuGet/Home/issues/10097)时警告 NU5128</span><span class="sxs-lookup"><span data-stu-id="68505-143">Warning for warning NU5128 when packastool with targetframework alias - [#10097](https://github.com/NuGet/Home/issues/10097)</span></span>

* <span data-ttu-id="68505-144">自定义生成中包目标中的 OutputPath 逻辑不能正常工作- [#9234](https://github.com/NuGet/Home/issues/9234)</span><span class="sxs-lookup"><span data-stu-id="68505-144">OutputPath logic in Pack targets in a customized build doesn't work properly - [#9234](https://github.com/NuGet/Home/issues/9234)</span></span>

* <span data-ttu-id="68505-145">VS OE：在客户端上缓存 IServiceBroker 实例- [#10141](https://github.com/NuGet/Home/issues/10141)</span><span class="sxs-lookup"><span data-stu-id="68505-145">VS OE:  cache IServiceBroker instance on client - [#10141](https://github.com/NuGet/Home/issues/10141)</span></span>

* <span data-ttu-id="68505-146">创建用于从 PM UI 中卸载的 NuGetProjectActions 并行操作- [#9956](https://github.com/NuGet/Home/issues/9956)</span><span class="sxs-lookup"><span data-stu-id="68505-146">Make creating NuGetProjectActions for uninstall  from PM UI a parallel operation - [#9956](https://github.com/NuGet/Home/issues/9956)</span></span>

* <span data-ttu-id="68505-147">性能：减少旧项目和非 PR 项目的 GetPackageSpecsAsync 中的 UIDelays- [#9953](https://github.com/NuGet/Home/issues/9953)</span><span class="sxs-lookup"><span data-stu-id="68505-147">Performance: Reduce UIDelays in GetPackageSpecsAsync for Legacy projects and non PR projects - [#9953](https://github.com/NuGet/Home/issues/9953)</span></span>

* <span data-ttu-id="68505-148">``dotnet nuget push *.nupkg`` 不推送多个文件 [#4393](https://github.com/NuGet/Home/issues/4393)</span><span class="sxs-lookup"><span data-stu-id="68505-148">``dotnet nuget push *.nupkg`` doesn't push more than one file - [#4393](https://github.com/NuGet/Home/issues/4393)</span></span>

* <span data-ttu-id="68505-149">重[#10198](https://github.com/NuGet/Home/issues/10198)定向时，输出将在 macOS 上的80个字符处换行</span><span class="sxs-lookup"><span data-stu-id="68505-149">Output is wrapped at 80 characters on macOS when redirected - [#10198](https://github.com/NuGet/Home/issues/10198)</span></span>

* <span data-ttu-id="68505-150">还原失败，并出现-Source <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406)</span><span class="sxs-lookup"><span data-stu-id="68505-150">Restore fails with -Source <Relative Path> - [#9406](https://github.com/NuGet/Home/issues/9406)</span></span>

* <span data-ttu-id="68505-151">netcoreapp 5.0-windows 不往返行程并且不分析平台信息- [#10177](https://github.com/NuGet/Home/issues/10177)</span><span class="sxs-lookup"><span data-stu-id="68505-151">netcoreapp5.0-windows does not round trip and does not parse platform information - [#10177](https://github.com/NuGet/Home/issues/10177)</span></span>

* <span data-ttu-id="68505-152">自定义 CPS 项目需要 AssemblyReferences 项目功能才能进行还原。</span><span class="sxs-lookup"><span data-stu-id="68505-152">Custom CPS projects require AssemblyReferences project capability in order to restore.</span></span><span data-ttu-id="68505-153"> - [#8071](https://github.com/NuGet/Home/issues/8071)</span><span class="sxs-lookup"><span data-stu-id="68505-153"> - [#8071](https://github.com/NuGet/Home/issues/8071)</span></span>

* <span data-ttu-id="68505-154">许可证和图标文件存在检查应始终使用区分大小写的比较 [#9817](https://github.com/NuGet/Home/issues/9817)</span><span class="sxs-lookup"><span data-stu-id="68505-154">License and icon file existence check should always use a case-sensitive comparison - [#9817](https://github.com/NuGet/Home/issues/9817)</span></span>

* <span data-ttu-id="68505-155">DotnetCLiToolReference 还原使得不项目计数/uptodateprojectscount 的原因非常困难- [#10038](https://github.com/NuGet/Home/issues/10038)</span><span class="sxs-lookup"><span data-stu-id="68505-155">DotnetCLiToolReference restores make it difficult to reason about no-op projects count/uptodateprojectscount - [#10038](https://github.com/NuGet/Home/issues/10038)</span></span>

* <span data-ttu-id="68505-156">在深色主题中通过 "选择 NuGet 包管理器格式" 对话框导航到选项卡时，很难查看包格式的划线框- [#9729](https://github.com/NuGet/Home/issues/9729)</span><span class="sxs-lookup"><span data-stu-id="68505-156">Hard to see the dash-line box of package format when navigating by tab through the “Choose NuGet Package Manager Format” dialog in Dark theme - [#9729](https://github.com/NuGet/Home/issues/9729)</span></span>

* <span data-ttu-id="68505-157">从 #10314 中排除传递框架引用 `CollectFrameworkReferences`  -  [](https://github.com/NuGet/Home/issues/10314)</span><span class="sxs-lookup"><span data-stu-id="68505-157">Exclude transitive framework references from `CollectFrameworkReferences` - [#10314](https://github.com/NuGet/Home/issues/10314)</span></span>

* <span data-ttu-id="68505-158">比较器静态属性应该是幂等的 [#10339](https://github.com/NuGet/Home/issues/10339)</span><span class="sxs-lookup"><span data-stu-id="68505-158">Comparer static properties should be idempotent  - [#10339](https://github.com/NuGet/Home/issues/10339)</span></span>

* <span data-ttu-id="68505-159">解析内部协定程序集加载 (修复 RPS 或获取异常) - [#9919](https://github.com/NuGet/Home/issues/9919)</span><span class="sxs-lookup"><span data-stu-id="68505-159">resolve internal contracts assembly loading (fix RPS or get exception) - [#9919](https://github.com/NuGet/Home/issues/9919)</span></span>

* <span data-ttu-id="68505-160">将 GetService 替换为 NuGet 中的 Getserviceasyn。客户端，第1部分- [#10362](https://github.com/NuGet/Home/issues/10362)</span><span class="sxs-lookup"><span data-stu-id="68505-160">Replace GetService with GetServiceAsync in NuGet.Clients, Part 1 - [#10362](https://github.com/NuGet/Home/issues/10362)</span></span>

* <span data-ttu-id="68505-161">CLI 安装不应安装未列出的包- [#7466](https://github.com/NuGet/Home/issues/7466)</span><span class="sxs-lookup"><span data-stu-id="68505-161">CLI installs should not install unlisted packages - [#7466](https://github.com/NuGet/Home/issues/7466)</span></span>

* <span data-ttu-id="68505-162">静态 msbuild graph 恢复-有关 MSBuildStartupDirectory 的 unnnecessary 日志记录- [#10335](https://github.com/NuGet/Home/issues/10335)</span><span class="sxs-lookup"><span data-stu-id="68505-162">Static msbuild graph restore - unnnecessary logging about MSBuildStartupDirectory - [#10335](https://github.com/NuGet/Home/issues/10335)</span></span>

* <span data-ttu-id="68505-163">标记为 PrivateAssets 的 Projectreference 的项目依赖项不应包含在 "锁定文件最新" 复选 [#8565](https://github.com/NuGet/Home/issues/8565)</span><span class="sxs-lookup"><span data-stu-id="68505-163">Project Dependencies of ProjectReferences marked as PrivateAssets should not be included in the lock file up to date check - [#8565](https://github.com/NuGet/Home/issues/8565)</span></span>

* <span data-ttu-id="68505-164">包含错误数据的 SDK 项目未在 VS [#10406](https://github.com/NuGet/Home/issues/10406)中显示还原错误</span><span class="sxs-lookup"><span data-stu-id="68505-164">SDK projects with bad data not showing restore errors in VS - [#10406](https://github.com/NuGet/Home/issues/10406)</span></span>

* <span data-ttu-id="68505-165">使用 LockedMode [#9623](https://github.com/NuGet/Home/issues/9623)从 cmd 行还原具有混合旧项目和 netstandard2 项目的解决方案时，NU1004</span><span class="sxs-lookup"><span data-stu-id="68505-165">NU1004 when restoring a solution that has mixed Legacy and netstandard2 projects from cmd line with LockedMode - [#9623](https://github.com/NuGet/Home/issues/9623)</span></span>

* <span data-ttu-id="68505-166">包包含通过依赖项包引入的内容到当前项目的包中， (基于 SDK 的项目仅) - [#8867](https://github.com/NuGet/Home/issues/8867)</span><span class="sxs-lookup"><span data-stu-id="68505-166">Pack includes content brought in through dependency packages into the current project's package (SDK based projects only) - [#8867](https://github.com/NuGet/Home/issues/8867)</span></span>

* <span data-ttu-id="68505-167">为 NuGet 的 VS 扩展性 API 故障添加遥测- [#10062](https://github.com/NuGet/Home/issues/10062)</span><span class="sxs-lookup"><span data-stu-id="68505-167">Add telemetry for NuGet's VS extensibility API faults - [#10062](https://github.com/NuGet/Home/issues/10062)</span></span>

* <span data-ttu-id="68505-168">在静态图形还原中添加 GenerateRestoreGraphFile 以改善 debugability。</span><span class="sxs-lookup"><span data-stu-id="68505-168">Add GenerateRestoreGraphFile in static graph restore to improve debugability.</span></span><span data-ttu-id="68505-169">  - [#10365](https://github.com/NuGet/Home/issues/10365)</span><span class="sxs-lookup"><span data-stu-id="68505-169">  - [#10365](https://github.com/NuGet/Home/issues/10365)</span></span>

* <span data-ttu-id="68505-170">无法打开 NuGet 包管理器- [#10336](https://github.com/NuGet/Home/issues/10336)</span><span class="sxs-lookup"><span data-stu-id="68505-170">Cannot open the NuGet Package manager - [#10336](https://github.com/NuGet/Home/issues/10336)</span></span>

* <span data-ttu-id="68505-171">NVDA/讲述人未阅读 "Apache-2.0" 链接[#10425](https://github.com/NuGet/Home/issues/10425)的 "许可证" 标签</span><span class="sxs-lookup"><span data-stu-id="68505-171">NVDA/Narrator is not reading "License" label for "Apache-2.0" link - [#10425](https://github.com/NuGet/Home/issues/10425)</span></span>

* <span data-ttu-id="68505-172">在 VS [#9402](https://github.com/NuGet/Home/issues/9402)中，最新状态栏消息不太好</span><span class="sxs-lookup"><span data-stu-id="68505-172">The up to date status bar message is not great in VS - [#9402](https://github.com/NuGet/Home/issues/9402)</span></span>

* <span data-ttu-id="68505-173">packages.config 上的 package.lock.js使用不正确的目标框架- [#10257](https://github.com/NuGet/Home/issues/10257)</span><span class="sxs-lookup"><span data-stu-id="68505-173">packages.config package.lock.json uses an incorrect target framework - [#10257](https://github.com/NuGet/Home/issues/10257)</span></span>

* <span data-ttu-id="68505-174">Codespaces：修复 https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)的遥测</span><span class="sxs-lookup"><span data-stu-id="68505-174">Codespaces:  fix telemetry from https://github.com/NuGet/NuGet.Client/pull/3786 - [#10439](https://github.com/NuGet/Home/issues/10439)</span></span>

* <span data-ttu-id="68505-175">启用 "RestoreLockedMode" 后生成解决方案时，NU1004 错误消失- [#8973](https://github.com/NuGet/Home/issues/8973)</span><span class="sxs-lookup"><span data-stu-id="68505-175">Error NU1004 disappears when building solution after enabling “RestoreLockedMode” - [#8973](https://github.com/NuGet/Home/issues/8973)</span></span>

* <span data-ttu-id="68505-176">反向跳转到反向中的 PMUI 应向前镜像 [#10234](https://github.com/NuGet/Home/issues/10234)</span><span class="sxs-lookup"><span data-stu-id="68505-176">Tabbing through PMUI in the reverse should mirror forward direction - [#10234](https://github.com/NuGet/Home/issues/10234)</span></span>

* <span data-ttu-id="68505-177">在实验实例中调试 PMUI 有时会引发从 SolutionView 到 ProjectView [#10416](https://github.com/NuGet/Home/issues/10416)的 InvalidCastException</span><span class="sxs-lookup"><span data-stu-id="68505-177">Debugging PMUI in Experimental Instance sometimes throws InvalidCastException from SolutionView to ProjectView - [#10416](https://github.com/NuGet/Home/issues/10416)</span></span>

* <span data-ttu-id="68505-178">在 "浏览" 选项卡中单击弃用的包后，默认版本为 null- [#10380](https://github.com/NuGet/Home/issues/10380)</span><span class="sxs-lookup"><span data-stu-id="68505-178">The default version is null after clicking a deprecated package in Browse tab - [#10380](https://github.com/NuGet/Home/issues/10380)</span></span>

* <span data-ttu-id="68505-179">重新获得焦点时，Visual Studio 中的 NuGet 管理器将重新加载- [#4176](https://github.com/NuGet/Home/issues/4176)</span><span class="sxs-lookup"><span data-stu-id="68505-179">The NuGet manager in Visual Studio reloads when focus is regained - [#4176](https://github.com/NuGet/Home/issues/4176)</span></span>

* <span data-ttu-id="68505-180">删除 IPackageSourceProvider2 和相关类型- [#10098](https://github.com/NuGet/Home/issues/10098)</span><span class="sxs-lookup"><span data-stu-id="68505-180">Remove IPackageSourceProvider2 and related types - [#10098](https://github.com/NuGet/Home/issues/10098)</span></span>

* <span data-ttu-id="68505-181">包 "NameOfPackage" 与项目中的 "全部" 框架不兼容- [#5127](https://github.com/NuGet/Home/issues/5127)</span><span class="sxs-lookup"><span data-stu-id="68505-181">Package 'NameOfPackage' is incompatible with 'all' frameworks in project - [#5127](https://github.com/NuGet/Home/issues/5127)</span></span>

* <span data-ttu-id="68505-182">CreateVersionsAsync 不必要的 NuGetVersion 比较- [#10436](https://github.com/NuGet/Home/issues/10436)</span><span class="sxs-lookup"><span data-stu-id="68505-182">CreateVersionsAsync does unnecessary NuGetVersion Compares - [#10436](https://github.com/NuGet/Home/issues/10436)</span></span>

* <span data-ttu-id="68505-183">NuGet。客户端应使用 ManagedImageMonikers 和[#9977](https://github.com/NuGet/Home/issues/9977) KnownMonikers 替换</span><span class="sxs-lookup"><span data-stu-id="68505-183">NuGet.Client should replace using of ManagedImageMonikers with KnownMonikers - [#9977](https://github.com/NuGet/Home/issues/9977)</span></span>

* <span data-ttu-id="68505-184">不推荐使用的图标与浏览器选项卡中不推荐使用的包的版本重叠- [#10452](https://github.com/NuGet/Home/issues/10452)</span><span class="sxs-lookup"><span data-stu-id="68505-184">The deprecated icon overlaps with the version of the deprecated package in Browse tab - [#10452](https://github.com/NuGet/Home/issues/10452)</span></span>

* <span data-ttu-id="68505-185">PackageReference NU1604 错误处理不同于 VS 和命令行 (Restore & 程序包管理器 UI) - [#9289](https://github.com/NuGet/Home/issues/9289)</span><span class="sxs-lookup"><span data-stu-id="68505-185">PackageReference NU1604 error handling is different across VS and command line (Restore & Package Manager UI) - [#9289](https://github.com/NuGet/Home/issues/9289)</span></span>

* <span data-ttu-id="68505-186">Codespaces：未注册必要的格式化程序- [#10467](https://github.com/NuGet/Home/issues/10467)</span><span class="sxs-lookup"><span data-stu-id="68505-186">Codespaces:  necessary formatters not registered - [#10467](https://github.com/NuGet/Home/issues/10467)</span></span>

* <span data-ttu-id="68505-187">从 NuGet 将 net45 作为目标框架删除- [#10470](https://github.com/NuGet/Home/issues/10470)</span><span class="sxs-lookup"><span data-stu-id="68505-187">Remove net45 as as a target framework from NuGet.Frameworks - [#10470](https://github.com/NuGet/Home/issues/10470)</span></span>

* <span data-ttu-id="68505-188">实现-添加新的 telemetries 以跟踪与 PMC 和 Powershell 使用相关的事件。</span><span class="sxs-lookup"><span data-stu-id="68505-188">Implementation - Add new telemetries to track events related to PMC and Powershell usage.</span></span><span data-ttu-id="68505-189"> - [#10142](https://github.com/NuGet/Home/issues/10142)</span><span class="sxs-lookup"><span data-stu-id="68505-189"> - [#10142](https://github.com/NuGet/Home/issues/10142)</span></span>

* <span data-ttu-id="68505-190">当包管理器 UI 中有多个可更新的包时，"预览更改" 窗口中只显示一个包- [#10483](https://github.com/NuGet/Home/issues/10483)</span><span class="sxs-lookup"><span data-stu-id="68505-190">Only one package shows in the Preview Changes window when there are multiple packages available to update in the Package Manager UI - [#10483](https://github.com/NuGet/Home/issues/10483)</span></span>

* <span data-ttu-id="68505-191">打包 multitargeted 项目时，应生成空的 frameworkReferences 组- [#10218](https://github.com/NuGet/Home/issues/10218)</span><span class="sxs-lookup"><span data-stu-id="68505-191">Empty frameworkReferences groups should be generated when packing multitargeted projects - [#10218](https://github.com/NuGet/Home/issues/10218)</span></span>

* <span data-ttu-id="68505-192">如果 "更新" 选项卡上的 "更新" 选项卡[#8963](https://github.com/NuGet/Home/issues/8963))  (中的 "选择" 选项卡上的复选框为突出显示，则很难查看 "更新" 选项卡中的程序包</span><span class="sxs-lookup"><span data-stu-id="68505-192">Hard to see the check-box of package in ‘Updates’ Tab is focused with a dash-line box when navigating through Tab in Blue/Blue (Extra Contrast)/Light themes - [#8963](https://github.com/NuGet/Home/issues/8963)</span></span>

* <span data-ttu-id="68505-193">"更新" 选项卡复选框无法很好地与屏幕阅读器一起使用- [#10449](https://github.com/NuGet/Home/issues/10449)</span><span class="sxs-lookup"><span data-stu-id="68505-193">Updates Tab checkboxes do not work well with screen-readers - [#10449](https://github.com/NuGet/Home/issues/10449)</span></span>

* <span data-ttu-id="68505-194">在 PMUI 中进行更新会导致对象引用未设置为对象的实例- [#9882](https://github.com/NuGet/Home/issues/9882)</span><span class="sxs-lookup"><span data-stu-id="68505-194">Updating in PMUI causes Object reference not set to an instance of an object - [#9882](https://github.com/NuGet/Home/issues/9882)</span></span>

* <span data-ttu-id="68505-195">实现-添加新的 telemetries 以跟踪与 PMC 相关的事件，并跟进 Powershell 使用情况。</span><span class="sxs-lookup"><span data-stu-id="68505-195">Implementation - Add new telemetries to track events related to PMC and Powershell usage follow up.</span></span><span data-ttu-id="68505-196"> - [#10478](https://github.com/NuGet/Home/issues/10478)</span><span class="sxs-lookup"><span data-stu-id="68505-196"> - [#10478](https://github.com/NuGet/Home/issues/10478)</span></span>

* <span data-ttu-id="68505-197">V2FeedPackageInfo 中的复制粘贴错误- [#10480](https://github.com/NuGet/Home/issues/10480)</span><span class="sxs-lookup"><span data-stu-id="68505-197">Copy-paste error in V2FeedPackageInfo - [#10480](https://github.com/NuGet/Home/issues/10480)</span></span>

* <span data-ttu-id="68505-198">NuGetPackageFileService 修复-使用 for 可释放 memorystream- [#10503](https://github.com/NuGet/Home/issues/10503)</span><span class="sxs-lookup"><span data-stu-id="68505-198">NuGetPackageFileService fix - use using for disposable memorystream - [#10503](https://github.com/NuGet/Home/issues/10503)</span></span>


<span data-ttu-id="68505-199">**[此版本中已修复的所有问题的列表-5.9。0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**</span><span class="sxs-lookup"><span data-stu-id="68505-199">**[List of all issues fixed in this release - 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**</span></span>

<span data-ttu-id="68505-200">**[此版本中的提交列表-5.9。0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**</span><span class="sxs-lookup"><span data-stu-id="68505-200">**[List of commits in this release - 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**</span></span>

### <a name="community-contributions"></a><span data-ttu-id="68505-201">社区参与</span><span class="sxs-lookup"><span data-stu-id="68505-201">Community contributions</span></span>

<span data-ttu-id="68505-202">感谢所有有助于使此 NuGet 版本非常出色的参与者！</span><span class="sxs-lookup"><span data-stu-id="68505-202">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="68505-203">谁</span><span class="sxs-lookup"><span data-stu-id="68505-203">Who</span></span>|<span data-ttu-id="68505-204">Pr</span><span class="sxs-lookup"><span data-stu-id="68505-204">PRs</span></span>|<span data-ttu-id="68505-205">问题</span><span class="sxs-lookup"><span data-stu-id="68505-205">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="68505-206">omajid</span><span class="sxs-lookup"><span data-stu-id="68505-206">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="68505-207">3865</span><span class="sxs-lookup"><span data-stu-id="68505-207">3865</span></span>](https://github.com/NuGet/NuGet.Client/pull/3865) | <span data-ttu-id="68505-208">V2FeedPackageInfo 中的复制粘贴错误- [#10480](https://github.com/NuGet/Home/issues/10480)</span><span class="sxs-lookup"><span data-stu-id="68505-208">Copy-paste error in V2FeedPackageInfo - [#10480](https://github.com/NuGet/Home/issues/10480)</span></span>
[<span data-ttu-id="68505-209">marcin-krystianc</span><span class="sxs-lookup"><span data-stu-id="68505-209">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="68505-210">3812</span><span class="sxs-lookup"><span data-stu-id="68505-210">3812</span></span>](https://github.com/NuGet/NuGet.Client/pull/3812) | <span data-ttu-id="68505-211">对于用 PrivateAssets = "All" 属性引用包的情况，缺少测试 [#10397](https://github.com/NuGet/Home/issues/10397)</span><span class="sxs-lookup"><span data-stu-id="68505-211">Missing tests for the case where packages are referenced with PrivateAssets="All" attribute - [#10397](https://github.com/NuGet/Home/issues/10397)</span></span>
[<span data-ttu-id="68505-212">marcin-krystianc</span><span class="sxs-lookup"><span data-stu-id="68505-212">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="68505-213">3739</span><span class="sxs-lookup"><span data-stu-id="68505-213">3739</span></span>](https://github.com/NuGet/NuGet.Client/pull/3739) | <span data-ttu-id="68505-214">添加了推送多个包的支持- [#4393](https://github.com/NuGet/Home/issues/4393)</span><span class="sxs-lookup"><span data-stu-id="68505-214">Adding support for pushing multiple packages - [#4393](https://github.com/NuGet/Home/issues/4393)</span></span>
[<span data-ttu-id="68505-215">marcin-krystianc</span><span class="sxs-lookup"><span data-stu-id="68505-215">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="68505-216">3723</span><span class="sxs-lookup"><span data-stu-id="68505-216">3723</span></span>](https://github.com/NuGet/NuGet.Client/pull/3723) | <span data-ttu-id="68505-217">禁用程序集签名时，NuGet 库的生成已断开- [#10173](https://github.com/NuGet/Home/issues/10173)</span><span class="sxs-lookup"><span data-stu-id="68505-217">Build of NuGet libraries is broken when assembly signing is disabled - [#10173](https://github.com/NuGet/Home/issues/10173)</span></span>
[<span data-ttu-id="68505-218">kant2002</span><span class="sxs-lookup"><span data-stu-id="68505-218">kant2002</span></span>](https://github.com/kant2002) | [<span data-ttu-id="68505-219">3807</span><span class="sxs-lookup"><span data-stu-id="68505-219">3807</span></span>](https://github.com/NuGet/NuGet.Client/pull/3807) | <span data-ttu-id="68505-220">清理参与的文档- [#10399](https://github.com/NuGet/Home/issues/10399)</span><span class="sxs-lookup"><span data-stu-id="68505-220">Clean-up the contributing docs - [#10399](https://github.com/NuGet/Home/issues/10399)</span></span>
[<span data-ttu-id="68505-221">PathogenDavid</span><span class="sxs-lookup"><span data-stu-id="68505-221">PathogenDavid</span></span>](https://github.com/PathogenDavid) | [<span data-ttu-id="68505-222">3754</span><span class="sxs-lookup"><span data-stu-id="68505-222">3754</span></span>](https://github.com/NuGet/NuGet.Client/pull/3754) | <span data-ttu-id="68505-223">许可证和图标文件存在检查应始终使用区分大小写的比较 [#9817](https://github.com/NuGet/Home/issues/9817)</span><span class="sxs-lookup"><span data-stu-id="68505-223">License and icon file existence check should always use a case-sensitive comparison - [#9817](https://github.com/NuGet/Home/issues/9817)</span></span>
[<span data-ttu-id="68505-224">campersau</span><span class="sxs-lookup"><span data-stu-id="68505-224">campersau</span></span>](https://github.com/campersau) | [<span data-ttu-id="68505-225">3677</span><span class="sxs-lookup"><span data-stu-id="68505-225">3677</span></span>](https://github.com/NuGet/NuGet.Client/pull/3677) | <span data-ttu-id="68505-226">使用 DecodePixelWidth [#10037](https://github.com/NuGet/Home/issues/10037)时，请使用 IGNORECOLORPROFILE 解决 WPF 问题</span><span class="sxs-lookup"><span data-stu-id="68505-226">Use BitmapCreateOptions.IgnoreColorProfile to workaround WPF issue when using DecodePixelWidth - [#10037](https://github.com/NuGet/Home/issues/10037)</span></span>
[<span data-ttu-id="68505-227">bjorkstromm</span><span class="sxs-lookup"><span data-stu-id="68505-227">bjorkstromm</span></span>](https://github.com/bjorkstromm) | [<span data-ttu-id="68505-228">3697</span><span class="sxs-lookup"><span data-stu-id="68505-228">3697</span></span>](https://github.com/NuGet/NuGet.Client/pull/3697) | <span data-ttu-id="68505-229">NuGet 中 Windows SDK 10 链接已断开。客户端贡献指南- [#10099](https://github.com/NuGet/Home/issues/10099)</span><span class="sxs-lookup"><span data-stu-id="68505-229">Windows SDK 10 link is broken in NuGet.Client Contribution guide - [#10099](https://github.com/NuGet/Home/issues/10099)</span></span>
[<span data-ttu-id="68505-230">bjorkstromm</span><span class="sxs-lookup"><span data-stu-id="68505-230">bjorkstromm</span></span>](https://github.com/bjorkstromm) | [<span data-ttu-id="68505-231">3696</span><span class="sxs-lookup"><span data-stu-id="68505-231">3696</span></span>](https://github.com/NuGet/NuGet.Client/pull/3696) | <span data-ttu-id="68505-232">NuGet 中的相对链接断开。客户端调试指南- [#10100](https://github.com/NuGet/Home/issues/10100)</span><span class="sxs-lookup"><span data-stu-id="68505-232">Relative links are broken in NuGet.Client debugging guide - [#10100](https://github.com/NuGet/Home/issues/10100)</span></span>
[<span data-ttu-id="68505-233">Nirmal4G</span><span class="sxs-lookup"><span data-stu-id="68505-233">Nirmal4G</span></span>](https://github.com/Nirmal4G) | [<span data-ttu-id="68505-234">3637</span><span class="sxs-lookup"><span data-stu-id="68505-234">3637</span></span>](https://github.com/NuGet/NuGet.Client/pull/3637) | <span data-ttu-id="68505-235">改善测试装置和相关的代码- [#9996](https://github.com/NuGet/Home/issues/9996)</span><span class="sxs-lookup"><span data-stu-id="68505-235">Improve test fixtures and related code - [#9996](https://github.com/NuGet/Home/issues/9996)</span></span>
[<span data-ttu-id="68505-236">rolfbjarne</span><span class="sxs-lookup"><span data-stu-id="68505-236">rolfbjarne</span></span>](https://github.com/rolfbjarne) | [<span data-ttu-id="68505-237">3743</span><span class="sxs-lookup"><span data-stu-id="68505-237">3743</span></span>](https://github.com/NuGet/NuGet.Client/pull/3743) | <span data-ttu-id="68505-238">重[#10198](https://github.com/NuGet/Home/issues/10198)定向时，输出将在 macOS 上的80个字符处换行</span><span class="sxs-lookup"><span data-stu-id="68505-238">Output is wrapped at 80 characters on macOS when redirected - [#10198](https://github.com/NuGet/Home/issues/10198)</span></span>
[<span data-ttu-id="68505-239">xen2</span><span class="sxs-lookup"><span data-stu-id="68505-239">xen2</span></span>](https://github.com/xen2) | [<span data-ttu-id="68505-240">2861</span><span class="sxs-lookup"><span data-stu-id="68505-240">2861</span></span>](https://github.com/NuGet/NuGet.Client/pull/2861) | <span data-ttu-id="68505-241">使 Nuget.exe 作为 .NET Standard 包提供 [#6150](https://github.com/NuGet/Home/issues/6150)</span><span class="sxs-lookup"><span data-stu-id="68505-241">Make NuGet.PackageManagement available as a .NET Standard package - [#6150](https://github.com/NuGet/Home/issues/6150)</span></span>
[<span data-ttu-id="68505-242">Anipik</span><span class="sxs-lookup"><span data-stu-id="68505-242">Anipik</span></span>](https://github.com/Anipik) | [<span data-ttu-id="68505-243">3810</span><span class="sxs-lookup"><span data-stu-id="68505-243">3810</span></span>](https://github.com/NuGet/NuGet.Client/pull/3810) | <span data-ttu-id="68505-244">引入一个新的 msbuild 属性，以便在包任务期间排除特定 tfm 的生成输出- [#10396](https://github.com/NuGet/Home/issues/10396)</span><span class="sxs-lookup"><span data-stu-id="68505-244">Introduce a new msbuild property to exclude build output for specific tfms during pack task - [#10396](https://github.com/NuGet/Home/issues/10396)</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="68505-245">欢迎反馈</span><span class="sxs-lookup"><span data-stu-id="68505-245">Feedback welcome</span></span>

<span data-ttu-id="68505-246">反馈对我们非常重要。</span><span class="sxs-lookup"><span data-stu-id="68505-246">Your feedback is important to us.</span></span>  <span data-ttu-id="68505-247">如果此版本有任何问题，请查看有关现有问题的 [GitHub 问题](https://github.com/NuGet/Home/issues) 和 [Visual Studio 开发人员社区](https://developercommunity.visualstudio.com/) 。</span><span class="sxs-lookup"><span data-stu-id="68505-247">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="68505-248">对于 NuGet 中的新问题，请报告 [GitHub 问题](https://github.com/NuGet/Home/issues/new)。</span><span class="sxs-lookup"><span data-stu-id="68505-248">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="68505-249">对于一般的 NuGet 体验问题，请通过 "帮助" 下的 "你喜欢的 IDE" 中的 " [报告问题](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) " 选项告知我们 **> 报告问题**。</span><span class="sxs-lookup"><span data-stu-id="68505-249">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
