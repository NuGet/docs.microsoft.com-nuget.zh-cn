---
title: "NuGet 4.0 RC 发行说明 | Microsoft Docs"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 906cc4dd-7948-4e86-a093-21df830ce8c3
description: "NuGet 4.0 RTM 的发行说明，包括已知问题、bug 修复、新增功能和 DCR。"
keywords: "NuGet 4.0 RTM 发行说明, bug 修复, 已知问题, 新增功能, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2cdee8b736fa2c651da803be9a10a6114936134a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="40-rtm-release-notes"></a><span data-ttu-id="4d73d-104">4.0 RTM 发行说明</span><span class="sxs-lookup"><span data-stu-id="4d73d-104">4.0 RTM Release Notes</span></span>

<span data-ttu-id="4d73d-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 采用的 NuGet 4.0 添加了 .NET Core 支持，拥有大量优质修补程序并可提高性能。</span><span class="sxs-lookup"><span data-stu-id="4d73d-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="4d73d-106">此版本还具有一些改进，如支持 PackageReference、作为 MSBuild 目标的 NuGet 命令、后台包还原等等。</span><span class="sxs-lookup"><span data-stu-id="4d73d-106">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="4d73d-107">已知问题</span><span class="sxs-lookup"><span data-stu-id="4d73d-107">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="4d73d-108">当有多个项目引用解决方案中的另一项目时，NuGet 还原可能会失败</span><span class="sxs-lookup"><span data-stu-id="4d73d-108">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="4d73d-109">问题：</span><span class="sxs-lookup"><span data-stu-id="4d73d-109">Issue:</span></span>
<span data-ttu-id="4d73d-110">如果解决方案中对同一项目的项目引用的大小写或路径不同，则 NuGet 还原可能会不起作用。</span><span class="sxs-lookup"><span data-stu-id="4d73d-110">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="4d73d-111">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="4d73d-111">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="4d73d-112">解决方法：</span><span class="sxs-lookup"><span data-stu-id="4d73d-112">Workaround:</span></span>
<span data-ttu-id="4d73d-113">将所有项目引用的大小写和相对路径修复为相同。</span><span class="sxs-lookup"><span data-stu-id="4d73d-113">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="4d73d-114">使用包管理器控制台时，“Enter”键可能不起作用</span><span class="sxs-lookup"><span data-stu-id="4d73d-114">While using Package Manager Console, 'Enter' key may not work</span></span>
#### <a name="issue"></a><span data-ttu-id="4d73d-115">问题：</span><span class="sxs-lookup"><span data-stu-id="4d73d-115">Issue:</span></span>
<span data-ttu-id="4d73d-116">有时无法在包管理器控制台中使用 Enter 键。</span><span class="sxs-lookup"><span data-stu-id="4d73d-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="4d73d-117">如果看到此内容，请在修补程序上签出进程，并提供有关重现步骤的其他任何有用信息。</span><span class="sxs-lookup"><span data-stu-id="4d73d-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="4d73d-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="4d73d-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="4d73d-119">解决方法：</span><span class="sxs-lookup"><span data-stu-id="4d73d-119">Workaround:</span></span>
<span data-ttu-id="4d73d-120">打开该解决方案之前，重启 Visual Studio 并打开 PMC。</span><span class="sxs-lookup"><span data-stu-id="4d73d-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="4d73d-121">或者，请尝试删除 `project.lock.json`，然后再次还原。</span><span class="sxs-lookup"><span data-stu-id="4d73d-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="4d73d-122">在 .NET Core 项目中，使用包含具有无效签名的程序集的包时，可能会出现无限还原循环</span><span class="sxs-lookup"><span data-stu-id="4d73d-122">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>
#### <a name="issue"></a><span data-ttu-id="4d73d-123">问题：</span><span class="sxs-lookup"><span data-stu-id="4d73d-123">Issue:</span></span>
<span data-ttu-id="4d73d-124">有时，使用包含具有无效签名的程序集的包或包版本设置有 'DateTime' 贴标时，会导致包自动还原无限循环运行。</span><span class="sxs-lookup"><span data-stu-id="4d73d-124">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="4d73d-125">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="4d73d-125">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="4d73d-126">解决方法：</span><span class="sxs-lookup"><span data-stu-id="4d73d-126">Workaround:</span></span>
<span data-ttu-id="4d73d-127">目前没有解决方法。</span><span class="sxs-lookup"><span data-stu-id="4d73d-127">There is no workaround at this time.</span></span>

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="4d73d-128">无法使用 Nuget 包管理器查看、添加或更新 DotNetCLITools</span><span class="sxs-lookup"><span data-stu-id="4d73d-128">You will be unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>
#### <a name="issue"></a><span data-ttu-id="4d73d-129">问题：</span><span class="sxs-lookup"><span data-stu-id="4d73d-129">Issue:</span></span>
<span data-ttu-id="4d73d-130">NuGet 包管理器不显示，且不允许添加/更新 DotNetCLITools。</span><span class="sxs-lookup"><span data-stu-id="4d73d-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="4d73d-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="4d73d-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

* #### <a name="workaround"></a><span data-ttu-id="4d73d-132">解决方法：</span><span class="sxs-lookup"><span data-stu-id="4d73d-132">Workaround:</span></span>
<span data-ttu-id="4d73d-133">必须在项目文件中手动编辑 DotNetCLIToolReferences。</span><span class="sxs-lookup"><span data-stu-id="4d73d-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="4d73d-134">如果对项目设置 PackageId 属性，则 NuGet 包还原会失败</span><span class="sxs-lookup"><span data-stu-id="4d73d-134">NuGet restore will fail when you set PackageId property for projects</span></span>
#### <a name="issue"></a><span data-ttu-id="4d73d-135">问题：</span><span class="sxs-lookup"><span data-stu-id="4d73d-135">Issue:</span></span>
<span data-ttu-id="4d73d-136">对于 .NET Core 项目，Visual Studio 中的 NuGet 还原不遵从项目的 PackageId 属性。</span><span class="sxs-lookup"><span data-stu-id="4d73d-136">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="4d73d-137">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="4d73d-137">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="4d73d-138">解决方法：</span><span class="sxs-lookup"><span data-stu-id="4d73d-138">Workaround:</span></span>
<span data-ttu-id="4d73d-139">使用命令行运行还原。</span><span class="sxs-lookup"><span data-stu-id="4d73d-139">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="4d73d-140">项目不包含 'obj' 文件夹时，包还原可能失败</span><span class="sxs-lookup"><span data-stu-id="4d73d-140">When your project does not have 'obj' folder, package restore may fail</span></span>
#### <a name="issue"></a><span data-ttu-id="4d73d-141">问题：</span><span class="sxs-lookup"><span data-stu-id="4d73d-141">Issue:</span></span>
<span data-ttu-id="4d73d-142">'obj' 文件夹被删除后 Visual Studio 无法还原 PackageReferences。</span><span class="sxs-lookup"><span data-stu-id="4d73d-142">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="4d73d-143">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="4d73d-143">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="4d73d-144">解决方法：</span><span class="sxs-lookup"><span data-stu-id="4d73d-144">Workaround:</span></span>
<span data-ttu-id="4d73d-145">手动创建 'obj' 文件夹后应可正常进行还原。</span><span class="sxs-lookup"><span data-stu-id="4d73d-145">Create 'obj' folder manually and the restore should work.</span></span> 

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="4d73d-146">在控制台中使用 Update-Package 手动更新包可能会失败</span><span class="sxs-lookup"><span data-stu-id="4d73d-146">Manually updating packages using Update-Package in console may fail</span></span>
#### <a name="issue"></a><span data-ttu-id="4d73d-147">问题：</span><span class="sxs-lookup"><span data-stu-id="4d73d-147">Issue:</span></span>
<span data-ttu-id="4d73d-148">在控制台中手动使用 Update-Package 对刚刚转换的 PackageReferences 项目仅适用一次。</span><span class="sxs-lookup"><span data-stu-id="4d73d-148">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="4d73d-149">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="4d73d-149">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="4d73d-150">解决方法：</span><span class="sxs-lookup"><span data-stu-id="4d73d-150">Workaround:</span></span>
<span data-ttu-id="4d73d-151">目前没有解决方法。</span><span class="sxs-lookup"><span data-stu-id="4d73d-151">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="4d73d-152">对目标框架版本重定目标可能会导致 Intellisense 不完整</span><span class="sxs-lookup"><span data-stu-id="4d73d-152">Retargeting target framework version may lead to incomplete Intellisense</span></span>
#### <a name="issue"></a><span data-ttu-id="4d73d-153">问题：</span><span class="sxs-lookup"><span data-stu-id="4d73d-153">Issue:</span></span>
<span data-ttu-id="4d73d-154">在 Visual Studio 中对目标框架版本重定目标可能会导致 Intellisense 不完整。</span><span class="sxs-lookup"><span data-stu-id="4d73d-154">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="4d73d-155">将 PackageReferences 用作包管理器格式时可能出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="4d73d-155">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="4d73d-156">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="4d73d-156">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="4d73d-157">解决方法：</span><span class="sxs-lookup"><span data-stu-id="4d73d-157">Workaround:</span></span>
<span data-ttu-id="4d73d-158">手动进行还原。</span><span class="sxs-lookup"><span data-stu-id="4d73d-158">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="4d73d-159">面向 .NET461 的项目引用面向 .NETStandard 的另一项目时 `msbuild /t:restore` 出现失败</span><span class="sxs-lookup"><span data-stu-id="4d73d-159">`msbuild /t:restore` fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="4d73d-160">问题：</span><span class="sxs-lookup"><span data-stu-id="4d73d-160">Issue:</span></span>
<span data-ttu-id="4d73d-161">面向 .NET461 的基于 PackageReferenece 的项目引用面向 .NETStandard 的另一基于 PackageReference 的项目时 msbuild /t:restore 出现失败。</span><span class="sxs-lookup"><span data-stu-id="4d73d-161">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="4d73d-162">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="4d73d-162">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="4d73d-163">解决方法：</span><span class="sxs-lookup"><span data-stu-id="4d73d-163">Workaround:</span></span>
<span data-ttu-id="4d73d-164">目前没有解决方法。</span><span class="sxs-lookup"><span data-stu-id="4d73d-164">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="4d73d-165">NuGet 4.0 RTM 时间框架中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="4d73d-165">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="4d73d-166">[NuGet 4.0 RC 发行说明](../release-notes/nuget-4.0-RC.md) - 列出了所有 NuGet 4.0 RC 中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="4d73d-166">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

<span data-ttu-id="4d73d-167">**Bug：**</span><span class="sxs-lookup"><span data-stu-id="4d73d-167">**Bug:**</span></span>

* <span data-ttu-id="4d73d-168">Visual Studio 中的 NuGet 还原不遵从项目的 PackageId 属性 - [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="4d73d-168">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

* <span data-ttu-id="4d73d-169">在 vsix 包中添加包时，NuGet ProjectSystemCache 出现错误 - [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="4d73d-169">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

* <span data-ttu-id="4d73d-170">如果在具有多个 TFM 的项目中使用了 IncludeSource，包会引发异常 - [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="4d73d-170">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

* <span data-ttu-id="4d73d-171">使用解决方案范围的包管理的更新时，VS 2017 RC3 出现故障 - [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="4d73d-171">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

* <span data-ttu-id="4d73d-172">无法卸载新安装的包 - [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="4d73d-172">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

* <span data-ttu-id="4d73d-173">迁移到 PackageRef 时，混合解决方案出现异常还原行为 - [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="4d73d-173">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

* <span data-ttu-id="4d73d-174">如果在启动 NuGet 操作（安装、更新或还原）后立即进行生成操作，可能导致 VS 挂起 - [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="4d73d-174">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

* <span data-ttu-id="4d73d-175">UI 挂起 - 死锁初始化 NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="4d73d-175">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

* <span data-ttu-id="4d73d-176">add package 命令应将版本添加为属性（而不是元素）- [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="4d73d-176">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

* <span data-ttu-id="4d73d-177">Dotnet Restore foo.sln - SLN 中的配置导致还原图中出现重复（但配置不同）项目时，此操作失败 - [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="4d73d-177">Dotnet Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

* <span data-ttu-id="4d73d-178">仅包含内容的包 - [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="4d73d-178">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

* <span data-ttu-id="4d73d-179">默认情况下，选择退出包格式选择器选项 - [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="4d73d-179">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

* <span data-ttu-id="4d73d-180">性能：CreateUAP_CSharp_VS.01.1.Create 项目使 Duration_TotalElapsedTime 回退了 3,153.570 毫秒 (149.1%)。</span><span class="sxs-lookup"><span data-stu-id="4d73d-180">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="4d73d-181">基线 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="4d73d-181">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

* <span data-ttu-id="4d73d-182">性能：ManagedLangs_CS_DDRIT.0300.Rebuild 解决方案使 Duration_TotalElapsedTime 回退了 1.5 秒。</span><span class="sxs-lookup"><span data-stu-id="4d73d-182">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="4d73d-183">基线 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="4d73d-183">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

* <span data-ttu-id="4d73d-184">多个 TFM 项目中出现提名失败 - [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="4d73d-184">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

* <span data-ttu-id="4d73d-185">性能：WebForms_DDRIT.1200.Close 解决方案使 VM_ImagesInMemory_Total_devenv 回退了 3.000 计数 (0.5%)。</span><span class="sxs-lookup"><span data-stu-id="4d73d-185">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="4d73d-186">基线 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="4d73d-186">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

* <span data-ttu-id="4d73d-187">vsfeedback - 面向 netcoreapp1.1 时出现包警告 - [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="4d73d-187">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

* <span data-ttu-id="4d73d-188">尝试将 NuGet 包添加到空 ASP.NET Core Web 应用程序中时，出现 PathTooLongException - [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="4d73d-188">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

* <span data-ttu-id="4d73d-189">包的运行过于频繁 - 目标依赖项关系图中存在涉及目标“包”的循环依赖时，dotnet 包失败 - [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="4d73d-189">Pack runs too often -- dotnet pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

* <span data-ttu-id="4d73d-190">包的运行过于频繁 - 生成 NuGet 包不包括所有配置 - [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="4d73d-190">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

* <span data-ttu-id="4d73d-191">使用 packageref 在 C++ 项目中添加 nuget 时，出现 NullReferenceException - [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="4d73d-191">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

* <span data-ttu-id="4d73d-192">辅助功能：讲述人不讲述用于选择要安装包的项目的复选框 - [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="4d73d-192">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

* <span data-ttu-id="4d73d-193">NuGet VS17 偶尔无法连接到 VSO/VSTS 源 - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="4d73d-193">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

* <span data-ttu-id="4d73d-194">如果 PackagePath 将路径指定为“contentFiles”，contentFiles 会输出到错误位置 - [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="4d73d-194">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

* <span data-ttu-id="4d73d-195">包目标将 VersionSuffix 追加到 PackageVersion 属性中 - [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="4d73d-195">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

* <span data-ttu-id="4d73d-196">指定包路径操作不适用于 dotnet 包 - [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="4d73d-196">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

* <span data-ttu-id="4d73d-197">在还原期间，NuGet 输出大量有关重复导入的警告 - [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="4d73d-197">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

* <span data-ttu-id="4d73d-198">在深色主题下，选择“NuGet 包管理器格式”对话框的显示不清晰 - [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="4d73d-198">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

* <span data-ttu-id="4d73d-199">生成还原时，VS 出现故障 - [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="4d73d-199">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

* <span data-ttu-id="4d73d-200">如果在 targetframeworks 中对 TFM 进行添加、保存和生成操作，Visual Studio 出现死锁。</span><span class="sxs-lookup"><span data-stu-id="4d73d-200">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="4d73d-201">10% 的时间 - [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="4d73d-201">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

* <span data-ttu-id="4d73d-202">nuget 包不输出有关成功打包项目的成功消息 - [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="4d73d-202">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

* <span data-ttu-id="4d73d-203">由于找不到 System.IO.Compression 4.1，PackTask 失败 - [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="4d73d-203">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

* <span data-ttu-id="4d73d-204">包的运行过于频繁 - 由于文件访问冲突，PackTask 频繁失败 - [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="4d73d-204">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

* <span data-ttu-id="4d73d-205">在后台还原期间，NuGet 打开输出窗口 - [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="4d73d-205">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

* <span data-ttu-id="4d73d-206">将 ServiceProvider 作为危险编码模式删除（这可能导致挂起）- [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="4d73d-206">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

* <span data-ttu-id="4d73d-207">性能/UIHang - 改善 DownloadTimeoutStream 的读取 - [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="4d73d-207">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

* <span data-ttu-id="4d73d-208">若在完成 NuGet 还原之前尝试关闭项目，Visual Studio 出现死锁 - [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="4d73d-208">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

* <span data-ttu-id="4d73d-209">有关 PackTask 和打包 `.nuspec` 的问题 - [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="4d73d-209">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

* <span data-ttu-id="4d73d-210">[vsfeedback] 无法在新项目上解析 nuget 包（需要重启 Visual Studio）- [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="4d73d-210">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

* <span data-ttu-id="4d73d-211">[vsfeedback] 显示可用包版本的“版本”下拉列表难以与所选的 nuget 包同步... - [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="4d73d-211">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

* <span data-ttu-id="4d73d-212">与 CPS 交互时，Nuget.Client 应使用 CPS JoinableTaskFactory 以防止死锁 - [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="4d73d-212">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

* <span data-ttu-id="4d73d-213">NuGet 3.5.0 不从包中解压缩 `.targets` - [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="4d73d-213">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

* <span data-ttu-id="4d73d-214">dotnet 包不支持 `.csproj` 中的标题 - [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="4d73d-214">dotnet pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

* <span data-ttu-id="4d73d-215">安装包导致 VS2017 RC 中出现错误对话框 - [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="4d73d-215">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

* <span data-ttu-id="4d73d-216">针对 .net core 项目的更新包操作似乎不起作用，因为 UI 没有从提名中获取 CPS 更新。</span><span class="sxs-lookup"><span data-stu-id="4d73d-216">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="4d73d-217"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="4d73d-217"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

* <span data-ttu-id="4d73d-218">改进未解析的引用警告 - [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="4d73d-218">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

* <span data-ttu-id="4d73d-219">dotnet 包 - ProjectReference 丢失版本信息 - [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="4d73d-219">dotnet pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

* <span data-ttu-id="4d73d-220">创建 UWP 应用、创建项目和重新生成的总运行时间回归 - [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="4d73d-220">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

* <span data-ttu-id="4d73d-221">尽管还原期间出现错误，仍显示成功还原消息。</span><span class="sxs-lookup"><span data-stu-id="4d73d-221">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="4d73d-222"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="4d73d-222"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

* <span data-ttu-id="4d73d-223">将 Nuget.CommandLine 3.4.4 重新发布到 Nuget.org - [# 2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="4d73d-223">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

* <span data-ttu-id="4d73d-224">在迁移期间，项目从 `project.json` 更改为 `.csproj` --- 还原失败 - [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="4d73d-224">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

* <span data-ttu-id="4d73d-225">在新创建的 xunit 测试项目上，还原失败 - [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="4d73d-225">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

* <span data-ttu-id="4d73d-226">核心项目可在打开状态下挂起和锁定 UI - [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="4d73d-226">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

* <span data-ttu-id="4d73d-227">修复生成任务的目标文件 - [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="4d73d-227">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

* <span data-ttu-id="4d73d-228">生成卸载引用的项目的解决方案后，错误列表中出现错误 - [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="4d73d-228">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

* <span data-ttu-id="4d73d-229">MSB4057：项目中不存在目标“_GenerateRestoreGraphProjectEntry”。</span><span class="sxs-lookup"><span data-stu-id="4d73d-229">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="4d73d-230"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="4d73d-230"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

* <span data-ttu-id="4d73d-231">vsfeedback：选择所有项目时，解决方案的 nuget 管理器 UI 出现故障 - [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="4d73d-231">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

* <span data-ttu-id="4d73d-232">存在尾随斜杠时，nuget.exe msbuildpath 失败 - [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="4d73d-232">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

* <span data-ttu-id="4d73d-233">vsfeedback：NuGet 还原提供 LinqToTwitter 项目的多个项目引用警告 - [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="4d73d-233">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

* <span data-ttu-id="4d73d-234">`.csproj` 的包不包括 minClientVersion 属性 - [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="4d73d-234">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

* <span data-ttu-id="4d73d-235">运送的 NuGet.Build.Tasks.Pack.dll 延迟了 VS2017 (d15rel 26014.00) 中的签名 - [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="4d73d-235">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

* <span data-ttu-id="4d73d-236">VSFeedback：使用 CMake 3.7.1 生成的 VS 2015 项目的还原失败 - [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="4d73d-236">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

* <span data-ttu-id="4d73d-237">VSFeedback：还原错误可能掩盖生成可提供的更完整的错误消息 - [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="4d73d-237">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

* <span data-ttu-id="4d73d-238">[VSFeedback] 还原网站项目的 NuGet 包时出现错误：值不能为 Null。</span><span class="sxs-lookup"><span data-stu-id="4d73d-238">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="4d73d-239"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="4d73d-239"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

* <span data-ttu-id="4d73d-240">迁移在 NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker 中引发“对象引用异常”- [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="4d73d-240">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

* <span data-ttu-id="4d73d-241">dotnet 包应使用生成包时所用的版本来打包工具 - [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="4d73d-241">dotnet pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

* <span data-ttu-id="4d73d-242">还原需要花费数秒时，新的后台还原将毫秒写入状态栏 - [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="4d73d-242">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

* <span data-ttu-id="4d73d-243">由于拼写错误，未能解析所有项目引用 - [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="4d73d-243">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

* <span data-ttu-id="4d73d-244">在包引用方案中启用 PCM 工作流 - [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="4d73d-244">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

* <span data-ttu-id="4d73d-245">在包管理器 UI 中找不到已安装的包 - [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="4d73d-245">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

* <span data-ttu-id="4d73d-246">PackagePath 为空时，dotnet 包失败 - [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="4d73d-246">dotnet pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

* <span data-ttu-id="4d73d-247">多用户方案中的还原任务失败 - [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="4d73d-247">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

* <span data-ttu-id="4d73d-248">使用 NuGet 包任务打包时，无法更改内容类型 - [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="4d73d-248">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

* <span data-ttu-id="4d73d-249">对于 MsBuild /t:pack，ContentFiles 的默认副本错误 - [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="4d73d-249">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

* <span data-ttu-id="4d73d-250">安装包还原将还原包的消息记录了两次 - [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="4d73d-250">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

* <span data-ttu-id="4d73d-251">删除 Guardrails - “运行时”部分的还原应仅应用于当前项目 - [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="4d73d-251">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

* <span data-ttu-id="4d73d-252">包任务在“content/”和“contentFiles/”中均放置了内容文件 - [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="4d73d-252">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

* <span data-ttu-id="4d73d-253">dotnet pack3 执行额外标记拆分操作 - [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="4d73d-253">dotnet pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

* <span data-ttu-id="4d73d-254">dotnet 包：打包具有包引用的项目导致重复导入警告 - [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="4d73d-254">dotnet pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

* <span data-ttu-id="4d73d-255">VS 中并非始终显示还原日志记录 - [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="4d73d-255">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

* <span data-ttu-id="4d73d-256">nuget 局部变量可帮助文本仍提到的包缓存 - [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="4d73d-256">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

* <span data-ttu-id="4d73d-257">Restore3 将 PackageReferences 与 TargetFrameworks 结合。</span><span class="sxs-lookup"><span data-stu-id="4d73d-257">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="4d73d-258"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="4d73d-258"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

* <span data-ttu-id="4d73d-259">在 VS“15”Preview 4 dev. 命令提示符中，</span><span class="sxs-lookup"><span data-stu-id="4d73d-259">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="4d73d-260">Nuget 选取意外的 MSBuild 版本 - [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="4d73d-260">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

* <span data-ttu-id="4d73d-261">还原失败时，写出目标/属性文件 - [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="4d73d-261">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

* <span data-ttu-id="4d73d-262">在 VS 15 命令提示符中运行时，还原期间的 NuGet 所遵循的兼容性填充码与 MSBuild 不同 - [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="4d73d-262">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

* <span data-ttu-id="4d73d-263">为 VS15 重新启用 PackFromProjectWithDevelopmentDependencySet - [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="4d73d-263">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

* <span data-ttu-id="4d73d-264">NuGet 的 Blend 出现问题 - [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="4d73d-264">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

* <span data-ttu-id="4d73d-265">将 4.0.0.2067 集成到 CLI 和 SDK 存储库以与 RC2 共同传送 - [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="4d73d-265">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

* <span data-ttu-id="4d73d-266">创建新核心控制台应用、关闭解决方案、打开解决方案和关闭解决方案时，VS 挂起 - [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="4d73d-266">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

* <span data-ttu-id="4d73d-267">针对 d15prerel.25916.01 打开项目时，点击出现挂起 - [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="4d73d-267">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

* <span data-ttu-id="4d73d-268">修复 dotnet/nuget.exe 局部变量的 doc/help 消息 - [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="4d73d-268">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

* <span data-ttu-id="4d73d-269">检查 PackTask 是否存在尾随或前导空格的问题 - [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="4d73d-269">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

* <span data-ttu-id="4d73d-270">dotnet 包从 obj（而不是 bin）进行打包 - [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="4d73d-270">dotnet pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

* <span data-ttu-id="4d73d-271">dotnet 包似乎始终将 ProjectReference 版本设置为 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="4d73d-271">dotnet pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

* <span data-ttu-id="4d73d-272">由于项目引用和 <TargetFramework>，dotnet 包失败 - [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="4d73d-272">dotnet pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

* <span data-ttu-id="4d73d-273">ProjectSystemCache.TryGetProjectNameByShortName 中的 LockRecursionException - [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="4d73d-273">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

* <span data-ttu-id="4d73d-274">删除 MSBuild 属性中的空格 - [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="4d73d-274">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

* <span data-ttu-id="4d73d-275">合并在项目加载上引发的两个项目事件 - [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="4d73d-275">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

* <span data-ttu-id="4d73d-276">`project.assets.json` 文件中的 P2P 库版本不正确 - [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="4d73d-276">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

* <span data-ttu-id="4d73d-277">由于源无响应且包不可用，还原出现故障 - [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="4d73d-277">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

* <span data-ttu-id="4d73d-278">出现大量 MSBuild 错误输出时，nuget.exe 可能挂起 - [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="4d73d-278">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

* <span data-ttu-id="4d73d-279">Blend 的 Restore-on-build 第一次失败，第二次成功（修复了 VS 方案）- [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="4d73d-279">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

<span data-ttu-id="4d73d-280">**DCR：**</span><span class="sxs-lookup"><span data-stu-id="4d73d-280">**DCR:**</span></span>

* <span data-ttu-id="4d73d-281">将 vsix 从 v2 vsix 迁移到 v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="4d73d-281">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

* <span data-ttu-id="4d73d-282">NuGet 应具有一个机制，该机制用于获取指向 MSBuild 中的锁定文件的路径 - [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="4d73d-282">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

* <span data-ttu-id="4d73d-283">将生成资产添加到 TFM 兼容性检查和资产文件 - [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="4d73d-283">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

* <span data-ttu-id="4d73d-284">在包目标中定义新的 ProjectCapability“包”，用于启用与包相关的功能 - [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="4d73d-284">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

* <span data-ttu-id="4d73d-285">以“GeneratePackageOnBuild”MSBuild 属性为条件，将包作为后期生成目标运行 - [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="4d73d-285">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

* <span data-ttu-id="4d73d-286">使用 NuGet 属性 RestoreProjectStyle 创建特定的 NuGet 项目 - [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="4d73d-286">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

* <span data-ttu-id="4d73d-287">为可传递的项目引用更改调整还原 - [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="4d73d-287">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

* <span data-ttu-id="4d73d-288">在非 UWP 项目的目标文件中添加 NuGet 属性 - [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="4d73d-288">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

* <span data-ttu-id="4d73d-289">UWP TargetPlatformVersion 支持 - [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="4d73d-289">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

* <span data-ttu-id="4d73d-290">将项目引用元数据传达到 NuGet 项目系统 - [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="4d73d-290">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

* <span data-ttu-id="4d73d-291">针对打包模式添加 UI - [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="4d73d-291">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

* <span data-ttu-id="4d73d-292">旧版 `.csproj` 需要在项目/目标中设置 NugetTargetMoniker 和 RuntimeIdentifiers - [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="4d73d-292">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

* <span data-ttu-id="4d73d-293">安装包可能与自动还原重叠 - [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="4d73d-293">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

* <span data-ttu-id="4d73d-294">未加载 VSPackage 时，不会发生上下文菜单 QueryStatus - [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="4d73d-294">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

* <span data-ttu-id="4d73d-295">解决方案还原和生成还原时仍显示对话框 - [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="4d73d-295">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

* <span data-ttu-id="4d73d-296">在 NuGet.Clients 解决方案生成中隔离 VSSDK 版本 - [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="4d73d-296">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

<span data-ttu-id="4d73d-297">**功能：**</span><span class="sxs-lookup"><span data-stu-id="4d73d-297">**Feature:**</span></span>

* <span data-ttu-id="4d73d-298">对 NuGet.Core.sln 中的字符串进行本地化 - [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="4d73d-298">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

* <span data-ttu-id="4d73d-299">Nuget 强制加载 LSL 模式下的 Web 应用程序项目 - [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="4d73d-299">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

* <span data-ttu-id="4d73d-300">对于“已安装 SDK”的包，用于阻止 UI 中的版本更改的 AutoReferenced PackageReference 支持 - [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="4d73d-300">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

* <span data-ttu-id="4d73d-301">为任何项目依赖项 (PackageRef) 正确传达 PackageSpec.Version - [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="4d73d-301">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

* <span data-ttu-id="4d73d-302">支持从命令行删除引用到 `.csproj` 中 - [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="4d73d-302">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

* <span data-ttu-id="4d73d-303">支持对 PackageReference 项目（常规和 xplat）和轻型解决方案加载的还原 - [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="4d73d-303">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

* <span data-ttu-id="4d73d-304">支持将引用从命令行添加到 `.csproj` 中 - [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="4d73d-304">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

* <span data-ttu-id="4d73d-305">对于 `packages.config` 或 `project.json`，支持轻型解决方案加载的 NuGet 还原 - [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="4d73d-305">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

* <span data-ttu-id="4d73d-306">由 nuget 生成的目标文件中的 contentFiles 支持 - [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="4d73d-306">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

* <span data-ttu-id="4d73d-307">使用 MSBuild 在 Mac 上建立用于 nuget.exe 验证的 Mono CI - [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="4d73d-307">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

* <span data-ttu-id="4d73d-308">从 v2 NuGet.Core 依赖项中移出 NuGet - [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="4d73d-308">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>


## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="4d73d-309">RTM 中已修复 GitHub 问题的链接</span><span class="sxs-lookup"><span data-stu-id="4d73d-309">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="4d73d-310">问题列表 1</span><span class="sxs-lookup"><span data-stu-id="4d73d-310">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[<span data-ttu-id="4d73d-311">问题列表 2</span><span class="sxs-lookup"><span data-stu-id="4d73d-311">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[<span data-ttu-id="4d73d-312">问题列表 3</span><span class="sxs-lookup"><span data-stu-id="4d73d-312">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[<span data-ttu-id="4d73d-313">问题列表 4</span><span class="sxs-lookup"><span data-stu-id="4d73d-313">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[<span data-ttu-id="4d73d-314">问题列表 5</span><span class="sxs-lookup"><span data-stu-id="4d73d-314">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")

