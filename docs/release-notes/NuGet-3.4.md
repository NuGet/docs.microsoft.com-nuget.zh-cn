---
title: NuGet 3.4 发行说明
description: NuGet 3.4 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776411"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="260cd-103">NuGet 3.4 发行说明</span><span class="sxs-lookup"><span data-stu-id="260cd-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="260cd-104">[NuGet 3.4-RC 发行说明](../release-notes/nuget-3.4-RC.md)  | [NuGet 3.4.1 发行说明](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="260cd-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="260cd-105">在 Visual Studio 2015 更新2和 Visual Studio 15 预览版中，NuGet 3.4 发布了3月 30 2016 日，并使用了一些思想原则构建：</span><span class="sxs-lookup"><span data-stu-id="260cd-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="260cd-106">跨平台支持</span><span class="sxs-lookup"><span data-stu-id="260cd-106">Cross-Platform support</span></span>
* <span data-ttu-id="260cd-107">性能改进</span><span class="sxs-lookup"><span data-stu-id="260cd-107">Performance improvements</span></span>
* <span data-ttu-id="260cd-108">细微的 UI 改进</span><span class="sxs-lookup"><span data-stu-id="260cd-108">Minor UI improvements</span></span>

<span data-ttu-id="260cd-109">以下功能以前已添加到 RC 中，并已在3.4 版本中更新或完成：</span><span class="sxs-lookup"><span data-stu-id="260cd-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="260cd-110">新功能</span><span class="sxs-lookup"><span data-stu-id="260cd-110">New Features</span></span>

* <span data-ttu-id="260cd-111">NuGet 客户端现在支持存储库中的 gzip 内容编码</span><span class="sxs-lookup"><span data-stu-id="260cd-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="260cd-112">Xproj 项目中的包支持 Pdb</span><span class="sxs-lookup"><span data-stu-id="260cd-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="260cd-113">在 contentFiles 元素中支持 iOS 和 Android 生成操作</span><span class="sxs-lookup"><span data-stu-id="260cd-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="260cd-114">支持 netstandard 和 netstandardapp framework 名字对象</span><span class="sxs-lookup"><span data-stu-id="260cd-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="260cd-115">新的用户界面功能</span><span class="sxs-lookup"><span data-stu-id="260cd-115">New User Interface Features</span></span>

* <span data-ttu-id="260cd-116">显著提高性能，尤其是在已安装、更新和合并选项卡上</span><span class="sxs-lookup"><span data-stu-id="260cd-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="260cd-117">聚合 "所有包源" 源可用于正确的搜索结果合并</span><span class="sxs-lookup"><span data-stu-id="260cd-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="260cd-118">"已安装" 和 "更新" 选项卡现在按字母顺序排序</span><span class="sxs-lookup"><span data-stu-id="260cd-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="260cd-119">添加了允许刷新搜索的刷新按钮</span><span class="sxs-lookup"><span data-stu-id="260cd-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="260cd-120">版本列表顶部的最新生成选项</span><span class="sxs-lookup"><span data-stu-id="260cd-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="260cd-121">更新和改进</span><span class="sxs-lookup"><span data-stu-id="260cd-121">Updates and Improvements</span></span>

* <span data-ttu-id="260cd-122">在中引用 `project.json` 的包含浮动版本的包在每次生成时都不会更新。</span><span class="sxs-lookup"><span data-stu-id="260cd-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="260cd-123">相反，它们仅在强制还原、清理、重新生成或修改时才进行更新 `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="260cd-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="260cd-124">使用 NuGet 配置 UI 时，不再将 nuget.org 存储库源强制转换为项目配置。</span><span class="sxs-lookup"><span data-stu-id="260cd-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="260cd-125">NuGet 不再还原共享项目中的包，也不写入锁定文件。</span><span class="sxs-lookup"><span data-stu-id="260cd-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="260cd-126">我们已改进网络故障并重试处理，使其无法访问或响应缓慢服务器。</span><span class="sxs-lookup"><span data-stu-id="260cd-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="260cd-127">在 Visual Studio 包管理器 UI 中，键盘和鼠标的行为得到了改善。</span><span class="sxs-lookup"><span data-stu-id="260cd-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="260cd-128">现在，我们支持 DNX 中的最新 `project.json` 架构。</span><span class="sxs-lookup"><span data-stu-id="260cd-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="260cd-129">重大更改</span><span class="sxs-lookup"><span data-stu-id="260cd-129">Breaking Changes</span></span>

* <span data-ttu-id="260cd-130">包的版本号现在规范化为格式的 *主要* 版本号。*次要*。*修补程序* -*预发行*  每个主要、次要和修补程序都被视为整数并删除任何前导零。</span><span class="sxs-lookup"><span data-stu-id="260cd-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="260cd-131">预发布信息被视为字符串，不会应用任何更改。</span><span class="sxs-lookup"><span data-stu-id="260cd-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="260cd-132">NuGet 客户端和 nuget.org 服务提供的搜索将在查询中使用这些数字。</span><span class="sxs-lookup"><span data-stu-id="260cd-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="260cd-133">有关更多详细信息，请参阅 [预发行版本](../create-packages/prerelease-packages.md)下的 NuGet 文档。</span><span class="sxs-lookup"><span data-stu-id="260cd-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="260cd-134">已知问题</span><span class="sxs-lookup"><span data-stu-id="260cd-134">Known Issues</span></span>

* <span data-ttu-id="260cd-135">**问题：** 在以下情况下，Windows 10 v1511 用户可能会遇到问题，甚至在 Visual Studio 中使用 Powershell 时出现 Visual Studio 崩溃：</span><span class="sxs-lookup"><span data-stu-id="260cd-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="260cd-136">安装/卸载具有 install.ps1/uninstall.ps1 脚本的包</span><span class="sxs-lookup"><span data-stu-id="260cd-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="260cd-137">加载具有 init.ps1 脚本的项目 (例如 EntityFramework) </span><span class="sxs-lookup"><span data-stu-id="260cd-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="260cd-138">发布 web 内容</span><span class="sxs-lookup"><span data-stu-id="260cd-138">Publishing web content</span></span>

* <span data-ttu-id="260cd-139">**解决方法：** 确保 Windows 10 安装已应用最新修补程序，专用 2016 (KB 3124263) 或更高版本的更新。</span><span class="sxs-lookup"><span data-stu-id="260cd-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="260cd-140">有关更多详细信息，请访问 [GitHub 问题 #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="260cd-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="260cd-141">**问题：** NuGet v2 协议重定向已断开。</span><span class="sxs-lookup"><span data-stu-id="260cd-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="260cd-142">将请求重定向到备用主机的自定义 NuGet 存储库不接受重定向请求。</span><span class="sxs-lookup"><span data-stu-id="260cd-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="260cd-143">**解决方法：**  若要解决此问题，请在 "设置" 中将包存储库 URI 配置为指向重定向的服务器位置。</span><span class="sxs-lookup"><span data-stu-id="260cd-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="260cd-144">有关详细信息，请参阅 [GitHub 拉取请求 #387](https://github.com/NuGet/NuGet.Client/pull/387)。</span><span class="sxs-lookup"><span data-stu-id="260cd-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="260cd-145">我们继续跟踪 GitHub 问题列表中的问题，可在以下位置找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="260cd-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>