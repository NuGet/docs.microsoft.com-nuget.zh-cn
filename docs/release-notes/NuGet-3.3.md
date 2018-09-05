---
title: NuGet 3.3 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.3 发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546642"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="eb37c-103">NuGet 3.3 发行说明</span><span class="sxs-lookup"><span data-stu-id="eb37c-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="eb37c-104">[NuGet 3.2.1 发行说明](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC 发行说明](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="eb37c-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="eb37c-105">NuGet 3.3 已于 2015 年 11 月 30 日与大量用户界面更新和命令行功能，以及一系列有用的 NuGet 客户端的修补程序的发布。</span><span class="sxs-lookup"><span data-stu-id="eb37c-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="eb37c-106">新增功能</span><span class="sxs-lookup"><span data-stu-id="eb37c-106">New Features</span></span>

* <span data-ttu-id="eb37c-107">已引入，允许 NuGet 命令行客户端能够无缝使用已经过身份验证源的凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="eb37c-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="eb37c-108">[说明如何安装 Visual Studio Team Services 凭据提供程序](../api/nuget-exe-credential-providers.md)和配置 NuGet 客户端使用它位于 NuGet 文档。</span><span class="sxs-lookup"><span data-stu-id="eb37c-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="eb37c-109">新用户界面功能</span><span class="sxs-lookup"><span data-stu-id="eb37c-109">New User Interface Features</span></span>

* <span data-ttu-id="eb37c-110">单独的浏览、 已安装，且更新可用的选项卡</span><span class="sxs-lookup"><span data-stu-id="eb37c-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="eb37c-111">更新可用徽章，指示有可用更新的包的数目</span><span class="sxs-lookup"><span data-stu-id="eb37c-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="eb37c-112">包在包列表中，指明是否安装包徽章或有可用更新</span><span class="sxs-lookup"><span data-stu-id="eb37c-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="eb37c-113">下载计数和作者添加到包列表</span><span class="sxs-lookup"><span data-stu-id="eb37c-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="eb37c-114">最高可用的版本编号和在包列表中的当前安装的版本编号</span><span class="sxs-lookup"><span data-stu-id="eb37c-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="eb37c-115">操作按钮，以允许快速安装、 更新和卸载从包列表</span><span class="sxs-lookup"><span data-stu-id="eb37c-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="eb37c-116">包详细信息面板上更清晰的操作按钮</span><span class="sxs-lookup"><span data-stu-id="eb37c-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="eb37c-117">在包详细信息面板上的包更新日期</span><span class="sxs-lookup"><span data-stu-id="eb37c-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="eb37c-118">合并在解决方案视图的面板</span><span class="sxs-lookup"><span data-stu-id="eb37c-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="eb37c-119">项目和解决方案视图上已安装的版本号的可排序网格</span><span class="sxs-lookup"><span data-stu-id="eb37c-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="eb37c-120">命令行的新功能</span><span class="sxs-lookup"><span data-stu-id="eb37c-120">New Command-line Features</span></span>

<span data-ttu-id="eb37c-121">在此版本中我们引入了`add`并`init`命令来初始化基于文件夹的存储库中所述[nuget.exe 参考](../tools/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="eb37c-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="eb37c-122">存储库构造和维护与此文件夹结构，将[提供了显著的性能好处](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)我们的博客上所述。</span><span class="sxs-lookup"><span data-stu-id="eb37c-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="eb37c-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="eb37c-123">ContentFiles</span></span>

<span data-ttu-id="eb37c-124">中现在支持内容`project.json`托管的新项目`contentFiles`文件夹并`.nuspec``contentFiles`元素表示法。</span><span class="sxs-lookup"><span data-stu-id="eb37c-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="eb37c-125">此内容可以更直接地指定由包的作者与项目系统之间的交互。</span><span class="sxs-lookup"><span data-stu-id="eb37c-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="eb37c-126">详细了解如何配置中的 contentFiles`.nuspec`中可以找到文档[.nuspec 引用](../reference/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="eb37c-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="eb37c-127">NuGet 局部变量缓存管理</span><span class="sxs-lookup"><span data-stu-id="eb37c-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="eb37c-128">NuGet 命令行已更新以包括有关如何管理工作站上的本地缓存信息。</span><span class="sxs-lookup"><span data-stu-id="eb37c-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="eb37c-129">中提供了有关局部变量命令的详细信息[NuGet 命令行参考](../tools/cli-ref-locals.md)。</span><span class="sxs-lookup"><span data-stu-id="eb37c-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="eb37c-130">已解决的问题</span><span class="sxs-lookup"><span data-stu-id="eb37c-130">Fixed Issues</span></span>

<span data-ttu-id="eb37c-131">**值得注意的问题**</span><span class="sxs-lookup"><span data-stu-id="eb37c-131">**Notable Issues**</span></span>

* <span data-ttu-id="eb37c-132">用于还原的 NuGet 命令行还原的支持打包在一起 Mono 的上一个解决方案文件[1543年](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="eb37c-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="eb37c-133">可以在 GitHub 上找到 3.3 版本中已解决的问题的完整列表[3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="eb37c-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="eb37c-134">在中记录的 3.3 的命令行版本中修复的问题列表[3.3 命令行里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)。</span><span class="sxs-lookup"><span data-stu-id="eb37c-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="eb37c-135">已知问题</span><span class="sxs-lookup"><span data-stu-id="eb37c-135">Known Issues</span></span>

<span data-ttu-id="eb37c-136">我们继续来跟踪我们的 GitHub 问题中，可以在中找到的问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="eb37c-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>