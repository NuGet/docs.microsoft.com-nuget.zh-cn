---
title: NuGet 4.3 RTM 发行说明
description: NuGet 4.3 RTM 的发行说明，包括已知问题、bug 修复、新增功能和 DCR。
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e9b6d15584d875f59ed64fe662944db3e37aeabb
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780172"
---
# <a name="nuget-43-release-notes"></a><span data-ttu-id="af5cc-103">NuGet 4.3 发行说明</span><span class="sxs-lookup"><span data-stu-id="af5cc-103">NuGet 4.3 Release Notes</span></span>

<span data-ttu-id="af5cc-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 附带 NuGet 4.3 RTM，NuGet 4.3 RTM 添加了对新方案（例如 .NET Standard 2.0/.NET Core 2.0）的支持、包含多种质量修复和提升性体能。</span><span class="sxs-lookup"><span data-stu-id="af5cc-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="af5cc-105">此版本还提供多方面的提升，例如对语义化版本控制 2.0.0 的支持、NuGet 警告和错误的 MSBuild 集成等等。</span><span class="sxs-lookup"><span data-stu-id="af5cc-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="summary-whats-new-in-430"></a><span data-ttu-id="af5cc-106">摘要:4.3.0 版中的新增功能</span><span class="sxs-lookup"><span data-stu-id="af5cc-106">Summary: What's New in 4.3.0</span></span>

## <a name="summary-whats-new-in-431"></a><span data-ttu-id="af5cc-107">摘要:4.3.1 版中的新增功能</span><span class="sxs-lookup"><span data-stu-id="af5cc-107">Summary: What's New in 4.3.1</span></span>

* <span data-ttu-id="af5cc-108">安全修复：~/.nuget 中针对所创建文件的权限过于开放 [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="af5cc-108">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>
* <span data-ttu-id="af5cc-109">安全修复：NUPKGs 中的文件可以具有高于 NUPKG 目录的相对路径 [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="af5cc-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="af5cc-110">已知问题</span><span class="sxs-lookup"><span data-stu-id="af5cc-110">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="af5cc-111">在某些情况下，NuGet 还原操作可能会将禁用的包源视作已启用进行处理</span><span class="sxs-lookup"><span data-stu-id="af5cc-111">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="af5cc-112">问题</span><span class="sxs-lookup"><span data-stu-id="af5cc-112">Issue</span></span>

<span data-ttu-id="af5cc-113">以下还原命令行方法将被禁用的包源视为已启用。</span><span class="sxs-lookup"><span data-stu-id="af5cc-113">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="af5cc-114">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="af5cc-114">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="af5cc-115">`dotnet restore`（不管是使用 VS 随附的 dotnet.exe，还是使用 NetCore SDK 2.0.0 随附的文件）</span><span class="sxs-lookup"><span data-stu-id="af5cc-115">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="af5cc-116">解决方法</span><span class="sxs-lookup"><span data-stu-id="af5cc-116">Workaround</span></span>

1. <span data-ttu-id="af5cc-117">使用 Visual Studio（2017 15.3 或更高版本）或 NuGet.exe（v4.3.0 或更高版本）</span><span class="sxs-lookup"><span data-stu-id="af5cc-117">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="af5cc-118">删除禁用的源，并继续使用 msbuild 或 dotnet.exe。</span><span class="sxs-lookup"><span data-stu-id="af5cc-118">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="af5cc-119">对于解决方案，可以在 NuGet.config 中使用“Clear”，再定义此解决方案所必需的源。</span><span class="sxs-lookup"><span data-stu-id="af5cc-119">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="af5cc-120">使用包管理器控制台时，“Enter”键可能不起作用</span><span class="sxs-lookup"><span data-stu-id="af5cc-120">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="af5cc-121">问题</span><span class="sxs-lookup"><span data-stu-id="af5cc-121">Issue</span></span>

<span data-ttu-id="af5cc-122">有时无法在包管理器控制台中使用 Enter 键。</span><span class="sxs-lookup"><span data-stu-id="af5cc-122">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="af5cc-123">如果看到此内容，请在修补程序上签出进程，并提供有关重现步骤的其他任何有用信息。</span><span class="sxs-lookup"><span data-stu-id="af5cc-123">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="af5cc-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="af5cc-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="af5cc-125">解决方法</span><span class="sxs-lookup"><span data-stu-id="af5cc-125">Workaround</span></span>

<span data-ttu-id="af5cc-126">打开该解决方案之前，重启 Visual Studio 并打开 PMC。</span><span class="sxs-lookup"><span data-stu-id="af5cc-126">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="af5cc-127">或者，请尝试删除 `project.lock.json`，然后再次还原。</span><span class="sxs-lookup"><span data-stu-id="af5cc-127">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="af5cc-128">无法使用 NuGet 包管理器查看、添加或更新 DotNetCLITools</span><span class="sxs-lookup"><span data-stu-id="af5cc-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="af5cc-129">问题</span><span class="sxs-lookup"><span data-stu-id="af5cc-129">Issue</span></span>

<span data-ttu-id="af5cc-130">NuGet 包管理器不显示，且不允许添加/更新 DotNetCLITools。</span><span class="sxs-lookup"><span data-stu-id="af5cc-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="af5cc-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="af5cc-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="af5cc-132">解决方法</span><span class="sxs-lookup"><span data-stu-id="af5cc-132">Workaround</span></span>

<span data-ttu-id="af5cc-133">必须在项目文件中手动编辑 DotNetCLIToolReferences。</span><span class="sxs-lookup"><span data-stu-id="af5cc-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="af5cc-134">对目标框架版本重定目标可能会导致 Intellisense 不完整</span><span class="sxs-lookup"><span data-stu-id="af5cc-134">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="af5cc-135">问题</span><span class="sxs-lookup"><span data-stu-id="af5cc-135">Issue</span></span>

<span data-ttu-id="af5cc-136">在 Visual Studio 中对目标框架版本重定目标可能会导致 Intellisense 不完整。</span><span class="sxs-lookup"><span data-stu-id="af5cc-136">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="af5cc-137">将 PackageReferences 用作包管理器格式时可能出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="af5cc-137">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="af5cc-138">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="af5cc-138">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="af5cc-139">解决方法</span><span class="sxs-lookup"><span data-stu-id="af5cc-139">Workaround</span></span>

<span data-ttu-id="af5cc-140">手动进行还原。</span><span class="sxs-lookup"><span data-stu-id="af5cc-140">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="af5cc-141">NuGet 4.3 RTM 时间框架中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="af5cc-141">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="af5cc-142">[NuGet 4.0 RTM 发行说明](../release-notes/nuget-4.0-RTM.md) - 列出所有 NuGet 4.0 RTM 修复的问题</span><span class="sxs-lookup"><span data-stu-id="af5cc-142">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="af5cc-143">特征</span><span class="sxs-lookup"><span data-stu-id="af5cc-143">Features</span></span>

- <span data-ttu-id="af5cc-144">提升 NuGet 还原性能 - 为命令行还原和 VS 实现更小的 NoOp - [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="af5cc-144">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="af5cc-145">NET Core 2.0：VS/Dotnet CLI 应开始使用现有的 NuGet 功能：FallBack 文件夹 - [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="af5cc-145">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="af5cc-146">NET Core 2.0：使用户可以忽略特定还原警告（或提升为错误）- [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="af5cc-146">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="af5cc-147">NET Core 2.0：CLI 本地化程序集 - [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="af5cc-147">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="af5cc-148">NET Core 2.0：将所有警告/错误注册到资产文件（包括 PackageTargetFallback）- [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="af5cc-148">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="af5cc-149">启用 TFM 支持：NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="af5cc-149">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="af5cc-150">减少 NuGet.Core 和 NuGet.Client 项目（和 DLL）的数量 - [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="af5cc-150">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="af5cc-151">添加将 NuGet 警告标记为错误的功能 - [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="af5cc-151">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="af5cc-152">Bug</span><span class="sxs-lookup"><span data-stu-id="af5cc-152">Bugs</span></span>

- <span data-ttu-id="af5cc-153">msbuild /t:pack 失败，“PackTask”任务不支持“DevelopmentDependency”参数 - [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="af5cc-153">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="af5cc-154">如果未在 PackagePath 末尾添加 Windows 目录分隔符，则内容文件的目录结构会合并 - [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="af5cc-154">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="af5cc-155">netcore 项目不支持设置为 developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="af5cc-155">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="af5cc-156">同步加载的 RestoreManagerPackage 锁定 UI 线程和死锁 VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="af5cc-156">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="af5cc-157">dotnet</span><span class="sxs-lookup"><span data-stu-id="af5cc-157">dotnet</span></span>
  - <span data-ttu-id="af5cc-158">dotnetcore Restore（和 msbuild /t:restore）跳过有显式解决方案项目依赖项的项目 [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="af5cc-158">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="af5cc-159">如果解决方案有引用大小写不同的同一项目的 projectreference，则还原可能不起作用。</span><span class="sxs-lookup"><span data-stu-id="af5cc-159">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="af5cc-160">这还会影响大小写相同的不同相对路径 - [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="af5cc-160">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="af5cc-161">NuGet 包还原的可执行文件不能再使用 .NET Core 2.0 执行 - [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="af5cc-161">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="af5cc-162">NuGet.exe 在分析解决方案文件时吞并异常的详细信息 - [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="af5cc-162">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="af5cc-163">如果 ContentTargetFolders 在 Windows 上包含以“/”结尾的路径，则包会将内容文件放在错误的位置 - [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="af5cc-163">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="af5cc-164">不能还原面向 netcoreapp1.1 的工具包的 DotNetCliToolReference - [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="af5cc-164">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="af5cc-165">Nuget 更新 CLI 将旧包版本条件留在项目文件中 (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="af5cc-165">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="af5cc-166">DCR</span><span class="sxs-lookup"><span data-stu-id="af5cc-166">DCRs</span></span>

- <span data-ttu-id="af5cc-167">从CPS nomation 读取 DotnetCliToolTargetFramework - [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="af5cc-167">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="af5cc-168">TPMinV check 应适用于 pj 样式 UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="af5cc-168">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="af5cc-169">提升 AutoReferenced 包的 UI 说明 - [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="af5cc-169">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="af5cc-170">NuGet restore 从运行时部分选择编译资产。</span><span class="sxs-lookup"><span data-stu-id="af5cc-170">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="af5cc-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="af5cc-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="af5cc-172">将依赖项诊断放在锁定文件中 - [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="af5cc-172">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="af5cc-173">4\.3 RTM 中已修复 GitHub 问题的链接</span><span class="sxs-lookup"><span data-stu-id="af5cc-173">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="af5cc-174">问题列表</span><span class="sxs-lookup"><span data-stu-id="af5cc-174">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
