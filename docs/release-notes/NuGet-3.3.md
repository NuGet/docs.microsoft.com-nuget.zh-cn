---
title: NuGet 3.3 发行说明
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.3 的发行说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: adf193437de237ed32da481e627552a8dba6f656
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821559"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="13a73-103">NuGet 3.3 发行说明</span><span class="sxs-lookup"><span data-stu-id="13a73-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="13a73-104">[NuGet 3.2.1 发行说明](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC 发行说明](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="13a73-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="13a73-105">NuGet 3.3 已释放 2015 年 11 月 30 日与大量的用户界面更新和命令行功能，以及有用修复 NuGet 客户端的集合。</span><span class="sxs-lookup"><span data-stu-id="13a73-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="13a73-106">新增功能</span><span class="sxs-lookup"><span data-stu-id="13a73-106">New Features</span></span>

* <span data-ttu-id="13a73-107">已引入，允许 NuGet 命令行客户端能够无缝配合使用经过身份验证的源的凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="13a73-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="13a73-108">[说明如何安装 Visual Studio Team Services 凭据提供程序](../api/nuget-exe-credential-providers.md)和配置 NuGet 客户端使用它位于 NuGet Docs。</span><span class="sxs-lookup"><span data-stu-id="13a73-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="13a73-109">新的用户界面功能</span><span class="sxs-lookup"><span data-stu-id="13a73-109">New User Interface Features</span></span>

* <span data-ttu-id="13a73-110">浏览、 已安装，和更新可用的单独选项卡</span><span class="sxs-lookup"><span data-stu-id="13a73-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="13a73-111">更新可用徽章，该值指示具有可用的更新的程序包数</span><span class="sxs-lookup"><span data-stu-id="13a73-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="13a73-112">在包列表中以指示是否将包安装到或有一个更新的包徽章</span><span class="sxs-lookup"><span data-stu-id="13a73-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="13a73-113">下载计数和作者添加到包列表</span><span class="sxs-lookup"><span data-stu-id="13a73-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="13a73-114">最高可用的版本编号和包列表上的当前安装的版本编号</span><span class="sxs-lookup"><span data-stu-id="13a73-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="13a73-115">操作按钮，以允许快速安装、 更新和卸载从包列表</span><span class="sxs-lookup"><span data-stu-id="13a73-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="13a73-116">包详细信息面板上的清楚地了解操作按钮</span><span class="sxs-lookup"><span data-stu-id="13a73-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="13a73-117">包详细信息面板上的包更新日期</span><span class="sxs-lookup"><span data-stu-id="13a73-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="13a73-118">合并解决方案视图中的面板</span><span class="sxs-lookup"><span data-stu-id="13a73-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="13a73-119">可排序网格的项目和安装的版本号，在解决方案视图</span><span class="sxs-lookup"><span data-stu-id="13a73-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="13a73-120">新的命令行功能</span><span class="sxs-lookup"><span data-stu-id="13a73-120">New Command-line Features</span></span>

<span data-ttu-id="13a73-121">在此版本中，我们将介绍`add`和`init`命令来初始化基于文件夹的存储库中所述[nuget.exe 引用](../tools/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="13a73-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="13a73-122">存储库构造并维护与此文件夹结构将[提供显著的性能优势](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)我们的博客上所述。</span><span class="sxs-lookup"><span data-stu-id="13a73-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="13a73-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="13a73-123">ContentFiles</span></span>

<span data-ttu-id="13a73-124">中现在支持内容`project.json`托管通过新的项目`contentFiles`文件夹和`.nuspec``contentFiles`元素表示法。</span><span class="sxs-lookup"><span data-stu-id="13a73-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="13a73-125">与项目系统的交互的包作者可以更直接指定此内容。</span><span class="sxs-lookup"><span data-stu-id="13a73-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="13a73-126">有关如何配置中的文件的详细信息`.nuspec`在找不到文档[.nuspec 引用](../reference/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="13a73-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="13a73-127">NuGet 局部变量缓存管理</span><span class="sxs-lookup"><span data-stu-id="13a73-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="13a73-128">NuGet 命令行已更新以包括有关如何管理工作站上的本地缓存的信息。</span><span class="sxs-lookup"><span data-stu-id="13a73-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="13a73-129">中提供了有关局部变量命令的详细信息[NuGet 命令行参考](../tools/cli-ref-locals.md)。</span><span class="sxs-lookup"><span data-stu-id="13a73-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="13a73-130">已解决的问题</span><span class="sxs-lookup"><span data-stu-id="13a73-130">Fixed Issues</span></span>

<span data-ttu-id="13a73-131">**值得注意的问题**</span><span class="sxs-lookup"><span data-stu-id="13a73-131">**Notable Issues**</span></span>

* <span data-ttu-id="13a73-132">NuGet 命令行对还原的还原的支持包解决方案上具有文件 Mono- [1543年](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="13a73-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="13a73-133">在 3.3 版本中已解决的问题的完整列表可以在 GitHub 上找到[3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="13a73-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="13a73-134">在 3.3 命令行版本中修复的问题的列表中记录[3.3 命令行里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)。</span><span class="sxs-lookup"><span data-stu-id="13a73-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="13a73-135">已知问题</span><span class="sxs-lookup"><span data-stu-id="13a73-135">Known Issues</span></span>

<span data-ttu-id="13a73-136">我们将继续在我们的 GitHub 问题列表，可在上跟踪问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="13a73-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>