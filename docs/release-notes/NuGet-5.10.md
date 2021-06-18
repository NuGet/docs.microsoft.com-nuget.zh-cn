---
title: NuGet 5.10 发行说明
description: NuGet 5.10 的发行说明，包括新功能、bug 修复和 DCR。
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356496"
---
# <a name="nuget-510-release-notes"></a><span data-ttu-id="6dc67-103">NuGet 5.10 发行说明</span><span class="sxs-lookup"><span data-stu-id="6dc67-103">NuGet 5.10 Release Notes</span></span>

<span data-ttu-id="6dc67-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="6dc67-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="6dc67-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="6dc67-105">NuGet version</span></span> | <span data-ttu-id="6dc67-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="6dc67-106">Available in Visual Studio version</span></span> | <span data-ttu-id="6dc67-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6dc67-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="6dc67-108">**5.10.0**</span><span class="sxs-lookup"><span data-stu-id="6dc67-108">**5.10.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="6dc67-109">Visual Studio 2019 版本 16.10</span><span class="sxs-lookup"><span data-stu-id="6dc67-109">Visual Studio 2019 version 16.10</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="6dc67-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="6dc67-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="6dc67-111"><sup>1</sup> 随 2019 Visual Studio .NET Core 工作负载一起安装</span><span class="sxs-lookup"><span data-stu-id="6dc67-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="6dc67-112">Visual Studio 16.10、MSBuild 16.10 和 .NET 5.0.300+ 需要 NuGet.exe 5.10 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="6dc67-112">Visual Studio 16.10, MSBuild 16.10, and .NET 5.0.300+ requires NuGet.exe 5.10 or later.</span></span>

## <a name="summary-whats-new-in-510"></a><span data-ttu-id="6dc67-113">摘要：5.10 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="6dc67-113">Summary: What's New in 5.10</span></span>

* <span data-ttu-id="6dc67-114">签名：实现 dotnet trusted-signers 命令 - [#8053](https://github.com/NuGet/Home/issues/8053)</span><span class="sxs-lookup"><span data-stu-id="6dc67-114">Signing: implement dotnet trusted-signers command - [#8053](https://github.com/NuGet/Home/issues/8053)</span></span>

* <span data-ttu-id="6dc67-115">在 Linux 上禁用默认验证，但在 Windows 上默认启用 - [#10713](https://github.com/NuGet/Home/issues/10713)</span><span class="sxs-lookup"><span data-stu-id="6dc67-115">Make default validation disabled on Linux, but enabled by default on Windows - [#10713](https://github.com/NuGet/Home/issues/10713)</span></span>

* <span data-ttu-id="6dc67-116">在 .NET 5+ Linux/MAC 上为包签名验证添加 ENV 变量 - [#10742](https://github.com/NuGet/Home/issues/10742)</span><span class="sxs-lookup"><span data-stu-id="6dc67-116">Add an ENV Variable for Package Signing Verification on .NET 5+ Linux/MAC - [#10742](https://github.com/NuGet/Home/issues/10742)</span></span>

* <span data-ttu-id="6dc67-117">提高大型解决方案的安装新包性能 - [#10166](https://github.com/NuGet/Home/issues/10166)</span><span class="sxs-lookup"><span data-stu-id="6dc67-117">Improve install new package performance for large solutions - [#10166](https://github.com/NuGet/Home/issues/10166)</span></span>

* <span data-ttu-id="6dc67-118">将项目类型 `nfproj` 添加到 Nuget CLI 的 supportedProjectExtensions 列表中。</span><span class="sxs-lookup"><span data-stu-id="6dc67-118">Add the project type `nfproj` to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="6dc67-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="6dc67-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="6dc67-120">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="6dc67-120">Issues fixed in this release</span></span>

* <span data-ttu-id="6dc67-121">打包 <requireLicenseAcceptance> 项目时取消元素 - [#5133](https://github.com/NuGet/Home/issues/5133)</span><span class="sxs-lookup"><span data-stu-id="6dc67-121">Suppress the <requireLicenseAcceptance> element when packing a project - [#5133](https://github.com/NuGet/Home/issues/5133)</span></span>

* <span data-ttu-id="6dc67-122">[CPVM] 预览警告应显示在 dotnet cli 上 - [#10226](https://github.com/NuGet/Home/issues/10226)</span><span class="sxs-lookup"><span data-stu-id="6dc67-122">[CPVM] preview warning should be shown on dotnet cli - [#10226](https://github.com/NuGet/Home/issues/10226)</span></span>

* <span data-ttu-id="6dc67-123">将 PMUI 的背景和前景色标记更新为 CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)</span><span class="sxs-lookup"><span data-stu-id="6dc67-123">Update the background and foreground color tokens of the PMUI to CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)</span></span>

* <span data-ttu-id="6dc67-124">[Bug Bash]在 PM UI 中快速切换选项卡时，错误"用户取消的操作"显示在"错误列表"窗口中 - [#10671](https://github.com/NuGet/Home/issues/10671)</span><span class="sxs-lookup"><span data-stu-id="6dc67-124">[Bug Bash] Error “operation canceled by user” show in Error List window when switching between tabs quickly in PM UI - [#10671](https://github.com/NuGet/Home/issues/10671)</span></span>

* <span data-ttu-id="6dc67-125">PM UI：提高解决方案级别的包安装性能 - [#10210](https://github.com/NuGet/Home/issues/10210)</span><span class="sxs-lookup"><span data-stu-id="6dc67-125">PM UI:  Improve package installation performance on the solution level - [#10210](https://github.com/NuGet/Home/issues/10210)</span></span>

* <span data-ttu-id="6dc67-126">将 GetService 替换为 NuGet.Clients 中所有位置的 GetServiceAsync - [#3784](https://github.com/NuGet/Home/issues/3784)</span><span class="sxs-lookup"><span data-stu-id="6dc67-126">Replace GetService with GetServiceAsync everywhere in NuGet.Clients - [#3784](https://github.com/NuGet/Home/issues/3784)</span></span>

* <span data-ttu-id="6dc67-127">NuGet.exe相对路径的包 `..` 性能问题 - [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="6dc67-127">NuGet.exe pack performance problem with `..` relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>

* <span data-ttu-id="6dc67-128">"nuget pack"的性能随源路径中的级别增加而降低 - [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="6dc67-128">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>

* <span data-ttu-id="6dc67-129">使用重复文件打包 nuspec 时，NuGet 不会出错。</span><span class="sxs-lookup"><span data-stu-id="6dc67-129">NuGet doesn't error when packaging nuspec with duplicate files.</span></span><span data-ttu-id="6dc67-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span><span class="sxs-lookup"><span data-stu-id="6dc67-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span></span>

* <span data-ttu-id="6dc67-131">NuGet 包"指定的 DateTimeOffset 不能转换为 Zip 文件时间戳"- [#7001](https://github.com/NuGet/Home/issues/7001)</span><span class="sxs-lookup"><span data-stu-id="6dc67-131">NuGet pack "The DateTimeOffset specified cannot be converted into a Zip file timestamp" - [#7001](https://github.com/NuGet/Home/issues/7001)</span></span>

* <span data-ttu-id="6dc67-132">打包包文件的时间戳按时区移动 - [#7395](https://github.com/NuGet/Home/issues/7395)</span><span class="sxs-lookup"><span data-stu-id="6dc67-132">Timestamps of file of packed package is shifted by the timezone - [#7395](https://github.com/NuGet/Home/issues/7395)</span></span>

* <span data-ttu-id="6dc67-133">NU1004 应包含更多可操作的信息 - [#7696](https://github.com/NuGet/Home/issues/7696)</span><span class="sxs-lookup"><span data-stu-id="6dc67-133">NU1004 should contain more actionable information  - [#7696](https://github.com/NuGet/Home/issues/7696)</span></span>

* <span data-ttu-id="6dc67-134">[Bug Bash][测试失败]运行 "dotnet restore --use-lock-file --locked-mode" 时，不应更新空的/格式错误的锁文件 - [#8640](https://github.com/NuGet/Home/issues/8640)</span><span class="sxs-lookup"><span data-stu-id="6dc67-134">[Bug Bash][Test Failure] The empty/malformed lock file should not be updated when running ‘dotnet restore --use-lock-file --locked-mode’ - [#8640](https://github.com/NuGet/Home/issues/8640)</span></span>

* <span data-ttu-id="6dc67-135">NuGetVersionRange 允许分析逻辑上不正确的范围 - [#9145](https://github.com/NuGet/Home/issues/9145)</span><span class="sxs-lookup"><span data-stu-id="6dc67-135">NuGetVersionRange allows logically incorrect ranges to be parsed - [#9145](https://github.com/NuGet/Home/issues/9145)</span></span>

* <span data-ttu-id="6dc67-136">PM UI 无法显示所选包源和悬停包源之间的可区分背景色[-](https://github.com/NuGet/Home/issues/9538) #9538</span><span class="sxs-lookup"><span data-stu-id="6dc67-136">PM UI can’t show distinguishable background color between selected and hovered package sources - [#9538](https://github.com/NuGet/Home/issues/9538)</span></span>

* <span data-ttu-id="6dc67-137">屏幕阅读器无法读取选择要安装到的项目的复选框[-](https://github.com/NuGet/Home/issues/9578) #9578</span><span class="sxs-lookup"><span data-stu-id="6dc67-137">Checkbox for selecting projects to install to isn't being read by screen reader - [#9578](https://github.com/NuGet/Home/issues/9578)</span></span>

* <span data-ttu-id="6dc67-138">详细信息窗格版本下拉列表的默认选择应为"已安装/更新"选项卡上的"已安装/最新""#9887 [](https://github.com/NuGet/Home/issues/9887)</span><span class="sxs-lookup"><span data-stu-id="6dc67-138">Details Pane Versions Dropdown default selection should be Installed/LatestStable on Installed/Updates tabs - [#9887](https://github.com/NuGet/Home/issues/9887)</span></span>

* <span data-ttu-id="6dc67-139">删除某些 .NET 5 SDK 报表 TargetPlatformMoniker 的解决方法 ` ,Version= `  -  [帐户](https://github.com/NuGet/Home/issues/9913)#9913</span><span class="sxs-lookup"><span data-stu-id="6dc67-139">Remove workaround account for some .NET 5 SDKs report TargetPlatformMoniker of ` ,Version= ` - [#9913](https://github.com/NuGet/Home/issues/9913)</span></span>

* <span data-ttu-id="6dc67-140">dotnet nuget verify 太静默 - [#10316](https://github.com/NuGet/Home/issues/10316)</span><span class="sxs-lookup"><span data-stu-id="6dc67-140">dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)</span></span>

* <span data-ttu-id="6dc67-141">VersionRange 无法分析单位数范围 - [#10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="6dc67-141">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>

* <span data-ttu-id="6dc67-142">VS 解决方案管理器在调试期间为 引发 null 异常 - [#10352](https://github.com/NuGet/Home/issues/10352)</span><span class="sxs-lookup"><span data-stu-id="6dc67-142">VS Solution manager throws null exception for during debugging - [#10352](https://github.com/NuGet/Home/issues/10352)</span></span>

* <span data-ttu-id="6dc67-143">将 CLI 异常消息移动到字符串资源文件 - [#10392](https://github.com/NuGet/Home/issues/10392)</span><span class="sxs-lookup"><span data-stu-id="6dc67-143">Move CLI exception messages to String Resource files - [#10392](https://github.com/NuGet/Home/issues/10392)</span></span>

* <span data-ttu-id="6dc67-144">删除 TabItemButtonAutomationPeer (死) - [#10435](https://github.com/NuGet/Home/issues/10435)</span><span class="sxs-lookup"><span data-stu-id="6dc67-144">Remove dead code (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)</span></span>

* <span data-ttu-id="6dc67-145">更新上下文菜单应滚动到第一个选定项 - [#10498](https://github.com/NuGet/Home/issues/10498)</span><span class="sxs-lookup"><span data-stu-id="6dc67-145">Update context menu should scroll to first selected item - [#10498](https://github.com/NuGet/Home/issues/10498)</span></span>

* <span data-ttu-id="6dc67-146">解决方案 PMUI 详细信息具有重叠的水平条 - [#10533](https://github.com/NuGet/Home/issues/10533)</span><span class="sxs-lookup"><span data-stu-id="6dc67-146">Solution PMUI Details has overlapping horizontal bar - [#10533](https://github.com/NuGet/Home/issues/10533)</span></span>

* <span data-ttu-id="6dc67-147">签名：证书过期且时间戳不受信任时不显示主签名详细信息 - [#10535](https://github.com/NuGet/Home/issues/10535)</span><span class="sxs-lookup"><span data-stu-id="6dc67-147">Signing:  primary signature details not displayed when certificate expired and timestamp untrusted - [#10535](https://github.com/NuGet/Home/issues/10535)</span></span>

* <span data-ttu-id="6dc67-148">如果没有启用的源，PM UI 将阻止显示 - [#10541](https://github.com/NuGet/Home/issues/10541)</span><span class="sxs-lookup"><span data-stu-id="6dc67-148">Having no enabled sources prevents the PM UI from showing - [#10541](https://github.com/NuGet/Home/issues/10541)</span></span>

* <span data-ttu-id="6dc67-149">包元数据 (详细信息，弃) 有时不会从 CodeSpaces 中的 nuget.org 请求 - [#10549](https://github.com/NuGet/Home/issues/10549)</span><span class="sxs-lookup"><span data-stu-id="6dc67-149">Package Metadata (details, deprecation) are sometimes not pulled from nuget.org in CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)</span></span>

* <span data-ttu-id="6dc67-150">PMUI 初始化在调试会话期间失败，异常 - [#10559](https://github.com/NuGet/Home/issues/10559)</span><span class="sxs-lookup"><span data-stu-id="6dc67-150">PMUI initialization fails with exception during debug session - [#10559](https://github.com/NuGet/Home/issues/10559)</span></span>

* <span data-ttu-id="6dc67-151">nuget 还原会导致 big endian 系统上的包完整性检查失败 - [#10567](https://github.com/NuGet/Home/issues/10567)</span><span class="sxs-lookup"><span data-stu-id="6dc67-151">nuget restore results in a package integrity check failure on big endian system - [#10567](https://github.com/NuGet/Home/issues/10567)</span></span>

* <span data-ttu-id="6dc67-152">引发 FormatException 而不是 PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)</span><span class="sxs-lookup"><span data-stu-id="6dc67-152">FormatException is thrown instead of PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)</span></span>

* <span data-ttu-id="6dc67-153">CPVM - 图形步进算法中的并发问题 - [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="6dc67-153">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>

* <span data-ttu-id="6dc67-154">添加 PMC powershell 版本遥测 - [#10609](https://github.com/NuGet/Home/issues/10609)</span><span class="sxs-lookup"><span data-stu-id="6dc67-154">Add PMC powershell version telemetry - [#10609](https://github.com/NuGet/Home/issues/10609)</span></span>

* <span data-ttu-id="6dc67-155">提高 NuGetVersion 排序性能 - [#10611](https://github.com/NuGet/Home/issues/10611)</span><span class="sxs-lookup"><span data-stu-id="6dc67-155">Improve NuGetVersion sort performance - [#10611](https://github.com/NuGet/Home/issues/10611)</span></span>

* <span data-ttu-id="6dc67-156">Trusted-signers Add 具有不一致的参数 - [#10647](https://github.com/NuGet/Home/issues/10647)</span><span class="sxs-lookup"><span data-stu-id="6dc67-156">Trusted-signers Add has inconsistent arguments - [#10647](https://github.com/NuGet/Home/issues/10647)</span></span>

* <span data-ttu-id="6dc67-157">Vs2019 v16.9.0：将 NuGet 程序包管理器中的选项卡从"更新"切换为"已安装"不会更新帧。</span><span class="sxs-lookup"><span data-stu-id="6dc67-157">Vs2019 v16.9.0: Switching tabs in NuGet Package Manager from "Updates" to "Installed" doesn't update the frame.</span></span><span data-ttu-id="6dc67-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span><span class="sxs-lookup"><span data-stu-id="6dc67-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span></span>

* <span data-ttu-id="6dc67-159">从 PMUI 中的版本号中删除"v"- [#10677](https://github.com/NuGet/Home/issues/10677)</span><span class="sxs-lookup"><span data-stu-id="6dc67-159">Remove the "v" from the version number in PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)</span></span>

* <span data-ttu-id="6dc67-160">INuGetProjectService.GetInstalledPackagesAsync 在收到 CPS 项目系统提名前引发 - [#10681](https://github.com/NuGet/Home/issues/10681)</span><span class="sxs-lookup"><span data-stu-id="6dc67-160">INuGetProjectService.GetInstalledPackagesAsync throws before receiving CPS project system nomination - [#10681](https://github.com/NuGet/Home/issues/10681)</span></span>

* <span data-ttu-id="6dc67-161">嵌入的图标会导致源"Microsoft Visual Studio脱机包"拒绝访问[-](https://github.com/NuGet/Home/issues/10687) #10687</span><span class="sxs-lookup"><span data-stu-id="6dc67-161">Embedded Icons cause Access Denied from source "Microsoft Visual Studio Offline Packages" on Browse tab - [#10687](https://github.com/NuGet/Home/issues/10687)</span></span>

* <span data-ttu-id="6dc67-162">未设置 MSBuildProjectExtensionsPath 时，INuGetProjectService.GetInstalledPackagesAsync 引发 - [#10739](https://github.com/NuGet/Home/issues/10739)</span><span class="sxs-lookup"><span data-stu-id="6dc67-162">INuGetProjectService.GetInstalledPackagesAsync throws when MSBuildProjectExtensionsPath is not set - [#10739](https://github.com/NuGet/Home/issues/10739)</span></span>

* <span data-ttu-id="6dc67-163">"dotnet nuget remove source nuget.org"第一次不起作用 - [#10745](https://github.com/NuGet/Home/issues/10745)</span><span class="sxs-lookup"><span data-stu-id="6dc67-163">"dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)</span></span>

* <span data-ttu-id="6dc67-164">Nuget 阻止异步方法中的线程池线程对 UI 线程进行同步调用 - [#10775](https://github.com/NuGet/Home/issues/10775)</span><span class="sxs-lookup"><span data-stu-id="6dc67-164">Nuget blocks a threadpool thread in an async method making a synchronous call to the UI thread - [#10775](https://github.com/NuGet/Home/issues/10775)</span></span>

* <span data-ttu-id="6dc67-165">工具 ->选项 -> NuGet 程序包管理器字符串被截断 - [#10779](https://github.com/NuGet/Home/issues/10779)</span><span class="sxs-lookup"><span data-stu-id="6dc67-165">Tools -> Options -> NuGet Package Manager string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)</span></span>

* <span data-ttu-id="6dc67-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` 是死代码并损害性能 - [#10790](https://github.com/NuGet/Home/issues/10790)</span><span class="sxs-lookup"><span data-stu-id="6dc67-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` is dead code and hurting performance - [#10790](https://github.com/NuGet/Home/issues/10790)</span></span>

* <span data-ttu-id="6dc67-167">在 NuGet SDK 包中使用嵌入式图标 - [#10795](https://github.com/NuGet/Home/issues/10795)</span><span class="sxs-lookup"><span data-stu-id="6dc67-167">Use embedded icon in NuGet SDK packages - [#10795](https://github.com/NuGet/Home/issues/10795)</span></span>

* <span data-ttu-id="6dc67-168">更新 SPDX 许可证列表 - [#10806](https://github.com/NuGet/Home/issues/10806)</span><span class="sxs-lookup"><span data-stu-id="6dc67-168">Update the SPDX license list - [#10806](https://github.com/NuGet/Home/issues/10806)</span></span>

<span data-ttu-id="6dc67-169">**[此版本中已修复的所有问题的列表 - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span><span class="sxs-lookup"><span data-stu-id="6dc67-169">**[List of all issues fixed in this release - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span></span>
  
<span data-ttu-id="6dc67-170">**[此版本中的提交列表 - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span><span class="sxs-lookup"><span data-stu-id="6dc67-170">**[List of commits in this release - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span></span>
  
### <a name="community-contributions"></a><span data-ttu-id="6dc67-171">社区参与</span><span class="sxs-lookup"><span data-stu-id="6dc67-171">Community contributions</span></span>

<span data-ttu-id="6dc67-172">感谢所有参与者，他们帮助使此 NuGet 版本变得出色！</span><span class="sxs-lookup"><span data-stu-id="6dc67-172">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="6dc67-173">谁</span><span class="sxs-lookup"><span data-stu-id="6dc67-173">Who</span></span>|<span data-ttu-id="6dc67-174">拉/拉</span><span class="sxs-lookup"><span data-stu-id="6dc67-174">PRs</span></span>|<span data-ttu-id="6dc67-175">问题</span><span class="sxs-lookup"><span data-stu-id="6dc67-175">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="6dc67-176">将</span><span class="sxs-lookup"><span data-stu-id="6dc67-176">louis-z</span></span>](https://github.com/louis-z) | [<span data-ttu-id="6dc67-177">3991</span><span class="sxs-lookup"><span data-stu-id="6dc67-177">3991</span></span>](https://github.com/NuGet/NuGet.Client/pull/3991) | <span data-ttu-id="6dc67-178">VersionRange 无法分析单位数范围 - [#10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="6dc67-178">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>
[<span data-ttu-id="6dc67-179">omajid</span><span class="sxs-lookup"><span data-stu-id="6dc67-179">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="6dc67-180">3860</span><span class="sxs-lookup"><span data-stu-id="6dc67-180">3860</span></span>](https://github.com/NuGet/NuGet.Client/pull/3860) | <span data-ttu-id="6dc67-181">NuGet.Client build.sh 中断 - [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="6dc67-181">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="6dc67-182">Nirmal4G</span><span class="sxs-lookup"><span data-stu-id="6dc67-182">Nirmal4G</span></span>](https://github.com/Nirmal4G) | [<span data-ttu-id="6dc67-183">3623</span><span class="sxs-lookup"><span data-stu-id="6dc67-183">3623</span></span>](https://github.com/NuGet/NuGet.Client/pull/3623) | <span data-ttu-id="6dc67-184">NuGet.Client build.sh 中断 - [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="6dc67-184">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="6dc67-185">BlackGad</span><span class="sxs-lookup"><span data-stu-id="6dc67-185">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="6dc67-186">3953</span><span class="sxs-lookup"><span data-stu-id="6dc67-186">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="6dc67-187">"nuget pack"的性能随源路径中的级别增加而降低 - [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="6dc67-187">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>
[<span data-ttu-id="6dc67-188">BlackGad</span><span class="sxs-lookup"><span data-stu-id="6dc67-188">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="6dc67-189">3953</span><span class="sxs-lookup"><span data-stu-id="6dc67-189">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="6dc67-190">NuGet.exe包性能问题。</span><span class="sxs-lookup"><span data-stu-id="6dc67-190">NuGet.exe pack performance problem with ..</span></span> <span data-ttu-id="6dc67-191">相对路径 - [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="6dc67-191">relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>
[<span data-ttu-id="6dc67-192">marcin-krystianc</span><span class="sxs-lookup"><span data-stu-id="6dc67-192">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="6dc67-193">3940</span><span class="sxs-lookup"><span data-stu-id="6dc67-193">3940</span></span>](https://github.com/NuGet/NuGet.Client/pull/3940) | <span data-ttu-id="6dc67-194">CPVM - 图形步进算法中的并发问题 - [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="6dc67-194">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>
[<span data-ttu-id="6dc67-195">一些</span><span class="sxs-lookup"><span data-stu-id="6dc67-195">josesimoes</span></span>](https://github.com/josesimoes) | [<span data-ttu-id="6dc67-196">3943</span><span class="sxs-lookup"><span data-stu-id="6dc67-196">3943</span></span>](https://github.com/NuGet/NuGet.Client/pull/3943) | <span data-ttu-id="6dc67-197">将项目类型 nfproj 添加到 Nuget CLI 的 supportedProjectExtensions 列表中。</span><span class="sxs-lookup"><span data-stu-id="6dc67-197">Add the project type nfproj to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="6dc67-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="6dc67-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="6dc67-199">欢迎反馈</span><span class="sxs-lookup"><span data-stu-id="6dc67-199">Feedback welcome</span></span>

<span data-ttu-id="6dc67-200">反馈对我们非常重要。</span><span class="sxs-lookup"><span data-stu-id="6dc67-200">Your feedback is important to us.</span></span>  <span data-ttu-id="6dc67-201">如果此版本有任何问题，请查看有关现有问题的 [GitHub 问题](https://github.com/NuGet/Home/issues) 和 [Visual Studio 开发人员社区](https://developercommunity.visualstudio.com/) 。</span><span class="sxs-lookup"><span data-stu-id="6dc67-201">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="6dc67-202">对于 NuGet 中的新问题，请报告 [GitHub 问题](https://github.com/NuGet/Home/issues/new)。</span><span class="sxs-lookup"><span data-stu-id="6dc67-202">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="6dc67-203">对于一般的 NuGet 体验问题，请通过 "帮助" 下的 "你喜欢的 IDE" 中的 " [报告问题](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) " 选项告知我们 **> 报告问题**。</span><span class="sxs-lookup"><span data-stu-id="6dc67-203">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
