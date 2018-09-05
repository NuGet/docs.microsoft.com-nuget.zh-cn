---
title: NuGet 1.0 和 1.1 版发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 1.1 发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6222a996f2fdcaaa81a1b16d1c6da2749936712a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547016"
---
# <a name="nuget-10-and-11-release-notes"></a><span data-ttu-id="43a8e-103">NuGet 1.0 和 1.1 版发行说明</span><span class="sxs-lookup"><span data-stu-id="43a8e-103">NuGet 1.0 and 1.1 Release Notes</span></span>

[<span data-ttu-id="43a8e-104">NuGet 1.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="43a8e-104">NuGet 1.2 Release Notes</span></span>](../release-notes/nuget-1.2.md)

<span data-ttu-id="43a8e-105">NuGet 1.0 已于 2011 年 1 月 13 日发布。</span><span class="sxs-lookup"><span data-stu-id="43a8e-105">NuGet 1.0 was released on January 13, 2011.</span></span>  <span data-ttu-id="43a8e-106">NuGet 1.1 已于 2011 年 2 月 12 日发布。</span><span class="sxs-lookup"><span data-stu-id="43a8e-106">NuGet 1.1 was released on February 12, 2011.</span></span>

## <a name="overview"></a><span data-ttu-id="43a8e-107">概述</span><span class="sxs-lookup"><span data-stu-id="43a8e-107">Overview</span></span>

<span data-ttu-id="43a8e-108">本文档包含各种版本的 NuGet 1.0 分组根据主要预览版本的发行说明。</span><span class="sxs-lookup"><span data-stu-id="43a8e-108">This document contains the release notes for the various releases of NuGet 1.0 grouped according to major preview release.</span></span>

<span data-ttu-id="43a8e-109">NuGet 包括以下组件：</span><span class="sxs-lookup"><span data-stu-id="43a8e-109">NuGet includes the following components:</span></span>

* <span data-ttu-id="43a8e-110">*NuGet.Tools.vsix* \* 组成：</span><span class="sxs-lookup"><span data-stu-id="43a8e-110">*NuGet.Tools.vsix* \* which consists of:</span></span>
  * <span data-ttu-id="43a8e-111">**添加库包对话框**\* 对话框用于浏览和安装包的 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="43a8e-111">**Add Library Package Dialog** \* Dialog within Visual Studio used to browse and install packages.</span></span>
  * <span data-ttu-id="43a8e-112">**包管理器控制台**\* Powershell 基于 Visual Studio 中的控制台。</span><span class="sxs-lookup"><span data-stu-id="43a8e-112">**Package Manager Console** \* Powershell based console within Visual Studio.</span></span>
* <span data-ttu-id="43a8e-113">*NuGet 命令行工具*\* 工具用于创建 （并最终发布） 包。</span><span class="sxs-lookup"><span data-stu-id="43a8e-113">*NuGet Command Line Tool* \* Tool used to create (and eventually publish) packages.</span></span>

<span data-ttu-id="43a8e-114">NuGet 工具 Visual Studio 扩展 (*NuGet.Tools.vsix*) 要求：</span><span class="sxs-lookup"><span data-stu-id="43a8e-114">The NuGet Tools Visual Studio Extension (*NuGet.Tools.vsix*) requires:</span></span>

* <span data-ttu-id="43a8e-115">Visual Studio 2010 或 Visual Web Developer 2010 速成版。</span><span class="sxs-lookup"><span data-stu-id="43a8e-115">Visual Studio 2010 or Visual Web Developer 2010 Express.</span></span>

<span data-ttu-id="43a8e-116">NuGet 命令行工具需要：</span><span class="sxs-lookup"><span data-stu-id="43a8e-116">The NuGet Command Line Tool requires:</span></span>

* <span data-ttu-id="43a8e-117">.NET framework 版本 4</span><span class="sxs-lookup"><span data-stu-id="43a8e-117">.NET Framework Version 4</span></span>

## <a name="installation"></a><span data-ttu-id="43a8e-118">安装</span><span class="sxs-lookup"><span data-stu-id="43a8e-118">Installation</span></span>

<span data-ttu-id="43a8e-119">若要使用此[最新版本](http://nuget.codeplex.com/releases/view/52018):</span><span class="sxs-lookup"><span data-stu-id="43a8e-119">To use this [latest release](http://nuget.codeplex.com/releases/view/52018):</span></span>

* <span data-ttu-id="43a8e-120">首先卸载较旧版本。</span><span class="sxs-lookup"><span data-stu-id="43a8e-120">First uninstall your older build.</span></span> <span data-ttu-id="43a8e-121">您需要以管理员身份来执行此操作运行 VS。</span><span class="sxs-lookup"><span data-stu-id="43a8e-121">You need to run VS as administrator to do this.</span></span>
* <span data-ttu-id="43a8e-122">你拥有的所有现有源中删除。</span><span class="sxs-lookup"><span data-stu-id="43a8e-122">Remove all the existing feeds that you have.</span></span>
* <span data-ttu-id="43a8e-123">添加新的订阅源指向[ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669)。</span><span class="sxs-lookup"><span data-stu-id="43a8e-123">Add a new feed pointing to [http://go.microsoft.com/fwlink/?LinkId=206669](http://go.microsoft.com/fwlink/?LinkId=206669).</span></span>

## <a name="nuget-11"></a><span data-ttu-id="43a8e-124">NuGet 1.1</span><span class="sxs-lookup"><span data-stu-id="43a8e-124">NuGet 1.1</span></span>

<span data-ttu-id="43a8e-125">在此版本中修复的问题列表[可在此处找到](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)</span><span class="sxs-lookup"><span data-stu-id="43a8e-125">The list of issues fixed in this release [can be found here](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)</span></span>

## <a name="nuget-10-rtm"></a><span data-ttu-id="43a8e-126">NuGet 1.0 RTM</span><span class="sxs-lookup"><span data-stu-id="43a8e-126">NuGet 1.0 RTM</span></span>

<span data-ttu-id="43a8e-127">自从 RC 以来 rtm 修复一个问题。</span><span class="sxs-lookup"><span data-stu-id="43a8e-127">One issue was fixed for RTM since the RC.</span></span>

* [<span data-ttu-id="43a8e-128">问题 474： 删除包影响解决方案中的所有项目</span><span class="sxs-lookup"><span data-stu-id="43a8e-128">Issue 474: Removing Packages Affects All Project In Solution</span></span>](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a><span data-ttu-id="43a8e-129">候选发布版本</span><span class="sxs-lookup"><span data-stu-id="43a8e-129">Release Candidate</span></span>

<span data-ttu-id="43a8e-130">以下是自 CTP 2 此 Release Candidate 中所做的更改。</span><span class="sxs-lookup"><span data-stu-id="43a8e-130">The following are the changes made in this Release Candidate since CTP 2.</span></span> <span data-ttu-id="43a8e-131">问题跟踪程序来查看 bug 的完整列表，请访问。</span><span class="sxs-lookup"><span data-stu-id="43a8e-131">Visit the Issue Tracker to see the full list of bugs.</span></span>

* [<span data-ttu-id="43a8e-132">更新包从控制台不会更新依赖项。</span><span class="sxs-lookup"><span data-stu-id="43a8e-132">Updating Package from Console does not update dependencies.</span></span>](http://nuget.codeplex.com/workitem/443)
* [<span data-ttu-id="43a8e-133">添加包提取 bin 不包引用 (CTP1)</span><span class="sxs-lookup"><span data-stu-id="43a8e-133">Adding package picks up bin not package reference (CTP1)</span></span>](http://nuget.codeplex.com/workitem/442)
* [<span data-ttu-id="43a8e-134">更新包离开损坏的引用</span><span class="sxs-lookup"><span data-stu-id="43a8e-134">Updating a package leaves broken references</span></span>](http://nuget.codeplex.com/workitem/440)
* [<span data-ttu-id="43a8e-135">获取包的更新失败，在对话框中，或在控制台中选择全部聚合的源</span><span class="sxs-lookup"><span data-stu-id="43a8e-135">Get-Package -Updates fails in the dialog, or when the 'All' aggregate source is selected in the console</span></span>](http://nuget.codeplex.com/workitem/439)
* [<span data-ttu-id="43a8e-136">获取包验证错误</span><span class="sxs-lookup"><span data-stu-id="43a8e-136">Getting package verification errors</span></span>](http://nuget.codeplex.com/workitem/426)
* [<span data-ttu-id="43a8e-137">不能从添加包对话框安装包时，用户则发出警告</span><span class="sxs-lookup"><span data-stu-id="43a8e-137">Warn users when a package cannot be installed from the Add Package Dialog</span></span>](http://nuget.codeplex.com/workitem/425)
* [<span data-ttu-id="43a8e-138">获取包的更新，则会引发更新大量的包时</span><span class="sxs-lookup"><span data-stu-id="43a8e-138">Get-Package -Updates throws when updating large number of packages</span></span>](http://nuget.codeplex.com/workitem/424)
* [<span data-ttu-id="43a8e-139">提高时 nuspec 文件编写错误的错误处理</span><span class="sxs-lookup"><span data-stu-id="43a8e-139">Improve error handling when nuspec files are authored incorrectly</span></span>](http://nuget.codeplex.com/workitem/423)
* [<span data-ttu-id="43a8e-140">Nuget pack 忽略指定的文件</span><span class="sxs-lookup"><span data-stu-id="43a8e-140">Nuget pack ignores specified files</span></span>](http://nuget.codeplex.com/workitem/422)
* [<span data-ttu-id="43a8e-141">删除第二个至最后一个包源，然后单击"下移"崩溃 VS</span><span class="sxs-lookup"><span data-stu-id="43a8e-141">Removing the second-to-last package source and then clicking "Move Down" crashes VS</span></span>](http://nuget.codeplex.com/workitem/418)
* [<span data-ttu-id="43a8e-142">安装包时移除程序集引用</span><span class="sxs-lookup"><span data-stu-id="43a8e-142">Remove assembly reference while installing packages</span></span>](http://nuget.codeplex.com/workitem/413)
* [<span data-ttu-id="43a8e-143">InvalidOperationException 时打开设置对话框</span><span class="sxs-lookup"><span data-stu-id="43a8e-143">InvalidOperationException when opening Settings dialog</span></span>](http://nuget.codeplex.com/workitem/411)
* [<span data-ttu-id="43a8e-144">在包管理器控制台中的包源的访问键不起作用</span><span class="sxs-lookup"><span data-stu-id="43a8e-144">Access Key for Package Source in Package Manager Console doesn't work</span></span>](http://nuget.codeplex.com/workitem/410)
* [<span data-ttu-id="43a8e-145">NuGet VS 设置对话框的访问键将焦点移动到错误的字段</span><span class="sxs-lookup"><span data-stu-id="43a8e-145">NuGet VS Settings Dialog Access Keys Give Focus to Wrong Fields</span></span>](http://nuget.codeplex.com/workitem/409)
* [<span data-ttu-id="43a8e-146">包 ID intellisense 不应查询项太多</span><span class="sxs-lookup"><span data-stu-id="43a8e-146">Package ID intellisense should not query too many items</span></span>](http://nuget.codeplex.com/workitem/404)
* [<span data-ttu-id="43a8e-147">将包添加到项目名称中的圆点字符的项目失败</span><span class="sxs-lookup"><span data-stu-id="43a8e-147">Failure adding package to project with a dot character in the Project name</span></span>](http://nuget.codeplex.com/workitem/403)
* [<span data-ttu-id="43a8e-148">Nuspec 中的指定文件的问题</span><span class="sxs-lookup"><span data-stu-id="43a8e-148">Issue with specified files in nuspec</span></span>](http://nuget.codeplex.com/workitem/400)
* [<span data-ttu-id="43a8e-149">使用更新版本时，应获取注册正确的官方源</span><span class="sxs-lookup"><span data-stu-id="43a8e-149">Correct official feed should get registered when using newer build</span></span>](http://nuget.codeplex.com/workitem/399)
* [<span data-ttu-id="43a8e-150">标记应使用空格而不是 #</span><span class="sxs-lookup"><span data-stu-id="43a8e-150">Tags should use spaces instead of #</span></span>](http://nuget.codeplex.com/workitem/397)
* [<span data-ttu-id="43a8e-151">IPackageMetadata 缺少某些有用的信息</span><span class="sxs-lookup"><span data-stu-id="43a8e-151">IPackageMetadata lacks some useful information</span></span>](http://nuget.codeplex.com/workitem/388)
* [<span data-ttu-id="43a8e-152">向对话框添加报告滥用行为链接</span><span class="sxs-lookup"><span data-stu-id="43a8e-152">Add Report Abuse Link to the Dialog</span></span>](http://nuget.codeplex.com/workitem/386)
* [<span data-ttu-id="43a8e-153">使用 App_Data 来解压缩包在 Visual Studio 中的分页符</span><span class="sxs-lookup"><span data-stu-id="43a8e-153">Using App_Data to unzip packages breaks in Visual Studio</span></span>](http://nuget.codeplex.com/workitem/380)
* [<span data-ttu-id="43a8e-154">实现标记</span><span class="sxs-lookup"><span data-stu-id="43a8e-154">Implement Tags</span></span>](http://nuget.codeplex.com/workitem/376)
* [<span data-ttu-id="43a8e-155">PackageBuilder 允许没有依赖项创建的空包</span><span class="sxs-lookup"><span data-stu-id="43a8e-155">PackageBuilder allows empty package with no dependencies to be created</span></span>](http://nuget.codeplex.com/workitem/373)
* [<span data-ttu-id="43a8e-156">添加包的所有者字段</span><span class="sxs-lookup"><span data-stu-id="43a8e-156">Add Owners Field for the Package</span></span>](http://nuget.codeplex.com/workitem/365)
* [<span data-ttu-id="43a8e-157">更新要说 NuGet 包管理器而不是 VSIX 工具的 VSIX 清单</span><span class="sxs-lookup"><span data-stu-id="43a8e-157">Update the VSIX manifest to say NuGet Package Manager rather than VSIX Tools</span></span>](http://nuget.codeplex.com/workitem/364)
* [<span data-ttu-id="43a8e-158">获取包命令将引发错误时选中全部源</span><span class="sxs-lookup"><span data-stu-id="43a8e-158">Get-Package command throws error when All source is selected</span></span>](http://nuget.codeplex.com/workitem/359)
* [<span data-ttu-id="43a8e-159">允许进行排序的选项对话框中的包源</span><span class="sxs-lookup"><span data-stu-id="43a8e-159">Allow ordering of package sources in Options dialog</span></span>](http://nuget.codeplex.com/workitem/356)
* [<span data-ttu-id="43a8e-160">更新包不会删除较旧版本</span><span class="sxs-lookup"><span data-stu-id="43a8e-160">Update-Package does not remove older version</span></span>](http://nuget.codeplex.com/workitem/352)
* [<span data-ttu-id="43a8e-161">依赖项的实现版本范围规范</span><span class="sxs-lookup"><span data-stu-id="43a8e-161">Implement Version Range Specification for Dependencies</span></span>](http://nuget.codeplex.com/workitem/347)
* [<span data-ttu-id="43a8e-162">单击"添加新的包"时，visual Studio 崩溃</span><span class="sxs-lookup"><span data-stu-id="43a8e-162">Visual Studio crashes when clicking "Add new package"</span></span>](http://nuget.codeplex.com/workitem/346)
* [<span data-ttu-id="43a8e-163">在添加包对话框中显示的下载和评级</span><span class="sxs-lookup"><span data-stu-id="43a8e-163">Display Downloads and Ratings in the Add Package Dialog</span></span>](http://nuget.codeplex.com/workitem/345)
* [<span data-ttu-id="43a8e-164">在对话框中的包源之间的更改不会更新活动的源</span><span class="sxs-lookup"><span data-stu-id="43a8e-164">Changing between package sources in the Dialog doesn't update active source</span></span>](http://nuget.codeplex.com/workitem/344)
* [<span data-ttu-id="43a8e-165">删除包管理器控制台窗口的键绑定</span><span class="sxs-lookup"><span data-stu-id="43a8e-165">Remove Key Binding for Package Manager Console Window</span></span>](http://nuget.codeplex.com/workitem/339)
* [<span data-ttu-id="43a8e-166">安装包未被识别为 cmdlet 名称...</span><span class="sxs-lookup"><span data-stu-id="43a8e-166">Install-Package is not recognized as the name of a cmdlet...</span></span>](http://nuget.codeplex.com/workitem/338)
* [<span data-ttu-id="43a8e-167">从本地上正则馈送源依赖项安装包将不解析</span><span class="sxs-lookup"><span data-stu-id="43a8e-167">Installing a package from a local feed the dependencies on regular feeds are not resolved</span></span>](http://nuget.codeplex.com/workitem/332)
* [<span data-ttu-id="43a8e-168">RemoveDependencies 应跳过仍在使用的依赖项</span><span class="sxs-lookup"><span data-stu-id="43a8e-168">RemoveDependencies should skip dependencies that are still in use</span></span>](http://nuget.codeplex.com/workitem/331)
* [<span data-ttu-id="43a8e-169">如果正在取消页面导航，用户无法导航到其他页面而原始页请求返回</span><span class="sxs-lookup"><span data-stu-id="43a8e-169">If cancelling page navigation, user cannot navigate to a different page while the original page request returns</span></span>](http://nuget.codeplex.com/workitem/325)
* [<span data-ttu-id="43a8e-170">调查性能 NuPack.Server 向源提供大量的包。</span><span class="sxs-lookup"><span data-stu-id="43a8e-170">Investigate performance of NuPack.Server for serving feeds with large number of packages.</span></span>](http://nuget.codeplex.com/workitem/324)
* [<span data-ttu-id="43a8e-171">包的第二个时间筛选它使用"新建"包源，而不是以前选定的源。</span><span class="sxs-lookup"><span data-stu-id="43a8e-171">The second time I filter for a package it uses the "New" package source, instead of the previously selected source.</span></span>](http://nuget.codeplex.com/workitem/321)
* [<span data-ttu-id="43a8e-172">选择对话框上的"联机"选项卡时，应选择默认包源。</span><span class="sxs-lookup"><span data-stu-id="43a8e-172">Default package source should be selected when selecting the "Online" tab on the dialog.</span></span>](http://nuget.codeplex.com/workitem/320)
* [<span data-ttu-id="43a8e-173">默认情况下，列表包应显示已安装的包</span><span class="sxs-lookup"><span data-stu-id="43a8e-173">List-Package should show installed packages by default</span></span>](http://nuget.codeplex.com/workitem/309)
* [<span data-ttu-id="43a8e-174">程序集引用 HintPaths</span><span class="sxs-lookup"><span data-stu-id="43a8e-174">Assembly Reference HintPaths</span></span>](http://nuget.codeplex.com/workitem/294)
* [<span data-ttu-id="43a8e-175">打开程序包管理器控制台时出现异常</span><span class="sxs-lookup"><span data-stu-id="43a8e-175">Exception while opening Package Manager Console</span></span>](http://nuget.codeplex.com/workitem/268)
* [<span data-ttu-id="43a8e-176">控制台 intellisense 下载整个源</span><span class="sxs-lookup"><span data-stu-id="43a8e-176">Console intellisense downloads entire feed</span></span>](http://nuget.codeplex.com/workitem/259)
* [<span data-ttu-id="43a8e-177">Default 包源应重命名为 'Active'</span><span class="sxs-lookup"><span data-stu-id="43a8e-177">'Default' package source should be renamed to 'Active'</span></span>](http://nuget.codeplex.com/workitem/258)
* [<span data-ttu-id="43a8e-178">包源 UI： 按确定应添加新的源，如果名称/源字段都为非空</span><span class="sxs-lookup"><span data-stu-id="43a8e-178">Package sources UI: pressing OK should add the new source if Name/Source fields are non-empty</span></span>](http://nuget.codeplex.com/workitem/257)
* [<span data-ttu-id="43a8e-179">当已安装的包很大，对话框就非常慢</span><span class="sxs-lookup"><span data-stu-id="43a8e-179">Dialog becomes super slow when the number of installed packages is large</span></span>](http://nuget.codeplex.com/workitem/243)
* [<span data-ttu-id="43a8e-180">支持的强名称程序集绑定重定向</span><span class="sxs-lookup"><span data-stu-id="43a8e-180">Support Binding Redirects for Strong Named Assemblies</span></span>](http://nuget.codeplex.com/workitem/238)
* [<span data-ttu-id="43a8e-181">添加包引用...UI 包源包括向下的下拉</span><span class="sxs-lookup"><span data-stu-id="43a8e-181">Add Package Reference... UI to include drop down for Package source</span></span>](http://nuget.codeplex.com/workitem/226)
* [<span data-ttu-id="43a8e-182">NuPack 需要支持的配置文件名称 agnostically 配置转换</span><span class="sxs-lookup"><span data-stu-id="43a8e-182">NuPack needs to support config transform agnostically of the config file name</span></span>](http://nuget.codeplex.com/workitem/224)
* [<span data-ttu-id="43a8e-183">允许 BasePath NuPack.exe 中重写</span><span class="sxs-lookup"><span data-stu-id="43a8e-183">Allows BasePath to be Overriden in NuPack.exe</span></span>](http://nuget.codeplex.com/workitem/222)
* [<span data-ttu-id="43a8e-184">包源回退行为</span><span class="sxs-lookup"><span data-stu-id="43a8e-184">Package Source Fallback Behavior</span></span>](http://nuget.codeplex.com/workitem/204)
* [<span data-ttu-id="43a8e-185">有关 GUI 崩溃</span><span class="sxs-lookup"><span data-stu-id="43a8e-185">Crash on GUI</span></span>](http://nuget.codeplex.com/workitem/201)
* [<span data-ttu-id="43a8e-186">添加排序选项添加包对话框</span><span class="sxs-lookup"><span data-stu-id="43a8e-186">Add sorting options to Add Package Dialog</span></span>](http://nuget.codeplex.com/workitem/179)
* [<span data-ttu-id="43a8e-187">快捷方式键以清除包管理器控制台</span><span class="sxs-lookup"><span data-stu-id="43a8e-187">shortcut key to clear the Package Manager Console</span></span>](http://nuget.codeplex.com/workitem/174)
* [<span data-ttu-id="43a8e-188">PowerConsole 导致 NuPack 控制台失败</span><span class="sxs-lookup"><span data-stu-id="43a8e-188">PowerConsole causes NuPack Console to fail</span></span>](http://nuget.codeplex.com/workitem/166)
* [<span data-ttu-id="43a8e-189">控制台和添加包对话框应在请求中设置用户代理</span><span class="sxs-lookup"><span data-stu-id="43a8e-189">Console and Add Package Dialog should set user agent in requests</span></span>](http://nuget.codeplex.com/workitem/141)
* [<span data-ttu-id="43a8e-190">设置在生成的 VSIX 和 NuPack.exe 版本号。</span><span class="sxs-lookup"><span data-stu-id="43a8e-190">Set version number of the VSIX and NuPack.exe in the build.</span></span>](http://nuget.codeplex.com/workitem/134)
* [<span data-ttu-id="43a8e-191">隐藏从-常见的 PowerShell 参数？</span><span class="sxs-lookup"><span data-stu-id="43a8e-191">Hide common PowerShell parameters from -?</span></span>](http://nuget.codeplex.com/workitem/118)
* [<span data-ttu-id="43a8e-192">添加-有关控制台命令的详细的帮助</span><span class="sxs-lookup"><span data-stu-id="43a8e-192">Add -detailed help for console commands</span></span>](http://nuget.codeplex.com/workitem/110)
* [<span data-ttu-id="43a8e-193">添加包对话框应允许选择当前的包源</span><span class="sxs-lookup"><span data-stu-id="43a8e-193">Add Package Dialog Should Allow Choosing the Current Package Source</span></span>](http://nuget.codeplex.com/workitem/88)
* [<span data-ttu-id="43a8e-194">将 NuPack.Core 类移到不同的命名空间</span><span class="sxs-lookup"><span data-stu-id="43a8e-194">Move NuPack.Core classes into different namespaces</span></span>](http://nuget.codeplex.com/workitem/50)
* [<span data-ttu-id="43a8e-195">添加到 cmdlet 的帮助</span><span class="sxs-lookup"><span data-stu-id="43a8e-195">Add help to cmdlets</span></span>](http://nuget.codeplex.com/workitem/23)
* [<span data-ttu-id="43a8e-196">包下载后验证哈希从数据源</span><span class="sxs-lookup"><span data-stu-id="43a8e-196">Verify hash from feed after package download</span></span>](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a><span data-ttu-id="43a8e-197">CTP 2</span><span class="sxs-lookup"><span data-stu-id="43a8e-197">CTP 2</span></span>

<span data-ttu-id="43a8e-198">在 CTP 2 中所做的显著更改如下：</span><span class="sxs-lookup"><span data-stu-id="43a8e-198">The following are the most significant changes made in CTP 2:</span></span>

* <span data-ttu-id="43a8e-199">切换来自 ATOM 馈送到 OData 服务终结点的包： 如果您升级到 CTP2 版本的 NuGet，请确保将以下 URL 添加为包源： `https://feed.nuget.org/ctp2/odata/v1/`。</span><span class="sxs-lookup"><span data-stu-id="43a8e-199">Switched the package feed from ATOM to an OData service endpoint: If you upgrade to the CTP2 version of NuGet, be sure to add the following URL as a package source: `https://feed.nuget.org/ctp2/odata/v1/`.</span></span>
* <span data-ttu-id="43a8e-200">重命名为添加包命令*Install-package*。</span><span class="sxs-lookup"><span data-stu-id="43a8e-200">Renamed the Add-Package command to *Install-Package*.</span></span>
* <span data-ttu-id="43a8e-201">更新`.nuspec`格式。</span><span class="sxs-lookup"><span data-stu-id="43a8e-201">Updated the `.nuspec` Format.</span></span> <span data-ttu-id="43a8e-202">`.nuspec`格式现在包括*iconUrl*字段用于指定一个 32 x 32 png 图标，它将显示在添加包对话框。</span><span class="sxs-lookup"><span data-stu-id="43a8e-202">The `.nuspec` format now includes the *iconUrl* field for specifying a 32x32 png icon which will show up in the Add Package Dialog.</span></span> <span data-ttu-id="43a8e-203">因此请确保设置，若要区分你的包。</span><span class="sxs-lookup"><span data-stu-id="43a8e-203">So be sure to set that to distinguish your package.</span></span> <span data-ttu-id="43a8e-204">`.nuspec`格式还包括新*projectUrl*字段可用于指向一个网页，提供了有关包的详细信息。</span><span class="sxs-lookup"><span data-stu-id="43a8e-204">The `.nuspec` format also includes the new *projectUrl* field which you can use to point to a web page that provides more information about your package.</span></span>

<span data-ttu-id="43a8e-205">此生成不会使用旧`.nupkg`文件。</span><span class="sxs-lookup"><span data-stu-id="43a8e-205">This build will not work with old `.nupkg` files.</span></span> <span data-ttu-id="43a8e-206">如果收到空引用异常，则表示使用旧`.nupkg`文件，并需要使用更新后重建[NuGet 命令行工具](http://nuget.codeplex.com/releases/52017/download/165468)。</span><span class="sxs-lookup"><span data-stu-id="43a8e-206">If you get null reference exceptions, you're using an old `.nupkg` file and need to rebuild it with the updated [NuGet command line tool](http://nuget.codeplex.com/releases/52017/download/165468).</span></span>

<span data-ttu-id="43a8e-207">下面是一系列功能和的 NuGet CTP 2 （不包括 bug 的细微代码清理等）。 已修复的 bug。</span><span class="sxs-lookup"><span data-stu-id="43a8e-207">The following is a list of features and bugs that were fixed for NuGet CTP 2 (does not include bugs for minor code cleanups etc.).</span></span>

* [<span data-ttu-id="43a8e-208">错误解包的包程序集时指定的程序集 TargetFramework。</span><span class="sxs-lookup"><span data-stu-id="43a8e-208">Error unpacking package assemblies when specifiying the TargetFramework for an assembly.</span></span>](http://nuget.codeplex.com/workitem/10)
* [<span data-ttu-id="43a8e-209">使 NuPack 控制台窗口更容易地发现</span><span class="sxs-lookup"><span data-stu-id="43a8e-209">Make NuPack Console window more discoverable</span></span>](http://nuget.codeplex.com/workitem/14)
* [<span data-ttu-id="43a8e-210">ILMerge nupack.exe 版本</span><span class="sxs-lookup"><span data-stu-id="43a8e-210">ILMerge the nupack.exe release</span></span>](http://nuget.codeplex.com/workitem/19)
* [<span data-ttu-id="43a8e-211">更好的错误/异常处理</span><span class="sxs-lookup"><span data-stu-id="43a8e-211">Better error/exception handling</span></span>](http://nuget.codeplex.com/workitem/24)
* <span data-ttu-id="43a8e-212">[[Nupack.Core]: PackageManager 应妥善处理与源相关的错误](http://nuget.codeplex.com/workitem/28)</span><span class="sxs-lookup"><span data-stu-id="43a8e-212">[[Nupack.Core]: PackageManager should gracefully handle feed-related errors](http://nuget.codeplex.com/workitem/28)</span></span>
* [<span data-ttu-id="43a8e-213">为控制台需要新图标</span><span class="sxs-lookup"><span data-stu-id="43a8e-213">Need a new icon for the console</span></span>](http://nuget.codeplex.com/workitem/29)
* [<span data-ttu-id="43a8e-214">在对话框中的字符串本地化</span><span class="sxs-lookup"><span data-stu-id="43a8e-214">Localize strings in the Dialog</span></span>](http://nuget.codeplex.com/workitem/38)
* [<span data-ttu-id="43a8e-215">NuPack 缓存在内存中的.nupack 文件下载</span><span class="sxs-lookup"><span data-stu-id="43a8e-215">NuPack caches downloaded .nupack files in memory</span></span>](http://nuget.codeplex.com/workitem/40)
* [<span data-ttu-id="43a8e-216">NuPack 控制台： 更改用于显示控制台的默认快捷方式</span><span class="sxs-lookup"><span data-stu-id="43a8e-216">NuPack Console: Change the default shortcut for displaying console</span></span>](http://nuget.codeplex.com/workitem/48)
* [<span data-ttu-id="43a8e-217">ProjectSystem 应支持常见属性的默认值</span><span class="sxs-lookup"><span data-stu-id="43a8e-217">ProjectSystem should support default values for common properties</span></span>](http://nuget.codeplex.com/workitem/49)
* [<span data-ttu-id="43a8e-218">使用一个 nuspec 文件的文件夹中运行 nupack.exe 应使用该 nuspec</span><span class="sxs-lookup"><span data-stu-id="43a8e-218">Running nupack.exe in a folder with just one nuspec file should use that nuspec</span></span>](http://nuget.codeplex.com/workitem/52)
* [<span data-ttu-id="43a8e-219">甚至在加载任何项目/解决方案时出现项目菜单</span><span class="sxs-lookup"><span data-stu-id="43a8e-219">Project Menu Shows Up Even When No Project/Solution Is Loaded</span></span>](http://nuget.codeplex.com/workitem/54)
* [<span data-ttu-id="43a8e-220">build.cmd 干净代码库的克隆上失败</span><span class="sxs-lookup"><span data-stu-id="43a8e-220">build.cmd fails on a clean clone of the codebase</span></span>](http://nuget.codeplex.com/workitem/56)
* [<span data-ttu-id="43a8e-221">更新可用的功能</span><span class="sxs-lookup"><span data-stu-id="43a8e-221">Updates available feature</span></span>](http://nuget.codeplex.com/workitem/57)
* [<span data-ttu-id="43a8e-222">对话框： 添加包对话框中通过在控制台中删除提示</span><span class="sxs-lookup"><span data-stu-id="43a8e-222">Dialog: Adding a package through the dialog removes the prompt in the console</span></span>](http://nuget.codeplex.com/workitem/73)
* [<span data-ttu-id="43a8e-223">通过单击安装来添加包通常较慢，没有视觉反馈</span><span class="sxs-lookup"><span data-stu-id="43a8e-223">Adding a package by clicking 'Install' is often slow, with no visual feedback</span></span>](http://nuget.codeplex.com/workitem/80)
* [<span data-ttu-id="43a8e-224">没有方法来发现其中我已安装的包已更新。</span><span class="sxs-lookup"><span data-stu-id="43a8e-224">There is no way to discover which of my installed packages have updates.</span></span>](http://nuget.codeplex.com/workitem/82)
* [<span data-ttu-id="43a8e-225">没有方法来更新该对话框中的已安装的程序包。</span><span class="sxs-lookup"><span data-stu-id="43a8e-225">There is no way to update an installed package in the dialog.</span></span>](http://nuget.codeplex.com/workitem/83)
* [<span data-ttu-id="43a8e-226">无法卸载该对话框中的已安装的包</span><span class="sxs-lookup"><span data-stu-id="43a8e-226">There is no way to uninstall an installed package in the dialog</span></span>](http://nuget.codeplex.com/workitem/84)
* [<span data-ttu-id="43a8e-227">&ldquo;添加包引用&hellip;&rdquo;出现在上下文菜单中的已安装的引用</span><span class="sxs-lookup"><span data-stu-id="43a8e-227">&ldquo;Add Package Reference&hellip;&rdquo; appears on the context menu of installed references</span></span>](http://nuget.codeplex.com/workitem/85)
* [<span data-ttu-id="43a8e-228">在更新后从控制台的包，它显示在旧版本和新版本安装</span><span class="sxs-lookup"><span data-stu-id="43a8e-228">After updating a package from the console, it shows both the old version and the new version as installed</span></span>](http://nuget.codeplex.com/workitem/86)
* [<span data-ttu-id="43a8e-229">在控制台中，当使用对话框中，活动使用后消失</span><span class="sxs-lookup"><span data-stu-id="43a8e-229">The activity in the console, when using the dialog, disappears after use</span></span>](http://nuget.codeplex.com/workitem/87)
* [<span data-ttu-id="43a8e-230">清除命令行中 nupack.exe 分析</span><span class="sxs-lookup"><span data-stu-id="43a8e-230">Cleanup command line parsing in nupack.exe</span></span>](http://nuget.codeplex.com/workitem/89)
* [<span data-ttu-id="43a8e-231">将友好名称添加到包源</span><span class="sxs-lookup"><span data-stu-id="43a8e-231">Add a friendly name to package sources</span></span>](http://nuget.codeplex.com/workitem/98)
* [<span data-ttu-id="43a8e-232">更新.nuspec 以支持包括包图标</span><span class="sxs-lookup"><span data-stu-id="43a8e-232">Update .nuspec to support including package icons</span></span>](http://nuget.codeplex.com/workitem/103)
* [<span data-ttu-id="43a8e-233">源用户界面不允许复制 URL</span><span class="sxs-lookup"><span data-stu-id="43a8e-233">Feed UI doesn't allow copying the URL</span></span>](http://nuget.codeplex.com/workitem/105)
* [<span data-ttu-id="43a8e-234">更好的删除包错误处理。</span><span class="sxs-lookup"><span data-stu-id="43a8e-234">Better remove-package error handling.</span></span>](http://nuget.codeplex.com/workitem/107)
* [<span data-ttu-id="43a8e-235">在控制台窗口中键入内容取决于游标焦点</span><span class="sxs-lookup"><span data-stu-id="43a8e-235">Typing in Console Window depends on cursor focus</span></span>](http://nuget.codeplex.com/workitem/112)
* [<span data-ttu-id="43a8e-236">错误消息看起来很多次</span><span class="sxs-lookup"><span data-stu-id="43a8e-236">Error messages look awful</span></span>](http://nuget.codeplex.com/workitem/116)
* [<span data-ttu-id="43a8e-237">未安装的包删除包的性能已损坏</span><span class="sxs-lookup"><span data-stu-id="43a8e-237">The performance of Remove-Package for a package that isn't installed is bad</span></span>](http://nuget.codeplex.com/workitem/117)
* [<span data-ttu-id="43a8e-238">删除包失败时没有任何包源</span><span class="sxs-lookup"><span data-stu-id="43a8e-238">Removing a package fails when there are no package sources</span></span>](http://nuget.codeplex.com/workitem/119)
* [<span data-ttu-id="43a8e-239">删除包失败的包源不可用时</span><span class="sxs-lookup"><span data-stu-id="43a8e-239">Remove-Package fails when the package source is unavailable</span></span>](http://nuget.codeplex.com/workitem/120)
* [<span data-ttu-id="43a8e-240">添加到包元数据和源的标题。</span><span class="sxs-lookup"><span data-stu-id="43a8e-240">Add Title to the package metadata and the feed.</span></span>](http://nuget.codeplex.com/workitem/125)
* [<span data-ttu-id="43a8e-241">添加回添加包的源参数</span><span class="sxs-lookup"><span data-stu-id="43a8e-241">Add the -Source parameter back to Add-Package</span></span>](http://nuget.codeplex.com/workitem/127)
* [<span data-ttu-id="43a8e-242">列表包都应具有的源参数</span><span class="sxs-lookup"><span data-stu-id="43a8e-242">List-Package should have a -Source parameter</span></span>](http://nuget.codeplex.com/workitem/128)
* [<span data-ttu-id="43a8e-243">更新 NuPack.Server 需要 NuPack 用户代理到下载包</span><span class="sxs-lookup"><span data-stu-id="43a8e-243">Update NuPack.Server to require NuPack User Agent To Download Package</span></span>](http://nuget.codeplex.com/workitem/142)
* [<span data-ttu-id="43a8e-244">许可证接受对话框必须列出所有依赖项，需要接受许可证</span><span class="sxs-lookup"><span data-stu-id="43a8e-244">License Acceptance Dialog Must List Licenses For All Dependencies That Require Acceptance</span></span>](http://nuget.codeplex.com/workitem/145)
* [<span data-ttu-id="43a8e-245">记录错误时引发的源中的包</span><span class="sxs-lookup"><span data-stu-id="43a8e-245">Log an error when a package throws in the feed</span></span>](http://nuget.codeplex.com/workitem/150)
* [<span data-ttu-id="43a8e-246">NuPack.exe 不应该允许一个空&lt;licenseurl&gt;元素</span><span class="sxs-lookup"><span data-stu-id="43a8e-246">NuPack.exe should not allow an empty &lt;licenseurl&gt; element</span></span>](http://nuget.codeplex.com/workitem/152)
* [<span data-ttu-id="43a8e-247">列表包重命名到 Get 的包中，添加的包安装包和删除包卸载包</span><span class="sxs-lookup"><span data-stu-id="43a8e-247">Rename List-Package to Get-Package, Add-Package to Install-Package, and Remove-Package to Uninstall-Package</span></span>](http://nuget.codeplex.com/workitem/155)
* [<span data-ttu-id="43a8e-248">使用解决方案导航器中的添加包引用菜单项使 Visual Studio 崩溃</span><span class="sxs-lookup"><span data-stu-id="43a8e-248">Using the Add Package Reference menu item from the Solution Navigator crashes Visual Studio</span></span>](http://nuget.codeplex.com/workitem/158)
* [<span data-ttu-id="43a8e-249">"可用的包源"标签缺少冒号</span><span class="sxs-lookup"><span data-stu-id="43a8e-249">"Available package sources" label is missing a colon</span></span>](http://nuget.codeplex.com/workitem/160)
* [<span data-ttu-id="43a8e-250">使.nuspec xml 元素的大小写一致地 camel 大小写</span><span class="sxs-lookup"><span data-stu-id="43a8e-250">Make .nuspec xml element casing consistently camel cased</span></span>](http://nuget.codeplex.com/workitem/161)
* [<span data-ttu-id="43a8e-251">需要打开 admin 的位 NuPack VSIX 的清单</span><span class="sxs-lookup"><span data-stu-id="43a8e-251">The NuPack VSIX's manifest needs to turn on the 'admin' bit</span></span>](http://nuget.codeplex.com/workitem/162)
* [<span data-ttu-id="43a8e-252">如果使用没有源运行列表包，则会为 null 引用错误</span><span class="sxs-lookup"><span data-stu-id="43a8e-252">If you run List-Package with no feeds, you get null ref error</span></span>](http://nuget.codeplex.com/workitem/164)
* [<span data-ttu-id="43a8e-253">nuget.exe： 指定目标路径</span><span class="sxs-lookup"><span data-stu-id="43a8e-253">nuget.exe: specify destination path</span></span>](http://nuget.codeplex.com/workitem/171)
* [<span data-ttu-id="43a8e-254">打开包管理控制台上 WinXP 的 Powershell 错误</span><span class="sxs-lookup"><span data-stu-id="43a8e-254">Powershell Errors Opening Package Management Console on WinXP</span></span>](http://nuget.codeplex.com/workitem/175)
* [<span data-ttu-id="43a8e-255">尝试加载包列表时 VS 崩溃</span><span class="sxs-lookup"><span data-stu-id="43a8e-255">VS Crashes while trying to load package list</span></span>](http://nuget.codeplex.com/workitem/176)
* [<span data-ttu-id="43a8e-256">允许元包 （无文件，仅依赖项）</span><span class="sxs-lookup"><span data-stu-id="43a8e-256">allow meta packages (no files, only dependencies)</span></span>](http://nuget.codeplex.com/workitem/180)
* [<span data-ttu-id="43a8e-257">将 Powershell 脚本转换为 Powershell 2.0 模块</span><span class="sxs-lookup"><span data-stu-id="43a8e-257">Convert Powershell Script to Powershell 2.0 Module</span></span>](http://nuget.codeplex.com/workitem/181)
* [<span data-ttu-id="43a8e-258">当指定为目标时，PathResolver 应放弃路径部分前面通配符字符</span><span class="sxs-lookup"><span data-stu-id="43a8e-258">PathResolver should discard path portion preceeding wildcard characters when target is specified</span></span>](http://nuget.codeplex.com/workitem/183)
* [<span data-ttu-id="43a8e-259">没有依赖关系</span><span class="sxs-lookup"><span data-stu-id="43a8e-259">No dependencies</span></span>](http://nuget.codeplex.com/workitem/186)
* [<span data-ttu-id="43a8e-260">安装 Elmah 时出错</span><span class="sxs-lookup"><span data-stu-id="43a8e-260">Error installing Elmah</span></span>](http://nuget.codeplex.com/workitem/192)
* [<span data-ttu-id="43a8e-261">配置转换不正常使用&lt;configsections&gt;</span><span class="sxs-lookup"><span data-stu-id="43a8e-261">Config transforms don't work correctly with &lt;configsections&gt;</span></span>](http://nuget.codeplex.com/workitem/194)
* [<span data-ttu-id="43a8e-262">变量 $global: projectCache 无法检索，因为尚未设置</span><span class="sxs-lookup"><span data-stu-id="43a8e-262">The variable '$global:projectCache' cannot be retrieved because it has not been set</span></span>](http://nuget.codeplex.com/workitem/203)
* [<span data-ttu-id="43a8e-263">添加用于创建 NuPack 包的 MSBuild 任务</span><span class="sxs-lookup"><span data-stu-id="43a8e-263">Add MSBuild task for creating NuPack packages</span></span>](http://nuget.codeplex.com/workitem/205)
* [<span data-ttu-id="43a8e-264">列出程序包需要支持搜索/筛选</span><span class="sxs-lookup"><span data-stu-id="43a8e-264">list-package needs to support searching/filtering</span></span>](http://nuget.codeplex.com/workitem/206)
* [<span data-ttu-id="43a8e-265">始终显示许可证的链接如果包的作者提供了一个许可证 URL</span><span class="sxs-lookup"><span data-stu-id="43a8e-265">Always display a link to license if the package author provides a license URL</span></span>](http://nuget.codeplex.com/workitem/208)
* [<span data-ttu-id="43a8e-266">使用删除包偶尔"拒绝访问"异常</span><span class="sxs-lookup"><span data-stu-id="43a8e-266">Occasional "Access Denied" exception with Remove-Package</span></span>](http://nuget.codeplex.com/workitem/213)
* [<span data-ttu-id="43a8e-267">单元测试失败： InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries</span><span class="sxs-lookup"><span data-stu-id="43a8e-267">Unit Tests Failing: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries</span></span>](http://nuget.codeplex.com/workitem/214)
* [<span data-ttu-id="43a8e-268">允许回退/默认组文件，如果找不到特定 framework 版本</span><span class="sxs-lookup"><span data-stu-id="43a8e-268">Allow for a fallback/default set of files if a specfic framework version cannot be found</span></span>](http://nuget.codeplex.com/workitem/223)
* [<span data-ttu-id="43a8e-269">添加包引用...UI 中不能删除包</span><span class="sxs-lookup"><span data-stu-id="43a8e-269">Add Package Reference... UI cannot remove a package</span></span>](http://nuget.codeplex.com/workitem/225)
* [<span data-ttu-id="43a8e-270">添加包引用崩溃 studio 时一个或多个项目已卸载</span><span class="sxs-lookup"><span data-stu-id="43a8e-270">Add Package Reference crashes studio when one or more project is unloaded</span></span>](http://nuget.codeplex.com/workitem/228)
* [<span data-ttu-id="43a8e-271">配置转换似乎不处理 web.debug.config 文件</span><span class="sxs-lookup"><span data-stu-id="43a8e-271">Config transform does not appear to work on web.debug.config file</span></span>](http://nuget.codeplex.com/workitem/229)
* [<span data-ttu-id="43a8e-272">init.ps1 不触发自定义包</span><span class="sxs-lookup"><span data-stu-id="43a8e-272">init.ps1 not firing on custom package</span></span>](http://nuget.codeplex.com/workitem/237)
* [<span data-ttu-id="43a8e-273">将路径添加到 feedlist 时, 的默认按钮设置为确定，因此如果我按 ENTER 会自动关闭</span><span class="sxs-lookup"><span data-stu-id="43a8e-273">When adding paths to the feedlist, the default button is set to OK, so if I press ENTER it automatically closes</span></span>](http://nuget.codeplex.com/workitem/240)
* [<span data-ttu-id="43a8e-274">尝试卸载依赖关系会导致 VS 崩溃如果尝试在行中的 2 倍</span><span class="sxs-lookup"><span data-stu-id="43a8e-274">Attempt to uninstall a dependency will crash VS if attempted 2 times in a row</span></span>](http://nuget.codeplex.com/workitem/241)
* [<span data-ttu-id="43a8e-275">在添加包对话框中显示项目 URL</span><span class="sxs-lookup"><span data-stu-id="43a8e-275">Display the Project URL in the Add Package dialog</span></span>](http://nuget.codeplex.com/workitem/253)
* [<span data-ttu-id="43a8e-276">默认为安装的程序包添加包对话框</span><span class="sxs-lookup"><span data-stu-id="43a8e-276">Default the Add-Package dialog to Installed Packages</span></span>](http://nuget.codeplex.com/workitem/254)
* [<span data-ttu-id="43a8e-277">更改包对话框中添加菜单项。</span><span class="sxs-lookup"><span data-stu-id="43a8e-277">Change Add Package Dialog menu item.</span></span>](http://nuget.codeplex.com/workitem/261)
* [<span data-ttu-id="43a8e-278">重命名命名空间和程序集</span><span class="sxs-lookup"><span data-stu-id="43a8e-278">Rename namespaces and assemblies</span></span>](http://nuget.codeplex.com/workitem/274)
* [<span data-ttu-id="43a8e-279">将 NuPack 项目重命名为 NuGet</span><span class="sxs-lookup"><span data-stu-id="43a8e-279">Rename the NuPack Project to NuGet</span></span>](http://nuget.codeplex.com/workitem/282)
* [<span data-ttu-id="43a8e-280">添加依赖项的列表下的以下文本</span><span class="sxs-lookup"><span data-stu-id="43a8e-280">Add the following text under the list of dependencies</span></span>](http://nuget.codeplex.com/workitem/288)
* [<span data-ttu-id="43a8e-281">将许可证接受对话框中的许可证接受文本</span><span class="sxs-lookup"><span data-stu-id="43a8e-281">Change the license acceptance text in the License Acceptance Dialog</span></span>](http://nuget.codeplex.com/workitem/291)
* [<span data-ttu-id="43a8e-282">将上面的包的列表许可证接受对话框中的文本</span><span class="sxs-lookup"><span data-stu-id="43a8e-282">Change the text in the License Acceptance Dialog above the list of packages</span></span>](http://nuget.codeplex.com/workitem/292)
* [<span data-ttu-id="43a8e-283">OData 使用的 fwlink 的 URL 不起作用</span><span class="sxs-lookup"><span data-stu-id="43a8e-283">OData doesn't work with an fwlink URL</span></span>](http://nuget.codeplex.com/workitem/304)
* [<span data-ttu-id="43a8e-284">包管理器 UI： 对包计数用于分页的主动缓存</span><span class="sxs-lookup"><span data-stu-id="43a8e-284">Package Manager UI: Over aggressive caching of package count used for paging</span></span>](http://nuget.codeplex.com/workitem/317)
* [<span data-ttu-id="43a8e-285">NuPack / NuGet-&gt;包管理器控制台错误</span><span class="sxs-lookup"><span data-stu-id="43a8e-285">NuPack / NuGet -&gt; Package Manager Console error</span></span>](http://nuget.codeplex.com/workitem/335)
* [<span data-ttu-id="43a8e-286">添加包对话框会显示许可接受有关已安装打包</span><span class="sxs-lookup"><span data-stu-id="43a8e-286">Add Package Dialog shows License Acceptance For Already Installed Packaged</span></span>](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a><span data-ttu-id="43a8e-287">CTP 1</span><span class="sxs-lookup"><span data-stu-id="43a8e-287">CTP 1</span></span>

<span data-ttu-id="43a8e-288">下面是一系列功能和 NuGet CTP 1 已修复的 bug。</span><span class="sxs-lookup"><span data-stu-id="43a8e-288">The following is a list of features and bugs that were fixed for NuGet CTP 1.</span></span>

* [<span data-ttu-id="43a8e-289">包扩展应重命名为.nupack</span><span class="sxs-lookup"><span data-stu-id="43a8e-289">Package extension should be renamed to .nupack</span></span>](http://nuget.codeplex.com/workitem/1)
* [<span data-ttu-id="43a8e-290">将包文件移动到文件夹</span><span class="sxs-lookup"><span data-stu-id="43a8e-290">Move package file into folder</span></span>](http://nuget.codeplex.com/workitem/2)
* [<span data-ttu-id="43a8e-291">合并安装&amp;添加 PS 命令</span><span class="sxs-lookup"><span data-stu-id="43a8e-291">Merge install &amp; Add PS commands</span></span>](http://nuget.codeplex.com/workitem/3)
* [<span data-ttu-id="43a8e-292">为动词-名词 cmdlet 创建别名</span><span class="sxs-lookup"><span data-stu-id="43a8e-292">Create aliases for Verb-Noun cmdlets</span></span>](http://nuget.codeplex.com/workitem/4)
* [<span data-ttu-id="43a8e-293">在 VS 中切换解决方案时即用会混淆 NuPack</span><span class="sxs-lookup"><span data-stu-id="43a8e-293">NuPack gets confused when switching solution in VS</span></span>](http://nuget.codeplex.com/workitem/6)
* [<span data-ttu-id="43a8e-294">我们应默认情况下隐藏的包的解决方案文件夹</span><span class="sxs-lookup"><span data-stu-id="43a8e-294">We should hide the 'packages' solution folder by default</span></span>](http://nuget.codeplex.com/workitem/11)
* [<span data-ttu-id="43a8e-295">在内容项中添加支持标记替换。</span><span class="sxs-lookup"><span data-stu-id="43a8e-295">Add support for token replacement in content items.</span></span>](http://nuget.codeplex.com/workitem/12)
* [<span data-ttu-id="43a8e-296">NuPack.UI 应使用 PackageSource API</span><span class="sxs-lookup"><span data-stu-id="43a8e-296">NuPack.UI should use the PackageSource API</span></span>](http://nuget.codeplex.com/workitem/26)
* <span data-ttu-id="43a8e-297">[[Nupack.Core]: PackageManager 将包标记为已安装它们之前，安装](http://nuget.codeplex.com/workitem/27)</span><span class="sxs-lookup"><span data-stu-id="43a8e-297">[[Nupack.Core]: PackageManager marks packages as installed prior to installing them](http://nuget.codeplex.com/workitem/27)</span></span>
* [<span data-ttu-id="43a8e-298">正在删除默认项目从解决方案仍显示为默认值已删除的项目</span><span class="sxs-lookup"><span data-stu-id="43a8e-298">Deleting default project from solution still shows the deleted project as default</span></span>](http://nuget.codeplex.com/workitem/30)
* [<span data-ttu-id="43a8e-299">新包失败，出现"无法添加一部分为指定的 URI 因为它已在包中。"</span><span class="sxs-lookup"><span data-stu-id="43a8e-299">New-Package fails with "Cannot add part for the specified URI because it's already in the package."</span></span>](http://nuget.codeplex.com/workitem/32)
* [<span data-ttu-id="43a8e-300">从 Visual Studio GUI 中删除"NuPack"字符串</span><span class="sxs-lookup"><span data-stu-id="43a8e-300">Remove "NuPack" strings from Visual Studio GUI</span></span>](http://nuget.codeplex.com/workitem/35)
* [<span data-ttu-id="43a8e-301">添加 COPYRIGHT.txt 到 Apache 标头文件</span><span class="sxs-lookup"><span data-stu-id="43a8e-301">Add Apache Header To a COPYRIGHT.txt file</span></span>](http://nuget.codeplex.com/workitem/36)
* [<span data-ttu-id="43a8e-302">删除更新 PackageSource 命令</span><span class="sxs-lookup"><span data-stu-id="43a8e-302">Remove Update-PackageSource Command</span></span>](http://nuget.codeplex.com/workitem/37)
* [<span data-ttu-id="43a8e-303">包管理器正在加载配置文件引发异常时不可用</span><span class="sxs-lookup"><span data-stu-id="43a8e-303">Package Manager unusable when loading profile throws an exception</span></span>](http://nuget.codeplex.com/workitem/39)
* [<span data-ttu-id="43a8e-304">init.ps1、 install.ps1 和 uninstall.ps1 需要接收其他状态</span><span class="sxs-lookup"><span data-stu-id="43a8e-304">init.ps1, install.ps1 and uninstall.ps1 need to receive additional state</span></span>](http://nuget.codeplex.com/workitem/41)
* [<span data-ttu-id="43a8e-305">控制台和 GUI 包合并到一个包</span><span class="sxs-lookup"><span data-stu-id="43a8e-305">Combine Console and GUI Packages Into One Package</span></span>](http://nuget.codeplex.com/workitem/42)
* [<span data-ttu-id="43a8e-306">如果应用到 XML 的不是根目录，Xml 转换逻辑不起作用</span><span class="sxs-lookup"><span data-stu-id="43a8e-306">Xml transform logic doesn't work if applied to XML that isn't at the root</span></span>](http://nuget.codeplex.com/workitem/43)
* [<span data-ttu-id="43a8e-307">管理包源设置对话框未更新 NuPack 控制台</span><span class="sxs-lookup"><span data-stu-id="43a8e-307">Manage package sources settings dialog not updating the NuPack console</span></span>](http://nuget.codeplex.com/workitem/44)
* [<span data-ttu-id="43a8e-308">NuPack 控制台 UI： 重命名为包源的包源下拉列表</span><span class="sxs-lookup"><span data-stu-id="43a8e-308">NuPack Console UI: Rename 'Package feed' drop-down list to 'Package source'</span></span>](http://nuget.codeplex.com/workitem/45)
* [<span data-ttu-id="43a8e-309">NuPack 控制台选项： 重命名存储库 UI，以与 NuPack 控制台保持一致</span><span class="sxs-lookup"><span data-stu-id="43a8e-309">NuPack Console Options: Rename 'Repository UI' to be consistent with NuPack Console</span></span>](http://nuget.codeplex.com/workitem/46)
* [<span data-ttu-id="43a8e-310">针对从 IIS 或 URL 打开一个网站添加包失败</span><span class="sxs-lookup"><span data-stu-id="43a8e-310">Add-Package fails against a website that was opened from IIS or a URL</span></span>](http://nuget.codeplex.com/workitem/53)
* [<span data-ttu-id="43a8e-311">包管理器源不使用 FwLink</span><span class="sxs-lookup"><span data-stu-id="43a8e-311">Package Manager Source Doesn't Work With FwLink</span></span>](http://nuget.codeplex.com/workitem/55)
* [<span data-ttu-id="43a8e-312">设置默认包源</span><span class="sxs-lookup"><span data-stu-id="43a8e-312">Set the default package source</span></span>](http://nuget.codeplex.com/workitem/59)
* [<span data-ttu-id="43a8e-313">如果提供只有一个源时，请在选项中，添加包源，，假定它是默认值。</span><span class="sxs-lookup"><span data-stu-id="43a8e-313">When adding package sources in option, when only one source is supplied, assume it's the default.</span></span>](http://nuget.codeplex.com/workitem/60)
* [<span data-ttu-id="43a8e-314">对话框用户界面显示了假"最近"的程序包</span><span class="sxs-lookup"><span data-stu-id="43a8e-314">The Dialog UI shows fake "recent" packages</span></span>](http://nuget.codeplex.com/workitem/62)
* [<span data-ttu-id="43a8e-315">选项： 单击取消按钮不会取消更改</span><span class="sxs-lookup"><span data-stu-id="43a8e-315">Options: Clicking cancel does not cancel changes</span></span>](http://nuget.codeplex.com/workitem/63)
* [<span data-ttu-id="43a8e-316">添加包引用对话框搜索不区分大小写</span><span class="sxs-lookup"><span data-stu-id="43a8e-316">Add Package Reference Dialog Search should be case insensitive</span></span>](http://nuget.codeplex.com/workitem/65)
* [<span data-ttu-id="43a8e-317">在 AssemblyInfo.cs 文件中修复公司元数据</span><span class="sxs-lookup"><span data-stu-id="43a8e-317">Fix company metadata in AssemblyInfo.cs files</span></span>](http://nuget.codeplex.com/workitem/67)
* [<span data-ttu-id="43a8e-318">VSIX 的版本号</span><span class="sxs-lookup"><span data-stu-id="43a8e-318">Version number for the VSIX</span></span>](http://nuget.codeplex.com/workitem/71)
* [<span data-ttu-id="43a8e-319">删除包： 使用-？两次显示帮助</span><span class="sxs-lookup"><span data-stu-id="43a8e-319">Remove-Package: Using -? displays help twice</span></span>](http://nuget.codeplex.com/workitem/72)
* [<span data-ttu-id="43a8e-320">执行项目级包安装/卸载包</span><span class="sxs-lookup"><span data-stu-id="43a8e-320">Execute install/uninstall packages for project level packages</span></span>](http://nuget.codeplex.com/workitem/74)
* [<span data-ttu-id="43a8e-321">服务器无法验证一个 nupack 失败时创建源</span><span class="sxs-lookup"><span data-stu-id="43a8e-321">Server unable to create feed when one nupack fails validation</span></span>](http://nuget.codeplex.com/workitem/90)
* [<span data-ttu-id="43a8e-322">需要替换 NuPack 图标</span><span class="sxs-lookup"><span data-stu-id="43a8e-322">Need to Replace NuPack Icons</span></span>](http://nuget.codeplex.com/workitem/94)
* [<span data-ttu-id="43a8e-323">NTLM http 代理的身份验证不到包源。</span><span class="sxs-lookup"><span data-stu-id="43a8e-323">NTLM http proxy does not authenticate to the package feed.</span></span>](http://nuget.codeplex.com/workitem/96)
* [<span data-ttu-id="43a8e-324">该对话框不会始终居中窗口中启动 VS</span><span class="sxs-lookup"><span data-stu-id="43a8e-324">The dialog doesn't always start centered in the VS window</span></span>](http://nuget.codeplex.com/workitem/100)
* [<span data-ttu-id="43a8e-325">不是在对话框中填充许多包详细信息中的字段</span><span class="sxs-lookup"><span data-stu-id="43a8e-325">Many of the fields in a packages details are not being populated in the dialog</span></span>](http://nuget.codeplex.com/workitem/102)
* [<span data-ttu-id="43a8e-326">对话框 UI 不会显示作者的名称</span><span class="sxs-lookup"><span data-stu-id="43a8e-326">Dialog UI doesn't show Authors' names</span></span>](http://nuget.codeplex.com/workitem/108)
* [<span data-ttu-id="43a8e-327">为什么-删除包版本</span><span class="sxs-lookup"><span data-stu-id="43a8e-327">Why -Version for Remove-Package</span></span>](http://nuget.codeplex.com/workitem/113)
* [<span data-ttu-id="43a8e-328">删除对话框 UI 上的最近选项卡</span><span class="sxs-lookup"><span data-stu-id="43a8e-328">Remove the Recent tab on the Dialog UI</span></span>](http://nuget.codeplex.com/workitem/115)
* [<span data-ttu-id="43a8e-329">VS 崩溃时正确打开对话框 UI 至少一个后单击解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="43a8e-329">VS crash when right click on solution folder after opening Dialog UI at least one.</span></span>](http://nuget.codeplex.com/workitem/126)
* [<span data-ttu-id="43a8e-330">更改列表包的本地参数到-安装</span><span class="sxs-lookup"><span data-stu-id="43a8e-330">Change the -Local parameter of List-Package to -Installed</span></span>](http://nuget.codeplex.com/workitem/129)
* [<span data-ttu-id="43a8e-331">将 packages.xml 重命名为 NuPack.config</span><span class="sxs-lookup"><span data-stu-id="43a8e-331">Rename packages.xml to NuPack.config</span></span>](http://nuget.codeplex.com/workitem/132)
* [<span data-ttu-id="43a8e-332">控制台强制光标到行尾</span><span class="sxs-lookup"><span data-stu-id="43a8e-332">Console forces cursor to the end of line</span></span>](http://nuget.codeplex.com/workitem/135)
* [<span data-ttu-id="43a8e-333">删除包 intellisense 会中断</span><span class="sxs-lookup"><span data-stu-id="43a8e-333">Remove-Package intellisense is broken</span></span>](http://nuget.codeplex.com/workitem/136)
* [<span data-ttu-id="43a8e-334">将 RequireLicenseAcceptance 标记添加到.nuspec 和源</span><span class="sxs-lookup"><span data-stu-id="43a8e-334">Add RequireLicenseAcceptance Flag to .nuspec and Feed</span></span>](http://nuget.codeplex.com/workitem/137)
* [<span data-ttu-id="43a8e-335">添加到.nuspec 格式和程序包的 LicenseUrl 源</span><span class="sxs-lookup"><span data-stu-id="43a8e-335">Add LicenseUrl to .nuspec Format and Package Feed</span></span>](http://nuget.codeplex.com/workitem/138)
* [<span data-ttu-id="43a8e-336">单击安装需要接受的包应显示接受对话框</span><span class="sxs-lookup"><span data-stu-id="43a8e-336">Clicking Install For Package That Requires Acceptance Should Show Acceptance Dialog</span></span>](http://nuget.codeplex.com/workitem/139)
* [<span data-ttu-id="43a8e-337">将免责声明文本添加到添加包对话框</span><span class="sxs-lookup"><span data-stu-id="43a8e-337">Add Disclaimer Text to the Add Package Dialog</span></span>](http://nuget.codeplex.com/workitem/140)
* [<span data-ttu-id="43a8e-338">添加免责声明时的包控制台首次运行</span><span class="sxs-lookup"><span data-stu-id="43a8e-338">Add Disclaimer When the Package Console is run the first time</span></span>](http://nuget.codeplex.com/workitem/143)
* [<span data-ttu-id="43a8e-339">在控制台中安装包后显示的免责声明</span><span class="sxs-lookup"><span data-stu-id="43a8e-339">Display Disclaimer After Installing Package In The Console</span></span>](http://nuget.codeplex.com/workitem/144)
* [<span data-ttu-id="43a8e-340">将.nupack 扩展重命名为.nupkg</span><span class="sxs-lookup"><span data-stu-id="43a8e-340">Rename the .nupack extension to .nupkg</span></span>](http://nuget.codeplex.com/workitem/146)