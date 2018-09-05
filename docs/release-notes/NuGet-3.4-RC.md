---
title: NuGet 3.4 RC 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.4 RC 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546749"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="44560-103">NuGet 3.4 RC 发行说明</span><span class="sxs-lookup"><span data-stu-id="44560-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="44560-104">[NuGet 3.3 发行说明](../release-notes/nuget-3.3.md) | [NuGet 3.4 发行说明](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="44560-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="44560-105">NuGet 3.4 RC 已发布于 2016 年 3 月 3 日与 Visual Studio 2015 Update 2 RC 一起，并且已生成具有几项基本原则在脑海中：</span><span class="sxs-lookup"><span data-stu-id="44560-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="44560-106">跨平台支持</span><span class="sxs-lookup"><span data-stu-id="44560-106">Cross-Platform support</span></span>
* <span data-ttu-id="44560-107">性能改进</span><span class="sxs-lookup"><span data-stu-id="44560-107">Performance improvements</span></span>
* <span data-ttu-id="44560-108">次要 UI 改进</span><span class="sxs-lookup"><span data-stu-id="44560-108">Minor UI improvements</span></span>

<span data-ttu-id="44560-109">以下功能都在此 RC 中，提供了计划 3.4 的最终版本的详细信息。</span><span class="sxs-lookup"><span data-stu-id="44560-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="44560-110">新增功能</span><span class="sxs-lookup"><span data-stu-id="44560-110">New Features</span></span>

* <span data-ttu-id="44560-111">NuGet 客户端现在支持 gzip 内容编码从存储库</span><span class="sxs-lookup"><span data-stu-id="44560-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="44560-112">从 xproj 项目包中支持 Pdb</span><span class="sxs-lookup"><span data-stu-id="44560-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="44560-113">支持 iOS 和 Android 生成 contentFiles 元素中的操作</span><span class="sxs-lookup"><span data-stu-id="44560-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="44560-114">支持 netstandard 和 netstandardapp 框架名字对象</span><span class="sxs-lookup"><span data-stu-id="44560-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="44560-115">新用户界面功能</span><span class="sxs-lookup"><span data-stu-id="44560-115">New User Interface Features</span></span>

* <span data-ttu-id="44560-116">尤其是在已安装、 更新和合并选项卡上的显著的性能改进</span><span class="sxs-lookup"><span data-stu-id="44560-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="44560-117">安装和更新选项卡现在按字母顺序排序</span><span class="sxs-lookup"><span data-stu-id="44560-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="44560-118">添加允许搜索要刷新的刷新按钮</span><span class="sxs-lookup"><span data-stu-id="44560-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="44560-119">更新和改进</span><span class="sxs-lookup"><span data-stu-id="44560-119">Updates and Improvements</span></span>

* <span data-ttu-id="44560-120">中引用的包`project.json`具有浮点版本将不会更新在每次生成。</span><span class="sxs-lookup"><span data-stu-id="44560-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="44560-121">相反，它们将在其中更新仅当强制还原、 清理、 重新生成或修改时`project.json`。</span><span class="sxs-lookup"><span data-stu-id="44560-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="44560-122">使用 NuGet 配置 UI 时，不能再强制 nuget.org 存储库源到项目配置。</span><span class="sxs-lookup"><span data-stu-id="44560-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="44560-123">NuGet 不能再还原在共享项目中的包，也不写入锁定文件。</span><span class="sxs-lookup"><span data-stu-id="44560-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="44560-124">我们改进了网络故障，然后重试处理无法访问或为响应速度缓慢的服务器。</span><span class="sxs-lookup"><span data-stu-id="44560-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="44560-125">键盘和鼠标行为是改进了 Visual Studio 包管理器 UI 中。</span><span class="sxs-lookup"><span data-stu-id="44560-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="44560-126">我们现在支持最新`project.json`DNX 中的架构。</span><span class="sxs-lookup"><span data-stu-id="44560-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="44560-127">已知问题</span><span class="sxs-lookup"><span data-stu-id="44560-127">Known Issues</span></span>

<span data-ttu-id="44560-128">我们继续来跟踪我们的 GitHub 问题中，可以在中找到的问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="44560-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>