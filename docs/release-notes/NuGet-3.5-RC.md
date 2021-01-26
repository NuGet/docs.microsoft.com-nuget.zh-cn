---
title: 3.5 RC 发行说明
description: NuGet 3.5 RC 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780200"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="d9f72-103">NuGet 3.5 RC 发行说明</span><span class="sxs-lookup"><span data-stu-id="d9f72-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="d9f72-104">[NuGet 3.5-Beta2 发行说明](../release-notes/nuget-3.5-Beta2.md)  | [NuGet 3.5-RTM 发行说明](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="d9f72-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="d9f72-105">3.5 版本侧重于提高 NuGet 客户端的质量和性能。</span><span class="sxs-lookup"><span data-stu-id="d9f72-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="d9f72-106">此外，我们还提供了一些功能，如对 [后备文件夹](https://github.com/NuGet/Home/issues/2899)的支持、 [PackageType](https://github.com/NuGet/Home/issues/2476) 的支持 `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="d9f72-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="d9f72-107">问题列表</span><span class="sxs-lookup"><span data-stu-id="d9f72-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="d9f72-108">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="d9f72-108">Bug Fixes</span></span>

* <span data-ttu-id="d9f72-109">安装/还原包失败，出现 "包包含多个 `.nuspec` 文件"。</span><span class="sxs-lookup"><span data-stu-id="d9f72-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="d9f72-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="d9f72-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="d9f72-111">不管 #3203 如何，nuget 包都会强制将 `.tt` 文件添加到[](https://github.com/NuGet/Home/issues/3203) content 文件夹中</span><span class="sxs-lookup"><span data-stu-id="d9f72-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="d9f72-112">`project.json`如果 JSON 文件中没有 packOptions 和所有者，nuget 包 .csproj () 崩溃[#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="d9f72-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="d9f72-113">的 nuget 包 `project.json` 忽略 packOptions 标记，如摘要、作者、所有者等 [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="d9f72-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="d9f72-114">nuget 包忽略 `.nuspec` `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)的输出中的依赖关系</span><span class="sxs-lookup"><span data-stu-id="d9f72-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="d9f72-115">使用 rollback 更新多个包会使项目处于损坏状态- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="d9f72-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="d9f72-116">不会为 netstandard 项目添加 ContentFiles 下的任何项目- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="d9f72-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="d9f72-117">无法正确打包面向 .Net Standard 的库目标- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="d9f72-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="d9f72-118">文件-> 新项目-> 类库 (可移植) 项目在 VS2015 和 Dev15 中失败- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="d9f72-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="d9f72-119">NuGet 错误-1.0.0-\* 不是有效的版本字符串- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="d9f72-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="d9f72-120">Find-Package 无法显示但 Install-Package 工作- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="d9f72-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="d9f72-121">Dev15 上的 "安装包 jquery. 验证" 时出错- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="d9f72-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="d9f72-122">在使用 NuGet 版本3.5.0 的 VS 上安装 VS 2015 update 3 时出现错误- [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="d9f72-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="d9f72-123">程序包管理器 UI：更新包后不显示新版本- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="d9f72-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="d9f72-124">-ApiKey on delete 命令行在3.5.0 中未被读/发送- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="d9f72-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="d9f72-125">字符串不正确：包的稳定版本不应具有预发行依赖项。</span><span class="sxs-lookup"><span data-stu-id="d9f72-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="d9f72-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="d9f72-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="d9f72-127">创建 PCL (net46 和 windows 10) project 获取 NullRef 异常。</span><span class="sxs-lookup"><span data-stu-id="d9f72-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="d9f72-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="d9f72-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="d9f72-129">当 allowedVersions 约束限制更高版本时，Nuget 更新应提供信息性消息 [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="d9f72-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="d9f72-130">凭据插件已退出，出现错误-1/在将凭据提供程序与多个源一起使用时下载包- [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="d9f72-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="d9f72-131">nuget 包-缺少有关包依赖项的 Newtonsoft.Js- [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="d9f72-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="d9f72-132">Linux/MacOS 上的 ExecuteSynchronizedCore 中的 Bug + Mono- [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="d9f72-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="d9f72-133">VS 不支持 repositoryPath 中的环境变量 ( # A0) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="d9f72-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="d9f72-134">解决辅助功能问题- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="d9f72-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="d9f72-135">拒绝带有断字符配置文件的便携式框架。</span><span class="sxs-lookup"><span data-stu-id="d9f72-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="d9f72-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="d9f72-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="d9f72-137">NuGet 包管理器应当清楚地说明包详细信息中的选项列表不适用于 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="d9f72-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="d9f72-138">NuGet 3.3.0 更新失败，并出现 "a 附加约束 ..."在 packages.config 中定义可防止此操作。 '</span><span class="sxs-lookup"><span data-stu-id="d9f72-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="d9f72-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="d9f72-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="d9f72-140">从不存在的本地源安装包将引发虚假消息 [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="d9f72-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="d9f72-141">"Upgrade v" 筛选器显示违反版本约束的升级- [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="d9f72-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="d9f72-142">性能改进</span><span class="sxs-lookup"><span data-stu-id="d9f72-142">Performance Improvements</span></span>

* <span data-ttu-id="d9f72-143">性能：提高 ContentModel 目标框架分析- [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="d9f72-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="d9f72-144">性能：避免读取 `runtime.json` 没有 rid [#3150](https://github.com/NuGet/Home/issues/3150)的还原文件。</span><span class="sxs-lookup"><span data-stu-id="d9f72-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="d9f72-145">在 CI 计算机上，ASP.NET Web 应用程序的还原从15秒到3秒的缩短。</span><span class="sxs-lookup"><span data-stu-id="d9f72-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="d9f72-146">性能：程序包管理器控制台 init.ps1 加载时间 [#2956](https://github.com/NuGet/Home/issues/2956)。</span><span class="sxs-lookup"><span data-stu-id="d9f72-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="d9f72-147">在某些情况下，从132s 到数十的打开 PackageManagerConsole 的时间已改进。</span><span class="sxs-lookup"><span data-stu-id="d9f72-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="d9f72-148">解决 NuGet 更新中的 ReSharper 性能问题- [#3044](https://github.com/NuGet/Home/issues/3044)：在示例项目上，安装包的时间从140s 减少到68s。</span><span class="sxs-lookup"><span data-stu-id="d9f72-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="d9f72-149">DCR</span><span class="sxs-lookup"><span data-stu-id="d9f72-149">DCRs</span></span>

* <span data-ttu-id="d9f72-150">NuGet 需要让用户知道在基于 dotnet tfm 的 PCL 中升级/安装可能会导致问题 [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="d9f72-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="d9f72-151">为 project （tfm = "dotnet"）警告安装/升级失败- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="d9f72-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="d9f72-152">添加 netcoreapp11 和 netstandard17 支持- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="d9f72-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="d9f72-153">将 NuGet-Warning 标题内容打印到 nuget.exe 中的控制台 [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="d9f72-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="d9f72-154">将 AssemblyMetadata 特性用于 `.nuspec` 标记替换- [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="d9f72-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="d9f72-155">从锁定文件中删除锁定的属性- [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="d9f72-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="d9f72-156">不应在安装或更新 #2807 中使用符号包</span><span class="sxs-lookup"><span data-stu-id="d9f72-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="d9f72-157">功能</span><span class="sxs-lookup"><span data-stu-id="d9f72-157">Features</span></span>

* <span data-ttu-id="d9f72-158">支持备用包文件夹- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="d9f72-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="d9f72-159">设计和实现包类型的概念以支持工具包- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="d9f72-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="d9f72-160">用于获取全局包文件夹的路径的 API- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="d9f72-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="d9f72-161">本机包更新支持- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="d9f72-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
