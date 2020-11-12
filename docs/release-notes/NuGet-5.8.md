---
title: NuGet 5.8 发行说明
description: NuGet 5.8 的发行说明，包括新功能、bug 修复和 Dcr。
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 86e173b9d760578454df8f5f817533f64e193996
ms.sourcegitcommit: 0cc6ac680c3202d0b036c0bed7910f6709215682
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2020
ms.locfileid: "94550739"
---
# <a name="nuget-58-release-notes"></a><span data-ttu-id="9ccc0-103">NuGet 5.8 发行说明</span><span class="sxs-lookup"><span data-stu-id="9ccc0-103">NuGet 5.8 Release Notes</span></span>

<span data-ttu-id="9ccc0-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="9ccc0-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="9ccc0-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="9ccc0-105">NuGet version</span></span> | <span data-ttu-id="9ccc0-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="9ccc0-106">Available in Visual Studio version</span></span> | <span data-ttu-id="9ccc0-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9ccc0-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="9ccc0-108">**5.8**</span><span class="sxs-lookup"><span data-stu-id="9ccc0-108">**5.8**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="9ccc0-109">Visual Studio 2019 版本 16.8</span><span class="sxs-lookup"><span data-stu-id="9ccc0-109">Visual Studio 2019 version 16.8</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="9ccc0-110">[5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="9ccc0-110">[5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="9ccc0-111"><sup>1</sup> 与带有 .net Core 工作负载的 Visual Studio 2019 一起安装</span><span class="sxs-lookup"><span data-stu-id="9ccc0-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="9ccc0-112">Visual Studio 16.8、MSBuild 16.8 和 .NET 5.0 需要 NuGet.exe 5.8 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="9ccc0-112">Visual Studio 16.8, MSBuild 16.8, and .NET 5.0 require NuGet.exe 5.8 or later.</span></span>


## <a name="summary-whats-new-in-58"></a><span data-ttu-id="9ccc0-113">摘要：5.8 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="9ccc0-113">Summary: What's New in 5.8</span></span>
<span data-ttu-id="9ccc0-114">🎉 **这是第一个版本，用于为面向 .net 5.0 的 NuGet 包提供完整创作和还原支持** 🎉</span><span class="sxs-lookup"><span data-stu-id="9ccc0-114">🎉 **This is the first release to offer full authoring and restoring support for NuGet packages targeting .NET 5.0** 🎉</span></span>

* <span data-ttu-id="9ccc0-115">包管理器 UI 包详细信息窗格中显示包漏洞详细信息- [#9850](https://github.com/NuGet/Home/issues/9850)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-115">Display package vulnerability details in the Package Manager UI package details pane - [#9850](https://github.com/NuGet/Home/issues/9850)</span></span>

* <span data-ttu-id="9ccc0-116">用新的命令 #8051 验证已签名 [`dotnet nuget verify`](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-verify) 的[#8051](https://github.com/NuGet/Home/issues/8051) NuGet 包</span><span class="sxs-lookup"><span data-stu-id="9ccc0-116">Verify signed NuGet packages with the new [`dotnet nuget verify`](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-verify) command - [#8051](https://github.com/NuGet/Home/issues/8051)</span></span>

* <span data-ttu-id="9ccc0-117">[`dotnet add package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) 支持 `--prerelease` 添加包的最新版本的选项，其中包括预发行版本- [#4699](https://github.com/NuGet/Home/issues/4699)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-117">[`dotnet add package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) supports `--prerelease` option to add the latest version of a package, including prerelease versions - [#4699](https://github.com/NuGet/Home/issues/4699)</span></span>

* <span data-ttu-id="9ccc0-118">通过 [`nuget.exe search`](https://docs.microsoft.com/nuget/reference/cli-reference/cli-ref-search) 命令[#9704](https://github.com/NuGet/Home/issues/9704)在 CLI 中搜索包</span><span class="sxs-lookup"><span data-stu-id="9ccc0-118">Search for packages in the CLI with [`nuget.exe search`](https://docs.microsoft.com/nuget/reference/cli-reference/cli-ref-search) command - [#9704](https://github.com/NuGet/Home/issues/9704)</span></span>

* <span data-ttu-id="9ccc0-119">[`dotnet list package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-list-package) 命令支持 `--verbosity` 选项 [#9600](https://github.com/NuGet/Home/issues/9600)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-119">[`dotnet list package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-list-package) command supports `--verbosity` option - [#9600](https://github.com/NuGet/Home/issues/9600)</span></span>

* <span data-ttu-id="9ccc0-120">在 Visual Studio 中为基于 PackageReference 的 .csproj 样式的项目启用快速 No-Op 还原优化- [#9565](https://github.com/NuGet/Home/issues/9565)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-120">Enable fast No-Op restore optimization for csproj-style, PackageReference-based projects in Visual Studio - [#9565](https://github.com/NuGet/Home/issues/9565)</span></span>

* <span data-ttu-id="9ccc0-121">解决方案级包管理器 UI 操作（如包安装和更新）的速度高达10倍- [#6010](https://github.com/NuGet/Home/issues/6010)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-121">Solution level Package Manager UI operations such as package installs and updates are up to 10x faster - [#6010](https://github.com/NuGet/Home/issues/6010)</span></span>

* <span data-ttu-id="9ccc0-122">Visual Studio 中的其他几个 NuGet 性能改进- [#9982](https://github.com/NuGet/Home/issues/9982)、 [#9984](https://github.com/NuGet/Home/issues/9984)、 [#10052](https://github.com/NuGet/Home/issues/10052) [#9903](https://github.com/NuGet/Home/issues/9903)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-122">Several other NuGet performance improvements in Visual Studio - [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903)</span></span>


### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="9ccc0-123">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="9ccc0-123">Issues fixed in this release</span></span>

<span data-ttu-id="9ccc0-124">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="9ccc0-124">**DCRs:**</span></span>

* <span data-ttu-id="9ccc0-125">.NET 5.0 TFM：框架优先规则- [#9436](https://github.com/NuGet/Home/issues/9436)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-125">.NET 5.0 TFM: Framework Precedence Rules - [#9436](https://github.com/NuGet/Home/issues/9436)</span></span>

* <span data-ttu-id="9ccc0-126">分析 TargetFramework 时，NuGet 不应推断点平台版本 [#9842](https://github.com/NuGet/Home/issues/9842)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-126">NuGet should not infer dots platform version when parsing TargetFramework - [#9842](https://github.com/NuGet/Home/issues/9842)</span></span>

* <span data-ttu-id="9ccc0-127">使用 TargetFrameworkMoniker & TargetPlatformMoniker 来推断框架，而不是使用单个 TFI、TFV、TPI、TPV 属性- [#9895](https://github.com/NuGet/Home/issues/9895)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-127">Use TargetFrameworkMoniker & TargetPlatformMoniker to infer the frameworks instead of using individual TFI, TFV, TPI, TPV properties - [#9895](https://github.com/NuGet/Home/issues/9895)</span></span>

* <span data-ttu-id="9ccc0-128">更新 `GetReferenceNearestTargetFrameworkTask()` 以支持平台 (的目标框架，如 net 5.0-windows) - [#9894](https://github.com/NuGet/Home/issues/9894)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-128">Update `GetReferenceNearestTargetFrameworkTask()` to support target frameworks with platforms (such as net5.0-windows) - [#9894](https://github.com/NuGet/Home/issues/9894)</span></span>

* <span data-ttu-id="9ccc0-129">.NET 5.0 Visual Studio Api- [#9650](https://github.com/NuGet/Home/issues/9650)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-129">.NET 5.0 Visual Studio APIs - [#9650](https://github.com/NuGet/Home/issues/9650)</span></span>

* <span data-ttu-id="9ccc0-130">程序包管理器 UI：合并或更新包操作由于 (包降级等错误而不会被阻止 ) - [#9224](https://github.com/NuGet/Home/issues/9224)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-130">Package Manager UI: Consolidate or Update packages operations should not be blocked due to errors (Package Downgrade, etc.) - [#9224](https://github.com/NuGet/Home/issues/9224)</span></span>

* <span data-ttu-id="9ccc0-131">对于具有功能的项目，NuGet 功能应会亮起;"PackageReferences"- [#9957](https://github.com/NuGet/Home/issues/9957)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-131">NuGet features should light up for projects that have the capability; "PackageReferences" - [#9957](https://github.com/NuGet/Home/issues/9957)</span></span>

* <span data-ttu-id="9ccc0-132">禁止在 Visual Studio 中 No-Op 还原消息- [#6384](https://github.com/NuGet/Home/issues/6384)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-132">Suppress No-Op Restore messages in Visual Studio - [#6384](https://github.com/NuGet/Home/issues/6384)</span></span>

<span data-ttu-id="9ccc0-133">**漏洞**</span><span class="sxs-lookup"><span data-stu-id="9ccc0-133">**Bugs:**</span></span>

* <span data-ttu-id="9ccc0-134">不应在后台线程上调用 OutputWindowTextWriter 构造函数- [#9764](https://github.com/NuGet/Home/issues/9764)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-134">OutputWindowTextWriter constructor should not be called on background thread - [#9764](https://github.com/NuGet/Home/issues/9764)</span></span>

* <span data-ttu-id="9ccc0-135">在大 Endian Cpu 上还原签名包- [#9547](https://github.com/NuGet/Home/issues/9547)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-135">Restore signed packages on Big Endian CPUs - [#9547](https://github.com/NuGet/Home/issues/9547)</span></span>

* <span data-ttu-id="9ccc0-136">OutputConsoleLogger 不应调用 MEF 构造函数中的关联方法- [#9591](https://github.com/NuGet/Home/issues/9591)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-136">OutputConsoleLogger should not call affinitized methods in MEF constructors - [#9591](https://github.com/NuGet/Home/issues/9591)</span></span>

* <span data-ttu-id="9ccc0-137">NuGet 中的 Bug `PrintJustified()` 方法- [#9737](https://github.com/NuGet/Home/issues/9737)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-137">Bug in NuGet.CommandLine.Console `PrintJustified()` method - [#9737](https://github.com/NuGet/Home/issues/9737)</span></span>

* <span data-ttu-id="9ccc0-138">由于绑定错误而对包元数据进行垃圾回收时，包管理器 UI 内存泄漏 [#9757](https://github.com/NuGet/Home/issues/9757)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-138">Package Manager UI memory leak when package metadata is garbage collected due to a bad binding - [#9757](https://github.com/NuGet/Home/issues/9757)</span></span>

* <span data-ttu-id="9ccc0-139">签名使用包管理器 UI 中的 packages.config 格式安装签名包时，错误列表中未显示任何警告- [#9798](https://github.com/NuGet/Home/issues/9798)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-139">[Signing] No warning is showed in Error List when installing a signed package with packages.config format in Package Manager UI - [#9798](https://github.com/NuGet/Home/issues/9798)</span></span>

* <span data-ttu-id="9ccc0-140">XPlat 不应具有公共 Api- [#9821](https://github.com/NuGet/Home/issues/9821)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-140">NuGet.CommandLine.XPlat should not have public APIs - [#9821](https://github.com/NuGet/Home/issues/9821)</span></span>

* <span data-ttu-id="9ccc0-141">通过使用 #9822 阻止线程池线程来减少解决方案加载时的资源争用 `BlockingCollection.Take()`  -  [#9822](https://github.com/NuGet/Home/issues/9822)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-141">Reduce resource contention at Solution Load time caused by blocking a threaded-pool thread with `BlockingCollection.Take()` - [#9822](https://github.com/NuGet/Home/issues/9822)</span></span>

* <span data-ttu-id="9ccc0-142">在命令行还原中，对于多目标项目，NuGet 应从内部版本中读取与目标框架相关的信息 [#9869](https://github.com/NuGet/Home/issues/9869)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-142">In command line restore, with multi targeted projects, NuGet should read the target framework related information from the inner build - [#9869](https://github.com/NuGet/Home/issues/9869)</span></span>

* <span data-ttu-id="9ccc0-143">通过 TargetFrameworkInformation 项读取运行时标识符图形- [#9874](https://github.com/NuGet/Home/issues/9874)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-143">Read Runtime Identifier graph through TargetFrameworkInformation item - [#9874](https://github.com/NuGet/Home/issues/9874)</span></span>

* <span data-ttu-id="9ccc0-144">与 Visual Studio 和常规 MSBuild 评估还原相比，静态图形还原与 CrossTargeting 属性不一致 [#9881](https://github.com/NuGet/Home/issues/9881)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-144">Static graph restore is inconsistent with regards to CrossTargeting property in compared to Visual Studio and regular MSBuild evaluation restore - [#9881](https://github.com/NuGet/Home/issues/9881)</span></span>

* <span data-ttu-id="9ccc0-145">在静态图形还原中，对于多目标项目，NuGet 应从内部版本中读取与目标框架相关的信息。</span><span class="sxs-lookup"><span data-stu-id="9ccc0-145">In static graph restore, with multi targeted projects, NuGet should read the target framework related information from the inner build.</span></span><span data-ttu-id="9ccc0-146"> - [#9870](https://github.com/NuGet/Home/issues/9870)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-146"> - [#9870](https://github.com/NuGet/Home/issues/9870)</span></span>

* <span data-ttu-id="9ccc0-147">允许 `net5.0-platform` 在 Visual Studio 中加载和还原项目- [#9863](https://github.com/NuGet/Home/issues/9863)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-147">Allow `net5.0-platform` projects to be loaded and restored in Visual Studio - [#9863](https://github.com/NuGet/Home/issues/9863)</span></span>

* <span data-ttu-id="9ccc0-148">在包管理器 UI 中显示解析的版本- [#9826](https://github.com/NuGet/Home/issues/9826)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-148">Display the resolved version in the Package Manager UI - [#9826](https://github.com/NuGet/Home/issues/9826)</span></span>

* <span data-ttu-id="9ccc0-149">程序包管理器 UI：解决方案资源管理器未显示所有 NuGet 包依赖项- [#9898](https://github.com/NuGet/Home/issues/9898)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-149">Package Manager UI: Solution Explorer is not showing all NuGet package dependencies - [#9898](https://github.com/NuGet/Home/issues/9898)</span></span>

* <span data-ttu-id="9ccc0-150">更新 SPDX 许可证列表- [#9946](https://github.com/NuGet/Home/issues/9946)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-150">Update the SPDX license list - [#9946](https://github.com/NuGet/Home/issues/9946)</span></span>

* <span data-ttu-id="9ccc0-151">打开 "管理 NuGet 包" 后发生 VS 2019 崩溃：图标导致图像 conversio 中出现未经处理的异常- [#9696](https://github.com/NuGet/Home/issues/9696)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-151">VS 2019 crashes after opening Manage NuGet Packages: icon causes unhandled exception in image conversio - [#9696](https://github.com/NuGet/Home/issues/9696)</span></span>

* <span data-ttu-id="9ccc0-152">需要 ilmerge 来排除 Newtonsoft.Js[#9966](https://github.com/NuGet/Home/issues/9966)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-152">NuGet.Packaging.Extraction needs ilmerge to exclude Newtonsoft.Json - [#9966](https://github.com/NuGet/Home/issues/9966)</span></span>

* <span data-ttu-id="9ccc0-153">当没有错误时，具有 ContinuePackingAfterGeneratingNuspec = false 的装箱应失败- [#9786](https://github.com/NuGet/Home/issues/9786)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-153">Packing with ContinuePackingAfterGeneratingNuspec=false should not fail when there are no errors - [#9786](https://github.com/NuGet/Home/issues/9786)</span></span>

* <span data-ttu-id="9ccc0-154">程序包管理器 UI：图标不能正确地反转颜色- [#10017](https://github.com/NuGet/Home/issues/10017)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-154">Package Manager UI: Icons aren't inverting colors properly - [#10017](https://github.com/NuGet/Home/issues/10017)</span></span>

* <span data-ttu-id="9ccc0-155">还原时最新项目和 No-Op 项目的项目计数不正确- [#10026](https://github.com/NuGet/Home/issues/10026)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-155">Incorrect project counts for Up-To-Date and No-Op projects at Restore - [#10026](https://github.com/NuGet/Home/issues/10026)</span></span>

* <span data-ttu-id="9ccc0-156">使用 `/p:RestoreUseStaticGraphEvaluation=true` 值中的结果不能为 Null- [#9280](https://github.com/NuGet/Home/issues/9280)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-156">Using `/p:RestoreUseStaticGraphEvaluation=true` Results in Value Cannot Be Null - [#9280](https://github.com/NuGet/Home/issues/9280)</span></span>

* <span data-ttu-id="9ccc0-157">`dotnet pack` 错误地将 alias 用于 WPF 库项目- [#10020](https://github.com/NuGet/Home/issues/10020)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-157">`dotnet pack` mistakenly uses alias for WPF Library projects - [#10020](https://github.com/NuGet/Home/issues/10020)</span></span>

* <span data-ttu-id="9ccc0-158">程序包管理器 UI：签名验证失败时的 NullReferenceException- [#10042](https://github.com/NuGet/Home/issues/10042)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-158">Package Manager UI: NullReferenceException when signature validation fails - [#10042](https://github.com/NuGet/Home/issues/10042)</span></span>

* <span data-ttu-id="9ccc0-159">Codespaces：不使用 `object` 项目元数据值的类型- [#10055](https://github.com/NuGet/Home/issues/10055)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-159">Codespaces: do not use `object` type for project metadata values  - [#10055](https://github.com/NuGet/Home/issues/10055)</span></span>

* <span data-ttu-id="9ccc0-160">Codespaces：在 "工具选项" 中保存包源将覆盖凭据- [#9711](https://github.com/NuGet/Home/issues/9711)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-160">Codespaces: saving package sources in tools options will overwrite credentials - [#9711](https://github.com/NuGet/Home/issues/9711)</span></span>


<span data-ttu-id="9ccc0-161">**[此版本中已修复的所有问题的列表-5。8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**</span><span class="sxs-lookup"><span data-stu-id="9ccc0-161">**[List of all issues fixed in this release - 5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**</span></span>

<span data-ttu-id="9ccc0-162">**[此版本中已修复的问题/提交列表-5。8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**</span><span class="sxs-lookup"><span data-stu-id="9ccc0-162">**[List of issues/commits fixed in this release - 5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**</span></span>

### <a name="community-contributions"></a><span data-ttu-id="9ccc0-163">社区参与</span><span class="sxs-lookup"><span data-stu-id="9ccc0-163">Community contributions</span></span>

<span data-ttu-id="9ccc0-164">感谢所有有助于使此 NuGet 版本非常出色的参与者！</span><span class="sxs-lookup"><span data-stu-id="9ccc0-164">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="9ccc0-165">谁</span><span class="sxs-lookup"><span data-stu-id="9ccc0-165">Who</span></span>|<span data-ttu-id="9ccc0-166">Pr</span><span class="sxs-lookup"><span data-stu-id="9ccc0-166">PRs</span></span>|<span data-ttu-id="9ccc0-167">问题</span><span class="sxs-lookup"><span data-stu-id="9ccc0-167">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="9ccc0-168">omajid</span><span class="sxs-lookup"><span data-stu-id="9ccc0-168">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="9ccc0-169">3437</span><span class="sxs-lookup"><span data-stu-id="9ccc0-169">3437</span></span>](https://github.com/NuGet/NuGet.Client/pull/3437) | <span data-ttu-id="9ccc0-170">错误消息中有拼写错误。</span><span class="sxs-lookup"><span data-stu-id="9ccc0-170">Typo in error message.</span></span> <span data-ttu-id="9ccc0-171">"管理员" 而不是 "administrator"- [#9662](https://github.com/NuGet/Home/issues/9662)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-171">"administator" instead of "administrator" - [#9662](https://github.com/NuGet/Home/issues/9662)</span></span>
[<span data-ttu-id="9ccc0-172">odalet</span><span class="sxs-lookup"><span data-stu-id="9ccc0-172">odalet</span></span>](https://github.com/odalet) | [<span data-ttu-id="9ccc0-173">3341</span><span class="sxs-lookup"><span data-stu-id="9ccc0-173">3341</span></span>](https://github.com/NuGet/NuGet.Client/pull/3341) | <span data-ttu-id="9ccc0-174">具有无效 AssemblyInformationalVersion 报表的 NuGet 包 "说明是必需的"- [#5548](https://github.com/NuGet/Home/issues/5548)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-174">NuGet Pack with invalid AssemblyInformationalVersion reports "description is required" - [#5548](https://github.com/NuGet/Home/issues/5548)</span></span>
[<span data-ttu-id="9ccc0-175">campersau</span><span class="sxs-lookup"><span data-stu-id="9ccc0-175">campersau</span></span>](https://github.com/campersau) | [<span data-ttu-id="9ccc0-176">3501</span><span class="sxs-lookup"><span data-stu-id="9ccc0-176">3501</span></span>](https://github.com/NuGet/NuGet.Client/pull/3501) | <span data-ttu-id="9ccc0-177">`RepositoryMetadata.Equals()` 不考虑分支和提交属性- [#9613](https://github.com/NuGet/Home/issues/9613)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-177">`RepositoryMetadata.Equals()` does not account for Branch and Commit properties - [#9613](https://github.com/NuGet/Home/issues/9613)</span></span>
[<span data-ttu-id="9ccc0-178">Youssef1313</span><span class="sxs-lookup"><span data-stu-id="9ccc0-178">Youssef1313</span></span>](https://github.com/Youssef1313) | [<span data-ttu-id="9ccc0-179">3599</span><span class="sxs-lookup"><span data-stu-id="9ccc0-179">3599</span></span>](https://github.com/NuGet/NuGet.Client/pull/3599) | <span data-ttu-id="9ccc0-180">单击 "Visual Studio 中的" "代码" 错误列表窗口应会转向 https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-180">Clicking NU code in Visual Studio Error List window should go to https://docs.microsoft.com/nuget/reference/errors-and-warnings/ - [#9934](https://github.com/NuGet/Home/issues/9934)</span></span>
[<span data-ttu-id="9ccc0-181">ChrisMaddock</span><span class="sxs-lookup"><span data-stu-id="9ccc0-181">ChrisMaddock</span></span>](https://github.com/ChrisMaddock) | [<span data-ttu-id="9ccc0-182">3624</span><span class="sxs-lookup"><span data-stu-id="9ccc0-182">3624</span></span>](https://github.com/NuGet/NuGet.Client/pull/3624) | <span data-ttu-id="9ccc0-183">通过 Visual Studio 选项添加新包源时使用 "https://"- [#9974](https://github.com/NuGet/Home/issues/9974)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-183">Use 'https://' when adding new package source through Visual Studio options - [#9974](https://github.com/NuGet/Home/issues/9974)</span></span>
[<span data-ttu-id="9ccc0-184">Therzok</span><span class="sxs-lookup"><span data-stu-id="9ccc0-184">Therzok</span></span>](https://github.com/Therzok) | [<span data-ttu-id="9ccc0-185">3636</span><span class="sxs-lookup"><span data-stu-id="9ccc0-185">3636</span></span>](https://github.com/NuGet/NuGet.Client/pull/3636) | <span data-ttu-id="9ccc0-186">`RuntimeEnvironmentHelper.IsRunningOnVisualStudio`Mono [#9989](https://github.com/NuGet/Home/issues/9989)上的性能问题</span><span class="sxs-lookup"><span data-stu-id="9ccc0-186">`RuntimeEnvironmentHelper.IsRunningOnVisualStudio` performance issue on Mono - [#9989](https://github.com/NuGet/Home/issues/9989)</span></span>
[<span data-ttu-id="9ccc0-187">thomaslevesque</span><span class="sxs-lookup"><span data-stu-id="9ccc0-187">thomaslevesque</span></span>](https://github.com/thomaslevesque) | [<span data-ttu-id="9ccc0-188">3442</span><span class="sxs-lookup"><span data-stu-id="9ccc0-188">3442</span></span>](https://github.com/NuGet/NuGet.Client/pull/3442) | <span data-ttu-id="9ccc0-189">为 SemanticVersion 类添加 TypeConverter- [#9125](https://github.com/NuGet/Home/issues/9125)</span><span class="sxs-lookup"><span data-stu-id="9ccc0-189">Add a TypeConverter for the SemanticVersion class - [#9125](https://github.com/NuGet/Home/issues/9125)</span></span>


## <a name="feedback-welcome"></a><span data-ttu-id="9ccc0-190">欢迎反馈</span><span class="sxs-lookup"><span data-stu-id="9ccc0-190">Feedback welcome</span></span>

<span data-ttu-id="9ccc0-191">反馈对我们非常重要。</span><span class="sxs-lookup"><span data-stu-id="9ccc0-191">Your feedback is important to us.</span></span>  <span data-ttu-id="9ccc0-192">如果此版本有任何问题，请查看有关现有问题的 [GitHub 问题](https://github.com/NuGet/Home/issues) 和 [Visual Studio 开发人员社区](https://developercommunity.visualstudio.com/) 。</span><span class="sxs-lookup"><span data-stu-id="9ccc0-192">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="9ccc0-193">对于 NuGet 中的新问题，请报告 [GitHub 问题](hhttps://github.com/NuGet/Home/issues/new)。</span><span class="sxs-lookup"><span data-stu-id="9ccc0-193">For new issues within NuGet, please report a [GitHub Issue](hhttps://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="9ccc0-194">对于一般的 NuGet 体验问题，请通过 "帮助" 下的 "你喜欢的 IDE" 中的 " [报告问题](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio) " 选项告知我们 **> 报告问题** 。</span><span class="sxs-lookup"><span data-stu-id="9ccc0-194">For general NuGet experience issues, let us know via the [Report a Problem](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>