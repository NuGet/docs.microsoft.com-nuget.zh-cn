---
title: "NuGet 1.0 和 1.1 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 1.1 的发行说明。"
keywords: "NuGet 1.1 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a596e61f144e7269f703f2dba3dddb4fd338e6a
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-10-and-11-release-notes"></a><span data-ttu-id="1051c-104">NuGet 1.0 和 1.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="1051c-104">NuGet 1.0 and 1.1 Release Notes</span></span>

[<span data-ttu-id="1051c-105">NuGet 1.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="1051c-105">NuGet 1.2 Release Notes</span></span>](../release-notes/nuget-1.2.md)

<span data-ttu-id="1051c-106">NuGet 1.0 已于 2011 年 1 月 13 日发布。</span><span class="sxs-lookup"><span data-stu-id="1051c-106">NuGet 1.0 was released on January 13, 2011.</span></span>  <span data-ttu-id="1051c-107">NuGet 1.1 已于 2011 年 2 月 12 日发布。</span><span class="sxs-lookup"><span data-stu-id="1051c-107">NuGet 1.1 was released on February 12, 2011.</span></span>

## <a name="overview"></a><span data-ttu-id="1051c-108">概述</span><span class="sxs-lookup"><span data-stu-id="1051c-108">Overview</span></span>

<span data-ttu-id="1051c-109">本文档包含 NuGet 1.0 可根据主要预览版本进行分组的各种版本的发行说明。</span><span class="sxs-lookup"><span data-stu-id="1051c-109">This document contains the release notes for the various releases of NuGet 1.0 grouped according to major preview release.</span></span>

<span data-ttu-id="1051c-110">NuGet 包括以下组件：</span><span class="sxs-lookup"><span data-stu-id="1051c-110">NuGet includes the following components:</span></span>

* <span data-ttu-id="1051c-111">*NuGet.Tools.vsix* \* 组成：</span><span class="sxs-lookup"><span data-stu-id="1051c-111">*NuGet.Tools.vsix* \* which consists of:</span></span>
  * <span data-ttu-id="1051c-112">**添加库包对话框**\* 用来浏览和安装包的 Visual Studio 中的对话框。</span><span class="sxs-lookup"><span data-stu-id="1051c-112">**Add Library Package Dialog** \* Dialog within Visual Studio used to browse and install packages.</span></span>
  * <span data-ttu-id="1051c-113">**程序包管理器控制台**\* Powershell 基于 Visual Studio 中的控制台。</span><span class="sxs-lookup"><span data-stu-id="1051c-113">**Package Manager Console** \* Powershell based console within Visual Studio.</span></span>
* <span data-ttu-id="1051c-114">*NuGet 命令行工具*\* 工具用于创建 （和最终发布） 包。</span><span class="sxs-lookup"><span data-stu-id="1051c-114">*NuGet Command Line Tool* \* Tool used to create (and eventually publish) packages.</span></span>

<span data-ttu-id="1051c-115">NuGet 工具的 Visual Studio 扩展 (*NuGet.Tools.vsix*) 要求：</span><span class="sxs-lookup"><span data-stu-id="1051c-115">The NuGet Tools Visual Studio Extension (*NuGet.Tools.vsix*) requires:</span></span>

* <span data-ttu-id="1051c-116">Visual Studio 2010 或 Visual Web Developer 2010 Express。</span><span class="sxs-lookup"><span data-stu-id="1051c-116">Visual Studio 2010 or Visual Web Developer 2010 Express.</span></span>

<span data-ttu-id="1051c-117">NuGet 命令行工具需要：</span><span class="sxs-lookup"><span data-stu-id="1051c-117">The NuGet Command Line Tool requires:</span></span>

* <span data-ttu-id="1051c-118">.NET framework 版本 4</span><span class="sxs-lookup"><span data-stu-id="1051c-118">.NET Framework Version 4</span></span>

## <a name="installation"></a><span data-ttu-id="1051c-119">安装</span><span class="sxs-lookup"><span data-stu-id="1051c-119">Installation</span></span>

<span data-ttu-id="1051c-120">若要使用此[最新版本](http://nuget.codeplex.com/releases/view/52018):</span><span class="sxs-lookup"><span data-stu-id="1051c-120">To use this [latest release](http://nuget.codeplex.com/releases/view/52018):</span></span>

* <span data-ttu-id="1051c-121">先卸载较旧生成。</span><span class="sxs-lookup"><span data-stu-id="1051c-121">First uninstall your older build.</span></span> <span data-ttu-id="1051c-122">你需要以管理员身份为此运行 VS。</span><span class="sxs-lookup"><span data-stu-id="1051c-122">You need to run VS as administrator to do this.</span></span>
* <span data-ttu-id="1051c-123">删除你具有的所有现有馈送。</span><span class="sxs-lookup"><span data-stu-id="1051c-123">Remove all the existing feeds that you have.</span></span>
* <span data-ttu-id="1051c-124">添加新的订阅源指向[http://go.microsoft.com/fwlink/?LinkId=206669](http://go.microsoft.com/fwlink/?LinkId=206669)。</span><span class="sxs-lookup"><span data-stu-id="1051c-124">Add a new feed pointing to [http://go.microsoft.com/fwlink/?LinkId=206669](http://go.microsoft.com/fwlink/?LinkId=206669).</span></span>

## <a name="nuget-11"></a><span data-ttu-id="1051c-125">NuGet 1.1</span><span class="sxs-lookup"><span data-stu-id="1051c-125">NuGet 1.1</span></span>

<span data-ttu-id="1051c-126">此版本中修复的问题列表[可在此处找到](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)</span><span class="sxs-lookup"><span data-stu-id="1051c-126">The list of issues fixed in this release [can be found here](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)</span></span>

## <a name="nuget-10-rtm"></a><span data-ttu-id="1051c-127">NuGet 1.0 RTM</span><span class="sxs-lookup"><span data-stu-id="1051c-127">NuGet 1.0 RTM</span></span>

<span data-ttu-id="1051c-128">一个问题已修复 RTM 以来 RC。</span><span class="sxs-lookup"><span data-stu-id="1051c-128">One issue was fixed for RTM since the RC.</span></span>

* [<span data-ttu-id="1051c-129">问题 474： 删除包影响解决方案中的所有项目</span><span class="sxs-lookup"><span data-stu-id="1051c-129">Issue 474: Removing Packages Affects All Project In Solution</span></span>](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a><span data-ttu-id="1051c-130">候选发布版</span><span class="sxs-lookup"><span data-stu-id="1051c-130">Release Candidate</span></span>

<span data-ttu-id="1051c-131">以下是以来 CTP 2 此候选发布版本中所做的更改。</span><span class="sxs-lookup"><span data-stu-id="1051c-131">The following are the changes made in this Release Candidate since CTP 2.</span></span> <span data-ttu-id="1051c-132">问题跟踪程序，以查看 bug 的完整列表，请访问。</span><span class="sxs-lookup"><span data-stu-id="1051c-132">Visit the Issue Tracker to see the full list of bugs.</span></span>

* [<span data-ttu-id="1051c-133">更新包从控制台不会更新依赖关系。</span><span class="sxs-lookup"><span data-stu-id="1051c-133">Updating Package from Console does not update dependencies.</span></span>](http://nuget.codeplex.com/workitem/443)
* [<span data-ttu-id="1051c-134">添加包选取 bin 不包参考 (CTP1)</span><span class="sxs-lookup"><span data-stu-id="1051c-134">Adding package picks up bin not package reference (CTP1)</span></span>](http://nuget.codeplex.com/workitem/442)
* [<span data-ttu-id="1051c-135">更新程序包离开损坏的引用</span><span class="sxs-lookup"><span data-stu-id="1051c-135">Updating a package leaves broken references</span></span>](http://nuget.codeplex.com/workitem/440)
* [<span data-ttu-id="1051c-136">获取包的更新无法正常工作，这是在对话框中，或在控制台中选择所有聚合的源</span><span class="sxs-lookup"><span data-stu-id="1051c-136">Get-Package -Updates fails in the dialog, or when the 'All' aggregate source is selected in the console</span></span>](http://nuget.codeplex.com/workitem/439)
* [<span data-ttu-id="1051c-137">获取包验证错误</span><span class="sxs-lookup"><span data-stu-id="1051c-137">Getting package verification errors</span></span>](http://nuget.codeplex.com/workitem/426)
* [<span data-ttu-id="1051c-138">用户无法从包对话框中添加安装包时警告</span><span class="sxs-lookup"><span data-stu-id="1051c-138">Warn users when a package cannot be installed from the Add Package Dialog</span></span>](http://nuget.codeplex.com/workitem/425)
* [<span data-ttu-id="1051c-139">获取包的更新包的数量大时，更新将引发</span><span class="sxs-lookup"><span data-stu-id="1051c-139">Get-Package -Updates throws when updating large number of packages</span></span>](http://nuget.codeplex.com/workitem/424)
* [<span data-ttu-id="1051c-140">提高时 nuspec 文件编写错误的错误处理</span><span class="sxs-lookup"><span data-stu-id="1051c-140">Improve error handling when nuspec files are authored incorrectly</span></span>](http://nuget.codeplex.com/workitem/423)
* [<span data-ttu-id="1051c-141">Nuget 包将忽略指定的文件</span><span class="sxs-lookup"><span data-stu-id="1051c-141">Nuget pack ignores specified files</span></span>](http://nuget.codeplex.com/workitem/422)
* [<span data-ttu-id="1051c-142">删除第二个至最后一包源，然后单击"下移"崩溃 VS</span><span class="sxs-lookup"><span data-stu-id="1051c-142">Removing the second-to-last package source and then clicking "Move Down" crashes VS</span></span>](http://nuget.codeplex.com/workitem/418)
* [<span data-ttu-id="1051c-143">安装包时移除程序集引用</span><span class="sxs-lookup"><span data-stu-id="1051c-143">Remove assembly reference while installing packages</span></span>](http://nuget.codeplex.com/workitem/413)
* [<span data-ttu-id="1051c-144">InvalidOperationException 时打开设置对话框</span><span class="sxs-lookup"><span data-stu-id="1051c-144">InvalidOperationException when opening Settings dialog</span></span>](http://nuget.codeplex.com/workitem/411)
* [<span data-ttu-id="1051c-145">在程序包管理器控制台中的程序包源的访问密钥不起作用</span><span class="sxs-lookup"><span data-stu-id="1051c-145">Access Key for Package Source in Package Manager Console doesn't work</span></span>](http://nuget.codeplex.com/workitem/410)
* [<span data-ttu-id="1051c-146">NuGet VS 设置对话框访问键将焦点移至错误字段</span><span class="sxs-lookup"><span data-stu-id="1051c-146">NuGet VS Settings Dialog Access Keys Give Focus to Wrong Fields</span></span>](http://nuget.codeplex.com/workitem/409)
* [<span data-ttu-id="1051c-147">包 ID intellisense 应不会查询太多的项</span><span class="sxs-lookup"><span data-stu-id="1051c-147">Package ID intellisense should not query too many items</span></span>](http://nuget.codeplex.com/workitem/404)
* [<span data-ttu-id="1051c-148">将包添加到项目中的项目名称的圆点字符与失败</span><span class="sxs-lookup"><span data-stu-id="1051c-148">Failure adding package to project with a dot character in the Project name</span></span>](http://nuget.codeplex.com/workitem/403)
* [<span data-ttu-id="1051c-149">Nuspec 中指定文件的问题</span><span class="sxs-lookup"><span data-stu-id="1051c-149">Issue with specified files in nuspec</span></span>](http://nuget.codeplex.com/workitem/400)
* [<span data-ttu-id="1051c-150">使用较新的生成时，应获取注册正确官方源</span><span class="sxs-lookup"><span data-stu-id="1051c-150">Correct official feed should get registered when using newer build</span></span>](http://nuget.codeplex.com/workitem/399)
* [<span data-ttu-id="1051c-151">标记应使用空格而不是 #</span><span class="sxs-lookup"><span data-stu-id="1051c-151">Tags should use spaces instead of #</span></span>](http://nuget.codeplex.com/workitem/397)
* [<span data-ttu-id="1051c-152">IPackageMetadata 缺少的一些有用信息</span><span class="sxs-lookup"><span data-stu-id="1051c-152">IPackageMetadata lacks some useful information</span></span>](http://nuget.codeplex.com/workitem/388)
* [<span data-ttu-id="1051c-153">将报告滥用行为链接添加到对话框</span><span class="sxs-lookup"><span data-stu-id="1051c-153">Add Report Abuse Link to the Dialog</span></span>](http://nuget.codeplex.com/workitem/386)
* [<span data-ttu-id="1051c-154">使用 App_Data 来解压缩包 Visual Studio 中的分隔线</span><span class="sxs-lookup"><span data-stu-id="1051c-154">Using App_Data to unzip packages breaks in Visual Studio</span></span>](http://nuget.codeplex.com/workitem/380)
* [<span data-ttu-id="1051c-155">实现标记</span><span class="sxs-lookup"><span data-stu-id="1051c-155">Implement Tags</span></span>](http://nuget.codeplex.com/workitem/376)
* [<span data-ttu-id="1051c-156">PackageBuilder 允许没有依赖项，要创建空包</span><span class="sxs-lookup"><span data-stu-id="1051c-156">PackageBuilder allows empty package with no dependencies to be created</span></span>](http://nuget.codeplex.com/workitem/373)
* [<span data-ttu-id="1051c-157">添加包的所有者字段</span><span class="sxs-lookup"><span data-stu-id="1051c-157">Add Owners Field for the Package</span></span>](http://nuget.codeplex.com/workitem/365)
* [<span data-ttu-id="1051c-158">更新 VSIX 清单可以显示为 NuGet 包管理器，而不是 VSIX 工具</span><span class="sxs-lookup"><span data-stu-id="1051c-158">Update the VSIX manifest to say NuGet Package Manager rather than VSIX Tools</span></span>](http://nuget.codeplex.com/workitem/364)
* [<span data-ttu-id="1051c-159">获取包命令将引发错误时将选择所有源</span><span class="sxs-lookup"><span data-stu-id="1051c-159">Get-Package command throws error when All source is selected</span></span>](http://nuget.codeplex.com/workitem/359)
* [<span data-ttu-id="1051c-160">允许包源选项对话框中的数据排序</span><span class="sxs-lookup"><span data-stu-id="1051c-160">Allow ordering of package sources in Options dialog</span></span>](http://nuget.codeplex.com/workitem/356)
* [<span data-ttu-id="1051c-161">更新包不会删除较旧版本</span><span class="sxs-lookup"><span data-stu-id="1051c-161">Update-Package does not remove older version</span></span>](http://nuget.codeplex.com/workitem/352)
* [<span data-ttu-id="1051c-162">依赖关系的的实现版本范围规范</span><span class="sxs-lookup"><span data-stu-id="1051c-162">Implement Version Range Specification for Dependencies</span></span>](http://nuget.codeplex.com/workitem/347)
* [<span data-ttu-id="1051c-163">单击"添加新的包"时，visual Studio 崩溃</span><span class="sxs-lookup"><span data-stu-id="1051c-163">Visual Studio crashes when clicking "Add new package"</span></span>](http://nuget.codeplex.com/workitem/346)
* [<span data-ttu-id="1051c-164">在添加包对话框中显示下载和评级</span><span class="sxs-lookup"><span data-stu-id="1051c-164">Display Downloads and Ratings in the Add Package Dialog</span></span>](http://nuget.codeplex.com/workitem/345)
* [<span data-ttu-id="1051c-165">在对话框中的包源之间更改不会获得更新活动的源</span><span class="sxs-lookup"><span data-stu-id="1051c-165">Changing between package sources in the Dialog doesn't update active source</span></span>](http://nuget.codeplex.com/workitem/344)
* [<span data-ttu-id="1051c-166">删除程序包管理器控制台窗口的键绑定</span><span class="sxs-lookup"><span data-stu-id="1051c-166">Remove Key Binding for Package Manager Console Window</span></span>](http://nuget.codeplex.com/workitem/339)
* [<span data-ttu-id="1051c-167">安装包未被识别为 cmdlet 的名称...</span><span class="sxs-lookup"><span data-stu-id="1051c-167">Install-Package is not recognized as the name of a cmdlet...</span></span>](http://nuget.codeplex.com/workitem/338)
* [<span data-ttu-id="1051c-168">从本地上正则馈送源依赖项安装程序包未解决</span><span class="sxs-lookup"><span data-stu-id="1051c-168">Installing a package from a local feed the dependencies on regular feeds are not resolved</span></span>](http://nuget.codeplex.com/workitem/332)
* [<span data-ttu-id="1051c-169">RemoveDependencies 应跳过仍在使用的依赖关系</span><span class="sxs-lookup"><span data-stu-id="1051c-169">RemoveDependencies should skip dependencies that are still in use</span></span>](http://nuget.codeplex.com/workitem/331)
* [<span data-ttu-id="1051c-170">如果正在取消页面导航，用户不能导航到其他页面时原始页请求返回</span><span class="sxs-lookup"><span data-stu-id="1051c-170">If cancelling page navigation, user cannot navigate to a different page while the original page request returns</span></span>](http://nuget.codeplex.com/workitem/325)
* [<span data-ttu-id="1051c-171">调查 NuPack.Server 性能来处理具有大量包的源。</span><span class="sxs-lookup"><span data-stu-id="1051c-171">Investigate performance of NuPack.Server for serving feeds with large number of packages.</span></span>](http://nuget.codeplex.com/workitem/324)
* [<span data-ttu-id="1051c-172">包的第二个时间筛选它使用"新建"包源，而不是以前选择的源。</span><span class="sxs-lookup"><span data-stu-id="1051c-172">The second time I filter for a package it uses the "New" package source, instead of the previously selected source.</span></span>](http://nuget.codeplex.com/workitem/321)
* [<span data-ttu-id="1051c-173">选择对话框上的"联机"选项卡时，应选择默认的程序包源。</span><span class="sxs-lookup"><span data-stu-id="1051c-173">Default package source should be selected when selecting the "Online" tab on the dialog.</span></span>](http://nuget.codeplex.com/workitem/320)
* [<span data-ttu-id="1051c-174">默认情况下，列表包应显示已安装的软件包</span><span class="sxs-lookup"><span data-stu-id="1051c-174">List-Package should show installed packages by default</span></span>](http://nuget.codeplex.com/workitem/309)
* [<span data-ttu-id="1051c-175">程序集引用 HintPaths</span><span class="sxs-lookup"><span data-stu-id="1051c-175">Assembly Reference HintPaths</span></span>](http://nuget.codeplex.com/workitem/294)
* [<span data-ttu-id="1051c-176">打开程序包管理器控制台时异常</span><span class="sxs-lookup"><span data-stu-id="1051c-176">Exception while opening Package Manager Console</span></span>](http://nuget.codeplex.com/workitem/268)
* [<span data-ttu-id="1051c-177">控制台 intellisense 下载整个源</span><span class="sxs-lookup"><span data-stu-id="1051c-177">Console intellisense downloads entire feed</span></span>](http://nuget.codeplex.com/workitem/259)
* [<span data-ttu-id="1051c-178">Default 包源应重命名为 'Active'</span><span class="sxs-lookup"><span data-stu-id="1051c-178">'Default' package source should be renamed to 'Active'</span></span>](http://nuget.codeplex.com/workitem/258)
* [<span data-ttu-id="1051c-179">包源 UI： 按确定应添加新的源，如果名称/源字段都为非空</span><span class="sxs-lookup"><span data-stu-id="1051c-179">Package sources UI: pressing OK should add the new source if Name/Source fields are non-empty</span></span>](http://nuget.codeplex.com/workitem/257)
* [<span data-ttu-id="1051c-180">已安装的包的数量很大时，对话框变得非常缓慢</span><span class="sxs-lookup"><span data-stu-id="1051c-180">Dialog becomes super slow when the number of installed packages is large</span></span>](http://nuget.codeplex.com/workitem/243)
* [<span data-ttu-id="1051c-181">支持强名称程序集绑定重定向</span><span class="sxs-lookup"><span data-stu-id="1051c-181">Support Binding Redirects for Strong Named Assemblies</span></span>](http://nuget.codeplex.com/workitem/238)
* [<span data-ttu-id="1051c-182">添加程序包引用...UI，以包括包源向下拖放</span><span class="sxs-lookup"><span data-stu-id="1051c-182">Add Package Reference... UI to include drop down for Package source</span></span>](http://nuget.codeplex.com/workitem/226)
* [<span data-ttu-id="1051c-183">NuPack 需要支持 agnostically 的配置文件名称的配置转换</span><span class="sxs-lookup"><span data-stu-id="1051c-183">NuPack needs to support config transform agnostically of the config file name</span></span>](http://nuget.codeplex.com/workitem/224)
* [<span data-ttu-id="1051c-184">允许 BasePath 要在 NuPack.exe 中的重写</span><span class="sxs-lookup"><span data-stu-id="1051c-184">Allows BasePath to be Overriden in NuPack.exe</span></span>](http://nuget.codeplex.com/workitem/222)
* [<span data-ttu-id="1051c-185">包源回退行为</span><span class="sxs-lookup"><span data-stu-id="1051c-185">Package Source Fallback Behavior</span></span>](http://nuget.codeplex.com/workitem/204)
* [<span data-ttu-id="1051c-186">有关 GUI 崩溃</span><span class="sxs-lookup"><span data-stu-id="1051c-186">Crash on GUI</span></span>](http://nuget.codeplex.com/workitem/201)
* [<span data-ttu-id="1051c-187">添加排序选项添加包对话框</span><span class="sxs-lookup"><span data-stu-id="1051c-187">Add sorting options to Add Package Dialog</span></span>](http://nuget.codeplex.com/workitem/179)
* [<span data-ttu-id="1051c-188">要清除 Package Manager Console 快捷键</span><span class="sxs-lookup"><span data-stu-id="1051c-188">shortcut key to clear the Package Manager Console</span></span>](http://nuget.codeplex.com/workitem/174)
* [<span data-ttu-id="1051c-189">PowerConsole 导致 NuPack 控制台失败</span><span class="sxs-lookup"><span data-stu-id="1051c-189">PowerConsole causes NuPack Console to fail</span></span>](http://nuget.codeplex.com/workitem/166)
* [<span data-ttu-id="1051c-190">控制台和添加包对话框应在请求中设置用户代理</span><span class="sxs-lookup"><span data-stu-id="1051c-190">Console and Add Package Dialog should set user agent in requests</span></span>](http://nuget.codeplex.com/workitem/141)
* [<span data-ttu-id="1051c-191">在生成中设置的 VSIX 和 NuPack.exe 的版本号。</span><span class="sxs-lookup"><span data-stu-id="1051c-191">Set version number of the VSIX and NuPack.exe in the build.</span></span>](http://nuget.codeplex.com/workitem/134)
* [<span data-ttu-id="1051c-192">隐藏从-常见的 PowerShell 参数？</span><span class="sxs-lookup"><span data-stu-id="1051c-192">Hide common PowerShell parameters from -?</span></span>](http://nuget.codeplex.com/workitem/118)
* [<span data-ttu-id="1051c-193">Add-有关控制台命令的详细的帮助</span><span class="sxs-lookup"><span data-stu-id="1051c-193">Add -detailed help for console commands</span></span>](http://nuget.codeplex.com/workitem/110)
* [<span data-ttu-id="1051c-194">添加包对话框应允许选择的当前程序包源</span><span class="sxs-lookup"><span data-stu-id="1051c-194">Add Package Dialog Should Allow Choosing the Current Package Source</span></span>](http://nuget.codeplex.com/workitem/88)
* [<span data-ttu-id="1051c-195">将 NuPack.Core 类移到不同的命名空间</span><span class="sxs-lookup"><span data-stu-id="1051c-195">Move NuPack.Core classes into different namespaces</span></span>](http://nuget.codeplex.com/workitem/50)
* [<span data-ttu-id="1051c-196">添加到 cmdlet 的帮助</span><span class="sxs-lookup"><span data-stu-id="1051c-196">Add help to cmdlets</span></span>](http://nuget.codeplex.com/workitem/23)
* [<span data-ttu-id="1051c-197">包下载后验证从馈送的哈希</span><span class="sxs-lookup"><span data-stu-id="1051c-197">Verify hash from feed after package download</span></span>](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a><span data-ttu-id="1051c-198">CTP 2</span><span class="sxs-lookup"><span data-stu-id="1051c-198">CTP 2</span></span>

<span data-ttu-id="1051c-199">以下是在 CTP 2 中所做的最重大更改：</span><span class="sxs-lookup"><span data-stu-id="1051c-199">The following are the most significant changes made in CTP 2:</span></span>

* <span data-ttu-id="1051c-200">切换到 OData 服务终结点从 ATOM 馈送的包： 如果你升级到 CTP2 版本的 NuGet，请务必为程序包源中添加下面的 URL: https://feed.nuget.org/ctp2/odata/v1/。</span><span class="sxs-lookup"><span data-stu-id="1051c-200">Switched the package feed from ATOM to an OData service endpoint: If you upgrade to the CTP2 version of NuGet, be sure to add the following URL as a package source: https://feed.nuget.org/ctp2/odata/v1/.</span></span>
* <span data-ttu-id="1051c-201">重命名为添加程序包命令*安装包*。</span><span class="sxs-lookup"><span data-stu-id="1051c-201">Renamed the Add-Package command to *Install-Package*.</span></span>
* <span data-ttu-id="1051c-202">更新`.nuspec`格式。</span><span class="sxs-lookup"><span data-stu-id="1051c-202">Updated the `.nuspec` Format.</span></span> <span data-ttu-id="1051c-203">`.nuspec`格式现在包括*iconUrl*字段用于指定将仅显示在包对话框中添加一个 32 x 32 png 图标。</span><span class="sxs-lookup"><span data-stu-id="1051c-203">The `.nuspec` format now includes the *iconUrl* field for specifying a 32x32 png icon which will show up in the Add Package Dialog.</span></span> <span data-ttu-id="1051c-204">因此请务必设置，若要将你的包区分开来。</span><span class="sxs-lookup"><span data-stu-id="1051c-204">So be sure to set that to distinguish your package.</span></span> <span data-ttu-id="1051c-205">`.nuspec`格式还包括新*projectUrl*字段可以用于指向提供有关你的包的详细信息的网页。</span><span class="sxs-lookup"><span data-stu-id="1051c-205">The `.nuspec` format also includes the new *projectUrl* field which you can use to point to a web page that provides more information about your package.</span></span>

<span data-ttu-id="1051c-206">此版本不会使用旧`.nupkg`文件。</span><span class="sxs-lookup"><span data-stu-id="1051c-206">This build will not work with old `.nupkg` files.</span></span> <span data-ttu-id="1051c-207">获取空引用异常时，如果你使用的旧`.nupkg`文件，并需要重建与已更新[NuGet 命令行工具](http://nuget.codeplex.com/releases/52017/download/165468)。</span><span class="sxs-lookup"><span data-stu-id="1051c-207">If you get null reference exceptions, you're using an old `.nupkg` file and need to rebuild it with the updated [NuGet command line tool](http://nuget.codeplex.com/releases/52017/download/165468).</span></span>

<span data-ttu-id="1051c-208">以下是功能和的 NuGet CTP 2 （不包括 bug 的细微的代码清理等）。 已修复的 bug 的列表。</span><span class="sxs-lookup"><span data-stu-id="1051c-208">The following is a list of features and bugs that were fixed for NuGet CTP 2 (does not include bugs for minor code cleanups etc.).</span></span>

* [<span data-ttu-id="1051c-209">错误解包的包程序集时指定的程序集 TargetFramework。</span><span class="sxs-lookup"><span data-stu-id="1051c-209">Error unpacking package assemblies when specifiying the TargetFramework for an assembly.</span></span>](http://nuget.codeplex.com/workitem/10)
* [<span data-ttu-id="1051c-210">NuPack 控制台窗口进行更容易地发现</span><span class="sxs-lookup"><span data-stu-id="1051c-210">Make NuPack Console window more discoverable</span></span>](http://nuget.codeplex.com/workitem/14)
* [<span data-ttu-id="1051c-211">ILMerge nupack.exe 版本</span><span class="sxs-lookup"><span data-stu-id="1051c-211">ILMerge the nupack.exe release</span></span>](http://nuget.codeplex.com/workitem/19)
* [<span data-ttu-id="1051c-212">更好的错误/异常处理</span><span class="sxs-lookup"><span data-stu-id="1051c-212">Better error/exception handling</span></span>](http://nuget.codeplex.com/workitem/24)
* <span data-ttu-id="1051c-213">[[Nupack.Core]: PackageManager 应妥善处理源相关的错误](http://nuget.codeplex.com/workitem/28)</span><span class="sxs-lookup"><span data-stu-id="1051c-213">[[Nupack.Core]: PackageManager should gracefully handle feed-related errors](http://nuget.codeplex.com/workitem/28)</span></span>
* [<span data-ttu-id="1051c-214">为控制台需要新建图标</span><span class="sxs-lookup"><span data-stu-id="1051c-214">Need a new icon for the console</span></span>](http://nuget.codeplex.com/workitem/29)
* [<span data-ttu-id="1051c-215">在对话框中的字符串本地化</span><span class="sxs-lookup"><span data-stu-id="1051c-215">Localize strings in the Dialog</span></span>](http://nuget.codeplex.com/workitem/38)
* [<span data-ttu-id="1051c-216">NuPack 缓存下载.nupack 在内存中的文件</span><span class="sxs-lookup"><span data-stu-id="1051c-216">NuPack caches downloaded .nupack files in memory</span></span>](http://nuget.codeplex.com/workitem/40)
* [<span data-ttu-id="1051c-217">NuPack 控制台： 更改用于显示控制台的默认快捷方式</span><span class="sxs-lookup"><span data-stu-id="1051c-217">NuPack Console: Change the default shortcut for displaying console</span></span>](http://nuget.codeplex.com/workitem/48)
* [<span data-ttu-id="1051c-218">ProjectSystem 应支持的公共属性的默认值</span><span class="sxs-lookup"><span data-stu-id="1051c-218">ProjectSystem should support default values for common properties</span></span>](http://nuget.codeplex.com/workitem/49)
* [<span data-ttu-id="1051c-219">使用一个 nuspec 文件的文件夹中运行 nupack.exe 应使用该 nuspec</span><span class="sxs-lookup"><span data-stu-id="1051c-219">Running nupack.exe in a folder with just one nuspec file should use that nuspec</span></span>](http://nuget.codeplex.com/workitem/52)
* [<span data-ttu-id="1051c-220">即使在加载没有项目/解决方案时将显示项目菜单</span><span class="sxs-lookup"><span data-stu-id="1051c-220">Project Menu Shows Up Even When No Project/Solution Is Loaded</span></span>](http://nuget.codeplex.com/workitem/54)
* [<span data-ttu-id="1051c-221">对基本代码的干净克隆 build.cmd 失败</span><span class="sxs-lookup"><span data-stu-id="1051c-221">build.cmd fails on a clean clone of the codebase</span></span>](http://nuget.codeplex.com/workitem/56)
* [<span data-ttu-id="1051c-222">更新可用功能</span><span class="sxs-lookup"><span data-stu-id="1051c-222">Updates available feature</span></span>](http://nuget.codeplex.com/workitem/57)
* [<span data-ttu-id="1051c-223">对话框： 添加包通过对话框中会删除提示在控制台中</span><span class="sxs-lookup"><span data-stu-id="1051c-223">Dialog: Adding a package through the dialog removes the prompt in the console</span></span>](http://nuget.codeplex.com/workitem/73)
* [<span data-ttu-id="1051c-224">通过单击安装来添加包通常速度慢，没有可视反馈</span><span class="sxs-lookup"><span data-stu-id="1051c-224">Adding a package by clicking 'Install' is often slow, with no visual feedback</span></span>](http://nuget.codeplex.com/workitem/80)
* [<span data-ttu-id="1051c-225">没有方法来发现哪些我已安装的程序包具有更新。</span><span class="sxs-lookup"><span data-stu-id="1051c-225">There is no way to discover which of my installed packages have updates.</span></span>](http://nuget.codeplex.com/workitem/82)
* [<span data-ttu-id="1051c-226">没有方法以更新对话框中的已安装的程序包。</span><span class="sxs-lookup"><span data-stu-id="1051c-226">There is no way to update an installed package in the dialog.</span></span>](http://nuget.codeplex.com/workitem/83)
* [<span data-ttu-id="1051c-227">无法卸载对话框中的安装的包</span><span class="sxs-lookup"><span data-stu-id="1051c-227">There is no way to uninstall an installed package in the dialog</span></span>](http://nuget.codeplex.com/workitem/84)
* [<span data-ttu-id="1051c-228">&ldquo;添加程序包引用&hellip;&rdquo;出现在上下文菜单中的已安装的引用</span><span class="sxs-lookup"><span data-stu-id="1051c-228">&ldquo;Add Package Reference&hellip;&rdquo; appears on the context menu of installed references</span></span>](http://nuget.codeplex.com/workitem/85)
* [<span data-ttu-id="1051c-229">更新后从控制台的包，它显示了旧版本和最新版本为已安装</span><span class="sxs-lookup"><span data-stu-id="1051c-229">After updating a package from the console, it shows both the old version and the new version as installed</span></span>](http://nuget.codeplex.com/workitem/86)
* [<span data-ttu-id="1051c-230">活动在控制台中，在使用对话框中，在使用后就会消失</span><span class="sxs-lookup"><span data-stu-id="1051c-230">The activity in the console, when using the dialog, disappears after use</span></span>](http://nuget.codeplex.com/workitem/87)
* [<span data-ttu-id="1051c-231">清除命令行分析中 nupack.exe</span><span class="sxs-lookup"><span data-stu-id="1051c-231">Cleanup command line parsing in nupack.exe</span></span>](http://nuget.codeplex.com/workitem/89)
* [<span data-ttu-id="1051c-232">将一个友好名称添加到包源</span><span class="sxs-lookup"><span data-stu-id="1051c-232">Add a friendly name to package sources</span></span>](http://nuget.codeplex.com/workitem/98)
* [<span data-ttu-id="1051c-233">更新.nuspec 以支持包括包图标</span><span class="sxs-lookup"><span data-stu-id="1051c-233">Update .nuspec to support including package icons</span></span>](http://nuget.codeplex.com/workitem/103)
* [<span data-ttu-id="1051c-234">源的 UI 不允许复制 URL</span><span class="sxs-lookup"><span data-stu-id="1051c-234">Feed UI doesn't allow copying the URL</span></span>](http://nuget.codeplex.com/workitem/105)
* [<span data-ttu-id="1051c-235">更好删除包的错误处理。</span><span class="sxs-lookup"><span data-stu-id="1051c-235">Better remove-package error handling.</span></span>](http://nuget.codeplex.com/workitem/107)
* [<span data-ttu-id="1051c-236">在控制台窗口中键入取决于游标焦点</span><span class="sxs-lookup"><span data-stu-id="1051c-236">Typing in Console Window depends on cursor focus</span></span>](http://nuget.codeplex.com/workitem/112)
* [<span data-ttu-id="1051c-237">错误消息查找很多次</span><span class="sxs-lookup"><span data-stu-id="1051c-237">Error messages look awful</span></span>](http://nuget.codeplex.com/workitem/116)
* [<span data-ttu-id="1051c-238">删除包的包的未安装的性能已损坏</span><span class="sxs-lookup"><span data-stu-id="1051c-238">The performance of Remove-Package for a package that isn't installed is bad</span></span>](http://nuget.codeplex.com/workitem/117)
* [<span data-ttu-id="1051c-239">删除程序包失败时没有包源</span><span class="sxs-lookup"><span data-stu-id="1051c-239">Removing a package fails when there are no package sources</span></span>](http://nuget.codeplex.com/workitem/119)
* [<span data-ttu-id="1051c-240">失败的包源不存在时删除包</span><span class="sxs-lookup"><span data-stu-id="1051c-240">Remove-Package fails when the package source is unavailable</span></span>](http://nuget.codeplex.com/workitem/120)
* [<span data-ttu-id="1051c-241">添加到包元数据和源的标题。</span><span class="sxs-lookup"><span data-stu-id="1051c-241">Add Title to the package metadata and the feed.</span></span>](http://nuget.codeplex.com/workitem/125)
* [<span data-ttu-id="1051c-242">添加回添加包-源参数</span><span class="sxs-lookup"><span data-stu-id="1051c-242">Add the -Source parameter back to Add-Package</span></span>](http://nuget.codeplex.com/workitem/127)
* [<span data-ttu-id="1051c-243">列出程序包应有-源参数</span><span class="sxs-lookup"><span data-stu-id="1051c-243">List-Package should have a -Source parameter</span></span>](http://nuget.codeplex.com/workitem/128)
* [<span data-ttu-id="1051c-244">更新 NuPack.Server 需要 NuPack 用户代理到下载更新包</span><span class="sxs-lookup"><span data-stu-id="1051c-244">Update NuPack.Server to require NuPack User Agent To Download Package</span></span>](http://nuget.codeplex.com/workitem/142)
* [<span data-ttu-id="1051c-245">许可证接受对话框必须对所有依赖项，要求用户接受列出许可证</span><span class="sxs-lookup"><span data-stu-id="1051c-245">License Acceptance Dialog Must List Licenses For All Dependencies That Require Acceptance</span></span>](http://nuget.codeplex.com/workitem/145)
* [<span data-ttu-id="1051c-246">在包源中引发时记录错误</span><span class="sxs-lookup"><span data-stu-id="1051c-246">Log an error when a package throws in the feed</span></span>](http://nuget.codeplex.com/workitem/150)
* [<span data-ttu-id="1051c-247">NuPack.exe 不应允许一个空&lt;licenseurl&gt;元素</span><span class="sxs-lookup"><span data-stu-id="1051c-247">NuPack.exe should not allow an empty &lt;licenseurl&gt; element</span></span>](http://nuget.codeplex.com/workitem/152)
* [<span data-ttu-id="1051c-248">将列出程序包重命名为 Get 包，添加的包安装包和删除包到卸载包</span><span class="sxs-lookup"><span data-stu-id="1051c-248">Rename List-Package to Get-Package, Add-Package to Install-Package, and Remove-Package to Uninstall-Package</span></span>](http://nuget.codeplex.com/workitem/155)
* [<span data-ttu-id="1051c-249">使用从解决方案导航器的添加程序包引用菜单项使 Visual Studio 崩溃</span><span class="sxs-lookup"><span data-stu-id="1051c-249">Using the Add Package Reference menu item from the Solution Navigator crashes Visual Studio</span></span>](http://nuget.codeplex.com/workitem/158)
* [<span data-ttu-id="1051c-250">"可用包源"标签缺少冒号</span><span class="sxs-lookup"><span data-stu-id="1051c-250">"Available package sources" label is missing a colon</span></span>](http://nuget.codeplex.com/workitem/160)
* [<span data-ttu-id="1051c-251">请.nuspec xml 元素的大小写一致地 camel 大小写形式</span><span class="sxs-lookup"><span data-stu-id="1051c-251">Make .nuspec xml element casing consistently camel cased</span></span>](http://nuget.codeplex.com/workitem/161)
* [<span data-ttu-id="1051c-252">NuPack VSIX 清单需要开启 admin 位</span><span class="sxs-lookup"><span data-stu-id="1051c-252">The NuPack VSIX's manifest needs to turn on the 'admin' bit</span></span>](http://nuget.codeplex.com/workitem/162)
* [<span data-ttu-id="1051c-253">如果你运行了任何源的列表包，则出现 null ref 错误</span><span class="sxs-lookup"><span data-stu-id="1051c-253">If you run List-Package with no feeds, you get null ref error</span></span>](http://nuget.codeplex.com/workitem/164)
* [<span data-ttu-id="1051c-254">nuget.exe： 指定目标路径</span><span class="sxs-lookup"><span data-stu-id="1051c-254">nuget.exe: specify destination path</span></span>](http://nuget.codeplex.com/workitem/171)
* [<span data-ttu-id="1051c-255">Powershell 错误打开 WinXP 上的包管理控制台</span><span class="sxs-lookup"><span data-stu-id="1051c-255">Powershell Errors Opening Package Management Console on WinXP</span></span>](http://nuget.codeplex.com/workitem/175)
* [<span data-ttu-id="1051c-256">尝试加载包列表时的 VS 崩溃</span><span class="sxs-lookup"><span data-stu-id="1051c-256">VS Crashes while trying to load package list</span></span>](http://nuget.codeplex.com/workitem/176)
* [<span data-ttu-id="1051c-257">允许元程序包 （没有文件，只有依赖关系）</span><span class="sxs-lookup"><span data-stu-id="1051c-257">allow meta packages (no files, only dependencies)</span></span>](http://nuget.codeplex.com/workitem/180)
* [<span data-ttu-id="1051c-258">将 Powershell 脚本转换为 Powershell 2.0 模块</span><span class="sxs-lookup"><span data-stu-id="1051c-258">Convert Powershell Script to Powershell 2.0 Module</span></span>](http://nuget.codeplex.com/workitem/181)
* [<span data-ttu-id="1051c-259">指定目标时，PathResolver 应丢弃路径部分前面通配符字符</span><span class="sxs-lookup"><span data-stu-id="1051c-259">PathResolver should discard path portion preceeding wildcard characters when target is specified</span></span>](http://nuget.codeplex.com/workitem/183)
* [<span data-ttu-id="1051c-260">没有依赖关系</span><span class="sxs-lookup"><span data-stu-id="1051c-260">No dependencies</span></span>](http://nuget.codeplex.com/workitem/186)
* [<span data-ttu-id="1051c-261">安装 Elmah 时出错</span><span class="sxs-lookup"><span data-stu-id="1051c-261">Error installing Elmah</span></span>](http://nuget.codeplex.com/workitem/192)
* [<span data-ttu-id="1051c-262">配置转换不正常使用&lt;configsections&gt;</span><span class="sxs-lookup"><span data-stu-id="1051c-262">Config transforms don't work correctly with &lt;configsections&gt;</span></span>](http://nuget.codeplex.com/workitem/194)
* [<span data-ttu-id="1051c-263">变量 $全局： projectCache 无法检索，因为尚未设置</span><span class="sxs-lookup"><span data-stu-id="1051c-263">The variable '$global:projectCache' cannot be retrieved because it has not been set</span></span>](http://nuget.codeplex.com/workitem/203)
* [<span data-ttu-id="1051c-264">添加用于创建 NuPack 程序包的 MSBuild 任务</span><span class="sxs-lookup"><span data-stu-id="1051c-264">Add MSBuild task for creating NuPack packages</span></span>](http://nuget.codeplex.com/workitem/205)
* [<span data-ttu-id="1051c-265">需要支持搜索/筛选列表程序包</span><span class="sxs-lookup"><span data-stu-id="1051c-265">list-package needs to support searching/filtering</span></span>](http://nuget.codeplex.com/workitem/206)
* [<span data-ttu-id="1051c-266">始终为许可证显示一个链接，如果程序包作者提供了一个许可证 URL</span><span class="sxs-lookup"><span data-stu-id="1051c-266">Always display a link to license if the package author provides a license URL</span></span>](http://nuget.codeplex.com/workitem/208)
* [<span data-ttu-id="1051c-267">使用删除包偶尔发生"拒绝访问"异常</span><span class="sxs-lookup"><span data-stu-id="1051c-267">Occasional "Access Denied" exception with Remove-Package</span></span>](http://nuget.codeplex.com/workitem/213)
* [<span data-ttu-id="1051c-268">未通过的单元测试： InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries</span><span class="sxs-lookup"><span data-stu-id="1051c-268">Unit Tests Failing: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries</span></span>](http://nuget.codeplex.com/workitem/214)
* [<span data-ttu-id="1051c-269">如果找不到特定 framework 版本，允许回退/默认组的文件</span><span class="sxs-lookup"><span data-stu-id="1051c-269">Allow for a fallback/default set of files if a specfic framework version cannot be found</span></span>](http://nuget.codeplex.com/workitem/223)
* [<span data-ttu-id="1051c-270">添加程序包引用...UI 中不能删除包</span><span class="sxs-lookup"><span data-stu-id="1051c-270">Add Package Reference... UI cannot remove a package</span></span>](http://nuget.codeplex.com/workitem/225)
* [<span data-ttu-id="1051c-271">添加程序包引用崩溃 studio 时一个或多个项目已卸载</span><span class="sxs-lookup"><span data-stu-id="1051c-271">Add Package Reference crashes studio when one or more project is unloaded</span></span>](http://nuget.codeplex.com/workitem/228)
* [<span data-ttu-id="1051c-272">配置转换似乎未处理 web.debug.config 文件</span><span class="sxs-lookup"><span data-stu-id="1051c-272">Config transform does not appear to work on web.debug.config file</span></span>](http://nuget.codeplex.com/workitem/229)
* [<span data-ttu-id="1051c-273">init.ps1 未触发上自定义包</span><span class="sxs-lookup"><span data-stu-id="1051c-273">init.ps1 not firing on custom package</span></span>](http://nuget.codeplex.com/workitem/237)
* [<span data-ttu-id="1051c-274">将路径添加到 feedlist，默认按钮时将设置为确定，因此如果按下 enter 键会自动关闭</span><span class="sxs-lookup"><span data-stu-id="1051c-274">When adding paths to the feedlist, the default button is set to OK, so if I press ENTER it automatically closes</span></span>](http://nuget.codeplex.com/workitem/240)
* [<span data-ttu-id="1051c-275">尝试卸载依赖关系将崩溃 VS，如果在行中尝试 2 次</span><span class="sxs-lookup"><span data-stu-id="1051c-275">Attempt to uninstall a dependency will crash VS if attempted 2 times in a row</span></span>](http://nuget.codeplex.com/workitem/241)
* [<span data-ttu-id="1051c-276">在添加包对话框中显示项目 URL</span><span class="sxs-lookup"><span data-stu-id="1051c-276">Display the Project URL in the Add Package dialog</span></span>](http://nuget.codeplex.com/workitem/253)
* [<span data-ttu-id="1051c-277">默认安装的程序包添加包对话框</span><span class="sxs-lookup"><span data-stu-id="1051c-277">Default the Add-Package dialog to Installed Packages</span></span>](http://nuget.codeplex.com/workitem/254)
* [<span data-ttu-id="1051c-278">更改添加包对话框菜单项。</span><span class="sxs-lookup"><span data-stu-id="1051c-278">Change Add Package Dialog menu item.</span></span>](http://nuget.codeplex.com/workitem/261)
* [<span data-ttu-id="1051c-279">重命名命名空间和程序集</span><span class="sxs-lookup"><span data-stu-id="1051c-279">Rename namespaces and assemblies</span></span>](http://nuget.codeplex.com/workitem/274)
* [<span data-ttu-id="1051c-280">将 NuPack 项目重命名为 NuGet</span><span class="sxs-lookup"><span data-stu-id="1051c-280">Rename the NuPack Project to NuGet</span></span>](http://nuget.codeplex.com/workitem/282)
* [<span data-ttu-id="1051c-281">添加以下文本下的依赖关系列表</span><span class="sxs-lookup"><span data-stu-id="1051c-281">Add the following text under the list of dependencies</span></span>](http://nuget.codeplex.com/workitem/288)
* [<span data-ttu-id="1051c-282">更改许可证接受对话框中的许可证接受文本</span><span class="sxs-lookup"><span data-stu-id="1051c-282">Change the license acceptance text in the License Acceptance Dialog</span></span>](http://nuget.codeplex.com/workitem/291)
* [<span data-ttu-id="1051c-283">更改包的列表上面许可证接受对话框中的文本</span><span class="sxs-lookup"><span data-stu-id="1051c-283">Change the text in the License Acceptance Dialog above the list of packages</span></span>](http://nuget.codeplex.com/workitem/292)
* [<span data-ttu-id="1051c-284">OData 不适用于 fwlink URL</span><span class="sxs-lookup"><span data-stu-id="1051c-284">OData doesn't work with an fwlink URL</span></span>](http://nuget.codeplex.com/workitem/304)
* [<span data-ttu-id="1051c-285">通过用于分页的包计数的主动缓存的程序包管理器 UI:</span><span class="sxs-lookup"><span data-stu-id="1051c-285">Package Manager UI: Over aggressive caching of package count used for paging</span></span>](http://nuget.codeplex.com/workitem/317)
* [<span data-ttu-id="1051c-286">NuPack / NuGet-&gt;程序包管理器控制台错误</span><span class="sxs-lookup"><span data-stu-id="1051c-286">NuPack / NuGet -&gt; Package Manager Console error</span></span>](http://nuget.codeplex.com/workitem/335)
* [<span data-ttu-id="1051c-287">添加包对话框显示许可证接受为已安装打包</span><span class="sxs-lookup"><span data-stu-id="1051c-287">Add Package Dialog shows License Acceptance For Already Installed Packaged</span></span>](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a><span data-ttu-id="1051c-288">CTP 1</span><span class="sxs-lookup"><span data-stu-id="1051c-288">CTP 1</span></span>

<span data-ttu-id="1051c-289">以下是功能和 NuGet CTP 1 已修复的 bug 的列表。</span><span class="sxs-lookup"><span data-stu-id="1051c-289">The following is a list of features and bugs that were fixed for NuGet CTP 1.</span></span>

* [<span data-ttu-id="1051c-290">包扩展应重命名为.nupack</span><span class="sxs-lookup"><span data-stu-id="1051c-290">Package extension should be renamed to .nupack</span></span>](http://nuget.codeplex.com/workitem/1)
* [<span data-ttu-id="1051c-291">将包文件移到文件夹</span><span class="sxs-lookup"><span data-stu-id="1051c-291">Move package file into folder</span></span>](http://nuget.codeplex.com/workitem/2)
* [<span data-ttu-id="1051c-292">合并安装&amp;添加 PS 命令</span><span class="sxs-lookup"><span data-stu-id="1051c-292">Merge install &amp; Add PS commands</span></span>](http://nuget.codeplex.com/workitem/3)
* [<span data-ttu-id="1051c-293">为动词-名词的 cmdlet 创建别名</span><span class="sxs-lookup"><span data-stu-id="1051c-293">Create aliases for Verb-Noun cmdlets</span></span>](http://nuget.codeplex.com/workitem/4)
* [<span data-ttu-id="1051c-294">在 VS 中切换解决方案时，获取混淆 NuPack</span><span class="sxs-lookup"><span data-stu-id="1051c-294">NuPack gets confused when switching solution in VS</span></span>](http://nuget.codeplex.com/workitem/6)
* [<span data-ttu-id="1051c-295">我们将默认情况下隐藏的包解决方案文件夹</span><span class="sxs-lookup"><span data-stu-id="1051c-295">We should hide the 'packages' solution folder by default</span></span>](http://nuget.codeplex.com/workitem/11)
* [<span data-ttu-id="1051c-296">在内容项添加标记替换的支持。</span><span class="sxs-lookup"><span data-stu-id="1051c-296">Add support for token replacement in content items.</span></span>](http://nuget.codeplex.com/workitem/12)
* [<span data-ttu-id="1051c-297">NuPack.UI 应使用 PackageSource API</span><span class="sxs-lookup"><span data-stu-id="1051c-297">NuPack.UI should use the PackageSource API</span></span>](http://nuget.codeplex.com/workitem/26)
* <span data-ttu-id="1051c-298">[[Nupack.Core]: PackageManager 会将包标记为安装它们之前，安装](http://nuget.codeplex.com/workitem/27)</span><span class="sxs-lookup"><span data-stu-id="1051c-298">[[Nupack.Core]: PackageManager marks packages as installed prior to installing them](http://nuget.codeplex.com/workitem/27)</span></span>
* [<span data-ttu-id="1051c-299">删除默认项目从解决方案仍为默认值会显示已删除的项目</span><span class="sxs-lookup"><span data-stu-id="1051c-299">Deleting default project from solution still shows the deleted project as default</span></span>](http://nuget.codeplex.com/workitem/30)
* [<span data-ttu-id="1051c-300">新包将会失败并"不能将部件添加为指定的 URI 因为它已在包中。"</span><span class="sxs-lookup"><span data-stu-id="1051c-300">New-Package fails with "Cannot add part for the specified URI because it's already in the package."</span></span>](http://nuget.codeplex.com/workitem/32)
* [<span data-ttu-id="1051c-301">从 Visual Studio GUI 中删除"NuPack"字符串</span><span class="sxs-lookup"><span data-stu-id="1051c-301">Remove "NuPack" strings from Visual Studio GUI</span></span>](http://nuget.codeplex.com/workitem/35)
* [<span data-ttu-id="1051c-302">添加 COPYRIGHT.txt 到 Apache 标头文件</span><span class="sxs-lookup"><span data-stu-id="1051c-302">Add Apache Header To a COPYRIGHT.txt file</span></span>](http://nuget.codeplex.com/workitem/36)
* [<span data-ttu-id="1051c-303">删除更新 PackageSource 命令</span><span class="sxs-lookup"><span data-stu-id="1051c-303">Remove Update-PackageSource Command</span></span>](http://nuget.codeplex.com/workitem/37)
* [<span data-ttu-id="1051c-304">程序包管理器不可用，加载配置文件时将引发异常</span><span class="sxs-lookup"><span data-stu-id="1051c-304">Package Manager unusable when loading profile throws an exception</span></span>](http://nuget.codeplex.com/workitem/39)
* [<span data-ttu-id="1051c-305">init.ps1 install.ps1，uninstall.ps1 需要接收其他状态</span><span class="sxs-lookup"><span data-stu-id="1051c-305">init.ps1, install.ps1 and uninstall.ps1 need to receive additional state</span></span>](http://nuget.codeplex.com/workitem/41)
* [<span data-ttu-id="1051c-306">将控制台和 GUI 包合并到一个包</span><span class="sxs-lookup"><span data-stu-id="1051c-306">Combine Console and GUI Packages Into One Package</span></span>](http://nuget.codeplex.com/workitem/42)
* [<span data-ttu-id="1051c-307">Xml 转换逻辑不起作用，如果应用于文件夹不是根目录的 XML</span><span class="sxs-lookup"><span data-stu-id="1051c-307">Xml transform logic doesn't work if applied to XML that isn't at the root</span></span>](http://nuget.codeplex.com/workitem/43)
* [<span data-ttu-id="1051c-308">管理包源设置对话框不更新 NuPack 控制台</span><span class="sxs-lookup"><span data-stu-id="1051c-308">Manage package sources settings dialog not updating the NuPack console</span></span>](http://nuget.codeplex.com/workitem/44)
* [<span data-ttu-id="1051c-309">NuPack 控制台用户界面： 重命名为包源的包源下拉列表</span><span class="sxs-lookup"><span data-stu-id="1051c-309">NuPack Console UI: Rename 'Package feed' drop-down list to 'Package source'</span></span>](http://nuget.codeplex.com/workitem/45)
* [<span data-ttu-id="1051c-310">NuPack 控制台选项： 重命名存储库 UI，以与 NuPack 控制台保持一致</span><span class="sxs-lookup"><span data-stu-id="1051c-310">NuPack Console Options: Rename 'Repository UI' to be consistent with NuPack Console</span></span>](http://nuget.codeplex.com/workitem/46)
* [<span data-ttu-id="1051c-311">针对从 IIS 或 URL 已打开的网站添加包失败</span><span class="sxs-lookup"><span data-stu-id="1051c-311">Add-Package fails against a website that was opened from IIS or a URL</span></span>](http://nuget.codeplex.com/workitem/53)
* [<span data-ttu-id="1051c-312">程序包管理器源不能使用 FwLink</span><span class="sxs-lookup"><span data-stu-id="1051c-312">Package Manager Source Doesn't Work With FwLink</span></span>](http://nuget.codeplex.com/workitem/55)
* [<span data-ttu-id="1051c-313">设置默认的程序包源</span><span class="sxs-lookup"><span data-stu-id="1051c-313">Set the default package source</span></span>](http://nuget.codeplex.com/workitem/59)
* [<span data-ttu-id="1051c-314">当提供只有一个源时，请在选项中，添加包源，则假定它是默认设置。</span><span class="sxs-lookup"><span data-stu-id="1051c-314">When adding package sources in option, when only one source is supplied, assume it's the default.</span></span>](http://nuget.codeplex.com/workitem/60)
* [<span data-ttu-id="1051c-315">对话框用户界面显示了假"最近"的程序包</span><span class="sxs-lookup"><span data-stu-id="1051c-315">The Dialog UI shows fake "recent" packages</span></span>](http://nuget.codeplex.com/workitem/62)
* [<span data-ttu-id="1051c-316">选项： 单击取消按钮不会取消更改</span><span class="sxs-lookup"><span data-stu-id="1051c-316">Options: Clicking cancel does not cancel changes</span></span>](http://nuget.codeplex.com/workitem/63)
* [<span data-ttu-id="1051c-317">添加包引用对话框搜索应区分大小写</span><span class="sxs-lookup"><span data-stu-id="1051c-317">Add Package Reference Dialog Search should be case insensitive</span></span>](http://nuget.codeplex.com/workitem/65)
* [<span data-ttu-id="1051c-318">修复 AssemblyInfo.cs 文件中的公司元数据</span><span class="sxs-lookup"><span data-stu-id="1051c-318">Fix company metadata in AssemblyInfo.cs files</span></span>](http://nuget.codeplex.com/workitem/67)
* [<span data-ttu-id="1051c-319">Vsix 的版本号</span><span class="sxs-lookup"><span data-stu-id="1051c-319">Version number for the VSIX</span></span>](http://nuget.codeplex.com/workitem/71)
* [<span data-ttu-id="1051c-320">删除包： 使用-？显示帮助两次</span><span class="sxs-lookup"><span data-stu-id="1051c-320">Remove-Package: Using -? displays help twice</span></span>](http://nuget.codeplex.com/workitem/72)
* [<span data-ttu-id="1051c-321">执行项目级别包安装/卸载包</span><span class="sxs-lookup"><span data-stu-id="1051c-321">Execute install/uninstall packages for project level packages</span></span>](http://nuget.codeplex.com/workitem/74)
* [<span data-ttu-id="1051c-322">服务器无法验证一个 nupack 失败时创建源</span><span class="sxs-lookup"><span data-stu-id="1051c-322">Server unable to create feed when one nupack fails validation</span></span>](http://nuget.codeplex.com/workitem/90)
* [<span data-ttu-id="1051c-323">需要更换 NuPack 图标</span><span class="sxs-lookup"><span data-stu-id="1051c-323">Need to Replace NuPack Icons</span></span>](http://nuget.codeplex.com/workitem/94)
* [<span data-ttu-id="1051c-324">NTLM http 代理的身份验证不到包源。</span><span class="sxs-lookup"><span data-stu-id="1051c-324">NTLM http proxy does not authenticate to the package feed.</span></span>](http://nuget.codeplex.com/workitem/96)
* [<span data-ttu-id="1051c-325">对话框不会始终为中心 VS 在窗口中启动</span><span class="sxs-lookup"><span data-stu-id="1051c-325">The dialog doesn't always start centered in the VS window</span></span>](http://nuget.codeplex.com/workitem/100)
* [<span data-ttu-id="1051c-326">许多包详细信息中的字段不会被填充在对话框中</span><span class="sxs-lookup"><span data-stu-id="1051c-326">Many of the fields in a packages details are not being populated in the dialog</span></span>](http://nuget.codeplex.com/workitem/102)
* [<span data-ttu-id="1051c-327">对话框 UI 不显示作者的名称</span><span class="sxs-lookup"><span data-stu-id="1051c-327">Dialog UI doesn't show Authors' names</span></span>](http://nuget.codeplex.com/workitem/108)
* [<span data-ttu-id="1051c-328">为什么-删除包的版本</span><span class="sxs-lookup"><span data-stu-id="1051c-328">Why -Version for Remove-Package</span></span>](http://nuget.codeplex.com/workitem/113)
* [<span data-ttu-id="1051c-329">删除对话框 UI 上的新选项卡</span><span class="sxs-lookup"><span data-stu-id="1051c-329">Remove the Recent tab on the Dialog UI</span></span>](http://nuget.codeplex.com/workitem/115)
* [<span data-ttu-id="1051c-330">VS 崩溃时正确打开对话框 UI 至少一个后单击解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="1051c-330">VS crash when right click on solution folder after opening Dialog UI at least one.</span></span>](http://nuget.codeplex.com/workitem/126)
* [<span data-ttu-id="1051c-331">更改列表包-本地参数到-安装</span><span class="sxs-lookup"><span data-stu-id="1051c-331">Change the -Local parameter of List-Package to -Installed</span></span>](http://nuget.codeplex.com/workitem/129)
* [<span data-ttu-id="1051c-332">将 packages.xml 重命名为 NuPack.config</span><span class="sxs-lookup"><span data-stu-id="1051c-332">Rename packages.xml to NuPack.config</span></span>](http://nuget.codeplex.com/workitem/132)
* [<span data-ttu-id="1051c-333">控制台强制光标到行的末尾</span><span class="sxs-lookup"><span data-stu-id="1051c-333">Console forces cursor to the end of line</span></span>](http://nuget.codeplex.com/workitem/135)
* [<span data-ttu-id="1051c-334">删除包 intellisense 已中断</span><span class="sxs-lookup"><span data-stu-id="1051c-334">Remove-Package intellisense is broken</span></span>](http://nuget.codeplex.com/workitem/136)
* [<span data-ttu-id="1051c-335">将 RequireLicenseAcceptance 标志添加到.nuspec 和源</span><span class="sxs-lookup"><span data-stu-id="1051c-335">Add RequireLicenseAcceptance Flag to .nuspec and Feed</span></span>](http://nuget.codeplex.com/workitem/137)
* [<span data-ttu-id="1051c-336">添加 LicenseUrl.nuspec 格式和包源</span><span class="sxs-lookup"><span data-stu-id="1051c-336">Add LicenseUrl to .nuspec Format and Package Feed</span></span>](http://nuget.codeplex.com/workitem/138)
* [<span data-ttu-id="1051c-337">单击需要接受的包的安装应显示接受对话框</span><span class="sxs-lookup"><span data-stu-id="1051c-337">Clicking Install For Package That Requires Acceptance Should Show Acceptance Dialog</span></span>](http://nuget.codeplex.com/workitem/139)
* [<span data-ttu-id="1051c-338">将免责声明文本添加到添加包对话框</span><span class="sxs-lookup"><span data-stu-id="1051c-338">Add Disclaimer Text to the Add Package Dialog</span></span>](http://nuget.codeplex.com/workitem/140)
* [<span data-ttu-id="1051c-339">添加免责声明时包控制台运行第一次</span><span class="sxs-lookup"><span data-stu-id="1051c-339">Add Disclaimer When the Package Console is run the first time</span></span>](http://nuget.codeplex.com/workitem/143)
* [<span data-ttu-id="1051c-340">在控制台中安装包后显示免责声明</span><span class="sxs-lookup"><span data-stu-id="1051c-340">Display Disclaimer After Installing Package In The Console</span></span>](http://nuget.codeplex.com/workitem/144)
* [<span data-ttu-id="1051c-341">将.nupack 扩展重命名为.nupkg</span><span class="sxs-lookup"><span data-stu-id="1051c-341">Rename the .nupack extension to .nupkg</span></span>](http://nuget.codeplex.com/workitem/146)