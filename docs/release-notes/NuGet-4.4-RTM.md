---
title: NuGet 4.4 RTM 发行说明
description: NuGet 4.3 RTM 的发行说明，包括已知问题、bug 修复、新增功能和 DCR。
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 970a920a401b8a74c04d84cbad9933c54e3cd19e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776285"
---
# <a name="nuget-44-release-notes"></a><span data-ttu-id="2a44a-103">NuGet 4.4 发行说明</span><span class="sxs-lookup"><span data-stu-id="2a44a-103">NuGet 4.4 Release Notes</span></span>

<span data-ttu-id="2a44a-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 附带 NuGet 4.4 RTM。</span><span class="sxs-lookup"><span data-stu-id="2a44a-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="summary-whats-new-in-440"></a><span data-ttu-id="2a44a-105">摘要:4.4.0 版中的新增功能</span><span class="sxs-lookup"><span data-stu-id="2a44a-105">Summary: What's New in 4.4.0</span></span>

## <a name="summary-whats-new-in-442"></a><span data-ttu-id="2a44a-106">摘要:4.4.2 版中的新增功能</span><span class="sxs-lookup"><span data-stu-id="2a44a-106">Summary: What's New in 4.4.2</span></span>

* <span data-ttu-id="2a44a-107">安全修复：~/.nuget 中针对所创建文件的权限过于开放 [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="2a44a-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-443"></a><span data-ttu-id="2a44a-108">摘要:4.4.3 版中的新增功能</span><span class="sxs-lookup"><span data-stu-id="2a44a-108">Summary: What's New in 4.4.3</span></span>

* <span data-ttu-id="2a44a-109">安全修复：NUPKGs 中的文件可以具有高于 NUPKG 目录的相对路径 [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="2a44a-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="2a44a-110">已知问题</span><span class="sxs-lookup"><span data-stu-id="2a44a-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="2a44a-111">使用 .NET Framework 和 NuGet 的 .NET Standard 2.0 的问题</span><span class="sxs-lookup"><span data-stu-id="2a44a-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="2a44a-112">.NET Standard 及其工具旨在使面向 .NET Framework 4.6.1 的项目可使用面向 .NET Standard 2.0 或更早版本的 NuGet 包和项目。</span><span class="sxs-lookup"><span data-stu-id="2a44a-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="2a44a-113">[本文档](https://github.com/dotnet/standard/issues/481)总结了该方案相关问题、解决问题的计划以及可使用当前工具状态部署的变通方法。</span><span class="sxs-lookup"><span data-stu-id="2a44a-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="2a44a-114">使用包管理器控制台时，“Enter”键可能不起作用</span><span class="sxs-lookup"><span data-stu-id="2a44a-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="2a44a-115">问题</span><span class="sxs-lookup"><span data-stu-id="2a44a-115">Issue</span></span>

<span data-ttu-id="2a44a-116">有时无法在包管理器控制台中使用 Enter 键。</span><span class="sxs-lookup"><span data-stu-id="2a44a-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="2a44a-117">如果看到此内容，请在修补程序上签出进程，并提供有关重现步骤的其他任何有用信息。</span><span class="sxs-lookup"><span data-stu-id="2a44a-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="2a44a-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="2a44a-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="2a44a-119">解决方法</span><span class="sxs-lookup"><span data-stu-id="2a44a-119">Workaround</span></span>

<span data-ttu-id="2a44a-120">打开该解决方案之前，重启 Visual Studio 并打开 PMC。</span><span class="sxs-lookup"><span data-stu-id="2a44a-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="2a44a-121">或者，请尝试删除 `project.lock.json`，然后再次还原。</span><span class="sxs-lookup"><span data-stu-id="2a44a-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="2a44a-122">无法使用 NuGet 包管理器查看、添加或更新 DotNetCLITools</span><span class="sxs-lookup"><span data-stu-id="2a44a-122">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="2a44a-123">问题</span><span class="sxs-lookup"><span data-stu-id="2a44a-123">Issue</span></span>

<span data-ttu-id="2a44a-124">NuGet 包管理器不显示，且不允许添加/更新 DotNetCLITools。</span><span class="sxs-lookup"><span data-stu-id="2a44a-124">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="2a44a-125">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="2a44a-125">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="2a44a-126">解决方法</span><span class="sxs-lookup"><span data-stu-id="2a44a-126">Workaround</span></span>

<span data-ttu-id="2a44a-127">必须在项目文件中手动编辑 DotNetCLIToolReferences。</span><span class="sxs-lookup"><span data-stu-id="2a44a-127">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="2a44a-128">对目标框架版本重定目标可能会导致 Intellisense 不完整</span><span class="sxs-lookup"><span data-stu-id="2a44a-128">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="2a44a-129">问题</span><span class="sxs-lookup"><span data-stu-id="2a44a-129">Issue</span></span>

<span data-ttu-id="2a44a-130">在 Visual Studio 中对目标框架版本重定目标可能会导致 Intellisense 不完整。</span><span class="sxs-lookup"><span data-stu-id="2a44a-130">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="2a44a-131">将 PackageReferences 用作包管理器格式时可能出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="2a44a-131">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="2a44a-132">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="2a44a-132">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="2a44a-133">解决方法</span><span class="sxs-lookup"><span data-stu-id="2a44a-133">Workaround</span></span>

<span data-ttu-id="2a44a-134">手动进行还原。</span><span class="sxs-lookup"><span data-stu-id="2a44a-134">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="2a44a-135">.NET Core 项目中的某个包内附具有无效签名的程序集，该包可触发还原操作无限循环</span><span class="sxs-lookup"><span data-stu-id="2a44a-135">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="2a44a-136">问题</span><span class="sxs-lookup"><span data-stu-id="2a44a-136">Issue</span></span>

<span data-ttu-id="2a44a-137">有时，如果所用包内附具有无效签名的程序集或者包版本设置有“DateTime”贴标，这会导致包自动还原操作无限循环 (dotnet/project-system#1457)。</span><span class="sxs-lookup"><span data-stu-id="2a44a-137">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="2a44a-138">解决方法</span><span class="sxs-lookup"><span data-stu-id="2a44a-138">Workaround</span></span>

<span data-ttu-id="2a44a-139">目前没有解决方法。</span><span class="sxs-lookup"><span data-stu-id="2a44a-139">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="2a44a-140">NuGet 4.4 RTM 时间框架中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="2a44a-140">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="2a44a-141">[NuGet 4.3 RTM 发行说明](../release-notes/nuget-4.3-RTM.md)- 列出了 NuGet 4.3 RTM 已修复的所有问题</span><span class="sxs-lookup"><span data-stu-id="2a44a-141">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="2a44a-142">特征</span><span class="sxs-lookup"><span data-stu-id="2a44a-142">Features</span></span>

- <span data-ttu-id="2a44a-143">支持 PMC 和 NuGet PM UI 方案中的轻量型解决方案加载 - [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="2a44a-143">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="2a44a-144">msbuild 包目标应具有公共挂钩，以用于在其本身之前运行用户目标 - [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="2a44a-144">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="2a44a-145">功能：将 dependencyVersion 开关添加到 nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="2a44a-145">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="2a44a-146">uap10.0.TODO.0 应映射到适用于 NuGet 的 .NET Standard 2.0 - [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="2a44a-146">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="2a44a-147">支持使用 msbuild/t:restore 的 Visual Studio 生成工具 SKU - [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="2a44a-147">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="2a44a-148">还原期间，如果需要适用于 .NET Standard 2.0 的 .NET 4.6.1 支持但尚未安装，则会出现错误 - [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="2a44a-148">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="2a44a-149">包 ID 前缀预留客户端 UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="2a44a-149">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="2a44a-150">提供本地化 nuget 组件以支持 dotnet.exe 本地化 - [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="2a44a-150">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="2a44a-151">Bug</span><span class="sxs-lookup"><span data-stu-id="2a44a-151">Bugs</span></span>

- <span data-ttu-id="2a44a-152">项目路径大小写不同可能导致还原丢失 PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="2a44a-152">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="2a44a-153">将带警告编号的错误代码移动到错误范围 - [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="2a44a-153">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="2a44a-154">未知 .NET Standard 版本与目标框架兼容时，出现误导性错误 - [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="2a44a-154">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="2a44a-155">测试文件的许可证混乱 - [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="2a44a-155">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="2a44a-156">EndToEnd 测试模板中缺少许可证标头 - [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="2a44a-156">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="2a44a-157">packages.config restore 显示错误为 NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="2a44a-157">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="2a44a-158">nuget.exe install 应在 mono 上具有 DisableParallelProcessing - [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="2a44a-158">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="2a44a-159">nuget.exe install 不正确地禁用缓存 - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="2a44a-159">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="2a44a-160">禁用 Restore 时，运行 packages.config 的还原命令的 VS 会显示不正确消息 - [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="2a44a-160">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="2a44a-161">VS；禁用 Restore 时，运行还原命令显示令人混乱的消息 - [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="2a44a-161">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="2a44a-162">缺少版本元数据时，GetRestoreDotnetCliToolsTask 失败 - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="2a44a-162">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="2a44a-163">dotnet</span><span class="sxs-lookup"><span data-stu-id="2a44a-163">dotnet</span></span>
  - <span data-ttu-id="2a44a-164">dotnetcore 添加包可从 csproj 清除空行 - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="2a44a-164">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="2a44a-165">NuGet.Config 中凭据设置的源名称要区分大小写 - [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="2a44a-165">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="2a44a-166">启用 GeneratePackageOnBuild 删除了包的整个历史记录 - [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="2a44a-166">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="2a44a-167">Restore 不会还原 mono.cecil 或 semver 包，但所有其他包都会还原。</span><span class="sxs-lookup"><span data-stu-id="2a44a-167">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="2a44a-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="2a44a-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="2a44a-169">错误和警告 - 源不可用时发生严重错误。</span><span class="sxs-lookup"><span data-stu-id="2a44a-169">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="2a44a-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="2a44a-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="2a44a-171">[DesignConsistency] NuGet 安装状态文本目前在深色主题方面看起来不正确。</span><span class="sxs-lookup"><span data-stu-id="2a44a-171">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="2a44a-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="2a44a-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="2a44a-173">解决方案中的更新包会对所有项目进行更新/安装 - [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="2a44a-173">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="2a44a-174">dotnet</span><span class="sxs-lookup"><span data-stu-id="2a44a-174">dotnet</span></span>
  - <span data-ttu-id="2a44a-175">根据 TargetFramework 与 TargetFrameworks，dotnetcore pack 的行为有所不同 - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="2a44a-175">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="2a44a-176">“工具”文件夹中包含的 DLL 引发警告 - [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="2a44a-176">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="2a44a-177">NuGet.ContentModel 将过多内存用于字符串操作 -[#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="2a44a-177">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="2a44a-178">对于 OSX，RuntimeEnvironmentHelper.IsLinux 返回 true - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="2a44a-178">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="2a44a-179">“dotnet 包”将 nuspec 置于 obj 下，而不是 obj\Debug 下 - [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="2a44a-179">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="2a44a-180">Nuget 极其缓慢的包升级 - [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="2a44a-180">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="2a44a-181">CPS 与尚未开启 LSL（轻量型解决方案还原）的较大型解决方案中的 Restore 不同步 - [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="2a44a-181">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="2a44a-182">SemVer 2.0 - 具有提供版本的 nuget pack 忽略元数据 (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="2a44a-182">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="2a44a-183">带版本号和 ExcludeVersion 标志的 Nuget.exe (3.+) 安装包不能将包更新到较新版本 - [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="2a44a-183">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="2a44a-184">顶级包违反约束时，Project.json restore 应发出警告 - [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="2a44a-184">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="2a44a-185">-ConfigFile 不在安装命令上设置自定义配置 - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="2a44a-185">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="2a44a-186">nuget.exe install 不遵循“-DisableParallelProcessing”开关 - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="2a44a-186">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="2a44a-187">DotNet.exe 或 msbuild.exe 仍在使用已禁用的源 - [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="2a44a-187">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="2a44a-188">修复在 LSL 方案中挂起 - [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="2a44a-188">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="2a44a-189">DCR</span><span class="sxs-lookup"><span data-stu-id="2a44a-189">DCRs</span></span>

- <span data-ttu-id="2a44a-190">nuget.exe install TargetFramework 支持 - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="2a44a-190">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="2a44a-191">添加不同的 msbuild 任务 UserAgent 字符串（netcore 与桌面 msbuild）- [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="2a44a-191">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="2a44a-192">PackagePathResolver.GetPackageDirectoryName 应为虚拟 - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="2a44a-192">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="2a44a-193">[DesignConsistency] 添加 NuGet 包时，消息混乱 - [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="2a44a-193">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="2a44a-194">[警告和错误] NoWarn 不通过 P2P 引用间接流动 - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="2a44a-194">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="2a44a-195">轻量级解决方案加载：PM UI、PMC 和 IV 的共同核心 - [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="2a44a-195">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="2a44a-196">轻量级解决方案加载：支持 - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="2a44a-196">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="2a44a-197">添加对 Visual Studio 触发的还原前 MSBuild 目标的支持 - [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="2a44a-197">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="2a44a-198">将公共目标添加到可使用 BeforeTargets 引用的 NuGet.targets - [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="2a44a-198">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="2a44a-199">包目标不能正确使用生成操作创建 contentFile - [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="2a44a-199">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="2a44a-200">RestoreOperationLogger.Do 会阻止线程池线程 - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="2a44a-200">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="2a44a-201">Docs</span><span class="sxs-lookup"><span data-stu-id="2a44a-201">Docs</span></span>

- <span data-ttu-id="2a44a-202">用于安装命令 DependencyVersion 和 Framework 标志的文档 - [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="2a44a-202">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="2a44a-203">文档中有关 NuGet 警告和错误的更新 - [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="2a44a-203">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="2a44a-204">4\.4 RTM 中已修复 GitHub 问题的链接</span><span class="sxs-lookup"><span data-stu-id="2a44a-204">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="2a44a-205">问题列表 1</span><span class="sxs-lookup"><span data-stu-id="2a44a-205">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="2a44a-206">问题列表 2</span><span class="sxs-lookup"><span data-stu-id="2a44a-206">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="2a44a-207">问题列表 3</span><span class="sxs-lookup"><span data-stu-id="2a44a-207">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
