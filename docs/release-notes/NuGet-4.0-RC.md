---
title: NuGet 4.0 RC 发行说明
description: NuGet 4.0 RC 的发行说明，包括已知问题、bug 修复、新增功能和 DCR。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 8124b11d0489a2c72ffcfdde28e8528c1da1f677
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="f1e77-103">NuGet 4.0 RC 发行说明</span><span class="sxs-lookup"><span data-stu-id="f1e77-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="f1e77-104">NuGet 3.5 RTM 发行说明</span><span class="sxs-lookup"><span data-stu-id="f1e77-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="f1e77-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) 重点增加了对 .NET Core 方案的支持，解决了主要客户反馈，并提高了各种方案的性能。</span><span class="sxs-lookup"><span data-stu-id="f1e77-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="f1e77-106">此版本引入了一些改进，如支持 PackageReference、作为 MSBuild 目标的 NuGet 命令、后台包还原等。</span><span class="sxs-lookup"><span data-stu-id="f1e77-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="f1e77-107">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="f1e77-107">Bug Fixes</span></span>

- <span data-ttu-id="f1e77-108">`dotnet pack --version-suffix foo` 中的行为更改 - [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="f1e77-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="f1e77-109">VS“15”计算机上的 nuget.exe restore 总是失败 - [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="f1e77-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="f1e77-110">.NET Core“文件”>“新建项目”在还原过程中应阻止生成 - [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="f1e77-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="f1e77-111">从 VS2015 迁移到 VS“15”的 ASP.NET Core Web 应用无法还原</span><span class="sxs-lookup"><span data-stu-id="f1e77-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="f1e77-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="f1e77-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="f1e77-113">[测试失败]“jQuery 验证”包无法通过 PM UI 卸载 - [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="f1e77-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="f1e77-114">将包安装到 UWP `project.json` 时，还应还原父项目 - [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="f1e77-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="f1e77-115">修改 NuGet 目标以将包源记录为高度详细而非普通 - [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="f1e77-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="f1e77-116">dotnet</span><span class="sxs-lookup"><span data-stu-id="f1e77-116">dotnet</span></span>
  - <span data-ttu-id="f1e77-117">dotnetcore pack3 应默认包含 XML 文档 - [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="f1e77-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="f1e77-118">当第一个为无包的源且选中全部源时，从 UI 的批量更新失败 - [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="f1e77-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="f1e77-119">Nuget pack 命令不包含所有文件 - [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="f1e77-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="f1e77-120">OOM 问题 - [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="f1e77-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="f1e77-121">资产文件的 ProjectFileDependencyGroups 部分应使用项目的库名称 - [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="f1e77-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="f1e77-122">“dotnet restore”和递归目录 - [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="f1e77-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="f1e77-123">Restore3 失败记录为警告而非错误 - [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="f1e77-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="f1e77-124">TFS 问题：“在工作区中找不到[文件]，或者你无权访问”- [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="f1e77-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="f1e77-125">在 VS 快速启动搜索框中键入“nuget <packagename>”，会保留“nuget ”前缀 - [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="f1e77-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="f1e77-126">System.Xml.XmlException：核心属性部分存在无法识别的根元素。</span><span class="sxs-lookup"><span data-stu-id="f1e77-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="f1e77-127">行：2，位置：2</span><span class="sxs-lookup"><span data-stu-id="f1e77-127">Line 2, position 2.</span></span><span data-ttu-id="f1e77-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="f1e77-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="f1e77-129">文本字段中具有转义 &lt; 或 &gt; 的 `.nuspec` 不再生成 - [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="f1e77-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="f1e77-130">nuget.exe delete 不会提示输入凭据（处于非交互模式）- [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="f1e77-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="f1e77-131">nuget.exe delete 警告本地源的 API 密钥（即使没有任何意义）- [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="f1e77-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="f1e77-132">安装 EF -pre 包时出现错误，体验不佳 - [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="f1e77-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="f1e77-133">在包管理器中更改选择后，Visual Studio 崩溃 - [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="f1e77-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="f1e77-134">dotnet</span><span class="sxs-lookup"><span data-stu-id="f1e77-134">dotnet</span></span>
  - <span data-ttu-id="f1e77-135">使用可变版本时，dotnetcore restore 在简单列表本地存储库上执行区分大小写的 ID 查找 - [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="f1e77-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="f1e77-136">对于 V2 源，nuget.exe delete 已被破坏 - [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="f1e77-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="f1e77-137">nuget.exe push timeout 需要更好的错误消息 - [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="f1e77-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="f1e77-138">不包含正确导入的工具还原失败且没有任何提示</span><span class="sxs-lookup"><span data-stu-id="f1e77-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="f1e77-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="f1e77-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="f1e77-140">即使从 nuget.org 进行安装，NuGet 也会在有专用源时提示输入凭据 - [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="f1e77-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="f1e77-141">ApplicationInsights 2.0 包已列出但尚不存在 - [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="f1e77-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="f1e77-142">VS“15”预览 5 分支中的 UI 延迟 - [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="f1e77-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="f1e77-143">在针对 UWP 生成的过程中，首个 OnBuild 事件未还原 - [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="f1e77-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="f1e77-144">PowerShell5 中断 EntityFramework 安装</span><span class="sxs-lookup"><span data-stu-id="f1e77-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="f1e77-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="f1e77-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="f1e77-146">将源添加到详细的日志记录（考虑为 3.5）- [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="f1e77-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="f1e77-147">NoCache 参数在 nuget 客户端版本 3.4+ 中无效 - [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="f1e77-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="f1e77-148">当凭据提供程序在 VS 中加载失败时，请勿中断 NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="f1e77-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="f1e77-149">功能</span><span class="sxs-lookup"><span data-stu-id="f1e77-149">Features</span></span>

- <span data-ttu-id="f1e77-150">设置 CI 以运行 x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="f1e77-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="f1e77-151">自动还原 3/3：非阻止 UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="f1e77-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="f1e77-152">自动还原 2/3：在指定的计算机上进行后台还原 - [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="f1e77-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="f1e77-153">还原项目引用以匹配生成行为（递归）- [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="f1e77-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="f1e77-154">VS“15”中支持 DPL - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="f1e77-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="f1e77-155">将设置文件移动到 Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="f1e77-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="f1e77-156">生成的还原属性和目标需要跨目标参与支持 - [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="f1e77-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="f1e77-157">NuGet 还原支持 PackageTargetFallback（以前称为导入）- [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="f1e77-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="f1e77-158">ToolsRef 实现 - [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="f1e77-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="f1e77-159">RID 的 Restore3 - [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="f1e77-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="f1e77-160">支持添加/删除/更新 PackageRefs 的 NuGet UI - [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="f1e77-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="f1e77-161">自动还原 1/3：通过缓存项目还原信息实现指定 API - [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="f1e77-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="f1e77-162">[0] NuGet 还原任务和目标 - [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="f1e77-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="f1e77-163">[1] 在 MSBuild 中启用解决方案级别还原 - [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="f1e77-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="f1e77-164">在 Visual Studio 中支持凭据提供程序公共扩展性 - [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="f1e77-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="f1e77-165">递归 NuGet 还原 - [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="f1e77-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="f1e77-166">无法在 dev15 上加载 Microsoft.TeamFoundation.Client，对于 VS“15”预览，需要将 Microsoft.TeamFoundation.Client 版本更新为 15.0 - [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="f1e77-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="f1e77-167">无法在 VS“15”预览中将 C++ 包安装到 C++ UWP 项目 - [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="f1e77-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="f1e77-168">Nupkg 需要支持 \buildCrossTargeting\ 文件夹 - 并导入 `.targets` / `.props` 来跨越 MSBuild 范围目标</span><span class="sxs-lookup"><span data-stu-id="f1e77-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="f1e77-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="f1e77-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="f1e77-170">ToolsReference 设计 - [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="f1e77-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="f1e77-171">修复 NuGet UI 以支持使用 `.csproj` 中的 PackageReferences 进行还原 - [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="f1e77-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="f1e77-172">将清除缓存按钮添加到 VS 包管理器设置 - [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="f1e77-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="f1e77-173">DCR</span><span class="sxs-lookup"><span data-stu-id="f1e77-173">DCRs</span></span>

- <span data-ttu-id="f1e77-174">发生自动还原时，应阻止解决方案还原</span><span class="sxs-lookup"><span data-stu-id="f1e77-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="f1e77-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="f1e77-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="f1e77-176">从 NuGet 包管理器 UI 进行的 NetCore 安装将安装到每个 TFM，而不是该包支持的那个 TFM - [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="f1e77-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="f1e77-177">还原指定 API 还需要支持 DotNetCliToolsReferences</span><span class="sxs-lookup"><span data-stu-id="f1e77-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="f1e77-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="f1e77-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="f1e77-179">将我们的 VS“15”vsix 标记为 systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="f1e77-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="f1e77-180">从引用 MS.VS.Services.Client 迁移到 MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="f1e77-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="f1e77-181">应按还原在项目级别考虑 $(RestoreLegacyPackagesDirectory) - [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="f1e77-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="f1e77-182">使用单个 TargetFramework 还原到项目不得调整属性 - [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="f1e77-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="f1e77-183">dotnet</span><span class="sxs-lookup"><span data-stu-id="f1e77-183">dotnet</span></span>
  - <span data-ttu-id="f1e77-184">dotnetcore restore3 foo.csproj 应遵循 projectref 依赖项，同时还原那些依赖项。</span><span class="sxs-lookup"><span data-stu-id="f1e77-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="f1e77-185">如生成</span><span class="sxs-lookup"><span data-stu-id="f1e77-185">Like build.</span></span><span data-ttu-id="f1e77-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="f1e77-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="f1e77-187">“类型”：“平台”依赖项在锁定文件中表示为“类型”：“包”- [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="f1e77-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="f1e77-188">nuget.exe 详细模式应显示下载 URL - [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="f1e77-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="f1e77-189">将 NuGet xplat 移动到 Microsoft.NetCore.App 和 netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="f1e77-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="f1e77-190">推送 - 从命令行推送时，应该可以替代符号服务器 - [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="f1e77-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="f1e77-191">合并用于查找全局包路径的代码 - [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="f1e77-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="f1e77-192">需要一个比 suppressParent 更好的名称 - [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="f1e77-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="f1e77-193">决定用于 MSBuild 项目的`project.json` 依赖项名称 - [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="f1e77-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="f1e77-194">将 SemVer 2.0.0 支持添加到 NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="f1e77-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="f1e77-195">允许具有 `.targets` 的传递依赖项 NuPkgs 在 MSBuild 中可用 - [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="f1e77-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="f1e77-196">命令行中的 NuGet 还原明显慢于 VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="f1e77-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="f1e77-197">使包 ID 和版本比较不区分大小写 - [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="f1e77-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="f1e77-198">NoCache 选项不适用于基于 `packages.config` 的还原/安装 (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="f1e77-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="f1e77-199">FindPackageByIdResource 资源需要一个默认的缓存上下文和记录器 - [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="f1e77-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
