---
title: "NuGet 3.4 RC 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.4 RC 的发行说明。"
keywords: "NuGet 3.4 RC 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 749068683d6e2a3fd9dd29c69d9ff50137acdd46
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="72d99-104">NuGet 3.4 RC 发行说明</span><span class="sxs-lookup"><span data-stu-id="72d99-104">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="72d99-105">[NuGet 3.3 发行说明](../release-notes/nuget-3.3.md) | [NuGet 3.4 发行说明](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="72d99-105">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="72d99-106">NuGet 3.4 RC 2016 年 3 月 3 日与 Visual Studio 2015 Update 2 RC 一起发布，并且用几原则思想的生成：</span><span class="sxs-lookup"><span data-stu-id="72d99-106">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="72d99-107">跨平台支持</span><span class="sxs-lookup"><span data-stu-id="72d99-107">Cross-Platform support</span></span>
* <span data-ttu-id="72d99-108">性能改进</span><span class="sxs-lookup"><span data-stu-id="72d99-108">Performance improvements</span></span>
* <span data-ttu-id="72d99-109">小的 UI 改进</span><span class="sxs-lookup"><span data-stu-id="72d99-109">Minor UI improvements</span></span>

<span data-ttu-id="72d99-110">下列功能是此 RC 中提供了更多计划 3.4 的最终版本。</span><span class="sxs-lookup"><span data-stu-id="72d99-110">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="72d99-111">新增功能</span><span class="sxs-lookup"><span data-stu-id="72d99-111">New Features</span></span>

* <span data-ttu-id="72d99-112">NuGet 客户端现在支持 gzip 内容编码从存储库</span><span class="sxs-lookup"><span data-stu-id="72d99-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="72d99-113">对 Pdb 的 xproj 项目中的包的支持</span><span class="sxs-lookup"><span data-stu-id="72d99-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="72d99-114">支持 iOS 和 Android 生成在 contentFiles 元素中的操作</span><span class="sxs-lookup"><span data-stu-id="72d99-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="72d99-115">支持 netstandard 和 netstandardapp 框架名字对象</span><span class="sxs-lookup"><span data-stu-id="72d99-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="72d99-116">新的用户界面功能</span><span class="sxs-lookup"><span data-stu-id="72d99-116">New User Interface Features</span></span>

* <span data-ttu-id="72d99-117">特别是在已安装、 更新和合并选项卡上的显著的性能改进</span><span class="sxs-lookup"><span data-stu-id="72d99-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="72d99-118">安装和更新选项卡现在按字母顺序排序</span><span class="sxs-lookup"><span data-stu-id="72d99-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="72d99-119">添加允许搜索要刷新的刷新按钮</span><span class="sxs-lookup"><span data-stu-id="72d99-119">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="72d99-120">更新和改进</span><span class="sxs-lookup"><span data-stu-id="72d99-120">Updates and Improvements</span></span>

* <span data-ttu-id="72d99-121">包中引用`project.json`具有浮点版本将不在每次生成上更新。</span><span class="sxs-lookup"><span data-stu-id="72d99-121">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="72d99-122">相反，它们将在其中更新仅当强制还原、 清理、 重新生成，或修改`project.json`。</span><span class="sxs-lookup"><span data-stu-id="72d99-122">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="72d99-123">当你使用 NuGet 配置 UI，无法再强制 nuget.org 存储库源到项目配置。</span><span class="sxs-lookup"><span data-stu-id="72d99-123">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="72d99-124">NuGet 无法再还原在共享项目中的包也不写入锁定文件。</span><span class="sxs-lookup"><span data-stu-id="72d99-124">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="72d99-125">我们改进了网络故障，然后重试处理无法访问或到响应速度缓慢的服务器。</span><span class="sxs-lookup"><span data-stu-id="72d99-125">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="72d99-126">在 Visual Studio 包管理器 UI 中改进了键盘和鼠标的行为。</span><span class="sxs-lookup"><span data-stu-id="72d99-126">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="72d99-127">我们现在支持最新`project.json`DNX 中的架构。</span><span class="sxs-lookup"><span data-stu-id="72d99-127">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="72d99-128">已知问题</span><span class="sxs-lookup"><span data-stu-id="72d99-128">Known Issues</span></span>

<span data-ttu-id="72d99-129">我们继续在我们的 GitHub 问题列表，可在上跟踪问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="72d99-129">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>