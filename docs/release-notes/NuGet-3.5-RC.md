---
title: 3.5 RC 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.5 RC 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548533"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="bc689-103">NuGet 3.5 RC 发行说明</span><span class="sxs-lookup"><span data-stu-id="bc689-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="bc689-104">[NuGet 3.5 Beta2 发行说明](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5 的 RTM 发行说明](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="bc689-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="bc689-105">3.5 版本侧重于提高质量和性能的 NuGet 客户端。</span><span class="sxs-lookup"><span data-stu-id="bc689-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="bc689-106">此外，我们对发布了一些功能，例如，为支持[Fallback 文件夹](https://github.com/NuGet/Home/issues/2899)， [PackageType](https://github.com/NuGet/Home/issues/2476)中支持`.nuspec`和的详细信息。</span><span class="sxs-lookup"><span data-stu-id="bc689-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="bc689-107">问题列表</span><span class="sxs-lookup"><span data-stu-id="bc689-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="bc689-108">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="bc689-108">Bug Fixes</span></span>

* <span data-ttu-id="bc689-109">包的安装/还原失败，出现"包包含多个`.nuspec`文件。"</span><span class="sxs-lookup"><span data-stu-id="bc689-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="bc689-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="bc689-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="bc689-111">nuget 包添加了强制`.tt`文件复制到 content 文件夹，无论什么- [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="bc689-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="bc689-112">nuget 包 csproj (使用`project.json`) 如果没有 packOptions 和在 JSON 文件的所有者将崩溃[#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="bc689-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="bc689-113">适用于 nuget 包`project.json`将忽略摘要、 作者和所有者等-packOptions 标记[#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="bc689-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="bc689-114">nuget pack 忽略输出中的依赖关系`.nuspec`有关`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="bc689-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="bc689-115">使用回滚更新多个包使项目处于中断状态- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="bc689-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="bc689-116">任何下的内容文件不会添加为 netstandard 项目- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="bc689-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="bc689-117">无法打包库面向.Net 标准正确- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="bc689-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="bc689-118">文件-> 新建项目-> 类库 （可移植） 项目失败 VS2015 和 Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="bc689-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="bc689-119">NuGet 错误-1.0.0-\* 不是有效的版本字符串- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="bc689-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="bc689-120">查找包失败到显示，但安装包的工作原理- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="bc689-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="bc689-121">错误时在 dev15-上的"安装包 jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="bc689-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="bc689-122">当已安装的 VS 2015 更新 3 使用的 NuGet 版本 3.5.0 错误发生的对和[#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="bc689-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="bc689-123">包管理器 UI： 在更新包后不会显示新版本- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="bc689-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="bc689-124">-ApiKey delete 命令行上不读取/发送中 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="bc689-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="bc689-125">不正确的字符串： 稳定的发行版的包不应具有在预发行版的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="bc689-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="bc689-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="bc689-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="bc689-127">正在创建 PCL （net46 和 windows 10） 项目 get NullRef 异常。</span><span class="sxs-lookup"><span data-stu-id="bc689-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="bc689-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="bc689-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="bc689-129">Nuget 更新的 allowedVersions 约束的限制更高版本时应提供信息性消息[#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="bc689-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="bc689-130">凭据插件已退出，错误为-1 / 错误下载包时使用多个源的凭据提供程序[# 2885年](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="bc689-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="bc689-131">nuget 包-缺少 Newtonsoft.Json 包依赖项- [# 2876年](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="bc689-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="bc689-132">在 Linux/MacOS + Mono-ExecuteSynchronizedCore bug [# 2860年](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="bc689-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="bc689-133">与不支持在 repositoryPath 中环境变量 （nuget.exe 执行）- [# 2763年](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="bc689-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="bc689-134">修复可访问性问题- [# 2745年](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="bc689-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="bc689-135">可移植框架使用连字符的由配置文件将被拒绝。</span><span class="sxs-lookup"><span data-stu-id="bc689-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="bc689-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="bc689-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="bc689-137">NuGet 包管理器应使它清楚该选项列表中包详细信息不适用于`project.json`  -  [# 2665年](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="bc689-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="bc689-138">NuGet 3.3.0 更新失败，出现...更多约束中定义 packages.config 阻止此操作。</span><span class="sxs-lookup"><span data-stu-id="bc689-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="bc689-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="bc689-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="bc689-140">从本地源不存在，则会引发错误的邮件-安装包[# 1674年](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="bc689-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="bc689-141">"升级版提供"筛选器将显示与版本约束的冲突的升级[# 1094年](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="bc689-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="bc689-142">性能改进</span><span class="sxs-lookup"><span data-stu-id="bc689-142">Performance Improvements</span></span>

* <span data-ttu-id="bc689-143">性能： 改善 ContentModel 目标框架分析- [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="bc689-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="bc689-144">性能： 避免读取`runtime.json`不具有 Rid 还原的文件[#3150](https://github.com/NuGet/Home/issues/3150)。</span><span class="sxs-lookup"><span data-stu-id="bc689-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="bc689-145">CI 计算机上的 ASP.NET Web 应用程序减少了超过 15 秒到 3 秒的示例中进行还原。</span><span class="sxs-lookup"><span data-stu-id="bc689-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="bc689-146">性能： 程序包管理器控制台 init.ps1 加载时间[# 2956年](https://github.com/NuGet/Home/issues/2956)。</span><span class="sxs-lookup"><span data-stu-id="bc689-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="bc689-147">时间才能打开 PackageManagerConsole 改进了在某些情况下从 132s年到 10 秒。</span><span class="sxs-lookup"><span data-stu-id="bc689-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="bc689-148">解决在 NuGet 更新-ReSharper 性能问题[#3044](https://github.com/NuGet/Home/issues/3044)： 上一个示例项目，安装包所花的时间减少从 140s年到 68s。</span><span class="sxs-lookup"><span data-stu-id="bc689-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="bc689-149">DCR</span><span class="sxs-lookup"><span data-stu-id="bc689-149">DCRs</span></span>

* <span data-ttu-id="bc689-150">NuGet 需要让用户知道，在基于 dotnet tfm 升级/安装 PCL 可能会导致问题- [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="bc689-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="bc689-151">错误安装/升级带 tfm 的项目，则发出警告 ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="bc689-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="bc689-152">添加了 netcoreapp11 和 netstandard17 支持- [# 2998年](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="bc689-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="bc689-153">打印 NuGet 警告标头内容，控制台中 nuget.exe- [# 2934年](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="bc689-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="bc689-154">利用 AssemblyMetadata 属性`.nuspec`令牌替换- [# 2851年](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="bc689-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="bc689-155">从锁定文件中的删除锁定的属性[# 2379年](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="bc689-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="bc689-156">符号包应不曾经用于安装或更新 #2807</span><span class="sxs-lookup"><span data-stu-id="bc689-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="bc689-157">功能</span><span class="sxs-lookup"><span data-stu-id="bc689-157">Features</span></span>

* <span data-ttu-id="bc689-158">支持回退的包文件夹- [# 2899年](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="bc689-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="bc689-159">设计和实现包类型的概念，以支持工具的包- [# 2476年](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="bc689-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="bc689-160">若要获取的全局包文件夹的路径的 API [# 2403年](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="bc689-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="bc689-161">本机包更新支持- [# 1291年](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="bc689-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
