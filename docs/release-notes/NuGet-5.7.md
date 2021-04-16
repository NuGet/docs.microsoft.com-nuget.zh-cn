---
title: NuGet 5.7 发行说明
description: NuGet 5.7 的发行说明，包括新功能、bug 修复和 Dcr。
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 58ab481f0c6a6cb5549c269788170b8c3ff6002f
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508782"
---
# <a name="nuget-57-release-notes"></a><span data-ttu-id="af945-103">NuGet 5.7 发行说明</span><span class="sxs-lookup"><span data-stu-id="af945-103">NuGet 5.7 Release Notes</span></span>

<span data-ttu-id="af945-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="af945-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="af945-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="af945-105">NuGet version</span></span> | <span data-ttu-id="af945-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="af945-106">Available in Visual Studio version</span></span> | <span data-ttu-id="af945-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="af945-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="af945-108">**5.7.0**</span><span class="sxs-lookup"><span data-stu-id="af945-108">**5.7.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="af945-109">Visual Studio 2019 版本 16.7</span><span class="sxs-lookup"><span data-stu-id="af945-109">Visual Studio 2019 version 16.7</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="af945-110">[3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="af945-110">[3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |
| [<span data-ttu-id="af945-111">**5.7.1**</span><span class="sxs-lookup"><span data-stu-id="af945-111">**5.7.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="af945-112">Visual Studio 2019 版本 16.7</span><span class="sxs-lookup"><span data-stu-id="af945-112">Visual Studio 2019 version 16.7</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="af945-113">[3.1.408](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="af945-113">[3.1.408](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="af945-114"><sup>1</sup> 与带有 .net Core 工作负载的 Visual Studio 2019 一起安装</span><span class="sxs-lookup"><span data-stu-id="af945-114"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-57"></a><span data-ttu-id="af945-115">摘要：5.7 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="af945-115">Summary: What's New in 5.7</span></span>

### <a name="features-added-in-this-release"></a><span data-ttu-id="af945-116">此版本中添加的功能</span><span class="sxs-lookup"><span data-stu-id="af945-116">Features added in this release</span></span>

* <span data-ttu-id="af945-117">添加了对 NuGet 包引用的 extern 别名支持- [#4989](https://github.com/NuGet/Home/issues/4989)</span><span class="sxs-lookup"><span data-stu-id="af945-117">Added extern alias support for NuGet package references - [#4989](https://github.com/NuGet/Home/issues/4989)</span></span>

* <span data-ttu-id="af945-118">通过允许它们共享数据源并减少 resfreshing，在已安装和更新选项卡之间进行切换更快 [#8294](https://github.com/NuGet/Home/issues/8294)</span><span class="sxs-lookup"><span data-stu-id="af945-118">Made switching between Installed and Updates tabs faster by allowing them to share a data source and reducing resfreshing - [#8294](https://github.com/NuGet/Home/issues/8294)</span></span>

* <span data-ttu-id="af945-119">通过)  (dotnet.exe 调用 MSBuild 静态 Graph api，提高还原速度： [#9644](https://github.com/NuGet/Home/issues/9644)</span><span class="sxs-lookup"><span data-stu-id="af945-119">Make restore faster - speed up evaluations by calling MSBuild Static Graph apis (dotnet.exe) - [#9644](https://github.com/NuGet/Home/issues/9644)</span></span>

* <span data-ttu-id="af945-120">为 PackageReference 项目添加了 Visual Studio 部分还原 (无操作 + +) - [#9513](https://github.com/NuGet/Home/issues/9513)</span><span class="sxs-lookup"><span data-stu-id="af945-120">Added Visual Studio partial restore for PackageReference projects (no-op++) - [#9513](https://github.com/NuGet/Home/issues/9513)</span></span>

* <span data-ttu-id="af945-121">对于每个 HTTP 请求返回的结果数超过请求数的结果包源，Visual Studio 包管理器 UI 会出现故障的情况。</span><span class="sxs-lookup"><span data-stu-id="af945-121">Visual Studio Package Manager UI will crash less often when searching misbehaving package sources that return more than the requested number of results per HTTP request.</span></span><span data-ttu-id="af945-122"> - [#8478](https://github.com/NuGet/Home/issues/8478)</span><span class="sxs-lookup"><span data-stu-id="af945-122"> - [#8478](https://github.com/NuGet/Home/issues/8478)</span></span>

* <span data-ttu-id="af945-123">添加了[#9236](https://github.com/NuGet/Home/issues/9236) VS PackageVersion 中非 SDK 样式项目的信息集成</span><span class="sxs-lookup"><span data-stu-id="af945-123">Added integration of PackageVersion information for non-SDK style projects in VS restore  - [#9236](https://github.com/NuGet/Home/issues/9236)</span></span>

* <span data-ttu-id="af945-124">添加了对 nuget.exe 更新的支持 `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)</span><span class="sxs-lookup"><span data-stu-id="af945-124">Added support for nuget.exe update `-self -Source` https://feed - [#1783](https://github.com/NuGet/Home/issues/1783)</span></span>

* <span data-ttu-id="af945-125">在%APPDATA%\NuGet 目录中添加了对多个配置文件的支持- [#9394](https://github.com/NuGet/Home/issues/9394)</span><span class="sxs-lookup"><span data-stu-id="af945-125">Added support for multiple config files in %APPDATA%\NuGet directory - [#9394](https://github.com/NuGet/Home/issues/9394)</span></span>

* <span data-ttu-id="af945-126">DeterministicSourcePaths 现在会将 NuGet 源包纳入帐户 [#9431](https://github.com/NuGet/Home/issues/9431)</span><span class="sxs-lookup"><span data-stu-id="af945-126">DeterministicSourcePaths now takes NuGet source packages into account - [#9431](https://github.com/NuGet/Home/issues/9431)</span></span>

* <span data-ttu-id="af945-127">添加了 INuGetProjectService GetInstalledPackagesAsync 扩展性 API- [#9702](https://github.com/NuGet/Home/issues/9702)</span><span class="sxs-lookup"><span data-stu-id="af945-127">Added INuGetProjectService.GetInstalledPackagesAsync extensibility API - [#9702](https://github.com/NuGet/Home/issues/9702)</span></span>

* <span data-ttu-id="af945-128">添加了互操作 API 以枚举回退文件夹，而无需解决方案/项目- [#9395](https://github.com/NuGet/Home/issues/9395)</span><span class="sxs-lookup"><span data-stu-id="af945-128">Added interop API to enumerate fallback folders without requiring a solution/project - [#9395](https://github.com/NuGet/Home/issues/9395)</span></span>

* <span data-ttu-id="af945-129">添加 `latest` 了 `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)的选项</span><span class="sxs-lookup"><span data-stu-id="af945-129">Added `latest` option for `-MSBuildVersion` - [#8808](https://github.com/NuGet/Home/issues/8808)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="af945-130">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="af945-130">Issues fixed in this release</span></span>

<span data-ttu-id="af945-131">**漏洞**</span><span class="sxs-lookup"><span data-stu-id="af945-131">**Bugs:**</span></span>

* <span data-ttu-id="af945-132">在 dotnet CLI 还原中，启动凭据插件时，如果 `DOTNET_HOST_PATH`  未定义环境变量，则在系统路径上尝试使用 DOTNET CLI。</span><span class="sxs-lookup"><span data-stu-id="af945-132">In a dotnet CLI restore, when launching credential plugins, try the dotnet CLI on the system path if the `DOTNET_HOST_PATH`  environment variable is not defined.</span></span><span data-ttu-id="af945-133"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span><span class="sxs-lookup"><span data-stu-id="af945-133"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span></span>

* <span data-ttu-id="af945-134">nuget.exe 规范使用版权 YYYY 的硬编码文本而不是 #8696 生成版权标记 `$copyright$`  -  [](https://github.com/NuGet/Home/issues/8696)</span><span class="sxs-lookup"><span data-stu-id="af945-134">nuget.exe spec generates a copyright tag with hard-coded text of Copyright YYYY Instead of `$copyright$` - [#8696](https://github.com/NuGet/Home/issues/8696)</span></span>

* <span data-ttu-id="af945-135">如果更改了程序集名称，则在使用 assemblyinfo 时，如果更改了程序集名称，NuGet.exe 将引发在 .csproj 包中忽略占位符和特性[#4234](https://github.com/NuGet/Home/issues/4234)的异常 "</span><span class="sxs-lookup"><span data-stu-id="af945-135">NuGet.exe throws exception 'authors required' during pack of a csproj ignoring placeholders and assemblyinfo attributes if the assembly name is changed - [#4234](https://github.com/NuGet/Home/issues/4234)</span></span>

* <span data-ttu-id="af945-136">HttpRequestMessage 会多次重复使用，而 SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)不支持</span><span class="sxs-lookup"><span data-stu-id="af945-136">HttpRequestMessage gets reused multiple times which is not supported with the SocketHttpHandler - [#8661](https://github.com/NuGet/Home/issues/8661)</span></span>

* <span data-ttu-id="af945-137">NuGet。索引5.6.0 预览版3和更高版本使用不同的公钥令牌- [#9481](https://github.com/NuGet/Home/issues/9481)</span><span class="sxs-lookup"><span data-stu-id="af945-137">NuGet.Indexing 5.6.0 preview 3 and later use a different public key token - [#9481](https://github.com/NuGet/Home/issues/9481)</span></span>

* <span data-ttu-id="af945-138">在创建 NuGet 包期间遵循 TreatWarningsAsErrors- [#7404](https://github.com/NuGet/Home/issues/7404)</span><span class="sxs-lookup"><span data-stu-id="af945-138">Honor TreatWarningsAsErrors during NuGet Package creation - [#7404](https://github.com/NuGet/Home/issues/7404)</span></span>

* <span data-ttu-id="af945-139">[CPVM]多个 p2p 项目的假包降级- [#9549](https://github.com/NuGet/Home/issues/9549)</span><span class="sxs-lookup"><span data-stu-id="af945-139">[CPVM] Spurious package downgrades for multiple p2p projects  - [#9549](https://github.com/NuGet/Home/issues/9549)</span></span>

* <span data-ttu-id="af945-140">"浏览" 选项卡并不与搜索框左对齐- [#9559](https://github.com/NuGet/Home/issues/9559)</span><span class="sxs-lookup"><span data-stu-id="af945-140">The “Browse” tab is not aligned left with search box - [#9559](https://github.com/NuGet/Home/issues/9559)</span></span>

* <span data-ttu-id="af945-141">安装的版本与安装了多个版本的包 id 的解决方案级别 PM UI 中的嵌入图标不一致- [#9321](https://github.com/NuGet/Home/issues/9321)</span><span class="sxs-lookup"><span data-stu-id="af945-141">The installed version is inconsistent with the embedded icon in the solution level PM UI for one package id with multiple versions installed - [#9321](https://github.com/NuGet/Home/issues/9321)</span></span>

* <span data-ttu-id="af945-142">泄漏： PartCreationPolicy (CreationPolicy) SolutionRestoreManager RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)</span><span class="sxs-lookup"><span data-stu-id="af945-142">Leak: PartCreationPolicy(CreationPolicy.NonShared) NuGet.SolutionRestoreManager.RestoreOperationLogger - [#9595](https://github.com/NuGet/Home/issues/9595)</span></span>

* <span data-ttu-id="af945-143">避免在无操作还原中读取资产文件- [#9693](https://github.com/NuGet/Home/issues/9693)</span><span class="sxs-lookup"><span data-stu-id="af945-143">Avoid reading the assets file in no-op restores - [#9693](https://github.com/NuGet/Home/issues/9693)</span></span>

* <span data-ttu-id="af945-144">NuGet 不支持从搜索中获取版本的下载计数 [#9086](https://github.com/NuGet/Home/issues/9086)</span><span class="sxs-lookup"><span data-stu-id="af945-144">NuGet.Protocol does not support getting a version's download count from search - [#9086](https://github.com/NuGet/Home/issues/9086)</span></span>

* <span data-ttu-id="af945-145">减少 JObject 依赖项，从而提高 PackageMetadataResourceV3 的内存性能 [#9719](https://github.com/NuGet/Home/issues/9719)</span><span class="sxs-lookup"><span data-stu-id="af945-145">Improve memory performance of PackageMetadataResourceV3 by reducing the JObject dependencies - [#9719](https://github.com/NuGet/Home/issues/9719)</span></span>

<span data-ttu-id="af945-146">**设计更改请求：**</span><span class="sxs-lookup"><span data-stu-id="af945-146">**Design change requests:**</span></span>

* <span data-ttu-id="af945-147">`<owners>`当元素为冗余时将其取消[#5134](https://github.com/NuGet/Home/issues/5134)</span><span class="sxs-lookup"><span data-stu-id="af945-147">Suppressed the `<owners>` element when it is redundant - [#5134](https://github.com/NuGet/Home/issues/5134)</span></span>

* <span data-ttu-id="af945-148">将 IntervalTrackers 记录为 ETW 事件- [#9593](https://github.com/NuGet/Home/issues/9593)</span><span class="sxs-lookup"><span data-stu-id="af945-148">Log IntervalTrackers as ETW events - [#9593](https://github.com/NuGet/Home/issues/9593)</span></span>

* <span data-ttu-id="af945-149">在 restore 上添加了信息性消息，通知 CPVM 用户该功能处于预览中- [#9340](https://github.com/NuGet/Home/issues/9340)</span><span class="sxs-lookup"><span data-stu-id="af945-149">Added an informational message on restore to inform CPVM users that the feature is in preview - [#9340](https://github.com/NuGet/Home/issues/9340)</span></span>

* <span data-ttu-id="af945-150">填充资产文件中解决方案资源管理器包/项目可传递依赖项- [#9580](https://github.com/NuGet/Home/issues/9580)</span><span class="sxs-lookup"><span data-stu-id="af945-150">Populate Solution Explorer package/project transitive dependencies from assets file - [#9580](https://github.com/NuGet/Home/issues/9580)</span></span>

* <span data-ttu-id="af945-151">"已安装的包" 选项卡不应将包列表分页- [#6995](https://github.com/NuGet/Home/issues/6995)</span><span class="sxs-lookup"><span data-stu-id="af945-151">Installed packages tab shouldn't paginate the packages list - [#6995](https://github.com/NuGet/Home/issues/6995)</span></span>

<span data-ttu-id="af945-152">**[此版本中已修复的所有问题的列表-5。7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**</span><span class="sxs-lookup"><span data-stu-id="af945-152">**[List of all issues fixed in this release - 5.7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**</span></span>

### <a name="community-contributions"></a><span data-ttu-id="af945-153">社区参与</span><span class="sxs-lookup"><span data-stu-id="af945-153">Community contributions</span></span>

<span data-ttu-id="af945-154">感谢所有有助于使此 NuGet 版本非常出色的参与者！</span><span class="sxs-lookup"><span data-stu-id="af945-154">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="af945-155">谁</span><span class="sxs-lookup"><span data-stu-id="af945-155">Who</span></span>|<span data-ttu-id="af945-156">Pr</span><span class="sxs-lookup"><span data-stu-id="af945-156">PRs</span></span>|<span data-ttu-id="af945-157">问题</span><span class="sxs-lookup"><span data-stu-id="af945-157">Issues</span></span>|
|----|----|----|
|[<span data-ttu-id="af945-158">campersau</span><span class="sxs-lookup"><span data-stu-id="af945-158">campersau</span></span>](https://github.com/campersau)|<span data-ttu-id="af945-159">[3433](https://github.com/NuGet/NuGet.Client/pull/3433)、 [3120](https://github.com/NuGet/NuGet.Client/pull/3120)</span><span class="sxs-lookup"><span data-stu-id="af945-159">[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)</span></span>|<span data-ttu-id="af945-160">NuGet 不支持从搜索中获取版本的下载计数 [#9086](https://github.com/NuGet/Home/issues/9086)</span><span class="sxs-lookup"><span data-stu-id="af945-160">NuGet.Protocol does not support getting a version's download count from search - [#9086](https://github.com/NuGet/Home/issues/9086)</span></span> </br><span data-ttu-id="af945-161">HttpRequestMessage 会多次重复使用，而 SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)不支持</span><span class="sxs-lookup"><span data-stu-id="af945-161">HttpRequestMessage gets reused multiple times which is not supported with the SocketHttpHandler - [#8661](https://github.com/NuGet/Home/issues/8661)</span></span>|
|[<span data-ttu-id="af945-162">Joseph Musser (jnm2) </span><span class="sxs-lookup"><span data-stu-id="af945-162">Joseph Musser (jnm2)</span></span>](https://github.com/jnm2)|[<span data-ttu-id="af945-163">3241</span><span class="sxs-lookup"><span data-stu-id="af945-163">3241</span></span>](https://github.com/NuGet/NuGet.Client/pull/3241)|<span data-ttu-id="af945-164">`<owners>`当元素为冗余时将其取消[#5134](https://github.com/NuGet/Home/issues/5134)</span><span class="sxs-lookup"><span data-stu-id="af945-164">Suppressed the `<owners>` element when it is redundant - [#5134](https://github.com/NuGet/Home/issues/5134)</span></span>|
|[<span data-ttu-id="af945-165">Volodymyr Shkolka (BlackGad) </span><span class="sxs-lookup"><span data-stu-id="af945-165">Volodymyr Shkolka (BlackGad)</span></span>](https://github.com/BlackGad)|[<span data-ttu-id="af945-166">3273</span><span class="sxs-lookup"><span data-stu-id="af945-166">3273</span></span>](https://github.com/NuGet/NuGet.Client/pull/3273)|<span data-ttu-id="af945-167">NuGet 无法从需要客户端证书的 HTTPS 源还原- [#5773](https://github.com/NuGet/Home/issues/5773)</span><span class="sxs-lookup"><span data-stu-id="af945-167">NuGet cannot restore from HTTPS sources that require Client Certificates - [#5773](https://github.com/NuGet/Home/issues/5773)</span></span>|
|[<span data-ttu-id="af945-168">Marius Ungureanu (Therzok) </span><span class="sxs-lookup"><span data-stu-id="af945-168">Marius Ungureanu (Therzok)</span></span>](https://github.com/Therzok)|[<span data-ttu-id="af945-169">3357</span><span class="sxs-lookup"><span data-stu-id="af945-169">3357</span></span>](https://github.com/NuGet/NuGet.Client/pull/3357)|<span data-ttu-id="af945-170">HttpSourceAuthenticationHandler SemaphoreSlim 未来的校对- [#9463](https://github.com/NuGet/Home/issues/9463)</span><span class="sxs-lookup"><span data-stu-id="af945-170">HttpSourceAuthenticationHandler SemaphoreSlim future proofing - [#9463](https://github.com/NuGet/Home/issues/9463)</span></span>|
|[<span data-ttu-id="af945-171">Sunner (SuNNjek) </span><span class="sxs-lookup"><span data-stu-id="af945-171">Sunner (SuNNjek)</span></span>](https://github.com/SuNNjek)|[<span data-ttu-id="af945-172">3088</span><span class="sxs-lookup"><span data-stu-id="af945-172">3088</span></span>](https://github.com/NuGet/NuGet.Client/pull/3088)|<span data-ttu-id="af945-173">nuget.exe 规范使用版权 YYYY 的硬编码文本而不是 #8696 生成版权标记 `$copyright$`  -  [](https://github.com/NuGet/Home/issues/8696)</span><span class="sxs-lookup"><span data-stu-id="af945-173">nuget.exe spec generates a copyright tag with hard-coded text of Copyright YYYY Instead of `$copyright$` - [#8696](https://github.com/NuGet/Home/issues/8696)</span></span>|
|[<span data-ttu-id="af945-174">Marc-olivier Spinelli (marc-olivier-Spinelli) </span><span class="sxs-lookup"><span data-stu-id="af945-174">Olivier Spinelli (olivier-spinelli)</span></span>](https://github.com/olivier-spinelli)|[<span data-ttu-id="af945-175">3335</span><span class="sxs-lookup"><span data-stu-id="af945-175">3335</span></span>](https://github.com/NuGet/NuGet.Client/pull/3335)|<span data-ttu-id="af945-176">在 dotnet CLI 还原中，启动凭据插件时，如果 `DOTNET_HOST_PATH`  未定义环境变量，则在系统路径上尝试使用 DOTNET CLI。</span><span class="sxs-lookup"><span data-stu-id="af945-176">In a dotnet CLI restore, when launching credential plugins, try the dotnet CLI on the system path if the `DOTNET_HOST_PATH`  environment variable is not defined.</span></span><span data-ttu-id="af945-177"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span><span class="sxs-lookup"><span data-stu-id="af945-177"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span></span>|
|[<span data-ttu-id="af945-178">goyzhang</span><span class="sxs-lookup"><span data-stu-id="af945-178">goyzhang</span></span>](https://github.com/goyzhang)|[<span data-ttu-id="af945-179">3370</span><span class="sxs-lookup"><span data-stu-id="af945-179">3370</span></span>](https://github.com/NuGet/NuGet.Client/pull/3370)|<span data-ttu-id="af945-180">添加 `latest` 了 `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)的选项</span><span class="sxs-lookup"><span data-stu-id="af945-180">Added `latest` option for `-MSBuildVersion` - [#8808](https://github.com/NuGet/Home/issues/8808)</span></span>|

## <a name="summary-whats-new-in-571"></a><span data-ttu-id="af945-181">摘要：5.7.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="af945-181">Summary: What's New in 5.7.1</span></span>

* <span data-ttu-id="af945-182">扩展 nupkg 文件以包含安装源- [#10354](https://github.com/NuGet/Home/issues/10354)</span><span class="sxs-lookup"><span data-stu-id="af945-182">Extend the .nupkg.metadata file to include the installation source - [#10354](https://github.com/NuGet/Home/issues/10354)</span></span>

* <span data-ttu-id="af945-183">在提取) 期间 (还原日志记录期间记录包- [#10384](https://github.com/NuGet/Home/issues/10384)</span><span class="sxs-lookup"><span data-stu-id="af945-183">Log package contenthash during restore logging (during extraction) - [#10384](https://github.com/NuGet/Home/issues/10384)</span></span>

* <span data-ttu-id="af945-184">如果按正常的详细级别还原，请记录正在从中还原包的源 [#10461](https://github.com/NuGet/Home/issues/10461)</span><span class="sxs-lookup"><span data-stu-id="af945-184">When restoring at normal verbosity, log which source a package is being restored from - [#10461](https://github.com/NuGet/Home/issues/10461)</span></span>

<span data-ttu-id="af945-185">**[此版本中已修复的所有问题的列表-5.7。1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f5724f84579cc29a79ee)**</span><span class="sxs-lookup"><span data-stu-id="af945-185">**[List of all issues fixed in this release - 5.7.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f5724f84579cc29a79ee)**</span></span>

<span data-ttu-id="af945-186">**[此版本中的提交列表-5.7。1](https://github.com/NuGet/NuGet.Client/compare/80512866a2c127e52ce3e86fd803fff77e9b9b52...5.7.1.4)**</span><span class="sxs-lookup"><span data-stu-id="af945-186">**[List of commits in this release - 5.7.1](https://github.com/NuGet/NuGet.Client/compare/80512866a2c127e52ce3e86fd803fff77e9b9b52...5.7.1.4)**</span></span>
