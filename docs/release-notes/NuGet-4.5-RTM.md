---
title: NuGet 4.5 RTM 发行说明
description: NuGet 4.5 RTM 的发行说明，包括已知问题、bug 修复、新增功能和 DCR。
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 1d04c508d029a6d92bbd480fe3bd7dc14727970e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="0266b-103">NuGet 4.5 RTM 发行说明</span><span class="sxs-lookup"><span data-stu-id="0266b-103">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="0266b-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 附带有 [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe)。</span><span class="sxs-lookup"><span data-stu-id="0266b-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="0266b-105">已知问题</span><span class="sxs-lookup"><span data-stu-id="0266b-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="0266b-106">使用 .NET Framework 和 NuGet 的 .NET Standard 2.0 的问题</span><span class="sxs-lookup"><span data-stu-id="0266b-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="0266b-107">.NET Standard 及其工具旨在使面向 .NET Framework 4.6.1 的项目可使用面向 .NET Standard 2.0 或更早版本的 NuGet 包和项目。</span><span class="sxs-lookup"><span data-stu-id="0266b-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="0266b-108">[本文档](https://github.com/dotnet/standard/issues/481)总结了该方案相关问题、解决问题的计划以及可使用当前工具状态部署的变通方法。</span><span class="sxs-lookup"><span data-stu-id="0266b-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="0266b-109">无法使用 NuGet 包管理器查看、添加或更新 DotNetCLITools</span><span class="sxs-lookup"><span data-stu-id="0266b-109">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="0266b-110">问题</span><span class="sxs-lookup"><span data-stu-id="0266b-110">Issue</span></span>

<span data-ttu-id="0266b-111">NuGet 包管理器不显示，且不允许添加/更新 DotNetCLITools。</span><span class="sxs-lookup"><span data-stu-id="0266b-111">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="0266b-112">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="0266b-112">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="0266b-113">解决方法</span><span class="sxs-lookup"><span data-stu-id="0266b-113">Workaround</span></span>

<span data-ttu-id="0266b-114">必须在项目文件中手动编辑 DotNetCLIToolReferences。</span><span class="sxs-lookup"><span data-stu-id="0266b-114">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="0266b-115">对目标框架版本重定目标可能会导致 Intellisense 不完整</span><span class="sxs-lookup"><span data-stu-id="0266b-115">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="0266b-116">问题</span><span class="sxs-lookup"><span data-stu-id="0266b-116">Issue</span></span>

<span data-ttu-id="0266b-117">在 Visual Studio 中对目标框架版本重定目标可能会导致 Intellisense 不完整。</span><span class="sxs-lookup"><span data-stu-id="0266b-117">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="0266b-118">将 PackageReferences 用作包管理器格式时可能出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="0266b-118">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="0266b-119">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="0266b-119">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="0266b-120">解决方法</span><span class="sxs-lookup"><span data-stu-id="0266b-120">Workaround</span></span>

<span data-ttu-id="0266b-121">手动进行还原。</span><span class="sxs-lookup"><span data-stu-id="0266b-121">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="0266b-122">.NET Core 项目中的某个包内附具有无效签名的程序集，该包可触发还原操作无限循环</span><span class="sxs-lookup"><span data-stu-id="0266b-122">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="0266b-123">问题</span><span class="sxs-lookup"><span data-stu-id="0266b-123">Issue</span></span>

<span data-ttu-id="0266b-124">有时，如果所用包内附具有无效签名的程序集或者包版本设置有“DateTime”贴标，这会导致包自动还原操作无限循环 [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457)。</span><span class="sxs-lookup"><span data-stu-id="0266b-124">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="0266b-125">解决方法</span><span class="sxs-lookup"><span data-stu-id="0266b-125">Workaround</span></span>

<span data-ttu-id="0266b-126">目前没有解决方法。</span><span class="sxs-lookup"><span data-stu-id="0266b-126">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="0266b-127">NuGet 4.5 RTM 时间框架中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="0266b-127">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="0266b-128">有关 NuGet 4.4 RTM 中已修复问题的信息，请参阅[NuGet 4.4 RTM 发行说明](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="0266b-128">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="0266b-129">功能</span><span class="sxs-lookup"><span data-stu-id="0266b-129">Features</span></span>

- <span data-ttu-id="0266b-130">禁用符号包的自动推送 - [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="0266b-130">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="0266b-131">Bug</span><span class="sxs-lookup"><span data-stu-id="0266b-131">Bugs</span></span>

- <span data-ttu-id="0266b-132">[回归] 在 15.5p1 中，Portable0.0 被跳过 - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="0266b-132">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="0266b-133">还原后包中的资产丢失 - [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="0266b-133">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="0266b-134">插件凭据提供程序不支持包含空格的 URI - [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="0266b-134">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="0266b-135">如果包无法还原，应在输出中打印错误，即使最低详细级别为“ON”- [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="0266b-135">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="0266b-136">dotnet</span><span class="sxs-lookup"><span data-stu-id="0266b-136">dotnet</span></span>
  - <span data-ttu-id="0266b-137">解决方案级别的 dotnetcore restore 不遵循 ProjectReference，且 ReferenceOutputAssembly 为 false，导致随机生成失败 - [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="0266b-137">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="0266b-138">PMC 中的自动完成无法与对象方法正确协作 -[#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="0266b-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="0266b-139">使用 Visual Studio 2015 工具集时 nuget.exe 还原失败 - [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="0266b-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="0266b-140">在 vs2017 中实例化 perf - pmc 成本高昂 - [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="0266b-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="0266b-141">慢速连接时获取依赖项信息速度缓慢 - [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="0266b-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="0266b-142">如果多个包共享通用的依赖项，带 -RemoveDependencies 的 uninstall-package 将失败 - [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="0266b-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="0266b-143">完成 NuGet.Core.nupkg 以便发布 - [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="0266b-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="0266b-144">将 -IncludeProjectReferences 用于 csproj + project.json 时，NuGet 包会解析目录名称中的依赖项 ID - [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="0266b-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="0266b-145">“NuGet.ProxyCache”的类型初始值设定项引发异常 - [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="0266b-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="0266b-146">使用 kudu 时的 nuget 还原性能问题 - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="0266b-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="0266b-147">搜索超出注册 blob 时，UI 客户端无法显示任何错误或警告 - [# 2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="0266b-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="0266b-148">Get-Packages -Updates 生成不正确的查询 - [# 2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="0266b-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="0266b-149">4.5 RTM 中已修复 GitHub 问题的链接</span><span class="sxs-lookup"><span data-stu-id="0266b-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="0266b-150">问题列表</span><span class="sxs-lookup"><span data-stu-id="0266b-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
