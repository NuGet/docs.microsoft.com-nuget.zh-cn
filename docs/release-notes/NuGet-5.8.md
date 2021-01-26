---
title: NuGet 5.8 发行说明
description: NuGet 5.8 的发行说明，包括新功能、bug 修复和 Dcr。
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 550971d77ed4b15129fdc58fef95e0cceda8d8d1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776172"
---
# <a name="nuget-58-release-notes"></a><span data-ttu-id="ad4b3-103">NuGet 5.8 发行说明</span><span class="sxs-lookup"><span data-stu-id="ad4b3-103">NuGet 5.8 Release Notes</span></span>

<span data-ttu-id="ad4b3-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="ad4b3-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="ad4b3-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="ad4b3-105">NuGet version</span></span> | <span data-ttu-id="ad4b3-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="ad4b3-106">Available in Visual Studio version</span></span> | <span data-ttu-id="ad4b3-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ad4b3-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="ad4b3-108">**5.8**</span><span class="sxs-lookup"><span data-stu-id="ad4b3-108">**5.8**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="ad4b3-109">Visual Studio 2019 版本 16.8</span><span class="sxs-lookup"><span data-stu-id="ad4b3-109">Visual Studio 2019 version 16.8</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="ad4b3-110">[5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="ad4b3-110">[5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |
| [<span data-ttu-id="ad4b3-111">**5.8.1**</span><span class="sxs-lookup"><span data-stu-id="ad4b3-111">**5.8.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="ad4b3-112">Visual Studio 2019 版本16.8。4</span><span class="sxs-lookup"><span data-stu-id="ad4b3-112">Visual Studio 2019 version 16.8.4</span></span>](https://visualstudio.microsoft.com/downloads/) | |

<span data-ttu-id="ad4b3-113"><sup>1</sup> 与带有 .net Core 工作负载的 Visual Studio 2019 一起安装</span><span class="sxs-lookup"><span data-stu-id="ad4b3-113"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="ad4b3-114">Visual Studio 16.8、MSBuild 16.8 和 .NET 5.0 需要 NuGet.exe 5.8 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="ad4b3-114">Visual Studio 16.8, MSBuild 16.8, and .NET 5.0 require NuGet.exe 5.8 or later.</span></span>


## <a name="summary-whats-new-in-58"></a><span data-ttu-id="ad4b3-115">摘要：5.8 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="ad4b3-115">Summary: What's New in 5.8</span></span>
<span data-ttu-id="ad4b3-116">🎉 **这是第一个版本，用于为面向 .net 5.0 的 NuGet 包提供完整创作和还原支持** 🎉</span><span class="sxs-lookup"><span data-stu-id="ad4b3-116">🎉 **This is the first release to offer full authoring and restoring support for NuGet packages targeting .NET 5.0** 🎉</span></span>

* <span data-ttu-id="ad4b3-117">使用 mmap/ [#9807](https://github.com/NuGet/Home/issues/9807) CreateFileMapping 提高 nupkg 提取速度</span><span class="sxs-lookup"><span data-stu-id="ad4b3-117">Speed up nupkg extraction using mmap/CreateFileMapping - [#9807](https://github.com/NuGet/Home/issues/9807)</span></span>

* <span data-ttu-id="ad4b3-118">包管理器 UI 包详细信息窗格中显示包漏洞详细信息- [#9850](https://github.com/NuGet/Home/issues/9850)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-118">Display package vulnerability details in the Package Manager UI package details pane - [#9850](https://github.com/NuGet/Home/issues/9850)</span></span>

* <span data-ttu-id="ad4b3-119">用新的命令 #8051 验证已签名 [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) 的[](https://github.com/NuGet/Home/issues/8051) NuGet 包</span><span class="sxs-lookup"><span data-stu-id="ad4b3-119">Verify signed NuGet packages with the new [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) command - [#8051](https://github.com/NuGet/Home/issues/8051)</span></span>

* <span data-ttu-id="ad4b3-120">[`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) 支持 `--prerelease` 添加包的最新版本的选项，其中包括预发行版本- [#4699](https://github.com/NuGet/Home/issues/4699)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-120">[`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) supports `--prerelease` option to add the latest version of a package, including prerelease versions - [#4699](https://github.com/NuGet/Home/issues/4699)</span></span>

* <span data-ttu-id="ad4b3-121">通过 [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) 命令[#9704](https://github.com/NuGet/Home/issues/9704)在 CLI 中搜索包</span><span class="sxs-lookup"><span data-stu-id="ad4b3-121">Search for packages in the CLI with [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) command - [#9704](https://github.com/NuGet/Home/issues/9704)</span></span>

* <span data-ttu-id="ad4b3-122">[`dotnet list package`](/dotnet/core/tools/dotnet-list-package) 命令支持 `--verbosity` 选项 [#9600](https://github.com/NuGet/Home/issues/9600)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-122">[`dotnet list package`](/dotnet/core/tools/dotnet-list-package) command supports `--verbosity` option - [#9600](https://github.com/NuGet/Home/issues/9600)</span></span>

* <span data-ttu-id="ad4b3-123">在 Visual Studio 中为基于 PackageReference 的 .csproj 样式的项目启用快速 No-Op 还原优化- [#9565](https://github.com/NuGet/Home/issues/9565)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-123">Enable fast No-Op restore optimization for csproj-style, PackageReference-based projects in Visual Studio - [#9565](https://github.com/NuGet/Home/issues/9565)</span></span>

* <span data-ttu-id="ad4b3-124">解决方案级包管理器 UI 操作（如包安装和更新）的速度高达10倍- [#6010](https://github.com/NuGet/Home/issues/6010)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-124">Solution level Package Manager UI operations such as package installs and updates are up to 10x faster - [#6010](https://github.com/NuGet/Home/issues/6010)</span></span>

* <span data-ttu-id="ad4b3-125">Visual Studio 中的其他几个 NuGet 性能改进- [#9982](https://github.com/NuGet/Home/issues/9982)、 [#9984](https://github.com/NuGet/Home/issues/9984)、 [#10052](https://github.com/NuGet/Home/issues/10052) [#9903](https://github.com/NuGet/Home/issues/9903)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-125">Several other NuGet performance improvements in Visual Studio - [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903)</span></span>


### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ad4b3-126">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="ad4b3-126">Issues fixed in this release</span></span>

<span data-ttu-id="ad4b3-127">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="ad4b3-127">**DCRs:**</span></span>

* <span data-ttu-id="ad4b3-128">.NET 5.0 TFM：框架优先规则- [#9436](https://github.com/NuGet/Home/issues/9436)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-128">.NET 5.0 TFM: Framework Precedence Rules - [#9436](https://github.com/NuGet/Home/issues/9436)</span></span>

* <span data-ttu-id="ad4b3-129">分析 TargetFramework 时，NuGet 不应推断点平台版本 [#9842](https://github.com/NuGet/Home/issues/9842)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-129">NuGet should not infer dots platform version when parsing TargetFramework - [#9842](https://github.com/NuGet/Home/issues/9842)</span></span>

* <span data-ttu-id="ad4b3-130">使用 TargetFrameworkMoniker & TargetPlatformMoniker 来推断框架，而不是使用单个 TFI、TFV、TPI、TPV 属性- [#9895](https://github.com/NuGet/Home/issues/9895)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-130">Use TargetFrameworkMoniker & TargetPlatformMoniker to infer the frameworks instead of using individual TFI, TFV, TPI, TPV properties - [#9895](https://github.com/NuGet/Home/issues/9895)</span></span>

* <span data-ttu-id="ad4b3-131">更新 `GetReferenceNearestTargetFrameworkTask()` 以支持平台 (的目标框架，如 net 5.0-windows) - [#9894](https://github.com/NuGet/Home/issues/9894)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-131">Update `GetReferenceNearestTargetFrameworkTask()` to support target frameworks with platforms (such as net5.0-windows) - [#9894](https://github.com/NuGet/Home/issues/9894)</span></span>

* <span data-ttu-id="ad4b3-132">.NET 5.0 Visual Studio Api- [#9650](https://github.com/NuGet/Home/issues/9650)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-132">.NET 5.0 Visual Studio APIs - [#9650](https://github.com/NuGet/Home/issues/9650)</span></span>

* <span data-ttu-id="ad4b3-133">程序包管理器 UI：合并或更新包操作由于 (包降级等错误而不会被阻止 ) - [#9224](https://github.com/NuGet/Home/issues/9224)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-133">Package Manager UI: Consolidate or Update packages operations should not be blocked due to errors (Package Downgrade, etc.) - [#9224](https://github.com/NuGet/Home/issues/9224)</span></span>

* <span data-ttu-id="ad4b3-134">对于具有功能的项目，NuGet 功能应会亮起;"PackageReferences"- [#9957](https://github.com/NuGet/Home/issues/9957)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-134">NuGet features should light up for projects that have the capability; "PackageReferences" - [#9957](https://github.com/NuGet/Home/issues/9957)</span></span>

* <span data-ttu-id="ad4b3-135">禁止在 Visual Studio 中 No-Op 还原消息- [#6384](https://github.com/NuGet/Home/issues/6384)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-135">Suppress No-Op Restore messages in Visual Studio - [#6384](https://github.com/NuGet/Home/issues/6384)</span></span>

<span data-ttu-id="ad4b3-136">**漏洞**</span><span class="sxs-lookup"><span data-stu-id="ad4b3-136">**Bugs:**</span></span>

* <span data-ttu-id="ad4b3-137">不应在后台线程上调用 OutputWindowTextWriter 构造函数- [#9764](https://github.com/NuGet/Home/issues/9764)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-137">OutputWindowTextWriter constructor should not be called on background thread - [#9764](https://github.com/NuGet/Home/issues/9764)</span></span>

* <span data-ttu-id="ad4b3-138">在大 Endian Cpu 上还原签名包- [#9547](https://github.com/NuGet/Home/issues/9547)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-138">Restore signed packages on Big Endian CPUs - [#9547](https://github.com/NuGet/Home/issues/9547)</span></span>

* <span data-ttu-id="ad4b3-139">OutputConsoleLogger 不应调用 MEF 构造函数中的关联方法- [#9591](https://github.com/NuGet/Home/issues/9591)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-139">OutputConsoleLogger should not call affinitized methods in MEF constructors - [#9591](https://github.com/NuGet/Home/issues/9591)</span></span>

* <span data-ttu-id="ad4b3-140">NuGet 中的 Bug `PrintJustified()` 方法- [#9737](https://github.com/NuGet/Home/issues/9737)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-140">Bug in NuGet.CommandLine.Console `PrintJustified()` method - [#9737](https://github.com/NuGet/Home/issues/9737)</span></span>

* <span data-ttu-id="ad4b3-141">由于绑定错误而对包元数据进行垃圾回收时，包管理器 UI 内存泄漏 [#9757](https://github.com/NuGet/Home/issues/9757)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-141">Package Manager UI memory leak when package metadata is garbage collected due to a bad binding - [#9757](https://github.com/NuGet/Home/issues/9757)</span></span>

* <span data-ttu-id="ad4b3-142">签名使用包管理器 UI 中的 packages.config 格式安装签名包时，错误列表中未显示任何警告- [#9798](https://github.com/NuGet/Home/issues/9798)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-142">[Signing] No warning is showed in Error List when installing a signed package with packages.config format in Package Manager UI - [#9798](https://github.com/NuGet/Home/issues/9798)</span></span>

* <span data-ttu-id="ad4b3-143">XPlat 不应具有公共 Api- [#9821](https://github.com/NuGet/Home/issues/9821)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-143">NuGet.CommandLine.XPlat should not have public APIs - [#9821](https://github.com/NuGet/Home/issues/9821)</span></span>

* <span data-ttu-id="ad4b3-144">通过使用 #9822 阻止线程池线程来减少解决方案加载时的资源争用 `BlockingCollection.Take()`  -  [](https://github.com/NuGet/Home/issues/9822)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-144">Reduce resource contention at Solution Load time caused by blocking a threaded-pool thread with `BlockingCollection.Take()` - [#9822](https://github.com/NuGet/Home/issues/9822)</span></span>

* <span data-ttu-id="ad4b3-145">在命令行还原中，对于多目标项目，NuGet 应从内部版本中读取与目标框架相关的信息 [#9869](https://github.com/NuGet/Home/issues/9869)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-145">In command line restore, with multi targeted projects, NuGet should read the target framework related information from the inner build - [#9869](https://github.com/NuGet/Home/issues/9869)</span></span>

* <span data-ttu-id="ad4b3-146">通过 TargetFrameworkInformation 项读取运行时标识符图形- [#9874](https://github.com/NuGet/Home/issues/9874)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-146">Read Runtime Identifier graph through TargetFrameworkInformation item - [#9874](https://github.com/NuGet/Home/issues/9874)</span></span>

* <span data-ttu-id="ad4b3-147">与 Visual Studio 和常规 MSBuild 评估还原相比，静态图形还原与 CrossTargeting 属性不一致 [#9881](https://github.com/NuGet/Home/issues/9881)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-147">Static graph restore is inconsistent with regards to CrossTargeting property in compared to Visual Studio and regular MSBuild evaluation restore - [#9881](https://github.com/NuGet/Home/issues/9881)</span></span>

* <span data-ttu-id="ad4b3-148">在静态图形还原中，对于多目标项目，NuGet 应从内部版本中读取与目标框架相关的信息。</span><span class="sxs-lookup"><span data-stu-id="ad4b3-148">In static graph restore, with multi targeted projects, NuGet should read the target framework related information from the inner build.</span></span><span data-ttu-id="ad4b3-149"> - [#9870](https://github.com/NuGet/Home/issues/9870)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-149"> - [#9870](https://github.com/NuGet/Home/issues/9870)</span></span>

* <span data-ttu-id="ad4b3-150">允许 `net5.0-platform` 在 Visual Studio 中加载和还原项目- [#9863](https://github.com/NuGet/Home/issues/9863)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-150">Allow `net5.0-platform` projects to be loaded and restored in Visual Studio - [#9863](https://github.com/NuGet/Home/issues/9863)</span></span>

* <span data-ttu-id="ad4b3-151">在包管理器 UI 中显示解析的版本- [#9826](https://github.com/NuGet/Home/issues/9826)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-151">Display the resolved version in the Package Manager UI - [#9826](https://github.com/NuGet/Home/issues/9826)</span></span>

* <span data-ttu-id="ad4b3-152">程序包管理器 UI：解决方案资源管理器未显示所有 NuGet 包依赖项- [#9898](https://github.com/NuGet/Home/issues/9898)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-152">Package Manager UI: Solution Explorer is not showing all NuGet package dependencies - [#9898](https://github.com/NuGet/Home/issues/9898)</span></span>

* <span data-ttu-id="ad4b3-153">更新 SPDX 许可证列表- [#9946](https://github.com/NuGet/Home/issues/9946)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-153">Update the SPDX license list - [#9946](https://github.com/NuGet/Home/issues/9946)</span></span>

* <span data-ttu-id="ad4b3-154">打开 "管理 NuGet 包" 后发生 VS 2019 崩溃：图标导致图像 conversio 中出现未经处理的异常- [#9696](https://github.com/NuGet/Home/issues/9696)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-154">VS 2019 crashes after opening Manage NuGet Packages: icon causes unhandled exception in image conversio - [#9696](https://github.com/NuGet/Home/issues/9696)</span></span>

* <span data-ttu-id="ad4b3-155">需要 ilmerge 来排除 Newtonsoft.Js[#9966](https://github.com/NuGet/Home/issues/9966)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-155">NuGet.Packaging.Extraction needs ilmerge to exclude Newtonsoft.Json - [#9966](https://github.com/NuGet/Home/issues/9966)</span></span>

* <span data-ttu-id="ad4b3-156">当没有错误时，具有 ContinuePackingAfterGeneratingNuspec = false 的装箱应失败- [#9786](https://github.com/NuGet/Home/issues/9786)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-156">Packing with ContinuePackingAfterGeneratingNuspec=false should not fail when there are no errors - [#9786](https://github.com/NuGet/Home/issues/9786)</span></span>

* <span data-ttu-id="ad4b3-157">程序包管理器 UI：图标不能正确地反转颜色- [#10017](https://github.com/NuGet/Home/issues/10017)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-157">Package Manager UI: Icons aren't inverting colors properly - [#10017](https://github.com/NuGet/Home/issues/10017)</span></span>

* <span data-ttu-id="ad4b3-158">还原时最新项目和 No-Op 项目的项目计数不正确- [#10026](https://github.com/NuGet/Home/issues/10026)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-158">Incorrect project counts for Up-To-Date and No-Op projects at Restore - [#10026](https://github.com/NuGet/Home/issues/10026)</span></span>

* <span data-ttu-id="ad4b3-159">使用 `/p:RestoreUseStaticGraphEvaluation=true` 值中的结果不能为 Null- [#9280](https://github.com/NuGet/Home/issues/9280)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-159">Using `/p:RestoreUseStaticGraphEvaluation=true` Results in Value Cannot Be Null - [#9280](https://github.com/NuGet/Home/issues/9280)</span></span>

* <span data-ttu-id="ad4b3-160">`dotnet pack` 错误地将 alias 用于 WPF 库项目- [#10020](https://github.com/NuGet/Home/issues/10020)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-160">`dotnet pack` mistakenly uses alias for WPF Library projects - [#10020](https://github.com/NuGet/Home/issues/10020)</span></span>

* <span data-ttu-id="ad4b3-161">程序包管理器 UI：签名验证失败时的 NullReferenceException- [#10042](https://github.com/NuGet/Home/issues/10042)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-161">Package Manager UI: NullReferenceException when signature validation fails - [#10042](https://github.com/NuGet/Home/issues/10042)</span></span>

* <span data-ttu-id="ad4b3-162">Codespaces：不使用 `object` 项目元数据值的类型- [#10055](https://github.com/NuGet/Home/issues/10055)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-162">Codespaces: do not use `object` type for project metadata values  - [#10055](https://github.com/NuGet/Home/issues/10055)</span></span>

* <span data-ttu-id="ad4b3-163">Codespaces：在 "工具选项" 中保存包源将覆盖凭据- [#9711](https://github.com/NuGet/Home/issues/9711)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-163">Codespaces: saving package sources in tools options will overwrite credentials - [#9711](https://github.com/NuGet/Home/issues/9711)</span></span>


<span data-ttu-id="ad4b3-164">**[此版本中已修复的所有问题的列表-5。8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**</span><span class="sxs-lookup"><span data-stu-id="ad4b3-164">**[List of all issues fixed in this release - 5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**</span></span>

<span data-ttu-id="ad4b3-165">**[此版本中的问题列表-5。8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**</span><span class="sxs-lookup"><span data-stu-id="ad4b3-165">**[List of issues in this release - 5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**</span></span>

### <a name="community-contributions"></a><span data-ttu-id="ad4b3-166">社区参与</span><span class="sxs-lookup"><span data-stu-id="ad4b3-166">Community contributions</span></span>

<span data-ttu-id="ad4b3-167">感谢所有有助于使此 NuGet 版本非常出色的参与者！</span><span class="sxs-lookup"><span data-stu-id="ad4b3-167">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="ad4b3-168">谁</span><span class="sxs-lookup"><span data-stu-id="ad4b3-168">Who</span></span>|<span data-ttu-id="ad4b3-169">Pr</span><span class="sxs-lookup"><span data-stu-id="ad4b3-169">PRs</span></span>|<span data-ttu-id="ad4b3-170">问题</span><span class="sxs-lookup"><span data-stu-id="ad4b3-170">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="ad4b3-171">omajid</span><span class="sxs-lookup"><span data-stu-id="ad4b3-171">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="ad4b3-172">3437</span><span class="sxs-lookup"><span data-stu-id="ad4b3-172">3437</span></span>](https://github.com/NuGet/NuGet.Client/pull/3437) | <span data-ttu-id="ad4b3-173">错误消息中有拼写错误。</span><span class="sxs-lookup"><span data-stu-id="ad4b3-173">Typo in error message.</span></span> <span data-ttu-id="ad4b3-174">"管理员" 而不是 "administrator"- [#9662](https://github.com/NuGet/Home/issues/9662)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-174">"administator" instead of "administrator" - [#9662](https://github.com/NuGet/Home/issues/9662)</span></span>
[<span data-ttu-id="ad4b3-175">odalet</span><span class="sxs-lookup"><span data-stu-id="ad4b3-175">odalet</span></span>](https://github.com/odalet) | [<span data-ttu-id="ad4b3-176">3341</span><span class="sxs-lookup"><span data-stu-id="ad4b3-176">3341</span></span>](https://github.com/NuGet/NuGet.Client/pull/3341) | <span data-ttu-id="ad4b3-177">具有无效 AssemblyInformationalVersion 报表的 NuGet 包 "说明是必需的"- [#5548](https://github.com/NuGet/Home/issues/5548)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-177">NuGet Pack with invalid AssemblyInformationalVersion reports "description is required" - [#5548](https://github.com/NuGet/Home/issues/5548)</span></span>
[<span data-ttu-id="ad4b3-178">campersau</span><span class="sxs-lookup"><span data-stu-id="ad4b3-178">campersau</span></span>](https://github.com/campersau) | [<span data-ttu-id="ad4b3-179">3501</span><span class="sxs-lookup"><span data-stu-id="ad4b3-179">3501</span></span>](https://github.com/NuGet/NuGet.Client/pull/3501) | <span data-ttu-id="ad4b3-180">`RepositoryMetadata.Equals()` 不考虑分支和提交属性- [#9613](https://github.com/NuGet/Home/issues/9613)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-180">`RepositoryMetadata.Equals()` does not account for Branch and Commit properties - [#9613](https://github.com/NuGet/Home/issues/9613)</span></span>
[<span data-ttu-id="ad4b3-181">Youssef1313</span><span class="sxs-lookup"><span data-stu-id="ad4b3-181">Youssef1313</span></span>](https://github.com/Youssef1313) | [<span data-ttu-id="ad4b3-182">3599</span><span class="sxs-lookup"><span data-stu-id="ad4b3-182">3599</span></span>](https://github.com/NuGet/NuGet.Client/pull/3599) | <span data-ttu-id="ad4b3-183">单击 "Visual Studio 中的" "代码" 错误列表窗口应会转向 https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-183">Clicking NU code in Visual Studio Error List window should go to https://docs.microsoft.com/nuget/reference/errors-and-warnings/ - [#9934](https://github.com/NuGet/Home/issues/9934)</span></span>
[<span data-ttu-id="ad4b3-184">ChrisMaddock</span><span class="sxs-lookup"><span data-stu-id="ad4b3-184">ChrisMaddock</span></span>](https://github.com/ChrisMaddock) | [<span data-ttu-id="ad4b3-185">3624</span><span class="sxs-lookup"><span data-stu-id="ad4b3-185">3624</span></span>](https://github.com/NuGet/NuGet.Client/pull/3624) | <span data-ttu-id="ad4b3-186">通过 Visual Studio 选项添加新包源时使用 "https://"- [#9974](https://github.com/NuGet/Home/issues/9974)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-186">Use 'https://' when adding new package source through Visual Studio options - [#9974](https://github.com/NuGet/Home/issues/9974)</span></span>
[<span data-ttu-id="ad4b3-187">Therzok</span><span class="sxs-lookup"><span data-stu-id="ad4b3-187">Therzok</span></span>](https://github.com/Therzok) | [<span data-ttu-id="ad4b3-188">3636</span><span class="sxs-lookup"><span data-stu-id="ad4b3-188">3636</span></span>](https://github.com/NuGet/NuGet.Client/pull/3636) | <span data-ttu-id="ad4b3-189">`RuntimeEnvironmentHelper.IsRunningOnVisualStudio`Mono [#9989](https://github.com/NuGet/Home/issues/9989)上的性能问题</span><span class="sxs-lookup"><span data-stu-id="ad4b3-189">`RuntimeEnvironmentHelper.IsRunningOnVisualStudio` performance issue on Mono - [#9989](https://github.com/NuGet/Home/issues/9989)</span></span>
[<span data-ttu-id="ad4b3-190">thomaslevesque</span><span class="sxs-lookup"><span data-stu-id="ad4b3-190">thomaslevesque</span></span>](https://github.com/thomaslevesque) | [<span data-ttu-id="ad4b3-191">3442</span><span class="sxs-lookup"><span data-stu-id="ad4b3-191">3442</span></span>](https://github.com/NuGet/NuGet.Client/pull/3442) | <span data-ttu-id="ad4b3-192">为 SemanticVersion 类添加 TypeConverter- [#9125](https://github.com/NuGet/Home/issues/9125)</span><span class="sxs-lookup"><span data-stu-id="ad4b3-192">Add a TypeConverter for the SemanticVersion class - [#9125](https://github.com/NuGet/Home/issues/9125)</span></span>

## <a name="summary-whats-new-in-581"></a><span data-ttu-id="ad4b3-193">摘要：5.8.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="ad4b3-193">Summary: What's New in 5.8.1</span></span>

* <span data-ttu-id="ad4b3-194">packages.config package.lock.js在 5.8- [#10257](https://github.com/NuGet/Home/issues/10257)中使用了错误的目标框架</span><span class="sxs-lookup"><span data-stu-id="ad4b3-194">packages.config package.lock.json uses an incorrect target framework in 5.8 - [#10257](https://github.com/NuGet/Home/issues/10257)</span></span>

* <span data-ttu-id="ad4b3-195">当混合 PackageReference 和 packages.config [#10326](https://github.com/NuGet/Home/issues/10326)时，5.8 + 16.8 无法解析可传递项目依赖项</span><span class="sxs-lookup"><span data-stu-id="ad4b3-195">5.8 + 16.8 Cannot resolve transitive project dependencies when mixing PackageReference and packages.config - [#10326](https://github.com/NuGet/Home/issues/10326)</span></span>

<span data-ttu-id="ad4b3-196">**[此版本中已修复的所有问题的列表-5.8。1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**</span><span class="sxs-lookup"><span data-stu-id="ad4b3-196">**[List of all issues fixed in this release - 5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**</span></span>

<span data-ttu-id="ad4b3-197">**[此版本中的提交列表-5.8。1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**</span><span class="sxs-lookup"><span data-stu-id="ad4b3-197">**[List of commits in this release - 5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="ad4b3-198">欢迎反馈</span><span class="sxs-lookup"><span data-stu-id="ad4b3-198">Feedback welcome</span></span>

<span data-ttu-id="ad4b3-199">反馈对我们非常重要。</span><span class="sxs-lookup"><span data-stu-id="ad4b3-199">Your feedback is important to us.</span></span>  <span data-ttu-id="ad4b3-200">如果此版本有任何问题，请查看有关现有问题的 [GitHub 问题](https://github.com/NuGet/Home/issues) 和 [Visual Studio 开发人员社区](https://developercommunity.visualstudio.com/) 。</span><span class="sxs-lookup"><span data-stu-id="ad4b3-200">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="ad4b3-201">对于 NuGet 中的新问题，请报告 [GitHub 问题](https://github.com/NuGet/Home/issues/new)。</span><span class="sxs-lookup"><span data-stu-id="ad4b3-201">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="ad4b3-202">对于一般的 NuGet 体验问题，请通过 "帮助" 下的 "你喜欢的 IDE" 中的 " [报告问题](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) " 选项告知我们 **> 报告问题**。</span><span class="sxs-lookup"><span data-stu-id="ad4b3-202">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>