---
title: NuGet 1.0 和1.1 发行说明
description: NuGet 1.1 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdd4bad54b08d956dbfdaf54220971492fd3ab02
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777214"
---
# <a name="nuget-10-and-11-release-notes"></a><span data-ttu-id="e7eb2-103">NuGet 1.0 和1.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="e7eb2-103">NuGet 1.0 and 1.1 Release Notes</span></span>

[<span data-ttu-id="e7eb2-104">NuGet 1.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="e7eb2-104">NuGet 1.2 Release Notes</span></span>](../release-notes/nuget-1.2.md)

<span data-ttu-id="e7eb2-105">NuGet 1.0 于2011年1月13日发布。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-105">NuGet 1.0 was released on January 13, 2011.</span></span>  <span data-ttu-id="e7eb2-106">NuGet 1.1 于2011年2月12日发布。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-106">NuGet 1.1 was released on February 12, 2011.</span></span>

## <a name="overview"></a><span data-ttu-id="e7eb2-107">概述</span><span class="sxs-lookup"><span data-stu-id="e7eb2-107">Overview</span></span>

<span data-ttu-id="e7eb2-108">本文档包含根据主要预览版进行分组的各种版本的 NuGet 1.0 发行说明。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-108">This document contains the release notes for the various releases of NuGet 1.0 grouped according to major preview release.</span></span>

<span data-ttu-id="e7eb2-109">NuGet 包含以下组件：</span><span class="sxs-lookup"><span data-stu-id="e7eb2-109">NuGet includes the following components:</span></span>

* <span data-ttu-id="e7eb2-110">*NuGet. .vsix* \*，其中包括：</span><span class="sxs-lookup"><span data-stu-id="e7eb2-110">*NuGet.Tools.vsix* \* which consists of:</span></span>
  * <span data-ttu-id="e7eb2-111">在 Visual Studio 中的 "**添加库包" 对话框** 中，用于浏览和安装包。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-111">**Add Library Package Dialog** \* Dialog within Visual Studio used to browse and install packages.</span></span>
  * <span data-ttu-id="e7eb2-112">Visual Studio 中的 **包管理器控制台**\* 基于 Powershell 的控制台。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-112">**Package Manager Console** \* Powershell based console within Visual Studio.</span></span>
* <span data-ttu-id="e7eb2-113">*NuGet 命令行工具* \* 工具，用于创建 (，并最终发布) 包。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-113">*NuGet Command Line Tool* \* Tool used to create (and eventually publish) packages.</span></span>

<span data-ttu-id="e7eb2-114">NuGet 工具 Visual Studio *扩展 ()* 需要：</span><span class="sxs-lookup"><span data-stu-id="e7eb2-114">The NuGet Tools Visual Studio Extension (*NuGet.Tools.vsix*) requires:</span></span>

* <span data-ttu-id="e7eb2-115">Visual Studio 2010 或 Visual Web Developer 2010 Express。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-115">Visual Studio 2010 or Visual Web Developer 2010 Express.</span></span>

<span data-ttu-id="e7eb2-116">NuGet 命令行工具需要：</span><span class="sxs-lookup"><span data-stu-id="e7eb2-116">The NuGet Command Line Tool requires:</span></span>

* <span data-ttu-id="e7eb2-117">.NET Framework 版本4</span><span class="sxs-lookup"><span data-stu-id="e7eb2-117">.NET Framework Version 4</span></span>

## <a name="installation"></a><span data-ttu-id="e7eb2-118">安装</span><span class="sxs-lookup"><span data-stu-id="e7eb2-118">Installation</span></span>

<span data-ttu-id="e7eb2-119">使用此 [最新版本](http://nuget.codeplex.com/releases/view/52018)：</span><span class="sxs-lookup"><span data-stu-id="e7eb2-119">To use this [latest release](http://nuget.codeplex.com/releases/view/52018):</span></span>

* <span data-ttu-id="e7eb2-120">首先卸载旧版本。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-120">First uninstall your older build.</span></span> <span data-ttu-id="e7eb2-121">需要以管理员身份运行 VS 才能执行此操作。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-121">You need to run VS as administrator to do this.</span></span>
* <span data-ttu-id="e7eb2-122">删除所有现有源。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-122">Remove all the existing feeds that you have.</span></span>
* <span data-ttu-id="e7eb2-123">添加指向的新源 <https://go.microsoft.com/fwlink/?LinkId=206669> 。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-123">Add a new feed pointing to <https://go.microsoft.com/fwlink/?LinkId=206669>.</span></span>

## <a name="nuget-11"></a><span data-ttu-id="e7eb2-124">NuGet 1.1</span><span class="sxs-lookup"><span data-stu-id="e7eb2-124">NuGet 1.1</span></span>

<span data-ttu-id="e7eb2-125">[可在此处找到](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)此版本中已修复问题的列表</span><span class="sxs-lookup"><span data-stu-id="e7eb2-125">The list of issues fixed in this release [can be found here](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)</span></span>

## <a name="nuget-10-rtm"></a><span data-ttu-id="e7eb2-126">NuGet 1.0 RTM</span><span class="sxs-lookup"><span data-stu-id="e7eb2-126">NuGet 1.0 RTM</span></span>

<span data-ttu-id="e7eb2-127">自 RC 以来，为 RTM 修复了一个问题。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-127">One issue was fixed for RTM since the RC.</span></span>

* [<span data-ttu-id="e7eb2-128">问题474：删除包会影响解决方案中的所有项目</span><span class="sxs-lookup"><span data-stu-id="e7eb2-128">Issue 474: Removing Packages Affects All Project In Solution</span></span>](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a><span data-ttu-id="e7eb2-129">候选发布版本</span><span class="sxs-lookup"><span data-stu-id="e7eb2-129">Release Candidate</span></span>

<span data-ttu-id="e7eb2-130">自 CTP 2 起，此候选发布版中的更改如下所述。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-130">The following are the changes made in this Release Candidate since CTP 2.</span></span> <span data-ttu-id="e7eb2-131">请访问问题跟踪程序，查看完整的错误列表。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-131">Visit the Issue Tracker to see the full list of bugs.</span></span>

* [<span data-ttu-id="e7eb2-132">从控制台更新包不会更新依赖项。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-132">Updating Package from Console does not update dependencies.</span></span>](http://nuget.codeplex.com/workitem/443)
* [<span data-ttu-id="e7eb2-133">添加包提取 bin not (CTP1) 的包引用 </span><span class="sxs-lookup"><span data-stu-id="e7eb2-133">Adding package picks up bin not package reference (CTP1)</span></span>](http://nuget.codeplex.com/workitem/442)
* [<span data-ttu-id="e7eb2-134">更新包会保留损坏的引用</span><span class="sxs-lookup"><span data-stu-id="e7eb2-134">Updating a package leaves broken references</span></span>](http://nuget.codeplex.com/workitem/440)
* [<span data-ttu-id="e7eb2-135">获取包-对话框中的更新失败，或在控制台中选择 "全部" 聚合源时失败</span><span class="sxs-lookup"><span data-stu-id="e7eb2-135">Get-Package -Updates fails in the dialog, or when the 'All' aggregate source is selected in the console</span></span>](http://nuget.codeplex.com/workitem/439)
* [<span data-ttu-id="e7eb2-136">获取包验证错误</span><span class="sxs-lookup"><span data-stu-id="e7eb2-136">Getting package verification errors</span></span>](http://nuget.codeplex.com/workitem/426)
* [<span data-ttu-id="e7eb2-137">当无法通过 "添加包" 对话框安装包时警告用户</span><span class="sxs-lookup"><span data-stu-id="e7eb2-137">Warn users when a package cannot be installed from the Add Package Dialog</span></span>](http://nuget.codeplex.com/workitem/425)
* [<span data-ttu-id="e7eb2-138">获取包-更新大量包时引发更新</span><span class="sxs-lookup"><span data-stu-id="e7eb2-138">Get-Package -Updates throws when updating large number of packages</span></span>](http://nuget.codeplex.com/workitem/424)
* [<span data-ttu-id="e7eb2-139">当错误编写 nuspec 文件时改进错误处理</span><span class="sxs-lookup"><span data-stu-id="e7eb2-139">Improve error handling when nuspec files are authored incorrectly</span></span>](http://nuget.codeplex.com/workitem/423)
* [<span data-ttu-id="e7eb2-140">Nuget 包忽略指定文件</span><span class="sxs-lookup"><span data-stu-id="e7eb2-140">Nuget pack ignores specified files</span></span>](http://nuget.codeplex.com/workitem/422)
* [<span data-ttu-id="e7eb2-141">删除第二个到最后一个包源，然后单击 "下移" 崩溃与</span><span class="sxs-lookup"><span data-stu-id="e7eb2-141">Removing the second-to-last package source and then clicking "Move Down" crashes VS</span></span>](http://nuget.codeplex.com/workitem/418)
* [<span data-ttu-id="e7eb2-142">安装包时删除程序集引用</span><span class="sxs-lookup"><span data-stu-id="e7eb2-142">Remove assembly reference while installing packages</span></span>](http://nuget.codeplex.com/workitem/413)
* [<span data-ttu-id="e7eb2-143">打开设置对话框时的 InvalidOperationException</span><span class="sxs-lookup"><span data-stu-id="e7eb2-143">InvalidOperationException when opening Settings dialog</span></span>](http://nuget.codeplex.com/workitem/411)
* [<span data-ttu-id="e7eb2-144">包源在包管理器控制台中的访问密钥无效</span><span class="sxs-lookup"><span data-stu-id="e7eb2-144">Access Key for Package Source in Package Manager Console doesn't work</span></span>](http://nuget.codeplex.com/workitem/410)
* [<span data-ttu-id="e7eb2-145">NuGet VS 设置对话框访问键将焦点放在错误字段上</span><span class="sxs-lookup"><span data-stu-id="e7eb2-145">NuGet VS Settings Dialog Access Keys Give Focus to Wrong Fields</span></span>](http://nuget.codeplex.com/workitem/409)
* [<span data-ttu-id="e7eb2-146">包 ID intellisense 不应查询太多项目</span><span class="sxs-lookup"><span data-stu-id="e7eb2-146">Package ID intellisense should not query too many items</span></span>](http://nuget.codeplex.com/workitem/404)
* [<span data-ttu-id="e7eb2-147">将包添加到项目名称中包含点字符的项目失败</span><span class="sxs-lookup"><span data-stu-id="e7eb2-147">Failure adding package to project with a dot character in the Project name</span></span>](http://nuget.codeplex.com/workitem/403)
* [<span data-ttu-id="e7eb2-148">Nuspec 中指定文件的问题</span><span class="sxs-lookup"><span data-stu-id="e7eb2-148">Issue with specified files in nuspec</span></span>](http://nuget.codeplex.com/workitem/400)
* [<span data-ttu-id="e7eb2-149">使用较新版本时应注册正确的官方源</span><span class="sxs-lookup"><span data-stu-id="e7eb2-149">Correct official feed should get registered when using newer build</span></span>](http://nuget.codeplex.com/workitem/399)
* [<span data-ttu-id="e7eb2-150">标记应使用空格而不是#</span><span class="sxs-lookup"><span data-stu-id="e7eb2-150">Tags should use spaces instead of #</span></span>](http://nuget.codeplex.com/workitem/397)
* [<span data-ttu-id="e7eb2-151">IPackageMetadata 缺少某些有用信息</span><span class="sxs-lookup"><span data-stu-id="e7eb2-151">IPackageMetadata lacks some useful information</span></span>](http://nuget.codeplex.com/workitem/388)
* [<span data-ttu-id="e7eb2-152">向对话添加 "报告滥用行为" 链接</span><span class="sxs-lookup"><span data-stu-id="e7eb2-152">Add Report Abuse Link to the Dialog</span></span>](http://nuget.codeplex.com/workitem/386)
* [<span data-ttu-id="e7eb2-153">在 Visual Studio 中使用 App_Data 解压缩包中断</span><span class="sxs-lookup"><span data-stu-id="e7eb2-153">Using App_Data to unzip packages breaks in Visual Studio</span></span>](http://nuget.codeplex.com/workitem/380)
* [<span data-ttu-id="e7eb2-154">实现标记</span><span class="sxs-lookup"><span data-stu-id="e7eb2-154">Implement Tags</span></span>](http://nuget.codeplex.com/workitem/376)
* [<span data-ttu-id="e7eb2-155">PackageBuilder 允许没有要创建的依赖项的空包</span><span class="sxs-lookup"><span data-stu-id="e7eb2-155">PackageBuilder allows empty package with no dependencies to be created</span></span>](http://nuget.codeplex.com/workitem/373)
* [<span data-ttu-id="e7eb2-156">为包添加所有者字段</span><span class="sxs-lookup"><span data-stu-id="e7eb2-156">Add Owners Field for the Package</span></span>](http://nuget.codeplex.com/workitem/365)
* [<span data-ttu-id="e7eb2-157">更新 VSIX 清单以表示 NuGet 包管理器，而不是 VSIX 工具</span><span class="sxs-lookup"><span data-stu-id="e7eb2-157">Update the VSIX manifest to say NuGet Package Manager rather than VSIX Tools</span></span>](http://nuget.codeplex.com/workitem/364)
* [<span data-ttu-id="e7eb2-158">选择 "所有源" 时，"获取包" 命令会引发错误</span><span class="sxs-lookup"><span data-stu-id="e7eb2-158">Get-Package command throws error when All source is selected</span></span>](http://nuget.codeplex.com/workitem/359)
* [<span data-ttu-id="e7eb2-159">允许在 "选项" 对话框中排序包源</span><span class="sxs-lookup"><span data-stu-id="e7eb2-159">Allow ordering of package sources in Options dialog</span></span>](http://nuget.codeplex.com/workitem/356)
* [<span data-ttu-id="e7eb2-160">更新-包不会删除较旧的版本</span><span class="sxs-lookup"><span data-stu-id="e7eb2-160">Update-Package does not remove older version</span></span>](http://nuget.codeplex.com/workitem/352)
* [<span data-ttu-id="e7eb2-161">实现依赖项的版本范围规范</span><span class="sxs-lookup"><span data-stu-id="e7eb2-161">Implement Version Range Specification for Dependencies</span></span>](http://nuget.codeplex.com/workitem/347)
* [<span data-ttu-id="e7eb2-162">单击 "添加新包" 时 Visual Studio 崩溃</span><span class="sxs-lookup"><span data-stu-id="e7eb2-162">Visual Studio crashes when clicking "Add new package"</span></span>](http://nuget.codeplex.com/workitem/346)
* [<span data-ttu-id="e7eb2-163">显示 "添加包" 对话框中的下载和分级</span><span class="sxs-lookup"><span data-stu-id="e7eb2-163">Display Downloads and Ratings in the Add Package Dialog</span></span>](http://nuget.codeplex.com/workitem/345)
* [<span data-ttu-id="e7eb2-164">对话框中的包源之间的更改不会更新活动源</span><span class="sxs-lookup"><span data-stu-id="e7eb2-164">Changing between package sources in the Dialog doesn't update active source</span></span>](http://nuget.codeplex.com/workitem/344)
* [<span data-ttu-id="e7eb2-165">删除程序包管理器控制台窗口的键绑定</span><span class="sxs-lookup"><span data-stu-id="e7eb2-165">Remove Key Binding for Package Manager Console Window</span></span>](http://nuget.codeplex.com/workitem/339)
* [<span data-ttu-id="e7eb2-166">安装包未被识别为 cmdlet 的名称 .。。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-166">Install-Package is not recognized as the name of a cmdlet...</span></span>](http://nuget.codeplex.com/workitem/338)
* [<span data-ttu-id="e7eb2-167">从本地源安装包未解析常规源上的依赖项</span><span class="sxs-lookup"><span data-stu-id="e7eb2-167">Installing a package from a local feed the dependencies on regular feeds are not resolved</span></span>](http://nuget.codeplex.com/workitem/332)
* [<span data-ttu-id="e7eb2-168">RemoveDependencies 应跳过仍在使用的依赖项</span><span class="sxs-lookup"><span data-stu-id="e7eb2-168">RemoveDependencies should skip dependencies that are still in use</span></span>](http://nuget.codeplex.com/workitem/331)
* [<span data-ttu-id="e7eb2-169">如果取消页面导航，则当原始页面请求返回时，用户无法导航到其他页面</span><span class="sxs-lookup"><span data-stu-id="e7eb2-169">If cancelling page navigation, user cannot navigate to a different page while the original page request returns</span></span>](http://nuget.codeplex.com/workitem/325)
* [<span data-ttu-id="e7eb2-170">调查 NuPack 的性能，以便为具有大量包的源提供服务。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-170">Investigate performance of NuPack.Server for serving feeds with large number of packages.</span></span>](http://nuget.codeplex.com/workitem/324)
* [<span data-ttu-id="e7eb2-171">第二次筛选包时，它将使用 "新" 包源，而不是以前选择的源。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-171">The second time I filter for a package it uses the "New" package source, instead of the previously selected source.</span></span>](http://nuget.codeplex.com/workitem/321)
* [<span data-ttu-id="e7eb2-172">选择对话框上的 "联机" 选项卡时，应选择默认的包源。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-172">Default package source should be selected when selecting the "Online" tab on the dialog.</span></span>](http://nuget.codeplex.com/workitem/320)
* [<span data-ttu-id="e7eb2-173">默认情况下，列表包应显示已安装的包</span><span class="sxs-lookup"><span data-stu-id="e7eb2-173">List-Package should show installed packages by default</span></span>](http://nuget.codeplex.com/workitem/309)
* [<span data-ttu-id="e7eb2-174">程序集引用 HintPaths</span><span class="sxs-lookup"><span data-stu-id="e7eb2-174">Assembly Reference HintPaths</span></span>](http://nuget.codeplex.com/workitem/294)
* [<span data-ttu-id="e7eb2-175">打开程序包管理器控制台时出现异常</span><span class="sxs-lookup"><span data-stu-id="e7eb2-175">Exception while opening Package Manager Console</span></span>](http://nuget.codeplex.com/workitem/268)
* [<span data-ttu-id="e7eb2-176">控制台 intellisense 下载整个源</span><span class="sxs-lookup"><span data-stu-id="e7eb2-176">Console intellisense downloads entire feed</span></span>](http://nuget.codeplex.com/workitem/259)
* [<span data-ttu-id="e7eb2-177">"Default" 包源应重命名为 "Active"</span><span class="sxs-lookup"><span data-stu-id="e7eb2-177">'Default' package source should be renamed to 'Active'</span></span>](http://nuget.codeplex.com/workitem/258)
* [<span data-ttu-id="e7eb2-178">包源 UI：如果名称/源字段非空，请按 "确定" 以添加新源</span><span class="sxs-lookup"><span data-stu-id="e7eb2-178">Package sources UI: pressing OK should add the new source if Name/Source fields are non-empty</span></span>](http://nuget.codeplex.com/workitem/257)
* [<span data-ttu-id="e7eb2-179">当已安装的包的数量较大时，对话框变慢</span><span class="sxs-lookup"><span data-stu-id="e7eb2-179">Dialog becomes super slow when the number of installed packages is large</span></span>](http://nuget.codeplex.com/workitem/243)
* [<span data-ttu-id="e7eb2-180">支持强名称程序集的绑定重定向</span><span class="sxs-lookup"><span data-stu-id="e7eb2-180">Support Binding Redirects for Strong Named Assemblies</span></span>](http://nuget.codeplex.com/workitem/238)
* [<span data-ttu-id="e7eb2-181">添加包引用 .。。用于包含包源的下拉的 UI</span><span class="sxs-lookup"><span data-stu-id="e7eb2-181">Add Package Reference... UI to include drop down for Package source</span></span>](http://nuget.codeplex.com/workitem/226)
* [<span data-ttu-id="e7eb2-182">NuPack 需要支持配置文件名称的配置转换 agnostically</span><span class="sxs-lookup"><span data-stu-id="e7eb2-182">NuPack needs to support config transform agnostically of the config file name</span></span>](http://nuget.codeplex.com/workitem/224)
* [<span data-ttu-id="e7eb2-183">允许在 NuPack.exe中重写 BasePath </span><span class="sxs-lookup"><span data-stu-id="e7eb2-183">Allows BasePath to be Overriden in NuPack.exe</span></span>](http://nuget.codeplex.com/workitem/222)
* [<span data-ttu-id="e7eb2-184">包源回退行为</span><span class="sxs-lookup"><span data-stu-id="e7eb2-184">Package Source Fallback Behavior</span></span>](http://nuget.codeplex.com/workitem/204)
* [<span data-ttu-id="e7eb2-185">GUI 崩溃</span><span class="sxs-lookup"><span data-stu-id="e7eb2-185">Crash on GUI</span></span>](http://nuget.codeplex.com/workitem/201)
* [<span data-ttu-id="e7eb2-186">添加排序选项以添加包对话框</span><span class="sxs-lookup"><span data-stu-id="e7eb2-186">Add sorting options to Add Package Dialog</span></span>](http://nuget.codeplex.com/workitem/179)
* [<span data-ttu-id="e7eb2-187">用于清除程序包管理器控制台的快捷键</span><span class="sxs-lookup"><span data-stu-id="e7eb2-187">shortcut key to clear the Package Manager Console</span></span>](http://nuget.codeplex.com/workitem/174)
* [<span data-ttu-id="e7eb2-188">PowerConsole 导致 NuPack 控制台失败</span><span class="sxs-lookup"><span data-stu-id="e7eb2-188">PowerConsole causes NuPack Console to fail</span></span>](http://nuget.codeplex.com/workitem/166)
* [<span data-ttu-id="e7eb2-189">控制台和 "添加包" 对话框应在请求中设置用户代理</span><span class="sxs-lookup"><span data-stu-id="e7eb2-189">Console and Add Package Dialog should set user agent in requests</span></span>](http://nuget.codeplex.com/workitem/141)
* [<span data-ttu-id="e7eb2-190">在生成中设置 VSIX 和 NuPack.exe 的版本号。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-190">Set version number of the VSIX and NuPack.exe in the build.</span></span>](http://nuget.codeplex.com/workitem/134)
* [<span data-ttu-id="e7eb2-191">从-？隐藏公共 PowerShell 参数</span><span class="sxs-lookup"><span data-stu-id="e7eb2-191">Hide common PowerShell parameters from -?</span></span>](http://nuget.codeplex.com/workitem/118)
* [<span data-ttu-id="e7eb2-192">为控制台命令添加详细帮助</span><span class="sxs-lookup"><span data-stu-id="e7eb2-192">Add -detailed help for console commands</span></span>](http://nuget.codeplex.com/workitem/110)
* [<span data-ttu-id="e7eb2-193">"添加包" 对话框应该允许选择当前包源</span><span class="sxs-lookup"><span data-stu-id="e7eb2-193">Add Package Dialog Should Allow Choosing the Current Package Source</span></span>](http://nuget.codeplex.com/workitem/88)
* [<span data-ttu-id="e7eb2-194">将 NuPack 类移到不同的命名空间</span><span class="sxs-lookup"><span data-stu-id="e7eb2-194">Move NuPack.Core classes into different namespaces</span></span>](http://nuget.codeplex.com/workitem/50)
* [<span data-ttu-id="e7eb2-195">向 cmdlet 添加帮助</span><span class="sxs-lookup"><span data-stu-id="e7eb2-195">Add help to cmdlets</span></span>](http://nuget.codeplex.com/workitem/23)
* [<span data-ttu-id="e7eb2-196">下载包后验证源中的哈希</span><span class="sxs-lookup"><span data-stu-id="e7eb2-196">Verify hash from feed after package download</span></span>](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a><span data-ttu-id="e7eb2-197">CTP 2</span><span class="sxs-lookup"><span data-stu-id="e7eb2-197">CTP 2</span></span>

<span data-ttu-id="e7eb2-198">下面是 CTP 2 中最重要的更改：</span><span class="sxs-lookup"><span data-stu-id="e7eb2-198">The following are the most significant changes made in CTP 2:</span></span>

* <span data-ttu-id="e7eb2-199">将包源从 ATOM 切换到 OData 服务终结点：如果升级到 CTP2 版本的 NuGet，请确保将以下 URL 作为包源添加： `https://feed.nuget.org/ctp2/odata/v1/` 。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-199">Switched the package feed from ATOM to an OData service endpoint: If you upgrade to the CTP2 version of NuGet, be sure to add the following URL as a package source: `https://feed.nuget.org/ctp2/odata/v1/`.</span></span>
* <span data-ttu-id="e7eb2-200">将 Add-Package 命令重命名为 *安装包*。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-200">Renamed the Add-Package command to *Install-Package*.</span></span>
* <span data-ttu-id="e7eb2-201">已更新 `.nuspec` 格式。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-201">Updated the `.nuspec` Format.</span></span> <span data-ttu-id="e7eb2-202">`.nuspec`现在，格式包括用于指定 32x32 png 图标的 *iconUrl* 字段，该图标将显示在 "添加包" 对话框中。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-202">The `.nuspec` format now includes the *iconUrl* field for specifying a 32x32 png icon which will show up in the Add Package Dialog.</span></span> <span data-ttu-id="e7eb2-203">因此，请确保将其设置为区分包。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-203">So be sure to set that to distinguish your package.</span></span> <span data-ttu-id="e7eb2-204">此 `.nuspec` 格式还包含新的 *projectUrl* 字段，可用于指向提供有关包的详细信息的网页。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-204">The `.nuspec` format also includes the new *projectUrl* field which you can use to point to a web page that provides more information about your package.</span></span>

<span data-ttu-id="e7eb2-205">此生成不适用于旧 `.nupkg` 文件。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-205">This build will not work with old `.nupkg` files.</span></span> <span data-ttu-id="e7eb2-206">如果收到空引用异常，则使用的是旧 `.nupkg` 文件，需要使用更新后的 [NuGet 命令行工具](http://nuget.codeplex.com/releases/52017/download/165468)重新生成它。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-206">If you get null reference exceptions, you're using an old `.nupkg` file and need to rebuild it with the updated [NuGet command line tool](http://nuget.codeplex.com/releases/52017/download/165468).</span></span>

<span data-ttu-id="e7eb2-207">下面列出了针对 NuGet CTP 2 修复的功能和 bug， (不包括次代码清理等的 bug ) 。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-207">The following is a list of features and bugs that were fixed for NuGet CTP 2 (does not include bugs for minor code cleanups etc.).</span></span>

* [<span data-ttu-id="e7eb2-208">为程序集指定 TargetFramework 时，解压缩包程序集时出错。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-208">Error unpacking package assemblies when specifiying the TargetFramework for an assembly.</span></span>](http://nuget.codeplex.com/workitem/10)
* [<span data-ttu-id="e7eb2-209">使 NuPack 控制台窗口更易发现</span><span class="sxs-lookup"><span data-stu-id="e7eb2-209">Make NuPack Console window more discoverable</span></span>](http://nuget.codeplex.com/workitem/14)
* [<span data-ttu-id="e7eb2-210">ILMerge nupack.exe 版本</span><span class="sxs-lookup"><span data-stu-id="e7eb2-210">ILMerge the nupack.exe release</span></span>](http://nuget.codeplex.com/workitem/19)
* [<span data-ttu-id="e7eb2-211">更好的错误/异常处理</span><span class="sxs-lookup"><span data-stu-id="e7eb2-211">Better error/exception handling</span></span>](http://nuget.codeplex.com/workitem/24)
* <span data-ttu-id="e7eb2-212">[[Nupack]： PackageManager 应适当处理与源相关的错误](http://nuget.codeplex.com/workitem/28)</span><span class="sxs-lookup"><span data-stu-id="e7eb2-212">[[Nupack.Core]: PackageManager should gracefully handle feed-related errors](http://nuget.codeplex.com/workitem/28)</span></span>
* [<span data-ttu-id="e7eb2-213">需要控制台的新图标</span><span class="sxs-lookup"><span data-stu-id="e7eb2-213">Need a new icon for the console</span></span>](http://nuget.codeplex.com/workitem/29)
* [<span data-ttu-id="e7eb2-214">在对话框中本地化字符串</span><span class="sxs-lookup"><span data-stu-id="e7eb2-214">Localize strings in the Dialog</span></span>](http://nuget.codeplex.com/workitem/38)
* [<span data-ttu-id="e7eb2-215">NuPack 在内存中缓存下载的 NuPack 文件</span><span class="sxs-lookup"><span data-stu-id="e7eb2-215">NuPack caches downloaded .nupack files in memory</span></span>](http://nuget.codeplex.com/workitem/40)
* [<span data-ttu-id="e7eb2-216">NuPack 控制台：更改显示控制台的默认快捷方式</span><span class="sxs-lookup"><span data-stu-id="e7eb2-216">NuPack Console: Change the default shortcut for displaying console</span></span>](http://nuget.codeplex.com/workitem/48)
* [<span data-ttu-id="e7eb2-217">ProjectSystem 应支持通用属性的默认值</span><span class="sxs-lookup"><span data-stu-id="e7eb2-217">ProjectSystem should support default values for common properties</span></span>](http://nuget.codeplex.com/workitem/49)
* [<span data-ttu-id="e7eb2-218">仅使用一个 nuspec 文件在文件夹中运行 nupack.exe 应使用该 nuspec</span><span class="sxs-lookup"><span data-stu-id="e7eb2-218">Running nupack.exe in a folder with just one nuspec file should use that nuspec</span></span>](http://nuget.codeplex.com/workitem/52)
* [<span data-ttu-id="e7eb2-219">即使没有加载任何项目/解决方案，"项目" 菜单也会显示</span><span class="sxs-lookup"><span data-stu-id="e7eb2-219">Project Menu Shows Up Even When No Project/Solution Is Loaded</span></span>](http://nuget.codeplex.com/workitem/54)
* [<span data-ttu-id="e7eb2-220">在基本代码的干净克隆上生成 .cmd 失败</span><span class="sxs-lookup"><span data-stu-id="e7eb2-220">build.cmd fails on a clean clone of the codebase</span></span>](http://nuget.codeplex.com/workitem/56)
* [<span data-ttu-id="e7eb2-221">更新可用功能</span><span class="sxs-lookup"><span data-stu-id="e7eb2-221">Updates available feature</span></span>](http://nuget.codeplex.com/workitem/57)
* [<span data-ttu-id="e7eb2-222">对话框：通过对话框添加包将删除控制台中的提示</span><span class="sxs-lookup"><span data-stu-id="e7eb2-222">Dialog: Adding a package through the dialog removes the prompt in the console</span></span>](http://nuget.codeplex.com/workitem/73)
* [<span data-ttu-id="e7eb2-223">通过单击 "安装" 添加包的速度通常较慢，无可视反馈</span><span class="sxs-lookup"><span data-stu-id="e7eb2-223">Adding a package by clicking 'Install' is often slow, with no visual feedback</span></span>](http://nuget.codeplex.com/workitem/80)
* [<span data-ttu-id="e7eb2-224">无法发现哪些已安装的包有更新。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-224">There is no way to discover which of my installed packages have updates.</span></span>](http://nuget.codeplex.com/workitem/82)
* [<span data-ttu-id="e7eb2-225">无法在对话框中更新已安装的包。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-225">There is no way to update an installed package in the dialog.</span></span>](http://nuget.codeplex.com/workitem/83)
* [<span data-ttu-id="e7eb2-226">无法在对话框中卸载已安装的包</span><span class="sxs-lookup"><span data-stu-id="e7eb2-226">There is no way to uninstall an installed package in the dialog</span></span>](http://nuget.codeplex.com/workitem/84)
* [<span data-ttu-id="e7eb2-227">&ldquo;添加包引用 &hellip; &rdquo; 出现在已安装的引用的上下文菜单上</span><span class="sxs-lookup"><span data-stu-id="e7eb2-227">&ldquo;Add Package Reference&hellip;&rdquo; appears on the context menu of installed references</span></span>](http://nuget.codeplex.com/workitem/85)
* [<span data-ttu-id="e7eb2-228">从控制台更新包后，它会将旧版本和新版本显示为已安装</span><span class="sxs-lookup"><span data-stu-id="e7eb2-228">After updating a package from the console, it shows both the old version and the new version as installed</span></span>](http://nuget.codeplex.com/workitem/86)
* [<span data-ttu-id="e7eb2-229">使用对话框时，控制台中的活动会在使用后消失</span><span class="sxs-lookup"><span data-stu-id="e7eb2-229">The activity in the console, when using the dialog, disappears after use</span></span>](http://nuget.codeplex.com/workitem/87)
* [<span data-ttu-id="e7eb2-230">清理 nupack.exe中的命令行分析 </span><span class="sxs-lookup"><span data-stu-id="e7eb2-230">Cleanup command line parsing in nupack.exe</span></span>](http://nuget.codeplex.com/workitem/89)
* [<span data-ttu-id="e7eb2-231">将友好名称添加到包源</span><span class="sxs-lookup"><span data-stu-id="e7eb2-231">Add a friendly name to package sources</span></span>](http://nuget.codeplex.com/workitem/98)
* [<span data-ttu-id="e7eb2-232">要支持包括包图标的 nuspec</span><span class="sxs-lookup"><span data-stu-id="e7eb2-232">Update .nuspec to support including package icons</span></span>](http://nuget.codeplex.com/workitem/103)
* [<span data-ttu-id="e7eb2-233">源 UI 不允许复制 URL</span><span class="sxs-lookup"><span data-stu-id="e7eb2-233">Feed UI doesn't allow copying the URL</span></span>](http://nuget.codeplex.com/workitem/105)
* [<span data-ttu-id="e7eb2-234">更好的删除包错误处理。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-234">Better remove-package error handling.</span></span>](http://nuget.codeplex.com/workitem/107)
* [<span data-ttu-id="e7eb2-235">在控制台窗口中键入依赖于游标焦点</span><span class="sxs-lookup"><span data-stu-id="e7eb2-235">Typing in Console Window depends on cursor focus</span></span>](http://nuget.codeplex.com/workitem/112)
* [<span data-ttu-id="e7eb2-236">错误消息的外观</span><span class="sxs-lookup"><span data-stu-id="e7eb2-236">Error messages look awful</span></span>](http://nuget.codeplex.com/workitem/116)
* [<span data-ttu-id="e7eb2-237">未安装的包的 Remove-Package 性能不佳</span><span class="sxs-lookup"><span data-stu-id="e7eb2-237">The performance of Remove-Package for a package that isn't installed is bad</span></span>](http://nuget.codeplex.com/workitem/117)
* [<span data-ttu-id="e7eb2-238">如果没有包源，则删除包会失败</span><span class="sxs-lookup"><span data-stu-id="e7eb2-238">Removing a package fails when there are no package sources</span></span>](http://nuget.codeplex.com/workitem/119)
* [<span data-ttu-id="e7eb2-239">当包源不可用时，删除包失败</span><span class="sxs-lookup"><span data-stu-id="e7eb2-239">Remove-Package fails when the package source is unavailable</span></span>](http://nuget.codeplex.com/workitem/120)
* [<span data-ttu-id="e7eb2-240">将标题添加到包元数据和源。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-240">Add Title to the package metadata and the feed.</span></span>](http://nuget.codeplex.com/workitem/125)
* [<span data-ttu-id="e7eb2-241">将-Source 参数添加回添加包</span><span class="sxs-lookup"><span data-stu-id="e7eb2-241">Add the -Source parameter back to Add-Package</span></span>](http://nuget.codeplex.com/workitem/127)
* [<span data-ttu-id="e7eb2-242">列表-包应具有-Source 参数</span><span class="sxs-lookup"><span data-stu-id="e7eb2-242">List-Package should have a -Source parameter</span></span>](http://nuget.codeplex.com/workitem/128)
* [<span data-ttu-id="e7eb2-243">更新 NuPack 以要求 NuPack 用户代理下载包</span><span class="sxs-lookup"><span data-stu-id="e7eb2-243">Update NuPack.Server to require NuPack User Agent To Download Package</span></span>](http://nuget.codeplex.com/workitem/142)
* [<span data-ttu-id="e7eb2-244">"许可证接受" 对话框必须列出所有需要接受的依赖项的许可证</span><span class="sxs-lookup"><span data-stu-id="e7eb2-244">License Acceptance Dialog Must List Licenses For All Dependencies That Require Acceptance</span></span>](http://nuget.codeplex.com/workitem/145)
* [<span data-ttu-id="e7eb2-245">在源中引发包时记录错误</span><span class="sxs-lookup"><span data-stu-id="e7eb2-245">Log an error when a package throws in the feed</span></span>](http://nuget.codeplex.com/workitem/150)
* [<span data-ttu-id="e7eb2-246">NuPack.exe 不应允许空的 &lt; licenseurl &gt; 元素</span><span class="sxs-lookup"><span data-stu-id="e7eb2-246">NuPack.exe should not allow an empty &lt;licenseurl&gt; element</span></span>](http://nuget.codeplex.com/workitem/152)
* [<span data-ttu-id="e7eb2-247">将 List-Package 重命名为获取包，Add-Package 安装包，并将 Remove-Package 为卸载包</span><span class="sxs-lookup"><span data-stu-id="e7eb2-247">Rename List-Package to Get-Package, Add-Package to Install-Package, and Remove-Package to Uninstall-Package</span></span>](http://nuget.codeplex.com/workitem/155)
* [<span data-ttu-id="e7eb2-248">使用解决方案导航器中的 "添加包引用" 菜单项导致 Visual Studio 崩溃</span><span class="sxs-lookup"><span data-stu-id="e7eb2-248">Using the Add Package Reference menu item from the Solution Navigator crashes Visual Studio</span></span>](http://nuget.codeplex.com/workitem/158)
* [<span data-ttu-id="e7eb2-249">"可用的包源" 标签缺少冒号</span><span class="sxs-lookup"><span data-stu-id="e7eb2-249">"Available package sources" label is missing a colon</span></span>](http://nuget.codeplex.com/workitem/160)
* [<span data-ttu-id="e7eb2-250">使. nuspec xml 元素大小写一致大小写</span><span class="sxs-lookup"><span data-stu-id="e7eb2-250">Make .nuspec xml element casing consistently camel cased</span></span>](http://nuget.codeplex.com/workitem/161)
* [<span data-ttu-id="e7eb2-251">NuPack VSIX 的清单需要启用 "admin" 位</span><span class="sxs-lookup"><span data-stu-id="e7eb2-251">The NuPack VSIX's manifest needs to turn on the 'admin' bit</span></span>](http://nuget.codeplex.com/workitem/162)
* [<span data-ttu-id="e7eb2-252">如果运行不带源的 List-Package，则会出现 null 引用错误</span><span class="sxs-lookup"><span data-stu-id="e7eb2-252">If you run List-Package with no feeds, you get null ref error</span></span>](http://nuget.codeplex.com/workitem/164)
* [<span data-ttu-id="e7eb2-253">nuget.exe：指定目标路径</span><span class="sxs-lookup"><span data-stu-id="e7eb2-253">nuget.exe: specify destination path</span></span>](http://nuget.codeplex.com/workitem/171)
* [<span data-ttu-id="e7eb2-254">在 WinXP 上打开包管理控制台时出现 Powershell 错误</span><span class="sxs-lookup"><span data-stu-id="e7eb2-254">Powershell Errors Opening Package Management Console on WinXP</span></span>](http://nuget.codeplex.com/workitem/175)
* [<span data-ttu-id="e7eb2-255">尝试加载包列表时 VS 崩溃</span><span class="sxs-lookup"><span data-stu-id="e7eb2-255">VS Crashes while trying to load package list</span></span>](http://nuget.codeplex.com/workitem/176)
* [<span data-ttu-id="e7eb2-256">允许元包不 (文件，仅) 依赖项 </span><span class="sxs-lookup"><span data-stu-id="e7eb2-256">allow meta packages (no files, only dependencies)</span></span>](http://nuget.codeplex.com/workitem/180)
* [<span data-ttu-id="e7eb2-257">将 Powershell 脚本转换为 Powershell 2.0 模块</span><span class="sxs-lookup"><span data-stu-id="e7eb2-257">Convert Powershell Script to Powershell 2.0 Module</span></span>](http://nuget.codeplex.com/workitem/181)
* [<span data-ttu-id="e7eb2-258">指定 target 后，PathResolver 应丢弃前面的通配符字符的路径部分</span><span class="sxs-lookup"><span data-stu-id="e7eb2-258">PathResolver should discard path portion preceeding wildcard characters when target is specified</span></span>](http://nuget.codeplex.com/workitem/183)
* [<span data-ttu-id="e7eb2-259">无依赖项</span><span class="sxs-lookup"><span data-stu-id="e7eb2-259">No dependencies</span></span>](http://nuget.codeplex.com/workitem/186)
* [<span data-ttu-id="e7eb2-260">安装 Elmah 时出错</span><span class="sxs-lookup"><span data-stu-id="e7eb2-260">Error installing Elmah</span></span>](http://nuget.codeplex.com/workitem/192)
* [<span data-ttu-id="e7eb2-261">使用 configsections 无法正常使用配置转换 &lt;&gt;</span><span class="sxs-lookup"><span data-stu-id="e7eb2-261">Config transforms don't work correctly with &lt;configsections&gt;</span></span>](http://nuget.codeplex.com/workitem/194)
* [<span data-ttu-id="e7eb2-262">无法检索变量 "$global:p rojectCache"，因为它尚未设置</span><span class="sxs-lookup"><span data-stu-id="e7eb2-262">The variable '$global:projectCache' cannot be retrieved because it has not been set</span></span>](http://nuget.codeplex.com/workitem/203)
* [<span data-ttu-id="e7eb2-263">添加用于创建 NuPack 包的 MSBuild 任务</span><span class="sxs-lookup"><span data-stu-id="e7eb2-263">Add MSBuild task for creating NuPack packages</span></span>](http://nuget.codeplex.com/workitem/205)
* [<span data-ttu-id="e7eb2-264">列表-包需要支持搜索/筛选</span><span class="sxs-lookup"><span data-stu-id="e7eb2-264">list-package needs to support searching/filtering</span></span>](http://nuget.codeplex.com/workitem/206)
* [<span data-ttu-id="e7eb2-265">如果包作者提供许可证 URL，则始终显示许可证的链接</span><span class="sxs-lookup"><span data-stu-id="e7eb2-265">Always display a link to license if the package author provides a license URL</span></span>](http://nuget.codeplex.com/workitem/208)
* [<span data-ttu-id="e7eb2-266">使用删除包偶尔出现 "拒绝访问" 异常</span><span class="sxs-lookup"><span data-stu-id="e7eb2-266">Occasional "Access Denied" exception with Remove-Package</span></span>](http://nuget.codeplex.com/workitem/213)
* [<span data-ttu-id="e7eb2-267">失败的单元测试： InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries</span><span class="sxs-lookup"><span data-stu-id="e7eb2-267">Unit Tests Failing: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries</span></span>](http://nuget.codeplex.com/workitem/214)
* [<span data-ttu-id="e7eb2-268">如果找不到针对特定 framework 版本，则允许使用回退/默认文件集</span><span class="sxs-lookup"><span data-stu-id="e7eb2-268">Allow for a fallback/default set of files if a specfic framework version cannot be found</span></span>](http://nuget.codeplex.com/workitem/223)
* [<span data-ttu-id="e7eb2-269">添加包引用 .。。UI 无法删除包</span><span class="sxs-lookup"><span data-stu-id="e7eb2-269">Add Package Reference... UI cannot remove a package</span></span>](http://nuget.codeplex.com/workitem/225)
* [<span data-ttu-id="e7eb2-270">卸载一个或多个项目时添加包引用崩溃 studio</span><span class="sxs-lookup"><span data-stu-id="e7eb2-270">Add Package Reference crashes studio when one or more project is unloaded</span></span>](http://nuget.codeplex.com/workitem/228)
* [<span data-ttu-id="e7eb2-271">配置转换似乎不适用于 web.debug.config 文件</span><span class="sxs-lookup"><span data-stu-id="e7eb2-271">Config transform does not appear to work on web.debug.config file</span></span>](http://nuget.codeplex.com/workitem/229)
* [<span data-ttu-id="e7eb2-272"> 不会在自定义包上触发init.ps1</span><span class="sxs-lookup"><span data-stu-id="e7eb2-272">init.ps1 not firing on custom package</span></span>](http://nuget.codeplex.com/workitem/237)
* [<span data-ttu-id="e7eb2-273">将路径添加到 feedlist 时，默认按钮设置为 "确定"，因此，如果我按 ENTER 自动关闭</span><span class="sxs-lookup"><span data-stu-id="e7eb2-273">When adding paths to the feedlist, the default button is set to OK, so if I press ENTER it automatically closes</span></span>](http://nuget.codeplex.com/workitem/240)
* [<span data-ttu-id="e7eb2-274">尝试卸载依赖项将崩溃，并在行中尝试2次</span><span class="sxs-lookup"><span data-stu-id="e7eb2-274">Attempt to uninstall a dependency will crash VS if attempted 2 times in a row</span></span>](http://nuget.codeplex.com/workitem/241)
* [<span data-ttu-id="e7eb2-275">在 "添加包" 对话框中显示项目 URL</span><span class="sxs-lookup"><span data-stu-id="e7eb2-275">Display the Project URL in the Add Package dialog</span></span>](http://nuget.codeplex.com/workitem/253)
* [<span data-ttu-id="e7eb2-276">默认情况下，Add-Package 对话框安装到已安装的包</span><span class="sxs-lookup"><span data-stu-id="e7eb2-276">Default the Add-Package dialog to Installed Packages</span></span>](http://nuget.codeplex.com/workitem/254)
* [<span data-ttu-id="e7eb2-277">更改 "添加包" 对话框菜单项。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-277">Change Add Package Dialog menu item.</span></span>](http://nuget.codeplex.com/workitem/261)
* [<span data-ttu-id="e7eb2-278">重命名命名空间和程序集</span><span class="sxs-lookup"><span data-stu-id="e7eb2-278">Rename namespaces and assemblies</span></span>](http://nuget.codeplex.com/workitem/274)
* [<span data-ttu-id="e7eb2-279">将 NuPack 项目重命名为 NuGet</span><span class="sxs-lookup"><span data-stu-id="e7eb2-279">Rename the NuPack Project to NuGet</span></span>](http://nuget.codeplex.com/workitem/282)
* [<span data-ttu-id="e7eb2-280">将以下文本添加到依赖项列表下</span><span class="sxs-lookup"><span data-stu-id="e7eb2-280">Add the following text under the list of dependencies</span></span>](http://nuget.codeplex.com/workitem/288)
* [<span data-ttu-id="e7eb2-281">在 "许可证接受" 对话框中更改许可证接受文本</span><span class="sxs-lookup"><span data-stu-id="e7eb2-281">Change the license acceptance text in the License Acceptance Dialog</span></span>](http://nuget.codeplex.com/workitem/291)
* [<span data-ttu-id="e7eb2-282">更改包列表上方的 "许可证接受" 对话框中的文本</span><span class="sxs-lookup"><span data-stu-id="e7eb2-282">Change the text in the License Acceptance Dialog above the list of packages</span></span>](http://nuget.codeplex.com/workitem/292)
* [<span data-ttu-id="e7eb2-283">OData 不适用于 fwlink URL</span><span class="sxs-lookup"><span data-stu-id="e7eb2-283">OData doesn't work with an fwlink URL</span></span>](http://nuget.codeplex.com/workitem/304)
* [<span data-ttu-id="e7eb2-284">包管理器 UI：通过积极缓存用于分页的包计数</span><span class="sxs-lookup"><span data-stu-id="e7eb2-284">Package Manager UI: Over aggressive caching of package count used for paging</span></span>](http://nuget.codeplex.com/workitem/317)
* [<span data-ttu-id="e7eb2-285">NuPack/NuGet- &gt; 程序包管理器控制台错误</span><span class="sxs-lookup"><span data-stu-id="e7eb2-285">NuPack / NuGet -&gt; Package Manager Console error</span></span>](http://nuget.codeplex.com/workitem/335)
* [<span data-ttu-id="e7eb2-286">"添加包" 对话框显示已安装包的许可证接受情况</span><span class="sxs-lookup"><span data-stu-id="e7eb2-286">Add Package Dialog shows License Acceptance For Already Installed Packaged</span></span>](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a><span data-ttu-id="e7eb2-287">CTP 1</span><span class="sxs-lookup"><span data-stu-id="e7eb2-287">CTP 1</span></span>

<span data-ttu-id="e7eb2-288">下面列出了针对 NuGet CTP 1 修复的功能和 bug。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-288">The following is a list of features and bugs that were fixed for NuGet CTP 1.</span></span>

* [<span data-ttu-id="e7eb2-289">包扩展应重命名为。 nupack</span><span class="sxs-lookup"><span data-stu-id="e7eb2-289">Package extension should be renamed to .nupack</span></span>](http://nuget.codeplex.com/workitem/1)
* [<span data-ttu-id="e7eb2-290">将包文件移动到文件夹</span><span class="sxs-lookup"><span data-stu-id="e7eb2-290">Move package file into folder</span></span>](http://nuget.codeplex.com/workitem/2)
* [<span data-ttu-id="e7eb2-291">合并安装 &amp; 添加 PS 命令</span><span class="sxs-lookup"><span data-stu-id="e7eb2-291">Merge install &amp; Add PS commands</span></span>](http://nuget.codeplex.com/workitem/3)
* [<span data-ttu-id="e7eb2-292">为 Verb-Noun cmdlet 创建别名</span><span class="sxs-lookup"><span data-stu-id="e7eb2-292">Create aliases for Verb-Noun cmdlets</span></span>](http://nuget.codeplex.com/workitem/4)
* [<span data-ttu-id="e7eb2-293">在 VS 中切换解决方案时，NuPack 混淆</span><span class="sxs-lookup"><span data-stu-id="e7eb2-293">NuPack gets confused when switching solution in VS</span></span>](http://nuget.codeplex.com/workitem/6)
* [<span data-ttu-id="e7eb2-294">默认情况下，应隐藏 "包" 解决方案文件夹</span><span class="sxs-lookup"><span data-stu-id="e7eb2-294">We should hide the 'packages' solution folder by default</span></span>](http://nuget.codeplex.com/workitem/11)
* [<span data-ttu-id="e7eb2-295">添加对内容项中的标记替换的支持。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-295">Add support for token replacement in content items.</span></span>](http://nuget.codeplex.com/workitem/12)
* [<span data-ttu-id="e7eb2-296">NuPack 应使用 Register-packagesource API</span><span class="sxs-lookup"><span data-stu-id="e7eb2-296">NuPack.UI should use the PackageSource API</span></span>](http://nuget.codeplex.com/workitem/26)
* <span data-ttu-id="e7eb2-297">[[Nupack]： PackageManager 在安装包之前将它们标记为已安装](http://nuget.codeplex.com/workitem/27)</span><span class="sxs-lookup"><span data-stu-id="e7eb2-297">[[Nupack.Core]: PackageManager marks packages as installed prior to installing them](http://nuget.codeplex.com/workitem/27)</span></span>
* [<span data-ttu-id="e7eb2-298">从解决方案中删除默认项目仍会将已删除的项目显示为默认项目</span><span class="sxs-lookup"><span data-stu-id="e7eb2-298">Deleting default project from solution still shows the deleted project as default</span></span>](http://nuget.codeplex.com/workitem/30)
* [<span data-ttu-id="e7eb2-299">新包失败，出现 "无法为指定的 URI 添加部分，因为它已在包中"。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-299">New-Package fails with "Cannot add part for the specified URI because it's already in the package."</span></span>](http://nuget.codeplex.com/workitem/32)
* [<span data-ttu-id="e7eb2-300">从 Visual Studio GUI 中删除 "NuPack" 字符串</span><span class="sxs-lookup"><span data-stu-id="e7eb2-300">Remove "NuPack" strings from Visual Studio GUI</span></span>](http://nuget.codeplex.com/workitem/35)
* [<span data-ttu-id="e7eb2-301">将 Apache 标头添加到 COPYRIGHT.txt 文件</span><span class="sxs-lookup"><span data-stu-id="e7eb2-301">Add Apache Header To a COPYRIGHT.txt file</span></span>](http://nuget.codeplex.com/workitem/36)
* [<span data-ttu-id="e7eb2-302">删除 Update-PackageSource 命令</span><span class="sxs-lookup"><span data-stu-id="e7eb2-302">Remove Update-PackageSource Command</span></span>](http://nuget.codeplex.com/workitem/37)
* [<span data-ttu-id="e7eb2-303">加载配置文件时程序包管理器不可用引发异常</span><span class="sxs-lookup"><span data-stu-id="e7eb2-303">Package Manager unusable when loading profile throws an exception</span></span>](http://nuget.codeplex.com/workitem/39)
* [<span data-ttu-id="e7eb2-304">init.ps1，install.ps1 和 uninstall.ps1 需要接收附加状态</span><span class="sxs-lookup"><span data-stu-id="e7eb2-304">init.ps1, install.ps1 and uninstall.ps1 need to receive additional state</span></span>](http://nuget.codeplex.com/workitem/41)
* [<span data-ttu-id="e7eb2-305">将控制台和 GUI 包合并到一个包中</span><span class="sxs-lookup"><span data-stu-id="e7eb2-305">Combine Console and GUI Packages Into One Package</span></span>](http://nuget.codeplex.com/workitem/42)
* [<span data-ttu-id="e7eb2-306">如果应用于不在根位置的 XML，则 Xml 转换逻辑不起作用</span><span class="sxs-lookup"><span data-stu-id="e7eb2-306">Xml transform logic doesn't work if applied to XML that isn't at the root</span></span>](http://nuget.codeplex.com/workitem/43)
* [<span data-ttu-id="e7eb2-307">管理包源设置对话框未更新 NuPack 控制台</span><span class="sxs-lookup"><span data-stu-id="e7eb2-307">Manage package sources settings dialog not updating the NuPack console</span></span>](http://nuget.codeplex.com/workitem/44)
* [<span data-ttu-id="e7eb2-308">NuPack 控制台 UI：将 "包源" 下拉列表重命名为 "包源"</span><span class="sxs-lookup"><span data-stu-id="e7eb2-308">NuPack Console UI: Rename 'Package feed' drop-down list to 'Package source'</span></span>](http://nuget.codeplex.com/workitem/45)
* [<span data-ttu-id="e7eb2-309">NuPack 控制台选项：将 "存储库 UI" 重命名为与 NuPack 控制台一致</span><span class="sxs-lookup"><span data-stu-id="e7eb2-309">NuPack Console Options: Rename 'Repository UI' to be consistent with NuPack Console</span></span>](http://nuget.codeplex.com/workitem/46)
* [<span data-ttu-id="e7eb2-310">对于从 IIS 或 URL 打开的网站，添加包失败</span><span class="sxs-lookup"><span data-stu-id="e7eb2-310">Add-Package fails against a website that was opened from IIS or a URL</span></span>](http://nuget.codeplex.com/workitem/53)
* [<span data-ttu-id="e7eb2-311">程序包管理器源不适用于 FwLink</span><span class="sxs-lookup"><span data-stu-id="e7eb2-311">Package Manager Source Doesn't Work With FwLink</span></span>](http://nuget.codeplex.com/workitem/55)
* [<span data-ttu-id="e7eb2-312">设置默认包源</span><span class="sxs-lookup"><span data-stu-id="e7eb2-312">Set the default package source</span></span>](http://nuget.codeplex.com/workitem/59)
* [<span data-ttu-id="e7eb2-313">如果在选项中添加包源，则仅提供一个源时，假定它是默认值。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-313">When adding package sources in option, when only one source is supplied, assume it's the default.</span></span>](http://nuget.codeplex.com/workitem/60)
* [<span data-ttu-id="e7eb2-314">对话框 UI 显示虚假的 "最近的" 包</span><span class="sxs-lookup"><span data-stu-id="e7eb2-314">The Dialog UI shows fake "recent" packages</span></span>](http://nuget.codeplex.com/workitem/62)
* [<span data-ttu-id="e7eb2-315">选项：单击 "取消" 不会取消更改</span><span class="sxs-lookup"><span data-stu-id="e7eb2-315">Options: Clicking cancel does not cancel changes</span></span>](http://nuget.codeplex.com/workitem/63)
* [<span data-ttu-id="e7eb2-316">添加包引用对话框搜索应该不区分大小写</span><span class="sxs-lookup"><span data-stu-id="e7eb2-316">Add Package Reference Dialog Search should be case insensitive</span></span>](http://nuget.codeplex.com/workitem/65)
* [<span data-ttu-id="e7eb2-317">修复 AssemblyInfo.cs 文件中的公司元数据</span><span class="sxs-lookup"><span data-stu-id="e7eb2-317">Fix company metadata in AssemblyInfo.cs files</span></span>](http://nuget.codeplex.com/workitem/67)
* [<span data-ttu-id="e7eb2-318">VSIX 的版本号</span><span class="sxs-lookup"><span data-stu-id="e7eb2-318">Version number for the VSIX</span></span>](http://nuget.codeplex.com/workitem/71)
* [<span data-ttu-id="e7eb2-319">删除包：使用-？显示帮助两次</span><span class="sxs-lookup"><span data-stu-id="e7eb2-319">Remove-Package: Using -? displays help twice</span></span>](http://nuget.codeplex.com/workitem/72)
* [<span data-ttu-id="e7eb2-320">执行项目级包的安装/卸载包</span><span class="sxs-lookup"><span data-stu-id="e7eb2-320">Execute install/uninstall packages for project level packages</span></span>](http://nuget.codeplex.com/workitem/74)
* [<span data-ttu-id="e7eb2-321">服务器无法在验证失败时创建源 nupack</span><span class="sxs-lookup"><span data-stu-id="e7eb2-321">Server unable to create feed when one nupack fails validation</span></span>](http://nuget.codeplex.com/workitem/90)
* [<span data-ttu-id="e7eb2-322">需要替换 NuPack 图标</span><span class="sxs-lookup"><span data-stu-id="e7eb2-322">Need to Replace NuPack Icons</span></span>](http://nuget.codeplex.com/workitem/94)
* [<span data-ttu-id="e7eb2-323">NTLM http 代理不对包源进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-323">NTLM http proxy does not authenticate to the package feed.</span></span>](http://nuget.codeplex.com/workitem/96)
* [<span data-ttu-id="e7eb2-324">对话框并不总是在 VS 窗口中居中</span><span class="sxs-lookup"><span data-stu-id="e7eb2-324">The dialog doesn't always start centered in the VS window</span></span>](http://nuget.codeplex.com/workitem/100)
* [<span data-ttu-id="e7eb2-325">包中的许多字段未在对话框中填充</span><span class="sxs-lookup"><span data-stu-id="e7eb2-325">Many of the fields in a packages details are not being populated in the dialog</span></span>](http://nuget.codeplex.com/workitem/102)
* [<span data-ttu-id="e7eb2-326">对话框 UI 不显示作者姓名</span><span class="sxs-lookup"><span data-stu-id="e7eb2-326">Dialog UI doesn't show Authors' names</span></span>](http://nuget.codeplex.com/workitem/108)
* [<span data-ttu-id="e7eb2-327">原因-删除包的版本</span><span class="sxs-lookup"><span data-stu-id="e7eb2-327">Why -Version for Remove-Package</span></span>](http://nuget.codeplex.com/workitem/113)
* [<span data-ttu-id="e7eb2-328">删除对话框 UI 上的 "最近" 选项卡</span><span class="sxs-lookup"><span data-stu-id="e7eb2-328">Remove the Recent tab on the Dialog UI</span></span>](http://nuget.codeplex.com/workitem/115)
* [<span data-ttu-id="e7eb2-329">当在对话框 UI 至少打开一次后右键单击解决方案文件夹时，VS 崩溃。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-329">VS crash when right click on solution folder after opening Dialog UI at least one.</span></span>](http://nuget.codeplex.com/workitem/126)
* [<span data-ttu-id="e7eb2-330">将 List-Package 的本地参数更改为-已安装</span><span class="sxs-lookup"><span data-stu-id="e7eb2-330">Change the -Local parameter of List-Package to -Installed</span></span>](http://nuget.codeplex.com/workitem/129)
* [<span data-ttu-id="e7eb2-331">将 packages.xml 重命名为 NuPack.config</span><span class="sxs-lookup"><span data-stu-id="e7eb2-331">Rename packages.xml to NuPack.config</span></span>](http://nuget.codeplex.com/workitem/132)
* [<span data-ttu-id="e7eb2-332">控制台强制将光标移到行尾</span><span class="sxs-lookup"><span data-stu-id="e7eb2-332">Console forces cursor to the end of line</span></span>](http://nuget.codeplex.com/workitem/135)
* [<span data-ttu-id="e7eb2-333">删除-包 intellisense 已中断</span><span class="sxs-lookup"><span data-stu-id="e7eb2-333">Remove-Package intellisense is broken</span></span>](http://nuget.codeplex.com/workitem/136)
* [<span data-ttu-id="e7eb2-334">向 nuspec 和源添加 RequireLicenseAcceptance 标志</span><span class="sxs-lookup"><span data-stu-id="e7eb2-334">Add RequireLicenseAcceptance Flag to .nuspec and Feed</span></span>](http://nuget.codeplex.com/workitem/137)
* [<span data-ttu-id="e7eb2-335">将 LicenseUrl 添加到 nuspec 格式和包源</span><span class="sxs-lookup"><span data-stu-id="e7eb2-335">Add LicenseUrl to .nuspec Format and Package Feed</span></span>](http://nuget.codeplex.com/workitem/138)
* [<span data-ttu-id="e7eb2-336">单击 "安装" 需要接受的包应显示 "接受" 对话框</span><span class="sxs-lookup"><span data-stu-id="e7eb2-336">Clicking Install For Package That Requires Acceptance Should Show Acceptance Dialog</span></span>](http://nuget.codeplex.com/workitem/139)
* [<span data-ttu-id="e7eb2-337">将免责声明文本添加到 "添加包" 对话框</span><span class="sxs-lookup"><span data-stu-id="e7eb2-337">Add Disclaimer Text to the Add Package Dialog</span></span>](http://nuget.codeplex.com/workitem/140)
* [<span data-ttu-id="e7eb2-338">首次运行包控制台时添加声明</span><span class="sxs-lookup"><span data-stu-id="e7eb2-338">Add Disclaimer When the Package Console is run the first time</span></span>](http://nuget.codeplex.com/workitem/143)
* [<span data-ttu-id="e7eb2-339">在控制台中安装包后显示声明</span><span class="sxs-lookup"><span data-stu-id="e7eb2-339">Display Disclaimer After Installing Package In The Console</span></span>](http://nuget.codeplex.com/workitem/144)
* [<span data-ttu-id="e7eb2-340">将 nupack 扩展名重命名为 nupkg。</span><span class="sxs-lookup"><span data-stu-id="e7eb2-340">Rename the .nupack extension to .nupkg</span></span>](http://nuget.codeplex.com/workitem/146)