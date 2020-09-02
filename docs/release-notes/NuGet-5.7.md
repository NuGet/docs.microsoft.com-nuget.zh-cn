---
title: NuGet 5.7 发行说明
description: NuGet 5.7 的发行说明，包括新功能、bug 修复和 Dcr。
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 6c821091983ab0b5d59b759e1ee9930cf449fd9d
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89364149"
---
# <a name="nuget-57-release-notes"></a><span data-ttu-id="a21ab-103">NuGet 5.7 发行说明</span><span class="sxs-lookup"><span data-stu-id="a21ab-103">NuGet 5.7 Release Notes</span></span>

<span data-ttu-id="a21ab-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="a21ab-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="a21ab-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="a21ab-105">NuGet version</span></span> | <span data-ttu-id="a21ab-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="a21ab-106">Available in Visual Studio version</span></span> | <span data-ttu-id="a21ab-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a21ab-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="a21ab-108">**5.7.0**</span><span class="sxs-lookup"><span data-stu-id="a21ab-108">**5.7.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="a21ab-109">Visual Studio 2019 版本 16.7</span><span class="sxs-lookup"><span data-stu-id="a21ab-109">Visual Studio 2019 version 16.7</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="a21ab-110">[3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="a21ab-110">[3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="a21ab-111"><sup>1</sup> 与带有 .net Core 工作负载的 Visual Studio 2019 一起安装</span><span class="sxs-lookup"><span data-stu-id="a21ab-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-57"></a><span data-ttu-id="a21ab-112">摘要：5.7 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="a21ab-112">Summary: What's New in 5.7</span></span>

### <a name="features-added-in-this-release"></a><span data-ttu-id="a21ab-113">此版本中添加的功能</span><span class="sxs-lookup"><span data-stu-id="a21ab-113">Features added in this release</span></span>

* <span data-ttu-id="a21ab-114">添加了对 NuGet 包引用的 extern 别名支持- [#4989](https://github.com/NuGet/Home/issues/4989)</span><span class="sxs-lookup"><span data-stu-id="a21ab-114">Added extern alias support for NuGet package references - [#4989](https://github.com/NuGet/Home/issues/4989)</span></span>

* <span data-ttu-id="a21ab-115">通过允许它们共享数据源并减少 resfreshing，在已安装和更新选项卡之间进行切换更快 [#8294](https://github.com/NuGet/Home/issues/8294)</span><span class="sxs-lookup"><span data-stu-id="a21ab-115">Made switching between Installed and Updates tabs faster by allowing them to share a data source and reducing resfreshing - [#8294](https://github.com/NuGet/Home/issues/8294)</span></span>

* <span data-ttu-id="a21ab-116">通过调用 MSBuild 静态图形 api ( # A0) - [#9644](https://github.com/NuGet/Home/issues/9644) ，提高还原速度</span><span class="sxs-lookup"><span data-stu-id="a21ab-116">Make restore faster - speed up evaluations by calling MSBuild Static Graph apis (dotnet.exe) - [#9644](https://github.com/NuGet/Home/issues/9644)</span></span>

* <span data-ttu-id="a21ab-117">为 PackageReference 项目添加了 Visual Studio 部分还原 (无操作 + +) - [#9513](https://github.com/NuGet/Home/issues/9513)</span><span class="sxs-lookup"><span data-stu-id="a21ab-117">Added Visual Studio partial restore for PackageReference projects (no-op++) - [#9513](https://github.com/NuGet/Home/issues/9513)</span></span>

* <span data-ttu-id="a21ab-118">对于每个 HTTP 请求返回的结果数超过请求数的结果包源，Visual Studio 包管理器 UI 会出现故障的情况。</span><span class="sxs-lookup"><span data-stu-id="a21ab-118">Visual Studio Package Manager UI will crash less often when searching misbehaving package sources that return more than the requested number of results per HTTP request.</span></span><span data-ttu-id="a21ab-119"> - [#8478](https://github.com/NuGet/Home/issues/8478)</span><span class="sxs-lookup"><span data-stu-id="a21ab-119"> - [#8478](https://github.com/NuGet/Home/issues/8478)</span></span>

* <span data-ttu-id="a21ab-120">添加了[#9236](https://github.com/NuGet/Home/issues/9236) VS PackageVersion 中非 SDK 样式项目的信息集成</span><span class="sxs-lookup"><span data-stu-id="a21ab-120">Added integration of PackageVersion information for non-SDK style projects in VS restore  - [#9236](https://github.com/NuGet/Home/issues/9236)</span></span>

* <span data-ttu-id="a21ab-121">添加了对 nuget.exe 更新的支持 `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)</span><span class="sxs-lookup"><span data-stu-id="a21ab-121">Added support for nuget.exe update `-self -Source` https://feed - [#1783](https://github.com/NuGet/Home/issues/1783)</span></span>

* <span data-ttu-id="a21ab-122">在%APPDATA%\NuGet 目录中添加了对多个配置文件的支持- [#9394](https://github.com/NuGet/Home/issues/9394)</span><span class="sxs-lookup"><span data-stu-id="a21ab-122">Added support for multiple config files in %APPDATA%\NuGet directory - [#9394](https://github.com/NuGet/Home/issues/9394)</span></span>

* <span data-ttu-id="a21ab-123">DeterministicSourcePaths 现在会将 NuGet 源包纳入帐户 [#9431](https://github.com/NuGet/Home/issues/9431)</span><span class="sxs-lookup"><span data-stu-id="a21ab-123">DeterministicSourcePaths now takes NuGet source packages into account - [#9431](https://github.com/NuGet/Home/issues/9431)</span></span>

* <span data-ttu-id="a21ab-124">添加了 INuGetProjectService GetInstalledPackagesAsync 扩展性 API- [#9702](https://github.com/NuGet/Home/issues/9702)</span><span class="sxs-lookup"><span data-stu-id="a21ab-124">Added INuGetProjectService.GetInstalledPackagesAsync extensibility API - [#9702](https://github.com/NuGet/Home/issues/9702)</span></span>

* <span data-ttu-id="a21ab-125">添加了互操作 API 以枚举回退文件夹，而无需解决方案/项目- [#9395](https://github.com/NuGet/Home/issues/9395)</span><span class="sxs-lookup"><span data-stu-id="a21ab-125">Added interop API to enumerate fallback folders without requiring a solution/project - [#9395](https://github.com/NuGet/Home/issues/9395)</span></span>

* <span data-ttu-id="a21ab-126">添加 `latest` 了 `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)的选项</span><span class="sxs-lookup"><span data-stu-id="a21ab-126">Added `latest` option for `-MSBuildVersion` - [#8808](https://github.com/NuGet/Home/issues/8808)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="a21ab-127">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="a21ab-127">Issues fixed in this release</span></span>

<span data-ttu-id="a21ab-128">**漏洞**</span><span class="sxs-lookup"><span data-stu-id="a21ab-128">**Bugs:**</span></span>

* <span data-ttu-id="a21ab-129">在 dotnet CLI 还原中，启动凭据插件时，如果 `DOTNET_HOST_PATH`  未定义环境变量，则在系统路径上尝试使用 DOTNET CLI。</span><span class="sxs-lookup"><span data-stu-id="a21ab-129">In a dotnet CLI restore, when launching credential plugins, try the dotnet CLI on the system path if the `DOTNET_HOST_PATH`  environment variable is not defined.</span></span><span data-ttu-id="a21ab-130"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span><span class="sxs-lookup"><span data-stu-id="a21ab-130"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span></span>

* <span data-ttu-id="a21ab-131">nuget.exe 规范使用版权 YYYY 的硬编码文本而不是 #8696 生成版权标记 `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)</span><span class="sxs-lookup"><span data-stu-id="a21ab-131">nuget.exe spec generates a copyright tag with hard-coded text of Copyright YYYY Instead of `$copyright$` - [#8696](https://github.com/NuGet/Home/issues/8696)</span></span>

* <span data-ttu-id="a21ab-132">如果更改了程序集名称，则在使用 assemblyinfo 时，如果更改了程序集名称，NuGet.exe 将引发在 .csproj 包中忽略占位符和特性[#4234](https://github.com/NuGet/Home/issues/4234)的异常 "</span><span class="sxs-lookup"><span data-stu-id="a21ab-132">NuGet.exe throws exception 'authors required' during pack of a csproj ignoring placeholders and assemblyinfo attributes if the assembly name is changed - [#4234](https://github.com/NuGet/Home/issues/4234)</span></span>

* <span data-ttu-id="a21ab-133">HttpRequestMessage 会多次重复使用，而 SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)不支持</span><span class="sxs-lookup"><span data-stu-id="a21ab-133">HttpRequestMessage gets reused multiple times which is not supported with the SocketHttpHandler - [#8661](https://github.com/NuGet/Home/issues/8661)</span></span>

* <span data-ttu-id="a21ab-134">NuGet。索引5.6.0 预览版3和更高版本使用不同的公钥令牌- [#9481](https://github.com/NuGet/Home/issues/9481)</span><span class="sxs-lookup"><span data-stu-id="a21ab-134">NuGet.Indexing 5.6.0 preview 3 and later use a different public key token - [#9481](https://github.com/NuGet/Home/issues/9481)</span></span>

* <span data-ttu-id="a21ab-135">在创建 NuGet 包期间遵循 TreatWarningsAsErrors- [#7404](https://github.com/NuGet/Home/issues/7404)</span><span class="sxs-lookup"><span data-stu-id="a21ab-135">Honor TreatWarningsAsErrors during NuGet Package creation - [#7404](https://github.com/NuGet/Home/issues/7404)</span></span>

* <span data-ttu-id="a21ab-136">[CPVM]多个 p2p 项目的假包降级- [#9549](https://github.com/NuGet/Home/issues/9549)</span><span class="sxs-lookup"><span data-stu-id="a21ab-136">[CPVM] Spurious package downgrades for multiple p2p projects  - [#9549](https://github.com/NuGet/Home/issues/9549)</span></span>

* <span data-ttu-id="a21ab-137">"浏览" 选项卡并不与搜索框左对齐- [#9559](https://github.com/NuGet/Home/issues/9559)</span><span class="sxs-lookup"><span data-stu-id="a21ab-137">The “Browse” tab is not aligned left with search box - [#9559](https://github.com/NuGet/Home/issues/9559)</span></span>

* <span data-ttu-id="a21ab-138">安装的版本与安装了多个版本的包 id 的解决方案级别 PM UI 中的嵌入图标不一致- [#9321](https://github.com/NuGet/Home/issues/9321)</span><span class="sxs-lookup"><span data-stu-id="a21ab-138">The installed version is inconsistent with the embedded icon in the solution level PM UI for one package id with multiple versions installed - [#9321](https://github.com/NuGet/Home/issues/9321)</span></span>

* <span data-ttu-id="a21ab-139">泄漏： PartCreationPolicy (CreationPolicy) SolutionRestoreManager RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)</span><span class="sxs-lookup"><span data-stu-id="a21ab-139">Leak: PartCreationPolicy(CreationPolicy.NonShared) NuGet.SolutionRestoreManager.RestoreOperationLogger - [#9595](https://github.com/NuGet/Home/issues/9595)</span></span>

* <span data-ttu-id="a21ab-140">避免在无操作还原中读取资产文件- [#9693](https://github.com/NuGet/Home/issues/9693)</span><span class="sxs-lookup"><span data-stu-id="a21ab-140">Avoid reading the assets file in no-op restores - [#9693](https://github.com/NuGet/Home/issues/9693)</span></span>

* <span data-ttu-id="a21ab-141">NuGet 不支持从搜索中获取版本的下载计数 [#9086](https://github.com/NuGet/Home/issues/9086)</span><span class="sxs-lookup"><span data-stu-id="a21ab-141">NuGet.Protocol does not support getting a version's download count from search - [#9086](https://github.com/NuGet/Home/issues/9086)</span></span>

* <span data-ttu-id="a21ab-142">减少 JObject 依赖项，从而提高 PackageMetadataResourceV3 的内存性能 [#9719](https://github.com/NuGet/Home/issues/9719)</span><span class="sxs-lookup"><span data-stu-id="a21ab-142">Improve memory performance of PackageMetadataResourceV3 by reducing the JObject dependencies - [#9719](https://github.com/NuGet/Home/issues/9719)</span></span>

<span data-ttu-id="a21ab-143">**设计更改请求：**</span><span class="sxs-lookup"><span data-stu-id="a21ab-143">**Design change requests:**</span></span>

* <span data-ttu-id="a21ab-144">`<owners>`当元素为冗余时将其取消[#5134](https://github.com/NuGet/Home/issues/5134)</span><span class="sxs-lookup"><span data-stu-id="a21ab-144">Suppressed the `<owners>` element when it is redundant - [#5134](https://github.com/NuGet/Home/issues/5134)</span></span>

* <span data-ttu-id="a21ab-145">将 IntervalTrackers 记录为 ETW 事件- [#9593](https://github.com/NuGet/Home/issues/9593)</span><span class="sxs-lookup"><span data-stu-id="a21ab-145">Log IntervalTrackers as ETW events - [#9593](https://github.com/NuGet/Home/issues/9593)</span></span>

* <span data-ttu-id="a21ab-146">在 restore 上添加了信息性消息，通知 CPVM 用户该功能处于预览中- [#9340](https://github.com/NuGet/Home/issues/9340)</span><span class="sxs-lookup"><span data-stu-id="a21ab-146">Added an informational message on restore to inform CPVM users that the feature is in preview - [#9340](https://github.com/NuGet/Home/issues/9340)</span></span>

* <span data-ttu-id="a21ab-147">填充资产文件中解决方案资源管理器包/项目可传递依赖项- [#9580](https://github.com/NuGet/Home/issues/9580)</span><span class="sxs-lookup"><span data-stu-id="a21ab-147">Populate Solution Explorer package/project transitive dependencies from assets file - [#9580](https://github.com/NuGet/Home/issues/9580)</span></span>

* <span data-ttu-id="a21ab-148">"已安装的包" 选项卡不应将包列表分页- [#6995](https://github.com/NuGet/Home/issues/6995)</span><span class="sxs-lookup"><span data-stu-id="a21ab-148">Installed packages tab shouldn't paginate the packages list - [#6995](https://github.com/NuGet/Home/issues/6995)</span></span>

<span data-ttu-id="a21ab-149">**[此版本中已修复的所有问题的列表-5。7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**</span><span class="sxs-lookup"><span data-stu-id="a21ab-149">**[List of all issues fixed in this release - 5.7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**</span></span>

### <a name="community-contributions"></a><span data-ttu-id="a21ab-150">社区参与</span><span class="sxs-lookup"><span data-stu-id="a21ab-150">Community contributions</span></span>

<span data-ttu-id="a21ab-151">感谢所有有助于使此 NuGet 版本非常出色的参与者！</span><span class="sxs-lookup"><span data-stu-id="a21ab-151">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="a21ab-152">谁</span><span class="sxs-lookup"><span data-stu-id="a21ab-152">Who</span></span>|<span data-ttu-id="a21ab-153">Pr</span><span class="sxs-lookup"><span data-stu-id="a21ab-153">PRs</span></span>|<span data-ttu-id="a21ab-154">问题</span><span class="sxs-lookup"><span data-stu-id="a21ab-154">Issues</span></span>|
|----|----|----|
|[<span data-ttu-id="a21ab-155">campersau</span><span class="sxs-lookup"><span data-stu-id="a21ab-155">campersau</span></span>](https://github.com/campersau)|<span data-ttu-id="a21ab-156">[3433](https://github.com/NuGet/NuGet.Client/pull/3433)、 [3120](https://github.com/NuGet/NuGet.Client/pull/3120)</span><span class="sxs-lookup"><span data-stu-id="a21ab-156">[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)</span></span>|<span data-ttu-id="a21ab-157">NuGet 不支持从搜索中获取版本的下载计数 [#9086](https://github.com/NuGet/Home/issues/9086)</span><span class="sxs-lookup"><span data-stu-id="a21ab-157">NuGet.Protocol does not support getting a version's download count from search - [#9086](https://github.com/NuGet/Home/issues/9086)</span></span> </br><span data-ttu-id="a21ab-158">HttpRequestMessage 会多次重复使用，而 SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)不支持</span><span class="sxs-lookup"><span data-stu-id="a21ab-158">HttpRequestMessage gets reused multiple times which is not supported with the SocketHttpHandler - [#8661](https://github.com/NuGet/Home/issues/8661)</span></span>|
|[<span data-ttu-id="a21ab-159">Joseph Musser (jnm2) </span><span class="sxs-lookup"><span data-stu-id="a21ab-159">Joseph Musser (jnm2)</span></span>](https://github.com/jnm2)|[<span data-ttu-id="a21ab-160">3241</span><span class="sxs-lookup"><span data-stu-id="a21ab-160">3241</span></span>](https://github.com/NuGet/NuGet.Client/pull/3241)|<span data-ttu-id="a21ab-161">`<owners>`当元素为冗余时将其取消[#5134](https://github.com/NuGet/Home/issues/5134)</span><span class="sxs-lookup"><span data-stu-id="a21ab-161">Suppressed the `<owners>` element when it is redundant - [#5134](https://github.com/NuGet/Home/issues/5134)</span></span>|
|[<span data-ttu-id="a21ab-162">Volodymyr Shkolka (BlackGad) </span><span class="sxs-lookup"><span data-stu-id="a21ab-162">Volodymyr Shkolka (BlackGad)</span></span>](https://github.com/BlackGad)|[<span data-ttu-id="a21ab-163">3273</span><span class="sxs-lookup"><span data-stu-id="a21ab-163">3273</span></span>](https://github.com/NuGet/NuGet.Client/pull/3273)|<span data-ttu-id="a21ab-164">NuGet 无法从需要客户端证书的 HTTPS 源还原- [#5773](https://github.com/NuGet/Home/issues/5773)</span><span class="sxs-lookup"><span data-stu-id="a21ab-164">NuGet cannot restore from HTTPS sources that require Client Certificates - [#5773](https://github.com/NuGet/Home/issues/5773)</span></span>|
|[<span data-ttu-id="a21ab-165">Marius Ungureanu (Therzok) </span><span class="sxs-lookup"><span data-stu-id="a21ab-165">Marius Ungureanu (Therzok)</span></span>](https://github.com/Therzok)|[<span data-ttu-id="a21ab-166">3357</span><span class="sxs-lookup"><span data-stu-id="a21ab-166">3357</span></span>](https://github.com/NuGet/NuGet.Client/pull/3357)|<span data-ttu-id="a21ab-167">HttpSourceAuthenticationHandler SemaphoreSlim 未来的校对- [#9463](https://github.com/NuGet/Home/issues/9463)</span><span class="sxs-lookup"><span data-stu-id="a21ab-167">HttpSourceAuthenticationHandler SemaphoreSlim future proofing - [#9463](https://github.com/NuGet/Home/issues/9463)</span></span>|
|[<span data-ttu-id="a21ab-168">Sunner (SuNNjek) </span><span class="sxs-lookup"><span data-stu-id="a21ab-168">Sunner (SuNNjek)</span></span>](https://github.com/SuNNjek)|[<span data-ttu-id="a21ab-169">3088</span><span class="sxs-lookup"><span data-stu-id="a21ab-169">3088</span></span>](https://github.com/NuGet/NuGet.Client/pull/3088)|<span data-ttu-id="a21ab-170">nuget.exe 规范使用版权 YYYY 的硬编码文本而不是 #8696 生成版权标记 `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)</span><span class="sxs-lookup"><span data-stu-id="a21ab-170">nuget.exe spec generates a copyright tag with hard-coded text of Copyright YYYY Instead of `$copyright$` - [#8696](https://github.com/NuGet/Home/issues/8696)</span></span>|
|[<span data-ttu-id="a21ab-171">Marc-olivier Spinelli (marc-olivier-Spinelli) </span><span class="sxs-lookup"><span data-stu-id="a21ab-171">Olivier Spinelli (olivier-spinelli)</span></span>](https://github.com/olivier-spinelli)|[<span data-ttu-id="a21ab-172">3335</span><span class="sxs-lookup"><span data-stu-id="a21ab-172">3335</span></span>](https://github.com/NuGet/NuGet.Client/pull/3335)|<span data-ttu-id="a21ab-173">在 dotnet CLI 还原中，启动凭据插件时，如果 `DOTNET_HOST_PATH`  未定义环境变量，则在系统路径上尝试使用 DOTNET CLI。</span><span class="sxs-lookup"><span data-stu-id="a21ab-173">In a dotnet CLI restore, when launching credential plugins, try the dotnet CLI on the system path if the `DOTNET_HOST_PATH`  environment variable is not defined.</span></span><span data-ttu-id="a21ab-174"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span><span class="sxs-lookup"><span data-stu-id="a21ab-174"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span></span>|
|[<span data-ttu-id="a21ab-175">goyzhang</span><span class="sxs-lookup"><span data-stu-id="a21ab-175">goyzhang</span></span>](https://github.com/goyzhang)|[<span data-ttu-id="a21ab-176">3370</span><span class="sxs-lookup"><span data-stu-id="a21ab-176">3370</span></span>](https://github.com/NuGet/NuGet.Client/pull/3370)|<span data-ttu-id="a21ab-177">添加 `latest` 了 `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)的选项</span><span class="sxs-lookup"><span data-stu-id="a21ab-177">Added `latest` option for `-MSBuildVersion` - [#8808](https://github.com/NuGet/Home/issues/8808)</span></span>|
