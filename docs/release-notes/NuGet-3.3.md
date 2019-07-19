---
title: NuGet 3.3 发行说明
description: NuGet 3.3 的发行说明, 包括已知问题、bug 修复、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 482c03a4f6ca39edf317b6ef8d535e79b53d5d16
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317043"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="47c85-103">NuGet 3.3 发行说明</span><span class="sxs-lookup"><span data-stu-id="47c85-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="47c85-104">[Nuget 3.2.1 发行说明](../release-notes/nuget-3.2.1.md) | [nuget 3.4-RC 发行说明](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="47c85-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="47c85-105">NuGet 3.3 于2015年11月30日发布, 具有大量用户界面更新和命令行功能, 以及对 NuGet 客户端的有用修补程序的集合。</span><span class="sxs-lookup"><span data-stu-id="47c85-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="47c85-106">新增功能</span><span class="sxs-lookup"><span data-stu-id="47c85-106">New Features</span></span>

* <span data-ttu-id="47c85-107">引入了凭据提供程序, 使 NuGet 命令行客户端能够与经过身份验证的源无缝协作。</span><span class="sxs-lookup"><span data-stu-id="47c85-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="47c85-108">NuGet 文档中提供了有关[如何安装 Visual Studio Team Services 凭据提供程序以及如何](../api/nuget-exe-credential-providers.md)配置 nuget 客户端以使用该提供程序的说明。</span><span class="sxs-lookup"><span data-stu-id="47c85-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="47c85-109">新的用户界面功能</span><span class="sxs-lookup"><span data-stu-id="47c85-109">New User Interface Features</span></span>

* <span data-ttu-id="47c85-110">单独的浏览、已安装和更新可用选项卡</span><span class="sxs-lookup"><span data-stu-id="47c85-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="47c85-111">更新可用徽章, 指示包含可用更新的包数</span><span class="sxs-lookup"><span data-stu-id="47c85-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="47c85-112">包列表中的包徽章, 用来指示包是否已安装或是否有可用更新</span><span class="sxs-lookup"><span data-stu-id="47c85-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="47c85-113">添加到包列表的下载计数和作者</span><span class="sxs-lookup"><span data-stu-id="47c85-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="47c85-114">包列表中可用的最高版本号和当前安装的版本号</span><span class="sxs-lookup"><span data-stu-id="47c85-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="47c85-115">允许从包列表快速安装、更新和卸载的操作按钮</span><span class="sxs-lookup"><span data-stu-id="47c85-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="47c85-116">包详细信息面板中更清晰的操作按钮</span><span class="sxs-lookup"><span data-stu-id="47c85-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="47c85-117">包更新日期包详细信息面板</span><span class="sxs-lookup"><span data-stu-id="47c85-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="47c85-118">解决方案视图中的合并面板</span><span class="sxs-lookup"><span data-stu-id="47c85-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="47c85-119">项目的可排序网格和解决方案视图上安装的版本号</span><span class="sxs-lookup"><span data-stu-id="47c85-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="47c85-120">新的命令行功能</span><span class="sxs-lookup"><span data-stu-id="47c85-120">New Command-line Features</span></span>

<span data-ttu-id="47c85-121">在此版本中, 我们`add`引入`init`了和命令, 以初始化基于文件夹的存储库, 如[nuget.exe 引用](../reference/nuget-exe-cli-reference.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="47c85-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="47c85-122">通过此文件夹结构构造和维护的存储库将[提供重要的性能优势](http://blog.nuget.org/20150922/Accelerate-Package-Source.html), 如博客中所述。</span><span class="sxs-lookup"><span data-stu-id="47c85-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="47c85-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="47c85-123">ContentFiles</span></span>

<span data-ttu-id="47c85-124">`project.json`在托管项目中, 通过新`contentFiles`文件夹和`.nuspec` `contentFiles`元素表示法现在支持内容。</span><span class="sxs-lookup"><span data-stu-id="47c85-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="47c85-125">包作者可以更直接指定此内容以与项目系统交互。</span><span class="sxs-lookup"><span data-stu-id="47c85-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="47c85-126">有关如何在`.nuspec`文档中配置 contentFiles 的详细信息, 请参阅[nuspec 引用](../reference/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="47c85-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="47c85-127">NuGet 局部变量缓存管理</span><span class="sxs-lookup"><span data-stu-id="47c85-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="47c85-128">NuGet 命令行已更新, 以包括有关如何管理工作站上的本地缓存的信息。</span><span class="sxs-lookup"><span data-stu-id="47c85-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="47c85-129">[NuGet 命令行参考](../reference/cli-reference/cli-ref-locals.md)中提供了有关局部变量命令的详细信息。</span><span class="sxs-lookup"><span data-stu-id="47c85-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="47c85-130">修复的问题</span><span class="sxs-lookup"><span data-stu-id="47c85-130">Fixed Issues</span></span>

<span data-ttu-id="47c85-131">**值得注意的问题**</span><span class="sxs-lookup"><span data-stu-id="47c85-131">**Notable Issues**</span></span>

* <span data-ttu-id="47c85-132">NuGet 命令行已还原对在 Mono 上使用解决方案文件还原包的支持- [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="47c85-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="47c85-133">3\.3 版本中解决的问题的完整列表可在 GitHub 上的[3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)下找到。</span><span class="sxs-lookup"><span data-stu-id="47c85-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="47c85-134">3\.3 命令行版本中修复的问题列表记录在[3.3 命令行里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)中。</span><span class="sxs-lookup"><span data-stu-id="47c85-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="47c85-135">已知问题</span><span class="sxs-lookup"><span data-stu-id="47c85-135">Known Issues</span></span>

<span data-ttu-id="47c85-136">我们继续跟踪 GitHub 问题列表中的问题, 可在以下位置找到:[http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="47c85-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>