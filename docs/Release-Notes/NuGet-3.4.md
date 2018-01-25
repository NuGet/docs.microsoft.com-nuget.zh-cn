---
title: "NuGet 3.4 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.4 的发行说明。"
keywords: "NuGet 3.4 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 515fb888aca2a8eb138c8fea1fb5b3f5a8f4e275
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="dc400-104">NuGet 3.4 发行说明</span><span class="sxs-lookup"><span data-stu-id="dc400-104">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="dc400-105">[NuGet 3.4 RC 发行说明](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 发行说明](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="dc400-105">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="dc400-106">NuGet 3.4 2016 年 3 月 30 日发布为 Visual Studio 2015 Update 2 和 Visual Studio 15 预览版的一部分，并且已生成与几项基本原则思想中：</span><span class="sxs-lookup"><span data-stu-id="dc400-106">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

*  <span data-ttu-id="dc400-107">跨平台支持</span><span class="sxs-lookup"><span data-stu-id="dc400-107">Cross-Platform support</span></span>
*  <span data-ttu-id="dc400-108">性能改进</span><span class="sxs-lookup"><span data-stu-id="dc400-108">Performance improvements</span></span>
*  <span data-ttu-id="dc400-109">小的 UI 改进</span><span class="sxs-lookup"><span data-stu-id="dc400-109">Minor UI improvements</span></span>

<span data-ttu-id="dc400-110">以下功能之前添加 RC 中和已更新或完成 3.4 版本：</span><span class="sxs-lookup"><span data-stu-id="dc400-110">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="dc400-111">新增功能</span><span class="sxs-lookup"><span data-stu-id="dc400-111">New Features</span></span>

* <span data-ttu-id="dc400-112">NuGet 客户端现在支持 gzip 内容编码从存储库</span><span class="sxs-lookup"><span data-stu-id="dc400-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="dc400-113">对 Pdb 的 xproj 项目中的包的支持</span><span class="sxs-lookup"><span data-stu-id="dc400-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="dc400-114">支持 iOS 和 Android 生成在 contentFiles 元素中的操作</span><span class="sxs-lookup"><span data-stu-id="dc400-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="dc400-115">支持 netstandard 和 netstandardapp 框架名字对象</span><span class="sxs-lookup"><span data-stu-id="dc400-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="dc400-116">新的用户界面功能</span><span class="sxs-lookup"><span data-stu-id="dc400-116">New User Interface Features</span></span>

* <span data-ttu-id="dc400-117">特别是在已安装、 更新和合并选项卡上的显著的性能改进</span><span class="sxs-lookup"><span data-stu-id="dc400-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="dc400-118">聚合的所有包源源可用与正确的搜索结果合并</span><span class="sxs-lookup"><span data-stu-id="dc400-118">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="dc400-119">安装和更新选项卡现在按字母顺序排序</span><span class="sxs-lookup"><span data-stu-id="dc400-119">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="dc400-120">添加允许搜索要刷新的刷新按钮</span><span class="sxs-lookup"><span data-stu-id="dc400-120">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="dc400-121">在版本列表顶部的最新生成选项</span><span class="sxs-lookup"><span data-stu-id="dc400-121">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="dc400-122">更新和改进</span><span class="sxs-lookup"><span data-stu-id="dc400-122">Updates and Improvements</span></span>

* <span data-ttu-id="dc400-123">包中引用`project.json`具有浮点版本将不在每次生成上更新。</span><span class="sxs-lookup"><span data-stu-id="dc400-123">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="dc400-124">相反，它们将在其中更新仅当强制还原、 清理、 重新生成，或修改`project.json`。</span><span class="sxs-lookup"><span data-stu-id="dc400-124">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="dc400-125">当你使用 NuGet 配置 UI，无法再强制 nuget.org 存储库源到项目配置。</span><span class="sxs-lookup"><span data-stu-id="dc400-125">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="dc400-126">NuGet 无法再还原在共享项目中的包也不写入锁定文件。</span><span class="sxs-lookup"><span data-stu-id="dc400-126">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="dc400-127">我们改进了网络故障，然后重试处理无法访问或到响应速度缓慢的服务器。</span><span class="sxs-lookup"><span data-stu-id="dc400-127">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="dc400-128">在 Visual Studio 包管理器 UI 中改进了键盘和鼠标的行为。</span><span class="sxs-lookup"><span data-stu-id="dc400-128">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="dc400-129">我们现在支持最新`project.json`DNX 中的架构。</span><span class="sxs-lookup"><span data-stu-id="dc400-129">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="dc400-130">重大更改</span><span class="sxs-lookup"><span data-stu-id="dc400-130">Breaking Changes</span></span>

* <span data-ttu-id="dc400-131">包版本号现在规范化为格式*主要*。*次要*。*修补程序*-*预发布*每个主版本号、 次版本、 和修补程序被视为整数并删除任何前导零。</span><span class="sxs-lookup"><span data-stu-id="dc400-131">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="dc400-132">预发布信息视为一个字符串，并向其应用任何更改。</span><span class="sxs-lookup"><span data-stu-id="dc400-132">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="dc400-133">将这些数用在查询中通过 NuGet 客户端和 nuget.org 服务提供的搜索。</span><span class="sxs-lookup"><span data-stu-id="dc400-133">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="dc400-134">在 NuGet 文档中找不到更多详细信息[预发行版本](../create-packages/prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="dc400-134">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="dc400-135">已知问题</span><span class="sxs-lookup"><span data-stu-id="dc400-135">Known Issues</span></span>

* <span data-ttu-id="dc400-136">**问题：** Windows 10 v1511 用户可能会遇到问题或甚至在 Visual Studio 系统崩溃时 Visual Studio 中的 Powershell 在以下方案：</span><span class="sxs-lookup"><span data-stu-id="dc400-136">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="dc400-137">安装 / 卸载具有 install.ps1 的包 / uninstall.ps1 脚本</span><span class="sxs-lookup"><span data-stu-id="dc400-137">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="dc400-138">加载具有 （如 EntityFramework) 的 init.ps1 脚本的项目</span><span class="sxs-lookup"><span data-stu-id="dc400-138">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="dc400-139">发布的 web 内容</span><span class="sxs-lookup"><span data-stu-id="dc400-139">Publishing web content</span></span>

* <span data-ttu-id="dc400-140">**解决方法：**确保 Windows 10 安装已应用最新修补程序、 expecially 2016 年 1 月 (KB 3124263) 或更高版本的更新。</span><span class="sxs-lookup"><span data-stu-id="dc400-140">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="dc400-141">更多详细信息位于[GitHub 问题 # 1638年](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="dc400-141">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="dc400-142">**问题：** NuGet v2 协议重定向已断开。</span><span class="sxs-lookup"><span data-stu-id="dc400-142">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="dc400-143">将请求重定向到备用主机的自定义 NuGet 存储库不接受重定向请求。</span><span class="sxs-lookup"><span data-stu-id="dc400-143">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="dc400-144">**解决方法：**若要解决此问题，将程序包存储库 URI 在设置配置为指向重定向的服务器的位置。</span><span class="sxs-lookup"><span data-stu-id="dc400-144">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="dc400-145">有关详细信息，请参阅[GitHub 拉取请求 #387](https://github.com/NuGet/NuGet.Client/pull/387)。</span><span class="sxs-lookup"><span data-stu-id="dc400-145">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="dc400-146">我们继续在我们的 GitHub 问题列表，可在上跟踪问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="dc400-146">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>