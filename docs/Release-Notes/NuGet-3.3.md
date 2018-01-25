---
title: "NuGet 3.3 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.3 的发行说明。"
keywords: "NuGet 3.3 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c83f87231497e14c36f1b8100b7bec720bb63b1c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="bf52c-104">NuGet 3.3 发行说明</span><span class="sxs-lookup"><span data-stu-id="bf52c-104">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="bf52c-105">[NuGet 3.2.1 发行说明](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC 发行说明](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="bf52c-105">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="bf52c-106">NuGet 3.3 已释放 2015 年 11 月 30 日与大量的用户界面更新和命令行功能，以及有用修复 NuGet 客户端的集合。</span><span class="sxs-lookup"><span data-stu-id="bf52c-106">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="bf52c-107">新增功能</span><span class="sxs-lookup"><span data-stu-id="bf52c-107">New Features</span></span>

* <span data-ttu-id="bf52c-108">已引入，允许 NuGet 命令行客户端能够无缝配合使用经过身份验证的源的凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="bf52c-108">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="bf52c-109">[说明如何安装 Visual Studio Team Services 凭据提供程序](../API/nuget-exe-Credential-Providers.md)和配置 NuGet 客户端使用它位于 NuGet Docs。</span><span class="sxs-lookup"><span data-stu-id="bf52c-109">[Instructions on how to install the Visual Studio Team Services credential provider ](../API/nuget-exe-Credential-Providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="bf52c-110">新的用户界面功能</span><span class="sxs-lookup"><span data-stu-id="bf52c-110">New User Interface Features</span></span>

* <span data-ttu-id="bf52c-111">浏览、 已安装，和更新可用的单独选项卡</span><span class="sxs-lookup"><span data-stu-id="bf52c-111">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="bf52c-112">更新可用徽章，该值指示具有可用的更新的程序包数</span><span class="sxs-lookup"><span data-stu-id="bf52c-112">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="bf52c-113">在包列表中以指示是否将包安装到或有一个更新的包徽章</span><span class="sxs-lookup"><span data-stu-id="bf52c-113">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="bf52c-114">下载计数和作者添加到包列表</span><span class="sxs-lookup"><span data-stu-id="bf52c-114">Download count and author added to the package list</span></span>
* <span data-ttu-id="bf52c-115">最高可用的版本编号和包列表上的当前安装的版本编号</span><span class="sxs-lookup"><span data-stu-id="bf52c-115">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="bf52c-116">操作按钮，以允许快速安装、 更新和卸载从包列表</span><span class="sxs-lookup"><span data-stu-id="bf52c-116">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="bf52c-117">包详细信息面板上的清楚地了解操作按钮</span><span class="sxs-lookup"><span data-stu-id="bf52c-117">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="bf52c-118">包详细信息面板上的包更新日期</span><span class="sxs-lookup"><span data-stu-id="bf52c-118">Package update date on the package detail panel</span></span>
* <span data-ttu-id="bf52c-119">合并解决方案视图中的面板</span><span class="sxs-lookup"><span data-stu-id="bf52c-119">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="bf52c-120">可排序网格的项目和安装的版本号，在解决方案视图</span><span class="sxs-lookup"><span data-stu-id="bf52c-120">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="bf52c-121">新的命令行功能</span><span class="sxs-lookup"><span data-stu-id="bf52c-121">New Command-line Features</span></span>

<span data-ttu-id="bf52c-122">在此版本中，我们将介绍`add`和`init`命令来初始化基于文件夹的存储库中所述[nuget.exe 引用](../tools/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="bf52c-122">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="bf52c-123">存储库构造并维护与此文件夹结构将[提供显著的性能优势](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)我们的博客上所述。</span><span class="sxs-lookup"><span data-stu-id="bf52c-123">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="bf52c-124">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="bf52c-124">ContentFiles</span></span>

<span data-ttu-id="bf52c-125">中现在支持内容`project.json`托管通过新的项目`contentFiles`文件夹和`.nuspec``contentFiles`元素表示法。</span><span class="sxs-lookup"><span data-stu-id="bf52c-125">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="bf52c-126">与项目系统的交互的包作者可以更直接指定此内容。</span><span class="sxs-lookup"><span data-stu-id="bf52c-126">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="bf52c-127">有关如何配置中的文件的详细信息`.nuspec`在找不到文档[.nuspec 引用](../schema/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="bf52c-127">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../schema/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="bf52c-128">NuGet 局部变量缓存管理</span><span class="sxs-lookup"><span data-stu-id="bf52c-128">NuGet Locals Cache Management</span></span>

<span data-ttu-id="bf52c-129">NuGet 命令行已更新以包括有关如何管理工作站上的本地缓存的信息。</span><span class="sxs-lookup"><span data-stu-id="bf52c-129">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="bf52c-130">中提供了有关局部变量命令的详细信息[NuGet 命令行参考](../tools/cli-ref-locals.md)。</span><span class="sxs-lookup"><span data-stu-id="bf52c-130">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="bf52c-131">已解决的问题</span><span class="sxs-lookup"><span data-stu-id="bf52c-131">Fixed Issues</span></span>

<span data-ttu-id="bf52c-132">**值得注意的问题**</span><span class="sxs-lookup"><span data-stu-id="bf52c-132">**Notable Issues**</span></span>

* <span data-ttu-id="bf52c-133">NuGet 命令行对还原的还原的支持包解决方案上具有文件 Mono- [1543年](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="bf52c-133">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="bf52c-134">在 3.3 版本中已解决的问题的完整列表可以在 GitHub 上找到[3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="bf52c-134">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="bf52c-135">在 3.3 命令行版本中修复的问题的列表中记录[3.3 命令行里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)。</span><span class="sxs-lookup"><span data-stu-id="bf52c-135">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="bf52c-136">已知问题</span><span class="sxs-lookup"><span data-stu-id="bf52c-136">Known Issues</span></span>

<span data-ttu-id="bf52c-137">我们继续在我们的 GitHub 问题列表，可在上跟踪问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="bf52c-137">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>